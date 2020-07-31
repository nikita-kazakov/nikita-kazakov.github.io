---
id: 6977
title: Object Oriented Objects Made Simple
date: 2020-02-24T00:23:48+00:00
author: Nikita Kazakov
layout: revision
guid: https://nikitakazakov.com/6941-revision-v1/
permalink: /6941-revision-v1/
---
Let&#8217;s break down what an object is in object oriented programming. An object could be anything but let&#8217;s ground ourselves with something simple.

Let&#8217;s use Jim as the object today.<figure class="wp-block-image size-large">

<img src="https://nikitakazakov.com/wp-content/uploads/2020/02/image-9.png" alt="" class="wp-image-6942" /> </figure> 

Just like any other human, Jim stores data in his brain.

I&#8217;m going to grossly over simplify the brain into two parts. Yes, it&#8217;s anatomically WRONG. We&#8217;re not learning biology here. This simplified model will help you understand how objects store data and communicate with other objects.

Below is Jim&#8217;s brain and the part of it that stores data about Jim has a circle around it.<figure class="wp-block-image size-large">

<img src="https://nikitakazakov.com/wp-content/uploads/2020/02/image-16-1024x487.png" alt="" class="wp-image-6956" srcset="https://nikitakazakov.com/wp-content/uploads/2020/02/image-16-1024x487.png 1024w, https://nikitakazakov.com/wp-content/uploads/2020/02/image-16-300x143.png 300w, https://nikitakazakov.com/wp-content/uploads/2020/02/image-16-768x365.png 768w, https://nikitakazakov.com/wp-content/uploads/2020/02/image-16.png 1354w" sizes="(max-width: 1024px) 100vw, 1024px" /> </figure> 

Unless Jim chooses to share his age or name with me, I won&#8217;t know it. All the data in his brain is **private to him**. I can&#8217;t dissect his brain and see what data he holds there. If that was the case, then none of us could lie.

All data inside the circle is isolated, or using a fancier programming vocabulary word, it is **ENCAPSULATED**. It is isolated from all things outside the circle.

If I meet Jim and just stare at him, I won&#8217;t know his name. I won&#8217;t know anything about him. We&#8217;ll just awkwardly stare at each other. I can&#8217;t telepathically get data from his brain.

If I ask Jim _what&#8217;s your name?_ — he needs the ability to to understand my question and respond to me.

That&#8217;s where the second part of our very simplified brain comes in. This part understands understands language. It is able to respond to questions. More importantly, it has direct access to the data in the data circle.<figure class="wp-block-image size-large">

<img src="https://nikitakazakov.com/wp-content/uploads/2020/02/image-18.png" alt="" class="wp-image-6958" srcset="https://nikitakazakov.com/wp-content/uploads/2020/02/image-18.png 946w, https://nikitakazakov.com/wp-content/uploads/2020/02/image-18-300x287.png 300w, https://nikitakazakov.com/wp-content/uploads/2020/02/image-18-768x734.png 768w" sizes="(max-width: 946px) 100vw, 946px" /> </figure> 

Stay with me, using this analogy we&#8217;ll understand how objects store data and how they understand messages and respond to them.

## Asking &#8220;What&#8217;s your name?&#8221;

Here&#8217;s what happens when you ask Jim&#8217;s name.

  1. Jim receives the question
  2. If the cortex circle understands the question, it can ask the data circle for Jim&#8217;s name.
  3. Data circle sends Jim&#8217;s name to the cortex.
  4. The cortex responds with &#8220;I&#8217;m Jim&#8221;.<figure class="wp-block-image size-large">

<img src="https://nikitakazakov.com/wp-content/uploads/2020/02/image-19-1024x523.png" alt="" class="wp-image-6959" srcset="https://nikitakazakov.com/wp-content/uploads/2020/02/image-19-1024x523.png 1024w, https://nikitakazakov.com/wp-content/uploads/2020/02/image-19-300x153.png 300w, https://nikitakazakov.com/wp-content/uploads/2020/02/image-19-768x392.png 768w, https://nikitakazakov.com/wp-content/uploads/2020/02/image-19-1536x784.png 1536w, https://nikitakazakov.com/wp-content/uploads/2020/02/image-19.png 1560w" sizes="(max-width: 1024px) 100vw, 1024px" /> </figure> 

The cortex is the middle man between you and Jim&#8217;s data. You can&#8217;t get to Jim&#8217;s data directly without first going through the cortex circle.

Let&#8217;s redraw the circles. The cortex circle will envelop the data circle like this:<figure class="wp-block-image size-large">

<img src="https://nikitakazakov.com/wp-content/uploads/2020/02/image-20-1024x623.png" alt="" class="wp-image-6960" srcset="https://nikitakazakov.com/wp-content/uploads/2020/02/image-20-1024x623.png 1024w, https://nikitakazakov.com/wp-content/uploads/2020/02/image-20-300x183.png 300w, https://nikitakazakov.com/wp-content/uploads/2020/02/image-20-768x467.png 768w, https://nikitakazakov.com/wp-content/uploads/2020/02/image-20.png 1288w" sizes="(max-width: 1024px) 100vw, 1024px" /> </figure> 

What happens if you ask a question that Jim&#8217;s cortex can&#8217;t understand? Let&#8217;s say you want to know Jim&#8217;s age but you ask in another language that he can&#8217;t understand.<figure class="wp-block-image size-large">

<img src="https://nikitakazakov.com/wp-content/uploads/2020/02/image-21-1024x657.png" alt="" class="wp-image-6961" srcset="https://nikitakazakov.com/wp-content/uploads/2020/02/image-21-1024x657.png 1024w, https://nikitakazakov.com/wp-content/uploads/2020/02/image-21-300x192.png 300w, https://nikitakazakov.com/wp-content/uploads/2020/02/image-21-768x492.png 768w, https://nikitakazakov.com/wp-content/uploads/2020/02/image-21.png 1282w" sizes="(max-width: 1024px) 100vw, 1024px" /> </figure> 

Even though Jim&#8217;s age is available in his data circle, the cortex circle cannot understand the question you just asked.

## Mapping an Object

An object in object oriented programming works very similarly as Jim did above. An object can be anything. Let&#8217;s say we have a cash register object. Just like Jim, an object that you create can have properties that you can specify. In this example, we created a cash amount of $200 as one property of this cash register. We can write as many as we want.<figure class="wp-block-image size-large">

<img src="https://nikitakazakov.com/wp-content/uploads/2020/02/image-22-1024x536.png" alt="" class="wp-image-6962" srcset="https://nikitakazakov.com/wp-content/uploads/2020/02/image-22-1024x536.png 1024w, https://nikitakazakov.com/wp-content/uploads/2020/02/image-22-300x157.png 300w, https://nikitakazakov.com/wp-content/uploads/2020/02/image-22-768x402.png 768w, https://nikitakazakov.com/wp-content/uploads/2020/02/image-22.png 1188w" sizes="(max-width: 1024px) 100vw, 1024px" /> </figure> 

When we ask an object for something and an object responds, that&#8217;s better understood as sending a message.

If I send a message to the cash register asking for the cash amount, what should happen?

Remember, we don&#8217;t have direct access to the cash data. To us the object properties are hidden. They are private to the object. They are encapsulated.<figure class="wp-block-image size-large">

<img src="https://nikitakazakov.com/wp-content/uploads/2020/02/image-23.png" alt="" class="wp-image-6963" srcset="https://nikitakazakov.com/wp-content/uploads/2020/02/image-23.png 638w, https://nikitakazakov.com/wp-content/uploads/2020/02/image-23-300x285.png 300w" sizes="(max-width: 638px) 100vw, 638px" /> </figure> 

The middle man circle that envelops the dark data circle is empty. The cash register object receives the **cash_amount?** message, it doesn&#8217;t know what to do with it.

Objects are not as smart as humans when making sense of what is asked of them. That&#8217;s where YOU come in. You have to specifically write the the messages that objects will understand and how they will respond to them.

In programming these messages are called **methods**.

Let&#8217;s say you write a **cash_sum?** method in the cash register object that will grab the cash value ($200) directly from the data circle and return it. You can now send a **cash_sum?** message to the cash register and it will know how to respond to you.<figure class="wp-block-image size-large">

<img src="https://nikitakazakov.com/wp-content/uploads/2020/02/image-24.png" alt="" class="wp-image-6965" srcset="https://nikitakazakov.com/wp-content/uploads/2020/02/image-24.png 634w, https://nikitakazakov.com/wp-content/uploads/2020/02/image-24-300x287.png 300w" sizes="(max-width: 634px) 100vw, 634px" /> </figure> 

## Methods

How do you know which messages (methods) an object should understand? Ask yourself, what should your object be able to do?

A cash register should be able to store cash (data) and you should be able to check the value of it, deposit money, and withdraw money from the register.

With that implemented, here&#8217;s how the cash register object looks like:<figure class="wp-block-image size-large">

<img src="https://nikitakazakov.com/wp-content/uploads/2020/02/image-26.png" alt="" class="wp-image-6967" srcset="https://nikitakazakov.com/wp-content/uploads/2020/02/image-26.png 922w, https://nikitakazakov.com/wp-content/uploads/2020/02/image-26-300x285.png 300w, https://nikitakazakov.com/wp-content/uploads/2020/02/image-26-768x730.png 768w" sizes="(max-width: 922px) 100vw, 922px" /> </figure> 

As a person trying to use this object, all you see is that this object understanding three messages `withdraw`, `cash_sum?`, and `deposit`. You have no idea what data the object is holding in the data circle. 

## Sending Messages

To send a message to an object, you first specify the object followed by a dot and then the message.

<pre class="EnlighterJSRAW" data-enlighter-language="ruby" data-enlighter-theme="" data-enlighter-highlight="" data-enlighter-linenumbers="" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group="">cash_register.cash_sum?    #200
</pre>

Let&#8217;s say you want to deposit or withdraw money into / from the cash register. The next question is how much? You can pass the amount as an argument with the message like this.

<pre class="EnlighterJSRAW" data-enlighter-language="generic" data-enlighter-theme="" data-enlighter-highlight="" data-enlighter-linenumbers="" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group="">cash_register.deposit(25)
cash_register.withdraw(50)</pre>

As an outsider passing a message to the cash register, you don&#8217;t need to worry about **HOW** it handles what you tell it to do. The cash register will do that internally. Again, that&#8217;s the idea of encapsulation. You trust the object to handle the messages you send to it without you meddling in them.

## Examples of Objects

Let&#8217;s take a look at how other objects might look like. Notice that with the TV remote object, I cannot send a message to it asking for it&#8217;s color or width. It won&#8217;t understand those messages as it doesn&#8217;t have them defined in the outer circle.

<pre class="EnlighterJSRAW" data-enlighter-language="ruby" data-enlighter-theme="" data-enlighter-highlight="" data-enlighter-linenumbers="" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group="">tv.color #error message. No method found.</pre><figure class="wp-block-image size-large">

<img src="https://nikitakazakov.com/wp-content/uploads/2020/02/image-27-1024x537.png" alt="" class="wp-image-6973" srcset="https://nikitakazakov.com/wp-content/uploads/2020/02/image-27-1024x537.png 1024w, https://nikitakazakov.com/wp-content/uploads/2020/02/image-27-300x157.png 300w, https://nikitakazakov.com/wp-content/uploads/2020/02/image-27-768x402.png 768w, https://nikitakazakov.com/wp-content/uploads/2020/02/image-27-1536x805.png 1536w, https://nikitakazakov.com/wp-content/uploads/2020/02/image-27.png 1664w" sizes="(max-width: 1024px) 100vw, 1024px" /> </figure> 

## Takeaways

  * When sending a message to an object, an object will always respond back. The response may be an error but there will always be a response.

link to understanding everything is an object post.