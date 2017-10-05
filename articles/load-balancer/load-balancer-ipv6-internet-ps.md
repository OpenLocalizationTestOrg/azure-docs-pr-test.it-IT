---
title: 'Creare un servizio di bilanciamento del carico di Azure con connessione Internet con IPv6: PowerShell | Documentazione Microsoft'
description: Informazioni sulla creazione di un servizio di bilanciamento del carico con connessione Internet con IPv6 usando PowerShell per Resource Manager
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
keywords: ipv6, azure load balancer, dual stack, ip pubblico, ipv6 nativo, mobili, iot
ms.assetid: d4c649e3-84ad-4343-8b6a-0e89f0b9e518
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 9d3cd37d3f2912301904b0a35f6fbc978d173079
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="get-started-creating-an-internet-facing-load-balancer-with-ipv6-using-powershell-for-resource-manager"></a><span data-ttu-id="93bc4-104">Introduzione alla creazione di un servizio di bilanciamento del carico con connessione Internet con IPv6 usando PowerShell per Resource Manager</span><span class="sxs-lookup"><span data-stu-id="93bc4-104">Get started creating an Internet facing load balancer with IPv6 using PowerShell for Resource Manager</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="93bc4-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="93bc4-105">PowerShell</span></span>](load-balancer-ipv6-internet-ps.md)
> * [<span data-ttu-id="93bc4-106">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="93bc4-106">Azure CLI</span></span>](load-balancer-ipv6-internet-cli.md)
> * [<span data-ttu-id="93bc4-107">Modello</span><span class="sxs-lookup"><span data-stu-id="93bc4-107">Template</span></span>](load-balancer-ipv6-internet-template.md)

<span data-ttu-id="93bc4-108">Azure Load Balancer è un servizio di bilanciamento del carico di livello 4 (TCP, UDP).</span><span class="sxs-lookup"><span data-stu-id="93bc4-108">An Azure load balancer is a Layer-4 (TCP, UDP) load balancer.</span></span> <span data-ttu-id="93bc4-109">Il servizio di bilanciamento del carico offre disponibilità elevata distribuendo il traffico in ingresso tra istanze del servizio integre in servizi cloud o macchine virtuali in un set di bilanciamento del carico .</span><span class="sxs-lookup"><span data-stu-id="93bc4-109">The load balancer provides high availability by distributing incoming traffic among healthy service instances in cloud services or virtual machines in a load balancer set.</span></span> <span data-ttu-id="93bc4-110">Azure Load Balancer può anche presentare tali servizi su più porte, più indirizzi IP o entrambi.</span><span class="sxs-lookup"><span data-stu-id="93bc4-110">Azure Load Balancer can also present those services on multiple ports, multiple IP addresses, or both.</span></span>

## <a name="example-deployment-scenario"></a><span data-ttu-id="93bc4-111">Scenario di distribuzione di esempio</span><span class="sxs-lookup"><span data-stu-id="93bc4-111">Example deployment scenario</span></span>

<span data-ttu-id="93bc4-112">Il diagramma seguente illustra la soluzione di bilanciamento del carico distribuita in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="93bc4-112">The following diagram illustrates the load balancing solution being deployed in this article.</span></span>

![Scenario del bilanciamento del carico](./media/load-balancer-ipv6-internet-ps/lb-ipv6-scenario.png)

<span data-ttu-id="93bc4-114">In questo scenario si creeranno le seguenti risorse di Azure:</span><span class="sxs-lookup"><span data-stu-id="93bc4-114">In this scenario you will create the following Azure resources:</span></span>

* <span data-ttu-id="93bc4-115">un servizio di bilanciamento del carico con connessione Internet con un indirizzo IP pubblico IPv4 e IPv6</span><span class="sxs-lookup"><span data-stu-id="93bc4-115">an Internet-facing Load Balancer with an IPv4 and an IPv6 Public IP address</span></span>
* <span data-ttu-id="93bc4-116">due regole di bilanciamento del carico per eseguire il mapping degli indirizzi VIP pubblici agli endpoint privati</span><span class="sxs-lookup"><span data-stu-id="93bc4-116">two load balancing rules to map the public VIPs to the private endpoints</span></span>
* <span data-ttu-id="93bc4-117">un set di disponibilità contenente le due macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="93bc4-117">an Availability Set to that contains the two VMs</span></span>
* <span data-ttu-id="93bc4-118">due macchine virtuali (VM)</span><span class="sxs-lookup"><span data-stu-id="93bc4-118">two virtual machines (VMs)</span></span>
* <span data-ttu-id="93bc4-119">un'interfaccia di rete virtuale per ogni VM con l'assegnazione degli indirizzi IPv4 e IPv6</span><span class="sxs-lookup"><span data-stu-id="93bc4-119">a virtual network interface for each VM with both IPv4 and IPv6 addresses assigned</span></span>

## <a name="deploying-the-solution-using-the-azure-powershell"></a><span data-ttu-id="93bc4-120">Distribuzione della soluzione tramite Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="93bc4-120">Deploying the solution using the Azure PowerShell</span></span>

<span data-ttu-id="93bc4-121">La procedura seguente illustra come creare un servizio di bilanciamento del carico con connessione Internet usando Azure Resource Manager con PowerShell.</span><span class="sxs-lookup"><span data-stu-id="93bc4-121">The following steps show how to create an Internet facing load balancer using Azure Resource Manager with PowerShell.</span></span> <span data-ttu-id="93bc4-122">Con Azure Resource Manager ogni risorsa viene creata e configurata singolarmente e quindi integrata per creare una risorsa.</span><span class="sxs-lookup"><span data-stu-id="93bc4-122">With Azure Resource Manager, each resource is created and configured individually, then put together to create a resource.</span></span>

<span data-ttu-id="93bc4-123">Per distribuire un servizio di bilanciamento del carico è necessario creare e configurare gli oggetti seguenti:</span><span class="sxs-lookup"><span data-stu-id="93bc4-123">To deploy a load balancer, you create and configure the following objects:</span></span>

* <span data-ttu-id="93bc4-124">Configurazione di IP front-end: contiene gli indirizzi IP pubblici per il traffico di rete in ingresso.</span><span class="sxs-lookup"><span data-stu-id="93bc4-124">Front-end IP configuration - contains public IP addresses for incoming network traffic.</span></span>
* <span data-ttu-id="93bc4-125">Pool di indirizzi back-end: contiene interfacce di rete (NIC) per le macchine virtuali per la ricezione di traffico di rete dal servizio di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="93bc4-125">Back-end address pool - contains network interfaces (NICs) for the virtual machines to receive network traffic from the load balancer.</span></span>
* <span data-ttu-id="93bc4-126">Regole di bilanciamento del carico: contengono regole per il mapping di una porta pubblica nel servizio di bilanciamento del carico alle porte nel pool di indirizzi back-end.</span><span class="sxs-lookup"><span data-stu-id="93bc4-126">Load balancing rules - contains rules mapping a public port on the load balancer to port in the back-end address pool.</span></span>
* <span data-ttu-id="93bc4-127">Regole NAT in ingresso: contengono regole per il mapping di una porta pubblica nel servizio di bilanciamento del carico a una porta per una macchina virtuale specifica nel pool di indirizzi back-end.</span><span class="sxs-lookup"><span data-stu-id="93bc4-127">Inbound NAT rules - contains rules mapping a public port on the load balancer to a port for a specific virtual machine in the back-end address pool.</span></span>
* <span data-ttu-id="93bc4-128">Probe: contengono probe di integrità usati per verificare la disponibilità di istanze di macchine virtuali nel pool di indirizzi back-end.</span><span class="sxs-lookup"><span data-stu-id="93bc4-128">Probes - contains health probes used to check availability of virtual machines instances in the back-end address pool.</span></span>

<span data-ttu-id="93bc4-129">Per altre informazioni, vedere [Supporto di Azure Resource Manager per Load Balancer](load-balancer-arm.md).</span><span class="sxs-lookup"><span data-stu-id="93bc4-129">For more information, see [Azure Resource Manager support for Load Balancer](load-balancer-arm.md).</span></span>

## <a name="set-up-powershell-to-use-resource-manager"></a><span data-ttu-id="93bc4-130">Configurazione di PowerShell per l'uso di Resource Manager</span><span class="sxs-lookup"><span data-stu-id="93bc4-130">Set up PowerShell to use Resource Manager</span></span>

<span data-ttu-id="93bc4-131">Assicurarsi di avere la versione di produzione più recente del modulo Azure Resource Manager per PowerShell.</span><span class="sxs-lookup"><span data-stu-id="93bc4-131">Make sure you have the latest production version of the Azure Resource Manager module for PowerShell.</span></span>

1. <span data-ttu-id="93bc4-132">Accesso ad Azure</span><span class="sxs-lookup"><span data-stu-id="93bc4-132">Sign into Azure</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

    <span data-ttu-id="93bc4-133">Immettere le credenziali quando richiesto.</span><span class="sxs-lookup"><span data-stu-id="93bc4-133">Enter your credentials when prompted.</span></span>

2. <span data-ttu-id="93bc4-134">Controllare le sottoscrizioni per l'account</span><span class="sxs-lookup"><span data-stu-id="93bc4-134">Check the subscriptions for the account</span></span>

    ```powershell
    Get-AzureRmSubscription
    ```

3. <span data-ttu-id="93bc4-135">Scegliere le sottoscrizioni ad Azure da usare.</span><span class="sxs-lookup"><span data-stu-id="93bc4-135">Choose which of your Azure subscriptions to use.</span></span>

    ```powershell
    Select-AzureRmSubscription -SubscriptionId 'GUID of subscription'
    ```

4. <span data-ttu-id="93bc4-136">Creare un nuovo gruppo di risorse. Ignorare questo passaggio se si usa un gruppo di risorse esistente.</span><span class="sxs-lookup"><span data-stu-id="93bc4-136">Create a resource group (skip this step if using an existing resource group)</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name NRP-RG -location "West US"
    ```

## <a name="create-a-virtual-network-and-a-public-ip-address-for-the-front-end-ip-pool"></a><span data-ttu-id="93bc4-137">Creare una rete virtuale e un indirizzo IP pubblico per il pool di indirizzi IP front-end</span><span class="sxs-lookup"><span data-stu-id="93bc4-137">Create a virtual network and a public IP address for the front-end IP pool</span></span>

1. <span data-ttu-id="93bc4-138">Creare una rete virtuale con una subnet.</span><span class="sxs-lookup"><span data-stu-id="93bc4-138">Create a virtual network with a subnet.</span></span>

    ```powershell
    $backendSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -AddressPrefix 10.0.2.0/24
    $vnet = New-AzureRmvirtualNetwork -Name VNet -ResourceGroupName NRP-RG -Location 'West US' -AddressPrefix 10.0.0.0/16 -Subnet $backendSubnet
    ```

2. <span data-ttu-id="93bc4-139">Creare risorse di indirizzi IP pubblici (PIP) di Azure per il pool di indirizzi IP front-end.</span><span class="sxs-lookup"><span data-stu-id="93bc4-139">Create Azure Public IP address (PIP) resources for the front-end IP address pool.</span></span>

    ```powershell
    $publicIPv4 = New-AzureRmPublicIpAddress -Name 'pub-ipv4' -ResourceGroupName NRP-RG -Location 'West US' -AllocationMethod Static -IpAddressVersion IPv4 -DomainNameLabel lbnrpipv4
    $publicIPv6 = New-AzureRmPublicIpAddress -Name 'pub-ipv6' -ResourceGroupName NRP-RG -Location 'West US' -AllocationMethod Dynamic -IpAddressVersion IPv6 -DomainNameLabel lbnrpipv6
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="93bc4-140">Il servizio di bilanciamento del carico usa l'etichetta di dominio dell'indirizzo IP pubblico come prefisso per il nome di dominio completo.</span><span class="sxs-lookup"><span data-stu-id="93bc4-140">The load balancer uses the domain label of the public IP as prefix for its FQDN.</span></span> <span data-ttu-id="93bc4-141">In questo esempio, i nomi di dominio completo sono *lbnrpipv4.westus.cloudapp.azure.com* e *lbnrpipv6.westus.cloudapp.azure.com*.</span><span class="sxs-lookup"><span data-stu-id="93bc4-141">In this example, the FQDNs are *lbnrpipv4.westus.cloudapp.azure.com* and *lbnrpipv6.westus.cloudapp.azure.com*.</span></span>

## <a name="create-a-front-end-ip-configurations-and-a-back-end-address-pool"></a><span data-ttu-id="93bc4-142">Creare una configurazione di indirizzi IP front-end e un pool di indirizzi back-end</span><span class="sxs-lookup"><span data-stu-id="93bc4-142">Create a Front-End IP configurations and a Back-End Address Pool</span></span>

1. <span data-ttu-id="93bc4-143">Creare una configurazione di indirizzi front-end che userà gli indirizzi IP pubblici creati.</span><span class="sxs-lookup"><span data-stu-id="93bc4-143">Create front-end address configuration that uses the Public IP addresses you created.</span></span>

    ```powershell
    $FEIPConfigv4 = New-AzureRmLoadBalancerFrontendIpConfig -Name "LB-Frontendv4" -PublicIpAddress $publicIPv4
    $FEIPConfigv6 = New-AzureRmLoadBalancerFrontendIpConfig -Name "LB-Frontendv6" -PublicIpAddress $publicIPv6
    ```

2. <span data-ttu-id="93bc4-144">Creare i pool di indirizzi back-end.</span><span class="sxs-lookup"><span data-stu-id="93bc4-144">Create back-end address pools.</span></span>

    ```powershell
    $backendpoolipv4 = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name "BackendPoolIPv4"
    $backendpoolipv6 = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name "BackendPoolIPv6"
    ```

## <a name="create-lb-rules-nat-rules-a-probe-and-a-load-balancer"></a><span data-ttu-id="93bc4-145">Creare regole di bilanciamento del carico, regole NAT, un probe e un servizio di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="93bc4-145">Create LB rules, NAT rules, a probe, and a load balancer</span></span>

<span data-ttu-id="93bc4-146">Questo esempio crea gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="93bc4-146">This example creates the following items:</span></span>

* <span data-ttu-id="93bc4-147">Una regola NAT per la conversione di tutto il traffico in ingresso nella porta 443 alla porta 4443</span><span class="sxs-lookup"><span data-stu-id="93bc4-147">a NAT rule to translate all incoming traffic on port 443 to port 4443</span></span>
* <span data-ttu-id="93bc4-148">Regola del servizio di bilanciamento del carico per il bilanciamento di tutto il traffico in ingresso sulla porta 80 verso la porta 80 negli indirizzi nel pool back-end.</span><span class="sxs-lookup"><span data-stu-id="93bc4-148">a load balancer rule to balance all incoming traffic on port 80 to port 80 on the addresses in the back-end pool.</span></span>
* <span data-ttu-id="93bc4-149">Regola del servizio di bilanciamento del carico per consentire la connessione RDP alle macchine virtuali sulla porta 3389.</span><span class="sxs-lookup"><span data-stu-id="93bc4-149">a load balancer rule to allow RDP connection to the VMs on port 3389.</span></span>
* <span data-ttu-id="93bc4-150">Una regola probe per il controllo dello stato di integrità in una pagina denominata *HealthProbe.aspx* o un servizio sulla porta 8080</span><span class="sxs-lookup"><span data-stu-id="93bc4-150">a probe rule to check the health status on a page named *HealthProbe.aspx* or a service on port 8080</span></span>
* <span data-ttu-id="93bc4-151">Un servizio di bilanciamento del carico che usa tutti questi oggetti</span><span class="sxs-lookup"><span data-stu-id="93bc4-151">a load balancer that uses all these objects</span></span>

1. <span data-ttu-id="93bc4-152">Creare le regole NAT.</span><span class="sxs-lookup"><span data-stu-id="93bc4-152">Create the NAT rules.</span></span>

    ```powershell
    $inboundNATRule1v4 = New-AzureRmLoadBalancerInboundNatRuleConfig -Name "NicNatRulev4" -FrontendIpConfiguration $FEIPConfigv4 -Protocol TCP -FrontendPort 443 -BackendPort 4443
    $inboundNATRule1v6 = New-AzureRmLoadBalancerInboundNatRuleConfig -Name "NicNatRulev6" -FrontendIpConfiguration $FEIPConfigv6 -Protocol TCP -FrontendPort 443 -BackendPort 4443
    ```

2. <span data-ttu-id="93bc4-153">Creare un probe di integrità.</span><span class="sxs-lookup"><span data-stu-id="93bc4-153">Create a health probe.</span></span> <span data-ttu-id="93bc4-154">Esistono due modi per configurare un probe:</span><span class="sxs-lookup"><span data-stu-id="93bc4-154">There are two ways to configure a probe:</span></span>

    <span data-ttu-id="93bc4-155">Probe HTTP</span><span class="sxs-lookup"><span data-stu-id="93bc4-155">HTTP probe</span></span>

    ```powershell
    $healthProbe = New-AzureRmLoadBalancerProbeConfig -Name 'HealthProbe-v4v6' -RequestPath 'HealthProbe.aspx' -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2
    ```

    <span data-ttu-id="93bc4-156">o probe TCP</span><span class="sxs-lookup"><span data-stu-id="93bc4-156">or TCP probe</span></span>

    ```powershell
    $healthProbe = New-AzureRmLoadBalancerProbeConfig -Name 'HealthProbe-v4v6' -Protocol Tcp -Port 8080 -IntervalInSeconds 15 -ProbeCount 2
    $RDPprobe = New-AzureRmLoadBalancerProbeConfig -Name 'RDPprobe' -Protocol Tcp -Port 3389 -IntervalInSeconds 15 -ProbeCount 2
    ```

    <span data-ttu-id="93bc4-157">Per questo esempio verranno usati probe TCP.</span><span class="sxs-lookup"><span data-stu-id="93bc4-157">For this example, we are going to use the TCP probes.</span></span>

3. <span data-ttu-id="93bc4-158">Creare una regola del servizio di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="93bc4-158">Create a load balancer rule.</span></span>

    ```powershell
    $lbrule1v4 = New-AzureRmLoadBalancerRuleConfig -Name "HTTPv4" -FrontendIpConfiguration $FEIPConfigv4 -BackendAddressPool $backendpoolipv4 -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 8080
    $lbrule1v6 = New-AzureRmLoadBalancerRuleConfig -Name "HTTPv6" -FrontendIpConfiguration $FEIPConfigv6 -BackendAddressPool $backendpoolipv6 -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 8080
    $RDPrule = New-AzureRmLoadBalancerRuleConfig -Name "RDPrule" -FrontendIpConfiguration $FEIPConfigv4 -BackendAddressPool $backendpoolipv4 -Probe $RDPprobe -Protocol Tcp -FrontendPort 3389 -BackendPort 3389
    ```

4. <span data-ttu-id="93bc4-159">Creare il servizio di bilanciamento del carico usando gli oggetti creati in precedenza.</span><span class="sxs-lookup"><span data-stu-id="93bc4-159">Create the load balancer using the previously created objects.</span></span>

    ```powershell
    $NRPLB = New-AzureRmLoadBalancer -ResourceGroupName NRP-RG -Name 'myNrpIPv6LB' -Location 'West US' -FrontendIpConfiguration $FEIPConfigv4,$FEIPConfigv6 -InboundNatRule $inboundNATRule1v6,$inboundNATRule1v4 -BackendAddressPool $backendpoolipv4,$backendpoolipv6 -Probe $healthProbe,$RDPprobe -LoadBalancingRule $lbrule1v4,$lbrule1v6,$RDPrule
    ```

## <a name="create-nics-for-the-back-end-vms"></a><span data-ttu-id="93bc4-160">Creare le schede di interfaccia di rete per le macchine virtuali back-end</span><span class="sxs-lookup"><span data-stu-id="93bc4-160">Create NICs for the back-end VMs</span></span>

1. <span data-ttu-id="93bc4-161">Ottenere la rete virtuale e la subnet per la rete virtuale in cui devono essere create le schede NIC.</span><span class="sxs-lookup"><span data-stu-id="93bc4-161">Get the Virtual Network and Virtual Network Subnet, where the NICs need to be created.</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -Name VNet -ResourceGroupName NRP-RG
    $backendSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -VirtualNetwork $vnet
    ```

2. <span data-ttu-id="93bc4-162">Creare le configurazioni IP e schede di interfaccia di rete per le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="93bc4-162">Create IP configurations and NICs for the VMs.</span></span>

    ```powershell
    $nic1IPv4 = New-AzureRmNetworkInterfaceIpConfig -Name "IPv4IPConfig" -PrivateIpAddressVersion "IPv4" -Subnet $backendSubnet -LoadBalancerBackendAddressPool $backendpoolipv4 -LoadBalancerInboundNatRule $inboundNATRule1v4
    $nic1IPv6 = New-AzureRmNetworkInterfaceIpConfig -Name "IPv6IPConfig" -PrivateIpAddressVersion "IPv6" -LoadBalancerBackendAddressPool $backendpoolipv6 -LoadBalancerInboundNatRule $inboundNATRule1v6
    $nic1 = New-AzureRmNetworkInterface -Name 'myNrpIPv6Nic0' -IpConfiguration $nic1IPv4,$nic1IPv6 -ResourceGroupName NRP-RG -Location 'West US'

    $nic2IPv4 = New-AzureRmNetworkInterfaceIpConfig -Name "IPv4IPConfig" -PrivateIpAddressVersion "IPv4" -Subnet $backendSubnet -LoadBalancerBackendAddressPool $backendpoolipv4
    $nic2IPv6 = New-AzureRmNetworkInterfaceIpConfig -Name "IPv6IPConfig" -PrivateIpAddressVersion "IPv6" -LoadBalancerBackendAddressPool $backendpoolipv6
    $nic2 = New-AzureRmNetworkInterface -Name 'myNrpIPv6Nic1' -IpConfiguration $nic2IPv4,$nic2IPv6 -ResourceGroupName NRP-RG -Location 'West US'
    ```

## <a name="create-virtual-machines-and-assign-the-newly-created-nics"></a><span data-ttu-id="93bc4-163">Creare le macchine virtuali e assegnare le schede di interfaccia di rete appena create</span><span class="sxs-lookup"><span data-stu-id="93bc4-163">Create virtual machines and assign the newly created NICs</span></span>

<span data-ttu-id="93bc4-164">Per altre informazioni, vedere [Creare e preconfigurare una macchina virtuale Windows con Resource Manager e Azure PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="93bc4-164">For more information about creating a VM, see [Create and preconfigure a Windows Virtual Machine with Resource Manager and Azure PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json)</span></span>

1. <span data-ttu-id="93bc4-165">Creare un set di disponibilità e l'account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="93bc4-165">Create an Availability Set and Storage account</span></span>

    ```powershell
    New-AzureRmAvailabilitySet -Name 'myNrpIPv6AvSet' -ResourceGroupName NRP-RG -location 'West US'
    $availabilitySet = Get-AzureRmAvailabilitySet -Name 'myNrpIPv6AvSet' -ResourceGroupName NRP-RG
    New-AzureRmStorageAccount -ResourceGroupName NRP-RG -Name 'mynrpipv6stacct' -Location 'West US' -SkuName "Standard_LRS"
    $CreatedStorageAccount = Get-AzureRmStorageAccount -ResourceGroupName NRP-RG -Name 'mynrpipv6stacct'
    ```

2. <span data-ttu-id="93bc4-166">Creare ogni macchina virtuale e assegnare le schede di interfaccia di rete create in precedenza</span><span class="sxs-lookup"><span data-stu-id="93bc4-166">Create each VM and assign the previous created NICs</span></span>

    ```powershell
    $mySecureCredentials= Get-Credential -Message "Type the username and password of the local administrator account."

    $vm1 = New-AzureRmVMConfig -VMName 'myNrpIPv6VM0' -VMSize 'Standard_G1' -AvailabilitySetId $availabilitySet.Id
    $vm1 = Set-AzureRmVMOperatingSystem -VM $vm1 -Windows -ComputerName 'myNrpIPv6VM0' -Credential $mySecureCredentials -ProvisionVMAgent -EnableAutoUpdate
    $vm1 = Set-AzureRmVMSourceImage -VM $vm1 -PublisherName MicrosoftWindowsServer -Offer WindowsServer -Skus 2012-R2-Datacenter -Version "latest"
    $vm1 = Add-AzureRmVMNetworkInterface -VM $vm1 -Id $nic1.Id -Primary
    $osDisk1Uri = $CreatedStorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/myNrpIPv6VM0osdisk.vhd"
    $vm1 = Set-AzureRmVMOSDisk -VM $vm1 -Name 'myNrpIPv6VM0osdisk' -VhdUri $osDisk1Uri -CreateOption FromImage
    New-AzureRmVM -ResourceGroupName NRP-RG -Location 'West US' -VM $vm1

    $vm2 = New-AzureRmVMConfig -VMName 'myNrpIPv6VM1' -VMSize 'Standard_G1' -AvailabilitySetId $availabilitySet.Id
    $vm2 = Set-AzureRmVMOperatingSystem -VM $vm2 -Windows -ComputerName 'myNrpIPv6VM1' -Credential $mySecureCredentials -ProvisionVMAgent -EnableAutoUpdate
    $vm2 = Set-AzureRmVMSourceImage -VM $vm2 -PublisherName MicrosoftWindowsServer -Offer WindowsServer -Skus 2012-R2-Datacenter -Version "latest"
    $vm2 = Add-AzureRmVMNetworkInterface -VM $vm2 -Id $nic2.Id -Primary
    $osDisk2Uri = $CreatedStorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/myNrpIPv6VM1osdisk.vhd"
    $vm2 = Set-AzureRmVMOSDisk -VM $vm2 -Name 'myNrpIPv6VM1osdisk' -VhdUri $osDisk2Uri -CreateOption FromImage
    New-AzureRmVM -ResourceGroupName NRP-RG -Location 'West US' -VM $vm2
    ```

## <a name="next-steps"></a><span data-ttu-id="93bc4-167">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="93bc4-167">Next steps</span></span>

[<span data-ttu-id="93bc4-168">Introduzione alla configurazione del bilanciamento del carico interno</span><span class="sxs-lookup"><span data-stu-id="93bc4-168">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="93bc4-169">Configurare una modalità di distribuzione del servizio di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="93bc4-169">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="93bc4-170">Configurare le impostazioni del timeout di inattività TCP per il bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="93bc4-170">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
