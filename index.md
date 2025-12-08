---
layout: default
title: Home
nav_order: 1
has_children: true
---

{% capture brief %}{% include_relative README.md %}{% endcapture %}
{{ brief | markdownify }}