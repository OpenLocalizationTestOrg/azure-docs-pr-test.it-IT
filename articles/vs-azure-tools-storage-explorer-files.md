---
title: aaaUsing Esplora archivi (Preview) con l'archiviazione di File di Azure | Documenti Microsoft
description: Informazioni su come illustrate le procedure toouse toowork di esplorazione dell'archiviazione (anteprima) con file le condivisioni file.
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
ms.openlocfilehash: 98eb3cde711ae3dbfdb6ffaec23ae24f822370e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="using-storage-explorer-preview-with-azure-file-storage"></a><span data-ttu-id="807e1-103">Uso di Storage Explorer (anteprima) con Archiviazione file di Azure</span><span class="sxs-lookup"><span data-stu-id="807e1-103">Using Storage Explorer (Preview) with Azure File storage</span></span>

<span data-ttu-id="807e1-104">File di archiviazione è un servizio che offre i file nelle condivisioni di hello cloud usando Azure hello protocollo Server Message Block (SMB) standard.</span><span class="sxs-lookup"><span data-stu-id="807e1-104">Azure File storage is a service that offers file shares in hello cloud using hello standard Server Message Block (SMB) Protocol.</span></span> <span data-ttu-id="807e1-105">Sono supportati sia SMB 2.1 che SMB 3.0.</span><span class="sxs-lookup"><span data-stu-id="807e1-105">Both SMB 2.1 and SMB 3.0 are supported.</span></span> <span data-ttu-id="807e1-106">Con l'archiviazione di File di Azure, è possibile eseguire la migrazione di applicazioni legacy che si basano su tooAzure condivisioni file rapidamente e senza costose.</span><span class="sxs-lookup"><span data-stu-id="807e1-106">With Azure File storage, you can migrate legacy applications that rely on file shares tooAzure quickly and without costly rewrites.</span></span> <span data-ttu-id="807e1-107">È possibile utilizzare File archiviazione tooexpose dati pubblicamente toohello world o dati dell'applicazione toostore privatamente.</span><span class="sxs-lookup"><span data-stu-id="807e1-107">You can use File storage tooexpose data publicly toohello world, or toostore application data privately.</span></span> <span data-ttu-id="807e1-108">In questo articolo si apprenderà come toouse toowork di esplorazione dell'archiviazione (anteprima) con file di condivisioni e i file.</span><span class="sxs-lookup"><span data-stu-id="807e1-108">In this article, you'll learn how toouse Storage Explorer (Preview) toowork with file shares and files.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="807e1-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="807e1-109">Prerequisites</span></span>

<span data-ttu-id="807e1-110">passaggi di hello toocomplete in questo articolo, è necessario seguente hello:</span><span class="sxs-lookup"><span data-stu-id="807e1-110">toocomplete hello steps in this article, you'll need hello following:</span></span>

- [<span data-ttu-id="807e1-111">Scaricare e installare Storage Explorer (anteprima)</span><span class="sxs-lookup"><span data-stu-id="807e1-111">Download and install Storage Explorer (preview)</span></span>](http://www.storageexplorer.com/)

- [<span data-ttu-id="807e1-112">Connettersi al servizio o account di archiviazione di Azure tooa</span><span class="sxs-lookup"><span data-stu-id="807e1-112">Connect tooa Azure storage account or service</span></span>](https://docs.microsoft.com//azure/vs-azure-tools-storage-manage-with-storage-explorer#connect-to-a-storage-account-or-service)

## <a name="create-a-file-share"></a><span data-ttu-id="807e1-113">Creare una condivisione file</span><span class="sxs-lookup"><span data-stu-id="807e1-113">Create a File Share</span></span>

<span data-ttu-id="807e1-114">Tutti i file devono risiedere in una condivisione file, ovvero un semplice raggruppamento logico di file.</span><span class="sxs-lookup"><span data-stu-id="807e1-114">All files must reside in a file share, which is simply a logical grouping of files.</span></span> <span data-ttu-id="807e1-115">Un account può contenere un numero illimitato di condivisioni file e ogni condivisione può archiviare un numero illimitato di file.</span><span class="sxs-lookup"><span data-stu-id="807e1-115">An account can contain an unlimited number of file shares, and each share can store an unlimited number of files.</span></span>

<span data-ttu-id="807e1-116">Hello alla procedura seguente viene illustrato come toocreate una condivisione di file all'interno di soluzioni di archiviazione (anteprima).</span><span class="sxs-lookup"><span data-stu-id="807e1-116">hello following steps illustrate how toocreate a file share within Storage Explorer (Preview).</span></span>

1. <span data-ttu-id="807e1-117">Aprire Storage Explorer (anteprima).</span><span class="sxs-lookup"><span data-stu-id="807e1-117">Open Storage Explorer (Preview).</span></span>

2. <span data-ttu-id="807e1-118">Nel riquadro di sinistra hello, espandere account di archiviazione hello entro il quale si desidera toocreate hello condivisione File</span><span class="sxs-lookup"><span data-stu-id="807e1-118">In hello left pane, expand hello storage account within which you wish toocreate hello File Share</span></span>

3. <span data-ttu-id="807e1-119">Fare doppio clic su **condivisioni File**e - scegliere dal menu di scelta rapida hello - **Crea condivisione File**.</span><span class="sxs-lookup"><span data-stu-id="807e1-119">Right-click **File Shares**, and - from hello context menu - select **Create File Share**.</span></span>

    ![Crea condivisione file](media/vs-azure-tools-storage-explorer-files/image1.png)

4. <span data-ttu-id="807e1-121">Verrà visualizzata una casella di testo di sotto di hello **condivisioni File** cartella.</span><span class="sxs-lookup"><span data-stu-id="807e1-121">A text box will appear below hello **File Shares** folder.</span></span> <span data-ttu-id="807e1-122">Immettere il nome di hello per la condivisione di file.</span><span class="sxs-lookup"><span data-stu-id="807e1-122">Enter hello name for your file share.</span></span> <span data-ttu-id="807e1-123">Vedere hello [condividere le regole di denominazione](https://docs.microsoft.com//azure/storage/storage-dotnet-how-to-use-blobs#create-a-container) sezione per un elenco di regole e restrizioni relative alla denominazione condivisioni file.</span><span class="sxs-lookup"><span data-stu-id="807e1-123">See hello [Share naming rules](https://docs.microsoft.com//azure/storage/storage-dotnet-how-to-use-blobs#create-a-container) section for a list of rules and restrictions on naming file shares.</span></span>

    ![Denominazione condivisione hello](media/vs-azure-tools-storage-explorer-files/image2.png)

5. <span data-ttu-id="807e1-125">Premere **invio** quando toocreate done hello condivisione file, o **Esc** toocancel.</span><span class="sxs-lookup"><span data-stu-id="807e1-125">Press **Enter** when done toocreate hello file share, or **Esc** toocancel.</span></span> <span data-ttu-id="807e1-126">Una volta condivisione file hello è stata creata correttamente, verrà visualizzato in hello **condivisioni File** cartella per hello selezionato di account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="807e1-126">Once hello file share has been successfully created, it will be displayed under hello **File Shares** folder for hello selected storage account.</span></span>

    ![nuova condivisione di Hello](media/vs-azure-tools-storage-explorer-files/image3.png)

## <a name="view-a-file-shares-contents"></a><span data-ttu-id="807e1-128">Visualizzare il contenuto di una condivisione file</span><span class="sxs-lookup"><span data-stu-id="807e1-128">View a file share's contents</span></span>

<span data-ttu-id="807e1-129">Le condivisioni file contengono file e cartelle, che a loro volta possono contenere file.</span><span class="sxs-lookup"><span data-stu-id="807e1-129">File shares contain files and folders (that can also contain files).</span></span>

<span data-ttu-id="807e1-130">Hello passaggi seguenti viene illustrato come contenuto di hello tooview di un file condivide all'interno di soluzioni di archiviazione (anteprima): +</span><span class="sxs-lookup"><span data-stu-id="807e1-130">hello following steps illustrate how tooview hello contents of a file share within Storage Explorer (Preview):+</span></span>

1. <span data-ttu-id="807e1-131">Aprire Storage Explorer (anteprima).</span><span class="sxs-lookup"><span data-stu-id="807e1-131">Open Storage Explorer (Preview).</span></span>

2. <span data-ttu-id="807e1-132">Nel riquadro di sinistra hello, espandere account di archiviazione di hello contenente desiderato tooview condivisione di file hello.</span><span class="sxs-lookup"><span data-stu-id="807e1-132">In hello left pane, expand hello storage account containing hello file share you wish tooview.</span></span>

3. <span data-ttu-id="807e1-133">Espandere l'account di archiviazione hello **condivisioni File**.</span><span class="sxs-lookup"><span data-stu-id="807e1-133">Expand hello storage account's **File Shares**.</span></span>

4. <span data-ttu-id="807e1-134">Condivisione di file hello pulsante destro del mouse si desidera tooview, quindi - scegliere dal menu di scelta rapida hello - **aprire**.</span><span class="sxs-lookup"><span data-stu-id="807e1-134">Right-click hello file share you wish tooview, and - from hello context menu - select **Open**.</span></span> <span data-ttu-id="807e1-135">È anche possibile fare doppio clic su condivisione file hello desiderato tooview.</span><span class="sxs-lookup"><span data-stu-id="807e1-135">You can also double-click hello file share you wish tooview.</span></span>

    ![Apri condivisione](media/vs-azure-tools-storage-explorer-files/image4.png)

5. <span data-ttu-id="807e1-137">riquadro principale Hello verrà visualizzato il contenuto della condivisione di file hello.</span><span class="sxs-lookup"><span data-stu-id="807e1-137">hello main pane will display hello file share's contents.</span></span>
    
    ![contenuto della condivisione di Hello](media/vs-azure-tools-storage-explorer-files/image5.png)

## <a name="delete-a-file-share"></a><span data-ttu-id="807e1-139">Eliminare una condivisione file</span><span class="sxs-lookup"><span data-stu-id="807e1-139">Delete a file share</span></span>

<span data-ttu-id="807e1-140">È possibile creare ed eliminare facilmente le condivisioni file in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="807e1-140">File shares can be easily created and deleted as needed.</span></span> <span data-ttu-id="807e1-141">(toosee come toodelete singoli file, fare riferimento a sezione toohello [la gestione dei file in una condivisione file](https://docs.microsoft.com//azure/vs-azure-tools-storage-explorer-blobs#managing-blobs-in-a-blob-container).)</span><span class="sxs-lookup"><span data-stu-id="807e1-141">(toosee how toodelete individual files, refer toohello section, [Managing files in a file share](https://docs.microsoft.com//azure/vs-azure-tools-storage-explorer-blobs#managing-blobs-in-a-blob-container).)</span></span>

<span data-ttu-id="807e1-142">Hello alla procedura seguente viene illustrato come toodelete una condivisione di file all'interno di soluzioni di archiviazione (anteprima):</span><span class="sxs-lookup"><span data-stu-id="807e1-142">hello following steps illustrate how toodelete a file share within Storage Explorer (Preview):</span></span>

1. <span data-ttu-id="807e1-143">Aprire Storage Explorer (anteprima).</span><span class="sxs-lookup"><span data-stu-id="807e1-143">Open Storage Explorer (Preview).</span></span>

2. <span data-ttu-id="807e1-144">Nel riquadro di sinistra hello, espandere account di archiviazione di hello contenente desiderato tooview condivisione di file hello.</span><span class="sxs-lookup"><span data-stu-id="807e1-144">In hello left pane, expand hello storage account containing hello file share you wish tooview.</span></span>

3. <span data-ttu-id="807e1-145">Espandere l'account di archiviazione hello **condivisioni File**.</span><span class="sxs-lookup"><span data-stu-id="807e1-145">Expand hello storage account's **File Shares**.</span></span>

4. <span data-ttu-id="807e1-146">Condivisione di file hello pulsante destro del mouse si desidera toodelete, quindi - scegliere dal menu di scelta rapida hello - **eliminare**.</span><span class="sxs-lookup"><span data-stu-id="807e1-146">Right-click hello file share you wish toodelete, and - from hello context menu - select **Delete**.</span></span> <span data-ttu-id="807e1-147">È anche possibile premere **eliminare** toodelete hello attualmente selezionato in una condivisione.</span><span class="sxs-lookup"><span data-stu-id="807e1-147">You can also press **Delete** toodelete hello currently selected file share.</span></span>

    ![Elimina](media/vs-azure-tools-storage-explorer-files/image6.png)

5. <span data-ttu-id="807e1-149">Selezionare **Sì** toohello nella finestra di conferma.</span><span class="sxs-lookup"><span data-stu-id="807e1-149">Select **Yes** toohello confirmation dialog.</span></span>
    
    ![Finestra di dialogo di conferma](media/vs-azure-tools-storage-explorer-files/image7.png)

## <a name="copy-a-file-share"></a><span data-ttu-id="807e1-151">Copiare una condivisione file</span><span class="sxs-lookup"><span data-stu-id="807e1-151">Copy a file share</span></span>

<span data-ttu-id="807e1-152">Esplorazione dell'archiviazione (anteprima) permette toocopy Appunti toohello condivisione file e quindi incollare tale condivisione di file in un altro account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="807e1-152">Storage Explorer (Preview) enables you toocopy a file share toohello clipboard, and then paste that file share into another storage account.</span></span> <span data-ttu-id="807e1-153">(toosee come toocopy singoli file, fare riferimento a sezione toohello [la gestione dei file in una condivisione file](https://docs.microsoft.com//azure/vs-azure-tools-storage-explorer-blobs#managing-blobs-in-a-blob-container).)</span><span class="sxs-lookup"><span data-stu-id="807e1-153">(toosee how toocopy individual files, refer toohello section, [Managing files in a file share](https://docs.microsoft.com//azure/vs-azure-tools-storage-explorer-blobs#managing-blobs-in-a-blob-container).)</span></span>

<span data-ttu-id="807e1-154">Hello alla procedura seguente viene illustrato come un file toocopy condividere da uno tooanother di account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="807e1-154">hello following steps illustrate how toocopy a file share from one storage account tooanother.</span></span>

1. <span data-ttu-id="807e1-155">Aprire Storage Explorer (anteprima).</span><span class="sxs-lookup"><span data-stu-id="807e1-155">Open Storage Explorer (Preview).</span></span>

2. <span data-ttu-id="807e1-156">Nel riquadro di sinistra hello, espandere account di archiviazione di hello contenente desiderato toocopy condivisione di file hello.</span><span class="sxs-lookup"><span data-stu-id="807e1-156">In hello left pane, expand hello storage account containing hello file share you wish toocopy.</span></span>

3. <span data-ttu-id="807e1-157">Espandere l'account di archiviazione hello **condivisioni File**.</span><span class="sxs-lookup"><span data-stu-id="807e1-157">Expand hello storage account's **File Shares**.</span></span>

4. <span data-ttu-id="807e1-158">Condivisione di file hello pulsante destro del mouse si desidera toocopy, quindi - scegliere dal menu di scelta rapida hello - **condivisione File di copia**.</span><span class="sxs-lookup"><span data-stu-id="807e1-158">Right-click hello file share you wish toocopy, and - from hello context menu - select **Copy File Share**.</span></span>

    ![Copia condivisione file](media/vs-azure-tools-storage-explorer-files/image8.png)

5. <span data-ttu-id="807e1-160">Fare doppio clic su account di archiviazione di destinazione"hello desiderato" in cui desidera toopaste condivisione di file hello e - dal menu di scelta rapida hello - selezionare **Incolla condivisione File**.</span><span class="sxs-lookup"><span data-stu-id="807e1-160">Right-click hello desired "target" storage account into which you want toopaste hello file share, and - from hello context menu - select **Paste File Share**.</span></span>

    ![Incolla condivisione file](media/vs-azure-tools-storage-explorer-files/image9.png)

## <a name="get-hello-sas-for-a-file-share"></a><span data-ttu-id="807e1-162">Ottenere hello firma di accesso condiviso per una condivisione file</span><span class="sxs-lookup"><span data-stu-id="807e1-162">Get hello SAS for a file share</span></span>

<span data-ttu-id="807e1-163">Oggetto [firma di accesso condiviso (SAS)](https://docs.microsoft.com//azure/storage/storage-dotnet-shared-access-signature-part-1) fornisce l'accesso delegato tooresources nell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="807e1-163">A [shared access signature (SAS)](https://docs.microsoft.com//azure/storage/storage-dotnet-shared-access-signature-part-1) provides delegated access tooresources in your storage account.</span></span> <span data-ttu-id="807e1-164">Ciò significa che è possibile concedere a che un client limitate tooobjects autorizzazioni nell'account di archiviazione per un determinato periodo di tempo e con un set specificato di autorizzazioni, senza dovere tooshare le chiavi di accesso di account.</span><span class="sxs-lookup"><span data-stu-id="807e1-164">This means that you can grant a client limited permissions tooobjects in your storage account for a specified period of time and with a specified set of permissions, without having tooshare your account access keys.</span></span>

<span data-ttu-id="807e1-165">Hello passaggi seguenti viene illustrato come toocreate una firma di accesso condiviso per un file di condividere: +</span><span class="sxs-lookup"><span data-stu-id="807e1-165">hello following steps illustrate how toocreate a SAS for a file share:+</span></span>

1. <span data-ttu-id="807e1-166">Aprire Storage Explorer (anteprima).</span><span class="sxs-lookup"><span data-stu-id="807e1-166">Open Storage Explorer (Preview).</span></span>

2. <span data-ttu-id="807e1-167">Nel riquadro di sinistra hello, espandere account di archiviazione hello contenente hello condivisione di file per i quali si desidera tooget una firma di accesso condiviso.</span><span class="sxs-lookup"><span data-stu-id="807e1-167">In hello left pane, expand hello storage account containing hello file share for which you wish tooget a SAS.</span></span>

3. <span data-ttu-id="807e1-168">Espandere l'account di archiviazione hello **condivisioni File**.</span><span class="sxs-lookup"><span data-stu-id="807e1-168">Expand hello storage account's **File Shares**.</span></span>

4. <span data-ttu-id="807e1-169">Condivisione di file desiderato hello e - scegliere dal menu di scelta rapida hello - **ottenere firma di accesso condiviso**.</span><span class="sxs-lookup"><span data-stu-id="807e1-169">Right-click hello desired file share, and - from hello context menu - select **Get Shared Access Signature**.</span></span>

    ![Ottenere la firma di accesso condiviso](media/vs-azure-tools-storage-explorer-files/image10.png)

5. <span data-ttu-id="807e1-171">In hello **firma di accesso condiviso** finestra di dialogo, specificare i criteri di hello, le date di inizio e di scadenza, fuso orario e desiderato per risorse hello livelli di accesso.</span><span class="sxs-lookup"><span data-stu-id="807e1-171">In hello **Shared Access Signature** dialog, specify hello policy, start and expiration dates, time zone, and access levels you want for hello resource.</span></span>

    ![Finestra di dialogo Firma di accesso condiviso](media/vs-azure-tools-storage-explorer-files/image11.png)

6. <span data-ttu-id="807e1-173">Al termine della specifica di opzioni di firma di accesso condiviso hello, selezionare **crea**.</span><span class="sxs-lookup"><span data-stu-id="807e1-173">When you're finished specifying hello SAS options, select **Create**.</span></span>

7. <span data-ttu-id="807e1-174">Un secondo **firma di accesso condiviso** finestra di dialogo verrà quindi visualizzato che elenchi hello condivisione file e URL hello e che è possibile utilizzare tooaccess QueryStrings hello risorsa di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="807e1-174">A second **Shared Access Signature** dialog will then display that lists hello file share along with hello URL and QueryStrings you can use tooaccess hello storage resource.</span></span> <span data-ttu-id="807e1-175">Selezionare **copia** Avanti URL toohello desiderato toocopy toohello Appunti.</span><span class="sxs-lookup"><span data-stu-id="807e1-175">Select **Copy** next toohello URL you wish toocopy toohello clipboard.</span></span>
    
    ![Seconda finestra di dialogo Firma di accesso condiviso](media/vs-azure-tools-storage-explorer-files/image12.png)

8. <span data-ttu-id="807e1-177">Al termine, scegliere **Chiudi**.</span><span class="sxs-lookup"><span data-stu-id="807e1-177">When done, select **Close**.</span></span>

## <a name="manage-access-policies-for-a-file-share"></a><span data-ttu-id="807e1-178">Gestire i criteri di accesso per una condivisione file</span><span class="sxs-lookup"><span data-stu-id="807e1-178">Manage Access Policies for a file share</span></span>

<span data-ttu-id="807e1-179">Hello passaggi seguenti viene illustrato come toomanage (aggiungere e rimuovere) criteri di accesso per una condivisione file: +.</span><span class="sxs-lookup"><span data-stu-id="807e1-179">hello following steps illustrate how toomanage (add and remove) access policies for a file share:+ .</span></span> <span data-ttu-id="807e1-180">i criteri di accesso Hello viene utilizzato per la creazione di URL di firma di accesso condiviso tramite la quale gli utenti possono utilizzare tooaccess hello risorsa di archiviazione File durante un periodo di tempo definito.</span><span class="sxs-lookup"><span data-stu-id="807e1-180">hello Access Policies is used for creating SAS URLs through which people can use tooaccess hello Storage File resource during a defined period of time.</span></span>

1. <span data-ttu-id="807e1-181">Aprire Storage Explorer (anteprima).</span><span class="sxs-lookup"><span data-stu-id="807e1-181">Open Storage Explorer (Preview).</span></span>

2. <span data-ttu-id="807e1-182">Nel riquadro di sinistra hello, espandere account di archiviazione hello contenente hello condivisione di file i cui criteri di accesso desiderato toomanage.</span><span class="sxs-lookup"><span data-stu-id="807e1-182">In hello left pane, expand hello storage account containing hello file share whose access policies you wish toomanage.</span></span>

3. <span data-ttu-id="807e1-183">Espandere l'account di archiviazione hello **condivisioni File**.</span><span class="sxs-lookup"><span data-stu-id="807e1-183">Expand hello storage account's **File Shares**.</span></span>

4. <span data-ttu-id="807e1-184">Selezionare condivisione di file desiderato hello e - dal menu di scelta rapida hello - **gestire criteri di accesso**.</span><span class="sxs-lookup"><span data-stu-id="807e1-184">Select hello desired file share, and - from hello context menu - select **Manage Access Policies**.</span></span>

    ![Menu di scelta rapida Manage Access Policies (Gestisci criteri di accesso)](media/vs-azure-tools-storage-explorer-files/image13.png)

5. <span data-ttu-id="807e1-186">Hello **criteri di accesso** finestra di dialogo verrà elencati i criteri di accesso già creati per la condivisione di file selezionato hello.</span><span class="sxs-lookup"><span data-stu-id="807e1-186">hello **Access Policies** dialog will list any access policies already created for hello selected file share.</span></span>
    
    ![Criteri di accesso](media/vs-azure-tools-storage-explorer-files/image14.png)

6. <span data-ttu-id="807e1-188">Seguire questi passaggi a seconda delle attività di gestione criteri di accesso hello:</span><span class="sxs-lookup"><span data-stu-id="807e1-188">Follow these steps depending on hello access policy management task:</span></span>
    
    - <span data-ttu-id="807e1-189">**Aggiungere nuovi criteri di accesso**: selezionare **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="807e1-189">**Add a new access policy** - Select **Add**.</span></span> <span data-ttu-id="807e1-190">Una volta generate, hello **criteri di accesso** finestra di dialogo verrà visualizzato hello appena aggiunto accedere criteri (con le impostazioni predefinite).</span><span class="sxs-lookup"><span data-stu-id="807e1-190">Once generated, hello **Access Policies** dialog will display hello newly added access policy (with default settings).</span></span>

    - <span data-ttu-id="807e1-191">**Modificare i criteri di accesso**: apportare le modifiche desiderate e scegliere **Salva**.</span><span class="sxs-lookup"><span data-stu-id="807e1-191">**Edit an access policy** - Make any desired edits, and select **Save**.</span></span>

    - <span data-ttu-id="807e1-192">**Rimuovere un criterio di accesso** : selezionare questa opzione **rimuovere** desiderato tooremove un criterio di accesso toohello successivo.</span><span class="sxs-lookup"><span data-stu-id="807e1-192">**Remove an access policy** - Select **Remove** next toohello access policy you wish tooremove.</span></span>

7. <span data-ttu-id="807e1-193">Creare un nuovo URL di firma di accesso condiviso con criteri di accesso creato in precedenza hello:</span><span class="sxs-lookup"><span data-stu-id="807e1-193">Create a new SAS URL using hello Access Policy you created earlier:</span></span>
    
    ![Ottenere una firma di accesso condiviso](media/vs-azure-tools-storage-explorer-files/image15.png)
    
    ![Nome e proprietà della firma di accesso condiviso](media/vs-azure-tools-storage-explorer-files/image16.png)

## <a name="managing-files-in-a-file-share"></a><span data-ttu-id="807e1-196">Gestione dei file in una condivisione file</span><span class="sxs-lookup"><span data-stu-id="807e1-196">Managing files in a file share</span></span>

<span data-ttu-id="807e1-197">Dopo aver creato una condivisione file, è possibile caricare una condivisione di file toothat file, scaricare un computer locale tooyour di file, aprire un file nel computer locale e molto altro ancora.</span><span class="sxs-lookup"><span data-stu-id="807e1-197">Once you've created a file share, you can upload a file toothat file share, download a file tooyour local computer, open a file on your local computer, and much more.</span></span>

<span data-ttu-id="807e1-198">Hello passaggi seguenti viene illustrato come condividono toomanage hello file (e cartelle) all'interno di un file.</span><span class="sxs-lookup"><span data-stu-id="807e1-198">hello following steps illustrate how toomanage hello files (and folders) within a file share.</span></span>

1.  <span data-ttu-id="807e1-199">Aprire Storage Explorer (anteprima).</span><span class="sxs-lookup"><span data-stu-id="807e1-199">Open Storage Explorer (Preview).</span></span>

2.  <span data-ttu-id="807e1-200">Nel riquadro di sinistra hello, espandere account di archiviazione di hello contenente desiderato toomanage condivisione di file hello.</span><span class="sxs-lookup"><span data-stu-id="807e1-200">In hello left pane, expand hello storage account containing hello file share you wish toomanage.</span></span>

3.  <span data-ttu-id="807e1-201">Espandere l'account di archiviazione hello **condivisioni File**.</span><span class="sxs-lookup"><span data-stu-id="807e1-201">Expand hello storage account's **File Shares**.</span></span>

4.  <span data-ttu-id="807e1-202">Fare doppio clic su condivisione file hello desiderato tooview.</span><span class="sxs-lookup"><span data-stu-id="807e1-202">Double-click hello file share you wish tooview.</span></span>

5.  <span data-ttu-id="807e1-203">riquadro principale Hello verrà visualizzato il contenuto della condivisione di file hello.</span><span class="sxs-lookup"><span data-stu-id="807e1-203">hello main pane will display hello file share's contents.</span></span>

    ![contenuto della condivisione di Hello](media/vs-azure-tools-storage-explorer-files/image17.png)

6.  <span data-ttu-id="807e1-205">riquadro principale Hello verrà visualizzato il contenuto della condivisione di file hello.</span><span class="sxs-lookup"><span data-stu-id="807e1-205">hello main pane will display hello file share's contents.</span></span>

7.  <span data-ttu-id="807e1-206">Seguire questi che passaggi a seconda attività hello desiderato tooperform:</span><span class="sxs-lookup"><span data-stu-id="807e1-206">Follow these steps depending on hello task you wish tooperform:</span></span>

    - <span data-ttu-id="807e1-207">**Caricare una condivisione di file tooa**</span><span class="sxs-lookup"><span data-stu-id="807e1-207">**Upload files tooa file share**</span></span>

        <span data-ttu-id="807e1-208">a.</span><span class="sxs-lookup"><span data-stu-id="807e1-208">a.</span></span>  <span data-ttu-id="807e1-209">Sulla barra degli strumenti del riquadro principale hello, selezionare **caricare**e quindi **Carica file** dal menu a discesa hello.</span><span class="sxs-lookup"><span data-stu-id="807e1-209">On hello main pane's toolbar, select **Upload**, and then **Upload Files** from hello drop-down menu.</span></span>

        ![Caricare file](media/vs-azure-tools-storage-explorer-files/image18.png)
        
        <span data-ttu-id="807e1-211">b.</span><span class="sxs-lookup"><span data-stu-id="807e1-211">b.</span></span> <span data-ttu-id="807e1-212">In hello **caricare file** finestra di dialogo, i puntini di sospensione selezionare hello (**...** ) pulsante a destra hello hello **file** file hello tooselect desiderato tooupload casella di testo.</span><span class="sxs-lookup"><span data-stu-id="807e1-212">In hello **Upload files** dialog, select hello ellipsis (**…**) button on hello right side of hello **Files** text box tooselect hello file(s) you wish tooupload.</span></span>

        ![Aggiunta di file](media/vs-azure-tools-storage-explorer-files/image19.png)

        <span data-ttu-id="807e1-214">c.</span><span class="sxs-lookup"><span data-stu-id="807e1-214">c.</span></span> <span data-ttu-id="807e1-215">Selezionare **Carica**.</span><span class="sxs-lookup"><span data-stu-id="807e1-215">Select **Upload**.</span></span>

    - <span data-ttu-id="807e1-216">**Caricare una condivisione di file di cartella tooa**</span><span class="sxs-lookup"><span data-stu-id="807e1-216">**Upload a folder tooa file share**</span></span>
        
        <span data-ttu-id="807e1-217">a.</span><span class="sxs-lookup"><span data-stu-id="807e1-217">a.</span></span> <span data-ttu-id="807e1-218">Sulla barra degli strumenti del riquadro principale hello, selezionare **caricare**e quindi **cartella caricare** dal menu a discesa hello.</span><span class="sxs-lookup"><span data-stu-id="807e1-218">On hello main pane's toolbar, select **Upload**, and then **Upload Folder** from hello drop-down menu.</span></span>

        ![Menu di Upload Folder (Carica cartella)](media/vs-azure-tools-storage-explorer-files/image20.png)

        <span data-ttu-id="807e1-220">b.</span><span class="sxs-lookup"><span data-stu-id="807e1-220">b.</span></span> <span data-ttu-id="807e1-221">In hello **cartella caricamento** finestra di dialogo, i puntini di sospensione selezionare hello (**...** ) pulsante a destra hello hello **cartella** cartella hello di tooselect casella testo cui si desidera tooupload il contenuto.</span><span class="sxs-lookup"><span data-stu-id="807e1-221">In hello **Upload folder** dialog, select hello ellipsis (**…**) button on hello right side of hello **Folder** text box tooselect hello folder whose contents you wish tooupload.</span></span>

        <span data-ttu-id="807e1-222">c.</span><span class="sxs-lookup"><span data-stu-id="807e1-222">c.</span></span> <span data-ttu-id="807e1-223">Facoltativamente, specificare una cartella di destinazione in cui hello verrà caricato il contenuto della cartella selezionata.</span><span class="sxs-lookup"><span data-stu-id="807e1-223">Optionally, specify a target folder into which hello selected folder's contents will be uploaded.</span></span> <span data-ttu-id="807e1-224">Se la cartella di destinazione hello non esiste, verrà creato.</span><span class="sxs-lookup"><span data-stu-id="807e1-224">If hello target folder doesn’t exist, it will be created.</span></span>

        <span data-ttu-id="807e1-225">d.</span><span class="sxs-lookup"><span data-stu-id="807e1-225">d.</span></span> <span data-ttu-id="807e1-226">Selezionare **Carica**.</span><span class="sxs-lookup"><span data-stu-id="807e1-226">Select **Upload**.</span></span>

    - <span data-ttu-id="807e1-227">**Scaricare un computer locale tooyour di file**</span><span class="sxs-lookup"><span data-stu-id="807e1-227">**Download a file tooyour local computer**</span></span>
        
        <span data-ttu-id="807e1-228">a.</span><span class="sxs-lookup"><span data-stu-id="807e1-228">a.</span></span> <span data-ttu-id="807e1-229">Selezionare il file hello desiderato toodownload.</span><span class="sxs-lookup"><span data-stu-id="807e1-229">Select hello file you wish toodownload.</span></span>
        
        <span data-ttu-id="807e1-230">b.</span><span class="sxs-lookup"><span data-stu-id="807e1-230">b.</span></span> <span data-ttu-id="807e1-231">Sulla barra degli strumenti del riquadro principale hello, selezionare **scaricare**.</span><span class="sxs-lookup"><span data-stu-id="807e1-231">On hello main pane's toolbar, select **Download**.</span></span>
        
        <span data-ttu-id="807e1-232">c.</span><span class="sxs-lookup"><span data-stu-id="807e1-232">c.</span></span> <span data-ttu-id="807e1-233">In hello **specificare dove toosave hello scaricati file** finestra di dialogo, specificare il percorso di hello in cui si desidera file hello scaricato e hello nome desiderato toogive è.</span><span class="sxs-lookup"><span data-stu-id="807e1-233">In hello **Specify where toosave hello downloaded file** dialog, specify hello location where you want hello file downloaded, and hello name you wish toogive it.</span></span>

        <span data-ttu-id="807e1-234">d.</span><span class="sxs-lookup"><span data-stu-id="807e1-234">d.</span></span> <span data-ttu-id="807e1-235">Selezionare **Salva**.</span><span class="sxs-lookup"><span data-stu-id="807e1-235">Select **Save**.</span></span>

    - <span data-ttu-id="807e1-236">**Aprire un file nel computer locale**</span><span class="sxs-lookup"><span data-stu-id="807e1-236">**Open a file on your local computer**</span></span>
        
        <span data-ttu-id="807e1-237">a.</span><span class="sxs-lookup"><span data-stu-id="807e1-237">a.</span></span>  <span data-ttu-id="807e1-238">Selezionare il file hello desiderato tooopen.</span><span class="sxs-lookup"><span data-stu-id="807e1-238">Select hello file you wish tooopen.</span></span>
        
        <span data-ttu-id="807e1-239">b.</span><span class="sxs-lookup"><span data-stu-id="807e1-239">b.</span></span>  <span data-ttu-id="807e1-240">Sulla barra degli strumenti del riquadro principale hello, selezionare **aprire**.</span><span class="sxs-lookup"><span data-stu-id="807e1-240">On hello main pane's toolbar, select **Open**.</span></span>
        
        <span data-ttu-id="807e1-241">c.</span><span class="sxs-lookup"><span data-stu-id="807e1-241">c.</span></span>  <span data-ttu-id="807e1-242">file Hello verrà scaricato e aperto con l'applicazione hello associata al tipo sottostante del file hello.</span><span class="sxs-lookup"><span data-stu-id="807e1-242">hello file will be downloaded and opened using hello application associated with hello file's underlying file type.</span></span>

    - <span data-ttu-id="807e1-243">**Copiare negli Appunti toohello un file**</span><span class="sxs-lookup"><span data-stu-id="807e1-243">**Copy a file toohello clipboard**</span></span>

        <span data-ttu-id="807e1-244">a.</span><span class="sxs-lookup"><span data-stu-id="807e1-244">a.</span></span> <span data-ttu-id="807e1-245">Selezionare il file hello desiderato toocopy.</span><span class="sxs-lookup"><span data-stu-id="807e1-245">Select hello file you wish toocopy.</span></span>

        <span data-ttu-id="807e1-246">b.</span><span class="sxs-lookup"><span data-stu-id="807e1-246">b.</span></span> <span data-ttu-id="807e1-247">Sulla barra degli strumenti del riquadro principale hello, selezionare **copia**.</span><span class="sxs-lookup"><span data-stu-id="807e1-247">On hello main pane's toolbar, select **Copy**.</span></span>

        <span data-ttu-id="807e1-248">c.</span><span class="sxs-lookup"><span data-stu-id="807e1-248">c.</span></span> <span data-ttu-id="807e1-249">Nel riquadro di sinistra hello, passare tooanother condivisione di file e fare doppio clic tooview nel riquadro principale hello.</span><span class="sxs-lookup"><span data-stu-id="807e1-249">In hello left pane, navigate tooanother file share, and double-click it tooview it in hello main pane.</span></span>

        <span data-ttu-id="807e1-250">d.</span><span class="sxs-lookup"><span data-stu-id="807e1-250">d.</span></span> <span data-ttu-id="807e1-251">Sulla barra degli strumenti del riquadro principale hello, selezionare **Incolla** toocreate una copia del file hello.</span><span class="sxs-lookup"><span data-stu-id="807e1-251">On hello main pane's toolbar, select **Paste** toocreate a copy of hello file.</span></span>

    - <span data-ttu-id="807e1-252">**Eliminare un file**</span><span class="sxs-lookup"><span data-stu-id="807e1-252">**Delete a file**</span></span>

        <span data-ttu-id="807e1-253">a.</span><span class="sxs-lookup"><span data-stu-id="807e1-253">a.</span></span> <span data-ttu-id="807e1-254">Selezionare il file hello desiderato toodelete.</span><span class="sxs-lookup"><span data-stu-id="807e1-254">Select hello file you wish toodelete.</span></span>

        <span data-ttu-id="807e1-255">b.</span><span class="sxs-lookup"><span data-stu-id="807e1-255">b.</span></span> <span data-ttu-id="807e1-256">Sulla barra degli strumenti del riquadro principale hello, selezionare **eliminare**.</span><span class="sxs-lookup"><span data-stu-id="807e1-256">On hello main pane's toolbar, select **Delete**.</span></span>

        <span data-ttu-id="807e1-257">c.</span><span class="sxs-lookup"><span data-stu-id="807e1-257">c.</span></span> <span data-ttu-id="807e1-258">Selezionare **Sì** toohello nella finestra di conferma.</span><span class="sxs-lookup"><span data-stu-id="807e1-258">Select **Yes** toohello confirmation dialog.</span></span>

## <a name="next-steps"></a><span data-ttu-id="807e1-259">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="807e1-259">Next steps</span></span>

- <span data-ttu-id="807e1-260">Hello vista [note sulla versione di esplorazione dell'archiviazione (anteprima) e video più recenti](http://www.storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="807e1-260">View hello [latest Storage Explorer (Preview) release notes and videos](http://www.storageexplorer.com/).</span></span>

- <span data-ttu-id="807e1-261">Informazioni su come troppo[creare applicazioni usando BLOB di Azure, tabelle, code e i file](https://azure.microsoft.com/documentation/services/storage/).</span><span class="sxs-lookup"><span data-stu-id="807e1-261">Learn how too[create applications using Azure blobs, tables, queues, and files](https://azure.microsoft.com/documentation/services/storage/).</span></span>
