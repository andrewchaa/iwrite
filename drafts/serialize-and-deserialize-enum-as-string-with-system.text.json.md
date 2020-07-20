# Serialize and deserialize enum as string with System.Text.Json

The same problem with a different tool. By default, enums are serialized as integer, which I think is not right. So to handle string values in API payload, you have to set string enum converter.

A few different wasy to achive the same goal. 

## Attribute

use [JsonConverter](https://docs.microsoft.com/en-us/dotnet/api/system.text.json.serialization.jsonconverterattribute?view=netcore-3.0) and [JsonStringEnumConverter](https://docs.microsoft.com/en-us/dotnet/api/system.text.json.serialization.jsonstringenumconverter?view=netcore-3.0).

```csharp
[JsonConverter(typeof(JsonStringEnumConverter))]
public enum AccountIdKind
{
    Iban = 1,
    Bban = 2
}
```

## Configure in Startup

```csharp
public void ConfigureServices(IServiceCollection services)
{
    ...
    services.AddControllers()
        .AddJsonOptions(x =>
        {
            x.JsonSerializerOptions.Converters.Add(new JsonStringEnumConverter());
        });

```



