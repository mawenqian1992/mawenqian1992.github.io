---
layout: page
title: 归档
tagline: A chronological archive of my writing
permalink: /archive.html
ref: archive
order: 1
---

<div class="archive-list">

{% assign current_year = "" %}

{% for post in site.posts %}
  {% assign post_year = post.date | date: "%Y" %}

  {% if post_year != current_year %}

    <h2>
      <a href="{{ "/archive/" | append: post_year | append: "/" | relative_url }}">
        {{ post_year }}
      </a>
    </h2>

    {% assign current_year = post_year %}

  {% endif %}
{% endfor %}

</div>