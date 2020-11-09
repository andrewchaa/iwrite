# Programatically create wiki pages on Azure DevOps

The API documentation is here, [https://docs.microsoft.com/en-us/rest/api/azure/devops/wiki/pages/create%20or%20update?view=azure-devops-rest-4.1](https://docs.microsoft.com/en-us/rest/api/azure/devops/wiki/pages/create%20or%20update?view=azure-devops-rest-4.1)

It has a handy client library: [https://docs.microsoft.com/en-us/azure/devops/integrate/get-started/client-libraries/samples?view=azure-devops](https://docs.microsoft.com/en-us/azure/devops/integrate/get-started/client-libraries/samples?view=azure-devops)

For me, using the client library was much easier. The library has several client HTTP client and I used WikiHttpClient. If you register it in your ServiceCollection, you can use it by getting it from IServiceProvider.

```csharp
public class Startup
{
    private static readonly IServiceCollection Services = new ServiceCollection();

    public static IServiceProvider ConfigureServices()
    {
        var devopsWikiToken = Environment.GetEnvironmentVariable("devops-wiki-token");
        var vssConnection = new VssConnection(new Uri("https://dev.azure.com/<your org>"), 
            new VssBasicCredential(string.Empty, devopsWikiToken));

        Services.AddSingleton(x => vssConnection.GetClient<WikiHttpClient>());

        return Services.BuildServiceProvider();
    }
}

```

