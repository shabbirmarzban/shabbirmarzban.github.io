---
layout: default
---
[![LinkedIn](https://img.shields.io/badge/linkedin-%230077B5.svg?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/smarzban/) [![WhatsApp](https://img.shields.io/badge/WhatsApp-25D366?style=for-the-badge&logo=whatsapp&logoColor=white)](https://wa.me/31685343018)

<h1>Latest Posts</h1>

<ul>
    {% for post in site.posts %}
    <li>
        <h2><a href="{{ post.url }}">{{ post.title }}</a></h2>
        {{ post.excerpt }}
    </li>
    {% endfor %}
</ul>

<object data="./resume.pdf" type="application/pdf" width="700px" height="700px">
    <embed src="./resume.pdf">
        <p>This browser does not support PDFs. Please download the PDF to view it: <a href="./resume.pdf">Download PDF</a>.</p>
    </embed>
</object>