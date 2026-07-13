---
layout: page
title: Archives
permalink: /archives/
---

{% assign years = site.posts | group_by_exp: 'post', "post.date | date: '%Y'" %}

{% for year in years %}
### <span id="y{{ year.name }}">{{ year.name }}</span>

{% assign posts_in_year = year.items | sort: 'date' | reverse %}
{% for post in posts_in_year %}
- [{{ post.date | date: "%Y-%m-%d" }} - {{ post.title }}]({{ post.url | relative_url }})
{% endfor %}

{% endfor %}
