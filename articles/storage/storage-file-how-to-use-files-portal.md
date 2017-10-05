---
title: Come gestire Archiviazione file di Azure dal portale di Azure | Microsoft Docs
description: Informazioni su come usare il portale di Azure per gestire Archiviazione file di Azure.
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
ms.openlocfilehash: d8ffb4359b0efe8da2f3bccb81c987bdeedf1a39
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/29/2017
---
# <a name="how-to-use-azure-file-storage-from-the-azure-portal"></a><span data-ttu-id="2f004-103">Come usare Archiviazione file di Azure dal portale di Azure</span><span class="sxs-lookup"><span data-stu-id="2f004-103">How to use Azure File storage from the Azure Portal</span></span>
<span data-ttu-id="2f004-104">Il [portale di Azure](https://portal.azure.com) fornisce un'interfaccia utente per la gestione di Archiviazione file di Azure.</span><span class="sxs-lookup"><span data-stu-id="2f004-104">The [Azure portal](https://portal.azure.com) provides a user interface for managing Azure File storage.</span></span> <span data-ttu-id="2f004-105">Dal Web browser è possibile eseguire le azioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="2f004-105">You can perform the following actions from your web browser:</span></span>

* <span data-ttu-id="2f004-106">Creare una condivisione file</span><span class="sxs-lookup"><span data-stu-id="2f004-106">Create a File Share</span></span>
* <span data-ttu-id="2f004-107">Caricare i file nella condivisione file e scaricarli.</span><span class="sxs-lookup"><span data-stu-id="2f004-107">Upload and download files to and from your file share.</span></span>
* <span data-ttu-id="2f004-108">Monitorare l'uso effettivo di ogni condivisione file.</span><span class="sxs-lookup"><span data-stu-id="2f004-108">Monitor the actual usage of each file share.</span></span>
* <span data-ttu-id="2f004-109">Rettificare la quota delle dimensioni della condivisione file.</span><span class="sxs-lookup"><span data-stu-id="2f004-109">Adjust the file share size quota.</span></span>
* <span data-ttu-id="2f004-110">Copiare i comandi di montaggio da usare per montare la condivisione file da un client Windows o Linux.</span><span class="sxs-lookup"><span data-stu-id="2f004-110">Copy the mount commands to use to mount your file share from a Windows or Linux client.</span></span>

## <a name="create-file-share"></a><span data-ttu-id="2f004-111">Creare la condivisione file</span><span class="sxs-lookup"><span data-stu-id="2f004-111">Create file share</span></span>
1. <span data-ttu-id="2f004-112">Accedere al portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="2f004-112">Sign in to the Azure portal.</span></span>
2. <span data-ttu-id="2f004-113">Nel menu di navigazione fare clic su **Account di archiviazione** o su **Account di archiviazione (versione classica)**.</span><span class="sxs-lookup"><span data-stu-id="2f004-113">On the navigation menu, click **Storage accounts** or **Storage accounts (classic)**.</span></span>
    
    ![Schermata che illustra come creare una condivisione file nel portale](media/storage-file-how-to-use-files-portal/use-files-portal-create-file-share1.png)

3. <span data-ttu-id="2f004-115">Scegliere l'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="2f004-115">Choose your storage account.</span></span>

    ![Schermata che illustra come creare una condivisione file nel portale](media/storage-file-how-to-use-files-portal/use-files-portal-create-file-share2.png)

4. <span data-ttu-id="2f004-117">Scegliere il servizio "File".</span><span class="sxs-lookup"><span data-stu-id="2f004-117">Choose "Files" service.</span></span>

    ![Schermata che illustra come creare una condivisione file nel portale](media/storage-file-how-to-use-files-portal/use-files-portal-create-file-share3.png)

5. <span data-ttu-id="2f004-119">Fare clic su "Condivisioni file" e selezionare il collegamento per creare la prima condivisione file.</span><span class="sxs-lookup"><span data-stu-id="2f004-119">Click "File shares" and follow the link to create your first file share.</span></span>

    ![Schermata che illustra come creare una condivisione file nel portale](media/storage-file-how-to-use-files-portal/use-files-portal-create-file-share4.png)

6. <span data-ttu-id="2f004-121">Immettere il nome della condivisione e le dimensioni, fino a 5120 GB, per creare la prima condivisione file.</span><span class="sxs-lookup"><span data-stu-id="2f004-121">Fill in the file share name and the size of the file share (up to 5120 GB) to create your first file share.</span></span> <span data-ttu-id="2f004-122">Dopo che la condivisione file è stata creata, è possibile montarla da qualsiasi file system che supporti SMB 2.1 o SMB 3.0.</span><span class="sxs-lookup"><span data-stu-id="2f004-122">Once the file share has been created, you can mount it from any file system that supports SMB 2.1 or SMB 3.0.</span></span> <span data-ttu-id="2f004-123">È possibile fare clic su **Quota** nella condivisione file per modificare le dimensioni del file fino a 5120 GB.</span><span class="sxs-lookup"><span data-stu-id="2f004-123">You could click on **Quota** on the file share to change the size of the file up to 5120 GB.</span></span> <span data-ttu-id="2f004-124">Vedere [Calcolatore prezzi di Azure](https://azure.microsoft.com/pricing/calculator/) per un preventivo dei costi di archiviazione relativi all'uso di Archiviazione file di Azure.</span><span class="sxs-lookup"><span data-stu-id="2f004-124">Please refer to [Azure Pricing Calculator](https://azure.microsoft.com/pricing/calculator/) to estimate the storage cost of using Azure File storage.</span></span>

    ![Schermata che illustra come creare una condivisione file nel portale](media/storage-file-how-to-use-files-portal/use-files-portal-create-file-share5.png)

## <a name="upload-and-download-files"></a><span data-ttu-id="2f004-126">Caricare e scaricare file</span><span class="sxs-lookup"><span data-stu-id="2f004-126">Upload and download files</span></span>
1. <span data-ttu-id="2f004-127">Scegliere una condivisione file già creata.</span><span class="sxs-lookup"><span data-stu-id="2f004-127">Choose one file share your have already created.</span></span>

    ![Schermata che illustra come caricare e scaricare file nel portale](media/storage-file-how-to-use-files-portal/use-files-portal-upload-file1.png)

2. <span data-ttu-id="2f004-129">Fare clic su **Carica** per aprire l'interfaccia utente per il caricamento dei file.</span><span class="sxs-lookup"><span data-stu-id="2f004-129">Click **Upload** to open the user interface for files uploading.</span></span>

    ![Schermata che illustra come caricare file nel portale](media/storage-file-how-to-use-files-portal/use-files-portal-upload-file2.png)

## <a name="connect-to-file-share"></a><span data-ttu-id="2f004-131">Connettersi alla condivisione file</span><span class="sxs-lookup"><span data-stu-id="2f004-131">Connect to file share</span></span>
-  <span data-ttu-id="2f004-132">Fare clic su **Connetti** per ottenere la riga di comando per montare la condivisione file da Windows e Linux.</span><span class="sxs-lookup"><span data-stu-id="2f004-132">Click **Connect** to get the command line for mounting the file share from Windows and Linux.</span></span> <span data-ttu-id="2f004-133">Gli utenti Linux possono vedere anche [Come usare Archiviazione file di Azure con Linux](storage-how-to-use-files-linux.md) per altre istruzioni sul montaggio per le altre distribuzioni Linux.</span><span class="sxs-lookup"><span data-stu-id="2f004-133">For Linux users, you can also refer to [How to use Azure File storage with Linux](storage-how-to-use-files-linux.md) for more mounting instructions for other Linux distributions.</span></span>

    ![Schermata che illustra come montare la condivisione file](media/storage-file-how-to-use-files-portal/use-files-portal-connect.png)
-  <span data-ttu-id="2f004-135">È possibile copiare i comandi per il montaggio della condivisione file in Windows o Linux ed eseguirla dalla VM di Azure o dal computer locale.</span><span class="sxs-lookup"><span data-stu-id="2f004-135">You can copy the commands for mounting file share on Windows or Linux and run it from you Azure VM or on-premises machine.</span></span>

    ![Screenshot che illustra i comandi di montaggio per Windows e Linux](media/storage-file-how-to-use-files-portal/use-files-portal-show-mount-commands.png)

<span data-ttu-id="2f004-137">**Suggerimento:**</span><span class="sxs-lookup"><span data-stu-id="2f004-137">**Tip:**</span></span>  
<span data-ttu-id="2f004-138">Per trovare la chiave di accesso dell'account di archiviazione per il montaggio, fare clic su **Visualizza chiavi di accesso per questo account di archiviazione** nella parte inferiore della pagina della connessione.</span><span class="sxs-lookup"><span data-stu-id="2f004-138">To find the storage account access key for mounting, click on **View access keys for this storage account** at the bottom of the connect page.</span></span>

## <a name="see-also"></a><span data-ttu-id="2f004-139">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="2f004-139">See also</span></span>
<span data-ttu-id="2f004-140">Vedere i collegamenti seguenti per ulteriori informazioni sull'archiviazione file di Azure.</span><span class="sxs-lookup"><span data-stu-id="2f004-140">See these links for more information about Azure File storage.</span></span>

* [<span data-ttu-id="2f004-141">Domande frequenti</span><span class="sxs-lookup"><span data-stu-id="2f004-141">FAQ</span></span>](storage-files-faq.md)
* [<span data-ttu-id="2f004-142">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="2f004-142">Troubleshooting</span></span>](storage-troubleshoot-file-connection-problems.md)