---
id: principle-002-deployment
title: Each service provider is individually deployed from its repository
version: 2019-09-07
author: Poul Kjeldager Sørensen <pks@dotnetdevops.org> https://pksorensen.com
contributers:
- Poul Kjeldager Sørensen <pks@dotnetdevops.org> https://pksorensen.com
tags:
- CI
- CD
- ServiceProvider
---

[ ] Provide Azure function CI / CD pipeline example for azure Devops.
[ ] Ask Daniel if he wants to be Author

# Each service provider is individually deployed from its repository

Each service is individually responsible of its CI and CD pipelines where they must become accessible for reverse proxy/gateway after success deployment. 

## Example



### Install DotNet SDK
```
- task: UseDotNet@2
    displayName: 'Use .NET Core sdk'
    inputs:
    useGlobalJson: true
```