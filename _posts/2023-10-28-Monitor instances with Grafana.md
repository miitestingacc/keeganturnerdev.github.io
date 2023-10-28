---
title: Monitor instances with Grafana
date: 28-10-2023
categories: [cloud]
tags: [cloud, monitoring]
image: /assets/grafana.jpg
---


*Grafana is an open-source, platform-independent data visualization and monitoring 
tool commonly used for tracking and analyzing metrics and time-series data.*

*It offers a user-friendly interface to create customizable dashboards that 
display data from various sources, such as databases and cloud instances* 

Step 1

First head over to <a href="https://grafana.com/" target="_blank">Grafana </a> and create a free account

Once you have created an account, navigate to your home menu, select **connections**, and **add new connection**.

Select the **Linux server** integration

Run the Grafana agent by selecting your instance operating system and architecture

Create a name for the API token that connects to your instance and then **Create token**

Copy the API token and save it in a document on your computer 

Update the server repositories 

```
sudo apt update -y
```

```
sudo apt upgrade -y
```

Copy the second command and paste it into your Linux server terminal

Test the Agent connection
Proceed to install integration


Step 2

add the instance hostname to the config file 


copy the config file and update the following file on your instance 

```
sudo nano /etc/grafana-agent.yaml
```

Paste the information from the config file under **integrations**

Save the updated file and restart the grafana-agent

```
sudo systemctl restart grafana-agent.service
```

Test connection and once the connection the test is successful, proceed to install *dashboards and alerts*



