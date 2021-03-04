# Deserializing yaml file in C\#

C\# supports serialization and deserialization of JSON out of the box with System.Text.Json. Yaml is a simplified version of JSON, yet you don't have much choice in the package that could handle YAML, other than [YAML.NET](https://github.com/aaubry/YamlDotNet) 

### Deserialize YAML

```csharp
var deserializer = new DeserializerBuilder()
        .Build();        
var banking = deserializer.Deserialize<Banking>(bankingYaml))
```

This is the simplest form. You can specify what naming convention you can use, such as camelcasing. I used it once it had a quirky behaviour. For example,

* yamlFile matches C\# object's YamlFile property.
* yamlName doesn't match YamlName property. It looks for Yamlname property.

TBC

