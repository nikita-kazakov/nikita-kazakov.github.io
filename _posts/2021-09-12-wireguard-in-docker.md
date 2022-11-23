---
title: Deploy Wireguard VPN in Docker
date: 2021-09-12
layout: post
permalink: /wireguard-vpn-in-docker
tags: 
    - docker
---

Most VPN setups assume that the entire server will be dedicated to the VPN. By using docker containers, I can run a vpn and other applications all on one single server.

Here's how to set up Wireguard VPN in a docker container on a cheap VPS server. I'm going to use a Vultr 1 CPU / 1 GB Ram Cloud Compute VPS droplet for this example. Let's use Ubuntu 20.04 as the server OS.

SSH into your VPS server.

Run `apt update` and `apt install curl` to update packages and install curl from the package manager.

# Install docker via script
`curl -fsSL https://get.docker.com -o get-docker.sh`  
`sudo sh get-docker.sh`

Install docker-compose which will set up Wireguard VPN container.

`apt install docker-compose`

# Wireguard VPN Docker Image
I'm standing on the shoulder of giants and want to give all the credit to the folks at [linuxserver for creating this Wireguard VPN Docker Image](https://hub.docker.com/r/linuxserver/wireguard). Feel free to read their docs to get more details on the setup I'm using below.

Create a docker compose yml file:
`touch docker-compose.yml`

Open the file with the nano editor:
`nano docker-compose.yml`

Paste these configuration settings into the file and save. Note the `PEERS=1,2,3,4,5`. I'm going to create 5 VPN 
configuration profiles that can be used on 5 different machines to access this VPN server. You can do more or less if 
you need to.

Note that I'm specifying a `PEERDNS` server. You want to specify a DNS server to use or otherwise it's going to use your ISP location. That's not private. I'm using [AdGuard DNS](https://adguard.com/en/blog/adguard-dns-new-addresses.html)  to ensure privacy and as a side-bonus, remove ads. There are other DNS addresses you can use but make sure they do not leak your ISP DNS location. We'll test that at the end of this tutorial.
```
---
version: "2.1"
services:
  wireguard:
    image: ghcr.io/linuxserver/wireguard
    container_name: wireguard
    cap_add:
      - NET_ADMIN
      - SYS_MODULE
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Europe/London
      - SERVERPORT=51820 #optional
      - PEERDNS=94.140.14.14 # Uses AdGuard DNS Server
      - PEERS=1,2,3,4,5
    volumes:
      - /path/to/appdata/config:/config
      - /lib/modules:/lib/modules
    ports:
      - 51820:51820/udp
    sysctls:
      - net.ipv4.conf.all.src_valid_mark=1
    restart: unless-stopped
```

Let's have docker-compose set this container up and run the container in detached mode:

`docker-compose up -d`

Run `docker ps` to take a look at the running image. 

Notice that it is running on udp port 51820 (standard Wireguard VPN port). You should also see an 'up' status which says that the container is currently running.

# VPN Config Files
Let's enter this docker container:
`docker exec -it wireguard bash`

What just happened above? You ran `docker exec` in the interactive and terminal mode (`-it`). You're running the container named `wireguard` and you're entering bash.

Note that your terminal prompt changed to something like `root@<container_id>`. You're inside the wireguard docker container! To exit this container, type in `exit` to return back to the VPS host.

While inside the container, navigate to the config folder:
`cd config`

Note that you'll see 5 folders: peer1, peer2, peer3, peer4, peer5. Each of those folders have separate configuration that you can use on different devices to run Wireguard VPN from this container.

Let's change directory to peer1: `cd peer1`

Let's look at `peer1.conf` with the head command: `head peer1.conf`. It will look something like this:

```
[Interface]
Address = 10.12.11.11
PrivateKey = +Nc/agXpHLNxmvtWBO4kgTddVjOewETBDQ5pFX3Sf0A=
ListenPort = 51820
DNS = 94.140.14.14 # Uses AdGuard DNS Server

[Peer]
PublicKey = j04cOA4lEFoGSojBaobODOkN8FlEzSX9tgehx6GCg=
Endpoint = 104.444.143.149:51820
```

Create a new file on your on your computer and paste the above into it. Save it as `peer1.conf`. 

**IMPORTANT** --- Add these two lines `AllowedIPs = 0.0.0.0/0, ::/0` and `PersistentKeepalive = 20` under `Endpoint` and save the file. 
This allows all traffic coming from you to go through the Wireguard VPN tunnel. Without this, your IP will be exposed.
I also add `PersistentKeepalive = 20` to send a packet every 20 seconds to Wireguard on your VPS. I found my connection was more reliable with this on.

Here's how the final config file looks like

```
[Interface]
Address = 10.13.13.2
PrivateKey = wAyK0+O7Ywp1Af7IN3xydUl1/BzwIzzRSiQIAmJ6ZFw=
ListenPort = 51820
DNS = 94.140.14.14

[Peer]
PublicKey = DHadrtHzVoC4dYhQk512ZIIdnqAG9JPsLREiRDG3ZRs=
PresharedKey = 4aUH7x92fBb5Oo30ADbOVAcS8G1WBHleHAYEFiQ9Aoc=
Endpoint = 149.27.103.100:51820
AllowedIPs = 0.0.0.0/0, ::/0
PersistentKeepalive = 20
```

You can now import this conf file into the Wireguard app on one of your devices. Remember, you have 5 generated conf files. 
In the `config` folder, go into each of the folders and repeat the process above and use those conf files on other devices.

Do not use the same conf file for multiple devices. 

# Getting a QR code

You can also read each conf file from a QR Code instead. Here's how you get a QR code:

`cd /app`  
`./show-peer 1`  

You'll see a QR code appear. You can take a screenshot and save it or you can directly scan it from your phone and use it.

To get a QR code for peer 2, you'd run:

`./show-peer 2`  

# Verifying VPN IP / DNS Security
Make sure you're not leaking DNS / IP by activating Wireguard VPN and visiting [ipleak.net](https://ipleak.net/).

Your IP location should show the location of your VPS host. The DNS location should show some other place. Both of 
these should not be anywhere close to your city. If you see your city show up, then you're leaking DNS. That's not 
good for your privacy.

That's it. The beauty of running Wireguard in a docker container is that it doesn't take up your entire server. You can still run other applications on your host server in docker containers simultaneously with the WireGuard VPN.

