---
title: Caricare un file VHD in Azure DevTest Labs usando Esplora archivi di Microsoft Azure | Microsoft Docs
description: Caricare un file VHD nell'account di archiviazione del lab usando Esplora archivi di Microsoft Azure
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
ms.openlocfilehash: 502e2536fb0fd2e9dfc4c7b85a6fb4e18202f38f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="upload-vhd-file-to-labs-storage-account-using-microsoft-azure-storage-explorer"></a><span data-ttu-id="a2ff3-103">Caricare un file VHD nell'account di archiviazione del lab usando Esplora archivi di Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="a2ff3-103">Upload VHD file to lab's storage account using Microsoft Azure Storage Explorer</span></span>

[!INCLUDE [devtest-lab-upload-vhd-selector](../../includes/devtest-lab-upload-vhd-selector.md)]

<span data-ttu-id="a2ff3-104">In Azure DevTest Labs è possibile usare i file VHD per creare immagini personalizzate da usare per il provisioning di macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="a2ff3-104">In Azure DevTest Labs, VHD files can be used to create custom images, which are used to provision virtual machines.</span></span> <span data-ttu-id="a2ff3-105">In questo articolo viene illustrato come usare [Esplora archivi di Microsoft Azure](../vs-azure-tools-storage-manage-with-storage-explorer.md) per caricare un file VHD nell'account di archiviazione di un lab.</span><span class="sxs-lookup"><span data-stu-id="a2ff3-105">This article illustrates how to use [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) to upload a VHD file to a lab's storage account.</span></span> <span data-ttu-id="a2ff3-106">Dopo avere caricato il file VHD, vedere la [sezione Passaggi successivi](#next-steps) per un elenco di articoli che illustrano come creare un'immagine personalizzata dal file VHD caricato.</span><span class="sxs-lookup"><span data-stu-id="a2ff3-106">Once you've uploaded your VHD file, the [Next steps section](#next-steps) lists some articles that illustrate how to create a custom image from the uploaded VHD file.</span></span> <span data-ttu-id="a2ff3-107">Per altre informazioni sui dischi e sui dischi rigidi virtuali in Azure, vedere [Informazioni sui dischi e sui dischi rigidi virtuali per le macchine virtuali](../virtual-machines/linux/about-disks-and-vhds.md)</span><span class="sxs-lookup"><span data-stu-id="a2ff3-107">For more information about disks and VHDs in Azure, see [About disks and VHDs for virtual machines](../virtual-machines/linux/about-disks-and-vhds.md)</span></span>

## <a name="step-by-step-instructions"></a><span data-ttu-id="a2ff3-108">Istruzioni dettagliate</span><span class="sxs-lookup"><span data-stu-id="a2ff3-108">Step-by-step instructions</span></span>

<span data-ttu-id="a2ff3-109">La procedura seguente illustra come caricare un file VHD in DevTest Labs usando [Esplora archivi di Microsoft Azure](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="a2ff3-109">The following steps walk you through uploading a VHD file to DevTest Labs using [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span></span>

1. <span data-ttu-id="a2ff3-110">[Scaricare e installare la versione più recente di Esplora archivi di Microsoft Azure](http://www.storageexplorer.com).</span><span class="sxs-lookup"><span data-stu-id="a2ff3-110">[Download and install the latest version of the Microsoft Azure Storage Explorer](http://www.storageexplorer.com).</span></span>

1. <span data-ttu-id="a2ff3-111">Ottenere il nome dell'account di archiviazione del lab usando il portale di Azure:</span><span class="sxs-lookup"><span data-stu-id="a2ff3-111">Get the name of the lab's storage account using the Azure portal:</span></span>

    1. <span data-ttu-id="a2ff3-112">Accedere al [portale di Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="a2ff3-112">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
    
    1. <span data-ttu-id="a2ff3-113">Selezionare **Altri servizi** e quindi **DevTest Labs** dall'elenco.</span><span class="sxs-lookup"><span data-stu-id="a2ff3-113">Select **More services**, and then select **DevTest Labs** from the list.</span></span>
    
    1. <span data-ttu-id="a2ff3-114">Nell'elenco dei lab selezionare il lab desiderato.</span><span class="sxs-lookup"><span data-stu-id="a2ff3-114">From the list of labs, select the desired lab.</span></span>  
    
    1. <span data-ttu-id="a2ff3-115">Nel pannello del lab selezionare **Configurazione**.</span><span class="sxs-lookup"><span data-stu-id="a2ff3-115">On the lab's blade, select **Configuration**.</span></span> 
    
    1. <span data-ttu-id="a2ff3-116">Nel pannello **Configurazione** del lab selezionare **Immagini personalizzate (dischi rigidi virtuali)**.</span><span class="sxs-lookup"><span data-stu-id="a2ff3-116">On the lab **Configuration** blade, select **Custom images (VHDs)**.</span></span>
    
    1. <span data-ttu-id="a2ff3-117">Nel pannello **Immagini personalizzate** selezionare **+Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="a2ff3-117">On the **Custom images** blade, Select **+Add**.</span></span> 
    
    1. <span data-ttu-id="a2ff3-118">Nel pannello **Immagine personalizzata** selezionare **VHD**.</span><span class="sxs-lookup"><span data-stu-id="a2ff3-118">On the **Custom image** blade, select **VHD**.</span></span>
    
    1. <span data-ttu-id="a2ff3-119">Nel pannello **VHD** selezionare l'opzione **Carica un file VHD con PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="a2ff3-119">On the **VHD** blade, select **Upload a VHD using PowerShell**.</span></span>
    
        ![Carica un file VHD con PowerShell][0]
    
    1. <span data-ttu-id="a2ff3-121">Nel pannello **Upload an image using PowerShell** (Carica un'immagine usando PowerShell) è visualizzata una chiamata al cmdlet **Add-AzureVhd**.</span><span class="sxs-lookup"><span data-stu-id="a2ff3-121">The **Upload an image using PowerShell** blade displays a call to the **Add-AzureVhd** cmdlet.</span></span> <span data-ttu-id="a2ff3-122">Il primo parametro (*Destination*) contiene il nome dell'account di archiviazione per il lab nel formato seguente:</span><span class="sxs-lookup"><span data-stu-id="a2ff3-122">The first parameter (*Destination*) contains the storage account name for the lab in the following format:</span></span>
    
        <span data-ttu-id="a2ff3-123">https://<STORAGE-ACCOUNT-NAME>.blob.core.windows.net/uploads/...</span><span class="sxs-lookup"><span data-stu-id="a2ff3-123">https://<STORAGE-ACCOUNT-NAME>.blob.core.windows.net/uploads/...</span></span> 

    1. <span data-ttu-id="a2ff3-124">Prendere nota del nome dell'account di archiviazione usato nei passaggi successivi.</span><span class="sxs-lookup"><span data-stu-id="a2ff3-124">Make note of the storage account name as it is used in later steps.</span></span>
    
1. <span data-ttu-id="a2ff3-125">Connettersi a un account di sottoscrizione di Azure usando Esplora archivi.</span><span class="sxs-lookup"><span data-stu-id="a2ff3-125">Connect to an Azure subscription account using Storage Explorer.</span></span>

    > [!TIP] 
    > 
    > <span data-ttu-id="a2ff3-126">Esplora archivi supporta diverse opzioni di connessione.</span><span class="sxs-lookup"><span data-stu-id="a2ff3-126">Storage Explorer supports several connection options.</span></span> <span data-ttu-id="a2ff3-127">In questa sezione viene illustrato come connettersi a un account di archiviazione associato alla sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="a2ff3-127">This section illustrates connecting to a storage account associated with your Azure subscription.</span></span> <span data-ttu-id="a2ff3-128">Per visualizzare altre opzioni di connessione supportate da Esplora archivi, vedere l'articolo [Introduzione a Esplora archivi](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="a2ff3-128">To see the other connection options supported by Storage Explorer, refer to the article, [Getting started with Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span></span>
 
    1. <span data-ttu-id="a2ff3-129">Aprire Esplora archivi.</span><span class="sxs-lookup"><span data-stu-id="a2ff3-129">Open Storage Explorer.</span></span>
    
    1. <span data-ttu-id="a2ff3-130">In Esplora archivi, selezionare **Azure Account settings** (Impostazioni account Azure).</span><span class="sxs-lookup"><span data-stu-id="a2ff3-130">In Storage Explorer, select **Azure Account settings**.</span></span> 
    
        ![Azure Account settings][1]
    
    1. <span data-ttu-id="a2ff3-132">Nel riquadro sinistro vengono visualizzati gli account Microsoft a cui si è connessi.</span><span class="sxs-lookup"><span data-stu-id="a2ff3-132">The left pane displays the Microsoft accounts you've logged in to.</span></span> <span data-ttu-id="a2ff3-133">Per connettersi a un altro account, selezionare **Aggiungi un account**e seguire le istruzioni nelle finestre di dialogo per accedere con un account Microsoft associato ad almeno una sottoscrizione di Azure attiva.</span><span class="sxs-lookup"><span data-stu-id="a2ff3-133">To connect to another account, select **Add an account**, and follow the dialogs to sign in with a Microsoft account that is associated with at least one active Azure subscription.</span></span>
    
        ![Aggiungi un account][2]
    
    1. <span data-ttu-id="a2ff3-135">Dopo avere effettuato l'acceso con un account Microsoft, il riquadro sinistro verrà popolato con le sottoscrizioni di Azure associate a quell'account.</span><span class="sxs-lookup"><span data-stu-id="a2ff3-135">Once you successfully sign in with a Microsoft account, the left pane populates with the Azure subscriptions associated with that account.</span></span> <span data-ttu-id="a2ff3-136">Selezionare le sottoscrizioni di Azure da utilizzare e quindi selezionare **Applica**.</span><span class="sxs-lookup"><span data-stu-id="a2ff3-136">Select the Azure subscriptions with which you want to work, and then select **Apply**.</span></span> <span data-ttu-id="a2ff3-137">Selezionando **Tutte le sottoscrizioni** , viene alternata la selezione di tutte o di nessuna delle sottoscrizioni di Azure elencate.</span><span class="sxs-lookup"><span data-stu-id="a2ff3-137">(Selecting **All subscriptions** toggles the selection of all or none of the listed Azure subscriptions.)</span></span>
    
        ![Selezionare le sottoscrizioni di Azure][3]
    
    1. <span data-ttu-id="a2ff3-139">Il riquadro sinistro mostra gli account di archiviazione associati alle sottoscrizioni di Azure selezionate.</span><span class="sxs-lookup"><span data-stu-id="a2ff3-139">The left pane displays the storage accounts associated with the selected Azure subscriptions.</span></span>
    
        ![Sottoscrizioni di Azure selezionate][4]

1. <span data-ttu-id="a2ff3-141">Individuare l'account di archiviazione del lab:</span><span class="sxs-lookup"><span data-stu-id="a2ff3-141">Locate the lab's storage account:</span></span>

    1. <span data-ttu-id="a2ff3-142">Nel riquadro sinistro di Esplora archivi, individuare ed espandere il nodo per la sottoscrizione di Azure proprietaria del lab.</span><span class="sxs-lookup"><span data-stu-id="a2ff3-142">In the Storage Explorer left pane, locate, and expand the node for the Azure subscription that owns the lab.</span></span>
    
    1. <span data-ttu-id="a2ff3-143">Nel nodo della sottoscrizione, espandere **Account di archiviazione**.</span><span class="sxs-lookup"><span data-stu-id="a2ff3-143">Under the subscription's node, expand **Storage Accounts**.</span></span>

    1. <span data-ttu-id="a2ff3-144">Espandere il nodo dell'account di archiviazione del lab per mostrare i nodi per **Contenitori BLOB**, **Condivisioni file**, **Code** e **Tabelle**.</span><span class="sxs-lookup"><span data-stu-id="a2ff3-144">Expand the lab's storage account node to reveal nodes for **Blob Containers**, **File Shares**, **Queues**, and **Tables**.</span></span>
    
    1. <span data-ttu-id="a2ff3-145">Espandere il nodo **Contenitori BLOB**.</span><span class="sxs-lookup"><span data-stu-id="a2ff3-145">Expand the **Blob Containers** node.</span></span>
    
    1. <span data-ttu-id="a2ff3-146">Selezionare il contenitore BLOB dei caricamenti per visualizzarne il contenuto nel riquadro di destra.</span><span class="sxs-lookup"><span data-stu-id="a2ff3-146">Select the uploads blob container to display its contents in the right pane.</span></span>
        
        ![Caricare una directory][5]

1. <span data-ttu-id="a2ff3-148">Caricare il file VHD tramite Esplora archivi:</span><span class="sxs-lookup"><span data-stu-id="a2ff3-148">Upload the VHD file using Storage Explorer:</span></span>

    1. <span data-ttu-id="a2ff3-149">Nel riquadro di destra di Esplora archivi dovrebbe essere visualizzato un elenco dei BLOB nel contenitore BLOB dei **caricamenti** dell'account di archiviazione del lab.</span><span class="sxs-lookup"><span data-stu-id="a2ff3-149">In the Storage Explorer right pane, you should see a listing of the blobs in the **uploads** blob container of the lab's storage account.</span></span> <span data-ttu-id="a2ff3-150">Sulla barra degli strumenti dell'editor di blob, selezionare **Carica**</span><span class="sxs-lookup"><span data-stu-id="a2ff3-150">On the blob editor toolbar, select **Upload**</span></span> 
        
        ![Pulsante Carica][6]
    
    1. <span data-ttu-id="a2ff3-152">Dal menu a discesa **Carica**, selezionare **Carica file...**.</span><span class="sxs-lookup"><span data-stu-id="a2ff3-152">From the **Upload** drop-down menu, select **Upload files...**.</span></span>
    
    1. <span data-ttu-id="a2ff3-153">Nella finestra di dialogo **Carica file**, selezionare i puntini di sospensione.</span><span class="sxs-lookup"><span data-stu-id="a2ff3-153">On the **Upload files** dialog, select the ellipsis.</span></span>
        
        ![Selezionare il file][8]  

    1. <span data-ttu-id="a2ff3-155">Nella finestra di dialogo **Seleziona file da caricare** selezionare il file VHD desiderato, quindi selezionare **Apri**.</span><span class="sxs-lookup"><span data-stu-id="a2ff3-155">On the **Select files to upload** dialog, browse to the desired VHD file, select it, and then select **Open**.</span></span>
    
    1. <span data-ttu-id="a2ff3-156">Verrà nuovamente visualizzata la finestra di dialogo **Carica file**, modificare **Tipo BLOB** in **BLOB di pagine**.</span><span class="sxs-lookup"><span data-stu-id="a2ff3-156">When returned to the **Upload files** dialog, change **Blob type** to **Page Blob**.</span></span>
    
    1. <span data-ttu-id="a2ff3-157">Selezionare **Carica**.</span><span class="sxs-lookup"><span data-stu-id="a2ff3-157">Select **Upload**.</span></span>

        ![Selezionare il file][9]  
    
    1. <span data-ttu-id="a2ff3-159">Il riquadro **Log attività** di Esplora archivi mostra lo stato di download e i collegamenti per annullare il caricamento.</span><span class="sxs-lookup"><span data-stu-id="a2ff3-159">The Storage Explorer **Activity Log** pane shows the download status (along with links to cancel the upload).</span></span> <span data-ttu-id="a2ff3-160">Il processo di caricamento di un file VHD può richiedere molto tempo a seconda delle dimensioni del file VHD e della velocità della connessione.</span><span class="sxs-lookup"><span data-stu-id="a2ff3-160">The process of uploading a VHD file can be lengthy depending on the size of the VHD file and your connection speed.</span></span> 

        ![Stato upload-file][10]  

## <a name="next-steps"></a><span data-ttu-id="a2ff3-162">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a2ff3-162">Next steps</span></span>

- [<span data-ttu-id="a2ff3-163">Creare un'immagine personalizzata in Azure DevTest Labs da un file VHD usando il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="a2ff3-163">Create a custom image in Azure DevTest Labs from a VHD file using the Azure portal</span></span>](devtest-lab-create-template.md)
- [<span data-ttu-id="a2ff3-164">Creare un'immagine personalizzata in Azure DevTest Labs da un file VHD usando PowerShell</span><span class="sxs-lookup"><span data-stu-id="a2ff3-164">Create a custom image in Azure DevTest Labs from a VHD file using PowerShell</span></span>](devtest-lab-create-custom-image-from-vhd-using-powershell.md)

[0]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-image-using-psh.png
[1]: ./media/devtest-lab-upload-vhd-using-storage-explorer/settings-icon.png
[2]: ./media/devtest-lab-upload-vhd-using-storage-explorer/add-account-link.png
[3]: ./media/devtest-lab-upload-vhd-using-storage-explorer/subscriptions-list.png
[4]: ./media/devtest-lab-upload-vhd-using-storage-explorer/storage-accounts-list.png
[5]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-dir.png
[6]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-button.png
[7]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-files.png
[8]: ./media/devtest-lab-upload-vhd-using-storage-explorer/select-file.png
[9]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-file.png
[10]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-status.png
