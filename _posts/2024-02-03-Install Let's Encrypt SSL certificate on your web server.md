---
title: Enable Let's Encrypt SSL certificate on your Linux web server
date: 2024-02-03
categories: [cloud]
tags: [cloud]
image: /assets/cert.webp
---

Lets Encrypt provides free SSL certificates to secure your web applications over HTTPS. The Certbot is a free and open-source program, 
which allows you to secure connections to your web server.

To install a Lets Encrypt Free SSL Certificate on your web server,
launch your terminal/command line and update your operating system repositories.

NOTE - Let's Encrypt Certbot requires a fully qualified domain name to be pointed to your web server address. 
Ensure that the DNS for your domain name is pointed to the server IP address on your domain host provider of choice.

Step 1 - Updating the repositories 

```
sudo apt update && sudo apt upgrade -y
```

Next, we need to configure the domain name in the Apache default configuration file. 
This is a configuration file for the default virtual host in the Apache web server. 
In Apache, virtual hosts allow you to host multiple websites on a single server, 
and the default virtual host is used when no other virtual hosts match the incoming request.

```
sudo nano /etc/apache2/sites-available/000-default.conf
```

Uncomment 'ServerName' and enter your domain name. 

Add 'ServerAlias' one line below and add your domain name with the 'www' prefix. 

![sites-available](/assets/Apache.jpg)

Save and exit the file. You can now restart Apache 


```
sudo service apache2 reload
```


Check if the Apache web server is running

```
sudo systemctl status apache2.service
```


Install Certbot 


Step 1 Install Certbot using PIP

This command installs Python 3, the "venv" module for creating Python virtual environments

```
sudo apt install python3 python3-venv libaugeas0
```


Step 2 Set up a virtual environment

We now create a Python virtual environment named "certbot" in the /opt/certbot/ directory using the "venv" module.

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

NOTE - If your web server is locked down to your private network, 
remember to temporarily open up HTTP and HTTPS access for all 
IP addresses to allow Let's Encrypt to access the server to complete the installation

Create the Certificate 

```
sudo certbot --apache
```

![sites-available](/assets/https.jpg)

or manually specify the domain names you require SSL certificates for

Create SSL certs for a specified domain

```
sudo certbot --apache -d example.com -d www.example.com
```

![sites-available](/assets/sslsuccess.jpg)
