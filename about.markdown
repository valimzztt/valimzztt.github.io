---
layout: default
title: About
permalink: /about/
---
<!-- Link the contact form CSS -->
<link rel="stylesheet" href="{{ './assets/css/style.css' | relative_url }}">
Welcome! I am currently a Master's student in Physics at McGill University, working in the [Ultrafast THz Spectroscopy Laboratory](https://thz.lab.mcgill.ca/), under the supervision of Professor David Cooke. My research focuses on ultrabroad THz spectroscopy to investigate the dynamics of polarons in halide perovskites.
I am passionate about understanding quantum materials and their applications in optoelectronic devices, with a strong interest in contributing to sustainable technologies.
Feel free to explore this site to learn more about my research, publications, and ongoing projects!

## Contact Form

Please use the form below to get in touch:

<form class="contact-form" action="https://formspree.io/f/xyzzebod" method="POST">
  <label for="name">Your Name:</label>
  <input type="text" id="name" name="name" placeholder="Enter your name" required>

  <label for="email">Your Email:</label>
  <input type="email" id="email" name="email" placeholder="Enter your email" required>

  <label for="message">Your Message:</label>
  <textarea id="message" name="message" rows="5" placeholder="Write your message here" required></textarea>

  <button type="submit">Send</button>
</form>