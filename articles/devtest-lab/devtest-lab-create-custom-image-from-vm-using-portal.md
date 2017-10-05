---
title: Creare un'immagine personalizzata di Azure DevTest Labs da una VM | Documentazione Microsoft
description: Informazioni su come creare un'immagine personalizzata in Azure DevTest Labs da una VM predisposta usando il portale di Azure
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/10/2017
ms.author: tarcher
ms.openlocfilehash: 9d2dcf7164985508d691e8a0c123efaf3b8aa19a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-custom-image-from-a-vm"></a><span data-ttu-id="056f1-103">Creare un'immagine personalizzata da una VM</span><span class="sxs-lookup"><span data-stu-id="056f1-103">Create a custom image from a VM</span></span>

[!INCLUDE [devtest-lab-custom-image-definition](../../includes/devtest-lab-custom-image-definition.md)]

## <a name="step-by-step-instructions"></a><span data-ttu-id="056f1-104">Istruzioni dettagliate</span><span class="sxs-lookup"><span data-stu-id="056f1-104">Step-by-step instructions</span></span>

<span data-ttu-id="056f1-105">È possibile creare un'immagine personalizzata da una macchina virtuale predisposta e successivamente utilizzare tale immagine per creare macchine virtuali identiche.</span><span class="sxs-lookup"><span data-stu-id="056f1-105">You can create a custom image from a provisioned VM, and afterwards use that custom image to create identical VMs.</span></span> <span data-ttu-id="056f1-106">I passaggi seguenti illustrano come creare un'immagine personalizzata da una macchina virtuale:</span><span class="sxs-lookup"><span data-stu-id="056f1-106">The following steps illustrate how to create a custom image from a VM:</span></span>

1. <span data-ttu-id="056f1-107">Accedere al [portale di Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="056f1-107">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="056f1-108">Selezionare **Altri servizi** e quindi **DevTest Labs** dall'elenco.</span><span class="sxs-lookup"><span data-stu-id="056f1-108">Select **More services**, and then select **DevTest Labs** from the list.</span></span>

1. <span data-ttu-id="056f1-109">Nell'elenco dei lab selezionare il lab desiderato.</span><span class="sxs-lookup"><span data-stu-id="056f1-109">From the list of labs, select the desired lab.</span></span>  

1. <span data-ttu-id="056f1-110">Nel pannello del lab selezionare **My virtual machines**(Macchine virtuali personali).</span><span class="sxs-lookup"><span data-stu-id="056f1-110">On the lab's blade, select **My virtual machines**.</span></span>
 
1. <span data-ttu-id="056f1-111">Nel pannello **My virtual machines** (Macchine virtuali personali) del lab selezionare la VM da cui creare l'immagine personalizzata.</span><span class="sxs-lookup"><span data-stu-id="056f1-111">On the **My virtual machines** blade, select the VM from which you want to create the custom image.</span></span>

1. <span data-ttu-id="056f1-112">Nel pannello della macchina virtuale selezionare **Crea immagine personalizzata (disco rigido virtuale)**.</span><span class="sxs-lookup"><span data-stu-id="056f1-112">On the VM's blade, select **Create custom image (VHD)**.</span></span>

    ![Voce di menu Crea immagine personalizzata](./media/devtest-lab-create-template/create-custom-image.png)

1. <span data-ttu-id="056f1-114">Nel pannello **Immagine personalizzata** immettere un nome e una descrizione per l'immagine personalizzata.</span><span class="sxs-lookup"><span data-stu-id="056f1-114">On the **Create image** blade, enter a name and description for your custom image.</span></span> <span data-ttu-id="056f1-115">Queste informazioni vengono visualizzate nell'elenco delle immagini di base quando si crea una VM.</span><span class="sxs-lookup"><span data-stu-id="056f1-115">This information is displayed in the list of bases when you create a VM.</span></span>

    ![Pannello Crea immagine personalizzata](./media/devtest-lab-create-template/create-custom-image-blade.png)

1. <span data-ttu-id="056f1-117">Indicare se è stato eseguito sysprep nella macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="056f1-117">Select whether sysprep was run on the VM.</span></span> <span data-ttu-id="056f1-118">Se non è stato eseguito sysprep nella VM, specificare se si desidera eseguirlo quando si crea una VM da questa immagine personalizzata.</span><span class="sxs-lookup"><span data-stu-id="056f1-118">If the sysprep was not run on the VM, specify whether you want sysprep run when a VM is created from this custom image.</span></span>

1. <span data-ttu-id="056f1-119">Selezionare **OK** al termine per creare l'immagine personalizzata.</span><span class="sxs-lookup"><span data-stu-id="056f1-119">Select **OK** when finished to create the custom image.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a><span data-ttu-id="056f1-120">Post di blog correlati</span><span class="sxs-lookup"><span data-stu-id="056f1-120">Related blog posts</span></span>

- [<span data-ttu-id="056f1-121">Custom images or formulas? (Immagini personalizzate o formule?)</span><span class="sxs-lookup"><span data-stu-id="056f1-121">Custom images or formulas?</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)
- [<span data-ttu-id="056f1-122">Copying Custom Images between Azure DevTest Labs (Copia di immagini personalizzate tra istanze di Azure DevTest Labs)</span><span class="sxs-lookup"><span data-stu-id="056f1-122">Copying Custom Images between Azure DevTest Labs</span></span>](http://www.visualstudiogeeks.com/blog/DevOps/How-To-Move-CustomImages-VHD-Between-AzureDevTestLabs#copying-custom-images-between-azure-devtest-labs)

##<a name="next-steps"></a><span data-ttu-id="056f1-123">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="056f1-123">Next steps</span></span>

- [<span data-ttu-id="056f1-124">Aggiungere una macchina virtuale al lab</span><span class="sxs-lookup"><span data-stu-id="056f1-124">Add a VM to your lab</span></span>](./devtest-lab-add-vm-with-artifacts.md)
