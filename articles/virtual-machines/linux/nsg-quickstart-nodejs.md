---
title: Aprire le porte per una VM Linux con l'interfaccia della riga di comando di Azure 1.0 | Documentazione Microsoft
description: Informazioni su come aprire una porta o creare un endpoint per la VM Linux tramite il modello di distribuzione Azure Resource Manager e l'interfaccia della riga di comando di Azure versione 1.0
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 847bc76c37ed929851712ba1c12463a01032e267
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="opening-ports-and-endpoints-to-a-linux-vm-in-azure-using-the-azure-cli-10"></a><span data-ttu-id="6f23a-103">Apertura di porte ed endpoint per una VM Linux in Azure con l'interfaccia della riga di comando di Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="6f23a-103">Opening ports and endpoints to a Linux VM in Azure using the Azure CLI 1.0</span></span>
<span data-ttu-id="6f23a-104">Aprire una porta o creare un endpoint in una macchina virtuale (VM) di Azure tramite la creazione di un filtro di rete su una subnet o un'interfaccia di rete di VM.</span><span class="sxs-lookup"><span data-stu-id="6f23a-104">You open a port, or create an endpoint, to a virtual machine (VM) in Azure by creating a network filter on a subnet or VM network interface.</span></span> <span data-ttu-id="6f23a-105">Questi filtri, che consentono di controllare il traffico in ingresso e in uscita, vengono inseriti in un gruppo di sicurezza di rete e collegati alla risorsa che riceve il traffico.</span><span class="sxs-lookup"><span data-stu-id="6f23a-105">You place these filters, which control both inbound and outbound traffic, on a Network Security Group attached to the resource that receives the traffic.</span></span> <span data-ttu-id="6f23a-106">Si userà un esempio comune di traffico Web sulla porta 80.</span><span class="sxs-lookup"><span data-stu-id="6f23a-106">Let's use a common example of web traffic on port 80.</span></span> <span data-ttu-id="6f23a-107">Questo articolo illustra come aprire una porta in una VM usando l'interfaccia della riga di comando di Azure versione 1.0.</span><span class="sxs-lookup"><span data-stu-id="6f23a-107">This article shows you how to open a port to a VM using the Azure CLI 1.0.</span></span>


## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="6f23a-108">Versioni dell'interfaccia della riga di comando per completare l'attività</span><span class="sxs-lookup"><span data-stu-id="6f23a-108">CLI versions to complete the task</span></span>
<span data-ttu-id="6f23a-109">È possibile completare l'attività usando una delle versioni seguenti dell'interfaccia della riga di comando:</span><span class="sxs-lookup"><span data-stu-id="6f23a-109">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="6f23a-110">[Interfaccia della riga di comando di Azure 1.0](#quick-commands): l'interfaccia della riga di comando per i modelli di distribuzione classica e di gestione delle risorse (questo articolo)</span><span class="sxs-lookup"><span data-stu-id="6f23a-110">[Azure CLI 1.0](#quick-commands) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="6f23a-111">[Interfaccia della riga di comando di Azure 2.0](nsg-quickstart.md): interfaccia della riga di comando di prossima generazione per il modello di distribuzione di Gestione risorsa</span><span class="sxs-lookup"><span data-stu-id="6f23a-111">[Azure CLI 2.0](nsg-quickstart.md) - our next generation CLI for the resource management deployment model</span></span>


## <a name="quick-commands"></a><span data-ttu-id="6f23a-112">Comandi rapidi</span><span class="sxs-lookup"><span data-stu-id="6f23a-112">Quick commands</span></span>
<span data-ttu-id="6f23a-113">Per creare un gruppo di sicurezza di rete e le regole, è necessario che sia installata e usata l'[interfaccia della riga di comando di Azure](../../cli-install-nodejs.md) versione 1.0 in modalità Resource Manager:</span><span class="sxs-lookup"><span data-stu-id="6f23a-113">To create a Network Security Group and rules you need [the Azure CLI 1.0](../../cli-install-nodejs.md) installed and using Resource Manager mode:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="6f23a-114">Nell'esempio seguente sostituire i nomi dei parametri di esempio con i valori desiderati.</span><span class="sxs-lookup"><span data-stu-id="6f23a-114">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="6f23a-115">I nomi dei parametri di esempio includono *myResourceGroup*, *myNetworkSecurityGroup* e *myVnet*.</span><span class="sxs-lookup"><span data-stu-id="6f23a-115">Example parameter names included *myResourceGroup*, *myNetworkSecurityGroup*, and *myVnet*.</span></span>

<span data-ttu-id="6f23a-116">Creare il gruppo di sicurezza di rete immettendo nomi e percorso in modo appropriato.</span><span class="sxs-lookup"><span data-stu-id="6f23a-116">Create your Network Security Group, entering your own names and location appropriately.</span></span> <span data-ttu-id="6f23a-117">L'esempio seguente crea un gruppo di sicurezza di rete denominato *myNetworkSecurityGroup* nella posizione *eastus*:</span><span class="sxs-lookup"><span data-stu-id="6f23a-117">The following example creates a Network Security Group named *myNetworkSecurityGroup* in the *eastus* location:</span></span>

```azurecli
azure network nsg create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNetworkSecurityGroup
```

<span data-ttu-id="6f23a-118">Aggiungere una regola per consentire il traffico HTTP al server Web o regolare per scenario in uso, come l'accesso SSH o la connettività al database.</span><span class="sxs-lookup"><span data-stu-id="6f23a-118">Add a rule to allow HTTP traffic to your webserver (or adjust for your own scenario, such as SSH access or database connectivity).</span></span> <span data-ttu-id="6f23a-119">L'esempio seguente crea una regola denominata *myNetworkSecurityGroupRule* per consentire il traffico TCP sulla porta 80:</span><span class="sxs-lookup"><span data-stu-id="6f23a-119">The following example creates a rule named *myNetworkSecurityGroupRule* to allow TCP traffic on port 80:</span></span>

```azurecli
azure network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRule \
    --protocol tcp \
    --direction inbound \
    --priority 1000 \
    --destination-port-range 80 \
    --access allow
```

<span data-ttu-id="6f23a-120">Associare il gruppo di sicurezza di rete con l'interfaccia di rete (NIC) della VM.</span><span class="sxs-lookup"><span data-stu-id="6f23a-120">Associate the Network Security Group with your VM's network interface (NIC).</span></span> <span data-ttu-id="6f23a-121">L'esempio seguente associa una scheda di interfaccia di rete esistente denominata *myNic* al gruppo di sicurezza di rete denominato *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="6f23a-121">The following example associates an existing NIC named *myNic* with the Network Security Group named *myNetworkSecurityGroup*:</span></span>

```azurecli
azure network nic set \
    --resource-group myResourceGroup \
    --network-security-group-name myNetworkSecurityGroup \
    --name myNic
```

<span data-ttu-id="6f23a-122">In alternativa, è possibile associare il gruppo di sicurezza di rete con una subnet di rete virtuale invece della sola interfaccia di rete in una singola VM.</span><span class="sxs-lookup"><span data-stu-id="6f23a-122">Alternatively, you can associate your Network Security Group with a virtual network subnet rather than just to the network interface on a single VM.</span></span> <span data-ttu-id="6f23a-123">L'esempio seguente associa una subnet esistente denominata *mySubnet* nella rete virtuale *myVnet* al gruppo di sicurezza di rete denominato *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="6f23a-123">The following example associates an existing subnet named *mySubnet* in the *myVnet* virtual network with the Network Security Group named *myNetworkSecurityGroup*:</span></span>

```azurecli
azure network vnet subnet set \
    --resource-group myResourceGroup \
    --network-security-group-name myNetworkSecurityGroup \
    --vnet-name myVnet --name mySubnet
```

## <a name="more-information-on-network-security-groups"></a><span data-ttu-id="6f23a-124">Altre informazioni sui gruppi di sicurezza di rete</span><span class="sxs-lookup"><span data-stu-id="6f23a-124">More information on Network Security Groups</span></span>
<span data-ttu-id="6f23a-125">I comandi rapidi seguenti consentono di rendere operativo il traffico verso la VM.</span><span class="sxs-lookup"><span data-stu-id="6f23a-125">The quick commands here allow you to get up and running with traffic flowing to your VM.</span></span> <span data-ttu-id="6f23a-126">I gruppi di sicurezza di rete offrono numerose funzionalità efficienti e la necessaria granularità per controllare l'accesso alle risorse.</span><span class="sxs-lookup"><span data-stu-id="6f23a-126">Network Security Groups provide many great features and granularity for controlling access to your resources.</span></span> <span data-ttu-id="6f23a-127">Per altre informazioni, leggere l'articolo sulla [creazione di un gruppo di sicurezza di rete e di regole dell'elenco di controllo di accesso qui](../../virtual-network/virtual-networks-create-nsg-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="6f23a-127">You can read more about [creating a Network Security Group and ACL rules here](../../virtual-network/virtual-networks-create-nsg-arm-cli.md).</span></span>

<span data-ttu-id="6f23a-128">È possibile definire le regole dell'elenco di controllo di accesso e i gruppi di sicurezza di rete come parte dei modelli di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="6f23a-128">You can define Network Security Groups and ACL rules as part of Azure Resource Manager templates.</span></span> <span data-ttu-id="6f23a-129">Per altre informazioni, leggere l'articolo [Come creare NSG utilizzando un modello](../../virtual-network/virtual-networks-create-nsg-arm-template.md).</span><span class="sxs-lookup"><span data-stu-id="6f23a-129">Read more about [creating Network Security Groups with templates](../../virtual-network/virtual-networks-create-nsg-arm-template.md).</span></span>

<span data-ttu-id="6f23a-130">Se si deve usare il port forwarding per eseguire il mapping di una sola porta esterna verso una porta interna della VM, usare un servizio di bilanciamento del carico e le regole Network Address Translation (NAT).</span><span class="sxs-lookup"><span data-stu-id="6f23a-130">If you need to use port-forwarding to map a unique external port to an internal port on your VM, use a load balancer and Network Address Translation (NAT) rules.</span></span> <span data-ttu-id="6f23a-131">Ad esempio, si desidera esporre la porta TCP 8080 esternamente e che il traffico venga indirizzato sulla porta TCP 80 in una VM.</span><span class="sxs-lookup"><span data-stu-id="6f23a-131">For example, you may want to expose TCP port 8080 externally and have traffic directed to TCP port 80 on a VM.</span></span> <span data-ttu-id="6f23a-132">Per altre informazioni, leggere l'articolo relativo alla [creazione di un servizio di bilanciamento del carico per Internet](../../load-balancer/load-balancer-get-started-internet-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="6f23a-132">You can learn about [creating an Internet-facing load balancer](../../load-balancer/load-balancer-get-started-internet-arm-cli.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="6f23a-133">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6f23a-133">Next steps</span></span>
<span data-ttu-id="6f23a-134">In questo esempio viene creata una regola semplice per consentire il traffico HTTP.</span><span class="sxs-lookup"><span data-stu-id="6f23a-134">In this example, you created a simple rule to allow HTTP traffic.</span></span> <span data-ttu-id="6f23a-135">È possibile trovare informazioni sulla creazione di ambienti più dettagliati negli articoli seguenti:</span><span class="sxs-lookup"><span data-stu-id="6f23a-135">You can find information on creating more detailed environments in the following articles:</span></span>

* [<span data-ttu-id="6f23a-136">Panoramica di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="6f23a-136">Azure Resource Manager overview</span></span>](../../azure-resource-manager/resource-group-overview.md)
* [<span data-ttu-id="6f23a-137">Che cos'è un gruppo di sicurezza di rete</span><span class="sxs-lookup"><span data-stu-id="6f23a-137">What is a Network Security Group (NSG)?</span></span>](../../virtual-network/virtual-networks-nsg.md)
* [<span data-ttu-id="6f23a-138">Panoramica di Azure Resource Manager per i servizi di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="6f23a-138">Azure Resource Manager Overview for Load Balancers</span></span>](../../load-balancer/load-balancer-arm.md)

