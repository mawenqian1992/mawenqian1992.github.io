---
layout: page
title: 归档
tagline: A chronological archive of my writing
permalink: /archive.html
ref: archive
order: 1
---

{% assign current_year = "" %}

{% for post in site.posts %}
{% assign post_year = post.date | date: "%Y" %}

{% if post_year != current_year %}
{% unless forloop.first %} </ul>
{% endunless %}

<h2>{{ post_year }}</h2>
<ul class="post-list">

{% assign current_year = post_year %}

{% endif %}

  <li>
    <span class="post-meta">{{ post.date | date: "%Y-%m-%d" }}</span>
    <h3>
      <a href="{{ post.url | absolute_url }}">{{ post.title | escape }}</a>
    </h3>
  </li>

{% endfor %}

</ul>