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
# <a name="use-powershell-to-enable-azure-diagnostics-in-a-virtual-machine-running-windows"></a><span data-ttu-id="0c751-103">Usare PowerShell per abilitare la Diagnostica di Azure in una macchina virtuale che esegue Windows</span><span class="sxs-lookup"><span data-stu-id="0c751-103">Use PowerShell to enable Azure Diagnostics in a virtual machine running Windows</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="0c751-104">Diagnostica di Azure è la funzionalità all'interno di Azure che consente la raccolta di dati di diagnostica in un'applicazione distribuita.</span><span class="sxs-lookup"><span data-stu-id="0c751-104">Azure Diagnostics is the capability within Azure that enables the collection of diagnostic data on a deployed application.</span></span> <span data-ttu-id="0c751-105">È possibile usare l'estensione di diagnostica per raccogliere dati di diagnostica come i log dell'applicazione o i contatori delle prestazioni da una macchina virtuale Azure (VM) che esegue Windows.</span><span class="sxs-lookup"><span data-stu-id="0c751-105">You can use the diagnostics extension to collect diagnostic data like application logs or performance counters from an Azure virtual machine (VM) that is running Windows.</span></span> <span data-ttu-id="0c751-106">Questo articolo illustra come usare Windows PowerShell per abilitare l'estensione di diagnostica per una VM.</span><span class="sxs-lookup"><span data-stu-id="0c751-106">This article describes how to use Windows PowerShell to enable the diagnostics extension for a VM.</span></span> <span data-ttu-id="0c751-107">Per i prerequisiti necessari per questo articolo, vedere [Come installare e configurare Azure PowerShell](/powershell/azure/overview) .</span><span class="sxs-lookup"><span data-stu-id="0c751-107">See [How to install and configure Azure PowerShell](/powershell/azure/overview) for the prerequisites needed for this article.</span></span>

## <a name="enable-the-diagnostics-extension-if-you-use-the-resource-manager-deployment-model"></a><span data-ttu-id="0c751-108">Abilitare l'estensione di diagnostica se si usa il modello di distribuzione di Gestione risorse</span><span class="sxs-lookup"><span data-stu-id="0c751-108">Enable the diagnostics extension if you use the Resource Manager deployment model</span></span>
<span data-ttu-id="0c751-109">È possibile abilitare l'estensione di diagnostica durante la creazione di una VM Windows con il modello di distribuzione di Gestione risorse di Azure aggiungendo la configurazione dell'estensione al modello di Gestione risorse.</span><span class="sxs-lookup"><span data-stu-id="0c751-109">You can enable the diagnostics extension while you create a Windows VM through the Azure Resource Manager deployment model by adding the extension configuration to the Resource Manager template.</span></span> <span data-ttu-id="0c751-110">Vedere [Creare una macchina virtuale Windows con monitoraggio e diagnostica mediante il modello di Azure Resource Manager](extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0c751-110">See [Create a Windows virtual machine with monitoring and diagnostics by using the Azure Resource Manager template](extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="0c751-111">Per abilitare l'estensione di diagnostica in una VM esistente creata mediante il modello di distribuzione di Resource Manager, è possibile usare il cmdlet di PowerShell [Set-AzureRMVMDiagnosticsExtension](/powershell/module/azurerm.compute/set-azurermvmdiagnosticsextension) come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="0c751-111">To enable the diagnostics extension on an existing VM that was created through the Resource Manager deployment model, you can use the [Set-AzureRMVMDiagnosticsExtension](/powershell/module/azurerm.compute/set-azurermvmdiagnosticsextension) PowerShell cmdlet as shown below.</span></span>

    $vm_resourcegroup = "myvmresourcegroup"
    $vm_name = "myvm"
    $diagnosticsconfig_path = "DiagnosticsPubConfig.xml"

    Set-AzureRmVMDiagnosticsExtension -ResourceGroupName $vm_resourcegroup -VMName $vm_name -DiagnosticsConfigurationPath $diagnosticsconfig_path


<span data-ttu-id="0c751-112">*$diagnosticsconfig_path* è il percorso del file contenente la configurazione di diagnostica in formato XML, come descritto nell'[esempio](#sample-diagnostics-configuration) riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="0c751-112">*$diagnosticsconfig_path* is the path to the file that contains the diagnostics configuration in XML, as described in the [sample](#sample-diagnostics-configuration) below.</span></span>  

<span data-ttu-id="0c751-113">Se il file di configurazione di diagnostica specifica un elemento **StorageAccount** con il nome di un account di archiviazione, lo script *Set-AzureRMVMDiagnosticsExtension* imposta automaticamente l'estensione di diagnostica per l'invio dei dati di diagnostica all'account di archiviazione specificato.</span><span class="sxs-lookup"><span data-stu-id="0c751-113">If the diagnostics configuration file specifies a **StorageAccount** element with a storage account name, then the *Set-AzureRMVMDiagnosticsExtension* script will automatically set the diagnostics extension to send diagnostic data to that storage account.</span></span> <span data-ttu-id="0c751-114">A tal fine, l'account di archiviazione deve trovarsi nella stessa sottoscrizione della VM.</span><span class="sxs-lookup"><span data-stu-id="0c751-114">For this to work, the storage account needs to be in the same subscription as the VM.</span></span>

<span data-ttu-id="0c751-115">Se nella configurazione di diagnostica non è specificato alcun elemento **StorageAccount** , è necessario passare il parametro *StorageAccountName* al cmdlet.</span><span class="sxs-lookup"><span data-stu-id="0c751-115">If no **StorageAccount** was specified in the diagnostics configuration, then you need to pass in the *StorageAccountName* parameter to the cmdlet.</span></span> <span data-ttu-id="0c751-116">Se il parametro *StorageAccountName* è specificato, il cmdlet userà sempre l'account di archiviazione specificato nel parametro e non quello specificato nel file di configurazione della diagnostica.</span><span class="sxs-lookup"><span data-stu-id="0c751-116">If the *StorageAccountName* parameter is specified, then the cmdlet will always use the storage account that is specified in the parameter and not the one that is specified in the diagnostics configuration file.</span></span>

<span data-ttu-id="0c751-117">Se l'account di archiviazione di diagnostica si trova in una sottoscrizione diversa da quella della VM, è necessario passare in modo esplicito i parametri *StorageAccountName* e *StorageAccountKey* al cmdlet.</span><span class="sxs-lookup"><span data-stu-id="0c751-117">If the diagnostics storage account is in a different subscription from the VM, then you need to explicitly pass in the *StorageAccountName* and *StorageAccountKey* parameters to the cmdlet.</span></span> <span data-ttu-id="0c751-118">Il parametro *StorageAccountKey* non è necessario quando l'account di archiviazione di diagnostica si trova nella stessa sottoscrizione perché il cmdlet può automaticamente eseguire una query e impostare il valore della chiave durante l'abilitazione dell'estensione di diagnostica.</span><span class="sxs-lookup"><span data-stu-id="0c751-118">The *StorageAccountKey* parameter is not needed when the diagnostics storage account is in the same subscription, as the cmdlet can automatically query and set the key value when enabling the diagnostics extension.</span></span> <span data-ttu-id="0c751-119">Tuttavia, se l'account di archiviazione di diagnostica si trova in una sottoscrizione diversa, il cmdlet potrebbe non essere in grado di ottenere automaticamente la chiave, quindi si deve specificare la chiave in modo esplicito tramite il parametro *StorageAccountKey* .</span><span class="sxs-lookup"><span data-stu-id="0c751-119">However, if the diagnostics storage account is in a different subscription, then the cmdlet might not be able to get the key automatically and you need to explicitly specify the key through the *StorageAccountKey* parameter.</span></span>  

    Set-AzureRmVMDiagnosticsExtension -ResourceGroupName $vm_resourcegroup -VMName $vm_name -DiagnosticsConfigurationPath $diagnosticsconfig_path -StorageAccountName $diagnosticsstorage_name -StorageAccountKey $diagnosticsstorage_key

<span data-ttu-id="0c751-120">Dopo aver abilitato l'estensione di diagnostica in una VM, è possibile ottenere le impostazioni correnti mediante il cmdlet [Get-AzureRMVmDiagnosticsExtension](/powershell/module/azurerm.compute/get-azurermvmdiagnosticsextension) .</span><span class="sxs-lookup"><span data-stu-id="0c751-120">Once the diagnostics extension is enabled on a VM, you can get the current settings by using the [Get-AzureRMVmDiagnosticsExtension](/powershell/module/azurerm.compute/get-azurermvmdiagnosticsextension) cmdlet.</span></span>

    Get-AzureRmVMDiagnosticsExtension -ResourceGroupName $vm_resourcegroup -VMName $vm_name

<span data-ttu-id="0c751-121">Il cmdlet restituisce *PublicSettings*, contenente la configurazione di diagnostica.</span><span class="sxs-lookup"><span data-stu-id="0c751-121">The cmdlet returns *PublicSettings*, which contains the diagnostics configuration.</span></span> <span data-ttu-id="0c751-122">Esistono due tipi di configurazione supportata: WadCfg e xmlCfg.</span><span class="sxs-lookup"><span data-stu-id="0c751-122">There are two kinds of configuration supported, WadCfg and xmlCfg.</span></span> <span data-ttu-id="0c751-123">WadCfg è una configurazione JSON e xmlCfg è una configurazione XML in un formato con codifica Base64.</span><span class="sxs-lookup"><span data-stu-id="0c751-123">WadCfg is JSON configuration, and xmlCfg is XML configuration in a Base64-encoded format.</span></span> <span data-ttu-id="0c751-124">Per leggere la configurazione XML è necessario decodificarla.</span><span class="sxs-lookup"><span data-stu-id="0c751-124">To read the XML, you need to decode it.</span></span>

    $publicsettings = (Get-AzureRmVMDiagnosticsExtension -ResourceGroupName $vm_resourcegroup -VMName $vm_name).PublicSettings
    $encodedconfig = (ConvertFrom-Json -InputObject $publicsettings).xmlCfg
    $xmlconfig = [System.Text.Encoding]::UTF8.GetString([System.Convert]::FromBase64String($encodedconfig))
    Write-Host $xmlconfig

<span data-ttu-id="0c751-125">Il cmdlet [Remove AzureRMVmDiagnosticsExtension](/powershell/module/azurerm.compute/remove-azurermvmdiagnosticsextension) può essere usato per rimuovere l'estensione di diagnostica dalla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="0c751-125">The [Remove-AzureRMVmDiagnosticsExtension](/powershell/module/azurerm.compute/remove-azurermvmdiagnosticsextension) cmdlet can be used to remove the diagnostics extension from the VM.</span></span>  

## <a name="enable-the-diagnostics-extension-if-you-use-the-classic-deployment-model"></a><span data-ttu-id="0c751-126">Abilitare l'estensione di diagnostica se si usa il modello di distribuzione classico</span><span class="sxs-lookup"><span data-stu-id="0c751-126">Enable the diagnostics extension if you use the classic deployment model</span></span>
<span data-ttu-id="0c751-127">È possibile usare il cmdlet [Set-AzureVMDiagnosticsExtension](/powershell/module/azure/set-azurevmdiagnosticsextension) per abilitare un'estensione di diagnostica in una VM creata tramite il modello di distribuzione classica.</span><span class="sxs-lookup"><span data-stu-id="0c751-127">You can use the [Set-AzureVMDiagnosticsExtension](/powershell/module/azure/set-azurevmdiagnosticsextension) cmdlet to enable a diagnostics extension on a VM that you create through the classic deployment model.</span></span> <span data-ttu-id="0c751-128">L'esempio seguente illustra come creare una nuova VM tramite il modello di distribuzione classico con l'estensione di diagnostica abilitata.</span><span class="sxs-lookup"><span data-stu-id="0c751-128">The following example shows how to create a new VM through the classic deployment model with the diagnostics extension enabled.</span></span>

    $VM = New-AzureVMConfig -Name $VM -InstanceSize Small -ImageName $VMImage
    $VM = Add-AzureProvisioningConfig -VM $VM -AdminUsername $Username -Password $Password -Windows
    $VM = Set-AzureVMDiagnosticsExtension -DiagnosticsConfigurationPath $Config_Path -VM $VM -StorageContext $Storage_Context
    New-AzureVM -Location $Location -ServiceName $Service_Name -VM $VM

<span data-ttu-id="0c751-129">Per abilitare l'estensione di diagnostica su una VM esistente creata tramite il modello di distribuzione classica, usare prima il cmdlet [Get-AzureVM](/powershell/module/azure/get-azurevm) per ottenere la configurazione della VM.</span><span class="sxs-lookup"><span data-stu-id="0c751-129">To enable the diagnostics extension on an existing VM that was created through the classic deployment model, first use the [Get-AzureVM](/powershell/module/azure/get-azurevm) cmdlet to get the VM configuration.</span></span> <span data-ttu-id="0c751-130">Aggiornare quindi la configurazione della VM per includere l'estensione di diagnostica tramite il cmdlet [Set-AzureVMDiagnosticsExtension](/powershell/module/azure/set-azurevmdiagnosticsextension) .</span><span class="sxs-lookup"><span data-stu-id="0c751-130">Then update the VM configuration to include the diagnostics extension by using the [Set-AzureVMDiagnosticsExtension](/powershell/module/azure/set-azurevmdiagnosticsextension) cmdlet.</span></span> <span data-ttu-id="0c751-131">Infine applicare la configurazione aggiornata alla VM tramite [Update-AzureVM](/powershell/module/azure/update-azurevm).</span><span class="sxs-lookup"><span data-stu-id="0c751-131">Finally, apply the updated configuration to the VM by using [Update-AzureVM](/powershell/module/azure/update-azurevm).</span></span>

    $VM = Get-AzureVM -ServiceName $Service_Name -Name $VM_Name
    $VM_Update = Set-AzureVMDiagnosticsExtension -DiagnosticsConfigurationPath $Config_Path -VM $VM -StorageContext $Storage_Context
    Update-AzureVM -ServiceName $Service_Name -Name $VM_Name -VM $VM_Update.VM

## <a name="sample-diagnostics-configuration"></a><span data-ttu-id="0c751-132">Configurazione di diagnostica di esempio</span><span class="sxs-lookup"><span data-stu-id="0c751-132">Sample diagnostics configuration</span></span>
<span data-ttu-id="0c751-133">Per la configurazione pubblica di diagnostica con gli script precedenti, è possibile usare il codice XML seguente.</span><span class="sxs-lookup"><span data-stu-id="0c751-133">The following XML can be used for the diagnostics public configuration with the above scripts.</span></span> <span data-ttu-id="0c751-134">Questa configurazione di esempio trasferirà diversi contatori delle prestazioni all'account di archiviazione di diagnostica insieme agli errori dai canali Application, Security e System nei registri eventi di Windows e a eventuali errori dai registri dell'infrastruttura di diagnostica.</span><span class="sxs-lookup"><span data-stu-id="0c751-134">This sample configuration will transfer various performance counters to the diagnostics storage account, along with errors from the application, security, and system channels in the Windows event logs and any errors from the diagnostics infrastructure logs.</span></span>

<span data-ttu-id="0c751-135">La configurazione deve essere aggiornata per includere gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="0c751-135">The configuration needs to be updated to include the following:</span></span>

* <span data-ttu-id="0c751-136">L'attributo *resourceID* dell'elemento **Metrics** deve essere aggiornato con l'ID risorsa per la VM.</span><span class="sxs-lookup"><span data-stu-id="0c751-136">The *resourceID* attribute of the **Metrics** element needs to be updated with the resource ID for the VM.</span></span>
  
  * <span data-ttu-id="0c751-137">L'ID risorsa può essere creato usando il modello seguente: "/subscriptions/{*ID della sottoscrizione con la VM*}/resourceGroups/{*Nome del gruppo di risorse per la VM*}/providers/Microsoft.Compute/virtualMachines/{*Nome della VM*}".</span><span class="sxs-lookup"><span data-stu-id="0c751-137">The resource ID can be constructed by using the following pattern: "/subscriptions/{*subscription ID for the subscription with the VM*}/resourceGroups/{*The resourcegroup name for the VM*}/providers/Microsoft.Compute/virtualMachines/{*The VM Name*}".</span></span>
  * <span data-ttu-id="0c751-138">Ad esempio, se l'ID della sottoscrizione in cui è in esecuzione la VM è **11111111-1111-1111-1111-111111111111**, il nome del gruppo di risorse è **MyResourceGroup** e il nome della VM è **MyWindowsVM**, allora il valore per *resourceID* sarà:</span><span class="sxs-lookup"><span data-stu-id="0c751-138">For example, if the subscription ID for the subscription where the VM is running is **11111111-1111-1111-1111-111111111111**, the resource group name for the resource group is **MyResourceGroup**, and the VM Name is **MyWindowsVM**, then the value for *resourceID* would be:</span></span>
    
      ```
      <Metrics resourceId="/subscriptions/11111111-1111-1111-1111-111111111111/resourceGroups/MyResourceGroup/providers/Microsoft.Compute/virtualMachines/MyWindowsVM" >
      ```
  * <span data-ttu-id="0c751-139">Per altre informazioni sulla generazione delle metriche in base alla configurazione dei contatori delle prestazioni e delle metriche, vedere [Tabella delle metriche di Diagnostica di Azure nell'archiviazione](extensions-diagnostics-template.md#wadmetrics-tables-in-storage).</span><span class="sxs-lookup"><span data-stu-id="0c751-139">For more information on how metrics are generated based on the performance counters and metrics configuration, see [Azure Diagnostics metrics table in storage](extensions-diagnostics-template.md#wadmetrics-tables-in-storage).</span></span>
* <span data-ttu-id="0c751-140">L'elemento **StorageAccount** deve essere aggiornato con il nome dell'account di archiviazione di diagnostica.</span><span class="sxs-lookup"><span data-stu-id="0c751-140">The **StorageAccount** element needs to be updated with the name of the diagnostics storage account.</span></span>
  
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

## <a name="next-steps"></a><span data-ttu-id="0c751-141">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0c751-141">Next steps</span></span>
* <span data-ttu-id="0c751-142">Per altre indicazioni sull'uso della funzionalità Diagnostica di Azure e altre tecniche per la risoluzione dei problemi, vedere [Abilitazione di Diagnostica in Servizi cloud e nelle macchine virtuali di Azure](../../cloud-services/cloud-services-dotnet-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="0c751-142">For additional guidance on using the Azure Diagnostics capability and other techniques to troubleshoot problems, see [Enabling Diagnostics in Azure Cloud Services and Virtual Machines](../../cloud-services/cloud-services-dotnet-diagnostics.md).</span></span>
* <span data-ttu-id="0c751-143">[schema di configurazioni di diagnostica](https://msdn.microsoft.com/library/azure/mt634524.aspx) illustra le varie opzioni di configurazione XML per l'estensione di diagnostica.</span><span class="sxs-lookup"><span data-stu-id="0c751-143">[Diagnostics configurations schema](https://msdn.microsoft.com/library/azure/mt634524.aspx) explains the various XML configurations options for the diagnostics extension.</span></span>

