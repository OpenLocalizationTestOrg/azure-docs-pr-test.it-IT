<span data-ttu-id="70b7e-101">Se si utilizzano un file toopass parametro parametri durante la distribuzione, è necessario toocreate un file JSON con un toohello simile formato riportato di seguito:</span><span class="sxs-lookup"><span data-stu-id="70b7e-101">If you use a parameter file toopass parameter values during deployment, you need toocreate a JSON file with a format similar toohello following example:</span></span>

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

<span data-ttu-id="70b7e-102">dimensioni di Hello del file di parametro hello non possono essere più di 64 KB.</span><span class="sxs-lookup"><span data-stu-id="70b7e-102">hello size of hello parameter file cannot be more than 64 KB.</span></span>

<span data-ttu-id="70b7e-103">Se è necessario un valore sensibile tooprovide per un parametro (ad esempio una password), aggiungere tale valore tooa chiave dell'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="70b7e-103">If you need tooprovide a sensitive value for a parameter (such as a password), add that value tooa key vault.</span></span> <span data-ttu-id="70b7e-104">Recuperare l'insieme di credenziali chiave hello durante la distribuzione, come illustrato nell'esempio precedente hello.</span><span class="sxs-lookup"><span data-stu-id="70b7e-104">Retrieve hello key vault during deployment as shown in hello previous example.</span></span> <span data-ttu-id="70b7e-105">Per ulteriori informazioni, vedere [Passare valori protetti durante la distribuzione](../articles/azure-resource-manager/resource-manager-keyvault-parameter.md).</span><span class="sxs-lookup"><span data-stu-id="70b7e-105">For more information, see [Pass secure values during deployment](../articles/azure-resource-manager/resource-manager-keyvault-parameter.md).</span></span> 

