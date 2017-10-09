---
title: aaaDeploy le macchine virtuali Linux in una rete esistente con il portale di Azure | Documenti Microsoft
description: Distribuire una VM Linux in una rete virtuale esistente a Azure tramite il portale di hello.
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
ms.openlocfilehash: 51272b8cdb1dc7f3fe768d2ebbf4ebe0d754cf19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodeploy-a-linux-virtual-machine-into-an-existing-azure-virtual-network-with-hello-azure-portal"></a><span data-ttu-id="d5abf-103">Come toodeploy una macchina virtuale di Linux in una rete virtuale di Azure esistente con hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="d5abf-103">How toodeploy a Linux virtual machine into an existing Azure Virtual Network with hello Azure portal</span></span>

<span data-ttu-id="d5abf-104">In questo articolo illustra come toodeploy una macchina virtuale (VM) in una rete virtuale esistente (VNet).</span><span class="sxs-lookup"><span data-stu-id="d5abf-104">This article shows you how toodeploy a virtual machine (VM) into an existing virtual network (VNet).</span></span> <span data-ttu-id="d5abf-105">Gli asset di Azure, come le reti virtuali e i gruppi di sicurezza di rete, devono essere risorse statiche, ovvero di lunga durata e distribuite raramente.</span><span class="sxs-lookup"><span data-stu-id="d5abf-105">Azure assets like VNets and network security groups should be static and long lived resources that are rarely deployed.</span></span> <span data-ttu-id="d5abf-106">Dopo la distribuzione di una rete virtuale, può essere riutilizzato da ridistribuzioni costante senza alcuna infrastruttura toohello effetto negativo.</span><span class="sxs-lookup"><span data-stu-id="d5abf-106">Once a VNet has been deployed, it can be reused by constant redeployments without any adverse affects toohello infrastructure.</span></span> <span data-ttu-id="d5abf-107">Pensa a una rete virtuale come un tradizionale commutatore di rete hardware - non è necessario passare un nuovo hardware per ciascuna distribuzione tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="d5abf-107">Thinking about a VNet as being a traditional hardware network switch - you would not need tooconfigure a brand new hardware switch with each deployment.</span></span>  

<span data-ttu-id="d5abf-108">Con una rete virtuale è configurata correttamente, è possibile continuare toodeploy nuovi server in tale rete virtuale a più volte con alcuni, se presente, le modifiche richieste per la durata hello di hello rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="d5abf-108">With a correctly configured VNet, you can continue toodeploy new servers into that VNet over and over with few, if any, changes required over hello life of hello VNet.</span></span>

## <a name="create-hello-resource-group"></a><span data-ttu-id="d5abf-109">Creare il gruppo di risorse hello</span><span class="sxs-lookup"><span data-stu-id="d5abf-109">Create hello resource group</span></span>

<span data-ttu-id="d5abf-110">Creare innanzitutto un tooorganize gruppo di risorse tutti gli oggetti creati in questa procedura dettagliata.</span><span class="sxs-lookup"><span data-stu-id="d5abf-110">First, create a resource group tooorganize everything you create in this walkthrough.</span></span> <span data-ttu-id="d5abf-111">Per altre informazioni sui gruppi di risorse di Azure, vedere [Panoramica di Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md)</span><span class="sxs-lookup"><span data-stu-id="d5abf-111">For more information about Azure resource groups, see [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md)</span></span>

![createResourceGroup](./media/deploy-linux-vm-into-existing-vnet-using-portal/createResourceGroup.png)


## <a name="create-hello-vnet"></a><span data-ttu-id="d5abf-113">Creare hello rete virtuale</span><span class="sxs-lookup"><span data-stu-id="d5abf-113">Create hello VNet</span></span>

<span data-ttu-id="d5abf-114">Successivamente, compilare un hello toolaunch di rete virtuale le macchine virtuali in.</span><span class="sxs-lookup"><span data-stu-id="d5abf-114">Next, build a VNet toolaunch hello VMs into.</span></span> <span data-ttu-id="d5abf-115">Hello rete virtuale contiene una subnet e associato al gruppo di sicurezza di rete hello con questa subnet in un passaggio successivo.</span><span class="sxs-lookup"><span data-stu-id="d5abf-115">hello VNet contains one subnet and is associated with hello network security group with this subnet in a later step.</span></span>

![createVNet](./media/deploy-linux-vm-into-existing-vnet-using-portal/createVNet.png)

## <a name="add-a-vnic-toohello-subnet"></a><span data-ttu-id="d5abf-117">Aggiungere una subnet toohello VNic</span><span class="sxs-lookup"><span data-stu-id="d5abf-117">Add a VNic toohello subnet</span></span>

<span data-ttu-id="d5abf-118">Schede di rete virtuale (VNics) sono importanti, come è possibile collegare le macchine virtuali toodifferent.</span><span class="sxs-lookup"><span data-stu-id="d5abf-118">Virtual network cards (VNics) are important as you can connect them toodifferent VMs.</span></span> <span data-ttu-id="d5abf-119">Questo approccio consente di mantenere hello VNic come una risorsa statica durante hello macchine virtuali può essere temporaneo.</span><span class="sxs-lookup"><span data-stu-id="d5abf-119">This approach keeps hello VNic as a static resource while hello VMs can be temporary.</span></span> <span data-ttu-id="d5abf-120">Creare una scheda di rete virtuale e associarlo a subnet hello creato nel passaggio precedente hello.</span><span class="sxs-lookup"><span data-stu-id="d5abf-120">Create a VNic and associate it with hello subnet created in hello previous step.</span></span>

![createVNic](./media/deploy-linux-vm-into-existing-vnet-using-portal/createVNic.png)

## <a name="create-hello-network-security-group"></a><span data-ttu-id="d5abf-122">Creare un gruppo di sicurezza di rete hello</span><span class="sxs-lookup"><span data-stu-id="d5abf-122">Create hello network security group</span></span>

<span data-ttu-id="d5abf-123">Gruppi di sicurezza di rete di Azure sono equivalenti tooa firewall a livello di rete hello.</span><span class="sxs-lookup"><span data-stu-id="d5abf-123">Azure network security groups are equivalent tooa firewall at hello network layer.</span></span> <span data-ttu-id="d5abf-124">Per altre informazioni sui gruppi di sicurezza di rete di Azure, vedere [Che cos'è un gruppo di sicurezza di rete](../../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="d5abf-124">For more information on Azure network security groups, see [What is a Network Security Group](../../virtual-network/virtual-networks-nsg.md).</span></span>

![createNSG](./media/deploy-linux-vm-into-existing-vnet-using-portal/createNSG.png)

## <a name="add-an-inbound-ssh-allow-rule"></a><span data-ttu-id="d5abf-126">Aggiungere una regola di assenso SSH in ingresso</span><span class="sxs-lookup"><span data-stu-id="d5abf-126">Add an inbound SSH allow rule</span></span>

<span data-ttu-id="d5abf-127">Hello VM richiede l'accesso da hello internet, in modo da una regola che consente la porta in ingresso 22 traffico toobe passati tramite hello rete tooport 22 hello viene creata la VM.</span><span class="sxs-lookup"><span data-stu-id="d5abf-127">hello VM needs access from hello internet, so a rule allowing inbound port 22 traffic toobe passed through hello network tooport 22 on hello VM is created.</span></span>

![createInboundSSH](./media/deploy-linux-vm-into-existing-vnet-using-portal/createInboundSSH.png)

## <a name="associate-hello-nsg-with-hello-subnet"></a><span data-ttu-id="d5abf-129">Associare subnet hello hello NSG</span><span class="sxs-lookup"><span data-stu-id="d5abf-129">Associate hello NSG with hello subnet</span></span>

<span data-ttu-id="d5abf-130">Con rete virtuale hello e una subnet hello creato, associare il gruppo di sicurezza rete hello subnet hello.</span><span class="sxs-lookup"><span data-stu-id="d5abf-130">With hello VNet and hello subnet created, associate hello network security group with hello subnet.</span></span> <span data-ttu-id="d5abf-131">È possibile associare i gruppi di sicurezza di rete a un'intera subnet o a una scheda di rete virtuale singola.</span><span class="sxs-lookup"><span data-stu-id="d5abf-131">Network security groups can be associated with either an entire subnet or an individual VNic.</span></span> <span data-ttu-id="d5abf-132">Con il filtro di traffico a livello di subnet hello firewall di hello, tutti VNics e hello macchine virtuali all'interno di subnet hello sono protetti dal gruppo di sicurezza di rete hello.</span><span class="sxs-lookup"><span data-stu-id="d5abf-132">With hello firewall filtering traffic at hello subnet level, all VNics and hello VMs within hello subnet are protected by hello network security group.</span></span> <span data-ttu-id="d5abf-133">Hello altri approcci è hello gruppo di sicurezza di rete viene associato solo un singolo VNic e protegge solo una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="d5abf-133">hello other approach is hello network security group being associated with just a single VNic and protecting just one VM.</span></span>

![associateNSG](./media/deploy-linux-vm-into-existing-vnet-using-portal/associateNSG.png)


## <a name="deploy-hello-vm-into-hello-vnet-and-nsg"></a><span data-ttu-id="d5abf-135">Distribuire hello VM nella rete virtuale hello e gruppo</span><span class="sxs-lookup"><span data-stu-id="d5abf-135">Deploy hello VM into hello VNet and NSG</span></span>

<span data-ttu-id="d5abf-136">Utilizzo di hello portale di Azure, hello VM Linux è toohello distribuito esistente al gruppo di risorse di Azure, rete virtuale, Subnet e scheda di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="d5abf-136">Using hello Azure portal, hello Linux VM is deployed toohello existing Azure Resource Group, VNet, Subnet, and VNic.</span></span>

![createVM](./media/deploy-linux-vm-into-existing-vnet-using-portal/createVM.png)

<span data-ttu-id="d5abf-138">Utilizzando le risorse esistenti di hello toochoose portale, è possibile indicare hello toodeploy Azure VM all'interno di una rete esistente hello.</span><span class="sxs-lookup"><span data-stu-id="d5abf-138">By using hello portal toochoose existing resources, you instruct Azure toodeploy hello VM inside hello existing network.</span></span> <span data-ttu-id="d5abf-139">Una volta distribuite la rete virtuale e la subnet possono essere usate come risorse statiche o permanenti nell'area di Azure.</span><span class="sxs-lookup"><span data-stu-id="d5abf-139">Once a VNet and subnet have been deployed, they can be left as static or permanent resources inside your Azure region.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="d5abf-140">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d5abf-140">Next steps</span></span>

* [<span data-ttu-id="d5abf-141">Utilizzare un toocreate modello di gestione risorse di Azure una distribuzione specifica</span><span class="sxs-lookup"><span data-stu-id="d5abf-141">Use an Azure Resource Manager template toocreate a specific deployment</span></span>](../windows/cli-deploy-templates.md)
* [<span data-ttu-id="d5abf-142">Creare un ambiente Linux completo mediante l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="d5abf-142">Create your own custom environment for a Linux VM using Azure CLI commands directly</span></span>](create-cli-complete.md)
* [<span data-ttu-id="d5abf-143">Creare una VM Linux in Azure usando i modelli</span><span class="sxs-lookup"><span data-stu-id="d5abf-143">Create a Linux VM on Azure using templates</span></span>](create-ssh-secured-vm-from-template.md)
