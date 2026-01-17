---
layout: page
title: Outreach Activities
permalink: /outreach/activities/
---

<ul class="activity-list">
  {% for activity in site.data.outreach %}
    <li class="activity-item">
      {% if activity.image %}
        <img src="{{ '/assets/images/' | append: activity.image }}" alt="{{ activity.title }}" class="activity-image">
      {% endif %}

      <div class="activity-content">
        <h3>{{ activity.title }}</h3>
        <p>
          <strong>Date:</strong> {{ activity.date }}
          {% if activity.location %}<br><strong>Location:</strong> {{ activity.location }}{% endif %}
        </p>
        <p>{{ activity.description }}</p>

        {% if activity.url %}
          <p><a href="{{ activity.url }}">Read more →</a></p>
        {% endif %}
      </div>
    </li>
  {% endfor %}
</ul>

<style>
.activity-list {
  list-style: none;
  padding: 0;
}

.activity-item {
  display: flex;
  background: #f5f5f5;
  border-radius: 10px;
  padding: 1em;
  margin-bottom: 1.5em;
  gap: 1em;
  align-items: flex-start;
}

.activity-image {
  width: 150px;
  height: auto;
  border-radius: 8px;
  object-fit: cover;
}

.activity-content {
  flex: 1;
}
</style>
