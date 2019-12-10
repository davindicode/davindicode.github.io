---
layout: page
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
    <a name="{{ category_name | slugize }}"></a>
    {% for post in site.categories[category_name] %}
    <article class="archive-item">
      <a href="{{ site.baseurl }}{{ post.url }}">
        <div class="post">
          <h3 style="margin-top:4px; font-size:95%;">{{ post.title }}</h3>
          <img style="width:90%; height:90%; margin-left:5%; margin-top:5%; margin-bottom:5%;" src="{{ site.baseurl }}/images/gyro.jpg">
        </div>
      </a>
    </article>
    {% endfor %}
  </div>
{% endfor %}
</div>
