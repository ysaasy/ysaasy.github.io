---
layout: base.njk
permalink: index.html
title: ""
nesting: "./"
date: 
---
{% block Head %}
<style>
	.boxd-container {
	
	  max-width: 600px;
	  margin: 2rem auto;
	  padding: 1rem;
	  font-family: Arial;
	}
	
	.boxd-entry {
	  display: flex;
	  align-items: flex-start;
	  margin-bottom: 0rem;
	  gap: 1rem;
	  text-align: left;
	}
	
	.boxd-entry img {
	  width: 100px;
	  border-radius: 4px;
	  position: relative;
	  top: -14px;
	}
	
	.boxd-content {
	  flex: 1;
	}
	
	.boxd-content a {
	  font-weight: 600;
	  color: #222;
	  text-decoration: none;
	}
	
	.boxd-content a:hover {
	  text-decoration: underline;
	}
	
	.boxd-date {
	  font-size: 0.85rem;
	  color: #777;
	  margin-top: 0.25rem;
	}
	
	.boxd-review {
	  margin-top: -0.6rem;
	  font-size: 0.85rem;
	}
</style>
{% endblock%}

# the page

i still don't know what to write here.

## recent entries
<div id="recentpostlistdiv">
  {% assign top_posts = collections.posts | reverse %}
	{%- for post in top_posts limit:3 -%}
		<a href="{{ post.data.permalink }}">{{ post.data.title }}</a><br>
	{% endfor %}
</div>
<a href="/archives.html">...</a>

## recently played
<iframe src="https://petrapixel.neocities.org/widgets/lastfm?center=1&marquee=1&font-family=Arial&font-size=16px&color=#000&username=ysaasy&swapPositions=1&delimiter=-&underline=0" frameborder="0" height="20" title="Last.Fm Status"></iframe>

<div id="letterboxd-diary" class="boxd-container" width="80%">

<script>
fetch("/boxd.json")
  .then(res => res.json())
  .then(entries => {
    const container = document.getElementById("letterboxd-diary");
    let html = "<h2>recently watched</h2>";

    entries.forEach(entry => {
      const date = new Date(entry.date);
      const formattedDate = date.toLocaleDateString(undefined, {
        year: "numeric",
        month: "short",
        day: "numeric"
      });

      html += `
        <div class="boxd-entry">
          ${entry.poster ? `<img src="${entry.poster}" alt="Poster for ${entry.title}">` : ""}
          <div class="boxd-content">
            <a href="${entry.link}" target="_blank">${entry.title}</a>
            <div class="boxd-date">${formattedDate}</div>
            ${entry.review ? `<div class="boxd-review">${entry.review}</div>` : ""}
          </div>
        </div>
      `;
    });

    container.innerHTML = html;
  })
  .catch(err => {
    document.getElementById("letterboxd-diary").innerText = "Error loading diary.";
    console.error(err);
  });
</script>