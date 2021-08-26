---
title: NCDU for disk usage in Linux / Mac
date: 2021-08-26
layout: post
permalink: /ncdu-disk-usage
tags:
    - linux
---

NCDU is my primary tool for figuring out what is taking up space on my Linux servers and Mac machine.

# Install
```
# Use brew to install on Mac
brew install ncdu

# Install on Ubuntu Linux
apt install ncdu
```

Run `ncdu` in the terminal and it will scan the entire system for all files. It displays results like a file manager would with number of `#` showing the large sized files and folders relative to others.

```
--- /Users/admin/Desktop/MISC -------------------------------------------------------------------------------------------------------
                                  /..
  129.4 MiB [###################] /Image Processing
   81.0 MiB [###########        ]  1049516_UniversityBanner150dpi_01_042821.jpg
   46.9 MiB [######             ]  linux-0.86.2-2021-05-20-ab8f4799.zip
   35.1 MiB [#####              ] /medals
   25.4 MiB [###                ]  test_run.mp4
```

Press `?` to get a list of useful commands.

Navigate in and out of folders with the left and right keys.

Put your cursor on a file / directory and press `d` to delete and `yes` to confirm.