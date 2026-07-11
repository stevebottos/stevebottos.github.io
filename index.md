---
layout: default
title: Home
---

# Hello :wave:
For the past 8 years I've been doing ML across a handful of companies. Right now I'm at [Engine](https://engine.com/). I'm lucky to enjoy what I do enough to pick up some personal research projects when I'm not at my day job. I try to catalog those endeavors here, with some shorter posts landing on [my X](https://x.com/home) or [LinkedIn](https://www.linkedin.com/in/stephen-bottos/). 

#### Some stuff I'm interested in right now...
I'm pretty focused on small vision/language models right now. I'm wondering how to improve the performance of visual-RAG from an engineering and cost standpoint. 

#### AI in my posts...
I try to write everything by hand. Sometimes I want to get a post written up but don't have the time to hand-write it entirely. It should be pretty obvious when AI is involved but I'll mention it in my posts anyway.

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
