---
layout: page
title: Projects
---

<div class="posts">
  {% for post in paginator.posts %}
  <div class="post">
    <h1 class="post-title">
      <a href="{{ post.url }}">
        {{ post.title }}
      </a>
    </h1>

    <span class="post-date">{{ post.date | date_to_string }}</span>

    {{ post.content }}
  </div>
  {% endfor %}
</div>

### Gaze Tracking System
<a href="https://stevebottos.github.io/jupnotes/GazeTrackerWriteup/" target="_blank">Click here </a>for a writeup put together using Jupyter Notebooks detailing Version 1 of the Gaze Tracking System. <br/>

---

