---
title: "Type of Algorithm"
layout: archive
permalink: /Data Structure
author_profile: true
sidebar_main: true
sidebar:
    nav: "sidebar-category"
---


{% assign posts = site.categories.['Data Structure'] %}
{% for post in posts %} {% include archive-single.html type=page.entries_layout %} {% endfor %}