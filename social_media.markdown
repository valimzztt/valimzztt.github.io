---
layout: page
title: Social Media
permalink: /outreach/social_media
instagramId: https://www.instagram.com/p/DKxuxPpt5en/
insta_posts:
  - https://www.instagram.com/p/DKxuxPpt5en/
  - https://www.instagram.com/p/DGEPRUUt6gJ/
  - https://www.instagram.com/p/DDI1HjNOFSc/
---

<p>
  I started the <strong>Graduate Spotlight</strong> series to showcase the incredible diversity of graduate student research happening at McGill Physics. Each video highlights a different project and the person behind it — from ultrafasr laser science to expolanets research!
</p>
<div class="insta-gallery">
  {% for url in page.insta_posts %}
    <div class="insta-embed">
      <blockquote 
        class="instagram-media" 
        data-instgrm-permalink="{{ url }}" 
        data-instgrm-version="14" 
        style="width:100%; margin: 0 auto;">
      </blockquote>
    </div>
  {% endfor %}
</div>
<script async src="//www.instagram.com/embed.js"></script>
<style>
.insta-gallery {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  gap: 1rem;
}

.insta-embed {
  flex: 1 1 300px;
  max-width: 320px;
}
</style>
