---
layout: page
title: 分类
tagline: Browse my writing by topic
permalink: /categories.html
ref: categories
order: 0
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

[回到首页]({{ '/' | absolute_url }})