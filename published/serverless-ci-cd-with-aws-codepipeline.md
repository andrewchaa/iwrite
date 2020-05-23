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
* branch: refs/head

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

#### Role

To support serverless to create stack, the role should have the below permission

* AWSLambdaFullAccess
* IAMFullAccess
* AmazonAPIGatewayAdministrator
* CloudFormationAdministrator

#### Buildspec

* Build specification: Use a buildspec file
* Logs: CloudWatch

```yaml
version: 0.2
env:
  variables:
    DOTNET_ROOT: /root/.dotnet
phases:
  install:
    runtime-versions:
      dotnet: 2.1
  pre_build:
    commands:
      - npm install -g serverless
      - cd src
      - cd Navien.Installers.Lambdas
      - dotnet clean
      - dotnet restore
  build:
    commands:
      - ./build.sh
      - serverless deploy --stage cicd | tee deploy.out
  post_build:
    commands:
      - . ./test.sh

```

### Add deploy stage

Skip

### Review

Review and "Create pipeline"

