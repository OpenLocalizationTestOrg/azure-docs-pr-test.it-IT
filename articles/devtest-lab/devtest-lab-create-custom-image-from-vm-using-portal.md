---
title: un'immagine personalizzata da una macchina virtuale Azure DevTest Labs in aaaCreate | Documenti Microsoft
description: Informazioni su come un'immagine personalizzata in Azure DevTest Labs da una macchina virtuale con provisioning toocreate hello portale di Azure
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
ms.openlocfilehash: 7dccb79d3db4aae676c7bd2f6b800301210491e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-image-from-a-vm"></a><span data-ttu-id="a9576-103">Creare un'immagine personalizzata da una VM</span><span class="sxs-lookup"><span data-stu-id="a9576-103">Create a custom image from a VM</span></span>

[!INCLUDE [devtest-lab-custom-image-definition](../../includes/devtest-lab-custom-image-definition.md)]

## <a name="step-by-step-instructions"></a><span data-ttu-id="a9576-104">Istruzioni dettagliate</span><span class="sxs-lookup"><span data-stu-id="a9576-104">Step-by-step instructions</span></span>

<span data-ttu-id="a9576-105">È possibile creare un'immagine personalizzata da una macchina virtuale di provisioning e successivamente usare tale toocreate immagine personalizzata macchine virtuali identiche.</span><span class="sxs-lookup"><span data-stu-id="a9576-105">You can create a custom image from a provisioned VM, and afterwards use that custom image toocreate identical VMs.</span></span> <span data-ttu-id="a9576-106">Hello alla procedura seguente viene illustrato come toocreate immagine personalizzata da una macchina virtuale:</span><span class="sxs-lookup"><span data-stu-id="a9576-106">hello following steps illustrate how toocreate a custom image from a VM:</span></span>

1. <span data-ttu-id="a9576-107">Accedi toohello [portale di Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="a9576-107">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="a9576-108">Selezionare **più servizi**, quindi selezionare **DevTest Labs** dall'elenco di hello.</span><span class="sxs-lookup"><span data-stu-id="a9576-108">Select **More services**, and then select **DevTest Labs** from hello list.</span></span>

1. <span data-ttu-id="a9576-109">Elenco dei laboratori hello selezionare lab desiderato hello.</span><span class="sxs-lookup"><span data-stu-id="a9576-109">From hello list of labs, select hello desired lab.</span></span>  

1. <span data-ttu-id="a9576-110">Nel pannello del lab hello, selezionare **macchine virtuali**.</span><span class="sxs-lookup"><span data-stu-id="a9576-110">On hello lab's blade, select **My virtual machines**.</span></span>
 
1. <span data-ttu-id="a9576-111">In hello **macchine virtuali** pannello selezionare hello VM da cui si desidera toocreate immagine personalizzata di hello.</span><span class="sxs-lookup"><span data-stu-id="a9576-111">On hello **My virtual machines** blade, select hello VM from which you want toocreate hello custom image.</span></span>

1. <span data-ttu-id="a9576-112">Nel pannello hello della macchina virtuale, selezionare **Crea immagine personalizzata (VHD)**.</span><span class="sxs-lookup"><span data-stu-id="a9576-112">On hello VM's blade, select **Create custom image (VHD)**.</span></span>

    ![Voce di menu Crea immagine personalizzata](./media/devtest-lab-create-template/create-custom-image.png)

1. <span data-ttu-id="a9576-114">In hello **Crea immagine** pannello, immettere un nome e una descrizione per l'immagine personalizzata.</span><span class="sxs-lookup"><span data-stu-id="a9576-114">On hello **Create image** blade, enter a name and description for your custom image.</span></span> <span data-ttu-id="a9576-115">Queste informazioni vengono visualizzate nell'elenco di hello di base quando si crea una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="a9576-115">This information is displayed in hello list of bases when you create a VM.</span></span>

    ![Pannello Crea immagine personalizzata](./media/devtest-lab-create-template/create-custom-image-blade.png)

1. <span data-ttu-id="a9576-117">Consente di indicare se è stato eseguito sysprep nella macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="a9576-117">Select whether sysprep was run on hello VM.</span></span> <span data-ttu-id="a9576-118">Se non è stato eseguito sysprep hello in hello macchina virtuale, specificare se si desidera eseguire quando una macchina virtuale viene creata da questa immagine personalizzata di sysprep.</span><span class="sxs-lookup"><span data-stu-id="a9576-118">If hello sysprep was not run on hello VM, specify whether you want sysprep run when a VM is created from this custom image.</span></span>

1. <span data-ttu-id="a9576-119">Selezionare **OK** quando toocreate termine hello immagine personalizzata.</span><span class="sxs-lookup"><span data-stu-id="a9576-119">Select **OK** when finished toocreate hello custom image.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a><span data-ttu-id="a9576-120">Post di blog correlati</span><span class="sxs-lookup"><span data-stu-id="a9576-120">Related blog posts</span></span>

- [<span data-ttu-id="a9576-121">Custom images or formulas? (Immagini personalizzate o formule?)</span><span class="sxs-lookup"><span data-stu-id="a9576-121">Custom images or formulas?</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)
- [<span data-ttu-id="a9576-122">Copying Custom Images between Azure DevTest Labs (Copia di immagini personalizzate tra istanze di Azure DevTest Labs)</span><span class="sxs-lookup"><span data-stu-id="a9576-122">Copying Custom Images between Azure DevTest Labs</span></span>](http://www.visualstudiogeeks.com/blog/DevOps/How-To-Move-CustomImages-VHD-Between-AzureDevTestLabs#copying-custom-images-between-azure-devtest-labs)

##<a name="next-steps"></a><span data-ttu-id="a9576-123">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a9576-123">Next steps</span></span>

- [<span data-ttu-id="a9576-124">Aggiungere un ambiente lab tooyour VM</span><span class="sxs-lookup"><span data-stu-id="a9576-124">Add a VM tooyour lab</span></span>](./devtest-lab-add-vm-with-artifacts.md)
