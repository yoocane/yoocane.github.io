---
layout: page
permalink: /publications/
title: Publications
description: Selected publications in reversed chronological order
years: [2022, 2021, 2020]
nav: false
nav_order: 1
---
<!-- _pages/publications.md -->
<div class="publications">

{%- for y in page.years %}
  <h2 class="year">{{y}}</h2>
  {% bibliography -f papers -q @*[year={{y}}]* %}
{% endfor %}

</div>
