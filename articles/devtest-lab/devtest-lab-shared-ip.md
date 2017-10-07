---
title: aaaUnderstand condiviso degli indirizzi IP in Azure DevTest Labs | Documenti Microsoft
description: Informazioni sul modo Azure DevTest Labs Usa condiviso IP indirizzi toominimize hello pubblica IP indirizzi necessari tooaccess macchine virtuali nel lab.
services: devtest-lab
documentationcenter: na
author: camsoper
manager: douge
editor: 
ms.assetid: 
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/16/2017
ms.author: casoper
ms.openlocfilehash: 8756410117a9d550d567d372174bf1ea96703c74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="understand-shared-ip-addresses-in-azure-devtest-labs"></a><span data-ttu-id="3bd6d-103">Comprendere gli indirizzi IP condivisi in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="3bd6d-103">Understand shared IP addresses in Azure DevTest Labs</span></span>

<span data-ttu-id="3bd6d-104">Azure DevTest Labs consente lab condivisione delle macchine virtuali hello stesso pubblico numero dell'indirizzo IP toominimize hello di pubblico tooaccess necessarie di indirizzi IP nel lab di singole macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="3bd6d-104">Azure DevTest Labs lets lab VMs share hello same public IP address toominimize hello number of public IP addresses required tooaccess your individual lab VMs.</span></span>  <span data-ttu-id="3bd6d-105">In questo articolo viene descritto come funzionano gli indirizzi IP condivisi e le opzioni di configurazione correlate.</span><span class="sxs-lookup"><span data-stu-id="3bd6d-105">This article describes how shared IPs work and their related configuration options.</span></span>

## <a name="shared-ip-setting"></a><span data-ttu-id="3bd6d-106">Impostazione di un indirizzo IP condiviso</span><span class="sxs-lookup"><span data-stu-id="3bd6d-106">Shared IP setting</span></span>

<span data-ttu-id="3bd6d-107">Quando viene creato, un lab si trova nella subnet di una rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="3bd6d-107">When you create a lab, it resides in a subnet of a virtual network.</span></span>  <span data-ttu-id="3bd6d-108">Per impostazione predefinita, questa subnet viene creata con **Abilita condivisa IP pubblico** impostare troppo*Sì*.</span><span class="sxs-lookup"><span data-stu-id="3bd6d-108">By default, this subnet is created with **Enable shared public IP** set too*Yes*.</span></span>  <span data-ttu-id="3bd6d-109">Questa configurazione crea un indirizzo IP pubblico per l'intera subnet hello.</span><span class="sxs-lookup"><span data-stu-id="3bd6d-109">This configuration creates one public IP address for hello entire subnet.</span></span>  <span data-ttu-id="3bd6d-110">Per altre informazioni sulla configurazione di reti e subnet virtuali, vedere [Configurare una rete virtuale per Azure DevTest Labs](devtest-lab-configure-vnet.md).</span><span class="sxs-lookup"><span data-stu-id="3bd6d-110">For more information about configuring virtual networks and subnets, see [Configure a virtual network in Azure DevTest Labs](devtest-lab-configure-vnet.md).</span></span>

![Nuova subnet del lab](media/devtest-lab-shared-ip/lab-subnet.png)

<span data-ttu-id="3bd6d-112">Per i lab esistenti, è possibile abilitare questa opzione selezionando **Criteri e configurazione > Reti virtuali**.</span><span class="sxs-lookup"><span data-stu-id="3bd6d-112">For existing labs, you can enable this option by selecting **Configuration and policies > Virtual Networks**.</span></span> <span data-ttu-id="3bd6d-113">Quindi, selezionare una rete virtuale dall'elenco hello e scegliere **abilitare IP pubblico condiviso** per una subnet selezionata.</span><span class="sxs-lookup"><span data-stu-id="3bd6d-113">Then, select a virtual network from hello list and choose **ENABLE SHARED PUBLIC IP** for a selected subnet.</span></span> <span data-ttu-id="3bd6d-114">È anche possibile disabilitare questa opzione in qualsiasi lab se non si desidera tooshare un indirizzo IP pubblico in lab, macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="3bd6d-114">You can also disable this option in any lab if you don't want tooshare a public IP address across lab VMs.</span></span>

<span data-ttu-id="3bd6d-115">Tutte le macchine virtuali creato in questa toousing predefinito lab un indirizzo IP condiviso.</span><span class="sxs-lookup"><span data-stu-id="3bd6d-115">Any VMs created in this lab default toousing a shared IP.</span></span>  <span data-ttu-id="3bd6d-116">Quando si creano hello macchina virtuale, questa impostazione può essere analizzata in hello **impostazioni avanzate** pannello **configurazione degli indirizzi IP**.</span><span class="sxs-lookup"><span data-stu-id="3bd6d-116">When creating hello VM, this setting can be observed in hello **Advanced settings** blade under **IP address configuration**.</span></span>

![Nuova macchina virtuale](media/devtest-lab-shared-ip/new-vm.png)

- <span data-ttu-id="3bd6d-118">**Condiviso:** tutte le macchine virtuali create come **Condivise** vengono inserite in un gruppo di risorse (RG).</span><span class="sxs-lookup"><span data-stu-id="3bd6d-118">**Shared:** All VMs created as **Shared** are placed into one resource group (RG).</span></span> <span data-ttu-id="3bd6d-119">Un singolo indirizzo IP viene assegnato a tale scopo RG e tutte le macchine virtuali in hello RG utilizzerà l'indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="3bd6d-119">A single IP address is assigned for that RG and all VMs in hello RG will use that IP address.</span></span>
- <span data-ttu-id="3bd6d-120">**Pubblico:** ciascuna macchina virtuale creata dispone del proprio indirizzo IP e viene creata nel proprio gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="3bd6d-120">**Public:** Every VM you create has its own IP address and is created in its own resource group.</span></span>
- <span data-ttu-id="3bd6d-121">**Privato:** ogni macchina virtuale creata usa un indirizzo IP privato.</span><span class="sxs-lookup"><span data-stu-id="3bd6d-121">**Private:** Every VM you create uses a private IP address.</span></span> <span data-ttu-id="3bd6d-122">Non sarà in grado di tooconnect toothis macchina virtuale direttamente da hello internet con Desktop remoto.</span><span class="sxs-lookup"><span data-stu-id="3bd6d-122">You will not be able tooconnect toothis VM directly from hello internet with Remote Desktop.</span></span>

<span data-ttu-id="3bd6d-123">Ogni volta che una macchina virtuale con IP condiviso abilitato viene aggiunto toohello subnet, DevTest Labs automaticamente aggiunge hello VM tooa il bilanciamento del carico e assegna un numero di porta TCP in indirizzo IP pubblico hello, inoltro toohello porta RDP in hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="3bd6d-123">Whenever a VM with shared IP enabled is added toohello subnet, DevTest Labs automatically adds hello VM tooa load balancer and assigns a TCP port number on hello public IP address, forwarding toohello RDP port on hello VM.</span></span>  

## <a name="using-hello-shared-ip"></a><span data-ttu-id="3bd6d-124">Utilizza hello condivisa IP</span><span class="sxs-lookup"><span data-stu-id="3bd6d-124">Using hello shared IP</span></span>

- <span data-ttu-id="3bd6d-125">**Gli utenti di Linux:** toohello SSH VM utilizzando l'indirizzo IP hello o nome di dominio completo, seguito da due punti, seguita dalla porta hello.</span><span class="sxs-lookup"><span data-stu-id="3bd6d-125">**Linux users:** SSH toohello VM by using hello IP address or fully qualified domain name, followed by a colon, followed by hello port.</span></span> <span data-ttu-id="3bd6d-126">Ad esempio, nella seguente figura hello hello RDP indirizzi toohello tooconnect macchina virtuale è `doclab-lab13998814308000.centralus.cloudapp.azure.com:51686`.</span><span class="sxs-lookup"><span data-stu-id="3bd6d-126">For example, in hello image below, hello RDP address tooconnect toohello VM is `doclab-lab13998814308000.centralus.cloudapp.azure.com:51686`.</span></span>

  ![Esempio di macchina virtuale](media/devtest-lab-shared-ip/vm-info.png)

- <span data-ttu-id="3bd6d-128">**Gli utenti di Windows:** hello seleziona **Connetti** pulsante hello toodownload portale Azure un file RDP configurati in precedenza e accedere hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="3bd6d-128">**Windows users:** Select hello **Connect** button on hello Azure portal toodownload a pre-configured RDP file and access hello VM.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3bd6d-129">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3bd6d-129">Next steps</span></span>

* [<span data-ttu-id="3bd6d-130">Definire i criteri di lab in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="3bd6d-130">Define lab policies in Azure DevTest Labs</span></span>](devtest-lab-set-lab-policy.md)
* [<span data-ttu-id="3bd6d-131">Configurare una rete virtuale per Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="3bd6d-131">Configure a virtual network in Azure DevTest Labs</span></span>](devtest-lab-configure-vnet.md)





