---
title: Run your own Grafana + Prometheus instance
date: 2024-03-30
categories: [cloud]
tags: [cloud, monitoring]
image: /assets/grafprom.png
---

*Grafana and Prometheus are open-source tools used for monitoring and visualizing data, logs, and metrics in system environments. 
Prometheus collects metrics from various hosts and sources and stores them in a time-series database, while Grafana provides a flexible 
interface for visualizing this data through customizable dashboards. Running Grafana and Prometheus locally on
your server or in a cloud environment gives you full control over your monitoring solution without relying on external services.*

Connect to the server where Grafana will be installed. I am deploying the application to a Ubuntu 22 instance on a cloud instance.

Step1 
Download Grafana for Ubuntu/Debian 

```
sudo apt-get install -y adduser libfontconfig1 musl
```
```
 sudo wget https://dl.grafana.com/enterprise/release/grafana-enterprise_10.4.1_amd64.deb
```
```
sudo dpkg -i grafana-enterprise_10.4.1_amd64.deb
```

Reference: https://grafana.com/grafana/download?pg=graf-deployment-options&plcmt=deploy-box-1

Step 2 
On the terminal command line, follow the prompts from the output:

```
sudo /bin/systemctl daemon-reload
```
```
sudo /bin/systemctl enable grafana-server
```

You can start grafana-server by executing
```
sudo /bin/systemctl start grafana-server
```

The next step would be to install Node Exporter on all the hosts you would like to monitor. This can include the same hosts where Grafana runs from locally. 

```
sudo wget https://github.com/prometheus/node_exporter/releases/download/v1.7.0/node_exporter-1.7.0.linux-amd64.tar.gz
```

Unpack the downloaded file 
```
 tar xvfz node_exporter-1.7.0.linux-amd64.tar.gz
```
```
cd node_exporter-1.7.0.linux-amd64.tar.gz
```

once you have changed directories to the downloaded file, run 
```
sudo nohup ./node_exporter &
```
This command launches the node_exporter process as a background task that continues to run even 
after the terminal session ends, making it a daemon process for exporting system metrics.

Repeat this process for all the servers/instances you wish to monitor.

Reference: https://prometheus.io/docs/guides/node-exporter/

Now we need to download Prometheus on the same host that will serve Grafana.
```
sudo wget https://github.com/prometheus/prometheus/releases/download/v2.51.0/prometheus-2.51.0.linux-amd64.tar.gz
```

Unpack the file and change directory to it 

```
tar xvfz prometheus-2.51.0.linux-amd64.tar.gz
```
```
cd prometheus-2.51.0.linux-amd64
```

find the prometheus.yml file and edit the `static_configs` section with the server IPs you wish to monitor
![prometheus.yml](/assets/settings.png)

Note: Host targets run on port 9100

Run the below command:
```
sudo nohup ./prometheus --config.file=./prometheus.yml &
```

You should now be able to access Grafana on the IP address of your server you over port 3000. 
http://serverip:3000

The default username is 'admin' and the password will also be 'admin' for the first log in.

Change and update your password upon successful login 

*Add Prometheus datasource*
From within the Grafana dashboard, navigate to ‘connections’, ‘data sources’ and add a new data source.

![datasource](/assets/config.png)

![datasource2](/assets/scrape.png)

You can now add or build a dashboard. I recommend importing the <a href="https://grafana.com/grafana/dashboards/1860-node-exporter-full/" target="_blank">node exporter </a> preconfigured dashboard.

![dashboard](/assets/dashboard.png)

We've outlined the installation steps for node_exporter, a pivotal component in monitoring system metrics with Prometheus. 
By following these instructions, you've seamlessly integrated node_exporter into your system, allowing Prometheus to collect crucial 
metrics for analysis. With Grafana's visualization capabilities complementing Prometheus's 
data collection, you're now equipped to monitor and analyze system performance. Happy monitoring!
