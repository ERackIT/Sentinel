# Install and manage the Azure Monitor Agent Extension

_Source:_ [Install and manage the Azure Monitor Agent | Microsoft Learn](https://learn.microsoft.com/en-us/azure/azure-monitor/agents/azure-monitor-agent-manage?tabs=azure-cli)   

## Install the AMA agent extension

You can view the availability of the Azure Monitor Linux Agent extension versions in each region by running:

```
az vm extension image list-versions -l <region> --name AzureMonitorLinuxAgent -p Microsoft.Azure.Monitor
```
  

### Install Agent with Auto Updates
To deploy the Azure Monitor Linux Agent Extension for **user-assigned** managed identity:
```
az vm extension set --name AzureMonitorLinuxAgent --publisher Microsoft.Azure.Monitor --ids <vm-resource-id> --enable-auto-upgrade true --settings '{"authentication":{"managedIdentity":{"identifier-name":"mi_res_id","identifier-value":"/subscriptions/<my-subscription-id>/resourceGroups/<my-resource-group>/providers/Microsoft.ManagedIdentity/userAssignedIdentities/<my-user-assigned-identity>"}}}'
```
  
To deploy the Azure Monitor Linux Agent Extension for **system-assigned** managed identity::
```
az vm extension set --name AzureMonitorLinuxAgent --publisher Microsoft.Azure.Monitor --ids <vm-resource-id> --enable-auto-upgrade true
```

  
### Install Agent with Auto Updates Disabled
To deploy the Azure Monitor Linux Agent Extension for **user-assigned** managed identity:
```
az vm extension set --name AzureMonitorLinuxAgent --publisher Microsoft.Azure.Monitor --ids <vm-resource-id> --enable-auto-upgrade false --settings '{"authentication":{"managedIdentity":{"identifier-name":"mi_res_id","identifier-value":"/subscriptions/<my-subscription-id>/resourceGroups/<my-resource-group>/providers/Microsoft.ManagedIdentity/userAssignedIdentities/<my-user-assigned-identity>"}}}'
```
  
  
To deploy the Azure Monitor Linux Agent Extension for **system-assigned** managed identity::
```
az vm extension set --name AzureMonitorLinuxAgent --publisher Microsoft.Azure.Monitor --ids <vm-resource-id> --enable-auto-upgrade false
```

  
## Update Agent

To do a one time update of the Azure Monitor Linux Agent:
```
az connectedmachine upgrade-extension --extension-targets "{\"Microsoft.Azure.Monitor.AzureMonitorLinuxAgent\":{\"targetVersion\":\"<target-version-number>\"}}" --machine-name <arc-server-name> --resource-group <resource-group-name>
```

  
  
To **enable auto updates** of the Azure Monitor Linux Agent:
```
az connectedmachine extension update --name AzureMonitorLinuxAgent --machine-name <arc-server-name> --resource-group <resource-group-name> --enable-auto-upgrade true
```

