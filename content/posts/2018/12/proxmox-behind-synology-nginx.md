---
title: "Proxmox Behind Synology's Nginx"
date: 2018-12-04T00:21:54+03:00
draft: false
rtl: false
---

# Introduction

I recently installed synology ds418 server in my house for cloud storage purposes, and I currently made it to work as a reverse proxy server with nginx.

# Setup

The below figure is the topology of my home network

![home-topolgy](/img/2018/12/home-toplogy.png)

So the problem was that noVNC of proxmox did not work after making it behind nginx. So the below nginx configuration open's a websocket with proxmox to support noVNC.

    vi /etc/nginx/sites-enabled/domian.com.conf 

    server {
        listen 80;
        listen 443;
        server_name pve.domain.com;
        ssl on;
        proxy_redirect off;

        location / {
            proxy_set_header X-Forwarded-Proto https;
            proxy_pass https://proxmox-ip:8006;   
            proxy_http_version 1.1;
            proxy_set_header Connection $http_connection;
            proxy_set_header Origin http://$host;
            proxy_set_header Upgrade $http_upgrade;
        }
    }

Test the new config

    nginx -t
    synoservicectl --restart nginx

Now test noVNC!