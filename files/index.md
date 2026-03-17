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
padding:8px;
}

td{
padding:8px;
border-bottom:1px solid #eee;
}

.name{
display:flex;
align-items:center;
gap:8px;
}

.date{
color:#666;
width:160px;
}
</style>

# 📦 Archivos

<input id="search" placeholder="Buscar...">

<table id="fileTable">
<thead>
<tr>
<th>Nombre</th>
<th>Fecha</th>
</tr>
</thead>
<tbody></tbody>
</table>

<script>

const owner="mglfcn"
const repo="ic"
const basePath="files"

let currentPath=""

function icon(name,type){
if(type==="dir") return "📁"
let ext=name.split(".").pop().toLowerCase()
if(ext==="zip") return "📦"
if(ext==="pdf") return "📄"
if(ext.match(/png|jpg|jpeg|gif/)) return "🖼️"
if(ext==="mp3") return "🎵"
if(ext==="mp4") return "🎬"
return "📄"
}

function formatDate(d){
let date=new Date(d)
return date.toISOString().split("T")[0]
}

async function loadFolder(path=""){

currentPath=path

let api=`https://api.github.com/repos/${owner}/${repo}/contents/${basePath}${path?"/"+path:""}`

let res=await fetch(api)

if(!res.ok){
document.querySelector("#fileTable tbody").innerHTML =
"<tr><td colspan='2'>⚠️ Límite API o error</td></tr>"
return
}

let data=await res.json()

let tbody=document.querySelector("#fileTable tbody")
tbody.innerHTML=""

if(path){
let up=path.split("/").slice(0,-1).join("/")
tbody.innerHTML+=`
<tr>
<td class="name">⬅ <a href="#" onclick="loadFolder('${up}');return false;">..</a></td>
<td></td>
</tr>`
}

data = data.filter(item =>
item.name !== "index.md" &&
!item.name.startsWith(".")
)

data.sort((a,b)=>{
if(a.type===b.type) return a.name.localeCompare(b.name)
return a.type==="dir"?-1:1
})

for(let item of data){

let date = item.type==="file" ? formatDate(item.git_url ? new Date() : new Date()) : ""

let row = document.createElement("tr")

if(item.type==="dir"){

row.innerHTML=`
<td class="name">
📁 <a href="#" onclick="loadFolder('${path?path+'/':''}${item.name}');return false;">
${item.name}
</a>
</td>
<td></td>
`

}else{

row.innerHTML=`
<td class="name">
${icon(item.name,"file")}
<a href="${item.download_url}">${item.name}</a>
</td>
<td class="date">${formatDate(new Date())}</td>
`

}

tbody.appendChild(row)

}

}

document.getElementById("search").addEventListener("keyup",function(){

let f=this.value.toLowerCase()

document.querySelectorAll("#fileTable tbody tr").forEach(r=>{
r.style.display=r.innerText.toLowerCase().includes(f)?"":"none"
})

})

loadFolder()

</script>
