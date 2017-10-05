---
title: Uso di Storage Explorer (anteprima) con Archiviazione file di Azure | Microsoft Docs
description: Informazioni su come usare Storage Explorer (anteprima) per l'utilizzo con file e condivisioni file.
services: storage
documentationcenter: na
author: cawaMS
manager: paulyuk
editor: 
ms.assetid: 
ms.service: storage
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/09/2017
ms.author: cawa
ms.openlocfilehash: 964691758254531cb92a5b1cbe055ef61d25dba8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="using-storage-explorer-preview-with-azure-file-storage"></a><span data-ttu-id="afb69-103">Uso di Storage Explorer (anteprima) con Archiviazione file di Azure</span><span class="sxs-lookup"><span data-stu-id="afb69-103">Using Storage Explorer (Preview) with Azure File storage</span></span>

<span data-ttu-id="afb69-104">Archiviazione file di Azure offre condivisioni file nel cloud usando il protocollo Server Message Block (SMB)standard.</span><span class="sxs-lookup"><span data-stu-id="afb69-104">Azure File storage is a service that offers file shares in the cloud using the standard Server Message Block (SMB) Protocol.</span></span> <span data-ttu-id="afb69-105">Sono supportati sia SMB 2.1 che SMB 3.0.</span><span class="sxs-lookup"><span data-stu-id="afb69-105">Both SMB 2.1 and SMB 3.0 are supported.</span></span> <span data-ttu-id="afb69-106">Con Archiviazione file di Azure si può eseguire la migrazione ad Azure delle applicazioni legacy basate su condivisioni file velocemente e senza costose riscritture.</span><span class="sxs-lookup"><span data-stu-id="afb69-106">With Azure File storage, you can migrate legacy applications that rely on file shares to Azure quickly and without costly rewrites.</span></span> <span data-ttu-id="afb69-107">È possibile usare Archiviazione file per esporre pubblicamente dati a livello mondiale o per archiviare privatamente dati applicazione.</span><span class="sxs-lookup"><span data-stu-id="afb69-107">You can use File storage to expose data publicly to the world, or to store application data privately.</span></span> <span data-ttu-id="afb69-108">Questo articolo illustra come usare Storage Explorer (anteprima) per l'utilizzo con file e condivisioni file.</span><span class="sxs-lookup"><span data-stu-id="afb69-108">In this article, you'll learn how to use Storage Explorer (Preview) to work with file shares and files.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="afb69-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="afb69-109">Prerequisites</span></span>

<span data-ttu-id="afb69-110">Per seguire la procedura descritta in questo articolo, è necessario eseguire queste operazioni:</span><span class="sxs-lookup"><span data-stu-id="afb69-110">To complete the steps in this article, you'll need the following:</span></span>

- [<span data-ttu-id="afb69-111">Scaricare e installare Storage Explorer (anteprima)</span><span class="sxs-lookup"><span data-stu-id="afb69-111">Download and install Storage Explorer (preview)</span></span>](http://www.storageexplorer.com/)

- [<span data-ttu-id="afb69-112">Connettersi a un account o a un servizio di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="afb69-112">Connect to a Azure storage account or service</span></span>](https://docs.microsoft.com//azure/vs-azure-tools-storage-manage-with-storage-explorer#connect-to-a-storage-account-or-service)

## <a name="create-a-file-share"></a><span data-ttu-id="afb69-113">Creare una condivisione file</span><span class="sxs-lookup"><span data-stu-id="afb69-113">Create a File Share</span></span>

<span data-ttu-id="afb69-114">Tutti i file devono risiedere in una condivisione file, ovvero un semplice raggruppamento logico di file.</span><span class="sxs-lookup"><span data-stu-id="afb69-114">All files must reside in a file share, which is simply a logical grouping of files.</span></span> <span data-ttu-id="afb69-115">Un account può contenere un numero illimitato di condivisioni file e ogni condivisione può archiviare un numero illimitato di file.</span><span class="sxs-lookup"><span data-stu-id="afb69-115">An account can contain an unlimited number of file shares, and each share can store an unlimited number of files.</span></span>

<span data-ttu-id="afb69-116">La procedura seguente illustra come creare una condivisione file all'interno di Storage Explorer (anteprima).</span><span class="sxs-lookup"><span data-stu-id="afb69-116">The following steps illustrate how to create a file share within Storage Explorer (Preview).</span></span>

1. <span data-ttu-id="afb69-117">Aprire Storage Explorer (anteprima).</span><span class="sxs-lookup"><span data-stu-id="afb69-117">Open Storage Explorer (Preview).</span></span>

2. <span data-ttu-id="afb69-118">Nel riquadro sinistro espandere l'account di archiviazione all'interno del quale si vuole creare la condivisione file.</span><span class="sxs-lookup"><span data-stu-id="afb69-118">In the left pane, expand the storage account within which you wish to create the File Share</span></span>

3. <span data-ttu-id="afb69-119">Fare clic con il pulsante destro del mouse su **Condivisioni file** e scegliere **Crea condivisione file** dal menu di scelta rapida.</span><span class="sxs-lookup"><span data-stu-id="afb69-119">Right-click **File Shares**, and - from the context menu - select **Create File Share**.</span></span>

    ![Crea condivisione file](media/vs-azure-tools-storage-explorer-files/image1.png)

4. <span data-ttu-id="afb69-121">Sotto la cartella **Condivisioni file** verrà visualizzata una casella di testo.</span><span class="sxs-lookup"><span data-stu-id="afb69-121">A text box will appear below the **File Shares** folder.</span></span> <span data-ttu-id="afb69-122">Immettere il nome per la condivisione file.</span><span class="sxs-lookup"><span data-stu-id="afb69-122">Enter the name for your file share.</span></span> <span data-ttu-id="afb69-123">Per un elenco di regole e restrizioni relative alla denominazione delle condivisioni file, vedere la sezione relativa alle [regole di denominazione delle condivisioni](https://docs.microsoft.com//azure/storage/storage-dotnet-how-to-use-blobs#create-a-container).</span><span class="sxs-lookup"><span data-stu-id="afb69-123">See the [Share naming rules](https://docs.microsoft.com//azure/storage/storage-dotnet-how-to-use-blobs#create-a-container) section for a list of rules and restrictions on naming file shares.</span></span>

    ![Denominare la condivisione](media/vs-azure-tools-storage-explorer-files/image2.png)

5. <span data-ttu-id="afb69-125">Premere **INVIO** al termine della creazione della condivisione file o **ESC** per annullare.</span><span class="sxs-lookup"><span data-stu-id="afb69-125">Press **Enter** when done to create the file share, or **Esc** to cancel.</span></span> <span data-ttu-id="afb69-126">La condivisione file appena creata viene visualizzata sotto la cartella **Condivisioni file** per l'account di archiviazione selezionato.</span><span class="sxs-lookup"><span data-stu-id="afb69-126">Once the file share has been successfully created, it will be displayed under the **File Shares** folder for the selected storage account.</span></span>

    ![La nuova condivisione](media/vs-azure-tools-storage-explorer-files/image3.png)

## <a name="view-a-file-shares-contents"></a><span data-ttu-id="afb69-128">Visualizzare il contenuto di una condivisione file</span><span class="sxs-lookup"><span data-stu-id="afb69-128">View a file share's contents</span></span>

<span data-ttu-id="afb69-129">Le condivisioni file contengono file e cartelle, che a loro volta possono contenere file.</span><span class="sxs-lookup"><span data-stu-id="afb69-129">File shares contain files and folders (that can also contain files).</span></span>

<span data-ttu-id="afb69-130">La procedura seguente illustra come visualizzare il contenuto di una condivisione file all'interno di Storage Explorer (anteprima).</span><span class="sxs-lookup"><span data-stu-id="afb69-130">The following steps illustrate how to view the contents of a file share within Storage Explorer (Preview):+</span></span>

1. <span data-ttu-id="afb69-131">Aprire Storage Explorer (anteprima).</span><span class="sxs-lookup"><span data-stu-id="afb69-131">Open Storage Explorer (Preview).</span></span>

2. <span data-ttu-id="afb69-132">Nel riquadro sinistro espandere l'account di archiviazione che contiene la condivisione file da visualizzare.</span><span class="sxs-lookup"><span data-stu-id="afb69-132">In the left pane, expand the storage account containing the file share you wish to view.</span></span>

3. <span data-ttu-id="afb69-133">Espandere le **Condivisioni file** dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="afb69-133">Expand the storage account's **File Shares**.</span></span>

4. <span data-ttu-id="afb69-134">Fare clic con il pulsante destro del mouse sulla condivisione file da visualizzare e scegliere **Apri** dal menu di scelta rapida.</span><span class="sxs-lookup"><span data-stu-id="afb69-134">Right-click the file share you wish to view, and - from the context menu - select **Open**.</span></span> <span data-ttu-id="afb69-135">È anche possibile fare doppio clic sulla condivisione file che si vuole visualizzare.</span><span class="sxs-lookup"><span data-stu-id="afb69-135">You can also double-click the file share you wish to view.</span></span>

    ![Apri condivisione](media/vs-azure-tools-storage-explorer-files/image4.png)

5. <span data-ttu-id="afb69-137">Nel riquadro principale verrà visualizzato il contenuto della condivisione file.</span><span class="sxs-lookup"><span data-stu-id="afb69-137">The main pane will display the file share's contents.</span></span>
    
    ![Contenuto della condivisione file](media/vs-azure-tools-storage-explorer-files/image5.png)

## <a name="delete-a-file-share"></a><span data-ttu-id="afb69-139">Eliminare una condivisione file</span><span class="sxs-lookup"><span data-stu-id="afb69-139">Delete a file share</span></span>

<span data-ttu-id="afb69-140">È possibile creare ed eliminare facilmente le condivisioni file in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="afb69-140">File shares can be easily created and deleted as needed.</span></span> <span data-ttu-id="afb69-141">Per informazioni su come eliminare singoli file, vedere la sezione relativa alla [gestione dei file in una condivisione file](https://docs.microsoft.com//azure/vs-azure-tools-storage-explorer-blobs#managing-blobs-in-a-blob-container).</span><span class="sxs-lookup"><span data-stu-id="afb69-141">(To see how to delete individual files, refer to the section, [Managing files in a file share](https://docs.microsoft.com//azure/vs-azure-tools-storage-explorer-blobs#managing-blobs-in-a-blob-container).)</span></span>

<span data-ttu-id="afb69-142">La procedura seguente illustra come eliminare una condivisione file all'interno di Storage Explorer (anteprima).</span><span class="sxs-lookup"><span data-stu-id="afb69-142">The following steps illustrate how to delete a file share within Storage Explorer (Preview):</span></span>

1. <span data-ttu-id="afb69-143">Aprire Storage Explorer (anteprima).</span><span class="sxs-lookup"><span data-stu-id="afb69-143">Open Storage Explorer (Preview).</span></span>

2. <span data-ttu-id="afb69-144">Nel riquadro sinistro espandere l'account di archiviazione che contiene la condivisione file da visualizzare.</span><span class="sxs-lookup"><span data-stu-id="afb69-144">In the left pane, expand the storage account containing the file share you wish to view.</span></span>

3. <span data-ttu-id="afb69-145">Espandere le **Condivisioni file** dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="afb69-145">Expand the storage account's **File Shares**.</span></span>

4. <span data-ttu-id="afb69-146">Fare clic con il pulsante destro del mouse sulla condivisione file da eliminare e scegliere **Elimina** dal menu di scelta rapida.</span><span class="sxs-lookup"><span data-stu-id="afb69-146">Right-click the file share you wish to delete, and - from the context menu - select **Delete**.</span></span> <span data-ttu-id="afb69-147">È anche possibile premere **CANC** per eliminare la condivisione file attualmente selezionata.</span><span class="sxs-lookup"><span data-stu-id="afb69-147">You can also press **Delete** to delete the currently selected file share.</span></span>

    ![Eliminazione](media/vs-azure-tools-storage-explorer-files/image6.png)

5. <span data-ttu-id="afb69-149">Fare clic su **Sì** nella finestra di dialogo di conferma.</span><span class="sxs-lookup"><span data-stu-id="afb69-149">Select **Yes** to the confirmation dialog.</span></span>
    
    ![Finestra di dialogo di conferma](media/vs-azure-tools-storage-explorer-files/image7.png)

## <a name="copy-a-file-share"></a><span data-ttu-id="afb69-151">Copiare una condivisione file</span><span class="sxs-lookup"><span data-stu-id="afb69-151">Copy a file share</span></span>

<span data-ttu-id="afb69-152">Storage Explorer (anteprima) consente di copiare una condivisione file negli Appunti e quindi incollarla in un altro account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="afb69-152">Storage Explorer (Preview) enables you to copy a file share to the clipboard, and then paste that file share into another storage account.</span></span> <span data-ttu-id="afb69-153">Per informazioni su come copiare singoli file, vedere la sezione relativa alla [gestione dei file in una condivisione file](https://docs.microsoft.com//azure/vs-azure-tools-storage-explorer-blobs#managing-blobs-in-a-blob-container).</span><span class="sxs-lookup"><span data-stu-id="afb69-153">(To see how to copy individual files, refer to the section, [Managing files in a file share](https://docs.microsoft.com//azure/vs-azure-tools-storage-explorer-blobs#managing-blobs-in-a-blob-container).)</span></span>

<span data-ttu-id="afb69-154">La procedura seguenti illustra come copiare una condivisione file da un account di archiviazione a un altro.</span><span class="sxs-lookup"><span data-stu-id="afb69-154">The following steps illustrate how to copy a file share from one storage account to another.</span></span>

1. <span data-ttu-id="afb69-155">Aprire Storage Explorer (anteprima).</span><span class="sxs-lookup"><span data-stu-id="afb69-155">Open Storage Explorer (Preview).</span></span>

2. <span data-ttu-id="afb69-156">Nel riquadro sinistro espandere l'account di archiviazione che contiene la condivisione file da copiare.</span><span class="sxs-lookup"><span data-stu-id="afb69-156">In the left pane, expand the storage account containing the file share you wish to copy.</span></span>

3. <span data-ttu-id="afb69-157">Espandere le **Condivisioni file** dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="afb69-157">Expand the storage account's **File Shares**.</span></span>

4. <span data-ttu-id="afb69-158">Fare clic con il pulsante destro del mouse sulla condivisione file da copiare e scegliere **Copy File Share** (Copia condivisione file) dal menu di scelta rapida.</span><span class="sxs-lookup"><span data-stu-id="afb69-158">Right-click the file share you wish to copy, and - from the context menu - select **Copy File Share**.</span></span>

    ![Copia condivisione file](media/vs-azure-tools-storage-explorer-files/image8.png)

5. <span data-ttu-id="afb69-160">Fare clic con il pulsante destro del mouse sull'account di archiviazione di destinazione in cui si vuole incollare la condivisione file e scegliere **Paste File Share** (Incolla condivisione file) dal menu di scelta rapida.</span><span class="sxs-lookup"><span data-stu-id="afb69-160">Right-click the desired "target" storage account into which you want to paste the file share, and - from the context menu - select **Paste File Share**.</span></span>

    ![Incolla condivisione file](media/vs-azure-tools-storage-explorer-files/image9.png)

## <a name="get-the-sas-for-a-file-share"></a><span data-ttu-id="afb69-162">Ottenere la firma di accesso condiviso per una condivisione file</span><span class="sxs-lookup"><span data-stu-id="afb69-162">Get the SAS for a file share</span></span>

<span data-ttu-id="afb69-163">Una [firma di accesso condiviso (SAS)](https://docs.microsoft.com//azure/storage/storage-dotnet-shared-access-signature-part-1) fornisce accesso delegato alle risorse nell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="afb69-163">A [shared access signature (SAS)](https://docs.microsoft.com//azure/storage/storage-dotnet-shared-access-signature-part-1) provides delegated access to resources in your storage account.</span></span> <span data-ttu-id="afb69-164">Questo significa che è possibile concedere a un client autorizzazioni limitate per BLOB, code o tabelle per un periodo di tempo specificato e con un set di autorizzazioni specificato senza dover condividere le chiavi di accesso dell'account.</span><span class="sxs-lookup"><span data-stu-id="afb69-164">This means that you can grant a client limited permissions to objects in your storage account for a specified period of time and with a specified set of permissions, without having to share your account access keys.</span></span>

<span data-ttu-id="afb69-165">La procedura seguente illustra come creare una firma di accesso condiviso per una condivisione file.</span><span class="sxs-lookup"><span data-stu-id="afb69-165">The following steps illustrate how to create a SAS for a file share:+</span></span>

1. <span data-ttu-id="afb69-166">Aprire Storage Explorer (anteprima).</span><span class="sxs-lookup"><span data-stu-id="afb69-166">Open Storage Explorer (Preview).</span></span>

2. <span data-ttu-id="afb69-167">Nel riquadro sinistro espandere l'account di archiviazione che contiene la condivisione file per cui si vuole ottenere una firma di accesso condiviso.</span><span class="sxs-lookup"><span data-stu-id="afb69-167">In the left pane, expand the storage account containing the file share for which you wish to get a SAS.</span></span>

3. <span data-ttu-id="afb69-168">Espandere le **Condivisioni file** dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="afb69-168">Expand the storage account's **File Shares**.</span></span>

4. <span data-ttu-id="afb69-169">Fare clic con il pulsante destro del mouse sulla condivisione file e scegliere **Get Shared Access Signature** (Ottieni firma di accesso condiviso) dal menu di scelta rapida.</span><span class="sxs-lookup"><span data-stu-id="afb69-169">Right-click the desired file share, and - from the context menu - select **Get Shared Access Signature**.</span></span>

    ![Ottenere la firma di accesso condiviso](media/vs-azure-tools-storage-explorer-files/image10.png)

5. <span data-ttu-id="afb69-171">Nella finestra di dialogo **Firma di accesso condiviso** specificare i criteri, le date di inizio e di scadenza, il fuso orario e i livelli di accesso da impostare per la risorsa.</span><span class="sxs-lookup"><span data-stu-id="afb69-171">In the **Shared Access Signature** dialog, specify the policy, start and expiration dates, time zone, and access levels you want for the resource.</span></span>

    ![Finestra di dialogo Firma di accesso condiviso](media/vs-azure-tools-storage-explorer-files/image11.png)

6. <span data-ttu-id="afb69-173">Una volta specificate le opzioni per la firma di accesso condiviso, scegliere **Crea**.</span><span class="sxs-lookup"><span data-stu-id="afb69-173">When you're finished specifying the SAS options, select **Create**.</span></span>

7. <span data-ttu-id="afb69-174">Verrà visualizzata una seconda finestra di dialogo **Firma di accesso condiviso** con l'elenco della condivisione file insieme all'URL e alle stringhe di query che è possibile usare per accedere alla risorsa di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="afb69-174">A second **Shared Access Signature** dialog will then display that lists the file share along with the URL and QueryStrings you can use to access the storage resource.</span></span> <span data-ttu-id="afb69-175">Selezionare **Copia** accanto all'URL che si vuole copiare negli Appunti.</span><span class="sxs-lookup"><span data-stu-id="afb69-175">Select **Copy** next to the URL you wish to copy to the clipboard.</span></span>
    
    ![Seconda finestra di dialogo Firma di accesso condiviso](media/vs-azure-tools-storage-explorer-files/image12.png)

8. <span data-ttu-id="afb69-177">Al termine, scegliere **Chiudi**.</span><span class="sxs-lookup"><span data-stu-id="afb69-177">When done, select **Close**.</span></span>

## <a name="manage-access-policies-for-a-file-share"></a><span data-ttu-id="afb69-178">Gestire i criteri di accesso per una condivisione file</span><span class="sxs-lookup"><span data-stu-id="afb69-178">Manage Access Policies for a file share</span></span>

<span data-ttu-id="afb69-179">La procedura seguente illustra come gestire, ovvero aggiungere e rimuovere, criteri di accesso per una condivisione file.</span><span class="sxs-lookup"><span data-stu-id="afb69-179">The following steps illustrate how to manage (add and remove) access policies for a file share:+ .</span></span> <span data-ttu-id="afb69-180">I criteri di accesso vengono usati per la creazione di URL di firma di accesso condiviso che permettono di accedere alla risorsa di Archiviazione file in un periodo di tempo specificato.</span><span class="sxs-lookup"><span data-stu-id="afb69-180">The Access Policies is used for creating SAS URLs through which people can use to access the Storage File resource during a defined period of time.</span></span>

1. <span data-ttu-id="afb69-181">Aprire Storage Explorer (anteprima).</span><span class="sxs-lookup"><span data-stu-id="afb69-181">Open Storage Explorer (Preview).</span></span>

2. <span data-ttu-id="afb69-182">Nel riquadro sinistro espandere l'account di archiviazione che contiene la condivisione file di cui si vogliono gestire i criteri di accesso.</span><span class="sxs-lookup"><span data-stu-id="afb69-182">In the left pane, expand the storage account containing the file share whose access policies you wish to manage.</span></span>

3. <span data-ttu-id="afb69-183">Espandere le **Condivisioni file** dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="afb69-183">Expand the storage account's **File Shares**.</span></span>

4. <span data-ttu-id="afb69-184">Selezionare la condivisione file e scegliere **Manage Access Policies** (Gestisci criteri di accesso) dal menu di scelta rapida.</span><span class="sxs-lookup"><span data-stu-id="afb69-184">Select the desired file share, and - from the context menu - select **Manage Access Policies**.</span></span>

    ![Menu di scelta rapida Manage Access Policies (Gestisci criteri di accesso)](media/vs-azure-tools-storage-explorer-files/image13.png)

5. <span data-ttu-id="afb69-186">Nella finestra di dialogo **Criteri di accesso** saranno elencati tutti i criteri di accesso già creati per la condivisione file selezionata.</span><span class="sxs-lookup"><span data-stu-id="afb69-186">The **Access Policies** dialog will list any access policies already created for the selected file share.</span></span>
    
    ![Criteri di accesso](media/vs-azure-tools-storage-explorer-files/image14.png)

6. <span data-ttu-id="afb69-188">Seguire questi passaggi a seconda dell'attività di gestione dei criteri di accesso:</span><span class="sxs-lookup"><span data-stu-id="afb69-188">Follow these steps depending on the access policy management task:</span></span>
    
    - <span data-ttu-id="afb69-189">**Aggiungere nuovi criteri di accesso**: selezionare **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="afb69-189">**Add a new access policy** - Select **Add**.</span></span> <span data-ttu-id="afb69-190">Una volta generati, nella finestra di dialogo **Criteri di accesso** verranno visualizzati i criteri di accesso appena aggiunti, con le impostazioni predefinite.</span><span class="sxs-lookup"><span data-stu-id="afb69-190">Once generated, the **Access Policies** dialog will display the newly added access policy (with default settings).</span></span>

    - <span data-ttu-id="afb69-191">**Modificare i criteri di accesso**: apportare le modifiche desiderate e scegliere **Salva**.</span><span class="sxs-lookup"><span data-stu-id="afb69-191">**Edit an access policy** - Make any desired edits, and select **Save**.</span></span>

    - <span data-ttu-id="afb69-192">**Rimuovere criteri di accesso**: selezionare **Rimuovi** accanto ai criteri di accesso da rimuovere.</span><span class="sxs-lookup"><span data-stu-id="afb69-192">**Remove an access policy** - Select **Remove** next to the access policy you wish to remove.</span></span>

7. <span data-ttu-id="afb69-193">Creare un nuovo URL di firma di accesso condiviso usando i criteri di accesso creati in precedenza:</span><span class="sxs-lookup"><span data-stu-id="afb69-193">Create a new SAS URL using the Access Policy you created earlier:</span></span>
    
    ![Ottenere una firma di accesso condiviso](media/vs-azure-tools-storage-explorer-files/image15.png)
    
    ![Nome e proprietà della firma di accesso condiviso](media/vs-azure-tools-storage-explorer-files/image16.png)

## <a name="managing-files-in-a-file-share"></a><span data-ttu-id="afb69-196">Gestione dei file in una condivisione file</span><span class="sxs-lookup"><span data-stu-id="afb69-196">Managing files in a file share</span></span>

<span data-ttu-id="afb69-197">Dopo aver creato una condivisione file, è possibile caricare un file in tale condivisione file, scaricare un file nel computer locale, aprire un file nel computer locale e molto altro ancora.</span><span class="sxs-lookup"><span data-stu-id="afb69-197">Once you've created a file share, you can upload a file to that file share, download a file to your local computer, open a file on your local computer, and much more.</span></span>

<span data-ttu-id="afb69-198">La procedura seguente illustra come gestire i file e le cartelle all'interno di una condivisione file.</span><span class="sxs-lookup"><span data-stu-id="afb69-198">The following steps illustrate how to manage the files (and folders) within a file share.</span></span>

1.  <span data-ttu-id="afb69-199">Aprire Storage Explorer (anteprima).</span><span class="sxs-lookup"><span data-stu-id="afb69-199">Open Storage Explorer (Preview).</span></span>

2.  <span data-ttu-id="afb69-200">Nel riquadro sinistro espandere l'account di archiviazione che contiene la condivisione file da gestire.</span><span class="sxs-lookup"><span data-stu-id="afb69-200">In the left pane, expand the storage account containing the file share you wish to manage.</span></span>

3.  <span data-ttu-id="afb69-201">Espandere le **Condivisioni file** dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="afb69-201">Expand the storage account's **File Shares**.</span></span>

4.  <span data-ttu-id="afb69-202">Fare doppio clic sulla condivisione file che si vuole visualizzare.</span><span class="sxs-lookup"><span data-stu-id="afb69-202">Double-click the file share you wish to view.</span></span>

5.  <span data-ttu-id="afb69-203">Nel riquadro principale verrà visualizzato il contenuto della condivisione file.</span><span class="sxs-lookup"><span data-stu-id="afb69-203">The main pane will display the file share's contents.</span></span>

    ![Contenuto della condivisione file](media/vs-azure-tools-storage-explorer-files/image17.png)

6.  <span data-ttu-id="afb69-205">Nel riquadro principale verrà visualizzato il contenuto della condivisione file.</span><span class="sxs-lookup"><span data-stu-id="afb69-205">The main pane will display the file share's contents.</span></span>

7.  <span data-ttu-id="afb69-206">Seguire questi passaggi in base all'attività da eseguire:</span><span class="sxs-lookup"><span data-stu-id="afb69-206">Follow these steps depending on the task you wish to perform:</span></span>

    - <span data-ttu-id="afb69-207">**Caricare file in una condivisione file**</span><span class="sxs-lookup"><span data-stu-id="afb69-207">**Upload files to a file share**</span></span>

        <span data-ttu-id="afb69-208">a.</span><span class="sxs-lookup"><span data-stu-id="afb69-208">a.</span></span>  <span data-ttu-id="afb69-209">Sulla barra degli strumenti del riquadro principale selezionare **Carica** e quindi **Carica i file** dal menu a discesa.</span><span class="sxs-lookup"><span data-stu-id="afb69-209">On the main pane's toolbar, select **Upload**, and then **Upload Files** from the drop-down menu.</span></span>

        ![Caricare file](media/vs-azure-tools-storage-explorer-files/image18.png)
        
        <span data-ttu-id="afb69-211">b.</span><span class="sxs-lookup"><span data-stu-id="afb69-211">b.</span></span> <span data-ttu-id="afb69-212">Nella finestra di dialogo **Carica i file** scegliere il pulsante con i puntini di sospensione (**…**) a destra della casella **File** per selezionare i file da caricare.</span><span class="sxs-lookup"><span data-stu-id="afb69-212">In the **Upload files** dialog, select the ellipsis (**…**) button on the right side of the **Files** text box to select the file(s) you wish to upload.</span></span>

        ![Aggiunta di file](media/vs-azure-tools-storage-explorer-files/image19.png)

        <span data-ttu-id="afb69-214">c.</span><span class="sxs-lookup"><span data-stu-id="afb69-214">c.</span></span> <span data-ttu-id="afb69-215">Selezionare **Carica**.</span><span class="sxs-lookup"><span data-stu-id="afb69-215">Select **Upload**.</span></span>

    - <span data-ttu-id="afb69-216">**Caricare una cartella in una condivisione file**</span><span class="sxs-lookup"><span data-stu-id="afb69-216">**Upload a folder to a file share**</span></span>
        
        <span data-ttu-id="afb69-217">a.</span><span class="sxs-lookup"><span data-stu-id="afb69-217">a.</span></span> <span data-ttu-id="afb69-218">Sulla barra degli strumenti del riquadro principale selezionare **Carica** e quindi **Upload Folder** (Carica cartella) dal menu a discesa.</span><span class="sxs-lookup"><span data-stu-id="afb69-218">On the main pane's toolbar, select **Upload**, and then **Upload Folder** from the drop-down menu.</span></span>

        ![Menu di Upload Folder (Carica cartella)](media/vs-azure-tools-storage-explorer-files/image20.png)

        <span data-ttu-id="afb69-220">b.</span><span class="sxs-lookup"><span data-stu-id="afb69-220">b.</span></span> <span data-ttu-id="afb69-221">Nella finestra di dialogo **Upload Folder** (Carica cartella) scegliere il pulsante con i puntini di sospensione (**…**) a destra della casella di testo **Cartella** per selezionare la cartella di cui si vuole caricare il contenuto.</span><span class="sxs-lookup"><span data-stu-id="afb69-221">In the **Upload folder** dialog, select the ellipsis (**…**) button on the right side of the **Folder** text box to select the folder whose contents you wish to upload.</span></span>

        <span data-ttu-id="afb69-222">c.</span><span class="sxs-lookup"><span data-stu-id="afb69-222">c.</span></span> <span data-ttu-id="afb69-223">È possibile specificare una cartella di destinazione in cui verrà caricato il contenuto della cartella selezionata.</span><span class="sxs-lookup"><span data-stu-id="afb69-223">Optionally, specify a target folder into which the selected folder's contents will be uploaded.</span></span> <span data-ttu-id="afb69-224">Se la cartella di destinazione non esiste, verrà creata.</span><span class="sxs-lookup"><span data-stu-id="afb69-224">If the target folder doesn’t exist, it will be created.</span></span>

        <span data-ttu-id="afb69-225">d.</span><span class="sxs-lookup"><span data-stu-id="afb69-225">d.</span></span> <span data-ttu-id="afb69-226">Selezionare **Carica**.</span><span class="sxs-lookup"><span data-stu-id="afb69-226">Select **Upload**.</span></span>

    - <span data-ttu-id="afb69-227">**Scaricare un file nel computer locale**</span><span class="sxs-lookup"><span data-stu-id="afb69-227">**Download a file to your local computer**</span></span>
        
        <span data-ttu-id="afb69-228">a.</span><span class="sxs-lookup"><span data-stu-id="afb69-228">a.</span></span> <span data-ttu-id="afb69-229">Selezionare il file da scaricare.</span><span class="sxs-lookup"><span data-stu-id="afb69-229">Select the file you wish to download.</span></span>
        
        <span data-ttu-id="afb69-230">b.</span><span class="sxs-lookup"><span data-stu-id="afb69-230">b.</span></span> <span data-ttu-id="afb69-231">Sulla barra degli strumenti del riquadro principale selezionare **Scarica**.</span><span class="sxs-lookup"><span data-stu-id="afb69-231">On the main pane's toolbar, select **Download**.</span></span>
        
        <span data-ttu-id="afb69-232">c.</span><span class="sxs-lookup"><span data-stu-id="afb69-232">c.</span></span> <span data-ttu-id="afb69-233">Nella finestra di dialogo **Specify where to save the downloaded file** (Specificare dove salvare il file scaricato) specificare il percorso in cui salvare il file scaricato e il nome da assegnare.</span><span class="sxs-lookup"><span data-stu-id="afb69-233">In the **Specify where to save the downloaded file** dialog, specify the location where you want the file downloaded, and the name you wish to give it.</span></span>

        <span data-ttu-id="afb69-234">d.</span><span class="sxs-lookup"><span data-stu-id="afb69-234">d.</span></span> <span data-ttu-id="afb69-235">Selezionare **Salva**.</span><span class="sxs-lookup"><span data-stu-id="afb69-235">Select **Save**.</span></span>

    - <span data-ttu-id="afb69-236">**Aprire un file nel computer locale**</span><span class="sxs-lookup"><span data-stu-id="afb69-236">**Open a file on your local computer**</span></span>
        
        <span data-ttu-id="afb69-237">a.</span><span class="sxs-lookup"><span data-stu-id="afb69-237">a.</span></span>  <span data-ttu-id="afb69-238">Selezionare il file da aprire.</span><span class="sxs-lookup"><span data-stu-id="afb69-238">Select the file you wish to open.</span></span>
        
        <span data-ttu-id="afb69-239">b.</span><span class="sxs-lookup"><span data-stu-id="afb69-239">b.</span></span>  <span data-ttu-id="afb69-240">Sulla barra degli strumenti del riquadro principale selezionare **Apri**.</span><span class="sxs-lookup"><span data-stu-id="afb69-240">On the main pane's toolbar, select **Open**.</span></span>
        
        <span data-ttu-id="afb69-241">c.</span><span class="sxs-lookup"><span data-stu-id="afb69-241">c.</span></span>  <span data-ttu-id="afb69-242">Il file verrà scaricato e aperto usando l'applicazione associata al tipo di file sottostante del file.</span><span class="sxs-lookup"><span data-stu-id="afb69-242">The file will be downloaded and opened using the application associated with the file's underlying file type.</span></span>

    - <span data-ttu-id="afb69-243">**Copiare un file negli Appunti**</span><span class="sxs-lookup"><span data-stu-id="afb69-243">**Copy a file to the clipboard**</span></span>

        <span data-ttu-id="afb69-244">a.</span><span class="sxs-lookup"><span data-stu-id="afb69-244">a.</span></span> <span data-ttu-id="afb69-245">Selezionare il file da copiare.</span><span class="sxs-lookup"><span data-stu-id="afb69-245">Select the file you wish to copy.</span></span>

        <span data-ttu-id="afb69-246">b.</span><span class="sxs-lookup"><span data-stu-id="afb69-246">b.</span></span> <span data-ttu-id="afb69-247">Sulla barra degli strumenti del riquadro principale selezionare **Copia**.</span><span class="sxs-lookup"><span data-stu-id="afb69-247">On the main pane's toolbar, select **Copy**.</span></span>

        <span data-ttu-id="afb69-248">c.</span><span class="sxs-lookup"><span data-stu-id="afb69-248">c.</span></span> <span data-ttu-id="afb69-249">Nel riquadro sinistro passare a un'altra condivisione file e fare doppio clic su di essa per visualizzarla nel riquadro principale.</span><span class="sxs-lookup"><span data-stu-id="afb69-249">In the left pane, navigate to another file share, and double-click it to view it in the main pane.</span></span>

        <span data-ttu-id="afb69-250">d.</span><span class="sxs-lookup"><span data-stu-id="afb69-250">d.</span></span> <span data-ttu-id="afb69-251">Sulla barra degli strumenti del riquadro principale selezionare **Incolla** per creare una copia del file.</span><span class="sxs-lookup"><span data-stu-id="afb69-251">On the main pane's toolbar, select **Paste** to create a copy of the file.</span></span>

    - <span data-ttu-id="afb69-252">**Eliminare un file**</span><span class="sxs-lookup"><span data-stu-id="afb69-252">**Delete a file**</span></span>

        <span data-ttu-id="afb69-253">a.</span><span class="sxs-lookup"><span data-stu-id="afb69-253">a.</span></span> <span data-ttu-id="afb69-254">Selezionare il file da eliminare.</span><span class="sxs-lookup"><span data-stu-id="afb69-254">Select the file you wish to delete.</span></span>

        <span data-ttu-id="afb69-255">b.</span><span class="sxs-lookup"><span data-stu-id="afb69-255">b.</span></span> <span data-ttu-id="afb69-256">Sulla barra degli strumenti del riquadro principale selezionare **Elimina**.</span><span class="sxs-lookup"><span data-stu-id="afb69-256">On the main pane's toolbar, select **Delete**.</span></span>

        <span data-ttu-id="afb69-257">c.</span><span class="sxs-lookup"><span data-stu-id="afb69-257">c.</span></span> <span data-ttu-id="afb69-258">Fare clic su **Sì** nella finestra di dialogo di conferma.</span><span class="sxs-lookup"><span data-stu-id="afb69-258">Select **Yes** to the confirmation dialog.</span></span>

## <a name="next-steps"></a><span data-ttu-id="afb69-259">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="afb69-259">Next steps</span></span>

- <span data-ttu-id="afb69-260">Vedere le note sulla versione e i video in [Microsoft Azure Storage Explorer](http://www.storageexplorer.com/)(anteprima).</span><span class="sxs-lookup"><span data-stu-id="afb69-260">View the [latest Storage Explorer (Preview) release notes and videos](http://www.storageexplorer.com/).</span></span>

- <span data-ttu-id="afb69-261">Informazioni su come creare applicazioni con BLOB, tabelle, code e file di Azure nella [Documentazione su Archiviazione](https://azure.microsoft.com/documentation/services/storage/).</span><span class="sxs-lookup"><span data-stu-id="afb69-261">Learn how to [create applications using Azure blobs, tables, queues, and files](https://azure.microsoft.com/documentation/services/storage/).</span></span>
