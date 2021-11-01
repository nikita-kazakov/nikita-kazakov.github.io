---
title: How to fix a corrupted usb drive with RMPrepUSB
date: 2021-11-01
layout: post
permalink: /fix-corrupt-usb-rmprepusb
tags:
    - tech
---

I tried to create bootable usb drives and all three attempts failed. When I went to reformat the drives, windows did not recognize them.

Windows native formatting tool could not reformat them. They were bricked.

# Solution
[RMPrepUSB](https://www.fosshub.com/RMPrepUSB.html) fixed all three USB drives. Download it, sinsert the usb drive, and run the application.

{% include image_center_caption.html
caption = "Selecting Options in RMPrepUSB"
image = "/assets/images/2021/rm_prep_usb_fix.jpg"
%}

If RMPrepUSB recognizes your usb drive -- you're in luck. Select any filesystem format from the options (FAT32) and click the `Prepare Drive` button.

Your USB will come back to life. You can now reformat it in any other way you want using the Windows format tool.