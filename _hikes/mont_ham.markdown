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

<style>
  /* --- Layout Grid --- */
  .hike-container {
    max-width: 1100px; /* Limits width on big screens */
    margin: 40px auto;
    padding: 0 20px;
    display: grid;
    grid-template-columns: 300px 1fr; /* Fixed Sidebar | Flexible Content */
    gap: 40px;
    font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif;
    color: #333;
  }

  /* --- Sidebar --- */
  .hike-sidebar {
    position: sticky;
    top: 40px; /* Stick to top when scrolling */
    height: fit-content;
  }

  .hike-card {
    background: #fff;
    border-radius: 12px;
    border: 1px solid #eaeaea;
    box-shadow: 0 4px 20px rgba(0, 0, 0, 0.05);
    padding: 30px;
    margin-bottom: 30px;
  }

  /* --- Typography & Stats --- */
  .stats-card h2 {
    margin-top: 0;
    font-size: 1.4rem;
    font-weight: 700;
    color: #222;
    margin-bottom: 20px;
  }

  .stat-item {
    display: flex;
    justify-content: space-between;
    margin-bottom: 12px;
    font-size: 0.95rem;
    padding-bottom: 12px;
    border-bottom: 1px solid #f5f5f5;
  }
  .stat-item:last-of-type {
    border-bottom: none;
  }

  .stat-label { color: #666; font-weight: 500; }
  .stat-value { font-weight: 700; color: #333; text-align: right; }

  /* --- Buttons --- */
  .divider { border: 0; margin: 10px 0; }
  
  .hike-actions { display: flex; flex-direction: column; gap: 12px; }

  .hike-btn {
    display: block;
    text-align: center;
    padding: 12px 15px;
    border-radius: 8px;
    text-decoration: none;
    font-weight: 600;
    font-size: 0.9rem;
    transition: all 0.2s ease;
  }

  .btn-primary {
    background-color: #2c3e50; /* Dark Blue/Grey Theme */
    color: white;
  }
  .btn-primary:hover {
    background-color: #1a252f;
    transform: translateY(-1px);
  }

  .btn-outline {
    background-color: white;
    color: #555;
    border: 1px solid #ddd;
  }
  .btn-outline:hover {
    border-color: #2c3e50;
    color: #2c3e50;
  }

  /* --- Main Content --- */
  .hike-hero {
    height: 350px;
    border-radius: 12px;
    background-size: cover;
    background-position: center;
    position: relative;
    margin-bottom: 30px;
    overflow: hidden; /* Keeps image corners rounded */
  }

  .hero-overlay {
    position: absolute;
    bottom: 0;
    left: 0;
    width: 100%;
    padding: 40px;
    background: linear-gradient(to top, rgba(0, 0, 0, 0.8), transparent);
    color: white;
  }

  .hero-overlay h1 {
    margin: 0;
    font-size: 2.5rem;
    font-weight: 300;
  }

  .hero-date { margin: 10px 0 0 0; opacity: 0.8; font-size: 1.1rem; }

  /* Text Styling */
  .content-card p {
    line-height: 1.8;
    color: #444;
    margin-bottom: 20px;
    font-size: 1.05rem;
  }
  .intro-text {
    font-size: 1.2rem !important;
    color: #222 !important;
    font-weight: 400;
  }

  /* --- Gallery --- */
  .gallery-title { font-size: 1.5rem; font-weight: 600; margin-bottom: 20px; color: #333; }

  .hike-gallery {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(250px, 1fr)); /* Bigger images */
    gap: 20px;
  }

  .gallery-img {
    width: 100%;
    height: 250px; /* Taller square-ish images */
    object-fit: cover;
    border-radius: 12px;
    transition: transform 0.3s ease;
    cursor: pointer;
    box-shadow: 0 4px 10px rgba(0,0,0,0.1);
  }

  .gallery-img:hover {
    transform: scale(1.02);
    box-shadow: 0 8px 20px rgba(0,0,0,0.15);
  }

  /* Mobile */
  @media (max-width: 850px) {
    .hike-container { grid-template-columns: 1fr; }
    .hike-sidebar { position: static; order: 2; }
    .hike-hero { height: 250px; }
    .hero-overlay h1 { font-size: 2rem; }
  }
</style>