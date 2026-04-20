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
details {
  margin-bottom: 1.5rem;
  border-bottom: 1px solid #eaeaea;
  padding-bottom: 0.5rem;
}

details summary {
  cursor: pointer;
  font-weight: 600;
  font-size: 1.4rem;
  list-style: none;
  display: flex;
  align-items: center;
}

details summary::before {
  content: "▶";
  font-size: 0.9rem;
  margin-right: 0.6rem;
  transition: transform 0.2s ease;
}

details[open] summary::before {
  content: "▼";
}

details summary:hover {
  opacity: 0.8;
}

.card {
  margin-top: 1rem;
}
</style>

{% assign groups = site.members | sort: "group_rank" | map: "group" | uniq %}

{% for group in groups %}
<details>
  <summary>{{ group }}</summary>

  {% assign members = site.members | sort: "group_order" | where: "group", group %}
  
  {% for member in members %}
  <div id="{{ member.profile.name | slugify }}">
    <div class="card {% if member.inline == false %}hoverable{% endif %}">
      <div class="row no-gutters">
        
        <div class="col-sm-4 col-md-3">
          <img src="{{ '/assets/img/team/' | append: member.profile.image | relative_url }}" 
               class="card-img img-fluid" 
               alt="{{ member.profile.name }}" />
        </div>

        <div class="team col-sm-8 col-md-9">
          <div class="card-body">
            
            <h5 class="card-title">{{ member.profile.name }}</h5>

            {% if member.profile.position %}
              {% if member.profile.team-position %}
                <h6 class="card-subtitle mb-2 text-muted">{{ member.profile.team-position }}</h6>
              {% else %}
                <h6 class="card-subtitle mb-2 text-muted">{{ member.profile.position }}</h6>
              {% endif %}
            {% endif %}

            <p class="card-text">
              {{ member.teaser }}
            </p>

            {% if member.profile.email %}
              <a href="mailto:{{ member.profile.email }}" class="card-link"><i class="fas fa-envelope"></i></a>
            {% endif %}
            {% if member.profile.phone %}
              <a href="tel:{{ member.profile.phone }}" class="card-link"><i class="fas fa-phone"></i></a>
            {% endif %}
            {% if member.profile.orcid %}
              <a href="https://orcid.org/{{ member.profile.orcid }}" class="card-link" target="_blank"><i class="fab fa-orcid"></i></a>
            {% endif %}
            {% if member.profile.twitter %}
              <a href="https://twitter.com/{{ member.profile.twitter }}" class="card-link" target="_blank"><i class="fab fa-twitter"></i></a>
            {% endif %}
            {% if member.profile.github %}
              <a href="https://github.com/{{ member.profile.github }}" class="card-link" target="_blank"><i class="fab fa-github"></i></a>
            {% endif %}
            {% if member.profile.website %}
              <a href="{{ member.profile.website }}" class="card-link" target="_blank"><i class="fas fa-globe"></i></a>
            {% endif %}

            <p class="card-text">
              <small class="text-muted">
                <i class="fas fa-thumbtack"></i> 
                {{ member.profile.address | replace: '<br />', ', ' }}
              </small>
            </p>

          </div>
        </div>

      </div>
    </div>
  </div>
  {% endfor %}

</details>
{% endfor %}
