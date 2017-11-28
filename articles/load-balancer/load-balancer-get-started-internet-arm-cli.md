---
title: con una connessione Internet aaaCreate bilanciamento del carico - CLI di Azure | Documenti Microsoft
description: Informazioni su come toocreate un Internet rivolto al bilanciamento del carico con Gestione risorse hello CLI di Azure
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: a8bcdd88-f94c-4537-8143-c710eaa86818
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: cadb5edb3b4a4e2f0813109d027eaafdc7ef7303
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="creating-an-internet-load-balancer-using-hello-azure-cli"></a><span data-ttu-id="9c9e1-103">Creazione di un bilanciamento del carico internet utilizzando hello CLI di Azure</span><span class="sxs-lookup"><span data-stu-id="9c9e1-103">Creating an internet load balancer using hello Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="9c9e1-104">Portale</span><span class="sxs-lookup"><span data-stu-id="9c9e1-104">Portal</span></span>](../load-balancer/load-balancer-get-started-internet-portal.md)
> * [<span data-ttu-id="9c9e1-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9c9e1-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-internet-arm-ps.md)
> * [<span data-ttu-id="9c9e1-106">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="9c9e1-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-internet-arm-cli.md)
> * [<span data-ttu-id="9c9e1-107">Modello</span><span class="sxs-lookup"><span data-stu-id="9c9e1-107">Template</span></span>](../load-balancer/load-balancer-get-started-internet-arm-template.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="9c9e1-108">Questo articolo descrive il modello di distribuzione di gestione risorse di hello.</span><span class="sxs-lookup"><span data-stu-id="9c9e1-108">This article covers hello Resource Manager deployment model.</span></span> <span data-ttu-id="9c9e1-109">È anche possibile [informazioni su come toocreate una connessione Internet bilanciamento del carico utilizzando la distribuzione classica](load-balancer-get-started-internet-classic-portal.md)</span><span class="sxs-lookup"><span data-stu-id="9c9e1-109">You can also [Learn how toocreate an Internet facing load balancer using classic deployment](load-balancer-get-started-internet-classic-portal.md)</span></span>

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="deploying-hello-solution-using-hello-azure-cli"></a><span data-ttu-id="9c9e1-110">La distribuzione di soluzioni hello utilizzando hello CLI di Azure</span><span class="sxs-lookup"><span data-stu-id="9c9e1-110">Deploying hello solution using hello Azure CLI</span></span>

<span data-ttu-id="9c9e1-111">Hello alla procedura seguente viene illustrato come una connessione Internet toocreate bilanciamento del carico con Gestione risorse di Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="9c9e1-111">hello following steps show how toocreate an Internet facing load balancer using Azure Resource Manager with CLI.</span></span> <span data-ttu-id="9c9e1-112">Con Gestione risorse di Azure creata e configurata singolarmente ogni risorsa, quindi riunire toocreate una risorsa.</span><span class="sxs-lookup"><span data-stu-id="9c9e1-112">With Azure Resource Manager each resource is created and configured individually, then put together toocreate a resource.</span></span>

<span data-ttu-id="9c9e1-113">È necessario creare e configurare hello oggetti toodeploy un bilanciamento del carico seguenti:</span><span class="sxs-lookup"><span data-stu-id="9c9e1-113">You must create and configure hello following objects toodeploy a load balancer:</span></span>

* <span data-ttu-id="9c9e1-114">Configurazione di IP front-end: contiene gli indirizzi IP pubblici per il traffico di rete in ingresso.</span><span class="sxs-lookup"><span data-stu-id="9c9e1-114">Front-end IP configuration - contains public IP addresses for incoming network traffic.</span></span>
* <span data-ttu-id="9c9e1-115">Pool di indirizzi di back-end - contiene le interfacce di rete (NIC) per tooreceive il traffico di rete dal servizio di bilanciamento del carico hello hello macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="9c9e1-115">Back-end address pool - contains network interfaces (NICs) for hello virtual machines tooreceive network traffic from hello load balancer.</span></span>
* <span data-ttu-id="9c9e1-116">Regole di bilanciamento del carico - contiene le regole di mapping di una porta pubblica su tooport del servizio di bilanciamento carico di hello nel pool di indirizzi back-end di hello.</span><span class="sxs-lookup"><span data-stu-id="9c9e1-116">Load balancing rules - contains rules mapping a public port on hello load balancer tooport in hello back-end address pool.</span></span>
* <span data-ttu-id="9c9e1-117">Regole NAT in ingresso - contiene le regole di mapping di una porta pubblica nella porta di tooa del bilanciamento del carico hello per una macchina virtuale specifica nel pool di indirizzi back-end di hello.</span><span class="sxs-lookup"><span data-stu-id="9c9e1-117">Inbound NAT rules - contains rules mapping a public port on hello load balancer tooa port for a specific virtual machine in hello back-end address pool.</span></span>
* <span data-ttu-id="9c9e1-118">Probe - contiene integrità probe usati toocheck disponibilità delle istanze di macchine virtuali nel pool di indirizzi back-end di hello.</span><span class="sxs-lookup"><span data-stu-id="9c9e1-118">Probes - contains health probes used toocheck availability of virtual machines instances in hello back-end address pool.</span></span>

<span data-ttu-id="9c9e1-119">Per altre informazioni, vedere [Supporto di Gestione risorse di Azure per il servizio di bilanciamento del carico](load-balancer-arm.md).</span><span class="sxs-lookup"><span data-stu-id="9c9e1-119">For more information see [Azure Resource Manager support for Load Balancer](load-balancer-arm.md).</span></span>

## <a name="set-up-cli-toouse-resource-manager"></a><span data-ttu-id="9c9e1-120">Impostare CLI toouse Gestione risorse</span><span class="sxs-lookup"><span data-stu-id="9c9e1-120">Set up CLI toouse Resource Manager</span></span>

1. <span data-ttu-id="9c9e1-121">Se non si è mai usato CLI di Azure, vedere [installare e configurare hello Azure CLI](../cli-install-nodejs.md) e seguire le istruzioni di hello toohello un punto in cui si seleziona l'account di Azure e la sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="9c9e1-121">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="9c9e1-122">Eseguire hello **modalità di configurazione azure** tooswitch tooResource Manager modalità comando, come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="9c9e1-122">Run hello **azure config mode** command tooswitch tooResource Manager mode, as shown below.</span></span>

    ```azurecli
        azure config mode arm
    ```

    <span data-ttu-id="9c9e1-123">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="9c9e1-123">Expected output:</span></span>

        info:    New mode is arm

## <a name="create-a-virtual-network-and-a-public-ip-address-for-hello-front-end-ip-pool"></a><span data-ttu-id="9c9e1-124">Creare una rete virtuale e un indirizzo IP pubblico per il pool IP front-end di hello</span><span class="sxs-lookup"><span data-stu-id="9c9e1-124">Create a virtual network and a public IP address for hello front-end IP pool</span></span>

1. <span data-ttu-id="9c9e1-125">Creare una rete virtuale (VNet) denominata *NRPVnet* in Stati Uniti orientali hello utilizzando un gruppo di risorse denominato *NRPRG*.</span><span class="sxs-lookup"><span data-stu-id="9c9e1-125">Create a virtual network (VNet) named *NRPVnet* in hello East US location using a resource group named *NRPRG*.</span></span>

    ```azurecli
        azure network vnet create NRPRG NRPVnet eastUS -a 10.0.0.0/16
    ```

    <span data-ttu-id="9c9e1-126">Creare una subnet denominata *NRPVnetSubnet* con un blocco CIDR di 10.0.0.0/24 in *NRPVnet*.</span><span class="sxs-lookup"><span data-stu-id="9c9e1-126">Create a subnet named *NRPVnetSubnet* with a CIDR block of 10.0.0.0/24 in *NRPVnet*.</span></span>

    ```azurecli
        azure network vnet subnet create NRPRG NRPVnet NRPVnetSubnet -a 10.0.0.0/24
    ```

2. <span data-ttu-id="9c9e1-127">Creare un indirizzo IP pubblico denominato *NRPPublicIP* toobe utilizzato da un pool IP front-end con nome DNS *loadbalancernrp.eastus.cloudapp.azure.com*. comando hello seguente utilizza il tipo di allocazione statica hello e timeout di inattività di 4 minuti.</span><span class="sxs-lookup"><span data-stu-id="9c9e1-127">Create a public IP address named *NRPPublicIP* toobe used by a front-end IP pool with DNS name *loadbalancernrp.eastus.cloudapp.azure.com*. hello command below uses hello static allocation type and idle timeout of 4 minutes.</span></span>

    ```azurecli
        azure network public-ip create -g NRPRG -n NRPPublicIP -l eastus -d loadbalancernrp -a static -i 4
    ```

   > [!IMPORTANT]
   > <span data-ttu-id="9c9e1-128">bilanciamento del carico Hello utilizzerà l'etichetta del dominio dell'indirizzo IP pubblico hello hello come il nome di dominio completo.</span><span class="sxs-lookup"><span data-stu-id="9c9e1-128">hello load balancer will use hello domain label of hello public IP as its FQDN.</span></span> <span data-ttu-id="9c9e1-129">Questo una modifica dalla distribuzione classica, che utilizza il servizio di cloud hello come hello bilanciamento del carico completamente dominio nome completo (FQDN).</span><span class="sxs-lookup"><span data-stu-id="9c9e1-129">This a change from classic deployment, which uses hello cloud service as hello load balancer Fully Qualified Domain Name (FQDN).</span></span>
   > <span data-ttu-id="9c9e1-130">In questo esempio, hello FQDN è *loadbalancernrp.eastus.cloudapp.azure.com*.</span><span class="sxs-lookup"><span data-stu-id="9c9e1-130">In this example, hello FQDN is *loadbalancernrp.eastus.cloudapp.azure.com*.</span></span>

## <a name="create-a-load-balancer"></a><span data-ttu-id="9c9e1-131">Creare un servizio di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="9c9e1-131">Create a load balancer</span></span>

<span data-ttu-id="9c9e1-132">il comando seguente Hello crea un bilanciamento del carico denominato *NRPlb* in hello *NRPRG* gruppo di risorse in hello *Stati Uniti orientali* località di Azure.</span><span class="sxs-lookup"><span data-stu-id="9c9e1-132">hello following command creates a load balancer named *NRPlb* in hello *NRPRG* resource group in hello *East US* Azure location.</span></span>

    ```azurecli
    azure network lb create NRPRG NRPlb eastus
    ```

## <a name="create-a-front-end-ip-pool-and-a-backend-address-pool"></a><span data-ttu-id="9c9e1-133">Creare un pool di indirizzi IP front-end e un pool di indirizzi back-end</span><span class="sxs-lookup"><span data-stu-id="9c9e1-133">Create a front-end IP pool and a backend address pool</span></span>
<span data-ttu-id="9c9e1-134">Questo esempio viene illustrato come toocreate hello front-end pool IP che riceve il traffico di rete in ingresso di hello in hello bilanciamento del carico e il pool IP back-end in cui pool front-end hello invia il traffico di rete con carico bilanciato hello hello.</span><span class="sxs-lookup"><span data-stu-id="9c9e1-134">This example demonstrates how toocreate hello front-end IP pool that receives hello incoming network traffic on hello load balancer and hello backend IP pool where hello front-end pool sends hello load balanced network traffic.</span></span>

1. <span data-ttu-id="9c9e1-135">Creare un pool IP front-end associazione hello creato nel passaggio precedente hello e bilanciamento del carico hello indirizzo IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="9c9e1-135">Create a front-end IP pool associating hello public IP created in hello previous step and hello load balancer.</span></span>

    ```azurecli
        azure network lb frontend-ip create nrpRG NRPlb NRPfrontendpool -i nrppublicip
    ```

2. <span data-ttu-id="9c9e1-136">Configurare un pool di indirizzi back-end utilizzato traffico in ingresso tooreceive dal pool IP front-end hello.</span><span class="sxs-lookup"><span data-stu-id="9c9e1-136">Set up a back-end address pool used tooreceive incoming traffic from hello front-end IP pool.</span></span>

    ```azurecli
        azure network lb address-pool create NRPRG NRPlb NRPbackendpool
    ```

## <a name="create-lb-rules-nat-rules-and-probe"></a><span data-ttu-id="9c9e1-137">Creare regole di bilanciamento del carico, regole NAT e probe</span><span class="sxs-lookup"><span data-stu-id="9c9e1-137">Create LB rules, NAT rules, and probe</span></span>

<span data-ttu-id="9c9e1-138">Questo esempio crea hello seguenti elementi.</span><span class="sxs-lookup"><span data-stu-id="9c9e1-138">This example creates hello following items.</span></span>

* <span data-ttu-id="9c9e1-139">un dispositivo NAT regola tootranslate tutto il traffico in ingresso sulla porta 21 tooport 22<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="9c9e1-139">a NAT rule tootranslate all incoming traffic on port 21 tooport 22<sup>1</sup></span></span>
* <span data-ttu-id="9c9e1-140">un dispositivo NAT tutto il traffico in ingresso sulla porta 23 tooport 22 tootranslate della regola</span><span class="sxs-lookup"><span data-stu-id="9c9e1-140">a NAT rule tootranslate all incoming traffic on port 23 tooport 22</span></span>
* <span data-ttu-id="9c9e1-141">un toobalance regola di bilanciamento carico di tutto il traffico in ingresso sulla porta 80 tooport 80 su hello indirizzi nel pool back-end hello.</span><span class="sxs-lookup"><span data-stu-id="9c9e1-141">a load balancer rule toobalance all incoming traffic on port 80 tooport 80 on hello addresses in hello back-end pool.</span></span>
* <span data-ttu-id="9c9e1-142">probe regola toocheck hello lo stato di integrità in una pagina denominata *HealthProbe.aspx*.</span><span class="sxs-lookup"><span data-stu-id="9c9e1-142">a probe rule toocheck hello health status on a page named *HealthProbe.aspx*.</span></span>

<span data-ttu-id="9c9e1-143"><sup>1</sup> le regole NAT sono associati tooa macchina virtuale specifica istanza bilanciamento del carico hello.</span><span class="sxs-lookup"><span data-stu-id="9c9e1-143"><sup>1</sup> NAT rules are associated tooa specific virtual machine instance behind hello load balancer.</span></span> <span data-ttu-id="9c9e1-144">il traffico di rete Hello in arrivo sulla porta 21 viene inviato a macchina virtuale specifica tooa sulla porta 22 associata a questa regola NAT.</span><span class="sxs-lookup"><span data-stu-id="9c9e1-144">hello network traffic arriving on port 21 is sent tooa specific virtual machine on port 22 associated with this NAT rule.</span></span> <span data-ttu-id="9c9e1-145">È necessario specificare un protocollo (UDP o TCP) per una regola NAT.</span><span class="sxs-lookup"><span data-stu-id="9c9e1-145">You must specify a protocol (UDP or TCP) for a NAT rule.</span></span> <span data-ttu-id="9c9e1-146">Entrambi i protocolli non possono essere assegnato toohello stessa porta.</span><span class="sxs-lookup"><span data-stu-id="9c9e1-146">Both protocols can't be assigned toohello same port.</span></span>

1. <span data-ttu-id="9c9e1-147">Creare le regole NAT di hello.</span><span class="sxs-lookup"><span data-stu-id="9c9e1-147">Create hello NAT rules.</span></span>

    ```azurecli
        azure network lb inbound-nat-rule create --resource-group nrprg --lb-name nrplb --name ssh1 --protocol tcp --frontend-port 21 --backend-port 22
        azure network lb inbound-nat-rule create --resource-group nrprg --lb-name nrplb --name ssh2 --protocol tcp --frontend-port 23 --backend-port 22
    ```

2. <span data-ttu-id="9c9e1-148">Creare una regola del servizio di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="9c9e1-148">Create a load balancer rule.</span></span>

    ```azurecli
        azure network lb rule create --resource-group nrprg --lb-name nrplb --name lbrule --protocol tcp --frontend-port 80 --backend-port 80 --frontend-ip-name NRPfrontendpool --backend-address-pool-name NRPbackendpool
    ```

3. <span data-ttu-id="9c9e1-149">Creare un probe di integrità.</span><span class="sxs-lookup"><span data-stu-id="9c9e1-149">Create a health probe.</span></span>

    ```azurecli
        azure network lb probe create --resource-group nrprg --lb-name nrplb --name healthprobe --protocol "http" --port 80 --path healthprobe.aspx --interval 15 --count 4
    ```

4. <span data-ttu-id="9c9e1-150">Verificare le impostazioni.</span><span class="sxs-lookup"><span data-stu-id="9c9e1-150">Check your settings.</span></span>

    ```azurecli
        azure network lb show nrprg nrplb
    ```

    <span data-ttu-id="9c9e1-151">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="9c9e1-151">Expected output:</span></span>

        info:    Executing command network lb show
        + Looking up hello load balancer "nrplb"
        + Looking up hello public ip "NRPPublicIP"
        data:    Id                              : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb
        data:    Name                            : nrplb
        data:    Type                            : Microsoft.Network/loadBalancers
        data:    Location                        : eastus
        data:    Provisioning State              : Succeeded
        data:    Frontend IP configurations:
        data:      Name                          : NRPfrontendpool
        data:      Provisioning state            : Succeeded
        data:      Public IP address id          : /subscriptions/####################################/resourceGroups/NRPRG/providers/Microsoft.Network/publicIPAddresses/NRPPublicIP
        data:      Public IP allocation method   : Static
        data:      Public IP address             : 40.114.13.145
        data:
        data:    Backend address pools:
        data:      Name                          : NRPbackendpool
        data:      Provisioning state            : Succeeded
        data:
        data:    Load balancing rules:
        data:      Name                          : HTTP
        data:      Provisioning state            : Succeeded
        data:      Protocol                      : Tcp
        data:      Frontend port                 : 80
        data:      Backend port                  : 80
        data:      Enable floating IP            : false
        data:      Idle timeout in minutes       : 4
        data:      Frontend IP configuration     : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/frontendIPConfigurations/NRPfrontendpool
        data:      Backend address pool          : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/NRPbackendpool
        data:
        data:    Inbound NAT rules:
        data:      Name                          : ssh1
        data:      Provisioning state            : Succeeded
        data:      Protocol                      : Tcp
        data:      Frontend port                 : 21
        data:      Backend port                  : 22
        data:      Enable floating IP            : false
        data:      Idle timeout in minutes       : 4
        data:      Frontend IP configuration     : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/frontendIPConfigurations/NRPfrontendpool
        data:
        data:      Name                          : ssh2
        data:      Provisioning state            : Succeeded
        data:      Protocol                      : Tcp
        data:      Frontend port                 : 23
        data:      Backend port                  : 22
        data:      Enable floating IP            : false
        data:      Idle timeout in minutes       : 4
        data:      Frontend IP configuration     : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/frontendIPConfigurations/NRPfrontendpool
        data:
        data:    Probes:
        data:      Name                          : healthprobe
        data:      Provisioning state            : Succeeded
        data:      Protocol                      : Http
        data:      Port                          : 80
        data:      Interval in seconds           : 15
        data:      Number of probes              : 4
        data:
        info:    network lb show command OK

## <a name="create-nics"></a><span data-ttu-id="9c9e1-152">Creare NIC</span><span class="sxs-lookup"><span data-stu-id="9c9e1-152">Create NICs</span></span>

<span data-ttu-id="9c9e1-153">È necessario toocreate NIC (o modificare quelli esistenti) e associarli tooNAT regole, regole di bilanciamento del carico e probe.</span><span class="sxs-lookup"><span data-stu-id="9c9e1-153">You need toocreate NICs (or modify existing ones) and associate them tooNAT rules, load balancer rules, and probes.</span></span>

1. <span data-ttu-id="9c9e1-154">Creare una scheda di rete denominata *lb-nic1 essere*e associarlo a hello *rdp1* NAT regola e hello *NRPbackendpool* pool di indirizzi back-end.</span><span class="sxs-lookup"><span data-stu-id="9c9e1-154">Create a NIC named *lb-nic1-be*, and associate it with hello *rdp1* NAT rule, and hello *NRPbackendpool* back-end address pool.</span></span>

    ```azurecli
        azure network nic create --resource-group nrprg --name lb-nic1-be --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet --lb-address-pool-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/NRPbackendpool" --lb-inbound-nat-rule-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp1" eastus
    ```

    <span data-ttu-id="9c9e1-155">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="9c9e1-155">Expected output:</span></span>

        info:    Executing command network nic create
        + Looking up hello network interface "lb-nic1-be"
        + Looking up hello subnet "nrpvnetsubnet"
        + Creating network interface "lb-nic1-be"
        + Looking up hello network interface "lb-nic1-be"
        data:    Id                              : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/networkInterfaces/lb-nic1-be
        data:    Name                            : lb-nic1-be
        data:    Type                            : Microsoft.Network/networkInterfaces
        data:    Location                        : eastus
        data:    Provisioning state              : Succeeded
        data:    Enable IP forwarding            : false
        data:    IP configurations:
        data:      Name                          : NIC-config
        data:      Provisioning state            : Succeeded
        data:      Private IP address            : 10.0.0.4
        data:      Private IP Allocation Method  : Dynamic
        data:      Subnet                        : /subscriptions/####################################/resourceGroups/NRPRG/providers/Microsoft.Network/virtualNetworks/NRPVnet/subnets/NRPVnetSubnet
        data:      Load balancer backend address pools
        data:        Id                          : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/NRPbackendpool
        data:      Load balancer inbound NAT rules:
        data:        Id                          : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp1
        data:
        info:    network nic create command OK

2. <span data-ttu-id="9c9e1-156">Creare una scheda di rete denominata *lb-nic2 essere*e associarlo a hello *rdp2* NAT regola e hello *NRPbackendpool* pool di indirizzi back-end.</span><span class="sxs-lookup"><span data-stu-id="9c9e1-156">Create a NIC named *lb-nic2-be*, and associate it with hello *rdp2* NAT rule, and hello *NRPbackendpool* back-end address pool.</span></span>

    ```azurecli
        azure network nic create --resource-group nrprg --name lb-nic2-be --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet --lb-address-pool-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/NRPbackendpool" --lb-inbound-nat-rule-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp2" eastus
    ```

3. <span data-ttu-id="9c9e1-157">Creare una macchina virtuale (VM) denominata *web1*e associarlo a una scheda di rete denominata hello *lb-nic1 essere*.</span><span class="sxs-lookup"><span data-stu-id="9c9e1-157">Create a virtual machine (VM) named *web1*, and associate it with hello NIC named *lb-nic1-be*.</span></span> <span data-ttu-id="9c9e1-158">Un account di archiviazione denominato *web1nrp* è stato creato prima dell'esecuzione comando hello riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="9c9e1-158">A storage account called *web1nrp* was created before running hello command below.</span></span>

    ```azurecli
        azure vm create --resource-group nrprg --name web1 --location eastus --vnet-name nrpvnet --vnet-subnet-name nrpvnetsubnet --nic-name lb-nic1-be --availset-name nrp-avset --storage-account-name web1nrp --os-type Windows --image-urn MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:4.0.20150825
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="9c9e1-159">Macchine virtuali in un toobe necessità bilanciamento di carico in hello stesso set di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="9c9e1-159">VMs in a load balancer need toobe in hello same availability set.</span></span> <span data-ttu-id="9c9e1-160">Utilizzare `azure availset create` toocreate un gruppo di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="9c9e1-160">Use `azure availset create` toocreate an availability set.</span></span>

    <span data-ttu-id="9c9e1-161">output di Hello deve essere simile toohello seguenti:</span><span class="sxs-lookup"><span data-stu-id="9c9e1-161">hello output should be similar toohello following:</span></span>

        info:    Executing command vm create
        + Looking up hello VM "web1"
        Enter username: azureuser
        Enter password for azureuser: *********
        Confirm password: *********
        info:    Using hello VM Size "Standard_A1"
        info:    hello [OS, Data] Disk or image configuration requires storage account
        + Looking up hello storage account web1nrp
        + Looking up hello availability set "nrp-avset"
        info:    Found an Availability set "nrp-avset"
        + Looking up hello NIC "lb-nic1-be"
        info:    Found an existing NIC "lb-nic1-be"
        info:    Found an IP configuration with virtual network subnet id "/subscriptions/####################################/resourceGroups/NRPRG/providers/Microsoft.Network/virtualNetworks/NRPVnet/subnets/NRPVnetSubnet" in hello NIC "lb-nic1-be"
        info:    This is a NIC without publicIP configured
        + Creating VM "web1"
        info:    vm create command OK

    > [!NOTE]
    > <span data-ttu-id="9c9e1-162">messaggio informativo Hello **si tratta di una scheda di rete senza publicIP configurato** previsto poiché hello NIC creato per la connessione utilizzando l'indirizzo IP pubblico di hello carico bilanciamento tooInternet bilanciamento del carico di hello.</span><span class="sxs-lookup"><span data-stu-id="9c9e1-162">hello informational message **This is a NIC without publicIP configured** is expected since hello NIC created for hello load balancer connecting tooInternet using hello load balancer public IP address.</span></span>

    <span data-ttu-id="9c9e1-163">Poiché hello *lb-nic1 essere* NIC è associata a hello *rdp1* regola NAT, è possibile connettersi troppo*web1* tramite RDP porta 3441 nel servizio di bilanciamento del carico hello.</span><span class="sxs-lookup"><span data-stu-id="9c9e1-163">Since hello *lb-nic1-be* NIC is associated with hello *rdp1* NAT rule, you can connect too*web1* using RDP through port 3441 on hello load balancer.</span></span>

4. <span data-ttu-id="9c9e1-164">Creare una macchina virtuale (VM) denominata *web2*e associarlo a una scheda di rete denominata hello *lb-nic2 essere*.</span><span class="sxs-lookup"><span data-stu-id="9c9e1-164">Create a virtual machine (VM) named *web2*, and associate it with hello NIC named *lb-nic2-be*.</span></span> <span data-ttu-id="9c9e1-165">Un account di archiviazione denominato *web1nrp* è stato creato prima dell'esecuzione comando hello riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="9c9e1-165">A storage account called *web1nrp* was created before running hello command below.</span></span>

    ```azurecli
        azure vm create --resource-group nrprg --name web2 --location eastus --vnet-name nrpvnet --vnet-subnet-name nrpvnetsubnet --nic-name lb-nic2-be --availset-name nrp-avset --storage-account-name web2nrp --os-type Windows --image-urn MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:4.0.20150825
    ```

## <a name="update-an-existing-load-balancer"></a><span data-ttu-id="9c9e1-166">Aggiornare un bilanciamento del carico esistente</span><span class="sxs-lookup"><span data-stu-id="9c9e1-166">Update an existing load balancer</span></span>
<span data-ttu-id="9c9e1-167">È possibile aggiungere regole che fanno riferimento a un servizio di bilanciamento del carico esistente.</span><span class="sxs-lookup"><span data-stu-id="9c9e1-167">You can add rules referencing an existing load balancer.</span></span> <span data-ttu-id="9c9e1-168">Nell'esempio riportato di seguito hello, una nuova regola di bilanciamento del carico viene aggiunto a bilanciamento del carico esistente tooan **NRPlb**</span><span class="sxs-lookup"><span data-stu-id="9c9e1-168">In hello next example, a new load balancer rule is added tooan existing load balancer **NRPlb**</span></span>

```azurecli
azure network lb rule create --resource-group nrprg --lb-name nrplb --name lbrule2 --protocol tcp --frontend-port 8080 --backend-port 8051 --frontend-ip-name frontendnrppool --backend-address-pool-name NRPbackendpool
```

## <a name="delete-a-load-balancer"></a><span data-ttu-id="9c9e1-169">Eliminare un servizio di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="9c9e1-169">Delete a load balancer</span></span>
<span data-ttu-id="9c9e1-170">Utilizzare hello comando tooremove un bilanciamento del carico seguenti:</span><span class="sxs-lookup"><span data-stu-id="9c9e1-170">Use hello following command tooremove a load balancer:</span></span>

```azurecli
azure network lb delete --resource-group nrprg --name nrplb
```

## <a name="next-steps"></a><span data-ttu-id="9c9e1-171">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9c9e1-171">Next steps</span></span>
[<span data-ttu-id="9c9e1-172">Introduzione alla configurazione del bilanciamento del carico interno</span><span class="sxs-lookup"><span data-stu-id="9c9e1-172">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-cli.md)

[<span data-ttu-id="9c9e1-173">Configurare una modalità di distribuzione del servizio di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="9c9e1-173">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="9c9e1-174">Configurare le impostazioni del timeout di inattività TCP per il bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="9c9e1-174">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
