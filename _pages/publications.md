---
layout: page
permalink: /publications/
title: publications
description: A complete list of publications can be found on my <a href='https://scholar.google.com/citations?user=_c6hHW8AAAAJ&hl=en'> Google Scholar profile (click here) </a>
years: [2022]
nav: true
nav_order: 1
---
<!-- _pages/publications.md -->
<div class="publications">

{%- for y in page.years %}
  <h2 class="year">{{y}}</h2>
  {% bibliography -f {{ site.scholar.bibliography }} -q @*[year={{y}}]* %}
{% endfor %}

</div>
