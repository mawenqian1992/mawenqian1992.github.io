---
layout: page
title: 标签
tagline: Explore my writing through tags and keywords.
permalink: /tags.html
ref: tags
order: 2
---

<div class="tag-grid">

{% assign all_tags = site.tags | sort %}

{% for tag in all_tags %}

<div class="tag-item" id="tag-{{ tag[0] | slugify }}">

  <h2>{{ tag[0] }}</h2>

  <div class="tag-posts">

    {% for post in tag[1] %}

    <div class="tag-post">
      <span class="tag-date">{{ post.date | date: "%Y-%m-%d" }}</span>
      <a href="{{ post.url | relative_url }}" title="{{ post.title }}">
        {{ post.title }}
      </a>
    </div>

    {% endfor %}

  </div>

</div>

{% endfor %}

<div class="tag-item">
  <h2><a href="{{ '/private/' | relative_url }}">密文</a></h2>
</div>

</div>