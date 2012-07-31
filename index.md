---
layout: page
title: Underflow by Jacob
tagline: Creative Passion
---
{% include JB/setup %}
<div>
  {{ paginator.page }}
</div>
{% for post in site.posts %}
{% capture pageurl %}{{ post.url }}{% endcapture %}
{% if forloop.index <= 4 %}
<div class="post-entry">
<h1  class="post-entry-title"><a href="{{ pageurl }}">{{ post.title }}</a></h1>
<div class="post-entry-date">{{ post.date | date: "%h %d, %Y" }}</div>
{% if post.imageurl %}<div class="post-entry-image"><img src="{{ post.imageurl }}" alt="Post Image"/></div>{% endif %}
<div class="post-entry-content">{{ post.content | strip_html | truncatewords:50 }}</div>
<div class="post-entry-more"><a href="{{ pageurl }}">more...</a></div>
</div>
<hr  class="post-entry-rule"/>
{% endif %}
{% endfor %}
