---
layout: home
title: Welcome to Miguel's Learning in Public Journal
---

I'm Miguel, and this is where I document my discoveries throughout my technical journey. From cloud infrastructure to AI tools, I share practical insights and hands-on experiences.

## Recent Posts

{% for post in site.posts limit:5 %}
- [{{ post.title }}]({{ post.url }}) - {{ post.date | date: "%B %d, %Y" }}
{% endfor %}

## What You'll Find Here

- **Infrastructure as Code**: Real-world experiences with Terraform, Azure Bicep, and cloud automation
- **AI & Development Tools**: Practical guides on GitHub Copilot, Microsoft Fabric, and emerging technologies  
- **Certifications & Learning**: Study guides, tips, and resources for technical certifications
- **DevOps & Security**: Best practices for secure, scalable development workflows

---

*Happy Building!* 🚀