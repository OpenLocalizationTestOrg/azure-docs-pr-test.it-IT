---
title: "Creazione di set di scalabilità di macchine virtuali con i cmdlet di PowerShell | Documentazione Microsoft"
description: "Introduzione alla creazione e alla gestione dei set di scalabilità delle macchine virtuali di Azure tramite i cmdlet di Azure PowerShell"
services: virtual-machines-windows
documentationcenter: 
author: danielsollondon
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 430d9d64-1f35-48f0-a4fd-9b69910ffa59
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/21/2017
ms.author: danielsollondon
ms.openlocfilehash: a3a36028a75d6cb7eb36277f3e2b5ab833c96a96
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="creating-virtual-machine-scale-sets-using-powershell-cmdlets"></a><span data-ttu-id="8b8fc-103">Creazione di set di scalabilità di macchine virtuali con i cmdlet di PowerShell</span><span class="sxs-lookup"><span data-stu-id="8b8fc-103">Creating Virtual Machine Scale Sets using PowerShell cmdlets</span></span>
<span data-ttu-id="8b8fc-104">Questo articolo illustra un esempio di come creare un set di scalabilità di macchine virtuali (VMSS).</span><span class="sxs-lookup"><span data-stu-id="8b8fc-104">This article walks through an example of how to create a Virtual Machine scale set (VMSS).</span></span> <span data-ttu-id="8b8fc-105">Crea un set di scalabilità di tre nodi, con la rete e la risorsa di archiviazione associate.</span><span class="sxs-lookup"><span data-stu-id="8b8fc-105">It creates a scale set of three nodes, with associated Networking and Storage.</span></span>

## <a name="first-steps"></a><span data-ttu-id="8b8fc-106">Primi passaggi</span><span class="sxs-lookup"><span data-stu-id="8b8fc-106">First Steps</span></span>
<span data-ttu-id="8b8fc-107">Assicurarsi di avere installato il modulo Azure PowerShell più recente o di avere i cmdlet di PowerShell necessari per la gestione e la creazione dei set di scalabilità di macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="8b8fc-107">Ensure you have the latest Azure PowerShell module installed, to make sure you have the PowerShell commandlets needed to maintain, and create scale sets.</span></span>
<span data-ttu-id="8b8fc-108">Passare agli strumenti della riga di comando [qui](http://aka.ms/webpi-azps) per i moduli Azure più recenti.</span><span class="sxs-lookup"><span data-stu-id="8b8fc-108">Go to the command line tools [here](http://aka.ms/webpi-azps) for the latest available Azure Modules.</span></span>

<span data-ttu-id="8b8fc-109">Per trovare i cmdlet relativi ai set di scalabilità di macchine virtuali, usare la stringa di ricerca \*VMSS\*.</span><span class="sxs-lookup"><span data-stu-id="8b8fc-109">To find VMSS related commandlets, use the search string \*VMSS\*.</span></span> <span data-ttu-id="8b8fc-110">Ad esempio _gcm *vmss*_</span><span class="sxs-lookup"><span data-stu-id="8b8fc-110">For example, _gcm *vmss*_</span></span>

## <a name="creating-a-vmss"></a><span data-ttu-id="8b8fc-111">Creazione di un set di scalabilità di macchina virtuale (VMSS)</span><span class="sxs-lookup"><span data-stu-id="8b8fc-111">Creating a VMSS</span></span>
#### <a name="create-resource-group"></a><span data-ttu-id="8b8fc-112">Crea gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="8b8fc-112">Create Resource Group</span></span>
```
$loc = 'westus';
$rgname = 'mynewrgwu';
  New-AzureRmResourceGroup -Name $rgname -Location $loc -Force;
```

### <a name="create-networking-vnet--subnet"></a><span data-ttu-id="8b8fc-113">Creare la rete (rete virtuale/subnet)</span><span class="sxs-lookup"><span data-stu-id="8b8fc-113">Create Networking (VNET / Subnet)</span></span>
#### <a name="subnet-specification"></a><span data-ttu-id="8b8fc-114">Specifica della subnet</span><span class="sxs-lookup"><span data-stu-id="8b8fc-114">Subnet Specification</span></span>
```
$subnetName = 'websubnet'
  $subnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix "10.0.0.0/24";
```

#### <a name="vnet-specification"></a><span data-ttu-id="8b8fc-115">Specifica della rete virtuale</span><span class="sxs-lookup"><span data-stu-id="8b8fc-115">VNET Specification</span></span>
```
$vnet = New-AzureRmVirtualNetwork -Force -Name ('vnet' + $rgname) -ResourceGroupName $rgname -Location $loc -AddressPrefix "10.0.0.0/16" -Subnet $subnet;
$vnet = Get-AzureRmVirtualNetwork -Name ('vnet' + $rgname) -ResourceGroupName $rgname;

# In this case assume the new subnet is the only one
$subnetId = $vnet.Subnets[0].Id;
```

#### <a name="create-public-ip-resource-to-allow-external-access"></a><span data-ttu-id="8b8fc-116">Creare la risorsa indirizzo IP pubblico per consentire l'accesso esterno</span><span class="sxs-lookup"><span data-stu-id="8b8fc-116">Create Public IP Resource to Allow External Access</span></span>
<span data-ttu-id="8b8fc-117">Questo verrà associato al bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="8b8fc-117">This will be bound to the Load Balancer.</span></span>

```
$pubip = New-AzureRmPublicIpAddress -Force -Name ('pubip' + $rgname) -ResourceGroupName $rgname -Location $loc -AllocationMethod Dynamic -DomainNameLabel ('pubip' + $rgname);
$pubip = Get-AzureRmPublicIpAddress -Name ('pubip' + $rgname) -ResourceGroupName $rgname;
```

#### <a name="create-load-balancer"></a><span data-ttu-id="8b8fc-118">Crea servizio di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="8b8fc-118">Create Load Balancer</span></span>
```
$frontendName = 'fe' + $rgname
$backendAddressPoolName = 'bepool' + $rgname
$probeName = 'vmssprobe' + $rgname
$inboundNatPoolName = 'innatpool' + $rgname
$lbruleName = 'lbrule' + $rgname
$lbName = 'vmsslb' + $rgname

# Bind Public IP to Load Balancer
$frontend = New-AzureRmLoadBalancerFrontendIpConfig -Name $frontendName -PublicIpAddress $pubip
```

#### <a name="configure-load-balancer"></a><span data-ttu-id="8b8fc-119">Configurare il bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="8b8fc-119">Configure Load Balancer</span></span>
<span data-ttu-id="8b8fc-120">Creare la configurazione del pool di indirizzi di back-end che verrà condivisa dalle schede di interfaccia di rete delle VM nel set di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="8b8fc-120">Create Backend Address Pool Config, this will be shared by the NICs of the VMs in the scale set.</span></span>

```
$backendAddressPool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name $backendAddressPoolName
```

<span data-ttu-id="8b8fc-121">Impostare la porta probe con bilanciamento del carico, modificare le impostazioni in base all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="8b8fc-121">Set Load Balanced Probe Port, change the settings as appropriate for your application.</span></span>

```
$probe = New-AzureRmLoadBalancerProbeConfig -Name $probeName -RequestPath healthcheck.aspx -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2
```

<span data-ttu-id="8b8fc-122">Creare un pool NAT in ingresso per la connettività diretta indirizzata (non con carico bilanciato) verso le VM del set di scalabilità tramite il bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="8b8fc-122">Create an inbound NAT pool for direct routed connectivity (not load balanced) to the VMs in the scale set via the Load Balancer.</span></span> <span data-ttu-id="8b8fc-123">Questo serve a dimostrare l'utilizzo di RDP e potrebbe non essere necessario nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="8b8fc-123">This is to demonstrate using RDP and may not be required in your application.</span></span>

```
$frontendpoolrangestart = 3360
$frontendpoolrangeend = 3370
$backendvmport = 3389
$inboundNatPool = New-AzureRmLoadBalancerInboundNatPoolConfig -Name $inboundNatPoolName -FrontendIPConfigurationId `
$frontend.Id -Protocol Tcp -FrontendPortRangeStart $frontendpoolrangestart -FrontendPortRangeEnd $frontendpoolrangeend -BackendPort $backendvmport;
```

<span data-ttu-id="8b8fc-124">Creare la regola con carico bilanciato. Questo esempio mostra il bilanciamento del carico delle richieste della porta 80 con le impostazioni dei passaggi precedenti.</span><span class="sxs-lookup"><span data-stu-id="8b8fc-124">Create the Load Balanced Rule, this example shows load balancing port 80 requests, using the settings from previous steps.</span></span>

```
$protocol = 'Tcp'
$feLBPort = 80
$beLBPort = 80

$lbrule = New-AzureRmLoadBalancerRuleConfig -Name $lbruleName `
-FrontendIPConfiguration $frontend -BackendAddressPool $backendAddressPool `
-Probe $probe -Protocol $protocol -FrontendPort $feLBPort -BackendPort $beLBPort `
-IdleTimeoutInMinutes 15 -EnableFloatingIP -LoadDistribution SourceIP -Verbose;
```

<span data-ttu-id="8b8fc-125">Creare il bilanciamento del carico con la configurazione.</span><span class="sxs-lookup"><span data-stu-id="8b8fc-125">Create Load Balancer with configuration.</span></span>

```
$actualLb = New-AzureRmLoadBalancer -Name $lbName -ResourceGroupName $rgname -Location $loc `
-FrontendIpConfiguration $frontend -BackendAddressPool $backendAddressPool `
-Probe $probe -LoadBalancingRule $lbrule -InboundNatPool $inboundNatPool -Verbose;
```

<span data-ttu-id="8b8fc-126">Controllare le impostazioni di bilanciamento del carico e verificare le configurazioni della porta con carico bilanciato. Si noti che non vengono visualizzate le regole NAT in ingresso fino a quando non vengono create le VM del set di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="8b8fc-126">Check  LB settings, check load balanced port configs, note, you will not see Inbound NAT rules until the VMs in the scale set are created.</span></span>

```
$expectedLb = Get-AzureRmLoadBalancer -Name $lbName -ResourceGroupName $rgname
```

##### <a name="configure-and-create-the-scale-set"></a><span data-ttu-id="8b8fc-127">Configurare e creare il set di scalabilità</span><span class="sxs-lookup"><span data-stu-id="8b8fc-127">Configure and Create the scale set</span></span>
<span data-ttu-id="8b8fc-128">Questo esempio di infrastruttura illustra come configurare, distribuire e scalare il traffico Web nel set di scalabilità, ma nelle immagini di VM specificate di seguito non sono presenti servizi Web installati.</span><span class="sxs-lookup"><span data-stu-id="8b8fc-128">Note, this infrastructure example shows how to set up distribute and scale web traffic across the scale set, but the VMs Images specified here do not have any web services installed.</span></span>

```
# specify scale set Name
$vmssName = 'vmss' + $rgname;

## specify VMSS specific details
$adminUsername = 'azadmin';
$adminPassword = "Password1234!";

$PublisherName = 'MicrosoftWindowsServer'
$Offer         = 'WindowsServer'
$Sku          = '2012-R2-Datacenter'
$Version       = 'latest'
$vmNamePrefix = 'winvmss'

###add an extension
$extname = 'BGInfo';
$publisher = 'Microsoft.Compute';
$exttype = 'BGInfo';
$extver = '2.1';
```

<span data-ttu-id="8b8fc-129">Associare NIC a bilanciamento del carico e subnet</span><span class="sxs-lookup"><span data-stu-id="8b8fc-129">Bind NIC to Load Balancer and Subnet</span></span>

```
$ipCfg = New-AzureRmVmssIPConfig -Name 'nic' `
-LoadBalancerInboundNatPoolsId $actualLb.InboundNatPools[0].Id `
-LoadBalancerBackendAddressPoolsId $actualLb.BackendAddressPools[0].Id `
-SubnetId $subnetId;
```

<span data-ttu-id="8b8fc-130">Creare la configurazione del set di scalabilità</span><span class="sxs-lookup"><span data-stu-id="8b8fc-130">Create scale set Config</span></span>

```
# Specify number of nodes
$numberofnodes = 3

$vmss = New-AzureRmVmssConfig -Location $loc -SkuCapacity $numberofnodes -SkuName 'Standard_A2' -UpgradePolicyMode 'automatic' `
    | Add-AzureRmVmssNetworkInterfaceConfiguration -Name $subnetName -Primary $true -IPConfiguration $ipCfg `
    | Set-AzureRmVmssOSProfile -ComputerNamePrefix $vmNamePrefix -AdminUsername $adminUsername -AdminPassword $adminPassword `
    | Set-AzureRmVmssStorageProfile -OsDiskCreateOption 'FromImage' -OsDiskCaching 'None' `
    -ImageReferenceOffer $Offer -ImageReferenceSku $Sku -ImageReferenceVersion $Version `
    -ImageReferencePublisher $PublisherName `
    | Add-AzureRmVmssExtension -Name $extname -Publisher $publisher -Type $exttype -TypeHandlerVersion $extver -AutoUpgradeMinorVersion $true
```

<span data-ttu-id="8b8fc-131">Definire la configurazione del set di scalabilità</span><span class="sxs-lookup"><span data-stu-id="8b8fc-131">Build scale set configuration</span></span>

```
New-AzureRmVmss -ResourceGroupName $rgname -Name $vmssName -VirtualMachineScaleSet $vmss -Verbose;
```

<span data-ttu-id="8b8fc-132">Il set di scalabilità è stato creato.</span><span class="sxs-lookup"><span data-stu-id="8b8fc-132">Now you have created the scale set.</span></span> <span data-ttu-id="8b8fc-133">In questo esempio è possibile testare la connessione alla singola macchina virtuale tramite RDP:</span><span class="sxs-lookup"><span data-stu-id="8b8fc-133">You can test connecting to the individual VM using RDP in this example:</span></span>

```
VM0 : pubipmynewrgwu.westus.cloudapp.azure.com:3360
VM1 : pubipmynewrgwu.westus.cloudapp.azure.com:3361
VM2 : pubipmynewrgwu.westus.cloudapp.azure.com:3362
```
