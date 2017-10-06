---
title: aaaEnable diagnostica nei servizi Cloud di Azure tramite PowerShell | Documenti Microsoft
description: Informazioni su come diagnostica tooenable per cloud services utilizzando PowerShell
services: cloud-services
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: 66e08754-8639-4022-ae18-4237749ba17d
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 09/06/2016
ms.author: adegeo
ms.openlocfilehash: 7c7444df13edc8d7f5663e20ec7558d36aac45d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="enable-diagnostics-in-azure-cloud-services-using-powershell"></a>Abilitare la diagnostica nei servizi cloud di Azure con PowerShell
È possibile raccogliere dati di diagnostica come i log applicazioni, i contatori delle prestazioni e così via. da un servizio Cloud tramite hello estensione diagnostica di Azure. In questo articolo viene descritto come tooenable hello estensione diagnostica di Azure per un servizio Cloud tramite PowerShell.  Vedere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview) per prerequisiti hello necessari per questo articolo.

## <a name="enable-diagnostics-extension-as-part-of-deploying-a-cloud-service"></a>Abilitare l'estensione delle funzionalità di diagnostica come parte della distribuzione di un servizio Cloud
Questo approccio è il tipo di integrazione toocontinuous applicabile di scenari, in cui diagnostica hello estensione può essere attivata come parte della distribuzione di hello servizio cloud. Quando si crea una nuova distribuzione di servizio Cloud, è possibile abilitare l'estensione diagnostica hello passando hello *ExtensionConfiguration* parametro toohello [New-AzureDeployment](/powershell/module/azure/new-azuredeployment?view=azuresmps-3.7.0) cmdlet. Hello *ExtensionConfiguration* parametro accetta una matrice di configurazioni di diagnostica che possono essere creati utilizzando hello [New AzureServiceDiagnosticsExtensionConfig](/powershell/module/azure/new-azureservicediagnosticsextensionconfig?view=azuresmps-3.7.0) cmdlet.

Hello esempio seguente viene illustrato come è possibile abilitare la diagnostica per un servizio cloud con un WebRole e WorkerRole, ognuno dei quali con una configurazione di diagnostica diversi.

```powershell
$service_name = "MyService"
$service_package = "CloudService.cspkg"
$service_config = "ServiceConfiguration.Cloud.cscfg"
$webrole_diagconfigpath = "MyService.WebRole.PubConfig.xml"
$workerrole_diagconfigpath = "MyService.WorkerRole.PubConfig.xml"

$webrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WebRole" -DiagnosticsConfigurationPath $webrole_diagconfigpath
$workerrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WorkerRole" -DiagnosticsConfigurationPath $workerrole_diagconfigpath

New-AzureDeployment -ServiceName $service_name -Slot Production -Package $service_package -Configuration $service_config -ExtensionConfiguration @($webrole_diagconfig,$workerrole_diagconfig)
```

Se il file di configurazione diagnostica hello specifica un `StorageAccount` elemento con un nome di account di archiviazione, quindi hello `New-AzureServiceDiagnosticsExtensionConfig` cmdlet utilizzeranno automaticamente l'account di archiviazione. Per questo toowork, account di archiviazione di hello deve toobe in hello stessa sottoscrizione come hello servizio Cloud distribuito.

Da pubblicano file di configurazione di estensione hello successivo generati da MSBuild hello Azure SDK 2.6 output di destinazione includono il nome account di archiviazione hello in base alla stringa di configurazione di diagnostica hello specificato nel file di configurazione del servizio hello (. cscfg). script Hello riportato di seguito viene illustrato come file di configurazione delle estensioni di tooparse hello da hello l'output di destinazione di pubblicazione e configurare l'estensione diagnostica per ogni ruolo durante la distribuzione di servizio cloud hello.

```powershell
$service_name = "MyService"
$service_package = "C:\build\output\CloudService.cspkg"
$service_config = "C:\build\output\ServiceConfiguration.Cloud.cscfg"

#Find hello Extensions path based on service configuration file
$extensionsSearchPath = Join-Path -Path (Split-Path -Parent $service_config) -ChildPath "Extensions"

$diagnosticsExtensions = Get-ChildItem -Path $extensionsSearchPath -Filter "PaaSDiagnostics.*.PubConfig.xml"
$diagnosticsConfigurations = @()
foreach ($extPath in $diagnosticsExtensions)
{
    #Find hello RoleName based on file naming convention PaaSDiagnostics.<RoleName>.PubConfig.xml
    $roleName = ""
    $roles = $extPath -split ".",0,"simplematch"
    if ($roles -is [system.array] -and $roles.Length -gt 1)
    {
        $roleName = $roles[1]
        $x = 2
        while ($x -le $roles.Length)
            {
               if ($roles[$x] -ne "PubConfig")
                {
                    $roleName = $roleName + "." + $roles[$x]
                }
                else
                {
                    break
                }
                $x++
            }
        $fullExtPath = Join-Path -path $extensionsSearchPath -ChildPath $extPath
        $diagnosticsconfig = New-AzureServiceDiagnosticsExtensionConfig -Role $roleName -DiagnosticsConfigurationPath $fullExtPath
        $diagnosticsConfigurations += $diagnosticsconfig
    }
}
New-AzureDeployment -ServiceName $service_name -Slot Production -Package $service_package -Configuration $service_config -ExtensionConfiguration $diagnosticsConfigurations
```

Visual Studio Online viene utilizzato un approccio simile per le distribuzioni automatiche dei servizi Cloud con l'estensione diagnostica hello. Per un esempio completo, vedere [Publish-AzureCloudDeployment.ps1](https://github.com/Microsoft/vso-agent-tasks/blob/master/Tasks/AzureCloudPowerShellDeployment/Publish-AzureCloudDeployment.ps1) .

Se non `StorageAccount` è stato specificato nella configurazione di diagnostica hello, è necessario toopass in hello *StorageAccountName* parametro toohello cmdlet. Se hello *StorageAccountName* viene specificato, quindi hello cmdlet sarà sempre utilizzare account di archiviazione hello specificato nel parametro hello e hello non è specificato nel file di configurazione di diagnostica hello.

Se la diagnostica hello account di archiviazione è in una sottoscrizione diversa da hello servizio Cloud, è necessario tooexplicitly passato hello *StorageAccountName* e *StorageAccountKey* parametri cmdlet toohello. Hello *StorageAccountKey* parametro non è necessaria quando diagnostica hello account di archiviazione è in hello stessa sottoscrizione, come i cmdlet di hello automaticamente può eseguire query e impostare il valore chiave di hello quando si abilita l'estensione diagnostica hello. Tuttavia, se hello account di archiviazione di diagnostica è in una sottoscrizione diversa, quindi hello cmdlet potrebbe non essere in grado di tooget chiave di hello automaticamente e tooexplicitly necessario specificare la chiave hello tramite hello *StorageAccountKey* parametro.

```powershell
$webrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WebRole" -DiagnosticsConfigurationPath $webrole_diagconfigpath -StorageAccountName $diagnosticsstorage_name -StorageAccountKey $diagnosticsstorage_key
$workerrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WorkerRole" -DiagnosticsConfigurationPath $workerrole_diagconfigpath -StorageAccountName $diagnosticsstorage_name -StorageAccountKey $diagnosticsstorage_key
```

## <a name="enable-diagnostics-extension-on-an-existing-cloud-service"></a>Abilitare l'estensione della diagnostica in un servizio Cloud esistente
È possibile utilizzare hello [Set AzureServiceDiagnosticsExtension](/powershell/module/azure/set-azureservicediagnosticsextension?view=azuresmps-3.7.0) cmdlet tooenable o aggiornamento configurazione della diagnostica in un servizio Cloud che è già in esecuzione.

[!INCLUDE [cloud-services-wad-warning](../../includes/cloud-services-wad-warning.md)]

```powershell
$service_name = "MyService"
$webrole_diagconfigpath = "MyService.WebRole.PubConfig.xml"
$workerrole_diagconfigpath = "MyService.WorkerRole.PubConfig.xml"

$webrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WebRole" -DiagnosticsConfigurationPath $webrole_diagconfigpath
$workerrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WorkerRole" -DiagnosticsConfigurationPath $workerrole_diagconfigpath

Set-AzureServiceDiagnosticsExtension -DiagnosticsConfiguration @($webrole_diagconfig,$workerrole_diagconfig) -ServiceName $service_name
```

## <a name="get-current-diagnostics-extension-configuration"></a>Ottenere la configurazione di estensione della diagnostica corrente
Hello utilizzare [Get AzureServiceDiagnosticsExtension](/powershell/module/azure/get-azureservicediagnosticsextension?view=azuresmps-3.7.0) cmdlet tooget hello configurazione di diagnostica corrente per un servizio cloud.

```powershell
Get-AzureServiceDiagnosticsExtension -ServiceName "MyService"
```

## <a name="remove-diagnostics-extension"></a>Rimuovere l'estensione della diagnostica
tooturn disattivata diagnostica in un cloud service è possibile utilizzare hello [Remove AzureServiceDiagnosticsExtension](/powershell/module/azure/remove-azureservicediagnosticsextension?view=azuresmps-3.7.0) cmdlet.

```powershell
Remove-AzureServiceDiagnosticsExtension -ServiceName "MyService"
```

Se è abilitata l'estensione di diagnostica hello utilizzando *Set AzureServiceDiagnosticsExtension* o hello *New AzureServiceDiagnosticsExtensionConfig* senza hello *ruolo* parametro, è possibile rimuovere l'estensione hello usando *Remove AzureServiceDiagnosticsExtension* senza hello *ruolo* parametro. Se hello *ruolo* parametro utilizzato durante l'abilitazione di estensione hello, quindi deve essere utilizzato anche quando si rimuove l'estensione hello.

estensione di diagnostica hello tooremove da ogni singolo ruolo:

```powershell
Remove-AzureServiceDiagnosticsExtension -ServiceName "MyService" -Role "WebRole"
```

## <a name="next-steps"></a>Passaggi successivi
* Per ulteriori informazioni sull'uso di diagnostica di Azure e altri problemi di tootroubleshoot tecniche, vedere [abilitazione di diagnostica in servizi Cloud di Azure e macchine virtuali](cloud-services-dotnet-diagnostics.md).
* Hello [dello Schema di configurazione di diagnostica](https://msdn.microsoft.com/library/azure/dn782207.aspx) illustra diverse configurazioni xml opzioni per l'estensione diagnostica hello hello.
* estensione di diagnostica tooenable hello per le macchine virtuali, vedere toolearn [creare una macchina virtuale Windows con monitoraggio e diagnostica usando il modello di gestione risorse di Azure](../virtual-machines/windows/extensions-diagnostics-template.md)
