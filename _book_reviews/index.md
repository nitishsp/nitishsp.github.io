---
layout: default
permalink: "/book_reviews/"
---
<div>
  <p>I recently started writing book reviews. This was mostly to improve my writing(and, to some extent, reading) skills. Here are a few of them:</p>

  {% for review in site.book_reviews %}
    {% if review.title != "Index" %}
      <a href="{{ review.url }}" style=""><img src="{{ review.goodreads_cover }}" alt="{{ review.book }}" width="200" height="300"></a>
    {% endif %}
  {% endfor %}
</div>