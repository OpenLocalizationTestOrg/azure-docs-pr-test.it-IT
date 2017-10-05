---
title: Posizione delle risorse di Azure nei modelli | Microsoft Docs
description: Viene illustrato come impostare una posizione per una risorsa in un modello di Azure Resource Manager
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
ms.openlocfilehash: 73e50a593c41e841dcaf184abb895406ff5001e9
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="set-resource-location-in-azure-resource-manager-templates"></a><span data-ttu-id="2d247-103">Impostare la posizione delle risorse nei modelli di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="2d247-103">Set resource location in Azure Resource Manager templates</span></span>
<span data-ttu-id="2d247-104">Quando si distribuisce un modello, è necessario fornire la posizione per ogni risorsa.</span><span class="sxs-lookup"><span data-stu-id="2d247-104">When deploying a template, you must provide a location for each resource.</span></span> <span data-ttu-id="2d247-105">In questo argomento viene illustrato come determinare le posizioni disponibili per la sottoscrizione per ogni tipo di risorsa.</span><span class="sxs-lookup"><span data-stu-id="2d247-105">This topic shows how to determine the locations that are available to your subscription for each resource type.</span></span>

## <a name="determine-supported-locations"></a><span data-ttu-id="2d247-106">Determinare le posizioni supportate</span><span class="sxs-lookup"><span data-stu-id="2d247-106">Determine supported locations</span></span>

<span data-ttu-id="2d247-107">Per un elenco completo delle posizioni supportate per ciascun tipo di risorsa, vedere [Prodotti disponibili in base all'area](https://azure.microsoft.com/regions/services/).</span><span class="sxs-lookup"><span data-stu-id="2d247-107">For a complete list of supported locations for each resource type, see [Products available by region](https://azure.microsoft.com/regions/services/).</span></span> <span data-ttu-id="2d247-108">Tuttavia, la sottoscrizione potrebbe non avere accesso a tutte le posizioni indicate in tale elenco.</span><span class="sxs-lookup"><span data-stu-id="2d247-108">However, your subscription might not have access to all the locations in that list.</span></span> <span data-ttu-id="2d247-109">Per visualizzare un elenco personalizzato delle posizioni disponibili per la sottoscrizione, usare Azure PowerShell o l'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="2d247-109">To see a customized list of locations that are available to your subscription, use Azure PowerShell or Azure CLI.</span></span> 

<span data-ttu-id="2d247-110">Nell'esempio seguente viene usato PowerShell per ottenere la posizione per il tipo di risorsa `Microsoft.Web\sites`:</span><span class="sxs-lookup"><span data-stu-id="2d247-110">The following example uses PowerShell to get the locations for the `Microsoft.Web\sites` resource type:</span></span>

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Web).ResourceTypes | Where-Object ResourceTypeName -eq sites).Locations
```

<span data-ttu-id="2d247-111">Nell'esempio seguente viene usata l'interfaccia della riga di comando di Azure 2.0 per ottenere la posizione per il tipo di risorsa `Microsoft.Web\sites`:</span><span class="sxs-lookup"><span data-stu-id="2d247-111">The following example uses Azure CLI 2.0 to get the locations for the `Microsoft.Web\sites` resource type:</span></span>

```azurecli
az provider show -n Microsoft.Web --query "resourceTypes[?resourceType=='sites'].locations"
```

## <a name="set-location-in-template"></a><span data-ttu-id="2d247-112">Impostare la posizione nel modello</span><span class="sxs-lookup"><span data-stu-id="2d247-112">Set location in template</span></span>

<span data-ttu-id="2d247-113">Dopo aver determinato le posizioni supportate per le risorse, è necessario impostare la posizione del modello.</span><span class="sxs-lookup"><span data-stu-id="2d247-113">After determining the supported locations for your resources, you need to set that location in your template.</span></span> <span data-ttu-id="2d247-114">Il modo più semplice per impostare questo valore consiste nel creare un gruppo di risorse in una posizione che supporti i tipi di risorsa e impostare ogni posizione su `[resourceGroup().location]`.</span><span class="sxs-lookup"><span data-stu-id="2d247-114">The easiest way to set this value is to create a resource group in a location that supports the resource types, and set each location to `[resourceGroup().location]`.</span></span> <span data-ttu-id="2d247-115">È possibile ridistribuire il modello a gruppi di risorse in posizioni diverse senza modificare i valori o i parametri del modello.</span><span class="sxs-lookup"><span data-stu-id="2d247-115">You can redeploy the template to resource groups in different locations, and not change any values in the template or parameters.</span></span> 

<span data-ttu-id="2d247-116">Nell'esempio seguente viene illustrato un account di archiviazione che viene distribuito nella stessa posizione del gruppo di risorse:</span><span class="sxs-lookup"><span data-stu-id="2d247-116">The following example shows a storage account that is deployed to the same location as the resource group:</span></span>

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

<span data-ttu-id="2d247-117">Se è necessario impostare come hardcoded la posizione del modello, specificare il nome di una delle aree supportate.</span><span class="sxs-lookup"><span data-stu-id="2d247-117">If you need to hardcode the location in your template, provide the name of one of the supported regions.</span></span> <span data-ttu-id="2d247-118">Nell'esempio seguente viene illustrato un account di archiviazione che viene sempre distribuito negli Stati Uniti centro-settentrionali:</span><span class="sxs-lookup"><span data-stu-id="2d247-118">The following example shows a storage account that is always deployed to North Central US:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="2d247-119">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2d247-119">Next steps</span></span>
* <span data-ttu-id="2d247-120">Per altri suggerimenti su come creare i modelli, vedere [Procedure consigliate per la creazione di modelli di Azure Resource Manager](resource-manager-template-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="2d247-120">For recommendations about how to create templates, see [Best practices for creating Azure Resource Manager templates](resource-manager-template-best-practices.md).</span></span>

