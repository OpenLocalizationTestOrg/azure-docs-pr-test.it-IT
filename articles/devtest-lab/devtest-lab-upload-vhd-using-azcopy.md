---
title: Caricare un file VHD in Azure DevTest Labs usando AzCopy | Microsoft Docs
description: Caricare un file VHD nell'account di archiviazione del lab usando AzCopy
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
ms.openlocfilehash: a4f43354740d9f17570932b0b9c753f46d67dc33
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="upload-vhd-file-to-labs-storage-account-using-azcopy"></a><span data-ttu-id="7cacb-103">Caricare un file VHD nell'account di archiviazione del lab usando AzCopy</span><span class="sxs-lookup"><span data-stu-id="7cacb-103">Upload VHD file to lab's storage account using AzCopy</span></span>

[!INCLUDE [devtest-lab-upload-vhd-selector](../../includes/devtest-lab-upload-vhd-selector.md)]

<span data-ttu-id="7cacb-104">In Azure DevTest Labs è possibile usare i file VHD per creare immagini personalizzate da utilizzare per il provisioning di macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="7cacb-104">In Azure DevTest Labs, VHD files can be used to create custom images, which are used to provision virtual machines.</span></span> <span data-ttu-id="7cacb-105">La procedura seguente illustra come usare l'utilità della riga di comando AzCopy per caricare un file VHD nell'account di archiviazione di un lab.</span><span class="sxs-lookup"><span data-stu-id="7cacb-105">The following steps walk you through using the AzCopy command-line utility to upload a VHD file to a lab's storage account.</span></span> <span data-ttu-id="7cacb-106">Dopo avere caricato il file VHD, vedere la [sezione Passaggi successivi](#next-steps) per un elenco di articoli che illustrano come creare un'immagine personalizzata dal file VHD caricato.</span><span class="sxs-lookup"><span data-stu-id="7cacb-106">Once you've uploaded your VHD file, the [Next steps section](#next-steps) lists some articles that illustrate how to create a custom image from the uploaded VHD file.</span></span> <span data-ttu-id="7cacb-107">Per altre informazioni sui dischi e sui dischi rigidi virtuali in Azure, vedere [Informazioni sui dischi e sui dischi rigidi virtuali per le macchine virtuali](../virtual-machines/linux/about-disks-and-vhds.md)</span><span class="sxs-lookup"><span data-stu-id="7cacb-107">For more information about disks and VHDs in Azure, see [About disks and VHDs for virtual machines](../virtual-machines/linux/about-disks-and-vhds.md)</span></span>

> [!NOTE] 
>  
> <span data-ttu-id="7cacb-108">AzCopy è un'utilità della riga di comando disponibile solo in Windows.</span><span class="sxs-lookup"><span data-stu-id="7cacb-108">AzCopy is a Windows-only command-line utility.</span></span>

## <a name="step-by-step-instructions"></a><span data-ttu-id="7cacb-109">Istruzioni dettagliate</span><span class="sxs-lookup"><span data-stu-id="7cacb-109">Step-by-step instructions</span></span>

<span data-ttu-id="7cacb-110">La procedura seguente illustra come caricare un file VHD in Azure DevTest Labs usando [AzCopy](http://aka.ms/downloadazcopy).</span><span class="sxs-lookup"><span data-stu-id="7cacb-110">The following steps walk you through uploading a VHD file to Azure DevTest Labs using [AzCopy](http://aka.ms/downloadazcopy).</span></span> 

1. <span data-ttu-id="7cacb-111">Ottenere il nome dell'account di archiviazione del lab tramite il portale di Azure:</span><span class="sxs-lookup"><span data-stu-id="7cacb-111">Get the name of the lab's storage account using the Azure portal:</span></span>

1. <span data-ttu-id="7cacb-112">Accedere al [portale di Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="7cacb-112">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="7cacb-113">Selezionare **Altri servizi** e quindi **DevTest Labs** dall'elenco.</span><span class="sxs-lookup"><span data-stu-id="7cacb-113">Select **More services**, and then select **DevTest Labs** from the list.</span></span>

1. <span data-ttu-id="7cacb-114">Nell'elenco dei lab selezionare il lab desiderato.</span><span class="sxs-lookup"><span data-stu-id="7cacb-114">From the list of labs, select the desired lab.</span></span>  

1. <span data-ttu-id="7cacb-115">Nel pannello del lab selezionare **Configurazione**.</span><span class="sxs-lookup"><span data-stu-id="7cacb-115">On the lab's blade, select **Configuration**.</span></span> 

1. <span data-ttu-id="7cacb-116">Nel pannello **Configurazione** del lab selezionare **Immagini personalizzate (dischi rigidi virtuali)**.</span><span class="sxs-lookup"><span data-stu-id="7cacb-116">On the lab **Configuration** blade, select **Custom images (VHDs)**.</span></span>

1. <span data-ttu-id="7cacb-117">Nel pannello **Immagini personalizzate** selezionare **+Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="7cacb-117">On the **Custom images** blade, Select **+Add**.</span></span> 

1. <span data-ttu-id="7cacb-118">Nel pannello **Immagine personalizzata** selezionare **VHD**.</span><span class="sxs-lookup"><span data-stu-id="7cacb-118">On the **Custom image** blade, select **VHD**.</span></span>

1. <span data-ttu-id="7cacb-119">Nel pannello **VHD** selezionare l'opzione **Carica un file VHD con PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="7cacb-119">On the **VHD** blade, select **Upload a VHD using PowerShell**.</span></span>

    ![Carica un file VHD con PowerShell](./media/devtest-lab-upload-vhd-using-azcopy/upload-image-using-psh.png)

1. <span data-ttu-id="7cacb-121">Nel pannello **Carica un'immagine con PowerShell** è visualizzata una chiamata al cmdlet **Add-AzureVhd**.</span><span class="sxs-lookup"><span data-stu-id="7cacb-121">The **Upload an image using PowerShell** blade displays a call to the **Add-AzureVhd** cmdlet.</span></span> <span data-ttu-id="7cacb-122">Il primo parametro (*Destination*) contiene l'URI per un contenitore BLOB (*uploads*) nel formato seguente:</span><span class="sxs-lookup"><span data-stu-id="7cacb-122">The first parameter (*Destination*) contains the URI for a blob container (*uploads*) in the following format:</span></span>

    ```
    https://<STORAGE-ACCOUNT-NAME>.blob.core.windows.net/uploads/...
    ``` 

1. <span data-ttu-id="7cacb-123">Prendere nota dell'URI completo in quanto verrà usato nei passaggi successivi.</span><span class="sxs-lookup"><span data-stu-id="7cacb-123">Make note of the full URI as it is used in later steps.</span></span>

1. <span data-ttu-id="7cacb-124">Caricare il file VHD usando AzCopy:</span><span class="sxs-lookup"><span data-stu-id="7cacb-124">Upload the VHD file using AzCopy:</span></span>
 
1. <span data-ttu-id="7cacb-125">[Scaricare e installare la versione più recente di AzCopy](http://aka.ms/downloadazcopy).</span><span class="sxs-lookup"><span data-stu-id="7cacb-125">[Download and install the latest version of AzCopy](http://aka.ms/downloadazcopy).</span></span>

1. <span data-ttu-id="7cacb-126">Aprire una finestra di comando e passare alla directory di installazione di AzCopy.</span><span class="sxs-lookup"><span data-stu-id="7cacb-126">Open a command window and navigate to the AzCopy installation directory.</span></span> <span data-ttu-id="7cacb-127">Se lo si desidera, è possibile aggiungere il percorso di installazione di AzCopy al percorso di sistema.</span><span class="sxs-lookup"><span data-stu-id="7cacb-127">Optionally, you can add the AzCopy installation location to your system path.</span></span> <span data-ttu-id="7cacb-128">Per impostazione predefinita, AzCopy viene installato nella directory seguente:</span><span class="sxs-lookup"><span data-stu-id="7cacb-128">By default, AzCopy is installed to the following directory:</span></span>

    ```command-line
    %ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy
    ```

1. <span data-ttu-id="7cacb-129">Usando la chiave dell'account di archiviazione e l'URI del contenitore BLOB, eseguire il comando seguente nel prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="7cacb-129">Using the storage account key and blob container URI, run the following command at the command prompt.</span></span> <span data-ttu-id="7cacb-130">Il valore *vhdFileName* deve essere racchiuso tra virgolette.</span><span class="sxs-lookup"><span data-stu-id="7cacb-130">The *vhdFileName* value needs to be in quotes.</span></span> <span data-ttu-id="7cacb-131">Il processo di caricamento di un file VHD può richiedere molto tempo a seconda delle dimensioni del file VHD e della velocità della connessione.</span><span class="sxs-lookup"><span data-stu-id="7cacb-131">The process of uploading a VHD file can be lengthy depending on the size of the VHD file and your connection speed.</span></span>   

    ```command-line
    AzCopy /Source:<sourceDirectory> /Dest:<blobContainerUri> /DestKey:<storageAccountKey> /Pattern:"<vhdFileName>" /BlobType:page
    ```

## <a name="next-steps"></a><span data-ttu-id="7cacb-132">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7cacb-132">Next steps</span></span>

- [<span data-ttu-id="7cacb-133">Creare un'immagine personalizzata in Azure DevTest Labs da un file VHD usando il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="7cacb-133">Create a custom image in Azure DevTest Labs from a VHD file using the Azure portal</span></span>](devtest-lab-create-template.md)
- [<span data-ttu-id="7cacb-134">Creare un'immagine personalizzata in Azure DevTest Labs da un file VHD usando PowerShell</span><span class="sxs-lookup"><span data-stu-id="7cacb-134">Create a custom image in Azure DevTest Labs from a VHD file using PowerShell</span></span>](devtest-lab-create-custom-image-from-vhd-using-powershell.md)