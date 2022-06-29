---
layout: default
title: Statistics
permalink : /statistics/
---

<h1> {{ page.title }} </h1>

*These notes closely follow [Introduction to Probability and Statistics for Engineers and Scientists](https://www.amazon.com/dp/0128243465) by Sheldon Ross; [All of Statistics](https://www.amazon.com/dp/1441923225) by Larry Wasserman and [Statistical Regression](https://www.khanacademy.org/math/statistics-probability/advanced-regression-inference-transforming) from Khan Academy.*

<img class="note-cover" src="/assets/images/statistics/cover.png"/>

{% assign statistics = site.statistics | sort: "item_num" %}
{% for note in statistics %}
<h3>
  <a href="{{ note.url }}">
    {{ note.title }}
  </a>
</h3>

<p>
  {{ note.excerpt }}
</p>

{% endfor %}