# Service Fabric skeleton service

On Service fabric, you can either create ASP.NET Core API service or worker process. I'm going to create a worker service today

## Visual Studio Template Skeleton

Right click on ServiceFabric project &gt; Create a new Service Fabric service

![](../.gitbook/assets/image%20%286%29.png)

Choose "Stateless Service" for worker service, as Stateful is the new evil in cloud era. It will create a skeleton service project. I named it xxxx.xxxx.xxxx.xxxx.Worker

![](../.gitbook/assets/image%20%287%29.png)

You launch it by pressing "CTRL + F5" on Visual Studio. That's my favourite way of deploying the new service fabric into the local dev machine cluster.

## Customise it

### Short name

You deploy it on to the cluster and notice that by default, the name of the service is pretty long. 

```text
fabric:/company.feature.service.type/company.feature.service.type.appName
```

Let's shorten it. Go to ServiceFabric project &gt; ApplicationPackageRoot &gt; Applicationmanifest.xml

Then shorten the name. 

First, remove all name spaces from service name

```markup
# Applicationmanifest.xml
<DefaultServices>
  <Service Name="Worker" ServicePackageActivationMode="ExclusiveProcess">
    <StatelessService ServiceTypeName="WorkerType" InstanceCount="[xxxx.xxxx.xxxx.xxxx.Worker_InstanceCount]">
      <SingletonPartition />
    </StatelessService>
  </Service>
</DefaultServices>
```

Secondly, shorten type name too for convenience

```markup
<!-- Applicationmanifest.xml -->
<DefaultServices>
  <Service Name="Worker" ServicePackageActivationMode="ExclusiveProcess">
    <StatelessService ServiceTypeName="WorkerType" InstanceCount="[xxxx.xxxx.xxxx.xxxx.Worker_InstanceCount]">
      <SingletonPartition />
    </StatelessService>
  </Service>
</DefaultServices>
```

```markup
<!-- ServiceManifest.xml -->
<ServiceTypes>
  <StatelessServiceType ServiceTypeName="WorkerType" />
</ServiceTypes>

```

```csharp
// Program.cs
private static void Main()
{
    try
    {
        ServiceRuntime.RegisterServiceAsync("WorkerType",
            context => new Worker(context)).GetAwaiter().GetResult();

```

