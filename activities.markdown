---
layout: page
title: Outreach Activities
permalink: /outreach/activities/
---

<div class="activity-container">
  
  <ul class="activity-list">
    {% for activity in site.data.outreach %}
      <li class="activity-item">
        
        {% if activity.image %}
          <div class="activity-image-wrapper">
            <img src="{{ '/assets/images/' | append: activity.image }}" alt="{{ activity.title }}" class="activity-image">
          </div>
        {% endif %}

        <div class="activity-content">
          <h3>{{ activity.title }}</h3>
          
          <p class="meta-info">
            <strong>Date:</strong> {{ activity.date }}
            {% if activity.location %}
              <span class="separator">•</span> 
              <strong>Location:</strong> {{ activity.location }}
            {% endif %}
          </p>
          
          <p class="description">{{ activity.description }}</p>

          {% if activity.url %}
            <a href="{{ activity.url }}" class="read-more">Read more &rarr;</a>
          {% endif %}
        </div>
      </li>
    {% endfor %}
  </ul>

</div>

<style>
/* 1. Container - Controls the overall width */
.activity-container {
  max-width: 100%; /* Stretches to full width */
  padding: 10px;
  margin: 0 auto;
}

.activity-list {
  list-style: none;
  padding: 0;
  margin: 0;
}

/* 2. The Card Style */
.activity-item {
  display: flex;
  background: #fff; /* White background */
  border: 1px solid #eaeaea;
  border-radius: 8px;
  box-shadow: 0 2px 15px rgba(0,0,0,0.08); /* Soft shadow */
  margin-bottom: 30px; /* Space between cards */
  overflow: hidden; /* Keeps image corners rounded */
  transition: transform 0.2s ease, box-shadow 0.2s ease;
}

.activity-item:hover {
  transform: translateY(-3px);
  box-shadow: 0 5px 20px rgba(0,0,0,0.12);
}

/* 3. Image Styling */
.activity-image-wrapper {
  flex: 0 1 350px; /* allow shrink */
  max-width: 350px;
  border-right: 1px solid #eaeaea;
}

.activity-image {
  width: 100%;
  height: 100%;
  object-fit: cover; /* Ensures image covers area without stretching */
  display: block;
}

/* 4. Content Styling */
.activity-content {
  flex: 1;
  padding: 30px;
  display: flex;
  flex-direction: column;
  justify-content: center;
}

.activity-content h3 {
  margin-top: 0;
  margin-bottom: 10px;
  font-size: 1.5rem;
  font-weight: 600;
  color: #333;
}

.meta-info {
  font-size: 0.9rem;
  color: #5ea88e; /* Your Green Accent */
  margin-bottom: 15px;
  text-transform: uppercase;
  font-weight: 600;
  letter-spacing: 0.5px;
}

.meta-info .separator {
  margin: 0 8px;
  color: #ccc;
}

.description {
  color: #666;
  line-height: 1.6;
  margin-bottom: 20px;
}

.read-more {
  display: inline-block;
  color: #5ea88e; /* Green accent */
  font-weight: 700;
  text-decoration: none;
  font-size: 0.95rem;
  transition: color 0.2s;
}

.read-more:hover {
  color: #3d7a64; /* Darker green on hover */
}

/* Mobile Responsiveness */
@media (max-width: 768px) {
  .activity-item {
    flex-direction: column; /* Stack image on top of text */
  }
  
  .activity-image-wrapper {
    flex: none;
    width: 100%;
    height: 200px;
    border-right: none;
    border-bottom: 1px solid #eaeaea;
  }
}
</style>

