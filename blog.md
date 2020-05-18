---
layout: blog
title: Blog
permalink: /blog/
---

<div id="All" class="w3-container category w3-animate-left">
  <div id="#{{ category_name | slugize }}"></div>
  {%- for post in site.posts -%}
    <div class="column">
      <div class="thumbnail" style="border: 1px solid black">
        <a href="{{ site.baseurl }}{{ post.url }}">
          <img style="width:95%; height:95%" src="{{ site.baseurl }}/images/thumbnail/{{ post.thumbnail }}" class="center">
        </a>
        <h3 style="margin-top:1px; margin-bottom:1px; text-align:center; font-size:95%;">{{ post.title }}</h3>
        <p style="margin-top:1px; font-size:12px;">{{ post.title }}</p>
      </div>
    </div>
  {%- endfor -%}
</div>

{%- for category in site.categories -%}
{% capture category_name %}{{ category | first }}{% endcapture %}
  <div id="{{ category_name }}" class="w3-container category w3-animate-left" style="display:none">
    <div id="#{{ category_name | slugize }}"></div>
    {%- for post in site.categories[category_name] -%}
      <div class="column">
        <div class="thumbnail" style="border: 1px solid black">
          <a href="{{ site.baseurl }}{{ post.url }}">
            <img style="width:95%; height:95%" src="{{ site.baseurl }}/images/thumbnail/{{ post.thumbnail }}" class="center">
          </a>
          <h3 style="margin-top:1px; margin-bottom:1px; text-align:center; font-size:95%;">{{ post.title }}</h3>
          <p style="margin-top:1px; font-size:12px;">{{ post.title }}</p>
        </div>
      </div>
    {%- endfor -%}
  </div>
{%- endfor -%}