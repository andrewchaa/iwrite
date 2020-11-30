# Conditional Build on Azure Devops Pipeline

We have one build that runs nightly to generate scores for every service in the company. It has a yaml file that defines all services and teams. For the last two weeks, I worked on this file and discovered that the file gets broken more often than I expects. So I wanted to do something about it. 

The first step is to add a test on the buld. It didn't have any build trigger. So I added it.

```yaml
name: scoring-services
trigger:
  branches:
    exclude:
      - master

```

Now also shedule it to run it nightly

```yaml
schedules:
  - cron: "0 0 * * *"
    displayName: Daily midnight build
    always: true
    branches:
      include:
        - master
```

To be continued ...

