---
layout: page
title: "Helpers"
---

Below are the helpers I use with this static website.

## Center Image and Caption

{% raw %}
```html
{% include image_center_caption.html 
    caption = "This is an awesome caption bro."
    image = "/assets/images/2014-09-03/wwwimage.jpeg"
    alt = "image showing www"
%}
```
{% endraw %}

# Youtube video helper
{% raw %}
```
{% include embed_youtube.html id="IeRdy6LrOAI" %}
```
{% endraw %}

# Em Dash
Simply type three dashes "-" in markdown.