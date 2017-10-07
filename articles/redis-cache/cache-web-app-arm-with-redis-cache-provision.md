---
title: aaaProvision App Web con Cache Redis
description: Usare l'app web di Azure Resource Manager modello toodeploy con Cache Redis.
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
ms.openlocfilehash: b95b5e230dc40c1157940c2017cba836975b6930
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-plus-redis-cache-using-a-template"></a><span data-ttu-id="f9127-103">Creare un’app Web più Cache Redis utilizzando un modello</span><span class="sxs-lookup"><span data-stu-id="f9127-103">Create a Web App plus Redis Cache using a template</span></span>
<span data-ttu-id="f9127-104">In questo argomento si apprenderà come toocreate un modello di gestione risorse di Azure che consente di distribuire un'App Web di Azure con cache Redis.</span><span class="sxs-lookup"><span data-stu-id="f9127-104">In this topic, you will learn how toocreate an Azure Resource Manager template that deploys an Azure Web App with Redis cache.</span></span> <span data-ttu-id="f9127-105">Si apprenderà come toodefine quali risorse vengono distribuite come toodefine parametri e che vengono specificati quando è eseguita la distribuzione di hello.</span><span class="sxs-lookup"><span data-stu-id="f9127-105">You will learn how toodefine which resources are deployed and how toodefine parameters that are specified when hello deployment is executed.</span></span> <span data-ttu-id="f9127-106">È possibile utilizzare questo modello per la propria distribuzioni o personalizzarlo toomeet esigenze.</span><span class="sxs-lookup"><span data-stu-id="f9127-106">You can use this template for your own deployments, or customize it toomeet your requirements.</span></span>

<span data-ttu-id="f9127-107">Per altre informazioni sulla creazione dei modelli, vedere [Creazione di modelli di Gestione risorse di Azure](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="f9127-107">For more information about creating templates, see [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="f9127-108">Per il modello di hello completo, vedere [App Web con il modello di Cache Redis](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-with-redis-cache/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="f9127-108">For hello complete template, see [Web App with Redis Cache template](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-with-redis-cache/azuredeploy.json).</span></span>

## <a name="what-you-will-deploy"></a><span data-ttu-id="f9127-109">Elementi distribuiti</span><span class="sxs-lookup"><span data-stu-id="f9127-109">What you will deploy</span></span>
<span data-ttu-id="f9127-110">In questo modello, verrà distribuito quanto segue:</span><span class="sxs-lookup"><span data-stu-id="f9127-110">In this template, you will deploy:</span></span>

* <span data-ttu-id="f9127-111">App Web di Azure</span><span class="sxs-lookup"><span data-stu-id="f9127-111">Azure Web App</span></span>
* <span data-ttu-id="f9127-112">Cache Redis di Azure.</span><span class="sxs-lookup"><span data-stu-id="f9127-112">Azure Redis Cache.</span></span>

<span data-ttu-id="f9127-113">toorun hello automaticamente la distribuzione, fare clic su hello seguente pulsante:</span><span class="sxs-lookup"><span data-stu-id="f9127-113">toorun hello deployment automatically, click hello following button:</span></span>

<span data-ttu-id="f9127-114">[![Distribuire tooAzure](./media/cache-web-app-arm-with-redis-cache-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-with-redis-cache%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="f9127-114">[![Deploy tooAzure](./media/cache-web-app-arm-with-redis-cache-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-with-redis-cache%2Fazuredeploy.json)</span></span>

## <a name="parameters-toospecify"></a><span data-ttu-id="f9127-115">I parametri toospecify</span><span class="sxs-lookup"><span data-stu-id="f9127-115">Parameters toospecify</span></span>
[!INCLUDE [app-service-web-deploy-web-parameters](../../includes/app-service-web-deploy-web-parameters.md)]

[!INCLUDE [cache-deploy-parameters](../../includes/cache-deploy-parameters.md)]

## <a name="variables-for-names"></a><span data-ttu-id="f9127-116">Variabili per i nomi</span><span class="sxs-lookup"><span data-stu-id="f9127-116">Variables for names</span></span>
<span data-ttu-id="f9127-117">Il modello utilizza i nomi delle variabili tooconstruct per le risorse di hello.</span><span class="sxs-lookup"><span data-stu-id="f9127-117">This template uses variables tooconstruct names for hello resources.</span></span> <span data-ttu-id="f9127-118">Usa hello [uniqueString](../azure-resource-manager/resource-group-template-functions-string.md#uniquestring) funzione tooconstruct un valore in base all'id di gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="f9127-118">It uses hello [uniqueString](../azure-resource-manager/resource-group-template-functions-string.md#uniquestring) function tooconstruct a value based on the resource group id.</span></span>

    "variables": {
      "hostingPlanName": "[concat('hostingplan', uniqueString(resourceGroup().id))]",
      "webSiteName": "[concat('webSite', uniqueString(resourceGroup().id))]",
      "cacheName": "[concat('cache', uniqueString(resourceGroup().id))]"
    },


## <a name="resources-toodeploy"></a><span data-ttu-id="f9127-119">Risorse toodeploy</span><span class="sxs-lookup"><span data-stu-id="f9127-119">Resources toodeploy</span></span>
[!INCLUDE [app-service-web-deploy-web-host](../../includes/app-service-web-deploy-web-host.md)]

### <a name="redis-cache"></a><span data-ttu-id="f9127-120">Cache Redis</span><span class="sxs-lookup"><span data-stu-id="f9127-120">Redis Cache</span></span>
<span data-ttu-id="f9127-121">Crea una Cache Redis di Azure viene usato con app web hello hello.</span><span class="sxs-lookup"><span data-stu-id="f9127-121">Creates hello Azure Redis Cache that is used with hello web app.</span></span> <span data-ttu-id="f9127-122">nome Hello della cache di hello è specificato in hello **cacheName** variabile.</span><span class="sxs-lookup"><span data-stu-id="f9127-122">hello name of hello cache is specified in hello **cacheName** variable.</span></span>

<span data-ttu-id="f9127-123">modello di Hello crea cache di hello in hello stesso percorso del gruppo di risorse hello.</span><span class="sxs-lookup"><span data-stu-id="f9127-123">hello template creates hello cache in hello same location as hello resource group.</span></span>

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


### <a name="web-app"></a><span data-ttu-id="f9127-124">App Web</span><span class="sxs-lookup"><span data-stu-id="f9127-124">Web app</span></span>
<span data-ttu-id="f9127-125">Crea app web hello con nome specificato in hello **webSiteName** variabile.</span><span class="sxs-lookup"><span data-stu-id="f9127-125">Creates hello web app with name specified in hello **webSiteName** variable.</span></span>

<span data-ttu-id="f9127-126">Si noti il che App web hello è configurato con l'impostazione di proprietà che consentono toowork con hello Cache Redis di app.</span><span class="sxs-lookup"><span data-stu-id="f9127-126">Notice that hello web app is configured with app setting properties that enable it toowork with hello Redis Cache.</span></span> <span data-ttu-id="f9127-127">Queste impostazioni app vengono create dinamicamente in base ai valori forniti durante la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="f9127-127">This app settings are dynamically created based on values provided during deployment.</span></span>

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

## <a name="commands-toorun-deployment"></a><span data-ttu-id="f9127-128">Comandi toorun distribuzione</span><span class="sxs-lookup"><span data-stu-id="f9127-128">Commands toorun deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a><span data-ttu-id="f9127-129">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f9127-129">PowerShell</span></span>
    New-AzureRmResourceGroupDeployment -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-with-redis-cache/azuredeploy.json -ResourceGroupName ExampleDeployGroup

### <a name="azure-cli"></a><span data-ttu-id="f9127-130">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="f9127-130">Azure CLI</span></span>
    azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-with-redis-cache/azuredeploy.json -g ExampleDeployGroup
