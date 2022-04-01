---
sidebar_position: 4
sidebar_label: Components Library
---
# @carelyo/component

The component library is a collections of components prevalent components and templates used across the carelyo apps.
You can install the component library in any carelyo project and use them.
The library is written in typescript and tests are written for each component. 
Read more about this in the [repo](https://gitlab.com/carelyo/frontend-team/component-library/-/blob/develop/README.md)

## Installing the package
To install the package you need to add the repository to your registry you can do that by adding it to a 
*.nmrc* file or running the following commands

### [Create personal access token](https://docs.gitlab.com/ee/user/profile/personal_access_tokens.html)
```bash
# Set URL for the package.
# npm i @carelyo/component will use this URL for download
npm config set @carelyo:registry=https://gitlab.com/api/v4/projects/34809448/packages/npm/

# Add the token for the scoped packages URL. Replace <your_token> with your personal access token
npm config set -- '//gitlab.example.com/api/v4/projects/34809448/packages/npm/:_authToken' "<your_token>"
```


### Install
````bash
npm i @carelyo/components
````