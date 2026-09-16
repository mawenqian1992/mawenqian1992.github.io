---
layout: page
title: 标签
tagline: A few more words
permalink: /tags.html
ref: tags
order: 2
---

# 标签

{% for tag in site.tags %}

<h2 id="tag-{{ tag[0] | slugify }}">{{ tag[0] }}</h2>

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

[回到首页]({{ '/' | absolute_url }})