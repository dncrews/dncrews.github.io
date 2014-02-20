---
layout: page
title: Stuff I Think About
tagline: "You're welcome, world"
---
{% include JB/setup %}

{% for post in site.posts %}
  ![dncrews](https://0.gravatar.com/avatar/eff4197983d28e75d3e450583c06dda7?d=https%3A%2F%2Fidenticons.github.com%2F59d133ec146115db1c8b9de416672894.png&r=x&s=15)
  [dncrews](http://github.com/dncrews) {{ post.date | date_to_string }} <br>
  Tags: {% for tag in post.tags %} [{{ tag }}](/tags.html#{{ tag }});  {% endfor %}
# [{{ post.title }}]({{ post.url }})
  
  <summary>{{ post.content | more: "excerpt" }}</summary>
  [More…]({{ post.url }})

{% endfor %}
