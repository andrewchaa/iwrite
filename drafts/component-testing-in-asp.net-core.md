# Component testing in ASP.NET Core

I define "Component testing" as tests that only mocks external depenencies. For example, i only mock API request, Service Bus event publishing, and database call. The SUT, System Under Test, is public interface, in this case, API endpoints.

It gives many benefits. By not using any other mocks, you increase the test coverage of the code massively. The test follow the same path as the real requsts comes in. It's more realistic test without the performance issue.

Create a xUnit test project. 

## WebApplicationFactory

Then you need a WebApplicationFactory to create a host for the tests. Install this package first.

```text
Microsoft.AspNetCore.Mvc.Testing
```

```csharp
public class TestApplicationFactory<TStartup> : WebApplicationFactory<TStartup> where TStartup : class
{
    public TestApplicationFactory() { }

    protected override IWebHostBuilder CreateWebHostBuilder() => new WebHostBuilder();

    protected override void ConfigureWebHost(IWebHostBuilder builder)
    {
        builder
            .UseKestrel()
            .UseEnvironment(Environment.GetEnvironmentVariable("ASPNETCORE_ENVIRONMENT") ?? "Development")
            .UseContentRoot(Directory.GetCurrentDirectory())
            .ConfigureAppConfiguration((context, configBuilder) =>
            {
                configBuilder.SetBasePath(context.HostingEnvironment.ContentRootPath);
                configBuilder.AddJsonFile("appsettings.json", true);
                configBuilder.AddJsonFile("appsettings.Development.json", optional: true, reloadOnChange: true);
            })
            .UseStartup<Startup>();

        builder.ConfigureTestServices(services =>
        {
        });
    }
}

```

## Tests

You can get HttpClient from the test application factory. The client will call to the local in-memory http host. I used AutoFixture to populate the request object

```csharp
public class CreateTransactionTests : IClassFixture<TestApplicationFactory<Startup>>
{
    private HttpClient _client;
    private Fixture _fixture;

    public CreateTransactionTests(TestApplicationFactory<Startup> factory)
    {
        _client = factory.CreateClient();
        _fixture = new Fixture();
    }

    [Fact]
    public async Task Should_return_200_Ok()
    {
        var transactionId = Guid.NewGuid();
        var request = _fixture.Build<CreateTransactionRequest>()
            .Create();
        var response = await _client.PutAsync($"/v1/transactions/{transactionId}", GetContent(request));

        Assert.Equal(HttpStatusCode.OK, response.StatusCode);
    }

    private static HttpContent GetContent<T>(T body)
    {
        var stringContent = JsonConvert.SerializeObject(body);
        return new StringContent(stringContent, Encoding.UTF8, "application/json");
    }

}

```

What is IClassFixture. It's "used to decorate xUnit.net test classes and collections to indicate a test which has per-test-class fixture data". An instance of the fixture data is initialized just before the first test in the class is run, and if it implements IDisposable, is disposed after the last test in the class is run





