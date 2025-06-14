---
layout: page
title: Outreach Activities
permalink: /outreach/activities
---

<div class="outreach-list">
  {% for activity in site.data.outreach %}
    <div class="outreach-entry">
      <h2>{{ activity.title }}</h2>
      <p><strong>Date:</strong> {{ activity.date }}</p>
      <p>{{ activity.description }}</p>
      {% if activity.url %}
        <p><a href="{{ activity.url }}">Read more →</a></p>
      {% endif %}
      <hr>
    </div>
  {% endfor %}
</div>

<style>
.outreach-list {
  max-width: 800px;
  margin: 2rem auto;
  padding: 0 1rem;
}

.outreach-entry {
  margin-bottom: 2rem;
}

.outreach-entry hr {
  margin-top: 1.5rem;
  border: none;
  border-top: 1px solid #ccc;
}
</style>
