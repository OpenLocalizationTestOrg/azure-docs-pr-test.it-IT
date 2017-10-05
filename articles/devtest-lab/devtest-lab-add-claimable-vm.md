---
title: Aggiungere una macchina virtuale a disposizione degli utenti in un lab in Azure DevTest Labs | Microsoft Docs
description: Informazioni su come aggiungere una macchina virtuale a disposizione degli utenti in un lab in Azure DevTest Labs
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: f671e66e-9630-4e30-a131-a6bad9ed9c11
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/17/2017
ms.author: tarcher
ms.openlocfilehash: 98950d72e90b0e178bae2fffa7644fd824a25eea
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="add-a-claimable-vm-to-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="4af1b-103">Aggiungere una macchina virtuale a disposizione degli utenti in un lab in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="4af1b-103">Add a claimable VM to a lab in Azure DevTest Labs</span></span>
<span data-ttu-id="4af1b-104">Per aggiungere una macchina virtuale a disposizione degli utenti a un lab è necessario seguire una procedura simile all'[aggiunta di una macchina virtuale standard](devtest-lab-add-vm.md), partendo da una *base* che può essere un'[immagine personalizzata](devtest-lab-create-template.md), una [formula](devtest-lab-manage-formulas.md) o un'[immagine del Marketplace](devtest-lab-configure-marketplace-images.md).</span><span class="sxs-lookup"><span data-stu-id="4af1b-104">You add a claimable VM to a lab in a similar manner to how you [add a standard VM](devtest-lab-add-vm.md) – from a *base* that is either a [custom image](devtest-lab-create-template.md), [formula](devtest-lab-manage-formulas.md), or [Marketplace image](devtest-lab-configure-marketplace-images.md).</span></span> <span data-ttu-id="4af1b-105">In questa esercitazione viene descritto come usare il portale di Azure per aggiungere una macchina virtuale a disposizione degli utenti a un lab in DevTest Labs e viene illustrato il processo che un utente deve seguire per richiedere la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="4af1b-105">This tutorial walks you through using the Azure portal to add a claimable VM to a lab in DevTest Labs, and shows the process a user follows to claim the VM.</span></span>

> [!NOTE]
> <span data-ttu-id="4af1b-106">Se si distribuiscono macchine virtuali lab tramite i [modelli di Azure Resource Manager](devtest-lab-create-environment-from-arm.md), è possibile creare macchine virtuali a disposizione degli utenti impostando la proprietà **allowClaim** su vero nella sezione delle proprietà.</span><span class="sxs-lookup"><span data-stu-id="4af1b-106">If you deploy lab VMs through [Azure Resource Manager templates](devtest-lab-create-environment-from-arm.md), you can create claimable VMs by setting the **allowClaim** property to true in the properties section.</span></span>
>
>

## <a name="steps-to-add-a-claimable-vm-to-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="4af1b-107">Procedura per aggiungere una macchina virtuale a disposizione degli utenti in un lab in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="4af1b-107">Steps to add a claimable VM to a lab in Azure DevTest Labs</span></span>
1. <span data-ttu-id="4af1b-108">Accedere al [portale di Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="4af1b-108">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
1. <span data-ttu-id="4af1b-109">Selezionare **Altri servizi** e quindi **DevTest Labs** dall'elenco.</span><span class="sxs-lookup"><span data-stu-id="4af1b-109">Select **More Services**, and then select **DevTest Labs** from the list.</span></span>
1. <span data-ttu-id="4af1b-110">Nell'elenco di lab selezionare il lab in cui si vuole creare la VM a disposizione degli utenti.</span><span class="sxs-lookup"><span data-stu-id="4af1b-110">From the list of labs, select the lab in which you want to create the claimable VM.</span></span>  
1. <span data-ttu-id="4af1b-111">Nel pannello **Panoramica** del lab selezionare **+ Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="4af1b-111">On the lab's **Overview** blade, select **+ Add**.</span></span>  

    ![Pulsante Aggiungi VM](./media/devtest-lab-add-vm/devtestlab-home-blade-add-vm.png)

1. <span data-ttu-id="4af1b-113">Nel pannello **Scegli una base** selezionare una base per la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="4af1b-113">On the **Choose a base** blade, select a base for the VM.</span></span>
1. <span data-ttu-id="4af1b-114">Nel pannello **Macchina virtuale** immettere un nome per la nuova macchina virtuale nella casella di testo **Nome macchina virtuale**.</span><span class="sxs-lookup"><span data-stu-id="4af1b-114">On the **Virtual machine** blade, enter a name for the new virtual machine in the **Virtual machine name** text box.</span></span>

    ![Pannello Lab VM (VM lab)](./media/devtest-lab-add-vm/devtestlab-lab-vm-blade.png)

1. <span data-ttu-id="4af1b-116">Immettere un **Nome utente** a cui vengono concessi privilegi di amministratore nella macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="4af1b-116">Enter a **User Name** that is granted administrator privileges on the virtual machine.</span></span>  
1. <span data-ttu-id="4af1b-117">Se si vuole usare una password archiviata nell'[archivio segreto](https://azure.microsoft.com/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store), selezionare **Use a saved secret** (Usa un segreto salvato) e specificare un valore chiave corrispondente al segreto (password).</span><span class="sxs-lookup"><span data-stu-id="4af1b-117">If you want to use a password stored in your [secret store](https://azure.microsoft.com/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store), select **Use a saved secret**, and specify a key value that corresponds to your secret (password).</span></span> <span data-ttu-id="4af1b-118">In alternativa, immettere una password nel campo di testo **Digita un valore**.</span><span class="sxs-lookup"><span data-stu-id="4af1b-118">Otherwise, enter a password in the text field labeled **Type a value**.</span></span>
1. <span data-ttu-id="4af1b-119">Il **tipo di disco della macchina virtuale** determina il tipo di disco di archiviazione consentito per le macchine virtuali nel lab.</span><span class="sxs-lookup"><span data-stu-id="4af1b-119">The **Virtual machine disk type** determines which storage disk type is allowed for the virtual machines in the lab.</span></span>
1. <span data-ttu-id="4af1b-120">Selezionare **Dimensioni macchina virtuale** e uno degli elementi predefiniti che specificano le memorie centrali del processore, la dimensione della RAM e le dimensioni dell'unità disco rigido della VM da creare.</span><span class="sxs-lookup"><span data-stu-id="4af1b-120">Select **Virtual machine size** and select one of the predefined items that specify the processor cores, RAM size, and the hard drive size of the VM to create.</span></span>
1. <span data-ttu-id="4af1b-121">Selezionare **Elementi** e dall'elenco di elementi selezionare e configurare gli elementi da aggiungere all'immagine di base.</span><span class="sxs-lookup"><span data-stu-id="4af1b-121">Select **Artifacts** and from the list of artifacts, select and configure the artifacts that you want to add to the base image.</span></span> <span data-ttu-id="4af1b-122">Se non si ha familiarità con DevTest Labs o con la configurazione di elementi, vedere la sezione [Aggiungere un elemento esistente in una macchina virtuale](devtest-lab-add-vm.md#add-an-existing-artifact-to-a-vm) e tornare qui al termine dell'operazione.</span><span class="sxs-lookup"><span data-stu-id="4af1b-122">If you're new to DevTest Labs or configuring artifacts, refer to the [Add an existing artifact to a VM](devtest-lab-add-vm.md#add-an-existing-artifact-to-a-vm) section, and then return here when finished.</span></span>
1. <span data-ttu-id="4af1b-123">Selezionare **Impostazioni avanzate** per configurare le opzioni di rete e le opzioni relative alla scadenza della VM.</span><span class="sxs-lookup"><span data-stu-id="4af1b-123">Select **Advanced settings** to configure the VM's network options and expiration options.</span></span> <span data-ttu-id="4af1b-124">In **Claim options** (Opzioni di richiesta), scegliere **Sì** per rendere la macchina a disposizione degli utenti.</span><span class="sxs-lookup"><span data-stu-id="4af1b-124">Under **Claim options**, choose **Yes** to make the machine claimable.</span></span>

  ![Scegliere di rendere la macchina virtuale a disposizione degli utenti.](./media/devtest-lab-add-vm/devtestlab-claim-VM-option.png)

1. <span data-ttu-id="4af1b-126">Se si vuole visualizzare o copiare il modello di Azure Resource Manager, vedere la sezione [Salvare il modello di Azure Resource Manager](devtest-lab-add-vm.md#save-azure-resource-manager-template) e tornare qui al termine dell'operazione.</span><span class="sxs-lookup"><span data-stu-id="4af1b-126">If you want to view or copy the Azure Resource Manager template, refer to the [Save Azure Resource Manager template](devtest-lab-add-vm.md#save-azure-resource-manager-template) section, and return here when finished.</span></span>
1. <span data-ttu-id="4af1b-127">Selezionare **Crea** per aggiungere la macchina virtuale specificata al lab.</span><span class="sxs-lookup"><span data-stu-id="4af1b-127">Select **Create** to add the specified VM to the lab.</span></span>
1. <span data-ttu-id="4af1b-128">Il pannello lab consente di visualizzare lo stato di creazione della VM prima come **Creazione**, poi come **Esecuzione** dopo aver avviato la VM.</span><span class="sxs-lookup"><span data-stu-id="4af1b-128">The lab blade displays the status of the VM's creation - first as **Creating**, then as **Running** after the VM has been started.</span></span>


## <a name="using-a-claimable-vm"></a><span data-ttu-id="4af1b-129">Usare una macchina virtuale a disposizione degli utenti</span><span class="sxs-lookup"><span data-stu-id="4af1b-129">Using a claimable VM</span></span>

<span data-ttu-id="4af1b-130">Un utente può richiedere qualsiasi macchina virtuale dall'elenco "Claimable virtual machines" (Macchine virtuali a disposizione degli utenti) effettuando una delle seguenti operazioni:</span><span class="sxs-lookup"><span data-stu-id="4af1b-130">A user can claim any VM from the list of "Claimable virtual machines" by doing one of these steps:</span></span>

* <span data-ttu-id="4af1b-131">Dall'elenco "Claimable virtual machines" (Macchine virtuali a disposizione degli utenti), nella parte inferiore del pannello Panoramica del lab, fare clic con il tasto destro del mouse su una delle macchine virtuali nell'elenco e scegliere **Claim machine** (Richiedi macchina).</span><span class="sxs-lookup"><span data-stu-id="4af1b-131">From the list of "Claimable virtual machines" at the bottom of the lab's Overview blade, right-click on one of the VMs in the list and choose **Claim machine**.</span></span>

 ![Richiedere una specifica macchina virtuale a disposizione degli utenti.](./media/devtest-lab-add-vm/devtestlab-claim-VM.png)


* <span data-ttu-id="4af1b-133">Nella parte superiore del pannello **Panoramica**, scegliere **Claim any** (Richiedi qualsiasi).</span><span class="sxs-lookup"><span data-stu-id="4af1b-133">At the top of the **Overview** blade, choose **Claim any**.</span></span> <span data-ttu-id="4af1b-134">Una macchina virtuale casuale viene assegnata dall'elenco di macchine virtuali a disposizione degli utenti.</span><span class="sxs-lookup"><span data-stu-id="4af1b-134">A random virtual machine is assigned from the list of claimable VMs.</span></span>

 ![Richiedere una macchina virtuale a disposizione degli utenti.](./media/devtest-lab-add-vm/devtestlab-claim-any.png)


<span data-ttu-id="4af1b-136">Quando una macchina virtuale viene richiesta da un utente, questa viene spostata in alto nell'elenco "My virtual machines" (Le mie macchine virtuali) e non è più disponibile per un altro utente.</span><span class="sxs-lookup"><span data-stu-id="4af1b-136">After a user claims a VM, it is moved up into their list of "My virtual machines" and is no longer claimable by any other user.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4af1b-137">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4af1b-137">Next steps</span></span>
* <span data-ttu-id="4af1b-138">Dopo avere creato la VM, è possibile connettersi ad essa selezionando **Connetti** nel pannello della VM.</span><span class="sxs-lookup"><span data-stu-id="4af1b-138">Once the VM has been created, you can connect to the VM by selecting **Connect** on the VM's blade.</span></span>
* <span data-ttu-id="4af1b-139">Esplorare la [raccolta dei modelli Azure Resource Manager di avvio rapido di DevTest Labs](https://github.com/Azure/azure-devtestlab/tree/master/ARMTemplates)</span><span class="sxs-lookup"><span data-stu-id="4af1b-139">Explore the [DevTest Labs Azure Resource Manager QuickStart template gallery](https://github.com/Azure/azure-devtestlab/tree/master/ARMTemplates)</span></span>
