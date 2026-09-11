---
title: "Notes"
description: "Lightning seminar notes: HTLC, MAC/HMAC, and routing failures. Written during Lightning Protocol Development."
permalink: /blog/
lang: en
fr_alt: /fr/blog/
---

# Notes

Lightning seminar notes: HTLC, MAC/HMAC, and routing failures. Written during Lightning Protocol Development.

<ul class="post-list">
  {% assign en_posts = site.posts | where: "lang", "en" %}
  {% for post in en_posts %}
    <li class="post-item">
      <h3><a href="{{ post.url | relative_url }}">{{ post.title }}</a></h3>
      <p class="meta">
        {{ post.date | date: "%b %-d, %Y" }}{% if post.tags and post.tags.size > 0 %} - {{ post.tags | join: ", " }}{% endif %}
      </p>
      {% if post.excerpt %}
        <p>{{ post.excerpt | strip_html | truncate: 180 }}</p>
      {% endif %}
    </li>
  {% endfor %}
</ul>
