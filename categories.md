---
layout: page
title: 分类
tagline: Browse my writing by topic
permalink: /categories.html
ref: categories
order: 0
---

# 分类

<div class="category-grid">

{% for category in site.categories %}

<div class="category-item">

<h2>{{ category[0] }}</h2>

<ul>
    {% for post in category[1] limit:3 %}
    <li>
        <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
        <small>{{ post.date | date: "%Y-%m-%d" }}</small>
    </li>
    {% endfor %}
</ul>

</div>

{% endfor %}

</div>