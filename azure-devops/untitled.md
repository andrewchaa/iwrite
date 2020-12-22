# Connecting to Service Bus from Azure DevOps Pipeline

The simplest option is to store a connection string on the service bus and save it as pipeline variable. Yet, for security, let's try a different option. 

* Create an Azure AD application and principal
* Create a service connection in Azure DevOps. It'll be Azure Resource Manager type connection and  will have the subscription for the service bus and the service principal that has access to the service bus.

The benefits are 1\) you can give just enough scope of permission to the service principal and 2\) see the usage history on Azure Devops

![](../.gitbook/assets/image%20%2825%29.png)

Let's create terraform scripts to provision the Azure AD application and principal.

```text
# locals.tf
locals {
  domainevent_cli_name = lower("${var.environment}-servicebus-domainevent-cli")
}

```

