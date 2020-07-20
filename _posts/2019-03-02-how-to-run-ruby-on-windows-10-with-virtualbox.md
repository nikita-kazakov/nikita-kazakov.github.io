---
id: 6660
title: How to Run Ruby on Windows 10 with VirtualBox
date: 2019-03-02T03:03:12+00:00
author: Nikita Kazakov
layout: post
guid: https://nikitakazakov.com/?p=6660
permalink: /how-to-run-ruby-on-windows-10-with-virtualbox/
site-sidebar-layout:
  - default
site-content-layout:
  - default
theme-transparent-header-meta:
  - default
categories:
  - Uncategorized
tags:
  - ruby
---
It’s hard enough to learn a new programming language by itself and it’s miserable when you run into avoidable system errors.

I learned the hard way. Folks on <a rel="noreferrer noopener" target="_blank" href="https://www.reddit.com/r/ruby/comments/a4ogkc/why_ruby_on_windows_is_hell/">Reddit faced similar issues</a>.

After installing ports of Ruby for windows and working through tutorials, I ran into system errors that don’t show up with Ruby on MacOS or Linux. 

Don’t make the <a rel="noreferrer noopener" target="_blank" href="http://#">same mistake as I did</a>.

I want to keep Windows and still run Ruby / Ruby on Rails. The solution was to setup a virtual machine using <a rel="noreferrer noopener" target="_blank" href="https://www.virtualbox.org/">VirtualBox.</a>

I’ll show you how to do this.

## Install VirtualBox

<a rel="noreferrer noopener" target="_blank" href="https://www.virtualbox.org/">VirtualBox </a>lets allows you to emulate Linux machines. Download and install it on your Windows system.

## Download Linux Image

Why bother setting up a Linux machine from scratch when you can download a ready-to-go Linux system for Virtualbox.

I’m using **Xubuntu 18.10 Cosmic** from <a rel="noreferrer noopener" target="_blank" href="https://www.osboxes.org/xubuntu/">osboxes.org.</a><figure class="wp-block-image">

![](https://paper-attachments.dropbox.com/s_B4F8639630B0FBC36DFABA0ACADCD708C18AE4C40D59D285D20FE9A240094838_1559597189434_2019-06-03_15-24-24.jpg) </figure> 

Decompress the file (I use <a rel="noreferrer noopener" target="_blank" href="https://rarlab.com/">WinRAR</a>). The image is over 5GB. &nbsp;I create a folder for it and place it here.<figure class="wp-block-image">

![](https://paper-attachments.dropbox.com/s_B4F8639630B0FBC36DFABA0ACADCD708C18AE4C40D59D285D20FE9A240094838_1559598239794_2019-06-03_15-43-11.jpg) </figure> 

## Setup VirtualBox

Open VirtualBox and click **NEW.**<figure class="wp-block-image">

<img src="https://nikitakazakov.com/wp-content/uploads/2019/06/2019-06-10_11-45-38.jpg" alt="" class="wp-image-6695" srcset="https://nikitakazakov.com/wp-content/uploads/2019/06/2019-06-10_11-45-38.jpg 314w, https://nikitakazakov.com/wp-content/uploads/2019/06/2019-06-10_11-45-38-300x281.jpg 300w" sizes="(max-width: 314px) 100vw, 314px" /> </figure> 

Select the folder where you placed the image file. Give the virtual machine a name.<figure class="wp-block-image">

![](https://paper-attachments.dropbox.com/s_B4F8639630B0FBC36DFABA0ACADCD708C18AE4C40D59D285D20FE9A240094838_1559598594997_image.png) </figure> 

I prefer to set 2GB (2048MB) of RAM.<figure class="wp-block-image">

<img src="https://nikitakazakov.com/wp-content/uploads/2019/06/2019-06-10_11-48-15.jpg" alt="" class="wp-image-6696" srcset="https://nikitakazakov.com/wp-content/uploads/2019/06/2019-06-10_11-48-15.jpg 614w, https://nikitakazakov.com/wp-content/uploads/2019/06/2019-06-10_11-48-15-300x136.jpg 300w" sizes="(max-width: 614px) 100vw, 614px" /> </figure> 

Let’s use our existing virtual hard disk. &nbsp;**Add** it. Click **Choose**.  
<figure class="wp-block-image">

![](https://paper-attachments.dropbox.com/s_B4F8639630B0FBC36DFABA0ACADCD708C18AE4C40D59D285D20FE9A240094838_1559598894814_2019-06-03_15-52-04.jpg) </figure> 

Click **Create.**<figure class="wp-block-image">

![](https://paper-attachments.dropbox.com/s_B4F8639630B0FBC36DFABA0ACADCD708C18AE4C40D59D285D20FE9A240094838_1559598879788_image.png) </figure> 

## VirtualBox Settings

Let’s go to settings to make sure this machine uses 3D acceleration for better performance.<figure class="wp-block-image">

![](https://paper-attachments.dropbox.com/s_B4F8639630B0FBC36DFABA0ACADCD708C18AE4C40D59D285D20FE9A240094838_1559599016285_2019-06-03_15-55-58.jpg) </figure> 

Change the following:

  * **Video Memory**: 128MB
  * Enable 3D Acceleration<figure class="wp-block-image">

![](https://paper-attachments.dropbox.com/s_B4F8639630B0FBC36DFABA0ACADCD708C18AE4C40D59D285D20FE9A240094838_1559599134399_2019-06-03_15-57-40.jpg) </figure> 

Now start the machine.<figure class="wp-block-image">

![](https://paper-attachments.dropbox.com/s_B4F8639630B0FBC36DFABA0ACADCD708C18AE4C40D59D285D20FE9A240094838_1559599199848_image.png) </figure> 

The system password is **osboxes.org** 

Xubuntu asks if you want to upgrade to a newer version. &nbsp;I don’t see a reason to upgrade. Notice that you don’t have a full screen. Let’s take care of that by installing Guest Additions.

## Installing Guest Additions

Right click anywhere on the desktop and **Open Terminal Here.** Make sure you have an internet connection because we&#8217;ll be downloading packages.<figure class="wp-block-image">

![](https://paper-attachments.dropbox.com/s_B4F8639630B0FBC36DFABA0ACADCD708C18AE4C40D59D285D20FE9A240094838_1559599675012_image.png) </figure> 

Don’t get intimidated by the command line screen. &nbsp;We won’t be here too long. &nbsp;We’ll need to update packages.  
Run:

<pre class="EnlighterJSRAW" data-enlighter-language="generic" data-enlighter-theme="" data-enlighter-highlight="" data-enlighter-linenumbers="" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group="">sudo apt-get update</pre>

Password is **osboxes.org**<figure class="wp-block-image">

![](https://paper-attachments.dropbox.com/s_B4F8639630B0FBC36DFABA0ACADCD708C18AE4C40D59D285D20FE9A240094838_1559599830472_image.png) </figure> 

As you type the password, you’ll notice nothing is happening. &nbsp;That’s normal. &nbsp;Although you don’t see anything, the machine is receiving input.

Select **Devices => Insert Guest Additions CD Image**<figure class="wp-block-image">

![](https://paper-attachments.dropbox.com/s_B4F8639630B0FBC36DFABA0ACADCD708C18AE4C40D59D285D20FE9A240094838_1559600052212_image.png) </figure> 

The CD image should automatically mount and a folder will come up. Drag **autorun.sh** on to the black terminal screen and hit **ENTER** to run it.<figure class="wp-block-image">

![](https://paper-attachments.dropbox.com/s_B4F8639630B0FBC36DFABA0ACADCD708C18AE4C40D59D285D20FE9A240094838_1559600225473_image.png) </figure> 

It will ask you for the password again. &nbsp;Also, say **yes** to removing an existing version of Virtual Additions.<figure class="wp-block-image">

![](https://paper-attachments.dropbox.com/s_B4F8639630B0FBC36DFABA0ACADCD708C18AE4C40D59D285D20FE9A240094838_1559600391562_2019-06-03_16-19-23.jpg) </figure> 

You should be able to maximize the screen and voila, it’s full screen!

Xubuntu has the taskbar on top. The user interface is fairly similar to windows.<figure class="wp-block-image">

![](https://paper-attachments.dropbox.com/s_B4F8639630B0FBC36DFABA0ACADCD708C18AE4C40D59D285D20FE9A240094838_1559601316944_taskbar_xubuntu.gif) </figure> 

## Allow clipboard sharing

I like to copy and paste commands from my host computer to my virtualbox machine. Let’s enable that.

Go to your VirtualBox settings. &nbsp;**General => Advanced**.

  * Shared Clipboard: **Bidirectional**
  * Drag’n’Drop: **Host To Guest**<figure class="wp-block-image">

![](https://paper-attachments.dropbox.com/s_B4F8639630B0FBC36DFABA0ACADCD708C18AE4C40D59D285D20FE9A240094838_1559602394809_2019-06-03_16-52-31.jpg) </figure> 

Reboot the machine for effects to take place.<figure class="wp-block-image">

![](https://paper-attachments.dropbox.com/s_B4F8639630B0FBC36DFABA0ACADCD708C18AE4C40D59D285D20FE9A240094838_1559602643299_image.png) </figure> 

## Install git

Let’s install git first so that we can then clone applications from git. Open your terminal and run:

<pre class="EnlighterJSRAW" data-enlighter-language="generic" data-enlighter-theme="" data-enlighter-highlight="" data-enlighter-linenumbers="" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group="">sudo apt-get install git</pre>

## Install ASDF-VM Version Management

Using a version manager is critical if you plan on running different projects from GitHub. A project might not be compatible with the version of Ruby you have installed.

We need a way to switch between versions of Ruby without installing and uninstalling them every time. 

See here on [how to setup ASDF-VM version manager](https://nikitakazakov.com/asdf-vm-version-manager-for-ruby-tutorial/) and then go to the next step.

## Installing RubyMine and setting up a ruby environment

You’re going to need a text editor to write Ruby. &nbsp;Although there are many options I prefer using a dedicated Ruby IDE such as RubyMine because it comes with debugging and autocomplete. Both are <a rel="noreferrer noopener" target="_blank" href="https://paper.dropbox.com/doc/Why-I-recommend-RubyMine-if-youre-starting-out-with-Ruby--AeaqIhkj7auxRuS5_zmPfJSCAQ-G5HoKC4PAkDYhH5shopdp">critical when learning a programming language</a>.

[Follow these steps to finish setting up RubyMine](https://nikitakazakov.com/how-to-install-rubymine-and-setup-a-ruby-environment-on-linux/) with a Ruby Environment

You now have a Linux environment that&#8217;s running in VirtualBox that also runs Ruby code. Happy developing.