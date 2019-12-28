---
layout: page
title: Blog
permalink: /blog/
---

<head>
  <style>
    img {
      border: 1px solid #ddd;
      border-radius: 4px;
      padding: 5px;
      width: 150px;
    }
    img:hover {
      box-shadow: 0 0 2px 1px rgba(0, 140, 186, 0.5);
    }
    .column {
      float: left;
      width: 33.33%;
      padding: 5px;
    }
    .row::after {
      content: "";
      clear: both;
      display: table;
    }
  </style>
</head>


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
        <div class="row">
          <div class="column">
            <div class="post">
              <h3 style="margin-top:4px; horizontal-align: middle; font-size:95%;">{{ post.title }}</h3>
              <img style="width:95%; height:95%;" src="{{ site.baseurl }}/images/thumbnail/{{ post.thumbnail }}">
            </div>
          </div>
        </div>
      </a>
    </article>
    {% endfor %}
  </div>
{% endfor %}
</div>
