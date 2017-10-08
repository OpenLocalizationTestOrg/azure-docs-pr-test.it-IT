---
title: aaaHow tooload bilanciare macchine virtuali di Windows in Azure | Documenti Microsoft
description: "Informazioni su come toouse hello Azure caricare bilanciamento toocreate un'applicazione a elevata disponibilità e sicura tra tre macchine virtuali di Windows"
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
ms.openlocfilehash: bfbd6a24e90a33e60d7d4f7b0c471af5d4e71f45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooload-balance-windows-virtual-machines-in-azure-toocreate-a-highly-available-application"></a><span data-ttu-id="abc2d-103">Come tooload bilanciare macchine virtuali Windows in Azure toocreate applicazioni a disponibilità elevata</span><span class="sxs-lookup"><span data-stu-id="abc2d-103">How tooload balance Windows virtual machines in Azure toocreate a highly available application</span></span>
<span data-ttu-id="abc2d-104">Il bilanciamento del carico offre un livello più elevato di disponibilità distribuendo le richieste in ingresso tra più macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="abc2d-104">Load balancing provides a higher level of availability by spreading incoming requests across multiple virtual machines.</span></span> <span data-ttu-id="abc2d-105">In questa esercitazione apprendere hello diversi componenti del servizio di bilanciamento del carico di Azure hello che distribuisce il traffico e garantire disponibilità elevata.</span><span class="sxs-lookup"><span data-stu-id="abc2d-105">In this tutorial, you learn about hello different components of hello Azure load balancer that distribute traffic and provide high availability.</span></span> <span data-ttu-id="abc2d-106">Si apprenderà come:</span><span class="sxs-lookup"><span data-stu-id="abc2d-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="abc2d-107">Creare un servizio di bilanciamento del carico di Azure</span><span class="sxs-lookup"><span data-stu-id="abc2d-107">Create an Azure load balancer</span></span>
> * <span data-ttu-id="abc2d-108">Creare un probe di integrità per il servizio di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="abc2d-108">Create a load balancer health probe</span></span>
> * <span data-ttu-id="abc2d-109">Creare regole del traffico di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="abc2d-109">Create load balancer traffic rules</span></span>
> * <span data-ttu-id="abc2d-110">Utilizzare toocreate estensione Script personalizzata hello un sito IIS di base</span><span class="sxs-lookup"><span data-stu-id="abc2d-110">Use hello Custom Script Extension toocreate a basic IIS site</span></span>
> * <span data-ttu-id="abc2d-111">Creare macchine virtuali e collegare bilanciamento del carico tooa</span><span class="sxs-lookup"><span data-stu-id="abc2d-111">Create virtual machines and attach tooa load balancer</span></span>
> * <span data-ttu-id="abc2d-112">Visualizzare un bilanciamento del carico in azione</span><span class="sxs-lookup"><span data-stu-id="abc2d-112">View a load balancer in action</span></span>
> * <span data-ttu-id="abc2d-113">Aggiungere e rimuovere macchine virtuali da un bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="abc2d-113">Add and remove VMs from a load balancer</span></span>

<span data-ttu-id="abc2d-114">Questa esercitazione richiede hello Azure PowerShell versione 3.6 o versioni successive del modulo.</span><span class="sxs-lookup"><span data-stu-id="abc2d-114">This tutorial requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="abc2d-115">Eseguire ` Get-Module -ListAvailable AzureRM` versione hello toofind.</span><span class="sxs-lookup"><span data-stu-id="abc2d-115">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="abc2d-116">Se è necessario tooupgrade, vedere [modulo installare Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="abc2d-116">If you need tooupgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>


## <a name="azure-load-balancer-overview"></a><span data-ttu-id="abc2d-117">Panoramica di Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="abc2d-117">Azure load balancer overview</span></span>
<span data-ttu-id="abc2d-118">Azure Load Balancer è un bilanciamento del carico di livello 4 (TCP, UDP) che offre disponibilità elevata mediante la distribuzione del traffico in ingresso nelle macchine virtuali integre.</span><span class="sxs-lookup"><span data-stu-id="abc2d-118">An Azure load balancer is a Layer-4 (TCP, UDP) load balancer that provides high availability by distributing incoming traffic among healthy VMs.</span></span> <span data-ttu-id="abc2d-119">Un probe di integrità di bilanciamento del carico consente di monitorare una determinata porta in ogni macchina virtuale e vengono distribuiti solo il traffico tooan operativo VM.</span><span class="sxs-lookup"><span data-stu-id="abc2d-119">A load balancer health probe monitors a given port on each VM and only distributes traffic tooan operational VM.</span></span>

<span data-ttu-id="abc2d-120">Definire una configurazione IP front-end che contenga uno o più indirizzi IP pubblici.</span><span class="sxs-lookup"><span data-stu-id="abc2d-120">You define a front-end IP configuration that contains one or more public IP addresses.</span></span> <span data-ttu-id="abc2d-121">Questa configurazione IP front-end consente il toobe di applicazioni e del servizio di bilanciamento del carico accessibile tramite Internet hello.</span><span class="sxs-lookup"><span data-stu-id="abc2d-121">This front-end IP configuration allows your load balancer and applications toobe accessible over hello Internet.</span></span> 

<span data-ttu-id="abc2d-122">Le macchine virtuali connesse tooa bilanciamento del carico utilizzando la scheda di interfaccia di rete virtuale (NIC).</span><span class="sxs-lookup"><span data-stu-id="abc2d-122">Virtual machines connect tooa load balancer using their virtual network interface card (NIC).</span></span> <span data-ttu-id="abc2d-123">toodistribute traffico toohello macchine virtuali, un pool di indirizzi back-end contiene indirizzi IP hello di hello virtuale (NIC) connesse toohello bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="abc2d-123">toodistribute traffic toohello VMs, a back-end address pool contains hello IP addresses of hello virtual (NICs) connected toohello load balancer.</span></span>

<span data-ttu-id="abc2d-124">flusso di hello toocontrol del traffico, definire regole di bilanciamento del carico per porte specifiche e protocolli che eseguono il mapping delle macchine virtuali tooyour.</span><span class="sxs-lookup"><span data-stu-id="abc2d-124">toocontrol hello flow of traffic, you define load balancer rules for specific ports and protocols that map tooyour VMs.</span></span>


## <a name="create-azure-load-balancer"></a><span data-ttu-id="abc2d-125">Creare un Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="abc2d-125">Create Azure load balancer</span></span>
<span data-ttu-id="abc2d-126">Questa sezione descrive come è possibile creare e configurare ciascun componente del servizio di bilanciamento del carico hello.</span><span class="sxs-lookup"><span data-stu-id="abc2d-126">This section details how you can create and configure each component of hello load balancer.</span></span> <span data-ttu-id="abc2d-127">Per poter creare un servizio di bilanciamento del carico è prima necessario creare un gruppo di risorse con [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="abc2d-127">Before you can create your load balancer, create a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="abc2d-128">esempio Hello crea un gruppo di risorse denominato *myResourceGroupLoadBalancer* in hello *EastUS* percorso:</span><span class="sxs-lookup"><span data-stu-id="abc2d-128">hello following example creates a resource group named *myResourceGroupLoadBalancer* in hello *EastUS* location:</span></span>

```powershell
New-AzureRmResourceGroup `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Location EastUS
```

### <a name="create-a-public-ip-address"></a><span data-ttu-id="abc2d-129">Creare un indirizzo IP pubblico</span><span class="sxs-lookup"><span data-stu-id="abc2d-129">Create a public IP address</span></span>
<span data-ttu-id="abc2d-130">tooaccess l'app in hello Internet, è necessario un indirizzo IP pubblico di bilanciamento del carico hello.</span><span class="sxs-lookup"><span data-stu-id="abc2d-130">tooaccess your app on hello Internet, you need a public IP address for hello load balancer.</span></span> <span data-ttu-id="abc2d-131">Creare un indirizzo IP pubblico con [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="abc2d-131">Create a public IP address with [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress).</span></span> <span data-ttu-id="abc2d-132">esempio Hello crea un indirizzo IP pubblico denominato *myPublicIP* in hello *myResourceGroupLoadBalancer* gruppo di risorse:</span><span class="sxs-lookup"><span data-stu-id="abc2d-132">hello following example creates a public IP address named *myPublicIP* in hello *myResourceGroupLoadBalancer* resource group:</span></span>

```powershell
$publicIP = New-AzureRmPublicIpAddress `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Location EastUS `
  -AllocationMethod Static `
  -Name myPublicIP
```

### <a name="create-a-load-balancer"></a><span data-ttu-id="abc2d-133">Creare un servizio di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="abc2d-133">Create a load balancer</span></span>
<span data-ttu-id="abc2d-134">Creare un indirizzo IP di front-end con [New-AzureRmLoadBalancerFrontendIpConfig](/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig).</span><span class="sxs-lookup"><span data-stu-id="abc2d-134">Create a frontend IP address with [New-AzureRmLoadBalancerFrontendIpConfig](/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig).</span></span> <span data-ttu-id="abc2d-135">esempio Hello crea un indirizzo IP di front-end denominato *myFrontEndPool*:</span><span class="sxs-lookup"><span data-stu-id="abc2d-135">hello following example creates a frontend IP address named *myFrontEndPool*:</span></span> 

```powershell
$frontendIP = New-AzureRmLoadBalancerFrontendIpConfig `
  -Name myFrontEndPool `
  -PublicIpAddress $publicIP
```

<span data-ttu-id="abc2d-136">Creare un pool di indirizzi back-end con [New-AzureRmLoadBalancerBackendAddressPoolConfig](/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig).</span><span class="sxs-lookup"><span data-stu-id="abc2d-136">Create a backend address pool with [New-AzureRmLoadBalancerBackendAddressPoolConfig](/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig).</span></span> <span data-ttu-id="abc2d-137">esempio Hello crea un pool di indirizzi back-end denominato *myBackEndPool*:</span><span class="sxs-lookup"><span data-stu-id="abc2d-137">hello following example creates a backend address pool named *myBackEndPool*:</span></span>

```powershell
$backendPool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name myBackEndPool
```

<span data-ttu-id="abc2d-138">A questo punto, creare bilanciamento del carico hello con [New AzureRmLoadBalancer](/powershell/module/azurerm.network/new-azurermloadbalancer).</span><span class="sxs-lookup"><span data-stu-id="abc2d-138">Now, create hello load balancer with [New-AzureRmLoadBalancer](/powershell/module/azurerm.network/new-azurermloadbalancer).</span></span> <span data-ttu-id="abc2d-139">esempio Hello crea un bilanciamento del carico denominato *myLoadBalancer* utilizzando hello *myPublicIP* indirizzo:</span><span class="sxs-lookup"><span data-stu-id="abc2d-139">hello following example creates a load balancer named *myLoadBalancer* using hello *myPublicIP* address:</span></span>

```powershell
$lb = New-AzureRmLoadBalancer `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Name myLoadBalancer `
  -Location EastUS `
  -FrontendIpConfiguration $frontendIP `
  -BackendAddressPool $backendPool
```

### <a name="create-a-health-probe"></a><span data-ttu-id="abc2d-140">Creare un probe di integrità</span><span class="sxs-lookup"><span data-stu-id="abc2d-140">Create a health probe</span></span>
<span data-ttu-id="abc2d-141">tooallow hello bilanciamento toomonitor hello stato di caricamento dell'app, utilizzare un probe di integrità.</span><span class="sxs-lookup"><span data-stu-id="abc2d-141">tooallow hello load balancer toomonitor hello status of your app, you use a health probe.</span></span> <span data-ttu-id="abc2d-142">probe di integrità Hello dinamicamente aggiunge o rimuove le macchine virtuali dalla rotazione di bilanciamento del carico hello in base alle loro controlli toohealth di risposta.</span><span class="sxs-lookup"><span data-stu-id="abc2d-142">hello health probe dynamically adds or removes VMs from hello load balancer rotation based on their response toohealth checks.</span></span> <span data-ttu-id="abc2d-143">Per impostazione predefinita, una macchina virtuale viene rimosso dalla distribuzione del servizio di bilanciamento del carico hello dopo due tentativi consecutivi non riusciti a intervalli di 15 secondi.</span><span class="sxs-lookup"><span data-stu-id="abc2d-143">By default, a VM is removed from hello load balancer distribution after two consecutive failures at 15-second intervals.</span></span> <span data-ttu-id="abc2d-144">Un probe di integrità viene creato in base a un protocollo o una specifica pagina di controllo integrità per l'app.</span><span class="sxs-lookup"><span data-stu-id="abc2d-144">You create a health probe based on a protocol or a specific health check page for your app.</span></span> 

<span data-ttu-id="abc2d-145">Hello di esempio seguente crea un probe TCP.</span><span class="sxs-lookup"><span data-stu-id="abc2d-145">hello following example creates a TCP probe.</span></span> <span data-ttu-id="abc2d-146">È anche possibile creare probe HTTP personalizzati per i controlli di integrità con granularità fine.</span><span class="sxs-lookup"><span data-stu-id="abc2d-146">You can also create custom HTTP probes for more fine grained health checks.</span></span> <span data-ttu-id="abc2d-147">Quando si utilizza un probe HTTP personalizzato, è necessario creare pagina di controllo di integrità hello, ad esempio *healthcheck.aspx*.</span><span class="sxs-lookup"><span data-stu-id="abc2d-147">When using a custom HTTP probe, you must create hello health check page, such as *healthcheck.aspx*.</span></span> <span data-ttu-id="abc2d-148">probe Hello deve restituire un **HTTP 200 OK** risposta per l'host hello carico bilanciamento tookeep hello nella rotazione.</span><span class="sxs-lookup"><span data-stu-id="abc2d-148">hello probe must return an **HTTP 200 OK** response for hello load balancer tookeep hello host in rotation.</span></span>

<span data-ttu-id="abc2d-149">toocreate un probe di integrità TCP, utilizzare [Aggiungi AzureRmLoadBalancerProbeConfig](/powershell/module/azurerm.network/add-azurermloadbalancerprobeconfig).</span><span class="sxs-lookup"><span data-stu-id="abc2d-149">toocreate a TCP health probe, you use [Add-AzureRmLoadBalancerProbeConfig](/powershell/module/azurerm.network/add-azurermloadbalancerprobeconfig).</span></span> <span data-ttu-id="abc2d-150">esempio Hello crea un probe di integrità denominato *myHealthProbe* che consente di monitorare ogni macchina virtuale:</span><span class="sxs-lookup"><span data-stu-id="abc2d-150">hello following example creates a health probe named *myHealthProbe* that monitors each VM:</span></span>

```powershell
Add-AzureRmLoadBalancerProbeConfig `
  -Name myHealthProbe `
  -LoadBalancer $lb `
  -Protocol tcp `
  -Port 80 `
  -IntervalInSeconds 15 `
  -ProbeCount 2
```

<span data-ttu-id="abc2d-151">Aggiorna bilanciamento del carico hello con [Set AzureRmLoadBalancer](/powershell/module/azurerm.network/set-azurermloadbalancer):</span><span class="sxs-lookup"><span data-stu-id="abc2d-151">Update hello load balancer with [Set-AzureRmLoadBalancer](/powershell/module/azurerm.network/set-azurermloadbalancer):</span></span>

```powershell
Set-AzureRmLoadBalancer -LoadBalancer $lb
```

### <a name="create-a-load-balancer-rule"></a><span data-ttu-id="abc2d-152">Creare una regola di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="abc2d-152">Create a load balancer rule</span></span>
<span data-ttu-id="abc2d-153">Una regola di bilanciamento del carico è toodefine utilizzato come il traffico è toohello distribuita le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="abc2d-153">A load balancer rule is used toodefine how traffic is distributed toohello VMs.</span></span> <span data-ttu-id="abc2d-154">Definire una configurazione IP front-end di hello per il traffico in ingresso hello e hello back-end pool tooreceive hello traffico IP, con origine necessari hello e porta di destinazione.</span><span class="sxs-lookup"><span data-stu-id="abc2d-154">You define hello front-end IP configuration for hello incoming traffic and hello back-end IP pool tooreceive hello traffic, along with hello required source and destination port.</span></span> <span data-ttu-id="abc2d-155">toomake che solo le macchine virtuali integro ricevano il traffico, è inoltre definire toouse probe di integrità hello.</span><span class="sxs-lookup"><span data-stu-id="abc2d-155">toomake sure only healthy VMs receive traffic, you also define hello health probe toouse.</span></span>

<span data-ttu-id="abc2d-156">Creare una regola di bilanciamento del carico con [Add-AzureRmLoadBalancerRuleConfig](/powershell/module/azurerm.network/add-azurermloadbalancerruleconfig).</span><span class="sxs-lookup"><span data-stu-id="abc2d-156">Create a load balancer rule with [Add-AzureRmLoadBalancerRuleConfig](/powershell/module/azurerm.network/add-azurermloadbalancerruleconfig).</span></span> <span data-ttu-id="abc2d-157">esempio Hello crea una regola di bilanciamento del carico denominata *myLoadBalancerRule* e consente di bilanciare il traffico sulla porta *80*:</span><span class="sxs-lookup"><span data-stu-id="abc2d-157">hello following example creates a load balancer rule named *myLoadBalancerRule* and balances traffic on port *80*:</span></span>

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

<span data-ttu-id="abc2d-158">Aggiorna bilanciamento del carico hello con [Set AzureRmLoadBalancer](/powershell/module/azurerm.network/set-azurermloadbalancer):</span><span class="sxs-lookup"><span data-stu-id="abc2d-158">Update hello load balancer with [Set-AzureRmLoadBalancer](/powershell/module/azurerm.network/set-azurermloadbalancer):</span></span>

```powershell
Set-AzureRmLoadBalancer -LoadBalancer $lb
```


## <a name="configure-virtual-network"></a><span data-ttu-id="abc2d-159">Configurare la rete virtuale</span><span class="sxs-lookup"><span data-stu-id="abc2d-159">Configure virtual network</span></span>
<span data-ttu-id="abc2d-160">Prima di distribuire alcune macchine virtuali e possibile eseguire il servizio di bilanciamento del test, creare hello che supporta le risorse di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="abc2d-160">Before you deploy some VMs and can test your balancer, create hello supporting virtual network resources.</span></span> <span data-ttu-id="abc2d-161">Per ulteriori informazioni sulle reti virtuali, vedere hello [gestire reti virtuali di Azure](tutorial-virtual-network.md) esercitazione.</span><span class="sxs-lookup"><span data-stu-id="abc2d-161">For more information about virtual networks, see hello [Manage Azure Virtual Networks](tutorial-virtual-network.md) tutorial.</span></span>

### <a name="create-network-resources"></a><span data-ttu-id="abc2d-162">Creare risorse di rete</span><span class="sxs-lookup"><span data-stu-id="abc2d-162">Create network resources</span></span>
<span data-ttu-id="abc2d-163">Creare una rete virtuale con [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork).</span><span class="sxs-lookup"><span data-stu-id="abc2d-163">Create a virtual network with [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork).</span></span> <span data-ttu-id="abc2d-164">esempio Hello crea una rete virtuale denominata *myVnet* con *mySubnet*:</span><span class="sxs-lookup"><span data-stu-id="abc2d-164">hello following example creates a virtual network named *myVnet* with *mySubnet*:</span></span>

```powershell
# Create subnet config
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
  -Name mySubnet `
  -AddressPrefix 192.168.1.0/24

# Create hello virtual network
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Location EastUS `
  -Name myVnet `
  -AddressPrefix 192.168.0.0/16 `
  -Subnet $subnetConfig
```

<span data-ttu-id="abc2d-165">Creare una regola per il gruppo di sicurezza di rete con [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig), quindi creare un gruppo di sicurezza di rete con [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup).</span><span class="sxs-lookup"><span data-stu-id="abc2d-165">Create a network security group rule with [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig), then create a network security group with [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup).</span></span> <span data-ttu-id="abc2d-166">Aggiungi subnet hello rete sicurezza gruppo toohello con [Set AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig) e quindi aggiornare la rete virtuale di hello con [Set AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork).</span><span class="sxs-lookup"><span data-stu-id="abc2d-166">Add hello network security group toohello subnet with [Set-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig) and then update hello virtual network with [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork).</span></span> 

<span data-ttu-id="abc2d-167">esempio Hello crea una regola di gruppo di sicurezza di rete denominata *myNetworkSecurityGroup* e lo applica troppo*mySubnet*:</span><span class="sxs-lookup"><span data-stu-id="abc2d-167">hello following example creates a network security group rule named *myNetworkSecurityGroup* and applies it too*mySubnet*:</span></span>

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

# Create hello network security group
$nsg = New-AzureRmNetworkSecurityGroup `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Location EastUS `
  -Name myNetworkSecurityGroup `
  -SecurityRules $nsgRule

# Apply hello network security group tooa subnet
Set-AzureRmVirtualNetworkSubnetConfig `
  -VirtualNetwork $vnet `
  -Name mySubnet `
  -NetworkSecurityGroup $nsg `
  -AddressPrefix 192.168.1.0/24

# Update hello virtual network
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
```

<span data-ttu-id="abc2d-168">Vengono create schede di interfaccia di rete virtuale con [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface).</span><span class="sxs-lookup"><span data-stu-id="abc2d-168">Virtual NICs are created with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface).</span></span> <span data-ttu-id="abc2d-169">Hello esempio crea tre schede di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="abc2d-169">hello following example creates three virtual NICs.</span></span> <span data-ttu-id="abc2d-170">(Una scheda di rete virtuale per ogni macchina virtuale viene creato per l'app in hello seguendo i passaggi).</span><span class="sxs-lookup"><span data-stu-id="abc2d-170">(One virtual NIC for each VM you create for your app in hello following steps).</span></span> <span data-ttu-id="abc2d-171">È possibile creare macchine virtuali e schede di rete virtuali aggiuntive in qualsiasi momento e aggiungerli toohello servizio di bilanciamento del carico:</span><span class="sxs-lookup"><span data-stu-id="abc2d-171">You can create additional virtual NICs and VMs at any time and add them toohello load balancer:</span></span>

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

## <a name="create-virtual-machines"></a><span data-ttu-id="abc2d-172">Creare macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="abc2d-172">Create virtual machines</span></span>
<span data-ttu-id="abc2d-173">disponibilità elevata di hello tooimprove dell'app, posizionare le macchine virtuali in un set di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="abc2d-173">tooimprove hello high availability of your app, place your VMs in an availability set.</span></span>

<span data-ttu-id="abc2d-174">Creare un set di disponibilità con [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset).</span><span class="sxs-lookup"><span data-stu-id="abc2d-174">Create an availability set with [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset).</span></span> <span data-ttu-id="abc2d-175">esempio Hello crea un set denominato di disponibilità *myAvailabilitySet*:</span><span class="sxs-lookup"><span data-stu-id="abc2d-175">hello following example creates an availability set named *myAvailabilitySet*:</span></span>

```powershell
$availabilitySet = New-AzureRmAvailabilitySet `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Name myAvailabilitySet `
  -Location EastUS `
  -Managed `
  -PlatformFaultDomainCount 3 `
  -PlatformUpdateDomainCount 2
```

<span data-ttu-id="abc2d-176">Impostare un amministratore di nome utente e password per le macchine virtuali hello con [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span><span class="sxs-lookup"><span data-stu-id="abc2d-176">Set an administrator username and password for hello VMs with [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="abc2d-177">Ora è possibile creare le macchine virtuali hello con [New AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="abc2d-177">Now you can create hello VMs with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span> <span data-ttu-id="abc2d-178">Hello seguente esempio crea tre macchine virtuali:</span><span class="sxs-lookup"><span data-stu-id="abc2d-178">hello following example creates three VMs:</span></span>

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

<span data-ttu-id="abc2d-179">Accetta toocreate di pochi minuti e configurare tutte le tre macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="abc2d-179">It takes a few minutes toocreate and configure all three VMs.</span></span>

### <a name="install-iis-with-custom-script-extension"></a><span data-ttu-id="abc2d-180">Installare IIS con l'estensione dello script personalizzata</span><span class="sxs-lookup"><span data-stu-id="abc2d-180">Install IIS with Custom Script Extension</span></span>
<span data-ttu-id="abc2d-181">Nell'esercitazione precedente su [come una macchina virtuale Windows toocustomize](tutorial-automate-vm-deployment.md), si è appreso come tooautomate personalizzazione con hello Custom Script di estensione per Windows.</span><span class="sxs-lookup"><span data-stu-id="abc2d-181">In a previous tutorial on [How toocustomize a Windows virtual machine](tutorial-automate-vm-deployment.md), you learned how tooautomate VM customization with hello Custom Script Extension for Windows.</span></span> <span data-ttu-id="abc2d-182">È possibile utilizzare hello stesso approccio tooinstall e configurare IIS sulle macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="abc2d-182">You can use hello same approach tooinstall and configure IIS on your VMs.</span></span>

<span data-ttu-id="abc2d-183">Utilizzare [Set AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) tooinstall hello estensione Script personalizzata.</span><span class="sxs-lookup"><span data-stu-id="abc2d-183">Use [Set-AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) tooinstall hello Custom Script Extension.</span></span> <span data-ttu-id="abc2d-184">Hello estensione esecuzioni `powershell Add-WindowsFeature Web-Server` tooinstall hello server Web IIS e quindi hello aggiornamenti *Default.htm* pagina tooshow hello hostname di hello VM:</span><span class="sxs-lookup"><span data-stu-id="abc2d-184">hello extension runs `powershell Add-WindowsFeature Web-Server` tooinstall hello IIS webserver and then updates hello *Default.htm* page tooshow hello hostname of hello VM:</span></span>

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

## <a name="test-load-balancer"></a><span data-ttu-id="abc2d-185">Testare il bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="abc2d-185">Test load balancer</span></span>
<span data-ttu-id="abc2d-186">Ottenere l'indirizzo IP pubblico di hello del servizio di bilanciamento del carico con [Get AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="abc2d-186">Obtain hello public IP address of your load balancer with [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span></span> <span data-ttu-id="abc2d-187">esempio Hello Ottiene hello di indirizzo IP per *myPublicIP* creato in precedenza:</span><span class="sxs-lookup"><span data-stu-id="abc2d-187">hello following example obtains hello IP address for *myPublicIP* created earlier:</span></span>

```powershell
Get-AzureRmPublicIPAddress `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Name myPublicIP | select IpAddress
```

<span data-ttu-id="abc2d-188">È quindi possibile immettere l'indirizzo IP pubblico hello nel browser web tooa.</span><span class="sxs-lookup"><span data-stu-id="abc2d-188">You can then enter hello public IP address in tooa web browser.</span></span> <span data-ttu-id="abc2d-189">sito Hello viene visualizzato, inclusi hello nome host della macchina virtuale hello tale bilanciamento del carico hello distribuite tooas traffico nel seguente esempio hello:</span><span class="sxs-lookup"><span data-stu-id="abc2d-189">hello website is displayed, including hello hostname of hello VM that hello load balancer distributed traffic tooas in hello following example:</span></span>

![Esecuzione del sito Web IIS](./media/tutorial-load-balancer/running-iis-website.png)

<span data-ttu-id="abc2d-191">servizio di bilanciamento del carico hello toosee distribuire il traffico tra tutte le tre macchine virtuali in esecuzione l'app, è possibile forza aggiornamento web browser.</span><span class="sxs-lookup"><span data-stu-id="abc2d-191">toosee hello load balancer distribute traffic across all three VMs running your app, you can force-refresh your web browser.</span></span>


## <a name="add-and-remove-vms"></a><span data-ttu-id="abc2d-192">aggiunta e rimozione di VM</span><span class="sxs-lookup"><span data-stu-id="abc2d-192">Add and remove VMs</span></span>
<span data-ttu-id="abc2d-193">È possibile la manutenzione tooperform hello macchine virtuali in esecuzione l'app, ad esempio l'installazione di aggiornamenti del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="abc2d-193">You may need tooperform maintenance on hello VMs running your app, such as installing OS updates.</span></span> <span data-ttu-id="abc2d-194">toodeal con un aumento del traffico tooyour app, potrebbe essere necessario tooadd altre macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="abc2d-194">toodeal with increased traffic tooyour app, you may need tooadd additional VMs.</span></span> <span data-ttu-id="abc2d-195">In questa sezione illustra come tooremove o aggiungere una macchina virtuale dal servizio di bilanciamento del carico hello.</span><span class="sxs-lookup"><span data-stu-id="abc2d-195">This section shows you how tooremove or add a VM from hello load balancer.</span></span>

### <a name="remove-a-vm-from-hello-load-balancer"></a><span data-ttu-id="abc2d-196">Rimuovere una macchina virtuale dal servizio di bilanciamento del carico hello</span><span class="sxs-lookup"><span data-stu-id="abc2d-196">Remove a VM from hello load balancer</span></span>
<span data-ttu-id="abc2d-197">Ottenere l'interfaccia di rete di hello con [Get AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface), quindi set hello *LoadBalancerBackendAddressPools* proprietà di hello NIC virtuale troppo*$null*.</span><span class="sxs-lookup"><span data-stu-id="abc2d-197">Get hello network interface card with [Get-AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface), then set hello *LoadBalancerBackendAddressPools* property of hello virtual NIC too*$null*.</span></span> <span data-ttu-id="abc2d-198">Infine, aggiornare NIC virtuale hello:</span><span class="sxs-lookup"><span data-stu-id="abc2d-198">Finally, update hello virtual NIC.:</span></span>

```powershell
$nic = Get-AzureRmNetworkInterface `
    -ResourceGroupName myResourceGroupLoadBalancer `
    -Name myNic2
$nic.Ipconfigurations[0].LoadBalancerBackendAddressPools=$null
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

<span data-ttu-id="abc2d-199">servizio di bilanciamento del carico hello toosee distribuire il traffico tra hello altre due macchine virtuali in esecuzione l'app è possibile forza aggiornamento web browser.</span><span class="sxs-lookup"><span data-stu-id="abc2d-199">toosee hello load balancer distribute traffic across hello remaining two VMs running your app you can force-refresh your web browser.</span></span> <span data-ttu-id="abc2d-200">È ora possibile eseguire la manutenzione in hello macchina virtuale, ad esempio l'installazione degli aggiornamenti del sistema operativo o l'esecuzione di un riavvio della VM.</span><span class="sxs-lookup"><span data-stu-id="abc2d-200">You can now perform maintenance on hello VM, such as installing OS updates or performing a VM reboot.</span></span>

### <a name="add-a-vm-toohello-load-balancer"></a><span data-ttu-id="abc2d-201">Aggiungere un bilanciamento del carico VM toohello</span><span class="sxs-lookup"><span data-stu-id="abc2d-201">Add a VM toohello load balancer</span></span>
<span data-ttu-id="abc2d-202">Dopo che esegue la manutenzione delle macchine Virtuali, o se è necessario tooexpand capacità, impostare hello *LoadBalancerBackendAddressPools* proprietà toohello NIC virtuale hello *BackendAddressPool* da [ Get-AzureRMLoadBalancer](/powershell/module/azurerm.network/get-azurermloadbalancer):</span><span class="sxs-lookup"><span data-stu-id="abc2d-202">After performing VM maintenance, or if you need tooexpand capacity, set hello *LoadBalancerBackendAddressPools* property of hello virtual NIC toohello *BackendAddressPool* from [Get-AzureRMLoadBalancer](/powershell/module/azurerm.network/get-azurermloadbalancer):</span></span>

<span data-ttu-id="abc2d-203">Ottieni bilanciamento del carico hello:</span><span class="sxs-lookup"><span data-stu-id="abc2d-203">Get hello load balancer:</span></span>

```powershell
$lb = Get-AzureRMLoadBalancer `
    -ResourceGroupName myResourceGroupLoadBalancer `
    -Name myLoadBalancer 
$nic.IpConfigurations[0].LoadBalancerBackendAddressPools=$lb.BackendAddressPools[0]
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

## <a name="next-steps"></a><span data-ttu-id="abc2d-204">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="abc2d-204">Next steps</span></span>

<span data-ttu-id="abc2d-205">In questa esercitazione è creato un servizio di bilanciamento del carico e collegato tooit macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="abc2d-205">In this tutorial, you created a load balancer and attached VMs tooit.</span></span> <span data-ttu-id="abc2d-206">Si è appreso come:</span><span class="sxs-lookup"><span data-stu-id="abc2d-206">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="abc2d-207">Creare un servizio di bilanciamento del carico di Azure</span><span class="sxs-lookup"><span data-stu-id="abc2d-207">Create an Azure load balancer</span></span>
> * <span data-ttu-id="abc2d-208">Creare un probe di integrità per il servizio di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="abc2d-208">Create a load balancer health probe</span></span>
> * <span data-ttu-id="abc2d-209">Creare regole del traffico di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="abc2d-209">Create load balancer traffic rules</span></span>
> * <span data-ttu-id="abc2d-210">Utilizzare toocreate estensione Script personalizzata hello un sito IIS di base</span><span class="sxs-lookup"><span data-stu-id="abc2d-210">Use hello Custom Script Extension toocreate a basic IIS site</span></span>
> * <span data-ttu-id="abc2d-211">Creare macchine virtuali e collegare bilanciamento del carico tooa</span><span class="sxs-lookup"><span data-stu-id="abc2d-211">Create virtual machines and attach tooa load balancer</span></span>
> * <span data-ttu-id="abc2d-212">Visualizzare un bilanciamento del carico in azione</span><span class="sxs-lookup"><span data-stu-id="abc2d-212">View a load balancer in action</span></span>
> * <span data-ttu-id="abc2d-213">Aggiungere e rimuovere macchine virtuali da un bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="abc2d-213">Add and remove VMs from a load balancer</span></span>

<span data-ttu-id="abc2d-214">Spostare toolearn esercitazione successiva toohello come reti VM toomanage.</span><span class="sxs-lookup"><span data-stu-id="abc2d-214">Advance toohello next tutorial toolearn how toomanage VM networking.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="abc2d-215">Gestire le VM e le reti virtuali</span><span class="sxs-lookup"><span data-stu-id="abc2d-215">Manage VMs and virtual networks</span></span>](./tutorial-virtual-network.md)
