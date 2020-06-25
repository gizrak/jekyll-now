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

    {% for item in site.wiki %}
	  <a href="{{ item.url }}">{{ item.title }}</a>,&nbsp;
	{% endfor %}
   </div>
</div>
