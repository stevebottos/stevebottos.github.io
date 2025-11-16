---
layout: default
title: Home
---

# Hello :wave:
I've spent the past 6 years working as a Machine Learning Engineer at progressively higher levels of responsibility across a handful of startups. I am currently a Lead at [Kibeam](https://kibeam.com/), where I oversee everything from Ops to edge model training/deployment to LLMs, and everything in between. In my spare time, I tinker with whatever else interests me, and that gets posted here.
#### Some stuff I'm interested in right now...
- Multimodal ML, especially video understanding
- Heirerchical Reasoning Models
- LLMs, and making them less unwieldy
- Prefix tuning/ QLoRa, improving VLM performance on spatial tasks
- Reinforcement Learning

---

## Recent Posts

{% for post in site.posts limit:3 %}
  <article class="post-preview">
    <h3><a href="{{ post.url | relative_url }}">{{ post.title }}</a></h3>
    <time datetime="{{ post.date | date_to_xmlschema }}">{{ post.date | date: "%B %d, %Y" }}</time>
    {% if post.tags and post.tags.size > 0 %}
      <div class="post-tags">
        {% for tag in post.tags %}
          <span class="tag">{{ tag }}</span>
        {% endfor %}
      </div>
    {% endif %}
    {% if post.excerpt %}
      <p>{{ post.excerpt }}</p>
      <p><a href="{{ post.url | relative_url }}" class="read-more">read more →</a></p>
    {% endif %}
  </article>
{% endfor %}

<p style="text-align: center; margin-top: 20px;"><a href="{{ site.baseurl }}/posts">View all posts →</a></p>
