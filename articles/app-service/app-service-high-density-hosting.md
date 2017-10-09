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
# <a name="high-density-hosting-on-azure-app-service"></a>Hosting ad alta densità nel servizio app di Azure
Quando si utilizza servizio App, l'applicazione viene separato da hello capacità allocata tooit da due concetti:

* **Applicazione Hello:** rappresenta l'applicazione hello e la relativa configurazione di runtime. Ad esempio, include hello versione di .NET che hello runtime deve caricare le impostazioni dell'app hello.
* **Piano di servizio App Hello:** definisce le caratteristiche di hello della capacità di hello, set di funzionalità disponibili e la località di un'applicazione hello. Le caratteristiche possono ad esempio corrispondere a un computer di grandi dimensioni (quattro core), quattro istanze e funzionalità Premium negli Stati Uniti orientali.

Un'app è sempre collegato tooan piano di servizio App, ma può fornire un piano di servizio App tooone capacità o altre app.

Di conseguenza, piattaforma hello fornisce hello flessibilità tooisolate una sola app o avere più applicazioni di condividere le risorse da un piano di servizio App di condivisione.

Se più app condividono un piano di servizio app, tuttavia, un'istanza dell'app viene eseguita in ogni istanza del piano di servizio app.

## <a name="per-app-scaling"></a>Scalabilità per app
*Scalabilità per app* è una funzionalità che può essere abilitata a livello di piano di servizio app ed essere quindi usata per ogni applicazione.

La scalabilità per app consente di ridimensionare un'app indipendentemente dal piano di servizio app in cui è ospitata. In questo modo, un servizio App piano può essere ridimensionato too10 istanze, ma un'applicazione può essere impostata solo cinque toouse.

   >[!NOTE]
   >La scalabilità per app è disponibile solo per i piani di servizio app con SKU **Premium**
   >

### <a name="per-app-scaling-using-powershell"></a>Scalabilità per app tramite PowerShell

È possibile creare un piano configurato come un *per ogni app scalabilità* piano passando hello ```-perSiteScaling $true``` attributo toohello ```New-AzureRmAppServicePlan``` cmdlet

```
New-AzureRmAppServicePlan -ResourceGroupName $ResourceGroup -Name $AppServicePlan `
                            -Location $Location `
                            -Tier Premium -WorkerSize Small `
                            -NumberofWorkers 5 -PerSiteScaling $true
```

Se si desidera che un servizio App esistente tooupdate pianificare toouse questa funzionalità: 

- ottenere il piano di destinazione hello```Get-AzureRmAppServicePlan```
- Modifica proprietà hello in locale```$newASP.PerSiteScaling = $true```
- registrazione del tooazure indietro delle modifiche```Set-AzureRmAppServicePlan``` 

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

A livello di applicazione hello, dobbiamo numero hello tooconfigure delle istanze di applicazione hello può usare nel piano di servizio app hello.

Nell'esempio hello sotto app hello è limitato tootwo istanze indipendentemente dal numero di istanze hello sottostante app servizio piano scale out a.

```
# Get hello app we want tooconfigure toouse "PerSiteScaling"
$newapp = Get-AzureRmWebApp -ResourceGroupName $ResourceGroup -Name $webapp
    
# Modify hello NumberOfWorkers setting toohello desired value.
$newapp.SiteConfig.NumberOfWorkers = 2
    
# Post updated app back tooazure
Set-AzureRmWebApp $newapp
```

> [!IMPORTANT]
> $newapp.SiteConfig.NumberOfWorkers è diverso da $newapp.MaxNumberOfWorkers. Per ogni app scalabilità utilizza $newapp. SiteConfig.NumberOfWorkers toodetermine hello scala caratteristiche dell'applicazione hello.

### <a name="per-app-scaling-using-azure-resource-manager"></a>Scalabilità per app tramite Azure Resource Manager

esempio Hello *modello di Azure Resource Manager* crea:

- Un piano di servizio App è la scalabilità too10 istanze
- un'app che è configurato con tooscale tooa un massimo di cinque istanze.

Hello piano di servizio App è l'impostazione hello **PerSiteScaling** tootrue proprietà ```"perSiteScaling": true```. app Hello è l'impostazione hello **numero di lavori** toouse too5 ```"properties": { "numberOfWorkers": "5" }```.

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

## <a name="recommended-configuration-for-high-density-hosting"></a>Configurazione consigliata per l'hosting ad alta densità
La scalabilità per app è una funzionalità abilitata sia nelle aree di Azure globali che negli ambienti del servizio app. Tuttavia, hello consigliabile strategia consiste nell'usare gli ambienti del servizio App tootake sfruttare le funzionalità avanzate e pool di dimensioni maggiori di hello della capacità.  

Seguire questi passaggi tooconfigure ad alta densità per le app di hosting:

1. Configurare l'ambiente del servizio App hello e scegliere un pool di lavoro è uno scenario di hosting toohello dedicato ad alta densità.
1. Creare un singolo piano di servizio App e le proporzioni toouse tutti hello capacità disponibile nel pool di lavoro hello.
1. Impostare hello PerSiteScaling flag tootrue hello piano di servizio App.
1. Nuove app vengono create e assegnate toothat piano di servizio App con il **il numero di lavori** impostata troppo**1**. Con questa configurazione genera hello massima densità possibile in questo pool di lavoro.
1. il numero di lavori Hello può essere configurato indipendentemente per risorse aggiuntive di app toogrant in base alle esigenze. ad esempio:
    - Un'utilizzo elevato di app è possibile impostare **il numero di lavori** troppo**3** toohave più capacità per l'app di elaborazione. 
    - Consente di impostare le app di basso utilizzo **il numero di lavori** troppo**1**.

## <a name="next-steps"></a>Passaggi successivi

- [Panoramica approfondita dei piani di servizio app di Azure](azure-web-sites-web-hosting-plans-in-depth-overview.md)
- [Introduzione tooApp ambiente del servizio](../app-service-web/app-service-app-service-environment-intro.md)
