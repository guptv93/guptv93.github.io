---
layout: default
title: Probability
permalink : /probability/
---

<h1> {{ page.title }} </h1>
<img class="note-cover" src="/assets/images/probability/probability_cover.jpeg"/>
{% assign probability = site.probability | sort: "item_num" %}
{% for note in probability %}
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