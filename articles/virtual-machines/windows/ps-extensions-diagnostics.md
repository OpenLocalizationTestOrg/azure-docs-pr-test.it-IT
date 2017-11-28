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
# <a name="use-powershell-tooenable-azure-diagnostics-in-a-virtual-machine-running-windows"></a><span data-ttu-id="129c9-103">Usare la diagnostica di Azure PowerShell tooenable in una macchina virtuale che esegue Windows</span><span class="sxs-lookup"><span data-stu-id="129c9-103">Use PowerShell tooenable Azure Diagnostics in a virtual machine running Windows</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="129c9-104">Diagnostica di Azure è possibilità hello all'interno di Azure che consente la raccolta hello dei dati di diagnostica in un'applicazione distribuita.</span><span class="sxs-lookup"><span data-stu-id="129c9-104">Azure Diagnostics is hello capability within Azure that enables hello collection of diagnostic data on a deployed application.</span></span> <span data-ttu-id="129c9-105">È possibile utilizzare hello diagnostica estensione toocollect dati di diagnostica come i log applicazioni o i contatori delle prestazioni da una macchina virtuale Azure (VM) che esegue Windows.</span><span class="sxs-lookup"><span data-stu-id="129c9-105">You can use hello diagnostics extension toocollect diagnostic data like application logs or performance counters from an Azure virtual machine (VM) that is running Windows.</span></span> <span data-ttu-id="129c9-106">In questo articolo viene descritto come tooenable di Windows PowerShell toouse hello estensione diagnostica per una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="129c9-106">This article describes how toouse Windows PowerShell tooenable hello diagnostics extension for a VM.</span></span> <span data-ttu-id="129c9-107">Vedere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview) per prerequisiti hello necessari per questo articolo.</span><span class="sxs-lookup"><span data-stu-id="129c9-107">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for hello prerequisites needed for this article.</span></span>

## <a name="enable-hello-diagnostics-extension-if-you-use-hello-resource-manager-deployment-model"></a><span data-ttu-id="129c9-108">Abilitare l'estensione di diagnostica hello se si utilizza il modello di distribuzione del hello Gestione risorse</span><span class="sxs-lookup"><span data-stu-id="129c9-108">Enable hello diagnostics extension if you use hello Resource Manager deployment model</span></span>
<span data-ttu-id="129c9-109">È possibile abilitare l'estensione diagnostica hello durante la creazione di una macchina virtuale di Windows tramite modello di distribuzione Azure Resource Manager hello aggiungendo hello estensione configurazione toohello Gestione risorse modello.</span><span class="sxs-lookup"><span data-stu-id="129c9-109">You can enable hello diagnostics extension while you create a Windows VM through hello Azure Resource Manager deployment model by adding hello extension configuration toohello Resource Manager template.</span></span> <span data-ttu-id="129c9-110">Vedere [creare una macchina virtuale Windows con monitoraggio e diagnostica usando il modello di gestione risorse di Azure hello](extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="129c9-110">See [Create a Windows virtual machine with monitoring and diagnostics by using hello Azure Resource Manager template](extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="129c9-111">estensione di diagnostica tooenable hello in una macchina virtuale esistente creata tramite il modello di distribuzione del hello Resource Manager, è possibile utilizzare hello [Set AzureRMVMDiagnosticsExtension](/powershell/module/azurerm.compute/set-azurermvmdiagnosticsextension) cmdlet di PowerShell come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="129c9-111">tooenable hello diagnostics extension on an existing VM that was created through hello Resource Manager deployment model, you can use hello [Set-AzureRMVMDiagnosticsExtension](/powershell/module/azurerm.compute/set-azurermvmdiagnosticsextension) PowerShell cmdlet as shown below.</span></span>

    $vm_resourcegroup = "myvmresourcegroup"
    $vm_name = "myvm"
    $diagnosticsconfig_path = "DiagnosticsPubConfig.xml"

    Set-AzureRmVMDiagnosticsExtension -ResourceGroupName $vm_resourcegroup -VMName $vm_name -DiagnosticsConfigurationPath $diagnosticsconfig_path


<span data-ttu-id="129c9-112">*$diagnosticsconfig_path* è hello percorso toohello contenente la configurazione della diagnostica hello in XML, come descritto nella hello [esempio](#sample-diagnostics-configuration) sotto.</span><span class="sxs-lookup"><span data-stu-id="129c9-112">*$diagnosticsconfig_path* is hello path toohello file that contains hello diagnostics configuration in XML, as described in hello [sample](#sample-diagnostics-configuration) below.</span></span>  

<span data-ttu-id="129c9-113">Se il file di configurazione diagnostica hello specifica un **StorageAccount** elemento con un nome di account di archiviazione, quindi hello *Set AzureRMVMDiagnosticsExtension* script imposterà automaticamente hello diagnostica estensione toosend dati di diagnostica toothat account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="129c9-113">If hello diagnostics configuration file specifies a **StorageAccount** element with a storage account name, then hello *Set-AzureRMVMDiagnosticsExtension* script will automatically set hello diagnostics extension toosend diagnostic data toothat storage account.</span></span> <span data-ttu-id="129c9-114">Per questo toowork, account di archiviazione di hello deve toobe in hello stessa sottoscrizione come hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="129c9-114">For this toowork, hello storage account needs toobe in hello same subscription as hello VM.</span></span>

<span data-ttu-id="129c9-115">Se non **StorageAccount** è stato specificato nella configurazione di diagnostica hello, è necessario toopass in hello *StorageAccountName* parametro toohello cmdlet.</span><span class="sxs-lookup"><span data-stu-id="129c9-115">If no **StorageAccount** was specified in hello diagnostics configuration, then you need toopass in hello *StorageAccountName* parameter toohello cmdlet.</span></span> <span data-ttu-id="129c9-116">Se hello *StorageAccountName* viene specificato, quindi hello cmdlet sarà sempre utilizzare account di archiviazione hello specificato nel parametro hello e hello non è specificato nel file di configurazione di diagnostica hello.</span><span class="sxs-lookup"><span data-stu-id="129c9-116">If hello *StorageAccountName* parameter is specified, then hello cmdlet will always use hello storage account that is specified in hello parameter and not hello one that is specified in hello diagnostics configuration file.</span></span>

<span data-ttu-id="129c9-117">Se la diagnostica hello account di archiviazione è in una sottoscrizione diversa da hello macchina virtuale, è necessario tooexplicitly passato hello *StorageAccountName* e *StorageAccountKey* parametri toohello cmdlet.</span><span class="sxs-lookup"><span data-stu-id="129c9-117">If hello diagnostics storage account is in a different subscription from hello VM, then you need tooexplicitly pass in hello *StorageAccountName* and *StorageAccountKey* parameters toohello cmdlet.</span></span> <span data-ttu-id="129c9-118">Hello *StorageAccountKey* parametro non è necessaria quando diagnostica hello account di archiviazione è in hello stessa sottoscrizione, come i cmdlet di hello automaticamente può eseguire query e impostare il valore chiave di hello quando si abilita l'estensione diagnostica hello.</span><span class="sxs-lookup"><span data-stu-id="129c9-118">hello *StorageAccountKey* parameter is not needed when hello diagnostics storage account is in hello same subscription, as hello cmdlet can automatically query and set hello key value when enabling hello diagnostics extension.</span></span> <span data-ttu-id="129c9-119">Tuttavia, se hello account di archiviazione di diagnostica è in una sottoscrizione diversa, quindi hello cmdlet potrebbe non essere in grado di tooget chiave di hello automaticamente e tooexplicitly necessario specificare la chiave hello tramite hello *StorageAccountKey* parametro.</span><span class="sxs-lookup"><span data-stu-id="129c9-119">However, if hello diagnostics storage account is in a different subscription, then hello cmdlet might not be able tooget hello key automatically and you need tooexplicitly specify hello key through hello *StorageAccountKey* parameter.</span></span>  

    Set-AzureRmVMDiagnosticsExtension -ResourceGroupName $vm_resourcegroup -VMName $vm_name -DiagnosticsConfigurationPath $diagnosticsconfig_path -StorageAccountName $diagnosticsstorage_name -StorageAccountKey $diagnosticsstorage_key

<span data-ttu-id="129c9-120">Una volta abilitata l'estensione diagnostica hello in una macchina virtuale, è possibile ottenere le impostazioni correnti di hello utilizzando hello [Get AzureRMVmDiagnosticsExtension](/powershell/module/azurerm.compute/get-azurermvmdiagnosticsextension) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="129c9-120">Once hello diagnostics extension is enabled on a VM, you can get hello current settings by using hello [Get-AzureRMVmDiagnosticsExtension](/powershell/module/azurerm.compute/get-azurermvmdiagnosticsextension) cmdlet.</span></span>

    Get-AzureRmVMDiagnosticsExtension -ResourceGroupName $vm_resourcegroup -VMName $vm_name

<span data-ttu-id="129c9-121">Hello cmdlet restituisce *PublicSettings*, che contiene la configurazione di diagnostica hello.</span><span class="sxs-lookup"><span data-stu-id="129c9-121">hello cmdlet returns *PublicSettings*, which contains hello diagnostics configuration.</span></span> <span data-ttu-id="129c9-122">Esistono due tipi di configurazione supportata: WadCfg e xmlCfg.</span><span class="sxs-lookup"><span data-stu-id="129c9-122">There are two kinds of configuration supported, WadCfg and xmlCfg.</span></span> <span data-ttu-id="129c9-123">WadCfg è una configurazione JSON e xmlCfg è una configurazione XML in un formato con codifica Base64.</span><span class="sxs-lookup"><span data-stu-id="129c9-123">WadCfg is JSON configuration, and xmlCfg is XML configuration in a Base64-encoded format.</span></span> <span data-ttu-id="129c9-124">tooread hello XML, è necessario toodecode è.</span><span class="sxs-lookup"><span data-stu-id="129c9-124">tooread hello XML, you need toodecode it.</span></span>

    $publicsettings = (Get-AzureRmVMDiagnosticsExtension -ResourceGroupName $vm_resourcegroup -VMName $vm_name).PublicSettings
    $encodedconfig = (ConvertFrom-Json -InputObject $publicsettings).xmlCfg
    $xmlconfig = [System.Text.Encoding]::UTF8.GetString([System.Convert]::FromBase64String($encodedconfig))
    Write-Host $xmlconfig

<span data-ttu-id="129c9-125">Hello [Remove AzureRMVmDiagnosticsExtension](/powershell/module/azurerm.compute/remove-azurermvmdiagnosticsextension) cmdlet può essere l'estensione di diagnostica hello tooremove utilizzati da hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="129c9-125">hello [Remove-AzureRMVmDiagnosticsExtension](/powershell/module/azurerm.compute/remove-azurermvmdiagnosticsextension) cmdlet can be used tooremove hello diagnostics extension from hello VM.</span></span>  

## <a name="enable-hello-diagnostics-extension-if-you-use-hello-classic-deployment-model"></a><span data-ttu-id="129c9-126">Abilitare l'estensione di diagnostica hello se si utilizza il modello di distribuzione classica hello</span><span class="sxs-lookup"><span data-stu-id="129c9-126">Enable hello diagnostics extension if you use hello classic deployment model</span></span>
<span data-ttu-id="129c9-127">È possibile utilizzare hello [Set AzureVMDiagnosticsExtension](/powershell/module/azure/set-azurevmdiagnosticsextension) tooenable cmdlet un'estensione di diagnostica in una macchina virtuale creata tramite il modello di distribuzione classica hello.</span><span class="sxs-lookup"><span data-stu-id="129c9-127">You can use hello [Set-AzureVMDiagnosticsExtension](/powershell/module/azure/set-azurevmdiagnosticsextension) cmdlet tooenable a diagnostics extension on a VM that you create through hello classic deployment model.</span></span> <span data-ttu-id="129c9-128">Hello seguente esempio viene illustrato come toocreate una nuova macchina virtuale tramite il modello di distribuzione classica hello con l'estensione diagnostica hello abilitato.</span><span class="sxs-lookup"><span data-stu-id="129c9-128">hello following example shows how toocreate a new VM through hello classic deployment model with hello diagnostics extension enabled.</span></span>

    $VM = New-AzureVMConfig -Name $VM -InstanceSize Small -ImageName $VMImage
    $VM = Add-AzureProvisioningConfig -VM $VM -AdminUsername $Username -Password $Password -Windows
    $VM = Set-AzureVMDiagnosticsExtension -DiagnosticsConfigurationPath $Config_Path -VM $VM -StorageContext $Storage_Context
    New-AzureVM -Location $Location -ServiceName $Service_Name -VM $VM

<span data-ttu-id="129c9-129">estensione di diagnostica tooenable hello in una macchina virtuale esistente creata tramite hello classico modello di distribuzione, hello prima di utilizzare [Get-AzureVM](/powershell/module/azure/get-azurevm) configurazione della macchina virtuale hello tooget cmdlet.</span><span class="sxs-lookup"><span data-stu-id="129c9-129">tooenable hello diagnostics extension on an existing VM that was created through hello classic deployment model, first use hello [Get-AzureVM](/powershell/module/azure/get-azurevm) cmdlet tooget hello VM configuration.</span></span> <span data-ttu-id="129c9-130">Quindi aggiornare l'estensione di diagnostica hello configurazione tooinclude hello VM utilizzando hello [Set AzureVMDiagnosticsExtension](/powershell/module/azure/set-azurevmdiagnosticsextension) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="129c9-130">Then update hello VM configuration tooinclude hello diagnostics extension by using hello [Set-AzureVMDiagnosticsExtension](/powershell/module/azure/set-azurevmdiagnosticsextension) cmdlet.</span></span> <span data-ttu-id="129c9-131">Infine, applicare hello aggiornato configurazione toohello VM utilizzando [Update-AzureVM](/powershell/module/azure/update-azurevm).</span><span class="sxs-lookup"><span data-stu-id="129c9-131">Finally, apply hello updated configuration toohello VM by using [Update-AzureVM](/powershell/module/azure/update-azurevm).</span></span>

    $VM = Get-AzureVM -ServiceName $Service_Name -Name $VM_Name
    $VM_Update = Set-AzureVMDiagnosticsExtension -DiagnosticsConfigurationPath $Config_Path -VM $VM -StorageContext $Storage_Context
    Update-AzureVM -ServiceName $Service_Name -Name $VM_Name -VM $VM_Update.VM

## <a name="sample-diagnostics-configuration"></a><span data-ttu-id="129c9-132">Configurazione di diagnostica di esempio</span><span class="sxs-lookup"><span data-stu-id="129c9-132">Sample diagnostics configuration</span></span>
<span data-ttu-id="129c9-133">Hello che codice XML seguente può essere utilizzato per hello diagnostica configurazione pubblica hello sopra gli script.</span><span class="sxs-lookup"><span data-stu-id="129c9-133">hello following XML can be used for hello diagnostics public configuration with hello above scripts.</span></span> <span data-ttu-id="129c9-134">Questa configurazione di esempio trasferirà vari prestazioni contatori toohello diagnostica account di archiviazione, insieme agli errori da un'applicazione hello, protezione e i canali di sistema nei registri eventi di Windows hello e gli eventuali errori da diagnostica di hello log dell'infrastruttura.</span><span class="sxs-lookup"><span data-stu-id="129c9-134">This sample configuration will transfer various performance counters toohello diagnostics storage account, along with errors from hello application, security, and system channels in hello Windows event logs and any errors from hello diagnostics infrastructure logs.</span></span>

<span data-ttu-id="129c9-135">configurazione di Hello deve seguenti di hello toobe tooinclude aggiornato:</span><span class="sxs-lookup"><span data-stu-id="129c9-135">hello configuration needs toobe updated tooinclude hello following:</span></span>

* <span data-ttu-id="129c9-136">Hello *resourceID* attributo di hello **metriche** elemento deve toobe aggiornata con ID di risorsa hello per hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="129c9-136">hello *resourceID* attribute of hello **Metrics** element needs toobe updated with hello resource ID for hello VM.</span></span>
  
  * <span data-ttu-id="129c9-137">Hello ID può essere creato utilizzando hello modello di risorsa: "le sottoscrizioni / {*ID per la sottoscrizione hello con hello VM*} / ResourceGroups / {*nome gruppo di risorse hello per hello VM*} / providers/Microsoft.Compute/virtualMachines/ {*hello nome della macchina virtuale*} ".</span><span class="sxs-lookup"><span data-stu-id="129c9-137">hello resource ID can be constructed by using hello following pattern: "/subscriptions/{*subscription ID for hello subscription with hello VM*}/resourceGroups/{*hello resourcegroup name for hello VM*}/providers/Microsoft.Compute/virtualMachines/{*hello VM Name*}".</span></span>
  * <span data-ttu-id="129c9-138">Ad esempio, se hello ID per sottoscrizione hello in hello macchina virtuale è in esecuzione è **11111111-1111-1111-1111-111111111111**, nome gruppo di risorse hello per il gruppo di risorse hello è **MyResourceGroup**, senza che sia hello nome della macchina virtuale **MyWindowsVM**, quindi hello valore per *resourceID* sarebbe:</span><span class="sxs-lookup"><span data-stu-id="129c9-138">For example, if hello subscription ID for hello subscription where hello VM is running is **11111111-1111-1111-1111-111111111111**, hello resource group name for hello resource group is **MyResourceGroup**, and hello VM Name is **MyWindowsVM**, then hello value for *resourceID* would be:</span></span>
    
      ```
      <Metrics resourceId="/subscriptions/11111111-1111-1111-1111-111111111111/resourceGroups/MyResourceGroup/providers/Microsoft.Compute/virtualMachines/MyWindowsVM" >
      ```
  * <span data-ttu-id="129c9-139">Per ulteriori informazioni su come le metriche sono i contatori delle prestazioni generati hello in base e la configurazione di metriche, vedere [tabella delle metriche di diagnostica di Azure nel servizio di archiviazione](extensions-diagnostics-template.md#wadmetrics-tables-in-storage).</span><span class="sxs-lookup"><span data-stu-id="129c9-139">For more information on how metrics are generated based on hello performance counters and metrics configuration, see [Azure Diagnostics metrics table in storage](extensions-diagnostics-template.md#wadmetrics-tables-in-storage).</span></span>
* <span data-ttu-id="129c9-140">Hello **StorageAccount** elemento deve toobe aggiornato con il nome di hello hello diagnostica dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="129c9-140">hello **StorageAccount** element needs toobe updated with hello name of hello diagnostics storage account.</span></span>
  
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

## <a name="next-steps"></a><span data-ttu-id="129c9-141">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="129c9-141">Next steps</span></span>
* <span data-ttu-id="129c9-142">Per ulteriori informazioni sull'uso di funzionalità di diagnostica Azure hello e altri problemi di tootroubleshoot tecniche, vedere [abilitazione di diagnostica in servizi Cloud di Azure e macchine virtuali](../../cloud-services/cloud-services-dotnet-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="129c9-142">For additional guidance on using hello Azure Diagnostics capability and other techniques tootroubleshoot problems, see [Enabling Diagnostics in Azure Cloud Services and Virtual Machines](../../cloud-services/cloud-services-dotnet-diagnostics.md).</span></span>
* <span data-ttu-id="129c9-143">[Schema di configurazione di diagnostica](https://msdn.microsoft.com/library/azure/mt634524.aspx) illustra diverse configurazioni XML opzioni per l'estensione diagnostica hello hello.</span><span class="sxs-lookup"><span data-stu-id="129c9-143">[Diagnostics configurations schema](https://msdn.microsoft.com/library/azure/mt634524.aspx) explains hello various XML configurations options for hello diagnostics extension.</span></span>

