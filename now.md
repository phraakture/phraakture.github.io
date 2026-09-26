---
layout: default
title: "Now"
permalink: /now/
---

<!-- A short note on where you are and what you're focused on right now. -->

- Where I am and what I'm working on.

## Currently reading

<ul>
{% for book in site.data.currently_reading %}
  <li><a href="{{ book.url }}"><em>{{ book.title | escape }}</em></a> by {{ book.author | escape }}</li>
{% else %}
  <li>Nothing at the moment.</li>
{% endfor %}
</ul>
