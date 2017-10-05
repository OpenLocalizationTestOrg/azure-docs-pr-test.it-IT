---
title: Montare l'archiviazione file di Azure da una macchina virtuale Windows di Azure | Microsoft Docs
description: Archiviare i file nel cloud con l'archiviazione file di Azure e montare la condivisione file nel cloud da una macchina virtuale (VM) Azure.
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
ms.openlocfilehash: 6ffb2d2da1e2439df6f5da543411e3c2c68d3435
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="use-azure-file-shares-with-windows-vms"></a><span data-ttu-id="e91de-103">Usare le condivisioni file di Azure con le macchine virtuali Windows</span><span class="sxs-lookup"><span data-stu-id="e91de-103">Use Azure file shares with Windows VMs</span></span> 

<span data-ttu-id="e91de-104">Le condivisioni file di Azure possono essere usate per archiviare file e accedervi da una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="e91de-104">You can use Azure file shares as a way to store and access files from your VM.</span></span> <span data-ttu-id="e91de-105">Ad esempio, è possibile archiviare uno script o il file di configurazione di un'applicazione che si intende condividere con tutte le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="e91de-105">For example, you can store a script or an application configuration file that you want all your VMs to share.</span></span> <span data-ttu-id="e91de-106">In questo argomento verrà illustrato come creare e montare una condivisione file di Azure e come caricare e scaricare file.</span><span class="sxs-lookup"><span data-stu-id="e91de-106">In this topic, we show you how to create and mount an Azure file share, and how to upload and download files.</span></span>

## <a name="connect-to-a-file-share-from-a-vm"></a><span data-ttu-id="e91de-107">Connettersi a una condivisione file da una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="e91de-107">Connect to a file share from a VM</span></span>

<span data-ttu-id="e91de-108">In questa sezione si presuppone che la condivisione file a cui si desidera connettersi sia già stata creata.</span><span class="sxs-lookup"><span data-stu-id="e91de-108">This section assumes you already have a file share that you want to connect to.</span></span> <span data-ttu-id="e91de-109">Se è necessario crearne una, vedere [Creare una condivisione file](#create-a-file-share) più avanti in questo argomento.</span><span class="sxs-lookup"><span data-stu-id="e91de-109">If you need to create one, see [Create a file share](#create-a-file-share) later in this topic.</span></span>

1. <span data-ttu-id="e91de-110">Accedere al [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e91de-110">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="e91de-111">Fare clic su **Account di archiviazione** nel menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="e91de-111">On the left menu, click **Storage accounts**.</span></span>
3. <span data-ttu-id="e91de-112">Scegliere l'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="e91de-112">Choose your storage account.</span></span>
4. <span data-ttu-id="e91de-113">Nella pagina **Panoramica** selezionare **File** dalla sezione **Servizi**.</span><span class="sxs-lookup"><span data-stu-id="e91de-113">In the **Overview** page, under **Services**, select **Files**.</span></span>
5. <span data-ttu-id="e91de-114">Selezionare una condivisione file.</span><span class="sxs-lookup"><span data-stu-id="e91de-114">Select a file share.</span></span>
6. <span data-ttu-id="e91de-115">Fare clic su **Connetti** per aprire una pagina in cui viene visualizzata la sintassi della riga di comando per montare la condivisione file da Windows o Linux.</span><span class="sxs-lookup"><span data-stu-id="e91de-115">Click **Connect** to open a page that shows the command-line syntax for mounting the file share from Windows or Linux.</span></span>
7. <span data-ttu-id="e91de-116">Evidenziare la sintassi del comando e incollarla in Blocco note o in un'altra applicazione di facile accesso.</span><span class="sxs-lookup"><span data-stu-id="e91de-116">Highlight the syntax of the command and paste it into Notepad or someplace else where you can easily access it.</span></span> 
8. <span data-ttu-id="e91de-117">Modificare la sintassi per rimuovere i caratteri iniziali **> ** e sostituire *[drive letter]* con la lettera di unità (ad esempio, **Y:**) in cui si desidera montare la condivisione file.</span><span class="sxs-lookup"><span data-stu-id="e91de-117">Edit the syntax to remove the leading **> ** and replace *[drive letter]* with the drive letter (for example, **Y:**) where you would like to mount the file share.</span></span>
8. <span data-ttu-id="e91de-118">Connettersi alla macchina virtuale e aprire un prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="e91de-118">Connect to your VM and open a command prompt.</span></span>
9. <span data-ttu-id="e91de-119">Incollare la sintassi di connessione modificata e premere **INVIO**.</span><span class="sxs-lookup"><span data-stu-id="e91de-119">Paste in the edited connection syntax and hit **Enter**.</span></span>
10. <span data-ttu-id="e91de-120">Quando la connessione è stata creata, verrà visualizzato il messaggio **Esecuzione comando riuscita.**</span><span class="sxs-lookup"><span data-stu-id="e91de-120">When the connection has been created, you get the message **The command completed successfully.**</span></span>
11. <span data-ttu-id="e91de-121">Verificare la connessione digitando la lettera di unità per passare all'unità e quindi digitare **dir** per vedere il contenuto della condivisione file.</span><span class="sxs-lookup"><span data-stu-id="e91de-121">Check the connection by typing in the drive letter to switch to that drive and then type **dir** to see the contents of the file share.</span></span>



## <a name="create-a-file-share"></a><span data-ttu-id="e91de-122">Creare una condivisione file</span><span class="sxs-lookup"><span data-stu-id="e91de-122">Create a file share</span></span> 
1. <span data-ttu-id="e91de-123">Accedere al [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e91de-123">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="e91de-124">Fare clic su **Account di archiviazione** nel menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="e91de-124">On the left menu, click **Storage accounts**.</span></span>
3. <span data-ttu-id="e91de-125">Scegliere l'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="e91de-125">Choose your storage account.</span></span>
4. <span data-ttu-id="e91de-126">Nella pagina **Panoramica** selezionare **File** dalla sezione **Servizi**.</span><span class="sxs-lookup"><span data-stu-id="e91de-126">In the **Overview** page, under **Services**, select **Files**.</span></span>
5. <span data-ttu-id="e91de-127">Fare clic su **Condivisione file** nella pagina Servizio file per creare la prima condivisione file.</span><span class="sxs-lookup"><span data-stu-id="e91de-127">In the File Service page, click **+ File share** to create your first file share.\\</span></span>
6. <span data-ttu-id="e91de-128">Immettere il nome della condivisione file.</span><span class="sxs-lookup"><span data-stu-id="e91de-128">Fill in the file share name.</span></span> <span data-ttu-id="e91de-129">I nomi delle condivisioni file possono contenere lettere minuscole, numeri e trattini singoli.</span><span class="sxs-lookup"><span data-stu-id="e91de-129">File share names can use lowercase letters, numbers and single hyphens.</span></span> <span data-ttu-id="e91de-130">Il nome non può iniziare con un trattino e non sono consentiti più trattini consecutivi.</span><span class="sxs-lookup"><span data-stu-id="e91de-130">The name cannot start with a hyphen and you can't use multiple, consecutive hyphens.</span></span> 
7. <span data-ttu-id="e91de-131">Immettere un limite per le dimensioni del file, fino a 5120 GB.</span><span class="sxs-lookup"><span data-stu-id="e91de-131">Fill in a limit on how large the file can be, up to 5120 GB.</span></span>
8. <span data-ttu-id="e91de-132">Fare clic su **OK** per distribuire la condivisione file.</span><span class="sxs-lookup"><span data-stu-id="e91de-132">Click **OK** to deploy the file share.</span></span>
   
## <a name="upload-files"></a><span data-ttu-id="e91de-133">Caricare file</span><span class="sxs-lookup"><span data-stu-id="e91de-133">Upload files</span></span>
1. <span data-ttu-id="e91de-134">Accedere al [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e91de-134">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="e91de-135">Fare clic su **Account di archiviazione** nel menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="e91de-135">On the left menu, click **Storage accounts**.</span></span>
3. <span data-ttu-id="e91de-136">Scegliere l'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="e91de-136">Choose your storage account.</span></span>
4. <span data-ttu-id="e91de-137">Nella pagina **Panoramica** selezionare **File** dalla sezione **Servizi**.</span><span class="sxs-lookup"><span data-stu-id="e91de-137">In the **Overview** page, under **Services**, select **Files**.</span></span>
5. <span data-ttu-id="e91de-138">Selezionare una condivisione file.</span><span class="sxs-lookup"><span data-stu-id="e91de-138">Select a file share.</span></span>
6. <span data-ttu-id="e91de-139">Fare clic su **Carica** per aprire la pagina **Carica file**.</span><span class="sxs-lookup"><span data-stu-id="e91de-139">Click **Upload** to open the **Upload files** page.</span></span>
7. <span data-ttu-id="e91de-140">Fare clic sull'icona della cartella per individuare nel file system locale il file da caricare.</span><span class="sxs-lookup"><span data-stu-id="e91de-140">Click on the folder icon to browse your local file system for a file to upload.</span></span>   
8. <span data-ttu-id="e91de-141">Fare clic su **Carica** per caricare il file nella condivisione file.</span><span class="sxs-lookup"><span data-stu-id="e91de-141">Click **Upload** to upload the file to the file share.</span></span>

## <a name="download-files"></a><span data-ttu-id="e91de-142">Download dei file</span><span class="sxs-lookup"><span data-stu-id="e91de-142">Download files</span></span>
1. <span data-ttu-id="e91de-143">Accedere al [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e91de-143">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="e91de-144">Fare clic su **Account di archiviazione** nel menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="e91de-144">On the left menu, click **Storage accounts**.</span></span>
3. <span data-ttu-id="e91de-145">Scegliere l'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="e91de-145">Choose your storage account.</span></span>
4. <span data-ttu-id="e91de-146">Nella pagina **Panoramica** selezionare **File** dalla sezione **Servizi**.</span><span class="sxs-lookup"><span data-stu-id="e91de-146">In the **Overview** page, under **Services**, select **Files**.</span></span>
5. <span data-ttu-id="e91de-147">Selezionare una condivisione file.</span><span class="sxs-lookup"><span data-stu-id="e91de-147">Select a file share.</span></span>
6. <span data-ttu-id="e91de-148">Fare clic con il pulsante destro del mouse sul file e scegliere **Scarica** per scaricarlo nel computer locale.</span><span class="sxs-lookup"><span data-stu-id="e91de-148">Right-click on the file and choose **Download** to download it to your local machine.</span></span>
   

## <a name="next-steps"></a><span data-ttu-id="e91de-149">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e91de-149">Next steps</span></span>

<span data-ttu-id="e91de-150">Le condivisioni file possono essere create e gestite anche usando PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e91de-150">You can also create and manage file shares using PowerShell.</span></span> <span data-ttu-id="e91de-151">Per altre informazioni, vedere [Introduzione ad Archiviazione file di Azure in Windows](../../storage/files/storage-dotnet-how-to-use-files.md).</span><span class="sxs-lookup"><span data-stu-id="e91de-151">For more information, see [Get started with Azure File storage on Windows](../../storage/files/storage-dotnet-how-to-use-files.md).</span></span>
