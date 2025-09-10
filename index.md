---
layout: home
title: Welcome to Miguel's Learning in Public Journal
---

## Blog Posts

<div class="featured-posts">
  {%- for post in site.posts -%}
    <article class="featured-post">
      {% if post.image %}
        <div class="featured-image">
          <img src="{{ post.image | relative_url }}" alt="{{ post.title }}">
        </div>
      {% endif %}
      <div class="featured-content">
        <h3><a href="{{ post.url | relative_url }}">{{ post.title }}</a></h3>
        <p class="post-meta">{{ post.date | date: "%B %d, %Y" }}</p>
        <p>{{ post.excerpt | strip_html | truncatewords: 50 }}</p>
        <a href="{{ post.url | relative_url }}" class="read-more">Read more →</a>
      </div>
    </article>
  {%- endfor -%}
</div>

## What You'll Find Here

<div class="topics-grid">
  <div class="topic-card">
    <h3>🏗️ Infrastructure as Code</h3>
    <p>Real-world experiences with Terraform, Azure Bicep, and cloud automation</p>
  </div>
  <div class="topic-card">
    <h3>🤖 AI & Development Tools</h3>
    <p>Practical guides on GitHub Copilot, Microsoft Fabric, and emerging technologies</p>
  </div>
  <div class="topic-card">
    <h3>📚 Certifications & Learning</h3>
    <p>Study guides, tips, and resources for technical certifications</p>
  </div>
  <div class="topic-card">
    <h3>🔒 DevOps & Security</h3>
    <p>Best practices for secure, scalable development workflows</p>
  </div>
</div>

---

*Happy Building!* 🚀