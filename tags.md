---
layout: page
title: Tags
permalink: /tags/
---

You can found specific post by tag.

{% for tag in site.data.tags %}

<h4 align="left"><font color="MediumTurquoise">{{ tag["name"] }}</font></h4>
<div>
	{% if site.tags[tag["slug"]] %}
        {% for post in site.tags[tag["slug"]] %}
            <a href="{{ post.url }}"><font color="Green">{{ post.title }}</font></a><br>
        {% endfor %}
    {% else %}
        <i>There are no posts for this tag.</i>
    {% endif %}
</div>

{% endfor %}

<br>