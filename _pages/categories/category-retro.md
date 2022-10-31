---
title: "회고"
layout: archive
permalink: categories/retro
author_profile: true
sidebar_main: true
---

{% assign posts = site.categories.retro %}
{% for post in posts %} {% include archive-single2.html type=page.entries_layout %} {% endfor %}