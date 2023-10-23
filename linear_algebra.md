---
layout: default
title: Linear Algebra
permalink : /linear_algebra/
---

<h1> {{ page.title }} </h1>

*These notes have been derived from (i) [Essence of Linear Algebra](https://www.youtube.com/playlist?list=PLZHQObOWTQDPD3MizzM2xVFitgF8hE_ab) (ii) [MIT OCW Linear Algebra](https://ocw.mit.edu/courses/mathematics/18-06sc-linear-algebra-fall-2011/index.htm), and (iii) [Matrix Methods in Machine Learning](https://laurentlessard.com/teaching/532-matrix-methods).*

<img class="note-cover" src="/assets/images/linear_algebra/algebra-cover.png"/>
{% assign linear_algebra = site.linear_algebra | sort: "item_num" %}
{% for note in linear_algebra %}
<h3>
  <a href="{{ note.url }}">
    {{ note.title }}
  </a>
</h3>

<p>
  {{ note.excerpt }}
</p>

{% endfor %}