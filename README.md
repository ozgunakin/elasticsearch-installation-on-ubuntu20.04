# Elasticsearch Installation on Ubuntu20.04

This is a guide for Apache Nifi installation on Ubuntu 20.04

## Step 1 - Prepare the Environment

Install apt-transport-https

```
sudo apt-get install apt-transport-https
```

Update GPG key

```
wget -qO - https://artifacts.elastic.co/GPG-KEY-elasticsearch | sudo apt-key add -
```

Add the repository to your system

```
echo "deb https://artifacts.elastic.co/packages/7.x/apt stable main" | sudo tee -a /etc/apt/sources.list.d/elastic-7.x.list
```

## Step 2 - Install Elasticsearch with Apt

Install latest version ap elasticsearch using apt package manager.

```
sudo apt-get update 
sudo apt-get install elasticsearch
```

## Step 4 - Configure Elasticsearch

Edit Elasticsearch yml file which is placed in /etc/elasticsearch.

```
sudo nano /etc/elasticsearch/elasticsearch.yml
```

Edit elasticsearch.yml file by changing the network host (to be able to reach Elasticsearch from a remote server).

Change the following line and save the file.

> network.host =0.0.0.0      #should be false

## Step 5 - Install Nifi Service

You need to install Nifi service to make easier the management of the Nifi as a service.

```
cd /opt/nifi-1.15.0
sudo ./bin/nifi.sh install
```

System daemon should be restarted to be able to start nifi using nifi service.

```
sudo systemctl daemon-reload
```

## Step 6 - Start Nifi Service

Start Nifi using Nifi service.

```
sudo service nifi start
```

Check the status of the service.

```
sudo service nifi status
```

