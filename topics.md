---
layout: page
title: Topics
permalink: /topics/
---

{% assign topics_csv = '' %}
{% for post in site.posts %}
  {% for category in post.categories %}
    {% assign topic_token = '|' | append: category | append: '|' %}
    {% unless topics_csv contains topic_token %}
      {% assign topics_csv = topics_csv | append: topic_token %}
    {% endunless %}
  {% endfor %}
{% endfor %}

{% assign topic_names = topics_csv | split: '|' | sort %}

{% for topic in topic_names %}
  {% unless topic == '' %}
### <span id="{{ topic | slugify }}">{{ topic }}</span>

{% assign posts_in_topic = site.posts | where_exp: 'post', "post.categories contains topic" %}
{% for post in posts_in_topic %}
- [{{ post.title }}]({{ post.url | relative_url }})
{% endfor %}

  {% endunless %}
{% endfor %}
