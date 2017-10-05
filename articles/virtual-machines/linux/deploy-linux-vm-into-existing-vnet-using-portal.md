---
title: Distribuire macchine virtuali Linux in una rete esistente con il portale di Azure | Microsoft Docs
description: Distribuire una macchina virtuale Linux in una rete virtuale di Azure esistente tramite il portale.
services: virtual-machines-linux
documentationcenter: virtual-machines-linux
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 964c0fc41773b50a9fbe476df47460484c2ada66
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-deploy-a-linux-virtual-machine-into-an-existing-azure-virtual-network-with-the-azure-portal"></a><span data-ttu-id="cbd77-103">Come distribuire una macchina virtuale Linux in una rete virtuale Azure esistente con il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="cbd77-103">How to deploy a Linux virtual machine into an existing Azure Virtual Network with the Azure portal</span></span>

<span data-ttu-id="cbd77-104">Questo articolo illustra come usare distribuire una macchina virtuale in una rete virtuale esistente.</span><span class="sxs-lookup"><span data-stu-id="cbd77-104">This article shows you how to deploy a virtual machine (VM) into an existing virtual network (VNet).</span></span> <span data-ttu-id="cbd77-105">Gli asset di Azure, come le reti virtuali e i gruppi di sicurezza di rete, devono essere risorse statiche, ovvero di lunga durata e distribuite raramente.</span><span class="sxs-lookup"><span data-stu-id="cbd77-105">Azure assets like VNets and network security groups should be static and long lived resources that are rarely deployed.</span></span> <span data-ttu-id="cbd77-106">Dopo essere stata distribuita, una rete virtuale può essere usata in nuove distribuzioni costanti, senza alcun effetto negativo sull'infrastruttura.</span><span class="sxs-lookup"><span data-stu-id="cbd77-106">Once a VNet has been deployed, it can be reused by constant redeployments without any adverse affects to the infrastructure.</span></span> <span data-ttu-id="cbd77-107">Si pensi a una rete virtuale come se fosse analoga a uno switch di rete hardware tradizionale, il quale non richiede una nuova configurazione a ogni distribuzione.</span><span class="sxs-lookup"><span data-stu-id="cbd77-107">Thinking about a VNet as being a traditional hardware network switch - you would not need to configure a brand new hardware switch with each deployment.</span></span>  

<span data-ttu-id="cbd77-108">In una rete virtuale configurata in modo appropriato, è possibile continuare a distribuire nuovi server più volte, apportando solo le modifiche indispensabili durante il ciclo di vita della rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="cbd77-108">With a correctly configured VNet, you can continue to deploy new servers into that VNet over and over with few, if any, changes required over the life of the VNet.</span></span>

## <a name="create-the-resource-group"></a><span data-ttu-id="cbd77-109">Creare il gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="cbd77-109">Create the resource group</span></span>

<span data-ttu-id="cbd77-110">Prima creare un gruppo di risorse per organizzare tutti gli elementi che si creano durante questa procedura dettagliata.</span><span class="sxs-lookup"><span data-stu-id="cbd77-110">First, create a resource group to organize everything you create in this walkthrough.</span></span> <span data-ttu-id="cbd77-111">Per altre informazioni sui gruppi di risorse di Azure, vedere [Panoramica di Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md)</span><span class="sxs-lookup"><span data-stu-id="cbd77-111">For more information about Azure resource groups, see [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md)</span></span>

![createResourceGroup](./media/deploy-linux-vm-into-existing-vnet-using-portal/createResourceGroup.png)


## <a name="create-the-vnet"></a><span data-ttu-id="cbd77-113">Creare la rete virtuale</span><span class="sxs-lookup"><span data-stu-id="cbd77-113">Create the VNet</span></span>

<span data-ttu-id="cbd77-114">Creare una rete virtuale in cui eseguire le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="cbd77-114">Next, build a VNet to launch the VMs into.</span></span> <span data-ttu-id="cbd77-115">La rete virtuale contiene una subnet e verrà associata al gruppo di sicurezza di rete con questa subnet in un passaggio successivo.</span><span class="sxs-lookup"><span data-stu-id="cbd77-115">The VNet contains one subnet and is associated with the network security group with this subnet in a later step.</span></span>

![createVNet](./media/deploy-linux-vm-into-existing-vnet-using-portal/createVNet.png)

## <a name="add-a-vnic-to-the-subnet"></a><span data-ttu-id="cbd77-117">Aggiungere una scheda di interfaccia di rete virtuale alla subnet</span><span class="sxs-lookup"><span data-stu-id="cbd77-117">Add a VNic to the subnet</span></span>

<span data-ttu-id="cbd77-118">Le schede di interfaccia rete virtuale sono importanti in quanto è connetterle a macchine virtuali diverse.</span><span class="sxs-lookup"><span data-stu-id="cbd77-118">Virtual network cards (VNics) are important as you can connect them to different VMs.</span></span> <span data-ttu-id="cbd77-119">In questo modo la scheda di interfaccia di rete virtuale diventa una risorsa statica, mentre le macchine virtuali possono essere temporanee.</span><span class="sxs-lookup"><span data-stu-id="cbd77-119">This approach keeps the VNic as a static resource while the VMs can be temporary.</span></span> <span data-ttu-id="cbd77-120">Creare una scheda di interfaccia di rete virtuale e associarla alla subnet creata nel passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="cbd77-120">Create a VNic and associate it with the subnet created in the previous step.</span></span>

![createVNic](./media/deploy-linux-vm-into-existing-vnet-using-portal/createVNic.png)

## <a name="create-the-network-security-group"></a><span data-ttu-id="cbd77-122">Creare il gruppo di sicurezza di rete</span><span class="sxs-lookup"><span data-stu-id="cbd77-122">Create the network security group</span></span>

<span data-ttu-id="cbd77-123">I gruppi di sicurezza di rete di Azure sono analoghi a un firewall a livello di rete.</span><span class="sxs-lookup"><span data-stu-id="cbd77-123">Azure network security groups are equivalent to a firewall at the network layer.</span></span> <span data-ttu-id="cbd77-124">Per altre informazioni sui gruppi di sicurezza di rete di Azure, vedere [Che cos'è un gruppo di sicurezza di rete](../../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="cbd77-124">For more information on Azure network security groups, see [What is a Network Security Group](../../virtual-network/virtual-networks-nsg.md).</span></span>

![createNSG](./media/deploy-linux-vm-into-existing-vnet-using-portal/createNSG.png)

## <a name="add-an-inbound-ssh-allow-rule"></a><span data-ttu-id="cbd77-126">Aggiungere una regola di assenso SSH in ingresso</span><span class="sxs-lookup"><span data-stu-id="cbd77-126">Add an inbound SSH allow rule</span></span>

<span data-ttu-id="cbd77-127">La macchina virtuale deve accedere da Internet, pertanto viene creata una regola che consente di lasciare entrare il traffico in ingresso verso la porta 22 della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="cbd77-127">The VM needs access from the internet, so a rule allowing inbound port 22 traffic to be passed through the network to port 22 on the VM is created.</span></span>

![createInboundSSH](./media/deploy-linux-vm-into-existing-vnet-using-portal/createInboundSSH.png)

## <a name="associate-the-nsg-with-the-subnet"></a><span data-ttu-id="cbd77-129">Associare il gruppo di sicurezza di rete alla subnet</span><span class="sxs-lookup"><span data-stu-id="cbd77-129">Associate the NSG with the subnet</span></span>

<span data-ttu-id="cbd77-130">Dopo aver creato la rete virtuale e la subnet, il gruppo di sicurezza di rete viene associato alla subnet.</span><span class="sxs-lookup"><span data-stu-id="cbd77-130">With the VNet and the subnet created, associate the network security group with the subnet.</span></span> <span data-ttu-id="cbd77-131">È possibile associare i gruppi di sicurezza di rete a un'intera subnet o a una scheda di rete virtuale singola.</span><span class="sxs-lookup"><span data-stu-id="cbd77-131">Network security groups can be associated with either an entire subnet or an individual VNic.</span></span> <span data-ttu-id="cbd77-132">Con il firewall che filtra il traffico a livello di subnet, tutte le schede di interfaccia di rete virtuale e le macchine virtuali all'interno della subnet sono protette dal gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="cbd77-132">With the firewall filtering traffic at the subnet level, all VNics and the VMs within the subnet are protected by the network security group.</span></span> <span data-ttu-id="cbd77-133">L'altro approccio è l'associazione del gruppo di sicurezza di rete con una sola scheda di interfaccia di rete virtuale e con la protezione di una sola macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="cbd77-133">The other approach is the network security group being associated with just a single VNic and protecting just one VM.</span></span>

![associateNSG](./media/deploy-linux-vm-into-existing-vnet-using-portal/associateNSG.png)


## <a name="deploy-the-vm-into-the-vnet-and-nsg"></a><span data-ttu-id="cbd77-135">Distribuire la macchina virtuale nella rete virtuale e nel gruppo di sicurezza di rete</span><span class="sxs-lookup"><span data-stu-id="cbd77-135">Deploy the VM into the VNet and NSG</span></span>

<span data-ttu-id="cbd77-136">Tramite il portale di Azure, la VM Linux viene distribuita nel gruppo di risorse, nella rete virtuale, nella subnet e nella scheda di rete virtuale esistenti.</span><span class="sxs-lookup"><span data-stu-id="cbd77-136">Using the Azure portal, the Linux VM is deployed to the existing Azure Resource Group, VNet, Subnet, and VNic.</span></span>

![createVM](./media/deploy-linux-vm-into-existing-vnet-using-portal/createVM.png)

<span data-ttu-id="cbd77-138">Usando il portale per scegliere le risorse esistenti, si indica ad Azure di distribuire la macchina virtuale all'interno della rete esistente.</span><span class="sxs-lookup"><span data-stu-id="cbd77-138">By using the portal to choose existing resources, you instruct Azure to deploy the VM inside the existing network.</span></span> <span data-ttu-id="cbd77-139">Una volta distribuite la rete virtuale e la subnet possono essere usate come risorse statiche o permanenti nell'area di Azure.</span><span class="sxs-lookup"><span data-stu-id="cbd77-139">Once a VNet and subnet have been deployed, they can be left as static or permanent resources inside your Azure region.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="cbd77-140">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="cbd77-140">Next steps</span></span>

* [<span data-ttu-id="cbd77-141">Usare un modello di Azure Resource Manager per creare una distribuzione specifica</span><span class="sxs-lookup"><span data-stu-id="cbd77-141">Use an Azure Resource Manager template to create a specific deployment</span></span>](../windows/cli-deploy-templates.md)
* [<span data-ttu-id="cbd77-142">Creare un ambiente Linux completo mediante l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="cbd77-142">Create your own custom environment for a Linux VM using Azure CLI commands directly</span></span>](create-cli-complete.md)
* [<span data-ttu-id="cbd77-143">Creare una VM Linux in Azure usando i modelli</span><span class="sxs-lookup"><span data-stu-id="cbd77-143">Create a Linux VM on Azure using templates</span></span>](create-ssh-secured-vm-from-template.md)
