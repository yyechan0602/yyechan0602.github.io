---
title: "백준"
layout: archive
permalink: /BaekJoon
author_profile: true
sidebar_main: true
sidebar:
    nav: "sidebar-category"
---


{% assign posts = site.categories.BaekJoon %}
{% for post in posts %} {% include archive-single.html type=page.entries_layout %} {% endfor %}

<!--
categories 를 바꿔준 후
[ data/navigation.yml ] 파일에 있는 
사이드바를 변경해주면 된다.
-->