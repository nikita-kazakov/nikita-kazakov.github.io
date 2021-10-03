---
title: Precision vs Scale in SQL
date: 2021-10-02
layout: post
permalink: /precision-scale-sql
tags:
    - sql
---

When I set a table column to decimal, I tend to forget the difference between precision and scale.

Precision is the number of significant digits and scale are the amount of digits after the decimal point.

Let's say we run migrations and add a price column with a precision of 5 and a scale of 2.

```
t.price :pre_tax_total, precision: 5, scale: 2
```

{% include image_center_caption.html
    caption = "Visualizing precision and scale."
    image = "/assets/images/2021/sql_scale.png"
%}

Let's experiment and see what happens when we update this column in Rails console:

```
Item.update(price: 500.50)
=> 500.50

Item.update(price: 40.50)
=> 40.50 # It will accept values with precision 5 or lower.

Item.update(price: 500.9911)
=> 500.99 # Notice it rounds it to 2 digits after the decimal.

Item.update(price: 500.999999)
=> 501.00 # Rounds up.

Item.update(price: 999.99)
=> 999.99 # This is the maximum value this column takes.

Item.update(price: 1000.00)
=> # ERROR. You exceeded precision 5. 
```

The column accepts numbers with a lower precision. The column will round up decimal value (scale) if it is more than 2 digits in our example. The column will return an error if the number of digits (precision) is higher than 5.
