---
layout: default
title: "Bike Trip: Montreal-Ottawa"
date: 2024-08-20
image: /assets/images/hikes/ottawa_bike/header.JPEG
location: "Montréal-Ottawa"
distance: "210 km"
duration: "2 days"
google_maps_link: "https://www.google.com/maps/embed?pb=!1m32!1m12!1m3!1d481648.390604931!2d-74.61331038463611!3d45.52150422308185!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!4m17!3e1!4m3!3m2!1d45.5127521!2d-73.56629099999999!4m5!1s0x4cceeb81480dd781%3A0x5faf289251a90419!2sVankleek%20Hill%2C%20Ontario!3m2!1d45.5196512!2d-74.6522016!4m5!1s0x4cce05b25f5113af%3A0x8a6a51e131dd15ed!2sOttawa%2C%20ON!3m2!1d45.420057199999995!2d-75.7003397!5e1!3m2!1sen!2sca!4v1750803885877!5m2!1sen!2sca"
komoot_link: "https://www.komoot.com/tour/1211859730"
gallery:
  - src: /assets/images/hikes/ottawa_bike/image7.JPEG
    alt: "View of the trail"
  - src: /assets/images/hikes/ottawa_bike/image2.JPEG
    alt: "Summit view"
  - src: /assets/images/hikes/ottawa_bike/image3.JPEG
    alt: "Landscape"
  - src: /assets/images/hikes/ottawa_bike/image4.JPEG
    alt: "Landscape"
  - src: /assets/images/hikes/ottawa_bike/image5.JPEG
    alt: "Landscape"
---
<link rel="stylesheet" href="{{ '/assets/css/hikes.css' | relative_url }}">

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
        <span class="stat-label">Duration</span>
        <span class="stat-value">{{ page.duration }}</span>
      </div>
    </div>

    <div class="hike-card gallery-card">
      <h3>Gallery</h3>
      <div class="sidebar-gallery-grid">
        {% if page.gallery %}
          {% for photo in page.gallery %}
            <img src="{{ photo.src | relative_url }}" alt="{{ photo.alt }}">
          {% endfor %}
        {% else %}
           <img src="/assets/images/hikes/ottawa_bike/image7.JPEG" alt="View">
           <img src="/assets/images/hikes/ottawa_bike/image2.JPEG" alt="View">
           <img src="/assets/images/hikes/ottawa_bike/image3.JPEG" alt="View">
           <img src="/assets/images/hikes/ottawa_bike/image4.JPEG" alt="View">
        {% endif %}
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
        <p>
        This was by far one of the most satisfying and spontaneous adventures I’ve done in Quebec! The idea to bike from Montréal to Ottawa had been in the back of my mind for a while, and one weekend, I finally decided to go for it,alongside with a good friend of mine.  
        </p> 

        <p>The route follows mostly well-maintained bike paths and quiet country roads. We also had the luck to stop for the night in Vanleek Hill, which is considered Ontario's "Gingerbread" capital (!), which turned out to be a very charming village with lots of houses that looked from the Victorian Age.</p> 

        <p>What was special about this trip was to see the vast fields of farmland, and for the first time in a while, I soaked in the feeling of covering real distances. Moreover, this was my first time in Ontario, and entering Canada's most important province by bike was definitely a special moment. </p>

        <p>I still remember that rolling into the capital on two wheels felt like a genuine achievement. Tired, yes, but more than anything, energized and satisfied about my first longer bike ride. I am already thinking what could be the next multi-day bike trip: maybe from Montreal to Boston?</p>
    </div>
    
    <div class="hike-card map-card">
        <h3>Route</h3>
        <iframe src="{{ page.google_maps_link }}" width="100%" height="350" style="border:0;" allowfullscreen="" loading="lazy" referrerpolicy="no-referrer-when-downgrade"></iframe>
    </div>

  </main>
</div>
