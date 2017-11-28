---
title: disco rigido virtuale aaaUpload file tooAzure DevTest Labs con AzCopy | Documenti Microsoft
description: Caricare l'account di archiviazione del toolab file disco rigido virtuale con AzCopy
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
ms.openlocfilehash: 14f9e933b0bd27451f6bcb94841ecc381213e578
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="upload-vhd-file-toolabs-storage-account-using-azcopy"></a><span data-ttu-id="30e28-103">Caricare l'account di archiviazione del toolab file disco rigido virtuale con AzCopy</span><span class="sxs-lookup"><span data-stu-id="30e28-103">Upload VHD file toolab's storage account using AzCopy</span></span>

[!INCLUDE [devtest-lab-upload-vhd-selector](../../includes/devtest-lab-upload-vhd-selector.md)]

<span data-ttu-id="30e28-104">In Azure DevTest Labs, i file VHD possono essere utilizzato toocreate immagini personalizzate, che sono utilizzati tooprovision le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="30e28-104">In Azure DevTest Labs, VHD files can be used toocreate custom images, which are used tooprovision virtual machines.</span></span> <span data-ttu-id="30e28-105">Hello alla procedura seguente fornisce indicazioni tooupload utilità della riga di comando di AzCopy hello utilizzando account di archiviazione del laboratorio di tooa file disco rigido virtuale.</span><span class="sxs-lookup"><span data-stu-id="30e28-105">hello following steps walk you through using hello AzCopy command-line utility tooupload a VHD file tooa lab's storage account.</span></span> <span data-ttu-id="30e28-106">Dopo aver caricato il file VHD, hello [passaggi successivi sezione](#next-steps) elenca alcuni articoli che illustrano come un'immagine personalizzata da hello toocreate caricamento del file di disco rigido virtuale.</span><span class="sxs-lookup"><span data-stu-id="30e28-106">Once you've uploaded your VHD file, hello [Next steps section](#next-steps) lists some articles that illustrate how toocreate a custom image from hello uploaded VHD file.</span></span> <span data-ttu-id="30e28-107">Per altre informazioni sui dischi e sui dischi rigidi virtuali in Azure, vedere [Informazioni sui dischi e sui dischi rigidi virtuali per le macchine virtuali](../virtual-machines/linux/about-disks-and-vhds.md)</span><span class="sxs-lookup"><span data-stu-id="30e28-107">For more information about disks and VHDs in Azure, see [About disks and VHDs for virtual machines](../virtual-machines/linux/about-disks-and-vhds.md)</span></span>

> [!NOTE] 
>  
> <span data-ttu-id="30e28-108">AzCopy è un'utilità della riga di comando disponibile solo in Windows.</span><span class="sxs-lookup"><span data-stu-id="30e28-108">AzCopy is a Windows-only command-line utility.</span></span>

## <a name="step-by-step-instructions"></a><span data-ttu-id="30e28-109">Istruzioni dettagliate</span><span class="sxs-lookup"><span data-stu-id="30e28-109">Step-by-step instructions</span></span>

<span data-ttu-id="30e28-110">Hello seguenti passaggi percorso di caricamento di un disco rigido virtuale del file tooAzure DevTest Labs utilizzando [AzCopy](http://aka.ms/downloadazcopy).</span><span class="sxs-lookup"><span data-stu-id="30e28-110">hello following steps walk you through uploading a VHD file tooAzure DevTest Labs using [AzCopy](http://aka.ms/downloadazcopy).</span></span> 

1. <span data-ttu-id="30e28-111">Ottenere il nome di hello dell'account di archiviazione dell'ambiente di test di hello utilizzando hello portale di Azure:</span><span class="sxs-lookup"><span data-stu-id="30e28-111">Get hello name of hello lab's storage account using hello Azure portal:</span></span>

1. <span data-ttu-id="30e28-112">Accedi toohello [portale di Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="30e28-112">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="30e28-113">Selezionare **più servizi**, quindi selezionare **DevTest Labs** dall'elenco di hello.</span><span class="sxs-lookup"><span data-stu-id="30e28-113">Select **More services**, and then select **DevTest Labs** from hello list.</span></span>

1. <span data-ttu-id="30e28-114">Elenco dei laboratori hello selezionare lab desiderato hello.</span><span class="sxs-lookup"><span data-stu-id="30e28-114">From hello list of labs, select hello desired lab.</span></span>  

1. <span data-ttu-id="30e28-115">Nel pannello del lab hello, selezionare **configurazione**.</span><span class="sxs-lookup"><span data-stu-id="30e28-115">On hello lab's blade, select **Configuration**.</span></span> 

1. <span data-ttu-id="30e28-116">Lab hello **configurazione** pannello seleziona **immagini personalizzate (VHD)**.</span><span class="sxs-lookup"><span data-stu-id="30e28-116">On hello lab **Configuration** blade, select **Custom images (VHDs)**.</span></span>

1. <span data-ttu-id="30e28-117">In hello **immagini personalizzate** pannello selezionare **+ Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="30e28-117">On hello **Custom images** blade, Select **+Add**.</span></span> 

1. <span data-ttu-id="30e28-118">In hello **immagine personalizzata** pannello seleziona **VHD**.</span><span class="sxs-lookup"><span data-stu-id="30e28-118">On hello **Custom image** blade, select **VHD**.</span></span>

1. <span data-ttu-id="30e28-119">In hello **VHD** pannello seleziona **caricare un disco rigido virtuale con PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="30e28-119">On hello **VHD** blade, select **Upload a VHD using PowerShell**.</span></span>

    ![Carica un file VHD con PowerShell](./media/devtest-lab-upload-vhd-using-azcopy/upload-image-using-psh.png)

1. <span data-ttu-id="30e28-121">Hello **carica un'immagine con PowerShell** pannello viene visualizzato un toohello chiamata **Add-AzureVhd** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="30e28-121">hello **Upload an image using PowerShell** blade displays a call toohello **Add-AzureVhd** cmdlet.</span></span> <span data-ttu-id="30e28-122">primo parametro Hello (*destinazione*) contiene hello URI per un contenitore blob (*Carica*) in hello seguente formato:</span><span class="sxs-lookup"><span data-stu-id="30e28-122">hello first parameter (*Destination*) contains hello URI for a blob container (*uploads*) in hello following format:</span></span>

    ```
    https://<STORAGE-ACCOUNT-NAME>.blob.core.windows.net/uploads/...
    ``` 

1. <span data-ttu-id="30e28-123">Prendere nota di hello completo URI usato nei passaggi successivi.</span><span class="sxs-lookup"><span data-stu-id="30e28-123">Make note of hello full URI as it is used in later steps.</span></span>

1. <span data-ttu-id="30e28-124">Caricare file VHD hello tramite AzCopy:</span><span class="sxs-lookup"><span data-stu-id="30e28-124">Upload hello VHD file using AzCopy:</span></span>
 
1. <span data-ttu-id="30e28-125">[Scaricare e installare una versione più recente di hello di AzCopy](http://aka.ms/downloadazcopy).</span><span class="sxs-lookup"><span data-stu-id="30e28-125">[Download and install hello latest version of AzCopy](http://aka.ms/downloadazcopy).</span></span>

1. <span data-ttu-id="30e28-126">Aprire una finestra di comando e passare toohello AzCopy directory di installazione.</span><span class="sxs-lookup"><span data-stu-id="30e28-126">Open a command window and navigate toohello AzCopy installation directory.</span></span> <span data-ttu-id="30e28-127">Facoltativamente, è possibile aggiungere hello AzCopy tooyour sistema percorso di installazione.</span><span class="sxs-lookup"><span data-stu-id="30e28-127">Optionally, you can add hello AzCopy installation location tooyour system path.</span></span> <span data-ttu-id="30e28-128">Per impostazione predefinita, AzCopy è installato toohello seguente directory:</span><span class="sxs-lookup"><span data-stu-id="30e28-128">By default, AzCopy is installed toohello following directory:</span></span>

    ```command-line
    %ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy
    ```

1. <span data-ttu-id="30e28-129">Per eseguire hello comando al prompt dei comandi di hello seguente utilizzando hello storage account chiave e del blob URI del contenitore.</span><span class="sxs-lookup"><span data-stu-id="30e28-129">Using hello storage account key and blob container URI, run hello following command at hello command prompt.</span></span> <span data-ttu-id="30e28-130">Hello *vhdFileName* . il valore deve toobe racchiuso tra virgolette.</span><span class="sxs-lookup"><span data-stu-id="30e28-130">hello *vhdFileName* value needs toobe in quotes.</span></span> <span data-ttu-id="30e28-131">processo Hello di caricamento di un file VHD può essere lungo a seconda delle dimensioni di hello del file VHD hello e la velocità della connessione.</span><span class="sxs-lookup"><span data-stu-id="30e28-131">hello process of uploading a VHD file can be lengthy depending on hello size of hello VHD file and your connection speed.</span></span>   

    ```command-line
    AzCopy /Source:<sourceDirectory> /Dest:<blobContainerUri> /DestKey:<storageAccountKey> /Pattern:"<vhdFileName>" /BlobType:page
    ```

## <a name="next-steps"></a><span data-ttu-id="30e28-132">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="30e28-132">Next steps</span></span>

- [<span data-ttu-id="30e28-133">Creare un'immagine personalizzata in Azure DevTest Labs da un file VHD utilizzando hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="30e28-133">Create a custom image in Azure DevTest Labs from a VHD file using hello Azure portal</span></span>](devtest-lab-create-template.md)
- [<span data-ttu-id="30e28-134">Creare un'immagine personalizzata in Azure DevTest Labs da un file VHD usando PowerShell</span><span class="sxs-lookup"><span data-stu-id="30e28-134">Create a custom image in Azure DevTest Labs from a VHD file using PowerShell</span></span>](devtest-lab-create-custom-image-from-vhd-using-powershell.md)