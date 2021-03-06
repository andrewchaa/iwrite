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
  cli_name = lower("${var.environment}-servicebus-domainevent-cli")
}

```

```text
# resource-ad-application
resource "azuread_application" "cli" {
  name                       = local.cli_name
  homepage                   = "https://${local.cli_name}"
  identifier_uris            = ["https://${local.cli_name}"]
  reply_urls                 = ["https://${local.cli_name}"]
  available_to_other_tenants = false
  oauth2_allow_implicit_flow = true

  provisioner "local-exec" {
    when        = destroy
    interpreter = ["pwsh", "-file"]
    command     = "${path.module}/tpl.service_connection_destroy.ps1"
    environment = {
      name = self.name
    }
  }
}

resource "azuread_service_principal" "cli" {
  application_id               = azuread_application.cli.application_id
  app_role_assignment_required = false
}

resource "random_password" "cli" {
  length  = 40
  special = false
}

resource "azuread_service_principal_password" "cli" {
  service_principal_id = azuread_service_principal.cli.id
  value                = random_password.cli.result
  end_date_relative    = "8760h"
}

resource "azurerm_role_assignment" "cli_receive" {
  scope                            = azurerm_servicebus_namespace.service_bus.id
  role_definition_name             = "Azure Service Bus Data Receiver"
  principal_id                     = azuread_service_principal.cli.id
  skip_service_principal_aad_check = true
}

resource "null_resource" "cli_service_connection_create" {
  triggers = {
    client_secret = azuread_service_principal_password.cli.value
    client_id     = azuread_service_principal.cli.application_id
  }

  provisioner "local-exec" {
    interpreter = ["pwsh", "-file"]
    command     = "${path.module}/tpl.service_connection_create.ps1"
    environment = {
      name              = local.cli_name
      client_id         = azuread_service_principal.cli.application_id
      client_secret     = azuread_service_principal_password.cli.value
      subscription_id   = data.azurerm_client_config.current.subscription_id
      subscription_name = data.azurerm_subscription.current.display_name
      tenant_id         = data.azurerm_client_config.current.tenant_id
    }
  }
}

```

I've used `role_definition_name` to assign a built-in role. You can get the full list of Azure built-in roles from [https://docs.microsoft.com/en-us/azure/role-based-access-control/built-in-roles](https://docs.microsoft.com/en-us/azure/role-based-access-control/built-in-roles)

