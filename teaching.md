---
layout: default
title: Teaching
permalink: /teaching/
description: Courses taught by Stefan Hirth, by institution.
---
<h1>Teaching</h1>

{% for inst in site.data.teaching.institutions %}
<h2 class="group-heading"><a href="{{ inst.url }}">{{ inst.name }}</a></h2>
<ul class="plain-list">
  {% for course in inst.courses %}
  <li>{{ course | markdownify | remove: '<p>' | remove: '</p>' }}</li>
  {% endfor %}
</ul>
{% endfor %}
