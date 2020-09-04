# Encrypt a sensitive information with Azure Key Vault

[Azure Key Vault](https://docs.microsoft.com/en-gb/azure/key-vault/general/basic-concepts) is a tool for securely storing and accessing secrets. A secret is anything that you want to tightly controll access to, such as API Keys. Another practical use case is storing the connection string to the database and and to the Service Bus in Azure Key Vault. 

## Things Azure Key Vault protects

### Key

Cryptographic keys used in other Microsoft Azure services

### Secret

Any sensitive information such as connection strings to SQL Server, Redis, or Storage.

### Certificate

x509 certificates being used in HTTPS / SSL communications

## Provision key Vault with Terraform

```text
resource "azurerm_resource_group" "web-resource-group" {
  name     = "${var.organisation}-${var.system}-${var.environment}-web-${var.location}"
  location = var.location
  tags     = var.tags
}

resource "azurerm_key_vault" "web" {
  name                            = "${var.environment}-web"
  resource_group_name             = azurerm_resource_group.web-resource-group.name
  location                        = azurerm_resource_group.web-resource-group.location
  sku_name                        = "standard"
  tenant_id                       = data.azurerm_client_config.client_config.tenant_id
  enabled_for_deployment          = true
  enabled_for_template_deployment = true
  tags                            = var.tags
}

# Access to terraform SP
data "azurerm_client_config" "client_config" {}

resource "azurerm_key_vault_access_policy" "ci" {
  key_vault_id = azurerm_key_vault.web.id
  tenant_id    = data.azurerm_client_config.client_config.tenant_id
  object_id    = data.azurerm_client_config.client_config.object_id

  certificate_permissions = [
    "get",
    "list",
    "update",
    "create",
    "import",
    "delete",
    "managecontacts",
    "manageissuers",
    "getissuers",
    "listissuers",
    "setissuers",
    "deleteissuers",
    "backup",
    "purge",
    "recover",
    "restore",
  ]

  key_permissions = [
    "create",
    "decrypt",
    "delete",
    "encrypt",
    "get",
    "import",
    "list",
    "purge",
    "recover",
    "restore",
    "sign",
    "unwrapKey",
    "update",
    "verify",
    "wrapKey",
  ]

  secret_permissions = [
    "delete",
    "get",
    "list",
    "set",
    "backup",
    "purge",
    "recover",
    "restore",
  ]

  storage_permissions = [
    "backup",
    "delete",
    "deletesas",
    "get",
    "getsas",
    "list",
    "listsas",
    "purge",
    "recover",
    "regeneratekey",
    "restore",
    "set",
    "setsas",
    "update",
  ]
}

resource "azurerm_key_vault_access_policy" "web-service-principle" {
  key_vault_id = azurerm_key_vault.web.id
  tenant_id    = data.azurerm_client_config.client_config.tenant_id
  object_id    = data.azurerm_client_config.client_config.object_id

  certificate_permissions = [
    "get"
  ]

  key_permissions = [
    "get"
  ]

  secret_permissions = [
    "get"
  ]
}

output "web_keyvault_url" {
  value = azurerm_key_vault.web.vault_uri
}
```



