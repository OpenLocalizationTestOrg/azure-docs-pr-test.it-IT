---
title: Usare Azure PowerShell per abilitare la diagnostica in una macchina virtuale Windows | Microsoft Docs
services: virtual-machines-windows
documentationcenter: 
description: Informazioni su come usare PowerShell per abilitare Diagnostica di Azure in una macchina virtuale che esegue Windows
author: sbtron
manager: timlt
editor: 
ms.assetid: 2e6d88f2-1980-4a24-827e-a81616a0d247
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 12/15/2015
ms.author: saurabh
ms.openlocfilehash: d0be4a712657edfc516c5f32e66519f5d9486728
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="use-powershell-to-enable-azure-diagnostics-in-a-virtual-machine-running-windows"></a>Usare PowerShell per abilitare la Diagnostica di Azure in una macchina virtuale che esegue Windows
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

Diagnostica di Azure è la funzionalità all'interno di Azure che consente la raccolta di dati di diagnostica in un'applicazione distribuita. È possibile usare l'estensione di diagnostica per raccogliere dati di diagnostica come i log dell'applicazione o i contatori delle prestazioni da una macchina virtuale Azure (VM) che esegue Windows. Questo articolo illustra come usare Windows PowerShell per abilitare l'estensione di diagnostica per una VM. Per i prerequisiti necessari per questo articolo, vedere [Come installare e configurare Azure PowerShell](/powershell/azure/overview) .

## <a name="enable-the-diagnostics-extension-if-you-use-the-resource-manager-deployment-model"></a>Abilitare l'estensione di diagnostica se si usa il modello di distribuzione di Gestione risorse
È possibile abilitare l'estensione di diagnostica durante la creazione di una VM Windows con il modello di distribuzione di Gestione risorse di Azure aggiungendo la configurazione dell'estensione al modello di Gestione risorse. Vedere [Creare una macchina virtuale Windows con monitoraggio e diagnostica mediante il modello di Azure Resource Manager](extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Per abilitare l'estensione di diagnostica in una VM esistente creata mediante il modello di distribuzione di Resource Manager, è possibile usare il cmdlet di PowerShell [Set-AzureRMVMDiagnosticsExtension](/powershell/module/azurerm.compute/set-azurermvmdiagnosticsextension) come illustrato di seguito.

    $vm_resourcegroup = "myvmresourcegroup"
    $vm_name = "myvm"
    $diagnosticsconfig_path = "DiagnosticsPubConfig.xml"

    Set-AzureRmVMDiagnosticsExtension -ResourceGroupName $vm_resourcegroup -VMName $vm_name -DiagnosticsConfigurationPath $diagnosticsconfig_path


*$diagnosticsconfig_path* è il percorso del file contenente la configurazione di diagnostica in formato XML, come descritto nell'[esempio](#sample-diagnostics-configuration) riportato di seguito.  

Se il file di configurazione di diagnostica specifica un elemento **StorageAccount** con il nome di un account di archiviazione, lo script *Set-AzureRMVMDiagnosticsExtension* imposta automaticamente l'estensione di diagnostica per l'invio dei dati di diagnostica all'account di archiviazione specificato. A tal fine, l'account di archiviazione deve trovarsi nella stessa sottoscrizione della VM.

Se nella configurazione di diagnostica non è specificato alcun elemento **StorageAccount** , è necessario passare il parametro *StorageAccountName* al cmdlet. Se il parametro *StorageAccountName* è specificato, il cmdlet userà sempre l'account di archiviazione specificato nel parametro e non quello specificato nel file di configurazione della diagnostica.

Se l'account di archiviazione di diagnostica si trova in una sottoscrizione diversa da quella della VM, è necessario passare in modo esplicito i parametri *StorageAccountName* e *StorageAccountKey* al cmdlet. Il parametro *StorageAccountKey* non è necessario quando l'account di archiviazione di diagnostica si trova nella stessa sottoscrizione perché il cmdlet può automaticamente eseguire una query e impostare il valore della chiave durante l'abilitazione dell'estensione di diagnostica. Tuttavia, se l'account di archiviazione di diagnostica si trova in una sottoscrizione diversa, il cmdlet potrebbe non essere in grado di ottenere automaticamente la chiave, quindi si deve specificare la chiave in modo esplicito tramite il parametro *StorageAccountKey* .  

    Set-AzureRmVMDiagnosticsExtension -ResourceGroupName $vm_resourcegroup -VMName $vm_name -DiagnosticsConfigurationPath $diagnosticsconfig_path -StorageAccountName $diagnosticsstorage_name -StorageAccountKey $diagnosticsstorage_key

Dopo aver abilitato l'estensione di diagnostica in una VM, è possibile ottenere le impostazioni correnti mediante il cmdlet [Get-AzureRMVmDiagnosticsExtension](/powershell/module/azurerm.compute/get-azurermvmdiagnosticsextension) .

    Get-AzureRmVMDiagnosticsExtension -ResourceGroupName $vm_resourcegroup -VMName $vm_name

Il cmdlet restituisce *PublicSettings*, contenente la configurazione di diagnostica. Esistono due tipi di configurazione supportata: WadCfg e xmlCfg. WadCfg è una configurazione JSON e xmlCfg è una configurazione XML in un formato con codifica Base64. Per leggere la configurazione XML è necessario decodificarla.

    $publicsettings = (Get-AzureRmVMDiagnosticsExtension -ResourceGroupName $vm_resourcegroup -VMName $vm_name).PublicSettings
    $encodedconfig = (ConvertFrom-Json -InputObject $publicsettings).xmlCfg
    $xmlconfig = [System.Text.Encoding]::UTF8.GetString([System.Convert]::FromBase64String($encodedconfig))
    Write-Host $xmlconfig

Il cmdlet [Remove AzureRMVmDiagnosticsExtension](/powershell/module/azurerm.compute/remove-azurermvmdiagnosticsextension) può essere usato per rimuovere l'estensione di diagnostica dalla macchina virtuale.  

## <a name="enable-the-diagnostics-extension-if-you-use-the-classic-deployment-model"></a>Abilitare l'estensione di diagnostica se si usa il modello di distribuzione classico
È possibile usare il cmdlet [Set-AzureVMDiagnosticsExtension](/powershell/module/azure/set-azurevmdiagnosticsextension) per abilitare un'estensione di diagnostica in una VM creata tramite il modello di distribuzione classica. L'esempio seguente illustra come creare una nuova VM tramite il modello di distribuzione classico con l'estensione di diagnostica abilitata.

    $VM = New-AzureVMConfig -Name $VM -InstanceSize Small -ImageName $VMImage
    $VM = Add-AzureProvisioningConfig -VM $VM -AdminUsername $Username -Password $Password -Windows
    $VM = Set-AzureVMDiagnosticsExtension -DiagnosticsConfigurationPath $Config_Path -VM $VM -StorageContext $Storage_Context
    New-AzureVM -Location $Location -ServiceName $Service_Name -VM $VM

Per abilitare l'estensione di diagnostica su una VM esistente creata tramite il modello di distribuzione classica, usare prima il cmdlet [Get-AzureVM](/powershell/module/azure/get-azurevm) per ottenere la configurazione della VM. Aggiornare quindi la configurazione della VM per includere l'estensione di diagnostica tramite il cmdlet [Set-AzureVMDiagnosticsExtension](/powershell/module/azure/set-azurevmdiagnosticsextension) . Infine applicare la configurazione aggiornata alla VM tramite [Update-AzureVM](/powershell/module/azure/update-azurevm).

    $VM = Get-AzureVM -ServiceName $Service_Name -Name $VM_Name
    $VM_Update = Set-AzureVMDiagnosticsExtension -DiagnosticsConfigurationPath $Config_Path -VM $VM -StorageContext $Storage_Context
    Update-AzureVM -ServiceName $Service_Name -Name $VM_Name -VM $VM_Update.VM

## <a name="sample-diagnostics-configuration"></a>Configurazione di diagnostica di esempio
Per la configurazione pubblica di diagnostica con gli script precedenti, è possibile usare il codice XML seguente. Questa configurazione di esempio trasferirà diversi contatori delle prestazioni all'account di archiviazione di diagnostica insieme agli errori dai canali Application, Security e System nei registri eventi di Windows e a eventuali errori dai registri dell'infrastruttura di diagnostica.

La configurazione deve essere aggiornata per includere gli elementi seguenti:

* L'attributo *resourceID* dell'elemento **Metrics** deve essere aggiornato con l'ID risorsa per la VM.
  
  * L'ID risorsa può essere creato usando il modello seguente: "/subscriptions/{*ID della sottoscrizione con la VM*}/resourceGroups/{*Nome del gruppo di risorse per la VM*}/providers/Microsoft.Compute/virtualMachines/{*Nome della VM*}".
  * Ad esempio, se l'ID della sottoscrizione in cui è in esecuzione la VM è **11111111-1111-1111-1111-111111111111**, il nome del gruppo di risorse è **MyResourceGroup** e il nome della VM è **MyWindowsVM**, allora il valore per *resourceID* sarà:
    
      ```
      <Metrics resourceId="/subscriptions/11111111-1111-1111-1111-111111111111/resourceGroups/MyResourceGroup/providers/Microsoft.Compute/virtualMachines/MyWindowsVM" >
      ```
  * Per altre informazioni sulla generazione delle metriche in base alla configurazione dei contatori delle prestazioni e delle metriche, vedere [Tabella delle metriche di Diagnostica di Azure nell'archiviazione](extensions-diagnostics-template.md#wadmetrics-tables-in-storage).
* L'elemento **StorageAccount** deve essere aggiornato con il nome dell'account di archiviazione di diagnostica.
  
    ```
    <?xml version="1.0" encoding="utf-8"?>
    <PublicConfig xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">
        <WadCfg>
          <DiagnosticMonitorConfiguration overallQuotaInMB="4096">
            <DiagnosticInfrastructureLogs scheduledTransferLogLevelFilter="Error"/>
            <PerformanceCounters scheduledTransferPeriod="PT1M">
          <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT15S" unit="Percent">
            <annotation displayName="CPU utilization" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Privileged Time" sampleRate="PT15S" unit="Percent">
            <annotation displayName="CPU privileged time" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% User Time" sampleRate="PT15S" unit="Percent">
            <annotation displayName="CPU user time" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Processor Information(_Total)\Processor Frequency" sampleRate="PT15S" unit="Count">
            <annotation displayName="CPU frequency" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\System\Processes" sampleRate="PT15S" unit="Count">
            <annotation displayName="Processes" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Process(_Total)\Thread Count" sampleRate="PT15S" unit="Count">
            <annotation displayName="Threads" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Process(_Total)\Handle Count" sampleRate="PT15S" unit="Count">
            <annotation displayName="Handles" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Memory\% Committed Bytes In Use" sampleRate="PT15S" unit="Percent">
            <annotation displayName="Memory usage" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Memory\Available Bytes" sampleRate="PT15S" unit="Bytes">
            <annotation displayName="Memory available" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Memory\Committed Bytes" sampleRate="PT15S" unit="Bytes">
            <annotation displayName="Memory committed" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Memory\Commit Limit" sampleRate="PT15S" unit="Bytes">
            <annotation displayName="Memory commit limit" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Memory\Pool Paged Bytes" sampleRate="PT15S" unit="Bytes">
            <annotation displayName="Memory paged pool" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Memory\Pool Nonpaged Bytes" sampleRate="PT15S" unit="Bytes">
            <annotation displayName="Memory non-paged pool" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\% Disk Time" sampleRate="PT15S" unit="Percent">
            <annotation displayName="Disk active time" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\% Disk Read Time" sampleRate="PT15S" unit="Percent">
            <annotation displayName="Disk active read time" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\% Disk Write Time" sampleRate="PT15S" unit="Percent">
            <annotation displayName="Disk active write time" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\Disk Transfers/sec" sampleRate="PT15S" unit="CountPerSecond">
            <annotation displayName="Disk operations" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\Disk Reads/sec" sampleRate="PT15S" unit="CountPerSecond">
            <annotation displayName="Disk read operations" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\Disk Writes/sec" sampleRate="PT15S" unit="CountPerSecond">
            <annotation displayName="Disk write operations" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\Disk Bytes/sec" sampleRate="PT15S" unit="BytesPerSecond">
            <annotation displayName="Disk speed" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\Disk Read Bytes/sec" sampleRate="PT15S" unit="BytesPerSecond">
            <annotation displayName="Disk read speed" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\Disk Write Bytes/sec" sampleRate="PT15S" unit="BytesPerSecond">
            <annotation displayName="Disk write speed" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\Avg. Disk Queue Length" sampleRate="PT15S" unit="Count">
            <annotation displayName="Disk average queue length" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\Avg. Disk Read Queue Length" sampleRate="PT15S" unit="Count">
            <annotation displayName="Disk average read queue length" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\Avg. Disk Write Queue Length" sampleRate="PT15S" unit="Count">
            <annotation displayName="Disk average write queue length" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\LogicalDisk(_Total)\% Free Space" sampleRate="PT15S" unit="Percent">
            <annotation displayName="Disk free space (percentage)" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\LogicalDisk(_Total)\Free Megabytes" sampleRate="PT15S" unit="Count">
            <annotation displayName="Disk free space (MB)" locale="en-us"/>
          </PerformanceCounterConfiguration>
        </PerformanceCounters>
        <Metrics resourceId="(Update with resource ID for the VM)" >
            <MetricAggregation scheduledTransferPeriod="PT1H"/>
            <MetricAggregation scheduledTransferPeriod="PT1M"/>
        </Metrics>
        <WindowsEventLog scheduledTransferPeriod="PT1M">
          <DataSource name="Application!*[System[(Level = 1 or Level = 2)]]"/>
          <DataSource name="Security!*[System[(Level = 1 or Level = 2)]"/>
          <DataSource name="System!*[System[(Level = 1 or Level = 2)]]"/>
        </WindowsEventLog>
          </DiagnosticMonitorConfiguration>
        </WadCfg>
        <StorageAccount>(Update with diagnostics storage account name)</StorageAccount>
    </PublicConfig>
    ```

## <a name="next-steps"></a>Passaggi successivi
* Per altre indicazioni sull'uso della funzionalità Diagnostica di Azure e altre tecniche per la risoluzione dei problemi, vedere [Abilitazione di Diagnostica in Servizi cloud e nelle macchine virtuali di Azure](../../cloud-services/cloud-services-dotnet-diagnostics.md).
* [schema di configurazioni di diagnostica](https://msdn.microsoft.com/library/azure/mt634524.aspx) illustra le varie opzioni di configurazione XML per l'estensione di diagnostica.

