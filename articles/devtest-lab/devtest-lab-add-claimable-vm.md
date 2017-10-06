---
title: un laboratorio tooa claimable VM Azure DevTest Labs aaaAdd | Documenti Microsoft
description: Informazioni su come tooadd un lab tooa claimable macchina virtuale in Azure DevTest Labs
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
ms.openlocfilehash: fe6385ae2e59b9636b82aec250dc3a1f8a40ba5d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-claimable-vm-tooa-lab-in-azure-devtest-labs"></a><span data-ttu-id="c5afe-103">Aggiungere un ambiente lab claimable tooa VM in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="c5afe-103">Add a claimable VM tooa lab in Azure DevTest Labs</span></span>
<span data-ttu-id="c5afe-104">Si aggiunge un claimable lab tooa macchina virtuale in un simile toohow modo si [aggiungere una macchina virtuale standard](devtest-lab-add-vm.md) : da un *base* in un [immagine personalizzata](devtest-lab-create-template.md), [formula](devtest-lab-manage-formulas.md), o [un'immagine del Marketplace](devtest-lab-configure-marketplace-images.md).</span><span class="sxs-lookup"><span data-stu-id="c5afe-104">You add a claimable VM tooa lab in a similar manner toohow you [add a standard VM](devtest-lab-add-vm.md) – from a *base* that is either a [custom image](devtest-lab-create-template.md), [formula](devtest-lab-manage-formulas.md), or [Marketplace image](devtest-lab-configure-marketplace-images.md).</span></span> <span data-ttu-id="c5afe-105">In questa esercitazione illustra hello tooadd portale Azure utilizzando un laboratorio VM tooa claimable di DevTest Labs e illustra il processo di hello di che un utente avrà seguito tooclaim hello VM.</span><span class="sxs-lookup"><span data-stu-id="c5afe-105">This tutorial walks you through using hello Azure portal tooadd a claimable VM tooa lab in DevTest Labs, and shows hello process a user follows tooclaim hello VM.</span></span>

> [!NOTE]
> <span data-ttu-id="c5afe-106">Se si distribuiscono le macchine virtuali lab tramite [modelli di gestione risorse di Azure](devtest-lab-create-environment-from-arm.md), è possibile creare macchine virtuali claimable impostazione hello **allowClaim** tootrue proprietà nella sezione proprietà hello.</span><span class="sxs-lookup"><span data-stu-id="c5afe-106">If you deploy lab VMs through [Azure Resource Manager templates](devtest-lab-create-environment-from-arm.md), you can create claimable VMs by setting hello **allowClaim** property tootrue in hello properties section.</span></span>
>
>

## <a name="steps-tooadd-a-claimable-vm-tooa-lab-in-azure-devtest-labs"></a><span data-ttu-id="c5afe-107">Passaggi tooadd un laboratorio tooa claimable VM Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="c5afe-107">Steps tooadd a claimable VM tooa lab in Azure DevTest Labs</span></span>
1. <span data-ttu-id="c5afe-108">Accedi toohello [portale di Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="c5afe-108">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
1. <span data-ttu-id="c5afe-109">Selezionare **più servizi**, quindi selezionare **DevTest Labs** dall'elenco di hello.</span><span class="sxs-lookup"><span data-stu-id="c5afe-109">Select **More Services**, and then select **DevTest Labs** from hello list.</span></span>
1. <span data-ttu-id="c5afe-110">Selezionare lab hello hello elenco di esercitazioni in cui si desidera toocreate hello claimable macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="c5afe-110">From hello list of labs, select hello lab in which you want toocreate hello claimable VM.</span></span>  
1. <span data-ttu-id="c5afe-111">Nel lab di hello **Panoramica** pannello seleziona **+ Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="c5afe-111">On hello lab's **Overview** blade, select **+ Add**.</span></span>  

    ![Pulsante Aggiungi VM](./media/devtest-lab-add-vm/devtestlab-home-blade-add-vm.png)

1. <span data-ttu-id="c5afe-113">In hello **scegliere una base** pannello, selezionare un valore di base per hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="c5afe-113">On hello **Choose a base** blade, select a base for hello VM.</span></span>
1. <span data-ttu-id="c5afe-114">In hello **macchina virtuale** pannello, immettere un nome per la macchina virtuale nuova hello in hello **nome della macchina virtuale** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="c5afe-114">On hello **Virtual machine** blade, enter a name for hello new virtual machine in hello **Virtual machine name** text box.</span></span>

    ![Pannello Lab VM (VM lab)](./media/devtest-lab-add-vm/devtestlab-lab-vm-blade.png)

1. <span data-ttu-id="c5afe-116">Immettere un **nome utente** che vengono concessi privilegi di amministratore nella macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="c5afe-116">Enter a **User Name** that is granted administrator privileges on hello virtual machine.</span></span>  
1. <span data-ttu-id="c5afe-117">Se si desidera toouse una password archiviati nel [archivio segreto](https://azure.microsoft.com/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store)selezionare **utilizzano un segreto salvato**e specificare un valore di chiave corrispondente tooyour segreto (password).</span><span class="sxs-lookup"><span data-stu-id="c5afe-117">If you want toouse a password stored in your [secret store](https://azure.microsoft.com/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store), select **Use a saved secret**, and specify a key value that corresponds tooyour secret (password).</span></span> <span data-ttu-id="c5afe-118">In caso contrario, immettere una password nel campo di testo hello etichettata **digitare un valore**.</span><span class="sxs-lookup"><span data-stu-id="c5afe-118">Otherwise, enter a password in hello text field labeled **Type a value**.</span></span>
1. <span data-ttu-id="c5afe-119">Hello **il tipo di disco di macchina virtuale** determina il tipo di disco di archiviazione è consentito per le macchine virtuali hello in lab hello.</span><span class="sxs-lookup"><span data-stu-id="c5afe-119">hello **Virtual machine disk type** determines which storage disk type is allowed for hello virtual machines in hello lab.</span></span>
1. <span data-ttu-id="c5afe-120">Selezionare **dimensioni della macchina virtuale** e selezionare una delle hello predefiniti elementi che specificano le dimensioni del disco rigido hello di hello VM toocreate core del processore hello e dimensioni della RAM.</span><span class="sxs-lookup"><span data-stu-id="c5afe-120">Select **Virtual machine size** and select one of hello predefined items that specify hello processor cores, RAM size, and hello hard drive size of hello VM toocreate.</span></span>
1. <span data-ttu-id="c5afe-121">Selezionare **elementi** e hello elenco di elementi, selezionare e configurare hello elementi che si desidera tooadd toohello immagine di base.</span><span class="sxs-lookup"><span data-stu-id="c5afe-121">Select **Artifacts** and from hello list of artifacts, select and configure hello artifacts that you want tooadd toohello base image.</span></span> <span data-ttu-id="c5afe-122">Se si è nuovo tooDevTest Labs o configurazione degli elementi, vedere toohello [aggiungere un tooa artefatto esistente VM](devtest-lab-add-vm.md#add-an-existing-artifact-to-a-vm) sezione e quindi tornare qui al termine.</span><span class="sxs-lookup"><span data-stu-id="c5afe-122">If you're new tooDevTest Labs or configuring artifacts, refer toohello [Add an existing artifact tooa VM](devtest-lab-add-vm.md#add-an-existing-artifact-to-a-vm) section, and then return here when finished.</span></span>
1. <span data-ttu-id="c5afe-123">Selezionare **impostazioni avanzate** opzioni di scadenza e le opzioni di rete della macchina virtuale di tooconfigure hello.</span><span class="sxs-lookup"><span data-stu-id="c5afe-123">Select **Advanced settings** tooconfigure hello VM's network options and expiration options.</span></span> <span data-ttu-id="c5afe-124">In **attestazione opzioni**, scegliere **Sì** macchina hello toomake claimable.</span><span class="sxs-lookup"><span data-stu-id="c5afe-124">Under **Claim options**, choose **Yes** toomake hello machine claimable.</span></span>

  ![Scegliere toomake hello claimable macchina virtuale.](./media/devtest-lab-add-vm/devtestlab-claim-VM-option.png)

1. <span data-ttu-id="c5afe-126">Se si desidera tooview o copiare il modello di gestione risorse di Azure hello, fare riferimento toohello [modello salvare Azure Resource Manager](devtest-lab-add-vm.md#save-azure-resource-manager-template) sezione e tornare qui al termine.</span><span class="sxs-lookup"><span data-stu-id="c5afe-126">If you want tooview or copy hello Azure Resource Manager template, refer toohello [Save Azure Resource Manager template](devtest-lab-add-vm.md#save-azure-resource-manager-template) section, and return here when finished.</span></span>
1. <span data-ttu-id="c5afe-127">Selezionare **crea** tooadd hello specificato lab toohello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="c5afe-127">Select **Create** tooadd hello specified VM toohello lab.</span></span>
1. <span data-ttu-id="c5afe-128">Pannello lab Hello Visualizza lo stato di hello della creazione della macchina virtuale di hello - innanzitutto come **creazione**, quindi come **esecuzione** dopo hello macchina virtuale è stata avviata.</span><span class="sxs-lookup"><span data-stu-id="c5afe-128">hello lab blade displays hello status of hello VM's creation - first as **Creating**, then as **Running** after hello VM has been started.</span></span>


## <a name="using-a-claimable-vm"></a><span data-ttu-id="c5afe-129">Usare una macchina virtuale a disposizione degli utenti</span><span class="sxs-lookup"><span data-stu-id="c5afe-129">Using a claimable VM</span></span>

<span data-ttu-id="c5afe-130">Un utente può richiedere qualsiasi macchina virtuale dall'elenco di hello di "Macchine virtuali Claimable" effettuando una delle operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="c5afe-130">A user can claim any VM from hello list of "Claimable virtual machines" by doing one of these steps:</span></span>

* <span data-ttu-id="c5afe-131">Elenco di hello di "Macchine virtuali Claimable" nella parte inferiore di hello del pannello della panoramica del lab hello, fare clic su una delle macchine virtuali di hello nell'elenco di hello e scegliere **macchina attestazione**.</span><span class="sxs-lookup"><span data-stu-id="c5afe-131">From hello list of "Claimable virtual machines" at hello bottom of hello lab's Overview blade, right-click on one of hello VMs in hello list and choose **Claim machine**.</span></span>

 ![Richiedere una specifica macchina virtuale a disposizione degli utenti.](./media/devtest-lab-add-vm/devtestlab-claim-VM.png)


* <span data-ttu-id="c5afe-133">Nella parte superiore di hello di hello **Panoramica** pannello, scegliere **qualsiasi attestazione**.</span><span class="sxs-lookup"><span data-stu-id="c5afe-133">At hello top of hello **Overview** blade, choose **Claim any**.</span></span> <span data-ttu-id="c5afe-134">Una macchina virtuale casuale viene assegnata dall'elenco di hello di claimable macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="c5afe-134">A random virtual machine is assigned from hello list of claimable VMs.</span></span>

 ![Richiedere una macchina virtuale a disposizione degli utenti.](./media/devtest-lab-add-vm/devtestlab-claim-any.png)


<span data-ttu-id="c5afe-136">Quando una macchina virtuale viene richiesta da un utente, questa viene spostata in alto nell'elenco "My virtual machines" (Le mie macchine virtuali) e non è più disponibile per un altro utente.</span><span class="sxs-lookup"><span data-stu-id="c5afe-136">After a user claims a VM, it is moved up into their list of "My virtual machines" and is no longer claimable by any other user.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c5afe-137">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c5afe-137">Next steps</span></span>
* <span data-ttu-id="c5afe-138">Una volta hello VM è stato creato, è possibile connettersi toohello VM selezionando **Connetti** nel pannello hello della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="c5afe-138">Once hello VM has been created, you can connect toohello VM by selecting **Connect** on hello VM's blade.</span></span>
* <span data-ttu-id="c5afe-139">Esplorare hello [raccolta di modelli di DevTest Labs Azure Resource Manager QuickStart](https://github.com/Azure/azure-devtestlab/tree/master/ARMTemplates)</span><span class="sxs-lookup"><span data-stu-id="c5afe-139">Explore hello [DevTest Labs Azure Resource Manager QuickStart template gallery](https://github.com/Azure/azure-devtestlab/tree/master/ARMTemplates)</span></span>
