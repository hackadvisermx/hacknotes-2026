
```
🎄 Welcome to The Open Door Challenge! 🎄
You're connected to a read-only Azure CLI session in "The Neighborhood" tenant.
Your mission: Review their network configurations and find what doesn't belong.
Connecting you now... ❄️
```


```
Welcome back! Let's start by exploring output formats.
First, let's see resource groups in JSON format (the default):
$ az group list
JSON format shows detailed structured data.

az group list
[
  {
    "id": "/subscriptions/2b0942f3-9bca-484b-a508-abdae2db5e64/resourceGroups/theneighborhood-rg1",
    "location": "eastus",
    "managedBy": null,
    "name": "theneighborhood-rg1",
    "properties": {
      "provisioningState": "Succeeded"
    },
    "tags": {}
  },
  {
    "id": "/subscriptions/2b0942f3-9bca-484b-a508-abdae2db5e64/resourceGroups/theneighborhood-rg2",
    "location": "westus",
    "managedBy": null,
    "name": "theneighborhood-rg2",
    "properties": {
      "provisioningState": "Succeeded"
    },
    "tags": {}
  }
]
```

```
Great! Now let's see the same data in table format for better readability 👀
$ az group list -o table
Notice how -o table changes the output format completely!
Both commands show the same data, just formatted differently.

az group list -o table
Name                 Location    ProvisioningState
-------------------  ----------  -------------------
theneighborhood-rg1  eastus      Succeeded
theneighborhood-rg2  westus      Succeeded

```

```
Lets take a look at Network Security Groups (NSGs).
To do this try: az network nsg list -o table
This lists all NSGs across resource groups.
For more information:
https://learn.microsoft.com/en-us/cli/azure/network/nsg?view=azure-cli-latest


az network nsg list -o table
Location    Name                   ResourceGroup
----------  ---------------------  -------------------
eastus      nsg-web-eastus         theneighborhood-rg1
eastus      nsg-db-eastus          theneighborhood-rg1
eastus      nsg-dev-eastus         theneighborhood-rg2
eastus      nsg-mgmt-eastus        theneighborhood-rg2
eastus      nsg-production-eastus  theneighborhood-rg1


```

```
Inspect the Network Security Group (web)  🕵️
Here is the NSG and its resource group:--name nsg-web-eastus --resource-group theneighborhood-rg1 

Hint: We want to show the NSG details. Use | less to page through the output.
Documentation: https://learn.microsoft.com/en-us/cli/azure/network/nsg?view=azure-cli-latest#az-network-nsg-show

az network nsg show --name nsg-web-eastus --resource-group theneighborhood-rg1 | less

{
  "id": "/subscriptions/2b0942f3-9bca-484b-a508-abdae2db5e64/resourceGroups/theneighborhood-rg1/providers/Microsoft.Network/networkSecurityGroups/nsg-web-eastus",
  "location": "eastus",
  "name": "nsg-web-eastus",
  "properties": {
    "securityRules": [
      {
        "name": "Allow-HTTP-Inbound",
        "properties": {
          "access": "Allow",
          "destinationPortRange": "80",
          "direction": "Inbound",
          "priority": 100,
          "protocol": "Tcp",
          "sourceAddressPrefix": "0.0.0.0/0"
        }
      },
      {
        "name": "Allow-HTTPS-Inbound",
        "properties": {
          "access": "Allow",
          "destinationPortRange": "443",
          "direction": "Inbound",
          "priority": 110,
          "protocol": "Tcp",
          "sourceAddressPrefix": "0.0.0.0/0"
        }
      },
      {
        "name": "Allow-AppGateway-HealthProbes",
        "properties": {
          "access": "Allow",
          "destinationPortRange": "80,443",
          "direction": "Inbound",
          "priority": 130,
          "protocol": "Tcp",
"destinationPortRange": "80,443",
          "direction": "Inbound",
          "priority": 130,
          "protocol": "Tcp",
          "sourceAddressPrefix": "AzureLoadBalancer"
        }
      },
      {
        "name": "Allow-Web-To-App",
        "properties": {
          "access": "Allow",
          "destinationPortRange": "8080,8443",
          "direction": "Inbound",
          "priority": 200,
          "protocol": "Tcp",
          "sourceAddressPrefix": "VirtualNetwork"
        }
      },
      {
        "name": "Deny-All-Inbound",
        "properties": {
          "access": "Deny",
          "destinationPortRange": "*",
          "direction": "Inbound",
          "priority": 4096,
          "protocol": "*",
          "sourceAddressPrefix": "*"
        }
      }
    ]
  },
  "resourceGroup": "theneighborhood-rg1",
  "tags": {
    "env": "web"
  }
}


```


```
Inspect the Network Security Group (mgmt)  🕵️
Here is the NSG and its resource group:--nsg-name nsg-mgmt-eastus --resource-group theneighborhood-rg2 

Hint: We want to list the NSG rules
Documentation: https://learn.microsoft.com/en-us/cli/azure/network/nsg/rule?view=azure-cli-latest#az-network-nsg-rule-list


az network nsg show --name nsg-mgmt-eastus --resource-group theneighborhood-rg2 | less

{
  "id": "/subscriptions/2b0942f3-9bca-484b-a508-abdae2db5e64/resourceGroups/theneighborhood-rg2/providers/Microsoft.Network/networkSecurityGroups/nsg-mgmt-eastus",
  "location": "eastus",
  "name": "nsg-mgmt-eastus",
  "properties": {
    "securityRules": [
      {
        "name": "Allow-AzureBastion",
        "properties": {
          "access": "Allow",
          "destinationPortRange": "443",
          "direction": "Inbound",
          "priority": 100,
          "protocol": "Tcp",
          "sourceAddressPrefix": "AzureBastion"
        }
      },
      {
        "name": "Allow-Monitoring-Inbound",
        "properties": {
          "access": "Allow",
          "destinationPortRange": "443",
          "direction": "Inbound",
          "priority": 110,
          "protocol": "Tcp",
          "sourceAddressPrefix": "AzureMonitor"
        }
      },
      {
        "name": "Allow-DNS-From-VNet",
        "properties": {
          "access": "Allow",
          "destinationPortRange": "53",
          "direction": "Inbound",
          "priority": 115,
          "protocol": "Udp",
          "sourceAddressPrefix": "VirtualNetwork"
        }
      },
      {
        "name": "Deny-All-Inbound",
        "properties": {
          "access": "Deny",
          "destinationPortRange": "*",
          "direction": "Inbound",
          "priority": 4096,
          "protocol": "*",
          "sourceAddressPrefix": "*"
        }
      },
      {
        "name": "Allow-Monitoring-Outbound",
        "properties": {
          "access": "Allow",
          "destinationAddressPrefix": "AzureMonitor",
          "destinationPortRange": "443",
          "direction": "Outbound",
          "priority": 200,
          "protocol": "Tcp"
        }
      },
      {
        "name": "Allow-AD-Identity-Outbound",
        "properties": {
          "access": "Allow",
          "destinationAddressPrefix": "AzureActiveDirectory",
          "destinationPortRange": "443",
          "direction": "Outbound",
          "priority": 210,
          "protocol": "Tcp"
        }
      },
      "destinationAddressPrefix": "AzureMonitor",
          "destinationPortRange": "443",
          "direction": "Outbound",
          "priority": 200,
          "protocol": "Tcp"
        }
      },
      {
        "name": "Allow-AD-Identity-Outbound",
        "properties": {
          "access": "Allow",
          "destinationAddressPrefix": "AzureActiveDirectory",
          "destinationPortRange": "443",
          "direction": "Outbound",
          "priority": 210,
          "protocol": "Tcp"
        }
      },
      {
        "name": "Allow-Backup-Outbound",
        "properties": {
          "access": "Allow",
          "destinationAddressPrefix": "AzureBackup",
          "destinationPortRange": "443",
          "direction": "Outbound",
          "priority": 220,
          "protocol": "Tcp"
        }
      }
    ]
  },
  "resourceGroup": "theneighborhood-rg2",
  "tags": {
    "env": "mgmt"
  }
}


```


```
Take a look at the rest of the NSG rules and examine their properties.
After enumerating the NSG rules, enter the command string to view the suspect rule and inspect its properties.
Hint: Review fields such as direction, access, protocol, source, destination and port settings.

Documentation: https://learn.microsoft.com/en-us/cli/azure/network/nsg/rule?view=azure-cli-latest#az-network-nsg-rule-show


az network nsg show --name nsg-production-eastus --resource-group theneighborhood-rg1




az network nsg rule show \
     --resource-group theneighborhood-rg1 \
     --nsg-name nsg-production-eastus  \
     --name Allow-RDP-From-Internet
{
  "name": "Allow-RDP-From-Internet",
  "properties": {
    "access": "Allow",
    "destinationPortRange": "3389",
    "direction": "Inbound",
    "priority": 120,
    "protocol": "Tcp",
    "sourceAddressPrefix": "0.0.0.0/0"
  }
}
    
    
 

```