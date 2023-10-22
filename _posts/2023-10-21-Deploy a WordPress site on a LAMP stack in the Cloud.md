---
title: Deploy a WordPress site on a LAMP stack in the Cloud
date: 2023-10-21
categories: [cloud]
tags: [cloud]
---

![WordPress](/assets/wordpress.png)


*WordPress is one of the most popular content management systems and today we will deploy this famous open-source 
program on our very own cloud instance*

First, create your virtual cloud instance. I will be making use of Ubuntu on xneelo.

Create an instance: How to guides

<a href="https://xneelo.co.za/help-centre/cloud/create-an-instance" target="_blank">xneelo Cloud </a>  
<a href="https://docs.aws.amazon.com/efs/latest/ug/gs-step-one-create-ec2-resources.html">AWS EC2 </a>  
  <a href="https://cloud.google.com/compute/docs/instances/create-start-instance">MS Azure VM </a>


Step 1

Update repositories

```
sudo apt update -y
```

```
sudo apt upgrade -y
```


Step 2

Install Apache web server 

```
sudo apt install apache2
```


