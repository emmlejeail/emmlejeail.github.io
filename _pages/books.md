---
layout: page
title: Book Reviews
permalink: /books
description: My opinions on books I have read for professional / carreer development as a software engineer
---

My opinion on books that I have read for work / professional development and that I would recommend.

{% for book in site.data.books %}
* [*{{ book.title }}*{% if book.author %} by {{ book.author }}{% endif %}]({{ book.link }}){:target="_blank"}
{% if book.rating %}  * My rating: {{ book.rating }}{% endif %}
{% if book.summary %}  * Summary: {{ book.summary }}{% endif %}
{% endfor %}
