# Elasticsearch Installation on Ubuntu20.04

This is a guide for Apache Nifi installation on Ubuntu 20.04

## Step 1 - Create a Download Repository

Create a download repository to save the Anaconda installer.

```
mkdir downloads
cd downloads
```

## Step 2 - Download Apache Nifi

Check the latest version on [https://nifi.apache.org/download.html](https://nifi.apache.org/download.html) before running the code. If there is a newer release you can change the download link.

```
wget https://dlcdn.apache.org/nifi/1.15.0/nifi-1.15.0-bin.tar.gz
```

## Step 3 - Extract & Move Nifi Files&#x20;

You need to extract files from the tar file you have downloaded.

```
sudo tar -zxvf nifi-1.15.0-bin.tar.gz
```

You can move extracted files to the Nifi installation directory which you select (/opt for me).

```
sudo mv nifi-1.15.0 /opt/
```

## Step 4 - Configure Nifi Properties

Go to the installation Nifi directory and reach into the config files.

```
cd /opt/nifi-1.15.0 
cd conf
```

Edit nifi.properties file by changing the web host (to be able to reach Nifi UI from a remote server) and theport (optional).

```
sudo nano nifi.properties
```

Edit the following lines and save the file.

> nifi.remote.input.secure=false      #should be false
>
>
>
> nifi.web.http.host=10.115.209.128 #the ip address of the host.
>
> nifi.web.http.port=7070 #port.
>
>
>
> nifi.web.https.host=                   #should be empty
>
> nifi.web.https.port=                   #should be empty

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

