---
title: Effettuare il provisioning di una Cache Redis con Azure Resource Manager | Documentazione Microsoft
description: Utilizzare il modello di Gestione risorse di Azure per distribuire una Cache Redis di Azure.
services: app-service
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: ce6f5372-7038-4655-b1c5-108f7c148282
ms.service: cache
ms.workload: web
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: sdanie
ms.openlocfilehash: cce5d63e8bad2dd066cb4c28e2a8a9cb16c47953
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-redis-cache-using-a-template"></a><span data-ttu-id="3cc30-103">Creare una Cache Redis utilizzando un modello</span><span class="sxs-lookup"><span data-stu-id="3cc30-103">Create a Redis Cache using a template</span></span>
<span data-ttu-id="3cc30-104">Questo argomento illustra come creare un modello di Azure Resource Manager che consente di distribuire un'istanza di Cache Redis di Azure.</span><span class="sxs-lookup"><span data-stu-id="3cc30-104">In this topic, you learn how to create an Azure Resource Manager template that deploys an Azure Redis Cache.</span></span> <span data-ttu-id="3cc30-105">La cache è utilizzabile con un account di archiviazione esistente per mantenere i dati di diagnostica.</span><span class="sxs-lookup"><span data-stu-id="3cc30-105">The cache can be used with an existing storage account to keep diagnostic data.</span></span> <span data-ttu-id="3cc30-106">Verrà anche illustrato come definire le risorse da distribuire e i parametri specificati quando viene eseguita la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="3cc30-106">You also learn how to define which resources are deployed and how to define parameters that are specified when the deployment is executed.</span></span> <span data-ttu-id="3cc30-107">È possibile usare questo modello per le proprie distribuzioni o personalizzarlo in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="3cc30-107">You can use this template for your own deployments, or customize it to meet your requirements.</span></span>

<span data-ttu-id="3cc30-108">Le impostazioni di diagnostica sono attualmente condivise da tutte le cache nella stessa area di una sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="3cc30-108">Currently, diagnostic settings are shared for all caches in the same region for a subscription.</span></span> <span data-ttu-id="3cc30-109">L'aggiornamento di una cache nell'area ha effetto su tutte le altre cache presenti nell'area.</span><span class="sxs-lookup"><span data-stu-id="3cc30-109">Updating one cache in the region affects all other caches in the region.</span></span>

<span data-ttu-id="3cc30-110">Per altre informazioni sulla creazione dei modelli, vedere [Creazione di modelli di Gestione risorse di Azure](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="3cc30-110">For more information about creating templates, see [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="3cc30-111">Per il modello completo, vedere il [modello di Cache Redis](https://github.com/Azure/azure-quickstart-templates/blob/master/101-redis-cache/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="3cc30-111">For the complete template, see [Redis Cache template](https://github.com/Azure/azure-quickstart-templates/blob/master/101-redis-cache/azuredeploy.json).</span></span>

> [!NOTE]
> <span data-ttu-id="3cc30-112">Sono disponibili modelli di Resource Manager per il nuovo [livello Premium](cache-premium-tier-intro.md) .</span><span class="sxs-lookup"><span data-stu-id="3cc30-112">Resource Manager templates for the new [Premium tier](cache-premium-tier-intro.md) are available.</span></span> 
> 
> * [<span data-ttu-id="3cc30-113">Creare una Cache Redis Premium con il clustering</span><span class="sxs-lookup"><span data-stu-id="3cc30-113">Create a Premium Redis Cache with clustering</span></span>](https://azure.microsoft.com/documentation/templates/201-redis-premium-cluster-diagnostics/)
> * [<span data-ttu-id="3cc30-114">Creare una Cache Redis Premium con persistenza dei dati</span><span class="sxs-lookup"><span data-stu-id="3cc30-114">Create Premium Redis Cache with data persistence</span></span>](https://azure.microsoft.com/documentation/templates/201-redis-premium-persistence/)
> * [<span data-ttu-id="3cc30-115">Creare una Cache Redis Premium con rete virtuale e clustering facoltativo</span><span class="sxs-lookup"><span data-stu-id="3cc30-115">Create Premium Redis Cache with VNet and optional clustering</span></span>](https://azure.microsoft.com/documentation/templates/201-redis-premium-vnet-cluster-diagnostics/)
> 
> <span data-ttu-id="3cc30-116">Per verificare gli ultimi modelli, vedere [Modelli di avvio rapido di Azure](https://azure.microsoft.com/documentation/templates/) e cercare `Redis Cache`.</span><span class="sxs-lookup"><span data-stu-id="3cc30-116">To check for the latest templates, see [Azure Quickstart Templates](https://azure.microsoft.com/documentation/templates/) and search for `Redis Cache`.</span></span>
> 
> 

## <a name="what-you-will-deploy"></a><span data-ttu-id="3cc30-117">Elementi distribuiti</span><span class="sxs-lookup"><span data-stu-id="3cc30-117">What you will deploy</span></span>
<span data-ttu-id="3cc30-118">In questo modello, verrà distribuita una Cache Redis di Azure che utilizza un account di archiviazione esistente per dati di diagnostica.</span><span class="sxs-lookup"><span data-stu-id="3cc30-118">In this template, you will deploy an Azure Redis Cache that uses an existing storage account for diagnostic data.</span></span>

<span data-ttu-id="3cc30-119">Per eseguire automaticamente la distribuzione, fare clic sul pulsante seguente:</span><span class="sxs-lookup"><span data-stu-id="3cc30-119">To run the deployment automatically, click the following button:</span></span>

<span data-ttu-id="3cc30-120">[![Distribuzione in Azure](./media/cache-redis-cache-arm-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-redis-cache%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="3cc30-120">[![Deploy to Azure](./media/cache-redis-cache-arm-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-redis-cache%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="3cc30-121">Parametri</span><span class="sxs-lookup"><span data-stu-id="3cc30-121">Parameters</span></span>
<span data-ttu-id="3cc30-122">Gestione risorse di Azure permette di definire i parametri per i valori da specificare durante la distribuzione del modello.</span><span class="sxs-lookup"><span data-stu-id="3cc30-122">With Azure Resource Manager, you define parameters for values you want to specify when the template is deployed.</span></span> <span data-ttu-id="3cc30-123">Il modello include una sezione denominata Parametri che contiene tutti i valori dei parametri.</span><span class="sxs-lookup"><span data-stu-id="3cc30-123">The template includes a section called Parameters that contains all of the parameter values.</span></span>
<span data-ttu-id="3cc30-124">È necessario definire un parametro per i valori che variano in base al progetto distribuito o all'ambiente in cui viene distribuito il progetto.</span><span class="sxs-lookup"><span data-stu-id="3cc30-124">You should define a parameter for those values that vary based on the project you are deploying or based on the environment you are deploying to.</span></span> <span data-ttu-id="3cc30-125">Non definire i parametri per i valori che rimangono invariati.</span><span class="sxs-lookup"><span data-stu-id="3cc30-125">Do not define parameters for values that always stay the same.</span></span> <span data-ttu-id="3cc30-126">Ogni valore di parametro nel modello viene usato per definire le risorse distribuite.</span><span class="sxs-lookup"><span data-stu-id="3cc30-126">Each parameter value is used in the template to define the resources that are deployed.</span></span> 

[!INCLUDE [app-service-web-deploy-redis-parameters](../../includes/cache-deploy-parameters.md)]

### <a name="rediscachelocation"></a><span data-ttu-id="3cc30-127">redisCacheLocation</span><span class="sxs-lookup"><span data-stu-id="3cc30-127">redisCacheLocation</span></span>
<span data-ttu-id="3cc30-128">Percorso dell'istanza di Cache Redis.</span><span class="sxs-lookup"><span data-stu-id="3cc30-128">The location of the Redis Cache.</span></span> <span data-ttu-id="3cc30-129">Per prestazioni ottimali, usare lo stesso percorso dell'app da usare con la cache.</span><span class="sxs-lookup"><span data-stu-id="3cc30-129">For best performance, use the same location as the app to be used with the cache.</span></span>

    "redisCacheLocation": {
      "type": "string"
    }

### <a name="existingdiagnosticsstorageaccountname"></a><span data-ttu-id="3cc30-130">existingDiagnosticsStorageAccountName</span><span class="sxs-lookup"><span data-stu-id="3cc30-130">existingDiagnosticsStorageAccountName</span></span>
<span data-ttu-id="3cc30-131">Nome dell'account di archiviazione esistente da utilizzare per le diagnostiche.</span><span class="sxs-lookup"><span data-stu-id="3cc30-131">The name of the existing storage account to use for diagnostics.</span></span> 

    "existingDiagnosticsStorageAccountName": {
      "type": "string"
    }

### <a name="enablenonsslport"></a><span data-ttu-id="3cc30-132">enableNonSslPort</span><span class="sxs-lookup"><span data-stu-id="3cc30-132">enableNonSslPort</span></span>
<span data-ttu-id="3cc30-133">Valore booleano che indica se è consentito l'accesso tramite le porte non SSL.</span><span class="sxs-lookup"><span data-stu-id="3cc30-133">A boolean value that indicates whether to allow access via non-SSL ports.</span></span>

    "enableNonSslPort": {
      "type": "bool"
    }

### <a name="diagnosticsstatus"></a><span data-ttu-id="3cc30-134">diagnosticsStatus</span><span class="sxs-lookup"><span data-stu-id="3cc30-134">diagnosticsStatus</span></span>
<span data-ttu-id="3cc30-135">Valore che indica se la diagnostica è abilitata.</span><span class="sxs-lookup"><span data-stu-id="3cc30-135">A value that indicates whether diagnostics is enabled.</span></span> <span data-ttu-id="3cc30-136">Utilizzare ON o OFF.</span><span class="sxs-lookup"><span data-stu-id="3cc30-136">Use ON or OFF.</span></span>

    "diagnosticsStatus": {
      "type": "string",
      "defaultValue": "ON",
      "allowedValues": [
            "ON",
            "OFF"
        ]
    }

## <a name="resources-to-deploy"></a><span data-ttu-id="3cc30-137">Risorse da distribuire</span><span class="sxs-lookup"><span data-stu-id="3cc30-137">Resources to deploy</span></span>
### <a name="redis-cache"></a><span data-ttu-id="3cc30-138">Cache Redis</span><span class="sxs-lookup"><span data-stu-id="3cc30-138">Redis Cache</span></span>
<span data-ttu-id="3cc30-139">Crea la Cache Redis di Azure.</span><span class="sxs-lookup"><span data-stu-id="3cc30-139">Creates the Azure Redis Cache.</span></span>

    {
      "apiVersion": "2015-08-01",
      "name": "[parameters('redisCacheName')]",
      "type": "Microsoft.Cache/Redis",
      "location": "[parameters('redisCacheLocation')]",
      "properties": {
        "enableNonSslPort": "[parameters('enableNonSslPort')]",
        "sku": {
          "capacity": "[parameters('redisCacheCapacity')]",
          "family": "[parameters('redisCacheFamily')]",
          "name": "[parameters('redisCacheSKU')]"
        }
      },
      "resources": [
        {
          "apiVersion": "2015-07-01",
          "type": "Microsoft.Cache/redis/providers/diagnosticsettings",
          "name": "[concat(parameters('redisCacheName'), '/Microsoft.Insights/service')]",
          "location": "[parameters('redisCacheLocation')]",
          "dependsOn": [
            "[concat('Microsoft.Cache/Redis/', parameters('redisCacheName'))]"
          ],
          "properties": {
            "status": "[parameters('diagnosticsStatus')]",
            "storageAccountName": "[parameters('existingDiagnosticsStorageAccountName')]"
          }
        }
      ]
    }



## <a name="commands-to-run-deployment"></a><span data-ttu-id="3cc30-140">Comandi per eseguire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="3cc30-140">Commands to run deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a><span data-ttu-id="3cc30-141">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3cc30-141">PowerShell</span></span>
    New-AzureRmResourceGroupDeployment -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-redis-cache/azuredeploy.json -ResourceGroupName ExampleDeployGroup -redisCacheName ExampleCache

### <a name="azure-cli"></a><span data-ttu-id="3cc30-142">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="3cc30-142">Azure CLI</span></span>
    azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-redis-cache/azuredeploy.json -g ExampleDeployGroup


