---
title: Script di PowerShell per creare una risorsa di Application Insights | Documentazione Microsoft
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
ms.openlocfilehash: a828af9c7d207dd84cc626fc70206018fd67e2dd
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="powershell-script-to-create-an-application-insights-resource"></a><span data-ttu-id="0ef97-103">Script di PowerShell per creare una risorsa di Application Insights</span><span class="sxs-lookup"><span data-stu-id="0ef97-103">PowerShell script to create an Application Insights resource</span></span>


<span data-ttu-id="0ef97-104">Se si vuole monitorare una nuova applicazione oppure una nuova versione di un'applicazione con [Azure Application Insights](https://azure.microsoft.com/services/application-insights/), è possibile configurare una nuova risorsa in Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="0ef97-104">When you want to monitor a new application - or a new version of an application - with [Azure Application Insights](https://azure.microsoft.com/services/application-insights/), you set up a new resource in Microsoft Azure.</span></span> <span data-ttu-id="0ef97-105">Questa risorsa verrà usata per analizzare e visualizzare i dati di telemetria provenienti dall'app.</span><span class="sxs-lookup"><span data-stu-id="0ef97-105">This resource is where the telemetry data from your app is analyzed and displayed.</span></span> 

<span data-ttu-id="0ef97-106">Per automatizzare la creazione di una nuova risorsa con PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0ef97-106">You can automate the creation of a new resource by using PowerShell.</span></span>

<span data-ttu-id="0ef97-107">Se, ad esempio, si intende sviluppare un'app per dispositivi mobili, è probabile che, in un dato momento, i clienti usino diverse versioni pubblicate dell'app.</span><span class="sxs-lookup"><span data-stu-id="0ef97-107">For example, if you are developing a mobile device app, it's likely that, at any time, there will be several published versions of your app in use by your customers.</span></span> <span data-ttu-id="0ef97-108">Se però si vuole evitare di combinare i risultati di telemetria delle diverse versioni,</span><span class="sxs-lookup"><span data-stu-id="0ef97-108">You don't want to get the telemetry results from different versions mixed up.</span></span> <span data-ttu-id="0ef97-109">è possibile fare in modo che il processo di compilazione crei una nuova risorsa per ogni compilazione.</span><span class="sxs-lookup"><span data-stu-id="0ef97-109">So you get your build process to create a new resource for each build.</span></span>

> [!NOTE]
> <span data-ttu-id="0ef97-110">Se si desidera creare un set di risorse simultaneamente, è consigliabile [creare le risorse tramite un modello di Azure](app-insights-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="0ef97-110">If you want to create a set of resources all at the same time, consider [creating the resources using an Azure template](app-insights-powershell.md).</span></span>
> 
> 

## <a name="script-to-create-an-application-insights-resource"></a><span data-ttu-id="0ef97-111">Script per creare una risorsa di Application Insights</span><span class="sxs-lookup"><span data-stu-id="0ef97-111">Script to create an Application Insights resource</span></span>
<span data-ttu-id="0ef97-112">Vedere le specifiche dei cmdlet:</span><span class="sxs-lookup"><span data-stu-id="0ef97-112">See the relevant cmdlet specs:</span></span>

* [<span data-ttu-id="0ef97-113">New-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="0ef97-113">New-AzureRmResource</span></span>](https://msdn.microsoft.com/library/mt652510.aspx)
* [<span data-ttu-id="0ef97-114">New-AzureRmRoleAssignment</span><span class="sxs-lookup"><span data-stu-id="0ef97-114">New-AzureRmRoleAssignment</span></span>](https://msdn.microsoft.com/library/mt678995.aspx)

<span data-ttu-id="0ef97-115">*Script di PowerShell*</span><span class="sxs-lookup"><span data-stu-id="0ef97-115">*PowerShell Script*</span></span>  

```PowerShell


###########################################
# Set Values
###########################################

# If running manually, uncomment before the first 
# execution to login to the Azure Portal:

# Add-AzureRmAccount / Login-AzureRmAccount

# Set the name of the Application Insights Resource

$appInsightsName = "TestApp"

# Set the application name used for the value of the Tag "AppInsightsApp" 

$applicationTagName = "MyApp"

# Set the name of the Resource Group to use.  
# Default is the application name.
$resourceGroupName = "MyAppResourceGroup"

###################################################
# Create the Resource and Output the name and iKey
###################################################

# Select the azure subscription
Select-AzureSubscription -SubscriptionName "MySubscription"

# Create the App Insights Resource


$resource = New-AzureRmResource `
  -ResourceName $appInsightsName `
  -ResourceGroupName $resourceGroupName `
  -Tag @{ applicationType = "web"; applicationName = $applicationTagName} `
  -ResourceType "Microsoft.Insights/components" `
  -Location "East US" `  # or North Europe, West Europe, South Central US
  -PropertyObject @{"Application_Type"="web"} `
  -Force

# Give owner access to the team

New-AzureRmRoleAssignment `
  -SignInName "myteam@fabrikam.com" `
  -RoleDefinitionName Owner `
  -Scope $resource.ResourceId 


# Display iKey
Write-Host "App Insights Name = " $resource.Name
Write-Host "IKey = " $resource.Properties.InstrumentationKey

```

## <a name="what-to-do-with-the-ikey"></a><span data-ttu-id="0ef97-116">Cosa fare con l'iKey</span><span class="sxs-lookup"><span data-stu-id="0ef97-116">What to do with the iKey</span></span>
<span data-ttu-id="0ef97-117">Per identificare le singole risorse, viene usata una chiave di strumentazione (iKey),</span><span class="sxs-lookup"><span data-stu-id="0ef97-117">Each resource is identified by its instrumentation key (iKey).</span></span> <span data-ttu-id="0ef97-118">ovvero l'output dello script di creazione della risorsa.</span><span class="sxs-lookup"><span data-stu-id="0ef97-118">The iKey is an output of the resource creation script.</span></span> <span data-ttu-id="0ef97-119">Lo script di compilazione deve fornire l'iKey all'istanza di Application Insights SDK incorporata nell'app.</span><span class="sxs-lookup"><span data-stu-id="0ef97-119">Your build script should provide the iKey to the Application Insights SDK embedded in your app.</span></span>

<span data-ttu-id="0ef97-120">È possibile fornire l'iKey all'SDK in due modi diversi:</span><span class="sxs-lookup"><span data-stu-id="0ef97-120">There are two ways to make the iKey available to the SDK:</span></span>

* <span data-ttu-id="0ef97-121">In [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md):</span><span class="sxs-lookup"><span data-stu-id="0ef97-121">In [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md):</span></span> 
  * <span data-ttu-id="0ef97-122">`<instrumentationkey>`*ikey*`</instrumentationkey>`</span><span class="sxs-lookup"><span data-stu-id="0ef97-122">`<instrumentationkey>`*ikey*`</instrumentationkey>`</span></span>
* <span data-ttu-id="0ef97-123">Oppure nel [codice di inizializzazione](app-insights-api-custom-events-metrics.md):</span><span class="sxs-lookup"><span data-stu-id="0ef97-123">Or in [initialization code](app-insights-api-custom-events-metrics.md):</span></span> 
  * <span data-ttu-id="0ef97-124">`Microsoft.ApplicationInsights.Extensibility.
    TelemetryConfiguration.Active.InstrumentationKey = "`*iKey*`";`</span><span class="sxs-lookup"><span data-stu-id="0ef97-124">`Microsoft.ApplicationInsights.Extensibility.
TelemetryConfiguration.Active.InstrumentationKey = "`*iKey*`";`</span></span>

## <a name="see-also"></a><span data-ttu-id="0ef97-125">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="0ef97-125">See also</span></span>
* [<span data-ttu-id="0ef97-126">Creare risorse Application Insights e test web da modelli</span><span class="sxs-lookup"><span data-stu-id="0ef97-126">Create Application Insights and web test resources from templates</span></span>](app-insights-powershell.md)
* [<span data-ttu-id="0ef97-127">Impostare il monitoraggio di diagnostica Azure con PowerShell</span><span class="sxs-lookup"><span data-stu-id="0ef97-127">Set up monitoring of Azure diagnostics with PowerShell</span></span>](app-insights-powershell-azure-diagnostics.md) 
* [<span data-ttu-id="0ef97-128">Impostare avvisi tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="0ef97-128">Set alerts by using PowerShell</span></span>](app-insights-powershell-alerts.md)

