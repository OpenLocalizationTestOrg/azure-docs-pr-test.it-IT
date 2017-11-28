---
title: un uso interno aaaCreate bilanciamento del carico - CLI di Azure | Documenti Microsoft
description: Informazioni su come un servizio di bilanciamento del carico interno utilizzando toocreate hello CLI di Azure in Gestione risorse
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
ms.openlocfilehash: 3aea6fdb07600f0d661ec6b8ffc784b03380a127
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-internal-load-balancer-by-using-hello-azure-cli"></a><span data-ttu-id="c2dfe-103">Creare un servizio di bilanciamento del carico interno utilizzando hello CLI di Azure</span><span class="sxs-lookup"><span data-stu-id="c2dfe-103">Create an internal load balancer by using hello Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="c2dfe-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="c2dfe-104">Azure Portal</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-portal.md)
> * [<span data-ttu-id="c2dfe-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c2dfe-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-ps.md)
> * [<span data-ttu-id="c2dfe-106">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="c2dfe-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-cli.md)
> * [<span data-ttu-id="c2dfe-107">Modello</span><span class="sxs-lookup"><span data-stu-id="c2dfe-107">Template</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-template.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="c2dfe-108">Azure offre due modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="c2dfe-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="c2dfe-109">In questo articolo viene illustrato l'utilizzo modello di distribuzione di gestione delle risorse hello, si consiglia di per la maggior parte delle nuove distribuzioni anziché hello [modello di distribuzione classica](load-balancer-get-started-ilb-classic-cli.md).</span><span class="sxs-lookup"><span data-stu-id="c2dfe-109">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello [classic deployment model](load-balancer-get-started-ilb-classic-cli.md).</span></span>

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

## <a name="deploy-hello-solution-by-using-hello-azure-cli"></a><span data-ttu-id="c2dfe-110">Distribuire la soluzione hello utilizzando hello CLI di Azure</span><span class="sxs-lookup"><span data-stu-id="c2dfe-110">Deploy hello solution by using hello Azure CLI</span></span>

<span data-ttu-id="c2dfe-111">Hello alla procedura seguente viene illustrato come toocreate con una connessione Internet il bilanciamento del carico con Gestione risorse di Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="c2dfe-111">hello following steps show how toocreate an Internet-facing load balancer by using Azure Resource Manager with CLI.</span></span> <span data-ttu-id="c2dfe-112">Con Gestione risorse di Azure, ogni risorsa viene creata e configurata individualmente e riunire toocreate una risorsa.</span><span class="sxs-lookup"><span data-stu-id="c2dfe-112">With Azure Resource Manager, each resource is created and configured individually, and then put together toocreate a resource.</span></span>

<span data-ttu-id="c2dfe-113">È necessario toocreate e configurare hello oggetti toodeploy un bilanciamento del carico seguenti:</span><span class="sxs-lookup"><span data-stu-id="c2dfe-113">You need toocreate and configure hello following objects toodeploy a load balancer:</span></span>

* <span data-ttu-id="c2dfe-114">**Configurazione di IP front-end**: contiene gli indirizzi IP pubblici per il traffico di rete in ingresso</span><span class="sxs-lookup"><span data-stu-id="c2dfe-114">**Front-end IP configuration**: contains public IP addresses for incoming network traffic</span></span>
* <span data-ttu-id="c2dfe-115">**Pool di indirizzi back-end**: contiene le interfacce di rete (NIC) che consentono di tooreceive il traffico di rete dal servizio di bilanciamento del carico hello hello macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="c2dfe-115">**Back-end address pool**: contains network interfaces (NICs) that enable hello virtual machines tooreceive network traffic from hello load balancer</span></span>
* <span data-ttu-id="c2dfe-116">**Regole di bilanciamento del carico**: contiene le regole che eseguono il mapping di una porta pubblica su tooport del servizio di bilanciamento carico di hello nel pool di indirizzi back-end di hello</span><span class="sxs-lookup"><span data-stu-id="c2dfe-116">**Load-balancing rules**: contains rules that map a public port on hello load balancer tooport in hello back-end address pool</span></span>
* <span data-ttu-id="c2dfe-117">**Regole NAT in ingresso**: contiene le regole che eseguono il mapping di una porta pubblica nella porta di tooa del bilanciamento del carico hello per una macchina virtuale specifica nel pool di indirizzi back-end di hello</span><span class="sxs-lookup"><span data-stu-id="c2dfe-117">**Inbound NAT rules**: contains rules that map a public port on hello load balancer tooa port for a specific virtual machine in hello back-end address pool</span></span>
* <span data-ttu-id="c2dfe-118">**Probe**: contiene i probe di integrità che vengono utilizzati toocheck hello disponibilità delle istanze di macchine virtuali nel pool di indirizzi back-end di hello</span><span class="sxs-lookup"><span data-stu-id="c2dfe-118">**Probes**: contains health probes that are used toocheck hello availability of virtual machines instances in hello back-end address pool</span></span>

<span data-ttu-id="c2dfe-119">Per altre informazioni, vedere [Supporto di Azure Resource Manager per Load Balancer](load-balancer-arm.md).</span><span class="sxs-lookup"><span data-stu-id="c2dfe-119">For more information, see [Azure Resource Manager support for Load Balancer](load-balancer-arm.md).</span></span>

## <a name="set-up-cli-toouse-resource-manager"></a><span data-ttu-id="c2dfe-120">Impostare CLI toouse Gestione risorse</span><span class="sxs-lookup"><span data-stu-id="c2dfe-120">Set up CLI toouse Resource Manager</span></span>

1. <span data-ttu-id="c2dfe-121">Se non si è mai usato CLI di Azure, vedere [installare e configurare hello Azure CLI](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="c2dfe-121">If you have never used Azure CLI, see [Install and configure hello Azure CLI](../cli-install-nodejs.md).</span></span> <span data-ttu-id="c2dfe-122">Seguire le istruzioni di hello toohello un punto in cui si seleziona l'account di Azure e la sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="c2dfe-122">Follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="c2dfe-123">Eseguire hello **modalità di configurazione azure** comando tooswitch tooResource Manager modalità, come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="c2dfe-123">Run hello **azure config mode** command tooswitch tooResource Manager mode, as follows:</span></span>

    ```azurecli
    azure config mode arm
    ```

    <span data-ttu-id="c2dfe-124">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="c2dfe-124">Expected output:</span></span>

        info:    New mode is arm

## <a name="create-an-internal-load-balancer-step-by-step"></a><span data-ttu-id="c2dfe-125">Per creare un servizio di bilanciamento del carico interno, attenersi alla procedura dettagliata descritta di seguito</span><span class="sxs-lookup"><span data-stu-id="c2dfe-125">Create an internal load balancer step by step</span></span>

1. <span data-ttu-id="c2dfe-126">Accedi tooAzure.</span><span class="sxs-lookup"><span data-stu-id="c2dfe-126">Sign in tooAzure.</span></span>

    ```azurecli
    azure login
    ```

    <span data-ttu-id="c2dfe-127">Quando richiesto, immettere le credenziali di Azure.</span><span class="sxs-lookup"><span data-stu-id="c2dfe-127">When prompted, enter your Azure credentials.</span></span>

2. <span data-ttu-id="c2dfe-128">Modificare la modalità di gestione delle risorse hello comando strumenti tooAzure.</span><span class="sxs-lookup"><span data-stu-id="c2dfe-128">Change hello command tools tooAzure Resource Manager mode.</span></span>

    ```azurecli
    azure config mode arm
    ```

## <a name="create-a-resource-group"></a><span data-ttu-id="c2dfe-129">Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="c2dfe-129">Create a resource group</span></span>

<span data-ttu-id="c2dfe-130">Tutte le risorse in Azure Resource Manager vengono associate a un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="c2dfe-130">All resources in Azure Resource Manager are associated with a resource group.</span></span> <span data-ttu-id="c2dfe-131">Se non è ancora stato fatto, creare un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="c2dfe-131">If you haven't done so yet, create a resource group.</span></span>

```azurecli
azure group create <resource group name> <location>
```

## <a name="create-an-internal-load-balancer-set"></a><span data-ttu-id="c2dfe-132">Creare un set di bilanciamento del carico interno</span><span class="sxs-lookup"><span data-stu-id="c2dfe-132">Create an internal load balancer set</span></span>

1. <span data-ttu-id="c2dfe-133">Creare un bilanciamento del carico interno</span><span class="sxs-lookup"><span data-stu-id="c2dfe-133">Create an internal load balancer</span></span>

    <span data-ttu-id="c2dfe-134">In hello seguente scenario, viene creato un gruppo di risorse denominato nrprg nell'area Stati Uniti orientali.</span><span class="sxs-lookup"><span data-stu-id="c2dfe-134">In hello following scenario, a resource group named nrprg is created in East US region.</span></span>

    ```azurecli
    azure network lb create --name nrprg --location eastus
    ```

   > [!NOTE]
   > <span data-ttu-id="c2dfe-135">Tutte le risorse per un bilanciamento del carico interno, ad esempio le reti virtuali e subnet della rete virtuale, è necessario hello stesso gruppo di risorse e in hello stessa area.</span><span class="sxs-lookup"><span data-stu-id="c2dfe-135">All resources for an internal load balancers, such as virtual networks and virtual network subnets, must be in hello same resource group and in hello same region.</span></span>

2. <span data-ttu-id="c2dfe-136">Creare un indirizzo IP front-end di bilanciamento del carico interno hello.</span><span class="sxs-lookup"><span data-stu-id="c2dfe-136">Create a front-end IP address for hello internal load balancer.</span></span>

    <span data-ttu-id="c2dfe-137">indirizzo IP Hello in uso deve essere entro l'intervallo di hello subnet della rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="c2dfe-137">hello IP address that you use must be within hello subnet range of your virtual network.</span></span>

    ```azurecli
    azure network lb frontend-ip create --resource-group nrprg --lb-name ilbset --name feilb --private-ip-address 10.0.0.7 --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet
    ```

3. <span data-ttu-id="c2dfe-138">Creare il pool di indirizzi back-end di hello.</span><span class="sxs-lookup"><span data-stu-id="c2dfe-138">Create hello back-end address pool.</span></span>

    ```azurecli
    azure network lb address-pool create --resource-group nrprg --lb-name ilbset --name beilb
    ```

    <span data-ttu-id="c2dfe-139">Dopo aver definito un indirizzo IP front-end e un pool di indirizzi back-end, è possibile creare regole del servizio di bilanciamento del carico, regole NAT in ingresso e probe di integrità personalizzati.</span><span class="sxs-lookup"><span data-stu-id="c2dfe-139">After you define a front-end IP address and a back-end address pool, you can create load balancer rules, inbound NAT rules, and customized health probes.</span></span>

4. <span data-ttu-id="c2dfe-140">Creare una regola di bilanciamento del carico di bilanciamento del carico interno hello.</span><span class="sxs-lookup"><span data-stu-id="c2dfe-140">Create a load balancer rule for hello internal load balancer.</span></span>

    <span data-ttu-id="c2dfe-141">Quando si seguono i passaggi precedenti hello, hello comando crea una regola di bilanciamento del carico per l'ascolto tooport 1433 nel pool di server front-end hello e pool di indirizzi back-end toohello di traffico di invio con bilanciamento del carico di rete, anche tramite la porta 1433.</span><span class="sxs-lookup"><span data-stu-id="c2dfe-141">When you follow hello previous steps, hello command creates a load-balancer rule for listening tooport 1433 in hello front-end pool and sending load-balanced network traffic toohello back-end address pool, also using port 1433.</span></span>

    ```azurecli
    azure network lb rule create --resource-group nrprg --lb-name ilbset --name ilbrule --protocol tcp --frontend-port 1433 --backend-port 1433 --frontend-ip-name feilb --backend-address-pool-name beilb
    ```

5. <span data-ttu-id="c2dfe-142">Creare regole NAT in ingresso.</span><span class="sxs-lookup"><span data-stu-id="c2dfe-142">Create inbound NAT rules.</span></span>

    <span data-ttu-id="c2dfe-143">Le regole NAT in ingresso sono endpoint toocreate utilizzati in un bilanciamento del carico che vanno tooa macchina virtuale specifica istanza.</span><span class="sxs-lookup"><span data-stu-id="c2dfe-143">Inbound NAT rules are used toocreate endpoints in a load balancer that go tooa specific virtual machine instance.</span></span> <span data-ttu-id="c2dfe-144">passaggi precedenti Hello create due regole NAT per il desktop remoto.</span><span class="sxs-lookup"><span data-stu-id="c2dfe-144">hello previous steps created two NAT rules  for remote desktop.</span></span>

    ```azurecli
    azure network lb inbound-nat-rule create --resource-group nrprg --lb-name ilbset --name NATrule1 --protocol TCP --frontend-port 5432 --backend-port 3389

    azure network lb inbound-nat-rule create --resource-group nrprg --lb-name ilbset --name NATrule2 --protocol TCP --frontend-port 5433 --backend-port 3389
    ```

6. <span data-ttu-id="c2dfe-145">Creare il probe di integrità servizio di bilanciamento del carico hello.</span><span class="sxs-lookup"><span data-stu-id="c2dfe-145">Create health probes for hello load balancer.</span></span>

    <span data-ttu-id="c2dfe-146">Un probe di integrità controlla tutti toomake istanze macchina virtuale che possono inviare il traffico di rete.</span><span class="sxs-lookup"><span data-stu-id="c2dfe-146">A health probe checks all virtual machine instances toomake sure they can send network traffic.</span></span> <span data-ttu-id="c2dfe-147">istanza di macchina virtuale Hello con i controlli di probe non viene rimosso dal servizio di bilanciamento del carico hello fino a quando non diventa nuovamente online e un controllo di probe determina che è integro.</span><span class="sxs-lookup"><span data-stu-id="c2dfe-147">hello virtual machine instance with failed probe checks is removed from hello load balancer until it goes back online and a probe check determines that it's healthy.</span></span>

    ```azurecli
    azure network lb probe create --resource-group nrprg --lb-name ilbset --name ilbprobe --protocol tcp --interval 300 --count 4
    ```

    > [!NOTE]
    > <span data-ttu-id="c2dfe-148">piattaforma Microsoft Azure Hello utilizza un indirizzo IPv4 statico, instradabile pubblicamente per un'ampia gamma di scenari di amministrazione.</span><span class="sxs-lookup"><span data-stu-id="c2dfe-148">hello Microsoft Azure platform uses a static, publicly routable IPv4 address for a variety of administrative scenarios.</span></span> <span data-ttu-id="c2dfe-149">indirizzo IP Hello è 168.63.129.16.</span><span class="sxs-lookup"><span data-stu-id="c2dfe-149">hello IP address is 168.63.129.16.</span></span> <span data-ttu-id="c2dfe-150">Questo indirizzo IP non deve essere bloccato da alcun firewall, perché potrebbe causare un comportamento imprevisto.</span><span class="sxs-lookup"><span data-stu-id="c2dfe-150">This IP address should not be blocked by any firewalls, because this can cause unexpected behavior.</span></span>
    > <span data-ttu-id="c2dfe-151">Con riguardo tooAzure interno il bilanciamento del carico, viene utilizzato questo indirizzo IP dal monitoraggio probe di stato di integrità hello toodetermine bilanciamento del carico hello per le macchine virtuali in un set con carico bilanciato.</span><span class="sxs-lookup"><span data-stu-id="c2dfe-151">With respect tooAzure internal load balancing, this IP address is used by monitoring probes from hello load balancer toodetermine hello health state for virtual machines in a load-balanced set.</span></span> <span data-ttu-id="c2dfe-152">Se un gruppo di sicurezza di rete è utilizzata toorestrict traffico tooAzure le macchine virtuali in un set di internamente con bilanciamento del carico o applicato tooa subnet della rete virtuale, assicurarsi che una regola di sicurezza di rete viene aggiunto il traffico tooallow 168.63.129.16.</span><span class="sxs-lookup"><span data-stu-id="c2dfe-152">If a network security group is used toorestrict traffic tooAzure virtual machines in an internally load-balanced set or is applied tooa virtual network subnet, ensure that a network security rule is added tooallow traffic from 168.63.129.16.</span></span>

## <a name="create-nics"></a><span data-ttu-id="c2dfe-153">Creare NIC</span><span class="sxs-lookup"><span data-stu-id="c2dfe-153">Create NICs</span></span>

<span data-ttu-id="c2dfe-154">È necessario toocreate NIC (o modificare quelli esistenti) e associarli tooNAT regole, regole di bilanciamento del carico e probe.</span><span class="sxs-lookup"><span data-stu-id="c2dfe-154">You need toocreate NICs (or modify existing ones) and associate them tooNAT rules, load balancer rules, and probes.</span></span>

1. <span data-ttu-id="c2dfe-155">Creare una scheda di rete denominata *lb-nic1 essere*e quindi associarlo hello *rdp1* NAT regola e hello *beilb* pool di indirizzi back-end.</span><span class="sxs-lookup"><span data-stu-id="c2dfe-155">Create an NIC named *lb-nic1-be*, and then associate it with hello *rdp1* NAT rule and hello *beilb* back-end address pool.</span></span>

    ```azurecli
    azure network nic create --resource-group nrprg --name lb-nic1-be --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet --lb-address-pool-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/beilb" --lb-inbound-nat-rule-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp1" --location eastus
    ```

    <span data-ttu-id="c2dfe-156">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="c2dfe-156">Expected output:</span></span>

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

2. <span data-ttu-id="c2dfe-157">Creare una scheda di rete denominata *lb-nic2 essere*e quindi associarlo hello *rdp2* NAT regola e hello *beilb* pool di indirizzi back-end.</span><span class="sxs-lookup"><span data-stu-id="c2dfe-157">Create an NIC named *lb-nic2-be*, and then associate it with hello *rdp2* NAT rule and hello *beilb* back-end address pool.</span></span>

    ```azurecli
    azure network nic create --resource-group nrprg --name lb-nic2-be --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet --lb-address-pool-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/beilb" --lb-inbound-nat-rule-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp2" --location eastus
    ```

3. <span data-ttu-id="c2dfe-158">Creare una macchina virtuale denominata *DB1*e quindi associarlo hello NIC denominato *lb-nic1 essere*.</span><span class="sxs-lookup"><span data-stu-id="c2dfe-158">Create a virtual machine named *DB1*, and then associate it with hello NIC named *lb-nic1-be*.</span></span> <span data-ttu-id="c2dfe-159">Un account di archiviazione denominato *web1nrp* sia stato creato prima hello eseguito il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="c2dfe-159">A storage account called *web1nrp* is created before hello following command runs:</span></span>

    ```azurecli
    azure vm create --resource--resource-grouproup nrprg --name DB1 --location eastus --vnet-name nrpvnet --vnet-subnet-name nrpvnetsubnet --nic-name lb-nic1-be --availset-name nrp-avset --storage-account-name web1nrp --os-type Windows --image-urn MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:4.0.20150825
    ```
    > [!IMPORTANT]
    > <span data-ttu-id="c2dfe-160">Macchine virtuali in un toobe necessità bilanciamento di carico in hello stesso set di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="c2dfe-160">VMs in a load balancer need toobe in hello same availability set.</span></span> <span data-ttu-id="c2dfe-161">Utilizzare `azure availset create` toocreate un gruppo di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="c2dfe-161">Use `azure availset create` toocreate an availability set.</span></span>

4. <span data-ttu-id="c2dfe-162">Creare una macchina virtuale (VM) denominata *DB2*e quindi associarlo hello NIC denominato *lb-nic2 essere*.</span><span class="sxs-lookup"><span data-stu-id="c2dfe-162">Create a virtual machine (VM) named *DB2*, and then associate it with hello NIC named *lb-nic2-be*.</span></span> <span data-ttu-id="c2dfe-163">Un account di archiviazione denominato *web1nrp* è stato creato prima di eseguire hello comando seguente.</span><span class="sxs-lookup"><span data-stu-id="c2dfe-163">A storage account called *web1nrp* was created before running hello following command.</span></span>

    ```azurecli
    azure vm create --resource--resource-grouproup nrprg --name DB2 --location eastus --vnet-name nrpvnet --vnet-subnet-name nrpvnetsubnet --nic-name lb-nic2-be --availset-name nrp-avset --storage-account-name web2nrp --os-type Windows --image-urn MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:4.0.20150825
    ```

## <a name="delete-a-load-balancer"></a><span data-ttu-id="c2dfe-164">Eliminare un servizio di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="c2dfe-164">Delete a load balancer</span></span>

<span data-ttu-id="c2dfe-165">tooremove un bilanciamento del carico, utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="c2dfe-165">tooremove a load balancer, use hello following command:</span></span>

```azurecli
azure network lb delete --resource-group nrprg --name ilbset
```

## <a name="next-steps"></a><span data-ttu-id="c2dfe-166">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c2dfe-166">Next steps</span></span>

[<span data-ttu-id="c2dfe-167">Configurare una modalità di distribuzione del servizio di bilanciamento del carico usando l'affinità dell'IP di origine</span><span class="sxs-lookup"><span data-stu-id="c2dfe-167">Configure a load balancer distribution mode by using source IP affinity</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="c2dfe-168">Configurare le impostazioni del timeout di inattività TCP per il bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="c2dfe-168">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)

