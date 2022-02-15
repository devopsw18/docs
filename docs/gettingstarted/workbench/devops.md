---
sidebar_position: 3
sidebar_label: DevOps
---
# Carelyo DevOps Workbench

# Pipeline introduction
The basic pipeline files can be found [here](https://gitlab.com/carelyo/ci_cd-pipeline-files). 

## Files
### main.yml

This is the main pipeline for building images on merge requests and pushing them to DockerHub. It's a heavily modified version of the [Docker CI/CD template from GitLab](https://gitlab.com/gitlab-org/gitlab-foss/-/blob/master/lib/gitlab/ci/templates/Docker.gitlab-ci.yml).

It **only** runs on Develop, Staging and main branches with a Dockerfile thanks to:

    rules:
    - if: $CI_PIPELINE_SOURCE == "merge_request_event" && $CI_MERGE_REQUEST_TARGET_BRANCH_NAME == "Develop" || $CI_MERGE_REQUEST_TARGET_BRANCH_NAME == "Staging" || $CI_MERGE_REQUEST_TARGET_BRANCH_NAME == "main"
    # Where a dockerfile exists
      exists:
      - Dockerfile

This can also be changed on a per-repo basis after importing ``ci_cd-pipeline-files/main.yml``.

### GitLab configuration
The variables used in the `gitlab-ci.yml` are set on a group-wide level through [its settings](https://gitlab.com/groups/carelyo/-/settings/ci_cd). It's also possible to set these on a per-project basis.

### Variables
 - `CI_REGISTRY` is where the DockerHub repo URL is stored.  
 - - These variables [are masked](https://docs.gitlab.com/ee/ci/variables/index.html#mask-a-cicd-variable), meaning they won't show up in job logs in plain text.
 - - `CI_REGISTRY_PASSWORD` is the DockerHub access token. The normal password is possible too but is less secure in case someone gains access to the GitLab account. Also it's not posssible to mask certain passwords(meaning ones with special characters etc).
 -- `CI_REGISTRY_USER` is where the DockerHub repo URL is stored.


## Monitoring

> Logging and monitoring the state of VMs, docker containers, and the services are done using [Checkmk](https://checkmk.com/).

* Log/Monitoring Server is logkib01 - 10.234.0.215


### Checkmk

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

**Edit the docker-compose file using vi**

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

## Open Firewall & Network Security Group

### Ingress Rule
This allows only you IP to access this resource
Network Security Group: NSG_Checkmk
Allow source your homeIP i.e., 10.0.0.2/32 and port 8080 

### IPtables
**Allow http 80 In**

```code
sudo iptables -I INPUT -p tcp --dport 80 -m conntrack --ctstate NEW,ESTABLISHED -j ACCEPT
```
```code
sudo iptables -I OUTPUT -p tcp --sport 80 -m conntrack --ctstate ESTABLISHED -j ACCEPT
```

**Allow https 443 In**
```code
sudo iptables -I INPUT -p tcp --dport 443 -m conntrack --ctstate NEW,ESTABLISHED -j ACCEPT
```
```code
sudo iptables -I OUTPUT -p tcp --sport 443 -m conntrack --ctstate ESTABLISHED -j ACCEPT
```
**Allow port udp 514 syslog in**
```code
sudo iptables -I INPUT -p udp --dport 514 -m conntrack --ctstate NEW,ESTABLISHED -j ACCEPT
```

***Allow 50514 tcp syslog in**
```code
sudo iptables -I INPUT -p tcp --dport 50514 -m conntrack --ctstate NEW,ESTABLISHED -j ACCEPT
```

**Save IPtables**
```code
sudo iptables-save > /etc/iptables/rules.v4
```

**Restore IPtable**
```code
sudo iptables-restore < /etc/iptables/rules.v4
```

**Install iptables-persistent**
```code
sudo apt-get install iptables-persistent
```

**Key current and Add new**
```code
sudo iptables-restore -n < /etc/iptables/rules.v4
```

### Login in to Checkmk server
Server IP:8080

### Add Agents
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
### Add Plugin to monitor docker container
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

### Install Haproxy On Ubuntu 20.04

**Grab the right PPA**
[Debian/Ubuntu HAProxy packages](https://haproxy.debian.net/#?distribution=Ubuntu&release=focal&version=2.4)

**Enable a dedicated PPA:**
```code
# sudo apt-get install --no-install-recommends software-properties-common -y
# sudo add-apt-repository ppa:vbernat/haproxy-2.4 -y
# sudo apt-get install haproxy=2.4.\* -y
```
**Verify Haproxy is installed**

```ubuntu
haproxy -v

HAProxy version 2.4.9-1ppa1~focal 2021/11/24 - https://haproxy.org/
Status: long-term supported branch - will stop receiving fixes around Q2 2026.
Known bugs: http://www.haproxy.org/bugs/bugs-2.4.9.html
Running on: Linux 5.11.0-1022-oracle #23~20.04.1-Ubuntu SMP Fri Nov 12 15:45:30 UTC 2021 x86_64
```

### Enable Haproxy
```code
systemctl enable --now haproxy
```

### Test Haproxy

```code
haproxy -f haproxy.cfg -c
```

### Haproxy Userlist
[Userlist](https://www.haproxy.com/documentation/hapee/latest/configuration/config-sections/userlist/)

#### Using encrypted passwords
**Generate SHA-256 encrypted password**

```code
sudo apt install whois
mkpasswd -m sha-256 mypassword123
```

### PSTree
```code
sudo apt install psmisc -y
```
```code
pstree
```
## Define Haproxy Certificate

**Get the Cert which is a .pem from Letsencrypt or Cloudflare** and concatennate it wtit the **Get the Key .key**
```code
cat fullchain.pem privkey.pem > /etc/haproxy/carlyo_certs/carelyo.ng.pem
```

## Swapfile

**What is Swap**
Swap is a portion of the hard drive storage that has beenset aside for the operating system to temporarily store that it can no longer hold in RAM.This lets you increase the amount of information that your server can keep in its working memory, with some caveats. The swap space on the hard drive will be used mainly when there is no longer sufficient space in RAM to hold in-use application data.

### Create Swap File
**Check if swap exist**
```code
sudo swapon --show
```

**Verify**

```code
free -h
              total        used        free      shared  buff/cache   available
Mem:           15Gi       302Mi        14Gi       1.0Mi       682Mi        15Gi
Swap:            0B          0B          0B
```

**Allocate 2GB of Swap File**

```code
sudo fallocate -l 2G /swapfile
```
**Verify**

```code
ls -lh /swapfile
```

### Enable Swap File

```code
sudo chmod 600 /swapfile
```

### Mark as Swap Space

```code
sudo mkswap /swapfile
```
### Enable Swap File

```code
sudo swapon /swapfile
```

**Verify**

```code
free -h
```

### Make Swap Permanent

```code
sudo cp /etc/fstab /etc/fstab.bak
```
**Add swap file to the end of the file /etc/fstab file**

```code
echo '/swapfile none swap sw 0 0' | sudo tee -a /etc/fstab
```
### Tunning Swap Settings
```code
cat /proc/sys/vm/swappiness
```
```code
sudo vi /etc/sysctl.conf
```
**Add to the buttom**
```
vm.swappiness=10
```

### Adjusting the Cache Pressure Setting
**Show current value**
```code
cat /proc/sys/vm/vfs_cache_pressure
```
**Change it to 50**
```code
sudo vi /etc/sysctl.conf
```
```code
vm.vfs_cache_pressure=50
```

### Swapfile Rule of Thumb
| Amount of RAM installed in system  |  Recommended swap space | Recommended swap space with hibernation  |
|-------------|-----------------|--------------------------------|
| ≤ 2GB       | 2X RAM          |    3X RAM                      |
| 2GB – 8GB   | = RAM           |    2X RAM                      |
| 8GB – 64GB  | 4G to 0.5X RAM  |    1.5X RAM                    |
| >64GB       | Minimum 4GB     |    Hibernation not recommended |


### LUA.CORS
Here the link [lua.cors](https://www.haproxy.com/blog/enabling-cors-in-haproxy/)

```bash
$ haproxy -vv | grep Lua
Built with Lua version: Lua 5.3.5

global
    lua-load /etc/haproxy/cors.lua
```
**File cors.lua**

```code
--
-- Cross-origin Request Sharing (CORS) implementation for HAProxy Lua host
--
-- CORS RFC:
-- https://www.w3.org/TR/cors/
--
-- Copyright (c) 2019. Nick Ramirez <nramirez@haproxy.com>
-- Copyright (c) 2019. HAProxy Technologies, LLC.

-- Loops through array to find the given string.
-- items: array of strings
-- test_str: string to search for
function contains(items, test_str)
  for _,item in pairs(items) do
    if item == test_str then
      return true
    end
  end

  return false
end

-- If the given origin is found within the allowed_origins string, it is returned. Otherwise, nil is returned.
-- origin: The value from the 'origin' request header
-- allowed_origins: Comma-delimited list of allowed origins. (e.g. localhost,localhost:8080,test.com)
function get_allowed_origin(origin, allowed_origins)
  if origin ~= nil then
    local allowed_origins = core.tokenize(allowed_origins, ",")

    -- Strip whitespace
    for index, value in ipairs(allowed_origins) do
      allowed_origins[index] = value:gsub("%s+", "")
    end

    if contains(allowed_origins, "*") then
      return "*"
    elseif contains(allowed_origins, origin:match("//([^/]+)")) then
      return origin
    end
  end

  return nil
end

-- Adds headers for CORS preflight request and then attaches them to the response
-- after it comes back from the server. This works with versions of HAProxy prior to 2.2.
-- The downside is that the OPTIONS request must be sent to the backend server first and can't
-- be intercepted and returned immediately.
-- txn: The current transaction object that gives access to response properties
-- allowed_methods: Comma-delimited list of allowed HTTP methods. (e.g. GET,POST,PUT,DELETE)
-- allowed_headers: Comma-delimited list of allowed headers. (e.g. X-Header1,X-Header2)
function preflight_request_ver1(txn, allowed_methods, allowed_headers)
  core.Debug("CORS: preflight request received")
  txn.http:res_set_header("Access-Control-Allow-Methods", allowed_methods)
  txn.http:res_set_header("Access-Control-Allow-Headers", allowed_headers)
  txn.http:res_set_header("Access-Control-Max-Age", 600)
  core.Debug("CORS: attaching allowed methods to response")
end

-- Add headers for CORS preflight request and then returns a 204 response.
-- The 'reply' function used here is available in HAProxy 2.2+. It allows HAProxy to return
-- a reply without contacting the server.
-- txn: The current transaction object that gives access to response properties
-- origin: The value from the 'origin' request header
-- allowed_methods: Comma-delimited list of allowed HTTP methods. (e.g. GET,POST,PUT,DELETE)
-- allowed_origins: Comma-delimited list of allowed origins. (e.g. localhost,localhost:8080,test.com)
-- allowed_headers: Comma-delimited list of allowed headers. (e.g. X-Header1,X-Header2)
function preflight_request_ver2(txn, origin, allowed_methods, allowed_origins, allowed_headers)
  core.Debug("CORS: preflight request received")

  local reply = txn:reply()
  reply:set_status(204, "No Content")
  reply:add_header("Content-Type", "text/html")
  reply:add_header("Access-Control-Allow-Methods", allowed_methods)
  reply:add_header("Access-Control-Allow-Headers", allowed_headers)
  reply:add_header("Access-Control-Max-Age", 600)

  local allowed_origin = get_allowed_origin(origin, allowed_origins)

  if allowed_origin == nil then
    core.Debug("CORS: " .. origin .. " not allowed")
  else
    core.Debug("CORS: " .. origin .. " allowed")
    reply:add_header("Access-Control-Allow-Origin", allowed_origin)

    if allowed_origin ~= "*" then
      reply:add_header("Vary", "Accept-Encoding,Origin")
    end
  end

  core.Debug("CORS: Returning reply to preflight request")
  txn:done(reply)
end

-- When invoked during a request, captures the origin header if present and stores it in a private variable.
-- If the request is OPTIONS and it is a supported version of HAProxy, returns a preflight request reply.
-- Otherwise, the preflight request header is added to the response after it has returned from the server.
-- txn: The current transaction object that gives access to response properties
-- allowed_methods: Comma-delimited list of allowed HTTP methods. (e.g. GET,POST,PUT,DELETE)
-- allowed_origins: Comma-delimited list of allowed origins. (e.g. localhost,localhost:8080,test.com)
-- allowed_headers: Comma-delimited list of allowed headers. (e.g. X-Header1,X-Header2)
function cors_request(txn, allowed_methods, allowed_origins, allowed_headers)
  local headers = txn.http:req_get_headers()
  local transaction_data = {}
  local origin = nil

  if headers["origin"] ~= nil and headers["origin"][0] ~= nil then
    core.Debug("CORS: Got 'Origin' header: " .. headers["origin"][0])
    origin = headers["origin"][0]
  end

  -- Bail if client did not send an Origin
  -- for example, it may be a regular OPTIONS request that is not a CORS preflight request
  if origin == nil or origin == '' then
    return
  end

  transaction_data["origin"] = origin
  transaction_data["allowed_methods"] = allowed_methods
  transaction_data["allowed_origins"] = allowed_origins
  transaction_data["allowed_headers"] = allowed_headers

  txn:set_priv(transaction_data)

  local method = txn.sf:method()
  transaction_data["method"] = method

  if method == "OPTIONS" and txn.reply ~= nil then
    preflight_request_ver2(txn, origin, allowed_methods, allowed_origins, allowed_headers)
  end
end

-- When invoked during a response, sets CORS headers so that the browser can read the response from permitted domains.
-- txn: The current transaction object that gives access to response properties.
function cors_response(txn)
  local transaction_data = txn:get_priv()

  if transaction_data == nil then
    return
  end

  local origin = transaction_data["origin"]
  local allowed_origins = transaction_data["allowed_origins"]
  local allowed_methods = transaction_data["allowed_methods"]
  local allowed_headers = transaction_data["allowed_headers"]
  local method = transaction_data["method"]

  -- Bail if client did not send an Origin
  if origin == nil or origin == '' then
    return
  end

  local allowed_origin = get_allowed_origin(origin, allowed_origins)

  if allowed_origin == nil then
    core.Debug("CORS: " .. origin .. " not allowed")
  else
    if method == "OPTIONS" and txn.reply == nil then
      preflight_request_ver1(txn, allowed_methods, allowed_headers)
    end

    core.Debug("CORS: " .. origin .. " allowed")
    txn.http:res_set_header("Access-Control-Allow-Origin", allowed_origin)

    if allowed_origin ~= "*" then
      txn.http:res_add_header("Vary", "Accept-Encoding,Origin")
    end
  end
end

-- Register the actions with HAProxy
core.register_action("cors", {"http-req"}, cors_request, 3)
core.register_action("cors", {"http-res"}, cors_response, 0)
```


## Block Volume Encryption
By default all volumes and their backups are encrypted using the Oracle-provided encryption keys. Each time a volume is cloned or restored from a backup the volume is assigned a new unique encryption key. This link talks about OCI Block Volume Service [BlockVolumeEncryption](https://docs.oracle.com/en-us/iaas/Content/Block/Concepts/overview.htm#BlockVolumeEncryption)

## Docker Installation

### Ubuntu 20.04
**Install docker cert**
```bash
sudo apt install apt-transport-https ca-certificates curl software-properties-common
```
```bash
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
```
**Download from the repo**
```bash
add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable"
```
```bash
apt-cache policy docker-ce
```
**Install docker-ce**
```bash
sudo apt install docker-ce
```
**Add user to docker group and sudo**
```bash
sudo usermod -aG docker ${USER}
```
**Start Docker on reboot**
```bash
sudo systemctl enable docker.service
```
```bash
sudo systemctl enable containerd.service
```
## Docker-compose Installation

**get the docker-composer file**

```bash
sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
```

**Make it executable**
```bash
sudo chmod +x /usr/local/bin/docker-compose
```
```bash
sudo ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose
```
**See docker-compose logs**
```bash
docker-compose logs -f --tail="all"
```