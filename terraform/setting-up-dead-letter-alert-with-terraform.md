# Setting up dead letter alert with Terraform

```text
resource "azurerm_monitor_action_group" "pager" {
  name                = "${var.organisation}-${var.system}-${var.environment}-${local.insights_app_name}_failure_action-${var.location}"
  resource_group_name = azurerm_resource_group.app_insights.name
  short_name          = "failures"
  enabled             = true

  webhook_receiver {
    name              = "Pager Duty"
    service_uri       = var.pager_duty_service_url
  }

  depends_on = [ azurerm_resource_group.app_insights ]
}

resource "azurerm_monitor_metric_alert" "deadLetteralert" {
  name = lower(
	    "al-${var.organisation}-${var.system}-${var.environment}-dead-messages-${var.location}",
  )
  resource_group_name = var.servicebus_resource_group_name
  scopes      = ["/subscriptions/${var.subscription_id}/resourceGroups/${var.servicebus_resource_group_name}/providers/Microsoft.ServiceBus/namespaces/${var.servicebus_namespace}"]

  description = "An alert rule to monitor dead lettered messages"
  enabled     = true
  frequency   = "PT5M"
  severity    = 1

  criteria {
    metric_namespace = "Microsoft.ServiceBus/namespaces"
    metric_name      = "DeadletteredMessages"
    aggregation      = "Average"
    operator         = "GreaterThan"
    threshold        = 0

    dimension {
      name     = "EntityName"
      operator = "Include"
      values   = [var.institution_onboarding_rollback_queue_name]
    }
  }

  action {
    action_group_id = azurerm_monitor_action_group.pager.id
  }

  depends_on = [ azurerm_application_insights.app_insights ]
}
```

