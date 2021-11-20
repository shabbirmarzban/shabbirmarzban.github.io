---
layout: default
---
# Social links

[![LinkedIn](https://img.shields.io/badge/linkedin-%230077B5.svg?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/smarzban/) [![WhatsApp](https://img.shields.io/badge/WhatsApp-25D366?style=for-the-badge&logo=whatsapp&logoColor=white)](https://wa.me/31685343018)

# Blog posts

<ul>
    {% for post in site.posts %}
    <li>
        <h2><a href="{{ post.url }}">{{ post.title }}</a></h2>
        {{ post.excerpt }}
    </li>
    {% endfor %}
</ul>
