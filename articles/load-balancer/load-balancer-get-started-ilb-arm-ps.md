---
title: Creare un servizio di bilanciamento del carico interno di Azure - PowerShell | Documentazione Microsoft
description: Informazioni su come creare un servizio di bilanciamento del carico interno in Gestione risorse con PowerShell
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
ms.assetid: c6c98981-df9d-4dd7-a94b-cc7d1dc99369
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 7bd31ab8f52ec5e81f6966000554be46eaa59396
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-internal-load-balancer-using-powershell"></a><span data-ttu-id="db507-103">Creare un servizio di bilanciamento del carico interno con PowerShell</span><span class="sxs-lookup"><span data-stu-id="db507-103">Create an internal load balancer using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="db507-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="db507-104">Azure Portal</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-portal.md)
> * [<span data-ttu-id="db507-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="db507-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-ps.md)
> * [<span data-ttu-id="db507-106">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="db507-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-cli.md)
> * [<span data-ttu-id="db507-107">Modello</span><span class="sxs-lookup"><span data-stu-id="db507-107">Template</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-template.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="db507-108">Azure offre due modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="db507-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="db507-109">Questo articolo illustra il modello di distribuzione Resource Manager che Microsoft consiglia di usare per le distribuzioni più recenti in sostituzione del [modello di distribuzione classica](load-balancer-get-started-ilb-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="db507-109">This article covers using the Resource Manager deployment model, which Microsoft recommends for most new deployments instead of the [classic deployment model](load-balancer-get-started-ilb-classic-ps.md).</span></span>

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

<span data-ttu-id="db507-110">La procedura seguente illustra come creare un servizio di bilanciamento del carico interno usando Azure Resource Manager con PowerShell.</span><span class="sxs-lookup"><span data-stu-id="db507-110">The following steps explain how to create an internal load balancer using Azure Resource Manager with PowerShell.</span></span> <span data-ttu-id="db507-111">Con Azure Resource Manager, gli elementi per creare un servizio di bilanciamento del carico interno vengono configurati singolarmente e poi integrati per creare un servizio di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="db507-111">With Azure Resource Manager, the items to create a Internal load balancer are configured individually and then combined to create a load balancer.</span></span>

<span data-ttu-id="db507-112">È necessario creare e configurare gli oggetti seguenti per distribuire un servizio di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="db507-112">You need to create and configure the following objects to deploy a load balancer:</span></span>

* <span data-ttu-id="db507-113">Configurazione di IP front-end: configurazione dell'indirizzo IP privato per il traffico di rete in ingresso.</span><span class="sxs-lookup"><span data-stu-id="db507-113">Front end IP configuration - will configure the private IP address for incoming network traffic</span></span>
* <span data-ttu-id="db507-114">Pool di indirizzi back end: configurazione delle interfacce di rete che riceveranno il traffico con carico bilanciato proveniente dal pool di indirizzi IP front end.</span><span class="sxs-lookup"><span data-stu-id="db507-114">Backend address pool - will configure the network interfaces which will receive the load balanced traffic coming from front end IP pool</span></span>
* <span data-ttu-id="db507-115">Regole di bilanciamento del carico: configurazione delle porte di origine e locali per il servizio di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="db507-115">Load balancing rules - source and local port configuration for the load balancer.</span></span>
* <span data-ttu-id="db507-116">Probe: configurazione del probe dello stato di integrità per le istanze di macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="db507-116">Probes - configures the health status probe for the Virtual Machine instances.</span></span>
* <span data-ttu-id="db507-117">Regole NAT in ingresso: configurazione delle regole della porta per accedere direttamente a una delle istanze di macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="db507-117">Inbound NAT rules - configures the port rules to directly access one of the Virtual Machine instances.</span></span>

<span data-ttu-id="db507-118">È possibile ottenere altre informazioni sui componenti del servizio di bilanciamento del carico con Gestione risorse di Azure in [Supporto di Gestione risorse di Azure per il bilanciamento del carico](load-balancer-arm.md).</span><span class="sxs-lookup"><span data-stu-id="db507-118">You can get more information about load balancer components with Azure resource manager at [Azure Resource Manager support for load balancer](load-balancer-arm.md).</span></span>

<span data-ttu-id="db507-119">La procedura seguente illustra come configurare un servizio di bilanciamento del carico tra due macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="db507-119">The following steps explain how to configure a load balancer between two virtual machines.</span></span>

## <a name="setup-powershell-to-use-resource-manager"></a><span data-ttu-id="db507-120">Configurare PowerShell per l'uso di Gestione risorse</span><span class="sxs-lookup"><span data-stu-id="db507-120">Setup PowerShell to use Resource Manager</span></span>

<span data-ttu-id="db507-121">Assicurarsi di disporre della versione di produzione più recente del modulo Azure per PowerShell e di aver configurato correttamente PowerShell per l'accesso alla sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="db507-121">Make sure you have the latest production version of the Azure module for PowerShell, and have PowerShell setup correctly to access your Azure subscription.</span></span>

### <a name="step-1"></a><span data-ttu-id="db507-122">Passaggio 1</span><span class="sxs-lookup"><span data-stu-id="db507-122">Step 1</span></span>

```powershell
Login-AzureRmAccount
```

### <a name="step-2"></a><span data-ttu-id="db507-123">Passaggio 2</span><span class="sxs-lookup"><span data-stu-id="db507-123">Step 2</span></span>

<span data-ttu-id="db507-124">Controllare le sottoscrizioni per l'account</span><span class="sxs-lookup"><span data-stu-id="db507-124">Check the subscriptions for the account</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="db507-125">Verrà richiesto di eseguire l'autenticazione con le proprie credenziali.</span><span class="sxs-lookup"><span data-stu-id="db507-125">You will be prompted to Authenticate with your credentials.</span></span>

### <a name="step-3"></a><span data-ttu-id="db507-126">Passaggio 3</span><span class="sxs-lookup"><span data-stu-id="db507-126">Step 3</span></span>

<span data-ttu-id="db507-127">Scegliere quali sottoscrizioni Azure usare.</span><span class="sxs-lookup"><span data-stu-id="db507-127">Choose which of your Azure subscriptions to use.</span></span>

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="create-resource-group-for-load-balancer"></a><span data-ttu-id="db507-128">Creare un gruppo di risorse per il servizio di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="db507-128">Create Resource Group for load balancer</span></span>

<span data-ttu-id="db507-129">Creare un nuovo gruppo di risorse (ignorare questo passaggio se si usa un gruppo di risorse esistente)</span><span class="sxs-lookup"><span data-stu-id="db507-129">Create a new resource group (skip this step if using an existing resource group)</span></span>

```powershell
New-AzureRmResourceGroup -Name NRP-RG -location "West US"
```

<span data-ttu-id="db507-130">Azure Resource Manager richiede che tutti i gruppi di risorse specifichino una località.</span><span class="sxs-lookup"><span data-stu-id="db507-130">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="db507-131">che viene usato come percorso predefinito per le risorse presenti in tale gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="db507-131">This is used as the default location for resources in that resource group.</span></span> <span data-ttu-id="db507-132">Assicurarsi che tutti i comandi per creare un servizio di bilanciamento del carico usino lo stesso gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="db507-132">Make sure all commands to create a load balancer will use the same resource group.</span></span>

<span data-ttu-id="db507-133">Nell'esempio precedente sono stati creare un gruppo di risorse denominato "NRP-RG" e la località "West US".</span><span class="sxs-lookup"><span data-stu-id="db507-133">In the example above we created a resource group called "NRP-RG" and location "West US".</span></span>

## <a name="create-virtual-network-and-a-private-ip-address-for-front-end-ip-pool"></a><span data-ttu-id="db507-134">Creare la rete virtuale e un indirizzo IP privato per il pool di indirizzi IP front-end</span><span class="sxs-lookup"><span data-stu-id="db507-134">Create Virtual Network and a private IP address for front end IP pool</span></span>

<span data-ttu-id="db507-135">Crea una subnet per la rete virtuale e la assegna alla variabile $backendSubnet</span><span class="sxs-lookup"><span data-stu-id="db507-135">Creates a subnet for the virtual network and assigns to variable $backendSubnet</span></span>

```powershell
$backendSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -AddressPrefix 10.0.2.0/24
```

<span data-ttu-id="db507-136">Creare una rete virtuale:</span><span class="sxs-lookup"><span data-stu-id="db507-136">Create a virtual network:</span></span>

```powershell
$vnet= New-AzureRmVirtualNetwork -Name NRPVNet -ResourceGroupName NRP-RG -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $backendSubnet
```

<span data-ttu-id="db507-137">Crea la rete virtuale e aggiunge la subnet lb-subnet-be alla rete virtuale NRPVNet e la assegna alla variabile $vnet</span><span class="sxs-lookup"><span data-stu-id="db507-137">Creates the virtual network and adds the subnet lb-subnet-be to the virtual network NRPVNet and assigns to variable $vnet</span></span>

## <a name="create-front-end-ip-pool-and-backend-address-pool"></a><span data-ttu-id="db507-138">Creare il pool di indirizzi IP front-end e il pool di indirizzi back-end</span><span class="sxs-lookup"><span data-stu-id="db507-138">Create Front end IP pool and backend address pool</span></span>

<span data-ttu-id="db507-139">Configurazione di un pool di indirizzi IP front-end per il traffico di rete in ingresso del servizio di bilanciamento del carico e un pool di indirizzi back-end per ricevere il traffico sottoposto a bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="db507-139">Setting up a front end IP pool for the incoming load balancer network traffic and backend address pool to receive the load balanced traffic.</span></span>

### <a name="step-1"></a><span data-ttu-id="db507-140">Passaggio 1</span><span class="sxs-lookup"><span data-stu-id="db507-140">Step 1</span></span>

<span data-ttu-id="db507-141">Creare un pool IP front-end usando l'indirizzo IP privato 10.0.2.5 per la subnet 10.0.2.0/24 che sarà l'endpoint del traffico di rete in ingresso.</span><span class="sxs-lookup"><span data-stu-id="db507-141">Create a front end IP pool using the private IP address 10.0.2.5 for the subnet 10.0.2.0/24 which will be the incoming network traffic endpoint.</span></span>

```powershell
$frontendIP = New-AzureRmLoadBalancerFrontendIpConfig -Name LB-Frontend -PrivateIpAddress 10.0.2.5 -SubnetId $vnet.subnets[0].Id
```

### <a name="step-2"></a><span data-ttu-id="db507-142">Passaggio 2</span><span class="sxs-lookup"><span data-stu-id="db507-142">Step 2</span></span>

<span data-ttu-id="db507-143">Configurare un pool di indirizzi back-end usato per ricevere il traffico in ingresso dal pool di indirizzi IP front-end:</span><span class="sxs-lookup"><span data-stu-id="db507-143">Set up a back end address pool used to receive incoming traffic from front end IP pool:</span></span>

```powershell
$beaddresspool= New-AzureRmLoadBalancerBackendAddressPoolConfig -Name "LB-backend"
```

## <a name="create-lb-rules-nat-rules-probe-and-load-balancer"></a><span data-ttu-id="db507-144">Creare regole di bilanciamento del carico, regole NAT, probe e il servizio di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="db507-144">Create LB rules, NAT rules, probe and load balancer</span></span>

<span data-ttu-id="db507-145">Dopo aver creato il pool di indirizzi IP front-end e il pool di indirizzi back-end, è necessario creare le regole che faranno parte della risorsa di bilanciamento carico:</span><span class="sxs-lookup"><span data-stu-id="db507-145">After creating the front end IP pool and the backend address pool, you will need to create the rules which will belong to the load balancer resource:</span></span>

### <a name="step-1"></a><span data-ttu-id="db507-146">Passaggio 1</span><span class="sxs-lookup"><span data-stu-id="db507-146">Step 1</span></span>

```powershell
$inboundNATRule1= New-AzureRmLoadBalancerInboundNatRuleConfig -Name "RDP1" -FrontendIpConfiguration $frontendIP -Protocol TCP -FrontendPort 3441 -BackendPort 3389

$inboundNATRule2= New-AzureRmLoadBalancerInboundNatRuleConfig -Name "RDP2" -FrontendIpConfiguration $frontendIP -Protocol TCP -FrontendPort 3442 -BackendPort 3389

$healthProbe = New-AzureRmLoadBalancerProbeConfig -Name "HealthProbe" -RequestPath "HealthProbe.aspx" -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2

$lbrule = New-AzureRmLoadBalancerRuleConfig -Name "HTTP" -FrontendIpConfiguration $frontendIP -BackendAddressPool $beAddressPool -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 80
```

<span data-ttu-id="db507-147">L'esempio precedente crea gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="db507-147">The example above is creating the following items:</span></span>

* <span data-ttu-id="db507-148">Regola NAT secondo cui tutto il traffico in ingresso sulla porta 3441 passerà alla porta 3389.</span><span class="sxs-lookup"><span data-stu-id="db507-148">NAT rule which all incoming traffic to port 3441 will go to port 3389.</span></span>
* <span data-ttu-id="db507-149">Seconda regola NAT secondo cui tutto il traffico in ingresso sulla porta 3442 passerà alla porta 3389.</span><span class="sxs-lookup"><span data-stu-id="db507-149">a second NAT rule which all incoming traffic to port 3442 will go to port 3389.</span></span>
* <span data-ttu-id="db507-150">Regola di bilanciamento del carico per bilanciare il carico di tutto il traffico in ingresso sulla porta pubblica 80 alla porta locale 80 nel pool di indirizzi back-end.</span><span class="sxs-lookup"><span data-stu-id="db507-150">a load balancer rule which will load balance all incoming traffic on public port 80 to local port 80 in the back end address pool.</span></span>
* <span data-ttu-id="db507-151">Regola probe per il controllo dello stato di integrità del percorso "HealthProbe.aspx"</span><span class="sxs-lookup"><span data-stu-id="db507-151">a probe rule which will check the health status for path "HealthProbe.aspx"</span></span>

### <a name="step-2"></a><span data-ttu-id="db507-152">Passaggio 2</span><span class="sxs-lookup"><span data-stu-id="db507-152">Step 2</span></span>

<span data-ttu-id="db507-153">Creare il servizio di bilanciamento del carico aggiungendo tutti gli oggetti (regole NAT, regole di bilanciamento del carico, configurazioni di probe):</span><span class="sxs-lookup"><span data-stu-id="db507-153">Create the load balancer adding all objects (NAT rules, Load balancer rules, probe configurations) together:</span></span>

```powershell
$NRPLB = New-AzureRmLoadBalancer -ResourceGroupName "NRP-RG" -Name "NRP-LB" -Location "West US" -FrontendIpConfiguration $frontendIP -InboundNatRule $inboundNATRule1,$inboundNatRule2 -LoadBalancingRule $lbrule -BackendAddressPool $beAddressPool -Probe $healthProbe
```

## <a name="create-network-interfaces"></a><span data-ttu-id="db507-154">Creare interfacce di rete</span><span class="sxs-lookup"><span data-stu-id="db507-154">Create network interfaces</span></span>

<span data-ttu-id="db507-155">Dopo aver creato il servizio di bilanciamento del carico interno, è necessario definire quali interfacce di rete riceveranno il traffico di rete con bilanciamento del carico in ingresso, regole NAT e probe.</span><span class="sxs-lookup"><span data-stu-id="db507-155">After creating the internal load balancer, you need define which network interfaces will be receiving the incoming load balanced network traffic, NAT rules and probe.</span></span> <span data-ttu-id="db507-156">In questo caso, l'interfaccia di rete viene configurata singolarmente e può essere assegnata a una macchina virtuale in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="db507-156">The network interface in this case is configured individually and can be assigned to a virtual machine later on.</span></span>

### <a name="step-1"></a><span data-ttu-id="db507-157">Passaggio 1</span><span class="sxs-lookup"><span data-stu-id="db507-157">Step 1</span></span>

<span data-ttu-id="db507-158">Ottenere la rete virtuale di risorse e la subnet per creare interfacce di rete:</span><span class="sxs-lookup"><span data-stu-id="db507-158">Get the resource virtual network and subnet to create network interfaces:</span></span>

```powershell
$vnet = Get-AzureRmVirtualNetwork -Name NRPVNet -ResourceGroupName NRP-RG

$backendSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -VirtualNetwork $vnet
```

<span data-ttu-id="db507-159">In questo passaggio viene creata un'interfaccia di rete che farà parte del pool di back-end del servizio di bilanciamento del carico e che assocerà la prima regola NAT per RDP per questa interfaccia di rete:</span><span class="sxs-lookup"><span data-stu-id="db507-159">This step creates a network interface which will belong to the load balancer back end pool and associate the first NAT rule for RDP for this network interface:</span></span>

```powershell
$backendnic1= New-AzureRmNetworkInterface -ResourceGroupName "NRP-RG" -Name lb-nic1-be -Location "West US" -PrivateIpAddress 10.0.2.6 -Subnet $backendSubnet -LoadBalancerBackendAddressPool $nrplb.BackendAddressPools[0] -LoadBalancerInboundNatRule $nrplb.InboundNatRules[0]
```

### <a name="step-2"></a><span data-ttu-id="db507-160">Passaggio 2</span><span class="sxs-lookup"><span data-stu-id="db507-160">Step 2</span></span>

<span data-ttu-id="db507-161">Creare una seconda interfaccia di rete denominata LB-Nic2-BE:</span><span class="sxs-lookup"><span data-stu-id="db507-161">Create a second network interface called LB-Nic2-BE:</span></span>

<span data-ttu-id="db507-162">In questo passaggio viene creata una seconda interfaccia di rete, che sarà assegnata allo stesso pool di back-end del servizio di bilanciamento del carico e che assocerà la seconda regola NAT creata per RDP:</span><span class="sxs-lookup"><span data-stu-id="db507-162">This step creates a second network interface, assigning to the same load balancer back end pool and associating the second NAT rule created for RDP:</span></span>

```powershell
$backendnic2= New-AzureRmNetworkInterface -ResourceGroupName "NRP-RG" -Name lb-nic2-be -Location "West US" -PrivateIpAddress 10.0.2.7 -Subnet $backendSubnet -LoadBalancerBackendAddressPool $nrplb.BackendAddressPools[0] -LoadBalancerInboundNatRule $nrplb.InboundNatRules[1]
```

<span data-ttu-id="db507-163">Il risultato finale sarà simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="db507-163">The end result will show the following:</span></span>

    $backendnic1

<span data-ttu-id="db507-164">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="db507-164">Expected output:</span></span>

    Name                 : lb-nic1-be
    ResourceGroupName    : NRP-RG
    Location             : westus
    Id                   : /subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/networkInterfaces/lb-nic1-be
    Etag                 : W/"d448256a-e1df-413a-9103-a137e07276d1"
    ProvisioningState    : Succeeded
    Tags                 :
    VirtualMachine       : null
    IpConfigurations     : [
                         {
                           "PrivateIpAddress": "10.0.2.6",
                           "PrivateIpAllocationMethod": "Static",
                           "Subnet": {
                             "Id": "/subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/virtualNetworks/NRPVNet/subnets/LB-Subnet-BE"
                           },
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
                           "ProvisioningState": "Succeeded",
                           "Name": "ipconfig1",
                           "Etag": "W/\"d448256a-e1df-413a-9103-a137e07276d1\"",
                           "Id": "/subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/networkInterfaces/lb-nic1-be/ipConfigurations/ipconfig1"
                         }
                       ]
    DnsSettings          : {
                         "DnsServers": [],
                         "AppliedDnsServers": []
                       }
    AppliedDnsSettings   :
    NetworkSecurityGroup : null
    Primary              : False



### <a name="step-3"></a><span data-ttu-id="db507-165">Passaggio 3</span><span class="sxs-lookup"><span data-stu-id="db507-165">Step 3</span></span>

<span data-ttu-id="db507-166">Usare il comando Add-AzureRmVMNetworkInterface per assegnare la scheda di rete a una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="db507-166">Use the command Add-AzureRmVMNetworkInterface to assign the NIC to a virtual Machine.</span></span>

<span data-ttu-id="db507-167">Vedere il documento [Creare una VM Windows con Resource Manager e PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json) per le istruzioni dettagliate su come creare una macchina virtuale e assegnare una scheda di interfaccia di rete.</span><span class="sxs-lookup"><span data-stu-id="db507-167">You can find the step by step instructions to create a virtual machine and assign to a NIC following the documentation: [Create an Azure VM using PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).</span></span>

## <a name="add-the-network-interface"></a><span data-ttu-id="db507-168">Aggiungere l'interfaccia di rete</span><span class="sxs-lookup"><span data-stu-id="db507-168">Add the network interface</span></span>

<span data-ttu-id="db507-169">Se è già stata creata una macchina virtuale, è possibile aggiungere l'interfaccia di rete seguendo questa procedura:</span><span class="sxs-lookup"><span data-stu-id="db507-169">If you already have a virtual machine created, you can add the network interface with the following steps:</span></span>

### <a name="step-1"></a><span data-ttu-id="db507-170">Passaggio 1</span><span class="sxs-lookup"><span data-stu-id="db507-170">Step 1</span></span>

<span data-ttu-id="db507-171">Se non è ancora stata eseguita questa operazione, caricare la risorsa di bilanciamento del carico in una variabile.</span><span class="sxs-lookup"><span data-stu-id="db507-171">Load the load balancer resource into a variable (if you haven't done that yet).</span></span> <span data-ttu-id="db507-172">La variabile usata viene chiamata $lb e usa gli stessi nomi della risorsa di bilanciamento del carico creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="db507-172">The variable used is called $lb and use the same names from the load balancer resource created above.</span></span>

```powershell
$lb = Get-AzureRmLoadBalancer –name NRP-LB -resourcegroupname NRP-RG
```

### <a name="step-2"></a><span data-ttu-id="db507-173">Passaggio 2</span><span class="sxs-lookup"><span data-stu-id="db507-173">Step 2</span></span>

<span data-ttu-id="db507-174">Caricare la configurazione back-end in una variabile.</span><span class="sxs-lookup"><span data-stu-id="db507-174">Load the backend configuration to a variable.</span></span>

```powershell
$backend = Get-AzureRmLoadBalancerBackendAddressPoolConfig -name backendpool1 -LoadBalancer $lb
```

### <a name="step-3"></a><span data-ttu-id="db507-175">Passaggio 3</span><span class="sxs-lookup"><span data-stu-id="db507-175">Step 3</span></span>

<span data-ttu-id="db507-176">Caricare l'interfaccia di rete già creata in una variabile.</span><span class="sxs-lookup"><span data-stu-id="db507-176">Load the already created network interface into a variable.</span></span> <span data-ttu-id="db507-177">Il nome della variabile usata è $nic.</span><span class="sxs-lookup"><span data-stu-id="db507-177">the variable name used is $nic.</span></span> <span data-ttu-id="db507-178">Il nome dell'interfaccia di rete usata è lo stesso dell'esempio precedente.</span><span class="sxs-lookup"><span data-stu-id="db507-178">The network interface name used is the same from the example above.</span></span>

```powershell
$nic = Get-AzureRmNetworkInterface –name lb-nic1-be -resourcegroupname NRP-RG
```

### <a name="step-4"></a><span data-ttu-id="db507-179">Passaggio 4</span><span class="sxs-lookup"><span data-stu-id="db507-179">Step 4</span></span>

<span data-ttu-id="db507-180">Modificare la configurazione back-end nell'interfaccia di rete.</span><span class="sxs-lookup"><span data-stu-id="db507-180">Change the backend configuration on the network interface.</span></span>

```powershell
$nic.IpConfigurations[0].LoadBalancerBackendAddressPools=$backend
```

### <a name="step-5"></a><span data-ttu-id="db507-181">Passaggio 5</span><span class="sxs-lookup"><span data-stu-id="db507-181">Step 5</span></span>

<span data-ttu-id="db507-182">Salvare l'oggetto interfaccia di rete.</span><span class="sxs-lookup"><span data-stu-id="db507-182">Save the network interface object.</span></span>

```powershell
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

<span data-ttu-id="db507-183">Dopo che un'interfaccia di rete viene aggiunta al pool di back-end di bilanciamento del carico, inizia a ricevere il traffico di rete in base alle regole di bilanciamento del carico per la risorsa di bilanciamento carico.</span><span class="sxs-lookup"><span data-stu-id="db507-183">After a network interface is added to the load balancer backend pool, it starts receiving network traffic based on the load balancing rules for that load balancer resource.</span></span>

## <a name="update-an-existing-load-balancer"></a><span data-ttu-id="db507-184">Aggiornare un bilanciamento del carico esistente</span><span class="sxs-lookup"><span data-stu-id="db507-184">Update an existing load balancer</span></span>

### <a name="step-1"></a><span data-ttu-id="db507-185">Passaggio 1</span><span class="sxs-lookup"><span data-stu-id="db507-185">Step 1</span></span>
<span data-ttu-id="db507-186">Usare il servizio di bilanciamento del carico dall'esempio precedente, assegnare l'oggetto del servizio di bilanciamento del carico alla variabile $slb usando Get-AzureRmLoadBalancer</span><span class="sxs-lookup"><span data-stu-id="db507-186">Using the load balancer from the example above, assign load balancer object to variable $slb using Get-AzureRmLoadBalancer</span></span>

```powershell
$slb = Get-AzureRmLoadBalancer -Name NRPLB -ResourceGroupName NRP-RG
```

### <a name="step-2"></a><span data-ttu-id="db507-187">Passaggio 2</span><span class="sxs-lookup"><span data-stu-id="db507-187">Step 2</span></span>

<span data-ttu-id="db507-188">Nell'esempio seguente, si aggiungerà una nuova regola NAT in ingresso mediante la porta 81 nel front-end e la porta 8181 per il pool di back-end a un bilanciamento del carico esistente</span><span class="sxs-lookup"><span data-stu-id="db507-188">In the following example, you will add a new Inbound NAT rule using port 81 in the front end and port 8181 for the back end pool to an existing load balancer</span></span>

```powershell
$slb | Add-AzureRmLoadBalancerInboundNatRuleConfig -Name NewRule -FrontendIpConfiguration $slb.FrontendIpConfigurations[0] -FrontendPort 81  -BackendPort 8181 -Protocol Tcp
```

### <a name="step-3"></a><span data-ttu-id="db507-189">Passaggio 3</span><span class="sxs-lookup"><span data-stu-id="db507-189">Step 3</span></span>

<span data-ttu-id="db507-190">Salvare la nuova configurazione utilizzando Set AzureLoadBalancer</span><span class="sxs-lookup"><span data-stu-id="db507-190">Save the new configuration using Set-AzureLoadBalancer</span></span>

```powershell
$slb | Set-AzureRmLoadBalancer
```

## <a name="remove-a-load-balancer"></a><span data-ttu-id="db507-191">Rimuovere un bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="db507-191">Remove a load balancer</span></span>

<span data-ttu-id="db507-192">Usare il comando Remove-AzureRmLoadBalancerr per eliminare un servizio di bilanciamento del carico creato in precedenza denominato "NRP-LB" in un gruppo di risorse denominato "NRP-RG"</span><span class="sxs-lookup"><span data-stu-id="db507-192">Use the command Remove-AzureRmLoadBalancer to delete a previously created load balancer named "NRP-LB"  in a resource group called "NRP-RG"</span></span>

```powershell
Remove-AzureRmLoadBalancer -Name NRPLB -ResourceGroupName NRP-RG
```

> [!NOTE]
> <span data-ttu-id="db507-193">È possibile utilizzare l’opzione facoltativa - Forzare per evitare la richiesta di eliminazione.</span><span class="sxs-lookup"><span data-stu-id="db507-193">You can use the optional switch -Force to avoid the prompt for deletion.</span></span>

## <a name="next-steps"></a><span data-ttu-id="db507-194">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="db507-194">Next steps</span></span>

[<span data-ttu-id="db507-195">Configurare una modalità di distribuzione del bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="db507-195">Configure a Load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="db507-196">Configurare le impostazioni del timeout di inattività TCP per il bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="db507-196">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
