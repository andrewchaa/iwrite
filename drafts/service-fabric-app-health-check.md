# Service Fabric app health check

Health check is a common pattern in cloud native applications, especially in Kubernetes services. Service Fabric supports health check. When you deploy a new version to a cluster, you can set up the  pipeline so that if the health is bad, the deployment fail. 

Add health check libraries

```bash
AspNetCore.HealthChecks.CosmosDb
```

Register the service against IHealthCheck interface

```csharp
// Startup.cs
public void ConfigureServices(IServiceCollection services)
{
    ....
    services.AddTransient<IEnumerable<IHealthCheck>>(x =>
    {
        var cosmosDbOptions = x.GetService<IOptions<CosmosDbOptions>>().Value;

        return new List<IHealthCheck>{new CosmosDbHealthCheck(cosmosDbOptions.ConnectionString)};
    });

}

```

