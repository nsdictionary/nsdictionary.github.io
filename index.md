---
layout: home
---

<div class="text">
    {% for post in site.posts %}
    <div class="article">
        <a href="{{ post.url }}">{{ post.title }}</a>
        <span class="article-information">
            <small>{{ post.date | date_to_string }}</small>
        </span>
    </div>
    {% endfor %}
</div>
