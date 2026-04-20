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
.team-filters {
  margin-bottom: 1.5rem;
  display: flex;
  flex-wrap: wrap;
  gap: 0.5rem;
}

.team-filter-btn {
  border: 1px solid #d0d0d0;
  background: #f8f9fa;
  padding: 0.45rem 0.8rem;
  border-radius: 999px;
  cursor: pointer;
  font-size: 0.95rem;
  transition: all 0.2s ease;
}

.team-filter-btn:hover {
  background: #eceff1;
}

.team-filter-btn.active {
  background: #dbeafe;
  border-color: #93c5fd;
  font-weight: 600;
}

.team-group {
  margin-bottom: 1.5rem;
  border-bottom: 1px solid #eaeaea;
  padding-bottom: 0.5rem;
}

.team-group summary {
  cursor: pointer;
  font-weight: 600;
  font-size: 1.4rem;
  list-style: none;
  display: flex;
  align-items: center;
  user-select: none;
}

.team-group summary::-webkit-details-marker {
  display: none;
}

.team-group summary::before {
  content: "▶";
  font-size: 0.9rem;
  margin-right: 0.6rem;
  transition: transform 0.2s ease;
}

.team-group[open] summary::before {
  content: "▼";
}

.team-group summary:hover {
  opacity: 0.8;
}

.member-card-wrapper {
  margin-top: 1rem;
  scroll-margin-top: 90px;
}

.member-card-wrapper.highlight-target .card {
  border: 2px solid #93c5fd;
  box-shadow: 0 0 0 0.2rem rgba(147, 197, 253, 0.35);
  transition: box-shadow 0.3s ease, border 0.3s ease;
}

.card {
  margin-top: 1rem;
}

.team-hidden {
  display: none !important;
}
</style>

{% assign groups = site.members | sort: "group_rank" | map: "group" | uniq %}

<div class="team-filters">
  <button class="team-filter-btn active" data-filter="all">All</button>
  {% for group in groups %}
    <button class="team-filter-btn" data-filter="{{ group | slugify }}">{{ group }}</button>
  {% endfor %}
</div>

{% for group in groups %}
<details class="team-group" data-group="{{ group | slugify }}">
  <summary>{{ group }}</summary>

  {% assign members = site.members | sort: "group_order" | where: "group", group %}

  {% for member in members %}
  <div id="{{ member.profile.name | slugify }}" class="member-card-wrapper">
    <div class="card {% if member.inline == false %}hoverable{% endif %}">
      <div class="row no-gutters">

        <div class="col-sm-4 col-md-3">
          <img
            src="{{ '/assets/img/team/' | append: member.profile.image | relative_url }}"
            class="card-img img-fluid"
            alt="{{ member.profile.name }}"
          />
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

<script>
document.addEventListener("DOMContentLoaded", function () {
  const buttons = document.querySelectorAll(".team-filter-btn");
  const groups = document.querySelectorAll(".team-group");

  function applyFilter(filter) {
    buttons.forEach(btn => {
      btn.classList.toggle("active", btn.dataset.filter === filter);
    });

    groups.forEach(group => {
      const matches = filter === "all" || group.dataset.group === filter;
      group.classList.toggle("team-hidden", !matches);
    });
  }

  buttons.forEach(button => {
    button.addEventListener("click", function () {
      const filter = this.dataset.filter;
      applyFilter(filter);
    });
  });

  function clearHighlights() {
    document.querySelectorAll(".member-card-wrapper.highlight-target").forEach(el => {
      el.classList.remove("highlight-target");
    });
  }

  function openAndFocusHashTarget() {
    const hash = window.location.hash;
    if (!hash) return;

    const target = document.querySelector(hash);
    if (!target) return;

    const parentGroup = target.closest(".team-group");
    if (!parentGroup) return;

    applyFilter("all");
    parentGroup.open = true;

    clearHighlights();
    target.classList.add("highlight-target");

    setTimeout(() => {
      target.scrollIntoView({ behavior: "smooth", block: "start" });
    }, 150);

    setTimeout(() => {
      target.classList.remove("highlight-target");
    }, 4000);
  }

  openAndFocusHashTarget();

  window.addEventListener("hashchange", function () {
    openAndFocusHashTarget();
  });
});
</script>
