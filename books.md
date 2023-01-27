---
layout: page
title: Books
description: My opinions on books I have read
---

Books that I have read for work / professional development and that I would recommend

{% for category in site.data.books %}
{% assign items = category[1] | sort_natural: "name" %}
### {{ category[0] | capitalize }}:
{% for item in items %}
* [{{ item.name }}]({{ item.link }}){:target="_blank"}
  * {{ item.description }}
{% endfor %}
{% endfor %}

----

{% if site.comments_repo %}
{% include comments.html %}
{% endif %}
