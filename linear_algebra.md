---
layout: default
title: Linear Algebra
permalink : /algebra/
---

<h1> {{ page.title }} </h1>
<img class="note-cover" src="/assets/images/linear_algebra/algebra-cover.png"/>

{% for note in site.linear_algebra %}
<h3>
  <a href="{{ note.url }}">
    {{ note.title }}
  </a>
</h3>
<p class="capitalize">
  {% assign excerpt = note.content | split: site.excerpt_separator %}
  {{ excerpt[1] | truncatewords: 25 }}
</p>

{% endfor %}