---
title: aaaCreate la prima macchina virtuale in un ambiente lab in Azure DevTest Labs | Documenti Microsoft
description: Informazioni su come toocreate prima macchina virtuale in un ambiente lab in Azure DevTest Labs
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: fbc5a438-6e02-4952-b654-b8fa7322ae5f
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/24/2017
ms.author: tarcher
ms.openlocfilehash: 4c3257efca9be6fdd190eaac1db731464e07fcfd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-vm-in-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="51249-103">Creare la prima macchina virtuale in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="51249-103">Create your first VM in a lab in Azure DevTest Labs</span></span>

<span data-ttu-id="51249-104">Quando si inizialmente accedere DevTest Labs e toocreate la prima macchina virtuale, probabilmente a tale scopo, utilizzando una pre-caricato [un'immagine del marketplace base](devtest-lab-configure-marketplace-images.md).</span><span class="sxs-lookup"><span data-stu-id="51249-104">When you initially access DevTest Labs and want toocreate your first VM, you will likely do so using a pre-loaded [base marketplace image](devtest-lab-configure-marketplace-images.md).</span></span> <span data-ttu-id="51249-105">Successivamente, sarà anche in grado di toochoose da un [immagine personalizzata e una formula](devtest-lab-add-vm.md) durante la creazione di più macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="51249-105">Later on, you'll also be able toochoose from a [custom image and a formula](devtest-lab-add-vm.md) when creating more VMs.</span></span> 

<span data-ttu-id="51249-106">In questa esercitazione illustra utilizzando hello tooadd portale Azure nel lab di tooa prima macchina virtuale di DevTest Labs.</span><span class="sxs-lookup"><span data-stu-id="51249-106">This tutorial walks you through using hello Azure portal tooadd your first VM tooa lab in DevTest Labs.</span></span>

## <a name="steps-tooadd-your-first-vm-tooa-lab-in-azure-devtest-labs"></a><span data-ttu-id="51249-107">I passaggi tooadd il lab di tooa prima di VM in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="51249-107">Steps tooadd your first VM tooa lab in Azure DevTest Labs</span></span>
1. <span data-ttu-id="51249-108">Accedi toohello [portale di Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="51249-108">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
1. <span data-ttu-id="51249-109">Selezionare **più servizi**, quindi selezionare **DevTest Labs** dall'elenco di hello.</span><span class="sxs-lookup"><span data-stu-id="51249-109">Select **More Services**, and then select **DevTest Labs** from hello list.</span></span>
1. <span data-ttu-id="51249-110">Elenco dei laboratori hello selezionare lab hello in cui si desidera toocreate hello VM.</span><span class="sxs-lookup"><span data-stu-id="51249-110">From hello list of labs, select hello lab in which you want toocreate hello VM.</span></span>  
1. <span data-ttu-id="51249-111">Nel lab di hello **Panoramica** pannello seleziona **+ Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="51249-111">On hello lab's **Overview** blade, select **+ Add**.</span></span>  

    ![Pulsante Aggiungi VM](./media/devtest-lab-add-vm/devtestlab-home-blade-add-vm.png)

1. <span data-ttu-id="51249-113">In hello **scegliere una base** pannello Seleziona immagine un marketplace per hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="51249-113">On hello **Choose a base** blade, select a marketplace image for hello VM.</span></span>
1. <span data-ttu-id="51249-114">In hello **macchina virtuale** pannello, immettere un nome per la macchina virtuale nuova hello in hello **nome della macchina virtuale** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="51249-114">On hello **Virtual machine** blade, enter a name for hello new virtual machine in hello **Virtual machine name** text box.</span></span>

    ![Pannello Lab VM (VM lab)](./media/devtest-lab-add-vm/devtestlab-lab-add-first-vm.png)

1. <span data-ttu-id="51249-116">Immettere un **nome utente** che vengono concessi privilegi di amministratore nella macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="51249-116">Enter a **User Name** that is granted administrator privileges on hello virtual machine.</span></span>  
1. <span data-ttu-id="51249-117">Immettere una password nel campo di testo hello etichettata **digitare un valore**.</span><span class="sxs-lookup"><span data-stu-id="51249-117">Enter a password in hello text field labeled **Type a value**.</span></span>
1. <span data-ttu-id="51249-118">Hello **il tipo di disco di macchina virtuale** determina il tipo di disco di archiviazione è consentito per le macchine virtuali hello in lab hello.</span><span class="sxs-lookup"><span data-stu-id="51249-118">hello **Virtual machine disk type** determines which storage disk type is allowed for hello virtual machines in hello lab.</span></span>
1. <span data-ttu-id="51249-119">Selezionare **dimensioni della macchina virtuale** e selezionare una delle hello predefiniti elementi che specificano le dimensioni del disco rigido hello di hello VM toocreate core del processore hello e dimensioni della RAM.</span><span class="sxs-lookup"><span data-stu-id="51249-119">Select **Virtual machine size** and select one of hello predefined items that specify hello processor cores, RAM size, and hello hard drive size of hello VM toocreate.</span></span>
1. <span data-ttu-id="51249-120">Selezionare **elementi** e - hello elenco di elementi - selezionare e configurare hello elementi che si desidera tooadd toohello immagine di base.</span><span class="sxs-lookup"><span data-stu-id="51249-120">Select **Artifacts** and - from hello list of artifacts - select and configure hello artifacts that you want tooadd toohello base image.</span></span>
    <span data-ttu-id="51249-121">**Nota:** Labs tooDevTest nuovo o di configurazione degli elementi, fare riferimento toohello [aggiungere un tooa artefatto esistente VM](./devtest-lab-add-vm.md#add-an-existing-artifact-to-a-vm) sezione e quindi tornare qui al termine.</span><span class="sxs-lookup"><span data-stu-id="51249-121">**Note:** If you're new tooDevTest Labs or configuring artifacts, refer toohello [Add an existing artifact tooa VM](./devtest-lab-add-vm.md#add-an-existing-artifact-to-a-vm) section, and then return here when finished.</span></span>
1. <span data-ttu-id="51249-122">Selezionare **crea** tooadd hello specificato lab toohello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="51249-122">Select **Create** tooadd hello specified VM toohello lab.</span></span>

   <span data-ttu-id="51249-123">Pannello lab Hello Visualizza lo stato di hello della creazione della macchina virtuale di hello - innanzitutto come **creazione**, quindi come **esecuzione** dopo hello macchina virtuale è stata avviata.</span><span class="sxs-lookup"><span data-stu-id="51249-123">hello lab blade displays hello status of hello VM's creation - first as **Creating**, then as **Running** after hello VM has been started.</span></span>

## <a name="next-steps"></a><span data-ttu-id="51249-124">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="51249-124">Next steps</span></span>
* <span data-ttu-id="51249-125">Una volta hello VM è stato creato, è possibile connettersi toohello VM selezionando **Connetti** nel pannello hello della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="51249-125">Once hello VM has been created, you can connect toohello VM by selecting **Connect** on hello VM's blade.</span></span>
* <span data-ttu-id="51249-126">Estrarre [aggiungere un ambiente lab tooa VM](devtest-lab-add-vm.md) per informazioni più complete sull'aggiunta di macchine virtuali successive nell'ambiente lab.</span><span class="sxs-lookup"><span data-stu-id="51249-126">Check out [Add a VM tooa lab](devtest-lab-add-vm.md) for more complete info about adding subsequent VMs in your lab.</span></span>
* <span data-ttu-id="51249-127">Esplorare hello [raccolta di modelli di DevTest Labs Azure Resource Manager QuickStart](https://github.com/Azure/azure-devtestlab/tree/master/ARMTemplates).</span><span class="sxs-lookup"><span data-stu-id="51249-127">Explore hello [DevTest Labs Azure Resource Manager QuickStart template gallery](https://github.com/Azure/azure-devtestlab/tree/master/ARMTemplates).</span></span>
