---
layout: page
permalink: /team.html
title: Team
page-title: HSE Lab
description: Members of the Health Systems Engineering Laboratory (HSE Lab).
nav: true
nav_order: 8
nav_rank:
---

<style>
.team-section {
  margin-bottom: 3rem;
}

.team-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(320px, 1fr));
  gap: 1.5rem;
  margin-top: 1rem;
}

.team-card {
  background: #fff;
  border: 1px solid rgba(0,0,0,0.08);
  border-radius: 18px;
  overflow: hidden;
  box-shadow: 0 8px 24px rgba(0,0,0,0.06);
  transition: transform 0.2s ease, box-shadow 0.2s ease;
  display: flex;
  flex-direction: column;
  height: 100%;
}

.team-card:hover {
  transform: translateY(-4px);
  box-shadow: 0 14px 30px rgba(0,0,0,0.10);
}

.team-card-img-wrap {
  width: 100%;
  aspect-ratio: 4 / 3;
  overflow: hidden;
  background: #f6f6f6;
}

.team-card-img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  display: block;
}

.team-card-body {
  padding: 1.2rem 1.2rem 1rem 1.2rem;
  display: flex;
  flex-direction: column;
  gap: 0.6rem;
  flex: 1;
}

.team-card-name {
  margin: 0;
  font-size: 1.2rem;
  line-height: 1.3;
}

.team-card-role {
  margin: 0;
  font-size: 0.95rem;
  font-weight: 600;
  color: #666;
}

.team-card-position {
  margin: 0;
  font-size: 0.95rem;
  color: #333;
}

.team-card-bio {
  margin: 0.2rem 0 0 0;
  font-size: 0.95rem;
  line-height: 1.6;
  color: #444;
}

.team-card-links {
  display: flex;
  flex-wrap: wrap;
  gap: 0.75rem;
  margin-top: 0.4rem;
  font-size: 0.92rem;
}

.team-card-links a {
  text-decoration: none;
}

.team-card-address {
  margin-top: auto;
  padding-top: 0.5rem;
  font-size: 0.9rem;
  color: #777;
  line-height: 1.5;
  border-top: 1px solid rgba(0,0,0,0.06);
}
</style>

{% assign groups = site.members | sort: "group_rank" | map: "group" | uniq %}

{% for group in groups %}
  {% assign members = site.members | sort: "group_order" | where: "group", group %}

  <section class="team-section">
    <h2>{{ group }}</h2>

    <div class="team-grid">
      {% for member in members %}
        <div class="team-card">
          {% if member.profile.image %}
            <div class="team-card-img-wrap">
              <img
                class="team-card-img"
                src="{{ '/assets/img/' | append: member.profile.image | relative_url }}"
                alt="{{ member.profile.name }}"
              >
            </div>
          {% endif %}

          <div class="team-card-body">
            <h3 class="team-card-name">{{ member.profile.name }}</h3>

            {% if member.group %}
              <p class="team-card-role">{{ member.group | replace: "-", " " }}</p>
            {% endif %}

            {% if member.profile.team-position %}
              <p class="team-card-position">{{ member.profile.team-position }}</p>
            {% elsif member.profile.position %}
              <p class="team-card-position">{{ member.profile.position }}</p>
            {% endif %}

            {% if member.teaser %}
              <p class="team-card-bio">{{ member.teaser | strip_html }}</p>
            {% endif %}

            <div class="team-card-links">
              {% if member.profile.email %}
                <a href="mailto:{{ member.profile.email }}">Email</a>
              {% endif %}
              {% if member.profile.website %}
                <a href="{{ member.profile.website }}" target="_blank" rel="noopener noreferrer">Website</a>
              {% endif %}
              {% if member.profile.orcid %}
                <a href="https://orcid.org/{{ member.profile.orcid }}" target="_blank" rel="noopener noreferrer">ORCID</a>
              {% endif %}
              {% if member.profile.github %}
                <a href="https://github.com/{{ member.profile.github }}" target="_blank" rel="noopener noreferrer">GitHub</a>
              {% endif %}
            </div>

            {% if member.profile.address %}
              <div class="team-card-address">
                {{ member.profile.address | replace: '
', '<br>' }}
              </div>
            {% endif %}
          </div>
        </div>
      {% endfor %}
    </div>
  </section>
{% endfor %}
