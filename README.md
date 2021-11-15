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
apt-get install elasticsearch
```

## Step 3 - Configure Elasticsearch

Edit Elasticsearch yml file which is placed in /etc/elasticsearch.

```
sudo nano /etc/elasticsearch/elasticsearch.yml
```

Edit elasticsearch.yml file by changing the network host (to be able to reach Elasticsearch from a remote server).

Change the following line and save the file.

> network.host =0.0.0.0      #sholud be changed
>
> discovery.seed.hosts = \["127.0.0.1"]
>
> \#Add following lines
>
> xpack.security.enabled: true xpack.security.transport.ssl.enabled: true xpack.security.transport.ssl.verification\_mode: certificate xpack.security.transport.ssl.client\_authentication: required xpack.security.transport.ssl.keystore.path: elastic-certificates.p12 xpack.security.transport.ssl.truststore.path: elastic-certificates.p12

## Step 4 - Enable X-pack Security



```
cd /usr/share/elasticsearch

./bin/elasticsearch-certutil ca

./bin/elasticsearch-certutil cert --ca elastic-stack-ca.p12

sudo chmod -R a+rwx elastic-certificates.p12

mv elasticsearch-certificates.p12 /etc/elasticsearch/elastic-certificates.p12

./bin/elasticsearch
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

