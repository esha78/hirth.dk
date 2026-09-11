---
layout: default
title: Publications
permalink: /publications/
description: Peer-reviewed publications by Stefan Hirth.
---
<h1>Publications</h1>

<p class="lede">{{ site.data.publications.intro }}</p>

<h2>Publications in peer-reviewed journals</h2>

{% for pub in site.data.publications.journal_articles %}
<div class="entry">
  <h3 class="entry-title">&ldquo;{{ pub.title }}&rdquo;</h3>
  {% if pub.authors %}<p class="entry-meta">{{ pub.authors | markdownify | remove: '<p>' | remove: '</p>' }}</p>{% endif %}
  <p class="entry-meta">{{ pub.venue }}</p>
  <p class="entry-links">
    {% for link in pub.links %}<a href="{{ link.url }}">{{ link.label }}</a>{% endfor %}
  </p>
  <p class="entry-abstract"><strong>Abstract:</strong> {{ pub.abstract }}</p>
</div>
{% endfor %}

<h2>Monographies</h2>

{% for mono in site.data.publications.monographs %}
<div class="entry">
  <h3 class="entry-title">&ldquo;{{ mono.title }}&rdquo; <span style="font-weight:400;">{{ mono.subtitle }}</span></h3>
  <p class="entry-meta">{{ mono.venue }}</p>
  <p class="entry-links">
    {% for link in mono.links %}<a href="{{ link.url }}">{{ link.label }}</a>{% endfor %}
  </p>
</div>
{% endfor %}
