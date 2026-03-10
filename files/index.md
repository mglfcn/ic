---
layout: default
title: Archivos
permalink: /files/
---

<style>

.wrapper{
max-width:1200px !important;
}

.file-table{
width:100%;
border-collapse:collapse;
font-family:system-ui;
}

.file-table th{
text-align:left;
border-bottom:2px solid #ddd;
padding:8px;
}

.file-table td{
padding:8px;
border-bottom:1px solid #eee;
}

.file-name{
display:flex;
align-items:center;
gap:8px;
}

.file-size{
text-align:right;
color:#666;
width:120px;
}

.file-download{
text-align:center;
width:80px;
}

</style>

# 📦 Archivos disponibles

<table class="file-table">

<tr>
<th>Nombre</th>
<th class="file-size">Tamaño</th>
<th class="file-download">Descargar</th>
</tr>

{% assign current_dir = page.dir %}

{% for file in site.static_files %}
{% if file.path contains current_dir %}
{% unless file.name == "index.md" %}

{% assign ext = file.extname | downcase %}

<tr>

<td class="file-name">

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

<td class="file-size">

{% if file.size %}
{% assign kb = file.size | divided_by: 1024 %}

{% if kb > 1024 %}
{{ kb | divided_by: 1024 }} MB
{% else %}
{{ kb }} KB
{% endif %}

{% else %}
-
{% endif %}

</td>

<td class="file-download">
<a href="{{ file.path | relative_url }}" download>⬇️</a>
</td>

</tr>

{% endunless %}
{% endif %}
{% endfor %}

</table>
