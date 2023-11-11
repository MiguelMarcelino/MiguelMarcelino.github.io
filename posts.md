---
layout: page
title: Posts
permalink: /posts/
---

{{include template_trimmer.js}}

<ul>
  {% for post in site.posts %}
    <div>
      <a href="{{ post.url }}">
        <h2>{{ post.title }}</h2>
      </a>
      <p> 
          <time datetime="{{ post.date | date: "%Y-%m-%d" }}">
              {{ post.date | date_to_long_string }}
          </time>
      </p>
    </div>
    <hr>
  {% endfor %}
</ul>
