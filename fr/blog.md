---
title: "Notes sur Lightning : HTLC, échecs de routage et paiements"
description: "J'ai appris Lightning en l'expliquant simplement. Notes pratiques du cours Lightning de Chaincode : HTLC, MAC/HMAC et pourquoi les paiements échouent."
permalink: /fr/blog/
lang: fr
en_alt: /blog/
---

# Notes

J'ai appris Lightning en l'expliquant simplement. Mes notes pratiques du cours Lightning de Chaincode — HTLC, MAC/HMAC et pourquoi les paiements échouent, sans jargon. (en anglais)

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
