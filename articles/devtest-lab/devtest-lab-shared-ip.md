---
title: Comprendere gli indirizzi IP condivisi in Azure DevTest Labs| Microsoft Docs
description: Informazioni su come Azure DevTest Labs usa gli indirizzi IP condivisi per ridurre al minimo gli indirizzi IP pubblici necessari per accedere alle macchine virtuali del lab.
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
ms.openlocfilehash: 9f6e1980bf5ea5b41da98a135d89f1c5159921a7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="understand-shared-ip-addresses-in-azure-devtest-labs"></a><span data-ttu-id="2d006-103">Comprendere gli indirizzi IP condivisi in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="2d006-103">Understand shared IP addresses in Azure DevTest Labs</span></span>

<span data-ttu-id="2d006-104">Azure DevTest Labs consente alle macchine virtuali del lab di condividere gli stessi indirizzi IP per ridurre al minimo il numero di indirizzi IP pubblici necessari per accedere alle singole macchine virtuali del lab.</span><span class="sxs-lookup"><span data-stu-id="2d006-104">Azure DevTest Labs lets lab VMs share the same public IP address to minimize the number of public IP addresses required to access your individual lab VMs.</span></span>  <span data-ttu-id="2d006-105">In questo articolo viene descritto come funzionano gli indirizzi IP condivisi e le opzioni di configurazione correlate.</span><span class="sxs-lookup"><span data-stu-id="2d006-105">This article describes how shared IPs work and their related configuration options.</span></span>

## <a name="shared-ip-setting"></a><span data-ttu-id="2d006-106">Impostazione di un indirizzo IP condiviso</span><span class="sxs-lookup"><span data-stu-id="2d006-106">Shared IP setting</span></span>

<span data-ttu-id="2d006-107">Quando viene creato, un lab si trova nella subnet di una rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="2d006-107">When you create a lab, it resides in a subnet of a virtual network.</span></span>  <span data-ttu-id="2d006-108">Per impostazione predefinita, questa subnet viene creata con **Enable shared public IP** (Abilita indirizzo IP pubblico condiviso) impostato su *Sì*.</span><span class="sxs-lookup"><span data-stu-id="2d006-108">By default, this subnet is created with **Enable shared public IP** set to *Yes*.</span></span>  <span data-ttu-id="2d006-109">Questa configurazione crea un indirizzo IP pubblico per l'intera subnet.</span><span class="sxs-lookup"><span data-stu-id="2d006-109">This configuration creates one public IP address for the entire subnet.</span></span>  <span data-ttu-id="2d006-110">Per altre informazioni sulla configurazione di reti e subnet virtuali, vedere [Configurare una rete virtuale per Azure DevTest Labs](devtest-lab-configure-vnet.md).</span><span class="sxs-lookup"><span data-stu-id="2d006-110">For more information about configuring virtual networks and subnets, see [Configure a virtual network in Azure DevTest Labs](devtest-lab-configure-vnet.md).</span></span>

![Nuova subnet del lab](media/devtest-lab-shared-ip/lab-subnet.png)

<span data-ttu-id="2d006-112">Per i lab esistenti, è possibile abilitare questa opzione selezionando **Criteri e configurazione > Reti virtuali**.</span><span class="sxs-lookup"><span data-stu-id="2d006-112">For existing labs, you can enable this option by selecting **Configuration and policies > Virtual Networks**.</span></span> <span data-ttu-id="2d006-113">Quindi, selezionare una rete virtuale dall'elenco e scegliere **ABILITA IP PUBBLICO CONDIVISO** per una subnet selezionata.</span><span class="sxs-lookup"><span data-stu-id="2d006-113">Then, select a virtual network from the list and choose **ENABLE SHARED PUBLIC IP** for a selected subnet.</span></span> <span data-ttu-id="2d006-114">È anche possibile disabilitare questa opzione in qualsiasi lab se non si desidera condividere un indirizzo IP con le macchine virtuali del lab.</span><span class="sxs-lookup"><span data-stu-id="2d006-114">You can also disable this option in any lab if you don't want to share a public IP address across lab VMs.</span></span>

<span data-ttu-id="2d006-115">Tutte le macchine virtuali create in questo lab usano per impostazione predefinita un indirizzo IP condiviso.</span><span class="sxs-lookup"><span data-stu-id="2d006-115">Any VMs created in this lab default to using a shared IP.</span></span>  <span data-ttu-id="2d006-116">Quando si crea la macchina virtuale, questa impostazione è visibile nel pannello **Impostazioni avanzate** in **Configurazione indirizzi IP**.</span><span class="sxs-lookup"><span data-stu-id="2d006-116">When creating the VM, this setting can be observed in the **Advanced settings** blade under **IP address configuration**.</span></span>

![Nuova macchina virtuale](media/devtest-lab-shared-ip/new-vm.png)

- <span data-ttu-id="2d006-118">**Condiviso:** tutte le macchine virtuali create come **Condivise** vengono inserite in un gruppo di risorse (RG).</span><span class="sxs-lookup"><span data-stu-id="2d006-118">**Shared:** All VMs created as **Shared** are placed into one resource group (RG).</span></span> <span data-ttu-id="2d006-119">Un singolo indirizzo IP viene assegnato al relativo gruppo di risorse e tutte le macchine virtuali nel gruppo di risorse utilizzeranno l'indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="2d006-119">A single IP address is assigned for that RG and all VMs in the RG will use that IP address.</span></span>
- <span data-ttu-id="2d006-120">**Pubblico:** ciascuna macchina virtuale creata dispone del proprio indirizzo IP e viene creata nel proprio gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="2d006-120">**Public:** Every VM you create has its own IP address and is created in its own resource group.</span></span>
- <span data-ttu-id="2d006-121">**Privato:** ogni macchina virtuale creata usa un indirizzo IP privato.</span><span class="sxs-lookup"><span data-stu-id="2d006-121">**Private:** Every VM you create uses a private IP address.</span></span> <span data-ttu-id="2d006-122">Non sarà possibile connettersi a questa macchina virtuale direttamente da Internet con Desktop remoto.</span><span class="sxs-lookup"><span data-stu-id="2d006-122">You will not be able to connect to this VM directly from the internet with Remote Desktop.</span></span>

<span data-ttu-id="2d006-123">Ogni volta che una macchina virtuale con indirizzo IP condiviso abilitato viene aggiunta alla subnet, DevTest Labs aggiunge automaticamente la macchina virtuale a un sistema di bilanciamento del carico e assegna un numero di porta TCP all'indirizzo IP pubblico, che inoltra alla porta RDP nella macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="2d006-123">Whenever a VM with shared IP enabled is added to the subnet, DevTest Labs automatically adds the VM to a load balancer and assigns a TCP port number on the public IP address, forwarding to the RDP port on the VM.</span></span>  

## <a name="using-the-shared-ip"></a><span data-ttu-id="2d006-124">Uso dell'indirizzo IP condiviso</span><span class="sxs-lookup"><span data-stu-id="2d006-124">Using the shared IP</span></span>

- <span data-ttu-id="2d006-125">**Utenti Linux:** il collegamento di SSH alla macchina virtuale avviene tramite l'indirizzo IP o un nome di dominio completo, seguito da due punti e dalla porta.</span><span class="sxs-lookup"><span data-stu-id="2d006-125">**Linux users:** SSH to the VM by using the IP address or fully qualified domain name, followed by a colon, followed by the port.</span></span> <span data-ttu-id="2d006-126">Nell'immagine seguente, ad esempio, l'indirizzo RDP per connettersi alla macchina virtuale è `doclab-lab13998814308000.centralus.cloudapp.azure.com:51686`.</span><span class="sxs-lookup"><span data-stu-id="2d006-126">For example, in the image below, the RDP address to connect to the VM is `doclab-lab13998814308000.centralus.cloudapp.azure.com:51686`.</span></span>

  ![Esempio di macchina virtuale](media/devtest-lab-shared-ip/vm-info.png)

- <span data-ttu-id="2d006-128">**Utenti Windows:** selezionare il pulsante **Connetti** dal portale Azure per scaricare un file RDP preconfigurato e accedere alla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="2d006-128">**Windows users:** Select the **Connect** button on the Azure portal to download a pre-configured RDP file and access the VM.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2d006-129">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2d006-129">Next steps</span></span>

* [<span data-ttu-id="2d006-130">Definire i criteri di lab in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="2d006-130">Define lab policies in Azure DevTest Labs</span></span>](devtest-lab-set-lab-policy.md)
* [<span data-ttu-id="2d006-131">Configurare una rete virtuale per Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="2d006-131">Configure a virtual network in Azure DevTest Labs</span></span>](devtest-lab-configure-vnet.md)





