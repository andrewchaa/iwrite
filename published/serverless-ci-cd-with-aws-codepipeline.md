# Serverless CI/CD with AWS CodePipeline

## Create a new Pipeline

### Choose pipeline settings

* name: navien-installer-infrastructure
* Service role: New service role
* Role name: automatically populated

### Add source stage

* Provider: Github
* Use "Connect to Github"
* Change detection options: Github webhooks \(recommended\)

### Add build stage

* Provider: AWS CodeBuild
* Region: Europe \(Ireland\)
* Create a new project

If you haven't created a project, create one now

### Project

* Name: navien-installer-infrastructure
* Environment image: Managed image
* Operating system: Ubuntu
* Runtime: Standard
* Image: aws/codebuild/standard:4.0
* Image version: Always use the latest
* Environment type: Linux
* Service role: New service role

#### Buildspec

* Build specification: Use a buildspec file
* Logs: CloudWatch

### Add deploy stage

Skip

### Review

Review and "Create pipeline"

