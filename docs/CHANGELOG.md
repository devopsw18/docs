# Changelog

Example Changelog File
TODO : add automation for changelog [link](https://docs.gitlab.com/ee/api/repositories.html#add-changelog-data-to-a-changelog-file)

```bash
update-changelog:
  stage: update_changelog
  script: 
    - latestVersion=$(git describe --tags --abbrev=0)
    - currentVersion=$(grep -oP '(?<=VERSION ")([^"]*)'version.h)
    - |
      curl --header "PRIVATE-TOKEN: token" --data 
      "version=$currentVersion&from=$latestVersion&to=release&branch=release" 
      "https://gitlab.com/api/v4/projects/111/repository/changelog"
  only: 
    - release
```

1.0.0 2022-01-06
