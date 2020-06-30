# Using TimeSpan configuration values in .NET Core

As [Mark Seeman wrote](https://blog.ploeh.dk/2019/11/25/timespan-configuration-values-in-net-core/), you can use TimeSpan setting in .NET Core's AppSettings.json. It's really handy and readable.

```javascript
"CosmosDb": {
  "ConnectionString": "AccountEndpoint=#{cosmos_db_endpoint}#;AccountKey=#{cosmos_db_primary_master_key}#;",
  "MaxRetryAttemptsOnRateLimitedRequests": 9,
  "MaxRetryWaitTimeOnRateLimitedRequests": "00:00:30" 
}
```

.NET Core support the conversion of the format to TimeSpan out of the box.

```csharp
// CosmosDbOptions.cs
public class CosmosDbOptions
{
    public string ConnectionString { get; set; }
    public int MaxRetryAttemptsOnRateLimitedRequests { get; set; }
    public TimeSpan MaxRetryWaitTimeOnRateLimitedRequests { get; set; }
}

// Startup.cs
public void ConfigureServices(IServiceCollection services)
{
    services.Configure<CosmosDbOptions>(Configuration.GetSection("CosmosDb"));
    var cosmosDbOptions = services.BuildServiceProvider().GetService<IOptions<CosmosDbOptions>>().Value;

    ....
    var client = new CosmosClient(cosmosDbOptions.ConnectionString, 
        new CosmosClientOptions
        {
            MaxRetryAttemptsOnRateLimitedRequests = cosmosDbOptions.MaxRetryAttemptsOnRateLimitedRequests,
            MaxRetryWaitTimeOnRateLimitedRequests = cosmosDbOptions.MaxRetryWaitTimeOnRateLimitedRequests
        });
    var container = client.GetContainer("xxxxx", "xxxxxxxxxxx");

```



