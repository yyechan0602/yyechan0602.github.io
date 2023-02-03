---
title: "Type of Algorithm"
layout: archive
permalink: /Type-Of-Algorithm
author_profile: true
sidebar_main: true
sidebar:
    nav: "sidebar-category"
---


{% assign posts = site.categories.['Type Of Algorithm'] %}
{% for post in posts %} {% include archive-single.html type=page.entries_layout %} {% endfor %}