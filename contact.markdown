---
layout: default
title: Contact
permalink: /contact/
---

<link rel="stylesheet" href="{{ './assets/css/style.css' | relative_url }}">
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
