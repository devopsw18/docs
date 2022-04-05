---
sidebar_position: 0
sidebar_label: Components Library
---
# Component Library

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

### Stories
Stories are how you view and develop your components.
You create a component for the component where you can display the functionalities
Locally you can view your stories by runnin
```bash
npm run start
```
Merging your feature branches to develop sucessful builds update the storybook page which can be found [here](https://carelyo.gitlab.io/frontend-team/component-library/?path=/story/examples--default)

### Installing Packages

Packages should be installed as dev dependcies in most cases unless it a necessary package.

Addition of any package should be justified by it being used in multiple component if a package is needed for only one functionality it much better to just write that code yourself.