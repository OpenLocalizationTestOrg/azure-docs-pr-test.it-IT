---
title: Creare un servizio di bilanciamento del carico con connessione Internet - Interfaccia della riga di comando di Azure | Documentazione Microsoft
description: Informazioni su come creare un servizio di bilanciamento del carico Internet in Gestione risorse mediante l'interfaccia della riga di comando di Azure.
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
ms.openlocfilehash: 3b1780033cbc8aa3e108a213a4d2bfd0332fd7d7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="creating-an-internet-load-balancer-using-the-azure-cli"></a><span data-ttu-id="7a878-103">Creazione di un servizio di bilanciamento del carico Internet tramite l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="7a878-103">Creating an internet load balancer using the Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="7a878-104">Portale</span><span class="sxs-lookup"><span data-stu-id="7a878-104">Portal</span></span>](../load-balancer/load-balancer-get-started-internet-portal.md)
> * [<span data-ttu-id="7a878-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="7a878-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-internet-arm-ps.md)
> * [<span data-ttu-id="7a878-106">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="7a878-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-internet-arm-cli.md)
> * [<span data-ttu-id="7a878-107">Modello</span><span class="sxs-lookup"><span data-stu-id="7a878-107">Template</span></span>](../load-balancer/load-balancer-get-started-internet-arm-template.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="7a878-108">Questo articolo illustra il modello di distribuzione Gestione risorse.</span><span class="sxs-lookup"><span data-stu-id="7a878-108">This article covers the Resource Manager deployment model.</span></span> <span data-ttu-id="7a878-109">Vedere [Informazioni su come creare un servizio di bilanciamento del carico Internet tramite la distribuzione classica](load-balancer-get-started-internet-classic-portal.md)</span><span class="sxs-lookup"><span data-stu-id="7a878-109">You can also [Learn how to create an Internet facing load balancer using classic deployment](load-balancer-get-started-internet-classic-portal.md)</span></span>

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="deploying-the-solution-using-the-azure-cli"></a><span data-ttu-id="7a878-110">Distribuzione della soluzione tramite l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="7a878-110">Deploying the solution using the Azure CLI</span></span>

<span data-ttu-id="7a878-111">La procedura seguente illustra come creare un servizio di bilanciamento del carico Internet usando Azure Resource Manager con l'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="7a878-111">The following steps show how to create an Internet facing load balancer using Azure Resource Manager with CLI.</span></span> <span data-ttu-id="7a878-112">Con Azure Resource Manager ogni risorsa viene creata e configurata singolarmente e quindi integrata per creare una risorsa.</span><span class="sxs-lookup"><span data-stu-id="7a878-112">With Azure Resource Manager each resource is created and configured individually, then put together to create a resource.</span></span>

<span data-ttu-id="7a878-113">Creare e configurare gli oggetti seguenti per distribuire un servizio di bilanciamento del carico:</span><span class="sxs-lookup"><span data-stu-id="7a878-113">You must create and configure the following objects to deploy a load balancer:</span></span>

* <span data-ttu-id="7a878-114">Configurazione di IP front-end: contiene gli indirizzi IP pubblici per il traffico di rete in ingresso.</span><span class="sxs-lookup"><span data-stu-id="7a878-114">Front-end IP configuration - contains public IP addresses for incoming network traffic.</span></span>
* <span data-ttu-id="7a878-115">Pool di indirizzi back-end: contiene interfacce di rete (NIC) per le macchine virtuali per la ricezione di traffico di rete dal servizio di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="7a878-115">Back-end address pool - contains network interfaces (NICs) for the virtual machines to receive network traffic from the load balancer.</span></span>
* <span data-ttu-id="7a878-116">Regole di bilanciamento del carico: contengono regole per il mapping di una porta pubblica nel servizio di bilanciamento del carico alle porte nel pool di indirizzi back-end.</span><span class="sxs-lookup"><span data-stu-id="7a878-116">Load balancing rules - contains rules mapping a public port on the load balancer to port in the back-end address pool.</span></span>
* <span data-ttu-id="7a878-117">Regole NAT in ingresso: contengono regole per il mapping di una porta pubblica nel servizio di bilanciamento del carico a una porta per una macchina virtuale specifica nel pool di indirizzi back-end.</span><span class="sxs-lookup"><span data-stu-id="7a878-117">Inbound NAT rules - contains rules mapping a public port on the load balancer to a port for a specific virtual machine in the back-end address pool.</span></span>
* <span data-ttu-id="7a878-118">Probe: contengono probe di integrità usati per verificare la disponibilità di istanze di macchine virtuali nel pool di indirizzi back-end.</span><span class="sxs-lookup"><span data-stu-id="7a878-118">Probes - contains health probes used to check availability of virtual machines instances in the back-end address pool.</span></span>

<span data-ttu-id="7a878-119">Per altre informazioni, vedere [Supporto di Gestione risorse di Azure per il servizio di bilanciamento del carico](load-balancer-arm.md).</span><span class="sxs-lookup"><span data-stu-id="7a878-119">For more information see [Azure Resource Manager support for Load Balancer](load-balancer-arm.md).</span></span>

## <a name="set-up-cli-to-use-resource-manager"></a><span data-ttu-id="7a878-120">Configurare l'interfaccia della riga di comando per l'uso di Resource Manager</span><span class="sxs-lookup"><span data-stu-id="7a878-120">Set up CLI to use Resource Manager</span></span>

1. <span data-ttu-id="7a878-121">Se l'interfaccia della riga di comando di Azure non è mai stata usata, vedere [Installare e configurare l'interfaccia della riga di comando di Azure](../cli-install-nodejs.md) e seguire le istruzioni fino al punto in cui si selezionano l'account e la sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="7a878-121">If you have never used Azure CLI, see [Install and Configure the Azure CLI](../cli-install-nodejs.md) and follow the instructions up to the point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="7a878-122">Eseguire il comando **azure config mode** per passare alla modalità Gestione risorse, come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="7a878-122">Run the **azure config mode** command to switch to Resource Manager mode, as shown below.</span></span>

    ```azurecli
        azure config mode arm
    ```

    <span data-ttu-id="7a878-123">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="7a878-123">Expected output:</span></span>

        info:    New mode is arm

## <a name="create-a-virtual-network-and-a-public-ip-address-for-the-front-end-ip-pool"></a><span data-ttu-id="7a878-124">Creare una rete virtuale e un indirizzo IP pubblico per il pool di indirizzi IP front-end</span><span class="sxs-lookup"><span data-stu-id="7a878-124">Create a virtual network and a public IP address for the front-end IP pool</span></span>

1. <span data-ttu-id="7a878-125">Creare una rete virtuale (VNet) denominata *NRPVnet* nella località Stati Uniti orientali usando un gruppo di risorse denominato *NRPRG*.</span><span class="sxs-lookup"><span data-stu-id="7a878-125">Create a virtual network (VNet) named *NRPVnet* in the East US location using a resource group named *NRPRG*.</span></span>

    ```azurecli
        azure network vnet create NRPRG NRPVnet eastUS -a 10.0.0.0/16
    ```

    <span data-ttu-id="7a878-126">Creare una subnet denominata *NRPVnetSubnet* con un blocco CIDR di 10.0.0.0/24 in *NRPVnet*.</span><span class="sxs-lookup"><span data-stu-id="7a878-126">Create a subnet named *NRPVnetSubnet* with a CIDR block of 10.0.0.0/24 in *NRPVnet*.</span></span>

    ```azurecli
        azure network vnet subnet create NRPRG NRPVnet NRPVnetSubnet -a 10.0.0.0/24
    ```

2. <span data-ttu-id="7a878-127">Creare un indirizzo IP pubblico denominato *NRPPublicIP* che dovrà essere usato da un pool di indirizzi IP front-end con nome DNS *loadbalancernrp.eastus.cloudapp.azure.com*.</span><span class="sxs-lookup"><span data-stu-id="7a878-127">Create a public IP address named *NRPPublicIP* to be used by a front-end IP pool with DNS name *loadbalancernrp.eastus.cloudapp.azure.com*.</span></span> <span data-ttu-id="7a878-128">Il comando seguente usa il tipo di allocazione statica e un timeout di inattività pari a 4 minuti.</span><span class="sxs-lookup"><span data-stu-id="7a878-128">The command below uses the static allocation type and idle timeout of 4 minutes.</span></span>

    ```azurecli
        azure network public-ip create -g NRPRG -n NRPPublicIP -l eastus -d loadbalancernrp -a static -i 4
    ```

   > [!IMPORTANT]
   > <span data-ttu-id="7a878-129">Il servizio di bilanciamento del carico userà l'etichetta di dominio dell'indirizzo IP pubblico come nome di dominio completo.</span><span class="sxs-lookup"><span data-stu-id="7a878-129">The load balancer will use the domain label of the public IP as its FQDN.</span></span> <span data-ttu-id="7a878-130">Questa è una differenza rispetto alla distribuzione classica, che usa il servizio cloud come nome di dominio completo del servizio di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="7a878-130">This a change from classic deployment, which uses the cloud service as the load balancer Fully Qualified Domain Name (FQDN).</span></span>
   > <span data-ttu-id="7a878-131">In questo esempio il nome di dominio completo è *loadbalancernrp.eastus.cloudapp.azure.com*.</span><span class="sxs-lookup"><span data-stu-id="7a878-131">In this example, the FQDN is *loadbalancernrp.eastus.cloudapp.azure.com*.</span></span>

## <a name="create-a-load-balancer"></a><span data-ttu-id="7a878-132">Creare un servizio di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="7a878-132">Create a load balancer</span></span>

<span data-ttu-id="7a878-133">Il comando seguente crea un servizio di bilanciamento del carico denominato *NRPlb* nel gruppo di risorse *NRPRG* nella località *Stati Uniti orientali* di Azure.</span><span class="sxs-lookup"><span data-stu-id="7a878-133">The following command creates a load balancer named *NRPlb* in the *NRPRG* resource group in the *East US* Azure location.</span></span>

    ```azurecli
    azure network lb create NRPRG NRPlb eastus
    ```

## <a name="create-a-front-end-ip-pool-and-a-backend-address-pool"></a><span data-ttu-id="7a878-134">Creare un pool di indirizzi IP front-end e un pool di indirizzi back-end</span><span class="sxs-lookup"><span data-stu-id="7a878-134">Create a front-end IP pool and a backend address pool</span></span>
<span data-ttu-id="7a878-135">Questo esempio spiega come creare il pool di indirizzi IP front-end che riceve il traffico di rete in entrata per il servizio di bilanciamento del carico e il pool di indirizzi IP back-end a cui il pool front-end invia il traffico di rete sottoposto a bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="7a878-135">This example demonstrates how to create the front-end IP pool that receives the incoming network traffic on the load balancer and the backend IP pool where the front-end pool sends the load balanced network traffic.</span></span>

1. <span data-ttu-id="7a878-136">Creare un pool di indirizzi IP front-end che associa l'indirizzo IP pubblico creato nel passaggio precedente e il servizio di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="7a878-136">Create a front-end IP pool associating the public IP created in the previous step and the load balancer.</span></span>

    ```azurecli
        azure network lb frontend-ip create nrpRG NRPlb NRPfrontendpool -i nrppublicip
    ```

2. <span data-ttu-id="7a878-137">Configurare un pool di indirizzi back-end usato per ricevere il traffico in ingresso dal pool di indirizzi IP front-end.</span><span class="sxs-lookup"><span data-stu-id="7a878-137">Set up a back-end address pool used to receive incoming traffic from the front-end IP pool.</span></span>

    ```azurecli
        azure network lb address-pool create NRPRG NRPlb NRPbackendpool
    ```

## <a name="create-lb-rules-nat-rules-and-probe"></a><span data-ttu-id="7a878-138">Creare regole di bilanciamento del carico, regole NAT e probe</span><span class="sxs-lookup"><span data-stu-id="7a878-138">Create LB rules, NAT rules, and probe</span></span>

<span data-ttu-id="7a878-139">Questo esempio crea gli elementi seguenti.</span><span class="sxs-lookup"><span data-stu-id="7a878-139">This example creates the following items.</span></span>

* <span data-ttu-id="7a878-140">Regola NAT per la conversione di tutto il traffico in ingresso sulla porta 21 alla porta 22<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="7a878-140">a NAT rule to translate all incoming traffic on port 21 to port 22<sup>1</sup></span></span>
* <span data-ttu-id="7a878-141">Regola NAT per la conversione di tutto il traffico in ingresso sulla porta 23 alla porta 22.</span><span class="sxs-lookup"><span data-stu-id="7a878-141">a NAT rule to translate all incoming traffic on port 23 to port 22</span></span>
* <span data-ttu-id="7a878-142">Regola del servizio di bilanciamento del carico per il bilanciamento di tutto il traffico in ingresso sulla porta 80 verso la porta 80 negli indirizzi nel pool back-end.</span><span class="sxs-lookup"><span data-stu-id="7a878-142">a load balancer rule to balance all incoming traffic on port 80 to port 80 on the addresses in the back-end pool.</span></span>
* <span data-ttu-id="7a878-143">Regola probe per il controllo dello stato di integrità in una pagina denominata *HealthProbe.aspx*.</span><span class="sxs-lookup"><span data-stu-id="7a878-143">a probe rule to check the health status on a page named *HealthProbe.aspx*.</span></span>

<span data-ttu-id="7a878-144"><sup>1</sup> Le regole NAT vengono associate a un'istanza di macchina virtuale specifica dietro al servizio di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="7a878-144"><sup>1</sup> NAT rules are associated to a specific virtual machine instance behind the load balancer.</span></span> <span data-ttu-id="7a878-145">Il traffico di rete in arrivo sulla porta 21 viene inviato a una specifica macchina virtuale sulla porta 22 associata a questa regola NAT.</span><span class="sxs-lookup"><span data-stu-id="7a878-145">The network traffic arriving on port 21 is sent to a specific virtual machine on port 22 associated with this NAT rule.</span></span> <span data-ttu-id="7a878-146">È necessario specificare un protocollo (UDP o TCP) per una regola NAT.</span><span class="sxs-lookup"><span data-stu-id="7a878-146">You must specify a protocol (UDP or TCP) for a NAT rule.</span></span> <span data-ttu-id="7a878-147">Entrambi i protocolli non possono essere assegnati alla stessa porta.</span><span class="sxs-lookup"><span data-stu-id="7a878-147">Both protocols can't be assigned to the same port.</span></span>

1. <span data-ttu-id="7a878-148">Creare le regole NAT.</span><span class="sxs-lookup"><span data-stu-id="7a878-148">Create the NAT rules.</span></span>

    ```azurecli
        azure network lb inbound-nat-rule create --resource-group nrprg --lb-name nrplb --name ssh1 --protocol tcp --frontend-port 21 --backend-port 22
        azure network lb inbound-nat-rule create --resource-group nrprg --lb-name nrplb --name ssh2 --protocol tcp --frontend-port 23 --backend-port 22
    ```

2. <span data-ttu-id="7a878-149">Creare una regola del servizio di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="7a878-149">Create a load balancer rule.</span></span>

    ```azurecli
        azure network lb rule create --resource-group nrprg --lb-name nrplb --name lbrule --protocol tcp --frontend-port 80 --backend-port 80 --frontend-ip-name NRPfrontendpool --backend-address-pool-name NRPbackendpool
    ```

3. <span data-ttu-id="7a878-150">Creare un probe di integrità.</span><span class="sxs-lookup"><span data-stu-id="7a878-150">Create a health probe.</span></span>

    ```azurecli
        azure network lb probe create --resource-group nrprg --lb-name nrplb --name healthprobe --protocol "http" --port 80 --path healthprobe.aspx --interval 15 --count 4
    ```

4. <span data-ttu-id="7a878-151">Verificare le impostazioni.</span><span class="sxs-lookup"><span data-stu-id="7a878-151">Check your settings.</span></span>

    ```azurecli
        azure network lb show nrprg nrplb
    ```

    <span data-ttu-id="7a878-152">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="7a878-152">Expected output:</span></span>

        info:    Executing command network lb show
        + Looking up the load balancer "nrplb"
        + Looking up the public ip "NRPPublicIP"
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

## <a name="create-nics"></a><span data-ttu-id="7a878-153">Creare NIC</span><span class="sxs-lookup"><span data-stu-id="7a878-153">Create NICs</span></span>

<span data-ttu-id="7a878-154">È necessario creare schede di interfaccia di rete (NIC) o modificare quelle esistenti e associarle a regole NAT, regole del servizio di bilanciamento del carico e probe.</span><span class="sxs-lookup"><span data-stu-id="7a878-154">You need to create NICs (or modify existing ones) and associate them to NAT rules, load balancer rules, and probes.</span></span>

1. <span data-ttu-id="7a878-155">Creare una schede di interfaccia di rete denominata *lb-nic1-be* e associarla alla regola NAT *rdp1* e al pool di indirizzi back-end *NRPbackendpool*.</span><span class="sxs-lookup"><span data-stu-id="7a878-155">Create a NIC named *lb-nic1-be*, and associate it with the *rdp1* NAT rule, and the *NRPbackendpool* back-end address pool.</span></span>

    ```azurecli
        azure network nic create --resource-group nrprg --name lb-nic1-be --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet --lb-address-pool-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/NRPbackendpool" --lb-inbound-nat-rule-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp1" eastus
    ```

    <span data-ttu-id="7a878-156">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="7a878-156">Expected output:</span></span>

        info:    Executing command network nic create
        + Looking up the network interface "lb-nic1-be"
        + Looking up the subnet "nrpvnetsubnet"
        + Creating network interface "lb-nic1-be"
        + Looking up the network interface "lb-nic1-be"
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

2. <span data-ttu-id="7a878-157">Creare una schede di interfaccia di rete denominata *lb-nic2-be* e associarla alla regola NAT *rdp2* e al pool di indirizzi back-end *NRPbackendpool*.</span><span class="sxs-lookup"><span data-stu-id="7a878-157">Create a NIC named *lb-nic2-be*, and associate it with the *rdp2* NAT rule, and the *NRPbackendpool* back-end address pool.</span></span>

    ```azurecli
        azure network nic create --resource-group nrprg --name lb-nic2-be --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet --lb-address-pool-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/NRPbackendpool" --lb-inbound-nat-rule-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp2" eastus
    ```

3. <span data-ttu-id="7a878-158">Creare una macchina virtuale (VM) denominata *web1* e associarla alla schede di interfaccia di rete denominata *lb-nic1-be*.</span><span class="sxs-lookup"><span data-stu-id="7a878-158">Create a virtual machine (VM) named *web1*, and associate it with the NIC named *lb-nic1-be*.</span></span> <span data-ttu-id="7a878-159">Un account di archiviazione denominato *web1nrp* è stato creato prima dell'esecuzione del comando seguente.</span><span class="sxs-lookup"><span data-stu-id="7a878-159">A storage account called *web1nrp* was created before running the command below.</span></span>

    ```azurecli
        azure vm create --resource-group nrprg --name web1 --location eastus --vnet-name nrpvnet --vnet-subnet-name nrpvnetsubnet --nic-name lb-nic1-be --availset-name nrp-avset --storage-account-name web1nrp --os-type Windows --image-urn MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:4.0.20150825
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="7a878-160">Le macchine virtuali in un servizio di bilanciamento del carico devono trovarsi nello stesso set di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="7a878-160">VMs in a load balancer need to be in the same availability set.</span></span> <span data-ttu-id="7a878-161">Usare `azure availset create` per creare un set di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="7a878-161">Use `azure availset create` to create an availability set.</span></span>

    <span data-ttu-id="7a878-162">L'output dovrebbe essere simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="7a878-162">The output should be similar to the following:</span></span>

        info:    Executing command vm create
        + Looking up the VM "web1"
        Enter username: azureuser
        Enter password for azureuser: *********
        Confirm password: *********
        info:    Using the VM Size "Standard_A1"
        info:    The [OS, Data] Disk or image configuration requires storage account
        + Looking up the storage account web1nrp
        + Looking up the availability set "nrp-avset"
        info:    Found an Availability set "nrp-avset"
        + Looking up the NIC "lb-nic1-be"
        info:    Found an existing NIC "lb-nic1-be"
        info:    Found an IP configuration with virtual network subnet id "/subscriptions/####################################/resourceGroups/NRPRG/providers/Microsoft.Network/virtualNetworks/NRPVnet/subnets/NRPVnetSubnet" in the NIC "lb-nic1-be"
        info:    This is a NIC without publicIP configured
        + Creating VM "web1"
        info:    vm create command OK

    > [!NOTE]
    > <span data-ttu-id="7a878-163">Il messaggio informativo **This is a NIC without publicIP configured** è un comportamento previsto, perché la NIC creata per il servizio di bilanciamento del carico si connette a Internet tramite l'indirizzo IP pubblico del servizio di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="7a878-163">The informational message **This is a NIC without publicIP configured** is expected since the NIC created for the load balancer connecting to Internet using the load balancer public IP address.</span></span>

    <span data-ttu-id="7a878-164">Poiché la schede di interfaccia di rete *lb-nic1-be* è associata alla regola NAT *rdp1*, è possibile connettersi a *web1* con RDP tramite la porta 3441 nel servizio di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="7a878-164">Since the *lb-nic1-be* NIC is associated with the *rdp1* NAT rule, you can connect to *web1* using RDP through port 3441 on the load balancer.</span></span>

4. <span data-ttu-id="7a878-165">Creare una macchina virtuale (VM) denominata *web2* e associarla alla schede di interfaccia di rete denominata *lb-nic2-be*.</span><span class="sxs-lookup"><span data-stu-id="7a878-165">Create a virtual machine (VM) named *web2*, and associate it with the NIC named *lb-nic2-be*.</span></span> <span data-ttu-id="7a878-166">Un account di archiviazione denominato *web1nrp* è stato creato prima dell'esecuzione del comando seguente.</span><span class="sxs-lookup"><span data-stu-id="7a878-166">A storage account called *web1nrp* was created before running the command below.</span></span>

    ```azurecli
        azure vm create --resource-group nrprg --name web2 --location eastus --vnet-name nrpvnet --vnet-subnet-name nrpvnetsubnet --nic-name lb-nic2-be --availset-name nrp-avset --storage-account-name web2nrp --os-type Windows --image-urn MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:4.0.20150825
    ```

## <a name="update-an-existing-load-balancer"></a><span data-ttu-id="7a878-167">Aggiornare un bilanciamento del carico esistente</span><span class="sxs-lookup"><span data-stu-id="7a878-167">Update an existing load balancer</span></span>
<span data-ttu-id="7a878-168">È possibile aggiungere regole che fanno riferimento a un servizio di bilanciamento del carico esistente.</span><span class="sxs-lookup"><span data-stu-id="7a878-168">You can add rules referencing an existing load balancer.</span></span> <span data-ttu-id="7a878-169">Nell'esempio seguente una nuova regola di bilanciamento del carico viene aggiunta a un servizio di bilanciamento del carico **NRPlb**</span><span class="sxs-lookup"><span data-stu-id="7a878-169">In the next example, a new load balancer rule is added to an existing load balancer **NRPlb**</span></span>

```azurecli
azure network lb rule create --resource-group nrprg --lb-name nrplb --name lbrule2 --protocol tcp --frontend-port 8080 --backend-port 8051 --frontend-ip-name frontendnrppool --backend-address-pool-name NRPbackendpool
```

## <a name="delete-a-load-balancer"></a><span data-ttu-id="7a878-170">Eliminare un servizio di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="7a878-170">Delete a load balancer</span></span>
<span data-ttu-id="7a878-171">Per rimuovere un servizio di bilanciamento del carico, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="7a878-171">Use the following command to remove a load balancer:</span></span>

```azurecli
azure network lb delete --resource-group nrprg --name nrplb
```

## <a name="next-steps"></a><span data-ttu-id="7a878-172">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7a878-172">Next steps</span></span>
[<span data-ttu-id="7a878-173">Introduzione alla configurazione del bilanciamento del carico interno</span><span class="sxs-lookup"><span data-stu-id="7a878-173">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-cli.md)

[<span data-ttu-id="7a878-174">Configurare una modalità di distribuzione del servizio di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="7a878-174">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="7a878-175">Configurare le impostazioni del timeout di inattività TCP per il bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="7a878-175">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
