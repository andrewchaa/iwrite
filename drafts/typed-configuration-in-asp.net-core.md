# Typed Configuration in ASP.NET Core

Another great thing I like is Typed Configuration in .NET Core. You create a class and bind the configuration section to it. It was possible before but it is much easier now.

```csharp
public class KeyVaultOptions
{
    public string TenantId { get; set; }
    public string ClientId { get; set; }
    public string ClientSecret { get; set; }
}

```



