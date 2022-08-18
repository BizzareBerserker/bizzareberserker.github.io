---
layout: page
title: Menu
permalink: /menu/
---

<div>

  {% for tag in site.tags %}
    <h2 class="post-list-heading">{{ tag[0] }}</h2>
    <ul>
        {% for post in tag[1] %} 
            <li> <a href="{{ post.url }}">{{ post.title }}</a> </li> 
        {% endfor %}
    </ul>
  {% endfor %}

</div>