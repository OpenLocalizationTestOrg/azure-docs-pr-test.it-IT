---
title: "aaaTutorial - compilazione di applicazioni a disponibilità elevata in macchine virtuali di Azure | Documenti Microsoft"
description: "Informazioni su come toocreate un'applicazione a elevata disponibilità e sicura tra tre macchine virtuali di Windows con un bilanciamento del carico in Azure"
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
ms.openlocfilehash: f9eff96be4f3999651c4108f0334e4eaa1a39c0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-load-balanced-highly-available-application-on-windows-virtual-machines-in-azure"></a><span data-ttu-id="4ea78-103">Creare un'applicazione con un servizio di bilanciamento del carico a disponibilità elevata in macchine virtuali Windows in Azure</span><span class="sxs-lookup"><span data-stu-id="4ea78-103">Build a load balanced, highly available application on Windows virtual machines in Azure</span></span>

<span data-ttu-id="4ea78-104">In questa esercitazione è creare un'applicazione a disponibilità elevata resilienti toomaintenance eventi.</span><span class="sxs-lookup"><span data-stu-id="4ea78-104">In this tutorial, you create a highly available application that is resilient toomaintenance events.</span></span> <span data-ttu-id="4ea78-105">app Hello utilizza un bilanciamento del carico, un set di disponibilità e tre macchine virtuali di Windows (VM).</span><span class="sxs-lookup"><span data-stu-id="4ea78-105">hello app uses a load balancer, an availability set, and three Windows virtual machines (VMs).</span></span> <span data-ttu-id="4ea78-106">In questa esercitazione viene installato IIS, sebbene sia possibile utilizzare questa esercitazione toodeploy un framework di applicazioni diverso utilizzando hello linee guida e i componenti di un'elevata disponibilità stesso.</span><span class="sxs-lookup"><span data-stu-id="4ea78-106">This tutorial installs IIS, though you can use this tutorial toodeploy a different application framework using hello same high availability components and guidelines.</span></span> 

## <a name="step-1---azure-prerequisites"></a><span data-ttu-id="4ea78-107">Passaggio 1: Prerequisiti di Azure</span><span class="sxs-lookup"><span data-stu-id="4ea78-107">Step 1 - Azure prerequisites</span></span>

<span data-ttu-id="4ea78-108">toocomplete questa esercitazione, assicurarsi di avere installato più recente hello [Azure PowerShell](/powershell/azure/overview) modulo.</span><span class="sxs-lookup"><span data-stu-id="4ea78-108">toocomplete this tutorial, make sure that you have installed hello latest [Azure PowerShell](/powershell/azure/overview) module.</span></span>

<span data-ttu-id="4ea78-109">Innanzitutto, accedi tooyour sottoscrizione di Azure con il comando account di accesso AzureRmAccount hello e seguire hello le direzioni.</span><span class="sxs-lookup"><span data-stu-id="4ea78-109">First, log in tooyour Azure subscription with hello Login-AzureRmAccount command and follow hello on-screen directions.</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="4ea78-110">Un gruppo di risorse di Azure è un contenitore logico in cui le risorse di Azure vengono distribuite e gestite.</span><span class="sxs-lookup"><span data-stu-id="4ea78-110">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> <span data-ttu-id="4ea78-111">Prima di poter creare altre risorse di Azure, è necessario toocreate un gruppo di risorse con [New AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="4ea78-111">Before you can create any other Azure resources, you need toocreate a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="4ea78-112">esempio Hello crea un gruppo di risorse denominato `myResourceGroup` in hello `westeurope` area:</span><span class="sxs-lookup"><span data-stu-id="4ea78-112">hello following example creates a resource group named `myResourceGroup` in hello `westeurope` region:</span></span> 

```powershell
New-AzureRmResourceGroup -ResourceGroupName myResourceGroup -Location westeurope
```

## <a name="step-2---create-availability-set"></a><span data-ttu-id="4ea78-113">Passaggio 2: Creare un set di disponibilità</span><span class="sxs-lookup"><span data-stu-id="4ea78-113">Step 2 - Create availability set</span></span>

<span data-ttu-id="4ea78-114">Le macchine virtuali possono essere create in domini logici di errore e di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="4ea78-114">Virtual machines can be created across logical fault and update domains.</span></span> <span data-ttu-id="4ea78-115">Ogni dominio logico rappresenta una parte dell'hardware nel Data Center di Azure sottostante hello.</span><span class="sxs-lookup"><span data-stu-id="4ea78-115">Each logical domain represents a portion of hardware in hello underlying Azure datacenter.</span></span> <span data-ttu-id="4ea78-116">Quando si creano due o più VM, le risorse di calcolo e di archiviazione vengono distribuite in tali domini.</span><span class="sxs-lookup"><span data-stu-id="4ea78-116">When you create two or more VMs, your compute and storage resources are distributed across these domains.</span></span> <span data-ttu-id="4ea78-117">Questa distribuzione mantiene la disponibilità di hello dell'app se un componente hardware necessità di manutenzione.</span><span class="sxs-lookup"><span data-stu-id="4ea78-117">This distribution maintains hello availability of your app if a hardware component needs maintenance.</span></span> <span data-ttu-id="4ea78-118">I set di disponibilità consentono di definire questi domini logici di errore e di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="4ea78-118">Availability sets let you define these logical fault and update domains.</span></span>

<span data-ttu-id="4ea78-119">Creare un set di disponibilità con [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset).</span><span class="sxs-lookup"><span data-stu-id="4ea78-119">Create an availability set with [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset).</span></span> <span data-ttu-id="4ea78-120">esempio Hello crea un set denominato di disponibilità `myAvailabilitySet`:</span><span class="sxs-lookup"><span data-stu-id="4ea78-120">hello following example creates an availability set named `myAvailabilitySet`:</span></span>

```powershell
$availabilitySet = New-AzureRmAvailabilitySet `
  -ResourceGroupName myResourceGroup `
  -Name myAvailabilitySet `
  -Location westeurope `
  -Managed `
  -PlatformFaultDomainCount 3 `
  -PlatformUpdateDomainCount 2
```

## <a name="step-3---create-load-balancer"></a><span data-ttu-id="4ea78-121">Passaggio 3: Creare il servizio di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="4ea78-121">Step 3 - Create load balancer</span></span>

<span data-ttu-id="4ea78-122">Un servizio di bilanciamento del carico di Azure distribuisce il traffico tra un set di VM definite usando regole di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="4ea78-122">An Azure load balancer distributes traffic across a set of defined VMs using load balancer rules.</span></span> <span data-ttu-id="4ea78-123">Un probe di integrità esegue il monitoraggio di una determinata porta in ogni macchina virtuale e vengono distribuiti solo il traffico tooan operativo VM.</span><span class="sxs-lookup"><span data-stu-id="4ea78-123">A health probe monitors a given port on each VM and only distributes traffic tooan operational VM.</span></span>

### <a name="create-public-ip-address"></a><span data-ttu-id="4ea78-124">Creare un indirizzo IP pubblico</span><span class="sxs-lookup"><span data-stu-id="4ea78-124">Create public IP address</span></span>

<span data-ttu-id="4ea78-125">tooaccess l'app in hello Internet, assegnare un bilanciamento del carico toohello indirizzo IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="4ea78-125">tooaccess your app on hello Internet, assign a public IP address toohello load balancer.</span></span> <span data-ttu-id="4ea78-126">Creare un indirizzo IP pubblico con [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="4ea78-126">Create a public IP address with [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress).</span></span> <span data-ttu-id="4ea78-127">esempio Hello crea un indirizzo IP pubblico denominato `myPublicIP`:</span><span class="sxs-lookup"><span data-stu-id="4ea78-127">hello following example creates a public IP address named `myPublicIP`:</span></span>

```powershell
$pip = New-AzureRmPublicIpAddress `
  -ResourceGroupName myResourceGroup `
  -Location westeurope `
  -AllocationMethod Static `
  -Name myPublicIP
```

### <a name="create-load-balancer"></a><span data-ttu-id="4ea78-128">Creare un servizio di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="4ea78-128">Create load balancer</span></span>

<span data-ttu-id="4ea78-129">Creare un indirizzo IP di front-end con [New-AzureRmLoadBalancerFrontendIpConfig](/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig).</span><span class="sxs-lookup"><span data-stu-id="4ea78-129">Create a frontend IP address with [New-AzureRmLoadBalancerFrontendIpConfig](/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig).</span></span> <span data-ttu-id="4ea78-130">esempio Hello crea un indirizzo IP di front-end denominato `myFrontEndPool`:</span><span class="sxs-lookup"><span data-stu-id="4ea78-130">hello following example creates a frontend IP address named `myFrontEndPool`:</span></span> 

```powershell
$frontendIP = New-AzureRmLoadBalancerFrontendIpConfig -Name myFrontEndPool -PublicIpAddress $pip
```

<span data-ttu-id="4ea78-131">Creare un pool di indirizzi back-end con [New-AzureRmLoadBalancerBackendAddressPoolConfig](/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig).</span><span class="sxs-lookup"><span data-stu-id="4ea78-131">Create a backend address pool with [New-AzureRmLoadBalancerBackendAddressPoolConfig](/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig).</span></span> <span data-ttu-id="4ea78-132">esempio Hello crea un pool di indirizzi back-end denominato `myBackEndPool`:</span><span class="sxs-lookup"><span data-stu-id="4ea78-132">hello following example creates a backend address pool named `myBackEndPool`:</span></span>

```powershell
$backendPool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name myBackEndPool
```

<span data-ttu-id="4ea78-133">A questo punto, creare bilanciamento del carico hello con [New AzureRmLoadBalancer](/powershell/module/azurerm.network/new-azurermloadbalancer).</span><span class="sxs-lookup"><span data-stu-id="4ea78-133">Now, create hello load balancer with [New-AzureRmLoadBalancer](/powershell/module/azurerm.network/new-azurermloadbalancer).</span></span> <span data-ttu-id="4ea78-134">esempio Hello crea un bilanciamento del carico denominato `myLoadBalancer` utilizzando hello `myPublicIP` indirizzo:</span><span class="sxs-lookup"><span data-stu-id="4ea78-134">hello following example creates a load balancer named `myLoadBalancer` using hello `myPublicIP` address:</span></span>

```powershell
$lb = New-AzureRmLoadBalancer `
  -ResourceGroupName myResourceGroup `
  -Name myLoadBalancer `
  -Location westeurope `
  -FrontendIpConfiguration $frontendIP `
  -BackendAddressPool $backendPool
```

### <a name="create-health-probe"></a><span data-ttu-id="4ea78-135">Creare un probe integrità</span><span class="sxs-lookup"><span data-stu-id="4ea78-135">Create health probe</span></span>

<span data-ttu-id="4ea78-136">tooallow hello bilanciamento toomonitor hello stato di caricamento dell'app, utilizzare un probe di integrità.</span><span class="sxs-lookup"><span data-stu-id="4ea78-136">tooallow hello load balancer toomonitor hello status of your app, you use a health probe.</span></span> <span data-ttu-id="4ea78-137">probe di integrità Hello dinamicamente aggiunge o rimuove le macchine virtuali dalla rotazione di bilanciamento del carico hello in base alle loro controlli toohealth di risposta.</span><span class="sxs-lookup"><span data-stu-id="4ea78-137">hello health probe dynamically adds or removes VMs from hello load balancer rotation based on their response toohealth checks.</span></span> <span data-ttu-id="4ea78-138">Per impostazione predefinita, una macchina virtuale viene rimosso dalla distribuzione del servizio di bilanciamento del carico hello dopo due tentativi consecutivi non riusciti a intervalli di 15 secondi.</span><span class="sxs-lookup"><span data-stu-id="4ea78-138">By default, a VM is removed from hello load balancer distribution after two consecutive failures at 15-second intervals.</span></span>

<span data-ttu-id="4ea78-139">Creare un probe integrità con [Add-AzureRmLoadBalancerProbeConfig](/powershell/module/azurerm.network/add-azurermloadbalancerprobeconfig).</span><span class="sxs-lookup"><span data-stu-id="4ea78-139">Create a health probe with [Add-AzureRmLoadBalancerProbeConfig](/powershell/module/azurerm.network/add-azurermloadbalancerprobeconfig).</span></span> <span data-ttu-id="4ea78-140">esempio Hello crea un probe di integrità denominato `myHealthProbe` che consente di monitorare ogni macchina virtuale:</span><span class="sxs-lookup"><span data-stu-id="4ea78-140">hello following example creates a health probe named `myHealthProbe` that monitors each VM:</span></span>

```powershell
Add-AzureRmLoadBalancerProbeConfig -Name myHealthProbe `
  -LoadBalancer $lb `
  -Protocol tcp `
  -Port 80 `
  -IntervalInSeconds 15 `
  -ProbeCount 2
```

### <a name="create-load-balancer-rule"></a><span data-ttu-id="4ea78-141">Creare le regole del bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="4ea78-141">Create load balancer rule</span></span>

<span data-ttu-id="4ea78-142">Una regola di bilanciamento del carico è toodefine utilizzato come il traffico è toohello distribuita le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="4ea78-142">A load balancer rule is used toodefine how traffic is distributed toohello VMs.</span></span>

<span data-ttu-id="4ea78-143">Creare una regola di bilanciamento del carico con [Add-AzureRmLoadBalancerRuleConfig](/powershell/module/azurerm.network/add-azurermloadbalancerruleconfig).</span><span class="sxs-lookup"><span data-stu-id="4ea78-143">Create a load balancer rule with [Add-AzureRmLoadBalancerRuleConfig](/powershell/module/azurerm.network/add-azurermloadbalancerruleconfig).</span></span> <span data-ttu-id="4ea78-144">esempio Hello crea una regola di bilanciamento del carico denominata `myLoadBalancerRule` e consente di bilanciare il traffico sulla porta `80`:</span><span class="sxs-lookup"><span data-stu-id="4ea78-144">hello following example creates a load balancer rule named `myLoadBalancerRule` and balances traffic on port `80`:</span></span>

```powershell
Add-AzureRmLoadBalancerRuleConfig -Name myLoadBalancerRule `
  -LoadBalancer $lb `
  -FrontendIpConfiguration $lb.FrontendIpConfigurations[0] `
  -BackendAddressPool $lb.BackendAddressPools[0] `
  -Protocol Tcp `
  -FrontendPort 80 `
  -BackendPort 80
```

<span data-ttu-id="4ea78-145">Aggiorna bilanciamento del carico hello con [Set AzureRmLoadBalancer](/powershell/module/azurerm.network/set-azurermloadbalancer):</span><span class="sxs-lookup"><span data-stu-id="4ea78-145">Update hello load balancer with [Set-AzureRmLoadBalancer](/powershell/module/azurerm.network/set-azurermloadbalancer):</span></span>

```powershell
Set-AzureRmLoadBalancer -LoadBalancer $lb
```

## <a name="step-4---configure-networking"></a><span data-ttu-id="4ea78-146">Passaggio 4: Configurare la rete</span><span class="sxs-lookup"><span data-stu-id="4ea78-146">Step 4 - Configure networking</span></span>

<span data-ttu-id="4ea78-147">Ogni macchina virtuale ha uno o più virtuale schede di rete (NIC) che si connettono tooa di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="4ea78-147">Each VM has one or more virtual network interface cards (NICs) that connect tooa virtual network.</span></span> <span data-ttu-id="4ea78-148">Questa rete virtuale è protetta toofilter traffico in base alle regole di accesso definito.</span><span class="sxs-lookup"><span data-stu-id="4ea78-148">This virtual network is secured toofilter traffic based on defined access rules.</span></span>

### <a name="create-virtual-network"></a><span data-ttu-id="4ea78-149">Creare una rete virtuale</span><span class="sxs-lookup"><span data-stu-id="4ea78-149">Create virtual network</span></span>

<span data-ttu-id="4ea78-150">Per prima cosa, configurare una subnet con [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig).</span><span class="sxs-lookup"><span data-stu-id="4ea78-150">First, configure a subnet with [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig).</span></span> <span data-ttu-id="4ea78-151">esempio Hello crea una subnet denominata `mySubnet`:</span><span class="sxs-lookup"><span data-stu-id="4ea78-151">hello following example creates a subnet named `mySubnet`:</span></span>

```powershell
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name mySubnet -AddressPrefix 192.168.1.0/24
```

<span data-ttu-id="4ea78-152">tooyour di connettività di rete tooprovide le macchine virtuali, creare una rete virtuale con [New AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork).</span><span class="sxs-lookup"><span data-stu-id="4ea78-152">tooprovide network connectivity tooyour VMs, create a virtual network with [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork).</span></span> <span data-ttu-id="4ea78-153">esempio Hello crea una rete virtuale denominata `myVnet` con `mySubnet`:</span><span class="sxs-lookup"><span data-stu-id="4ea78-153">hello following example creates a virtual network named `myVnet` with `mySubnet`:</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName myResourceGroup `
  -Location westeurope `
  -Name myVnet `
  -AddressPrefix 192.168.0.0/16 `
  -Subnet $subnetConfig
```

### <a name="configure-network-security"></a><span data-ttu-id="4ea78-154">Configurare la sicurezza di rete</span><span class="sxs-lookup"><span data-stu-id="4ea78-154">Configure network security</span></span>

<span data-ttu-id="4ea78-155">Un [gruppo di sicurezza di rete](../../virtual-network/virtual-networks-nsg.md) di Azure consente di controllare il traffico in ingresso e in uscita per una o più macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="4ea78-155">An Azure [network security group](../../virtual-network/virtual-networks-nsg.md) (NSG) controls inbound and outbound traffic for one or many virtual machines.</span></span> <span data-ttu-id="4ea78-156">Le regole di un gruppo di sicurezza di rete consentono o impediscono il traffico di rete su una porta specifica o un intervallo di porte.</span><span class="sxs-lookup"><span data-stu-id="4ea78-156">Network security group rules allow or deny network traffic on a specific port or port range.</span></span> <span data-ttu-id="4ea78-157">Queste regole possono includere un prefisso dell'indirizzo di origine, in modo che solo il traffico proveniente da un'origine specificata possa comunicare con una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="4ea78-157">These rules can also include a source address prefix so that only traffic originating at a predefined source can communicate with a virtual machine.</span></span>

<span data-ttu-id="4ea78-158">tooallow web tooreach traffico l'app, creare una regola gruppo di sicurezza di rete con [New AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig).</span><span class="sxs-lookup"><span data-stu-id="4ea78-158">tooallow web traffic tooreach your app, create a network security group rule with [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig).</span></span> <span data-ttu-id="4ea78-159">esempio Hello crea una regola di gruppo di sicurezza di rete denominata `myNetworkSecurityGroupRule`:</span><span class="sxs-lookup"><span data-stu-id="4ea78-159">hello following example creates a network security group rule named `myNetworkSecurityGroupRule`:</span></span>

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

<span data-ttu-id="4ea78-160">Creare un gruppo di sicurezza di rete con [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup).</span><span class="sxs-lookup"><span data-stu-id="4ea78-160">Create a network security group with [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup).</span></span> <span data-ttu-id="4ea78-161">esempio Hello crea un gruppo denominato `myNetworkSecurityGroup`:</span><span class="sxs-lookup"><span data-stu-id="4ea78-161">hello following example creates an NSG named `myNetworkSecurityGroup`:</span></span>

```powershell
$nsg = New-AzureRmNetworkSecurityGroup `
  -ResourceGroupName myResourceGroup `
  -Location westeurope `
  -Name myNetworkSecurityGroup `
  -SecurityRules $nsgRule
```

<span data-ttu-id="4ea78-162">Aggiungi subnet hello rete sicurezza gruppo toohello con [Set AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig):</span><span class="sxs-lookup"><span data-stu-id="4ea78-162">Add hello network security group toohello subnet with [Set-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig):</span></span>

```powershell
Set-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet `
  -Name mySubnet `
  -NetworkSecurityGroup $nsg `
  -AddressPrefix 192.168.1.0/24
```

<span data-ttu-id="4ea78-163">Rete virtuale hello di Update con [Set AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork):</span><span class="sxs-lookup"><span data-stu-id="4ea78-163">Update hello virtual network with [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork):</span></span>

```powershell
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
```

### <a name="create-virtual-network-interface-cards"></a><span data-ttu-id="4ea78-164">Creare le schede di interfaccia di rete virtuali</span><span class="sxs-lookup"><span data-stu-id="4ea78-164">Create virtual network interface cards</span></span>

<span data-ttu-id="4ea78-165">Caricare una funzione di bilanciamento del carico con risorse di interfaccia di rete virtuale hello anziché hello VM effettivo.</span><span class="sxs-lookup"><span data-stu-id="4ea78-165">Load balancers function with hello virtual NIC resource rather than hello actual VM.</span></span> <span data-ttu-id="4ea78-166">Hello NIC virtuale è connessa toohello bilanciamento del carico e quindi collegato tooa macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="4ea78-166">hello virtual NIC is connected toohello load balancer, and then attached tooa VM.</span></span>

<span data-ttu-id="4ea78-167">Creare una scheda di interfaccia di rete virtuale con [New AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface).</span><span class="sxs-lookup"><span data-stu-id="4ea78-167">Create a virtual NIC with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface).</span></span> <span data-ttu-id="4ea78-168">Hello esempio crea tre schede di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="4ea78-168">hello following example creates three virtual NICs.</span></span> <span data-ttu-id="4ea78-169">(Una scheda di rete virtuale per ogni macchina virtuale creato per l'app in hello seguendo i passaggi):</span><span class="sxs-lookup"><span data-stu-id="4ea78-169">(One virtual NIC for each VM you create for your app in hello following steps):</span></span>


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

## <a name="step-5---create-virtual-machines"></a><span data-ttu-id="4ea78-170">Passaggio 5 - Creare le macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="4ea78-170">Step 5 - Create virtual machines</span></span>

<span data-ttu-id="4ea78-171">Con hello tutti i componenti sul posto sottostante, è ora possibile creare toorun macchine virtuali a disponibilità elevata dell'app.</span><span class="sxs-lookup"><span data-stu-id="4ea78-171">With all hello underlying components in place, you can now create highly available VMs toorun your app.</span></span> 

<span data-ttu-id="4ea78-172">Ottenere hello username e password necessari per l'account di amministratore hello nella macchina virtuale hello con [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span><span class="sxs-lookup"><span data-stu-id="4ea78-172">Get hello username and password needed for hello administrator account on hello virtual machine with [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="4ea78-173">Creare le macchine virtuali hello con [New AzureRmVMConfig](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/new-azurermvmconfig), [Set AzureRmVMOperatingSystem](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmoperatingsystem), [Set AzureRmVMSourceImage](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmsourceimage), [Set-AzureRmVMOSDisk](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmosdisk), [AzureRmVMNetworkInterface aggiungere](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/add-azurermvmnetworkinterface), e [nuova AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="4ea78-173">Create hello VMs with [New-AzureRmVMConfig](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/new-azurermvmconfig), [Set-AzureRmVMOperatingSystem](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmoperatingsystem), [Set-AzureRmVMSourceImage](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmsourceimage), [Set-AzureRmVMOSDisk](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmosdisk), [Add-AzureRmVMNetworkInterface](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/add-azurermvmnetworkinterface), and [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span> <span data-ttu-id="4ea78-174">Hello seguente esempio crea tre macchine virtuali:</span><span class="sxs-lookup"><span data-stu-id="4ea78-174">hello following example creates three VMs:</span></span>

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

<span data-ttu-id="4ea78-175">Accetta diversi minuti toocreate e configurare tutte le tre macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="4ea78-175">It takes several minutes toocreate and configure all three VMs.</span></span> <span data-ttu-id="4ea78-176">Hello probe di integrità di bilanciamento del carico rileva automaticamente quando l'applicazione hello è in esecuzione in ogni macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="4ea78-176">hello load balancer health probe automatically detects when hello app is running on each VM.</span></span> <span data-ttu-id="4ea78-177">Dopo l'applicazione hello è in esecuzione, regola di bilanciamento del carico hello avvia toodistribute traffico.</span><span class="sxs-lookup"><span data-stu-id="4ea78-177">Once hello app is running, hello load balancer rule starts toodistribute traffic.</span></span>

### <a name="install-hello-app"></a><span data-ttu-id="4ea78-178">Installare l'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="4ea78-178">Install hello app</span></span> 

<span data-ttu-id="4ea78-179">Le estensioni di macchina virtuale di Azure sono attività di configurazione macchina virtuale tooautomate utilizzato, ad esempio l'installazione di applicazioni e la configurazione del sistema operativo hello.</span><span class="sxs-lookup"><span data-stu-id="4ea78-179">Azure virtual machine extensions are used tooautomate virtual machine configuration tasks such as installing applications and configuring hello operating system.</span></span> <span data-ttu-id="4ea78-180">Hello [estensione script personalizzato per Windows](./../virtual-machines-windows-extensions-customscript.md) è toorun usato qualsiasi script di PowerShell nella macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="4ea78-180">hello [custom script extension for Windows](./../virtual-machines-windows-extensions-customscript.md) is used toorun any PowerShell script on hello virtual machine.</span></span> <span data-ttu-id="4ea78-181">script Hello può essere archiviato in archiviazione di Azure, qualsiasi endpoint HTTP accessibile, o incorporato in configurazione dell'estensione script personalizzata hello.</span><span class="sxs-lookup"><span data-stu-id="4ea78-181">hello script can be stored in Azure storage, any accessible HTTP endpoint, or embedded in hello custom script extension configuration.</span></span> <span data-ttu-id="4ea78-182">Quando si utilizza l'estensione script personalizzata hello, l'agente VM di Azure hello gestisce l'esecuzione dello script hello.</span><span class="sxs-lookup"><span data-stu-id="4ea78-182">When using hello custom script extension, hello Azure VM agent manages hello script execution.</span></span>

<span data-ttu-id="4ea78-183">Utilizzare [Set AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) tooinstall hello un'estensione personalizzata.</span><span class="sxs-lookup"><span data-stu-id="4ea78-183">Use [Set-AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) tooinstall hello custom script extension.</span></span> <span data-ttu-id="4ea78-184">Hello estensione esecuzioni `powershell Add-WindowsFeature Web-Server` server Web IIS di hello tooinstall:</span><span class="sxs-lookup"><span data-stu-id="4ea78-184">hello extension runs `powershell Add-WindowsFeature Web-Server` tooinstall hello IIS webserver:</span></span>

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

### <a name="test-your-app"></a><span data-ttu-id="4ea78-185">Test dell'app</span><span class="sxs-lookup"><span data-stu-id="4ea78-185">Test your app</span></span>

<span data-ttu-id="4ea78-186">Ottenere l'indirizzo IP pubblico di hello del servizio di bilanciamento del carico con [Get AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="4ea78-186">Obtain hello public IP address of your load balancer with [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span></span> <span data-ttu-id="4ea78-187">esempio Hello Ottiene hello di indirizzo IP per `myPublicIP` creato in precedenza:</span><span class="sxs-lookup"><span data-stu-id="4ea78-187">hello following example obtains hello IP address for `myPublicIP` created earlier:</span></span>

```powershell
Get-AzureRmPublicIPAddress -ResourceGroupName myResourceGroup -Name myPublicIP | select IpAddress
```

<span data-ttu-id="4ea78-188">Immettere l'indirizzo IP pubblico hello nel browser web tooa.</span><span class="sxs-lookup"><span data-stu-id="4ea78-188">Enter hello public IP address in tooa web browser.</span></span> <span data-ttu-id="4ea78-189">Con hello NSG regola, viene visualizzato il sito Web IIS predefinito hello.</span><span class="sxs-lookup"><span data-stu-id="4ea78-189">With hello NSG rule in place, hello default IIS website is displayed.</span></span> 

![Sito IIS predefinito](media/load-balanced-iis-tutorial/iis.png)

## <a name="step-6--management-tasks"></a><span data-ttu-id="4ea78-191">Passaggio 6 - Attività di gestione</span><span class="sxs-lookup"><span data-stu-id="4ea78-191">Step 6 – Management tasks</span></span>

<span data-ttu-id="4ea78-192">È possibile la manutenzione tooperform hello macchine virtuali in esecuzione l'app, ad esempio l'installazione di aggiornamenti del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="4ea78-192">You may need tooperform maintenance on hello VMs running your app, such as installing OS updates.</span></span> <span data-ttu-id="4ea78-193">toodeal con un aumento del traffico tooyour app, potrebbe essere necessario tooadd altre macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="4ea78-193">toodeal with increased traffic tooyour app, you may need tooadd additional VMs.</span></span> <span data-ttu-id="4ea78-194">In questa sezione illustra come tooremove o aggiungere una macchina virtuale dal servizio di bilanciamento del carico hello.</span><span class="sxs-lookup"><span data-stu-id="4ea78-194">This section shows you how tooremove or add a VM from hello load balancer.</span></span> 

### <a name="remove-a-vm-from-hello-load-balancer"></a><span data-ttu-id="4ea78-195">Rimuovere una macchina virtuale dal servizio di bilanciamento del carico hello</span><span class="sxs-lookup"><span data-stu-id="4ea78-195">Remove a VM from hello load balancer</span></span>

<span data-ttu-id="4ea78-196">Rimuovere una macchina virtuale dal pool di indirizzi back-end hello reimpostando proprietà LoadBalancerBackendAddressPools hello hello scheda di rete.</span><span class="sxs-lookup"><span data-stu-id="4ea78-196">Remove a VM from hello backend address pool by resetting hello LoadBalancerBackendAddressPools property of hello network interface card.</span></span>

<span data-ttu-id="4ea78-197">Ottenere l'interfaccia di rete di hello con [Get AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface):</span><span class="sxs-lookup"><span data-stu-id="4ea78-197">Get hello network interface card with [Get-AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface):</span></span>

```powershell
$nic = Get-AzureRmNetworkInterface -ResourceGroupName myResourceGroup -Name myNic2
``` 

<span data-ttu-id="4ea78-198">Impostare la proprietà di LoadBalancerBackendAddressPools hello della scheda di interfaccia di rete hello troppo null$:</span><span class="sxs-lookup"><span data-stu-id="4ea78-198">Set hello LoadBalancerBackendAddressPools property of hello network interface card too$null:</span></span>

```powershell
$nic.Ipconfigurations[0].LoadBalancerBackendAddressPools=$null
```

<span data-ttu-id="4ea78-199">Aggiorna scheda di interfaccia di rete hello:</span><span class="sxs-lookup"><span data-stu-id="4ea78-199">Update hello network interface card:</span></span>

```powershell
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

### <a name="add-a-vm-toohello-load-balancer"></a><span data-ttu-id="4ea78-200">Aggiungere un bilanciamento del carico VM toohello</span><span class="sxs-lookup"><span data-stu-id="4ea78-200">Add a VM toohello load balancer</span></span>

<span data-ttu-id="4ea78-201">Dopo l'esecuzione della manutenzione di macchina virtuale o se è necessario tooexpand capacità, aggiunta hello NIC del pool di indirizzi back-end toohello VM di bilanciamento del carico hello.</span><span class="sxs-lookup"><span data-stu-id="4ea78-201">After performing VM maintenance, or if you need tooexpand capacity, adding hello NIC of a VM toohello backend address pool of hello load balancer.</span></span>

<span data-ttu-id="4ea78-202">Ottieni bilanciamento del carico hello:</span><span class="sxs-lookup"><span data-stu-id="4ea78-202">Get hello load balancer:</span></span>

```powershell
$lb = Get-AzureRMLoadBalancer -ResourceGroupName myResourceGroup -Name myLoadBalancer 
```

<span data-ttu-id="4ea78-203">Aggiungere pool di indirizzi back-end hello della scheda di interfaccia di rete toohello bilanciamento di carico hello:</span><span class="sxs-lookup"><span data-stu-id="4ea78-203">Add hello backend address pool of hello load balancer toohello network interface card:</span></span>

```powershell
$nic.IpConfigurations[0].LoadBalancerBackendAddressPools=$lb.BackendAddressPools[0]
```

<span data-ttu-id="4ea78-204">Aggiorna scheda di interfaccia di rete hello:</span><span class="sxs-lookup"><span data-stu-id="4ea78-204">Update hello network interface card:</span></span>

```powershell
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

## <a name="next-steps"></a><span data-ttu-id="4ea78-205">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4ea78-205">Next Steps</span></span>

<span data-ttu-id="4ea78-206">Esempi: [script di esempio di PowerShell per macchine virtuali di Azure](./../virtual-machines-windows-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="4ea78-206">Samples – [Azure Virtual Machine PowerShell sample scripts](./../virtual-machines-windows-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>
