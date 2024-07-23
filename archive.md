---
layout: base
title: Archive
---

{% assign date_format = site.minima.date_format | default: "%b %-d, %Y" %}
{% assign sorted_tags = site.tags | sort %}
{% for tag in sorted_tags %}
  <h3 id="{{ tag[0] }}">#{{ tag[0] }}</h3>
  <ul>
    {% for post in tag[1] %}
      <li><a href="{{ post.url | relative_url }}">{{ post.date | date: date_format }} - {{ post.title }}</a></li>
    {% endfor %}
  </ul>
{% endfor %}
