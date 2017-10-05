---
title: Creare la prima macchina virtuale in Azure DevTest Labs | Microsoft Docs
description: Informazioni su come creare una macchina virtuale in un lab in Azure DevTest Labs
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
ms.openlocfilehash: aa6b60b799e1e98815cf288d5612f98cd77cc00e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-your-first-vm-in-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="c461f-103">Creare la prima macchina virtuale in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="c461f-103">Create your first VM in a lab in Azure DevTest Labs</span></span>

<span data-ttu-id="c461f-104">Quando si accede inizialmente a DevTest Labs e si intende creare la prima macchina virtuale, questa operazione avverrà tramite un'[immagine del marketplace base](devtest-lab-configure-marketplace-images.md) precaricata.</span><span class="sxs-lookup"><span data-stu-id="c461f-104">When you initially access DevTest Labs and want to create your first VM, you will likely do so using a pre-loaded [base marketplace image](devtest-lab-configure-marketplace-images.md).</span></span> <span data-ttu-id="c461f-105">In un secondo momento durante la creazione di altre macchine virtuali sarà possibile scegliere da un [immagine personalizzata e una formula](devtest-lab-add-vm.md).</span><span class="sxs-lookup"><span data-stu-id="c461f-105">Later on, you'll also be able to choose from a [custom image and a formula](devtest-lab-add-vm.md) when creating more VMs.</span></span> 

<span data-ttu-id="c461f-106">Questa esercitazione illustra l'uso del portale di Azure per aggiungere la prima macchina virtuale in un lab in DevTest Labs.</span><span class="sxs-lookup"><span data-stu-id="c461f-106">This tutorial walks you through using the Azure portal to add your first VM to a lab in DevTest Labs.</span></span>

## <a name="steps-to-add-your-first-vm-to-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="c461f-107">Passaggi per aggiungere la prima macchina virtuale a un lab in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="c461f-107">Steps to add your first VM to a lab in Azure DevTest Labs</span></span>
1. <span data-ttu-id="c461f-108">Accedere al [portale di Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="c461f-108">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
1. <span data-ttu-id="c461f-109">Selezionare **Altri servizi** e quindi **DevTest Labs** dall'elenco.</span><span class="sxs-lookup"><span data-stu-id="c461f-109">Select **More Services**, and then select **DevTest Labs** from the list.</span></span>
1. <span data-ttu-id="c461f-110">Nell'elenco di lab selezionare il lab in cui si vuole creare la nuova VM.</span><span class="sxs-lookup"><span data-stu-id="c461f-110">From the list of labs, select the lab in which you want to create the VM.</span></span>  
1. <span data-ttu-id="c461f-111">Nel pannello **Panoramica** del lab selezionare **+ Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="c461f-111">On the lab's **Overview** blade, select **+ Add**.</span></span>  

    ![Pulsante Aggiungi VM](./media/devtest-lab-add-vm/devtestlab-home-blade-add-vm.png)

1. <span data-ttu-id="c461f-113">Nel pannello **Scegli una base** selezionare un'immagine del marketplace per la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="c461f-113">On the **Choose a base** blade, select a marketplace image for the VM.</span></span>
1. <span data-ttu-id="c461f-114">Nel pannello **Macchina virtuale** immettere un nome per la nuova macchina virtuale nella casella di testo **Nome macchina virtuale**.</span><span class="sxs-lookup"><span data-stu-id="c461f-114">On the **Virtual machine** blade, enter a name for the new virtual machine in the **Virtual machine name** text box.</span></span>

    ![Pannello Lab VM (VM lab)](./media/devtest-lab-add-vm/devtestlab-lab-add-first-vm.png)

1. <span data-ttu-id="c461f-116">Immettere un **Nome utente** a cui vengono concessi privilegi di amministratore nella macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="c461f-116">Enter a **User Name** that is granted administrator privileges on the virtual machine.</span></span>  
1. <span data-ttu-id="c461f-117">Immettere una password nel campo di testo **Digita un valore**.</span><span class="sxs-lookup"><span data-stu-id="c461f-117">Enter a password in the text field labeled **Type a value**.</span></span>
1. <span data-ttu-id="c461f-118">Il **tipo di disco della macchina virtuale** determina il tipo di disco di archiviazione consentito per le macchine virtuali nel lab.</span><span class="sxs-lookup"><span data-stu-id="c461f-118">The **Virtual machine disk type** determines which storage disk type is allowed for the virtual machines in the lab.</span></span>
1. <span data-ttu-id="c461f-119">Selezionare **Dimensioni macchina virtuale** e uno degli elementi predefiniti che specificano le memorie centrali del processore, la dimensione della RAM e le dimensioni dell'unità disco rigido della VM da creare.</span><span class="sxs-lookup"><span data-stu-id="c461f-119">Select **Virtual machine size** and select one of the predefined items that specify the processor cores, RAM size, and the hard drive size of the VM to create.</span></span>
1. <span data-ttu-id="c461f-120">Selezionare **Elementi** e dall'elenco di elementi selezionare e configurare gli elementi da aggiungere all'immagine di base.</span><span class="sxs-lookup"><span data-stu-id="c461f-120">Select **Artifacts** and - from the list of artifacts - select and configure the artifacts that you want to add to the base image.</span></span>
    <span data-ttu-id="c461f-121">**Nota:** se non si ha familiarità con DevTest Labs o con la configurazione di elementi, vedere la sezione [Aggiungere un elemento esistente in una macchina virtuale](./devtest-lab-add-vm.md#add-an-existing-artifact-to-a-vm) e tornare qui al termine dell'operazione.</span><span class="sxs-lookup"><span data-stu-id="c461f-121">**Note:** If you're new to DevTest Labs or configuring artifacts, refer to the [Add an existing artifact to a VM](./devtest-lab-add-vm.md#add-an-existing-artifact-to-a-vm) section, and then return here when finished.</span></span>
1. <span data-ttu-id="c461f-122">Selezionare **Crea** per aggiungere la macchina virtuale specificata al lab.</span><span class="sxs-lookup"><span data-stu-id="c461f-122">Select **Create** to add the specified VM to the lab.</span></span>

   <span data-ttu-id="c461f-123">Il pannello lab consente di visualizzare lo stato di creazione della VM prima come **Creazione**, poi come **Esecuzione** dopo aver avviato la VM.</span><span class="sxs-lookup"><span data-stu-id="c461f-123">The lab blade displays the status of the VM's creation - first as **Creating**, then as **Running** after the VM has been started.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c461f-124">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c461f-124">Next steps</span></span>
* <span data-ttu-id="c461f-125">Dopo avere creato la VM, è possibile connettersi ad essa selezionando **Connetti** nel pannello della VM.</span><span class="sxs-lookup"><span data-stu-id="c461f-125">Once the VM has been created, you can connect to the VM by selecting **Connect** on the VM's blade.</span></span>
* <span data-ttu-id="c461f-126">Vedere [Aggiungere una macchina virtuale a un lab](devtest-lab-add-vm.md) per informazioni più complete sull'aggiunta di successive macchine virtuali nel lab.</span><span class="sxs-lookup"><span data-stu-id="c461f-126">Check out [Add a VM to a lab](devtest-lab-add-vm.md) for more complete info about adding subsequent VMs in your lab.</span></span>
* <span data-ttu-id="c461f-127">Esplorare la [raccolta dei modelli di avvio rapido di Azure Resource Manager di DevTest Labs](https://github.com/Azure/azure-devtestlab/tree/master/ARMTemplates).</span><span class="sxs-lookup"><span data-stu-id="c461f-127">Explore the [DevTest Labs Azure Resource Manager QuickStart template gallery](https://github.com/Azure/azure-devtestlab/tree/master/ARMTemplates).</span></span>
