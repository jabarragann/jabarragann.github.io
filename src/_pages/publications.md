---
layout: archive
title: "Publications"
permalink: /publications/
author_profile: true
---

{% if site.author.googlescholar %}
You can also find my articles on <a href="{{ site.author.googlescholar }}">my Google Scholar profile</a>.
{% endif %}

## Journal Articles

{% bibliography --query @article %}

## Conference Papers

{% bibliography --query @inproceedings %}
