# Logging onto Application Insights from ASP.NET Core api service

You can send trace logs to Application Insight.

Install Microsoft.ApplicationInsights.AspNetCore package

```bash
Microsoft.ApplicationInsights.AspNetCore
```

Add Application Insights telemetery in ConfigureServices

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddControllers();
    services.AddApplicationInsightsTelemetry();
}
```

Set up the instrumentation key in your appsettings.json

```javascript
{
  "ApplicationInsights": {
    "InstrumentationKey": "#{app_insights_instrumentation_key}#"
  },
  "Logging": {
    "LogLevel": {
      "Default": "Information",
      "Microsoft": "Warning",
      "Microsoft.Hosting.Lifetime": "Information"
    }
  }
}
```

