---
layout: default
title: Funded Projects
permalink: /funded-projects/
description: Externally funded research projects led by or involving Stefan Hirth.
---
<h1>Externally Funded Research Projects</h1>

{% for proj in site.data.funded_projects.projects %}
<div class="entry">
  <h3 class="entry-title">{{ proj.title }}</h3>
  <div class="entry-abstract">{{ proj.body | markdownify }}</div>
</div>
{% endfor %}
