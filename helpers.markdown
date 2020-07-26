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

# Linking to other posts / pages

{% raw %}
```
[how to submit PDUs]({% link _posts/2020-02-16-how-to-submit-pdus-to-pmi-to-renew-your-pmp.md %})
```
{% endraw %}

# Alerts
{% raw %}
```
**2020 Update**: I don't use Pug templating anymore. I do use [HAML](https://haml.info) with Ruby and Ruby on Rails and it is very similar.
{: .notice--info}
```
{% endraw %}

**2020 Update**: I don't use Pug templating anymore. I do use [HAML](https://haml.info) with Ruby and Ruby on Rails and it is very similar.
{: .notice--info}

**Watch out!** This paragraph of text has been [emphasized](#) with the `{: .notice}` class.
{: .notice}

**Watch out!** This paragraph of text has been [emphasized](#) with the `{: .notice--primary}` class.
{: .notice--primary}

**Watch out!** This paragraph of text has been [emphasized](#) with the `{: .notice--accent}` class.
{: .notice--accent}

**Watch out!** This paragraph of text has been [emphasized](#) with the `{: .notice--info}` class.
{: .notice--info}

**Watch out!** This paragraph of text has been [emphasized](#) with the `{: .notice--warning}` class.
{: .notice--warning}

**Watch out!** This paragraph of text has been [emphasized](#) with the `{: .notice--success}` class.
{: .notice--success}

**Watch out!** This paragraph of text has been [emphasized](#) with the `{: .notice--danger}` class.
{: .notice--danger}