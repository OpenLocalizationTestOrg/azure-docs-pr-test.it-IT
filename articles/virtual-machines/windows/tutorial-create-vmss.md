---
title: "Creare un set di scalabilità di macchine virtuali Windows in Azure | Documentazione Microsoft"
description: "Creare e distribuire un'applicazione a disponibilità elevata in VM Windows usando un set di scalabilità di macchine virtuali"
services: virtual-machine-scale-sets
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: 
ms.topic: article
ms.date: 08/11/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: 6600d3b401495f6c291249935b16bcc36c9b8f4b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-virtual-machine-scale-set-and-deploy-a-highly-available-app-on-windows"></a><span data-ttu-id="02a10-103">Creare un set di scalabilità di macchine virtuali e distribuire un'app a disponibilità elevata in Windows</span><span class="sxs-lookup"><span data-stu-id="02a10-103">Create a Virtual Machine Scale Set and deploy a highly available app on Windows</span></span>
<span data-ttu-id="02a10-104">Un set di scalabilità di macchine virtuali consente di distribuire e gestire un set di macchine virtuali identiche con scalabilità automatica.</span><span class="sxs-lookup"><span data-stu-id="02a10-104">A virtual machine scale set allows you to deploy and manage a set of identical, auto-scaling virtual machines.</span></span> <span data-ttu-id="02a10-105">È possibile adattare manualmente il numero di VM nel set di scalabilità o definire regole di scalabilità automatica in base all'utilizzo della CPU, alla richiesta di memoria o al traffico di rete.</span><span class="sxs-lookup"><span data-stu-id="02a10-105">You can scale the number of VMs in the scale set manually, or define rules to autoscale based on CPU usage, memory demand, or network traffic.</span></span> <span data-ttu-id="02a10-106">In questa esercitazione viene distribuito un set di scalabilità di macchine virtuali in Azure.</span><span class="sxs-lookup"><span data-stu-id="02a10-106">In this tutorial, you deploy a virtual machine scale set in Azure.</span></span> <span data-ttu-id="02a10-107">Si apprenderà come:</span><span class="sxs-lookup"><span data-stu-id="02a10-107">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="02a10-108">Usare l'estensione dello script personalizzata per definire un sito IIS da ridimensionare</span><span class="sxs-lookup"><span data-stu-id="02a10-108">Use the Custom Script Extension to define an IIS site to scale</span></span>
> * <span data-ttu-id="02a10-109">Creare un bilanciamento del carico per il set di scalabilità</span><span class="sxs-lookup"><span data-stu-id="02a10-109">Create a load balancer for your scale set</span></span>
> * <span data-ttu-id="02a10-110">Creare un set di scalabilità di macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="02a10-110">Create a virtual machine scale set</span></span>
> * <span data-ttu-id="02a10-111">Aumentare o diminuire il numero di istanze in un set di scalabilità</span><span class="sxs-lookup"><span data-stu-id="02a10-111">Increase or decrease the number of instances in a scale set</span></span>
> * <span data-ttu-id="02a10-112">Creare regole di scalabilità automatica</span><span class="sxs-lookup"><span data-stu-id="02a10-112">Create autoscale rules</span></span>

<span data-ttu-id="02a10-113">Questa esercitazione richiede il modulo Azure PowerShell 3.6 o versioni successive.</span><span class="sxs-lookup"><span data-stu-id="02a10-113">This tutorial requires the Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="02a10-114">Eseguire ` Get-Module -ListAvailable AzureRM` per trovare la versione.</span><span class="sxs-lookup"><span data-stu-id="02a10-114">Run ` Get-Module -ListAvailable AzureRM` to find the version.</span></span> <span data-ttu-id="02a10-115">Se è necessario eseguire l'aggiornamento, vedere [Installare e configurare Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="02a10-115">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>


## <a name="scale-set-overview"></a><span data-ttu-id="02a10-116">Informazioni generali sui set di scalabilità</span><span class="sxs-lookup"><span data-stu-id="02a10-116">Scale Set overview</span></span>
<span data-ttu-id="02a10-117">I set di scalabilità usano concetti simili a quelli descritti nell'esercitazione precedente [Creare VM a disponibilità elevata](tutorial-availability-sets.md).</span><span class="sxs-lookup"><span data-stu-id="02a10-117">Scale sets use similar concepts as you learned about in the previous tutorial to [Create highly available VMs](tutorial-availability-sets.md).</span></span> <span data-ttu-id="02a10-118">Le VM di un set di scalabilità sono distribuite in domini di errore e di aggiornamento esattamente come le VM di un set di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="02a10-118">VMs in a scale set are distributed across fault and update domains just like VMs in an availability set.</span></span>

<span data-ttu-id="02a10-119">Le VM vengono create in base alle esigenze in un set di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="02a10-119">VMs are created as needed in a scale set.</span></span> <span data-ttu-id="02a10-120">È possibile definire regole di scalabilità automatica per controllare le modalità e i tempi di aggiunta e rimozione delle VM dal set di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="02a10-120">You define autoscale rules to control how and when VMs are added or removed from the scale set.</span></span> <span data-ttu-id="02a10-121">Queste regole possono essere attivate in base a determinate metriche, ad esempio il carico della CPU, l'utilizzo della memoria o il traffico di rete.</span><span class="sxs-lookup"><span data-stu-id="02a10-121">These rules can trigger based on metrics such as CPU load, memory usage, or network traffic.</span></span>

<span data-ttu-id="02a10-122">I set di scalabilità supportano fino a 1.000 VM quando si usa un'immagine della piattaforma Azure.</span><span class="sxs-lookup"><span data-stu-id="02a10-122">Scale sets support up to 1,000 VMs when you use an Azure platform image.</span></span> <span data-ttu-id="02a10-123">Per i carichi di lavoro con requisiti significativi di installazione o personalizzazione di VM, si consiglia di [creare un'immagine di VM personalizzata](tutorial-custom-images.md).</span><span class="sxs-lookup"><span data-stu-id="02a10-123">For workloads with significant installation or VM customization requirements, you may wish to [Create a custom VM image](tutorial-custom-images.md).</span></span> <span data-ttu-id="02a10-124">È possibile creare fino a 100 VM in un set di scalabilità quando si usa un'immagine personalizzata.</span><span class="sxs-lookup"><span data-stu-id="02a10-124">You can create up to 100 VMs in a scale set when using a custom image.</span></span>


## <a name="create-an-app-to-scale"></a><span data-ttu-id="02a10-125">Creare un'app per la scalabilità</span><span class="sxs-lookup"><span data-stu-id="02a10-125">Create an app to scale</span></span>
<span data-ttu-id="02a10-126">Per poter creare un set di scalabilità è prima necessario creare un gruppo di risorse con il comando [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="02a10-126">Before you can create a scale set, create a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="02a10-127">L'esempio seguente crea un gruppo di risorse denominato *myResourceGroupAutomate* nella posizione *EastUS*:</span><span class="sxs-lookup"><span data-stu-id="02a10-127">The following example creates a resource group named *myResourceGroupAutomate* in the *EastUS* location:</span></span>

```powershell
New-AzureRmResourceGroup -ResourceGroupName myResourceGroupScaleSet -Location EastUS
```

<span data-ttu-id="02a10-128">In un'esercitazione precedente si è appreso come [automatizzare la configurazione della VM](tutorial-automate-vm-deployment.md) usando l'estensione dello script personalizzata.</span><span class="sxs-lookup"><span data-stu-id="02a10-128">In an earlier tutorial, you learned how to [Automate VM configuration](tutorial-automate-vm-deployment.md) using the Custom Script Extension.</span></span> <span data-ttu-id="02a10-129">Creare una configurazione del set di scalabilità e quindi applicare un'estensione dello script personalizzata per installare e configurare IIS:</span><span class="sxs-lookup"><span data-stu-id="02a10-129">Create a scale set configuration then apply a Custom Script Extension to install and configure IIS:</span></span>

```powershell
# Create a config object
$vmssConfig = New-AzureRmVmssConfig `
    -Location EastUS `
    -SkuCapacity 2 `
    -SkuName Standard_DS2 `
    -UpgradePolicyMode Automatic

# Define the script for your Custom Script Extension to run
$publicSettings = @{
    "fileUris" = (,"https://raw.githubusercontent.com/iainfoulds/azure-samples/master/automate-iis.ps1");
    "commandToExecute" = "powershell -ExecutionPolicy Unrestricted -File automate-iis.ps1"
}

# Use Custom Script Extension to install IIS and configure basic website
Add-AzureRmVmssExtension -VirtualMachineScaleSet $vmssConfig `
    -Name "customScript" `
    -Publisher "Microsoft.Compute" `
    -Type "CustomScriptExtension" `
    -TypeHandlerVersion 1.8 `
    -Setting $publicSettings
```

## <a name="create-scale-load-balancer"></a><span data-ttu-id="02a10-130">Creare un bilanciamento del carico di scalabilità</span><span class="sxs-lookup"><span data-stu-id="02a10-130">Create scale load balancer</span></span>
<span data-ttu-id="02a10-131">Azure Load Balancer è un bilanciamento del carico di livello 4 (TCP, UDP) che offre disponibilità elevata mediante la distribuzione del traffico in ingresso fra le VM integre.</span><span class="sxs-lookup"><span data-stu-id="02a10-131">An Azure load balancer is a Layer-4 (TCP, UDP) load balancer that provides high availability by distributing incoming traffic among healthy VMs.</span></span> <span data-ttu-id="02a10-132">Un probe di integrità del bilanciamento del carico monitora una determinata porta in ogni VM e distribuisce il traffico solo a una VM operativa.</span><span class="sxs-lookup"><span data-stu-id="02a10-132">A load balancer health probe monitors a given port on each VM and only distributes traffic to an operational VM.</span></span> <span data-ttu-id="02a10-133">Per altre informazioni, vedere l'esercitazione successiva in [Come bilanciare il carico delle macchine virtuali di Windows](tutorial-load-balancer.md).</span><span class="sxs-lookup"><span data-stu-id="02a10-133">For more information, see the next tutorial on [How to load balance Windows virtual machines](tutorial-load-balancer.md).</span></span>

<span data-ttu-id="02a10-134">Creare un bilanciamento del carico con un indirizzo IP pubblico che distribuisce il traffico Web sulla porta 80:</span><span class="sxs-lookup"><span data-stu-id="02a10-134">Create a load balancer that has a public IP address and distributes web traffic on port 80:</span></span>

```powershell
# Create a public IP address
$publicIP = New-AzureRmPublicIpAddress `
  -ResourceGroupName myResourceGroupScaleSet `
  -Location EastUS `
  -AllocationMethod Static `
  -Name myPublicIP

# Create a frontend and backend IP pool
$frontendIP = New-AzureRmLoadBalancerFrontendIpConfig `
  -Name myFrontEndPool `
  -PublicIpAddress $publicIP
$backendPool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name myBackEndPool

# Create the load balancer
$lb = New-AzureRmLoadBalancer `
  -ResourceGroupName myResourceGroupScaleSet `
  -Name myLoadBalancer `
  -Location EastUS `
  -FrontendIpConfiguration $frontendIP `
  -BackendAddressPool $backendPool

# Create a load balancer health probe on port 80
Add-AzureRmLoadBalancerProbeConfig -Name myHealthProbe `
  -LoadBalancer $lb `
  -Protocol tcp `
  -Port 80 `
  -IntervalInSeconds 15 `
  -ProbeCount 2

# Create a load balancer rule to distribute traffic on port 80
Add-AzureRmLoadBalancerRuleConfig `
  -Name myLoadBalancerRule `
  -LoadBalancer $lb `
  -FrontendIpConfiguration $lb.FrontendIpConfigurations[0] `
  -BackendAddressPool $lb.BackendAddressPools[0] `
  -Protocol Tcp `
  -FrontendPort 80 `
  -BackendPort 80

# Update the load balancer configuration
Set-AzureRmLoadBalancer -LoadBalancer $lb
```

## <a name="create-a-scale-set"></a><span data-ttu-id="02a10-135">Creare un set di scalabilità</span><span class="sxs-lookup"><span data-stu-id="02a10-135">Create a scale set</span></span>
<span data-ttu-id="02a10-136">Ora si può creare un set di scalabilità di macchine virtuali con [New-AzureRmVmss](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="02a10-136">Now create a virtual machine scale set with [New-AzureRmVmss](/powershell/module/azurerm.compute/new-azurermvm).</span></span> <span data-ttu-id="02a10-137">Nell'esempio seguente viene creato un set di scalabilità denominato *myScaleSet*:</span><span class="sxs-lookup"><span data-stu-id="02a10-137">The following example creates a scale set named *myScaleSet*:</span></span>

```powershell
# Reference a virtual machine image from the gallery
Set-AzureRmVmssStorageProfile $vmssConfig `
  -ImageReferencePublisher MicrosoftWindowsServer `
  -ImageReferenceOffer WindowsServer `
  -ImageReferenceSku 2016-Datacenter `
  -ImageReferenceVersion latest

# Set up information for authenticating with the virtual machine
Set-AzureRmVmssOsProfile $vmssConfig `
  -AdminUsername azureuser `
  -AdminPassword P@ssword! `
  -ComputerNamePrefix myVM

# Create the virtual network resources
$subnet = New-AzureRmVirtualNetworkSubnetConfig `
  -Name "mySubnet" `
  -AddressPrefix 10.0.0.0/24
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName "myResourceGroupScaleSet" `
  -Name "myVnet" `
  -Location "EastUS" `
  -AddressPrefix 10.0.0.0/16 `
  -Subnet $subnet
$ipConfig = New-AzureRmVmssIpConfig `
  -Name "myIPConfig" `
  -LoadBalancerBackendAddressPoolsId $lb.BackendAddressPools[0].Id `
  -SubnetId $vnet.Subnets[0].Id

# Attach the virtual network to the config object
Add-AzureRmVmssNetworkInterfaceConfiguration `
  -VirtualMachineScaleSet $vmssConfig `
  -Name "network-config" `
  -Primary $true `
  -IPConfiguration $ipConfig

# Create the scale set with the config object (this step might take a few minutes)
New-AzureRmVmss `
  -ResourceGroupName myResourceGroupScaleSet `
  -Name myScaleSet `
  -VirtualMachineScaleSet $vmssConfig
```

<span data-ttu-id="02a10-138">La creazione e la configurazione di tutte le macchine virtuali e risorse del set di scalabilità richiedono alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="02a10-138">It takes a few minutes to create and configure all the scale set resources and VMs.</span></span>


## <a name="test-your-app"></a><span data-ttu-id="02a10-139">Test dell'app</span><span class="sxs-lookup"><span data-stu-id="02a10-139">Test your app</span></span>
<span data-ttu-id="02a10-140">Per vedere il sito Web IIS in azione, ottenere l'indirizzo IP pubblico del servizio di bilanciamento del carico con il comando [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="02a10-140">To see your IIS website in action, obtain the public IP address of your load balancer with [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span></span> <span data-ttu-id="02a10-141">L'esempio seguente ottiene l'indirizzo IP per *myPublicIP* creato come parte del set di scalabilità:</span><span class="sxs-lookup"><span data-stu-id="02a10-141">The following example obtains the IP address for *myPublicIP* created as part of the scale set:</span></span>

```powershell
Get-AzureRmPublicIPAddress -ResourceGroupName myResourceGroupScaleSet -Name myPublicIP | select IpAddress
```

<span data-ttu-id="02a10-142">Immettere l'indirizzo IP pubblico in un Web browser.</span><span class="sxs-lookup"><span data-stu-id="02a10-142">Enter the public IP address in to a web browser.</span></span> <span data-ttu-id="02a10-143">Verrà visualizzata l'app, con il nome host della VM a cui il servizio di bilanciamento del carico ha distribuito il traffico:</span><span class="sxs-lookup"><span data-stu-id="02a10-143">The app is displayed, including the hostname of the VM that the load balancer distributed traffic to:</span></span>

![Esecuzione del sito IIS](./media/tutorial-create-vmss/running-iis-site.png)

<span data-ttu-id="02a10-145">Per verificare il funzionamento del set di scalabilità, è possibile imporre l'aggiornamento del Web browser per visualizzare la distribuzione del traffico da parte del bilanciamento del carico tra tutte le VM che eseguono l'app.</span><span class="sxs-lookup"><span data-stu-id="02a10-145">To see the scale set in action, you can force-refresh your web browser to see the load balancer distribute traffic across all the VMs running your app.</span></span>


## <a name="management-tasks"></a><span data-ttu-id="02a10-146">Attività di gestione</span><span class="sxs-lookup"><span data-stu-id="02a10-146">Management tasks</span></span>
<span data-ttu-id="02a10-147">Nel ciclo di vita del set di scalabilità, potrebbe essere necessario eseguire una o più attività di gestione.</span><span class="sxs-lookup"><span data-stu-id="02a10-147">Throughout the lifecycle of the scale set, you may need to run one or more management tasks.</span></span> <span data-ttu-id="02a10-148">Si potrebbe anche voler creare script per automatizzare le attività di ciclo di vita.</span><span class="sxs-lookup"><span data-stu-id="02a10-148">Additionally, you may want to create scripts that automate various lifecycle-tasks.</span></span> <span data-ttu-id="02a10-149">Azure PowerShell offre un modo rapido per eseguire queste operazioni.</span><span class="sxs-lookup"><span data-stu-id="02a10-149">Azure PowerShell provides a quick way to do those tasks.</span></span> <span data-ttu-id="02a10-150">Di seguito vengono illustrate alcune attività comuni.</span><span class="sxs-lookup"><span data-stu-id="02a10-150">Here are a few common tasks.</span></span>

### <a name="view-vms-in-a-scale-set"></a><span data-ttu-id="02a10-151">Visualizzare le VM in un set di scalabilità</span><span class="sxs-lookup"><span data-stu-id="02a10-151">View VMs in a scale set</span></span>
<span data-ttu-id="02a10-152">Per visualizzare l'elenco delle VM in esecuzione nel set di scalabilità, usare [Get-AzureRmVmssVM](/powershell/module/azurerm.compute/get-azurermvmssvm) come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="02a10-152">To view a list of VMs running in your scale set, use [Get-AzureRmVmssVM](/powershell/module/azurerm.compute/get-azurermvmssvm) as follows:</span></span>

```powershell
# Get current scale set
$scaleset = Get-AzureRmVmss `
  -ResourceGroupName myResourceGroupScaleSet `
  -VMScaleSetName myScaleSet

# Loop through the instanaces in your scale set
for ($i=1; $i -le ($scaleset.Sku.Capacity - 1); $i++) {
    Get-AzureRmVmssVM -ResourceGroupName myResourceGroupScaleSet `
      -VMScaleSetName myScaleSet `
      -InstanceId $i
}
```


### <a name="increase-or-decrease-vm-instances"></a><span data-ttu-id="02a10-153">Aumentare o diminuire le istanze delle macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="02a10-153">Increase or decrease VM instances</span></span>
<span data-ttu-id="02a10-154">Per visualizzare il numero di istanze attualmente presenti in un set di scalabilità, usare il comando [Get-AzureRmVmss](/powershell/module/azurerm.compute/get-azurermvmss) ed eseguire una query su *sku.capacity*:</span><span class="sxs-lookup"><span data-stu-id="02a10-154">To see the number of instances you currently have in a scale set, use [Get-AzureRmVmss](/powershell/module/azurerm.compute/get-azurermvmss) and query on *sku.capacity*:</span></span>

```powershell
Get-AzureRmVmss -ResourceGroupName myResourceGroupScaleSet `
    -VMScaleSetName myScaleSet | `
    Select -ExpandProperty Sku
```

<span data-ttu-id="02a10-155">È possibile quindi aumentare o ridurre manualmente il numero di macchine virtuali nel set di scalabilità con [Update-AzureRmVmss](/powershell/module/azurerm.compute/update-azurermvmss).</span><span class="sxs-lookup"><span data-stu-id="02a10-155">You can then manually increase or decrease the number of virtual machines in the scale set with [Update-AzureRmVmss](/powershell/module/azurerm.compute/update-azurermvmss).</span></span> <span data-ttu-id="02a10-156">L'esempio seguente imposta il numero di VM del set di scalabilità su *5*:</span><span class="sxs-lookup"><span data-stu-id="02a10-156">The following example sets the number of VMs in your scale set to *5*:</span></span>

```powershell
# Get current scale set
$scaleset = Get-AzureRmVmss `
  -ResourceGroupName myResourceGroupScaleSet `
  -VMScaleSetName myScaleSet

# Set and update the capacity of your scale set
$scaleset.sku.capacity = 5
Update-AzureRmVmss -ResourceGroupName myResourceGroupScaleSet `
    -Name myScaleSet `
    -VirtualMachineScaleSet $scaleset
```

<span data-ttu-id="02a10-157">Sono necessari alcuni minuti per aggiornare il numero specificato di istanze del set di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="02a10-157">If takes a few minutes to update the specified number of instances in your scale set.</span></span>


### <a name="configure-autoscale-rules"></a><span data-ttu-id="02a10-158">Configurare le regole di scalabilità automatica</span><span class="sxs-lookup"><span data-stu-id="02a10-158">Configure autoscale rules</span></span>
<span data-ttu-id="02a10-159">Anziché scalare manualmente il numero di istanze del set di scalabilità, si definiscono regole di scalabilità automatica.</span><span class="sxs-lookup"><span data-stu-id="02a10-159">Rather than manually scaling the number of instances in your scale set, you define autoscale rules.</span></span> <span data-ttu-id="02a10-160">Queste regole monitorano le istanze nel set di scalabilità e rispondono di conseguenza in base alle metriche e alle soglie definite.</span><span class="sxs-lookup"><span data-stu-id="02a10-160">These rules monitor the instances in your scale set and respond accordingly based on metrics and thresholds you define.</span></span> <span data-ttu-id="02a10-161">L'esempio seguente scala orizzontalmente il numero di istanze di uno quando il carico della CPU medio è maggiore del 60% per un periodo di 5 minuti.</span><span class="sxs-lookup"><span data-stu-id="02a10-161">The following example scales out the number of instances by one when the average CPU load is greater than 60% over a 5 minute period.</span></span> <span data-ttu-id="02a10-162">Se il carico della CPU medio scende poi sotto il 30% per un periodo di 5 minuti, le istanze vengono ridotte di una:</span><span class="sxs-lookup"><span data-stu-id="02a10-162">If the average CPU load then drops below 30% over a 5 minute period, the instances are scaled in by one instance:</span></span>

```powershell
# Define your scale set information
$mySubscriptionId = (Get-AzureRmSubscription).Id
$myResourceGroup = "myResourceGroupScaleSet"
$myScaleSet = "myScaleSet"
$myLocation = "East US"

# Create a scale up rule to increase the number instances after 60% average CPU usage exceeded for a 5 minute period
$myRuleScaleUp = New-AzureRmAutoscaleRule `
  -MetricName "Percentage CPU" `
  -MetricResourceId /subscriptions/$mySubscriptionId/resourceGroups/$myResourceGroup/providers/Microsoft.Compute/virtualMachineScaleSets/$myScaleSet `
  -Operator GreaterThan `
  -MetricStatistic Average `
  -Threshold 60 `
  -TimeGrain 00:01:00 `
  -TimeWindow 00:05:00 `
  -ScaleActionCooldown 00:05:00 `
  -ScaleActionDirection Increase `
  -ScaleActionValue 1

# Create a scale down rule to decrease the number of instances after 30% average CPU usage over a 5 minute period
$myRuleScaleDown = New-AzureRmAutoscaleRule `
  -MetricName "Percentage CPU" `
  -MetricResourceId /subscriptions/$mySubscriptionId/resourceGroups/$myResourceGroup/providers/Microsoft.Compute/virtualMachineScaleSets/$myScaleSet `
  -Operator LessThan `
  -MetricStatistic Average `
  -Threshold 30 `
  -TimeGrain 00:01:00 `
  -TimeWindow 00:05:00 `
  -ScaleActionCooldown 00:05:00 `
  -ScaleActionDirection Decrease `
  -ScaleActionValue 1

# Create a scale profile with your scale up and scale down rules
$myScaleProfile = New-AzureRmAutoscaleProfile `
  -DefaultCapacity 2  `
  -MaximumCapacity 10 `
  -MinimumCapacity 2 `
  -Rules $myRuleScaleUp,$myRuleScaleDown `
  -Name "autoprofile"

# Apply the autoscale rules
Add-AzureRmAutoscaleSetting `
  -Location $myLocation `
  -Name "autosetting" `
  -ResourceGroup $myResourceGroup `
  -TargetResourceId /subscriptions/$mySubscriptionId/resourceGroups/$myResourceGroup/providers/Microsoft.Compute/virtualMachineScaleSets/$myScaleSet `
  -AutoscaleProfiles $myScaleProfile
```


## <a name="next-steps"></a><span data-ttu-id="02a10-163">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="02a10-163">Next steps</span></span>
<span data-ttu-id="02a10-164">In questa esercitazione è stato creato un set di scalabilità di macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="02a10-164">In this tutorial, you created a virtual machine scale set.</span></span> <span data-ttu-id="02a10-165">Si è appreso come:</span><span class="sxs-lookup"><span data-stu-id="02a10-165">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="02a10-166">Usare l'estensione dello script personalizzata per definire un sito IIS da ridimensionare</span><span class="sxs-lookup"><span data-stu-id="02a10-166">Use the Custom Script Extension to define an IIS site to scale</span></span>
> * <span data-ttu-id="02a10-167">Creare un bilanciamento del carico per il set di scalabilità</span><span class="sxs-lookup"><span data-stu-id="02a10-167">Create a load balancer for your scale set</span></span>
> * <span data-ttu-id="02a10-168">Creare un set di scalabilità di macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="02a10-168">Create a virtual machine scale set</span></span>
> * <span data-ttu-id="02a10-169">Aumentare o diminuire il numero di istanze in un set di scalabilità</span><span class="sxs-lookup"><span data-stu-id="02a10-169">Increase or decrease the number of instances in a scale set</span></span>
> * <span data-ttu-id="02a10-170">Creare regole di scalabilità automatica</span><span class="sxs-lookup"><span data-stu-id="02a10-170">Create autoscale rules</span></span>

<span data-ttu-id="02a10-171">Passare all'esercitazione successiva per maggiori informazioni sui concetti di bilanciamento del carico per le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="02a10-171">Advance to the next tutorial to learn more about load balancing concepts for virtual machines.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="02a10-172">Bilanciare il carico delle macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="02a10-172">Load balance virtual machines</span></span>](tutorial-load-balancer.md)
