# Register all your services to IServiceCollection

It's the default IoC container for .NET core applications. 

* Read json configuration file and assign the values to typed configuration object.
* Register services

```csharp
public class Startup
{
    private static readonly IServiceCollection Services = new ServiceCollection();

    public static IServiceCollection ConfigureServices()
    {
        var configBuilder = new ConfigurationBuilder();
        configBuilder.AddEnvironmentVariables();
        configBuilder.AddJsonFile("appsettings.json", optional: false, reloadOnChange: true);
#if DEBUG
        configBuilder.AddJsonFile($"appsettings.Development.json", true);
#endif
        var config = configBuilder.Build();
        Services.Configure<GithubOptions>(config.GetSection("Github"));
        
        Services.AddMediatR(typeof(PullPostsCommand).Assembly);
        return Services;
    }

    public static IServiceProvider Build()
    {
        return ConfigureServices()
            .BuildServiceProvider();
    } 
}

```

#### Environment Variables

On Mac, `printenv` will show all available environment variables. 

