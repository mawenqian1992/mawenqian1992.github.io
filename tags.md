---
layout: default
title: 标签
permalink: /tags/
---

# 标签

{% for tag in site.tags %}

<h2 id="{{ tag[0] }}">{{ tag[0] }}</h2>

<ul>
    {% for post in tag[1] %}
    <li>
        <a href="{{ post.url | relative_url }}">
            {{ post.title }}
        </a>
        <small>
            {{ post.date | date: "%Y-%m-%d" }}
        </small>
    </li>
    {% endfor %}
</ul>

{% endfor %}
