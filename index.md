---
layout: home
author_profile: true
title: "John Kamau"
header:
  overlay_color: "#0a1628"
  overlay_filter: "0.5"
  caption: ""
excerpt: "Penetration Tester · SOC Analyst · CTF Player"
---

<div class="stats-row">
  <div class="stat-item">
    <span class="stat-num">12+</span>
    <span class="stat-label">CTF Challenges Solved</span>
  </div>
  <div class="stat-item">
    <span class="stat-num">5</span>
    <span class="stat-label">Certifications</span>
  </div>
  <div class="stat-item">
    <span class="stat-num">8</span>
    <span class="stat-label">Projects Completed</span>
  </div>
  <div class="stat-item">
    <span class="stat-num">3</span>
    <span class="stat-label">Bug Bounties</span>
  </div>
</div>

## Featured Projects

{% assign featured = site.portfolio | where: "featured", true %}
{% for project in featured limit:3 %}
<div class="portfolio-card">
  <h3><a href="{{ project.url }}">{{ project.title }}</a></h3>
  <p class="project-type {{ project.type }}">{{ project.type | upcase }}</p>
  <p>{{ project.excerpt }}</p>
  <div class="project-tags">
    {% for tag in project.tags %}
    <span class="p-tag">{{ tag }}</span>
    {% endfor %}
  </div>
</div>
{% endfor %}

<div style="text-align:center; margin-top: 1.5rem;">
  <a href="/portfolio/" class="btn btn--primary">View All Projects</a>
</div>
