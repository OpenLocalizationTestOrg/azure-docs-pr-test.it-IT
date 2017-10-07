---
title: una macchina virtuale scala set per Windows in Azure aaaCreate | Documenti Microsoft
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
ms.openlocfilehash: a3914571005c28a492c069d880992630851afae7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-scale-set-and-deploy-a-highly-available-app-on-windows"></a><span data-ttu-id="d3eb3-103">Creare un set di scalabilità di macchine virtuali e distribuire un'app a disponibilità elevata in Windows</span><span class="sxs-lookup"><span data-stu-id="d3eb3-103">Create a Virtual Machine Scale Set and deploy a highly available app on Windows</span></span>
<span data-ttu-id="d3eb3-104">Un set di scalabilità della macchina virtuale consente toodeploy e gestire un set di macchine virtuali identiche e la scalabilità automatica.</span><span class="sxs-lookup"><span data-stu-id="d3eb3-104">A virtual machine scale set allows you toodeploy and manage a set of identical, auto-scaling virtual machines.</span></span> <span data-ttu-id="d3eb3-105">È possibile ridimensionare manualmente numero hello di macchine virtuali nel set di scalabilità hello o definire tooautoscale regole in base all'utilizzo della CPU, la richiesta di memoria o il traffico di rete.</span><span class="sxs-lookup"><span data-stu-id="d3eb3-105">You can scale hello number of VMs in hello scale set manually, or define rules tooautoscale based on CPU usage, memory demand, or network traffic.</span></span> <span data-ttu-id="d3eb3-106">In questa esercitazione viene distribuito un set di scalabilità di macchine virtuali in Azure.</span><span class="sxs-lookup"><span data-stu-id="d3eb3-106">In this tutorial, you deploy a virtual machine scale set in Azure.</span></span> <span data-ttu-id="d3eb3-107">Si apprenderà come:</span><span class="sxs-lookup"><span data-stu-id="d3eb3-107">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="d3eb3-108">Utilizzare toodefine estensione Script personalizzata hello un tooscale del sito IIS</span><span class="sxs-lookup"><span data-stu-id="d3eb3-108">Use hello Custom Script Extension toodefine an IIS site tooscale</span></span>
> * <span data-ttu-id="d3eb3-109">Creare un bilanciamento del carico per il set di scalabilità</span><span class="sxs-lookup"><span data-stu-id="d3eb3-109">Create a load balancer for your scale set</span></span>
> * <span data-ttu-id="d3eb3-110">Creare un set di scalabilità di macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="d3eb3-110">Create a virtual machine scale set</span></span>
> * <span data-ttu-id="d3eb3-111">Aumentare o diminuire il numero di hello di istanze in un set di scalabilità</span><span class="sxs-lookup"><span data-stu-id="d3eb3-111">Increase or decrease hello number of instances in a scale set</span></span>
> * <span data-ttu-id="d3eb3-112">Creare regole di scalabilità automatica</span><span class="sxs-lookup"><span data-stu-id="d3eb3-112">Create autoscale rules</span></span>

<span data-ttu-id="d3eb3-113">Questa esercitazione richiede hello Azure PowerShell versione 3.6 o versioni successive del modulo.</span><span class="sxs-lookup"><span data-stu-id="d3eb3-113">This tutorial requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="d3eb3-114">Eseguire ` Get-Module -ListAvailable AzureRM` versione hello toofind.</span><span class="sxs-lookup"><span data-stu-id="d3eb3-114">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="d3eb3-115">Se è necessario tooupgrade, vedere [modulo installare Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="d3eb3-115">If you need tooupgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>


## <a name="scale-set-overview"></a><span data-ttu-id="d3eb3-116">Informazioni generali sui set di scalabilità</span><span class="sxs-lookup"><span data-stu-id="d3eb3-116">Scale Set overview</span></span>
<span data-ttu-id="d3eb3-117">Set di scalabilità di utilizzare concetti simili come sono state descritte nell'esercitazione precedente hello troppo[creare macchine virtuali a disponibilità elevata](tutorial-availability-sets.md).</span><span class="sxs-lookup"><span data-stu-id="d3eb3-117">Scale sets use similar concepts as you learned about in hello previous tutorial too[Create highly available VMs](tutorial-availability-sets.md).</span></span> <span data-ttu-id="d3eb3-118">Le VM di un set di scalabilità sono distribuite in domini di errore e di aggiornamento esattamente come le VM di un set di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="d3eb3-118">VMs in a scale set are distributed across fault and update domains just like VMs in an availability set.</span></span>

<span data-ttu-id="d3eb3-119">Le macchine virtuali vengono create in base alle esigenze in un set di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="d3eb3-119">VMs are created as needed in a scale set.</span></span> <span data-ttu-id="d3eb3-120">Definire toocontrol le regole di scalabilità automatica come e quando le macchine virtuali vengono aggiunti o rimossi dal set di scalabilità hello.</span><span class="sxs-lookup"><span data-stu-id="d3eb3-120">You define autoscale rules toocontrol how and when VMs are added or removed from hello scale set.</span></span> <span data-ttu-id="d3eb3-121">Queste regole possono essere attivate in base a determinate metriche, ad esempio il carico della CPU, l'utilizzo della memoria o il traffico di rete.</span><span class="sxs-lookup"><span data-stu-id="d3eb3-121">These rules can trigger based on metrics such as CPU load, memory usage, or network traffic.</span></span>

<span data-ttu-id="d3eb3-122">Scala imposta supporto backup too1, 000 macchine virtuali quando si utilizza un'immagine della piattaforma Azure.</span><span class="sxs-lookup"><span data-stu-id="d3eb3-122">Scale sets support up too1,000 VMs when you use an Azure platform image.</span></span> <span data-ttu-id="d3eb3-123">Per i carichi di lavoro con installazione significativo o i requisiti di personalizzazione di macchina virtuale, è preferibile troppo[creare un'immagine di macchina virtuale personalizzata](tutorial-custom-images.md).</span><span class="sxs-lookup"><span data-stu-id="d3eb3-123">For workloads with significant installation or VM customization requirements, you may wish too[Create a custom VM image](tutorial-custom-images.md).</span></span> <span data-ttu-id="d3eb3-124">È possibile creare le macchine virtuali too100 in una scala impostata quando si utilizza un'immagine personalizzata.</span><span class="sxs-lookup"><span data-stu-id="d3eb3-124">You can create up too100 VMs in a scale set when using a custom image.</span></span>


## <a name="create-an-app-tooscale"></a><span data-ttu-id="d3eb3-125">Creare un'app tooscale</span><span class="sxs-lookup"><span data-stu-id="d3eb3-125">Create an app tooscale</span></span>
<span data-ttu-id="d3eb3-126">Per poter creare un set di scalabilità è prima necessario creare un gruppo di risorse con il comando [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="d3eb3-126">Before you can create a scale set, create a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="d3eb3-127">esempio Hello crea un gruppo di risorse denominato *myResourceGroupAutomate* in hello *EastUS* percorso:</span><span class="sxs-lookup"><span data-stu-id="d3eb3-127">hello following example creates a resource group named *myResourceGroupAutomate* in hello *EastUS* location:</span></span>

```powershell
New-AzureRmResourceGroup -ResourceGroupName myResourceGroupScaleSet -Location EastUS
```

<span data-ttu-id="d3eb3-128">In un'esercitazione precedente, si è appreso come troppo[configurazione della macchina virtuale automatizzare](tutorial-automate-vm-deployment.md) utilizzando hello estensione Script personalizzata.</span><span class="sxs-lookup"><span data-stu-id="d3eb3-128">In an earlier tutorial, you learned how too[Automate VM configuration](tutorial-automate-vm-deployment.md) using hello Custom Script Extension.</span></span> <span data-ttu-id="d3eb3-129">Creare la configurazione di un set di scalabilità, quindi applicare un tooinstall estensione Script personalizzata e configurare IIS:</span><span class="sxs-lookup"><span data-stu-id="d3eb3-129">Create a scale set configuration then apply a Custom Script Extension tooinstall and configure IIS:</span></span>

```powershell
# Create a config object
$vmssConfig = New-AzureRmVmssConfig `
    -Location EastUS `
    -SkuCapacity 2 `
    -SkuName Standard_DS2 `
    -UpgradePolicyMode Automatic

# Define hello script for your Custom Script Extension toorun
$publicSettings = @{
    "fileUris" = (,"https://raw.githubusercontent.com/iainfoulds/azure-samples/master/automate-iis.ps1");
    "commandToExecute" = "powershell -ExecutionPolicy Unrestricted -File automate-iis.ps1"
}

# Use Custom Script Extension tooinstall IIS and configure basic website
Add-AzureRmVmssExtension -VirtualMachineScaleSet $vmssConfig `
    -Name "customScript" `
    -Publisher "Microsoft.Compute" `
    -Type "CustomScriptExtension" `
    -TypeHandlerVersion 1.8 `
    -Setting $publicSettings
```

## <a name="create-scale-load-balancer"></a><span data-ttu-id="d3eb3-130">Creare un bilanciamento del carico di scalabilità</span><span class="sxs-lookup"><span data-stu-id="d3eb3-130">Create scale load balancer</span></span>
<span data-ttu-id="d3eb3-131">Azure Load Balancer è un bilanciamento del carico di livello 4 (TCP, UDP) che offre disponibilità elevata mediante la distribuzione del traffico in ingresso nelle macchine virtuali integre.</span><span class="sxs-lookup"><span data-stu-id="d3eb3-131">An Azure load balancer is a Layer-4 (TCP, UDP) load balancer that provides high availability by distributing incoming traffic among healthy VMs.</span></span> <span data-ttu-id="d3eb3-132">Un probe di integrità di bilanciamento del carico consente di monitorare una determinata porta in ogni macchina virtuale e vengono distribuiti solo il traffico tooan operativo VM.</span><span class="sxs-lookup"><span data-stu-id="d3eb3-132">A load balancer health probe monitors a given port on each VM and only distributes traffic tooan operational VM.</span></span> <span data-ttu-id="d3eb3-133">Per ulteriori informazioni, vedere l'esercitazione successiva hello in [come tooload bilanciare le macchine virtuali Windows](tutorial-load-balancer.md).</span><span class="sxs-lookup"><span data-stu-id="d3eb3-133">For more information, see hello next tutorial on [How tooload balance Windows virtual machines](tutorial-load-balancer.md).</span></span>

<span data-ttu-id="d3eb3-134">Creare un bilanciamento del carico con un indirizzo IP pubblico che distribuisce il traffico Web sulla porta 80:</span><span class="sxs-lookup"><span data-stu-id="d3eb3-134">Create a load balancer that has a public IP address and distributes web traffic on port 80:</span></span>

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

# Create hello load balancer
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

# Create a load balancer rule toodistribute traffic on port 80
Add-AzureRmLoadBalancerRuleConfig `
  -Name myLoadBalancerRule `
  -LoadBalancer $lb `
  -FrontendIpConfiguration $lb.FrontendIpConfigurations[0] `
  -BackendAddressPool $lb.BackendAddressPools[0] `
  -Protocol Tcp `
  -FrontendPort 80 `
  -BackendPort 80

# Update hello load balancer configuration
Set-AzureRmLoadBalancer -LoadBalancer $lb
```

## <a name="create-a-scale-set"></a><span data-ttu-id="d3eb3-135">Creare un set di scalabilità</span><span class="sxs-lookup"><span data-stu-id="d3eb3-135">Create a scale set</span></span>
<span data-ttu-id="d3eb3-136">Ora si può creare un set di scalabilità di macchine virtuali con [New-AzureRmVmss](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="d3eb3-136">Now create a virtual machine scale set with [New-AzureRmVmss](/powershell/module/azurerm.compute/new-azurermvm).</span></span> <span data-ttu-id="d3eb3-137">esempio Hello crea un set denominato di scalabilità *myScaleSet*:</span><span class="sxs-lookup"><span data-stu-id="d3eb3-137">hello following example creates a scale set named *myScaleSet*:</span></span>

```powershell
# Reference a virtual machine image from hello gallery
Set-AzureRmVmssStorageProfile $vmssConfig `
  -ImageReferencePublisher MicrosoftWindowsServer `
  -ImageReferenceOffer WindowsServer `
  -ImageReferenceSku 2016-Datacenter `
  -ImageReferenceVersion latest

# Set up information for authenticating with hello virtual machine
Set-AzureRmVmssOsProfile $vmssConfig `
  -AdminUsername azureuser `
  -AdminPassword P@ssword! `
  -ComputerNamePrefix myVM

# Create hello virtual network resources
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

# Attach hello virtual network toohello config object
Add-AzureRmVmssNetworkInterfaceConfiguration `
  -VirtualMachineScaleSet $vmssConfig `
  -Name "network-config" `
  -Primary $true `
  -IPConfiguration $ipConfig

# Create hello scale set with hello config object (this step might take a few minutes)
New-AzureRmVmss `
  -ResourceGroupName myResourceGroupScaleSet `
  -Name myScaleSet `
  -VirtualMachineScaleSet $vmssConfig
```

<span data-ttu-id="d3eb3-138">Accetta toocreate di pochi minuti e configurare tutti i set di hello scalabilità delle risorse e le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="d3eb3-138">It takes a few minutes toocreate and configure all hello scale set resources and VMs.</span></span>


## <a name="test-your-app"></a><span data-ttu-id="d3eb3-139">Test dell'app</span><span class="sxs-lookup"><span data-stu-id="d3eb3-139">Test your app</span></span>
<span data-ttu-id="d3eb3-140">toosee il sito Web IIS in azione, ottenere indirizzo IP pubblico di hello del servizio di bilanciamento del carico con [Get AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="d3eb3-140">toosee your IIS website in action, obtain hello public IP address of your load balancer with [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span></span> <span data-ttu-id="d3eb3-141">esempio Hello Ottiene hello di indirizzo IP per *myPublicIP* creati come parte del set di scalabilità hello:</span><span class="sxs-lookup"><span data-stu-id="d3eb3-141">hello following example obtains hello IP address for *myPublicIP* created as part of hello scale set:</span></span>

```powershell
Get-AzureRmPublicIPAddress -ResourceGroupName myResourceGroupScaleSet -Name myPublicIP | select IpAddress
```

<span data-ttu-id="d3eb3-142">Immettere l'indirizzo IP pubblico hello nel browser web tooa.</span><span class="sxs-lookup"><span data-stu-id="d3eb3-142">Enter hello public IP address in tooa web browser.</span></span> <span data-ttu-id="d3eb3-143">viene visualizzata, Hello app, inclusi hostname hello di hello VM che hello il carico del traffico di bilanciamento del carico distribuito per:</span><span class="sxs-lookup"><span data-stu-id="d3eb3-143">hello app is displayed, including hello hostname of hello VM that hello load balancer distributed traffic to:</span></span>

![Esecuzione del sito IIS](./media/tutorial-create-vmss/running-iis-site.png)

<span data-ttu-id="d3eb3-145">toosee set nell'azione di scalabilità hello, è possibile forza l'aggiornamento del carico di web browser toosee hello distribuire il servizio di bilanciamento del traffico tra tutte le macchine virtuali hello esegue l'app.</span><span class="sxs-lookup"><span data-stu-id="d3eb3-145">toosee hello scale set in action, you can force-refresh your web browser toosee hello load balancer distribute traffic across all hello VMs running your app.</span></span>


## <a name="management-tasks"></a><span data-ttu-id="d3eb3-146">Attività di gestione</span><span class="sxs-lookup"><span data-stu-id="d3eb3-146">Management tasks</span></span>
<span data-ttu-id="d3eb3-147">Nel ciclo di vita hello del set di scalabilità di hello, potrebbe essere necessario toorun uno o più attività di gestione.</span><span class="sxs-lookup"><span data-stu-id="d3eb3-147">Throughout hello lifecycle of hello scale set, you may need toorun one or more management tasks.</span></span> <span data-ttu-id="d3eb3-148">Inoltre, è consigliabile toocreate script che automatizzano le varie attività di ciclo di vita.</span><span class="sxs-lookup"><span data-stu-id="d3eb3-148">Additionally, you may want toocreate scripts that automate various lifecycle-tasks.</span></span> <span data-ttu-id="d3eb3-149">Azure PowerShell fornisce un toodo rapidamente le attività.</span><span class="sxs-lookup"><span data-stu-id="d3eb3-149">Azure PowerShell provides a quick way toodo those tasks.</span></span> <span data-ttu-id="d3eb3-150">Di seguito vengono illustrate alcune attività comuni.</span><span class="sxs-lookup"><span data-stu-id="d3eb3-150">Here are a few common tasks.</span></span>

### <a name="view-vms-in-a-scale-set"></a><span data-ttu-id="d3eb3-151">Visualizzare le macchine virtuali in un set di scalabilità</span><span class="sxs-lookup"><span data-stu-id="d3eb3-151">View VMs in a scale set</span></span>
<span data-ttu-id="d3eb3-152">imposta un elenco di macchine virtuali in esecuzione nella scala tooview, utilizzare [Get AzureRmVmssVM](/powershell/module/azurerm.compute/get-azurermvmssvm) come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="d3eb3-152">tooview a list of VMs running in your scale set, use [Get-AzureRmVmssVM](/powershell/module/azurerm.compute/get-azurermvmssvm) as follows:</span></span>

```powershell
# Get current scale set
$scaleset = Get-AzureRmVmss `
  -ResourceGroupName myResourceGroupScaleSet `
  -VMScaleSetName myScaleSet

# Loop through hello instanaces in your scale set
for ($i=1; $i -le ($scaleset.Sku.Capacity - 1); $i++) {
    Get-AzureRmVmssVM -ResourceGroupName myResourceGroupScaleSet `
      -VMScaleSetName myScaleSet `
      -InstanceId $i
}
```


### <a name="increase-or-decrease-vm-instances"></a><span data-ttu-id="d3eb3-153">Aumentare o diminuire le istanze delle macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="d3eb3-153">Increase or decrease VM instances</span></span>
<span data-ttu-id="d3eb3-154">numero di hello toosee di istanze attualmente in una scala impostate, utilizzare [Get AzureRmVmss](/powershell/module/azurerm.compute/get-azurermvmss) ed eseguire query su *sku.capacity*:</span><span class="sxs-lookup"><span data-stu-id="d3eb3-154">toosee hello number of instances you currently have in a scale set, use [Get-AzureRmVmss](/powershell/module/azurerm.compute/get-azurermvmss) and query on *sku.capacity*:</span></span>

```powershell
Get-AzureRmVmss -ResourceGroupName myResourceGroupScaleSet `
    -VMScaleSetName myScaleSet | `
    Select -ExpandProperty Sku
```

<span data-ttu-id="d3eb3-155">È possibile quindi manualmente aumentare o diminuire il numero di hello di macchine virtuali in hello set di scalabilità con [aggiornamento AzureRmVmss](/powershell/module/azurerm.compute/update-azurermvmss).</span><span class="sxs-lookup"><span data-stu-id="d3eb3-155">You can then manually increase or decrease hello number of virtual machines in hello scale set with [Update-AzureRmVmss](/powershell/module/azurerm.compute/update-azurermvmss).</span></span> <span data-ttu-id="d3eb3-156">Hello che segue viene impostato il numero di hello di macchine virtuali la scala impostata troppo*5*:</span><span class="sxs-lookup"><span data-stu-id="d3eb3-156">hello following example sets hello number of VMs in your scale set too*5*:</span></span>

```powershell
# Get current scale set
$scaleset = Get-AzureRmVmss `
  -ResourceGroupName myResourceGroupScaleSet `
  -VMScaleSetName myScaleSet

# Set and update hello capacity of your scale set
$scaleset.sku.capacity = 5
Update-AzureRmVmss -ResourceGroupName myResourceGroupScaleSet `
    -Name myScaleSet `
    -VirtualMachineScaleSet $scaleset
```

<span data-ttu-id="d3eb3-157">Se accetta alcuni hello tooupdate di minuti specificato numero di istanze in set di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="d3eb3-157">If takes a few minutes tooupdate hello specified number of instances in your scale set.</span></span>


### <a name="configure-autoscale-rules"></a><span data-ttu-id="d3eb3-158">Configurare le regole di scalabilità automatica</span><span class="sxs-lookup"><span data-stu-id="d3eb3-158">Configure autoscale rules</span></span>
<span data-ttu-id="d3eb3-159">Anziché imposta manualmente il numero di hello di istanze di ridimensionamento la scala, definire le regole di scalabilità automatica.</span><span class="sxs-lookup"><span data-stu-id="d3eb3-159">Rather than manually scaling hello number of instances in your scale set, you define autoscale rules.</span></span> <span data-ttu-id="d3eb3-160">Queste regole consentono il monitoraggio hello istanze la scala è impostata e rispondono di conseguenza, in base alle metriche e alle soglie definite.</span><span class="sxs-lookup"><span data-stu-id="d3eb3-160">These rules monitor hello instances in your scale set and respond accordingly based on metrics and thresholds you define.</span></span> <span data-ttu-id="d3eb3-161">Hello di esempio seguente consente una scalabilità orizzontale numero hello di istanze di uno quando carico hello medio della CPU è maggiore di 60% in un periodo di 5 minuti.</span><span class="sxs-lookup"><span data-stu-id="d3eb3-161">hello following example scales out hello number of instances by one when hello average CPU load is greater than 60% over a 5 minute period.</span></span> <span data-ttu-id="d3eb3-162">Se il carico della CPU Media hello quindi scende sotto il 30% in un periodo di 5 minuti, le istanze di hello vengono ridimensionate da un'istanza:</span><span class="sxs-lookup"><span data-stu-id="d3eb3-162">If hello average CPU load then drops below 30% over a 5 minute period, hello instances are scaled in by one instance:</span></span>

```powershell
# Define your scale set information
$mySubscriptionId = (Get-AzureRmSubscription).Id
$myResourceGroup = "myResourceGroupScaleSet"
$myScaleSet = "myScaleSet"
$myLocation = "East US"

# Create a scale up rule tooincrease hello number instances after 60% average CPU usage exceeded for a 5 minute period
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

# Create a scale down rule toodecrease hello number of instances after 30% average CPU usage over a 5 minute period
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

# Apply hello autoscale rules
Add-AzureRmAutoscaleSetting `
  -Location $myLocation `
  -Name "autosetting" `
  -ResourceGroup $myResourceGroup `
  -TargetResourceId /subscriptions/$mySubscriptionId/resourceGroups/$myResourceGroup/providers/Microsoft.Compute/virtualMachineScaleSets/$myScaleSet `
  -AutoscaleProfiles $myScaleProfile
```


## <a name="next-steps"></a><span data-ttu-id="d3eb3-163">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d3eb3-163">Next steps</span></span>
<span data-ttu-id="d3eb3-164">In questa esercitazione è stato creato un set di scalabilità di macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="d3eb3-164">In this tutorial, you created a virtual machine scale set.</span></span> <span data-ttu-id="d3eb3-165">Si è appreso come:</span><span class="sxs-lookup"><span data-stu-id="d3eb3-165">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="d3eb3-166">Utilizzare toodefine estensione Script personalizzata hello un tooscale del sito IIS</span><span class="sxs-lookup"><span data-stu-id="d3eb3-166">Use hello Custom Script Extension toodefine an IIS site tooscale</span></span>
> * <span data-ttu-id="d3eb3-167">Creare un bilanciamento del carico per il set di scalabilità</span><span class="sxs-lookup"><span data-stu-id="d3eb3-167">Create a load balancer for your scale set</span></span>
> * <span data-ttu-id="d3eb3-168">Creare un set di scalabilità di macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="d3eb3-168">Create a virtual machine scale set</span></span>
> * <span data-ttu-id="d3eb3-169">Aumentare o diminuire il numero di hello di istanze in un set di scalabilità</span><span class="sxs-lookup"><span data-stu-id="d3eb3-169">Increase or decrease hello number of instances in a scale set</span></span>
> * <span data-ttu-id="d3eb3-170">Creare regole di scalabilità automatica</span><span class="sxs-lookup"><span data-stu-id="d3eb3-170">Create autoscale rules</span></span>

<span data-ttu-id="d3eb3-171">Spostare toolearn esercitazione successiva toohello ulteriori informazioni su concetti per le macchine virtuali di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="d3eb3-171">Advance toohello next tutorial toolearn more about load balancing concepts for virtual machines.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d3eb3-172">Bilanciare il carico di macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="d3eb3-172">Load balance virtual machines</span></span>](tutorial-load-balancer.md)
