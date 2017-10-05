---
title: Come bilanciare il carico delle macchine virtuali di Windows in Azure | Microsoft Docs
description: "Informazioni su come usare Azure Load Balancer per creare un'applicazione sicura e a disponibilità elevata in tre macchine virtuali di Windows"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 08/11/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: 6738d88d5a0430abaf3855dbf97a618e4c83617f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-load-balance-windows-virtual-machines-in-azure-to-create-a-highly-available-application"></a><span data-ttu-id="65e23-103">Come bilanciare il carico per le macchine virtuali di Windows in Azure per creare un'applicazione a disponibilità elevata</span><span class="sxs-lookup"><span data-stu-id="65e23-103">How to load balance Windows virtual machines in Azure to create a highly available application</span></span>
<span data-ttu-id="65e23-104">Il bilanciamento del carico offre un livello più elevato di disponibilità distribuendo le richieste in ingresso tra più macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="65e23-104">Load balancing provides a higher level of availability by spreading incoming requests across multiple virtual machines.</span></span> <span data-ttu-id="65e23-105">In questa esercitazione vengono illustrati i diversi componenti di Azure Load Balancer che distribuiscono il traffico e garantiscono una disponibilità elevata.</span><span class="sxs-lookup"><span data-stu-id="65e23-105">In this tutorial, you learn about the different components of the Azure load balancer that distribute traffic and provide high availability.</span></span> <span data-ttu-id="65e23-106">Si apprenderà come:</span><span class="sxs-lookup"><span data-stu-id="65e23-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="65e23-107">Creare un servizio di bilanciamento del carico di Azure</span><span class="sxs-lookup"><span data-stu-id="65e23-107">Create an Azure load balancer</span></span>
> * <span data-ttu-id="65e23-108">Creare un probe di integrità per il servizio di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="65e23-108">Create a load balancer health probe</span></span>
> * <span data-ttu-id="65e23-109">Creare regole del traffico di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="65e23-109">Create load balancer traffic rules</span></span>
> * <span data-ttu-id="65e23-110">Usare l'estensione dello script personalizzata per creare un sito IIS di base</span><span class="sxs-lookup"><span data-stu-id="65e23-110">Use the Custom Script Extension to create a basic IIS site</span></span>
> * <span data-ttu-id="65e23-111">Creare macchine virtuali e collegarsi a un bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="65e23-111">Create virtual machines and attach to a load balancer</span></span>
> * <span data-ttu-id="65e23-112">Visualizzare un bilanciamento del carico in azione</span><span class="sxs-lookup"><span data-stu-id="65e23-112">View a load balancer in action</span></span>
> * <span data-ttu-id="65e23-113">Aggiungere e rimuovere macchine virtuali da un bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="65e23-113">Add and remove VMs from a load balancer</span></span>

<span data-ttu-id="65e23-114">Questa esercitazione richiede il modulo Azure PowerShell 3.6 o versioni successive.</span><span class="sxs-lookup"><span data-stu-id="65e23-114">This tutorial requires the Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="65e23-115">Eseguire ` Get-Module -ListAvailable AzureRM` per trovare la versione.</span><span class="sxs-lookup"><span data-stu-id="65e23-115">Run ` Get-Module -ListAvailable AzureRM` to find the version.</span></span> <span data-ttu-id="65e23-116">Se è necessario eseguire l'aggiornamento, vedere [Installare e configurare Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="65e23-116">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>


## <a name="azure-load-balancer-overview"></a><span data-ttu-id="65e23-117">Panoramica di Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="65e23-117">Azure load balancer overview</span></span>
<span data-ttu-id="65e23-118">Azure Load Balancer è un bilanciamento del carico di livello 4 (TCP, UDP) che offre disponibilità elevata mediante la distribuzione del traffico in ingresso nelle macchine virtuali integre.</span><span class="sxs-lookup"><span data-stu-id="65e23-118">An Azure load balancer is a Layer-4 (TCP, UDP) load balancer that provides high availability by distributing incoming traffic among healthy VMs.</span></span> <span data-ttu-id="65e23-119">Un probe di integrità del bilanciamento del carico monitora una determinata porta in ogni VM e distribuisce il traffico solo a una VM operativa.</span><span class="sxs-lookup"><span data-stu-id="65e23-119">A load balancer health probe monitors a given port on each VM and only distributes traffic to an operational VM.</span></span>

<span data-ttu-id="65e23-120">Definire una configurazione IP front-end che contenga uno o più indirizzi IP pubblici.</span><span class="sxs-lookup"><span data-stu-id="65e23-120">You define a front-end IP configuration that contains one or more public IP addresses.</span></span> <span data-ttu-id="65e23-121">Questa configurazione IP front-end garantisce l'accessibilità al bilanciamento del carico e alle applicazioni tramite Internet.</span><span class="sxs-lookup"><span data-stu-id="65e23-121">This front-end IP configuration allows your load balancer and applications to be accessible over the Internet.</span></span> 

<span data-ttu-id="65e23-122">Le macchine virtuali si connettono a un bilanciamento del carico tramite la scheda di interfaccia di rete virtuale (NIC).</span><span class="sxs-lookup"><span data-stu-id="65e23-122">Virtual machines connect to a load balancer using their virtual network interface card (NIC).</span></span> <span data-ttu-id="65e23-123">Per distribuire il traffico alle macchine virtuali, è necessario che un pool di indirizzi back-end contenga gli indirizzi IP delle schede di interfaccia di rete virtuale connesse al bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="65e23-123">To distribute traffic to the VMs, a back-end address pool contains the IP addresses of the virtual (NICs) connected to the load balancer.</span></span>

<span data-ttu-id="65e23-124">Per controllare il flusso del traffico, è necessario definire le regole di bilanciamento del carico per porte e protocolli specifici che eseguono il mapping delle macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="65e23-124">To control the flow of traffic, you define load balancer rules for specific ports and protocols that map to your VMs.</span></span>


## <a name="create-azure-load-balancer"></a><span data-ttu-id="65e23-125">Creare un Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="65e23-125">Create Azure load balancer</span></span>
<span data-ttu-id="65e23-126">Questa sezione descrive dettagliatamente come creare e configurare ogni componente del bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="65e23-126">This section details how you can create and configure each component of the load balancer.</span></span> <span data-ttu-id="65e23-127">Per poter creare un servizio di bilanciamento del carico è prima necessario creare un gruppo di risorse con [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="65e23-127">Before you can create your load balancer, create a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="65e23-128">L'esempio seguente crea un gruppo di risorse denominato *myResourceGroupLoadBalancer* nella posizione *EastUS*:</span><span class="sxs-lookup"><span data-stu-id="65e23-128">The following example creates a resource group named *myResourceGroupLoadBalancer* in the *EastUS* location:</span></span>

```powershell
New-AzureRmResourceGroup `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Location EastUS
```

### <a name="create-a-public-ip-address"></a><span data-ttu-id="65e23-129">Creare un indirizzo IP pubblico</span><span class="sxs-lookup"><span data-stu-id="65e23-129">Create a public IP address</span></span>
<span data-ttu-id="65e23-130">Per accedere all'app in Internet, assegnare un indirizzo IP pubblico al servizio di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="65e23-130">To access your app on the Internet, you need a public IP address for the load balancer.</span></span> <span data-ttu-id="65e23-131">Creare un indirizzo IP pubblico con [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="65e23-131">Create a public IP address with [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress).</span></span> <span data-ttu-id="65e23-132">Nell'esempio seguente viene creato un indirizzo IP pubblico denominato *myPublicIP* nel gruppo di risorse *myResourceGroupLoadBalancer*:</span><span class="sxs-lookup"><span data-stu-id="65e23-132">The following example creates a public IP address named *myPublicIP* in the *myResourceGroupLoadBalancer* resource group:</span></span>

```powershell
$publicIP = New-AzureRmPublicIpAddress `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Location EastUS `
  -AllocationMethod Static `
  -Name myPublicIP
```

### <a name="create-a-load-balancer"></a><span data-ttu-id="65e23-133">Creare un servizio di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="65e23-133">Create a load balancer</span></span>
<span data-ttu-id="65e23-134">Creare un indirizzo IP di front-end con [New-AzureRmLoadBalancerFrontendIpConfig](/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig).</span><span class="sxs-lookup"><span data-stu-id="65e23-134">Create a frontend IP address with [New-AzureRmLoadBalancerFrontendIpConfig](/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig).</span></span> <span data-ttu-id="65e23-135">Nell'esempio seguente viene creato un indirizzo IP front-end denominato *myFrontEndPool*:</span><span class="sxs-lookup"><span data-stu-id="65e23-135">The following example creates a frontend IP address named *myFrontEndPool*:</span></span> 

```powershell
$frontendIP = New-AzureRmLoadBalancerFrontendIpConfig `
  -Name myFrontEndPool `
  -PublicIpAddress $publicIP
```

<span data-ttu-id="65e23-136">Creare un pool di indirizzi back-end con [New-AzureRmLoadBalancerBackendAddressPoolConfig](/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig).</span><span class="sxs-lookup"><span data-stu-id="65e23-136">Create a backend address pool with [New-AzureRmLoadBalancerBackendAddressPoolConfig](/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig).</span></span> <span data-ttu-id="65e23-137">L'esempio seguente crea un pool di indirizzi back-end denominato *myBackEndPool*:</span><span class="sxs-lookup"><span data-stu-id="65e23-137">The following example creates a backend address pool named *myBackEndPool*:</span></span>

```powershell
$backendPool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name myBackEndPool
```

<span data-ttu-id="65e23-138">Creare il servizio di bilanciamento del carico con [New-AzureRmLoadBalancer](/powershell/module/azurerm.network/new-azurermloadbalancer).</span><span class="sxs-lookup"><span data-stu-id="65e23-138">Now, create the load balancer with [New-AzureRmLoadBalancer](/powershell/module/azurerm.network/new-azurermloadbalancer).</span></span> <span data-ttu-id="65e23-139">Nell'esempio seguente viene creato un servizio di bilanciamento del carico denominato *myLoadBalancer* con l'indirizzo *myPublicIP*:</span><span class="sxs-lookup"><span data-stu-id="65e23-139">The following example creates a load balancer named *myLoadBalancer* using the *myPublicIP* address:</span></span>

```powershell
$lb = New-AzureRmLoadBalancer `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Name myLoadBalancer `
  -Location EastUS `
  -FrontendIpConfiguration $frontendIP `
  -BackendAddressPool $backendPool
```

### <a name="create-a-health-probe"></a><span data-ttu-id="65e23-140">Creare un probe di integrità</span><span class="sxs-lookup"><span data-stu-id="65e23-140">Create a health probe</span></span>
<span data-ttu-id="65e23-141">Per consentire al servizio di bilanciamento del carico di monitorare lo stato dell'app, si usa un probe di integrità.</span><span class="sxs-lookup"><span data-stu-id="65e23-141">To allow the load balancer to monitor the status of your app, you use a health probe.</span></span> <span data-ttu-id="65e23-142">Il probe di integrità aggiunge o rimuove in modo dinamico le VM nella rotazione del servizio di bilanciamento del carico in base alla rispettiva risposta ai controlli di integrità.</span><span class="sxs-lookup"><span data-stu-id="65e23-142">The health probe dynamically adds or removes VMs from the load balancer rotation based on their response to health checks.</span></span> <span data-ttu-id="65e23-143">Per impostazione predefinita, una VM viene rimossa dalla distribuzione del servizio di bilanciamento del carico dopo due errori consecutivi a intervalli di 15 secondi.</span><span class="sxs-lookup"><span data-stu-id="65e23-143">By default, a VM is removed from the load balancer distribution after two consecutive failures at 15-second intervals.</span></span> <span data-ttu-id="65e23-144">Un probe di integrità viene creato in base a un protocollo o una specifica pagina di controllo integrità per l'app.</span><span class="sxs-lookup"><span data-stu-id="65e23-144">You create a health probe based on a protocol or a specific health check page for your app.</span></span> 

<span data-ttu-id="65e23-145">Nell'esempio seguente viene creato un probe TCP.</span><span class="sxs-lookup"><span data-stu-id="65e23-145">The following example creates a TCP probe.</span></span> <span data-ttu-id="65e23-146">È anche possibile creare probe HTTP personalizzati per i controlli di integrità con granularità fine.</span><span class="sxs-lookup"><span data-stu-id="65e23-146">You can also create custom HTTP probes for more fine grained health checks.</span></span> <span data-ttu-id="65e23-147">Quando si usa un probe HTTP personalizzato, è necessario creare la pagina di controllo integrità, ad esempio *healthcheck.aspx*.</span><span class="sxs-lookup"><span data-stu-id="65e23-147">When using a custom HTTP probe, you must create the health check page, such as *healthcheck.aspx*.</span></span> <span data-ttu-id="65e23-148">Il probe deve restituire la risposta **HTTP 200 OK** affinché il servizio di bilanciamento del carico mantenga l'host nella rotazione.</span><span class="sxs-lookup"><span data-stu-id="65e23-148">The probe must return an **HTTP 200 OK** response for the load balancer to keep the host in rotation.</span></span>

<span data-ttu-id="65e23-149">Per creare un probe integrità con TCP, usare [Add-AzureRmLoadBalancerProbeConfig](/powershell/module/azurerm.network/add-azurermloadbalancerprobeconfig).</span><span class="sxs-lookup"><span data-stu-id="65e23-149">To create a TCP health probe, you use [Add-AzureRmLoadBalancerProbeConfig](/powershell/module/azurerm.network/add-azurermloadbalancerprobeconfig).</span></span> <span data-ttu-id="65e23-150">Nell'esempio seguente viene creato un probe di integrità denominato *myHealthProbe* che monitora ogni VM:</span><span class="sxs-lookup"><span data-stu-id="65e23-150">The following example creates a health probe named *myHealthProbe* that monitors each VM:</span></span>

```powershell
Add-AzureRmLoadBalancerProbeConfig `
  -Name myHealthProbe `
  -LoadBalancer $lb `
  -Protocol tcp `
  -Port 80 `
  -IntervalInSeconds 15 `
  -ProbeCount 2
```

<span data-ttu-id="65e23-151">Creare il servizio di bilanciamento del carico con [Set-AzureRmLoadBalancer](/powershell/module/azurerm.network/set-azurermloadbalancer):</span><span class="sxs-lookup"><span data-stu-id="65e23-151">Update the load balancer with [Set-AzureRmLoadBalancer](/powershell/module/azurerm.network/set-azurermloadbalancer):</span></span>

```powershell
Set-AzureRmLoadBalancer -LoadBalancer $lb
```

### <a name="create-a-load-balancer-rule"></a><span data-ttu-id="65e23-152">Creare una regola di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="65e23-152">Create a load balancer rule</span></span>
<span data-ttu-id="65e23-153">Una regola di bilanciamento del carico consente di definire come il traffico verrà distribuito alle VM.</span><span class="sxs-lookup"><span data-stu-id="65e23-153">A load balancer rule is used to define how traffic is distributed to the VMs.</span></span> <span data-ttu-id="65e23-154">Definire la configurazione IP front-end per il traffico in ingresso e il pool IP di back-end affinché riceva il traffico, insieme alla porta di origine e di destinazione necessaria.</span><span class="sxs-lookup"><span data-stu-id="65e23-154">You define the front-end IP configuration for the incoming traffic and the back-end IP pool to receive the traffic, along with the required source and destination port.</span></span> <span data-ttu-id="65e23-155">Per assicurarsi che solo le macchine virtuali integre ricevano il traffico, è necessario anche definire il probe di integrità da usare.</span><span class="sxs-lookup"><span data-stu-id="65e23-155">To make sure only healthy VMs receive traffic, you also define the health probe to use.</span></span>

<span data-ttu-id="65e23-156">Creare una regola di bilanciamento del carico con [Add-AzureRmLoadBalancerRuleConfig](/powershell/module/azurerm.network/add-azurermloadbalancerruleconfig).</span><span class="sxs-lookup"><span data-stu-id="65e23-156">Create a load balancer rule with [Add-AzureRmLoadBalancerRuleConfig](/powershell/module/azurerm.network/add-azurermloadbalancerruleconfig).</span></span> <span data-ttu-id="65e23-157">Nell'esempio seguente viene creata una regola di bilanciamento del carico denominata *myLoadBalancerRule* e il traffico viene bilanciato sulla porta *80*:</span><span class="sxs-lookup"><span data-stu-id="65e23-157">The following example creates a load balancer rule named *myLoadBalancerRule* and balances traffic on port *80*:</span></span>

```powershell
$probe = Get-AzureRmLoadBalancerProbeConfig -LoadBalancer $lb -Name myHealthProbe

Add-AzureRmLoadBalancerRuleConfig `
  -Name myLoadBalancerRule `
  -LoadBalancer $lb `
  -FrontendIpConfiguration $lb.FrontendIpConfigurations[0] `
  -BackendAddressPool $lb.BackendAddressPools[0] `
  -Protocol Tcp `
  -FrontendPort 80 `
  -BackendPort 80 `
  -Probe $probe
```

<span data-ttu-id="65e23-158">Creare il servizio di bilanciamento del carico con [Set-AzureRmLoadBalancer](/powershell/module/azurerm.network/set-azurermloadbalancer):</span><span class="sxs-lookup"><span data-stu-id="65e23-158">Update the load balancer with [Set-AzureRmLoadBalancer](/powershell/module/azurerm.network/set-azurermloadbalancer):</span></span>

```powershell
Set-AzureRmLoadBalancer -LoadBalancer $lb
```


## <a name="configure-virtual-network"></a><span data-ttu-id="65e23-159">Configurare la rete virtuale</span><span class="sxs-lookup"><span data-stu-id="65e23-159">Configure virtual network</span></span>
<span data-ttu-id="65e23-160">Prima di distribuire alcune macchine virtuali e testare il servizio di bilanciamento, creare le risorse di rete virtuale di supporto.</span><span class="sxs-lookup"><span data-stu-id="65e23-160">Before you deploy some VMs and can test your balancer, create the supporting virtual network resources.</span></span> <span data-ttu-id="65e23-161">Per altre informazioni sulle reti virtuali, vedere l'esercitazione [Gestire le reti virtuali di Azure](tutorial-virtual-network.md).</span><span class="sxs-lookup"><span data-stu-id="65e23-161">For more information about virtual networks, see the [Manage Azure Virtual Networks](tutorial-virtual-network.md) tutorial.</span></span>

### <a name="create-network-resources"></a><span data-ttu-id="65e23-162">Creare risorse di rete</span><span class="sxs-lookup"><span data-stu-id="65e23-162">Create network resources</span></span>
<span data-ttu-id="65e23-163">Creare una rete virtuale con [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork).</span><span class="sxs-lookup"><span data-stu-id="65e23-163">Create a virtual network with [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork).</span></span> <span data-ttu-id="65e23-164">Nell'esempio seguente viene creata una rete virtuale denominata *myVnet* con una subnet denominata *mySubnet*:</span><span class="sxs-lookup"><span data-stu-id="65e23-164">The following example creates a virtual network named *myVnet* with *mySubnet*:</span></span>

```powershell
# Create subnet config
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
  -Name mySubnet `
  -AddressPrefix 192.168.1.0/24

# Create the virtual network
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Location EastUS `
  -Name myVnet `
  -AddressPrefix 192.168.0.0/16 `
  -Subnet $subnetConfig
```

<span data-ttu-id="65e23-165">Creare una regola per il gruppo di sicurezza di rete con [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig), quindi creare un gruppo di sicurezza di rete con [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup).</span><span class="sxs-lookup"><span data-stu-id="65e23-165">Create a network security group rule with [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig), then create a network security group with [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup).</span></span> <span data-ttu-id="65e23-166">Aggiungere il gruppo di sicurezza di rete alla subnet con [Set-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig) e quindi aggiornare la rete virtuale con [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork).</span><span class="sxs-lookup"><span data-stu-id="65e23-166">Add the network security group to the subnet with [Set-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig) and then update the virtual network with [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork).</span></span> 

<span data-ttu-id="65e23-167">Nell'esempio seguente viene creata una regola del gruppo di sicurezza di rete denominata *myNetworkSecurityGroup* che viene applicata a *mySubnet*:</span><span class="sxs-lookup"><span data-stu-id="65e23-167">The following example creates a network security group rule named *myNetworkSecurityGroup* and applies it to *mySubnet*:</span></span>

```powershell
# Create security rule config
$nsgRule = New-AzureRmNetworkSecurityRuleConfig `
  -Name myNetworkSecurityGroupRule `
  -Protocol Tcp `
  -Direction Inbound `
  -Priority 1001 `
  -SourceAddressPrefix * `
  -SourcePortRange * `
  -DestinationAddressPrefix * `
  -DestinationPortRange 80 `
  -Access Allow

# Create the network security group
$nsg = New-AzureRmNetworkSecurityGroup `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Location EastUS `
  -Name myNetworkSecurityGroup `
  -SecurityRules $nsgRule

# Apply the network security group to a subnet
Set-AzureRmVirtualNetworkSubnetConfig `
  -VirtualNetwork $vnet `
  -Name mySubnet `
  -NetworkSecurityGroup $nsg `
  -AddressPrefix 192.168.1.0/24

# Update the virtual network
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
```

<span data-ttu-id="65e23-168">Vengono create schede di interfaccia di rete virtuale con [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface).</span><span class="sxs-lookup"><span data-stu-id="65e23-168">Virtual NICs are created with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface).</span></span> <span data-ttu-id="65e23-169">L'esempio seguente crea tre schede di interfaccia di rete virtuali,</span><span class="sxs-lookup"><span data-stu-id="65e23-169">The following example creates three virtual NICs.</span></span> <span data-ttu-id="65e23-170">Una scheda di interfaccia di rete virtuale per ogni VM creata per l'app nei passaggi successivi.</span><span class="sxs-lookup"><span data-stu-id="65e23-170">(One virtual NIC for each VM you create for your app in the following steps).</span></span> <span data-ttu-id="65e23-171">È possibile creare altre schede di interfaccia di rete virtuale e macchine virtuali in qualsiasi momento e aggiungerle al bilanciamento del carico:</span><span class="sxs-lookup"><span data-stu-id="65e23-171">You can create additional virtual NICs and VMs at any time and add them to the load balancer:</span></span>

```powershell
for ($i=1; $i -le 3; $i++)
{
   New-AzureRmNetworkInterface `
     -ResourceGroupName myResourceGroupLoadBalancer `
     -Name myNic$i `
     -Location EastUS `
     -Subnet $vnet.Subnets[0] `
     -LoadBalancerBackendAddressPool $lb.BackendAddressPools[0]
}
```

## <a name="create-virtual-machines"></a><span data-ttu-id="65e23-172">Creare macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="65e23-172">Create virtual machines</span></span>
<span data-ttu-id="65e23-173">Per aumentare la disponibilità elevata dell'app, posizionare le macchine virtuali in un set di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="65e23-173">To improve the high availability of your app, place your VMs in an availability set.</span></span>

<span data-ttu-id="65e23-174">Creare un set di disponibilità con [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset).</span><span class="sxs-lookup"><span data-stu-id="65e23-174">Create an availability set with [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset).</span></span> <span data-ttu-id="65e23-175">Nell'esempio seguente viene creato un set di disponibilità denominato *myAvailabilitySet*:</span><span class="sxs-lookup"><span data-stu-id="65e23-175">The following example creates an availability set named *myAvailabilitySet*:</span></span>

```powershell
$availabilitySet = New-AzureRmAvailabilitySet `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Name myAvailabilitySet `
  -Location EastUS `
  -Managed `
  -PlatformFaultDomainCount 3 `
  -PlatformUpdateDomainCount 2
```

<span data-ttu-id="65e23-176">Impostare nome utente e password dell'amministratore delle macchine virtuali con il comando [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span><span class="sxs-lookup"><span data-stu-id="65e23-176">Set an administrator username and password for the VMs with [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="65e23-177">A questo punto è possibile creare le macchine virtuale con [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="65e23-177">Now you can create the VMs with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span> <span data-ttu-id="65e23-178">L'esempio seguente crea tre macchine virtuali:</span><span class="sxs-lookup"><span data-stu-id="65e23-178">The following example creates three VMs:</span></span>

```powershell
for ($i=1; $i -le 3; $i++)
{
  $vm = New-AzureRmVMConfig `
    -VMName myVM$i `
    -VMSize Standard_D1 `
    -AvailabilitySetId $availabilitySet.Id
  $vm = Set-AzureRmVMOperatingSystem `
    -VM $vm `
    -Windows `
    -ComputerName myVM$i `
    -Credential $cred `
    -ProvisionVMAgent `
    -EnableAutoUpdate
  $vm = Set-AzureRmVMSourceImage `
    -VM $vm `
    -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer `
    -Skus 2016-Datacenter `
    -Version latest
  $vm = Set-AzureRmVMOSDisk `
    -VM $vm `
    -Name myOsDisk$i `
    -DiskSizeInGB 128 `
    -CreateOption FromImage `
    -Caching ReadWrite
  $nic = Get-AzureRmNetworkInterface `
    -ResourceGroupName myResourceGroupLoadBalancer `
    -Name myNic$i
  $vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
  New-AzureRmVM `
    -ResourceGroupName myResourceGroupLoadBalancer `
    -Location EastUS `
    -VM $vm
}
```

<span data-ttu-id="65e23-179">La creazione e la configurazione di tutte e tre le VM richiedono alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="65e23-179">It takes a few minutes to create and configure all three VMs.</span></span>

### <a name="install-iis-with-custom-script-extension"></a><span data-ttu-id="65e23-180">Installare IIS con l'estensione dello script personalizzata</span><span class="sxs-lookup"><span data-stu-id="65e23-180">Install IIS with Custom Script Extension</span></span>
<span data-ttu-id="65e23-181">Nell'esercitazione precedente su [Come personalizzare una macchina virtuale di Windows](tutorial-automate-vm-deployment.md), si è appreso come automatizzare la personalizzazione della macchina virtuale con l'estensione dello script personalizzata per Windows.</span><span class="sxs-lookup"><span data-stu-id="65e23-181">In a previous tutorial on [How to customize a Windows virtual machine](tutorial-automate-vm-deployment.md), you learned how to automate VM customization with the Custom Script Extension for Windows.</span></span> <span data-ttu-id="65e23-182">È possibile usare lo stesso approccio per installare e configurare IIS nelle macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="65e23-182">You can use the same approach to install and configure IIS on your VMs.</span></span>

<span data-ttu-id="65e23-183">Usare il comando [Set-AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) per installare l'estensione dello script personalizzata.</span><span class="sxs-lookup"><span data-stu-id="65e23-183">Use [Set-AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) to install the Custom Script Extension.</span></span> <span data-ttu-id="65e23-184">L'estensione esegue `powershell Add-WindowsFeature Web-Server` per installare il server Web IIS e quindi aggiorna la pagina *Default.htm* per visualizzare il nome host della VM:</span><span class="sxs-lookup"><span data-stu-id="65e23-184">The extension runs `powershell Add-WindowsFeature Web-Server` to install the IIS webserver and then updates the *Default.htm* page to show the hostname of the VM:</span></span>

```powershell
for ($i=1; $i -le 3; $i++)
{
   Set-AzureRmVMExtension `
     -ResourceGroupName myResourceGroupLoadBalancer `
     -ExtensionName IIS `
     -VMName myVM$i `
     -Publisher Microsoft.Compute `
     -ExtensionType CustomScriptExtension `
     -TypeHandlerVersion 1.4 `
     -SettingString '{"commandToExecute":"powershell Add-WindowsFeature Web-Server; powershell Add-Content -Path \"C:\\inetpub\\wwwroot\\Default.htm\" -Value $($env:computername)"}' `
     -Location EastUS
}
```

## <a name="test-load-balancer"></a><span data-ttu-id="65e23-185">Testare il bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="65e23-185">Test load balancer</span></span>
<span data-ttu-id="65e23-186">Ottenere l'indirizzo IP pubblico del servizio di bilanciamento del carico con il comando [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="65e23-186">Obtain the public IP address of your load balancer with [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span></span> <span data-ttu-id="65e23-187">Nell'esempio seguente si ottiene l'indirizzo IP per *myPublicIP* creato in precedenza:</span><span class="sxs-lookup"><span data-stu-id="65e23-187">The following example obtains the IP address for *myPublicIP* created earlier:</span></span>

```powershell
Get-AzureRmPublicIPAddress `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Name myPublicIP | select IpAddress
```

<span data-ttu-id="65e23-188">Sarà quindi possibile immettere l'indirizzo IP pubblico in un Web browser.</span><span class="sxs-lookup"><span data-stu-id="65e23-188">You can then enter the public IP address in to a web browser.</span></span> <span data-ttu-id="65e23-189">Verrà visualizzato il sito Web, con il nome host della macchina virtuale a cui il servizio di bilanciamento del carico ha distribuito il traffico, come nell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="65e23-189">The website is displayed, including the hostname of the VM that the load balancer distributed traffic to as in the following example:</span></span>

![Esecuzione del sito Web IIS](./media/tutorial-load-balancer/running-iis-website.png)

<span data-ttu-id="65e23-191">Per verificare la distribuzione del traffico tra tutte e tre le VM che eseguono l'app da parte del servizio di bilanciamento del carico, forzare l'aggiornamento del Web browser.</span><span class="sxs-lookup"><span data-stu-id="65e23-191">To see the load balancer distribute traffic across all three VMs running your app, you can force-refresh your web browser.</span></span>


## <a name="add-and-remove-vms"></a><span data-ttu-id="65e23-192">aggiunta e rimozione di VM</span><span class="sxs-lookup"><span data-stu-id="65e23-192">Add and remove VMs</span></span>
<span data-ttu-id="65e23-193">Potrebbe essere necessario eseguire attività di manutenzione sulle VM che eseguono l'app, ad esempio per installare aggiornamenti del sistema operativo,</span><span class="sxs-lookup"><span data-stu-id="65e23-193">You may need to perform maintenance on the VMs running your app, such as installing OS updates.</span></span> <span data-ttu-id="65e23-194">oppure aggiungere altre VM per gestire un aumento del traffico verso l'app.</span><span class="sxs-lookup"><span data-stu-id="65e23-194">To deal with increased traffic to your app, you may need to add additional VMs.</span></span> <span data-ttu-id="65e23-195">Questa sezione illustra come rimuovere o aggiungere una VM nel servizio di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="65e23-195">This section shows you how to remove or add a VM from the load balancer.</span></span>

### <a name="remove-a-vm-from-the-load-balancer"></a><span data-ttu-id="65e23-196">Rimuovere una VM dal servizio di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="65e23-196">Remove a VM from the load balancer</span></span>
<span data-ttu-id="65e23-197">Ottenere la scheda di interfaccia di rete con [Get-AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface) e quindi impostare la proprietà *LoadBalancerBackendAddressPools* della scheda di interfaccia di rete virtuale su *$null*.</span><span class="sxs-lookup"><span data-stu-id="65e23-197">Get the network interface card with [Get-AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface), then set the *LoadBalancerBackendAddressPools* property of the virtual NIC to *$null*.</span></span> <span data-ttu-id="65e23-198">Infine, aggiornare la scheda di interfaccia di rete virtuale:</span><span class="sxs-lookup"><span data-stu-id="65e23-198">Finally, update the virtual NIC.:</span></span>

```powershell
$nic = Get-AzureRmNetworkInterface `
    -ResourceGroupName myResourceGroupLoadBalancer `
    -Name myNic2
$nic.Ipconfigurations[0].LoadBalancerBackendAddressPools=$null
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

<span data-ttu-id="65e23-199">Per verificare la distribuzione del traffico nelle due VM restanti che eseguono l'app da parte del servizio di bilanciamento del carico, forzare l'aggiornamento del Web browser.</span><span class="sxs-lookup"><span data-stu-id="65e23-199">To see the load balancer distribute traffic across the remaining two VMs running your app you can force-refresh your web browser.</span></span> <span data-ttu-id="65e23-200">È ora possibile eseguire attività di manutenzione sulla VM, ad esempio installare aggiornamenti del sistema operativo o eseguire un riavvio della VM.</span><span class="sxs-lookup"><span data-stu-id="65e23-200">You can now perform maintenance on the VM, such as installing OS updates or performing a VM reboot.</span></span>

### <a name="add-a-vm-to-the-load-balancer"></a><span data-ttu-id="65e23-201">Aggiungere una VM al servizio di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="65e23-201">Add a VM to the load balancer</span></span>
<span data-ttu-id="65e23-202">Dopo avere eseguito la manutenzione della VM o se è necessario espandere la capacità, impostare la proprietà *LoadBalancerBackendAddressPools* della scheda di interfaccia di rete virtuale su *BackendAddressPool* in [Get-AzureRMLoadBalancer](/powershell/module/azurerm.network/get-azurermloadbalancer):</span><span class="sxs-lookup"><span data-stu-id="65e23-202">After performing VM maintenance, or if you need to expand capacity, set the *LoadBalancerBackendAddressPools* property of the virtual NIC to the *BackendAddressPool* from [Get-AzureRMLoadBalancer](/powershell/module/azurerm.network/get-azurermloadbalancer):</span></span>

<span data-ttu-id="65e23-203">Ottenere il servizio di bilanciamento del carico:</span><span class="sxs-lookup"><span data-stu-id="65e23-203">Get the load balancer:</span></span>

```powershell
$lb = Get-AzureRMLoadBalancer `
    -ResourceGroupName myResourceGroupLoadBalancer `
    -Name myLoadBalancer 
$nic.IpConfigurations[0].LoadBalancerBackendAddressPools=$lb.BackendAddressPools[0]
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

## <a name="next-steps"></a><span data-ttu-id="65e23-204">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="65e23-204">Next steps</span></span>

<span data-ttu-id="65e23-205">In questa esercitazione viene creato un bilanciamento del carico e vengono collegate le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="65e23-205">In this tutorial, you created a load balancer and attached VMs to it.</span></span> <span data-ttu-id="65e23-206">Si è appreso come:</span><span class="sxs-lookup"><span data-stu-id="65e23-206">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="65e23-207">Creare un servizio di bilanciamento del carico di Azure</span><span class="sxs-lookup"><span data-stu-id="65e23-207">Create an Azure load balancer</span></span>
> * <span data-ttu-id="65e23-208">Creare un probe di integrità per il servizio di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="65e23-208">Create a load balancer health probe</span></span>
> * <span data-ttu-id="65e23-209">Creare regole del traffico di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="65e23-209">Create load balancer traffic rules</span></span>
> * <span data-ttu-id="65e23-210">Usare l'estensione dello script personalizzata per creare un sito IIS di base</span><span class="sxs-lookup"><span data-stu-id="65e23-210">Use the Custom Script Extension to create a basic IIS site</span></span>
> * <span data-ttu-id="65e23-211">Creare macchine virtuali e collegarsi a un bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="65e23-211">Create virtual machines and attach to a load balancer</span></span>
> * <span data-ttu-id="65e23-212">Visualizzare un bilanciamento del carico in azione</span><span class="sxs-lookup"><span data-stu-id="65e23-212">View a load balancer in action</span></span>
> * <span data-ttu-id="65e23-213">Aggiungere e rimuovere macchine virtuali da un bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="65e23-213">Add and remove VMs from a load balancer</span></span>

<span data-ttu-id="65e23-214">Passare all'esercitazione successiva per imparare a gestire la rete delle macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="65e23-214">Advance to the next tutorial to learn how to manage VM networking.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="65e23-215">Gestire le VM e le reti virtuali</span><span class="sxs-lookup"><span data-stu-id="65e23-215">Manage VMs and virtual networks</span></span>](./tutorial-virtual-network.md)
