---
layout: archive
permalink: portfolio/
date: 2018-06-06
modified: 2018-06-07
excerpt: "Projects big and small I've been working on"
---
<div>
{% for post in site.categories.projects %}
  {% include post-grid.html %}
{% endfor %}
</div><!-- /.tiles -->
