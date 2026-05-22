---
layout: single
title: "Projects"
permalink: /portfolio/
author_profile: true
---

A collection of my cybersecurity projects, CTF write-ups, and research work.

<div class="filter-btns" style="margin-bottom: 1.5rem;">
  <strong>Filter:</strong>
  <a href="/portfolio/" class="btn btn--small btn--primary">All</a>
  <a href="/portfolio/?type=red-team" class="btn btn--small btn--inverse">Red Team</a>
  <a href="/portfolio/?type=blue-team" class="btn btn--small btn--inverse">Blue Team</a>
  <a href="/portfolio/?type=ctf" class="btn btn--small btn--inverse">CTF Write-up</a>
</div>

{% assign projects = site.portfolio | sort: "date" | reverse %}
{% for project in projects %}
<div class="portfolio-card">
  <h3><a href="{{ project.url }}">{{ project.title }}</a></h3>
  <span class="badge badge--{{ project.type }}">{{ project.type }}</span>
  <p>{{ project.excerpt }}</p>
  <div class="project-tags">
    {% for tag in project.tags %}
    <span class="p-tag">{{ tag }}</span>
    {% endfor %}
  </div>
  <a href="{{ project.url }}" class="btn btn--small btn--inverse">Read More →</a>
</div>
{% endfor %}
