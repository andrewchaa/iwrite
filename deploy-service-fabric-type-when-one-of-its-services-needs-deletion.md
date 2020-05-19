# Deploy Service Fabric type when one of its services needs deletion

Sometimes, you create a service and delete it. You don't need it for good or at least not for now. So, you deleted the service. Your solution file doesn't include the project any more. Everything works ok. Now you deploy it to Service Fabric cluster via Azure Devops. Then you get this error.

> "Error Services must be explicitly deleted before removing their Service Types."

You have 3 options

* In SF Explorer, navigate to the service and click Actions &gt; Delete Service
* In PowerShell

```bash
Connect-ServiceFabricCluster
Remove-ServiceFabricService -ServiceName fabric:/MyApp/MyService
```

* In Service Fabric Powershell

Here I use Service Fabric Powershell as I deploy my SF app / type via Azure Devops

#### Service Fabric PowerShell

* Display name: Remove fabric:/MyApp/MyService
* Clsuter Service Connection: &lt;&lt; your connection &gt;&gt;
* Script Type: Inline Script
* Inline Script

```bash
Remove-ServiceFabricService -ServiceName fabric:/MyApp/MyService -Force
```



