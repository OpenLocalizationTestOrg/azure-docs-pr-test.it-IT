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
# <a name="using-powershell-tooset-up-application-insights-for-an-azure-web-app"></a>Utilizzo di PowerShell tooset di Application Insights per un'app web di Azure
[Microsoft Azure](https://azure.com) può essere [configurata la diagnostica di Azure toosend](app-insights-azure-diagnostics.md) troppo[Azure Application Insights](app-insights-overview.md). diagnostica Hello correlare tooAzure servizi di Cloud e macchine virtuali di Azure. Complementari telemetria hello inviato dall'App hello utilizzando hello Application Insights SDK. Come parte di automatizzare il processo di hello di creazione di nuove risorse in Azure, è possibile configurare diagnostica tramite PowerShell.

## <a name="azure-template"></a>Modello di Azure
Se è hello web app in Azure e creare le risorse utilizzando un modello di gestione risorse di Azure, è possibile configurare Application Insights mediante l'aggiunta di questo nodo risorse toohello:

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

* `nameOfAIAppResource`-un nome per hello risorsa di Application Insights
* `myWebAppName`-id hello dell'app web hello

## <a name="enable-diagnostics-extension-as-part-of-deploying-a-cloud-service"></a>Abilitare l'estensione delle funzionalità di diagnostica come parte della distribuzione di un servizio Cloud
Hello `New-AzureDeployment` cmdlet ha un parametro `ExtensionConfiguration`, che accetta una matrice di configurazioni di diagnostica. È possibile crearli utilizzando hello `New-AzureServiceDiagnosticsExtensionConfig` cmdlet. ad esempio:

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

## <a name="enable-diagnostics-extension-on-an-existing-cloud-service"></a>Abilitare l'estensione della diagnostica in un servizio Cloud esistente
In un servizio esistente, usare `Set-AzureServiceDiagnosticsExtension`.

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

## <a name="get-current-diagnostics-extension-configuration"></a>Ottenere la configurazione di estensione della diagnostica corrente
```ps

    Get-AzureServiceDiagnosticsExtension -ServiceName "MyService"
```


## <a name="remove-diagnostics-extension"></a>Rimuovere l'estensione della diagnostica
```ps

    Remove-AzureServiceDiagnosticsExtension -ServiceName "MyService"
```

Se è abilitata l'estensione di diagnostica hello utilizzando `Set-AzureServiceDiagnosticsExtension` o `New-AzureServiceDiagnosticsExtensionConfig` senza il parametro di ruolo hello, quindi è possibile rimuovere hello estensione utilizzando `Remove-AzureServiceDiagnosticsExtension` senza il parametro Role hello. Se è stato utilizzato il parametro Role hello quando si abilita estensione hello quindi deve inoltre essere utilizzata durante la rimozione di estensione hello.

estensione di diagnostica hello tooremove da ogni singolo ruolo:

```ps

    Remove-AzureServiceDiagnosticsExtension -ServiceName "MyService" -Role "WebRole"
```


## <a name="see-also"></a>Vedere anche
* [Monitorare le app dei Servizi cloud di Azure con Application Insights](app-insights-cloudservices.md)
* [Inviare informazioni di diagnostica Azure tooApplication](app-insights-azure-diagnostics.md)
* [Automatizzare la configurazione degli avvisi](app-insights-powershell-alerts.md)

