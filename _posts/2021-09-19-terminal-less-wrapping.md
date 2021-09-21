---
title: Use less -S to avoid wrapping in the terminal
date: 2021-09-19
layout: post
permalink: /terminal-less-wrapping
tags: 
    - linux
---

When I run `docker ps` to look at docker containers, the results are always wrapped and hard to read because there are 
too many displayed columns.

A good solution is to pipe the output to `less` with an `-s` flag which chops long lines
rather than wrapping them.

`docker ps | less -S`

The result is tabular display that fits on the screen and looks something like this. 

```bash
CONTAINER ID   IMAGE                             COMMAND                  CREATED        STATUS                PORTS                                            NAMES
72cebf9ede0c   ghcr.io/linuxserver/bookstack     "/init"                  30 hours ago   Up 14 hours           443/tcp, 0.0.0.0:6890->80/tcp                    bookstack
2250d96b7203   ghcr.io/linuxserver/mariadb       "/init"                  30 hours ago   Up 30 hours           3306/tcp                                         bookstack_db
a46886b6a048   alpine:latest                     "/bin/sh"                2 days ago     Up 2 days             0.0.0.0:5000->80/tcp                             optimistic_lederberg
f6c1ffd8026b   ruby:2.7.4-alpine3.14             "irb"                    13 days ago    Up 13 days                                                             ruby-2.7
9d68028b9f75   wordpress:latest                  "docker-entrypoint.s…"   5 months ago   Up 5 months           0.0.0.0:4444->80/tcp                             wordpress_setup_wordpress_1
ef916710b8b2   mysql:5.7                         "docker-entrypoint.s…"   5 months ago   Up 5 months           3306/tcp, 33060/tcp
```

Hit the left and right keys see more columns in the terminal.




