---
sidebar_position: 1
sidebar_label: DevOps
---
# Carelyo DevOps Workbench

## DevOps Workbench

## Monitoring

> Logging and monitoring the state of VMs, docker containers, and the services are done using [Checkmk](https://checkmk.com/).

* Log/Monitoring Server is logkib01 - 10.234.0.215


## Checkmk

Checkmk is free and open source. We are running the enterprise edition which allows us monitor 25 nodes for free. We can also us the open source version.

### Install Checkmk

We are using the docker version. We get it from here [Checkmk](https://checkmk.com/l/t/enterprise-free-trial)

Upload it to the the log server.

```bash
## Secure copy from local computer to the log server on the cloud
scp check-mk-free-docker-2.0.0p17.tar.gz log01:/tmp

## ssh into the log server to load the file
sudo -i 
cd /tmp
docker load -i check-mk-free-docker-2.0.0p17.tar.gz

## Create a folder called monitor
mkdir monitor
cd monitor
touch docker-compose.yml
```

## Edit the docker-compose file using vi

```bash
version: '3.1'
services:
  log01:
     image: checkmk/check-mk-free:2.0.0p17
     container_name: log01
     restart: always
     tmpfs:
       - /opt/omd/sites/cmk/tmp:uid=1000,gid=1000
     ports:
       - 8080:5000
     volumes:
       - monitoring:/omd/sites
       - /etc/localtime:/etc/localtime:ro
volumes:
  monitoring: {}

Save the file.
```

```bash
## Rund the docker-compose file
docker-compose up -d

## View docker-compose logs
docker-compose logs -f --tail="all"
```

## Open Firewall and Network Security Group

### Ingress Rule
Network Security Group: NSG_Checkmk
Allow source your homeIP i.e., 10.0.0.2/32 and port 8080
