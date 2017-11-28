---
title: un'immagine personalizzata Azure DevTest Labs da un file VHD aaaCreate | Documenti Microsoft
description: Informazioni su come un'immagine personalizzata in Azure DevTest Labs da un file di disco rigido virtuale tramite toocreate hello portale di Azure
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: b795bc61-7c28-40e6-82fc-96d629ee0568
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/10/2017
ms.author: tarcher
ms.openlocfilehash: 80af8ea1cb72380f868df0a76c4a0dcd92e63cf5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-image-from-a-vhd-file"></a><span data-ttu-id="57a40-103">Creare un'immagine personalizzata da un file VHD</span><span class="sxs-lookup"><span data-stu-id="57a40-103">Create a custom image from a VHD file</span></span>

[!INCLUDE [devtest-lab-create-custom-image-from-vhd-selector](../../includes/devtest-lab-create-custom-image-from-vhd-selector.md)]

[!INCLUDE [devtest-lab-custom-image-definition](../../includes/devtest-lab-custom-image-definition.md)]

[!INCLUDE [devtest-lab-upload-vhd-options](../../includes/devtest-lab-upload-vhd-options.md)]

## <a name="step-by-step-instructions"></a><span data-ttu-id="57a40-104">Istruzioni dettagliate</span><span class="sxs-lookup"><span data-stu-id="57a40-104">Step-by-step instructions</span></span>

<span data-ttu-id="57a40-105">Hello passaggi seguenti consentono di eseguire la creazione di un'immagine personalizzata da un file VHD utilizzando hello portale di Azure:</span><span class="sxs-lookup"><span data-stu-id="57a40-105">hello following steps walk you through creating a custom image from a VHD file using hello Azure portal:</span></span>

1. <span data-ttu-id="57a40-106">Accedi toohello [portale di Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="57a40-106">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="57a40-107">Selezionare **più servizi**, quindi selezionare **DevTest Labs** dall'elenco di hello.</span><span class="sxs-lookup"><span data-stu-id="57a40-107">Select **More services**, and then select **DevTest Labs** from hello list.</span></span>

1. <span data-ttu-id="57a40-108">Elenco dei laboratori hello selezionare lab desiderato hello.</span><span class="sxs-lookup"><span data-stu-id="57a40-108">From hello list of labs, select hello desired lab.</span></span>  

1. <span data-ttu-id="57a40-109">Nel pannello del lab hello, selezionare **configurazione**.</span><span class="sxs-lookup"><span data-stu-id="57a40-109">On hello lab's blade, select **Configuration**.</span></span> 

1. <span data-ttu-id="57a40-110">Lab hello **configurazione** pannello seleziona **immagini personalizzate (VHD)**.</span><span class="sxs-lookup"><span data-stu-id="57a40-110">On hello lab **Configuration** blade, select **Custom images (VHDs)**.</span></span>

1. <span data-ttu-id="57a40-111">In hello **immagini personalizzate** pannello seleziona **+ Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="57a40-111">On hello **Custom images** blade, select **+Add**.</span></span>

    ![Aggiungere un'immagine personalizzata](./media/devtest-lab-create-template/add-custom-image.png)

1. <span data-ttu-id="57a40-113">Immettere il nome di hello dell'immagine personalizzata hello.</span><span class="sxs-lookup"><span data-stu-id="57a40-113">Enter hello name of hello custom image.</span></span> <span data-ttu-id="57a40-114">Questo nome viene visualizzato nell'elenco di hello di immagini di base durante la creazione di una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="57a40-114">This name is displayed in hello list of base images when creating a VM.</span></span>

1. <span data-ttu-id="57a40-115">Immettere una descrizione hello dell'immagine personalizzata hello.</span><span class="sxs-lookup"><span data-stu-id="57a40-115">Enter hello description of hello custom image.</span></span> <span data-ttu-id="57a40-116">Questa descrizione viene visualizzata nell'elenco di hello di immagini di base durante la creazione di una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="57a40-116">This description is displayed in hello list of base images when creating a VM.</span></span>

1. <span data-ttu-id="57a40-117">Selezionare **VHD**.</span><span class="sxs-lookup"><span data-stu-id="57a40-117">Select **VHD**.</span></span>

1. <span data-ttu-id="57a40-118">Da hello **VHD** pannello, il file di disco rigido virtuale selezionare hello desiderato.</span><span class="sxs-lookup"><span data-stu-id="57a40-118">From hello **VHD** blade, select hello desired VHD file.</span></span>

1. <span data-ttu-id="57a40-119">Selezionare **OK** tooclose hello **VHD** blade.</span><span class="sxs-lookup"><span data-stu-id="57a40-119">Select **OK** tooclose hello **VHD** blade.</span></span>

1. <span data-ttu-id="57a40-120">Selezionare **Configurazione sistema operativo**.</span><span class="sxs-lookup"><span data-stu-id="57a40-120">Select **OS configuration**.</span></span>

1. <span data-ttu-id="57a40-121">In hello **configurazione del sistema operativo** scheda, selezionare l'opzione **Windows** o **Linux**.</span><span class="sxs-lookup"><span data-stu-id="57a40-121">On hello **OS configuration** tab, select either **Windows** or **Linux**.</span></span>

1. <span data-ttu-id="57a40-122">Se **Windows** è selezionata, specificare tramite la casella di controllo di hello se *Sysprep* è stato eseguito nel computer di hello.</span><span class="sxs-lookup"><span data-stu-id="57a40-122">If **Windows** is selected, specify via hello checkbox whether *Sysprep* has been run on hello machine.</span></span> 

1. <span data-ttu-id="57a40-123">Selezionare **OK** tooclose hello **configurazione del sistema operativo** blade.</span><span class="sxs-lookup"><span data-stu-id="57a40-123">Select **OK** tooclose hello **OS configuration** blade.</span></span>

1. <span data-ttu-id="57a40-124">Selezionare **OK** toocreate immagine personalizzata di hello.</span><span class="sxs-lookup"><span data-stu-id="57a40-124">Select **OK** toocreate hello custom image.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a><span data-ttu-id="57a40-125">Post di blog correlati</span><span class="sxs-lookup"><span data-stu-id="57a40-125">Related blog posts</span></span>

- [<span data-ttu-id="57a40-126">Custom images or formulas? (Immagini personalizzate o formule?)</span><span class="sxs-lookup"><span data-stu-id="57a40-126">Custom images or formulas?</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)
- [<span data-ttu-id="57a40-127">Copying Custom Images between Azure DevTest Labs (Copia di immagini personalizzate tra istanze di Azure DevTest Labs)</span><span class="sxs-lookup"><span data-stu-id="57a40-127">Copying Custom Images between Azure DevTest Labs</span></span>](http://www.visualstudiogeeks.com/blog/DevOps/How-To-Move-CustomImages-VHD-Between-AzureDevTestLabs#copying-custom-images-between-azure-devtest-labs)

##<a name="next-steps"></a><span data-ttu-id="57a40-128">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="57a40-128">Next steps</span></span>

- [<span data-ttu-id="57a40-129">Aggiungere un ambiente lab tooyour VM</span><span class="sxs-lookup"><span data-stu-id="57a40-129">Add a VM tooyour lab</span></span>](./devtest-lab-add-vm-with-artifacts.md)
