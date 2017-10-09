---
title: aaaPowerShell script toocreate una risorsa di Application Insights | Documenti Microsoft
description: Consente di automatizzare la creazione di risorse di Application Insights.
services: application-insights
documentationcenter: windows
author: CFreemanwa
manager: carmonm
ms.assetid: f0082c9b-43ad-4576-a417-4ea8e0daf3d9
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 11/19/2016
ms.author: bwren
ms.openlocfilehash: 2ac00376d38026d64c2c5deabfaca60588924510
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="powershell-script-toocreate-an-application-insights-resource"></a><span data-ttu-id="5c370-103">Script di PowerShell toocreate una risorsa di Application Insights</span><span class="sxs-lookup"><span data-stu-id="5c370-103">PowerShell script toocreate an Application Insights resource</span></span>


<span data-ttu-id="5c370-104">Quando si desidera toomonitor una nuova applicazione - o una nuova versione di un'applicazione - con [Azure Application Insights](https://azure.microsoft.com/services/application-insights/), impostare una nuova risorsa in Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="5c370-104">When you want toomonitor a new application - or a new version of an application - with [Azure Application Insights](https://azure.microsoft.com/services/application-insights/), you set up a new resource in Microsoft Azure.</span></span> <span data-ttu-id="5c370-105">Questa risorsa è in cui i dati di telemetria hello dall'app vengono analizzati e visualizzati.</span><span class="sxs-lookup"><span data-stu-id="5c370-105">This resource is where hello telemetry data from your app is analyzed and displayed.</span></span> 

<span data-ttu-id="5c370-106">È possibile automatizzare la creazione di hello di una nuova risorsa tramite PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5c370-106">You can automate hello creation of a new resource by using PowerShell.</span></span>

<span data-ttu-id="5c370-107">Se, ad esempio, si intende sviluppare un'app per dispositivi mobili, è probabile che, in un dato momento, i clienti usino diverse versioni pubblicate dell'app.</span><span class="sxs-lookup"><span data-stu-id="5c370-107">For example, if you are developing a mobile device app, it's likely that, at any time, there will be several published versions of your app in use by your customers.</span></span> <span data-ttu-id="5c370-108">Per evitare che i risultati di telemetria hello tooget da diverse versioni confuse.</span><span class="sxs-lookup"><span data-stu-id="5c370-108">You don't want tooget hello telemetry results from different versions mixed up.</span></span> <span data-ttu-id="5c370-109">Per ottenere il toocreate processo di compilazione una nuova risorsa per ogni compilazione.</span><span class="sxs-lookup"><span data-stu-id="5c370-109">So you get your build process toocreate a new resource for each build.</span></span>

> [!NOTE]
> <span data-ttu-id="5c370-110">Se si desidera toocreate un set di risorse tutto hello stesso tempo, prendere in considerazione [la creazione di risorse hello utilizzando un modello di Azure](app-insights-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="5c370-110">If you want toocreate a set of resources all at hello same time, consider [creating hello resources using an Azure template](app-insights-powershell.md).</span></span>
> 
> 

## <a name="script-toocreate-an-application-insights-resource"></a><span data-ttu-id="5c370-111">Script toocreate una risorsa di Application Insights</span><span class="sxs-lookup"><span data-stu-id="5c370-111">Script toocreate an Application Insights resource</span></span>
<span data-ttu-id="5c370-112">Vedere le specifiche di cmdlet pertinenti hello:</span><span class="sxs-lookup"><span data-stu-id="5c370-112">See hello relevant cmdlet specs:</span></span>

* [<span data-ttu-id="5c370-113">New-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="5c370-113">New-AzureRmResource</span></span>](https://msdn.microsoft.com/library/mt652510.aspx)
* [<span data-ttu-id="5c370-114">New-AzureRmRoleAssignment</span><span class="sxs-lookup"><span data-stu-id="5c370-114">New-AzureRmRoleAssignment</span></span>](https://msdn.microsoft.com/library/mt678995.aspx)

<span data-ttu-id="5c370-115">*Script di PowerShell*</span><span class="sxs-lookup"><span data-stu-id="5c370-115">*PowerShell Script*</span></span>  

```PowerShell


###########################################
# Set Values
###########################################

# If running manually, uncomment before hello first 
# execution toologin toohello Azure Portal:

# Add-AzureRmAccount / Login-AzureRmAccount

# Set hello name of hello Application Insights Resource

$appInsightsName = "TestApp"

# Set hello application name used for hello value of hello Tag "AppInsightsApp" 

$applicationTagName = "MyApp"

# Set hello name of hello Resource Group toouse.  
# Default is hello application name.
$resourceGroupName = "MyAppResourceGroup"

###################################################
# Create hello Resource and Output hello name and iKey
###################################################

# Select hello azure subscription
Select-AzureSubscription -SubscriptionName "MySubscription"

# Create hello App Insights Resource


$resource = New-AzureRmResource `
  -ResourceName $appInsightsName `
  -ResourceGroupName $resourceGroupName `
  -Tag @{ applicationType = "web"; applicationName = $applicationTagName} `
  -ResourceType "Microsoft.Insights/components" `
  -Location "East US" `  # or North Europe, West Europe, South Central US
  -PropertyObject @{"Application_Type"="web"} `
  -Force

# Give owner access toohello team

New-AzureRmRoleAssignment `
  -SignInName "myteam@fabrikam.com" `
  -RoleDefinitionName Owner `
  -Scope $resource.ResourceId 


# Display iKey
Write-Host "App Insights Name = " $resource.Name
Write-Host "IKey = " $resource.Properties.InstrumentationKey

```

## <a name="what-toodo-with-hello-ikey"></a><span data-ttu-id="5c370-116">Quali toodo con iKey hello</span><span class="sxs-lookup"><span data-stu-id="5c370-116">What toodo with hello iKey</span></span>
<span data-ttu-id="5c370-117">Per identificare le singole risorse, viene usata una chiave di strumentazione (iKey),</span><span class="sxs-lookup"><span data-stu-id="5c370-117">Each resource is identified by its instrumentation key (iKey).</span></span> <span data-ttu-id="5c370-118">iKey Hello è un output dello script di creazione risorsa hello.</span><span class="sxs-lookup"><span data-stu-id="5c370-118">hello iKey is an output of hello resource creation script.</span></span> <span data-ttu-id="5c370-119">Lo script di compilazione deve fornire hello iKey toohello che Application Insights SDK incorporato nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="5c370-119">Your build script should provide hello iKey toohello Application Insights SDK embedded in your app.</span></span>

<span data-ttu-id="5c370-120">Esistono due modi toomake hello iKey disponibili toohello SDK:</span><span class="sxs-lookup"><span data-stu-id="5c370-120">There are two ways toomake hello iKey available toohello SDK:</span></span>

* <span data-ttu-id="5c370-121">In [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md):</span><span class="sxs-lookup"><span data-stu-id="5c370-121">In [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md):</span></span> 
  * <span data-ttu-id="5c370-122">`<instrumentationkey>`*ikey*`</instrumentationkey>`</span><span class="sxs-lookup"><span data-stu-id="5c370-122">`<instrumentationkey>`*ikey*`</instrumentationkey>`</span></span>
* <span data-ttu-id="5c370-123">Oppure nel [codice di inizializzazione](app-insights-api-custom-events-metrics.md):</span><span class="sxs-lookup"><span data-stu-id="5c370-123">Or in [initialization code](app-insights-api-custom-events-metrics.md):</span></span> 
  * <span data-ttu-id="5c370-124">`Microsoft.ApplicationInsights.Extensibility.
    TelemetryConfiguration.Active.InstrumentationKey = "`*iKey*`";`</span><span class="sxs-lookup"><span data-stu-id="5c370-124">`Microsoft.ApplicationInsights.Extensibility.
TelemetryConfiguration.Active.InstrumentationKey = "`*iKey*`";`</span></span>

## <a name="see-also"></a><span data-ttu-id="5c370-125">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="5c370-125">See also</span></span>
* [<span data-ttu-id="5c370-126">Creare risorse Application Insights e test web da modelli</span><span class="sxs-lookup"><span data-stu-id="5c370-126">Create Application Insights and web test resources from templates</span></span>](app-insights-powershell.md)
* [<span data-ttu-id="5c370-127">Impostare il monitoraggio di diagnostica Azure con PowerShell</span><span class="sxs-lookup"><span data-stu-id="5c370-127">Set up monitoring of Azure diagnostics with PowerShell</span></span>](app-insights-powershell-azure-diagnostics.md) 
* [<span data-ttu-id="5c370-128">Impostare avvisi tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="5c370-128">Set alerts by using PowerShell</span></span>](app-insights-powershell-alerts.md)

