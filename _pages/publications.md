---
layout: archive
title: "Publications"
permalink: /publications/
author_profile: true
---

{% if site.author.googlescholar %}
  <p class="wordwrap">You can also find my articles on <a href="{{site.author.googlescholar}}">my Google Scholar profile</a>.</p>
  <p>* denotes equal contribution.</p>  
{% endif %}

{% include base_path %}

{% for post in site.publications reversed %}
  {% include archive-single-pub.html %}
{% endfor %}
