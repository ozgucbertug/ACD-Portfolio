---
layout: default
title: Assignment 1
nav_order: 2
parent: Home
permalink: /A1/
---

{% capture brief %}{% include_relative BRIEF.md %}{% endcapture %}
{{ brief | markdownify }}
