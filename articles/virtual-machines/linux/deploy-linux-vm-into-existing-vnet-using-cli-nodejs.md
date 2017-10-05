---
title: Distribuire macchine virtuali Linux in una rete esistente con l'interfaccia della riga di comando Azure 1.0 | Microsoft Docs
description: Come distribuire una macchina virtuale Linux in una rete virtuale esistente usando l'interfaccia della riga di comando di Azure 1.0
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 767a3f7cadba6b1e71e5a8f5995a9db090e419dd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-deploy-a-linux-virtual-machine-into-an-existing-azure-virtual-network-with-the-azure-cli-10"></a><span data-ttu-id="e17dd-103">Come distribuire una macchina virtuale Linux in una rete virtuale Azure esistente con l'interfaccia della riga di comando di Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="e17dd-103">How to deploy a Linux virtual machine into an existing Azure Virtual Network with the Azure CLI 1.0</span></span>

<span data-ttu-id="e17dd-104">Questo articolo illustra come usare l'interfaccia della riga di comando di Azure 1.0 per distribuire una macchina virtuale in una rete virtuale esistente.</span><span class="sxs-lookup"><span data-stu-id="e17dd-104">This article shows you how to use Azure CLI 1.0 to deploy a virtual machine (VM) into an existing Virtual Network (VNet).</span></span> <span data-ttu-id="e17dd-105">I requisiti sono:</span><span class="sxs-lookup"><span data-stu-id="e17dd-105">The requirements are:</span></span>

- [<span data-ttu-id="e17dd-106">Un account di Azure</span><span class="sxs-lookup"><span data-stu-id="e17dd-106">an Azure account</span></span>](https://azure.microsoft.com/pricing/free-trial/)
- [<span data-ttu-id="e17dd-107">File di chiavi SSH pubbliche e private</span><span class="sxs-lookup"><span data-stu-id="e17dd-107">SSH public and private key files</span></span>](mac-create-ssh-keys.md)


## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="e17dd-108">Versioni dell'interfaccia della riga di comando per completare l'attività</span><span class="sxs-lookup"><span data-stu-id="e17dd-108">CLI versions to complete the task</span></span>
<span data-ttu-id="e17dd-109">È possibile completare l'attività usando una delle versioni seguenti dell'interfaccia della riga di comando:</span><span class="sxs-lookup"><span data-stu-id="e17dd-109">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="e17dd-110">[Interfaccia della riga di comando di Azure 1.0](#quick-commands): l'interfaccia della riga di comando per i modelli di distribuzione classica e di gestione delle risorse (questo articolo)</span><span class="sxs-lookup"><span data-stu-id="e17dd-110">[Azure CLI 1.0](#quick-commands) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="e17dd-111">[Interfaccia della riga di comando di Azure 2.0](deploy-linux-vm-into-existing-vnet-using-cli.md): interfaccia della riga di comando di prossima generazione per il modello di distribuzione di Gestione risorsa</span><span class="sxs-lookup"><span data-stu-id="e17dd-111">[Azure CLI 2.0](deploy-linux-vm-into-existing-vnet-using-cli.md) - our next generation CLI for the resource management deployment model</span></span>


## <a name="quick-commands"></a><span data-ttu-id="e17dd-112">Comandi rapidi</span><span class="sxs-lookup"><span data-stu-id="e17dd-112">Quick Commands</span></span>

<span data-ttu-id="e17dd-113">Se si vuole eseguire rapidamente l'attività, la sezione seguente indica dettagliatamente i comandi necessari.</span><span class="sxs-lookup"><span data-stu-id="e17dd-113">If you need to quickly accomplish the task, the following section details the commands needed.</span></span> <span data-ttu-id="e17dd-114">Altre informazioni dettagliate e il contesto per ogni passaggio sono disponibili nelle sezioni successive del documento, [a partire da qui](deploy-linux-vm-into-existing-vnet-using-cli.md#detailed-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="e17dd-114">More detailed information and context for each step can be found the rest of the document, [starting here](deploy-linux-vm-into-existing-vnet-using-cli.md#detailed-walkthrough).</span></span>

<span data-ttu-id="e17dd-115">Prerequisiti: gruppo di risorse, rete virtuale, gruppo di sicurezza di rete con SSH in ingresso, subnet.</span><span class="sxs-lookup"><span data-stu-id="e17dd-115">Pre-requirements: Resource Group, VNet, NSG with SSH inbound, Subnet.</span></span> <span data-ttu-id="e17dd-116">Sostituire gli esempi con le impostazioni desiderate.</span><span class="sxs-lookup"><span data-stu-id="e17dd-116">Replace any examples with your own settings.</span></span>

### <a name="deploy-the-vm-into-the-virtual-network-infrastructure"></a><span data-ttu-id="e17dd-117">Distribuire la macchina virtuale nell'infrastruttura di rete virtuale</span><span class="sxs-lookup"><span data-stu-id="e17dd-117">Deploy the VM into the virtual network infrastructure</span></span>

```azurecli
azure vm create myVM \
    -g myResourceGroup \
    -l eastus \
    -y linux \
    -Q Debian \
    -o mystorageaccount \
    -u myAdminUser \
    -M ~/.ssh/id_rsa.pub \
    -n myVM \
    -F myVNet \
    -j mySubnet \
    -N myVNic
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="e17dd-118">Procedura dettagliata</span><span class="sxs-lookup"><span data-stu-id="e17dd-118">Detailed walkthrough</span></span>

<span data-ttu-id="e17dd-119">Gli asset di Azure, come le reti virtuali e i gruppi di sicurezza di rete devono essere risorse statiche, ovvero di lunga durata e distribuite raramente.</span><span class="sxs-lookup"><span data-stu-id="e17dd-119">Azure assets like the VNets and network security groups should be static and long lived resources that are rarely deployed.</span></span> <span data-ttu-id="e17dd-120">Dopo essere stata distribuita, una rete virtuale può essere usata in nuove distribuzioni senza alcun effetto negativo sull'infrastruttura.</span><span class="sxs-lookup"><span data-stu-id="e17dd-120">Once a VNet has been deployed, it can be reused by new deployments without any adverse affects to the infrastructure.</span></span> <span data-ttu-id="e17dd-121">Si pensi a una rete virtuale come se fosse uno switch di rete hardware tradizionale.</span><span class="sxs-lookup"><span data-stu-id="e17dd-121">Think about a VNet as being a traditional hardware network switch.</span></span> <span data-ttu-id="e17dd-122">Non è necessario configurare un nuovo switch hardware a ogni distribuzione.</span><span class="sxs-lookup"><span data-stu-id="e17dd-122">You would not need to configure a brand new hardware switch with each deployment.</span></span> <span data-ttu-id="e17dd-123">In una rete virtuale configurata in modo appropriato, è possibile continuare a distribuire nuovi server più volte, apportando solo le modifiche indispensabili durante il ciclo di vita della rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="e17dd-123">With a correctly configured VNet, you can continue to deploy new servers into that VNet over and over with few, if any, changes required over the life of the VNet.</span></span>

## <a name="create-the-resource-group"></a><span data-ttu-id="e17dd-124">Creare il gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="e17dd-124">Create the resource group</span></span>

<span data-ttu-id="e17dd-125">Prima creare un gruppo di risorse per organizzare tutti gli elementi che si creano durante questa procedura dettagliata.</span><span class="sxs-lookup"><span data-stu-id="e17dd-125">First, create a resource group to organize everything you create in this walkthrough.</span></span> <span data-ttu-id="e17dd-126">Per altre informazioni sui gruppi di risorse, vedere [Panoramica di Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md)</span><span class="sxs-lookup"><span data-stu-id="e17dd-126">For more information about resource groups, see [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md)</span></span>

```azurecli
azure group create myResourceGroup --location eastus
```

## <a name="create-the-vnet"></a><span data-ttu-id="e17dd-127">Creare la rete virtuale</span><span class="sxs-lookup"><span data-stu-id="e17dd-127">Create the VNet</span></span>

<span data-ttu-id="e17dd-128">Il primo passaggio consiste nella compilazione di una rete virtuale nella quale eseguire le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="e17dd-128">The first step is to build a VNet to launch the VMs into.</span></span> <span data-ttu-id="e17dd-129">Ai fini di questa procedura, la rete virtuale contiene una subnet.</span><span class="sxs-lookup"><span data-stu-id="e17dd-129">The VNet contains one subnet for this walkthrough.</span></span> <span data-ttu-id="e17dd-130">Per altre informazioni sulle reti virtuali di Azure, vedere [Creare una rete virtuale (classica) usando l'interfaccia della riga di comando di Azure](../../virtual-network/virtual-networks-create-vnet-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="e17dd-130">For more information on Azure VNets, see [Create a virtual network by using the Azure CLI](../../virtual-network/virtual-networks-create-vnet-arm-cli.md)</span></span>

```azurecli
azure network vnet create myVNet \
    --resource-group myResourceGroup \
    --address-prefixes 10.10.0.0/24 \
    --location eastus
```

## <a name="create-the-network-security-group"></a><span data-ttu-id="e17dd-131">Creare il gruppo di sicurezza di rete</span><span class="sxs-lookup"><span data-stu-id="e17dd-131">Create the network security group</span></span>

<span data-ttu-id="e17dd-132">La subnet è protetta da un gruppo di sicurezza di rete esistente, quindi creare il gruppo di sicurezza di rete prima della subnet.</span><span class="sxs-lookup"><span data-stu-id="e17dd-132">The subnet is built behind an existing network security group so build the network security group before the subnet.</span></span> <span data-ttu-id="e17dd-133">I gruppi di sicurezza di rete di Azure sono analoghi a un firewall a livello di rete.</span><span class="sxs-lookup"><span data-stu-id="e17dd-133">Azure network security groups are equivalent to a firewall at the network layer.</span></span> <span data-ttu-id="e17dd-134">Per altre informazioni sui gruppi di sicurezza di rete di Azure, vedere [Come creare gruppi di sicurezza di rete usando l'interfaccia della riga di comando di Azure](../../virtual-network/virtual-networks-create-nsg-arm-cli.md)</span><span class="sxs-lookup"><span data-stu-id="e17dd-134">For more information on Azure network security groups, see [How to create network security groups in the Azure CLI](../../virtual-network/virtual-networks-create-nsg-arm-cli.md)</span></span>

```azurecli
azure network nsg create myNetworkSecurityGroup \
    --resource-group myResourceGroup \
    --location eastus
```

## <a name="add-an-inbound-ssh-allow-rule"></a><span data-ttu-id="e17dd-135">Aggiungere una regola di assenso SSH in ingresso</span><span class="sxs-lookup"><span data-stu-id="e17dd-135">Add an inbound SSH allow rule</span></span>

<span data-ttu-id="e17dd-136">La macchina virtuale deve accedere da Internet, pertanto è necessaria una regola che consenta di lasciare entrare il traffico in ingresso verso la porta 22 della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="e17dd-136">The VM needs access from the internet so a rule allowing inbound port 22 traffic to be passed through the network to port 22 on the VM is needed.</span></span>

```azurecli
azure network nsg rule create inboundSSH \
    --resource-group myResourceGroup \
    --nsg-name myNSG \
    --access Allow \
    --protocol Tcp \
    --direction Inbound \
    --priority 100 \
    --source-address-prefix Internet \
    --source-port-range 22 \
    --destination-address-prefix 10.10.0.0/24 \
    --destination-port-range 22
```

## <a name="add-a-subnet-to-the-vnet"></a><span data-ttu-id="e17dd-137">Aggiungere una subnet alla rete virtuale</span><span class="sxs-lookup"><span data-stu-id="e17dd-137">Add a subnet to the VNet</span></span>

<span data-ttu-id="e17dd-138">Le macchine virtuali all'interno della rete virtuale devono trovarsi in una subnet.</span><span class="sxs-lookup"><span data-stu-id="e17dd-138">VMs within the VNet must be located in a subnet.</span></span> <span data-ttu-id="e17dd-139">Ogni rete virtuale può avere più subnet.</span><span class="sxs-lookup"><span data-stu-id="e17dd-139">Each VNet can have multiple subnets.</span></span> <span data-ttu-id="e17dd-140">Creare la subnet e associarla al gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="e17dd-140">Create the subnet and associate with the network security group.</span></span>

```azurecli
azure network vnet subnet create mySubNet \
    --resource-group myResourceGroup \
    --vnet-name myVNet \
    --address-prefix 10.10.0.0/26 \
    --network-security-group-name myNetworkSecurityGroup
```

<span data-ttu-id="e17dd-141">La subnet è ora aggiunta all'interno della rete virtuale e associata a un gruppo di sicurezza di rete e alla regola.</span><span class="sxs-lookup"><span data-stu-id="e17dd-141">The Subnet is now added inside the VNet and associated with the network security group and rule.</span></span>


## <a name="add-a-vnic-to-the-subnet"></a><span data-ttu-id="e17dd-142">Aggiungere una scheda di interfaccia di rete virtuale alla subnet</span><span class="sxs-lookup"><span data-stu-id="e17dd-142">Add a VNic to the subnet</span></span>

<span data-ttu-id="e17dd-143">Le schede di interfaccia rete virtuale sono importanti in quanto è possibile riusarle connettendole a macchine virtuali differenti.</span><span class="sxs-lookup"><span data-stu-id="e17dd-143">Virtual network cards (VNics) are important as you can reuse them by connecting them to different VMs.</span></span> <span data-ttu-id="e17dd-144">In questo modo la scheda di interfaccia di rete virtuale diventa una risorsa statica, mentre le macchine virtuali possono essere temporanee.</span><span class="sxs-lookup"><span data-stu-id="e17dd-144">This approach keeps the VNic as a static resource while the VMs can be temporary.</span></span> <span data-ttu-id="e17dd-145">Creare una scheda di interfaccia di rete virtuale e associarla alla subnet creata nel passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="e17dd-145">Create a VNic and associate it with the subnet created in the previous step.</span></span>

```azurecli
azure network nic create myVNic \
    --resource-group myResourceGroup \
    --location eastus \
    ---subnet-vnet-name myVNet \
    --subnet-name mySubNet
```

## <a name="deploy-the-vm-into-the-vnet-and-nsg"></a><span data-ttu-id="e17dd-146">Distribuire la macchina virtuale nella rete virtuale e nel gruppo di sicurezza di rete</span><span class="sxs-lookup"><span data-stu-id="e17dd-146">Deploy the VM into the VNet and NSG</span></span>

<span data-ttu-id="e17dd-147">A questo punto sono disponibili una rete virtuale, una subnet all'interno di tale rete virtuale e un gruppo di sicurezza di rete che protegge la subnet da tutto il traffico in ingresso tranne quello verso la porta 22 per SSH.</span><span class="sxs-lookup"><span data-stu-id="e17dd-147">You now have a VNet and subnet inside that VNet, and a network security group acting to protect the subnet by blocking all inbound traffic except port 22 for SSH.</span></span> <span data-ttu-id="e17dd-148">È ora possibile distribuire la macchina virtuale all'interno di questa infrastruttura di rete esistente.</span><span class="sxs-lookup"><span data-stu-id="e17dd-148">The VM can now be deployed inside this existing network infrastructure.</span></span>

<span data-ttu-id="e17dd-149">Con l'interfaccia della riga di comando di Azure e il comando `azure vm create`, la VM Linux viene distribuita nel gruppo di risorse, nella rete virtuale, nella subnet e nella scheda di rete virtuale esistenti.</span><span class="sxs-lookup"><span data-stu-id="e17dd-149">Using the Azure CLI, and the `azure vm create` command, the Linux VM is deployed to the existing Azure Resource Group, VNet, Subnet, and VNic.</span></span> <span data-ttu-id="e17dd-150">Per altre informazioni sull'utilizzo dell'interfaccia della riga di comando per distribuire una macchina virtuale completa, vedere [Creare un ambiente Linux completo tramite l'interfaccia della riga di comando di Azure](create-cli-complete.md).</span><span class="sxs-lookup"><span data-stu-id="e17dd-150">For more information on using the CLI to deploy a complete VM, see [Create a complete Linux environment by using the Azure CLI](create-cli-complete.md)</span></span>

```azurecli
azure vm create myVM \
    --resource-group myResourceGroup \
    --location eastus \
    --os-type linux \
    --image-urn Debian \
    --storage-account-name mystorageaccount \
    --admin-username myAdminUser \
    --ssh-publickey-file ~/.ssh/id_rsa.pub \
    --vnet-name myVNet \
    --vnet-subnet-name mySubnet \
    --nic-name myVNic
```

<span data-ttu-id="e17dd-151">Usando i flag dell'interfaccia della riga di comando per chiamare le risorse esistenti, si indica ad Azure di distribuire la macchina virtuale all'interno della rete esistente.</span><span class="sxs-lookup"><span data-stu-id="e17dd-151">By using the CLI flags to call out existing resources, you instruct Azure to deploy the VM inside the existing network.</span></span> <span data-ttu-id="e17dd-152">Una volta distribuite la rete virtuale e la subnet possono essere usate come risorse statiche o permanenti nell'area di Azure.</span><span class="sxs-lookup"><span data-stu-id="e17dd-152">Once a VNet and subnet have been deployed, they can be left as static or permanent resources inside your Azure region.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="e17dd-153">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e17dd-153">Next steps</span></span>

* [<span data-ttu-id="e17dd-154">Usare un modello di Azure Resource Manager per creare una distribuzione specifica</span><span class="sxs-lookup"><span data-stu-id="e17dd-154">Use an Azure Resource Manager template to create a specific deployment</span></span>](../windows/cli-deploy-templates.md)
* [<span data-ttu-id="e17dd-155">Creare un ambiente Linux completo mediante l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="e17dd-155">Create your own custom environment for a Linux VM using Azure CLI commands directly</span></span>](create-cli-complete.md)
* [<span data-ttu-id="e17dd-156">Creare una VM Linux in Azure usando i modelli</span><span class="sxs-lookup"><span data-stu-id="e17dd-156">Create a Linux VM on Azure using templates</span></span>](create-ssh-secured-vm-from-template.md)
