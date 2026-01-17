---
layout: default
permalink: /cv_new/
---

{% include career-profile.html %}
{% unless site.data.data.sidebar.education %}
  {% include education.html %}
{% endunless %}
