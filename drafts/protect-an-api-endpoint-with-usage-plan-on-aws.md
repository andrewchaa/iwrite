# Protect an API endpoint with usage plan on AWS

All of the APIs [our mobile app](https://apps.apple.com/gb/app/navien-uk-boiler-registration/id1475222482) uses are protected by AWS IAM and Cognito User Pool policies. The users need to register for the mobile app first and then get confirmed. Once they log in, they get access token from the user pool. The access token expires in an hour, which is the default behaviour. 

Recently, we received a new business requirement that another central system needs to access the backend and update the warranty information. The system will call this api once a day like a batch job in old days. We needed another policy. The simplest approach is to use API key with usage plan. 

## Usage plan

A [usage plan](https://docs.aws.amazon.com/apigateway/latest/developerguide/api-gateway-api-usage-plans.html) specifies who can access one or more deployed API stages and methods—and also how much and how fast they can access them. The plan uses API keys to identify API clients and meters access to the associated API stages for each key. It also lets you configure throttling limits and quota limits that are enforced on individual client API keys.

## Create a usage plan

Go to API Gateway &gt; Usage plans and click "Create" button.

* Name
* Description

I skipped the stage for now. 

### Usage Plan API Keys

Choose "Add API Key" below to search through your existing API keys. Once a key is associated with a plan, API Gateway will meter all requests from the key and apply the plan's throttling and quota limits.

I've created a new one as I don't have any existing one. 

Now you have an active usage plan with an api key. The client can use this API key to access the API.

