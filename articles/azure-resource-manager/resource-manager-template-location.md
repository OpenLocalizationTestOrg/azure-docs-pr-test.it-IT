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
# <a name="set-resource-location-in-azure-resource-manager-templates"></a><span data-ttu-id="80cac-103">Impostare la posizione delle risorse nei modelli di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="80cac-103">Set resource location in Azure Resource Manager templates</span></span>
<span data-ttu-id="80cac-104">Quando si distribuisce un modello, è necessario fornire la posizione per ogni risorsa.</span><span class="sxs-lookup"><span data-stu-id="80cac-104">When deploying a template, you must provide a location for each resource.</span></span> <span data-ttu-id="80cac-105">Questo argomento viene illustrato come percorsi di hello toodetermine sottoscrizione tooyour disponibili per ogni risorsa di tipo.</span><span class="sxs-lookup"><span data-stu-id="80cac-105">This topic shows how toodetermine hello locations that are available tooyour subscription for each resource type.</span></span>

## <a name="determine-supported-locations"></a><span data-ttu-id="80cac-106">Determinare le posizioni supportate</span><span class="sxs-lookup"><span data-stu-id="80cac-106">Determine supported locations</span></span>

<span data-ttu-id="80cac-107">Per un elenco completo delle posizioni supportate per ciascun tipo di risorsa, vedere [Prodotti disponibili in base all'area](https://azure.microsoft.com/regions/services/).</span><span class="sxs-lookup"><span data-stu-id="80cac-107">For a complete list of supported locations for each resource type, see [Products available by region](https://azure.microsoft.com/regions/services/).</span></span> <span data-ttu-id="80cac-108">Tuttavia, la sottoscrizione potrebbe non avere accesso tooall hello posizioni nell'elenco.</span><span class="sxs-lookup"><span data-stu-id="80cac-108">However, your subscription might not have access tooall hello locations in that list.</span></span> <span data-ttu-id="80cac-109">toosee un elenco personalizzato di percorsi di sottoscrizione tooyour disponibili, usare Azure PowerShell o l'interfaccia CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="80cac-109">toosee a customized list of locations that are available tooyour subscription, use Azure PowerShell or Azure CLI.</span></span> 

<span data-ttu-id="80cac-110">Hello seguente utilizza percorsi di PowerShell tooget hello per hello `Microsoft.Web\sites` tipo di risorsa:</span><span class="sxs-lookup"><span data-stu-id="80cac-110">hello following example uses PowerShell tooget hello locations for hello `Microsoft.Web\sites` resource type:</span></span>

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Web).ResourceTypes | Where-Object ResourceTypeName -eq sites).Locations
```

<span data-ttu-id="80cac-111">Hello seguente utilizza percorsi di hello tooget CLI di Azure 2.0 per hello `Microsoft.Web\sites` tipo di risorsa:</span><span class="sxs-lookup"><span data-stu-id="80cac-111">hello following example uses Azure CLI 2.0 tooget hello locations for hello `Microsoft.Web\sites` resource type:</span></span>

```azurecli
az provider show -n Microsoft.Web --query "resourceTypes[?resourceType=='sites'].locations"
```

## <a name="set-location-in-template"></a><span data-ttu-id="80cac-112">Impostare la posizione nel modello</span><span class="sxs-lookup"><span data-stu-id="80cac-112">Set location in template</span></span>

<span data-ttu-id="80cac-113">Dopo aver determinato i percorsi di hello è supportato per le risorse, è necessario tooset tale posizione nel modello.</span><span class="sxs-lookup"><span data-stu-id="80cac-113">After determining hello supported locations for your resources, you need tooset that location in your template.</span></span> <span data-ttu-id="80cac-114">Hello più semplice tooset modo questo valore è una risorsa gruppo in un percorso che supporta i tipi di risorse hello toocreate e impostare ogni posizione troppo`[resourceGroup().location]`.</span><span class="sxs-lookup"><span data-stu-id="80cac-114">hello easiest way tooset this value is toocreate a resource group in a location that supports hello resource types, and set each location too`[resourceGroup().location]`.</span></span> <span data-ttu-id="80cac-115">È possibile ridistribuire i gruppi di tooresource modello hello in posizioni diverse e non modificano i valori nel modello di hello o parametri.</span><span class="sxs-lookup"><span data-stu-id="80cac-115">You can redeploy hello template tooresource groups in different locations, and not change any values in hello template or parameters.</span></span> 

<span data-ttu-id="80cac-116">Hello esempio seguente viene illustrato un account di archiviazione è distribuito toohello stesso percorso del gruppo di risorse hello:</span><span class="sxs-lookup"><span data-stu-id="80cac-116">hello following example shows a storage account that is deployed toohello same location as hello resource group:</span></span>

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

<span data-ttu-id="80cac-117">Se è necessario il percorso di hello toohardcode nel modello, specificare il nome di hello di una delle aree di hello è supportato.</span><span class="sxs-lookup"><span data-stu-id="80cac-117">If you need toohardcode hello location in your template, provide hello name of one of hello supported regions.</span></span> <span data-ttu-id="80cac-118">Hello di esempio seguente viene illustrato un account di archiviazione è sempre distribuito tooNorth centrale USA:</span><span class="sxs-lookup"><span data-stu-id="80cac-118">hello following example shows a storage account that is always deployed tooNorth Central US:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="80cac-119">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="80cac-119">Next steps</span></span>
* <span data-ttu-id="80cac-120">Per indicazioni su come toocreate modelli, vedere [procedure consigliate per la creazione di modelli di Azure Resource Manager](resource-manager-template-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="80cac-120">For recommendations about how toocreate templates, see [Best practices for creating Azure Resource Manager templates](resource-manager-template-best-practices.md).</span></span>

