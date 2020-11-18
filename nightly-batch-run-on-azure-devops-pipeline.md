# Nightly batch run on Azure DevOps Pipeline

I have a simple console app that parses a yaml file and create wiki pages upon it. The yaml has a list of all services with details like domain and team name. The wiki page needs update once a day.

My choice of solution is 

* Create a console app that does the job.
* Set up a pipeline that runs nightly to execute the console app.

First, build a console app and publish it as artifact.

```yaml
name: 1.0$(Rev:.r)

trigger:
  branches:
    include:
    - master
    - hotfix/*
    - release/*
    - feature/*
    - bugfix/*
    - backlog/*
    - task/*

variables:
  major: 1
  minor: 0
  patch: $[counter(variables['minor'], 0)]
  version: $(major).$(minor).$(patch)
  dotnetCliVersion: 3.1.101
  buildConfiguration: Release
  buildPlatform: x64
  buildProjects: "**/*.csproj"
  cliProject: '**/*Clis.csproj'

jobs:
  - job: build_solution
    pool:
      vmImage: windows-2019
    steps:
      - checkout: self
        clean: true
        
      - task: UseDotNet@2        
        inputs:
          packageType: 'sdk'
          version: $(dotnetCliVersion)
          displayName: dotnet install

      # Restore packages
      - task: DotNetCoreCLI@2
        displayName: Restore Packages
        inputs:
          command: restore
          feedsToUse: select
          vstsFeed: 'innovation-release'
          includeNuGetOrg: false
          projects: $(buildProjects)
          noCache: false

      # Build          
      - task: DotNetCoreCLI@2
        displayName: Build Projects
        inputs:
          projects: $(buildProjects)
          packDirectory: '$(Build.ArtifactStagingDirectory)'
          arguments: '-c $(buildConfiguration) /p:Platform=x64 /p:Version=$(Build.BuildNumber) --no-restore'      

      # Publish the cli application
      - task: DotNetCoreCLI@2
        displayName: Publish Console Project
        inputs:
          command: publish
          publishWebProjects: false
          zipAfterPublish: false
          projects: $(cliProject)
          arguments: --no-build --no-restore -c Release /p:Platform=x64 /p:Version=$(Build.BuildNumber) -o "$(Build.ArtifactStagingDirectory)\cli\"

      - publish: $(Build.ArtifactStagingDirectory)\cli
        displayName: Publish Artifact
        artifact: cli

      - pwsh: |
          Write-Host "##vso[build.addbuildtag]$(version)"
        displayName: add build tag
```

Now, I have a build artifact that contains the console application. Create another pipeline that will download the artifact and run the executable. 

```yaml
name: $(Build.DefinitionName)-$(Date:yyyyMMdd)$(Rev:.r)
schedules:
  - cron: "0 0 * * *"
    displayName: Nightly run
    always: true
    branches:
      include:
        - master
trigger: none
parameters:  
  - name: build_tag
    displayName: Build Tag
    type: string
    default: latest
variables:
  - name: major
    value: 1
  - name: minor
    value: 0
  - name: patch
    value: $[counter(variables['minor'], 0)]
  - name: version
    value: $(major).$(minor).$(patch)
resources:
  repositories:
    - repository: templates
      type: git
      name: /yaml-templates
      ref: refs/heads/master      
  pipelines:
    - pipeline: build
      source: ci

jobs:
  - job: run_cli
    pool:
      vmImage: windows-2019
    steps:
      - download: none
      - task: DownloadPipelineArtifact@2
        displayName: download cli from '$(resources.pipeline.build.pipelineName)' with tag '${{ parameters.build_tag }}'
        name: download_artifact_console
        inputs:
          source: specific
          project: $(System.TeamProjectId)
          pipeline: $(resources.pipeline.build.pipelineID)
          artifactName: cli
          path: $(Pipeline.Workspace)/cli
          runVersion: latest
          allowPartiallySucceededBuilds: false
          allowFailedBuilds: false
      # Execute cli app
      - pwsh: ./Clis.exe --cmd create-domainpage
        workingDirectory: $(Pipeline.Workspace)/cli
        displayName: Executing script
        env:
          wiki-token: $(wiki-token)

```

Lastly, we need to the access token for the cli app. It needs read only access to a repository and write access to wiki. You can create variables for the pipeline. Set it as secret so that the value wouldn't be visible.

