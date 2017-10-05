---
title: Gestire le risorse di archiviazione BLOB di Azure con Esplora archivi (anteprima) | Documentazione Microsoft
description: Gestire contenitori BLOB e BLOB di Azure con Storage Explorer (anteprima)
services: storage
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 2f09e545-ec94-4d89-b96c-14783cc9d7a9
ms.service: storage
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/18/2016
ms.author: kraigb
ms.openlocfilehash: f833027203441e12340bd93f3570de073d297223
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="manage-azure-blob-storage-resources-with-storage-explorer-preview"></a><span data-ttu-id="669a2-103">Gestire le risorse dell'archivio BLOB di Azure con Storage Explorer (anteprima)</span><span class="sxs-lookup"><span data-stu-id="669a2-103">Manage Azure Blob Storage resources with Storage Explorer (Preview)</span></span>
## <a name="overview"></a><span data-ttu-id="669a2-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="669a2-104">Overview</span></span>
<span data-ttu-id="669a2-105">[Archiviazione BLOB di Azure](storage/blobs/storage-dotnet-how-to-use-blobs.md) è un servizio per l'archiviazione di grandi quantità di dati non strutturati, ad esempio dati di testo o binari, a cui è possibile accedere da qualsiasi parte del mondo tramite HTTP o HTTPS.</span><span class="sxs-lookup"><span data-stu-id="669a2-105">[Azure Blob Storage](storage/blobs/storage-dotnet-how-to-use-blobs.md) is a service for storing large amounts of unstructured data, such as text or binary data, that can be accessed from anywhere in the world via HTTP or HTTPS.</span></span>
<span data-ttu-id="669a2-106">L'archiviazione BLOB può essere usata per esporre dati pubblicamente a livello mondiale o archiviare privatamente i dati delle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="669a2-106">You can use Blob storage to expose data publicly to the world, or to store application data privately.</span></span> <span data-ttu-id="669a2-107">In questo articolo si apprenderà come usare Storage Explorer (anteprima) per l'utilizzo di contenitori BLOB e BLOB.</span><span class="sxs-lookup"><span data-stu-id="669a2-107">In this article, you'll learn how to use Storage Explorer (Preview) to work with blob containers and blobs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="669a2-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="669a2-108">Prerequisites</span></span>
<span data-ttu-id="669a2-109">Per seguire la procedura descritta in questo articolo, è necessario eseguire queste operazioni:</span><span class="sxs-lookup"><span data-stu-id="669a2-109">To complete the steps in this article, you'll need the following:</span></span>

* [<span data-ttu-id="669a2-110">Scaricare e installare Storage Explorer (anteprima)</span><span class="sxs-lookup"><span data-stu-id="669a2-110">Download and install Storage Explorer (preview)</span></span>](http://www.storageexplorer.com)
* [<span data-ttu-id="669a2-111">Connettersi a un account o a un servizio di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="669a2-111">Connect to a Azure storage account or service</span></span>](vs-azure-tools-storage-manage-with-storage-explorer.md#connect-to-a-storage-account-or-service)

## <a name="create-a-blob-container"></a><span data-ttu-id="669a2-112">Creare un contenitore BLOB</span><span class="sxs-lookup"><span data-stu-id="669a2-112">Create a blob container</span></span>
<span data-ttu-id="669a2-113">Tutti i BLOB devono risiedere in un contenitore BLOB, che è semplicemente un raggruppamento logico di BLOB.</span><span class="sxs-lookup"><span data-stu-id="669a2-113">All blobs must reside in a blob container, which is simply a logical grouping of blobs.</span></span> <span data-ttu-id="669a2-114">Un account può contenere un numero illimitato di contenitori e ogni contenitore può archiviare un numero illimitato di BLOB.</span><span class="sxs-lookup"><span data-stu-id="669a2-114">An account can contain an unlimited number of containers, and each container can store an unlimited number of blobs.</span></span>

<span data-ttu-id="669a2-115">I passaggi seguenti illustrano come creare un contenitore BLOB all'interno di Storage Explorer (anteprima).</span><span class="sxs-lookup"><span data-stu-id="669a2-115">The following steps illustrate how to create a blob container within Storage Explorer (Preview).</span></span>

1. <span data-ttu-id="669a2-116">Aprire Storage Explorer (anteprima).</span><span class="sxs-lookup"><span data-stu-id="669a2-116">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="669a2-117">Nel riquadro sinistro espandere l'account di archiviazione all'interno del quale si vuole creare il contenitore BLOB.</span><span class="sxs-lookup"><span data-stu-id="669a2-117">In the left pane, expand the storage account within which you wish to create the blob container.</span></span>
3. <span data-ttu-id="669a2-118">Fare clic con il pulsante destro del mouse su **Contenitori BLOB** e scegliere **Crea contenitore BLOB** dal menu di scelta rapida.</span><span class="sxs-lookup"><span data-stu-id="669a2-118">Right-click **Blob Containers**, and - from the context menu - select **Create Blob Container**.</span></span>

   ![Menu di scelta rapida Crea contenitore BLOB][0]
4. <span data-ttu-id="669a2-120">Sotto la cartella **contenitori BLOB** verrà visualizzata una casella di testo.</span><span class="sxs-lookup"><span data-stu-id="669a2-120">A text box will appear below the **Blob Containers** folder.</span></span> <span data-ttu-id="669a2-121">Immettere il nome per il contenitore BLOB.</span><span class="sxs-lookup"><span data-stu-id="669a2-121">Enter the name for your blob container.</span></span> <span data-ttu-id="669a2-122">Per un elenco di regole e restrizioni relative alla denominazione dei contenitori BLOB, vedere [Regole di denominazione dei contenitori](storage/blobs/storage-dotnet-how-to-use-blobs.md#create-a-container).</span><span class="sxs-lookup"><span data-stu-id="669a2-122">See the [Container naming rules](storage/blobs/storage-dotnet-how-to-use-blobs.md#create-a-container) section for a list of rules and restrictions on naming blob containers.</span></span>

   ![Casella di testo Crea contenitore BLOB][1]
5. <span data-ttu-id="669a2-124">Premere **INVIO** al termine della creazione del contenitore BLOB o **ESC** per annullare.</span><span class="sxs-lookup"><span data-stu-id="669a2-124">Press **Enter** when done to create the blob container, or **Esc** to cancel.</span></span> <span data-ttu-id="669a2-125">Dopo aver creato il contenitore BLOB, verrà visualizzato sotto la cartella **contenitori BLOB** per l'account di archiviazione selezionato.</span><span class="sxs-lookup"><span data-stu-id="669a2-125">Once the blob container has been successfully created, it will be displayed under the **Blob Containers** folder for the selected storage account.</span></span>

   ![Contenitore BLOB creato][2]

## <a name="view-a-blob-containers-contents"></a><span data-ttu-id="669a2-127">Visualizzare il contenuto di un contenitore BLOB</span><span class="sxs-lookup"><span data-stu-id="669a2-127">View a blob container's contents</span></span>
<span data-ttu-id="669a2-128">I contenitori BLOB includono BLOB e cartelle, che possono anche contenere BLOB.</span><span class="sxs-lookup"><span data-stu-id="669a2-128">Blob containers contain blobs and folders (that can also contain blobs).</span></span>

<span data-ttu-id="669a2-129">I passaggi seguenti illustrano come visualizzare il contenuto di un contenitore BLOB all'interno di Storage Explorer (anteprima):</span><span class="sxs-lookup"><span data-stu-id="669a2-129">The following steps illustrate how to view the contents of a blob container within Storage Explorer (Preview):</span></span>

1. <span data-ttu-id="669a2-130">Aprire Storage Explorer (anteprima).</span><span class="sxs-lookup"><span data-stu-id="669a2-130">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="669a2-131">Nel riquadro sinistro espandere l'account di archiviazione che include il contenitore BLOB da visualizzare.</span><span class="sxs-lookup"><span data-stu-id="669a2-131">In the left pane, expand the storage account containing the blob container you wish to view.</span></span>
3. <span data-ttu-id="669a2-132">Espandere **contenitori BLOB**dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="669a2-132">Expand the storage account's **Blob Containers**.</span></span>
4. <span data-ttu-id="669a2-133">Fare clic con il pulsante destro del mouse sul contenitore BLOB che si vuole visualizzare e scegliere **Open Blob Container Editor**(Apri editor contenitori BLOB) dal menu di scelta rapida.</span><span class="sxs-lookup"><span data-stu-id="669a2-133">Right-click the blob container you wish to view, and - from the context menu - select **Open Blob Container Editor**.</span></span>
   <span data-ttu-id="669a2-134">È anche possibile fare doppio clic sul contenitore BLOB che si vuole visualizzare.</span><span class="sxs-lookup"><span data-stu-id="669a2-134">You can also double-click the blob container you wish to view.</span></span>

   ![Menu di scelta rapida Open Blob Container Editor (Apri editor contenitori BLOB)][19]
5. <span data-ttu-id="669a2-136">Nel riquadro principale verrà visualizzato il contenuto del contenitore BLOB.</span><span class="sxs-lookup"><span data-stu-id="669a2-136">The main pane will display the blob container's contents.</span></span>

   ![Editor contenitori BLOB][3]

## <a name="delete-a-blob-container"></a><span data-ttu-id="669a2-138">Eliminare un contenitore BLOB</span><span class="sxs-lookup"><span data-stu-id="669a2-138">Delete a blob container</span></span>
<span data-ttu-id="669a2-139">I contenitori di BLOB possono essere creati facilmente ed eliminati in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="669a2-139">Blob containers can be easily created and deleted as needed.</span></span> <span data-ttu-id="669a2-140">Per informazioni su come eliminare singoli BLOB, vedere la sezione [Gestione dei BLOB in un contenitore BLOB](#managing-blobs-in-a-blob-container).</span><span class="sxs-lookup"><span data-stu-id="669a2-140">(To see how to delete individual blobs, refer to the section, [Managing blobs in a blob container](#managing-blobs-in-a-blob-container).)</span></span>

<span data-ttu-id="669a2-141">I passaggi seguenti illustrano come eliminare un contenitore BLOB all'interno di Storage Explorer (anteprima):</span><span class="sxs-lookup"><span data-stu-id="669a2-141">The following steps illustrate how to delete a blob container within Storage Explorer (Preview):</span></span>

1. <span data-ttu-id="669a2-142">Aprire Storage Explorer (anteprima).</span><span class="sxs-lookup"><span data-stu-id="669a2-142">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="669a2-143">Nel riquadro sinistro espandere l'account di archiviazione che include il contenitore BLOB da visualizzare.</span><span class="sxs-lookup"><span data-stu-id="669a2-143">In the left pane, expand the storage account containing the blob container you wish to view.</span></span>
3. <span data-ttu-id="669a2-144">Espandere **contenitori BLOB**dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="669a2-144">Expand the storage account's **Blob Containers**.</span></span>
4. <span data-ttu-id="669a2-145">Fare clic con il pulsante destro del mouse sul contenitore BLOB che si vuole eliminare e scegliere **Elimina**dal menu di scelta rapida.</span><span class="sxs-lookup"><span data-stu-id="669a2-145">Right-click the blob container you wish to delete, and - from the context menu - select **Delete**.</span></span>
   <span data-ttu-id="669a2-146">È anche possibile premere **CANC** per eliminare il contenitore BLOB attualmente selezionato.</span><span class="sxs-lookup"><span data-stu-id="669a2-146">You can also press **Delete** to delete the currently selected blob container.</span></span>

   ![Menu di scelta rapida Elimina per il contenitore BLOB][4]
5. <span data-ttu-id="669a2-148">Fare clic su **Sì** nella finestra di dialogo di conferma.</span><span class="sxs-lookup"><span data-stu-id="669a2-148">Select **Yes** to the confirmation dialog.</span></span>

   ![Menu di scelta rapida dell'eliminazione per il contenitore BLOB][5]

## <a name="copy-a-blob-container"></a><span data-ttu-id="669a2-150">Copiare un contenitore BLOB</span><span class="sxs-lookup"><span data-stu-id="669a2-150">Copy a blob container</span></span>
<span data-ttu-id="669a2-151">Storage Explorer (anteprima) consente di copiare un contenitore BLOB negli Appunti e quindi incollarlo in un altro account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="669a2-151">Storage Explorer (Preview) enables you to copy a blob container to the clipboard, and then paste that blob container into another storage account.</span></span> <span data-ttu-id="669a2-152">Per informazioni su come copiare singoli BLOB, vedere la sezione [Gestione dei BLOB in un contenitore BLOB](#managing-blobs-in-a-blob-container).</span><span class="sxs-lookup"><span data-stu-id="669a2-152">(To see how to copy individual blobs, refer to the section, [Managing blobs in a blob container](#managing-blobs-in-a-blob-container).)</span></span>

<span data-ttu-id="669a2-153">I passaggi seguenti illustrano come copiare un contenitore BLOB da un account di archiviazione a un altro.</span><span class="sxs-lookup"><span data-stu-id="669a2-153">The following steps illustrate how to copy a blob container from one storage account to another.</span></span>

1. <span data-ttu-id="669a2-154">Aprire Storage Explorer (anteprima).</span><span class="sxs-lookup"><span data-stu-id="669a2-154">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="669a2-155">Nel riquadro sinistro espandere l'account di archiviazione che include il contenitore BLOB da copiare.</span><span class="sxs-lookup"><span data-stu-id="669a2-155">In the left pane, expand the storage account containing the blob container you wish to copy.</span></span>
3. <span data-ttu-id="669a2-156">Espandere **contenitori BLOB**dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="669a2-156">Expand the storage account's **Blob Containers**.</span></span>
4. <span data-ttu-id="669a2-157">Fare clic con il pulsante destro del mouse sul contenitore BLOB che si vuole copiare e scegliere **Copy Blob Container**(Copia contenitore BLOB) dal menu di scelta rapida.</span><span class="sxs-lookup"><span data-stu-id="669a2-157">Right-click the blob container you wish to copy, and - from the context menu - select **Copy Blob Container**.</span></span>

   ![Menu di scelta Copy Blob Container (Copia contenitore BLOB)][6]
5. <span data-ttu-id="669a2-159">Fare clic con il pulsante destro del mouse sull'account di archiviazione di "destinazione" in cui si vuole incollare il contenitore BLOB e - scegliere **Paste Blob Container**(Incolla contenitore BLOB) dal menu di scelta rapida.</span><span class="sxs-lookup"><span data-stu-id="669a2-159">Right-click the desired "target" storage account into which you want to paste the blob container, and - from the context menu - select **Paste Blob Container**.</span></span>

   ![Menu di scelta rapida Paste Blob Container (Incolla contenitore BLOB)][7]

## <a name="get-the-sas-for-a-blob-container"></a><span data-ttu-id="669a2-161">Ottenere la firma di accesso condiviso per un contenitore BLOB</span><span class="sxs-lookup"><span data-stu-id="669a2-161">Get the SAS for a blob container</span></span>
<span data-ttu-id="669a2-162">Una [firma di accesso condiviso (SAS)](storage/common/storage-dotnet-shared-access-signature-part-1.md) fornisce accesso delegato alle risorse nell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="669a2-162">A [shared access signature (SAS)](storage/common/storage-dotnet-shared-access-signature-part-1.md) provides delegated access to resources in your storage account.</span></span>
<span data-ttu-id="669a2-163">Questo significa che è possibile concedere a un client autorizzazioni limitate per BLOB, code o tabelle per un periodo di tempo specificato e con un set di autorizzazioni specificato senza dover condividere le chiavi di accesso dell'account.</span><span class="sxs-lookup"><span data-stu-id="669a2-163">This means that you can grant a client limited permissions to objects in your storage account for a specified period of time and with a specified set of permissions, without having to share your account access keys.</span></span>

<span data-ttu-id="669a2-164">I passaggi seguenti illustrano come creare una firma di accesso condiviso per un contenitore BLOB:</span><span class="sxs-lookup"><span data-stu-id="669a2-164">The following steps illustrate how to create a SAS for a blob container:</span></span>

1. <span data-ttu-id="669a2-165">Aprire Storage Explorer (anteprima).</span><span class="sxs-lookup"><span data-stu-id="669a2-165">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="669a2-166">Nel riquadro sinistro espandere l'account di archiviazione che include il contenitore BLOB per cui si vuole ottenere una firma di accesso condiviso.</span><span class="sxs-lookup"><span data-stu-id="669a2-166">In the left pane, expand the storage account containing the blob container for which you wish to get a SAS.</span></span>
3. <span data-ttu-id="669a2-167">Espandere **contenitori BLOB**dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="669a2-167">Expand the storage account's **Blob Containers**.</span></span>
4. <span data-ttu-id="669a2-168">Fare clic con il pulsante destro del mouse sul contenitore BLOB desiderato e scegliere **Get Shared Access Signature**(Ottieni firma di accesso condiviso) dal menu di scelta rapida.</span><span class="sxs-lookup"><span data-stu-id="669a2-168">Right-click the desired blob container, and - from the context menu - select **Get Shared Access Signature**.</span></span>

   ![Menu di scelta rapida Get Shared Access Signature (Ottieni firma di accesso condiviso)][8]
5. <span data-ttu-id="669a2-170">Nella finestra di dialogo **Firma di accesso condiviso** specificare i criteri, le date di inizio e di scadenza, il fuso orario e i livelli di accesso da impostare per la risorsa.</span><span class="sxs-lookup"><span data-stu-id="669a2-170">In the **Shared Access Signature** dialog, specify the policy, start and expiration dates, time zone, and access levels you want for the resource.</span></span>

   ![Opzioni di Get Shared Access Signature (Ottieni firma di accesso condiviso)][9]
6. <span data-ttu-id="669a2-172">Una volta specificate le opzioni per la firma di accesso condiviso, scegliere **Crea**.</span><span class="sxs-lookup"><span data-stu-id="669a2-172">When you're finished specifying the SAS options, select **Create**.</span></span>
7. <span data-ttu-id="669a2-173">Verrà visualizzata una seconda finestra di dialogo **Firma di accesso condiviso** con l'elenco del contenitore BLOB insieme all'URL e alle stringhe di query che è possibile usare per accedere alla risorsa di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="669a2-173">A second **Shared Access Signature** dialog will then display that lists the blob container along with the URL and QueryStrings you can use to access the storage resource.</span></span>
   <span data-ttu-id="669a2-174">Selezionare **Copia** accanto all'URL che si vuole copiare negli Appunti.</span><span class="sxs-lookup"><span data-stu-id="669a2-174">Select **Copy** next to the URL you wish to copy to the clipboard.</span></span>

   ![Copiare gli URL della firma di accesso condiviso][10]
8. <span data-ttu-id="669a2-176">Al termine, scegliere **Chiudi**.</span><span class="sxs-lookup"><span data-stu-id="669a2-176">When done, select **Close**.</span></span>

## <a name="manage-access-policies-for-a-blob-container"></a><span data-ttu-id="669a2-177">Gestire i criteri di accesso per un contenitore BLOB</span><span class="sxs-lookup"><span data-stu-id="669a2-177">Manage Access Policies for a blob container</span></span>
<span data-ttu-id="669a2-178">I passaggi seguenti illustrano come gestire, ovvero aggiungere e rimuovere, criteri di accesso per un contenitore BLOB:</span><span class="sxs-lookup"><span data-stu-id="669a2-178">The following steps illustrate how to manage (add and remove) access policies for a blob container:</span></span>

1. <span data-ttu-id="669a2-179">Aprire Storage Explorer (anteprima).</span><span class="sxs-lookup"><span data-stu-id="669a2-179">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="669a2-180">Nel riquadro sinistro espandere l'account di archiviazione che include il contenitore BLOB di cui si vogliono gestire i criteri di accesso.</span><span class="sxs-lookup"><span data-stu-id="669a2-180">In the left pane, expand the storage account containing the blob container whose access policies you wish to manage.</span></span>
3. <span data-ttu-id="669a2-181">Espandere **contenitori BLOB**dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="669a2-181">Expand the storage account's **Blob Containers**.</span></span>
4. <span data-ttu-id="669a2-182">Selezionare il contenitore BLOB desiderato e scegliere **Manage Access Policies**(Gestisci criteri di accesso) dal menu di scelta rapida.</span><span class="sxs-lookup"><span data-stu-id="669a2-182">Select the desired blob container, and - from the context menu - select **Manage Access Policies**.</span></span>

   ![Menu di scelta rapida Manage Access Policies (Gestisci criteri di accesso)][11]
5. <span data-ttu-id="669a2-184">Nella finestra di dialogo **Criteri di accesso** saranno elencati tutti i criteri di accesso già creati per il contenitore BLOB selezionato.</span><span class="sxs-lookup"><span data-stu-id="669a2-184">The **Access Policies** dialog will list any access policies already created for the selected blob container.</span></span>

   ![Opzioni di Criteri di accesso][12]        
6. <span data-ttu-id="669a2-186">Seguire questi passaggi a seconda dell'attività di gestione dei criteri di accesso:</span><span class="sxs-lookup"><span data-stu-id="669a2-186">Follow these steps depending on the access policy management task:</span></span>

   * <span data-ttu-id="669a2-187">**Aggiungere nuovi criteri di accesso**: selezionare **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="669a2-187">**Add a new access policy** - Select **Add**.</span></span> <span data-ttu-id="669a2-188">Una volta generati, nella finestra di dialogo **Criteri di accesso** verranno visualizzati i criteri di accesso appena aggiunti, con le impostazioni predefinite.</span><span class="sxs-lookup"><span data-stu-id="669a2-188">Once generated, the **Access Policies** dialog will display the newly added access policy (with default settings).</span></span>
   * <span data-ttu-id="669a2-189">**Modificare i criteri di accesso**: apportare le modifiche desiderate e scegliere **Salva**.</span><span class="sxs-lookup"><span data-stu-id="669a2-189">**Edit an access policy** -  Make any desired edits, and select **Save**.</span></span>
   * <span data-ttu-id="669a2-190">**Rimuovere criteri di accesso**: selezionare **Rimuovi** accanto ai criteri di accesso da rimuovere.</span><span class="sxs-lookup"><span data-stu-id="669a2-190">**Remove an access policy** - Select **Remove** next to the access policy you wish to remove.</span></span>

## <a name="set-the-public-access-level-for-a-blob-container"></a><span data-ttu-id="669a2-191">Impostare il livello di accesso pubblico per un contenitore BLOB</span><span class="sxs-lookup"><span data-stu-id="669a2-191">Set the Public Access Level for a blob container</span></span>
<span data-ttu-id="669a2-192">Per impostazione predefinita, ogni contenitore BLOB è impostato su "No public access" (Nessun accesso pubblico).</span><span class="sxs-lookup"><span data-stu-id="669a2-192">By default, every blob container is set to "No public access".</span></span>

<span data-ttu-id="669a2-193">La procedura seguente illustra come specificare un livello di accesso pubblico per un contenitore BLOB.</span><span class="sxs-lookup"><span data-stu-id="669a2-193">The following steps illustrate how to specify a public access level for a blob container.</span></span>

1. <span data-ttu-id="669a2-194">Aprire Storage Explorer (anteprima).</span><span class="sxs-lookup"><span data-stu-id="669a2-194">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="669a2-195">Nel riquadro sinistro espandere l'account di archiviazione che include il contenitore BLOB di cui si vogliono gestire i criteri di accesso.</span><span class="sxs-lookup"><span data-stu-id="669a2-195">In the left pane, expand the storage account containing the blob container whose access policies you wish to manage.</span></span>
3. <span data-ttu-id="669a2-196">Espandere **contenitori BLOB**dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="669a2-196">Expand the storage account's **Blob Containers**.</span></span>
4. <span data-ttu-id="669a2-197">Selezionare il contenitore BLOB desiderato e scegliere **Set Public Access Level**(Imposta livello di accesso pubblico) dal menu di scelta rapida.</span><span class="sxs-lookup"><span data-stu-id="669a2-197">Select the desired blob container, and - from the context menu - select **Set Public Access Level**.</span></span>

   ![Menu di scelta rapida Set Public Access Level (Imposta livello di accesso pubblico)][13]
5. <span data-ttu-id="669a2-199">Nella finestra di dialogo **Set Container Public Access Level** (Imposta livello di accesso pubblico del contenitore) specificare il livello di accesso desiderato.</span><span class="sxs-lookup"><span data-stu-id="669a2-199">In the **Set Container Public Access Level** dialog, specify the desired access level.</span></span>

   ![Opzioni di Set Public Access Level (Imposta livello di accesso pubblico)][14]
6. <span data-ttu-id="669a2-201">Selezionare **Applica**.</span><span class="sxs-lookup"><span data-stu-id="669a2-201">Select **Apply**.</span></span>

## <a name="managing-blobs-in-a-blob-container"></a><span data-ttu-id="669a2-202">Gestione dei BLOB in un contenitore BLOB</span><span class="sxs-lookup"><span data-stu-id="669a2-202">Managing blobs in a blob container</span></span>
<span data-ttu-id="669a2-203">Dopo aver creato un contenitore BLOB, è possibile caricare un BLOB in tale contenitore BLOB, scaricare un BLOB nel computer locale, aprire un BLOB nel computer locale e molto altro ancora.</span><span class="sxs-lookup"><span data-stu-id="669a2-203">Once you've created a blob container, you can upload a blob to that blob container, download a blob to your local computer, open a blob on your local computer, and much more.</span></span>

<span data-ttu-id="669a2-204">I passaggi seguenti illustrano come gestire i BLOB e le cartelle all'interno di un contenitore BLOB.</span><span class="sxs-lookup"><span data-stu-id="669a2-204">The following steps illustrate how to manage the blobs (and folders) within a blob container.</span></span>

1. <span data-ttu-id="669a2-205">Aprire Storage Explorer (anteprima).</span><span class="sxs-lookup"><span data-stu-id="669a2-205">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="669a2-206">Nel riquadro sinistro espandere l'account di archiviazione che include il contenitore BLOB da gestire.</span><span class="sxs-lookup"><span data-stu-id="669a2-206">In the left pane, expand the storage account containing the blob container you wish to manage.</span></span>
3. <span data-ttu-id="669a2-207">Espandere **contenitori BLOB**dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="669a2-207">Expand the storage account's **Blob Containers**.</span></span>
4. <span data-ttu-id="669a2-208">Fare doppio clic sul contenitore BLOB che si vuole visualizzare.</span><span class="sxs-lookup"><span data-stu-id="669a2-208">Double-click the blob container you wish to view.</span></span>
5. <span data-ttu-id="669a2-209">Nel riquadro principale verrà visualizzato il contenuto del contenitore BLOB.</span><span class="sxs-lookup"><span data-stu-id="669a2-209">The main pane will display the blob container's contents.</span></span>

   ![Visualizzazione del contenitore BLOB][3]
6. <span data-ttu-id="669a2-211">Nel riquadro principale verrà visualizzato il contenuto del contenitore BLOB.</span><span class="sxs-lookup"><span data-stu-id="669a2-211">The main pane will display the blob container's contents.</span></span>
7. <span data-ttu-id="669a2-212">Seguire questi passaggi in base all'attività da eseguire:</span><span class="sxs-lookup"><span data-stu-id="669a2-212">Follow these steps depending on the task you wish to perform:</span></span>

   * <span data-ttu-id="669a2-213">**Caricare file in un contenitore BLOB**</span><span class="sxs-lookup"><span data-stu-id="669a2-213">**Upload files to a blob container**</span></span>

     1. <span data-ttu-id="669a2-214">Sulla barra degli strumenti del riquadro principale selezionare **Carica** e quindi **Carica i file** dal menu a discesa.</span><span class="sxs-lookup"><span data-stu-id="669a2-214">On the main pane's toolbar, select **Upload**, and then **Upload Files** from the drop-down menu.</span></span>

        ![Menu Carica i file][15]
     2. <span data-ttu-id="669a2-216">Nella finestra di dialogo **Carica i file** scegliere il pulsante con i puntini di sospensione (**…**) a destra della casella **File** per selezionare i file da caricare.</span><span class="sxs-lookup"><span data-stu-id="669a2-216">In the **Upload files** dialog, select the ellipsis (**…**) button on the right side of the **Files** text box to select the file(s) you wish to upload.</span></span>

        ![Opzioni di Carica i file][16]
     3. <span data-ttu-id="669a2-218">Specificare un valore per tipo **Tipo BLOB**.</span><span class="sxs-lookup"><span data-stu-id="669a2-218">Specify the type of **Blob type**.</span></span> <span data-ttu-id="669a2-219">L'articolo [Introduzione all'archiviazione BLOB di Azure con .NET](storage/blobs/storage-dotnet-how-to-use-blobs.md#blob-service-concepts) illustra le differenze tra i vari tipi di BLOB.</span><span class="sxs-lookup"><span data-stu-id="669a2-219">The article [Get started with Azure Blob storage using .NET](storage/blobs/storage-dotnet-how-to-use-blobs.md#blob-service-concepts) explains the differences between the various blob types.</span></span>
     4. <span data-ttu-id="669a2-220">È possibile specificare una cartella di destinazione in cui verranno caricati i file selezionati.</span><span class="sxs-lookup"><span data-stu-id="669a2-220">Optionally, specify a target folder into which the selected file(s) will be uploaded.</span></span> <span data-ttu-id="669a2-221">Se la cartella di destinazione non esiste, verrà creata.</span><span class="sxs-lookup"><span data-stu-id="669a2-221">If the target folder doesn’t exist, it will be created.</span></span>
     5. <span data-ttu-id="669a2-222">Selezionare **Carica**.</span><span class="sxs-lookup"><span data-stu-id="669a2-222">Select **Upload**.</span></span>
   * <span data-ttu-id="669a2-223">**Caricare una cartella in un contenitore BLOB**</span><span class="sxs-lookup"><span data-stu-id="669a2-223">**Upload a folder to a blob container**</span></span>

     1. <span data-ttu-id="669a2-224">Sulla barra degli strumenti del riquadro principale selezionare **Carica** e quindi **Upload Folder** (Carica cartella) dal menu a discesa.</span><span class="sxs-lookup"><span data-stu-id="669a2-224">On the main pane's toolbar, select **Upload**, and then **Upload Folder** from the drop-down menu.</span></span>

        ![Menu di Upload Folder (Carica cartella)][17]
     2. <span data-ttu-id="669a2-226">Nella finestra di dialogo **Upload Folder** (Carica cartella) scegliere il pulsante con i puntini di sospensione (**…**) a destra della casella di testo **Cartella** per selezionare la cartella di cui si vuole caricare il contenuto.</span><span class="sxs-lookup"><span data-stu-id="669a2-226">In the **Upload folder** dialog, select the ellipsis (**…**) button on the right side of the **Folder** text box to select the folder whose contents you wish to upload.</span></span>

        ![Opzioni di Upload Folder (Carica cartella)][18]
     3. <span data-ttu-id="669a2-228">Specificare un valore per tipo **Tipo BLOB**.</span><span class="sxs-lookup"><span data-stu-id="669a2-228">Specify the type of **Blob type**.</span></span> <span data-ttu-id="669a2-229">L'articolo [Introduzione all'archiviazione BLOB di Azure con .NET](storage/blobs/storage-dotnet-how-to-use-blobs.md#blob-service-concepts) illustra le differenze tra i vari tipi di BLOB.</span><span class="sxs-lookup"><span data-stu-id="669a2-229">The article [Get started with Azure Blob storage using .NET](storage/blobs/storage-dotnet-how-to-use-blobs.md#blob-service-concepts) explains the differences between the various blob types.</span></span>
     4. <span data-ttu-id="669a2-230">È possibile specificare una cartella di destinazione in cui verrà caricato il contenuto della cartella selezionata.</span><span class="sxs-lookup"><span data-stu-id="669a2-230">Optionally, specify a target folder into which the selected folder's contents will be uploaded.</span></span> <span data-ttu-id="669a2-231">Se la cartella di destinazione non esiste, verrà creata.</span><span class="sxs-lookup"><span data-stu-id="669a2-231">If the target folder doesn’t exist, it will be created.</span></span>
     5. <span data-ttu-id="669a2-232">Selezionare **Carica**.</span><span class="sxs-lookup"><span data-stu-id="669a2-232">Select **Upload**.</span></span>
   * <span data-ttu-id="669a2-233">**Scaricare un BLOB nel computer locale**</span><span class="sxs-lookup"><span data-stu-id="669a2-233">**Download a blob to your local computer**</span></span>

     1. <span data-ttu-id="669a2-234">Selezionare il blob che si vuole scaricare.</span><span class="sxs-lookup"><span data-stu-id="669a2-234">Select the blob you wish to download.</span></span>
     2. <span data-ttu-id="669a2-235">Sulla barra degli strumenti del riquadro principale selezionare **Scarica**.</span><span class="sxs-lookup"><span data-stu-id="669a2-235">On the main pane's toolbar, select **Download**.</span></span>
     3. <span data-ttu-id="669a2-236">Nella finestra di dialogo **Specify where to save the downloaded blob** (Specificare dove salvare il BLOB scaricato) specificare il percorso in cui salvare il BLOB scaricato e il nome da assegnare.</span><span class="sxs-lookup"><span data-stu-id="669a2-236">In the **Specify where to save the downloaded blob** dialog, specify the location where you want the blob downloaded, and the name you wish to give it.</span></span>  
     4. <span data-ttu-id="669a2-237">Selezionare **Salva**.</span><span class="sxs-lookup"><span data-stu-id="669a2-237">Select **Save**.</span></span>
   * <span data-ttu-id="669a2-238">**Aprire un BLOB nel computer locale**</span><span class="sxs-lookup"><span data-stu-id="669a2-238">**Open a blob on your local computer**</span></span>

     1. <span data-ttu-id="669a2-239">Selezionare il BLOB che si vuole aprire.</span><span class="sxs-lookup"><span data-stu-id="669a2-239">Select the blob you wish to open.</span></span>
     2. <span data-ttu-id="669a2-240">Sulla barra degli strumenti del riquadro principale selezionare **Apri**.</span><span class="sxs-lookup"><span data-stu-id="669a2-240">On the main pane's toolbar, select **Open**.</span></span>
     3. <span data-ttu-id="669a2-241">Il BLOB verrà scaricato e aperto usando l'applicazione associata al tipo di file sottostante del BLOB.</span><span class="sxs-lookup"><span data-stu-id="669a2-241">The blob will be downloaded and opened using the application associated with the blob's underlying file type.</span></span>
   * <span data-ttu-id="669a2-242">**Copiare un BLOB negli Appunti**</span><span class="sxs-lookup"><span data-stu-id="669a2-242">**Copy a blob to the clipboard**</span></span>

     1. <span data-ttu-id="669a2-243">Selezionare il BLOB che si vuole copiare.</span><span class="sxs-lookup"><span data-stu-id="669a2-243">Select the blob you wish to copy.</span></span>
     2. <span data-ttu-id="669a2-244">Sulla barra degli strumenti del riquadro principale selezionare **Copia**.</span><span class="sxs-lookup"><span data-stu-id="669a2-244">On the main pane's toolbar, select **Copy**.</span></span>
     3. <span data-ttu-id="669a2-245">Nel riquadro a sinistra passare a un altro contenitore BLOB e fare doppio clic su esso per visualizzarlo nel riquadro principale.</span><span class="sxs-lookup"><span data-stu-id="669a2-245">In the left pane, navigate to another blob container, and double-click it to view it in the main pane.</span></span>
     4. <span data-ttu-id="669a2-246">Sulla barra degli strumenti del riquadro principale selezionare **Incolla** per creare una copia del BLOB.</span><span class="sxs-lookup"><span data-stu-id="669a2-246">On the main pane's toolbar, select **Paste** to create a copy of the blob.</span></span>
   * <span data-ttu-id="669a2-247">**Eliminare un BLOB**</span><span class="sxs-lookup"><span data-stu-id="669a2-247">**Delete a blob**</span></span>

     1. <span data-ttu-id="669a2-248">Selezionare il BLOB che si vuole eliminare.</span><span class="sxs-lookup"><span data-stu-id="669a2-248">Select the blob you wish to delete.</span></span>
     2. <span data-ttu-id="669a2-249">Sulla barra degli strumenti del riquadro principale selezionare **Elimina**.</span><span class="sxs-lookup"><span data-stu-id="669a2-249">On the main pane's toolbar, select **Delete**.</span></span>
     3. <span data-ttu-id="669a2-250">Fare clic su **Sì** nella finestra di dialogo di conferma.</span><span class="sxs-lookup"><span data-stu-id="669a2-250">Select **Yes** to the confirmation dialog.</span></span>

## <a name="next-steps"></a><span data-ttu-id="669a2-251">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="669a2-251">Next steps</span></span>
* <span data-ttu-id="669a2-252">Vedere le note sulla versione e i video in [Microsoft Azure Storage Explorer](http://www.storageexplorer.com)(anteprima).</span><span class="sxs-lookup"><span data-stu-id="669a2-252">View the [latest Storage Explorer (Preview) release notes and videos](http://www.storageexplorer.com).</span></span>
* <span data-ttu-id="669a2-253">Informazioni su come creare applicazioni con BLOB, tabelle, code e file di Azure nella [Documentazione su Archiviazione](https://azure.microsoft.com/documentation/services/storage/).</span><span class="sxs-lookup"><span data-stu-id="669a2-253">Learn how to [create applications using Azure blobs, tables, queues, and files](https://azure.microsoft.com/documentation/services/storage/).</span></span>

[0]: ./media/vs-azure-tools-storage-explorer-blobs/blob-containers-create-context-menu.png
[1]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-create.png
[2]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-create-done.png
[3]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-editor.png
[4]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-delete-context-menu.png
[5]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-delete-confirmation.png
[6]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-copy-context-menu.png
[7]: ./media/vs-azure-tools-storage-explorer-blobs/blob-containers-paste-context-menu.png
[8]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-get-sas-context-menu.png
[9]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-get-sas-options.png
[10]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-get-sas-urls.png
[11]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-manage-access-policies-context-menu.png
[12]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-manage-access-policies-options.png
[13]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-set-public-access-level-context-menu.png
[14]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-set-public-access-level-options.png
[15]: ./media/vs-azure-tools-storage-explorer-blobs/blob-upload-files-menu.png
[16]: ./media/vs-azure-tools-storage-explorer-blobs/blob-upload-files-options.png
[17]: ./media/vs-azure-tools-storage-explorer-blobs/blob-upload-folder-menu.png
[18]: ./media/vs-azure-tools-storage-explorer-blobs/blob-upload-folder-options.png
[19]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-open-editor-context-menu.png
