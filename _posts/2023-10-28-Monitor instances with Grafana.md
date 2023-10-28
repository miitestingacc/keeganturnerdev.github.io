---
title: Monitor instances with Grafana
date: 28-10-2023
categories: [cloud]
tags: [cloud, monitoring]
image: /assets/grafana.jpg
---


**Grafana is an open-source, platform-independent data visualization and monitoring 
tool commonly used for tracking and analyzing metrics and time-series data.
It offers a user-friendly interface to create customizable dashboards that 
display data from various sources, such as databases and cloud instances**


Step 1

First head over to <a href="https://grafana.com/" target="_blank">Grafana </a> and create a free account

Once you have created an account, navigate to your home menu, select **connections**, and **add new connection**.

Select the **Linux server** integration

Run the Grafana agent by selecting your instance operating system and architecture

![chooseos](/assets/chooseos.jpg)

Create a name for the API token that connects to your instance and then **Create token**

Copy the API token and save it in a document on your computer 

Update the repositories on the instance 

```
sudo apt update -y
```

```
sudo apt upgrade -y
```

Copy the second command and paste it into your Linux server terminal

![copycommand](/assets/copycommand.jpg)


Test the Agent connection and then proceed to install the integration



Step 2

add the instance hostname to the config file

![intergration](/assets/intergration.jpg)

copy the code and update the config file


```
sudo nano /etc/grafana-agent.yaml
```

![yaml](/assets/yaml.jpg)

Paste the information from the config file under **integrations**

Save the updated file and restart the grafana-agent

```
sudo systemctl restart grafana-agent.service
```

Test connection and once the connection the test is successful, proceed to install *dashboards and alerts*

On Grafana, navigate to *Home > Dashboards > Integration > Linux Node* and will now be able to monitor your server resources 

![dashboard](/assets/monitoring.jpg)


*There you have it! 
You have successfully connected your cloud instance and can 
monitor your server resources on the prebuilt Grafana dashboards.*


