# GitLab & Kubernetes
GitLab connects to our K8s cluster through their [agent](https://docs.gitlab.com/ee/user/clusters/agent/install/index.html). The agent & its config file are located [in the deployment repository](https://gitlab.com/carelyo/deployment). 

The deployment process is specified in each repo's `.gitlab-ci.yml` file.
## The config file
[The configuration file](https://gitlab.com/carelyo/deployment/-/blob/Develop/.gitlab/agents/gitlab-cluster-agent/config.yaml) is used to set various settings for the runner, for example to grant access to it from within the entire Carelyo group in GitLab.
## Updating the GitLab agent
In order to update the agent from time to time with new features from GitLab, critical security patches etc, [follow these instructions](https://docs.gitlab.com/ee/user/clusters/agent/install/index.html#update-the-agent-version).
