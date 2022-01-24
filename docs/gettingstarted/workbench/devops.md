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
This allows only you IP to access this resource
Network Security Group: NSG_Checkmk
Allow source your homeIP i.e., 10.0.0.2/32 and port 8080 

### Login in to Checkmk server
Server IP:8080

## Add Agents
To add anagent 
- Clicck Setup > Agents > Windows, Linus, Solaris, AIX
- Since we are monitoring Ubuntu, click the Linux DEB to download the agent
- next copy the file to the Ubuntu server

```bash
## Secure copy from local computer to the log server on the cloud
scp check-mk-agent_2.0.0p17-74a3d18d9c2e1ce4_all.deb ubuntuserver:/tmp

## install the agent
dpkg -i check-mk-agent_2.0.0p17-74a3d18d9c2e1ce4_all.deb
```
## Add Plugin to monitor docker container
To monitor additional services you may need plugins.
Download the plugin from the checkmk server at 
Setup > Agents > Other operating systems or from the **internet**

```bash
## upload it to the server to this location
cd /usr/lib/check_mk_agent/plugins/ 
```

log in to the checkmk via the web browser Server IP:8080
- Setup > Add host
-  Enter the hostname: myserver
-  Under Network address: Enter the IPv4 address i.e., 10.0.9.0
-  Save & go to service configuration
-  This takes you to Setup > Hosts > Main directory >Properties of host myserver > Services of host myserver
- - Check all the services that you want to monitor and click **Full service scan** and on the top right you should see changes if any, then click **Activate on selected sites** to implement the changes

## HAPROXY

### LUA.CORS
Here the link [lua.cors](https://www.haproxy.com/blog/enabling-cors-in-haproxy/)

```bash
$ haproxy -vv | grep Lua
Built with Lua version: Lua 5.3.5

global
    lua-load /etc/haproxy/cors.lua
```

## Block Volume Encryption
By default all volumes and their backups are encrypted using the Oracle-provided encryption keys. Each time a volume is cloned or restored from a backup the volume is assigned a new unique encryption key. This link talks about OCI Block Volume Service [BlockVolumeEncryption](https://docs.oracle.com/en-us/iaas/Content/Block/Concepts/overview.htm#BlockVolumeEncryption)