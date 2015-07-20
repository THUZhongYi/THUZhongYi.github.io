---
layout: page
title: Tags
permalink: /tags/
---

{% for tag in site.data.tags %}
<div class="by-tag">
	<font color="MidnightBlue" size="4.5px">{{ tag["name"] }}</font><br>
	{% if site.tags[tag["slug"]] %}
    	{% for post in site.tags[tag["slug"]] %}
    	<a href="{{ post.url }}"><font color="Green">{{ post.title }}</font></a>  <span class="post-meta"><i>{{ post.date | date: "%b %-d, %Y" }}</i></span><br>
    	{% endfor %}
	{% else %}
    	<i>There are no posts for this tag.</i><br>
	{% endif %}
	<br>
</div>
{% endfor %}

<br>