---
title: risorse di archiviazione Blob di Azure aaaManage con Esplora risorse di archiviazione (anteprima) | Documenti Microsoft
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
ms.openlocfilehash: 503dd061b205875da127378ab48e8d465800fc09
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-blob-storage-resources-with-storage-explorer-preview"></a><span data-ttu-id="153ad-103">Gestire le risorse dell'archivio BLOB di Azure con Storage Explorer (anteprima)</span><span class="sxs-lookup"><span data-stu-id="153ad-103">Manage Azure Blob Storage resources with Storage Explorer (Preview)</span></span>
## <a name="overview"></a><span data-ttu-id="153ad-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="153ad-104">Overview</span></span>
<span data-ttu-id="153ad-105">[Archiviazione Blob di Azure](storage/blobs/storage-dotnet-how-to-use-blobs.md) è un servizio per l'archiviazione di grandi quantità di dati non strutturati, ad esempio dati di testo o binario, che è possibile accedere da qualsiasi in HelloWorld tramite HTTP o HTTPS.</span><span class="sxs-lookup"><span data-stu-id="153ad-105">[Azure Blob Storage](storage/blobs/storage-dotnet-how-to-use-blobs.md) is a service for storing large amounts of unstructured data, such as text or binary data, that can be accessed from anywhere in hello world via HTTP or HTTPS.</span></span>
<span data-ttu-id="153ad-106">È possibile utilizzare dati tooexpose di archiviazione Blob pubblicamente toohello world o dati dell'applicazione toostore privatamente.</span><span class="sxs-lookup"><span data-stu-id="153ad-106">You can use Blob storage tooexpose data publicly toohello world, or toostore application data privately.</span></span> <span data-ttu-id="153ad-107">In questo articolo si apprenderà come toouse Esplora archivi (Preview) toowork blob contenitori e BLOB.</span><span class="sxs-lookup"><span data-stu-id="153ad-107">In this article, you'll learn how toouse Storage Explorer (Preview) toowork with blob containers and blobs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="153ad-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="153ad-108">Prerequisites</span></span>
<span data-ttu-id="153ad-109">passaggi di hello toocomplete in questo articolo, è necessario seguente hello:</span><span class="sxs-lookup"><span data-stu-id="153ad-109">toocomplete hello steps in this article, you'll need hello following:</span></span>

* [<span data-ttu-id="153ad-110">Scaricare e installare Storage Explorer (anteprima)</span><span class="sxs-lookup"><span data-stu-id="153ad-110">Download and install Storage Explorer (preview)</span></span>](http://www.storageexplorer.com)
* [<span data-ttu-id="153ad-111">Connettersi al servizio o account di archiviazione di Azure tooa</span><span class="sxs-lookup"><span data-stu-id="153ad-111">Connect tooa Azure storage account or service</span></span>](vs-azure-tools-storage-manage-with-storage-explorer.md#connect-to-a-storage-account-or-service)

## <a name="create-a-blob-container"></a><span data-ttu-id="153ad-112">Creare un contenitore BLOB</span><span class="sxs-lookup"><span data-stu-id="153ad-112">Create a blob container</span></span>
<span data-ttu-id="153ad-113">Tutti i BLOB devono risiedere in un contenitore BLOB, che è semplicemente un raggruppamento logico di BLOB.</span><span class="sxs-lookup"><span data-stu-id="153ad-113">All blobs must reside in a blob container, which is simply a logical grouping of blobs.</span></span> <span data-ttu-id="153ad-114">Un account può contenere un numero illimitato di contenitori e ogni contenitore può archiviare un numero illimitato di BLOB.</span><span class="sxs-lookup"><span data-stu-id="153ad-114">An account can contain an unlimited number of containers, and each container can store an unlimited number of blobs.</span></span>

<span data-ttu-id="153ad-115">Hello passaggi seguenti viene illustrato come toocreate un contenitore di blob all'interno di soluzioni di archiviazione (anteprima).</span><span class="sxs-lookup"><span data-stu-id="153ad-115">hello following steps illustrate how toocreate a blob container within Storage Explorer (Preview).</span></span>

1. <span data-ttu-id="153ad-116">Aprire Storage Explorer (anteprima).</span><span class="sxs-lookup"><span data-stu-id="153ad-116">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="153ad-117">Nel riquadro di sinistra hello, espandere account di archiviazione hello entro il quale si desidera contenitore di blob toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="153ad-117">In hello left pane, expand hello storage account within which you wish toocreate hello blob container.</span></span>
3. <span data-ttu-id="153ad-118">Fare doppio clic su **contenitori Blob**e - scegliere dal menu di scelta rapida hello - **crea contenitore Blob**.</span><span class="sxs-lookup"><span data-stu-id="153ad-118">Right-click **Blob Containers**, and - from hello context menu - select **Create Blob Container**.</span></span>

   ![Menu di scelta rapida Crea contenitore BLOB][0]
4. <span data-ttu-id="153ad-120">Verrà visualizzata una casella di testo di sotto di hello **contenitori Blob** cartella.</span><span class="sxs-lookup"><span data-stu-id="153ad-120">A text box will appear below hello **Blob Containers** folder.</span></span> <span data-ttu-id="153ad-121">Immettere il nome di hello per il contenitore del blob.</span><span class="sxs-lookup"><span data-stu-id="153ad-121">Enter hello name for your blob container.</span></span> <span data-ttu-id="153ad-122">Vedere hello [le regole di denominazione contenitore](storage/blobs/storage-dotnet-how-to-use-blobs.md#create-a-container) sezione per un elenco di regole e restrizioni relative alla denominazione contenitori blob.</span><span class="sxs-lookup"><span data-stu-id="153ad-122">See hello [Container naming rules](storage/blobs/storage-dotnet-how-to-use-blobs.md#create-a-container) section for a list of rules and restrictions on naming blob containers.</span></span>

   ![Casella di testo Crea contenitore BLOB][1]
5. <span data-ttu-id="153ad-124">Premere **invio** termine contenitore blob hello toocreate o **Esc** toocancel.</span><span class="sxs-lookup"><span data-stu-id="153ad-124">Press **Enter** when done toocreate hello blob container, or **Esc** toocancel.</span></span> <span data-ttu-id="153ad-125">Dopo aver creato correttamente il contenitore di blob hello, che verrà visualizzato in hello **contenitori Blob** cartella per hello selezionato di account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="153ad-125">Once hello blob container has been successfully created, it will be displayed under hello **Blob Containers** folder for hello selected storage account.</span></span>

   ![Contenitore BLOB creato][2]

## <a name="view-a-blob-containers-contents"></a><span data-ttu-id="153ad-127">Visualizzare il contenuto di un contenitore BLOB</span><span class="sxs-lookup"><span data-stu-id="153ad-127">View a blob container's contents</span></span>
<span data-ttu-id="153ad-128">I contenitori BLOB includono BLOB e cartelle, che possono anche contenere BLOB.</span><span class="sxs-lookup"><span data-stu-id="153ad-128">Blob containers contain blobs and folders (that can also contain blobs).</span></span>

<span data-ttu-id="153ad-129">Hello passaggi seguenti viene illustrato come contenuto di hello tooview di un contenitore di blob all'interno di soluzioni di archiviazione (anteprima):</span><span class="sxs-lookup"><span data-stu-id="153ad-129">hello following steps illustrate how tooview hello contents of a blob container within Storage Explorer (Preview):</span></span>

1. <span data-ttu-id="153ad-130">Aprire Storage Explorer (anteprima).</span><span class="sxs-lookup"><span data-stu-id="153ad-130">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="153ad-131">Nel riquadro di sinistra hello, espandere il contenitore di blob hello desiderato tooview account di archiviazione di hello.</span><span class="sxs-lookup"><span data-stu-id="153ad-131">In hello left pane, expand hello storage account containing hello blob container you wish tooview.</span></span>
3. <span data-ttu-id="153ad-132">Espandere l'account di archiviazione hello **contenitori Blob**.</span><span class="sxs-lookup"><span data-stu-id="153ad-132">Expand hello storage account's **Blob Containers**.</span></span>
4. <span data-ttu-id="153ad-133">Contenitore di blob hello pulsante destro del mouse si desidera tooview e - scegliere dal menu di scelta rapida hello - **Apri Editor di contenitore Blob**.</span><span class="sxs-lookup"><span data-stu-id="153ad-133">Right-click hello blob container you wish tooview, and - from hello context menu - select **Open Blob Container Editor**.</span></span>
   <span data-ttu-id="153ad-134">È anche possibile fare doppio clic sul contenitore blob hello desiderato tooview.</span><span class="sxs-lookup"><span data-stu-id="153ad-134">You can also double-click hello blob container you wish tooview.</span></span>

   ![Menu di scelta rapida Open Blob Container Editor (Apri editor contenitori BLOB)][19]
5. <span data-ttu-id="153ad-136">riquadro principale Hello verrà visualizzato il contenuto del contenitore blob hello.</span><span class="sxs-lookup"><span data-stu-id="153ad-136">hello main pane will display hello blob container's contents.</span></span>

   ![Editor contenitori BLOB][3]

## <a name="delete-a-blob-container"></a><span data-ttu-id="153ad-138">Eliminare un contenitore BLOB</span><span class="sxs-lookup"><span data-stu-id="153ad-138">Delete a blob container</span></span>
<span data-ttu-id="153ad-139">I contenitori di BLOB possono essere creati facilmente ed eliminati in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="153ad-139">Blob containers can be easily created and deleted as needed.</span></span> <span data-ttu-id="153ad-140">(toosee come blob singolo toodelete, fare riferimento a sezione toohello [gestione dei BLOB in un contenitore blob](#managing-blobs-in-a-blob-container).)</span><span class="sxs-lookup"><span data-stu-id="153ad-140">(toosee how toodelete individual blobs, refer toohello section, [Managing blobs in a blob container](#managing-blobs-in-a-blob-container).)</span></span>

<span data-ttu-id="153ad-141">Hello passaggi seguenti viene illustrato come toodelete un contenitore di blob all'interno di soluzioni di archiviazione (anteprima):</span><span class="sxs-lookup"><span data-stu-id="153ad-141">hello following steps illustrate how toodelete a blob container within Storage Explorer (Preview):</span></span>

1. <span data-ttu-id="153ad-142">Aprire Storage Explorer (anteprima).</span><span class="sxs-lookup"><span data-stu-id="153ad-142">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="153ad-143">Nel riquadro di sinistra hello, espandere il contenitore di blob hello desiderato tooview account di archiviazione di hello.</span><span class="sxs-lookup"><span data-stu-id="153ad-143">In hello left pane, expand hello storage account containing hello blob container you wish tooview.</span></span>
3. <span data-ttu-id="153ad-144">Espandere l'account di archiviazione hello **contenitori Blob**.</span><span class="sxs-lookup"><span data-stu-id="153ad-144">Expand hello storage account's **Blob Containers**.</span></span>
4. <span data-ttu-id="153ad-145">Contenitore di blob hello pulsante destro del mouse si desidera toodelete e - scegliere dal menu di scelta rapida hello - **eliminare**.</span><span class="sxs-lookup"><span data-stu-id="153ad-145">Right-click hello blob container you wish toodelete, and - from hello context menu - select **Delete**.</span></span>
   <span data-ttu-id="153ad-146">È anche possibile premere **eliminare** contenitore di toodelete hello blob attualmente selezionato.</span><span class="sxs-lookup"><span data-stu-id="153ad-146">You can also press **Delete** toodelete hello currently selected blob container.</span></span>

   ![Menu di scelta rapida Elimina per il contenitore BLOB][4]
5. <span data-ttu-id="153ad-148">Selezionare **Sì** toohello nella finestra di conferma.</span><span class="sxs-lookup"><span data-stu-id="153ad-148">Select **Yes** toohello confirmation dialog.</span></span>

   ![Menu di scelta rapida dell'eliminazione per il contenitore BLOB][5]

## <a name="copy-a-blob-container"></a><span data-ttu-id="153ad-150">Copiare un contenitore BLOB</span><span class="sxs-lookup"><span data-stu-id="153ad-150">Copy a blob container</span></span>
<span data-ttu-id="153ad-151">Esplorazione dell'archiviazione (anteprima) permette di toocopy toohello Appunti contenitore blob e quindi incollare che blob contenitore in un altro account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="153ad-151">Storage Explorer (Preview) enables you toocopy a blob container toohello clipboard, and then paste that blob container into another storage account.</span></span> <span data-ttu-id="153ad-152">(toosee come blob singolo toocopy, fare riferimento a sezione toohello [gestione dei BLOB in un contenitore blob](#managing-blobs-in-a-blob-container).)</span><span class="sxs-lookup"><span data-stu-id="153ad-152">(toosee how toocopy individual blobs, refer toohello section, [Managing blobs in a blob container](#managing-blobs-in-a-blob-container).)</span></span>

<span data-ttu-id="153ad-153">Hello alla procedura seguente viene illustrato come un contenitore di blob da un archivio toocopy account tooanother.</span><span class="sxs-lookup"><span data-stu-id="153ad-153">hello following steps illustrate how toocopy a blob container from one storage account tooanother.</span></span>

1. <span data-ttu-id="153ad-154">Aprire Storage Explorer (anteprima).</span><span class="sxs-lookup"><span data-stu-id="153ad-154">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="153ad-155">Nel riquadro di sinistra hello, espandere il contenitore di blob hello desiderato toocopy account di archiviazione di hello.</span><span class="sxs-lookup"><span data-stu-id="153ad-155">In hello left pane, expand hello storage account containing hello blob container you wish toocopy.</span></span>
3. <span data-ttu-id="153ad-156">Espandere l'account di archiviazione hello **contenitori Blob**.</span><span class="sxs-lookup"><span data-stu-id="153ad-156">Expand hello storage account's **Blob Containers**.</span></span>
4. <span data-ttu-id="153ad-157">Contenitore di blob hello pulsante destro del mouse si desidera toocopy e - scegliere dal menu di scelta rapida hello - **contenitore Blob di copia**.</span><span class="sxs-lookup"><span data-stu-id="153ad-157">Right-click hello blob container you wish toocopy, and - from hello context menu - select **Copy Blob Container**.</span></span>

   ![Menu di scelta Copy Blob Container (Copia contenitore BLOB)][6]
5. <span data-ttu-id="153ad-159">Fare doppio clic su account di archiviazione di destinazione"hello desiderato" in cui desidera toopaste hello blob contenitore e - dal menu di scelta rapida hello - selezionare **contenitore Blob Incolla**.</span><span class="sxs-lookup"><span data-stu-id="153ad-159">Right-click hello desired "target" storage account into which you want toopaste hello blob container, and - from hello context menu - select **Paste Blob Container**.</span></span>

   ![Menu di scelta rapida Paste Blob Container (Incolla contenitore BLOB)][7]

## <a name="get-hello-sas-for-a-blob-container"></a><span data-ttu-id="153ad-161">Ottenere hello firma di accesso condiviso per un contenitore blob</span><span class="sxs-lookup"><span data-stu-id="153ad-161">Get hello SAS for a blob container</span></span>
<span data-ttu-id="153ad-162">Oggetto [firma di accesso condiviso (SAS)](storage/common/storage-dotnet-shared-access-signature-part-1.md) fornisce l'accesso delegato tooresources nell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="153ad-162">A [shared access signature (SAS)](storage/common/storage-dotnet-shared-access-signature-part-1.md) provides delegated access tooresources in your storage account.</span></span>
<span data-ttu-id="153ad-163">Ciò significa che è possibile concedere a che un client limitate tooobjects autorizzazioni nell'account di archiviazione per un determinato periodo di tempo e con un set specificato di autorizzazioni, senza la necessità di condividere le chiavi di accesso di account.</span><span class="sxs-lookup"><span data-stu-id="153ad-163">This means that you can grant a client limited permissions tooobjects in your storage account for a specified period of time and with a specified set of permissions, without having to share your account access keys.</span></span>

<span data-ttu-id="153ad-164">Hello passaggi seguenti viene illustrato come toocreate una firma di accesso condiviso per un contenitore di blob:</span><span class="sxs-lookup"><span data-stu-id="153ad-164">hello following steps illustrate how toocreate a SAS for a blob container:</span></span>

1. <span data-ttu-id="153ad-165">Aprire Storage Explorer (anteprima).</span><span class="sxs-lookup"><span data-stu-id="153ad-165">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="153ad-166">Nel riquadro di sinistra hello, espandere account di archiviazione hello contenitore hello blob per i quali si desidera tooget una firma di accesso condiviso.</span><span class="sxs-lookup"><span data-stu-id="153ad-166">In hello left pane, expand hello storage account containing hello blob container for which you wish tooget a SAS.</span></span>
3. <span data-ttu-id="153ad-167">Espandere l'account di archiviazione hello **contenitori Blob**.</span><span class="sxs-lookup"><span data-stu-id="153ad-167">Expand hello storage account's **Blob Containers**.</span></span>
4. <span data-ttu-id="153ad-168">Contenitore blob desiderato hello e - scegliere dal menu di scelta rapida hello - **ottenere firma di accesso condiviso**.</span><span class="sxs-lookup"><span data-stu-id="153ad-168">Right-click hello desired blob container, and - from hello context menu - select **Get Shared Access Signature**.</span></span>

   ![Menu di scelta rapida Get Shared Access Signature (Ottieni firma di accesso condiviso)][8]
5. <span data-ttu-id="153ad-170">In hello **firma di accesso condiviso** finestra di dialogo, specificare i criteri di hello, le date di inizio e di scadenza, fuso orario e desiderato per risorse hello livelli di accesso.</span><span class="sxs-lookup"><span data-stu-id="153ad-170">In hello **Shared Access Signature** dialog, specify hello policy, start and expiration dates, time zone, and access levels you want for hello resource.</span></span>

   ![Opzioni di Get Shared Access Signature (Ottieni firma di accesso condiviso)][9]
6. <span data-ttu-id="153ad-172">Al termine della specifica di opzioni di firma di accesso condiviso hello, selezionare **crea**.</span><span class="sxs-lookup"><span data-stu-id="153ad-172">When you're finished specifying hello SAS options, select **Create**.</span></span>
7. <span data-ttu-id="153ad-173">Un secondo **firma di accesso condiviso** finestra di dialogo verrà quindi visualizzato elenchi hello contenitore blob insieme hello URL che è possibile utilizzare tooaccess QueryStrings hello risorsa di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="153ad-173">A second **Shared Access Signature** dialog will then display that lists hello blob container along with hello URL and QueryStrings you can use tooaccess hello storage resource.</span></span>
   <span data-ttu-id="153ad-174">Selezionare **copia** Avanti URL toohello desiderato toocopy toohello Appunti.</span><span class="sxs-lookup"><span data-stu-id="153ad-174">Select **Copy** next toohello URL you wish toocopy toohello clipboard.</span></span>

   ![Copiare gli URL della firma di accesso condiviso][10]
8. <span data-ttu-id="153ad-176">Al termine, scegliere **Chiudi**.</span><span class="sxs-lookup"><span data-stu-id="153ad-176">When done, select **Close**.</span></span>

## <a name="manage-access-policies-for-a-blob-container"></a><span data-ttu-id="153ad-177">Gestire i criteri di accesso per un contenitore BLOB</span><span class="sxs-lookup"><span data-stu-id="153ad-177">Manage Access Policies for a blob container</span></span>
<span data-ttu-id="153ad-178">Hello passaggi seguenti viene illustrato come toomanage (aggiungere e rimuovere) criteri di accesso per un contenitore blob:</span><span class="sxs-lookup"><span data-stu-id="153ad-178">hello following steps illustrate how toomanage (add and remove) access policies for a blob container:</span></span>

1. <span data-ttu-id="153ad-179">Aprire Storage Explorer (anteprima).</span><span class="sxs-lookup"><span data-stu-id="153ad-179">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="153ad-180">Nel riquadro di sinistra hello, espandere account di archiviazione hello contenitore hello blob i cui criteri di accesso desiderato toomanage.</span><span class="sxs-lookup"><span data-stu-id="153ad-180">In hello left pane, expand hello storage account containing hello blob container whose access policies you wish toomanage.</span></span>
3. <span data-ttu-id="153ad-181">Espandere l'account di archiviazione hello **contenitori Blob**.</span><span class="sxs-lookup"><span data-stu-id="153ad-181">Expand hello storage account's **Blob Containers**.</span></span>
4. <span data-ttu-id="153ad-182">Selezionare il contenitore di blob desiderato hello e - dal menu di scelta rapida hello - **gestire criteri di accesso**.</span><span class="sxs-lookup"><span data-stu-id="153ad-182">Select hello desired blob container, and - from hello context menu - select **Manage Access Policies**.</span></span>

   ![Menu di scelta rapida Manage Access Policies (Gestisci criteri di accesso)][11]
5. <span data-ttu-id="153ad-184">Hello **criteri di accesso** finestra di dialogo verrà elencati i criteri di accesso già creati per il contenitore di blob selezionati hello.</span><span class="sxs-lookup"><span data-stu-id="153ad-184">hello **Access Policies** dialog will list any access policies already created for hello selected blob container.</span></span>

   ![Opzioni di Criteri di accesso][12]        
6. <span data-ttu-id="153ad-186">Seguire questi passaggi a seconda delle attività di gestione criteri di accesso hello:</span><span class="sxs-lookup"><span data-stu-id="153ad-186">Follow these steps depending on hello access policy management task:</span></span>

   * <span data-ttu-id="153ad-187">**Aggiungere nuovi criteri di accesso**: selezionare **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="153ad-187">**Add a new access policy** - Select **Add**.</span></span> <span data-ttu-id="153ad-188">Una volta generate, hello **criteri di accesso** finestra di dialogo verrà visualizzato hello appena aggiunto accedere criteri (con le impostazioni predefinite).</span><span class="sxs-lookup"><span data-stu-id="153ad-188">Once generated, hello **Access Policies** dialog will display hello newly added access policy (with default settings).</span></span>
   * <span data-ttu-id="153ad-189">**Modificare i criteri di accesso**: apportare le modifiche desiderate e scegliere **Salva**.</span><span class="sxs-lookup"><span data-stu-id="153ad-189">**Edit an access policy** -  Make any desired edits, and select **Save**.</span></span>
   * <span data-ttu-id="153ad-190">**Rimuovere un criterio di accesso** : selezionare questa opzione **rimuovere** desiderato tooremove un criterio di accesso toohello successivo.</span><span class="sxs-lookup"><span data-stu-id="153ad-190">**Remove an access policy** - Select **Remove** next toohello access policy you wish tooremove.</span></span>

## <a name="set-hello-public-access-level-for-a-blob-container"></a><span data-ttu-id="153ad-191">Impostare hello a livello di accesso pubblico per un contenitore blob</span><span class="sxs-lookup"><span data-stu-id="153ad-191">Set hello Public Access Level for a blob container</span></span>
<span data-ttu-id="153ad-192">Per impostazione predefinita, ogni contenitore di blob è troppo "Nessun accesso pubblico".</span><span class="sxs-lookup"><span data-stu-id="153ad-192">By default, every blob container is set too"No public access".</span></span>

<span data-ttu-id="153ad-193">Hello passaggi seguenti viene illustrato come toospecify pubblica accedere a livello di un contenitore blob.</span><span class="sxs-lookup"><span data-stu-id="153ad-193">hello following steps illustrate how toospecify a public access level for a blob container.</span></span>

1. <span data-ttu-id="153ad-194">Aprire Storage Explorer (anteprima).</span><span class="sxs-lookup"><span data-stu-id="153ad-194">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="153ad-195">Nel riquadro di sinistra hello, espandere account di archiviazione hello contenitore hello blob i cui criteri di accesso desiderato toomanage.</span><span class="sxs-lookup"><span data-stu-id="153ad-195">In hello left pane, expand hello storage account containing hello blob container whose access policies you wish toomanage.</span></span>
3. <span data-ttu-id="153ad-196">Espandere l'account di archiviazione hello **contenitori Blob**.</span><span class="sxs-lookup"><span data-stu-id="153ad-196">Expand hello storage account's **Blob Containers**.</span></span>
4. <span data-ttu-id="153ad-197">Selezionare il contenitore di blob desiderato hello e - dal menu di scelta rapida hello - **impostare livello di accesso pubblico**.</span><span class="sxs-lookup"><span data-stu-id="153ad-197">Select hello desired blob container, and - from hello context menu - select **Set Public Access Level**.</span></span>

   ![Menu di scelta rapida Set Public Access Level (Imposta livello di accesso pubblico)][13]
5. <span data-ttu-id="153ad-199">In hello **impostare livello di accesso pubblico contenitore** finestra di dialogo, specificare il livello di accesso di hello desiderato.</span><span class="sxs-lookup"><span data-stu-id="153ad-199">In hello **Set Container Public Access Level** dialog, specify hello desired access level.</span></span>

   ![Opzioni di Set Public Access Level (Imposta livello di accesso pubblico)][14]
6. <span data-ttu-id="153ad-201">Selezionare **Applica**.</span><span class="sxs-lookup"><span data-stu-id="153ad-201">Select **Apply**.</span></span>

## <a name="managing-blobs-in-a-blob-container"></a><span data-ttu-id="153ad-202">Gestione dei BLOB in un contenitore BLOB</span><span class="sxs-lookup"><span data-stu-id="153ad-202">Managing blobs in a blob container</span></span>
<span data-ttu-id="153ad-203">Dopo aver creato un contenitore blob, è possibile caricare un contenitore di blob toothat blob, scaricare un computer locale tooyour di blob, aprire un blob nel computer locale e molto altro ancora.</span><span class="sxs-lookup"><span data-stu-id="153ad-203">Once you've created a blob container, you can upload a blob toothat blob container, download a blob tooyour local computer, open a blob on your local computer, and much more.</span></span>

<span data-ttu-id="153ad-204">Hello alla procedura seguente viene illustrato come toomanage hello BLOB (e cartelle) all'interno di un contenitore blob.</span><span class="sxs-lookup"><span data-stu-id="153ad-204">hello following steps illustrate how toomanage hello blobs (and folders) within a blob container.</span></span>

1. <span data-ttu-id="153ad-205">Aprire Storage Explorer (anteprima).</span><span class="sxs-lookup"><span data-stu-id="153ad-205">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="153ad-206">Nel riquadro di sinistra hello, espandere il contenitore di blob hello desiderato toomanage account di archiviazione di hello.</span><span class="sxs-lookup"><span data-stu-id="153ad-206">In hello left pane, expand hello storage account containing hello blob container you wish toomanage.</span></span>
3. <span data-ttu-id="153ad-207">Espandere l'account di archiviazione hello **contenitori Blob**.</span><span class="sxs-lookup"><span data-stu-id="153ad-207">Expand hello storage account's **Blob Containers**.</span></span>
4. <span data-ttu-id="153ad-208">Fare doppio clic sul contenitore di blob hello desiderato tooview.</span><span class="sxs-lookup"><span data-stu-id="153ad-208">Double-click hello blob container you wish tooview.</span></span>
5. <span data-ttu-id="153ad-209">riquadro principale Hello verrà visualizzato il contenuto del contenitore blob hello.</span><span class="sxs-lookup"><span data-stu-id="153ad-209">hello main pane will display hello blob container's contents.</span></span>

   ![Visualizzazione del contenitore BLOB][3]
6. <span data-ttu-id="153ad-211">riquadro principale Hello verrà visualizzato il contenuto del contenitore blob hello.</span><span class="sxs-lookup"><span data-stu-id="153ad-211">hello main pane will display hello blob container's contents.</span></span>
7. <span data-ttu-id="153ad-212">Seguire questi che passaggi a seconda attività hello desiderato tooperform:</span><span class="sxs-lookup"><span data-stu-id="153ad-212">Follow these steps depending on hello task you wish tooperform:</span></span>

   * <span data-ttu-id="153ad-213">**Caricare contenitore blob tooa di file**</span><span class="sxs-lookup"><span data-stu-id="153ad-213">**Upload files tooa blob container**</span></span>

     1. <span data-ttu-id="153ad-214">Sulla barra degli strumenti del riquadro principale hello, selezionare **caricare**e quindi **Carica file** dal menu a discesa hello.</span><span class="sxs-lookup"><span data-stu-id="153ad-214">On hello main pane's toolbar, select **Upload**, and then **Upload Files** from hello drop-down menu.</span></span>

        ![Menu Carica i file][15]
     2. <span data-ttu-id="153ad-216">In hello **caricare file** finestra di dialogo, i puntini di sospensione selezionare hello (**...** ) pulsante a destra hello hello **file** file hello tooselect desiderato tooupload casella di testo.</span><span class="sxs-lookup"><span data-stu-id="153ad-216">In hello **Upload files** dialog, select hello ellipsis (**…**) button on hello right side of hello **Files** text box tooselect hello file(s) you wish tooupload.</span></span>

        ![Opzioni di Carica i file][16]
     3. <span data-ttu-id="153ad-218">Specificare il tipo di hello di **Blob tipo**.</span><span class="sxs-lookup"><span data-stu-id="153ad-218">Specify hello type of **Blob type**.</span></span> <span data-ttu-id="153ad-219">articolo Hello [Introduzione all'archiviazione Blob di Azure usando .NET](storage/blobs/storage-dotnet-how-to-use-blobs.md#blob-service-concepts) vengono illustrate le differenze di hello tra hello vari tipi di blob.</span><span class="sxs-lookup"><span data-stu-id="153ad-219">hello article [Get started with Azure Blob storage using .NET](storage/blobs/storage-dotnet-how-to-use-blobs.md#blob-service-concepts) explains hello differences between hello various blob types.</span></span>
     4. <span data-ttu-id="153ad-220">Facoltativamente, specificare una cartella di destinazione in cui verranno caricati i file selezionati hello.</span><span class="sxs-lookup"><span data-stu-id="153ad-220">Optionally, specify a target folder into which hello selected file(s) will be uploaded.</span></span> <span data-ttu-id="153ad-221">Se la cartella di destinazione hello non esiste, verrà creato.</span><span class="sxs-lookup"><span data-stu-id="153ad-221">If hello target folder doesn’t exist, it will be created.</span></span>
     5. <span data-ttu-id="153ad-222">Selezionare **Carica**.</span><span class="sxs-lookup"><span data-stu-id="153ad-222">Select **Upload**.</span></span>
   * <span data-ttu-id="153ad-223">**Caricare un contenitore di blob tooa cartella**</span><span class="sxs-lookup"><span data-stu-id="153ad-223">**Upload a folder tooa blob container**</span></span>

     1. <span data-ttu-id="153ad-224">Sulla barra degli strumenti del riquadro principale hello, selezionare **caricare**e quindi **cartella caricare** dal menu a discesa hello.</span><span class="sxs-lookup"><span data-stu-id="153ad-224">On hello main pane's toolbar, select **Upload**, and then **Upload Folder** from hello drop-down menu.</span></span>

        ![Menu di Upload Folder (Carica cartella)][17]
     2. <span data-ttu-id="153ad-226">In hello **cartella caricamento** finestra di dialogo, i puntini di sospensione selezionare hello (**...** ) pulsante a destra hello hello **cartella** cartella hello di tooselect casella testo cui si desidera tooupload il contenuto.</span><span class="sxs-lookup"><span data-stu-id="153ad-226">In hello **Upload folder** dialog, select hello ellipsis (**…**) button on hello right side of hello **Folder** text box tooselect hello folder whose contents you wish tooupload.</span></span>

        ![Opzioni di Upload Folder (Carica cartella)][18]
     3. <span data-ttu-id="153ad-228">Specificare il tipo di hello di **Blob tipo**.</span><span class="sxs-lookup"><span data-stu-id="153ad-228">Specify hello type of **Blob type**.</span></span> <span data-ttu-id="153ad-229">articolo Hello [Introduzione all'archiviazione Blob di Azure usando .NET](storage/blobs/storage-dotnet-how-to-use-blobs.md#blob-service-concepts) vengono illustrate le differenze di hello tra hello vari tipi di blob.</span><span class="sxs-lookup"><span data-stu-id="153ad-229">hello article [Get started with Azure Blob storage using .NET](storage/blobs/storage-dotnet-how-to-use-blobs.md#blob-service-concepts) explains hello differences between hello various blob types.</span></span>
     4. <span data-ttu-id="153ad-230">Facoltativamente, specificare una cartella di destinazione in cui hello verrà caricato il contenuto della cartella selezionata.</span><span class="sxs-lookup"><span data-stu-id="153ad-230">Optionally, specify a target folder into which hello selected folder's contents will be uploaded.</span></span> <span data-ttu-id="153ad-231">Se la cartella di destinazione hello non esiste, verrà creato.</span><span class="sxs-lookup"><span data-stu-id="153ad-231">If hello target folder doesn’t exist, it will be created.</span></span>
     5. <span data-ttu-id="153ad-232">Selezionare **Carica**.</span><span class="sxs-lookup"><span data-stu-id="153ad-232">Select **Upload**.</span></span>
   * <span data-ttu-id="153ad-233">**Scaricare un computer locale tooyour di blob**</span><span class="sxs-lookup"><span data-stu-id="153ad-233">**Download a blob tooyour local computer**</span></span>

     1. <span data-ttu-id="153ad-234">Selezionare i blob hello desiderato toodownload.</span><span class="sxs-lookup"><span data-stu-id="153ad-234">Select hello blob you wish toodownload.</span></span>
     2. <span data-ttu-id="153ad-235">Sulla barra degli strumenti del riquadro principale hello, selezionare **scaricare**.</span><span class="sxs-lookup"><span data-stu-id="153ad-235">On hello main pane's toolbar, select **Download**.</span></span>
     3. <span data-ttu-id="153ad-236">In hello **specificare dove toosave hello scaricato blob** finestra di dialogo, specificare il percorso di hello in cui si desidera blob hello scaricato e hello nome desiderato toogive è.</span><span class="sxs-lookup"><span data-stu-id="153ad-236">In hello **Specify where toosave hello downloaded blob** dialog, specify hello location where you want hello blob downloaded, and hello name you wish toogive it.</span></span>  
     4. <span data-ttu-id="153ad-237">Selezionare **Salva**.</span><span class="sxs-lookup"><span data-stu-id="153ad-237">Select **Save**.</span></span>
   * <span data-ttu-id="153ad-238">**Aprire un BLOB nel computer locale**</span><span class="sxs-lookup"><span data-stu-id="153ad-238">**Open a blob on your local computer**</span></span>

     1. <span data-ttu-id="153ad-239">Selezionare i blob hello desiderato tooopen.</span><span class="sxs-lookup"><span data-stu-id="153ad-239">Select hello blob you wish tooopen.</span></span>
     2. <span data-ttu-id="153ad-240">Sulla barra degli strumenti del riquadro principale hello, selezionare **aprire**.</span><span class="sxs-lookup"><span data-stu-id="153ad-240">On hello main pane's toolbar, select **Open**.</span></span>
     3. <span data-ttu-id="153ad-241">blob Hello verrà scaricato e aperto con l'applicazione hello associata al tipo di file sottostante del blob hello.</span><span class="sxs-lookup"><span data-stu-id="153ad-241">hello blob will be downloaded and opened using hello application associated with hello blob's underlying file type.</span></span>
   * <span data-ttu-id="153ad-242">**Copiare negli Appunti toohello un blob**</span><span class="sxs-lookup"><span data-stu-id="153ad-242">**Copy a blob toohello clipboard**</span></span>

     1. <span data-ttu-id="153ad-243">Selezionare i blob hello desiderato toocopy.</span><span class="sxs-lookup"><span data-stu-id="153ad-243">Select hello blob you wish toocopy.</span></span>
     2. <span data-ttu-id="153ad-244">Sulla barra degli strumenti del riquadro principale hello, selezionare **copia**.</span><span class="sxs-lookup"><span data-stu-id="153ad-244">On hello main pane's toolbar, select **Copy**.</span></span>
     3. <span data-ttu-id="153ad-245">Nel riquadro di sinistra hello, passare il contenitore di blob tooanother e fare doppio clic tooview nel riquadro principale hello.</span><span class="sxs-lookup"><span data-stu-id="153ad-245">In hello left pane, navigate tooanother blob container, and double-click it tooview it in hello main pane.</span></span>
     4. <span data-ttu-id="153ad-246">Sulla barra degli strumenti del riquadro principale hello, selezionare **Incolla** toocreate una copia di blob hello.</span><span class="sxs-lookup"><span data-stu-id="153ad-246">On hello main pane's toolbar, select **Paste** toocreate a copy of hello blob.</span></span>
   * <span data-ttu-id="153ad-247">**Eliminare un BLOB**</span><span class="sxs-lookup"><span data-stu-id="153ad-247">**Delete a blob**</span></span>

     1. <span data-ttu-id="153ad-248">Selezionare i blob hello desiderato toodelete.</span><span class="sxs-lookup"><span data-stu-id="153ad-248">Select hello blob you wish toodelete.</span></span>
     2. <span data-ttu-id="153ad-249">Sulla barra degli strumenti del riquadro principale hello, selezionare **eliminare**.</span><span class="sxs-lookup"><span data-stu-id="153ad-249">On hello main pane's toolbar, select **Delete**.</span></span>
     3. <span data-ttu-id="153ad-250">Selezionare **Sì** toohello nella finestra di conferma.</span><span class="sxs-lookup"><span data-stu-id="153ad-250">Select **Yes** toohello confirmation dialog.</span></span>

## <a name="next-steps"></a><span data-ttu-id="153ad-251">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="153ad-251">Next steps</span></span>
* <span data-ttu-id="153ad-252">Hello vista [note sulla versione di esplorazione dell'archiviazione (anteprima) e video più recenti](http://www.storageexplorer.com).</span><span class="sxs-lookup"><span data-stu-id="153ad-252">View hello [latest Storage Explorer (Preview) release notes and videos](http://www.storageexplorer.com).</span></span>
* <span data-ttu-id="153ad-253">Informazioni su come troppo[creare applicazioni usando BLOB di Azure, tabelle, code e i file](https://azure.microsoft.com/documentation/services/storage/).</span><span class="sxs-lookup"><span data-stu-id="153ad-253">Learn how too[create applications using Azure blobs, tables, queues, and files](https://azure.microsoft.com/documentation/services/storage/).</span></span>

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
