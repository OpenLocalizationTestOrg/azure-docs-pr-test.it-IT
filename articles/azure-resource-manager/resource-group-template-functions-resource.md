---
title: funzioni di modello di gestione risorse aaaAzure - risorse | Documenti Microsoft
description: Vengono descritti le risorse toouse funzioni hello un valori tooretrieve modello di gestione risorse di Azure.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/09/2017
ms.author: tomfitz
ms.openlocfilehash: c9d524b338b8b7ea6d8c9e0135d48e4fb8f167c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="resource-functions-for-azure-resource-manager-templates"></a>Funzioni delle risorse per i modelli di Azure Resource Manager

Gestione risorse offre hello funzioni per ottenere i valori delle risorse seguenti:

* [listKeys e list{Value}](#listkeys)
* [provider](#providers)
* [reference](#reference)
* [resourceGroup](#resourcegroup)
* [resourceId](#resourceid)
* [sottoscrizione](#subscription)

i valori tooget parametri, variabili o la distribuzione corrente di hello, vedere [funzioni con valori di distribuzione](resource-group-template-functions-deployment.md).

<a id="listkeys" />
<a id="list" />

## <a name="listkeys-and-listvalue"></a>listKeys e list{Value}
`listKeys(resourceName or resourceIdentifier, apiVersion)`

`list{Value}(resourceName or resourceIdentifier, apiVersion)`

Restituisce hello valori per qualsiasi tipo di risorsa che supporta l'operazione di elenco hello. utilizzo più comune di Hello è `listKeys`. 

### <a name="parameters"></a>parameters

| Parametro | Obbligatorio | Tipo | Descrizione |
|:--- |:--- |:--- |:--- |
| resourceName o resourceIdentifier |Sì |string |Identificatore univoco per la risorsa hello. |
| apiVersion |Sì |string |Versione dell'API dello stato di runtime della risorsa. In genere, nel formato di hello, **aaaa-mm-gg**. |

### <a name="return-value"></a>Valore restituito

Hello ha restituito l'elenco chiavi dell'oggetto è hello seguente formato:

```json
{
  "keys": [
    {
      "keyName": "key1",
      "permissions": "Full",
      "value": "{value}"
    },
    {
      "keyName": "key2",
      "permissions": "Full",
      "value": "{value}"
    }
  ]
}
```

Altre funzioni list possono avere formati di restituzione diversi. formato di hello toosee di una funzione, includerla nella sezione di output di hello come mostrato nel modello di esempio hello. 

### <a name="remarks"></a>Osservazioni

Qualsiasi operazione che inizia con **list** può essere usata come funzione nel modello. le operazioni disponibili Hello includono non solo elenco chiavi del, ma anche di operazioni quali `list`, `listAdminKeys`, e `listStatus`. Tuttavia, è possibile utilizzare **elenco** le operazioni che richiedono valori hello corpo della richiesta. Ad esempio, hello [elenco Account SAS](/rest/api/storagerp/storageaccounts#StorageAccounts_ListAccountSAS) operazione richiede i parametri del corpo della richiesta come *signedExpiry*, pertanto non può essere utilizzato all'interno di un modello.

toodetermine quali tipi di risorse dispone di un'operazione di elenco, è necessario hello le opzioni seguenti:

* Hello vista [operazioni dell'API REST](/rest/api/) per un provider di risorse e cercare l'elenco delle operazioni. Ad esempio, gli account di archiviazione sono hello [elenco chiavi dell'operazione](/rest/api/storagerp/storageaccounts#StorageAccounts_ListKeys).
* Hello utilizzare [Get AzureRmProviderOperation](/powershell/module/azurerm.resources/get-azurermprovideroperation) cmdlet di PowerShell. Hello seguente esempio mostra come ottenere tutte le operazioni di elenco per gli account di archiviazione:

  ```powershell
  Get-AzureRmProviderOperation -OperationSearchString "Microsoft.Storage/*" | where {$_.Operation -like "*list*"} | FT Operation
  ```
* Utilizzare hello comando CLI di Azure toofilter hello solo l'elenco delle operazioni seguenti:

  ```azurecli
  az provider operation show --namespace Microsoft.Storage --query "resourceTypes[?name=='storageAccounts'].operations[].name | [?contains(@, 'list')]"
  ```

Specificare la risorsa hello utilizzando entrambi hello [funzione resourceId](#resourceid), o formato hello `{providerNamespace}/{resourceType}/{resourceName}`.


### <a name="example"></a>Esempio

Hello esempio seguente viene illustrato come chiavi tooreturn hello primaria e secondaria da un account di archiviazione in hello restituisce sezione.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "storageAccountId": {
            "type": "string"
        }
    },
    "resources": [],
    "outputs": {
        "storageKeysOutput": {
            "value": "[listKeys(parameters('storageAccountId'), '2016-01-01')]",
            "type" : "object"
        }
    }
}
``` 

<a id="providers" />

## <a name="providers"></a>provider
`providers(providerNamespace, [resourceType])`

Restituisce informazioni su un provider di risorse e i relativi tipi di risorse supportati. Se non si specifica un tipo di risorsa, la funzione hello restituisce tutti i tipi di hello è supportato per i provider di risorse hello.

### <a name="parameters"></a>parameters

| Parametro | Obbligatorio | Tipo | Descrizione |
|:--- |:--- |:--- |:--- |
| providerNamespace |Sì |string |Namespace del provider di hello |
| resourceType |No |string |tipo di Hello della risorsa all'interno di hello specificato dello spazio dei nomi. |

### <a name="return-value"></a>Valore restituito

Ogni tipo supportato viene restituito in hello seguente formato: 

```json
{
    "resourceType": "{name of resource type}",
    "locations": [ all supported locations ],
    "apiVersions": [ all supported API versions ]
}
```

Matrice di ordinamento di hello restituito non è garantito che i valori.

### <a name="example"></a>Esempio

Hello di esempio seguente viene illustrato come toouse hello funzione del provider:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "providerOutput": {
            "value": "[providers('Microsoft.Web', 'sites')]",
            "type" : "object"
        }
    }
}
```

Hello esempio precedente restituisce un oggetto hello seguente formato:

```json
{
  "resourceType": "sites",
  "locations": [
    "South Central US",
    "North Europe",
    "West Europe",
    "Southeast Asia",
    ...
  ],
  "apiVersions": [
    "2016-08-01",
    "2016-03-01",
    "2015-08-01-preview",
    "2015-08-01",
    ...
  ]
}
```

<a id="reference" />

## <a name="reference"></a>reference
`reference(resourceName or resourceIdentifier, [apiVersion])`

Restituisce un oggetto che rappresenta lo stato di runtime di una risorsa.

### <a name="parameters"></a>Parametri

| Parametro | Obbligatorio | Tipo | Descrizione |
|:--- |:--- |:--- |:--- |
| resourceName o resourceIdentifier |Sì |string |Nome o identificatore univoco di una risorsa. |
| apiVersion |No |string |Versione dell'API di hello risorsa specificata. Includere questo parametro quando la risorsa hello non è disponibile nel modello stesso. In genere, nel formato di hello, **aaaa-mm-gg**. |

### <a name="return-value"></a>Valore restituito

Ogni tipo di risorsa restituisce proprietà diverse per la funzione di riferimento hello. funzione Hello non restituisce un singolo formato predefinito. toosee hello per un tipo di risorsa, restituiscono oggetto hello in hello restituisce sezione come illustrato nell'esempio hello.

### <a name="remarks"></a>Osservazioni

funzione riferimento Hello deriva il relativo valore da uno stato di runtime e non può essere utilizzato nella sezione variabili hello. Può essere usata, invece, nella sezione outputs di un modello. 

Utilizzando hello reference (funzione), in modo implicito dichiarare che una risorsa dipende un'altra risorsa se viene eseguito il provisioning di risorse a cui fa riferimento hello nel modello stesso. Proprietà dependsOn hello di tooalso use non è necessario. Hello funzione non viene valutata fino a quando non hello risorsa di riferimento è stata completata la distribuzione.

i nomi delle proprietà di toosee hello e i valori per un tipo di risorsa, creare un modello che restituisce l'oggetto hello nella sezione di output di hello. Se si dispone di una risorsa esistente di quel tipo, il modello restituisce l'oggetto di hello senza distribuire le risorse di nuovo. 

In genere, si utilizza hello **riferimento** funzione tooreturn un valore specifico da un oggetto, ad esempio URI dell'endpoint blob hello o un nome di dominio completo.

```json
"outputs": {
    "BlobUri": {
        "value": "[reference(concat('Microsoft.Storage/storageAccounts/', parameters('storageAccountName')), '2016-01-01').primaryEndpoints.blob]",
        "type" : "string"
    },
    "FQDN": {
        "value": "[reference(concat('Microsoft.Network/publicIPAddresses/', parameters('ipAddressName')), '2016-03-30').dnsSettings.fqdn]",
        "type" : "string"
    }
}
```

### <a name="example"></a>Esempio

riferimenti e toodeploy risorse hello in hello modello stesso, usare:

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
      "storageAccountName": { 
          "type": "string"
      }
  },
  "resources": [
    {
      "name": "[parameters('storageAccountName')]",
      "type": "Microsoft.Storage/storageAccounts",
      "apiVersion": "2016-12-01",
      "sku": {
        "name": "Standard_LRS"
      },
      "kind": "Storage",
      "location": "[resourceGroup().location]",
      "tags": {},
      "properties": {
      }
    }
  ],
  "outputs": {
      "referenceOutput": {
          "type": "object",
          "value": "[reference(parameters('storageAccountName'))]"
      }
    }
}
``` 

Hello esempio precedente restituisce un oggetto hello seguente formato:

```json
{
   "creationTime": "2017-06-13T21:24:46.618364Z",
   "primaryEndpoints": {
     "blob": "https://examplestorage.blob.core.windows.net/",
     "file": "https://examplestorage.file.core.windows.net/",
     "queue": "https://examplestorage.queue.core.windows.net/",
     "table": "https://examplestorage.table.core.windows.net/"
   },
   "primaryLocation": "southcentralus",
   "provisioningState": "Succeeded",
   "statusOfPrimary": "available",
   "supportsHttpsTrafficOnly": false
}
```

Hello seguente fa riferimento a un account di archiviazione che non è distribuito in questo modello. Hello account di archiviazione esiste già all'interno di hello stesso gruppo di risorse.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "storageAccountName": {
            "type": "string"
        }
    },
    "resources": [],
    "outputs": {
        "ExistingStorage": {
            "value": "[reference(concat('Microsoft.Storage/storageAccounts/', parameters('storageAccountName')), '2016-01-01')]",
            "type" : "object"
        }
    }
}
```

<a id="resourcegroup" />

## <a name="resourcegroup"></a>resourceGroup
`resourceGroup()`

Restituisce un oggetto che rappresenta il gruppo di risorse corrente hello. 

### <a name="return-value"></a>Valore restituito

Hello ha restituito l'oggetto si trova in hello seguente formato:

```json
{
  "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}",
  "name": "{resourceGroupName}",
  "location": "{resourceGroupLocation}",
  "tags": {
  },
  "properties": {
    "provisioningState": "{status}"
  }
}
```

### <a name="remarks"></a>Osservazioni

Un utilizzo comune della funzione resourceGroup hello è risorse toocreate hello stesso percorso del gruppo di risorse hello. Hello esempio seguente usa hello risorsa gruppo tooassign hello posizione per un sito web.

```json
"resources": [
   {
      "apiVersion": "2016-08-01",
      "type": "Microsoft.Web/sites",
      "name": "[parameters('siteName')]",
      "location": "[resourceGroup().location]",
      ...
   }
]
```

### <a name="example"></a>Esempio

Hello modello seguente restituisce le proprietà di hello hello del gruppo di risorse.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "subscriptionOutput": {
            "value": "[resourceGroup()]",
            "type" : "object"
        }
    }
}
```

Hello esempio precedente restituisce un oggetto hello seguente formato:

```json
{
  "id": "/subscriptions/{subscription-id}/resourceGroups/examplegroup",
  "name": "examplegroup",
  "location": "southcentralus",
  "properties": {
    "provisioningState": "Succeeded"
  }
}
```

<a id="resourceid" />

## <a name="resourceid"></a>resourceId
`resourceId([subscriptionId], [resourceGroupName], resourceType, resourceName1, [resourceName2]...)`

Restituisce hello identificatore univoco di una risorsa. Utilizzare questa funzione quando il nome di risorsa hello è ambiguo o non è disponibile all'interno di hello stesso modello. 

### <a name="parameters"></a>parameters

| Parametro | Obbligatorio | Tipo | Descrizione |
|:--- |:--- |:--- |:--- |
| subscriptionId |No |Stringa (in formato GUID) |Valore predefinito è la sottoscrizione corrente hello. Specificare questo valore quando è necessario tooretrieve una risorsa in un'altra sottoscrizione. |
| resourceGroupName |No |string |Il valore predefinito è il gruppo di risorse corrente. Specificare questo valore quando è necessario tooretrieve una risorsa in un altro gruppo di risorse. |
| resourceType |Sì |string |Tipo di risorsa, incluso lo spazio dei nomi del provider di risorse. |
| resourceName1 |Sì |string |Nome della risorsa. |
| resourceName2 |No |string |Segmento successivo del nome della risorsa se la risorsa è annidata. |

### <a name="return-value"></a>Valore restituito

Identificatore Hello viene restituito in hello seguente formato:

```json
/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/{resourceProviderNamespace}/{resourceType}/{resourceName}
```

### <a name="remarks"></a>Osservazioni

Hello è specificare i valori dei parametri dipendono dalla risorsa hello: in hello stesso gruppo di risorse e di sottoscrizione di distribuzione corrente di hello.

ID di risorsa hello tooget per un account di archiviazione in hello stessa sottoscrizione e il gruppo di risorse, utilizzare:

```json
"[resourceId('Microsoft.Storage/storageAccounts','examplestorage')]"
```

ID della risorsa hello tooget per un account di archiviazione in hello stessa sottoscrizione, ma un gruppo di risorse diverso, utilizzare:

```json
"[resourceId('otherResourceGroup', 'Microsoft.Storage/storageAccounts','examplestorage')]"
```

ID della risorsa hello tooget per un account di archiviazione in una sottoscrizione diversa e il gruppo di risorse, utilizzare:

```json
"[resourceId('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx', 'otherResourceGroup', 'Microsoft.Storage/storageAccounts','examplestorage')]"
```

ID di risorsa hello tooget per un database in un gruppo di risorse diverso, utilizzare:

```json
"[resourceId('otherResourceGroup', 'Microsoft.SQL/servers/databases', parameters('serverName'), parameters('databaseName'))]"
```

Spesso, è necessario toouse questa funzione quando si utilizza un account di archiviazione o di una rete virtuale in un gruppo di risorse alternativo. Hello esempio seguente viene illustrato come una risorsa da un gruppo di risorse esterne può essere facilmente usata:

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
      "virtualNetworkName": {
          "type": "string"
      },
      "virtualNetworkResourceGroup": {
          "type": "string"
      },
      "subnet1Name": {
          "type": "string"
      },
      "nicName": {
          "type": "string"
      }
  },
  "variables": {
      "vnetID": "[resourceId(parameters('virtualNetworkResourceGroup'), 'Microsoft.Network/virtualNetworks', parameters('virtualNetworkName'))]",
      "subnet1Ref": "[concat(variables('vnetID'),'/subnets/', parameters('subnet1Name'))]"
  },
  "resources": [
  {
      "apiVersion": "2015-05-01-preview",
      "type": "Microsoft.Network/networkInterfaces",
      "name": "[parameters('nicName')]",
      "location": "[parameters('location')]",
      "properties": {
          "ipConfigurations": [{
              "name": "ipconfig1",
              "properties": {
                  "privateIPAllocationMethod": "Dynamic",
                  "subnet": {
                      "id": "[variables('subnet1Ref')]"
                  }
              }
          }]
       }
  }]
}
```

### <a name="example"></a>Esempio

Hello esempio seguente restituisce hello ID di risorsa per un account di archiviazione nel gruppo di risorse hello:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "sameRGOutput": {
            "value": "[resourceId('Microsoft.Storage/storageAccounts','examplestorage')]",
            "type" : "string"
        },
        "differentRGOutput": {
            "value": "[resourceId('otherResourceGroup', 'Microsoft.Storage/storageAccounts','examplestorage')]",
            "type" : "string"
        },
        "differentSubOutput": {
            "value": "[resourceId('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx', 'otherResourceGroup', 'Microsoft.Storage/storageAccounts','examplestorage')]",
            "type" : "string"
        },
        "nestedResourceOutput": {
            "value": "[resourceId('Microsoft.SQL/servers/databases', 'serverName', 'databaseName')]",
            "type" : "string"
        }
    }
}
```

Hello output di hello precedente esempio con i valori predefiniti di hello è:

| Nome | Tipo | Valore |
| ---- | ---- | ----- |
| sameRGOutput | String | /subscriptions/{id-sott-corrente}/resourceGroups/examplegroup/providers/Microsoft.Storage/storageAccounts/examplestorage |
| differentRGOutput | String | /subscriptions/{id-sott-corrente}/resourceGroups/otherResourceGroup/providers/Microsoft.Storage/storageAccounts/examplestorage |
| differentSubOutput | String | /subscriptions/{id-sott-differente}/resourceGroups/otherResourceGroup/providers/Microsoft.Storage/storageAccounts/examplestorage |
| nestedResourceOutput | String | /subscriptions/{id-sott-corrente}/resourceGroups/examplegroup/providers/Microsoft.SQL/servers/serverName/databases/databaseName |

<a id="subscription" />

## <a name="subscription"></a>sottoscrizione
`subscription()`

Restituisce informazioni dettagliate sulla sottoscrizione hello per la distribuzione corrente di hello. 

### <a name="return-value"></a>Valore restituito

funzione Hello restituisce hello seguente formato:

```json
{
    "id": "/subscriptions/{subscription-id}",
    "subscriptionId": "{subscription-id}",
    "tenantId": "{tenant-id}",
    "displayName": "{name-of-subscription}"
}
```

### <a name="example"></a>Esempio

Hello esempio seguente viene illustrata hello sottoscrizione funzione chiamato nella sezione di output di hello. 

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "subscriptionOutput": {
            "value": "[subscription()]",
            "type" : "object"
        }
    }
}
```

## <a name="next-steps"></a>Passaggi successivi
* Per una descrizione delle sezioni hello in un modello di gestione risorse di Azure, vedere [modelli Authoring Azure Resource Manager](resource-group-authoring-templates.md).
* toomerge più modelli, vedere [con modelli collegati con Azure Resource Manager](resource-group-linked-templates.md).
* tooiterate un numero specificato di volte durante la creazione di un tipo di risorsa, vedere [creare più istanze delle risorse in Azure Resource Manager](resource-group-create-multiple.md).
* toosee come modello hello toodeploy è stato creato, vedere [distribuire un'applicazione con il modello di gestione risorse di Azure](resource-group-template-deploy.md).

