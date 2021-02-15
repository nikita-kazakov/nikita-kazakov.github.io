---
layout: page
title: "Helpers"
---

Below are the helpers I use with this static website.

# Center Image and Caption

{% raw %}
```html
{% include image_center_caption.html 
    caption = "This is an awesome caption bro."
    image = "/assets/images/2014-09-03/wwwimage.jpeg"
    alt = "image showing www"
%}
```
{% endraw %}

# Table that overflows horizontally

For example, my SQL tables are big and need to overflow-x but I don't want the entire page to overflow. 
You need to wrap a div around the table like this.

Make sure you leave **empty spaces** between the divs and the kramdown table or otherwise it won't work.


{% raw %}
```
<div class=".table--overflow" markdown="block">

| id |                  name                   | album_id | media_type_id | genre_id |                                composer                                | milliseconds |  bytes   | unit_price | created_at | updated_at |
|----|-----------------------------------------|----------|---------------|----------|------------------------------------------------------------------------|--------------|----------|------------|------------|------------|
|  1 | For Those About To Rock (We Salute You) |        1 |             1 |        1 | Angus Young, Malcolm Young, Brian Johnson                              |       343719 | 11170334 |          0 | 05:37.6    | 05:37.6    |
|  2 | Balls to the Wall                       |        2 |             2 |        1 |                                                                        |       342562 |  5510424 |          0 | 05:37.6    | 05:37.6    |
|  3 | Fast As a Shark                         |        3 |             2 |        1 | F. Baltes, S. Kaufman, U. Dirkscneider & W. Hoffman                    |       230619 |  3990994 |          0 | 05:37.6    | 05:37.6    |
|  4 | Restless and Wild                       |        3 |             2 |        1 | F. Baltes, R.A. Smith-Diesel, S. Kaufman, U. Dirkscneider & W. Hoffman |       252051 |  4331779 |          0 | 05:37.6    | 05:37.6    |

</div>
```
{% endraw %}

Add the following scss to your project if you haven't already. It makes sure the table overflows and
ensure each table row does not wrap.

```scss
.table--overflow  {
  overflow-x: auto;
  table {
    white-space: nowrap;
  }
}
```

# Easily create ascii tables from csv
Use [ascii-tables](https://ozh.github.io/ascii-tables/) and output the style *Github Markdown* and paste it into your markdown.

If you're copying sql tables:
postico => csv => ascii-tables => markdown.

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