---
title: "aaaHigh densità hosting nel servizio App di Azure | Documenti Microsoft"
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
ms.openlocfilehash: a10cb81ace13ba6992b572a44361061ecf72b266
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="high-density-hosting-on-azure-app-service"></a><span data-ttu-id="ce27a-103">Hosting ad alta densità nel servizio app di Azure</span><span class="sxs-lookup"><span data-stu-id="ce27a-103">High density hosting on Azure App Service</span></span>
<span data-ttu-id="ce27a-104">Quando si utilizza servizio App, l'applicazione viene separato da hello capacità allocata tooit da due concetti:</span><span class="sxs-lookup"><span data-stu-id="ce27a-104">When using App Service, your application is decoupled from hello capacity allocated tooit by two concepts:</span></span>

* <span data-ttu-id="ce27a-105">**Applicazione Hello:** rappresenta l'applicazione hello e la relativa configurazione di runtime.</span><span class="sxs-lookup"><span data-stu-id="ce27a-105">**hello Application:** Represents hello app and its runtime configuration.</span></span> <span data-ttu-id="ce27a-106">Ad esempio, include hello versione di .NET che hello runtime deve caricare le impostazioni dell'app hello.</span><span class="sxs-lookup"><span data-stu-id="ce27a-106">For example, it includes hello version of .NET that hello runtime should load, hello app settings.</span></span>
* <span data-ttu-id="ce27a-107">**Piano di servizio App Hello:** definisce le caratteristiche di hello della capacità di hello, set di funzionalità disponibili e la località di un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="ce27a-107">**hello App Service Plan:** Defines hello characteristics of hello capacity, available feature set, and locality of hello application.</span></span> <span data-ttu-id="ce27a-108">Le caratteristiche possono ad esempio corrispondere a un computer di grandi dimensioni (quattro core), quattro istanze e funzionalità Premium negli Stati Uniti orientali.</span><span class="sxs-lookup"><span data-stu-id="ce27a-108">For example, characteristics might be large (four cores) machine, four instances, Premium features in East US.</span></span>

<span data-ttu-id="ce27a-109">Un'app è sempre collegato tooan piano di servizio App, ma può fornire un piano di servizio App tooone capacità o altre app.</span><span class="sxs-lookup"><span data-stu-id="ce27a-109">An app is always linked tooan App Service plan, but an App Service plan can provide capacity tooone or more apps.</span></span>

<span data-ttu-id="ce27a-110">Di conseguenza, piattaforma hello fornisce hello flessibilità tooisolate una sola app o avere più applicazioni di condividere le risorse da un piano di servizio App di condivisione.</span><span class="sxs-lookup"><span data-stu-id="ce27a-110">As a result, hello platform provides hello flexibility tooisolate a single app or have multiple apps share resources by sharing an App Service plan.</span></span>

<span data-ttu-id="ce27a-111">Se più app condividono un piano di servizio app, tuttavia, un'istanza dell'app viene eseguita in ogni istanza del piano di servizio app.</span><span class="sxs-lookup"><span data-stu-id="ce27a-111">However, when multiple apps share an App Service plan, an instance of that app runs on every instance of that App Service plan.</span></span>

## <a name="per-app-scaling"></a><span data-ttu-id="ce27a-112">Scalabilità per app</span><span class="sxs-lookup"><span data-stu-id="ce27a-112">Per app scaling</span></span>
<span data-ttu-id="ce27a-113">*Scalabilità per app* è una funzionalità che può essere abilitata a livello di piano di servizio app ed essere quindi usata per ogni applicazione.</span><span class="sxs-lookup"><span data-stu-id="ce27a-113">*Per app scaling* is a feature that can be enabled at the App Service plan level and then used per application.</span></span>

<span data-ttu-id="ce27a-114">La scalabilità per app consente di ridimensionare un'app indipendentemente dal piano di servizio app in cui è ospitata.</span><span class="sxs-lookup"><span data-stu-id="ce27a-114">Per app scaling scales an app independently from the App Service plan that hosts it.</span></span> <span data-ttu-id="ce27a-115">In questo modo, un servizio App piano può essere ridimensionato too10 istanze, ma un'applicazione può essere impostata solo cinque toouse.</span><span class="sxs-lookup"><span data-stu-id="ce27a-115">This way, an App Service plan can be scaled too10 instances, but an app can be set toouse only five.</span></span>

   >[!NOTE]
   ><span data-ttu-id="ce27a-116">La scalabilità per app è disponibile solo per i piani di servizio app con SKU **Premium**</span><span class="sxs-lookup"><span data-stu-id="ce27a-116">Per app scaling is available only for **Premium** SKU App Service plans</span></span>
   >

### <a name="per-app-scaling-using-powershell"></a><span data-ttu-id="ce27a-117">Scalabilità per app tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="ce27a-117">Per app scaling using PowerShell</span></span>

<span data-ttu-id="ce27a-118">È possibile creare un piano configurato come un *per ogni app scalabilità* piano passando hello ```-perSiteScaling $true``` attributo toohello ```New-AzureRmAppServicePlan``` cmdlet</span><span class="sxs-lookup"><span data-stu-id="ce27a-118">You can create a plan configured as a *Per app scaling* plan by passing in hello ```-perSiteScaling $true``` attribute toohello ```New-AzureRmAppServicePlan``` commandlet</span></span>

```
New-AzureRmAppServicePlan -ResourceGroupName $ResourceGroup -Name $AppServicePlan `
                            -Location $Location `
                            -Tier Premium -WorkerSize Small `
                            -NumberofWorkers 5 -PerSiteScaling $true
```

<span data-ttu-id="ce27a-119">Se si desidera che un servizio App esistente tooupdate pianificare toouse questa funzionalità:</span><span class="sxs-lookup"><span data-stu-id="ce27a-119">If you want tooupdate an existing App Service plan toouse this feature:</span></span> 

- <span data-ttu-id="ce27a-120">ottenere il piano di destinazione hello```Get-AzureRmAppServicePlan```</span><span class="sxs-lookup"><span data-stu-id="ce27a-120">get hello target plan ```Get-AzureRmAppServicePlan```</span></span>
- <span data-ttu-id="ce27a-121">Modifica proprietà hello in locale```$newASP.PerSiteScaling = $true```</span><span class="sxs-lookup"><span data-stu-id="ce27a-121">modifying hello property locally ```$newASP.PerSiteScaling = $true```</span></span>
- <span data-ttu-id="ce27a-122">registrazione del tooazure indietro delle modifiche```Set-AzureRmAppServicePlan```</span><span class="sxs-lookup"><span data-stu-id="ce27a-122">posting your changes back tooazure ```Set-AzureRmAppServicePlan```</span></span> 

```
# Get hello new App Service Plan and modify hello "PerSiteScaling" property.
$newASP = Get-AzureRmAppServicePlan -ResourceGroupName $ResourceGroup -Name $AppServicePlan
$newASP

#Modify hello local copy toouse "PerSiteScaling" property.
$newASP.PerSiteScaling = $true
$newASP
    
#Post updated app service plan back tooazure
Set-AzureRmAppServicePlan $newASP
```

<span data-ttu-id="ce27a-123">A livello di applicazione hello, dobbiamo numero hello tooconfigure delle istanze di applicazione hello può usare nel piano di servizio app hello.</span><span class="sxs-lookup"><span data-stu-id="ce27a-123">At hello app level, we need tooconfigure hello number of instances hello app can use in hello app service plan.</span></span>

<span data-ttu-id="ce27a-124">Nell'esempio hello sotto app hello è limitato tootwo istanze indipendentemente dal numero di istanze hello sottostante app servizio piano scale out a.</span><span class="sxs-lookup"><span data-stu-id="ce27a-124">In hello example below, hello app is limited tootwo instances regardless of how many instances hello underlying app service plan scales out to.</span></span>

```
# Get hello app we want tooconfigure toouse "PerSiteScaling"
$newapp = Get-AzureRmWebApp -ResourceGroupName $ResourceGroup -Name $webapp
    
# Modify hello NumberOfWorkers setting toohello desired value.
$newapp.SiteConfig.NumberOfWorkers = 2
    
# Post updated app back tooazure
Set-AzureRmWebApp $newapp
```

> [!IMPORTANT]
> <span data-ttu-id="ce27a-125">$newapp.SiteConfig.NumberOfWorkers è diverso da $newapp.MaxNumberOfWorkers.</span><span class="sxs-lookup"><span data-stu-id="ce27a-125">$newapp.SiteConfig.NumberOfWorkers is different form $newapp.MaxNumberOfWorkers.</span></span> <span data-ttu-id="ce27a-126">Per ogni app scalabilità utilizza $newapp. SiteConfig.NumberOfWorkers toodetermine hello scala caratteristiche dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="ce27a-126">Per app scaling uses $newapp.SiteConfig.NumberOfWorkers toodetermine hello scale characteristics of hello app.</span></span>

### <a name="per-app-scaling-using-azure-resource-manager"></a><span data-ttu-id="ce27a-127">Scalabilità per app tramite Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="ce27a-127">Per app scaling using Azure Resource Manager</span></span>

<span data-ttu-id="ce27a-128">esempio Hello *modello di Azure Resource Manager* crea:</span><span class="sxs-lookup"><span data-stu-id="ce27a-128">hello following *Azure Resource Manager template* creates:</span></span>

- <span data-ttu-id="ce27a-129">Un piano di servizio App è la scalabilità too10 istanze</span><span class="sxs-lookup"><span data-stu-id="ce27a-129">An App Service plan that's scaled out too10 instances</span></span>
- <span data-ttu-id="ce27a-130">un'app che è configurato con tooscale tooa un massimo di cinque istanze.</span><span class="sxs-lookup"><span data-stu-id="ce27a-130">an app that's configured tooscale tooa max of five instances.</span></span>

<span data-ttu-id="ce27a-131">Hello piano di servizio App è l'impostazione hello **PerSiteScaling** tootrue proprietà ```"perSiteScaling": true```.</span><span class="sxs-lookup"><span data-stu-id="ce27a-131">hello App Service plan is setting hello **PerSiteScaling** property tootrue ```"perSiteScaling": true```.</span></span> <span data-ttu-id="ce27a-132">app Hello è l'impostazione hello **numero di lavori** toouse too5 ```"properties": { "numberOfWorkers": "5" }```.</span><span class="sxs-lookup"><span data-stu-id="ce27a-132">hello app is setting hello **number of workers** toouse too5 ```"properties": { "numberOfWorkers": "5" }```.</span></span>

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

## <a name="recommended-configuration-for-high-density-hosting"></a><span data-ttu-id="ce27a-133">Configurazione consigliata per l'hosting ad alta densità</span><span class="sxs-lookup"><span data-stu-id="ce27a-133">Recommended configuration for high density hosting</span></span>
<span data-ttu-id="ce27a-134">La scalabilità per app è una funzionalità abilitata sia nelle aree di Azure globali che negli ambienti del servizio app.</span><span class="sxs-lookup"><span data-stu-id="ce27a-134">Per app scaling is a feature that is enabled in both global Azure regions and App Service Environments.</span></span> <span data-ttu-id="ce27a-135">Tuttavia, hello consigliabile strategia consiste nell'usare gli ambienti del servizio App tootake sfruttare le funzionalità avanzate e pool di dimensioni maggiori di hello della capacità.</span><span class="sxs-lookup"><span data-stu-id="ce27a-135">However, hello recommended strategy is to use App Service Environments tootake advantage of their advanced features and hello larger pools of capacity.</span></span>  

<span data-ttu-id="ce27a-136">Seguire questi passaggi tooconfigure ad alta densità per le app di hosting:</span><span class="sxs-lookup"><span data-stu-id="ce27a-136">Follow these steps tooconfigure high density hosting for your apps:</span></span>

1. <span data-ttu-id="ce27a-137">Configurare l'ambiente del servizio App hello e scegliere un pool di lavoro è uno scenario di hosting toohello dedicato ad alta densità.</span><span class="sxs-lookup"><span data-stu-id="ce27a-137">Configure hello App Service Environment and choose a worker pool that is dedicated toohello high density hosting scenario.</span></span>
1. <span data-ttu-id="ce27a-138">Creare un singolo piano di servizio App e le proporzioni toouse tutti hello capacità disponibile nel pool di lavoro hello.</span><span class="sxs-lookup"><span data-stu-id="ce27a-138">Create a single App Service plan, and scale it toouse all hello available capacity on hello worker pool.</span></span>
1. <span data-ttu-id="ce27a-139">Impostare hello PerSiteScaling flag tootrue hello piano di servizio App.</span><span class="sxs-lookup"><span data-stu-id="ce27a-139">Set hello PerSiteScaling flag tootrue on hello App Service plan.</span></span>
1. <span data-ttu-id="ce27a-140">Nuove app vengono create e assegnate toothat piano di servizio App con il **il numero di lavori** impostata troppo**1**.</span><span class="sxs-lookup"><span data-stu-id="ce27a-140">New apps are created and assigned toothat App Service plan with the **numberOfWorkers** property set too**1**.</span></span> <span data-ttu-id="ce27a-141">Con questa configurazione genera hello massima densità possibile in questo pool di lavoro.</span><span class="sxs-lookup"><span data-stu-id="ce27a-141">Using this configuration yields hello highest density possible on this worker pool.</span></span>
1. <span data-ttu-id="ce27a-142">il numero di lavori Hello può essere configurato indipendentemente per risorse aggiuntive di app toogrant in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="ce27a-142">hello number of workers can be configured independently per app toogrant additional resources as needed.</span></span> <span data-ttu-id="ce27a-143">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="ce27a-143">For example:</span></span>
    - <span data-ttu-id="ce27a-144">Un'utilizzo elevato di app è possibile impostare **il numero di lavori** troppo**3** toohave più capacità per l'app di elaborazione.</span><span class="sxs-lookup"><span data-stu-id="ce27a-144">A high-use app can set **numberOfWorkers** too**3** toohave more processing capacity for that app.</span></span> 
    - <span data-ttu-id="ce27a-145">Consente di impostare le app di basso utilizzo **il numero di lavori** troppo**1**.</span><span class="sxs-lookup"><span data-stu-id="ce27a-145">Low-use apps would set **numberOfWorkers** too**1**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ce27a-146">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ce27a-146">Next Steps</span></span>

- [<span data-ttu-id="ce27a-147">Panoramica approfondita dei piani di servizio app di Azure</span><span class="sxs-lookup"><span data-stu-id="ce27a-147">Azure App Service plans in-depth overview</span></span>](azure-web-sites-web-hosting-plans-in-depth-overview.md)
- [<span data-ttu-id="ce27a-148">Introduzione tooApp ambiente del servizio</span><span class="sxs-lookup"><span data-stu-id="ce27a-148">Introduction tooApp Service Environment</span></span>](../app-service-web/app-service-app-service-environment-intro.md)
