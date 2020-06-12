# Calling api endpoints with Refit

[Refit ](https://github.com/reactiveui/refit)is

> The automatic type-safe REST library for .NET Core, Xamarin and .NET. Heavily inspired by Square's Retrofit library, Refit turns your REST API into a live interface

Refit turns your REST API into a live interface

```csharp
public interface IApi
{
    [Put("/v1/transactions/{transactionId}")]
    Task<IApiResponse> CreateTransaction(Guid transactionId);
}
```



