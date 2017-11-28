---
title: bilanciamento del carico aaaCreate con una connessione Internet di Azure con IPv6 - PowerShell | Documenti Microsoft
description: Informazioni su come toocreate una connessione Internet bilanciamento del carico con IPv6 tramite PowerShell per Gestione risorse
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
ms.openlocfilehash: 6ebb108399b070e06dddc33b7a774481eb44d717
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internet-facing-load-balancer-with-ipv6-using-powershell-for-resource-manager"></a><span data-ttu-id="24b7a-104">Introduzione alla creazione di un servizio di bilanciamento del carico con connessione Internet con IPv6 usando PowerShell per Resource Manager</span><span class="sxs-lookup"><span data-stu-id="24b7a-104">Get started creating an Internet facing load balancer with IPv6 using PowerShell for Resource Manager</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="24b7a-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="24b7a-105">PowerShell</span></span>](load-balancer-ipv6-internet-ps.md)
> * [<span data-ttu-id="24b7a-106">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="24b7a-106">Azure CLI</span></span>](load-balancer-ipv6-internet-cli.md)
> * [<span data-ttu-id="24b7a-107">Modello</span><span class="sxs-lookup"><span data-stu-id="24b7a-107">Template</span></span>](load-balancer-ipv6-internet-template.md)

<span data-ttu-id="24b7a-108">Azure Load Balancer è un servizio di bilanciamento del carico di livello 4 (TCP, UDP).</span><span class="sxs-lookup"><span data-stu-id="24b7a-108">An Azure load balancer is a Layer-4 (TCP, UDP) load balancer.</span></span> <span data-ttu-id="24b7a-109">servizio di bilanciamento del carico Hello garantisce disponibilità elevata mediante la distribuzione del traffico in entrata tra le istanze del servizio di integrità in servizi cloud o macchine virtuali in un set di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="24b7a-109">hello load balancer provides high availability by distributing incoming traffic among healthy service instances in cloud services or virtual machines in a load balancer set.</span></span> <span data-ttu-id="24b7a-110">Azure Load Balancer può anche presentare tali servizi su più porte, più indirizzi IP o entrambi.</span><span class="sxs-lookup"><span data-stu-id="24b7a-110">Azure Load Balancer can also present those services on multiple ports, multiple IP addresses, or both.</span></span>

## <a name="example-deployment-scenario"></a><span data-ttu-id="24b7a-111">Scenario di distribuzione di esempio</span><span class="sxs-lookup"><span data-stu-id="24b7a-111">Example deployment scenario</span></span>

<span data-ttu-id="24b7a-112">Hello diagramma seguente illustra una soluzione viene distribuita in questo articolo di bilanciamento del carico di hello.</span><span class="sxs-lookup"><span data-stu-id="24b7a-112">hello following diagram illustrates hello load balancing solution being deployed in this article.</span></span>

![Scenario del bilanciamento del carico](./media/load-balancer-ipv6-internet-ps/lb-ipv6-scenario.png)

<span data-ttu-id="24b7a-114">In questo scenario creerai hello seguendo le risorse di Azure:</span><span class="sxs-lookup"><span data-stu-id="24b7a-114">In this scenario you will create hello following Azure resources:</span></span>

* <span data-ttu-id="24b7a-115">un servizio di bilanciamento del carico con connessione Internet con un indirizzo IP pubblico IPv4 e IPv6</span><span class="sxs-lookup"><span data-stu-id="24b7a-115">an Internet-facing Load Balancer with an IPv4 and an IPv6 Public IP address</span></span>
* <span data-ttu-id="24b7a-116">due bilanciamento regole toomap hello VIP toohello privato endpoint pubblici di carico</span><span class="sxs-lookup"><span data-stu-id="24b7a-116">two load balancing rules toomap hello public VIPs toohello private endpoints</span></span>
* <span data-ttu-id="24b7a-117">un Set di disponibilità toothat contiene macchine virtuali hello due</span><span class="sxs-lookup"><span data-stu-id="24b7a-117">an Availability Set toothat contains hello two VMs</span></span>
* <span data-ttu-id="24b7a-118">due macchine virtuali (VM)</span><span class="sxs-lookup"><span data-stu-id="24b7a-118">two virtual machines (VMs)</span></span>
* <span data-ttu-id="24b7a-119">un'interfaccia di rete virtuale per ogni VM con l'assegnazione degli indirizzi IPv4 e IPv6</span><span class="sxs-lookup"><span data-stu-id="24b7a-119">a virtual network interface for each VM with both IPv4 and IPv6 addresses assigned</span></span>

## <a name="deploying-hello-solution-using-hello-azure-powershell"></a><span data-ttu-id="24b7a-120">Distribuzione di soluzioni hello utilizzando hello Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="24b7a-120">Deploying hello solution using hello Azure PowerShell</span></span>

<span data-ttu-id="24b7a-121">Hello alla procedura seguente viene illustrato come una connessione Internet toocreate bilanciamento del carico con Gestione risorse di Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="24b7a-121">hello following steps show how toocreate an Internet facing load balancer using Azure Resource Manager with PowerShell.</span></span> <span data-ttu-id="24b7a-122">Con Gestione risorse di Azure, ogni risorsa viene creato e configurato singolarmente, quindi riunire toocreate una risorsa.</span><span class="sxs-lookup"><span data-stu-id="24b7a-122">With Azure Resource Manager, each resource is created and configured individually, then put together toocreate a resource.</span></span>

<span data-ttu-id="24b7a-123">toodeploy un bilanciamento del carico, per creare e configurare hello seguenti oggetti:</span><span class="sxs-lookup"><span data-stu-id="24b7a-123">toodeploy a load balancer, you create and configure hello following objects:</span></span>

* <span data-ttu-id="24b7a-124">Configurazione di IP front-end: contiene gli indirizzi IP pubblici per il traffico di rete in ingresso.</span><span class="sxs-lookup"><span data-stu-id="24b7a-124">Front-end IP configuration - contains public IP addresses for incoming network traffic.</span></span>
* <span data-ttu-id="24b7a-125">Pool di indirizzi di back-end - contiene le interfacce di rete (NIC) per tooreceive il traffico di rete dal servizio di bilanciamento del carico hello hello macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="24b7a-125">Back-end address pool - contains network interfaces (NICs) for hello virtual machines tooreceive network traffic from hello load balancer.</span></span>
* <span data-ttu-id="24b7a-126">Regole di bilanciamento del carico - contiene le regole di mapping di una porta pubblica su tooport del servizio di bilanciamento carico di hello nel pool di indirizzi back-end di hello.</span><span class="sxs-lookup"><span data-stu-id="24b7a-126">Load balancing rules - contains rules mapping a public port on hello load balancer tooport in hello back-end address pool.</span></span>
* <span data-ttu-id="24b7a-127">Regole NAT in ingresso - contiene le regole di mapping di una porta pubblica nella porta di tooa del bilanciamento del carico hello per una macchina virtuale specifica nel pool di indirizzi back-end di hello.</span><span class="sxs-lookup"><span data-stu-id="24b7a-127">Inbound NAT rules - contains rules mapping a public port on hello load balancer tooa port for a specific virtual machine in hello back-end address pool.</span></span>
* <span data-ttu-id="24b7a-128">Probe - contiene integrità probe usati toocheck disponibilità delle istanze di macchine virtuali nel pool di indirizzi back-end di hello.</span><span class="sxs-lookup"><span data-stu-id="24b7a-128">Probes - contains health probes used toocheck availability of virtual machines instances in hello back-end address pool.</span></span>

<span data-ttu-id="24b7a-129">Per altre informazioni, vedere [Supporto di Azure Resource Manager per Load Balancer](load-balancer-arm.md).</span><span class="sxs-lookup"><span data-stu-id="24b7a-129">For more information, see [Azure Resource Manager support for Load Balancer](load-balancer-arm.md).</span></span>

## <a name="set-up-powershell-toouse-resource-manager"></a><span data-ttu-id="24b7a-130">Configurare PowerShell toouse Gestione risorse</span><span class="sxs-lookup"><span data-stu-id="24b7a-130">Set up PowerShell toouse Resource Manager</span></span>

<span data-ttu-id="24b7a-131">Assicurarsi di disporre di hello ultima versione di produzione del modulo di gestione risorse di Azure hello per PowerShell.</span><span class="sxs-lookup"><span data-stu-id="24b7a-131">Make sure you have hello latest production version of hello Azure Resource Manager module for PowerShell.</span></span>

1. <span data-ttu-id="24b7a-132">Accesso ad Azure</span><span class="sxs-lookup"><span data-stu-id="24b7a-132">Sign into Azure</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

    <span data-ttu-id="24b7a-133">Immettere le credenziali quando richiesto.</span><span class="sxs-lookup"><span data-stu-id="24b7a-133">Enter your credentials when prompted.</span></span>

2. <span data-ttu-id="24b7a-134">Controllare le sottoscrizioni di hello per account hello</span><span class="sxs-lookup"><span data-stu-id="24b7a-134">Check hello subscriptions for hello account</span></span>

    ```powershell
    Get-AzureRmSubscription
    ```

3. <span data-ttu-id="24b7a-135">Scegliere quali di toouse le sottoscrizioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="24b7a-135">Choose which of your Azure subscriptions toouse.</span></span>

    ```powershell
    Select-AzureRmSubscription -SubscriptionId 'GUID of subscription'
    ```

4. <span data-ttu-id="24b7a-136">Creare un nuovo gruppo di risorse. Ignorare questo passaggio se si usa un gruppo di risorse esistente.</span><span class="sxs-lookup"><span data-stu-id="24b7a-136">Create a resource group (skip this step if using an existing resource group)</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name NRP-RG -location "West US"
    ```

## <a name="create-a-virtual-network-and-a-public-ip-address-for-hello-front-end-ip-pool"></a><span data-ttu-id="24b7a-137">Creare una rete virtuale e un indirizzo IP pubblico per il pool IP front-end di hello</span><span class="sxs-lookup"><span data-stu-id="24b7a-137">Create a virtual network and a public IP address for hello front-end IP pool</span></span>

1. <span data-ttu-id="24b7a-138">Creare una rete virtuale con una subnet.</span><span class="sxs-lookup"><span data-stu-id="24b7a-138">Create a virtual network with a subnet.</span></span>

    ```powershell
    $backendSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -AddressPrefix 10.0.2.0/24
    $vnet = New-AzureRmvirtualNetwork -Name VNet -ResourceGroupName NRP-RG -Location 'West US' -AddressPrefix 10.0.0.0/16 -Subnet $backendSubnet
    ```

2. <span data-ttu-id="24b7a-139">Creare risorse (PIP) per pool di indirizzi IP front-end hello di indirizzo IP pubblico di Azure.</span><span class="sxs-lookup"><span data-stu-id="24b7a-139">Create Azure Public IP address (PIP) resources for hello front-end IP address pool.</span></span>

    ```powershell
    $publicIPv4 = New-AzureRmPublicIpAddress -Name 'pub-ipv4' -ResourceGroupName NRP-RG -Location 'West US' -AllocationMethod Static -IpAddressVersion IPv4 -DomainNameLabel lbnrpipv4
    $publicIPv6 = New-AzureRmPublicIpAddress -Name 'pub-ipv6' -ResourceGroupName NRP-RG -Location 'West US' -AllocationMethod Dynamic -IpAddressVersion IPv6 -DomainNameLabel lbnrpipv6
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="24b7a-140">bilanciamento del carico di Hello Usa etichetta hello del dominio dell'indirizzo IP pubblico hello come prefisso per il nome di dominio completo.</span><span class="sxs-lookup"><span data-stu-id="24b7a-140">hello load balancer uses hello domain label of hello public IP as prefix for its FQDN.</span></span> <span data-ttu-id="24b7a-141">In questo esempio, sono nomi di dominio completi hello *lbnrpipv4.westus.cloudapp.azure.com* e *lbnrpipv6.westus.cloudapp.azure.com*.</span><span class="sxs-lookup"><span data-stu-id="24b7a-141">In this example, hello FQDNs are *lbnrpipv4.westus.cloudapp.azure.com* and *lbnrpipv6.westus.cloudapp.azure.com*.</span></span>

## <a name="create-a-front-end-ip-configurations-and-a-back-end-address-pool"></a><span data-ttu-id="24b7a-142">Creare una configurazione di indirizzi IP front-end e un pool di indirizzi back-end</span><span class="sxs-lookup"><span data-stu-id="24b7a-142">Create a Front-End IP configurations and a Back-End Address Pool</span></span>

1. <span data-ttu-id="24b7a-143">Creare una configurazione di indirizzo front-end che utilizza indirizzi IP pubblici hello che è stato creato.</span><span class="sxs-lookup"><span data-stu-id="24b7a-143">Create front-end address configuration that uses hello Public IP addresses you created.</span></span>

    ```powershell
    $FEIPConfigv4 = New-AzureRmLoadBalancerFrontendIpConfig -Name "LB-Frontendv4" -PublicIpAddress $publicIPv4
    $FEIPConfigv6 = New-AzureRmLoadBalancerFrontendIpConfig -Name "LB-Frontendv6" -PublicIpAddress $publicIPv6
    ```

2. <span data-ttu-id="24b7a-144">Creare i pool di indirizzi back-end.</span><span class="sxs-lookup"><span data-stu-id="24b7a-144">Create back-end address pools.</span></span>

    ```powershell
    $backendpoolipv4 = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name "BackendPoolIPv4"
    $backendpoolipv6 = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name "BackendPoolIPv6"
    ```

## <a name="create-lb-rules-nat-rules-a-probe-and-a-load-balancer"></a><span data-ttu-id="24b7a-145">Creare regole di bilanciamento del carico, regole NAT, un probe e un servizio di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="24b7a-145">Create LB rules, NAT rules, a probe, and a load balancer</span></span>

<span data-ttu-id="24b7a-146">In questo esempio crea hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="24b7a-146">This example creates hello following items:</span></span>

* <span data-ttu-id="24b7a-147">un dispositivo NAT tutto il traffico in ingresso sulla porta 443 tooport 4443 tootranslate della regola</span><span class="sxs-lookup"><span data-stu-id="24b7a-147">a NAT rule tootranslate all incoming traffic on port 443 tooport 4443</span></span>
* <span data-ttu-id="24b7a-148">un toobalance regola di bilanciamento carico di tutto il traffico in ingresso sulla porta 80 tooport 80 su hello indirizzi nel pool back-end hello.</span><span class="sxs-lookup"><span data-stu-id="24b7a-148">a load balancer rule toobalance all incoming traffic on port 80 tooport 80 on hello addresses in hello back-end pool.</span></span>
* <span data-ttu-id="24b7a-149">un carico del servizio di bilanciamento regola tooallow RDP connessione toohello macchine virtuali sulla porta 3389.</span><span class="sxs-lookup"><span data-stu-id="24b7a-149">a load balancer rule tooallow RDP connection toohello VMs on port 3389.</span></span>
* <span data-ttu-id="24b7a-150">probe regola toocheck hello lo stato di integrità in una pagina denominata *HealthProbe.aspx* o un servizio sulla porta 8080</span><span class="sxs-lookup"><span data-stu-id="24b7a-150">a probe rule toocheck hello health status on a page named *HealthProbe.aspx* or a service on port 8080</span></span>
* <span data-ttu-id="24b7a-151">Un servizio di bilanciamento del carico che usa tutti questi oggetti</span><span class="sxs-lookup"><span data-stu-id="24b7a-151">a load balancer that uses all these objects</span></span>

1. <span data-ttu-id="24b7a-152">Creare le regole NAT di hello.</span><span class="sxs-lookup"><span data-stu-id="24b7a-152">Create hello NAT rules.</span></span>

    ```powershell
    $inboundNATRule1v4 = New-AzureRmLoadBalancerInboundNatRuleConfig -Name "NicNatRulev4" -FrontendIpConfiguration $FEIPConfigv4 -Protocol TCP -FrontendPort 443 -BackendPort 4443
    $inboundNATRule1v6 = New-AzureRmLoadBalancerInboundNatRuleConfig -Name "NicNatRulev6" -FrontendIpConfiguration $FEIPConfigv6 -Protocol TCP -FrontendPort 443 -BackendPort 4443
    ```

2. <span data-ttu-id="24b7a-153">Creare un probe di integrità.</span><span class="sxs-lookup"><span data-stu-id="24b7a-153">Create a health probe.</span></span> <span data-ttu-id="24b7a-154">Esistono due modi tooconfigure un probe:</span><span class="sxs-lookup"><span data-stu-id="24b7a-154">There are two ways tooconfigure a probe:</span></span>

    <span data-ttu-id="24b7a-155">Probe HTTP</span><span class="sxs-lookup"><span data-stu-id="24b7a-155">HTTP probe</span></span>

    ```powershell
    $healthProbe = New-AzureRmLoadBalancerProbeConfig -Name 'HealthProbe-v4v6' -RequestPath 'HealthProbe.aspx' -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2
    ```

    <span data-ttu-id="24b7a-156">o probe TCP</span><span class="sxs-lookup"><span data-stu-id="24b7a-156">or TCP probe</span></span>

    ```powershell
    $healthProbe = New-AzureRmLoadBalancerProbeConfig -Name 'HealthProbe-v4v6' -Protocol Tcp -Port 8080 -IntervalInSeconds 15 -ProbeCount 2
    $RDPprobe = New-AzureRmLoadBalancerProbeConfig -Name 'RDPprobe' -Protocol Tcp -Port 3389 -IntervalInSeconds 15 -ProbeCount 2
    ```

    <span data-ttu-id="24b7a-157">In questo esempio verrà hello toouse che probe TCP.</span><span class="sxs-lookup"><span data-stu-id="24b7a-157">For this example, we are going toouse hello TCP probes.</span></span>

3. <span data-ttu-id="24b7a-158">Creare una regola del servizio di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="24b7a-158">Create a load balancer rule.</span></span>

    ```powershell
    $lbrule1v4 = New-AzureRmLoadBalancerRuleConfig -Name "HTTPv4" -FrontendIpConfiguration $FEIPConfigv4 -BackendAddressPool $backendpoolipv4 -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 8080
    $lbrule1v6 = New-AzureRmLoadBalancerRuleConfig -Name "HTTPv6" -FrontendIpConfiguration $FEIPConfigv6 -BackendAddressPool $backendpoolipv6 -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 8080
    $RDPrule = New-AzureRmLoadBalancerRuleConfig -Name "RDPrule" -FrontendIpConfiguration $FEIPConfigv4 -BackendAddressPool $backendpoolipv4 -Probe $RDPprobe -Protocol Tcp -FrontendPort 3389 -BackendPort 3389
    ```

4. <span data-ttu-id="24b7a-159">Creazione di bilanciamento del carico hello utilizzando oggetti hello creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="24b7a-159">Create hello load balancer using hello previously created objects.</span></span>

    ```powershell
    $NRPLB = New-AzureRmLoadBalancer -ResourceGroupName NRP-RG -Name 'myNrpIPv6LB' -Location 'West US' -FrontendIpConfiguration $FEIPConfigv4,$FEIPConfigv6 -InboundNatRule $inboundNATRule1v6,$inboundNATRule1v4 -BackendAddressPool $backendpoolipv4,$backendpoolipv6 -Probe $healthProbe,$RDPprobe -LoadBalancingRule $lbrule1v4,$lbrule1v6,$RDPrule
    ```

## <a name="create-nics-for-hello-back-end-vms"></a><span data-ttu-id="24b7a-160">Creare schede di rete per hello macchine virtuali di back-end</span><span class="sxs-lookup"><span data-stu-id="24b7a-160">Create NICs for hello back-end VMs</span></span>

1. <span data-ttu-id="24b7a-161">Ottenere hello rete virtuale e Subnet di rete virtuale, in cui hello NIC devono toobe creato.</span><span class="sxs-lookup"><span data-stu-id="24b7a-161">Get hello Virtual Network and Virtual Network Subnet, where hello NICs need toobe created.</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -Name VNet -ResourceGroupName NRP-RG
    $backendSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -VirtualNetwork $vnet
    ```

2. <span data-ttu-id="24b7a-162">Creare le configurazioni IP e schede di rete per le macchine virtuali hello.</span><span class="sxs-lookup"><span data-stu-id="24b7a-162">Create IP configurations and NICs for hello VMs.</span></span>

    ```powershell
    $nic1IPv4 = New-AzureRmNetworkInterfaceIpConfig -Name "IPv4IPConfig" -PrivateIpAddressVersion "IPv4" -Subnet $backendSubnet -LoadBalancerBackendAddressPool $backendpoolipv4 -LoadBalancerInboundNatRule $inboundNATRule1v4
    $nic1IPv6 = New-AzureRmNetworkInterfaceIpConfig -Name "IPv6IPConfig" -PrivateIpAddressVersion "IPv6" -LoadBalancerBackendAddressPool $backendpoolipv6 -LoadBalancerInboundNatRule $inboundNATRule1v6
    $nic1 = New-AzureRmNetworkInterface -Name 'myNrpIPv6Nic0' -IpConfiguration $nic1IPv4,$nic1IPv6 -ResourceGroupName NRP-RG -Location 'West US'

    $nic2IPv4 = New-AzureRmNetworkInterfaceIpConfig -Name "IPv4IPConfig" -PrivateIpAddressVersion "IPv4" -Subnet $backendSubnet -LoadBalancerBackendAddressPool $backendpoolipv4
    $nic2IPv6 = New-AzureRmNetworkInterfaceIpConfig -Name "IPv6IPConfig" -PrivateIpAddressVersion "IPv6" -LoadBalancerBackendAddressPool $backendpoolipv6
    $nic2 = New-AzureRmNetworkInterface -Name 'myNrpIPv6Nic1' -IpConfiguration $nic2IPv4,$nic2IPv6 -ResourceGroupName NRP-RG -Location 'West US'
    ```

## <a name="create-virtual-machines-and-assign-hello-newly-created-nics"></a><span data-ttu-id="24b7a-163">Creare macchine virtuali e assegnare hello appena creati NIC</span><span class="sxs-lookup"><span data-stu-id="24b7a-163">Create virtual machines and assign hello newly created NICs</span></span>

<span data-ttu-id="24b7a-164">Per altre informazioni, vedere [Creare e preconfigurare una macchina virtuale Windows con Resource Manager e Azure PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="24b7a-164">For more information about creating a VM, see [Create and preconfigure a Windows Virtual Machine with Resource Manager and Azure PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json)</span></span>

1. <span data-ttu-id="24b7a-165">Creare un set di disponibilità e l'account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="24b7a-165">Create an Availability Set and Storage account</span></span>

    ```powershell
    New-AzureRmAvailabilitySet -Name 'myNrpIPv6AvSet' -ResourceGroupName NRP-RG -location 'West US'
    $availabilitySet = Get-AzureRmAvailabilitySet -Name 'myNrpIPv6AvSet' -ResourceGroupName NRP-RG
    New-AzureRmStorageAccount -ResourceGroupName NRP-RG -Name 'mynrpipv6stacct' -Location 'West US' -SkuName "Standard_LRS"
    $CreatedStorageAccount = Get-AzureRmStorageAccount -ResourceGroupName NRP-RG -Name 'mynrpipv6stacct'
    ```

2. <span data-ttu-id="24b7a-166">Creare ogni macchina virtuale e assegnare le schede NIC hello precedente creato</span><span class="sxs-lookup"><span data-stu-id="24b7a-166">Create each VM and assign hello previous created NICs</span></span>

    ```powershell
    $mySecureCredentials= Get-Credential -Message "Type hello username and password of hello local administrator account."

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

## <a name="next-steps"></a><span data-ttu-id="24b7a-167">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="24b7a-167">Next steps</span></span>

[<span data-ttu-id="24b7a-168">Introduzione alla configurazione del bilanciamento del carico interno</span><span class="sxs-lookup"><span data-stu-id="24b7a-168">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="24b7a-169">Configurare una modalità di distribuzione del servizio di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="24b7a-169">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="24b7a-170">Configurare le impostazioni del timeout di inattività TCP per il bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="24b7a-170">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
