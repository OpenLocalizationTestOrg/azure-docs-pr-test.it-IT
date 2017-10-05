---
title: Creare un servizio di bilanciamento del carico interno - Interfaccia della riga di comando di Azure | Documentazione Microsoft
description: Informazioni su come creare un servizio di bilanciamento del carico interno con l'interfaccia della riga di comando di Resource Manager
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
ms.assetid: c7a24e92-b4da-43c0-90f2-841c1b7ce489
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 128b91c685b5f7e494a69ca5b04165a0ee7cbb78
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-internal-load-balancer-by-using-the-azure-cli"></a><span data-ttu-id="d8acb-103">Creare un servizio di bilanciamento del carico interno tramite l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="d8acb-103">Create an internal load balancer by using the Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="d8acb-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="d8acb-104">Azure Portal</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-portal.md)
> * [<span data-ttu-id="d8acb-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d8acb-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-ps.md)
> * [<span data-ttu-id="d8acb-106">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="d8acb-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-cli.md)
> * [<span data-ttu-id="d8acb-107">Modello</span><span class="sxs-lookup"><span data-stu-id="d8acb-107">Template</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-template.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="d8acb-108">Azure offre due modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="d8acb-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="d8acb-109">Questo articolo illustra il modello di distribuzione Resource Manager che Microsoft consiglia di usare per le distribuzioni più recenti in sostituzione del [modello di distribuzione classica](load-balancer-get-started-ilb-classic-cli.md).</span><span class="sxs-lookup"><span data-stu-id="d8acb-109">This article covers using the Resource Manager deployment model, which Microsoft recommends for most new deployments instead of the [classic deployment model](load-balancer-get-started-ilb-classic-cli.md).</span></span>

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

## <a name="deploy-the-solution-by-using-the-azure-cli"></a><span data-ttu-id="d8acb-110">Distribuire la soluzione tramite l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="d8acb-110">Deploy the solution by using the Azure CLI</span></span>

<span data-ttu-id="d8acb-111">La procedura seguente illustra come creare un servizio di bilanciamento del carico Internet usando Azure Resource Manager con l'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="d8acb-111">The following steps show how to create an Internet-facing load balancer by using Azure Resource Manager with CLI.</span></span> <span data-ttu-id="d8acb-112">Con Azure Resource Manager ogni risorsa viene creata e configurata singolarmente e quindi integrata per creare una risorsa.</span><span class="sxs-lookup"><span data-stu-id="d8acb-112">With Azure Resource Manager, each resource is created and configured individually, and then put together to create a resource.</span></span>

<span data-ttu-id="d8acb-113">È necessario creare e configurare gli oggetti seguenti per distribuire un servizio di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="d8acb-113">You need to create and configure the following objects to deploy a load balancer:</span></span>

* <span data-ttu-id="d8acb-114">**Configurazione di IP front-end**: contiene gli indirizzi IP pubblici per il traffico di rete in ingresso</span><span class="sxs-lookup"><span data-stu-id="d8acb-114">**Front-end IP configuration**: contains public IP addresses for incoming network traffic</span></span>
* <span data-ttu-id="d8acb-115">**Pool di indirizzi back-end**: contiene interfacce di rete (NIC) per le macchine virtuali per la ricezione di traffico di rete dal servizio di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="d8acb-115">**Back-end address pool**: contains network interfaces (NICs) that enable the virtual machines to receive network traffic from the load balancer</span></span>
* <span data-ttu-id="d8acb-116">**Regole di bilanciamento del carico**: contiene le regole che eseguono il mapping di una porta pubblica sul servizio di bilanciamento del carico alla porta nel pool di indirizzi back-end</span><span class="sxs-lookup"><span data-stu-id="d8acb-116">**Load-balancing rules**: contains rules that map a public port on the load balancer to port in the back-end address pool</span></span>
* <span data-ttu-id="d8acb-117">**Regole NAT in ingresso**: contiene le regole che eseguono il mapping di una porta pubblica sul servizio di bilanciamento del carico a una porta per una macchina virtuale specifica nel pool di indirizzi back-end</span><span class="sxs-lookup"><span data-stu-id="d8acb-117">**Inbound NAT rules**: contains rules that map a public port on the load balancer to a port for a specific virtual machine in the back-end address pool</span></span>
* <span data-ttu-id="d8acb-118">**Probe**: contengono probe di integrità usati per verificare la disponibilità di istanze di macchine virtuali nel pool di indirizzi back-end</span><span class="sxs-lookup"><span data-stu-id="d8acb-118">**Probes**: contains health probes that are used to check the availability of virtual machines instances in the back-end address pool</span></span>

<span data-ttu-id="d8acb-119">Per altre informazioni, vedere [Supporto di Azure Resource Manager per Load Balancer](load-balancer-arm.md).</span><span class="sxs-lookup"><span data-stu-id="d8acb-119">For more information, see [Azure Resource Manager support for Load Balancer](load-balancer-arm.md).</span></span>

## <a name="set-up-cli-to-use-resource-manager"></a><span data-ttu-id="d8acb-120">Configurare l'interfaccia della riga di comando per l'uso di Resource Manager</span><span class="sxs-lookup"><span data-stu-id="d8acb-120">Set up CLI to use Resource Manager</span></span>

1. <span data-ttu-id="d8acb-121">Se l'interfaccia della riga di comando di Azure non è mai stata usata, vedere [Installare e configurare l'interfaccia della riga di comando di Azure](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="d8acb-121">If you have never used Azure CLI, see [Install and configure the Azure CLI](../cli-install-nodejs.md).</span></span> <span data-ttu-id="d8acb-122">Seguire le istruzioni fino al punto in cui si seleziona l'account Azure e la sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="d8acb-122">Follow the instructions up to the point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="d8acb-123">Eseguire il comando **azure config mode** per passare alla modalità Resource Manager, come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="d8acb-123">Run the **azure config mode** command to switch to Resource Manager mode, as follows:</span></span>

    ```azurecli
    azure config mode arm
    ```

    <span data-ttu-id="d8acb-124">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="d8acb-124">Expected output:</span></span>

        info:    New mode is arm

## <a name="create-an-internal-load-balancer-step-by-step"></a><span data-ttu-id="d8acb-125">Per creare un servizio di bilanciamento del carico interno, attenersi alla procedura dettagliata descritta di seguito</span><span class="sxs-lookup"><span data-stu-id="d8acb-125">Create an internal load balancer step by step</span></span>

1. <span data-ttu-id="d8acb-126">Accedere ad Azure.</span><span class="sxs-lookup"><span data-stu-id="d8acb-126">Sign in to Azure.</span></span>

    ```azurecli
    azure login
    ```

    <span data-ttu-id="d8acb-127">Quando richiesto, immettere le credenziali di Azure.</span><span class="sxs-lookup"><span data-stu-id="d8acb-127">When prompted, enter your Azure credentials.</span></span>

2. <span data-ttu-id="d8acb-128">Attivare la modalità Azure Resource Manager per gli strumenti di comando.</span><span class="sxs-lookup"><span data-stu-id="d8acb-128">Change the command tools to Azure Resource Manager mode.</span></span>

    ```azurecli
    azure config mode arm
    ```

## <a name="create-a-resource-group"></a><span data-ttu-id="d8acb-129">Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="d8acb-129">Create a resource group</span></span>

<span data-ttu-id="d8acb-130">Tutte le risorse in Azure Resource Manager vengono associate a un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="d8acb-130">All resources in Azure Resource Manager are associated with a resource group.</span></span> <span data-ttu-id="d8acb-131">Se non è ancora stato fatto, creare un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="d8acb-131">If you haven't done so yet, create a resource group.</span></span>

```azurecli
azure group create <resource group name> <location>
```

## <a name="create-an-internal-load-balancer-set"></a><span data-ttu-id="d8acb-132">Creare un set di bilanciamento del carico interno</span><span class="sxs-lookup"><span data-stu-id="d8acb-132">Create an internal load balancer set</span></span>

1. <span data-ttu-id="d8acb-133">Creare un bilanciamento del carico interno</span><span class="sxs-lookup"><span data-stu-id="d8acb-133">Create an internal load balancer</span></span>

    <span data-ttu-id="d8acb-134">Nello scenario seguente, viene creato un gruppo di risorse denominato nrprg viene creato nell'area Stati Uniti orientali.</span><span class="sxs-lookup"><span data-stu-id="d8acb-134">In the following scenario, a resource group named nrprg is created in East US region.</span></span>

    ```azurecli
    azure network lb create --name nrprg --location eastus
    ```

   > [!NOTE]
   > <span data-ttu-id="d8acb-135">Tutte le risorse per un servizio di bilanciamento del carico interno, ad esempio reti virtuali e subnet della rete virtuale, devono essere nello stesso gruppo di risorse e nella stessa area.</span><span class="sxs-lookup"><span data-stu-id="d8acb-135">All resources for an internal load balancers, such as virtual networks and virtual network subnets, must be in the same resource group and in the same region.</span></span>

2. <span data-ttu-id="d8acb-136">Creare un indirizzo IP di front-end per il servizio di bilanciamento del carico interno.</span><span class="sxs-lookup"><span data-stu-id="d8acb-136">Create a front-end IP address for the internal load balancer.</span></span>

    <span data-ttu-id="d8acb-137">L'indirizzo IP usato deve essere compreso nell'intervallo della subnet della rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="d8acb-137">The IP address that you use must be within the subnet range of your virtual network.</span></span>

    ```azurecli
    azure network lb frontend-ip create --resource-group nrprg --lb-name ilbset --name feilb --private-ip-address 10.0.0.7 --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet
    ```

3. <span data-ttu-id="d8acb-138">Creare un pool di indirizzi back-end.</span><span class="sxs-lookup"><span data-stu-id="d8acb-138">Create the back-end address pool.</span></span>

    ```azurecli
    azure network lb address-pool create --resource-group nrprg --lb-name ilbset --name beilb
    ```

    <span data-ttu-id="d8acb-139">Dopo aver definito un indirizzo IP front-end e un pool di indirizzi back-end, è possibile creare regole del servizio di bilanciamento del carico, regole NAT in ingresso e probe di integrità personalizzati.</span><span class="sxs-lookup"><span data-stu-id="d8acb-139">After you define a front-end IP address and a back-end address pool, you can create load balancer rules, inbound NAT rules, and customized health probes.</span></span>

4. <span data-ttu-id="d8acb-140">Creare una regola del servizio di bilanciamento del carico per il servizio di bilanciamento del carico interno.</span><span class="sxs-lookup"><span data-stu-id="d8acb-140">Create a load balancer rule for the internal load balancer.</span></span>

    <span data-ttu-id="d8acb-141">Attenendosi alla procedura precedente, il comando crea una regola del servizio di bilanciamento del carico in ascolto sulla porta 1433 nel pool front-end e invia traffico di rete con bilanciamento del carico al pool di indirizzi back-end usando ancora la porta 1433.</span><span class="sxs-lookup"><span data-stu-id="d8acb-141">When you follow the previous steps, the command creates a load-balancer rule for listening to port 1433 in the front-end pool and sending load-balanced network traffic to the back-end address pool, also using port 1433.</span></span>

    ```azurecli
    azure network lb rule create --resource-group nrprg --lb-name ilbset --name ilbrule --protocol tcp --frontend-port 1433 --backend-port 1433 --frontend-ip-name feilb --backend-address-pool-name beilb
    ```

5. <span data-ttu-id="d8acb-142">Creare regole NAT in ingresso.</span><span class="sxs-lookup"><span data-stu-id="d8acb-142">Create inbound NAT rules.</span></span>

    <span data-ttu-id="d8acb-143">Le regole NAT in ingresso vengono usate per creare endpoint in un servizio di bilanciamento del carico che viene inviato a un'istanza di macchina virtuale specifica.</span><span class="sxs-lookup"><span data-stu-id="d8acb-143">Inbound NAT rules are used to create endpoints in a load balancer that go to a specific virtual machine instance.</span></span> <span data-ttu-id="d8acb-144">Nei passaggi precedenti sono state create due regole NAT per il desktop remoto.</span><span class="sxs-lookup"><span data-stu-id="d8acb-144">The previous steps created two NAT rules  for remote desktop.</span></span>

    ```azurecli
    azure network lb inbound-nat-rule create --resource-group nrprg --lb-name ilbset --name NATrule1 --protocol TCP --frontend-port 5432 --backend-port 3389

    azure network lb inbound-nat-rule create --resource-group nrprg --lb-name ilbset --name NATrule2 --protocol TCP --frontend-port 5433 --backend-port 3389
    ```

6. <span data-ttu-id="d8acb-145">Creare probe di integrità per il servizio di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="d8acb-145">Create health probes for the load balancer.</span></span>

    <span data-ttu-id="d8acb-146">Un probe di integrità controlla tutte le istanze di una macchina virtuale per assicurarsi che possano inviare il traffico di rete.</span><span class="sxs-lookup"><span data-stu-id="d8acb-146">A health probe checks all virtual machine instances to make sure they can send network traffic.</span></span> <span data-ttu-id="d8acb-147">L'istanza della macchina virtuale con controlli di probe falliti non viene rimossa dal servizio di bilanciamento del carico fino a quando non è nuovamente online e il controllo dei probe ne certifica l'integrità.</span><span class="sxs-lookup"><span data-stu-id="d8acb-147">The virtual machine instance with failed probe checks is removed from the load balancer until it goes back online and a probe check determines that it's healthy.</span></span>

    ```azurecli
    azure network lb probe create --resource-group nrprg --lb-name ilbset --name ilbprobe --protocol tcp --interval 300 --count 4
    ```

    > [!NOTE]
    > <span data-ttu-id="d8acb-148">La piattaforma Microsoft Azure usa un indirizzo IPv4 statico e instradabile pubblicamente per un'ampia gamma di scenari di amministrazione.</span><span class="sxs-lookup"><span data-stu-id="d8acb-148">The Microsoft Azure platform uses a static, publicly routable IPv4 address for a variety of administrative scenarios.</span></span> <span data-ttu-id="d8acb-149">L'indirizzo IP è 168.63.129.16.</span><span class="sxs-lookup"><span data-stu-id="d8acb-149">The IP address is 168.63.129.16.</span></span> <span data-ttu-id="d8acb-150">Questo indirizzo IP non deve essere bloccato da alcun firewall, perché potrebbe causare un comportamento imprevisto.</span><span class="sxs-lookup"><span data-stu-id="d8acb-150">This IP address should not be blocked by any firewalls, because this can cause unexpected behavior.</span></span>
    > <span data-ttu-id="d8acb-151">Per quanto riguarda il bilanciamento del carico interno di Azure, questo indirizzo IP viene usato da probe di monitoraggio del servizio di bilanciamento del carico per determinare lo stato di integrità delle macchine virtuali in un set con carico bilanciato.</span><span class="sxs-lookup"><span data-stu-id="d8acb-151">With respect to Azure internal load balancing, this IP address is used by monitoring probes from the load balancer to determine the health state for virtual machines in a load-balanced set.</span></span> <span data-ttu-id="d8acb-152">Se si usa un gruppo di sicurezza di rete per limitare il traffico alle macchine virtuali di Azure in un set con carico bilanciato internamente o lo si applica a una subnet di rete virtuale, assicurarsi di aggiungere una regola di sicurezza di rete per consentire il traffico dall'indirizzo 168.63.129.16.</span><span class="sxs-lookup"><span data-stu-id="d8acb-152">If a network security group is used to restrict traffic to Azure virtual machines in an internally load-balanced set or is applied to a virtual network subnet, ensure that a network security rule is added to allow traffic from 168.63.129.16.</span></span>

## <a name="create-nics"></a><span data-ttu-id="d8acb-153">Creare NIC</span><span class="sxs-lookup"><span data-stu-id="d8acb-153">Create NICs</span></span>

<span data-ttu-id="d8acb-154">È necessario creare schede di interfaccia di rete (NIC) o modificare quelle esistenti e associarle a regole NAT, regole del servizio di bilanciamento del carico e probe.</span><span class="sxs-lookup"><span data-stu-id="d8acb-154">You need to create NICs (or modify existing ones) and associate them to NAT rules, load balancer rules, and probes.</span></span>

1. <span data-ttu-id="d8acb-155">Creare una scheda di interfaccia di rete denominata *lb-nic1-be* e associarla alla regola NAT *rdp1* e al pool di indirizzi back-end *beilb*.</span><span class="sxs-lookup"><span data-stu-id="d8acb-155">Create an NIC named *lb-nic1-be*, and then associate it with the *rdp1* NAT rule and the *beilb* back-end address pool.</span></span>

    ```azurecli
    azure network nic create --resource-group nrprg --name lb-nic1-be --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet --lb-address-pool-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/beilb" --lb-inbound-nat-rule-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp1" --location eastus
    ```

    <span data-ttu-id="d8acb-156">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="d8acb-156">Expected output:</span></span>

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

2. <span data-ttu-id="d8acb-157">Creare una scheda di interfaccia di rete denominata *lb-nic2-be* e associarla alla regola NAT *rdp2* e al pool di indirizzi back-end *beilb*.</span><span class="sxs-lookup"><span data-stu-id="d8acb-157">Create an NIC named *lb-nic2-be*, and then associate it with the *rdp2* NAT rule and the *beilb* back-end address pool.</span></span>

    ```azurecli
    azure network nic create --resource-group nrprg --name lb-nic2-be --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet --lb-address-pool-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/beilb" --lb-inbound-nat-rule-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp2" --location eastus
    ```

3. <span data-ttu-id="d8acb-158">Creare una macchina virtuale denominata *DB1* e associarla alla scheda di interfaccia di rete denominata *lb-nic1-be*.</span><span class="sxs-lookup"><span data-stu-id="d8acb-158">Create a virtual machine named *DB1*, and then associate it with the NIC named *lb-nic1-be*.</span></span> <span data-ttu-id="d8acb-159">Un account di archiviazione denominato *web1nrp* è stato creato prima dell'esecuzione del comando seguente:</span><span class="sxs-lookup"><span data-stu-id="d8acb-159">A storage account called *web1nrp* is created before the following command runs:</span></span>

    ```azurecli
    azure vm create --resource--resource-grouproup nrprg --name DB1 --location eastus --vnet-name nrpvnet --vnet-subnet-name nrpvnetsubnet --nic-name lb-nic1-be --availset-name nrp-avset --storage-account-name web1nrp --os-type Windows --image-urn MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:4.0.20150825
    ```
    > [!IMPORTANT]
    > <span data-ttu-id="d8acb-160">Le macchine virtuali in un servizio di bilanciamento del carico devono trovarsi nello stesso set di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="d8acb-160">VMs in a load balancer need to be in the same availability set.</span></span> <span data-ttu-id="d8acb-161">Usare `azure availset create` per creare un set di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="d8acb-161">Use `azure availset create` to create an availability set.</span></span>

4. <span data-ttu-id="d8acb-162">Creare una macchina virtuale (VM) denominata *DB2* e associarla alla scheda di interfaccia di rete denominata *lb-nic2-be*.</span><span class="sxs-lookup"><span data-stu-id="d8acb-162">Create a virtual machine (VM) named *DB2*, and then associate it with the NIC named *lb-nic2-be*.</span></span> <span data-ttu-id="d8acb-163">Un account di archiviazione denominato *web1nrp* è stato creato prima dell'esecuzione del comando seguente.</span><span class="sxs-lookup"><span data-stu-id="d8acb-163">A storage account called *web1nrp* was created before running the following command.</span></span>

    ```azurecli
    azure vm create --resource--resource-grouproup nrprg --name DB2 --location eastus --vnet-name nrpvnet --vnet-subnet-name nrpvnetsubnet --nic-name lb-nic2-be --availset-name nrp-avset --storage-account-name web2nrp --os-type Windows --image-urn MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:4.0.20150825
    ```

## <a name="delete-a-load-balancer"></a><span data-ttu-id="d8acb-164">Eliminare un servizio di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="d8acb-164">Delete a load balancer</span></span>

<span data-ttu-id="d8acb-165">Per rimuovere un servizio di bilanciamento del carico, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="d8acb-165">To remove a load balancer, use the following command:</span></span>

```azurecli
azure network lb delete --resource-group nrprg --name ilbset
```

## <a name="next-steps"></a><span data-ttu-id="d8acb-166">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d8acb-166">Next steps</span></span>

[<span data-ttu-id="d8acb-167">Configurare una modalità di distribuzione del servizio di bilanciamento del carico usando l'affinità dell'IP di origine</span><span class="sxs-lookup"><span data-stu-id="d8acb-167">Configure a load balancer distribution mode by using source IP affinity</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="d8acb-168">Configurare le impostazioni del timeout di inattività TCP per il bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="d8acb-168">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)

