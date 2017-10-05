---
title: Aprire le porte per una VM Linux con l'interfaccia della riga di comando di Azure 2.0 | Documentazione Microsoft
description: Informazioni su come aprire una porta o creare un endpoint per la VM Linux tramite il modello di distribuzione Azure Resource Manager e l'interfaccia della riga di comando di Azure 2.0
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
ms.openlocfilehash: d176187fe465264b5f433260de5178b48ca9dd4a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="open-ports-and-endpoints-to-a-linux-vm-with-the-azure-cli"></a><span data-ttu-id="4274f-103">Aprire porte ed endpoint per una VM Linux con l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="4274f-103">Open ports and endpoints to a Linux VM with the Azure CLI</span></span>
<span data-ttu-id="4274f-104">Aprire una porta o creare un endpoint in una macchina virtuale (VM) di Azure tramite la creazione di un filtro di rete su una subnet o un'interfaccia di rete di VM.</span><span class="sxs-lookup"><span data-stu-id="4274f-104">You open a port, or create an endpoint, to a virtual machine (VM) in Azure by creating a network filter on a subnet or VM network interface.</span></span> <span data-ttu-id="4274f-105">Questi filtri, che consentono di controllare il traffico in ingresso e in uscita, vengono inseriti in un gruppo di sicurezza di rete e collegati alla risorsa che riceve il traffico.</span><span class="sxs-lookup"><span data-stu-id="4274f-105">You place these filters, which control both inbound and outbound traffic, on a Network Security Group attached to the resource that receives the traffic.</span></span> <span data-ttu-id="4274f-106">Si userà un esempio comune di traffico Web sulla porta 80.</span><span class="sxs-lookup"><span data-stu-id="4274f-106">Let's use a common example of web traffic on port 80.</span></span> <span data-ttu-id="4274f-107">Questo articolo illustra come aprire una porta in una VM con l'interfaccia della riga di comando di Azure 2.0.</span><span class="sxs-lookup"><span data-stu-id="4274f-107">This article shows you how to open a port to a VM with the Azure CLI 2.0.</span></span> <span data-ttu-id="4274f-108">È possibile anche eseguire questi passaggi tramite l'[interfaccia della riga di comando di Azure 1.0](nsg-quickstart-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="4274f-108">You can also perform these steps with the [Azure CLI 1.0](nsg-quickstart-nodejs.md).</span></span>


## <a name="quick-commands"></a><span data-ttu-id="4274f-109">Comandi rapidi</span><span class="sxs-lookup"><span data-stu-id="4274f-109">Quick commands</span></span>
<span data-ttu-id="4274f-110">Per creare un gruppo di sicurezza di rete e le regole è necessario aver installato la versione più recente dell'[interfaccia della riga di comando di Azure 2.0](/cli/azure/install-az-cli2) e aver eseguito l'accesso a un account Azure usando [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="4274f-110">To create a Network Security Group and rules you need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="4274f-111">Nell'esempio seguente sostituire i nomi dei parametri di esempio con i valori desiderati.</span><span class="sxs-lookup"><span data-stu-id="4274f-111">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="4274f-112">I nomi dei parametri di esempio includono *myResourceGroup*, *myNetworkSecurityGroup* e *myVnet*.</span><span class="sxs-lookup"><span data-stu-id="4274f-112">Example parameter names include *myResourceGroup*, *myNetworkSecurityGroup*, and *myVnet*.</span></span>

<span data-ttu-id="4274f-113">Creare il gruppo di sicurezza di rete con [az network nsg create](/cli/azure/network/nsg#create).</span><span class="sxs-lookup"><span data-stu-id="4274f-113">Create the network security group with [az network nsg create](/cli/azure/network/nsg#create).</span></span> <span data-ttu-id="4274f-114">L'esempio seguente crea un gruppo di sicurezza di rete denominato *myNetworkSecurityGroup* nella posizione *eastus*:</span><span class="sxs-lookup"><span data-stu-id="4274f-114">The following example creates a network security group named *myNetworkSecurityGroup* in the *eastus* location:</span></span>

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNetworkSecurityGroup
```

<span data-ttu-id="4274f-115">Aggiungere una regola con [az network nsg rule create](/cli/azure/network/nsg/rule#create) per consentire il traffico HTTP al server Web (o in base allo scenario specifico, come l'accesso SSH o la connettività al database).</span><span class="sxs-lookup"><span data-stu-id="4274f-115">Add a rule with [az network nsg rule create](/cli/azure/network/nsg/rule#create) to allow HTTP traffic to your webserver (or adjust for your own scenario, such as SSH access or database connectivity).</span></span> <span data-ttu-id="4274f-116">L'esempio seguente crea una regola denominata *myNetworkSecurityGroupRule* per consentire il traffico TCP sulla porta 80:</span><span class="sxs-lookup"><span data-stu-id="4274f-116">The following example creates a rule named *myNetworkSecurityGroupRule* to allow TCP traffic on port 80:</span></span>

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRule \
    --protocol tcp \
    --priority 1000 \
    --destination-port-range 80
```

<span data-ttu-id="4274f-117">Associare il gruppo di sicurezza di rete all'interfaccia di rete della VM (NIC) utilizzando [az network nic update](/cli/azure/network/nic#update).</span><span class="sxs-lookup"><span data-stu-id="4274f-117">Associate the Network Security Group with your VM's network interface (NIC) with [az network nic update](/cli/azure/network/nic#update).</span></span> <span data-ttu-id="4274f-118">L'esempio seguente associa una scheda di interfaccia di rete esistente denominata *myNic* al gruppo di sicurezza di rete denominato *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="4274f-118">The following example associates an existing NIC named *myNic* with the Network Security Group named *myNetworkSecurityGroup*:</span></span>

```azurecli
az network nic update \
    --resource-group myResourceGroup \
    --name myNic \
    --network-security-group myNetworkSecurityGroup
```

<span data-ttu-id="4274f-119">In alternativa, è possibile associare il gruppo di sicurezza di rete a una subnet di rete virtuale utilizzando [az network vnet subnet update](/cli/azure/network/vnet/subnet#update) anziché solo all'interfaccia di rete di una singola VM.</span><span class="sxs-lookup"><span data-stu-id="4274f-119">Alternatively, you can associate your Network Security Group with a virtual network subnet with [az network vnet subnet update](/cli/azure/network/vnet/subnet#update) rather than just to the network interface on a single VM.</span></span> <span data-ttu-id="4274f-120">L'esempio seguente associa una subnet esistente denominata *mySubnet* nella rete virtuale *myVnet* al gruppo di sicurezza di rete denominato *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="4274f-120">The following example associates an existing subnet named *mySubnet* in the *myVnet* virtual network with the Network Security Group named *myNetworkSecurityGroup*:</span></span>

```azurecli
az network vnet subnet update \
    --resource-group myResourceGroup \
    --vnet-name myVnet \
    --name mySubnet \
    --network-security-group myNetworkSecurityGroup
```

## <a name="more-information-on-network-security-groups"></a><span data-ttu-id="4274f-121">Altre informazioni sui gruppi di sicurezza di rete</span><span class="sxs-lookup"><span data-stu-id="4274f-121">More information on Network Security Groups</span></span>
<span data-ttu-id="4274f-122">I comandi rapidi seguenti consentono di rendere operativo il traffico verso la VM.</span><span class="sxs-lookup"><span data-stu-id="4274f-122">The quick commands here allow you to get up and running with traffic flowing to your VM.</span></span> <span data-ttu-id="4274f-123">I gruppi di sicurezza di rete offrono numerose funzionalità efficienti e la necessaria granularità per controllare l'accesso alle risorse.</span><span class="sxs-lookup"><span data-stu-id="4274f-123">Network Security Groups provide many great features and granularity for controlling access to your resources.</span></span> <span data-ttu-id="4274f-124">Per altre informazioni, leggere l'articolo sulla [creazione di un gruppo di sicurezza di rete e di regole dell'elenco di controllo di accesso qui](tutorial-virtual-network.md#secure-network-traffic).</span><span class="sxs-lookup"><span data-stu-id="4274f-124">You can read more about [creating a Network Security Group and ACL rules here](tutorial-virtual-network.md#secure-network-traffic).</span></span>

<span data-ttu-id="4274f-125">Per le applicazioni Web a disponibilità elevata, è consigliabile inserire le macchine virtuali dietro a un Azure Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="4274f-125">For highly available web applications, you should place your VMs behind an Azure Load Balancer.</span></span> <span data-ttu-id="4274f-126">Il bilanciamento del carico distribuisce il traffico alle macchine virtuali, con un gruppo di sicurezza di rete che consente di filtrare il traffico.</span><span class="sxs-lookup"><span data-stu-id="4274f-126">The load balancer distributes traffic to VMs, with a Network Security Group that provides traffic filtering.</span></span> <span data-ttu-id="4274f-127">Per altre informazioni, vedere [Come bilanciare il carico per le macchine virtuali di Linux in Azure per creare un'applicazione a disponibilità elevata](tutorial-load-balancer.md).</span><span class="sxs-lookup"><span data-stu-id="4274f-127">For more information, see [How to load balance Linux virtual machines in Azure to create a highly available application](tutorial-load-balancer.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="4274f-128">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4274f-128">Next steps</span></span>
<span data-ttu-id="4274f-129">In questo esempio viene creata una regola semplice per consentire il traffico HTTP.</span><span class="sxs-lookup"><span data-stu-id="4274f-129">In this example, you created a simple rule to allow HTTP traffic.</span></span> <span data-ttu-id="4274f-130">È possibile trovare informazioni sulla creazione di ambienti più dettagliati negli articoli seguenti:</span><span class="sxs-lookup"><span data-stu-id="4274f-130">You can find information on creating more detailed environments in the following articles:</span></span>

* [<span data-ttu-id="4274f-131">Panoramica di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="4274f-131">Azure Resource Manager overview</span></span>](../../azure-resource-manager/resource-group-overview.md)
* [<span data-ttu-id="4274f-132">Che cos'è un gruppo di sicurezza di rete</span><span class="sxs-lookup"><span data-stu-id="4274f-132">What is a Network Security Group (NSG)?</span></span>](../../virtual-network/virtual-networks-nsg.md)
