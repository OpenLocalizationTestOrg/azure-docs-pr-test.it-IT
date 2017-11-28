---
title: aaaHow toomanage archiviazione di File di Azure dal portale di Azure hello | Documenti Microsoft
description: Informazioni su archiviazione di File di Azure toouse hello toomanage portale Azure.
services: storage
documentationcenter: 
author: RenaShahMSFT
manager: aungoo
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/27/2017
ms.author: renash
ms.openlocfilehash: 6ad2fbbf9ee2f86748b1b175d0f63274144dc5eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-file-storage-from-hello-azure-portal"></a><span data-ttu-id="7197f-103">Come archiviazione di File di Azure toouse da hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="7197f-103">How toouse Azure File storage from hello Azure Portal</span></span>
<span data-ttu-id="7197f-104">Hello [portale di Azure](https://portal.azure.com) fornisce un'interfaccia utente per gestire l'archiviazione di File di Azure.</span><span class="sxs-lookup"><span data-stu-id="7197f-104">hello [Azure portal](https://portal.azure.com) provides a user interface for managing Azure File storage.</span></span> <span data-ttu-id="7197f-105">È possibile eseguire hello seguente azioni dal web browser:</span><span class="sxs-lookup"><span data-stu-id="7197f-105">You can perform hello following actions from your web browser:</span></span>

* <span data-ttu-id="7197f-106">Creare una condivisione file</span><span class="sxs-lookup"><span data-stu-id="7197f-106">Create a File Share</span></span>
* <span data-ttu-id="7197f-107">Caricare e scaricare file tooand dalla condivisione di file.</span><span class="sxs-lookup"><span data-stu-id="7197f-107">Upload and download files tooand from your file share.</span></span>
* <span data-ttu-id="7197f-108">Monitorare l'utilizzo effettivo di hello di ciascuna condivisione file.</span><span class="sxs-lookup"><span data-stu-id="7197f-108">Monitor hello actual usage of each file share.</span></span>
* <span data-ttu-id="7197f-109">Regolare quota delle dimensioni di condivisione file hello.</span><span class="sxs-lookup"><span data-stu-id="7197f-109">Adjust hello file share size quota.</span></span>
* <span data-ttu-id="7197f-110">Copiare hello montaggio comandi toouse toomount condividere il file da un client di Windows o Linux.</span><span class="sxs-lookup"><span data-stu-id="7197f-110">Copy hello mount commands toouse toomount your file share from a Windows or Linux client.</span></span>

## <a name="create-file-share"></a><span data-ttu-id="7197f-111">Creare la condivisione file</span><span class="sxs-lookup"><span data-stu-id="7197f-111">Create file share</span></span>
1. <span data-ttu-id="7197f-112">Accedi toohello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="7197f-112">Sign in toohello Azure portal.</span></span>
2. <span data-ttu-id="7197f-113">Nel menu di navigazione hello, fare clic su **gli account di archiviazione** o **gli account di archiviazione (classico)**.</span><span class="sxs-lookup"><span data-stu-id="7197f-113">On hello navigation menu, click **Storage accounts** or **Storage accounts (classic)**.</span></span>
    
    ![Schermata che illustra la modalità di condivisione di file toocreate nel portale di hello](./media/storage-how-to-use-files-portal/use-files-portal-create-file-share1.png)

3. <span data-ttu-id="7197f-115">Scegliere l'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="7197f-115">Choose your storage account.</span></span>

    ![Schermata che illustra la modalità di condivisione di file toocreate nel portale di hello](./media/storage-how-to-use-files-portal/use-files-portal-create-file-share2.png)

4. <span data-ttu-id="7197f-117">Scegliere il servizio "File".</span><span class="sxs-lookup"><span data-stu-id="7197f-117">Choose "Files" service.</span></span>

    ![Schermata che illustra la modalità di condivisione di file toocreate nel portale di hello](./media/storage-how-to-use-files-portal/use-files-portal-create-file-share3.png)

5. <span data-ttu-id="7197f-119">Fare clic su "Condivisioni di File" e seguire toocreate collegamento hello condivisione del primo file.</span><span class="sxs-lookup"><span data-stu-id="7197f-119">Click "File shares" and follow hello link toocreate your first file share.</span></span>

    ![Schermata che illustra la modalità di condivisione di file toocreate nel portale di hello](./media/storage-how-to-use-files-portal/use-files-portal-create-file-share4.png)

6. <span data-ttu-id="7197f-121">Immettere il nome di condivisione file hello e dimensioni hello di hello file share (backup GB too5120) toocreate condivisione file di primo.</span><span class="sxs-lookup"><span data-stu-id="7197f-121">Fill in hello file share name and hello size of hello file share (up too5120 GB) toocreate your first file share.</span></span> <span data-ttu-id="7197f-122">Dopo aver creata una condivisione di hello, è possibile montarlo da qualsiasi file system che supporta SMB 2.1 o SMB 3.0.</span><span class="sxs-lookup"><span data-stu-id="7197f-122">Once hello file share has been created, you can mount it from any file system that supports SMB 2.1 or SMB 3.0.</span></span> <span data-ttu-id="7197f-123">È possibile fare clic su **Quota** su hello toochange hello dimensioni della condivisione file del file hello too5120 GB.</span><span class="sxs-lookup"><span data-stu-id="7197f-123">You could click on **Quota** on hello file share toochange hello size of hello file up too5120 GB.</span></span> <span data-ttu-id="7197f-124">Consultare troppo[calcolatore dei costi Azure](https://azure.microsoft.com/pricing/calculator/) costi di archiviazione di hello tooestimate dell'utilizzo dell'archiviazione di File di Azure.</span><span class="sxs-lookup"><span data-stu-id="7197f-124">Please refer too[Azure Pricing Calculator](https://azure.microsoft.com/pricing/calculator/) tooestimate hello storage cost of using Azure File storage.</span></span>

    ![Schermata che illustra la modalità di condivisione di file toocreate nel portale di hello](./media/storage-how-to-use-files-portal/use-files-portal-create-file-share5.png)

## <a name="upload-and-download-files"></a><span data-ttu-id="7197f-126">Caricare e scaricare file</span><span class="sxs-lookup"><span data-stu-id="7197f-126">Upload and download files</span></span>
1. <span data-ttu-id="7197f-127">Scegliere una condivisione file già creata.</span><span class="sxs-lookup"><span data-stu-id="7197f-127">Choose one file share your have already created.</span></span>

    ![Schermata che illustra come tooupload e scaricare file da hello portale](./media/storage-how-to-use-files-portal/use-files-portal-upload-file1.png)

2. <span data-ttu-id="7197f-129">Fare clic su **caricare** per aprire l'interfaccia utente di hello per i file di caricamento.</span><span class="sxs-lookup"><span data-stu-id="7197f-129">Click **Upload** to open hello user interface for files uploading.</span></span>

    ![Schermata che illustra come i file dal portale hello tooupload](./media/storage-how-to-use-files-portal/use-files-portal-upload-file2.png)

## <a name="connect-toofile-share"></a><span data-ttu-id="7197f-131">Connettersi toofile condivisione</span><span class="sxs-lookup"><span data-stu-id="7197f-131">Connect toofile share</span></span>
-  <span data-ttu-id="7197f-132">Fare clic su **Connetti** per ottenere la riga di comando hello per condivisione file hello di montaggio da Windows e Linux.</span><span class="sxs-lookup"><span data-stu-id="7197f-132">Click **Connect** to get hello command line for mounting hello file share from Windows and Linux.</span></span> <span data-ttu-id="7197f-133">Per gli utenti Linux, è anche possibile fare riferimento troppo[come archiviazione di File di Azure con Linux toouse](../storage-how-to-use-files-linux.md) per ulteriori istruzioni per altre distribuzioni di Linux.</span><span class="sxs-lookup"><span data-stu-id="7197f-133">For Linux users, you can also refer too[How toouse Azure File storage with Linux](../storage-how-to-use-files-linux.md) for more mounting instructions for other Linux distributions.</span></span>

    ![Schermata che illustra come toomount hello condivisione file](./media/storage-how-to-use-files-portal/use-files-portal-connect.png)
-  <span data-ttu-id="7197f-135">È possibile copiare hello comandi per il montaggio di file di condividono in Windows o Linux ed eseguirlo da parte dell'utente macchina VM di Azure o in locale.</span><span class="sxs-lookup"><span data-stu-id="7197f-135">You can copy hello commands for mounting file share on Windows or Linux and run it from you Azure VM or on-premises machine.</span></span>

    ![Schermata che mostra i comandi di montaggio di hello per Windows e Linux](./media/storage-how-to-use-files-portal/use-files-portal-show-mount-commands.png)

<span data-ttu-id="7197f-137">**Suggerimento:**</span><span class="sxs-lookup"><span data-stu-id="7197f-137">**Tip:**</span></span>  
<span data-ttu-id="7197f-138">toofind chiave di accesso account di archiviazione hello per l'installazione, fare clic su **per questo account di archiviazione delle chiavi di accesso alla visualizzazione** nella parte inferiore di hello di hello pagina Connetti.</span><span class="sxs-lookup"><span data-stu-id="7197f-138">toofind hello storage account access key for mounting, click on **View access keys for this storage account** at hello bottom of hello connect page.</span></span>

## <a name="see-also"></a><span data-ttu-id="7197f-139">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="7197f-139">See also</span></span>
<span data-ttu-id="7197f-140">Vedere i collegamenti seguenti per ulteriori informazioni sull'archiviazione file di Azure.</span><span class="sxs-lookup"><span data-stu-id="7197f-140">See these links for more information about Azure File storage.</span></span>

* [<span data-ttu-id="7197f-141">Domande frequenti</span><span class="sxs-lookup"><span data-stu-id="7197f-141">FAQ</span></span>](../storage-files-faq.md)
* [<span data-ttu-id="7197f-142">Risoluzione dei problemi in Windows</span><span class="sxs-lookup"><span data-stu-id="7197f-142">Troubleshooting on Windows</span></span>](storage-troubleshoot-windows-file-connection-problems.md)      
* [<span data-ttu-id="7197f-143">Risoluzione dei problemi in Linux</span><span class="sxs-lookup"><span data-stu-id="7197f-143">Troubleshooting on Linux</span></span>](storage-troubleshoot-linux-file-connection-problems.md)    