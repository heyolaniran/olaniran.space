---
title: "Notes on Lightning: HTLCs, routing failures, and how payments move"
description: "I learned Lightning by explaining it simply. Hands-on notes from Chaincode's Lightning protocol course: HTLCs, MAC/HMAC, and why payments fail."
permalink: /blog/
lang: en
fr_alt: /fr/blog/
---

# Notes

I learned Lightning by breaking it down in public. These are my hands-on notes from Chaincode's Lightning protocol course — HTLCs, MAC/HMAC, and why payments fail, explained without jargon.

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
