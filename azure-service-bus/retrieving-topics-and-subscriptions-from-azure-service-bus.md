# Retrieving Topics and Subscriptions from Azure Service Bus

Recently, I have been working on a small project of a tool that generates all the domain events automatically. To get all the topics details, it connects to the service bus and retrieve all topic descriptions.

```csharp
var managementClient = new ManagementClient(_configs.ServiceBusConnectionString);
var topics = new List<TopicDescription>();

for (int i = 0; i < 1000; i += 100)
{
    var ts = await managementClient.GetTopicsAsync(100, i);
    if (!ts.Any())
        break;

    topics.AddRange(ts);
}

await Populate(topics.Select(x => new DomainEventTopic(x.Path, 0)));

```

