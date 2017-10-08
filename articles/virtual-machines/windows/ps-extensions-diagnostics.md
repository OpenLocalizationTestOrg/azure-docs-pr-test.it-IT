---
title: diagnostica di Azure PowerShell tooenable in una macchina virtuale Windows aaaUse | Documenti Microsoft
services: virtual-machines-windows
documentationcenter: 
description: Informazioni su come toouse PowerShell tooenable diagnostica Azure in una macchina virtuale che esegue Windows
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
ms.openlocfilehash: e945f0de154b5ba600f845f0d577b48e2254573b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-tooenable-azure-diagnostics-in-a-virtual-machine-running-windows"></a>Usare la diagnostica di Azure PowerShell tooenable in una macchina virtuale che esegue Windows
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

Diagnostica di Azure è possibilità hello all'interno di Azure che consente la raccolta hello dei dati di diagnostica in un'applicazione distribuita. È possibile utilizzare hello diagnostica estensione toocollect dati di diagnostica come i log applicazioni o i contatori delle prestazioni da una macchina virtuale Azure (VM) che esegue Windows. In questo articolo viene descritto come tooenable di Windows PowerShell toouse hello estensione diagnostica per una macchina virtuale. Vedere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview) per prerequisiti hello necessari per questo articolo.

## <a name="enable-hello-diagnostics-extension-if-you-use-hello-resource-manager-deployment-model"></a>Abilitare l'estensione di diagnostica hello se si utilizza il modello di distribuzione del hello Gestione risorse
È possibile abilitare l'estensione diagnostica hello durante la creazione di una macchina virtuale di Windows tramite modello di distribuzione Azure Resource Manager hello aggiungendo hello estensione configurazione toohello Gestione risorse modello. Vedere [creare una macchina virtuale Windows con monitoraggio e diagnostica usando il modello di gestione risorse di Azure hello](extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

estensione di diagnostica tooenable hello in una macchina virtuale esistente creata tramite il modello di distribuzione del hello Resource Manager, è possibile utilizzare hello [Set AzureRMVMDiagnosticsExtension](/powershell/module/azurerm.compute/set-azurermvmdiagnosticsextension) cmdlet di PowerShell come illustrato di seguito.

    $vm_resourcegroup = "myvmresourcegroup"
    $vm_name = "myvm"
    $diagnosticsconfig_path = "DiagnosticsPubConfig.xml"

    Set-AzureRmVMDiagnosticsExtension -ResourceGroupName $vm_resourcegroup -VMName $vm_name -DiagnosticsConfigurationPath $diagnosticsconfig_path


*$diagnosticsconfig_path* è hello percorso toohello contenente la configurazione della diagnostica hello in XML, come descritto nella hello [esempio](#sample-diagnostics-configuration) sotto.  

Se il file di configurazione diagnostica hello specifica un **StorageAccount** elemento con un nome di account di archiviazione, quindi hello *Set AzureRMVMDiagnosticsExtension* script imposterà automaticamente hello diagnostica estensione toosend dati di diagnostica toothat account di archiviazione. Per questo toowork, account di archiviazione di hello deve toobe in hello stessa sottoscrizione come hello macchina virtuale.

Se non **StorageAccount** è stato specificato nella configurazione di diagnostica hello, è necessario toopass in hello *StorageAccountName* parametro toohello cmdlet. Se hello *StorageAccountName* viene specificato, quindi hello cmdlet sarà sempre utilizzare account di archiviazione hello specificato nel parametro hello e hello non è specificato nel file di configurazione di diagnostica hello.

Se la diagnostica hello account di archiviazione è in una sottoscrizione diversa da hello macchina virtuale, è necessario tooexplicitly passato hello *StorageAccountName* e *StorageAccountKey* parametri toohello cmdlet. Hello *StorageAccountKey* parametro non è necessaria quando diagnostica hello account di archiviazione è in hello stessa sottoscrizione, come i cmdlet di hello automaticamente può eseguire query e impostare il valore chiave di hello quando si abilita l'estensione diagnostica hello. Tuttavia, se hello account di archiviazione di diagnostica è in una sottoscrizione diversa, quindi hello cmdlet potrebbe non essere in grado di tooget chiave di hello automaticamente e tooexplicitly necessario specificare la chiave hello tramite hello *StorageAccountKey* parametro.  

    Set-AzureRmVMDiagnosticsExtension -ResourceGroupName $vm_resourcegroup -VMName $vm_name -DiagnosticsConfigurationPath $diagnosticsconfig_path -StorageAccountName $diagnosticsstorage_name -StorageAccountKey $diagnosticsstorage_key

Una volta abilitata l'estensione diagnostica hello in una macchina virtuale, è possibile ottenere le impostazioni correnti di hello utilizzando hello [Get AzureRMVmDiagnosticsExtension](/powershell/module/azurerm.compute/get-azurermvmdiagnosticsextension) cmdlet.

    Get-AzureRmVMDiagnosticsExtension -ResourceGroupName $vm_resourcegroup -VMName $vm_name

Hello cmdlet restituisce *PublicSettings*, che contiene la configurazione di diagnostica hello. Esistono due tipi di configurazione supportata: WadCfg e xmlCfg. WadCfg è una configurazione JSON e xmlCfg è una configurazione XML in un formato con codifica Base64. tooread hello XML, è necessario toodecode è.

    $publicsettings = (Get-AzureRmVMDiagnosticsExtension -ResourceGroupName $vm_resourcegroup -VMName $vm_name).PublicSettings
    $encodedconfig = (ConvertFrom-Json -InputObject $publicsettings).xmlCfg
    $xmlconfig = [System.Text.Encoding]::UTF8.GetString([System.Convert]::FromBase64String($encodedconfig))
    Write-Host $xmlconfig

Hello [Remove AzureRMVmDiagnosticsExtension](/powershell/module/azurerm.compute/remove-azurermvmdiagnosticsextension) cmdlet può essere l'estensione di diagnostica hello tooremove utilizzati da hello macchina virtuale.  

## <a name="enable-hello-diagnostics-extension-if-you-use-hello-classic-deployment-model"></a>Abilitare l'estensione di diagnostica hello se si utilizza il modello di distribuzione classica hello
È possibile utilizzare hello [Set AzureVMDiagnosticsExtension](/powershell/module/azure/set-azurevmdiagnosticsextension) tooenable cmdlet un'estensione di diagnostica in una macchina virtuale creata tramite il modello di distribuzione classica hello. Hello seguente esempio viene illustrato come toocreate una nuova macchina virtuale tramite il modello di distribuzione classica hello con l'estensione diagnostica hello abilitato.

    $VM = New-AzureVMConfig -Name $VM -InstanceSize Small -ImageName $VMImage
    $VM = Add-AzureProvisioningConfig -VM $VM -AdminUsername $Username -Password $Password -Windows
    $VM = Set-AzureVMDiagnosticsExtension -DiagnosticsConfigurationPath $Config_Path -VM $VM -StorageContext $Storage_Context
    New-AzureVM -Location $Location -ServiceName $Service_Name -VM $VM

estensione di diagnostica tooenable hello in una macchina virtuale esistente creata tramite hello classico modello di distribuzione, hello prima di utilizzare [Get-AzureVM](/powershell/module/azure/get-azurevm) configurazione della macchina virtuale hello tooget cmdlet. Quindi aggiornare l'estensione di diagnostica hello configurazione tooinclude hello VM utilizzando hello [Set AzureVMDiagnosticsExtension](/powershell/module/azure/set-azurevmdiagnosticsextension) cmdlet. Infine, applicare hello aggiornato configurazione toohello VM utilizzando [Update-AzureVM](/powershell/module/azure/update-azurevm).

    $VM = Get-AzureVM -ServiceName $Service_Name -Name $VM_Name
    $VM_Update = Set-AzureVMDiagnosticsExtension -DiagnosticsConfigurationPath $Config_Path -VM $VM -StorageContext $Storage_Context
    Update-AzureVM -ServiceName $Service_Name -Name $VM_Name -VM $VM_Update.VM

## <a name="sample-diagnostics-configuration"></a>Configurazione di diagnostica di esempio
Hello che codice XML seguente può essere utilizzato per hello diagnostica configurazione pubblica hello sopra gli script. Questa configurazione di esempio trasferirà vari prestazioni contatori toohello diagnostica account di archiviazione, insieme agli errori da un'applicazione hello, protezione e i canali di sistema nei registri eventi di Windows hello e gli eventuali errori da diagnostica di hello log dell'infrastruttura.

configurazione di Hello deve seguenti di hello toobe tooinclude aggiornato:

* Hello *resourceID* attributo di hello **metriche** elemento deve toobe aggiornata con ID di risorsa hello per hello macchina virtuale.
  
  * Hello ID può essere creato utilizzando hello modello di risorsa: "le sottoscrizioni / {*ID per la sottoscrizione hello con hello VM*} / ResourceGroups / {*nome gruppo di risorse hello per hello VM*} / providers/Microsoft.Compute/virtualMachines/ {*hello nome della macchina virtuale*} ".
  * Ad esempio, se hello ID per sottoscrizione hello in hello macchina virtuale è in esecuzione è **11111111-1111-1111-1111-111111111111**, nome gruppo di risorse hello per il gruppo di risorse hello è **MyResourceGroup**, senza che sia hello nome della macchina virtuale **MyWindowsVM**, quindi hello valore per *resourceID* sarebbe:
    
      ```
      <Metrics resourceId="/subscriptions/11111111-1111-1111-1111-111111111111/resourceGroups/MyResourceGroup/providers/Microsoft.Compute/virtualMachines/MyWindowsVM" >
      ```
  * Per ulteriori informazioni su come le metriche sono i contatori delle prestazioni generati hello in base e la configurazione di metriche, vedere [tabella delle metriche di diagnostica di Azure nel servizio di archiviazione](extensions-diagnostics-template.md#wadmetrics-tables-in-storage).
* Hello **StorageAccount** elemento deve toobe aggiornato con il nome di hello hello diagnostica dell'account di archiviazione.
  
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
        <Metrics resourceId="(Update with resource ID for hello VM)" >
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
* Per ulteriori informazioni sull'uso di funzionalità di diagnostica Azure hello e altri problemi di tootroubleshoot tecniche, vedere [abilitazione di diagnostica in servizi Cloud di Azure e macchine virtuali](../../cloud-services/cloud-services-dotnet-diagnostics.md).
* [Schema di configurazione di diagnostica](https://msdn.microsoft.com/library/azure/mt634524.aspx) illustra diverse configurazioni XML opzioni per l'estensione diagnostica hello hello.

