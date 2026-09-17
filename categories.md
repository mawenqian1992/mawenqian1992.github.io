---
layout: page
title: 分类
tagline: Browse my writing by topic
permalink: /categories.html
ref: categories
order: 0
---

<div class="category-grid">

{% for category in site.categories %}

<div class="category-item">

<h2>{{ category[0] }}</h2>

<div class="category-posts">
    {% for post in category[1] limit:3 %}
    <div class="category-post">
        <a href="{{ post.url | relative_url }}" title="{{ post.title }}">{{ post.title }}</a>
        <small>{{ post.date | date: "%Y-%m-%d" }}</small>
    </div>
    {% endfor %}
</div>

</div>

{% endfor %}

</div>