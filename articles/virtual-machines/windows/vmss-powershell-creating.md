---
title: "scalabilità della macchina virtuale aaaCreating imposta utilizzando i cmdlet di PowerShell | Documenti Microsoft"
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
ms.openlocfilehash: 7979be367d04c904b60d78849c1b751a52cc8caf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="creating-virtual-machine-scale-sets-using-powershell-cmdlets"></a><span data-ttu-id="58168-103">Creazione di set di scalabilità di macchine virtuali con i cmdlet di PowerShell</span><span class="sxs-lookup"><span data-stu-id="58168-103">Creating Virtual Machine Scale Sets using PowerShell cmdlets</span></span>
<span data-ttu-id="58168-104">Questo articolo viene illustrato un esempio di come toocreate un scalabilità della macchina virtuale impostare (VMSS).</span><span class="sxs-lookup"><span data-stu-id="58168-104">This article walks through an example of how toocreate a Virtual Machine scale set (VMSS).</span></span> <span data-ttu-id="58168-105">Crea un set di scalabilità di tre nodi, con la rete e la risorsa di archiviazione associate.</span><span class="sxs-lookup"><span data-stu-id="58168-105">It creates a scale set of three nodes, with associated Networking and Storage.</span></span>

## <a name="first-steps"></a><span data-ttu-id="58168-106">Primi passaggi</span><span class="sxs-lookup"><span data-stu-id="58168-106">First Steps</span></span>
<span data-ttu-id="58168-107">Verificare che si dispone di hello più recente di Azure PowerShell modulo necessari toomaintain toomake di avere i cmdlet di PowerShell hello e creare set di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="58168-107">Ensure you have hello latest Azure PowerShell module installed, toomake sure you have hello PowerShell commandlets needed toomaintain, and create scale sets.</span></span>
<span data-ttu-id="58168-108">Passare a strumenti da riga di comando toohello [qui](http://aka.ms/webpi-azps) per hello moduli di Azure più recenti disponibili.</span><span class="sxs-lookup"><span data-stu-id="58168-108">Go toohello command line tools [here](http://aka.ms/webpi-azps) for hello latest available Azure Modules.</span></span>

<span data-ttu-id="58168-109">toofind VMSS correlati cmdlet, usare la stringa di ricerca hello \*VMSS\*.</span><span class="sxs-lookup"><span data-stu-id="58168-109">toofind VMSS related commandlets, use hello search string \*VMSS\*.</span></span> <span data-ttu-id="58168-110">Ad esempio _gcm *vmss*_</span><span class="sxs-lookup"><span data-stu-id="58168-110">For example, _gcm *vmss*_</span></span>

## <a name="creating-a-vmss"></a><span data-ttu-id="58168-111">Creazione di un set di scalabilità di macchina virtuale (VMSS)</span><span class="sxs-lookup"><span data-stu-id="58168-111">Creating a VMSS</span></span>
#### <a name="create-resource-group"></a><span data-ttu-id="58168-112">Crea gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="58168-112">Create Resource Group</span></span>
```
$loc = 'westus';
$rgname = 'mynewrgwu';
  New-AzureRmResourceGroup -Name $rgname -Location $loc -Force;
```

### <a name="create-networking-vnet--subnet"></a><span data-ttu-id="58168-113">Creare la rete (rete virtuale/subnet)</span><span class="sxs-lookup"><span data-stu-id="58168-113">Create Networking (VNET / Subnet)</span></span>
#### <a name="subnet-specification"></a><span data-ttu-id="58168-114">Specifica della subnet</span><span class="sxs-lookup"><span data-stu-id="58168-114">Subnet Specification</span></span>
```
$subnetName = 'websubnet'
  $subnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix "10.0.0.0/24";
```

#### <a name="vnet-specification"></a><span data-ttu-id="58168-115">Specifica della rete virtuale</span><span class="sxs-lookup"><span data-stu-id="58168-115">VNET Specification</span></span>
```
$vnet = New-AzureRmVirtualNetwork -Force -Name ('vnet' + $rgname) -ResourceGroupName $rgname -Location $loc -AddressPrefix "10.0.0.0/16" -Subnet $subnet;
$vnet = Get-AzureRmVirtualNetwork -Name ('vnet' + $rgname) -ResourceGroupName $rgname;

# In this case assume hello new subnet is hello only one
$subnetId = $vnet.Subnets[0].Id;
```

#### <a name="create-public-ip-resource-tooallow-external-access"></a><span data-ttu-id="58168-116">Creare una risorsa IP pubblica tooAllow accesso esterno</span><span class="sxs-lookup"><span data-stu-id="58168-116">Create Public IP Resource tooAllow External Access</span></span>
<span data-ttu-id="58168-117">Questo sarà associato toohello bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="58168-117">This will be bound toohello Load Balancer.</span></span>

```
$pubip = New-AzureRmPublicIpAddress -Force -Name ('pubip' + $rgname) -ResourceGroupName $rgname -Location $loc -AllocationMethod Dynamic -DomainNameLabel ('pubip' + $rgname);
$pubip = Get-AzureRmPublicIpAddress -Name ('pubip' + $rgname) -ResourceGroupName $rgname;
```

#### <a name="create-load-balancer"></a><span data-ttu-id="58168-118">Crea servizio di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="58168-118">Create Load Balancer</span></span>
```
$frontendName = 'fe' + $rgname
$backendAddressPoolName = 'bepool' + $rgname
$probeName = 'vmssprobe' + $rgname
$inboundNatPoolName = 'innatpool' + $rgname
$lbruleName = 'lbrule' + $rgname
$lbName = 'vmsslb' + $rgname

# Bind Public IP tooLoad Balancer
$frontend = New-AzureRmLoadBalancerFrontendIpConfig -Name $frontendName -PublicIpAddress $pubip
```

#### <a name="configure-load-balancer"></a><span data-ttu-id="58168-119">Configurare il bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="58168-119">Configure Load Balancer</span></span>
<span data-ttu-id="58168-120">Creare la configurazione del Pool di indirizzi back-end, questo verrà condiviso da hello schede di rete di macchine virtuali hello in set di scalabilità hello.</span><span class="sxs-lookup"><span data-stu-id="58168-120">Create Backend Address Pool Config, this will be shared by hello NICs of hello VMs in hello scale set.</span></span>

```
$backendAddressPool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name $backendAddressPoolName
```

<span data-ttu-id="58168-121">Impostare la porta Probe con bilanciamento di carico, modificare le impostazioni di hello come appropriato per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="58168-121">Set Load Balanced Probe Port, change hello settings as appropriate for your application.</span></span>

```
$probe = New-AzureRmLoadBalancerProbeConfig -Name $probeName -RequestPath healthcheck.aspx -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2
```

<span data-ttu-id="58168-122">Creare un pool NAT in ingresso per la connettività indirizzato diretto (non con carico bilanciato) toohello macchine virtuali nella scala hello impostate tramite hello bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="58168-122">Create an inbound NAT pool for direct routed connectivity (not load balanced) toohello VMs in hello scale set via hello Load Balancer.</span></span> <span data-ttu-id="58168-123">Si tratta toodemonstrate tramite RDP e potrebbe non essere necessario nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="58168-123">This is toodemonstrate using RDP and may not be required in your application.</span></span>

```
$frontendpoolrangestart = 3360
$frontendpoolrangeend = 3370
$backendvmport = 3389
$inboundNatPool = New-AzureRmLoadBalancerInboundNatPoolConfig -Name $inboundNatPoolName -FrontendIPConfigurationId `
$frontend.Id -Protocol Tcp -FrontendPortRangeStart $frontendpoolrangestart -FrontendPortRangeEnd $frontendpoolrangeend -BackendPort $backendvmport;
```

<span data-ttu-id="58168-124">Creare hello regola di con bilanciamento del carico, in questo esempio viene illustrato il carico delle 80 richieste porta bilanciamento del carico, utilizzando le impostazioni di hello nei passaggi precedenti.</span><span class="sxs-lookup"><span data-stu-id="58168-124">Create hello Load Balanced Rule, this example shows load balancing port 80 requests, using hello settings from previous steps.</span></span>

```
$protocol = 'Tcp'
$feLBPort = 80
$beLBPort = 80

$lbrule = New-AzureRmLoadBalancerRuleConfig -Name $lbruleName `
-FrontendIPConfiguration $frontend -BackendAddressPool $backendAddressPool `
-Probe $probe -Protocol $protocol -FrontendPort $feLBPort -BackendPort $beLBPort `
-IdleTimeoutInMinutes 15 -EnableFloatingIP -LoadDistribution SourceIP -Verbose;
```

<span data-ttu-id="58168-125">Creare il bilanciamento del carico con la configurazione.</span><span class="sxs-lookup"><span data-stu-id="58168-125">Create Load Balancer with configuration.</span></span>

```
$actualLb = New-AzureRmLoadBalancer -Name $lbName -ResourceGroupName $rgname -Location $loc `
-FrontendIpConfiguration $frontend -BackendAddressPool $backendAddressPool `
-Probe $probe -LoadBalancingRule $lbrule -InboundNatPool $inboundNatPool -Verbose;
```

<span data-ttu-id="58168-126">Controllare le impostazioni di LB, controllare carico bilanciato porta configurazioni, si noti che non si vedranno vengono create le regole NAT in ingresso finché hello macchine virtuali nel set di scalabilità hello.</span><span class="sxs-lookup"><span data-stu-id="58168-126">Check  LB settings, check load balanced port configs, note, you will not see Inbound NAT rules until hello VMs in hello scale set are created.</span></span>

```
$expectedLb = Get-AzureRmLoadBalancer -Name $lbName -ResourceGroupName $rgname
```

##### <a name="configure-and-create-hello-scale-set"></a><span data-ttu-id="58168-127">Configurazione e set di scalabilità di hello crea</span><span class="sxs-lookup"><span data-stu-id="58168-127">Configure and Create hello scale set</span></span>
<span data-ttu-id="58168-128">Si noti che questo esempio di infrastruttura viene illustrato come distribuire tooset backup e il traffico web scala tra set di scalabilità hello ma hello immagini di macchine virtuali specificate qui non dispone dei servizi web installati.</span><span class="sxs-lookup"><span data-stu-id="58168-128">Note, this infrastructure example shows how tooset up distribute and scale web traffic across hello scale set, but hello VMs Images specified here do not have any web services installed.</span></span>

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

<span data-ttu-id="58168-129">Associare tooLoad NIC bilanciamento e Subnet</span><span class="sxs-lookup"><span data-stu-id="58168-129">Bind NIC tooLoad Balancer and Subnet</span></span>

```
$ipCfg = New-AzureRmVmssIPConfig -Name 'nic' `
-LoadBalancerInboundNatPoolsId $actualLb.InboundNatPools[0].Id `
-LoadBalancerBackendAddressPoolsId $actualLb.BackendAddressPools[0].Id `
-SubnetId $subnetId;
```

<span data-ttu-id="58168-130">Creare la configurazione del set di scalabilità</span><span class="sxs-lookup"><span data-stu-id="58168-130">Create scale set Config</span></span>

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

<span data-ttu-id="58168-131">Definire la configurazione del set di scalabilità</span><span class="sxs-lookup"><span data-stu-id="58168-131">Build scale set configuration</span></span>

```
New-AzureRmVmss -ResourceGroupName $rgname -Name $vmssName -VirtualMachineScaleSet $vmss -Verbose;
```

<span data-ttu-id="58168-132">Ora è stato creato il set di scalabilità di hello.</span><span class="sxs-lookup"><span data-stu-id="58168-132">Now you have created hello scale set.</span></span> <span data-ttu-id="58168-133">È possibile testare la connessione toohello singole macchine Virtuali tramite RDP in questo esempio:</span><span class="sxs-lookup"><span data-stu-id="58168-133">You can test connecting toohello individual VM using RDP in this example:</span></span>

```
VM0 : pubipmynewrgwu.westus.cloudapp.azure.com:3360
VM1 : pubipmynewrgwu.westus.cloudapp.azure.com:3361
VM2 : pubipmynewrgwu.westus.cloudapp.azure.com:3362
```
