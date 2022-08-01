---
title: "Java"
layout: archive
permalink: categories/java
author_profile: true
sidebar_main: true
---

{% assign posts = sites.categories.java %}
{% for post in posts %} 
{% include archive-single.html type=page.entries_layout %} 
{% endfor %}