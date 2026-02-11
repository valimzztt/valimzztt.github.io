---
layout: default
title: "Mont Ham"
date: 2024-08-20
image: /assets/images/hikes/quebec.JPEG
location: "Eastern Townships, Quebec"
distance: "26 km"
elevation: "540 m"
duration: "5 hours"
google_maps_link: "https://g.co/kgs/th3sjDs"
komoot_link: "https://www.komoot.com/smarttour/e1324739862/to-the-highest-peak-of-the-alpstein-spectacular-saentis-tour?ref=wdd"
gallery:
  - src: /assets/images/hikes/mount-ham/ham1.jpg
    alt: "View of the trail"
  - src: /assets/images/hikes/mount-ham/ham2.jpg
    alt: "Summit view"
  - src: /assets/images/hikes/mount-ham/ham3.jpg
    alt: "Landscape"
  - src: /assets/images/hikes/mount-ham/ham4.jpg
    alt: "Landscape"
---

<div class="hike-container">
  
  <aside class="hike-sidebar">
    <div class="hike-card stats-card">
      <h2>Hike Details</h2>
      
      <div class="stat-item">
        <span class="stat-label">Location</span>
        <span class="stat-value">{{ page.location }}</span>
      </div>
      
      <div class="stat-item">
        <span class="stat-label">Distance</span>
        <span class="stat-value">{{ page.distance }}</span>
      </div>
      
      <div class="stat-item">
        <span class="stat-label">Elevation</span>
        <span class="stat-value">{{ page.elevation }}</span>
      </div>

      <div class="stat-item">
        <span class="stat-label">Duration</span>
        <span class="stat-value">{{ page.duration }}</span>
      </div>
      
      <hr class="divider">
      
      <div class="hike-actions">
        <a href="{{ page.google_maps_link }}" target="_blank" class="hike-btn btn-outline">View on Google Maps</a>
        <a href="{{ page.komoot_link }}" target="_blank" class="hike-btn btn-primary">View on Komoot</a>
      </div>
    </div>
  </aside>

  <main class="hike-main">
    
    <div class="hike-hero" style="background-image: url('{{ page.image | relative_url }}');">
      <div class="hero-overlay">
        <h1>{{ page.title }}</h1>
        <p class="hero-date">{{ page.date | date: "%B %d, %Y" }}</p>
      </div>
    </div>

    <div class="hike-card content-card">
      <p class="intro-text">
        This was my very first hike in Quebec, and I picked it with one goal in mind: to finally witness the famous eastern Canadian fall foliage.
      </p>

      <p>
        Mount Ham, located in Saint-Joseph-de-Ham-Sud, is nestled in the <strong>Eastern Townships</strong> — a region I hadn’t explored much before. At 713 metres above sea level, it's one of the tallest peaks in the lowlands of the Appalachian range, making it a great choice for a half-day hike with rewarding views.
      </p>

      <p>
        While the terrain around Montreal isn’t exactly known for dramatic elevation changes, and I generally tend to gravitate toward more alpine landscapes, I found myself pleasantly surprised. The trail was peaceful, with bursts of colour starting to show on the trees, and the summit offered a panoramic view over the rolling hills of the Townships.
      </p>
      
      <p>
        It wasn’t the most challenging or jaw-dropping hike I’ve done, but something about being surrounded by the stillness of the forest in a new part of the province made it memorable. I’m already looking forward to doing some more hikes in the area next fall!
      </p>
    </div>

    <h3 class="gallery-title">Photo Gallery</h3>
    <div class="hike-gallery">
      {% for photo in page.gallery %}
        <img src="{{ photo.src | relative_url }}" alt="{{ photo.alt }}" class="gallery-img">
      {% endfor %}
    </div>

  </main>
</div>
