# C\# LINQ in the wild

Note for myself

#### Distinct, ignoring case

Use StringComparer \([https://stackoverflow.com/questions/283063/linq-distinct-operator-ignore-case](https://stackoverflow.com/questions/283063/linq-distinct-operator-ignore-case)\)

```csharp
private static List<string> GetDomains(IList<DomainService> services)
{
    return services
        .Select(x => x.Domain)
        .Distinct(StringComparer.OrdinalIgnoreCase)
        .OrderBy(x => x)
        .ToList();
}
```

#### Flatten queries, returning list of lists

{% embed url="https://stackoverflow.com/questions/958949/difference-between-select-and-selectmany" %}

```csharp
var releases = bankingCore.DeploymentGroups
    .Where(x => x.ReleaseDefinitions != null)
    .SelectMany(x => x.ReleaseDefinitions)
    .ToList();
var builds = bankingCore.DeploymentGroups
    .Where(x => x.BuildDefinitions != null)
    .SelectMany(x => x.BuildDefinitions)
    .ToList();
```



