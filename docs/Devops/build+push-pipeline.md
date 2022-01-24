
# Introduction
The basic pipeline files can be found [here](https://gitlab.com/carelyo/ci_cd-pipeline-files). 

# Files
## main.yml

This is the main pipeline for building images on merge requests and pushing them to DockerHub.

## dev-staging_branches.yml
Imports and expands on `main.yml`.
This file is for repos where we only want the Build+Push pipeline to run on the *Develop* & *Staging* branches. The only change (for now) compared to **main.yml** is the addition of

    except:
		variables:
		- $CI_COMMIT_REF_NAME =~ /main/

Which prevents it from being run on the main branch.

You could also add it directly to the repos *gitlab-ci.yml* at the bottom after importing **main.yml**, but this is a lot more efficient as it's used for multiple repos.

# GitLab configuration
The variables used in the `gitlab-ci.yml` are set on a group-wide level through [its settings](https://gitlab.com/groups/carelyo/-/settings/ci_cd). It's also possible to set these on a per-project basis.

## Variables
 - `CI_REGISTRY` is where the DockerHub repo URL is stored.  
 - - These variables [are masked](https://docs.gitlab.com/ee/ci/variables/index.html#mask-a-cicd-variable), meaning they won't show up in job logs in plain text.
 - - `CI_REGISTRY_PASSWORD` is the DockerHub access token. The normal password is possible too but is less secure in case someone gains access to the GitLab account. Also it's not posssible to mask certain passwords(meaning ones with special characters etc).
 -- `CI_REGISTRY_USER` is where the DockerHub repo URL is stored.
