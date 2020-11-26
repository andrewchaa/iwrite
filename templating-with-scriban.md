# Templating with scriban

 Scriban is "a fast, powerful, safe and lightweight scripting language and engine for .NET, which was primarily developed for text templating with a compatibility mode for parsing `liquid` templates." \([https://github.com/lunet-io/scriban](https://github.com/lunet-io/scriban)\)

Simply create a template and pass data object as parameter.

```csharp
    var template = Template.Parse(@"
##Ownership 
| **Domain Event** | **Subscriptions** | **Domain** | **Sub Domain** | **Team**  | **Team Lead** | **CodeBase**  |
|--|--|--|--|--|--|--|
| {{name}} |   | [{{domain}}](/{{domain_link}}) | {{sub_domain}} | {{team}}  |   | {{repository}}  |

<br>
<br>
");
    return template.Render(new
    {
        _domainEvent.Name,
        _serviceDefinition.Domain,
        DomainLink = $"{CbWiki.DomainPageRoot}/{_serviceDefinition.Domain} Domain".ToWikiLink(),
        _serviceDefinition.SubDomain,
        _serviceDefinition.Team,
        _serviceDefinition.Repository
    });
    
```

