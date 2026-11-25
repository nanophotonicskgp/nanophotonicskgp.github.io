---
layout: page
permalink: /members/
title: Members
description: Group members and alumni.
nav: true
nav_order: 7
---

{% assign groups = site.members | sort: "group_rank" | map: "group" | uniq %}
{% for group in groups %}
<h2>{{ group }}</h2>
  {% assign members = site.members | sort: "year" | where: "group", group %}
  <div class="row row-cols-1 row-cols-sm-2 row-cols-md-3 g-4">
    {% for member in members %}
    <div class="col mb-4">
      <div class="card h-100 {% if member.inline == false %}hoverable{% endif %}">
        <img src="{{ '/assets/img/' | append: member.profile.image | relative_url }}" class="card-img-top img-fluid" alt="{{ member.profile.name }}" style="object-fit: cover; height: 250px;" />
        <div class="team card-body d-flex flex-column">
          {% if member.inline == false %}
            {% if member.external == true %}
              <a href="{{ member.profile.website }}">
            {% else %}
              <a href="{{ member.url | relative_url }}">
            {% endif %}
          {% endif %}
            <h5 class="card-title">{{ member.profile.name }}</h5>
            {% if member.profile.position %}
              {% if member.profile.team-position %}
                <h6 class="card-subtitle mb-2 text-muted">{{ member.profile.team-position }}</h6>
              {% else %}
                <h6 class="card-subtitle mb-2 text-muted">{{ member.profile.position }}</h6>
              {% endif %}
            {% endif %}
            <p class="card-text">{{ member.teaser }}</p>
          {% if member.inline == false %}</a>{% endif %}
          <div class="mt-auto">
            <div class="card-links mb-2">
              {% if member.profile.email %}
                <a href="mailto:{{ member.profile.email }}" class="card-link"><i class="fas fa-envelope"></i></a>
              {% endif %}
              {% if member.profile.phone %}
                <a href="tel:{{ member.profile.phone }}" class="card-link"><i class="fas fa-phone"></i></a>
              {% endif %}
              {% if member.profile.orcid %}
                <a href="https://orcid.org{{ member.profile.orcid }}" class="card-link" target="_blank"><i class="fab fa-orcid"></i></a>
              {% endif %}
              {% if member.profile.twitter %}
                <a href="https://twitter.com{{ member.profile.twitter }}" class="card-link" target="_blank"><i class="fab fa-twitter"></i></a>
              {% endif %}
              {% if member.profile.github %}
                <a href="https://github.com{{ member.profile.github }}" class="card-link" target="_blank"><i class="fab fa-github"></i></a>
              {% endif %}
              {% if member.profile.linkedin %}
                <a href="https://linkedin.com{{ member.profile.linkedin }}" class="card-link" title="LinkedIn"><i class="fa-brands fa-linkedin"></i></a>
              {% endif %}  
              {% if member.profile.researchgate %}
                <a href="https://researchgate.net{{ member.profile.researchgate }}" class="card-link" target="_blank"><i class="ai ai-researchgate"></i></a>
              {% endif %}  
              {% if member.profile.gscholar %}
                <a href="https://google.com{{ member.profile.gscholar }}" class="card-link" target="_blank"><i class="ai ai-google-scholar"></i></a>
              {% endif %}  
              {% if member.profile.website %}
                <a href="{{ member.profile.website }}" class="card-link" target="_blank"><i class="fas fa-globe"></i></a>
              {% endif %}     
              {% if member.profile.cv %}
                <a
                  {% if member.profile.cv contains '://' %}
                    href="{{ member.profile.cv }}"
                  {% else %}
                    href="{{ member.profile.cv | prepend: 'assets/pdf/' | relative_url }}"
                  {% endif %}
                  target="_blank"
                  rel="noopener noreferrer"
                  class="card-link"
                >
                  <i class="fas fa-file-pdf"></i>
                </a>
              {% endif %}
            </div>
            {% if member.profile.address %}
            <p class="card-text">
              <small class="text-muted"><i class="fas fa-thumbtack"></i> {{ member.profile.address | replace: '<br />', ', ' }}</small>
            </p>
            {% endif %}
          </div>
        </div>
      </div>
    </div>
    {% endfor %}
  </div>
{% endfor %}
