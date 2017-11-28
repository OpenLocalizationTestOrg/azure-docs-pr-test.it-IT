---
title: aaaOpen porte tooa VM Linux con Azure CLI 2.0 | Documenti Microsoft
description: Informazioni su come tooopen una porta / creare una VM Linux di tooyour endpoint utilizzando la distribuzione di gestione risorse di Azure hello del modello e hello Azure CLI 2.0
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: eef9842b-495a-46cf-99a6-74e49807e74e
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 08/21/2017
ms.author: iainfou
ms.openlocfilehash: c79b31206e97558171609cf033bb3cb3370777c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="open-ports-and-endpoints-tooa-linux-vm-with-hello-azure-cli"></a><span data-ttu-id="f0449-103">Aprire le porte e gli endpoint tooa VM Linux con hello CLI di Azure</span><span class="sxs-lookup"><span data-stu-id="f0449-103">Open ports and endpoints tooa Linux VM with hello Azure CLI</span></span>
<span data-ttu-id="f0449-104">Aprire una porta o creare un endpoint, tooa macchina virtuale (VM) in Azure tramite la creazione di un filtro di rete su una subnet o l'interfaccia di rete VM.</span><span class="sxs-lookup"><span data-stu-id="f0449-104">You open a port, or create an endpoint, tooa virtual machine (VM) in Azure by creating a network filter on a subnet or VM network interface.</span></span> <span data-ttu-id="f0449-105">Questi filtri, che consentono di controllare il traffico in ingresso e in uscita, posizionare in una risorsa toohello gruppo di sicurezza di rete associata che riceve il traffico di hello.</span><span class="sxs-lookup"><span data-stu-id="f0449-105">You place these filters, which control both inbound and outbound traffic, on a Network Security Group attached toohello resource that receives hello traffic.</span></span> <span data-ttu-id="f0449-106">Si userà un esempio comune di traffico Web sulla porta 80.</span><span class="sxs-lookup"><span data-stu-id="f0449-106">Let's use a common example of web traffic on port 80.</span></span> <span data-ttu-id="f0449-107">In questo articolo illustra come tooopen tooa una porta VM con hello CLI di Azure 2.0.</span><span class="sxs-lookup"><span data-stu-id="f0449-107">This article shows you how tooopen a port tooa VM with hello Azure CLI 2.0.</span></span> <span data-ttu-id="f0449-108">È anche possibile eseguire questi passaggi con hello [CLI di Azure 1.0](nsg-quickstart-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="f0449-108">You can also perform these steps with hello [Azure CLI 1.0](nsg-quickstart-nodejs.md).</span></span>


## <a name="quick-commands"></a><span data-ttu-id="f0449-109">Comandi rapidi</span><span class="sxs-lookup"><span data-stu-id="f0449-109">Quick commands</span></span>
<span data-ttu-id="f0449-110">Gruppo di sicurezza di rete toocreate e regole, è necessario hello più recente [CLI di Azure 2.0](/cli/azure/install-az-cli2) installato e registrato con un account Azure tooan [accesso az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="f0449-110">toocreate a Network Security Group and rules you need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="f0449-111">In hello negli esempi seguenti, sostituire i nomi dei parametri di esempio con i valori desiderati.</span><span class="sxs-lookup"><span data-stu-id="f0449-111">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="f0449-112">I nomi dei parametri di esempio includono *myResourceGroup*, *myNetworkSecurityGroup* e *myVnet*.</span><span class="sxs-lookup"><span data-stu-id="f0449-112">Example parameter names include *myResourceGroup*, *myNetworkSecurityGroup*, and *myVnet*.</span></span>

<span data-ttu-id="f0449-113">Creare un gruppo di sicurezza di rete hello con [rete az creare](/cli/azure/network/nsg#create).</span><span class="sxs-lookup"><span data-stu-id="f0449-113">Create hello network security group with [az network nsg create](/cli/azure/network/nsg#create).</span></span> <span data-ttu-id="f0449-114">esempio Hello crea un gruppo di sicurezza di rete denominato *myNetworkSecurityGroup* in hello *eastus* percorso:</span><span class="sxs-lookup"><span data-stu-id="f0449-114">hello following example creates a network security group named *myNetworkSecurityGroup* in hello *eastus* location:</span></span>

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNetworkSecurityGroup
```

<span data-ttu-id="f0449-115">Aggiungere una regola con [creare una regola gruppo rete az](/cli/azure/network/nsg/rule#create) tooallow HTTP traffico webserver tooyour (o modificare per proprio scenario, ad esempio la connettività di accesso o database SSH).</span><span class="sxs-lookup"><span data-stu-id="f0449-115">Add a rule with [az network nsg rule create](/cli/azure/network/nsg/rule#create) tooallow HTTP traffic tooyour webserver (or adjust for your own scenario, such as SSH access or database connectivity).</span></span> <span data-ttu-id="f0449-116">esempio Hello crea una regola denominata *myNetworkSecurityGroupRule* tooallow TCP il traffico sulla porta 80:</span><span class="sxs-lookup"><span data-stu-id="f0449-116">hello following example creates a rule named *myNetworkSecurityGroupRule* tooallow TCP traffic on port 80:</span></span>

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRule \
    --protocol tcp \
    --priority 1000 \
    --destination-port-range 80
```

<span data-ttu-id="f0449-117">Associare il gruppo di sicurezza di rete hello con interfaccia di rete della macchina virtuale (NIC) [aggiornamento nic di rete az](/cli/azure/network/nic#update).</span><span class="sxs-lookup"><span data-stu-id="f0449-117">Associate hello Network Security Group with your VM's network interface (NIC) with [az network nic update](/cli/azure/network/nic#update).</span></span> <span data-ttu-id="f0449-118">esempio Hello associa una scheda di rete esistente denominato *myNic* con il gruppo di sicurezza di rete denominata hello *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="f0449-118">hello following example associates an existing NIC named *myNic* with hello Network Security Group named *myNetworkSecurityGroup*:</span></span>

```azurecli
az network nic update \
    --resource-group myResourceGroup \
    --name myNic \
    --network-security-group myNetworkSecurityGroup
```

<span data-ttu-id="f0449-119">In alternativa, è possibile associare il gruppo di sicurezza di rete a una subnet di rete virtuale con [aggiornare subnet rete virtuale di rete az](/cli/azure/network/vnet/subnet#update) anziché semplicemente toohello interfaccia di rete in una singola macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="f0449-119">Alternatively, you can associate your Network Security Group with a virtual network subnet with [az network vnet subnet update](/cli/azure/network/vnet/subnet#update) rather than just toohello network interface on a single VM.</span></span> <span data-ttu-id="f0449-120">esempio Hello associa una subnet esistente denominata *mySubnet* in hello *myVnet* rete virtuale con il gruppo di sicurezza di rete denominata hello *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="f0449-120">hello following example associates an existing subnet named *mySubnet* in hello *myVnet* virtual network with hello Network Security Group named *myNetworkSecurityGroup*:</span></span>

```azurecli
az network vnet subnet update \
    --resource-group myResourceGroup \
    --vnet-name myVnet \
    --name mySubnet \
    --network-security-group myNetworkSecurityGroup
```

## <a name="more-information-on-network-security-groups"></a><span data-ttu-id="f0449-121">Altre informazioni sui gruppi di sicurezza di rete</span><span class="sxs-lookup"><span data-stu-id="f0449-121">More information on Network Security Groups</span></span>
<span data-ttu-id="f0449-122">Hello rapido comandi consentono di tooget backup e in esecuzione con traffico propagazione tooyour macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="f0449-122">hello quick commands here allow you tooget up and running with traffic flowing tooyour VM.</span></span> <span data-ttu-id="f0449-123">Gruppi di sicurezza di rete forniscono numerose funzionalità eccellenti e granularità per il controllo tooyour di accedere alle risorse.</span><span class="sxs-lookup"><span data-stu-id="f0449-123">Network Security Groups provide many great features and granularity for controlling access tooyour resources.</span></span> <span data-ttu-id="f0449-124">Per altre informazioni, leggere l'articolo sulla [creazione di un gruppo di sicurezza di rete e di regole dell'elenco di controllo di accesso qui](tutorial-virtual-network.md#secure-network-traffic).</span><span class="sxs-lookup"><span data-stu-id="f0449-124">You can read more about [creating a Network Security Group and ACL rules here](tutorial-virtual-network.md#secure-network-traffic).</span></span>

<span data-ttu-id="f0449-125">Per le applicazioni Web a disponibilità elevata, è consigliabile inserire le macchine virtuali dietro a un Azure Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="f0449-125">For highly available web applications, you should place your VMs behind an Azure Load Balancer.</span></span> <span data-ttu-id="f0449-126">bilanciamento del carico di Hello distribuisce il traffico tooVMs, con un gruppo di sicurezza di rete che consente di filtrare il traffico.</span><span class="sxs-lookup"><span data-stu-id="f0449-126">hello load balancer distributes traffic tooVMs, with a Network Security Group that provides traffic filtering.</span></span> <span data-ttu-id="f0449-127">Per ulteriori informazioni, vedere [come macchine saldo tooload virtuali Linux in Azure toocreate applicazioni a disponibilità elevata](tutorial-load-balancer.md).</span><span class="sxs-lookup"><span data-stu-id="f0449-127">For more information, see [How tooload balance Linux virtual machines in Azure toocreate a highly available application](tutorial-load-balancer.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f0449-128">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f0449-128">Next steps</span></span>
<span data-ttu-id="f0449-129">In questo esempio è stato creato il traffico HTTP tooallow una semplice regola.</span><span class="sxs-lookup"><span data-stu-id="f0449-129">In this example, you created a simple rule tooallow HTTP traffic.</span></span> <span data-ttu-id="f0449-130">È possibile trovare informazioni sulla creazione di ambienti più dettagliati in hello seguenti articoli:</span><span class="sxs-lookup"><span data-stu-id="f0449-130">You can find information on creating more detailed environments in hello following articles:</span></span>

* [<span data-ttu-id="f0449-131">Panoramica di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="f0449-131">Azure Resource Manager overview</span></span>](../../azure-resource-manager/resource-group-overview.md)
* [<span data-ttu-id="f0449-132">Che cos'è un gruppo di sicurezza di rete</span><span class="sxs-lookup"><span data-stu-id="f0449-132">What is a Network Security Group (NSG)?</span></span>](../../virtual-network/virtual-networks-nsg.md)
