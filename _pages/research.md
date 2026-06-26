---
layout: page
permalink: /research/
title: research
description: Papers and research outputs. A complete list is also available on my <a href='https://scholar.google.com/citations?user=_c6hHW8AAAAJ&hl=en'>Google Scholar profile</a>.
years: [2026, 2024, 2023]
nav: true
nav_order: 1
---
<!-- _pages/research.md -->
<div class="publications">

{%- for y in page.years %}
  <h2 class="year">{{y}}</h2>
  {% bibliography -f {{ site.scholar.bibliography }} -q @*[year={{y}}]* %}
{% endfor %}

</div>
