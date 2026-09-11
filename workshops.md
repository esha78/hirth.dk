---
layout: default
title: Workshops
permalink: /workshops/
description: Workshops organized by Stefan Hirth in Aarhus.
---
<h1>Workshops</h1>

{% for e in site.data.workshops.events %}
<div class="entry">
  <h3 class="entry-title">{{ e.dates }}</h3>
  <div class="entry-abstract">{{ e.body | markdownify }}</div>
</div>
{% endfor %}
