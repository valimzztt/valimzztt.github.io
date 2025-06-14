---
layout: page
title: Public Talks
layout: page
title: Public Talks
permalink: /outreach/public_talks/
---

Here is a list of public talks I organized as part of the McGill Physics Outreach series:

<ul class="talk-list">
  {% for talk in site.data.public_talks %}
    <li class="talk-item">
      {% if talk.image %}
        <img src="{{ '/assets/images/' | append: talk.image }}" alt="{{ talk.title }}" class="talk-image">
      {% endif %}
      <div class="talk-content">
        <h3>{{ talk.title }}</h3>
        <p><strong>Speaker:</strong> {{ talk.speaker }}<br>
           <strong>Date:</strong> {{ talk.date }}<br>
           <strong>Location:</strong> {{ talk.location }}</p>
        <p>{{ talk.description }}</p>
      </div>
    </li>
  {% endfor %}
</ul>

<style>
.talk-list {
  list-style: none;
  padding: 0;
}

.talk-item {
  display: flex;
  background: #f5f5f5;
  border-radius: 10px;
  padding: 1em;
  margin-bottom: 1.5em;
  gap: 1em;
  align-items: flex-start;
}

.talk-image {
  width: 150px;
  height: auto;
  border-radius: 8px;
  object-fit: cover;
}

.talk-content {
  flex: 1;
}
</style>
