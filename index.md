---
layout: page
title: 我叫拳四郎
tagline: Supporting tagline
---
{% include JB/setup %}
<div>Fuck ni</div> 
<ul class="posts">
  {% for post in site.posts %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>


