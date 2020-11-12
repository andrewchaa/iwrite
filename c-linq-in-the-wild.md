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

