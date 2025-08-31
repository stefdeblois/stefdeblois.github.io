```markdown

layout: default
title: Blog

My Articles

{% for post in site.posts %}
    [{{ post.title }}]({{ post.url }})
{% endfor %}
