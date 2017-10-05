---
title: "Eseguire il provisioning dell’app Web con Cache Redis"
description: Utilizzare il modello di Gestione risorse di Azure per distribuire l'app Web con Cache Redis.
services: app-service
documentationcenter: 
author: steved0x
manager: erickson-doug
editor: 
ms.assetid: 6e99c71f-ef8e-4570-a307-e4c059e60c35
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: sdanie
ms.openlocfilehash: 810c1cedd4fe0bd6ecdf9bd32dfb241f5f345300
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-web-app-plus-redis-cache-using-a-template"></a><span data-ttu-id="69387-103">Creare un’app Web più Cache Redis utilizzando un modello</span><span class="sxs-lookup"><span data-stu-id="69387-103">Create a Web App plus Redis Cache using a template</span></span>
<span data-ttu-id="69387-104">In questo argomento viene illustrato come creare un modello di Gestione risorse di Azure che consente di distribuire un'app Web di Azure con Cache Redis.</span><span class="sxs-lookup"><span data-stu-id="69387-104">In this topic, you will learn how to create an Azure Resource Manager template that deploys an Azure Web App with Redis cache.</span></span> <span data-ttu-id="69387-105">Verrà illustrato come definire le risorse da distribuire e i parametri specificati quando viene eseguita la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="69387-105">You will learn how to define which resources are deployed and how to define parameters that are specified when the deployment is executed.</span></span> <span data-ttu-id="69387-106">È possibile usare questo modello per le proprie distribuzioni o personalizzarlo in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="69387-106">You can use this template for your own deployments, or customize it to meet your requirements.</span></span>

<span data-ttu-id="69387-107">Per altre informazioni sulla creazione dei modelli, vedere [Creazione di modelli di Gestione risorse di Azure](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="69387-107">For more information about creating templates, see [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="69387-108">Per il modello completo, vedere l’articolo relativo all’ [app Web con modello Cache Redis](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-with-redis-cache/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="69387-108">For the complete template, see [Web App with Redis Cache template](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-with-redis-cache/azuredeploy.json).</span></span>

## <a name="what-you-will-deploy"></a><span data-ttu-id="69387-109">Elementi distribuiti</span><span class="sxs-lookup"><span data-stu-id="69387-109">What you will deploy</span></span>
<span data-ttu-id="69387-110">In questo modello, verrà distribuito quanto segue:</span><span class="sxs-lookup"><span data-stu-id="69387-110">In this template, you will deploy:</span></span>

* <span data-ttu-id="69387-111">App Web di Azure</span><span class="sxs-lookup"><span data-stu-id="69387-111">Azure Web App</span></span>
* <span data-ttu-id="69387-112">Cache Redis di Azure.</span><span class="sxs-lookup"><span data-stu-id="69387-112">Azure Redis Cache.</span></span>

<span data-ttu-id="69387-113">Per eseguire automaticamente la distribuzione, fare clic sul pulsante seguente:</span><span class="sxs-lookup"><span data-stu-id="69387-113">To run the deployment automatically, click the following button:</span></span>

<span data-ttu-id="69387-114">[![Distribuzione in Azure](./media/cache-web-app-arm-with-redis-cache-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-with-redis-cache%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="69387-114">[![Deploy to Azure](./media/cache-web-app-arm-with-redis-cache-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-with-redis-cache%2Fazuredeploy.json)</span></span>

## <a name="parameters-to-specify"></a><span data-ttu-id="69387-115">Parametri da specificare</span><span class="sxs-lookup"><span data-stu-id="69387-115">Parameters to specify</span></span>
[!INCLUDE [app-service-web-deploy-web-parameters](../../includes/app-service-web-deploy-web-parameters.md)]

[!INCLUDE [cache-deploy-parameters](../../includes/cache-deploy-parameters.md)]

## <a name="variables-for-names"></a><span data-ttu-id="69387-116">Variabili per i nomi</span><span class="sxs-lookup"><span data-stu-id="69387-116">Variables for names</span></span>
<span data-ttu-id="69387-117">Questo modello si serve di variabili per costruire i nomi delle risorse.</span><span class="sxs-lookup"><span data-stu-id="69387-117">This template uses variables to construct names for the resources.</span></span> <span data-ttu-id="69387-118">Tramite la funzione [uniqueString](../azure-resource-manager/resource-group-template-functions-string.md#uniquestring) viene creato un valore in base all'ID del gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="69387-118">It uses the [uniqueString](../azure-resource-manager/resource-group-template-functions-string.md#uniquestring) function to construct a value based on the resource group id.</span></span>

    "variables": {
      "hostingPlanName": "[concat('hostingplan', uniqueString(resourceGroup().id))]",
      "webSiteName": "[concat('webSite', uniqueString(resourceGroup().id))]",
      "cacheName": "[concat('cache', uniqueString(resourceGroup().id))]"
    },


## <a name="resources-to-deploy"></a><span data-ttu-id="69387-119">Risorse da distribuire</span><span class="sxs-lookup"><span data-stu-id="69387-119">Resources to deploy</span></span>
[!INCLUDE [app-service-web-deploy-web-host](../../includes/app-service-web-deploy-web-host.md)]

### <a name="redis-cache"></a><span data-ttu-id="69387-120">Cache Redis</span><span class="sxs-lookup"><span data-stu-id="69387-120">Redis Cache</span></span>
<span data-ttu-id="69387-121">Crea la Cache Redis di Azure che viene utilizzata con l'app Web.</span><span class="sxs-lookup"><span data-stu-id="69387-121">Creates the Azure Redis Cache that is used with the web app.</span></span> <span data-ttu-id="69387-122">Il nome della cache è specificato nella variabile **cacheName** .</span><span class="sxs-lookup"><span data-stu-id="69387-122">The name of the cache is specified in the **cacheName** variable.</span></span>

<span data-ttu-id="69387-123">Il modello crea la cache nella stessa posizione in cui si trova il gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="69387-123">The template creates the cache in the same location as the resource group.</span></span>

    {
      "name": "[variables('cacheName')]",
      "type": "Microsoft.Cache/Redis",
      "location": "[resourceGroup().location]",
      "apiVersion": "2015-08-01",
      "dependsOn": [ ],
      "tags": {
        "displayName": "cache"
      },
      "properties": {
        "sku": {
          "name": "[parameters('cacheSKUName')]",
          "family": "[parameters('cacheSKUFamily')]",
          "capacity": "[parameters('cacheSKUCapacity')]"
        }
      }
    }


### <a name="web-app"></a><span data-ttu-id="69387-124">App Web</span><span class="sxs-lookup"><span data-stu-id="69387-124">Web app</span></span>
<span data-ttu-id="69387-125">Crea l'app Web con il nome specificato nella variabile **webSiteName** .</span><span class="sxs-lookup"><span data-stu-id="69387-125">Creates the web app with name specified in the **webSiteName** variable.</span></span>

<span data-ttu-id="69387-126">Si noti che l'app Web è configurata con proprietà di impostazione dell’app che consentono di utilizzare Cache Redis.</span><span class="sxs-lookup"><span data-stu-id="69387-126">Notice that the web app is configured with app setting properties that enable it to work with the Redis Cache.</span></span> <span data-ttu-id="69387-127">Queste impostazioni app vengono create dinamicamente in base ai valori forniti durante la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="69387-127">This app settings are dynamically created based on values provided during deployment.</span></span>

    {
      "apiVersion": "2015-08-01",
      "name": "[variables('webSiteName')]",
      "type": "Microsoft.Web/sites",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Web/serverFarms/', variables('hostingPlanName'))]",
        "[concat('Microsoft.Cache/Redis/', variables('cacheName'))]"
      ],
      "tags": {
        "[concat('hidden-related:', resourceGroup().id, '/providers/Microsoft.Web/serverfarms/', variables('hostingPlanName'))]": "empty",
        "displayName": "Website"
      },
      "properties": {
        "name": "[variables('webSiteName')]",
        "serverFarmId": "[resourceId('Microsoft.Web/serverfarms', variables('hostingPlanName'))]"
      },
      "resources": [
        {
          "apiVersion": "2015-08-01",
          "type": "config",
          "name": "appsettings",
          "dependsOn": [
            "[concat('Microsoft.Web/Sites/', variables('webSiteName'))]",
            "[concat('Microsoft.Cache/Redis/', variables('cacheName'))]"
          ],
          "properties": {
            "CacheConnection": "[concat(variables('cacheName'),'.redis.cache.windows.net,abortConnect=false,ssl=true,password=', listKeys(resourceId('Microsoft.Cache/Redis', variables('cacheName')), '2015-08-01').primaryKey)]"
          }
        }
      ]
    }

## <a name="commands-to-run-deployment"></a><span data-ttu-id="69387-128">Comandi per eseguire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="69387-128">Commands to run deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a><span data-ttu-id="69387-129">PowerShell</span><span class="sxs-lookup"><span data-stu-id="69387-129">PowerShell</span></span>
    New-AzureRmResourceGroupDeployment -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-with-redis-cache/azuredeploy.json -ResourceGroupName ExampleDeployGroup

### <a name="azure-cli"></a><span data-ttu-id="69387-130">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="69387-130">Azure CLI</span></span>
    azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-with-redis-cache/azuredeploy.json -g ExampleDeployGroup
