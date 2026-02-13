---
layout: default
title: "Valentina Mazzotti"
permalink: /cv/
---
<link rel="stylesheet" href="{{ '/assets/css/cv.css' | relative_url }}">

<div class="cv-container">
  
  <aside class="cv-sidebar">
    <nav>
      <a href="#personal-info" class="cv-nav-link">Personal information</a>
      <a href="#profile" class="cv-nav-link">Profile</a>
      <a href="#work" class="cv-nav-link">Work</a>
      <a href="#education" class="cv-nav-link">Education</a>
      <a href="#skills" class="cv-nav-link">Skills</a>
      <a href="#publications" class="cv-nav-link">Publications</a>
    </nav>
  </aside>

  <main class="cv-main">
    
    <h1>CV</h1>
    <p class="cv-intro">See <a href="https://www.linkedin.com/in/valentina-mazzotti/">my LinkedIn profile</a> for additional information.</p>

    <section id="personal-info" class="cv-card">
      <h2>{{ site.data.cv.personal.title }}</h2>
      <div class="info-grid">
        
        <div class="info-label">Name</div>
        <div class="info-value">{{ site.data.cv.personal.name }}</div>

        <div class="info-label">Email</div>
        <div class="info-value highlight">
          <a href="mailto:{{ site.data.cv.personal.email }}">{{ site.data.cv.personal.email }}</a>
        </div>

        <div class="info-label">Location</div>
        <div class="info-value">{{ site.data.cv.personal.location }}</div>

        <div class="info-label">Citizenship</div>
        <div class="info-value">{{ site.data.cv.personal.citizenship }}</div>

      </div>
    </section>

    <section id="work" class="cv-card">
      <h2>{{ site.data.cv.experiences.title }}</h2>
      {% for exp in site.data.cv.experiences.info %}
        <div class="entry">
          <div class="entry-header">
            <span class="date-badge">{{ exp.time }}</span>
            <span class="entry-role">{{ exp.role }}</span>
          </div>
          <div class="entry-location">📍 {{ exp.company }}</div> 
          <p>{{ exp.details | markdownify }}</p>
        </div>
      {% endfor %}
    </section>

    <section id="education" class="cv-card">
      <h2>{{ site.data.cv.education.title }}</h2>
      {% for edu in site.data.cv.education.info %}
        <div class="entry">
          <div class="entry-header">
            <span class="date-badge">{{ edu.time }}</span>
            <span class="entry-role">{{ edu.degree }}</span>
          </div>
          <div class="entry-location"> {{ edu.university }}</div>
          <p>{{ edu.details | markdownify }}</p>
        </div>
      {% endfor %}
    </section>

    <section id="skills" class="cv-card">
      <h2>Languages & Skills</h2>
      
      <h3>Languages</h3>
      <ul>
        {% for lang in site.data.cv.sidebar.languages.info %}
          <li><strong>{{ lang.idiom }}</strong> - {{ lang.level }}</li>
        {% endfor %}
      </ul>
      <br>

      <h3>Toolkit</h3>
      <ul>
        {% for skill in site.data.cv.skills.toolset %}
          <li><strong>{{ skill.name }}:</strong> {{ skill.type }}</li>
        {% endfor %}
      </ul>
    </section>

    <section id="publications" class="cv-card">
      <h2>{{ site.data.cv.publications.title }}</h2>
      <p>{{ site.data.cv.publications.intro | markdownify }}</p>
      <ul>
        {% for pub in site.data.cv.publications.papers %}
          <li style="margin-bottom: 15px;">
            <strong><a href="{{ pub.link }}" style="color: #2c7a63;">{{ pub.title }}</a></strong><br>
            <em>{{ pub.authors }}</em><br>
            <span style="color: #666; font-size: 0.9em;">{{ pub.conference }}</span>
          </li>
        {% endfor %}
      </ul>
    </section>

    <section id="profile" class="cv-card">
      <p>{{ site.data.cv['career-profile'].summary | markdownify }}</p>
    </section>

  </main>
</div>