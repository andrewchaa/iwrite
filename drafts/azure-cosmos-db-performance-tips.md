# Azure Cosmos DB performance tips

## Hosting

* For query-intensive workloads, [use Windows 64-bit](https://docs.microsoft.com/en-us/azure/cosmos-db/performance-tips-dotnet-sdk-v3-sql)

## Networking

If possible, user Direc mode, which is the default

Direct mode supports connectivity through TCP protocol and is the default connectivity mode if you're using the [Microsoft.Azure.Cosmos/.NET V3 SDK](https://github.com/Azure/azure-cosmos-dotnet-v3). This offers better performance and requires fewer network hops than Gateway mode.

Gateway mode is handy when your applications run withint a corporate network with strict firewall

## SDK

