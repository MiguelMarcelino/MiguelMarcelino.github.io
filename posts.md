---
layout: page
title: Posts
permalink: /posts/
---

{{include template_trimmer.js}}

{% include parsers.html %}

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
      <p>
        <script>getSubstring("{{ post.content }}", 0, 200);</script>
      </p>
      <p>
        <script>getSubstring("asfassssssssssssssssssssssssssssssssssssssssss", 0, 200);</script>
      </p>
    </div>
  {% endfor %}
</ul>
