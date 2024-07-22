---
layout: page
title: Archive
---

{% assign sorted_tags = site.tags | sort %}
{% for tag in sorted_tags %}
  <h3 id="{{ tag[0] }}">#{{ tag[0] }}</h3>
  <ul>
    {% for post in tag[1] %}
      <li><a href="{{ post.url | relative_url }}">{{ post.date | date: "%Y %B" }} - {{ post.title }}</a></li>
    {% endfor %}
  </ul>
{% endfor %}
