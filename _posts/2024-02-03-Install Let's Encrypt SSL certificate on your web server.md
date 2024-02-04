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

Configure the domain name in the Apache default configuration file 

```
sudo nano /etc/apache2/sites-available/000-default.conf
```

Uncomment 'ServerName' and enter your domain name. 

Add 'ServerAlias' one line below and add your domain name with the 'www' prefix. 

![sites-available](/assets/Apache.jpg)

Save and exit the file. You can now restart Apache 

```
sudo service apache 12 reload
```

Check if the Apache web server is running

```
sudo systemctl status apache2.service
```

Install Certbot 

Step 1 Install Certbot using PIP

```
sudo apt install python3 python3-venv libaugeas0
```

Step 2 Set up a virtual environment

```
sudo python3 -m venv /opt/certbot/
```

```
sudo /opt/certbot/bin/pip install --upgrade pip
```

Step 3 Install Certbot


```
sudo /opt/certbot/bin/pip install certbot certbot-apache
```

Create a symlink for Certbot to run 

```
sudo ln -s /opt/certbot/bin/certbot /usr/bin/certbot
```

Create the Certificate 

```
sudo certbot --apache
```

Create SSL certs for a specified domain

```
sudo certbot --apache -d example.com -d www.example.com
```


