---
layout: single
title: "Projects"
permalink: /portfolio/
author_profile: true
---

A collection of my cybersecurity projects, CTF write-ups, and research work.

<div class="filter-btns">
  <button class="filter-btn active" data-filter="all">All</button>
  <button class="filter-btn" data-filter="red-team">Red Team</button>
  <button class="filter-btn" data-filter="blue-team">Blue Team</button>
  <button class="filter-btn" data-filter="ctf">CTF Write-up</button>
</div>

<div class="portfolio-grid">
{% assign projects = site.portfolio | sort: "date" | reverse %}
{% for project in projects %}
  <div class="portfolio-card" data-type="{{ project.type }}">
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
</div>

<script>
const buttons = document.querySelectorAll('.filter-btn');
const cards = document.querySelectorAll('.portfolio-card');

buttons.forEach(btn => {
  btn.addEventListener('click', () => {

    // Update active button
    buttons.forEach(b => b.classList.remove('active'));
    btn.classList.add('active');

    const filter = btn.getAttribute('data-filter');

    // Show or hide cards
    cards.forEach(card => {
      if (filter === 'all' || card.getAttribute('data-type') === filter) {
        card.style.display = 'block';
      } else {
        card.style.display = 'none';
      }
    });

  });
});
</script>
