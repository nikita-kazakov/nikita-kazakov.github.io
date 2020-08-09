---
title: How a VPN keeps you secure at starbucks hotspots
date: 2018-12-19T15:50:46+00:00
layout: post
permalink: /hiding-securing-online-vpn/
tags: tech
---
What juicy details are you revealing as you browse the web?

From your IP address, your [approximate location](https://www.iplocation.net/) is visible. If you&#8217;re transmitting any data such as form fields, usernames, or passwords over a website that&#8217;s not secured by HTTPS, [it can be sniffed](https://www.youtube.com/watch?v=YzP3ZL4vlkY).

In fact, packets can be captured and reveal what you&#8217;re browsing.

<img src="http://nikitakazakov.com/wp-content/uploads/2018/12/2018-12-22_15-50-52-1024x395.jpg" sizes="(max-width: 1024px) 100vw, 1024px" srcset="http://nikitakazakov.com/wp-content/uploads/2018/12/2018-12-22_15-50-52-1024x395.jpg 1024w, http://nikitakazakov.com/wp-content/uploads/2018/12/2018-12-22_15-50-52-300x116.jpg 300w, http://nikitakazakov.com/wp-content/uploads/2018/12/2018-12-22_15-50-52-768x296.jpg 768w, http://nikitakazakov.com/wp-content/uploads/2018/12/2018-12-22_15-50-52.jpg 1058w" alt="" width="1024" height="395" /> 

The easiest place to prey on you and your data is on public WiFi hotspots.  Airports and coffee shops are big targets because many people use these hotspots.

It&#8217;s true that much of the internet uses HTTPS encryption. You&#8217;re safe browsing HTTPS secured sites, even on compromised public hotspots. The problem is getting caught off guard and sending data over an non-secure connection.

A VPN (Virtual Private Network) solves this problem and encrypts ALL of your connections from your device.

## VPN Tunnel

Let&#8217;s take a look at what happens when you access the internet normally without a VPN.

<img src="http://nikitakazakov.com/wp-content/uploads/2018/12/2018-12-11_15-44-08.jpg" sizes="(max-width: 773px) 100vw, 773px" srcset="http://nikitakazakov.com/wp-content/uploads/2018/12/2018-12-11_15-44-08.jpg 773w, http://nikitakazakov.com/wp-content/uploads/2018/12/2018-12-11_15-44-08-300x106.jpg 300w, http://nikitakazakov.com/wp-content/uploads/2018/12/2018-12-11_15-44-08-768x271.jpg 768w" alt="" width="773" height="273" /> 

You type google.com into your browser and make a website request.  That request routes through your ISP to google.com

google.com routes a response through your ISP back to you and you see the website on your screen.

So what&#8217;s the problem?

The hotspot that you&#8217;re connected to is a middle man between you and the ISP. If the hotspot is compromised, you&#8217;re vulnerable.

<img src="http://nikitakazakov.com/wp-content/uploads/2018/12/2018-12-22_16-16-41-1024x483.jpg" sizes="(max-width: 1024px) 100vw, 1024px" srcset="http://nikitakazakov.com/wp-content/uploads/2018/12/2018-12-22_16-16-41-1024x483.jpg 1024w, http://nikitakazakov.com/wp-content/uploads/2018/12/2018-12-22_16-16-41-300x142.jpg 300w, http://nikitakazakov.com/wp-content/uploads/2018/12/2018-12-22_16-16-41-768x362.jpg 768w, http://nikitakazakov.com/wp-content/uploads/2018/12/2018-12-22_16-16-41.jpg 1178w" alt="" width="1024" height="483" /> 

This is where a VPN solution comes into the picture.

A VPN service is essentially a secure middle man between you and the internet. It&#8217;s an encrypted tunnel. When you access any website, the request always goes through the encrypted VPN tunnel and then the VPN server forwards your request to the website.

<img src="http://nikitakazakov.com/wp-content/uploads/2018/12/2018-12-11_15-53-43-1024x534.jpg" sizes="(max-width: 1024px) 100vw, 1024px" srcset="http://nikitakazakov.com/wp-content/uploads/2018/12/2018-12-11_15-53-43-1024x534.jpg 1024w, http://nikitakazakov.com/wp-content/uploads/2018/12/2018-12-11_15-53-43-300x156.jpg 300w, http://nikitakazakov.com/wp-content/uploads/2018/12/2018-12-11_15-53-43-768x400.jpg 768w, http://nikitakazakov.com/wp-content/uploads/2018/12/2018-12-11_15-53-43.jpg 1176w" alt="" width="1024" height="534" /> 

The website sends its response to the VPN and the VPN tunnel relays that response to you.

Nobody can sniff traffic or see what you&#8217;re requesting within that encrypted tunnel.

Even if you&#8217;re on a compromised WiFi hotspot using a VPN, the only thing that will be visible is you connecting to your VPN IP address. The actual data that passes through is encrypted.

The baddies and your ISP can&#8217;t see what websites you&#8217;re browsing. Your entire connection is encrypted and secure.

## Commerical VPN vs your own VPN

I&#8217;ve tried using popular paid VPN services with poor results.  The problem was IP blacklisting.

Websites tend to blacklist popular VPN IP addresses as they feel they are threats.

When using a premium VPN service, I couldn&#8217;t access several websites. Remember, you&#8217;re sharing a paid VPN IP address with lots of other people that are using that paid service.

I was able to resolve the blacklisting problem by [setting up my own VPN on Vultr](http://nikitakazakov.com/how-to-create-a-vpn-with-vultr-and-openvpn/).  With Vultr, I had a dedicated IP that wasn&#8217;t shared with other users and therefore wasn&#8217;t blacklisted. I like this method and I&#8217;m sticking with it.

## Do NOT torrent with your own VPN

Do NOT torrent questionable content with your own VPN. You&#8217;re the only person on the VPN and are easily identifiable.

That&#8217;s why premium VPN services exist.  There are many people on one premium VPN IP address (plausible deniability) and a premium VPN service doesn&#8217;t keep logs.