---
id: 3219
title: How to create a VPN with Vultr and OpenVPN
date: 2018-12-19T15:44:18+00:00
author: Nikita Kazakov
excerpt: |
layout: post
guid: http://nikitakazakov.com/?p=3217
permalink: /how-to-create-a-vpn-with-vultr-and-openvpn/
ocean_gallery_link_images:
  - 'off'
  - 'off'
ocean_sidebar:
  - "0"
  - "0"
ocean_second_sidebar:
  - "0"
  - "0"
ocean_disable_margins:
  - enable
  - enable
ocean_display_top_bar:
  - default
  - default
ocean_display_header:
  - default
  - default
ocean_center_header_left_menu:
  - "0"
  - "0"
ocean_custom_header_template:
  - "0"
  - "0"
ocean_header_custom_menu:
  - "0"
  - "0"
ocean_menu_typo_font_family:
  - "0"
  - "0"
ocean_disable_title:
  - default
  - default
ocean_disable_heading:
  - default
  - default
ocean_disable_breadcrumbs:
  - default
  - default
ocean_display_footer_widgets:
  - default
  - default
ocean_display_footer_bottom:
  - default
  - default
ocean_custom_footer_template:
  - "0"
  - "0"
ocean_link_format_target:
  - self
  - self
ocean_quote_format_link:
  - post
  - post
ocean_post_layout:
  - full-screen
  - full-screen
site-sidebar-layout:
  - default
site-content-layout:
  - default
theme-transparent-header-meta:
  - default
image: /wp-content/uploads/2018/12/VPNtube.jpg
categories:
  - Uncategorized
tags:
  - "2018"
  - security
---
I&#8217;ve talked about how a VPN (virtual private network) hides your browsing habits from your ISP (internet service provider). It also secures your online connections from public WiFi hotspot attacks.

[vultr.com](http://vultr.com) lets you setup a VPN quickly using OpenVPN and it&#8217;s super cheap if you&#8217;re using it short-term. They have a o_ne-click s_etup.

I see this as a great option if you&#8217;re travelling or working from questionable locations.

I found Vultr to be cheap because they charge by the hour rather than monthly. If you need a VPN for a couple of days, it&#8217;ll cost you less than $1.

Let&#8217;s begin.

Sign up on [vultr.com](http://vultr.com), deploy a new server, and pick a location. If you pick a location that&#8217;s far from you, the speed will be a bit slower when you use your VPN service.

Don&#8217;t use this VPN for torrenting  
Don&#8217;t use this VPN for torrenting or other potentially less than legal activities.

Vultr most likely keeps log

<button type="button"></button><img style="outline: red dashed 1px;" title="" src="http://nikitakazakov.com/wp-content/uploads/2018/12/2018-12-11_16-09-26-1024x553.jpg" sizes="(max-width: 1024px) 100vw, 1024px" srcset="http://nikitakazakov.com/wp-content/uploads/2018/12/2018-12-11_16-09-26-1024x553.jpg 1024w, http://nikitakazakov.com/wp-content/uploads/2018/12/2018-12-11_16-09-26-300x162.jpg 300w, http://nikitakazakov.com/wp-content/uploads/2018/12/2018-12-11_16-09-26-768x415.jpg 768w, http://nikitakazakov.com/wp-content/uploads/2018/12/2018-12-11_16-09-26.jpg 1284w" alt="" width="1024" height="553" />

Select the Application tab and select OpenVPN to be installed.

<img title="" src="http://nikitakazakov.com/wp-content/uploads/2018/12/2018-12-11_16-13-59-1024x455.jpg" sizes="(max-width: 1024px) 100vw, 1024px" srcset="http://nikitakazakov.com/wp-content/uploads/2018/12/2018-12-11_16-13-59-1024x455.jpg 1024w, http://nikitakazakov.com/wp-content/uploads/2018/12/2018-12-11_16-13-59-300x133.jpg 300w, http://nikitakazakov.com/wp-content/uploads/2018/12/2018-12-11_16-13-59-768x341.jpg 768w, http://nikitakazakov.com/wp-content/uploads/2018/12/2018-12-11_16-13-59.jpg 1488w" alt="" width="1024" height="455" /> 

You can select the $5 plan which sports 1GB of memory. That&#8217;s more than enough.

<img src="http://nikitakazakov.com/wp-content/uploads/2018/12/2018-12-11_16-17-58-1024x264.jpg" sizes="(max-width: 1024px) 100vw, 1024px" srcset="http://nikitakazakov.com/wp-content/uploads/2018/12/2018-12-11_16-17-58-1024x264.jpg 1024w, http://nikitakazakov.com/wp-content/uploads/2018/12/2018-12-11_16-17-58-300x77.jpg 300w, http://nikitakazakov.com/wp-content/uploads/2018/12/2018-12-11_16-17-58-768x198.jpg 768w, http://nikitakazakov.com/wp-content/uploads/2018/12/2018-12-11_16-17-58.jpg 1527w" alt="" width="1024" height="264" /> 

Hit the deploy button. Remember, you&#8217;re charged by the hour.  If you only need a VPN for a day or so it&#8217;ll come out to be less than $1.

Deploy the server.

<img src="http://nikitakazakov.com/wp-content/uploads/2018/12/2018-12-11_16-17-34.jpg" sizes="(max-width: 447px) 100vw, 447px" srcset="http://nikitakazakov.com/wp-content/uploads/2018/12/2018-12-11_16-17-34.jpg 447w, http://nikitakazakov.com/wp-content/uploads/2018/12/2018-12-11_16-17-34-300x64.jpg 300w" alt="" width="447" height="96" /> 

## Accessing OpenVPN

Select the server.

<img src="http://nikitakazakov.com/wp-content/uploads/2018/12/2018-12-19_13-57-45.jpg" sizes="(max-width: 873px) 100vw, 873px" srcset="http://nikitakazakov.com/wp-content/uploads/2018/12/2018-12-19_13-57-45.jpg 873w, http://nikitakazakov.com/wp-content/uploads/2018/12/2018-12-19_13-57-45-300x230.jpg 300w, http://nikitakazakov.com/wp-content/uploads/2018/12/2018-12-19_13-57-45-768x589.jpg 768w" alt="" width="873" height="670" /> 

Vultr has automatically setup OpenVPN on the server and now you need to login using the given credentials.

You&#8217;ll likely get an unsecure page warning.  Don&#8217;t worry about that. The actual VPN connection you&#8217;ll use will be secure.

<img title="" src="http://nikitakazakov.com/wp-content/uploads/2018/12/2018-12-19_14-03-33-1024x515.jpg" sizes="(max-width: 1024px) 100vw, 1024px" srcset="http://nikitakazakov.com/wp-content/uploads/2018/12/2018-12-19_14-03-33-1024x515.jpg 1024w, http://nikitakazakov.com/wp-content/uploads/2018/12/2018-12-19_14-03-33-300x151.jpg 300w, http://nikitakazakov.com/wp-content/uploads/2018/12/2018-12-19_14-03-33-768x386.jpg 768w, http://nikitakazakov.com/wp-content/uploads/2018/12/2018-12-19_14-03-33.jpg 1181w" alt="" width="1024" height="515" />  
<img src="http://nikitakazakov.com/wp-content/uploads/2018/12/2018-12-19_14-04-42.jpg" sizes="(max-width: 701px) 100vw, 701px" srcset="http://nikitakazakov.com/wp-content/uploads/2018/12/2018-12-19_14-04-42.jpg 701w, http://nikitakazakov.com/wp-content/uploads/2018/12/2018-12-19_14-04-42-300x258.jpg 300w" alt="" width="701" height="604" /> 

Type in your credentials and log in.

Use the provided links to download OpenVPN for your operating system.  Install it.

<img src="http://nikitakazakov.com/wp-content/uploads/2018/12/2018-12-19_14-09-21-1024x527.jpg" sizes="(max-width: 1024px) 100vw, 1024px" srcset="http://nikitakazakov.com/wp-content/uploads/2018/12/2018-12-19_14-09-21-1024x527.jpg 1024w, http://nikitakazakov.com/wp-content/uploads/2018/12/2018-12-19_14-09-21-300x155.jpg 300w, http://nikitakazakov.com/wp-content/uploads/2018/12/2018-12-19_14-09-21-768x396.jpg 768w, http://nikitakazakov.com/wp-content/uploads/2018/12/2018-12-19_14-09-21.jpg 1033w" alt="" width="1024" height="527" /> 

Download the user profile. OpenVPN will use it to secure your VPN connection.

Right click on the OpenVPN connection and import the user profile you downloaded. Now connect to it.

The connection is active when the OpenVPN computer icon lights up with a green color.

<img src="http://nikitakazakov.com/wp-content/uploads/2018/12/2018-12-19_14-17-11-1024x613.jpg" sizes="(max-width: 1024px) 100vw, 1024px" srcset="http://nikitakazakov.com/wp-content/uploads/2018/12/2018-12-19_14-17-11-1024x613.jpg 1024w, http://nikitakazakov.com/wp-content/uploads/2018/12/2018-12-19_14-17-11-300x179.jpg 300w, http://nikitakazakov.com/wp-content/uploads/2018/12/2018-12-19_14-17-11-768x459.jpg 768w, http://nikitakazakov.com/wp-content/uploads/2018/12/2018-12-19_14-17-11.jpg 1125w" alt="" width="1024" height="613" /> 

## Test Anonymity

Go ahead and test your anonymity.  You can use [ipleak.net](https://ipleak.net/) or [browserleaks.com/ip](https://browserleaks.com/ip) to ensure your geo-location is not your real location.

<img src="http://nikitakazakov.com/wp-content/uploads/2018/12/2018-12-19_14-24-31.jpg" sizes="(max-width: 602px) 100vw, 602px" srcset="http://nikitakazakov.com/wp-content/uploads/2018/12/2018-12-19_14-24-31.jpg 602w, http://nikitakazakov.com/wp-content/uploads/2018/12/2018-12-19_14-24-31-300x232.jpg 300w" alt="" width="602" height="466" /> 

You&#8217;re now browsing the internet securely and no one except the VPN server can see what you&#8217;re browsing.