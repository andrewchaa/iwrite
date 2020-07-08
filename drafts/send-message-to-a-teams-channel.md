# Send message to a Teams' channel

To merge a PR into main branch, it takes quite a few approvals and often it takes a while to get all the approvals. Also when people are under pressure, reviewing others PR gets delayed or depriortised. It was becoming an issue that PRs stay pending without be resolved or merged. 

We started posting pending PRs in the group chat. Soon, it became a chore. So I thought we could automate it by scripting it.

## Creating an [incoming webhook](https://docs.microsoft.com/en-us/microsoftteams/platform/webhooks-and-connectors/how-to/add-incoming-webhook)

Click ... on the top right corner to open the menu and choose Connector

![](../.gitbook/assets/image%20%2814%29.png)

Select Incoming Webhook. It'll give you an api endpoint for you to use.

```bash
https://outlook.office.com/webhook/xxxxx/IncomingWebhook/xxxx
```

Now Let's use the webhook endpoint to [send messages](https://docs.microsoft.com/en-us/microsoftteams/platform/webhooks-and-connectors/how-to/connectors-using).

## Sending messages

There's a playground to test your message format: [https://amdesigner.azurewebsites.net/](https://amdesigner.azurewebsites.net/)

To send a message, you call the webhook endpoint with string content. It supports mark down syntax.

```csharp
var chatRoom =
    "https://outlook.office.com/webhook/xxxxxxx";

var card = GetBody(facts);

var client = new HttpClient();
var response = await client.PostAsync(
    chatRoom,
    new StringContent(card));

```







