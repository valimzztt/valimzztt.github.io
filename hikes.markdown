---
layout: default
title: "Hiking"
permalink: /hobbies/
hero_image: /assets/images/hikes/aosta.JPEG
---
<link rel="stylesheet" href="{{ './assets/css/style.css' | relative_url }}">

I have a passion for staying active and exploring the outdoors.
Whether it's running, biking, hiking, or skiing, I find joy and energy in connecting with nature. 

<div class="hero-header">
  <img src="{{ page.hero_image }}" alt="Hiking intro" class="hero-img">
  <div class="hero-text">
    <h1>Welcome to My Hikes</h1>
    <p>Discover some of my favorite hiking adventures from around the world 🌍</p>
  </div>
</div>

<div class="hike-grid">
  {% for hike in site.hikes %}
    <div class="hike-card">
      <a href="{{ hike.url }}">
        <img src="{{ hike.image }}" alt="{{ hike.title }}">
        <h3>{{ hike.title }}</h3>
        <p>{{ hike.location }}</p>
      </a>
    </div>
  {% endfor %}
</div>
