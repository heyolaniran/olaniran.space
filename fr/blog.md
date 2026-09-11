---
title: "Notes"
description: "Notes de séminaire Lightning : HTLC, MAC/HMAC et échecs de routage, écrites pendant le Lightning Protocol Development."
permalink: /fr/blog/
lang: fr
en_alt: /blog/
---

# Notes

Notes de séminaire Lightning : HTLC, MAC/HMAC et échecs de routage. Écrites pendant le Lightning Protocol Development. (en anglais)

<ul class="post-list">
  {% assign fr_posts = site.posts | where: "lang", "en" %}
  {% for post in fr_posts %}
    <li class="post-item">
      <h3><a href="{{ post.url | relative_url }}">{{ post.title }}</a></h3>
      <p class="meta">
        {{ post.date | date: "%-d %b %Y" }}{% if post.tags and post.tags.size > 0 %} - {{ post.tags | join: ", " }}{% endif %}
      </p>
      {% if post.excerpt %}
        <p>{{ post.excerpt | strip_html | truncate: 180 }}</p>
      {% endif %}
    </li>
  {% endfor %}
</ul>
