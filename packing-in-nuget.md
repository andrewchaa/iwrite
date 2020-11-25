# Packing in Nuget

## Support multiple .NET versions

Recently, I came across an error, 'DomainEvents.AttributesPackage 1.0.55'. You are trying to install this package into a project that targets 'Unsupported,Version=v0.0', but the package does not contain any assembly references or content files that are compatible with that framework. For more information, contact the package author. It was because I didn't [support multiple .NET versions](https://docs.microsoft.com/en-us/nuget/create-packages/supporting-multiple-target-frameworks). 

Let's [update project file to support multiple .NET framework versions](https://docs.microsoft.com/en-us/nuget/create-packages/multiple-target-frameworks-project-file).

```markup
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFrameworks>netstandard2.1;net45;net46</TargetFrameworks>
    <Platforms>x64</Platforms>
    <IsPackable>True</IsPackable>
    <Description>Decorate your domain event classes to publish the event details to ClearBank Domain Events wiki</Description>
    <Company>Bank</Company>
    <Authors>Bank </Authors>
    <Product>Domain Events Package</Product>
  </PropertyGroup>

</Project>

```

Now, `dotnet pack` will create .nupkg targetting both .NET Standard 2.1 and .NET Framework 4.5 and 4.6. Make sure you reload the project. 

