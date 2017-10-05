---
title: "Hosting ad alta densità nel servizio app di Azure | Microsoft Docs"
description: "Hosting ad alta densità nel servizio app di Azure"
author: btardif
manager: erikre
editor: 
services: app-service\web
documentationcenter: 
ms.assetid: a903cb78-4927-47b0-8427-56412c4e3e64
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 06/12/2017
ms.author: byvinyal
ms.openlocfilehash: 459a310a719695f6366470976d857ec2f9d6f4a1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="high-density-hosting-on-azure-app-service"></a><span data-ttu-id="87341-103">Hosting ad alta densità nel servizio app di Azure</span><span class="sxs-lookup"><span data-stu-id="87341-103">High density hosting on Azure App Service</span></span>
<span data-ttu-id="87341-104">Quando si usa il servizio app, l'applicazione viene distinta dalla capacità ad essa allocata in base a due concetti:</span><span class="sxs-lookup"><span data-stu-id="87341-104">When using App Service, your application is decoupled from the capacity allocated to it by two concepts:</span></span>

* <span data-ttu-id="87341-105">**Applicazione:** rappresenta l'app e la relativa configurazione di runtime.</span><span class="sxs-lookup"><span data-stu-id="87341-105">**The Application:** Represents the app and its runtime configuration.</span></span> <span data-ttu-id="87341-106">Include ad esempio la versione di .NET che dovrà essere caricata dal runtime e le impostazioni dell'app.</span><span class="sxs-lookup"><span data-stu-id="87341-106">For example, it includes the version of .NET that the runtime should load, the app settings.</span></span>
* <span data-ttu-id="87341-107">**Piano di servizio app:** definisce le caratteristiche in termini di capacità, set di funzionalità disponibile e località dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="87341-107">**The App Service Plan:** Defines the characteristics of the capacity, available feature set, and locality of the application.</span></span> <span data-ttu-id="87341-108">Le caratteristiche possono ad esempio corrispondere a un computer di grandi dimensioni (quattro core), quattro istanze e funzionalità Premium negli Stati Uniti orientali.</span><span class="sxs-lookup"><span data-stu-id="87341-108">For example, characteristics might be large (four cores) machine, four instances, Premium features in East US.</span></span>

<span data-ttu-id="87341-109">Un'app è sempre collegata a un piano di servizio app, ma un piano di servizio app può fornire capacità a una o più app.</span><span class="sxs-lookup"><span data-stu-id="87341-109">An app is always linked to an App Service plan, but an App Service plan can provide capacity to one or more apps.</span></span>

<span data-ttu-id="87341-110">La piattaforma garantisce quindi la possibilità di isolare una singola app o consentire a più app di condividere le risorse condividendo un piano di servizio app.</span><span class="sxs-lookup"><span data-stu-id="87341-110">As a result, the platform provides the flexibility to isolate a single app or have multiple apps share resources by sharing an App Service plan.</span></span>

<span data-ttu-id="87341-111">Se più app condividono un piano di servizio app, tuttavia, un'istanza dell'app viene eseguita in ogni istanza del piano di servizio app.</span><span class="sxs-lookup"><span data-stu-id="87341-111">However, when multiple apps share an App Service plan, an instance of that app runs on every instance of that App Service plan.</span></span>

## <a name="per-app-scaling"></a><span data-ttu-id="87341-112">Scalabilità per app</span><span class="sxs-lookup"><span data-stu-id="87341-112">Per app scaling</span></span>
<span data-ttu-id="87341-113">*Scalabilità per app* è una funzionalità che può essere abilitata a livello di piano di servizio app ed essere quindi usata per ogni applicazione.</span><span class="sxs-lookup"><span data-stu-id="87341-113">*Per app scaling* is a feature that can be enabled at the App Service plan level and then used per application.</span></span>

<span data-ttu-id="87341-114">La scalabilità per app consente di ridimensionare un'app indipendentemente dal piano di servizio app in cui è ospitata.</span><span class="sxs-lookup"><span data-stu-id="87341-114">Per app scaling scales an app independently from the App Service plan that hosts it.</span></span> <span data-ttu-id="87341-115">È così possibile configurare un piano di servizio app per offrire 10 istanze e impostare un'app in modo che usi solo cinque istanze.</span><span class="sxs-lookup"><span data-stu-id="87341-115">This way, an App Service plan can be scaled to 10 instances, but an app can be set to use only five.</span></span>

   >[!NOTE]
   ><span data-ttu-id="87341-116">La scalabilità per app è disponibile solo per i piani di servizio app con SKU **Premium**</span><span class="sxs-lookup"><span data-stu-id="87341-116">Per app scaling is available only for **Premium** SKU App Service plans</span></span>
   >

### <a name="per-app-scaling-using-powershell"></a><span data-ttu-id="87341-117">Scalabilità per app tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="87341-117">Per app scaling using PowerShell</span></span>

<span data-ttu-id="87341-118">È possibile creare un piano configurato come piano di *scalabilità per app* passando l'attributo ```-perSiteScaling $true``` al cmdlet ```New-AzureRmAppServicePlan```</span><span class="sxs-lookup"><span data-stu-id="87341-118">You can create a plan configured as a *Per app scaling* plan by passing in the ```-perSiteScaling $true``` attribute to the ```New-AzureRmAppServicePlan``` commandlet</span></span>

```
New-AzureRmAppServicePlan -ResourceGroupName $ResourceGroup -Name $AppServicePlan `
                            -Location $Location `
                            -Tier Premium -WorkerSize Small `
                            -NumberofWorkers 5 -PerSiteScaling $true
```

<span data-ttu-id="87341-119">Se si desidera aggiornare un piano di servizio app esistente per usare questa funzionalità:</span><span class="sxs-lookup"><span data-stu-id="87341-119">If you want to update an existing App Service plan to use this feature:</span></span> 

- <span data-ttu-id="87341-120">ottenere il piano di destinazione ```Get-AzureRmAppServicePlan```</span><span class="sxs-lookup"><span data-stu-id="87341-120">get the target plan ```Get-AzureRmAppServicePlan```</span></span>
- <span data-ttu-id="87341-121">modificare la proprietà localmente ```$newASP.PerSiteScaling = $true```</span><span class="sxs-lookup"><span data-stu-id="87341-121">modifying the property locally ```$newASP.PerSiteScaling = $true```</span></span>
- <span data-ttu-id="87341-122">pubblicare le modifiche su Azure ```Set-AzureRmAppServicePlan```</span><span class="sxs-lookup"><span data-stu-id="87341-122">posting your changes back to azure ```Set-AzureRmAppServicePlan```</span></span> 

```
# Get the new App Service Plan and modify the "PerSiteScaling" property.
$newASP = Get-AzureRmAppServicePlan -ResourceGroupName $ResourceGroup -Name $AppServicePlan
$newASP

#Modify the local copy to use "PerSiteScaling" property.
$newASP.PerSiteScaling = $true
$newASP
    
#Post updated app service plan back to azure
Set-AzureRmAppServicePlan $newASP
```

<span data-ttu-id="87341-123">A livello di app, è necessario configurare il numero di istanze che l'app può usare nel piano di servizio app.</span><span class="sxs-lookup"><span data-stu-id="87341-123">At the app level, we need to configure the number of instances the app can use in the app service plan.</span></span>

<span data-ttu-id="87341-124">Nell'esempio seguente l'app è limitata a due istanze indipendentemente dall'aggiunta del numero di istanze al piano di servizio app sottostante.</span><span class="sxs-lookup"><span data-stu-id="87341-124">In the example below, the app is limited to two instances regardless of how many instances the underlying app service plan scales out to.</span></span>

```
# Get the app we want to configure to use "PerSiteScaling"
$newapp = Get-AzureRmWebApp -ResourceGroupName $ResourceGroup -Name $webapp
    
# Modify the NumberOfWorkers setting to the desired value.
$newapp.SiteConfig.NumberOfWorkers = 2
    
# Post updated app back to azure
Set-AzureRmWebApp $newapp
```

> [!IMPORTANT]
> <span data-ttu-id="87341-125">$newapp.SiteConfig.NumberOfWorkers è diverso da $newapp.MaxNumberOfWorkers.</span><span class="sxs-lookup"><span data-stu-id="87341-125">$newapp.SiteConfig.NumberOfWorkers is different form $newapp.MaxNumberOfWorkers.</span></span> <span data-ttu-id="87341-126">La scalabilità per app usa $newapp.SiteConfig.NumberOfWorkers per determinare le caratteristiche di scalabilità dell'app.</span><span class="sxs-lookup"><span data-stu-id="87341-126">Per app scaling uses $newapp.SiteConfig.NumberOfWorkers to determine the scale characteristics of the app.</span></span>

### <a name="per-app-scaling-using-azure-resource-manager"></a><span data-ttu-id="87341-127">Scalabilità per app tramite Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="87341-127">Per app scaling using Azure Resource Manager</span></span>

<span data-ttu-id="87341-128">Il *modello di Azure Resource Manager* seguente crea:</span><span class="sxs-lookup"><span data-stu-id="87341-128">The following *Azure Resource Manager template* creates:</span></span>

- <span data-ttu-id="87341-129">un piano di servizio app a cui sono aggiunte 10 istanze</span><span class="sxs-lookup"><span data-stu-id="87341-129">An App Service plan that's scaled out to 10 instances</span></span>
- <span data-ttu-id="87341-130">un'app che è configurata per l'aggiunta di un massimo di cinque istanze.</span><span class="sxs-lookup"><span data-stu-id="87341-130">an app that's configured to scale to a max of five instances.</span></span>

<span data-ttu-id="87341-131">Il piano di servizio app imposta la proprietà **PerSiteScaling** su true ```"perSiteScaling": true```.</span><span class="sxs-lookup"><span data-stu-id="87341-131">The App Service plan is setting the **PerSiteScaling** property to true ```"perSiteScaling": true```.</span></span> <span data-ttu-id="87341-132">L'app imposta il **numero di ruoli di lavoro** da usare su 5 ```"properties": { "numberOfWorkers": "5" }```.</span><span class="sxs-lookup"><span data-stu-id="87341-132">The app is setting the **number of workers** to use to 5 ```"properties": { "numberOfWorkers": "5" }```.</span></span>

```
{
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters":{
        "appServicePlanName": { "type": "string" },
        "appName": { "type": "string" }
        },
    "resources": [
    {
        "comments": "App Service Plan with per site perSiteScaling = true",
        "type": "Microsoft.Web/serverFarms",
        "sku": {
            "name": "P1",
            "tier": "Premium",
            "size": "P1",
            "family": "P",
            "capacity": 10
            },
        "name": "[parameters('appServicePlanName')]",
        "apiVersion": "2015-08-01",
        "location": "West US",
        "properties": {
            "name": "[parameters('appServicePlanName')]",
            "perSiteScaling": true
        }
    },
    {
        "type": "Microsoft.Web/sites",
        "name": "[parameters('appName')]",
        "apiVersion": "2015-08-01-preview",
        "location": "West US",
        "dependsOn": [ "[resourceId('Microsoft.Web/serverFarms', parameters('appServicePlanName'))]" ],
        "properties": { "serverFarmId": "[resourceId('Microsoft.Web/serverFarms', parameters('appServicePlanName'))]" },
        "resources": [ {
                "comments": "",
                "type": "config",
                "name": "web",
                "apiVersion": "2015-08-01",
                "location": "West US",
                "dependsOn": [ "[resourceId('Microsoft.Web/Sites', parameters('appName'))]" ],
                "properties": { "numberOfWorkers": "5" }
            } ]
        }]
}
```

## <a name="recommended-configuration-for-high-density-hosting"></a><span data-ttu-id="87341-133">Configurazione consigliata per l'hosting ad alta densità</span><span class="sxs-lookup"><span data-stu-id="87341-133">Recommended configuration for high density hosting</span></span>
<span data-ttu-id="87341-134">La scalabilità per app è una funzionalità abilitata sia nelle aree di Azure globali che negli ambienti del servizio app.</span><span class="sxs-lookup"><span data-stu-id="87341-134">Per app scaling is a feature that is enabled in both global Azure regions and App Service Environments.</span></span> <span data-ttu-id="87341-135">È tuttavia consigliabile usare gli ambienti del servizio app per sfruttarne le funzionalità avanzate e i pool di capacità di maggiori dimensioni.</span><span class="sxs-lookup"><span data-stu-id="87341-135">However, the recommended strategy is to use App Service Environments to take advantage of their advanced features and the larger pools of capacity.</span></span>  

<span data-ttu-id="87341-136">Per configurare l'hosting ad alta densità per le app, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="87341-136">Follow these steps to configure high density hosting for your apps:</span></span>

1. <span data-ttu-id="87341-137">Configurare l'ambiente del servizio app e scegliere un pool di lavoro da dedicare allo scenario di hosting ad alta densità.</span><span class="sxs-lookup"><span data-stu-id="87341-137">Configure the App Service Environment and choose a worker pool that is dedicated to the high density hosting scenario.</span></span>
1. <span data-ttu-id="87341-138">Creare un singolo piano di servizio app e ridimensionarlo in modo da usare tutta la capacità disponibile del pool di lavoro.</span><span class="sxs-lookup"><span data-stu-id="87341-138">Create a single App Service plan, and scale it to use all the available capacity on the worker pool.</span></span>
1. <span data-ttu-id="87341-139">Impostare il flag PerSiteScaling su true nel piano di servizio app.</span><span class="sxs-lookup"><span data-stu-id="87341-139">Set the PerSiteScaling flag to true on the App Service plan.</span></span>
1. <span data-ttu-id="87341-140">Vengono create nuove app e assegnate al piano di servizio app con la proprietà **numberOfWorkers** impostata su **1**.</span><span class="sxs-lookup"><span data-stu-id="87341-140">New apps are created and assigned to that App Service plan with the **numberOfWorkers** property set to **1**.</span></span> <span data-ttu-id="87341-141">L'uso di questa configurazione consente di ottenere la massima densità possibile nel pool di lavoro.</span><span class="sxs-lookup"><span data-stu-id="87341-141">Using this configuration yields the highest density possible on this worker pool.</span></span>
1. <span data-ttu-id="87341-142">Il numero di ruoli di lavoro può essere configurato in modo indipendente per ogni app, per concedere risorse aggiuntive in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="87341-142">The number of workers can be configured independently per app to grant additional resources as needed.</span></span> <span data-ttu-id="87341-143">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="87341-143">For example:</span></span>
    - <span data-ttu-id="87341-144">Per un'app a utilizzo elevato è possibile impostare **numberOfWorkers** su **3** per avere una maggiore capacità di elaborazione per l'app.</span><span class="sxs-lookup"><span data-stu-id="87341-144">A high-use app can set **numberOfWorkers** to **3** to have more processing capacity for that app.</span></span> 
    - <span data-ttu-id="87341-145">Per le app a basso utilizzo impostare **numberOfWorkers** su **1**.</span><span class="sxs-lookup"><span data-stu-id="87341-145">Low-use apps would set **numberOfWorkers** to **1**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="87341-146">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="87341-146">Next Steps</span></span>

- [<span data-ttu-id="87341-147">Panoramica approfondita dei piani di servizio app di Azure</span><span class="sxs-lookup"><span data-stu-id="87341-147">Azure App Service plans in-depth overview</span></span>](azure-web-sites-web-hosting-plans-in-depth-overview.md)
- [<span data-ttu-id="87341-148">Introduzione all'ambiente del servizio app</span><span class="sxs-lookup"><span data-stu-id="87341-148">Introduction to App Service Environment</span></span>](../app-service-web/app-service-app-service-environment-intro.md)