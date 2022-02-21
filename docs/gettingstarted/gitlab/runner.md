---
sidebar_position: 2
sidebar_label: GitLab Runner
---

# GitLab Runner

## Setting up Gitlab Runner on ubuntu 20.04 server

## SSH into ubuntu server
> Change to root
```
sudo -i
apt update
apt upgrade -y
```
> copy below code into terminal


```
curl -L "https://packages.gitlab.com/install/repositories/runner/gitlab-runner/script.deb.sh" | sudo bash
```


```
apt-get install gitlab-runner
```
> To get the "REG-TOKEN" go to passit and look for "Gitlab-bot"
> Log into gitlab using the "Gitlab-bot" account, go to groups -> Carelyo-ReactJS -> Settings -> CI/CD -> expand Runners and copy the token under "Group Runners"
```
gitlab-runner register   --non-interactive   --url "https://gitlab.com"   --registration-token "REG-TOKEN"   --executor "shell"   --description "carelyo-runner-2"   --tag-list "ocirunner,docker"   --run-
untagged="true"   --locked="true"
```

>Change registration token "REG-TOKEN" to Group token from carelyo, change description
to suiting name.

# Install Docker and setup permission

>Copy the below commands and paste them into the terminal.



```
apt-get update
```

```
apt-get install \
    ca-certificates \
    curl \
    gnupg \
    lsb-release
```

```
url -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
```

```
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
  ```

```
sudo groupadd docker
```

```
sudo usermod -aG docker $USER
```

```
newgrp docker
```

```
sudo chmod 666 /var/run/docker.sock
```


# Required additional software

```
sudo apt install nodejs
```
```
sudo apt install npm
```
```
sudo npm install --global yarn
```
