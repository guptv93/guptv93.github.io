---
layout: default
title: Probability
permalink : /probability/
---

<h1> {{ page.title }} </h1>
<img class="note-cover" src="/assets/images/probability/probability_cover.jpeg"/>

{% for note in site.probability %}
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