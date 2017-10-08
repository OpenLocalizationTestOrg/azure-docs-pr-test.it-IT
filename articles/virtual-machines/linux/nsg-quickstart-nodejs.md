---
title: aaaOpen porte tooa VM Linux con 1.0 CLI di Azure | Documenti Microsoft
description: Informazioni su come tooopen una porta / creare una VM Linux di tooyour endpoint utilizzando la distribuzione di gestione risorse di Azure hello del modello e hello Azure CLI 1.0
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
ms.openlocfilehash: 337c37d151f527b43d4852291159b2f70a00accc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="opening-ports-and-endpoints-tooa-linux-vm-in-azure-using-hello-azure-cli-10"></a><span data-ttu-id="7b223-103">Apertura porte ed endpoint tooa VM Linux in Azure tramite hello Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="7b223-103">Opening ports and endpoints tooa Linux VM in Azure using hello Azure CLI 1.0</span></span>
<span data-ttu-id="7b223-104">Aprire una porta o creare un endpoint, tooa macchina virtuale (VM) in Azure tramite la creazione di un filtro di rete su una subnet o l'interfaccia di rete VM.</span><span class="sxs-lookup"><span data-stu-id="7b223-104">You open a port, or create an endpoint, tooa virtual machine (VM) in Azure by creating a network filter on a subnet or VM network interface.</span></span> <span data-ttu-id="7b223-105">Questi filtri, che consentono di controllare il traffico in ingresso e in uscita, posizionare in una risorsa toohello gruppo di sicurezza di rete associata che riceve il traffico di hello.</span><span class="sxs-lookup"><span data-stu-id="7b223-105">You place these filters, which control both inbound and outbound traffic, on a Network Security Group attached toohello resource that receives hello traffic.</span></span> <span data-ttu-id="7b223-106">Si userà un esempio comune di traffico Web sulla porta 80.</span><span class="sxs-lookup"><span data-stu-id="7b223-106">Let's use a common example of web traffic on port 80.</span></span> <span data-ttu-id="7b223-107">In questo articolo viene illustrato come una porta tooa VM utilizzando tooopen hello Azure CLI 1.0.</span><span class="sxs-lookup"><span data-stu-id="7b223-107">This article shows you how tooopen a port tooa VM using hello Azure CLI 1.0.</span></span>


## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="7b223-108">Attività hello toocomplete versioni CLI</span><span class="sxs-lookup"><span data-stu-id="7b223-108">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="7b223-109">È possibile completare l'attività hello utilizzando una delle seguenti versioni CLI hello:</span><span class="sxs-lookup"><span data-stu-id="7b223-109">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="7b223-110">[Azure CLI 1.0](#quick-commands) : l'interfaccia CLI per hello classic risorse Gestione modelli di distribuzione e (in questo articolo)</span><span class="sxs-lookup"><span data-stu-id="7b223-110">[Azure CLI 1.0](#quick-commands) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="7b223-111">[Azure CLI 2.0](nsg-quickstart.md) -la prossima generazione CLI per modello di distribuzione di gestione risorse hello</span><span class="sxs-lookup"><span data-stu-id="7b223-111">[Azure CLI 2.0](nsg-quickstart.md) - our next generation CLI for hello resource management deployment model</span></span>


## <a name="quick-commands"></a><span data-ttu-id="7b223-112">Comandi rapidi</span><span class="sxs-lookup"><span data-stu-id="7b223-112">Quick commands</span></span>
<span data-ttu-id="7b223-113">toocreate un gruppo di sicurezza di rete e le regole è necessario [hello Azure CLI 1.0](../../cli-install-nodejs.md) installati e utilizzando la modalità di gestione risorse:</span><span class="sxs-lookup"><span data-stu-id="7b223-113">toocreate a Network Security Group and rules you need [hello Azure CLI 1.0](../../cli-install-nodejs.md) installed and using Resource Manager mode:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="7b223-114">In hello negli esempi seguenti, sostituire i nomi dei parametri di esempio con i valori desiderati.</span><span class="sxs-lookup"><span data-stu-id="7b223-114">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="7b223-115">I nomi dei parametri di esempio includono *myResourceGroup*, *myNetworkSecurityGroup* e *myVnet*.</span><span class="sxs-lookup"><span data-stu-id="7b223-115">Example parameter names included *myResourceGroup*, *myNetworkSecurityGroup*, and *myVnet*.</span></span>

<span data-ttu-id="7b223-116">Creare il gruppo di sicurezza di rete immettendo nomi e percorso in modo appropriato.</span><span class="sxs-lookup"><span data-stu-id="7b223-116">Create your Network Security Group, entering your own names and location appropriately.</span></span> <span data-ttu-id="7b223-117">esempio Hello crea un gruppo di sicurezza di rete denominata *myNetworkSecurityGroup* in hello *eastus* percorso:</span><span class="sxs-lookup"><span data-stu-id="7b223-117">hello following example creates a Network Security Group named *myNetworkSecurityGroup* in hello *eastus* location:</span></span>

```azurecli
azure network nsg create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNetworkSecurityGroup
```

<span data-ttu-id="7b223-118">Aggiungere un server Web tooyour di traffico HTTP tooallow regola (o modificare per proprio scenario, ad esempio la connettività di accesso o database SSH).</span><span class="sxs-lookup"><span data-stu-id="7b223-118">Add a rule tooallow HTTP traffic tooyour webserver (or adjust for your own scenario, such as SSH access or database connectivity).</span></span> <span data-ttu-id="7b223-119">esempio Hello crea una regola denominata *myNetworkSecurityGroupRule* tooallow TCP il traffico sulla porta 80:</span><span class="sxs-lookup"><span data-stu-id="7b223-119">hello following example creates a rule named *myNetworkSecurityGroupRule* tooallow TCP traffic on port 80:</span></span>

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

<span data-ttu-id="7b223-120">Associare l'interfaccia di rete della macchina virtuale (NIC) hello il gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="7b223-120">Associate hello Network Security Group with your VM's network interface (NIC).</span></span> <span data-ttu-id="7b223-121">esempio Hello associa una scheda di rete esistente denominato *myNic* con il gruppo di sicurezza di rete denominata hello *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="7b223-121">hello following example associates an existing NIC named *myNic* with hello Network Security Group named *myNetworkSecurityGroup*:</span></span>

```azurecli
azure network nic set \
    --resource-group myResourceGroup \
    --network-security-group-name myNetworkSecurityGroup \
    --name myNic
```

<span data-ttu-id="7b223-122">In alternativa, è possibile associare il gruppo di sicurezza di rete con una subnet della rete virtuale anziché semplicemente toohello interfaccia di rete in una singola macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="7b223-122">Alternatively, you can associate your Network Security Group with a virtual network subnet rather than just toohello network interface on a single VM.</span></span> <span data-ttu-id="7b223-123">esempio Hello associa una subnet esistente denominata *mySubnet* in hello *myVnet* rete virtuale con il gruppo di sicurezza di rete denominata hello *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="7b223-123">hello following example associates an existing subnet named *mySubnet* in hello *myVnet* virtual network with hello Network Security Group named *myNetworkSecurityGroup*:</span></span>

```azurecli
azure network vnet subnet set \
    --resource-group myResourceGroup \
    --network-security-group-name myNetworkSecurityGroup \
    --vnet-name myVnet --name mySubnet
```

## <a name="more-information-on-network-security-groups"></a><span data-ttu-id="7b223-124">Altre informazioni sui gruppi di sicurezza di rete</span><span class="sxs-lookup"><span data-stu-id="7b223-124">More information on Network Security Groups</span></span>
<span data-ttu-id="7b223-125">Hello rapido comandi consentono di tooget backup e in esecuzione con traffico propagazione tooyour macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="7b223-125">hello quick commands here allow you tooget up and running with traffic flowing tooyour VM.</span></span> <span data-ttu-id="7b223-126">Gruppi di sicurezza di rete forniscono numerose funzionalità eccellenti e granularità per il controllo tooyour di accedere alle risorse.</span><span class="sxs-lookup"><span data-stu-id="7b223-126">Network Security Groups provide many great features and granularity for controlling access tooyour resources.</span></span> <span data-ttu-id="7b223-127">Per altre informazioni, leggere l'articolo sulla [creazione di un gruppo di sicurezza di rete e di regole dell'elenco di controllo di accesso qui](../../virtual-network/virtual-networks-create-nsg-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="7b223-127">You can read more about [creating a Network Security Group and ACL rules here](../../virtual-network/virtual-networks-create-nsg-arm-cli.md).</span></span>

<span data-ttu-id="7b223-128">È possibile definire le regole dell'elenco di controllo di accesso e i gruppi di sicurezza di rete come parte dei modelli di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="7b223-128">You can define Network Security Groups and ACL rules as part of Azure Resource Manager templates.</span></span> <span data-ttu-id="7b223-129">Per altre informazioni, leggere l'articolo [Come creare NSG utilizzando un modello](../../virtual-network/virtual-networks-create-nsg-arm-template.md).</span><span class="sxs-lookup"><span data-stu-id="7b223-129">Read more about [creating Network Security Groups with templates](../../virtual-network/virtual-networks-create-nsg-arm-template.md).</span></span>

<span data-ttu-id="7b223-130">Se è necessario toouse il port forwarding toomap una porta interna tooan di porta esterna univoco nella VM, utilizzare un servizio di bilanciamento del carico e le regole Network Address Translation (NAT).</span><span class="sxs-lookup"><span data-stu-id="7b223-130">If you need toouse port-forwarding toomap a unique external port tooan internal port on your VM, use a load balancer and Network Address Translation (NAT) rules.</span></span> <span data-ttu-id="7b223-131">Ad esempio, è possibile desidera tooexpose la porta TCP 8080 esternamente e il traffico diretto tooTCP porta 80 in una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="7b223-131">For example, you may want tooexpose TCP port 8080 externally and have traffic directed tooTCP port 80 on a VM.</span></span> <span data-ttu-id="7b223-132">Per altre informazioni, leggere l'articolo relativo alla [creazione di un servizio di bilanciamento del carico per Internet](../../load-balancer/load-balancer-get-started-internet-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="7b223-132">You can learn about [creating an Internet-facing load balancer](../../load-balancer/load-balancer-get-started-internet-arm-cli.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="7b223-133">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7b223-133">Next steps</span></span>
<span data-ttu-id="7b223-134">In questo esempio è stato creato il traffico HTTP tooallow una semplice regola.</span><span class="sxs-lookup"><span data-stu-id="7b223-134">In this example, you created a simple rule tooallow HTTP traffic.</span></span> <span data-ttu-id="7b223-135">È possibile trovare informazioni sulla creazione di ambienti più dettagliati in hello seguenti articoli:</span><span class="sxs-lookup"><span data-stu-id="7b223-135">You can find information on creating more detailed environments in hello following articles:</span></span>

* [<span data-ttu-id="7b223-136">Panoramica di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="7b223-136">Azure Resource Manager overview</span></span>](../../azure-resource-manager/resource-group-overview.md)
* [<span data-ttu-id="7b223-137">Che cos'è un gruppo di sicurezza di rete</span><span class="sxs-lookup"><span data-stu-id="7b223-137">What is a Network Security Group (NSG)?</span></span>](../../virtual-network/virtual-networks-nsg.md)
* [<span data-ttu-id="7b223-138">Panoramica di Azure Resource Manager per i servizi di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="7b223-138">Azure Resource Manager Overview for Load Balancers</span></span>](../../load-balancer/load-balancer-arm.md)

