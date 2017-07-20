---
layout: default
permalink: /tutoriales/
title: turoriales
---

<div class="home">
  <ul class="post-list">
    {% for tutorial in site.tutoriales %}
      <li>
        <span class="post-meta">{{ tutorial.date | date: "%b %-d, %Y" }}</span>

        <h2>
          <a class="post-link" href="{{ tutorial.url }}">{{ tutorial.title | escape }}</a>
        </h2>
        <p class="description">{% if tutorial.description %}{{ tutorial.description | strip_html | strip_newlines | truncate: 250 }}{% else %}{{ tutorial.content | strip_html | strip_newlines | truncate: 250 }}{% endif %}</p>
        <a href="{{ tutorial.url }}">Read more</a>
      </li>
    {% endfor %}
  </ul>

</div>

