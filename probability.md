---
layout: default
title: Probability
permalink : /probability/
---

<h1> {{ page.title }} </h1>

*These notes closely follow Introduction to Probability, [book](https://www.amazon.com/dp/188652923X/) and [video lectures](https://ocw.mit.edu/resources/res-6-012-introduction-to-probability-spring-2018/index.htm), by Dimitri P. Bertsekas and John N. Tsitsiklis.*

<img class="note-cover" src="/assets/images/probability/probability_cover.jpeg"/>

{% assign probability = site.probability | sort: "item_num" %}
{% for note in probability %}
<h3>
  <a href="{{ note.url }}">
    {{ note.title }}
  </a>
</h3>

<p>
  {{ note.excerpt }}
</p>

{% endfor %}