# Build a React app with Azure Devops Pipeline

## New Pipeline

* Create a new pipeline by clicking "New pipeline"
* I chose "Azure Repos Git"

## Pipeline yaml

```yaml
# azure-pipelines.yml

trigger:
- master

pool:
  vmImage: 'ubuntu-latest'

variables:
  azureSubscription: team-xxxx
  WebAppName: <<your app name here>>  
  system.debug: False

steps:

- task: Npm@1
  inputs:
    command: 'install'
    workingDir: 'src/'
    verbose: False

- task: Npm@1
  inputs:
    command: 'custom'
    workingDir: 'src/'
    customCommand: 'run build'
    verbose: False
```

