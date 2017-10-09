---
title: aaaUsing PowerShell toosetup Application Insights in un Azure | Documenti Microsoft
description: Automatizzare la configurazione diagnostica Azure toopipe tooApplication Insights.
services: application-insights
documentationcenter: .net
author: sbtron
manager: carmonm
ms.assetid: 4ac803a8-f424-4c0c-b18f-4b9c189a64a5
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 11/17/2015
ms.author: bwren
ms.openlocfilehash: c48a5d8eb23df162522860935af876063aaa6976
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="using-powershell-tooset-up-application-insights-for-an-azure-web-app"></a><span data-ttu-id="e843f-103">Utilizzo di PowerShell tooset di Application Insights per un'app web di Azure</span><span class="sxs-lookup"><span data-stu-id="e843f-103">Using PowerShell tooset up Application Insights for an Azure web app</span></span>
<span data-ttu-id="e843f-104">[Microsoft Azure](https://azure.com) può essere [configurata la diagnostica di Azure toosend](app-insights-azure-diagnostics.md) troppo[Azure Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e843f-104">[Microsoft Azure](https://azure.com) can be [configured toosend Azure Diagnostics](app-insights-azure-diagnostics.md) too[Azure Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="e843f-105">diagnostica Hello correlare tooAzure servizi di Cloud e macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="e843f-105">hello diagnostics relate tooAzure Cloud Services and Azure VMs.</span></span> <span data-ttu-id="e843f-106">Complementari telemetria hello inviato dall'App hello utilizzando hello Application Insights SDK.</span><span class="sxs-lookup"><span data-stu-id="e843f-106">They complement hello telemetry that you send from within hello app using hello Application Insights SDK.</span></span> <span data-ttu-id="e843f-107">Come parte di automatizzare il processo di hello di creazione di nuove risorse in Azure, è possibile configurare diagnostica tramite PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e843f-107">As part of automating hello process of creating new resources in Azure, you can configure diagnostics using PowerShell.</span></span>

## <a name="azure-template"></a><span data-ttu-id="e843f-108">Modello di Azure</span><span class="sxs-lookup"><span data-stu-id="e843f-108">Azure template</span></span>
<span data-ttu-id="e843f-109">Se è hello web app in Azure e creare le risorse utilizzando un modello di gestione risorse di Azure, è possibile configurare Application Insights mediante l'aggiunta di questo nodo risorse toohello:</span><span class="sxs-lookup"><span data-stu-id="e843f-109">If hello web app is in Azure and you create your resources using an Azure Resource Manager template, you can configure Application Insights by adding this toohello resources node:</span></span>

    {
      resources: [
        /* Create Application Insights resource */
        {
          "apiVersion": "2015-05-01",
          "type": "microsoft.insights/components",
          "name": "nameOfAIAppResource",
          "location": "centralus",
          "kind": "web",
          "properties": { "ApplicationId": "nameOfAIAppResource" },
          "dependsOn": [
            "[concat('Microsoft.Web/sites/', myWebAppName)]"
          ]
        }
       ]
     } 

* <span data-ttu-id="e843f-110">`nameOfAIAppResource`-un nome per hello risorsa di Application Insights</span><span class="sxs-lookup"><span data-stu-id="e843f-110">`nameOfAIAppResource` - a name for hello Application Insights resource</span></span>
* <span data-ttu-id="e843f-111">`myWebAppName`-id hello dell'app web hello</span><span class="sxs-lookup"><span data-stu-id="e843f-111">`myWebAppName` - hello id of hello web app</span></span>

## <a name="enable-diagnostics-extension-as-part-of-deploying-a-cloud-service"></a><span data-ttu-id="e843f-112">Abilitare l'estensione delle funzionalità di diagnostica come parte della distribuzione di un servizio Cloud</span><span class="sxs-lookup"><span data-stu-id="e843f-112">Enable diagnostics extension as part of deploying a Cloud Service</span></span>
<span data-ttu-id="e843f-113">Hello `New-AzureDeployment` cmdlet ha un parametro `ExtensionConfiguration`, che accetta una matrice di configurazioni di diagnostica.</span><span class="sxs-lookup"><span data-stu-id="e843f-113">hello `New-AzureDeployment` cmdlet has a parameter `ExtensionConfiguration`, which takes an array of diagnostics configurations.</span></span> <span data-ttu-id="e843f-114">È possibile crearli utilizzando hello `New-AzureServiceDiagnosticsExtensionConfig` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="e843f-114">These can be created using hello `New-AzureServiceDiagnosticsExtensionConfig` cmdlet.</span></span> <span data-ttu-id="e843f-115">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="e843f-115">For example:</span></span>

```ps

    $service_package = "CloudService.cspkg"
    $service_config = "ServiceConfiguration.Cloud.cscfg"
    $diagnostics_storagename = "myservicediagnostics"
    $webrole_diagconfigpath = "MyService.WebRole.PubConfig.xml" 
    $workerrole_diagconfigpath = "MyService.WorkerRole.PubConfig.xml"

    $primary_storagekey = (Get-AzureStorageKey `
     -StorageAccountName "$diagnostics_storagename").Primary
    $storage_context = New-AzureStorageContext `
       -StorageAccountName $diagnostics_storagename `
       -StorageAccountKey $primary_storagekey

    $webrole_diagconfig = `
     New-AzureServiceDiagnosticsExtensionConfig `
      -Role "WebRole" -Storage_context $storageContext `
      -DiagnosticsConfigurationPath $webrole_diagconfigpath
    $workerrole_diagconfig = `
     New-AzureServiceDiagnosticsExtensionConfig `
      -Role "WorkerRole" `
      -StorageContext $storage_context `
      -DiagnosticsConfigurationPath $workerrole_diagconfigpath

    New-AzureDeployment `
      -ServiceName $service_name `
      -Slot Production `
      -Package $service_package `
      -Configuration $service_config `
      -ExtensionConfiguration @($webrole_diagconfig,$workerrole_diagconfig)

``` 

## <a name="enable-diagnostics-extension-on-an-existing-cloud-service"></a><span data-ttu-id="e843f-116">Abilitare l'estensione della diagnostica in un servizio Cloud esistente</span><span class="sxs-lookup"><span data-stu-id="e843f-116">Enable diagnostics extension on an existing Cloud Service</span></span>
<span data-ttu-id="e843f-117">In un servizio esistente, usare `Set-AzureServiceDiagnosticsExtension`.</span><span class="sxs-lookup"><span data-stu-id="e843f-117">On an existing service, use `Set-AzureServiceDiagnosticsExtension`.</span></span>

```ps

    $service_name = "MyService"
    $diagnostics_storagename = "myservicediagnostics"
    $webrole_diagconfigpath = "MyService.WebRole.PubConfig.xml" 
    $workerrole_diagconfigpath = "MyService.WorkerRole.PubConfig.xml"
    $primary_storagekey = (Get-AzureStorageKey `
         -StorageAccountName "$diagnostics_storagename").Primary
    $storage_context = New-AzureStorageContext `
        -StorageAccountName $diagnostics_storagename `
        -StorageAccountKey $primary_storagekey

    Set-AzureServiceDiagnosticsExtension `
        -StorageContext $storage_context `
        -DiagnosticsConfigurationPath $webrole_diagconfigpath `
        -ServiceName $service_name `
        -Slot Production `
        -Role "WebRole" 
    Set-AzureServiceDiagnosticsExtension `
        -StorageContext $storage_context `
        -DiagnosticsConfigurationPath $workerrole_diagconfigpath `
        -ServiceName $service_name `
        -Slot Production `
        -Role "WorkerRole"
```

## <a name="get-current-diagnostics-extension-configuration"></a><span data-ttu-id="e843f-118">Ottenere la configurazione di estensione della diagnostica corrente</span><span class="sxs-lookup"><span data-stu-id="e843f-118">Get current diagnostics extension configuration</span></span>
```ps

    Get-AzureServiceDiagnosticsExtension -ServiceName "MyService"
```


## <a name="remove-diagnostics-extension"></a><span data-ttu-id="e843f-119">Rimuovere l'estensione della diagnostica</span><span class="sxs-lookup"><span data-stu-id="e843f-119">Remove diagnostics extension</span></span>
```ps

    Remove-AzureServiceDiagnosticsExtension -ServiceName "MyService"
```

<span data-ttu-id="e843f-120">Se è abilitata l'estensione di diagnostica hello utilizzando `Set-AzureServiceDiagnosticsExtension` o `New-AzureServiceDiagnosticsExtensionConfig` senza il parametro di ruolo hello, quindi è possibile rimuovere hello estensione utilizzando `Remove-AzureServiceDiagnosticsExtension` senza il parametro Role hello.</span><span class="sxs-lookup"><span data-stu-id="e843f-120">If you enabled hello diagnostics extension using either `Set-AzureServiceDiagnosticsExtension` or `New-AzureServiceDiagnosticsExtensionConfig` without hello Role parameter, then you can remove hello extension using `Remove-AzureServiceDiagnosticsExtension` without hello Role parameter.</span></span> <span data-ttu-id="e843f-121">Se è stato utilizzato il parametro Role hello quando si abilita estensione hello quindi deve inoltre essere utilizzata durante la rimozione di estensione hello.</span><span class="sxs-lookup"><span data-stu-id="e843f-121">If hello Role parameter was used when enabling hello extension then it must also be used when removing hello extension.</span></span>

<span data-ttu-id="e843f-122">estensione di diagnostica hello tooremove da ogni singolo ruolo:</span><span class="sxs-lookup"><span data-stu-id="e843f-122">tooremove hello diagnostics extension from each individual role:</span></span>

```ps

    Remove-AzureServiceDiagnosticsExtension -ServiceName "MyService" -Role "WebRole"
```


## <a name="see-also"></a><span data-ttu-id="e843f-123">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="e843f-123">See also</span></span>
* [<span data-ttu-id="e843f-124">Monitorare le app dei Servizi cloud di Azure con Application Insights</span><span class="sxs-lookup"><span data-stu-id="e843f-124">Monitor Azure Cloud Services apps with Application Insights</span></span>](app-insights-cloudservices.md)
* [<span data-ttu-id="e843f-125">Inviare informazioni di diagnostica Azure tooApplication</span><span class="sxs-lookup"><span data-stu-id="e843f-125">Send Azure Diagnostics tooApplication Insights</span></span>](app-insights-azure-diagnostics.md)
* [<span data-ttu-id="e843f-126">Automatizzare la configurazione degli avvisi</span><span class="sxs-lookup"><span data-stu-id="e843f-126">Automate configuring alerts</span></span>](app-insights-powershell-alerts.md)

