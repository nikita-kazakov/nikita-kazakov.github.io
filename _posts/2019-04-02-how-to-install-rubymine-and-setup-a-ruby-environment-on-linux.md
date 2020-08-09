---
title: How to install RubyMine and setup a Ruby environment on Linux
date: 2019-04-02T17:40:56+00:00
author: Nikita Kazakov
layout: post
permalink: /how-to-install-rubymine-and-setup-a-ruby-environment-on-linux/
tags:
  - ruby
---

You’re going to need a text editor to write Ruby. &nbsp;Although there are many options I prefer using a dedicated Ruby IDE such as RubyMine because it comes with debugging and autocomplete. 

Both are <a rel="noreferrer noopener" target="_blank" href="https://paper.dropbox.com/doc/Why-I-recommend-RubyMine-if-youre-starting-out-with-Ruby--AeaqIhkj7auxRuS5_zmPfJSCAQ-G5HoKC4PAkDYhH5shopdp">critical when learning a programming language</a>.

I&#8217;m running Xubuntu. Xubuntu comes with a Firefox web-browser. Download the Linux version of <a rel="noreferrer noopener" target="_blank" href="https://www.jetbrains.com/ruby/">RubyMine</a>.<figure class="wp-block-image">

![](https://paper-attachments.dropbox.com/s_B4F8639630B0FBC36DFABA0ACADCD708C18AE4C40D59D285D20FE9A240094838_1559653578936_image.png) </figure> 

Decompress the tar.gz file and open /bin folder. Drag **rubymine.sh** to the terminal window and run it to install RubyMine.<figure class="wp-block-image">

![](https://paper-attachments.dropbox.com/s_B4F8639630B0FBC36DFABA0ACADCD708C18AE4C40D59D285D20FE9A240094838_1559659993586_2019-06-04_08-52-20.jpg) </figure> 

Use the default settings for now, including the keymap scheme and theme. You can use the free 30 day evaluation license.

## Setting up version manager SDK

If you&#8217;re using a [version manager with Ruby](https://nikitakazakov.com/asdf-vm-version-manager-for-ruby-tutorial/), then you have to select it in RubyMine. Go to **settings** and under **languages and frameworks** select **Ruby SDK and Gems.** In my case, I&#8217;m using ASDF to run Ruby 2.4.4. Select it.<figure class="wp-block-image">

<img src="https://nikitakazakov.com/wp-content/uploads/2019/06/2019-06-10_13-59-25.jpg" alt="" class="wp-image-6704" srcset="https://nikitakazakov.com/wp-content/uploads/2019/06/2019-06-10_13-59-25.jpg 972w, https://nikitakazakov.com/wp-content/uploads/2019/06/2019-06-10_13-59-25-300x123.jpg 300w, https://nikitakazakov.com/wp-content/uploads/2019/06/2019-06-10_13-59-25-768x316.jpg 768w" sizes="(max-width: 972px) 100vw, 972px" /> </figure> 

Give your new project a name and create it.<figure class="wp-block-image">

![](https://paper-attachments.dropbox.com/s_B4F8639630B0FBC36DFABA0ACADCD708C18AE4C40D59D285D20FE9A240094838_1559660518272_image.png) </figure> 

Right click on the **project folder => new => ruby file**<figure class="wp-block-image">

![](https://paper-attachments.dropbox.com/s_B4F8639630B0FBC36DFABA0ACADCD708C18AE4C40D59D285D20FE9A240094838_1559660629801_image.png) </figure> 

Give it a name and you’ll see it generate a file name with a *.rb extension. That’s a ruby file extension.<figure class="wp-block-image">

![](https://paper-attachments.dropbox.com/s_B4F8639630B0FBC36DFABA0ACADCD708C18AE4C40D59D285D20FE9A240094838_1559660684805_image.png) </figure> 

## Setting up version manager SDK {#mce_2}

If you&#8217;re using a [version manager with Ruby](https://nikitakazakov.com/asdf-vm-version-manager-for-ruby-tutorial/), then you have to select it in RubyMine. Go to **settings** and under **languages and frameworks** select **Ruby SDK and Gems.** In my case, I&#8217;m using ASDF to run Ruby 2.4.4. Select it.<figure class="wp-block-image">

![This image has an empty alt attribute; its file name is 2019-06-10_13-59-25.jpg](https://nikitakazakov.com/wp-content/uploads/2019/06/2019-06-10_13-59-25.jpg) </figure> 

You’re ready to type Ruby code in the main window and run it.