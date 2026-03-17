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
width:180px;
}

</style>

# 📦 Archivos

<input id="search" placeholder="Buscar archivo...">

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
if(ext==="png"||ext==="jpg"||ext==="jpeg"||ext==="gif") return "🖼️"
if(ext==="mp3") return "🎵"
if(ext==="mp4") return "🎬"

return "📄"
}

async function loadFolder(path=""){

currentPath=path

let api=`https://api.github.com/repos/${owner}/${repo}/contents/${basePath}/${path}`

let res=await fetch(api)
let data=await res.json()

let tbody=document.querySelector("#fileTable tbody")
tbody.innerHTML=""

if(path){

let up=path.split("/").slice(0,-1).join("/")

let tr=document.createElement("tr")

tr.innerHTML=`
<td class="name">⬅ <a href="#" onclick="loadFolder('${up}');return false;">..</a></td>
<td></td>
`

tbody.appendChild(tr)

}

data.sort((a,b)=>{

if(a.type===b.type) return a.name.localeCompare(b.name)

return a.type==="dir"?-1:1

})

for(let item of data){

if(item.name === "index.md") continue;

let tr=document.createElement("tr")

let name=icon(item.name,item.type)+" "

if(item.type==="dir"){

tr.innerHTML=`
<td class="name">${name}<a href="#" onclick="loadFolder('${path?path+'/':''}${item.name}');return false;">${item.name}</a></td>
<td></td>
`

}else{

tr.innerHTML=`
<td class="name">${name}<a href="${item.download_url}">${item.name}</a></td>
<td class="date">...</td>
`

loadDate(item.path,tr)

}

tbody.appendChild(tr)

}

}

async function loadDate(path,row){

let url=`https://api.github.com/repos/${owner}/${repo}/commits?path=${path}&per_page=1`

try{

let r=await fetch(url)
let d=await r.json()

let date=new Date(d[0].commit.committer.date)

row.querySelector(".date").innerText=
date.toISOString().split("T")[0]

}catch(e){

row.querySelector(".date").innerText="-"

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
