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

<h2 id="category-{{ category[0] | slugify }}">{{ category[0] }}</h2>

<div class="category-posts">

    {% for post in category[1] %}

    <div class="category-post">
        <span class="category-date">{{ post.date | date: "%Y-%m-%d" }}</span>
        <a href="{{ post.url | relative_url }}" title="{{ post.title }}">
            {{ post.title }}
        </a>
    </div>

    {% endfor %}

</div>

</div>

{% endfor %}

</div>