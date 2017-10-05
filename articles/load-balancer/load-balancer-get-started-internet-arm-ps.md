---
title: Creare un servizio di bilanciamento del carico con connessione Internet di Azure - PowerShell | Documentazione Microsoft
description: Informazioni sulla creazione di un servizio di bilanciamento del carico Internet in Resource Manager con PowerShell
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
ms.assetid: 8257f548-7019-417f-b15f-d004a1eec826
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: f610afbdfac7b5dd9a1a5eb6812c86d8ce0d63e3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <span data-ttu-id="bf3d1-103"><a name="get-started"></a>Creazione di un servizio di bilanciamento del carico per Internet in Resource Manager con PowerShell</span><span class="sxs-lookup"><span data-stu-id="bf3d1-103"><a name="get-started"></a>Creating an Internet-facing load balancer in Resource Manager by using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="bf3d1-104">Portale</span><span class="sxs-lookup"><span data-stu-id="bf3d1-104">Portal</span></span>](../load-balancer/load-balancer-get-started-internet-portal.md)
> * [<span data-ttu-id="bf3d1-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="bf3d1-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-internet-arm-ps.md)
> * [<span data-ttu-id="bf3d1-106">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="bf3d1-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-internet-arm-cli.md)
> * [<span data-ttu-id="bf3d1-107">Modello</span><span class="sxs-lookup"><span data-stu-id="bf3d1-107">Template</span></span>](../load-balancer/load-balancer-get-started-internet-arm-template.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="bf3d1-108">Questo articolo illustra il modello di distribuzione Gestione risorse.</span><span class="sxs-lookup"><span data-stu-id="bf3d1-108">This article covers the Resource Manager deployment model.</span></span> <span data-ttu-id="bf3d1-109">È inoltre possibile [trovare informazioni su come creare un servizio di bilanciamento del carico Internet tramite il modello di distribuzione classica](load-balancer-get-started-internet-classic-cli.md).</span><span class="sxs-lookup"><span data-stu-id="bf3d1-109">You can also [learn how to create an Internet-facing load balancer by using the classic deployment model](load-balancer-get-started-internet-classic-cli.md).</span></span>

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="deploying-the-solution-by-using-azure-powershell"></a><span data-ttu-id="bf3d1-110">Distribuzione della soluzione mediante Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="bf3d1-110">Deploying the solution by using Azure PowerShell</span></span>

<span data-ttu-id="bf3d1-111">Le procedure seguenti illustrano come creare un servizio di bilanciamento del carico con connessione Internet usando Azure Resource Manager con PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bf3d1-111">The following procedures explain how to create an Internet-facing load balancer by using Azure Resource Manager with PowerShell.</span></span> <span data-ttu-id="bf3d1-112">Con Azure Resource Manager, ogni risorsa viene creata e configurata singolarmente e poi integrata per creare una servizio di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="bf3d1-112">With Azure Resource Manager, each resource is created and configured individually, and then put together to create a load balancer.</span></span>

<span data-ttu-id="bf3d1-113">Per distribuire un servizio di bilanciamento del carico è necessario creare e configurare gli oggetti seguenti:</span><span class="sxs-lookup"><span data-stu-id="bf3d1-113">You must create and configure the following objects to deploy a load balancer:</span></span>

* <span data-ttu-id="bf3d1-114">Configurazione IP front-end: contiene gli indirizzi IP pubblici (PIP) per il traffico di rete in ingresso.</span><span class="sxs-lookup"><span data-stu-id="bf3d1-114">Front-end IP configuration: contains public IP (PIP) addresses for incoming network traffic.</span></span>
* <span data-ttu-id="bf3d1-115">Pool di indirizzi back-end: contiene le interfacce di rete (NIC) per consentire alle macchine virtuali di ricevere il traffico di rete dal servizio di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="bf3d1-115">Back-end address pool: contains network interfaces (NICs) for the virtual machines to receive network traffic from the load balancer.</span></span>
* <span data-ttu-id="bf3d1-116">Regole di bilanciamento del carico: contiene le regole che eseguono il mapping di una porta pubblica sul servizio di bilanciamento del carico a una porta nel pool di indirizzi back-end.</span><span class="sxs-lookup"><span data-stu-id="bf3d1-116">Load-balancing rules: contains rules that map a public port on the load balancer to a port in the back-end address pool.</span></span>
* <span data-ttu-id="bf3d1-117">Regole NAT: contiene le regole che eseguono il mapping di una porta pubblica sul servizio di bilanciamento del carico a una porta per una macchina virtuale specifica nel pool di indirizzi back-end.</span><span class="sxs-lookup"><span data-stu-id="bf3d1-117">Inbound NAT rules: contains rules that map a public port on the load balancer to a port for a specific virtual machine in the back-end address pool.</span></span>
* <span data-ttu-id="bf3d1-118">Probe: contiene probe di integrità usati per verificare la disponibilità di istanze di macchine virtuali nel pool di indirizzi back-end.</span><span class="sxs-lookup"><span data-stu-id="bf3d1-118">Probes: contains health probes used to check availability of virtual machine instances in the back-end address pool.</span></span>

<span data-ttu-id="bf3d1-119">Per altre informazioni, vedere [Supporto di Azure Resource Manager per Load Balancer](load-balancer-arm.md).</span><span class="sxs-lookup"><span data-stu-id="bf3d1-119">For more information, see [Azure Resource Manager support for Load Balancer](load-balancer-arm.md).</span></span>

## <a name="set-up-powershell-to-use-resource-manager"></a><span data-ttu-id="bf3d1-120">Configurazione di PowerShell per l'uso di Resource Manager</span><span class="sxs-lookup"><span data-stu-id="bf3d1-120">Set up PowerShell to use Resource Manager</span></span>

<span data-ttu-id="bf3d1-121">Assicurarsi di avere la versione di produzione più recente del modulo Azure Resource Manager per PowerShell:</span><span class="sxs-lookup"><span data-stu-id="bf3d1-121">Make sure you have the latest production version of the Azure Resource Manager module for PowerShell:</span></span>

1. <span data-ttu-id="bf3d1-122">Accedere ad Azure.</span><span class="sxs-lookup"><span data-stu-id="bf3d1-122">Sign in to Azure.</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

    <span data-ttu-id="bf3d1-123">Immettere le credenziali quando richiesto.</span><span class="sxs-lookup"><span data-stu-id="bf3d1-123">Enter your credentials when prompted.</span></span>

2. <span data-ttu-id="bf3d1-124">Controllare le sottoscrizioni per l'account.</span><span class="sxs-lookup"><span data-stu-id="bf3d1-124">Check the subscriptions for the account.</span></span>

    ```powershell
    Get-AzureRmSubscription
    ```

3. <span data-ttu-id="bf3d1-125">Scegliere le sottoscrizioni ad Azure da usare.</span><span class="sxs-lookup"><span data-stu-id="bf3d1-125">Choose which of your Azure subscriptions to use.</span></span>

    ```powershell
    Select-AzureRmSubscription -SubscriptionId 'GUID of subscription'
    ```

4. <span data-ttu-id="bf3d1-126">Creare un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="bf3d1-126">Create a resource group.</span></span> <span data-ttu-id="bf3d1-127">Se si usa un gruppo di risorse esistente, ignorare questo passaggio.</span><span class="sxs-lookup"><span data-stu-id="bf3d1-127">(Skip this step if you're using an existing resource group.)</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name NRP-RG -location "West US"
    ```

## <a name="create-a-virtual-network-and-a-public-ip-address-for-the-front-end-ip-pool"></a><span data-ttu-id="bf3d1-128">Creare una rete virtuale e un indirizzo IP pubblico per il pool di indirizzi IP front-end</span><span class="sxs-lookup"><span data-stu-id="bf3d1-128">Create a virtual network and a public IP address for the front-end IP pool</span></span>

1. <span data-ttu-id="bf3d1-129">Creare una subnet e una rete virtuale</span><span class="sxs-lookup"><span data-stu-id="bf3d1-129">Create a subnet and a virtual network.</span></span>

    ```powershell
    $backendSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -AddressPrefix 10.0.2.0/24
    New-AzureRmvirtualNetwork -Name NRPVNet -ResourceGroupName NRP-RG -Location 'West US' -AddressPrefix 10.0.0.0/16 -Subnet $backendSubnet
    ```

2. <span data-ttu-id="bf3d1-130">Creare una risorsa di indirizzo IP pubblico di Azure denominata **PublicIP** che dovrà essere usata da un pool di indirizzi IP front-end con nome DNS **loadbalancernrp.westus.cloudapp.azure.com**.</span><span class="sxs-lookup"><span data-stu-id="bf3d1-130">Create an Azure public IP address resource, named **PublicIP**, to be used by a front-end IP pool with the DNS name **loadbalancernrp.westus.cloudapp.azure.com**.</span></span> <span data-ttu-id="bf3d1-131">Il comando seguente usa il tipo di allocazione statica.</span><span class="sxs-lookup"><span data-stu-id="bf3d1-131">The following command uses the static allocation type.</span></span>

    ```powershell
    $publicIP = New-AzureRmPublicIpAddress -Name PublicIp -ResourceGroupName NRP-RG -Location 'West US' -AllocationMethod Static -DomainNameLabel loadbalancernrp
    ```

   > [!IMPORTANT]
   > <span data-ttu-id="bf3d1-132">Il servizio di bilanciamento del carico usa l'etichetta di dominio dell'indirizzo IP pubblico come prefisso per il nome di dominio completo.</span><span class="sxs-lookup"><span data-stu-id="bf3d1-132">The load balancer uses the domain label of the public IP as a prefix for its FQDN.</span></span> <span data-ttu-id="bf3d1-133">Questa è una differenza rispetto al modello di distribuzione classica, che usa il servizio cloud come nome di dominio completo del servizio di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="bf3d1-133">This is different from the classic deployment model, which uses the cloud service as the load balancer FQDN.</span></span>
   > <span data-ttu-id="bf3d1-134">In questo esempio il nome di dominio completo è **loadbalancernrp.westus.cloudapp.azure.com**.</span><span class="sxs-lookup"><span data-stu-id="bf3d1-134">In this example, the FQDN is **loadbalancernrp.westus.cloudapp.azure.com**.</span></span>

## <a name="create-a-front-end-ip-pool-and-a-back-end-address-pool"></a><span data-ttu-id="bf3d1-135">Creazione di un pool di indirizzi IP front-end e un pool di indirizzi back-end</span><span class="sxs-lookup"><span data-stu-id="bf3d1-135">Create a front-end IP pool and a back-end address pool</span></span>

1. <span data-ttu-id="bf3d1-136">Creare un pool di indirizzi IP front-end denominato **LB-Frontend** che usa la risorsa **PublicIp**.</span><span class="sxs-lookup"><span data-stu-id="bf3d1-136">Create a front-end IP pool named **LB-Frontend** that uses the **PublicIp** resource.</span></span>

    ```powershell
    $frontendIP = New-AzureRmLoadBalancerFrontendIpConfig -Name LB-Frontend -PublicIpAddress $publicIP
    ```

2. <span data-ttu-id="bf3d1-137">Creare un pool di indirizzi back-end denominato **LB-backend**.</span><span class="sxs-lookup"><span data-stu-id="bf3d1-137">Create a back-end address pool named **LB-backend**.</span></span>

    ```powershell
    $beaddresspool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name LB-backend
    ```

## <a name="create-nat-rules-a-load-balancer-rule-a-probe-and-a-load-balancer"></a><span data-ttu-id="bf3d1-138">Creazione di regole NAT, una regola di bilanciamento del carico, un probe e un servizio di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="bf3d1-138">Create NAT rules, a load balancer rule, a probe, and a load balancer</span></span>

<span data-ttu-id="bf3d1-139">Questo esempio crea gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="bf3d1-139">This example creates the following items:</span></span>

* <span data-ttu-id="bf3d1-140">Una regola NAT per la conversione di tutto il traffico in ingresso nella porta 3441 alla porta 3389</span><span class="sxs-lookup"><span data-stu-id="bf3d1-140">A NAT rule to translate all incoming traffic on port 3441 to port 3389</span></span>
* <span data-ttu-id="bf3d1-141">Una regola NAT per la conversione di tutto il traffico in ingresso nella porta 3442 alla porta 3389</span><span class="sxs-lookup"><span data-stu-id="bf3d1-141">A NAT rule to translate all incoming traffic on port 3442 to port 3389</span></span>
* <span data-ttu-id="bf3d1-142">Una regola probe per il controllo dello stato di integrità in una pagina denominata **HealthProbe.aspx**</span><span class="sxs-lookup"><span data-stu-id="bf3d1-142">A probe rule to check the health status on a page named **HealthProbe.aspx**</span></span>
* <span data-ttu-id="bf3d1-143">Una regola di bilanciamento del carico per il bilanciamento di tutto il traffico in ingresso nella porta 80 alla porta 80 negli indirizzi nel pool back-end</span><span class="sxs-lookup"><span data-stu-id="bf3d1-143">A load balancer rule to balance all incoming traffic on port 80 to port 80 on the addresses in the back-end pool</span></span>
* <span data-ttu-id="bf3d1-144">Un servizio di bilanciamento del carico che usa tutti questi oggetti</span><span class="sxs-lookup"><span data-stu-id="bf3d1-144">A load balancer that uses all these objects</span></span>

<span data-ttu-id="bf3d1-145">Usare i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="bf3d1-145">Use these steps:</span></span>

1. <span data-ttu-id="bf3d1-146">Creare le regole NAT.</span><span class="sxs-lookup"><span data-stu-id="bf3d1-146">Create the NAT rules.</span></span>

    ```powershell
    $inboundNATRule1= New-AzureRmLoadBalancerInboundNatRuleConfig -Name RDP1 -FrontendIpConfiguration $frontendIP -Protocol TCP -FrontendPort 3441 -BackendPort 3389

    $inboundNATRule2= New-AzureRmLoadBalancerInboundNatRuleConfig -Name RDP2 -FrontendIpConfiguration $frontendIP -Protocol TCP -FrontendPort 3442 -BackendPort 3389
    ```

2. <span data-ttu-id="bf3d1-147">Creare un probe di integrità.</span><span class="sxs-lookup"><span data-stu-id="bf3d1-147">Create a health probe.</span></span> <span data-ttu-id="bf3d1-148">Esistono due modi per configurare un probe:</span><span class="sxs-lookup"><span data-stu-id="bf3d1-148">There are two ways to configure a probe:</span></span>

    <span data-ttu-id="bf3d1-149">Probe HTTP</span><span class="sxs-lookup"><span data-stu-id="bf3d1-149">HTTP probe</span></span>

    ```powershell
    $healthProbe = New-AzureRmLoadBalancerProbeConfig -Name HealthProbe -RequestPath 'HealthProbe.aspx' -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2
    ```

    <span data-ttu-id="bf3d1-150">Probe TCP</span><span class="sxs-lookup"><span data-stu-id="bf3d1-150">TCP probe</span></span>

    ```powershell
    $healthProbe = New-AzureRmLoadBalancerProbeConfig -Name HealthProbe -Protocol Tcp -Port 80 -IntervalInSeconds 15 -ProbeCount 2
    ```

3. <span data-ttu-id="bf3d1-151">Creare una regola del servizio di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="bf3d1-151">Create a load balancer rule.</span></span>

    ```powershell
    $lbrule = New-AzureRmLoadBalancerRuleConfig -Name HTTP -FrontendIpConfiguration $frontendIP -BackendAddressPool  $beAddressPool -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 80
    ```

4. <span data-ttu-id="bf3d1-152">Creare il servizio di bilanciamento del carico usando gli oggetti creati in precedenza.</span><span class="sxs-lookup"><span data-stu-id="bf3d1-152">Create the load balancer by using the previously created objects.</span></span>

    ```powershell
    $NRPLB = New-AzureRmLoadBalancer -ResourceGroupName NRP-RG -Name NRP-LB -Location 'West US' -FrontendIpConfiguration $frontendIP -InboundNatRule $inboundNATRule1,$inboundNatRule2 -LoadBalancingRule $lbrule -BackendAddressPool $beAddressPool -Probe $healthProbe
    ```

## <a name="create-nics"></a><span data-ttu-id="bf3d1-153">Creare NIC</span><span class="sxs-lookup"><span data-stu-id="bf3d1-153">Create NICs</span></span>

<span data-ttu-id="bf3d1-154">Creare interfacce di rete (o modificare quelle esistenti) e associarle a regole NAT, regole di bilanciamento del carico e probe:</span><span class="sxs-lookup"><span data-stu-id="bf3d1-154">Create network interfaces (or modify existing ones) and then associate them to NAT rules, load balancer rules, and probes:</span></span>

1. <span data-ttu-id="bf3d1-155">Ottenere la rete virtuale e la subnet per la rete virtuale in cui devono essere create le NIC.</span><span class="sxs-lookup"><span data-stu-id="bf3d1-155">Get the virtual network and a virtual network subnet, where the NICs need to be created.</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -Name NRPVNet -ResourceGroupName NRP-RG
    $backendSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -VirtualNetwork $vnet
    ```

2. <span data-ttu-id="bf3d1-156">Creare una NIC denominata **lb-nic1-be**e associarla alla prima regola NAT, quindi al primo (e unico) pool di indirizzi back-end.</span><span class="sxs-lookup"><span data-stu-id="bf3d1-156">Create a NIC named **lb-nic1-be**, and associate it with the first NAT rule and the first (and only) back-end address pool.</span></span>

    ```powershell
    $backendnic1= New-AzureRmNetworkInterface -ResourceGroupName NRP-RG -Name lb-nic1-be -Location 'West US' -PrivateIpAddress 10.0.2.6 -Subnet $backendSubnet -LoadBalancerBackendAddressPool $nrplb.BackendAddressPools[0] -LoadBalancerInboundNatRule $nrplb.InboundNatRules[0]
    ```

3. <span data-ttu-id="bf3d1-157">Creare una NIC denominata **lb-nic2-be**e associarla alla seconda regola NAT, quindi al primo (e unico) pool di indirizzi back-end.</span><span class="sxs-lookup"><span data-stu-id="bf3d1-157">Create a NIC named **lb-nic2-be**, and associate it with the second NAT rule and the first (and only) back-end address pool.</span></span>

    ```powershell
    $backendnic2= New-AzureRmNetworkInterface -ResourceGroupName NRP-RG -Name lb-nic2-be -Location 'West US' -PrivateIpAddress 10.0.2.7 -Subnet $backendSubnet -LoadBalancerBackendAddressPool $nrplb.BackendAddressPools[0] -LoadBalancerInboundNatRule $nrplb.InboundNatRules[1]
    ```

4. <span data-ttu-id="bf3d1-158">Creare le NIC.</span><span class="sxs-lookup"><span data-stu-id="bf3d1-158">Check the NICs.</span></span>

        $backendnic1

    <span data-ttu-id="bf3d1-159">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="bf3d1-159">Expected output:</span></span>

        Name                 : lb-nic1-be
        ResourceGroupName    : NRP-RG
        Location             : westus
        Id                   : /subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/networkInterfaces/lb-nic1-be
        Etag                 : W/"d448256a-e1df-413a-9103-a137e07276d1"
        ResourceGuid         : 896cac4f-152a-40b9-b079-3e2201a5906e
        ProvisioningState    : Succeeded
        Tags                 :
        VirtualMachine       : null
        IpConfigurations     : [
                            {
                            "Name": "ipconfig1",
                            "Etag": "W/\"d448256a-e1df-413a-9103-a137e07276d1\"",
                            "Id": "/subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/networkInterfaces/lb-nic1-be/ipConfigurations/ipconfig1",
                            "PrivateIpAddress": "10.0.2.6",
                            "PrivateIpAllocationMethod": "Static",
                            "Subnet": {
                                "Id": "/subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/virtualNetworks/NRPVNet/subnets/LB-Subnet-BE"
                            },
                            "ProvisioningState": "Succeeded",
                            "PrivateIpAddressVersion": "IPv4",
                            "PublicIpAddress": {
                                "Id": null
                            },
                            "LoadBalancerBackendAddressPools": [
                                {
                                "Id": "/subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/loadBalancers/NRPlb/backendAddressPools/LB-backend"
                                }
                            ],
                            "LoadBalancerInboundNatRules": [
                                {
                                "Id": "/subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/loadBalancers/NRPlb/inboundNatRules/RDP1"
                                }
                            ],
                            "Primary": true,
                            "ApplicationGatewayBackendAddressPools": []
                            }
                        ]
        DnsSettings          : {
                            "DnsServers": [],
                            "AppliedDnsServers": [],
                            "InternalDomainNameSuffix": "prcwibzcuvie5hnxav0yjks2cd.dx.internal.cloudapp.net"
                        }
        EnableIPForwarding   : False
        NetworkSecurityGroup : null
        Primary              :

5. <span data-ttu-id="bf3d1-160">Usare il cmdlet `Add-AzureRmVMNetworkInterface` per assegnare le schede NIC a macchine virtuali diverse.</span><span class="sxs-lookup"><span data-stu-id="bf3d1-160">Use the `Add-AzureRmVMNetworkInterface` cmdlet to assign the NICs to different VMs.</span></span>

## <a name="create-a-virtual-machine"></a><span data-ttu-id="bf3d1-161">Creare una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="bf3d1-161">Create a virtual machine</span></span>

<span data-ttu-id="bf3d1-162">Per indicazioni sulla creazione di una macchina virtuale e sull'assegnazione di una scheda di interfaccia di rete, vedere [Creare una VM di Azure con PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="bf3d1-162">For guidance on creating a virtual machine and assigning a NIC, see [Create an Azure VM using PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).</span></span>

## <a name="add-the-network-interface-to-the-load-balancer"></a><span data-ttu-id="bf3d1-163">Aggiunta dell'interfaccia di rete al servizio di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="bf3d1-163">Add the network interface to the load balancer</span></span>

1. <span data-ttu-id="bf3d1-164">Recuperare il servizio di bilanciamento del carico da Azure.</span><span class="sxs-lookup"><span data-stu-id="bf3d1-164">Retrieve the load balancer from Azure.</span></span>

    <span data-ttu-id="bf3d1-165">Se non è ancora stata eseguita questa operazione, caricare la risorsa di bilanciamento del carico in una variabile.</span><span class="sxs-lookup"><span data-stu-id="bf3d1-165">Load the load balancer resource into a variable (if you haven't done that yet).</span></span> <span data-ttu-id="bf3d1-166">La variabile si chiama **$lb**. Usare gli stessi nomi della risorsa di bilanciamento del carico creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="bf3d1-166">The variable is called **$lb**. Use the same names from the load balancer resource that you created earlier.</span></span>

    ```powershell
    $lb= get-azurermloadbalancer -name NRP-LB -resourcegroupname NRP-RG
    ```

2. <span data-ttu-id="bf3d1-167">Caricare la configurazione back-end in una variabile.</span><span class="sxs-lookup"><span data-stu-id="bf3d1-167">Load the back-end configuration to a variable.</span></span>

    ```powershell
    $backend=Get-AzureRmLoadBalancerBackendAddressPoolConfig -name LB-backend -LoadBalancer $lb
    ```

3. <span data-ttu-id="bf3d1-168">Caricare l'interfaccia di rete già creata in una variabile.</span><span class="sxs-lookup"><span data-stu-id="bf3d1-168">Load the already created network interface into a variable.</span></span> <span data-ttu-id="bf3d1-169">Il nome della variabile è **$nic**.</span><span class="sxs-lookup"><span data-stu-id="bf3d1-169">The variable name is **$nic**.</span></span> <span data-ttu-id="bf3d1-170">Il nome dell'interfaccia di rete è lo stesso dell'esempio precedente.</span><span class="sxs-lookup"><span data-stu-id="bf3d1-170">The network interface name is the same one from the earlier example.</span></span>

    ```powershell
    $nic =get-azurermnetworkinterface -name lb-nic1-be -resourcegroupname NRP-RG
    ```

4. <span data-ttu-id="bf3d1-171">Modificare la configurazione back-end nell'interfaccia di rete.</span><span class="sxs-lookup"><span data-stu-id="bf3d1-171">Change the back-end configuration on the network interface.</span></span>

    ```powershell
    $nic.IpConfigurations[0].LoadBalancerBackendAddressPools=$backend
    ```

5. <span data-ttu-id="bf3d1-172">Salvare l'oggetto interfaccia di rete.</span><span class="sxs-lookup"><span data-stu-id="bf3d1-172">Save the network interface object.</span></span>

    ```powershell
    Set-AzureRmNetworkInterface -NetworkInterface $nic
    ```

    <span data-ttu-id="bf3d1-173">Dopo che un'interfaccia di rete viene aggiunta al pool di back-end di bilanciamento del carico, inizia a ricevere il traffico di rete in base alle regole di bilanciamento del carico per la risorsa di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="bf3d1-173">After a network interface is added to the load balancer back-end pool, it starts receiving network traffic based on the load-balancing rules for that load balancer resource.</span></span>

## <a name="update-an-existing-load-balancer"></a><span data-ttu-id="bf3d1-174">Aggiornare un bilanciamento del carico esistente</span><span class="sxs-lookup"><span data-stu-id="bf3d1-174">Update an existing load balancer</span></span>

1. <span data-ttu-id="bf3d1-175">Usando il servizio di bilanciamento del carico dell'esempio precedente, assegnare un oggetto di bilanciamento del carico alla variabile **$slb** usando `Get-AzureLoadBalancer`.</span><span class="sxs-lookup"><span data-stu-id="bf3d1-175">By using the load balancer from the earlier example, assign a load balancer object to the variable **$slb** by using `Get-AzureLoadBalancer`.</span></span>

    ```powershell
    $slb = get-AzureRmLoadBalancer -Name NRP-LB -ResourceGroupName NRP-RG
    ```

2. <span data-ttu-id="bf3d1-176">Nell'esempio seguente, si aggiunge una regola NAT in ingresso mediante la porta 81 nel pool di front-end e la porta 8181 per il pool di back-end a un servizio di bilanciamento del carico esistente.</span><span class="sxs-lookup"><span data-stu-id="bf3d1-176">In the following example, you add an inbound NAT rule--by using port 81 in the front-end pool and port 8181 for the back-end pool--to an existing load balancer.</span></span>

    ```powershell
    $slb | Add-AzureRmLoadBalancerInboundNatRuleConfig -Name NewRule -FrontendIpConfiguration $slb.FrontendIpConfigurations[0] -FrontendPort 81  -BackendPort 8181 -Protocol TCP
    ```

3. <span data-ttu-id="bf3d1-177">Salvare la nuova configurazione tramite `Set-AzureLoadBalancer`.</span><span class="sxs-lookup"><span data-stu-id="bf3d1-177">Save the new configuration by using `Set-AzureLoadBalancer`.</span></span>

    ```powershell
    $slb | Set-AzureRmLoadBalancer
    ```

## <a name="remove-a-load-balancer"></a><span data-ttu-id="bf3d1-178">Rimuovere un bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="bf3d1-178">Remove a load balancer</span></span>

<span data-ttu-id="bf3d1-179">Usare il comando `Remove-AzureLoadBalancer` per eliminare un servizio di bilanciamento del carico creato in precedenza denominato **NRP-LB** in un gruppo di risorse di nome **NRP-RG**.</span><span class="sxs-lookup"><span data-stu-id="bf3d1-179">Use the command `Remove-AzureLoadBalancer` to delete a previously created load balancer named **NRP-LB** in a resource group called **NRP-RG**.</span></span>

```powershell
Remove-AzureRmLoadBalancer -Name NRP-LB -ResourceGroupName NRP-RG
```

> [!NOTE]
> <span data-ttu-id="bf3d1-180">È possibile usare l'opzione facoltativa **-Force** per evitare la richiesta di eliminazione.</span><span class="sxs-lookup"><span data-stu-id="bf3d1-180">You can use the optional switch **-Force** to avoid the prompt for deletion.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bf3d1-181">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="bf3d1-181">Next steps</span></span>

[<span data-ttu-id="bf3d1-182">Introduzione alla configurazione del bilanciamento del carico interno</span><span class="sxs-lookup"><span data-stu-id="bf3d1-182">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="bf3d1-183">Configurare una modalità di distribuzione del servizio di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="bf3d1-183">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="bf3d1-184">Configurare le impostazioni del timeout di inattività TCP per il bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="bf3d1-184">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
