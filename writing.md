---
layout: page
title: Writing
---

Empirical notes and research writeups. All code and data available on [GitHub](https://github.com/JoelNithishKumar).

---

{% if site.posts.size > 0 %}
<ul class="post-list">
{% for post in site.posts %}
  <li>
    <a class="post-title-link" href="{{ post.url | relative_url }}">{{ post.title }}</a>
    <p class="post-meta">
      {{ post.date | date: "%B %-d, %Y" }}
      &nbsp;
      {% for tag in post.tags %}<span class="tag">{{ tag }}</span>{% endfor %}
      {% if post.repo %}
        &nbsp;·&nbsp; <a href="{{ post.repo }}" target="_blank" rel="noopener">Code</a>
      {% endif %}
    </p>
  </li>
{% endfor %}
</ul>
{% else %}
<p class="muted">First article coming soon.</p>
{% endif %}
