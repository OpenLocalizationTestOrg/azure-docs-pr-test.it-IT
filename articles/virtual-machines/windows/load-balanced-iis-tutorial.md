---
title: "Esercitazione: Creare un'applicazione a disponibilità elevata nelle VM di Azure | Microsoft Docs"
description: "Informazioni su come creare un'applicazione sicura e a disponibilità elevata in tre macchine virtuali Windows con un servizio di bilanciamento del carico in Azure"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 03/30/2017
ms.author: davidmu
ms.openlocfilehash: 4b8690a11ec0e711782a112622e1193c24292289
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="build-a-load-balanced-highly-available-application-on-windows-virtual-machines-in-azure"></a><span data-ttu-id="87ba6-103">Creare un'applicazione con un servizio di bilanciamento del carico a disponibilità elevata in macchine virtuali Windows in Azure</span><span class="sxs-lookup"><span data-stu-id="87ba6-103">Build a load balanced, highly available application on Windows virtual machines in Azure</span></span>

<span data-ttu-id="87ba6-104">In questa esercitazione viene creata un'applicazione a disponibilità elevata resiliente agli eventi di manutenzione.</span><span class="sxs-lookup"><span data-stu-id="87ba6-104">In this tutorial, you create a highly available application that is resilient to maintenance events.</span></span> <span data-ttu-id="87ba6-105">L'app usa un servizio di bilanciamento del carico, un set di disponibilità e tre macchine virtuali (VM) Windows.</span><span class="sxs-lookup"><span data-stu-id="87ba6-105">The app uses a load balancer, an availability set, and three Windows virtual machines (VMs).</span></span> <span data-ttu-id="87ba6-106">Questa esercitazione installa IIS ma può essere usata per distribuire un diverso framework applicazione sfruttando le stesse linee guida e gli stessi componenti a disponibilità elevata.</span><span class="sxs-lookup"><span data-stu-id="87ba6-106">This tutorial installs IIS, though you can use this tutorial to deploy a different application framework using the same high availability components and guidelines.</span></span> 

## <a name="step-1---azure-prerequisites"></a><span data-ttu-id="87ba6-107">Passaggio 1: Prerequisiti di Azure</span><span class="sxs-lookup"><span data-stu-id="87ba6-107">Step 1 - Azure prerequisites</span></span>

<span data-ttu-id="87ba6-108">Per completare questa esercitazione, verificare di aver installato l'ultima versione del modulo [Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="87ba6-108">To complete this tutorial, make sure that you have installed the latest [Azure PowerShell](/powershell/azure/overview) module.</span></span>

<span data-ttu-id="87ba6-109">Accedere prima alla sottoscrizione di Azure con il comando Login-AzureRmAccount e seguire le istruzioni visualizzate.</span><span class="sxs-lookup"><span data-stu-id="87ba6-109">First, log in to your Azure subscription with the Login-AzureRmAccount command and follow the on-screen directions.</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="87ba6-110">Un gruppo di risorse di Azure è un contenitore logico in cui le risorse di Azure vengono distribuite e gestite.</span><span class="sxs-lookup"><span data-stu-id="87ba6-110">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> <span data-ttu-id="87ba6-111">Per poter creare qualsiasi altra risorsa di Azure, è necessario prima creare un gruppo di risorse con [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="87ba6-111">Before you can create any other Azure resources, you need to create a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="87ba6-112">L'esempio seguente crea un gruppo di risorse denominato `myResourceGroup` nell'area `westeurope`:</span><span class="sxs-lookup"><span data-stu-id="87ba6-112">The following example creates a resource group named `myResourceGroup` in the `westeurope` region:</span></span> 

```powershell
New-AzureRmResourceGroup -ResourceGroupName myResourceGroup -Location westeurope
```

## <a name="step-2---create-availability-set"></a><span data-ttu-id="87ba6-113">Passaggio 2: Creare un set di disponibilità</span><span class="sxs-lookup"><span data-stu-id="87ba6-113">Step 2 - Create availability set</span></span>

<span data-ttu-id="87ba6-114">Le macchine virtuali possono essere create in domini logici di errore e di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="87ba6-114">Virtual machines can be created across logical fault and update domains.</span></span> <span data-ttu-id="87ba6-115">Ogni dominio logico rappresenta una parte dell'hardware del data center di Azure sottostante.</span><span class="sxs-lookup"><span data-stu-id="87ba6-115">Each logical domain represents a portion of hardware in the underlying Azure datacenter.</span></span> <span data-ttu-id="87ba6-116">Quando si creano due o più VM, le risorse di calcolo e di archiviazione vengono distribuite in tali domini.</span><span class="sxs-lookup"><span data-stu-id="87ba6-116">When you create two or more VMs, your compute and storage resources are distributed across these domains.</span></span> <span data-ttu-id="87ba6-117">Questa distribuzione assicura la disponibilità dell'app in caso di manutenzione di un componente hardware.</span><span class="sxs-lookup"><span data-stu-id="87ba6-117">This distribution maintains the availability of your app if a hardware component needs maintenance.</span></span> <span data-ttu-id="87ba6-118">I set di disponibilità consentono di definire questi domini logici di errore e di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="87ba6-118">Availability sets let you define these logical fault and update domains.</span></span>

<span data-ttu-id="87ba6-119">Creare un set di disponibilità con [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset).</span><span class="sxs-lookup"><span data-stu-id="87ba6-119">Create an availability set with [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset).</span></span> <span data-ttu-id="87ba6-120">Nell'esempio seguente viene creato un set di disponibilità chiamato `myAvailabilitySet`:</span><span class="sxs-lookup"><span data-stu-id="87ba6-120">The following example creates an availability set named `myAvailabilitySet`:</span></span>

```powershell
$availabilitySet = New-AzureRmAvailabilitySet `
  -ResourceGroupName myResourceGroup `
  -Name myAvailabilitySet `
  -Location westeurope `
  -Managed `
  -PlatformFaultDomainCount 3 `
  -PlatformUpdateDomainCount 2
```

## <a name="step-3---create-load-balancer"></a><span data-ttu-id="87ba6-121">Passaggio 3: Creare il servizio di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="87ba6-121">Step 3 - Create load balancer</span></span>

<span data-ttu-id="87ba6-122">Un servizio di bilanciamento del carico di Azure distribuisce il traffico tra un set di VM definite usando regole di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="87ba6-122">An Azure load balancer distributes traffic across a set of defined VMs using load balancer rules.</span></span> <span data-ttu-id="87ba6-123">Un probe di integrità monitora una determinata porta in ogni VM e distribuisce il traffico solo a una VM operativa.</span><span class="sxs-lookup"><span data-stu-id="87ba6-123">A health probe monitors a given port on each VM and only distributes traffic to an operational VM.</span></span>

### <a name="create-public-ip-address"></a><span data-ttu-id="87ba6-124">Creare un indirizzo IP pubblico</span><span class="sxs-lookup"><span data-stu-id="87ba6-124">Create public IP address</span></span>

<span data-ttu-id="87ba6-125">Per accedere all'app in Internet, assegnare un indirizzo IP pubblico al servizio di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="87ba6-125">To access your app on the Internet, assign a public IP address to the load balancer.</span></span> <span data-ttu-id="87ba6-126">Creare un indirizzo IP pubblico con [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="87ba6-126">Create a public IP address with [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress).</span></span> <span data-ttu-id="87ba6-127">L'esempio seguente crea un indirizzo IP pubblico denominato `myPublicIP`:</span><span class="sxs-lookup"><span data-stu-id="87ba6-127">The following example creates a public IP address named `myPublicIP`:</span></span>

```powershell
$pip = New-AzureRmPublicIpAddress `
  -ResourceGroupName myResourceGroup `
  -Location westeurope `
  -AllocationMethod Static `
  -Name myPublicIP
```

### <a name="create-load-balancer"></a><span data-ttu-id="87ba6-128">Creare un servizio di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="87ba6-128">Create load balancer</span></span>

<span data-ttu-id="87ba6-129">Creare un indirizzo IP di front-end con [New-AzureRmLoadBalancerFrontendIpConfig](/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig).</span><span class="sxs-lookup"><span data-stu-id="87ba6-129">Create a frontend IP address with [New-AzureRmLoadBalancerFrontendIpConfig](/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig).</span></span> <span data-ttu-id="87ba6-130">L'esempio seguente crea un indirizzo IP front-end denominato `myFrontEndPool`:</span><span class="sxs-lookup"><span data-stu-id="87ba6-130">The following example creates a frontend IP address named `myFrontEndPool`:</span></span> 

```powershell
$frontendIP = New-AzureRmLoadBalancerFrontendIpConfig -Name myFrontEndPool -PublicIpAddress $pip
```

<span data-ttu-id="87ba6-131">Creare un pool di indirizzi back-end con [New-AzureRmLoadBalancerBackendAddressPoolConfig](/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig).</span><span class="sxs-lookup"><span data-stu-id="87ba6-131">Create a backend address pool with [New-AzureRmLoadBalancerBackendAddressPoolConfig](/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig).</span></span> <span data-ttu-id="87ba6-132">L'esempio seguente crea un pool di indirizzi IP back-end denominato `myBackEndPool`:</span><span class="sxs-lookup"><span data-stu-id="87ba6-132">The following example creates a backend address pool named `myBackEndPool`:</span></span>

```powershell
$backendPool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name myBackEndPool
```

<span data-ttu-id="87ba6-133">Creare il servizio di bilanciamento del carico con [New-AzureRmLoadBalancer](/powershell/module/azurerm.network/new-azurermloadbalancer).</span><span class="sxs-lookup"><span data-stu-id="87ba6-133">Now, create the load balancer with [New-AzureRmLoadBalancer](/powershell/module/azurerm.network/new-azurermloadbalancer).</span></span> <span data-ttu-id="87ba6-134">L'esempio seguente crea un servizio di bilanciamento del carico denominato `myLoadBalancer` con l'indirizzo `myPublicIP`:</span><span class="sxs-lookup"><span data-stu-id="87ba6-134">The following example creates a load balancer named `myLoadBalancer` using the `myPublicIP` address:</span></span>

```powershell
$lb = New-AzureRmLoadBalancer `
  -ResourceGroupName myResourceGroup `
  -Name myLoadBalancer `
  -Location westeurope `
  -FrontendIpConfiguration $frontendIP `
  -BackendAddressPool $backendPool
```

### <a name="create-health-probe"></a><span data-ttu-id="87ba6-135">Creare un probe integrità</span><span class="sxs-lookup"><span data-stu-id="87ba6-135">Create health probe</span></span>

<span data-ttu-id="87ba6-136">Per consentire al servizio di bilanciamento del carico di monitorare lo stato dell'app, si usa un probe di integrità.</span><span class="sxs-lookup"><span data-stu-id="87ba6-136">To allow the load balancer to monitor the status of your app, you use a health probe.</span></span> <span data-ttu-id="87ba6-137">Il probe di integrità aggiunge o rimuove in modo dinamico le VM nella rotazione del servizio di bilanciamento del carico in base alla rispettiva risposta ai controlli di integrità.</span><span class="sxs-lookup"><span data-stu-id="87ba6-137">The health probe dynamically adds or removes VMs from the load balancer rotation based on their response to health checks.</span></span> <span data-ttu-id="87ba6-138">Per impostazione predefinita, una VM viene rimossa dalla distribuzione del servizio di bilanciamento del carico dopo due errori consecutivi a intervalli di 15 secondi.</span><span class="sxs-lookup"><span data-stu-id="87ba6-138">By default, a VM is removed from the load balancer distribution after two consecutive failures at 15-second intervals.</span></span>

<span data-ttu-id="87ba6-139">Creare un probe integrità con [Add-AzureRmLoadBalancerProbeConfig](/powershell/module/azurerm.network/add-azurermloadbalancerprobeconfig).</span><span class="sxs-lookup"><span data-stu-id="87ba6-139">Create a health probe with [Add-AzureRmLoadBalancerProbeConfig](/powershell/module/azurerm.network/add-azurermloadbalancerprobeconfig).</span></span> <span data-ttu-id="87ba6-140">L'esempio seguente crea un probe di integrità denominato `myHealthProbe` che monitora ogni VM:</span><span class="sxs-lookup"><span data-stu-id="87ba6-140">The following example creates a health probe named `myHealthProbe` that monitors each VM:</span></span>

```powershell
Add-AzureRmLoadBalancerProbeConfig -Name myHealthProbe `
  -LoadBalancer $lb `
  -Protocol tcp `
  -Port 80 `
  -IntervalInSeconds 15 `
  -ProbeCount 2
```

### <a name="create-load-balancer-rule"></a><span data-ttu-id="87ba6-141">Creare le regole del bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="87ba6-141">Create load balancer rule</span></span>

<span data-ttu-id="87ba6-142">Una regola di bilanciamento del carico consente di definire come il traffico verrà distribuito alle VM.</span><span class="sxs-lookup"><span data-stu-id="87ba6-142">A load balancer rule is used to define how traffic is distributed to the VMs.</span></span>

<span data-ttu-id="87ba6-143">Creare una regola di bilanciamento del carico con [Add-AzureRmLoadBalancerRuleConfig](/powershell/module/azurerm.network/add-azurermloadbalancerruleconfig).</span><span class="sxs-lookup"><span data-stu-id="87ba6-143">Create a load balancer rule with [Add-AzureRmLoadBalancerRuleConfig](/powershell/module/azurerm.network/add-azurermloadbalancerruleconfig).</span></span> <span data-ttu-id="87ba6-144">L'esempio seguente crea una regola di bilanciamento del carico denominata `myLoadBalancerRule` e bilancia il traffico sulla porta `80`:</span><span class="sxs-lookup"><span data-stu-id="87ba6-144">The following example creates a load balancer rule named `myLoadBalancerRule` and balances traffic on port `80`:</span></span>

```powershell
Add-AzureRmLoadBalancerRuleConfig -Name myLoadBalancerRule `
  -LoadBalancer $lb `
  -FrontendIpConfiguration $lb.FrontendIpConfigurations[0] `
  -BackendAddressPool $lb.BackendAddressPools[0] `
  -Protocol Tcp `
  -FrontendPort 80 `
  -BackendPort 80
```

<span data-ttu-id="87ba6-145">Creare il servizio di bilanciamento del carico con [Set-AzureRmLoadBalancer](/powershell/module/azurerm.network/set-azurermloadbalancer):</span><span class="sxs-lookup"><span data-stu-id="87ba6-145">Update the load balancer with [Set-AzureRmLoadBalancer](/powershell/module/azurerm.network/set-azurermloadbalancer):</span></span>

```powershell
Set-AzureRmLoadBalancer -LoadBalancer $lb
```

## <a name="step-4---configure-networking"></a><span data-ttu-id="87ba6-146">Passaggio 4: Configurare la rete</span><span class="sxs-lookup"><span data-stu-id="87ba6-146">Step 4 - Configure networking</span></span>

<span data-ttu-id="87ba6-147">Ogni VM ha una o più schede di interfaccia di rete (NIC) virtuali per la connessione a una rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="87ba6-147">Each VM has one or more virtual network interface cards (NICs) that connect to a virtual network.</span></span> <span data-ttu-id="87ba6-148">Tale rete virtuale è protetta in modo da filtrare il traffico in base alle regole di accesso definite.</span><span class="sxs-lookup"><span data-stu-id="87ba6-148">This virtual network is secured to filter traffic based on defined access rules.</span></span>

### <a name="create-virtual-network"></a><span data-ttu-id="87ba6-149">Creare una rete virtuale</span><span class="sxs-lookup"><span data-stu-id="87ba6-149">Create virtual network</span></span>

<span data-ttu-id="87ba6-150">Per prima cosa, configurare una subnet con [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig).</span><span class="sxs-lookup"><span data-stu-id="87ba6-150">First, configure a subnet with [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig).</span></span> <span data-ttu-id="87ba6-151">Nell'esempio seguente viene creata una subnet denominata `mySubnet`:</span><span class="sxs-lookup"><span data-stu-id="87ba6-151">The following example creates a subnet named `mySubnet`:</span></span>

```powershell
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name mySubnet -AddressPrefix 192.168.1.0/24
```

<span data-ttu-id="87ba6-152">Per fornire la connettività di rete alle macchine virtuali, creare una rete virtuale con [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork).</span><span class="sxs-lookup"><span data-stu-id="87ba6-152">To provide network connectivity to your VMs, create a virtual network with [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork).</span></span> <span data-ttu-id="87ba6-153">L'esempio seguente crea una rete virtuale denominata `myVnet` con `mySubnet`:</span><span class="sxs-lookup"><span data-stu-id="87ba6-153">The following example creates a virtual network named `myVnet` with `mySubnet`:</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName myResourceGroup `
  -Location westeurope `
  -Name myVnet `
  -AddressPrefix 192.168.0.0/16 `
  -Subnet $subnetConfig
```

### <a name="configure-network-security"></a><span data-ttu-id="87ba6-154">Configurare la sicurezza di rete</span><span class="sxs-lookup"><span data-stu-id="87ba6-154">Configure network security</span></span>

<span data-ttu-id="87ba6-155">Un [gruppo di sicurezza di rete](../../virtual-network/virtual-networks-nsg.md) di Azure consente di controllare il traffico in ingresso e in uscita per una o più macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="87ba6-155">An Azure [network security group](../../virtual-network/virtual-networks-nsg.md) (NSG) controls inbound and outbound traffic for one or many virtual machines.</span></span> <span data-ttu-id="87ba6-156">Le regole di un gruppo di sicurezza di rete consentono o impediscono il traffico di rete su una porta specifica o un intervallo di porte.</span><span class="sxs-lookup"><span data-stu-id="87ba6-156">Network security group rules allow or deny network traffic on a specific port or port range.</span></span> <span data-ttu-id="87ba6-157">Queste regole possono includere un prefisso dell'indirizzo di origine, in modo che solo il traffico proveniente da un'origine specificata possa comunicare con una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="87ba6-157">These rules can also include a source address prefix so that only traffic originating at a predefined source can communicate with a virtual machine.</span></span>

<span data-ttu-id="87ba6-158">Per consentire al traffico Web di raggiungere l'app, creare una regola del gruppo di sicurezza di rete con [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig).</span><span class="sxs-lookup"><span data-stu-id="87ba6-158">To allow web traffic to reach your app, create a network security group rule with [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig).</span></span> <span data-ttu-id="87ba6-159">L'esempio seguente crea una regola del gruppo di sicurezza di rete denominata `myNetworkSecurityGroupRule`:</span><span class="sxs-lookup"><span data-stu-id="87ba6-159">The following example creates a network security group rule named `myNetworkSecurityGroupRule`:</span></span>

```powershell
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
```

<span data-ttu-id="87ba6-160">Creare un gruppo di sicurezza di rete con [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup).</span><span class="sxs-lookup"><span data-stu-id="87ba6-160">Create a network security group with [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup).</span></span> <span data-ttu-id="87ba6-161">L'esempio seguente crea un gruppo di sicurezza di rete denominato `myNetworkSecurityGroup`:</span><span class="sxs-lookup"><span data-stu-id="87ba6-161">The following example creates an NSG named `myNetworkSecurityGroup`:</span></span>

```powershell
$nsg = New-AzureRmNetworkSecurityGroup `
  -ResourceGroupName myResourceGroup `
  -Location westeurope `
  -Name myNetworkSecurityGroup `
  -SecurityRules $nsgRule
```

<span data-ttu-id="87ba6-162">Aggiungere il gruppo di sicurezza di rete alla subnet con [Set-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig):</span><span class="sxs-lookup"><span data-stu-id="87ba6-162">Add the network security group to the subnet with [Set-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig):</span></span>

```powershell
Set-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet `
  -Name mySubnet `
  -NetworkSecurityGroup $nsg `
  -AddressPrefix 192.168.1.0/24
```

<span data-ttu-id="87ba6-163">Aggiornare la rete virtuale con [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork):</span><span class="sxs-lookup"><span data-stu-id="87ba6-163">Update the virtual network with [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork):</span></span>

```powershell
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
```

### <a name="create-virtual-network-interface-cards"></a><span data-ttu-id="87ba6-164">Creare le schede di interfaccia di rete virtuali</span><span class="sxs-lookup"><span data-stu-id="87ba6-164">Create virtual network interface cards</span></span>

<span data-ttu-id="87ba6-165">Per il funzionamento dei servizi di bilanciamento del carico viene usata la risorsa NIC virtuale anziché la VM effettiva.</span><span class="sxs-lookup"><span data-stu-id="87ba6-165">Load balancers function with the virtual NIC resource rather than the actual VM.</span></span> <span data-ttu-id="87ba6-166">La scheda di interfaccia di rete virtuale è connessa al servizio di bilanciamento del carico e quindi collegata a una VM.</span><span class="sxs-lookup"><span data-stu-id="87ba6-166">The virtual NIC is connected to the load balancer, and then attached to a VM.</span></span>

<span data-ttu-id="87ba6-167">Creare una scheda di interfaccia di rete virtuale con [New AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface).</span><span class="sxs-lookup"><span data-stu-id="87ba6-167">Create a virtual NIC with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface).</span></span> <span data-ttu-id="87ba6-168">L'esempio seguente crea tre schede di interfaccia di rete virtuali,</span><span class="sxs-lookup"><span data-stu-id="87ba6-168">The following example creates three virtual NICs.</span></span> <span data-ttu-id="87ba6-169">una per ogni VM creata per l'app nei passaggi successivi:</span><span class="sxs-lookup"><span data-stu-id="87ba6-169">(One virtual NIC for each VM you create for your app in the following steps):</span></span>


```powershell
for ($i=1; $i -le 3; $i++)
{
   New-AzureRmNetworkInterface -ResourceGroupName myResourceGroup `
     -Name myNic$i `
     -Location westeurope `
     -Subnet $vnet.Subnets[0] `
     -LoadBalancerBackendAddressPool $lb.BackendAddressPools[0]
}

```

## <a name="step-5---create-virtual-machines"></a><span data-ttu-id="87ba6-170">Passaggio 5 - Creare le macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="87ba6-170">Step 5 - Create virtual machines</span></span>

<span data-ttu-id="87ba6-171">Dopo aver implementato tutti i componenti sottostanti, è possibile creare VM a disponibilità elevata per eseguire l'app.</span><span class="sxs-lookup"><span data-stu-id="87ba6-171">With all the underlying components in place, you can now create highly available VMs to run your app.</span></span> 

<span data-ttu-id="87ba6-172">Ottenere il nome utente e la password necessari per l'account amministratore nella macchina virtuale con [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span><span class="sxs-lookup"><span data-stu-id="87ba6-172">Get the username and password needed for the administrator account on the virtual machine with [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="87ba6-173">Creare le macchine virtuali con [New-AzureRmVMConfig](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/new-azurermvmconfig), [Set-AzureRmVMOperatingSystem](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmoperatingsystem), [Set-AzureRmVMSourceImage](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmsourceimage), [Set-AzureRmVMOSDisk](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmosdisk), [Add-AzureRmVMNetworkInterface](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/add-azurermvmnetworkinterface) e [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="87ba6-173">Create the VMs with [New-AzureRmVMConfig](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/new-azurermvmconfig), [Set-AzureRmVMOperatingSystem](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmoperatingsystem), [Set-AzureRmVMSourceImage](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmsourceimage), [Set-AzureRmVMOSDisk](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmosdisk), [Add-AzureRmVMNetworkInterface](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/add-azurermvmnetworkinterface), and [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span> <span data-ttu-id="87ba6-174">L'esempio seguente crea tre macchine virtuali:</span><span class="sxs-lookup"><span data-stu-id="87ba6-174">The following example creates three VMs:</span></span>

```powershell
for ($i=1; $i -le 3; $i++)
{
   $vm = New-AzureRmVMConfig -VMName myVM$i -VMSize Standard_D1 -AvailabilitySetId $availabilitySet.Id
   $vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName myVM$i -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
   $vm = Set-AzureRmVMSourceImage -VM $vm -PublisherName MicrosoftWindowsServer -Offer WindowsServer -Skus 2016-Datacenter -Version latest
   $vm = Set-AzureRmVMOSDisk -VM $vm -Name myOsDisk$i -StorageAccountType StandardLRS -DiskSizeInGB 128 -CreateOption FromImage -Caching ReadWrite
   $nic = Get-AzureRmNetworkInterface -ResourceGroupName myResourceGroup -Name myNic$i
   $vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
   New-AzureRmVM -ResourceGroupName myResourceGroup -Location westeurope -VM $vm
}

```

<span data-ttu-id="87ba6-175">La creazione e la configurazione di tutte e tre le macchine virtuali richiedono vari minuti.</span><span class="sxs-lookup"><span data-stu-id="87ba6-175">It takes several minutes to create and configure all three VMs.</span></span> <span data-ttu-id="87ba6-176">Il probe di integrità del servizio di bilanciamento del carico rileva quando l'app è in esecuzione in ogni VM.</span><span class="sxs-lookup"><span data-stu-id="87ba6-176">The load balancer health probe automatically detects when the app is running on each VM.</span></span> <span data-ttu-id="87ba6-177">Quando l'app è in esecuzione, la regola di bilanciamento del carico inizia a distribuire il traffico.</span><span class="sxs-lookup"><span data-stu-id="87ba6-177">Once the app is running, the load balancer rule starts to distribute traffic.</span></span>

### <a name="install-the-app"></a><span data-ttu-id="87ba6-178">Installare l'app</span><span class="sxs-lookup"><span data-stu-id="87ba6-178">Install the app</span></span> 

<span data-ttu-id="87ba6-179">Le estensioni delle macchine virtuali di Azure vengono usate per automatizzare le attività di configurazione delle macchine virtuali, ad esempio l'installazione di applicazioni e la configurazione del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="87ba6-179">Azure virtual machine extensions are used to automate virtual machine configuration tasks such as installing applications and configuring the operating system.</span></span> <span data-ttu-id="87ba6-180">L'[estensione personalizzata dello script per Windows](./../virtual-machines-windows-extensions-customscript.md) viene usata per eseguire qualsiasi script PowerShell in una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="87ba6-180">The [custom script extension for Windows](./../virtual-machines-windows-extensions-customscript.md) is used to run any PowerShell script on the virtual machine.</span></span> <span data-ttu-id="87ba6-181">Lo script può essere salvato nell'archiviazione di Azure, in qualsiasi endpoint HTTP accessibile o incorporato nella configurazione dell'estensione dello script personalizzata.</span><span class="sxs-lookup"><span data-stu-id="87ba6-181">The script can be stored in Azure storage, any accessible HTTP endpoint, or embedded in the custom script extension configuration.</span></span> <span data-ttu-id="87ba6-182">Quando si usa l'estensione dello script personalizzata, l'agente VM di Azure gestisce l'esecuzione dello script.</span><span class="sxs-lookup"><span data-stu-id="87ba6-182">When using the custom script extension, the Azure VM agent manages the script execution.</span></span>

<span data-ttu-id="87ba6-183">Usare [AzureRmVMExtension Set](/powershell/module/azurerm.compute/set-azurermvmextension) per installare l'estensione dello script personalizzata.</span><span class="sxs-lookup"><span data-stu-id="87ba6-183">Use [Set-AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) to install the custom script extension.</span></span> <span data-ttu-id="87ba6-184">L'estensione esegue `powershell Add-WindowsFeature Web-Server` per l'installazione del server Web IIS:</span><span class="sxs-lookup"><span data-stu-id="87ba6-184">The extension runs `powershell Add-WindowsFeature Web-Server` to install the IIS webserver:</span></span>

```powershell
for ($i=1; $i -le 3; $i++)
{
   Set-AzureRmVMExtension -ResourceGroupName myResourceGroup `
     -ExtensionName IIS `
     -VMName myVM$i `
     -Publisher Microsoft.Compute `
     -ExtensionType CustomScriptExtension `
     -TypeHandlerVersion 1.4 `
     -SettingString '{"commandToExecute":"powershell Add-WindowsFeature Web-Server"}' `
     -Location westeurope
}
```

### <a name="test-your-app"></a><span data-ttu-id="87ba6-185">Test dell'app</span><span class="sxs-lookup"><span data-stu-id="87ba6-185">Test your app</span></span>

<span data-ttu-id="87ba6-186">Ottenere l'indirizzo IP pubblico del servizio di bilanciamento del carico con [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="87ba6-186">Obtain the public IP address of your load balancer with [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span></span> <span data-ttu-id="87ba6-187">L'esempio seguente ottiene l'indirizzo IP `myPublicIP` creato in precedenza:</span><span class="sxs-lookup"><span data-stu-id="87ba6-187">The following example obtains the IP address for `myPublicIP` created earlier:</span></span>

```powershell
Get-AzureRmPublicIPAddress -ResourceGroupName myResourceGroup -Name myPublicIP | select IpAddress
```

<span data-ttu-id="87ba6-188">Immettere l'indirizzo IP pubblico in un Web browser.</span><span class="sxs-lookup"><span data-stu-id="87ba6-188">Enter the public IP address in to a web browser.</span></span> <span data-ttu-id="87ba6-189">Dopo aver aggiunto la regola del gruppo di sicurezza di rete, viene visualizzato il sito Web IIS predefinito.</span><span class="sxs-lookup"><span data-stu-id="87ba6-189">With the NSG rule in place, the default IIS website is displayed.</span></span> 

![Sito IIS predefinito](media/load-balanced-iis-tutorial/iis.png)

## <a name="step-6--management-tasks"></a><span data-ttu-id="87ba6-191">Passaggio 6 - Attività di gestione</span><span class="sxs-lookup"><span data-stu-id="87ba6-191">Step 6 – Management tasks</span></span>

<span data-ttu-id="87ba6-192">Potrebbe essere necessario eseguire attività di manutenzione sulle VM che eseguono l'app, ad esempio per installare aggiornamenti del sistema operativo,</span><span class="sxs-lookup"><span data-stu-id="87ba6-192">You may need to perform maintenance on the VMs running your app, such as installing OS updates.</span></span> <span data-ttu-id="87ba6-193">oppure aggiungere altre VM per gestire un aumento del traffico verso l'app.</span><span class="sxs-lookup"><span data-stu-id="87ba6-193">To deal with increased traffic to your app, you may need to add additional VMs.</span></span> <span data-ttu-id="87ba6-194">Questa sezione illustra come rimuovere o aggiungere una VM nel servizio di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="87ba6-194">This section shows you how to remove or add a VM from the load balancer.</span></span> 

### <a name="remove-a-vm-from-the-load-balancer"></a><span data-ttu-id="87ba6-195">Rimuovere una VM dal servizio di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="87ba6-195">Remove a VM from the load balancer</span></span>

<span data-ttu-id="87ba6-196">Rimuovere una macchina virtuale dal pool di indirizzi back-end reimpostando la proprietà LoadBalancerBackendAddressPools della scheda di interfaccia di rete.</span><span class="sxs-lookup"><span data-stu-id="87ba6-196">Remove a VM from the backend address pool by resetting the LoadBalancerBackendAddressPools property of the network interface card.</span></span>

<span data-ttu-id="87ba6-197">Ottenere una scheda di interfaccia di rete con [Get-AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface):</span><span class="sxs-lookup"><span data-stu-id="87ba6-197">Get the network interface card with [Get-AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface):</span></span>

```powershell
$nic = Get-AzureRmNetworkInterface -ResourceGroupName myResourceGroup -Name myNic2
``` 

<span data-ttu-id="87ba6-198">Impostare la proprietà LoadBalancerBackendAddressPools della scheda di interfaccia di rete su $null:</span><span class="sxs-lookup"><span data-stu-id="87ba6-198">Set the LoadBalancerBackendAddressPools property of the network interface card to $null:</span></span>

```powershell
$nic.Ipconfigurations[0].LoadBalancerBackendAddressPools=$null
```

<span data-ttu-id="87ba6-199">Aggiornare la scheda di interfaccia di rete:</span><span class="sxs-lookup"><span data-stu-id="87ba6-199">Update the network interface card:</span></span>

```powershell
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

### <a name="add-a-vm-to-the-load-balancer"></a><span data-ttu-id="87ba6-200">Aggiungere una VM al servizio di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="87ba6-200">Add a VM to the load balancer</span></span>

<span data-ttu-id="87ba6-201">Al termine della manutenzione di una macchina virtuale o se è necessario espandere la capacità, aggiungere la scheda di interfaccia di rete di una macchina virtuale al pool di indirizzi back-end del servizio di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="87ba6-201">After performing VM maintenance, or if you need to expand capacity, adding the NIC of a VM to the backend address pool of the load balancer.</span></span>

<span data-ttu-id="87ba6-202">Ottenere il servizio di bilanciamento del carico:</span><span class="sxs-lookup"><span data-stu-id="87ba6-202">Get the load balancer:</span></span>

```powershell
$lb = Get-AzureRMLoadBalancer -ResourceGroupName myResourceGroup -Name myLoadBalancer 
```

<span data-ttu-id="87ba6-203">Aggiungere il pool di indirizzi back-end del servizio di bilanciamento del carico alla scheda di interfaccia di rete:</span><span class="sxs-lookup"><span data-stu-id="87ba6-203">Add the backend address pool of the load balancer to the network interface card:</span></span>

```powershell
$nic.IpConfigurations[0].LoadBalancerBackendAddressPools=$lb.BackendAddressPools[0]
```

<span data-ttu-id="87ba6-204">Aggiornare la scheda di interfaccia di rete:</span><span class="sxs-lookup"><span data-stu-id="87ba6-204">Update the network interface card:</span></span>

```powershell
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

## <a name="next-steps"></a><span data-ttu-id="87ba6-205">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="87ba6-205">Next Steps</span></span>

<span data-ttu-id="87ba6-206">Esempi: [script di esempio di PowerShell per macchine virtuali di Azure](./../virtual-machines-windows-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="87ba6-206">Samples – [Azure Virtual Machine PowerShell sample scripts](./../virtual-machines-windows-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>
