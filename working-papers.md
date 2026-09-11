---
layout: default
title: Working Papers
permalink: /working-papers/
description: Working papers and work in progress by Stefan Hirth.
---
<h1>Working papers</h1>

{% for pub in site.data.working_papers.papers %}
<div class="entry">
  <h3 class="entry-title">&ldquo;{{ pub.title }}&rdquo;</h3>
  {% if pub.authors %}<p class="entry-meta">{{ pub.authors | markdownify | remove: '<p>' | remove: '</p>' }}</p>{% endif %}
  <p class="entry-meta">{{ pub.date }}</p>
  <p class="entry-links">
    {% for link in pub.links %}<a href="{{ link.url }}">{{ link.label }}</a>{% endfor %}
  </p>
  <p class="entry-abstract"><strong>Abstract:</strong> {{ pub.abstract }}</p>
</div>
{% endfor %}

<h2>Work in progress</h2>

{% for pub in site.data.working_papers.work_in_progress %}
<div class="entry">
  <h3 class="entry-title">&ldquo;{{ pub.title }}&rdquo;</h3>
  {% if pub.authors %}<p class="entry-meta">{{ pub.authors | markdownify | remove: '<p>' | remove: '</p>' }}</p>{% endif %}
</div>
{% endfor %}
