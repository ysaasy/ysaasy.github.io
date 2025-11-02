---
layout: base.njk
permalink: archive.html
title: archive
publish: true
modified: 2025-11-02
---
# {{ title }}

{% assign top_posts = collections.posts | reverse %}
{%- for post in top_posts-%}
<a href="{{ post.data.permalink }}">{{ post.data.date | formatDate }} » {{ post.data.title }}</a><br>
{% endfor %}