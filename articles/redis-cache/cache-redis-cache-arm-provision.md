---
title: una Cache Redis con Azure Resource Manager aaaProvision | Documenti Microsoft
description: Utilizzare Gestione risorse di Azure modello toodeploy Cache Redis di Azure.
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
ms.openlocfilehash: 46e7b3b2493ac51dbe6bab0b086304802afc5d48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-redis-cache-using-a-template"></a><span data-ttu-id="ea078-103">Creare una Cache Redis utilizzando un modello</span><span class="sxs-lookup"><span data-stu-id="ea078-103">Create a Redis Cache using a template</span></span>
<span data-ttu-id="ea078-104">In questo argomento è illustrato come toocreate un modello di gestione risorse di Azure che distribuisce un Azure Redis Cache.</span><span class="sxs-lookup"><span data-stu-id="ea078-104">In this topic, you learn how toocreate an Azure Resource Manager template that deploys an Azure Redis Cache.</span></span> <span data-ttu-id="ea078-105">cache di Hello è utilizzabile con un'archiviazione account tookeep diagnostica dati esistenti.</span><span class="sxs-lookup"><span data-stu-id="ea078-105">hello cache can be used with an existing storage account tookeep diagnostic data.</span></span> <span data-ttu-id="ea078-106">Verrà inoltre descritto come toodefine quali risorse vengono distribuite come toodefine parametri e che vengono specificati quando è eseguita la distribuzione di hello.</span><span class="sxs-lookup"><span data-stu-id="ea078-106">You also learn how toodefine which resources are deployed and how toodefine parameters that are specified when hello deployment is executed.</span></span> <span data-ttu-id="ea078-107">È possibile utilizzare questo modello per la propria distribuzioni o personalizzarlo toomeet esigenze.</span><span class="sxs-lookup"><span data-stu-id="ea078-107">You can use this template for your own deployments, or customize it toomeet your requirements.</span></span>

<span data-ttu-id="ea078-108">Attualmente, le impostazioni di diagnostica vengono condivisi per tutte le cache di hello stessa area per una sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="ea078-108">Currently, diagnostic settings are shared for all caches in hello same region for a subscription.</span></span> <span data-ttu-id="ea078-109">Aggiornamento della cache di una regione hello influisce su tutte le altre cache nell'area di hello.</span><span class="sxs-lookup"><span data-stu-id="ea078-109">Updating one cache in hello region affects all other caches in hello region.</span></span>

<span data-ttu-id="ea078-110">Per altre informazioni sulla creazione dei modelli, vedere [Creazione di modelli di Gestione risorse di Azure](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="ea078-110">For more information about creating templates, see [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="ea078-111">Per il modello di hello completo, vedere [modello Cache Redis](https://github.com/Azure/azure-quickstart-templates/blob/master/101-redis-cache/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="ea078-111">For hello complete template, see [Redis Cache template](https://github.com/Azure/azure-quickstart-templates/blob/master/101-redis-cache/azuredeploy.json).</span></span>

> [!NOTE]
> <span data-ttu-id="ea078-112">Modelli di gestione risorse per hello nuovo [livello Premium](cache-premium-tier-intro.md) sono disponibili.</span><span class="sxs-lookup"><span data-stu-id="ea078-112">Resource Manager templates for hello new [Premium tier](cache-premium-tier-intro.md) are available.</span></span> 
> 
> * [<span data-ttu-id="ea078-113">Creare una Cache Redis Premium con il clustering</span><span class="sxs-lookup"><span data-stu-id="ea078-113">Create a Premium Redis Cache with clustering</span></span>](https://azure.microsoft.com/documentation/templates/201-redis-premium-cluster-diagnostics/)
> * [<span data-ttu-id="ea078-114">Creare una Cache Redis Premium con persistenza dei dati</span><span class="sxs-lookup"><span data-stu-id="ea078-114">Create Premium Redis Cache with data persistence</span></span>](https://azure.microsoft.com/documentation/templates/201-redis-premium-persistence/)
> * [<span data-ttu-id="ea078-115">Creare una Cache Redis Premium con rete virtuale e clustering facoltativo</span><span class="sxs-lookup"><span data-stu-id="ea078-115">Create Premium Redis Cache with VNet and optional clustering</span></span>](https://azure.microsoft.com/documentation/templates/201-redis-premium-vnet-cluster-diagnostics/)
> 
> <span data-ttu-id="ea078-116">toocheck per i modelli più recenti di hello, vedere [modelli di avvio rapido di Azure](https://azure.microsoft.com/documentation/templates/) e cercare `Redis Cache`.</span><span class="sxs-lookup"><span data-stu-id="ea078-116">toocheck for hello latest templates, see [Azure Quickstart Templates](https://azure.microsoft.com/documentation/templates/) and search for `Redis Cache`.</span></span>
> 
> 

## <a name="what-you-will-deploy"></a><span data-ttu-id="ea078-117">Elementi distribuiti</span><span class="sxs-lookup"><span data-stu-id="ea078-117">What you will deploy</span></span>
<span data-ttu-id="ea078-118">In questo modello, verrà distribuita una Cache Redis di Azure che utilizza un account di archiviazione esistente per dati di diagnostica.</span><span class="sxs-lookup"><span data-stu-id="ea078-118">In this template, you will deploy an Azure Redis Cache that uses an existing storage account for diagnostic data.</span></span>

<span data-ttu-id="ea078-119">toorun hello automaticamente la distribuzione, fare clic su hello seguente pulsante:</span><span class="sxs-lookup"><span data-stu-id="ea078-119">toorun hello deployment automatically, click hello following button:</span></span>

<span data-ttu-id="ea078-120">[![Distribuire tooAzure](./media/cache-redis-cache-arm-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-redis-cache%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="ea078-120">[![Deploy tooAzure](./media/cache-redis-cache-arm-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-redis-cache%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="ea078-121">parameters</span><span class="sxs-lookup"><span data-stu-id="ea078-121">Parameters</span></span>
<span data-ttu-id="ea078-122">Con Gestione risorse di Azure, si definiscono i parametri per i valori si desidera toospecify quando viene distribuito il modello di hello.</span><span class="sxs-lookup"><span data-stu-id="ea078-122">With Azure Resource Manager, you define parameters for values you want toospecify when hello template is deployed.</span></span> <span data-ttu-id="ea078-123">modello Hello include una sezione denominata parametri che contiene tutti i valori di parametro hello.</span><span class="sxs-lookup"><span data-stu-id="ea078-123">hello template includes a section called Parameters that contains all of hello parameter values.</span></span>
<span data-ttu-id="ea078-124">È necessario definire un parametro per i valori che variano in base progetto hello che si distribuisce o Hello che si distribuisce ambiente di hello.</span><span class="sxs-lookup"><span data-stu-id="ea078-124">You should define a parameter for those values that vary based on hello project you are deploying or based on hello environment you are deploying to.</span></span> <span data-ttu-id="ea078-125">Non definire parametri per i valori che restano sempre hello stesso.</span><span class="sxs-lookup"><span data-stu-id="ea078-125">Do not define parameters for values that always stay hello same.</span></span> <span data-ttu-id="ea078-126">Ogni valore del parametro viene utilizzato in hello modello toodefine hello le risorse distribuite.</span><span class="sxs-lookup"><span data-stu-id="ea078-126">Each parameter value is used in hello template toodefine hello resources that are deployed.</span></span> 

[!INCLUDE [app-service-web-deploy-redis-parameters](../../includes/cache-deploy-parameters.md)]

### <a name="rediscachelocation"></a><span data-ttu-id="ea078-127">redisCacheLocation</span><span class="sxs-lookup"><span data-stu-id="ea078-127">redisCacheLocation</span></span>
<span data-ttu-id="ea078-128">percorso di Hello di hello Cache Redis.</span><span class="sxs-lookup"><span data-stu-id="ea078-128">hello location of hello Redis Cache.</span></span> <span data-ttu-id="ea078-129">Per prestazioni ottimali, utilizzare hello stesso percorso come hello app toobe utilizzato con cache di hello.</span><span class="sxs-lookup"><span data-stu-id="ea078-129">For best performance, use hello same location as hello app toobe used with hello cache.</span></span>

    "redisCacheLocation": {
      "type": "string"
    }

### <a name="existingdiagnosticsstorageaccountname"></a><span data-ttu-id="ea078-130">existingDiagnosticsStorageAccountName</span><span class="sxs-lookup"><span data-stu-id="ea078-130">existingDiagnosticsStorageAccountName</span></span>
<span data-ttu-id="ea078-131">nome di Hello di hello esistente toouse account di archiviazione per diagnostica.</span><span class="sxs-lookup"><span data-stu-id="ea078-131">hello name of hello existing storage account toouse for diagnostics.</span></span> 

    "existingDiagnosticsStorageAccountName": {
      "type": "string"
    }

### <a name="enablenonsslport"></a><span data-ttu-id="ea078-132">enableNonSslPort</span><span class="sxs-lookup"><span data-stu-id="ea078-132">enableNonSslPort</span></span>
<span data-ttu-id="ea078-133">Un valore booleano che indica se tooallow accedere tramite le porte non SSL.</span><span class="sxs-lookup"><span data-stu-id="ea078-133">A boolean value that indicates whether tooallow access via non-SSL ports.</span></span>

    "enableNonSslPort": {
      "type": "bool"
    }

### <a name="diagnosticsstatus"></a><span data-ttu-id="ea078-134">diagnosticsStatus</span><span class="sxs-lookup"><span data-stu-id="ea078-134">diagnosticsStatus</span></span>
<span data-ttu-id="ea078-135">Valore che indica se la diagnostica è abilitata.</span><span class="sxs-lookup"><span data-stu-id="ea078-135">A value that indicates whether diagnostics is enabled.</span></span> <span data-ttu-id="ea078-136">Utilizzare ON o OFF.</span><span class="sxs-lookup"><span data-stu-id="ea078-136">Use ON or OFF.</span></span>

    "diagnosticsStatus": {
      "type": "string",
      "defaultValue": "ON",
      "allowedValues": [
            "ON",
            "OFF"
        ]
    }

## <a name="resources-toodeploy"></a><span data-ttu-id="ea078-137">Risorse toodeploy</span><span class="sxs-lookup"><span data-stu-id="ea078-137">Resources toodeploy</span></span>
### <a name="redis-cache"></a><span data-ttu-id="ea078-138">Cache Redis</span><span class="sxs-lookup"><span data-stu-id="ea078-138">Redis Cache</span></span>
<span data-ttu-id="ea078-139">Crea hello Cache Redis di Azure.</span><span class="sxs-lookup"><span data-stu-id="ea078-139">Creates hello Azure Redis Cache.</span></span>

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



## <a name="commands-toorun-deployment"></a><span data-ttu-id="ea078-140">Comandi toorun distribuzione</span><span class="sxs-lookup"><span data-stu-id="ea078-140">Commands toorun deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a><span data-ttu-id="ea078-141">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ea078-141">PowerShell</span></span>
    New-AzureRmResourceGroupDeployment -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-redis-cache/azuredeploy.json -ResourceGroupName ExampleDeployGroup -redisCacheName ExampleCache

### <a name="azure-cli"></a><span data-ttu-id="ea078-142">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="ea078-142">Azure CLI</span></span>
    azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-redis-cache/azuredeploy.json -g ExampleDeployGroup


