---
layout: base.njk
permalink: notes.html
title: notes
publish: true
modified: 2025-11-08
---
# {{ title }}
everything i've been thinking
<br>



{% assign top_notes = collections.notes | reverse %}
{%- for post in top_notes-%}
<a href="{{ post.data.page.url}}">{{ post.data.title }}</a><br>
{% endfor %}

