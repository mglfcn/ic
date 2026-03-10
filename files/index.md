---
layout: default
title: Archivos
permalink: /files/
---

<style>

.wrapper{max-width:1200px!important}

#search{
width:100%;
padding:8px;
margin-bottom:12px;
font-size:16px;
}

table{
width:100%;
border-collapse:collapse;
font-family:system-ui;
}

th{
text-align:left;
border-bottom:2px solid #ddd;
cursor:pointer;
padding:8px;
}

td{
padding:8px;
border-bottom:1px solid #eee;
}

.size{
text-align:right;
color:#666;
width:120px;
}

.download{
text-align:center;
width:80px;
}

.name{
display:flex;
align-items:center;
gap:8px;
}

</style>

# 📦 Archivos

<input id="search" placeholder="Buscar archivo...">

<table id="fileTable">

<thead>
<tr>
<th onclick="sortTable(0)">Nombre</th>
<th onclick="sortTable(1)">Tamaño</th>
<th>Descargar</th>
</tr>
</thead>

<tbody>

{% assign current_dir = page.dir %}

{% for file in site.static_files %}
{% if file.path contains current_dir %}
{% unless file.name == "index.md" %}

{% assign ext = file.extname | downcase %}

<tr>

<td class="name">

{% case ext %}
{% when '.zip' %}📦
{% when '.pdf' %}📄
{% when '.png' %}🖼️
{% when '.jpg' %}🖼️
{% when '.jpeg' %}🖼️
{% when '.gif' %}🖼️
{% when '.mp3' %}🎵
{% when '.mp4' %}🎬
{% when '.exe' %}⚙️
{% else %}📁
{% endcase %}

<a href="{{ file.path | relative_url }}">
{{ file.name }}
</a>

</td>

<!-- <td class="size">

{% if file.size %}
{% assign kb=file.size | divided_by:1024 %}

{% if kb > 1024 %}
{{ kb | divided_by:1024 }} MB
{% else %}
{{ kb }} KB
{% endif %}

{% endif %}

</td> -->

<td class="download">
<a href="{{ file.path | relative_url }}" download>⬇️</a>
</td>

</tr>

{% endunless %}
{% endif %}
{% endfor %}

</tbody>
</table>

<script>

const search=document.getElementById("search")

search.addEventListener("keyup",function(){

let filter=search.value.toLowerCase()
let rows=document.querySelectorAll("#fileTable tbody tr")

rows.forEach(row=>{
let text=row.innerText.toLowerCase()
row.style.display=text.includes(filter)?"":"none"
})

})

function sortTable(n){

let table=document.getElementById("fileTable")
let rows=Array.from(table.rows).slice(1)
let asc=table.classList.toggle("asc")

rows.sort((a,b)=>{
let A=a.cells[n].innerText
let B=b.cells[n].innerText
return asc?A.localeCompare(B):B.localeCompare(A)
})

rows.forEach(r=>table.appendChild(r))

}

</script>
