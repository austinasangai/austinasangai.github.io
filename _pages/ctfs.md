---
title: "CTF Writeups"
permalink: /ctfs/
layout: page
---
## My CTF Writeups

<ul>
{% for post in site.posts %}
  {% if post.categories contains "CTF" %}
    <li>
      <a href="{{ post.url }}">{{ post.title }}</a> — {{ post.date | date: "%B %d, %Y" }}
    </li>
  {% endif %}
{% endfor %}
</ul>

[⬅️ Back to Home]({{ '/' | relative_url }})
