---
title: How to install RubyMine and setup a Ruby environment on Linux
date: 2019-04-02T17:40:56+00:00
author: Nikita Kazakov
layout: post
permalink: /how-to-install-rubymine-and-setup-a-ruby-environment-on-linux/
tags:
  - ruby
---

You’re going to need a text editor to write Ruby. Although there are many options I prefer using a dedicated Ruby IDE such as RubyMine because it comes with debugging and autocomplete.

Both are [critical when learning a programming language](https://youtu.be/UE7GWOOTsRQ).

I’m running Xubuntu. Xubuntu comes with a Firefox web-browser. Download the Linux version of [RubyMine](https://www.jetbrains.com/ruby/).

{% include image_center_caption.html
    caption = ""
    image = "/assets/images/imported/rubylinux-1.png"
%}

Decompress the tar.gz file and open /bin folder. Drag **rubymine.sh** to the terminal window and run it to install RubyMine.

{% include image_center_caption.html
caption = ""
image = "/assets/images/imported/rubylinux-2.jpg"
%}

Use the default settings for now, including the keymap scheme and theme. You can use the free 30 day evaluation license.

## Setting up version manager SDK

If you’re using a [version manager with Ruby](https://wordpress.selfhostbaby.xyz/asdf-vm-version-manager-for-ruby-tutorial/), then you have to select it in RubyMine. Go to **settings** and under **languages and frameworks** select **Ruby SDK and Gems.** In my case, I’m using ASDF to run Ruby 2.4.4. Select it.

{% include image_center_caption.html
caption = ""
image = "/assets/images/imported/rubylinux-3.jpg"
%}

Give your new project a name and create it.

{% include image_center_caption.html
caption = ""
image = "/assets/images/imported/rubylinux-4.png"
%}

Right click on the **project folder => new => ruby file**

{% include image_center_caption.html
caption = ""
image = "/assets/images/imported/rubylinux-5.png"
%}

Give it a name and you’ll see it generate a file name with a *.rb extension. That’s a ruby file extension.

{% include image_center_caption.html
caption = ""
image = "/assets/images/imported/rubylinux-6.png"
%}

## Setting up version manager SDK

If you’re using a [version manager with Ruby](https://wordpress.selfhostbaby.xyz/asdf-vm-version-manager-for-ruby-tutorial/), then you have to select it in RubyMine. Go to **settings** and under **languages and frameworks** select **Ruby SDK and Gems.** In my case, I’m using ASDF to run Ruby 2.4.4. Select it.

{% include image_center_caption.html
caption = ""
image = "/assets/images/imported/rubylinux-7.jpg"
%}

You’re ready to type Ruby code in the main window and run it.
