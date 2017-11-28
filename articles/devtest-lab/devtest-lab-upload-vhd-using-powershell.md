---
title: disco rigido virtuale aaaUpload file tooAzure DevTest Labs tramite PowerShell | Documenti Microsoft
description: Caricare l'account di archiviazione del toolab file disco rigido virtuale con PowerShell
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
ms.openlocfilehash: 9c3ee96e212457b0ef8203714b419350cb97f895
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="upload-vhd-file-toolabs-storage-account-using-powershell"></a><span data-ttu-id="8ca6c-103">Caricare l'account di archiviazione del toolab file disco rigido virtuale con PowerShell</span><span class="sxs-lookup"><span data-stu-id="8ca6c-103">Upload VHD file toolab's storage account using PowerShell</span></span>

[!INCLUDE [devtest-lab-upload-vhd-selector](../../includes/devtest-lab-upload-vhd-selector.md)]

<span data-ttu-id="8ca6c-104">In Azure DevTest Labs, i file VHD possono essere utilizzato toocreate immagini personalizzate, che sono utilizzati tooprovision le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="8ca6c-104">In Azure DevTest Labs, VHD files can be used toocreate custom images, which are used tooprovision virtual machines.</span></span> <span data-ttu-id="8ca6c-105">Hello passaggi seguenti consentono l'utilizzo di PowerShell tooupload account di archiviazione del laboratorio di tooa file disco rigido virtuale.</span><span class="sxs-lookup"><span data-stu-id="8ca6c-105">hello following steps walk you through using PowerShell tooupload a VHD file tooa lab's storage account.</span></span> <span data-ttu-id="8ca6c-106">Dopo aver caricato il file VHD, hello [passaggi successivi sezione](#next-steps) elenca alcuni articoli che illustrano come un'immagine personalizzata da hello toocreate caricamento del file di disco rigido virtuale.</span><span class="sxs-lookup"><span data-stu-id="8ca6c-106">Once you've uploaded your VHD file, hello [Next steps section](#next-steps) lists some articles that illustrate how toocreate a custom image from hello uploaded VHD file.</span></span> <span data-ttu-id="8ca6c-107">Per altre informazioni sui dischi e sui dischi rigidi virtuali in Azure, vedere [Informazioni sui dischi e sui dischi rigidi virtuali per le macchine virtuali](../virtual-machines/linux/about-disks-and-vhds.md)</span><span class="sxs-lookup"><span data-stu-id="8ca6c-107">For more information about disks and VHDs in Azure, see [About disks and VHDs for virtual machines](../virtual-machines/linux/about-disks-and-vhds.md)</span></span>

## <a name="step-by-step-instructions"></a><span data-ttu-id="8ca6c-108">Istruzioni dettagliate</span><span class="sxs-lookup"><span data-stu-id="8ca6c-108">Step-by-step instructions</span></span>

<span data-ttu-id="8ca6c-109">esempio Hello passaggi di percorso di caricamento di un disco rigido virtuale del file tooAzure DevTest Labs tramite PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8ca6c-109">hello following steps walk you through uploading a VHD file tooAzure DevTest Labs using PowerShell.</span></span> 

1. <span data-ttu-id="8ca6c-110">Accedi toohello [portale di Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="8ca6c-110">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="8ca6c-111">Selezionare **più servizi**, quindi selezionare **DevTest Labs** dall'elenco di hello.</span><span class="sxs-lookup"><span data-stu-id="8ca6c-111">Select **More services**, and then select **DevTest Labs** from hello list.</span></span>

1. <span data-ttu-id="8ca6c-112">Elenco dei laboratori hello selezionare lab desiderato hello.</span><span class="sxs-lookup"><span data-stu-id="8ca6c-112">From hello list of labs, select hello desired lab.</span></span>  

1. <span data-ttu-id="8ca6c-113">Nel pannello del lab hello, selezionare **configurazione**.</span><span class="sxs-lookup"><span data-stu-id="8ca6c-113">On hello lab's blade, select **Configuration**.</span></span> 

1. <span data-ttu-id="8ca6c-114">Lab hello **configurazione** pannello seleziona **immagini personalizzate (VHD)**.</span><span class="sxs-lookup"><span data-stu-id="8ca6c-114">On hello lab **Configuration** blade, select **Custom images (VHDs)**.</span></span>

1. <span data-ttu-id="8ca6c-115">In hello **immagini personalizzate** pannello selezionare **+ Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="8ca6c-115">On hello **Custom images** blade, Select **+Add**.</span></span> 

1. <span data-ttu-id="8ca6c-116">In hello **immagine personalizzata** pannello seleziona **VHD**.</span><span class="sxs-lookup"><span data-stu-id="8ca6c-116">On hello **Custom image** blade, select **VHD**.</span></span>

1. <span data-ttu-id="8ca6c-117">In hello **VHD** pannello seleziona **caricare un disco rigido virtuale con PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="8ca6c-117">On hello **VHD** blade, select **Upload a VHD using PowerShell**.</span></span>

    ![Carica un file VHD con PowerShell](./media/devtest-lab-upload-vhd-using-powershell/upload-image-using-psh.png)

1. <span data-ttu-id="8ca6c-119">In hello **carica un'immagine con PowerShell** blade, editor di testo tooa PowerShell script copia hello generato.</span><span class="sxs-lookup"><span data-stu-id="8ca6c-119">On hello **Upload an image using PowerShell** blade, copy hello generated PowerShell script tooa text editor.</span></span>

1. <span data-ttu-id="8ca6c-120">Modificare hello **LocalFilePath** parametro di hello **Add-AzureVhd** cmdlet toopoint toohello percorso del file di disco rigido virtuale che si desidera tooupload hello.</span><span class="sxs-lookup"><span data-stu-id="8ca6c-120">Modify hello **LocalFilePath** parameter of hello **Add-AzureVhd** cmdlet toopoint toohello location of hello VHD file you want tooupload.</span></span>

1. <span data-ttu-id="8ca6c-121">Al prompt di PowerShell, eseguire hello **Add-AzureVhd** cmdlet (con hello modificato **LocalFilePath** parametro).</span><span class="sxs-lookup"><span data-stu-id="8ca6c-121">At a PowerShell prompt, run hello **Add-AzureVhd** cmdlet (with hello modified **LocalFilePath** parameter).</span></span>

> [!WARNING] 
> 
> <span data-ttu-id="8ca6c-122">processo Hello di caricamento di un file VHD può essere lungo a seconda delle dimensioni di hello del file VHD hello e la velocità della connessione.</span><span class="sxs-lookup"><span data-stu-id="8ca6c-122">hello process of uploading a VHD file can be lengthy depending on hello size of hello VHD file and your connection speed.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8ca6c-123">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8ca6c-123">Next steps</span></span>

- [<span data-ttu-id="8ca6c-124">Creare un'immagine personalizzata in Azure DevTest Labs da un file VHD utilizzando hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="8ca6c-124">Create a custom image in Azure DevTest Labs from a VHD file using hello Azure portal</span></span>](devtest-lab-create-template.md)
- [<span data-ttu-id="8ca6c-125">Creare un'immagine personalizzata in Azure DevTest Labs da un file VHD usando PowerShell</span><span class="sxs-lookup"><span data-stu-id="8ca6c-125">Create a custom image in Azure DevTest Labs from a VHD file using PowerShell</span></span>](devtest-lab-create-custom-image-from-vhd-using-powershell.md)
