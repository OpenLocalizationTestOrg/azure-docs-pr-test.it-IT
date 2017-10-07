---
title: disco rigido virtuale aaaUpload file tooAzure DevTest Labs tramite Esplora archivi di Microsoft Azure | Documenti Microsoft
description: Caricare l'account di archiviazione del toolab file disco rigido virtuale tramite Esplora archivi di Microsoft Azure
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
ms.openlocfilehash: 686691e3676cea4b2d7cd8bf045bc43a792c667e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="upload-vhd-file-toolabs-storage-account-using-microsoft-azure-storage-explorer"></a><span data-ttu-id="41b9c-103">Caricare l'account di archiviazione del toolab file disco rigido virtuale tramite Esplora archivi di Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="41b9c-103">Upload VHD file toolab's storage account using Microsoft Azure Storage Explorer</span></span>

[!INCLUDE [devtest-lab-upload-vhd-selector](../../includes/devtest-lab-upload-vhd-selector.md)]

<span data-ttu-id="41b9c-104">In Azure DevTest Labs, i file VHD possono essere utilizzato toocreate immagini personalizzate, che sono utilizzati tooprovision le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="41b9c-104">In Azure DevTest Labs, VHD files can be used toocreate custom images, which are used tooprovision virtual machines.</span></span> <span data-ttu-id="41b9c-105">Questo articolo illustra come toouse [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) account di archiviazione dell'ambiente di test di tooa tooupload un disco rigido virtuale del file.</span><span class="sxs-lookup"><span data-stu-id="41b9c-105">This article illustrates how toouse [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) tooupload a VHD file tooa lab's storage account.</span></span> <span data-ttu-id="41b9c-106">Dopo aver caricato il file VHD, hello [passaggi successivi sezione](#next-steps) elenca alcuni articoli che illustrano come un'immagine personalizzata da hello toocreate caricamento del file di disco rigido virtuale.</span><span class="sxs-lookup"><span data-stu-id="41b9c-106">Once you've uploaded your VHD file, hello [Next steps section](#next-steps) lists some articles that illustrate how toocreate a custom image from hello uploaded VHD file.</span></span> <span data-ttu-id="41b9c-107">Per altre informazioni sui dischi e sui dischi rigidi virtuali in Azure, vedere [Informazioni sui dischi e sui dischi rigidi virtuali per le macchine virtuali](../virtual-machines/linux/about-disks-and-vhds.md)</span><span class="sxs-lookup"><span data-stu-id="41b9c-107">For more information about disks and VHDs in Azure, see [About disks and VHDs for virtual machines](../virtual-machines/linux/about-disks-and-vhds.md)</span></span>

## <a name="step-by-step-instructions"></a><span data-ttu-id="41b9c-108">Istruzioni dettagliate</span><span class="sxs-lookup"><span data-stu-id="41b9c-108">Step-by-step instructions</span></span>

<span data-ttu-id="41b9c-109">Hello seguenti passaggi percorso di caricamento di un disco rigido virtuale del file Labs tooDevTest utilizzando [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="41b9c-109">hello following steps walk you through uploading a VHD file tooDevTest Labs using [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span></span>

1. <span data-ttu-id="41b9c-110">[Scaricare e installare hello la versione più recente di Microsoft Azure Storage Explorer hello](http://www.storageexplorer.com).</span><span class="sxs-lookup"><span data-stu-id="41b9c-110">[Download and install hello latest version of hello Microsoft Azure Storage Explorer](http://www.storageexplorer.com).</span></span>

1. <span data-ttu-id="41b9c-111">Ottenere il nome di hello dell'account di archiviazione dell'ambiente di test di hello utilizzando hello portale di Azure:</span><span class="sxs-lookup"><span data-stu-id="41b9c-111">Get hello name of hello lab's storage account using hello Azure portal:</span></span>

    1. <span data-ttu-id="41b9c-112">Accedi toohello [portale di Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="41b9c-112">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
    
    1. <span data-ttu-id="41b9c-113">Selezionare **più servizi**, quindi selezionare **DevTest Labs** dall'elenco di hello.</span><span class="sxs-lookup"><span data-stu-id="41b9c-113">Select **More services**, and then select **DevTest Labs** from hello list.</span></span>
    
    1. <span data-ttu-id="41b9c-114">Elenco dei laboratori hello selezionare lab desiderato hello.</span><span class="sxs-lookup"><span data-stu-id="41b9c-114">From hello list of labs, select hello desired lab.</span></span>  
    
    1. <span data-ttu-id="41b9c-115">Nel pannello del lab hello, selezionare **configurazione**.</span><span class="sxs-lookup"><span data-stu-id="41b9c-115">On hello lab's blade, select **Configuration**.</span></span> 
    
    1. <span data-ttu-id="41b9c-116">Lab hello **configurazione** pannello seleziona **immagini personalizzate (VHD)**.</span><span class="sxs-lookup"><span data-stu-id="41b9c-116">On hello lab **Configuration** blade, select **Custom images (VHDs)**.</span></span>
    
    1. <span data-ttu-id="41b9c-117">In hello **immagini personalizzate** pannello selezionare **+ Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="41b9c-117">On hello **Custom images** blade, Select **+Add**.</span></span> 
    
    1. <span data-ttu-id="41b9c-118">In hello **immagine personalizzata** pannello seleziona **VHD**.</span><span class="sxs-lookup"><span data-stu-id="41b9c-118">On hello **Custom image** blade, select **VHD**.</span></span>
    
    1. <span data-ttu-id="41b9c-119">In hello **VHD** pannello seleziona **caricare un disco rigido virtuale con PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="41b9c-119">On hello **VHD** blade, select **Upload a VHD using PowerShell**.</span></span>
    
        ![Carica un file VHD con PowerShell][0]
    
    1. <span data-ttu-id="41b9c-121">Hello **carica un'immagine con PowerShell** pannello viene visualizzato un toohello chiamata **Add-AzureVhd** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="41b9c-121">hello **Upload an image using PowerShell** blade displays a call toohello **Add-AzureVhd** cmdlet.</span></span> <span data-ttu-id="41b9c-122">primo parametro Hello (*destinazione*) il nome di account di archiviazione di hello per lab hello in hello seguente formato:</span><span class="sxs-lookup"><span data-stu-id="41b9c-122">hello first parameter (*Destination*) contains hello storage account name for hello lab in hello following format:</span></span>
    
        <span data-ttu-id="41b9c-123">https://<STORAGE-ACCOUNT-NAME>.blob.core.windows.net/uploads/...</span><span class="sxs-lookup"><span data-stu-id="41b9c-123">https://<STORAGE-ACCOUNT-NAME>.blob.core.windows.net/uploads/...</span></span> 

    1. <span data-ttu-id="41b9c-124">Prendere nota del nome di account di archiviazione hello perché è usato nei passaggi successivi.</span><span class="sxs-lookup"><span data-stu-id="41b9c-124">Make note of hello storage account name as it is used in later steps.</span></span>
    
1. <span data-ttu-id="41b9c-125">Connettersi tooan account di sottoscrizione di Azure tramite Esplora archivi.</span><span class="sxs-lookup"><span data-stu-id="41b9c-125">Connect tooan Azure subscription account using Storage Explorer.</span></span>

    > [!TIP] 
    > 
    > <span data-ttu-id="41b9c-126">Esplora archivi supporta diverse opzioni di connessione.</span><span class="sxs-lookup"><span data-stu-id="41b9c-126">Storage Explorer supports several connection options.</span></span> <span data-ttu-id="41b9c-127">In questa sezione viene illustrato l'account di archiviazione tooa connessione associato alla sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="41b9c-127">This section illustrates connecting tooa storage account associated with your Azure subscription.</span></span> <span data-ttu-id="41b9c-128">toosee hello altre opzioni di connessione supportate da Esplora archivi, consultare l'articolo toohello [Introduzione a soluzioni di archiviazione](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="41b9c-128">toosee hello other connection options supported by Storage Explorer, refer toohello article, [Getting started with Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span></span>
 
    1. <span data-ttu-id="41b9c-129">Aprire Esplora archivi.</span><span class="sxs-lookup"><span data-stu-id="41b9c-129">Open Storage Explorer.</span></span>
    
    1. <span data-ttu-id="41b9c-130">In Esplora archivi, selezionare **Azure Account settings** (Impostazioni account Azure).</span><span class="sxs-lookup"><span data-stu-id="41b9c-130">In Storage Explorer, select **Azure Account settings**.</span></span> 
    
        ![Azure Account settings][1]
    
    1. <span data-ttu-id="41b9c-132">riquadro di sinistra Hello consente di visualizzare gli account Microsoft hello a che è effettuato l'accesso.</span><span class="sxs-lookup"><span data-stu-id="41b9c-132">hello left pane displays hello Microsoft accounts you've logged in to.</span></span> <span data-ttu-id="41b9c-133">tooconnect tooanother account, selezionare **aggiungere un account**e seguire hello toosign di finestre di dialogo con un account Microsoft associato ad almeno una sottoscrizione di Azure attiva.</span><span class="sxs-lookup"><span data-stu-id="41b9c-133">tooconnect tooanother account, select **Add an account**, and follow hello dialogs toosign in with a Microsoft account that is associated with at least one active Azure subscription.</span></span>
    
        ![Aggiungi un account][2]
    
    1. <span data-ttu-id="41b9c-135">Quando si accede correttamente con un account Microsoft, riquadro di sinistra hello popola con hello le sottoscrizioni di Azure associate all'account.</span><span class="sxs-lookup"><span data-stu-id="41b9c-135">Once you successfully sign in with a Microsoft account, hello left pane populates with hello Azure subscriptions associated with that account.</span></span> <span data-ttu-id="41b9c-136">Selezionare le sottoscrizioni di Azure a cui desidera toowork e quindi selezionare di hello **applica**.</span><span class="sxs-lookup"><span data-stu-id="41b9c-136">Select hello Azure subscriptions with which you want toowork, and then select **Apply**.</span></span> <span data-ttu-id="41b9c-137">(Selezione **tutte le sottoscrizioni** hello di attiva o disattiva la selezione di tutti o nessuno dei hello elencate le sottoscrizioni di Azure.)</span><span class="sxs-lookup"><span data-stu-id="41b9c-137">(Selecting **All subscriptions** toggles hello selection of all or none of hello listed Azure subscriptions.)</span></span>
    
        ![Selezionare le sottoscrizioni di Azure][3]
    
    1. <span data-ttu-id="41b9c-139">riquadro di sinistra Hello consente di visualizzare gli account di archiviazione hello associati alle sottoscrizioni Azure hello selezionato.</span><span class="sxs-lookup"><span data-stu-id="41b9c-139">hello left pane displays hello storage accounts associated with hello selected Azure subscriptions.</span></span>
    
        ![Sottoscrizioni di Azure selezionate][4]

1. <span data-ttu-id="41b9c-141">Individuare l'account di archiviazione dell'ambiente di test di hello:</span><span class="sxs-lookup"><span data-stu-id="41b9c-141">Locate hello lab's storage account:</span></span>

    1. <span data-ttu-id="41b9c-142">Nel riquadro sinistro di Esplora archivi hello, individuare ed espandere nodo hello per la sottoscrizione di Azure che possiede lab hello hello.</span><span class="sxs-lookup"><span data-stu-id="41b9c-142">In hello Storage Explorer left pane, locate, and expand hello node for hello Azure subscription that owns hello lab.</span></span>
    
    1. <span data-ttu-id="41b9c-143">Nel nodo della sottoscrizione hello, espandere **gli account di archiviazione**.</span><span class="sxs-lookup"><span data-stu-id="41b9c-143">Under hello subscription's node, expand **Storage Accounts**.</span></span>

    1. <span data-ttu-id="41b9c-144">Espandere i nodi del lab hello storage account nodo tooreveal per **contenitori Blob**, **condivisioni File**, **code**, e **tabelle**.</span><span class="sxs-lookup"><span data-stu-id="41b9c-144">Expand hello lab's storage account node tooreveal nodes for **Blob Containers**, **File Shares**, **Queues**, and **Tables**.</span></span>
    
    1. <span data-ttu-id="41b9c-145">Espandere hello **contenitori Blob** nodo.</span><span class="sxs-lookup"><span data-stu-id="41b9c-145">Expand hello **Blob Containers** node.</span></span>
    
    1. <span data-ttu-id="41b9c-146">Selezionare il contenuto di hello caricamenti blob contenitore toodisplay nel riquadro di destra hello.</span><span class="sxs-lookup"><span data-stu-id="41b9c-146">Select hello uploads blob container toodisplay its contents in hello right pane.</span></span>
        
        ![Caricare una directory][5]

1. <span data-ttu-id="41b9c-148">Caricare file VHD hello tramite Esplora archivi:</span><span class="sxs-lookup"><span data-stu-id="41b9c-148">Upload hello VHD file using Storage Explorer:</span></span>

    1. <span data-ttu-id="41b9c-149">Nel riquadro destro di Esplora archivi hello, vedrai un elenco di BLOB hello in hello **Carica** contenitore blob dell'account di archiviazione dell'ambiente di test di hello.</span><span class="sxs-lookup"><span data-stu-id="41b9c-149">In hello Storage Explorer right pane, you should see a listing of hello blobs in hello **uploads** blob container of hello lab's storage account.</span></span> <span data-ttu-id="41b9c-150">Nella barra degli strumenti editor blob hello, selezionare **caricare**</span><span class="sxs-lookup"><span data-stu-id="41b9c-150">On hello blob editor toolbar, select **Upload**</span></span> 
        
        ![Pulsante Carica][6]
    
    1. <span data-ttu-id="41b9c-152">Da hello **caricare** menu a discesa, seleziona **caricare i file...** .</span><span class="sxs-lookup"><span data-stu-id="41b9c-152">From hello **Upload** drop-down menu, select **Upload files...**.</span></span>
    
    1. <span data-ttu-id="41b9c-153">In hello **caricare file** finestra di dialogo, i puntini di sospensione hello selezionare.</span><span class="sxs-lookup"><span data-stu-id="41b9c-153">On hello **Upload files** dialog, select hello ellipsis.</span></span>
        
        ![Selezionare il file][8]  

    1. <span data-ttu-id="41b9c-155">In hello **tooupload selezionare file** finestra di dialogo Sfoglia toohello desiderato di file VHD, selezionarlo e quindi selezionare **aprire**.</span><span class="sxs-lookup"><span data-stu-id="41b9c-155">On hello **Select files tooupload** dialog, browse toohello desired VHD file, select it, and then select **Open**.</span></span>
    
    1. <span data-ttu-id="41b9c-156">Quando restituito toohello **caricare file** finestra di dialogo Modifica **Blob tipo** troppo**Blob di pagine**.</span><span class="sxs-lookup"><span data-stu-id="41b9c-156">When returned toohello **Upload files** dialog, change **Blob type** too**Page Blob**.</span></span>
    
    1. <span data-ttu-id="41b9c-157">Selezionare **Carica**.</span><span class="sxs-lookup"><span data-stu-id="41b9c-157">Select **Upload**.</span></span>

        ![Selezionare il file][9]  
    
    1. <span data-ttu-id="41b9c-159">Esplora archivi Hello **Log attività** riquadro viene visualizzato lo stato di download hello (insieme ai collegamenti toocancel hello caricamento).</span><span class="sxs-lookup"><span data-stu-id="41b9c-159">hello Storage Explorer **Activity Log** pane shows hello download status (along with links toocancel hello upload).</span></span> <span data-ttu-id="41b9c-160">processo Hello di caricamento di un file VHD può essere lungo a seconda delle dimensioni di hello del file VHD hello e la velocità della connessione.</span><span class="sxs-lookup"><span data-stu-id="41b9c-160">hello process of uploading a VHD file can be lengthy depending on hello size of hello VHD file and your connection speed.</span></span> 

        ![Stato upload-file][10]  

## <a name="next-steps"></a><span data-ttu-id="41b9c-162">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="41b9c-162">Next steps</span></span>

- [<span data-ttu-id="41b9c-163">Creare un'immagine personalizzata in Azure DevTest Labs da un file VHD utilizzando hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="41b9c-163">Create a custom image in Azure DevTest Labs from a VHD file using hello Azure portal</span></span>](devtest-lab-create-template.md)
- [<span data-ttu-id="41b9c-164">Creare un'immagine personalizzata in Azure DevTest Labs da un file VHD usando PowerShell</span><span class="sxs-lookup"><span data-stu-id="41b9c-164">Create a custom image in Azure DevTest Labs from a VHD file using PowerShell</span></span>](devtest-lab-create-custom-image-from-vhd-using-powershell.md)

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
