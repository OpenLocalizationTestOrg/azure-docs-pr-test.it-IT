Se si utilizzano un file toopass parametro parametri durante la distribuzione, è necessario toocreate un file JSON con un toohello simile formato riportato di seguito:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "webSiteName": {
            "value": "ExampleSite"
        },
        "webSiteHostingPlanName": {
            "value": "DefaultPlan"
        },
        "webSiteLocation": {
            "value": "West US"
        },
        "adminPassword": {
            "reference": {
               "keyVault": {
                  "id": "/subscriptions/{guid}/resourceGroups/{group-name}/providers/Microsoft.KeyVault/vaults/{vault-name}"
               }, 
               "secretName": "sqlAdminPassword" 
            }   
        }
   }
}
```

dimensioni di Hello del file di parametro hello non possono essere più di 64 KB.

Se è necessario un valore sensibile tooprovide per un parametro (ad esempio una password), aggiungere tale valore tooa chiave dell'insieme di credenziali. Recuperare l'insieme di credenziali chiave hello durante la distribuzione, come illustrato nell'esempio precedente hello. Per ulteriori informazioni, vedere [Passare valori protetti durante la distribuzione](../articles/azure-resource-manager/resource-manager-keyvault-parameter.md). 

