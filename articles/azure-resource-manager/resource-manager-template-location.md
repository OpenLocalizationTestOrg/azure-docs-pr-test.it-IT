---
title: percorso della risorsa aaaAzure nel modello | Documenti Microsoft
description: Viene illustrato come tooset un percorso per una risorsa in un modello di gestione risorse di Azure
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/03/2017
ms.author: tomfitz
ms.openlocfilehash: f2ad6ca6ac5f34484a2e5e57dd8d67c77dacc41a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="set-resource-location-in-azure-resource-manager-templates"></a>Impostare la posizione delle risorse nei modelli di Azure Resource Manager
Quando si distribuisce un modello, è necessario fornire la posizione per ogni risorsa. Questo argomento viene illustrato come percorsi di hello toodetermine sottoscrizione tooyour disponibili per ogni risorsa di tipo.

## <a name="determine-supported-locations"></a>Determinare le posizioni supportate

Per un elenco completo delle posizioni supportate per ciascun tipo di risorsa, vedere [Prodotti disponibili in base all'area](https://azure.microsoft.com/regions/services/). Tuttavia, la sottoscrizione potrebbe non avere accesso tooall hello posizioni nell'elenco. toosee un elenco personalizzato di percorsi di sottoscrizione tooyour disponibili, usare Azure PowerShell o l'interfaccia CLI di Azure. 

Hello seguente utilizza percorsi di PowerShell tooget hello per hello `Microsoft.Web\sites` tipo di risorsa:

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Web).ResourceTypes | Where-Object ResourceTypeName -eq sites).Locations
```

Hello seguente utilizza percorsi di hello tooget CLI di Azure 2.0 per hello `Microsoft.Web\sites` tipo di risorsa:

```azurecli
az provider show -n Microsoft.Web --query "resourceTypes[?resourceType=='sites'].locations"
```

## <a name="set-location-in-template"></a>Impostare la posizione nel modello

Dopo aver determinato i percorsi di hello è supportato per le risorse, è necessario tooset tale posizione nel modello. Hello più semplice tooset modo questo valore è una risorsa gruppo in un percorso che supporta i tipi di risorse hello toocreate e impostare ogni posizione troppo`[resourceGroup().location]`. È possibile ridistribuire i gruppi di tooresource modello hello in posizioni diverse e non modificano i valori nel modello di hello o parametri. 

Hello esempio seguente viene illustrato un account di archiviazione è distribuito toohello stesso percorso del gruppo di risorse hello:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "variables": {
      "storageName": "[concat('storage', uniqueString(resourceGroup().id))]"
    },
    "resources": [
    {
      "apiVersion": "2016-01-01",
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[variables('storageName')]",
      "location": "[resourceGroup().location]",
      "tags": {
        "Dept": "Finance",
        "Environment": "Production"
      },
      "sku": {
        "name": "Standard_LRS"
      },
      "kind": "Storage",
      "properties": { }
    }
    ]
}
```

Se è necessario il percorso di hello toohardcode nel modello, specificare il nome di hello di una delle aree di hello è supportato. Hello di esempio seguente viene illustrato un account di archiviazione è sempre distribuito tooNorth centrale USA:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [
    {
      "apiVersion": "2016-01-01",
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[concat('storageloc', uniqueString(resourceGroup().id))]",
      "location": "North Central US",
      "tags": {
        "Dept": "Finance",
        "Environment": "Production"
      },
      "sku": {
        "name": "Standard_LRS"
      },
      "kind": "Storage",
      "properties": { }
    }
    ]
}
```

## <a name="next-steps"></a>Passaggi successivi
* Per indicazioni su come toocreate modelli, vedere [procedure consigliate per la creazione di modelli di Azure Resource Manager](resource-manager-template-best-practices.md).

