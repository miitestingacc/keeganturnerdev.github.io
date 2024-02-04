---
title: Install Let's Encrypt SSL certificate on your web server
date: 2024-02-03
categories: [cloud]
tags: [cloud]
image: /assets/certbot.png
---

Lets Encrypt provides free SSL certificates to secure your web applications over HTTPS. 

To install a Lets Encrypt Free SSL Certificate on your web server,
launch your terminal and update your operating system repositories.

NOTE - Let's Encrypt Certbot requires a fully qualified domain name to be pointed to your web server address. 
Ensure that the DNS for your domain name is pointed to the server IP address on your domain host provider of choice.

```
sudo apt update && sudo apt upgrade -y
```


