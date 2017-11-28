---
title: aaaOpen porte tooa VM utilizzando hello portale di Azure | Documenti Microsoft
description: Informazioni su come tooopen una porta / creare una macchina virtuale Windows di tooyour endpoint utilizzando il modello di distribuzione Gestione risorse di hello in hello portale di Azure
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: f7cf0319-5ee7-435e-8f94-c484bf5ee6f1
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 08/21/2017
ms.author: iainfou
ms.openlocfilehash: aba789c65254651899aa688f256fe616c3d0126d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooopen-ports-tooa-virtual-machine-with-hello-azure-portal"></a><span data-ttu-id="4337f-103">Come tooopen porte tooa la macchina virtuale con hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="4337f-103">How tooopen ports tooa virtual machine with hello Azure portal</span></span>
[!INCLUDE [virtual-machines-common-nsg-quickstart](../../../includes/virtual-machines-common-nsg-quickstart.md)]

## <a name="quick-commands"></a><span data-ttu-id="4337f-104">Comandi rapidi</span><span class="sxs-lookup"><span data-stu-id="4337f-104">Quick commands</span></span>
<span data-ttu-id="4337f-105">È possibile [eseguire questi passaggi anche tramite Azure PowerShell](nsg-quickstart-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="4337f-105">You can also [perform these steps using Azure PowerShell](nsg-quickstart-powershell.md).</span></span>

<span data-ttu-id="4337f-106">Come prima operazione, creare il gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="4337f-106">First, create your Network Security Group.</span></span> <span data-ttu-id="4337f-107">Selezionare un gruppo di risorse nel portale di hello, scegliere **Aggiungi**, quindi cercare e selezionare **il gruppo di sicurezza di rete**:</span><span class="sxs-lookup"><span data-stu-id="4337f-107">Select a resource group in hello portal, choose **Add**, then search for and select **Network security group**:</span></span>

![Aggiungere un gruppo di sicurezza di rete](./media/nsg-quickstart-portal/add-nsg.png)

<span data-ttu-id="4337f-109">Immettere un nome per il gruppo di sicurezza di rete e selezionare o creare un gruppo di risorse, quindi selezionare una posizione.</span><span class="sxs-lookup"><span data-stu-id="4337f-109">Enter a name for your Network Security Group, select or create a resource group, and select a location.</span></span> <span data-ttu-id="4337f-110">Al termine selezionare **Crea**:</span><span class="sxs-lookup"><span data-stu-id="4337f-110">Select **Create** when finished:</span></span>

![Creare un gruppo di sicurezza di rete](./media/nsg-quickstart-portal/create-nsg.png)

<span data-ttu-id="4337f-112">Selezionare il nuovo gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="4337f-112">Select your new Network Security Group.</span></span> <span data-ttu-id="4337f-113">Selezionare 'Regole di sicurezza in ingresso', quindi selezionare hello **Aggiungi** toocreate pulsante una regola:</span><span class="sxs-lookup"><span data-stu-id="4337f-113">Select 'Inbound security rules', then select hello **Add** button toocreate a rule:</span></span>

![Aggiungere una regola in entrata](./media/nsg-quickstart-portal/add-inbound-rule.png)

<span data-ttu-id="4337f-115">Scegliere un comune **servizio** dal menu a discesa hello, ad esempio *HTTP*.</span><span class="sxs-lookup"><span data-stu-id="4337f-115">Choose a common **Service** from hello drop-down menu, such as *HTTP*.</span></span> <span data-ttu-id="4337f-116">È inoltre possibile selezionare *personalizzato* tooprovide toouse una porta specifica.</span><span class="sxs-lookup"><span data-stu-id="4337f-116">You can also select *Custom* tooprovide a specific port toouse.</span></span> <span data-ttu-id="4337f-117">Se si desidera, modificare la priorità hello o il nome.</span><span class="sxs-lookup"><span data-stu-id="4337f-117">If desired, change hello priority or name.</span></span> <span data-ttu-id="4337f-118">Hello priorità influisce sull'ordine hello in cui vengono applicate regole - valore numerico di hello inferiore hello, hello precedenti hello regola viene applicata.</span><span class="sxs-lookup"><span data-stu-id="4337f-118">hello priority affects hello order in which rules are applied - hello lower hello numerical value, hello earlier hello rule is applied.</span></span> <span data-ttu-id="4337f-119">È inoltre possibile selezionare **avanzate** nella parte superiore di hello di tooenter questa schermata uno specifico intervallo di origine IP blocco o la porta, ad esempio.</span><span class="sxs-lookup"><span data-stu-id="4337f-119">You can also select **Advanced** at hello top of this screen tooenter a specific source IP block or port range, for example.</span></span> <span data-ttu-id="4337f-120">Quando si è pronti, selezionare **OK** regola hello toocreate:</span><span class="sxs-lookup"><span data-stu-id="4337f-120">When you are ready, select **OK** toocreate hello rule:</span></span>

![Creare una regola in entrata](./media/nsg-quickstart-portal/create-inbound-rule.png)

<span data-ttu-id="4337f-122">Il passaggio finale consiste tooassociate la sicurezza della rete di gruppo con una subnet o un'interfaccia di rete specifici.</span><span class="sxs-lookup"><span data-stu-id="4337f-122">Your final step is tooassociate your Network Security Group with a subnet or a specific network interface.</span></span> <span data-ttu-id="4337f-123">Associare si hello il gruppo di sicurezza di rete a una subnet.</span><span class="sxs-lookup"><span data-stu-id="4337f-123">Let's associate hello Network Security Group with a subnet.</span></span> <span data-ttu-id="4337f-124">Selezionare **Subnet**, quindi scegliere **Associa**:</span><span class="sxs-lookup"><span data-stu-id="4337f-124">Select **Subnets**, then choose **Associate**:</span></span>

![Associare un gruppo di sicurezza di rete con una subnet](./media/nsg-quickstart-portal/associate-subnet.png)

<span data-ttu-id="4337f-126">Selezionare la rete virtuale e quindi selezionare la subnet appropriata hello:</span><span class="sxs-lookup"><span data-stu-id="4337f-126">Select your virtual network, and then select hello appropriate subnet:</span></span>

![Associare un gruppo di sicurezza di rete con una rete virtuale](./media/nsg-quickstart-portal/select-vnet-subnet.png)

<span data-ttu-id="4337f-128">È stato creato un gruppo di sicurezza di rete, è stata creata una regola in entrata che consente il traffico sulla porta 80 ed è stata associata a una subnet.</span><span class="sxs-lookup"><span data-stu-id="4337f-128">You have now created a Network Security Group, created an inbound rule that allows traffic on port 80, and associated it with a subnet.</span></span> <span data-ttu-id="4337f-129">Tutte le macchine virtuali si connettono toothat subnet sono raggiungibili sulla porta 80.</span><span class="sxs-lookup"><span data-stu-id="4337f-129">Any VMs you connect toothat subnet are reachable on port 80.</span></span>

## <a name="more-information-on-network-security-groups"></a><span data-ttu-id="4337f-130">Altre informazioni sui gruppi di sicurezza di rete</span><span class="sxs-lookup"><span data-stu-id="4337f-130">More information on Network Security Groups</span></span>
<span data-ttu-id="4337f-131">Hello rapido comandi consentono di tooget backup e in esecuzione con traffico propagazione tooyour macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="4337f-131">hello quick commands here allow you tooget up and running with traffic flowing tooyour VM.</span></span> <span data-ttu-id="4337f-132">Gruppi di sicurezza di rete forniscono numerose funzionalità eccellenti e granularità per il controllo tooyour di accedere alle risorse.</span><span class="sxs-lookup"><span data-stu-id="4337f-132">Network Security Groups provide many great features and granularity for controlling access tooyour resources.</span></span> <span data-ttu-id="4337f-133">Per altre informazioni, leggere l'articolo sulla [creazione di un gruppo di sicurezza di rete e di regole dell'elenco di controllo di accesso qui](../../virtual-network/virtual-networks-create-nsg-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="4337f-133">You can read more about [creating a Network Security Group and ACL rules here](../../virtual-network/virtual-networks-create-nsg-arm-ps.md).</span></span>

<span data-ttu-id="4337f-134">Per le applicazioni Web a disponibilità elevata, è consigliabile inserire le macchine virtuali dietro a un Azure Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="4337f-134">For highly available web applications, you should place your VMs behind an Azure Load Balancer.</span></span> <span data-ttu-id="4337f-135">bilanciamento del carico di Hello distribuisce il traffico tooVMs, con un gruppo di sicurezza di rete che consente di filtrare il traffico.</span><span class="sxs-lookup"><span data-stu-id="4337f-135">hello load balancer distributes traffic tooVMs, with a Network Security Group that provides traffic filtering.</span></span> <span data-ttu-id="4337f-136">Per ulteriori informazioni, vedere [come macchine saldo tooload virtuali Linux in Azure toocreate applicazioni a disponibilità elevata](tutorial-load-balancer.md).</span><span class="sxs-lookup"><span data-stu-id="4337f-136">For more information, see [How tooload balance Linux virtual machines in Azure toocreate a highly available application](tutorial-load-balancer.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="4337f-137">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4337f-137">Next steps</span></span>
<span data-ttu-id="4337f-138">In questo esempio è stato creato il traffico HTTP tooallow una semplice regola.</span><span class="sxs-lookup"><span data-stu-id="4337f-138">In this example, you created a simple rule tooallow HTTP traffic.</span></span> <span data-ttu-id="4337f-139">È possibile trovare informazioni sulla creazione di ambienti più dettagliati in hello seguenti articoli:</span><span class="sxs-lookup"><span data-stu-id="4337f-139">You can find information on creating more detailed environments in hello following articles:</span></span>

* [<span data-ttu-id="4337f-140">Panoramica di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="4337f-140">Azure Resource Manager overview</span></span>](../../azure-resource-manager/resource-group-overview.md)
* [<span data-ttu-id="4337f-141">Che cos'è un gruppo di sicurezza di rete</span><span class="sxs-lookup"><span data-stu-id="4337f-141">What is a Network Security Group (NSG)?</span></span>](../../virtual-network/virtual-networks-nsg.md)