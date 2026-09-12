---
layout: default
title: 分类
permalink: /categories/
---

# 分类

{% for category in site.categories %}

## {{ category[0] }}

<ul>
    {% for post in category[1] %}
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
