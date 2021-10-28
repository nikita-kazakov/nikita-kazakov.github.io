---
title: How to apt install any package on Heroku
date: 2021-10-28
layout: post
permalink: /apt-install-heroku
tags:
    - web development
---

I got stuck when trying to install the mediainfo package through `apt install mediainfo`. Using buildpacks failed and the solution was to use [heroku-buildpack-apt](https://github.com/heroku/heroku-buildpack-apt).

# 3rd party build packs
Search the [3rd party Heroku buildpacks](https://elements.heroku.com/buildpacks) to find if someone has already created a buildpack for your Linux package.

{% include image_center_caption.html
caption = "Search Heroku Buildpacks"
image = "/assets/images/2021/heroku_search.png"
%}

There were plenty of options for MediaInfo. I chose one and ran this command in the Heroku CLI:

```
heroku buildpacks:add https://github.com/bubobox/heroku-buildpack-mediainfo -a <app>
```

Make sure you re-release your app so changes take place. 
The fastest way to do that is to add an environment variable to your app and Heroku will automatically re-release it.

Go to Settings => Config Vars => Reveal Config Vars

This approach failed with the following error as I tried to run MediaInfo in the Rails console:

```
MediaInfo.from('http://commondatastorage.googleapis.com/gtv-videos-bucket/sample/BigBuckBunny.mp4')
```
I got this error:
```
version `CURL_OPENSSL_3' not found (required by /app/vendor/mediainfo/mediainfo)
```

I tried other buildpacks but the same error came up. I suspect it's because the available buildpacks haven't been updated in a while. I didn't want to write my own buildpack.

# Working Solution

Install the MediaInfo package yourself by using the [heroku-buildpack-apt](https://github.com/heroku/heroku-buildpack-apt) buildpack.

Add this buildpack from the Heroku CLI:

```
heroku buildpacks:add --index 1 heroku-community/apt
```

Create a file named `Aptfile` and add a package name on each new line that you want Heroku to automatically add to your application. In my case, I wanted `mediainfo` apt package.

```
# AptFile
# You can write comments in this file.
mediainfo
```
Redeploy your app to Heroku and try out MediaInfo in the Rails Console again. It worked for me.
