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
# <a name="powershell-script-toocreate-an-application-insights-resource"></a>Script di PowerShell toocreate una risorsa di Application Insights


Quando si desidera toomonitor una nuova applicazione - o una nuova versione di un'applicazione - con [Azure Application Insights](https://azure.microsoft.com/services/application-insights/), impostare una nuova risorsa in Microsoft Azure. Questa risorsa è in cui i dati di telemetria hello dall'app vengono analizzati e visualizzati. 

È possibile automatizzare la creazione di hello di una nuova risorsa tramite PowerShell.

Se, ad esempio, si intende sviluppare un'app per dispositivi mobili, è probabile che, in un dato momento, i clienti usino diverse versioni pubblicate dell'app. Per evitare che i risultati di telemetria hello tooget da diverse versioni confuse. Per ottenere il toocreate processo di compilazione una nuova risorsa per ogni compilazione.

> [!NOTE]
> Se si desidera toocreate un set di risorse tutto hello stesso tempo, prendere in considerazione [la creazione di risorse hello utilizzando un modello di Azure](app-insights-powershell.md).
> 
> 

## <a name="script-toocreate-an-application-insights-resource"></a>Script toocreate una risorsa di Application Insights
Vedere le specifiche di cmdlet pertinenti hello:

* [New-AzureRmResource](https://msdn.microsoft.com/library/mt652510.aspx)
* [New-AzureRmRoleAssignment](https://msdn.microsoft.com/library/mt678995.aspx)

*Script di PowerShell*  

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

## <a name="what-toodo-with-hello-ikey"></a>Quali toodo con iKey hello
Per identificare le singole risorse, viene usata una chiave di strumentazione (iKey), iKey Hello è un output dello script di creazione risorsa hello. Lo script di compilazione deve fornire hello iKey toohello che Application Insights SDK incorporato nell'applicazione.

Esistono due modi toomake hello iKey disponibili toohello SDK:

* In [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md): 
  * `<instrumentationkey>`*ikey*`</instrumentationkey>`
* Oppure nel [codice di inizializzazione](app-insights-api-custom-events-metrics.md): 
  * `Microsoft.ApplicationInsights.Extensibility.
    TelemetryConfiguration.Active.InstrumentationKey = "`*iKey*`";`

## <a name="see-also"></a>Vedere anche
* [Creare risorse Application Insights e test web da modelli](app-insights-powershell.md)
* [Impostare il monitoraggio di diagnostica Azure con PowerShell](app-insights-powershell-azure-diagnostics.md) 
* [Impostare avvisi tramite PowerShell](app-insights-powershell-alerts.md)

