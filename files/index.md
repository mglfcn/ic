---
layout: default
title: Descargas
permalink: /files/
---

<style>
.wrapper {
  max-width: 1200px !important;
}

.page-content {
  max-width: 1200px !important;
}

.file-list {
  list-style: none;
  padding: 0;
}

.file-item {
  display: flex;
  align-items: center;
  padding: 10px;
  border-bottom: 1px solid #ddd;
}

.file-icon {
  width: 32px;
  text-align: center;
  margin-right: 12px;
  font-size: 20px;
}

.file-name {
  flex: 1;
}

.file-meta {
  color: #666;
  min-width: 80px;
  text-align: right;
}
</style>

# 📦 Archivos disponibles

<ul class="file-list">

{% raw %}
{% assign current_dir = page.dir %}

{% for file in site.static_files %}
  {% if file.path contains current_dir %}
  {% unless file.name == "index.md" %}

  {% assign ext = file.extname | downcase %}

  <li class="file-item">

    <span class="file-icon">
      {% case ext %}
        {% when '.zip' %}📦
        {% when '.pdf' %}📄
        {% when '.png' %}🖼️
        {% when '.jpg' %}🖼️
        {% when '.jpeg' %}🖼️
        {% when '.gif' %}🖼️
        {% when '.mp4' %}🎬
        {% when '.mp3' %}🎵
        {% when '.txt' %}📄
        {% when '.exe' %}⚙️
        {% else %}📁
      {% endcase %}
    </span>

    <span class="file-name">
      <a href="{{ file.path | relative_url }}" download>
        {{ file.name }}
      </a>
    </span>

    <span class="file-meta">
      {{ file.size | divided_by: 1024 }} KB
    </span>

  </li>

  {% endunless %}
  {% endif %}
{% endfor %}
{% endraw %}

</ul>
