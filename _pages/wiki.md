---
layout: default
title: "Wiki"
permalink: /wiki/
author_profile: true
---

<div id="main" role="main">
  {% include sidebar.html %}

  <div class="archive">
    {% unless page.header.overlay_color or page.header.overlay_image %}
      <h1 id="page-title" class="page__title">{{ page.title }}</h1>
    {% endunless %}
    
    {% assign groups = site.wiki | group_by: "category" | sort: "name" %}
    {% for group in groups %}
        <h3>{{ group.name | remove: '["' | remove: '"]' }}</h3>
        {% for item in group.items %}
            <a href="{{ item.url }}">{{ item.title }}</a>,&nbsp;
        {% endfor %}
    {% endfor %}
   </div>
</div>
