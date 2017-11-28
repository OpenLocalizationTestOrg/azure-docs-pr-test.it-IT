---
title: Azure interna aaaCreate bilanciamento del carico - PowerShell | Documenti Microsoft
description: Informazioni su come toocreate un interno bilanciamento del carico con PowerShell in Gestione risorse
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
ms.openlocfilehash: 4b9657c77aa32a142de49ff7871ed6a396b22223
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-internal-load-balancer-using-powershell"></a><span data-ttu-id="be342-103">Creare un servizio di bilanciamento del carico interno con PowerShell</span><span class="sxs-lookup"><span data-stu-id="be342-103">Create an internal load balancer using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="be342-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="be342-104">Azure Portal</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-portal.md)
> * [<span data-ttu-id="be342-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="be342-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-ps.md)
> * [<span data-ttu-id="be342-106">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="be342-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-cli.md)
> * [<span data-ttu-id="be342-107">Modello</span><span class="sxs-lookup"><span data-stu-id="be342-107">Template</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-template.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="be342-108">Azure offre due modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="be342-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="be342-109">In questo articolo viene illustrato l'utilizzo modello di distribuzione di gestione delle risorse hello, si consiglia di per la maggior parte delle nuove distribuzioni anziché hello [modello di distribuzione classica](load-balancer-get-started-ilb-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="be342-109">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello [classic deployment model](load-balancer-get-started-ilb-classic-ps.md).</span></span>

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

<span data-ttu-id="be342-110">Hello alla procedura seguente viene illustrato come toocreate un interno bilanciamento del carico con Gestione risorse di Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="be342-110">hello following steps explain how toocreate an internal load balancer using Azure Resource Manager with PowerShell.</span></span> <span data-ttu-id="be342-111">Con Gestione risorse di Azure, hello elementi toocreate un bilanciamento del carico interno vengono configurate singolarmente e quindi combinati toocreate un bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="be342-111">With Azure Resource Manager, hello items toocreate a Internal load balancer are configured individually and then combined toocreate a load balancer.</span></span>

<span data-ttu-id="be342-112">È necessario toocreate e configurare hello oggetti toodeploy un bilanciamento del carico seguenti:</span><span class="sxs-lookup"><span data-stu-id="be342-112">You need toocreate and configure hello following objects toodeploy a load balancer:</span></span>

* <span data-ttu-id="be342-113">Configurazione IP end front - configurerà l'indirizzo IP privato hello in arrivo il traffico di rete</span><span class="sxs-lookup"><span data-stu-id="be342-113">Front end IP configuration - will configure hello private IP address for incoming network traffic</span></span>
* <span data-ttu-id="be342-114">Pool di indirizzi back-end - configurerà le interfacce di rete hello che riceveranno il traffico con carico bilanciato hello in arrivo dal pool IP front-end</span><span class="sxs-lookup"><span data-stu-id="be342-114">Backend address pool - will configure hello network interfaces which will receive hello load balanced traffic coming from front end IP pool</span></span>
* <span data-ttu-id="be342-115">Regole di bilanciamento del carico - di origine e configurazione della porta locale per hello bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="be342-115">Load balancing rules - source and local port configuration for hello load balancer.</span></span>
* <span data-ttu-id="be342-116">Probe - configura i probe di stato di integrità hello per le istanze di macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="be342-116">Probes - configures hello health status probe for hello Virtual Machine instances.</span></span>
* <span data-ttu-id="be342-117">Regole NAT in ingresso - configurare l'accesso alla toodirectly regole di porta hello una delle istanze di macchine virtuali hello.</span><span class="sxs-lookup"><span data-stu-id="be342-117">Inbound NAT rules - configures hello port rules toodirectly access one of hello Virtual Machine instances.</span></span>

<span data-ttu-id="be342-118">È possibile ottenere altre informazioni sui componenti del servizio di bilanciamento del carico con Gestione risorse di Azure in [Supporto di Gestione risorse di Azure per il bilanciamento del carico](load-balancer-arm.md).</span><span class="sxs-lookup"><span data-stu-id="be342-118">You can get more information about load balancer components with Azure resource manager at [Azure Resource Manager support for load balancer](load-balancer-arm.md).</span></span>

<span data-ttu-id="be342-119">Hello passaggi seguenti illustrano come tooconfigure un bilanciamento del carico tra due macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="be342-119">hello following steps explain how tooconfigure a load balancer between two virtual machines.</span></span>

## <a name="setup-powershell-toouse-resource-manager"></a><span data-ttu-id="be342-120">Il programma di installazione PowerShell toouse Gestione risorse</span><span class="sxs-lookup"><span data-stu-id="be342-120">Setup PowerShell toouse Resource Manager</span></span>

<span data-ttu-id="be342-121">Assicurarsi di disporre hello ultima versione di produzione di hello modulo Azure per PowerShell e PowerShell è installato installazione tooaccess correttamente la sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="be342-121">Make sure you have hello latest production version of hello Azure module for PowerShell, and have PowerShell setup correctly tooaccess your Azure subscription.</span></span>

### <a name="step-1"></a><span data-ttu-id="be342-122">Passaggio 1</span><span class="sxs-lookup"><span data-stu-id="be342-122">Step 1</span></span>

```powershell
Login-AzureRmAccount
```

### <a name="step-2"></a><span data-ttu-id="be342-123">Passaggio 2</span><span class="sxs-lookup"><span data-stu-id="be342-123">Step 2</span></span>

<span data-ttu-id="be342-124">Controllare le sottoscrizioni di hello per account hello</span><span class="sxs-lookup"><span data-stu-id="be342-124">Check hello subscriptions for hello account</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="be342-125">Sarà richiesto tooAuthenticate con le credenziali.</span><span class="sxs-lookup"><span data-stu-id="be342-125">You will be prompted tooAuthenticate with your credentials.</span></span>

### <a name="step-3"></a><span data-ttu-id="be342-126">Passaggio 3</span><span class="sxs-lookup"><span data-stu-id="be342-126">Step 3</span></span>

<span data-ttu-id="be342-127">Scegliere quali di toouse le sottoscrizioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="be342-127">Choose which of your Azure subscriptions toouse.</span></span>

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="create-resource-group-for-load-balancer"></a><span data-ttu-id="be342-128">Creare un gruppo di risorse per il servizio di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="be342-128">Create Resource Group for load balancer</span></span>

<span data-ttu-id="be342-129">Creare un nuovo gruppo di risorse (ignorare questo passaggio se si usa un gruppo di risorse esistente)</span><span class="sxs-lookup"><span data-stu-id="be342-129">Create a new resource group (skip this step if using an existing resource group)</span></span>

```powershell
New-AzureRmResourceGroup -Name NRP-RG -location "West US"
```

<span data-ttu-id="be342-130">Gestione risorse di Azure richiede che tutti i gruppi di risorse specifichino un percorso</span><span class="sxs-lookup"><span data-stu-id="be342-130">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="be342-131">Viene utilizzato come percorso predefinito di hello per le risorse in tale gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="be342-131">This is used as hello default location for resources in that resource group.</span></span> <span data-ttu-id="be342-132">Assicurarsi che tutti i comandi toocreate utilizzerà un bilanciamento del carico hello stesso gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="be342-132">Make sure all commands toocreate a load balancer will use hello same resource group.</span></span>

<span data-ttu-id="be342-133">In hello esempio precedente viene creato un gruppo di risorse denominato "NRP-RG" e il percorso "Stati Uniti occidentali".</span><span class="sxs-lookup"><span data-stu-id="be342-133">In hello example above we created a resource group called "NRP-RG" and location "West US".</span></span>

## <a name="create-virtual-network-and-a-private-ip-address-for-front-end-ip-pool"></a><span data-ttu-id="be342-134">Creare la rete virtuale e un indirizzo IP privato per il pool di indirizzi IP front-end</span><span class="sxs-lookup"><span data-stu-id="be342-134">Create Virtual Network and a private IP address for front end IP pool</span></span>

<span data-ttu-id="be342-135">Crea una subnet per la rete virtuale hello e assegna toovariable $backendSubnet</span><span class="sxs-lookup"><span data-stu-id="be342-135">Creates a subnet for hello virtual network and assigns toovariable $backendSubnet</span></span>

```powershell
$backendSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -AddressPrefix 10.0.2.0/24
```

<span data-ttu-id="be342-136">Creare una rete virtuale:</span><span class="sxs-lookup"><span data-stu-id="be342-136">Create a virtual network:</span></span>

```powershell
$vnet= New-AzureRmVirtualNetwork -Name NRPVNet -ResourceGroupName NRP-RG -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $backendSubnet
```

<span data-ttu-id="be342-137">Crea rete virtuale hello e aggiunge una rete virtuale di essere lb-subnet toohello subnet hello NRPVNet e assegna toovariable $vnet</span><span class="sxs-lookup"><span data-stu-id="be342-137">Creates hello virtual network and adds hello subnet lb-subnet-be toohello virtual network NRPVNet and assigns toovariable $vnet</span></span>

## <a name="create-front-end-ip-pool-and-backend-address-pool"></a><span data-ttu-id="be342-138">Creare il pool di indirizzi IP front-end e il pool di indirizzi back-end</span><span class="sxs-lookup"><span data-stu-id="be342-138">Create Front end IP pool and backend address pool</span></span>

<span data-ttu-id="be342-139">Impostazione di un pool IP front-end per hello in arrivo carico del traffico di rete del servizio di bilanciamento e traffico con carico bilanciato di back-end indirizzi pool tooreceive hello.</span><span class="sxs-lookup"><span data-stu-id="be342-139">Setting up a front end IP pool for hello incoming load balancer network traffic and backend address pool tooreceive hello load balanced traffic.</span></span>

### <a name="step-1"></a><span data-ttu-id="be342-140">Passaggio 1</span><span class="sxs-lookup"><span data-stu-id="be342-140">Step 1</span></span>

<span data-ttu-id="be342-141">Creare un pool IP di front-end utilizzando l'indirizzo IP privato hello 10.0.2.5 per hello subnet 10.0.2.0/24 che sarà l'endpoint del traffico di rete in ingresso hello.</span><span class="sxs-lookup"><span data-stu-id="be342-141">Create a front end IP pool using hello private IP address 10.0.2.5 for hello subnet 10.0.2.0/24 which will be hello incoming network traffic endpoint.</span></span>

```powershell
$frontendIP = New-AzureRmLoadBalancerFrontendIpConfig -Name LB-Frontend -PrivateIpAddress 10.0.2.5 -SubnetId $vnet.subnets[0].Id
```

### <a name="step-2"></a><span data-ttu-id="be342-142">Passaggio 2</span><span class="sxs-lookup"><span data-stu-id="be342-142">Step 2</span></span>

<span data-ttu-id="be342-143">Configurare un pool di indirizzi back-end utilizzato traffico in ingresso tooreceive dal pool IP front-end:</span><span class="sxs-lookup"><span data-stu-id="be342-143">Set up a back end address pool used tooreceive incoming traffic from front end IP pool:</span></span>

```powershell
$beaddresspool= New-AzureRmLoadBalancerBackendAddressPoolConfig -Name "LB-backend"
```

## <a name="create-lb-rules-nat-rules-probe-and-load-balancer"></a><span data-ttu-id="be342-144">Creare regole di bilanciamento del carico, regole NAT, probe e il servizio di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="be342-144">Create LB rules, NAT rules, probe and load balancer</span></span>

<span data-ttu-id="be342-145">Dopo la creazione di pool IP front-end di hello e pool di indirizzi back-end di hello, è necessario utilizzare le regole di hello toocreate apparterranno toohello risorsa di bilanciamento del carico:</span><span class="sxs-lookup"><span data-stu-id="be342-145">After creating hello front end IP pool and hello backend address pool, you will need toocreate hello rules which will belong toohello load balancer resource:</span></span>

### <a name="step-1"></a><span data-ttu-id="be342-146">Passaggio 1</span><span class="sxs-lookup"><span data-stu-id="be342-146">Step 1</span></span>

```powershell
$inboundNATRule1= New-AzureRmLoadBalancerInboundNatRuleConfig -Name "RDP1" -FrontendIpConfiguration $frontendIP -Protocol TCP -FrontendPort 3441 -BackendPort 3389

$inboundNATRule2= New-AzureRmLoadBalancerInboundNatRuleConfig -Name "RDP2" -FrontendIpConfiguration $frontendIP -Protocol TCP -FrontendPort 3442 -BackendPort 3389

$healthProbe = New-AzureRmLoadBalancerProbeConfig -Name "HealthProbe" -RequestPath "HealthProbe.aspx" -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2

$lbrule = New-AzureRmLoadBalancerRuleConfig -Name "HTTP" -FrontendIpConfiguration $frontendIP -BackendAddressPool $beAddressPool -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 80
```

<span data-ttu-id="be342-147">esempio Hello precedente crea hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="be342-147">hello example above is creating hello following items:</span></span>

* <span data-ttu-id="be342-148">La regola NAT tutti in ingresso che il traffico tooport 3441 entra tooport 3389.</span><span class="sxs-lookup"><span data-stu-id="be342-148">NAT rule which all incoming traffic tooport 3441 will go tooport 3389.</span></span>
* <span data-ttu-id="be342-149">una seconda regola NAT tutti in ingresso che il traffico tooport 3442 entra tooport 3389.</span><span class="sxs-lookup"><span data-stu-id="be342-149">a second NAT rule which all incoming traffic tooport 3442 will go tooport 3389.</span></span>
* <span data-ttu-id="be342-150">una regola di bilanciamento del carico che caricherà bilanciare tutto il traffico in ingresso sulla porta di porta pubblica 80 toolocal 80 nel pool di indirizzi back-end hello.</span><span class="sxs-lookup"><span data-stu-id="be342-150">a load balancer rule which will load balance all incoming traffic on public port 80 toolocal port 80 in hello back end address pool.</span></span>
* <span data-ttu-id="be342-151">una regola di probe che controlla lo stato di integrità hello per il percorso "HealthProbe.aspx"</span><span class="sxs-lookup"><span data-stu-id="be342-151">a probe rule which will check hello health status for path "HealthProbe.aspx"</span></span>

### <a name="step-2"></a><span data-ttu-id="be342-152">Passaggio 2</span><span class="sxs-lookup"><span data-stu-id="be342-152">Step 2</span></span>

<span data-ttu-id="be342-153">Creazione di bilanciamento del carico hello sommando tutti gli oggetti (le regole NAT, regole di bilanciamento del carico, le configurazioni di probe):</span><span class="sxs-lookup"><span data-stu-id="be342-153">Create hello load balancer adding all objects (NAT rules, Load balancer rules, probe configurations) together:</span></span>

```powershell
$NRPLB = New-AzureRmLoadBalancer -ResourceGroupName "NRP-RG" -Name "NRP-LB" -Location "West US" -FrontendIpConfiguration $frontendIP -InboundNatRule $inboundNATRule1,$inboundNatRule2 -LoadBalancingRule $lbrule -BackendAddressPool $beAddressPool -Probe $healthProbe
```

## <a name="create-network-interfaces"></a><span data-ttu-id="be342-154">Creare interfacce di rete</span><span class="sxs-lookup"><span data-stu-id="be342-154">Create network interfaces</span></span>

<span data-ttu-id="be342-155">Dopo la creazione di bilanciamento del carico interno hello, è necessario definire le interfacce di rete verranno ricevuto hello in arrivo con carico bilanciato il traffico di rete, le regole NAT e probe.</span><span class="sxs-lookup"><span data-stu-id="be342-155">After creating hello internal load balancer, you need define which network interfaces will be receiving hello incoming load balanced network traffic, NAT rules and probe.</span></span> <span data-ttu-id="be342-156">in questo caso, l'interfaccia di rete Hello viene configurata singolarmente e può essere assegnato macchina virtuale tooa in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="be342-156">hello network interface in this case is configured individually and can be assigned tooa virtual machine later on.</span></span>

### <a name="step-1"></a><span data-ttu-id="be342-157">Passaggio 1</span><span class="sxs-lookup"><span data-stu-id="be342-157">Step 1</span></span>

<span data-ttu-id="be342-158">Ottenere risorse hello virtuale rete e subnet toocreate interfacce di rete:</span><span class="sxs-lookup"><span data-stu-id="be342-158">Get hello resource virtual network and subnet toocreate network interfaces:</span></span>

```powershell
$vnet = Get-AzureRmVirtualNetwork -Name NRPVNet -ResourceGroupName NRP-RG

$backendSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -VirtualNetwork $vnet
```

<span data-ttu-id="be342-159">Questo passaggio viene creata un'interfaccia di rete che appartengono a pool back-end di bilanciamento del carico toohello e associare la regola NAT prima hello per RDP per questa interfaccia di rete:</span><span class="sxs-lookup"><span data-stu-id="be342-159">This step creates a network interface which will belong toohello load balancer back end pool and associate hello first NAT rule for RDP for this network interface:</span></span>

```powershell
$backendnic1= New-AzureRmNetworkInterface -ResourceGroupName "NRP-RG" -Name lb-nic1-be -Location "West US" -PrivateIpAddress 10.0.2.6 -Subnet $backendSubnet -LoadBalancerBackendAddressPool $nrplb.BackendAddressPools[0] -LoadBalancerInboundNatRule $nrplb.InboundNatRules[0]
```

### <a name="step-2"></a><span data-ttu-id="be342-160">Passaggio 2</span><span class="sxs-lookup"><span data-stu-id="be342-160">Step 2</span></span>

<span data-ttu-id="be342-161">Creare una seconda interfaccia di rete denominata LB-Nic2-BE:</span><span class="sxs-lookup"><span data-stu-id="be342-161">Create a second network interface called LB-Nic2-BE:</span></span>

<span data-ttu-id="be342-162">Questo passaggio viene creata una seconda interfaccia di rete, assegnazione toohello il bilanciamento del carico stesso terminare pool e associare la regola NAT secondo hello creato per RDP:</span><span class="sxs-lookup"><span data-stu-id="be342-162">This step creates a second network interface, assigning toohello same load balancer back end pool and associating hello second NAT rule created for RDP:</span></span>

```powershell
$backendnic2= New-AzureRmNetworkInterface -ResourceGroupName "NRP-RG" -Name lb-nic2-be -Location "West US" -PrivateIpAddress 10.0.2.7 -Subnet $backendSubnet -LoadBalancerBackendAddressPool $nrplb.BackendAddressPools[0] -LoadBalancerInboundNatRule $nrplb.InboundNatRules[1]
```

<span data-ttu-id="be342-163">risultato finale Hello mostrerà seguente hello:</span><span class="sxs-lookup"><span data-stu-id="be342-163">hello end result will show hello following:</span></span>

    $backendnic1

<span data-ttu-id="be342-164">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="be342-164">Expected output:</span></span>

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



### <a name="step-3"></a><span data-ttu-id="be342-165">Passaggio 3</span><span class="sxs-lookup"><span data-stu-id="be342-165">Step 3</span></span>

<span data-ttu-id="be342-166">Utilizzare hello comando Add-AzureRmVMNetworkInterface tooassign hello NIC tooa macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="be342-166">Use hello command Add-AzureRmVMNetworkInterface tooassign hello NIC tooa virtual Machine.</span></span>

<span data-ttu-id="be342-167">È possibile trovare istruzioni dettagliate toocreate una macchina virtuale hello e assegnare tooa NIC seguente documentazione hello: [creare una macchina virtuale di Azure con PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="be342-167">You can find hello step by step instructions toocreate a virtual machine and assign tooa NIC following hello documentation: [Create an Azure VM using PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).</span></span>

## <a name="add-hello-network-interface"></a><span data-ttu-id="be342-168">Aggiungere l'interfaccia di rete hello</span><span class="sxs-lookup"><span data-stu-id="be342-168">Add hello network interface</span></span>

<span data-ttu-id="be342-169">Se si dispone già di una macchina virtuale creata, è possibile aggiungere l'interfaccia di rete hello con hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="be342-169">If you already have a virtual machine created, you can add hello network interface with hello following steps:</span></span>

### <a name="step-1"></a><span data-ttu-id="be342-170">Passaggio 1</span><span class="sxs-lookup"><span data-stu-id="be342-170">Step 1</span></span>

<span data-ttu-id="be342-171">Caricare la risorsa di servizio di bilanciamento carico hello in una variabile (se non è stato fatto che ancora).</span><span class="sxs-lookup"><span data-stu-id="be342-171">Load hello load balancer resource into a variable (if you haven't done that yet).</span></span> <span data-ttu-id="be342-172">variabile di Hello utilizzato è denominato $lb e utilizzare hello stessi nomi di risorsa di bilanciamento del carico hello creati in precedenza.</span><span class="sxs-lookup"><span data-stu-id="be342-172">hello variable used is called $lb and use hello same names from hello load balancer resource created above.</span></span>

```powershell
$lb = Get-AzureRmLoadBalancer –name NRP-LB -resourcegroupname NRP-RG
```

### <a name="step-2"></a><span data-ttu-id="be342-173">Passaggio 2</span><span class="sxs-lookup"><span data-stu-id="be342-173">Step 2</span></span>

<span data-ttu-id="be342-174">Carica la variabile tooa di configurazione back-end di hello.</span><span class="sxs-lookup"><span data-stu-id="be342-174">Load hello backend configuration tooa variable.</span></span>

```powershell
$backend = Get-AzureRmLoadBalancerBackendAddressPoolConfig -name backendpool1 -LoadBalancer $lb
```

### <a name="step-3"></a><span data-ttu-id="be342-175">Passaggio 3</span><span class="sxs-lookup"><span data-stu-id="be342-175">Step 3</span></span>

<span data-ttu-id="be342-176">Caricare l'interfaccia di rete hello già creato in una variabile.</span><span class="sxs-lookup"><span data-stu-id="be342-176">Load hello already created network interface into a variable.</span></span> <span data-ttu-id="be342-177">nome della variabile Hello utilizzato è $ scheda di rete.</span><span class="sxs-lookup"><span data-stu-id="be342-177">hello variable name used is $nic.</span></span> <span data-ttu-id="be342-178">nome di interfaccia di rete Hello utilizzato è hello stesso esempio hello precedente.</span><span class="sxs-lookup"><span data-stu-id="be342-178">hello network interface name used is hello same from hello example above.</span></span>

```powershell
$nic = Get-AzureRmNetworkInterface –name lb-nic1-be -resourcegroupname NRP-RG
```

### <a name="step-4"></a><span data-ttu-id="be342-179">Passaggio 4</span><span class="sxs-lookup"><span data-stu-id="be342-179">Step 4</span></span>

<span data-ttu-id="be342-180">Modificare la configurazione back-end di hello nell'interfaccia di rete hello.</span><span class="sxs-lookup"><span data-stu-id="be342-180">Change hello backend configuration on hello network interface.</span></span>

```powershell
$nic.IpConfigurations[0].LoadBalancerBackendAddressPools=$backend
```

### <a name="step-5"></a><span data-ttu-id="be342-181">Passaggio 5</span><span class="sxs-lookup"><span data-stu-id="be342-181">Step 5</span></span>

<span data-ttu-id="be342-182">Salvare un oggetto di interfaccia di rete hello.</span><span class="sxs-lookup"><span data-stu-id="be342-182">Save hello network interface object.</span></span>

```powershell
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

<span data-ttu-id="be342-183">Dopo l'aggiunta di un'interfaccia di rete pool back-end di bilanciamento del carico toohello, avvia la ricezione di traffico di rete in base alle regole per la risorsa del servizio di bilanciamento carico di bilanciamento del carico di hello.</span><span class="sxs-lookup"><span data-stu-id="be342-183">After a network interface is added toohello load balancer backend pool, it starts receiving network traffic based on hello load balancing rules for that load balancer resource.</span></span>

## <a name="update-an-existing-load-balancer"></a><span data-ttu-id="be342-184">Aggiornare un bilanciamento del carico esistente</span><span class="sxs-lookup"><span data-stu-id="be342-184">Update an existing load balancer</span></span>

### <a name="step-1"></a><span data-ttu-id="be342-185">Passaggio 1</span><span class="sxs-lookup"><span data-stu-id="be342-185">Step 1</span></span>
<span data-ttu-id="be342-186">Usa bilanciamento del carico hello dall'esempio hello precedente, assegnare $slb utilizzando Get-AzureRmLoadBalancer toovariable di oggetto servizio di bilanciamento carico</span><span class="sxs-lookup"><span data-stu-id="be342-186">Using hello load balancer from hello example above, assign load balancer object toovariable $slb using Get-AzureRmLoadBalancer</span></span>

```powershell
$slb = Get-AzureRmLoadBalancer -Name NRPLB -ResourceGroupName NRP-RG
```

### <a name="step-2"></a><span data-ttu-id="be342-187">Passaggio 2</span><span class="sxs-lookup"><span data-stu-id="be342-187">Step 2</span></span>

<span data-ttu-id="be342-188">Nell'esempio seguente di hello, si aggiungerà una nuova regola NAT in ingresso utilizzando la porta 81 nel front-end hello e porta 8181 per il backup di hello end di bilanciamento del carico di pool tooan esistente</span><span class="sxs-lookup"><span data-stu-id="be342-188">In hello following example, you will add a new Inbound NAT rule using port 81 in hello front end and port 8181 for hello back end pool tooan existing load balancer</span></span>

```powershell
$slb | Add-AzureRmLoadBalancerInboundNatRuleConfig -Name NewRule -FrontendIpConfiguration $slb.FrontendIpConfigurations[0] -FrontendPort 81  -BackendPort 8181 -Protocol Tcp
```

### <a name="step-3"></a><span data-ttu-id="be342-189">Passaggio 3</span><span class="sxs-lookup"><span data-stu-id="be342-189">Step 3</span></span>

<span data-ttu-id="be342-190">Salvare hello nuova configurazione utilizzando Set-AzureLoadBalancer</span><span class="sxs-lookup"><span data-stu-id="be342-190">Save hello new configuration using Set-AzureLoadBalancer</span></span>

```powershell
$slb | Set-AzureRmLoadBalancer
```

## <a name="remove-a-load-balancer"></a><span data-ttu-id="be342-191">Rimuovere un bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="be342-191">Remove a load balancer</span></span>

<span data-ttu-id="be342-192">Utilizzare hello comando Remove-AzureRmLoadBalancer toodelete un bilanciamento del carico creato in precedenza denominata "NRP-LB" in un gruppo di risorse denominato "NRP-RG"</span><span class="sxs-lookup"><span data-stu-id="be342-192">Use hello command Remove-AzureRmLoadBalancer toodelete a previously created load balancer named "NRP-LB"  in a resource group called "NRP-RG"</span></span>

```powershell
Remove-AzureRmLoadBalancer -Name NRPLB -ResourceGroupName NRP-RG
```

> [!NOTE]
> <span data-ttu-id="be342-193">È possibile utilizzare hello facoltativo switch - Force tooavoid hello Richiedi l'eliminazione.</span><span class="sxs-lookup"><span data-stu-id="be342-193">You can use hello optional switch -Force tooavoid hello prompt for deletion.</span></span>

## <a name="next-steps"></a><span data-ttu-id="be342-194">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="be342-194">Next steps</span></span>

[<span data-ttu-id="be342-195">Configurare una modalità di distribuzione del bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="be342-195">Configure a Load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="be342-196">Configurare le impostazioni del timeout di inattività TCP per il bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="be342-196">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
