---
layout: blog
title: Blog
permalink: /blog/
---

<div id="archives">
{%- for category in site.categories -%}
  <div class="archive-group">
    {% capture category_name %}{{ category | first }}{% endcapture %}
    <div id="#{{ category_name | slugize }}"></div>
    <p></p>
    <h3 class="category-head">{{ category_name }}</h3>
    {%- for post in site.categories[category_name] -%}
    <div class="row">
      <div class="column">
        <article class="archive-item">
          <div class="post">
            <h3 style="margin-top:4px; text-align:center; font-size:95%;">{{ post.title }}</h3>
            <a href="{{ site.baseurl }}{{ post.url }}">
              <img style="width:100%; height:100%;" src="{{ site.baseurl }}/images/thumbnail/{{ post.thumbnail }}">
            </a>
          </div>
        </article>
      </div>
    <div>
    {%- endfor -%}                                                                                                         
  </div>
{%- endfor -%}
</div>
