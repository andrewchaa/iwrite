# Create a lambda function that's called on AWS SNS topic message

AWS [SNS](https://docs.aws.amazon.com/sns/latest/dg/welcome.html) is a managed service that provides message delivery from publishers to subscribers. Recently, I had a few incidents with my personal mobile app project. It calls an external API to create a company for a third party entity. The issue was their APIs were very unstable, often failing to respond to the request. I need to convert the api call to messaging, so that I can rerun those dead-lettered message in the next day, if any.

Let's [create a function](https://www.serverless.com/framework/docs/providers/aws/events/sns/) that subscribes to a SNS topic



