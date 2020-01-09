---
layout: blog
title: Blog
permalink: /blog/
---

<div id="archives">
{% for category in site.categories %}
  <div class="archive-group">
    {% capture category_name %}{{ category | first }}{% endcapture %}
    <div id="#{{ category_name | slugize }}"></div>
    <p></p>
    <h3 class="category-head">{{ category_name }}</h3>
    {% for post in site.categories[category_name] %}
    {% if forloop.counter0 == 0 or forloop.counter0 == 3 %}
    <div class="row">
    {% endif %}
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
    {% if forloop.counter0 == 0 or forloop.counter0 == 3 %}
    <div>
    {% endif %}
    {% endfor %}                                                                                                         
  </div>
{% endfor %}
</div>
