---
title: archiviazione di file di Azure da una macchina virtuale Windows Azure aaaMount | Documenti Microsoft
description: Archiviare i file nel cloud hello con l'archiviazione di file di Azure e montare la condivisione di file cloud da una macchina virtuale di Azure (VM).
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: 
ms.tgt_pltfrm: 
ms.devlang: 
ms.topic: article
ms.date: 06/15/2017
ms.author: cynthn
ms.openlocfilehash: 965f1c1b3f0d07fec6d86f9312a05e02e8ce7fe0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-file-shares-with-windows-vms"></a><span data-ttu-id="311e5-103">Usare le condivisioni file di Azure con le macchine virtuali Windows</span><span class="sxs-lookup"><span data-stu-id="311e5-103">Use Azure file shares with Windows VMs</span></span> 

<span data-ttu-id="311e5-104">È possibile usare condivisioni di file di Azure come un modo toostore e accedere ai file dalla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="311e5-104">You can use Azure file shares as a way toostore and access files from your VM.</span></span> <span data-ttu-id="311e5-105">Ad esempio, è possibile archiviare uno script o un file di configurazione dell'applicazione che si desidera che tutti i tooshare di macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="311e5-105">For example, you can store a script or an application configuration file that you want all your VMs tooshare.</span></span> <span data-ttu-id="311e5-106">In questo argomento viene illustrata come condivisione di file toocreate e montaggio di Azure e come tooupload e scaricare file.</span><span class="sxs-lookup"><span data-stu-id="311e5-106">In this topic, we show you how toocreate and mount an Azure file share, and how tooupload and download files.</span></span>

## <a name="connect-tooa-file-share-from-a-vm"></a><span data-ttu-id="311e5-107">Connettersi tooa condivisione di file da una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="311e5-107">Connect tooa file share from a VM</span></span>

<span data-ttu-id="311e5-108">In questa sezione si presuppone il che hai già un file di condivisione desiderata tooconnect per.</span><span class="sxs-lookup"><span data-stu-id="311e5-108">This section assumes you already have a file share that you want tooconnect to.</span></span> <span data-ttu-id="311e5-109">Se è necessario toocreate uno, vedere [creare una condivisione file](#create-a-file-share) più avanti in questo argomento.</span><span class="sxs-lookup"><span data-stu-id="311e5-109">If you need toocreate one, see [Create a file share](#create-a-file-share) later in this topic.</span></span>

1. <span data-ttu-id="311e5-110">Accedi toohello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="311e5-110">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="311e5-111">Scegliere dal menu a sinistra, hello **gli account di archiviazione**.</span><span class="sxs-lookup"><span data-stu-id="311e5-111">On hello left menu, click **Storage accounts**.</span></span>
3. <span data-ttu-id="311e5-112">Scegliere l'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="311e5-112">Choose your storage account.</span></span>
4. <span data-ttu-id="311e5-113">In hello **Panoramica** pagina **servizi**selezionare **file**.</span><span class="sxs-lookup"><span data-stu-id="311e5-113">In hello **Overview** page, under **Services**, select **Files**.</span></span>
5. <span data-ttu-id="311e5-114">Selezionare una condivisione file.</span><span class="sxs-lookup"><span data-stu-id="311e5-114">Select a file share.</span></span>
6. <span data-ttu-id="311e5-115">Fare clic su **Connetti** tooopen una pagina in cui viene illustrata la sintassi della riga di comando hello per la condivisione di file hello di montaggio da Windows o Linux.</span><span class="sxs-lookup"><span data-stu-id="311e5-115">Click **Connect** tooopen a page that shows hello command-line syntax for mounting hello file share from Windows or Linux.</span></span>
7. <span data-ttu-id="311e5-116">Evidenziare hello sintassi del comando hello e incollarlo nel blocco note o in altre posizioni in cui è possibile accedervi facilmente.</span><span class="sxs-lookup"><span data-stu-id="311e5-116">Highlight hello syntax of hello command and paste it into Notepad or someplace else where you can easily access it.</span></span> 
8. <span data-ttu-id="311e5-117">Modifica iniziali di hello hello sintassi tooremove * * > * * e sostituire *[lettera di unità]* con lettera di unità hello (ad esempio, **y:**) in cui si desidera toomount condivisione di file hello.</span><span class="sxs-lookup"><span data-stu-id="311e5-117">Edit hello syntax tooremove hello leading **> ** and replace *[drive letter]* with hello drive letter (for example, **Y:**) where you would like toomount hello file share.</span></span>
8. <span data-ttu-id="311e5-118">Connettersi tooyour macchina virtuale e aprire un prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="311e5-118">Connect tooyour VM and open a command prompt.</span></span>
9. <span data-ttu-id="311e5-119">Incolla in hello modificare la sintassi di connessione e premere **invio**.</span><span class="sxs-lookup"><span data-stu-id="311e5-119">Paste in hello edited connection syntax and hit **Enter**.</span></span>
10. <span data-ttu-id="311e5-120">Quando hello connessione è stata creata, viene visualizzato il messaggio di hello **hello comando completato.**</span><span class="sxs-lookup"><span data-stu-id="311e5-120">When hello connection has been created, you get hello message **hello command completed successfully.**</span></span>
11. <span data-ttu-id="311e5-121">Controllare la connessione hello digitando hello lettera tooswitch toothat unità e quindi digitare **dir** contenuto hello toosee della condivisione file hello.</span><span class="sxs-lookup"><span data-stu-id="311e5-121">Check hello connection by typing in hello drive letter tooswitch toothat drive and then type **dir** toosee hello contents of hello file share.</span></span>



## <a name="create-a-file-share"></a><span data-ttu-id="311e5-122">Creare una condivisione file</span><span class="sxs-lookup"><span data-stu-id="311e5-122">Create a file share</span></span> 
1. <span data-ttu-id="311e5-123">Accedi toohello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="311e5-123">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="311e5-124">Scegliere dal menu a sinistra, hello **gli account di archiviazione**.</span><span class="sxs-lookup"><span data-stu-id="311e5-124">On hello left menu, click **Storage accounts**.</span></span>
3. <span data-ttu-id="311e5-125">Scegliere l'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="311e5-125">Choose your storage account.</span></span>
4. <span data-ttu-id="311e5-126">In hello **Panoramica** pagina **servizi**selezionare **file**.</span><span class="sxs-lookup"><span data-stu-id="311e5-126">In hello **Overview** page, under **Services**, select **Files**.</span></span>
5. <span data-ttu-id="311e5-127">Nella pagina del servizio File hello, fare clic su **+ condivisione File** toocreate condivisione del primo file. \\</span><span class="sxs-lookup"><span data-stu-id="311e5-127">In hello File Service page, click **+ File share** toocreate your first file share.\\</span></span>
6. <span data-ttu-id="311e5-128">Inserire il nome di condivisione file hello.</span><span class="sxs-lookup"><span data-stu-id="311e5-128">Fill in hello file share name.</span></span> <span data-ttu-id="311e5-129">I nomi delle condivisioni file possono contenere lettere minuscole, numeri e trattini singoli.</span><span class="sxs-lookup"><span data-stu-id="311e5-129">File share names can use lowercase letters, numbers and single hyphens.</span></span> <span data-ttu-id="311e5-130">Hello nome non può iniziare con un trattino e non è possibile utilizzare più trattini consecutivi.</span><span class="sxs-lookup"><span data-stu-id="311e5-130">hello name cannot start with a hyphen and you can't use multiple, consecutive hyphens.</span></span> 
7. <span data-ttu-id="311e5-131">Riempimento in un limite per le dimensioni file hello possibile too5120 GB.</span><span class="sxs-lookup"><span data-stu-id="311e5-131">Fill in a limit on how large hello file can be, up too5120 GB.</span></span>
8. <span data-ttu-id="311e5-132">Fare clic su **OK** toodeploy condivisione di file hello.</span><span class="sxs-lookup"><span data-stu-id="311e5-132">Click **OK** toodeploy hello file share.</span></span>
   
## <a name="upload-files"></a><span data-ttu-id="311e5-133">Caricare file</span><span class="sxs-lookup"><span data-stu-id="311e5-133">Upload files</span></span>
1. <span data-ttu-id="311e5-134">Accedi toohello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="311e5-134">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="311e5-135">Scegliere dal menu a sinistra, hello **gli account di archiviazione**.</span><span class="sxs-lookup"><span data-stu-id="311e5-135">On hello left menu, click **Storage accounts**.</span></span>
3. <span data-ttu-id="311e5-136">Scegliere l'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="311e5-136">Choose your storage account.</span></span>
4. <span data-ttu-id="311e5-137">In hello **Panoramica** pagina **servizi**selezionare **file**.</span><span class="sxs-lookup"><span data-stu-id="311e5-137">In hello **Overview** page, under **Services**, select **Files**.</span></span>
5. <span data-ttu-id="311e5-138">Selezionare una condivisione file.</span><span class="sxs-lookup"><span data-stu-id="311e5-138">Select a file share.</span></span>
6. <span data-ttu-id="311e5-139">Fare clic su **caricare** tooopen hello **caricare file** pagina.</span><span class="sxs-lookup"><span data-stu-id="311e5-139">Click **Upload** tooopen hello **Upload files** page.</span></span>
7. <span data-ttu-id="311e5-140">Fare clic su hello cartella icona toobrowse nel file system locale per tooupload un file.</span><span class="sxs-lookup"><span data-stu-id="311e5-140">Click on hello folder icon toobrowse your local file system for a file tooupload.</span></span>   
8. <span data-ttu-id="311e5-141">Fare clic su **caricare** condivisione di file toohello file hello tooupload.</span><span class="sxs-lookup"><span data-stu-id="311e5-141">Click **Upload** tooupload hello file toohello file share.</span></span>

## <a name="download-files"></a><span data-ttu-id="311e5-142">Download dei file</span><span class="sxs-lookup"><span data-stu-id="311e5-142">Download files</span></span>
1. <span data-ttu-id="311e5-143">Accedi toohello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="311e5-143">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="311e5-144">Scegliere dal menu a sinistra, hello **gli account di archiviazione**.</span><span class="sxs-lookup"><span data-stu-id="311e5-144">On hello left menu, click **Storage accounts**.</span></span>
3. <span data-ttu-id="311e5-145">Scegliere l'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="311e5-145">Choose your storage account.</span></span>
4. <span data-ttu-id="311e5-146">In hello **Panoramica** pagina **servizi**selezionare **file**.</span><span class="sxs-lookup"><span data-stu-id="311e5-146">In hello **Overview** page, under **Services**, select **Files**.</span></span>
5. <span data-ttu-id="311e5-147">Selezionare una condivisione file.</span><span class="sxs-lookup"><span data-stu-id="311e5-147">Select a file share.</span></span>
6. <span data-ttu-id="311e5-148">Fare clic sul file hello e scegliere **scaricare** toodownload il computer locale tooyour.</span><span class="sxs-lookup"><span data-stu-id="311e5-148">Right-click on hello file and choose **Download** toodownload it tooyour local machine.</span></span>
   

## <a name="next-steps"></a><span data-ttu-id="311e5-149">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="311e5-149">Next steps</span></span>

<span data-ttu-id="311e5-150">Le condivisioni file possono essere create e gestite anche usando PowerShell.</span><span class="sxs-lookup"><span data-stu-id="311e5-150">You can also create and manage file shares using PowerShell.</span></span> <span data-ttu-id="311e5-151">Per altre informazioni, vedere [Introduzione ad Archiviazione file di Azure in Windows](../../storage/files/storage-dotnet-how-to-use-files.md).</span><span class="sxs-lookup"><span data-stu-id="311e5-151">For more information, see [Get started with Azure File storage on Windows](../../storage/files/storage-dotnet-how-to-use-files.md).</span></span>
