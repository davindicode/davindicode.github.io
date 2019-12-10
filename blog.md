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
      <a href="{{ site.baseurl }}{{ post.url }}">{{post.title}}</a>
      <img border="0" alt="W3Schools" src="{{ site.baseurl }}/images/gyro.jpg" width="100" height="100">
    </article>
    {% endfor %}
  </div>
{% endfor %}
</div>
