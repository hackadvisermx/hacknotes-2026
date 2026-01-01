https://hhc25-wetty-prod.holidayhackchallenge.com/?&challenge=termMSBlobstorage&username=hackadviser

```
🎄 Welcome! 🎄
In a moment, you will be connected to an Azure CLI session in the "neighborhood" tenant.
Your mission: 🔍 Investigate and find WHERE a security vulnerability exists.
Good luck! I'm sure you will do great. Connecting you now...

```


You may not know this but the Azure cli help messages are very easy to access. First, try typing:
$ az help | less

```
az-help


```


Next, you've already been configured with credentials. 🔑
  $ az account show | less
  - Pipe the output to | less so you can scroll.
  - Press 'q' to exit less.

```
	az account show
{
  "environmentName": "AzureCloud",
  "id": "2b0942f3-9bca-484b-a508-abdae2db5e64",
  "isDefault": true,
  "name": "theneighborhood-sub",
  "state": "Enabled",
  "tenantId": "90a38eda-4006-4dd5-924c-6ca55cacc14d",
  "user": {
    "name": "theneighborhood@theneighborhood.invalid",
    "type": "user"
  }
}
```

Now that you've run a few commands, Let's take a look at some Azure storage accounts.
Try: az storage account list | less
For more information:
https://learn.microsoft.com/en-us/cli/azure/storage/account?view=azure-cli-latest


```
az storage account list

    "virtualNetworkRules": []
      }
    },
    "resourceGroup": "theneighborhood-rg2",
    "sku": {
      "name": "Premium_LRS"
    },
    "tags": {
      "critical": "true"
    }
  },
  {
    "id": "/subscriptions/2b0942f3-9bca-484b-a508-abdae2db5e64/resourceGroups/theneighborhood-rg1/providers/Microsoft.Storage/storageAccounts/neighborhood5",
    "kind": "StorageV2",
    "location": "eastus",
    "name": "neighborhood5",
    "properties": {
      "accessTier": "Cool",
      "allowBlobPublicAccess": false,
      "isHnsEnabled": true,
      "minimumTlsVersion": "TLS1_2"
    },
    "resourceGroup": "theneighborhood-rg1",
    "sku": {
      "name": "Standard_LRS"
    },
    "tags": {
      "project": "Homes"
    }
  },
  {
    "id": "/subscriptions/2b0942f3-9bca-484b-a508-abdae2db5e64/resourceGroups/theneighborhood-rg2/providers/Microsoft.Storage/storageAccounts/neighborhood6",
    "kind": "StorageV2",
    "location": "centralus",
    "name": "neighborhood6",
    "properties": {
      "accessTier": "Hot",
      "allowBlobPublicAccess": false,
      "minimumTlsVersion": "TLS1_2",
      "tags": {
        "replicate": "true"
      }
    },
    "resourceGroup": "theneighborhood-rg2",
    "sku": {
      "name": "Standard_ZRS"
    },
    "tags": {}
  }
]
```

 hmm... one of these looks suspicious 🚨, i think there may be a misconfiguration here somewhere.
Try showing the account that has a common misconfiguration: az storage account show --name xxxxxxxxxx | less

```
 az storage account show --name neighborhood2
{
  "id": "/subscriptions/2b0942f3-9bca-484b-a508-abdae2db5e64/resourceGroups/theneighborhood-rg1/providers/Microsoft.Storage/storageAccounts/neighborhood2",
  "name": "neighborhood2",
  "location": "eastus2",
  "kind": "StorageV2",
  "sku": {
    "name": "Standard_GRS"
  },
  "properties": {
    "accessTier": "Cool",
    "allowBlobPublicAccess": true,
    "minimumTlsVersion": "TLS1_0",
    "encryption": {
      "services": {
        "blob": {
          "enabled": false
        }
      },
      "keySource": "Microsoft.Storage"
    }
  },
  "resourceGroup": "theneighborhood-rg1",
  "tags": {
    "owner": "Admin"
  }
}
```

Now we need to list containers in neighborhood2. After running the command what's interesting in the list?
For more information:
https://learn.microsoft.com/en-us/cli/azure/storage/container?view=azure-cli-latest#az-storage-container-list

```
az storage container list --account-name neighborhood2
[
  {
    "name": "public",
    "properties": {
      "lastModified": "2024-01-15T09:00:00Z",
      "publicAccess": "Blob"
    }
  },
  {
    "name": "private",
    "properties": {
      "lastModified": "2024-02-05T11:12:00Z",
      "publicAccess": null
    }
  }
]
```

Let's take a look at the blob list in the public container for neighborhood2.
For more information:
https://learn.microsoft.com/en-us/cli/azure/storage/blob?view=azure-cli-latest#az-storage-blob-list

```
az storage blob list --container-name public --account-name neighborhood2
[
  {
    "name": "refrigerator_inventory.pdf",
    "properties": {
      "contentLength": 45678,
      "contentType": "application/pdf",
      "metadata": {
        "created_by": "NeighborhoodWatch",
        "document_type": "inventory",
        "last_updated": "2024-12-15"
      }
    }
  },
  {
    "name": "admin_credentials.txt",
    "properties": {
      "contentLength": 1024,
      "contentType": "text/plain",
      "metadata": {
        "note": "admins only"
      }
    }
  },
  {
    "name": "network_config.json",
    "properties": {
      "contentLength": 2048,
      "contentType": "application/json",
      "metadata": {
        "encrypted": "false",
        "environment": "prod"
      }
    }
  }
]


```


Try downloading and viewing the blob file named admin_credentials.txt from the public container.
💡 hint: --file /dev/stdout should print in the terminal. Dont forget to use | less!

```
az storage blob download \
    --account-name neighborhood2 \
    --container-name public \
    --name admin_credentials.txt \
    --file /dev/stdout | less
    
Azure Portal Credentials
User: azureadmin
Pass: AzUR3!P@ssw0rd#2025

Windows Server Credentials
User: administrator
Pass: W1nD0ws$Srv!@42

SQL Server Credentials
User: sa
Pass: SqL!P@55#2025$

Active Directory Domain Admin
User: corp\administrator
Pass: D0m@in#Adm!n$765

Exchange Admin Credentials
User: exchangeadmin
Pass: Exch@ng3!M@il#432

VMware vSphere Credentials
User: vsphereadmin
Pass: VMW@r3#Clu$ter!99

Network Switch Credentials
User: netadmin
Pass: N3t!Sw!tch$C0nfig#

Firewall Admin Credentials
User: fwadmin
Pass: F1r3W@ll#S3cur3!77

Backup Server Credentials
User: backupadmin
Pass: B@ckUp!Srv#2025$

Monitoring System Admin
User: monitoradmin
Pass: M0n!t0r#Sys$P@ss!

SharePoint Admin Credentials
User: spadmin
Pass: Sh@r3P0!nt#Adm!n2025

Git Server Admin
User: gitadmin
Pass: G1t#Srv!Rep0$C0de


```

