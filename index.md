---
title: Online Hosted Instructions
permalink: index.html
layout: home
---

## Exercises to support Microsoft Learn modules

{% assign exercises = site.pages | where_exp:"page", "page.url contains '/Instructions/Exercises'" %}
{% for activity in exercises  %}
- [{{ activity.lab.title }}]({{ site.github.url }}{{ activity.url }}) |
{% endfor %}
