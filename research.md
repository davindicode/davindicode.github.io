---
layout: blog
title: Research
permalink: /research/
---

<div id="All" class="w3-container category w3-animate-left">
  <div id="#{{ category_name | slugize }}"></div>
  {%- for post in site.works -%}
    <div class="column">
      <div class="thumbnail">
        <a href="{{ site.baseurl }}{{ post.url }}">
          <img src="{{ site.baseurl }}/images/thumbnail/{{ post.thumbnail }}" class="center">
        </a>
        <h4 style="margin-top:0px; margin-bottom:0px; text-align:center; font-size:80%;">{{ post.title }}</h4>
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
        <div class="thumbnail">
          <a href="{{ site.baseurl }}{{ post.url }}">
            <img src="{{ site.baseurl }}/images/thumbnail/research/{{ post.thumbnail }}" class="center">
          </a>
          <h4 style="margin-top:0px; margin-bottom:0px; text-align:center; font-size:80%;">{{ post.title }}</h4>
        </div>
      </div>
    {%- endfor -%}
  </div>
{%- endfor -%}