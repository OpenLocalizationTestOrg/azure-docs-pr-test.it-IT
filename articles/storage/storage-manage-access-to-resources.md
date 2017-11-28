---
title: accesso in lettura pubblico aaaEnable per contenitori e BLOB nell'archiviazione Blob di Azure | Documenti Microsoft
description: Informazioni su come toomake contenitori e BLOB disponibili per l'accesso anonimo e come tooaccess li a livello di codice.
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: a2cffee6-3224-4f2a-8183-66ca23b2d2d7
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: marsma
ms.openlocfilehash: 0675b5dc4d32a3a0a34376ae4c049542b07ba03a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-anonymous-read-access-toocontainers-and-blobs"></a><span data-ttu-id="b0570-103">Gestire BLOB e accesso in lettura anonimo toocontainers</span><span class="sxs-lookup"><span data-stu-id="b0570-103">Manage anonymous read access toocontainers and blobs</span></span>
<span data-ttu-id="b0570-104">È possibile abilitare l'accesso in lettura anonimo, pubblica tooa contenitore e i relativi BLOB nell'archiviazione Blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="b0570-104">You can enable anonymous, public read access tooa container and its blobs in Azure Blob storage.</span></span> <span data-ttu-id="b0570-105">In questo modo, è possibile concedere l'accesso di sola lettura alle risorse di toothese senza condividere la chiave dell'account e senza una firma di accesso condiviso (SAS).</span><span class="sxs-lookup"><span data-stu-id="b0570-105">By doing so, you can grant read-only access toothese resources without sharing your account key, and without requiring a shared access signature (SAS).</span></span>

<span data-ttu-id="b0570-106">Accesso in lettura pubblico è ideale per scenari in cui si desidera determinati tooalways BLOB sia disponibile per l'accesso in lettura anonimo.</span><span class="sxs-lookup"><span data-stu-id="b0570-106">Public read access is best for scenarios where you want certain blobs tooalways be available for anonymous read access.</span></span> <span data-ttu-id="b0570-107">Per un controllo più accurato, è possibile creare una firma di accesso condiviso.</span><span class="sxs-lookup"><span data-stu-id="b0570-107">For more fine-grained control, you can create a shared access signature.</span></span> <span data-ttu-id="b0570-108">Firme di accesso condiviso consentono di tooprovide limitato l'accesso con autorizzazioni diverse, per un periodo di tempo specifico.</span><span class="sxs-lookup"><span data-stu-id="b0570-108">Shared access signatures enable you tooprovide restricted access using different permissions, for a specific time period.</span></span> <span data-ttu-id="b0570-109">Per altre informazioni sulla creazione di firme di accesso condiviso, vedere [Uso delle firme di accesso condiviso](storage-dotnet-shared-access-signature-part-1.md).</span><span class="sxs-lookup"><span data-stu-id="b0570-109">For more information about creating shared access signatures, see [Using shared access signatures (SAS) in Azure Storage](storage-dotnet-shared-access-signature-part-1.md).</span></span>

## <a name="grant-anonymous-users-permissions-toocontainers-and-blobs"></a><span data-ttu-id="b0570-110">Concedere agli utenti anonimi le autorizzazioni toocontainers e BLOB</span><span class="sxs-lookup"><span data-stu-id="b0570-110">Grant anonymous users permissions toocontainers and blobs</span></span>
<span data-ttu-id="b0570-111">Per impostazione predefinita, un contenitore e tutti i BLOB in esso contenuti sono accessibili solo dal proprietario hello hello dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="b0570-111">By default, a container and any blobs within it may be accessed only by hello owner of hello storage account.</span></span> <span data-ttu-id="b0570-112">toogive utenti anonimi le autorizzazioni di lettura tooa contenitore e nei relativi BLOB, è possibile impostare autorizzazioni contenitore di hello tooallow accesso pubblico.</span><span class="sxs-lookup"><span data-stu-id="b0570-112">toogive anonymous users read permissions tooa container and its blobs, you can set hello container permissions tooallow public access.</span></span> <span data-ttu-id="b0570-113">Gli utenti anonimi possono leggere i BLOB in un contenitore accessibile pubblicamente senza effettuare l'autenticazione richiesta hello.</span><span class="sxs-lookup"><span data-stu-id="b0570-113">Anonymous users can read blobs within a publicly accessible container without authenticating hello request.</span></span>

<span data-ttu-id="b0570-114">È possibile configurare un contenitore con queste autorizzazioni hello:</span><span class="sxs-lookup"><span data-stu-id="b0570-114">You can configure a container with hello following permissions:</span></span>

* <span data-ttu-id="b0570-115">**Accesso in lettura non pubblico:** contenitore hello e nei relativi BLOB sono accessibili solo dal proprietario dell'account di archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="b0570-115">**No public read access:** hello container and its blobs can be accessed only by hello storage account owner.</span></span> <span data-ttu-id="b0570-116">Si tratta hello predefinita per tutti i contenitori di nuovo.</span><span class="sxs-lookup"><span data-stu-id="b0570-116">This is hello default for all new containers.</span></span>
* <span data-ttu-id="b0570-117">**Solo per i BLOB l'accesso in lettura pubblico:** BLOB nel contenitore hello può essere letto da una richiesta anonima, ma i dati del contenitore non sono disponibili.</span><span class="sxs-lookup"><span data-stu-id="b0570-117">**Public read access for blobs only:** Blobs within hello container can be read by anonymous request, but container data is not available.</span></span> <span data-ttu-id="b0570-118">I client anonimi non è possibile enumerare i BLOB di hello all'interno del contenitore di hello.</span><span class="sxs-lookup"><span data-stu-id="b0570-118">Anonymous clients cannot enumerate hello blobs within hello container.</span></span>
* <span data-ttu-id="b0570-119">**Accesso in lettura pubblico completo:** i dati del BLOB e del contenitore possono essere letti tramite richiesta anonima.</span><span class="sxs-lookup"><span data-stu-id="b0570-119">**Full public read access:** All container and blob data can be read by anonymous request.</span></span> <span data-ttu-id="b0570-120">I client possono enumerare i BLOB all'interno del contenitore hello da una richiesta anonima, ma non è possibile enumerare i contenitori nell'account di archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="b0570-120">Clients can enumerate blobs within hello container by anonymous request, but cannot enumerate containers within hello storage account.</span></span>

<span data-ttu-id="b0570-121">È possibile utilizzare queste autorizzazioni contenitore tooset hello:</span><span class="sxs-lookup"><span data-stu-id="b0570-121">You can use hello following tooset container permissions:</span></span>

* [<span data-ttu-id="b0570-122">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="b0570-122">Azure portal</span></span>](https://portal.azure.com)
* [<span data-ttu-id="b0570-123">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="b0570-123">Azure PowerShell</span></span>](storage-powershell-guide-full.md#how-to-manage-azure-blobs)
* [<span data-ttu-id="b0570-124">Interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="b0570-124">Azure CLI 2.0</span></span>](storage-azure-cli.md#create-and-manage-blobs)
* <span data-ttu-id="b0570-125">A livello di programmazione, utilizzando una delle librerie client di archiviazione hello o hello API REST</span><span class="sxs-lookup"><span data-stu-id="b0570-125">Programmatically, by using one of hello storage client libraries or hello REST API</span></span>

### <a name="set-container-permissions-in-hello-azure-portal"></a><span data-ttu-id="b0570-126">Impostare le autorizzazioni del contenitore in hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="b0570-126">Set container permissions in hello Azure portal</span></span>
<span data-ttu-id="b0570-127">autorizzazioni del contenitore tooset in hello [portale di Azure](https://portal.azure.com), seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="b0570-127">tooset container permissions in hello [Azure portal](https://portal.azure.com), follow these steps:</span></span>

1. <span data-ttu-id="b0570-128">Aprire il **account di archiviazione** pannello nel portale di hello.</span><span class="sxs-lookup"><span data-stu-id="b0570-128">Open your **Storage account** blade in hello portal.</span></span> <span data-ttu-id="b0570-129">È possibile trovare l'account di archiviazione selezionando **gli account di archiviazione** nel Pannello di hello menu principale del portale.</span><span class="sxs-lookup"><span data-stu-id="b0570-129">You can find your storage account by selecting **Storage accounts** in hello main portal menu blade.</span></span>
1. <span data-ttu-id="b0570-130">In **servizio BLOB** nel Pannello di hello menu, selezionare **contenitori**.</span><span class="sxs-lookup"><span data-stu-id="b0570-130">Under **BLOB SERVICE** on hello menu blade, select **Containers**.</span></span>
1. <span data-ttu-id="b0570-131">Fare clic su una riga di hello contenitore o del contenitore di hello selezionare i puntini di sospensione tooopen hello **menu di scelta rapida**.</span><span class="sxs-lookup"><span data-stu-id="b0570-131">Right-click on hello container row or select hello ellipsis tooopen hello container's **Context menu**.</span></span>
1. <span data-ttu-id="b0570-132">Selezionare **criterio di accesso** nel menu di scelta rapida hello.</span><span class="sxs-lookup"><span data-stu-id="b0570-132">Select **Access policy** in hello context menu.</span></span>
1. <span data-ttu-id="b0570-133">Selezionare un **tipo di accesso** da hello menu a discesa.</span><span class="sxs-lookup"><span data-stu-id="b0570-133">Select an **Access type** from hello drop down menu.</span></span>

    ![Finestra di dialogo Modifica metadati contenitore](./media/storage-manage-access-to-resources/storage-manage-access-to-resources-0.png)

### <a name="set-container-permissions-with-net"></a><span data-ttu-id="b0570-135">Impostare le autorizzazioni per il contenitore con .NET</span><span class="sxs-lookup"><span data-stu-id="b0570-135">Set container permissions with .NET</span></span>
<span data-ttu-id="b0570-136">tooset le autorizzazioni per un contenitore usando c# e hello libreria Client di archiviazione per .NET, recuperare innanzitutto le autorizzazioni esistenti del contenitore hello dal chiamante hello **GetPermissions** metodo.</span><span class="sxs-lookup"><span data-stu-id="b0570-136">tooset permissions for a container using C# and hello Storage Client Library for .NET, first retrieve hello container's existing permissions by calling hello **GetPermissions** method.</span></span> <span data-ttu-id="b0570-137">Quindi set hello **PublicAccess** proprietà hello **BlobContainerPermissions** oggetto restituito da hello **GetPermissions** metodo.</span><span class="sxs-lookup"><span data-stu-id="b0570-137">Then set hello **PublicAccess** property for hello **BlobContainerPermissions** object that is returned by hello **GetPermissions** method.</span></span> <span data-ttu-id="b0570-138">Chiamare infine hello **SetPermissions** metodo con hello aggiornate le autorizzazioni.</span><span class="sxs-lookup"><span data-stu-id="b0570-138">Finally, call hello **SetPermissions** method with hello updated permissions.</span></span>

<span data-ttu-id="b0570-139">Hello di esempio seguente imposta le autorizzazioni del contenitore hello toofull accesso in lettura pubblico.</span><span class="sxs-lookup"><span data-stu-id="b0570-139">hello following example sets hello container's permissions toofull public read access.</span></span> <span data-ttu-id="b0570-140">tooset toopublic di autorizzazioni di accesso in lettura per BLOB, impostare hello **PublicAccess** proprietà troppo**BlobContainerPublicAccessType.Blob**.</span><span class="sxs-lookup"><span data-stu-id="b0570-140">tooset permissions toopublic read access for blobs only, set hello **PublicAccess** property too**BlobContainerPublicAccessType.Blob**.</span></span> <span data-ttu-id="b0570-141">impostare tutte le autorizzazioni per gli utenti anonimi, tooremove hello proprietà troppo**BlobContainerPublicAccessType.Off**.</span><span class="sxs-lookup"><span data-stu-id="b0570-141">tooremove all permissions for anonymous users, set hello property too**BlobContainerPublicAccessType.Off**.</span></span>

```csharp
public static void SetPublicContainerPermissions(CloudBlobContainer container)
{
    BlobContainerPermissions permissions = container.GetPermissions();
    permissions.PublicAccess = BlobContainerPublicAccessType.Container;
    container.SetPermissions(permissions);
}
```

## <a name="access-containers-and-blobs-anonymously"></a><span data-ttu-id="b0570-142">Accesso anonimo a contenitori e BLOB</span><span class="sxs-lookup"><span data-stu-id="b0570-142">Access containers and blobs anonymously</span></span>
<span data-ttu-id="b0570-143">Un client che accede a contenitori e BLOB in modo anonimo può usare costruttori che non richiedono credenziali.</span><span class="sxs-lookup"><span data-stu-id="b0570-143">A client that accesses containers and blobs anonymously can use constructors that do not require credentials.</span></span> <span data-ttu-id="b0570-144">Hello seguono esempi mostra alcuni modi tooreference risorse del servizio Blob in modo anonimo.</span><span class="sxs-lookup"><span data-stu-id="b0570-144">hello following examples show a few different ways tooreference Blob service resources anonymously.</span></span>

### <a name="create-an-anonymous-client-object"></a><span data-ttu-id="b0570-145">Creare un oggetto client anonimo</span><span class="sxs-lookup"><span data-stu-id="b0570-145">Create an anonymous client object</span></span>
<span data-ttu-id="b0570-146">È possibile creare un nuovo oggetto client di servizio per l'accesso anonimo, fornendo l'endpoint del servizio Blob hello per conto di hello.</span><span class="sxs-lookup"><span data-stu-id="b0570-146">You can create a new service client object for anonymous access by providing hello Blob service endpoint for hello account.</span></span> <span data-ttu-id="b0570-147">Tuttavia, è inoltre necessario conoscere il nome di hello di un contenitore in tale account che è disponibile per l'accesso anonimo.</span><span class="sxs-lookup"><span data-stu-id="b0570-147">However, you must also know hello name of a container in that account that's available for anonymous access.</span></span>

```csharp
public static void CreateAnonymousBlobClient()
{
    // Create hello client object using hello Blob service endpoint.
    CloudBlobClient blobClient = new CloudBlobClient(new Uri(@"https://storagesample.blob.core.windows.net"));

    // Get a reference tooa container that's available for anonymous access.
    CloudBlobContainer container = blobClient.GetContainerReference("sample-container");

    // Read hello container's properties. Note this is only possible when hello container supports full public read access.
    container.FetchAttributes();
    Console.WriteLine(container.Properties.LastModified);
    Console.WriteLine(container.Properties.ETag);
}
```

### <a name="reference-a-container-anonymously"></a><span data-ttu-id="b0570-148">Fare riferimento a un contenitore in modo anonimo</span><span class="sxs-lookup"><span data-stu-id="b0570-148">Reference a container anonymously</span></span>
<span data-ttu-id="b0570-149">Se si dispone di hello URL tooa contenitore che è disponibile in modo anonimo, è possibile utilizzare il contenitore di hello tooreference direttamente.</span><span class="sxs-lookup"><span data-stu-id="b0570-149">If you have hello URL tooa container that is anonymously available, you can use it tooreference hello container directly.</span></span>

```csharp
public static void ListBlobsAnonymously()
{
    // Get a reference tooa container that's available for anonymous access.
    CloudBlobContainer container = new CloudBlobContainer(new Uri(@"https://storagesample.blob.core.windows.net/sample-container"));

    // List blobs in hello container.
    foreach (IListBlobItem blobItem in container.ListBlobs())
    {
        Console.WriteLine(blobItem.Uri);
    }
}
```

### <a name="reference-a-blob-anonymously"></a><span data-ttu-id="b0570-150">Fare riferimento a un BLOB in modo anonimo</span><span class="sxs-lookup"><span data-stu-id="b0570-150">Reference a blob anonymously</span></span>
<span data-ttu-id="b0570-151">Se si dispone di hello URL tooa blob disponibili per l'accesso anonimo, è possibile fare riferimento blob hello direttamente tramite URL:</span><span class="sxs-lookup"><span data-stu-id="b0570-151">If you have hello URL tooa blob that is available for anonymous access, you can reference hello blob directly using that URL:</span></span>

```csharp
public static void DownloadBlobAnonymously()
{
    CloudBlockBlob blob = new CloudBlockBlob(new Uri(@"https://storagesample.blob.core.windows.net/sample-container/logfile.txt"));
    blob.DownloadToFile(@"C:\Temp\logfile.txt", System.IO.FileMode.Create);
}
```

## <a name="features-available-tooanonymous-users"></a><span data-ttu-id="b0570-152">Utenti tooanonymous disponibili funzionalità</span><span class="sxs-lookup"><span data-stu-id="b0570-152">Features available tooanonymous users</span></span>
<span data-ttu-id="b0570-153">Hello nella tabella seguente mostra le operazioni che possono essere chiamate dagli utenti anonimi quando ACL di un contenitore è impostato l'accesso pubblico tooallow.</span><span class="sxs-lookup"><span data-stu-id="b0570-153">hello following table shows which operations may be called by anonymous users when a container's ACL is set tooallow public access.</span></span>

| <span data-ttu-id="b0570-154">Operazione REST</span><span class="sxs-lookup"><span data-stu-id="b0570-154">REST Operation</span></span> | <span data-ttu-id="b0570-155">Autorizzazione con accesso in lettura pubblico completo</span><span class="sxs-lookup"><span data-stu-id="b0570-155">Permission with full public read access</span></span> | <span data-ttu-id="b0570-156">Autorizzazione con accesso in lettura pubblico solo per BLOB</span><span class="sxs-lookup"><span data-stu-id="b0570-156">Permission with public read access for blobs only</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b0570-157">List Containers</span><span class="sxs-lookup"><span data-stu-id="b0570-157">List Containers</span></span> |<span data-ttu-id="b0570-158">Solo proprietario</span><span class="sxs-lookup"><span data-stu-id="b0570-158">Owner only</span></span> |<span data-ttu-id="b0570-159">Solo proprietario</span><span class="sxs-lookup"><span data-stu-id="b0570-159">Owner only</span></span> |
| <span data-ttu-id="b0570-160">Create Container</span><span class="sxs-lookup"><span data-stu-id="b0570-160">Create Container</span></span> |<span data-ttu-id="b0570-161">Solo proprietario</span><span class="sxs-lookup"><span data-stu-id="b0570-161">Owner only</span></span> |<span data-ttu-id="b0570-162">Solo proprietario</span><span class="sxs-lookup"><span data-stu-id="b0570-162">Owner only</span></span> |
| <span data-ttu-id="b0570-163">Get Container Properties</span><span class="sxs-lookup"><span data-stu-id="b0570-163">Get Container Properties</span></span> |<span data-ttu-id="b0570-164">Tutti</span><span class="sxs-lookup"><span data-stu-id="b0570-164">All</span></span> |<span data-ttu-id="b0570-165">Solo proprietario</span><span class="sxs-lookup"><span data-stu-id="b0570-165">Owner only</span></span> |
| <span data-ttu-id="b0570-166">Get Container Metadata</span><span class="sxs-lookup"><span data-stu-id="b0570-166">Get Container Metadata</span></span> |<span data-ttu-id="b0570-167">Tutti</span><span class="sxs-lookup"><span data-stu-id="b0570-167">All</span></span> |<span data-ttu-id="b0570-168">Solo proprietario</span><span class="sxs-lookup"><span data-stu-id="b0570-168">Owner only</span></span> |
| <span data-ttu-id="b0570-169">Set Container Metadata</span><span class="sxs-lookup"><span data-stu-id="b0570-169">Set Container Metadata</span></span> |<span data-ttu-id="b0570-170">Solo proprietario</span><span class="sxs-lookup"><span data-stu-id="b0570-170">Owner only</span></span> |<span data-ttu-id="b0570-171">Solo proprietario</span><span class="sxs-lookup"><span data-stu-id="b0570-171">Owner only</span></span> |
| <span data-ttu-id="b0570-172">Get Container ACL</span><span class="sxs-lookup"><span data-stu-id="b0570-172">Get Container ACL</span></span> |<span data-ttu-id="b0570-173">Solo proprietario</span><span class="sxs-lookup"><span data-stu-id="b0570-173">Owner only</span></span> |<span data-ttu-id="b0570-174">Solo proprietario</span><span class="sxs-lookup"><span data-stu-id="b0570-174">Owner only</span></span> |
| <span data-ttu-id="b0570-175">Set Container ACL</span><span class="sxs-lookup"><span data-stu-id="b0570-175">Set Container ACL</span></span> |<span data-ttu-id="b0570-176">Solo proprietario</span><span class="sxs-lookup"><span data-stu-id="b0570-176">Owner only</span></span> |<span data-ttu-id="b0570-177">Solo proprietario</span><span class="sxs-lookup"><span data-stu-id="b0570-177">Owner only</span></span> |
| <span data-ttu-id="b0570-178">Delete Container</span><span class="sxs-lookup"><span data-stu-id="b0570-178">Delete Container</span></span> |<span data-ttu-id="b0570-179">Solo proprietario</span><span class="sxs-lookup"><span data-stu-id="b0570-179">Owner only</span></span> |<span data-ttu-id="b0570-180">Solo proprietario</span><span class="sxs-lookup"><span data-stu-id="b0570-180">Owner only</span></span> |
| <span data-ttu-id="b0570-181">List Blobs</span><span class="sxs-lookup"><span data-stu-id="b0570-181">List Blobs</span></span> |<span data-ttu-id="b0570-182">Tutti</span><span class="sxs-lookup"><span data-stu-id="b0570-182">All</span></span> |<span data-ttu-id="b0570-183">Solo proprietario</span><span class="sxs-lookup"><span data-stu-id="b0570-183">Owner only</span></span> |
| <span data-ttu-id="b0570-184">Put Blob</span><span class="sxs-lookup"><span data-stu-id="b0570-184">Put Blob</span></span> |<span data-ttu-id="b0570-185">Solo proprietario</span><span class="sxs-lookup"><span data-stu-id="b0570-185">Owner only</span></span> |<span data-ttu-id="b0570-186">Solo proprietario</span><span class="sxs-lookup"><span data-stu-id="b0570-186">Owner only</span></span> |
| <span data-ttu-id="b0570-187">Get Blob</span><span class="sxs-lookup"><span data-stu-id="b0570-187">Get Blob</span></span> |<span data-ttu-id="b0570-188">Tutti</span><span class="sxs-lookup"><span data-stu-id="b0570-188">All</span></span> |<span data-ttu-id="b0570-189">Tutti</span><span class="sxs-lookup"><span data-stu-id="b0570-189">All</span></span> |
| <span data-ttu-id="b0570-190">Get Blob Properties</span><span class="sxs-lookup"><span data-stu-id="b0570-190">Get Blob Properties</span></span> |<span data-ttu-id="b0570-191">Tutti</span><span class="sxs-lookup"><span data-stu-id="b0570-191">All</span></span> |<span data-ttu-id="b0570-192">Tutti</span><span class="sxs-lookup"><span data-stu-id="b0570-192">All</span></span> |
| <span data-ttu-id="b0570-193">Set Blob Properties</span><span class="sxs-lookup"><span data-stu-id="b0570-193">Set Blob Properties</span></span> |<span data-ttu-id="b0570-194">Solo proprietario</span><span class="sxs-lookup"><span data-stu-id="b0570-194">Owner only</span></span> |<span data-ttu-id="b0570-195">Solo proprietario</span><span class="sxs-lookup"><span data-stu-id="b0570-195">Owner only</span></span> |
| <span data-ttu-id="b0570-196">Get Blob Metadata</span><span class="sxs-lookup"><span data-stu-id="b0570-196">Get Blob Metadata</span></span> |<span data-ttu-id="b0570-197">Tutti</span><span class="sxs-lookup"><span data-stu-id="b0570-197">All</span></span> |<span data-ttu-id="b0570-198">Tutti</span><span class="sxs-lookup"><span data-stu-id="b0570-198">All</span></span> |
| <span data-ttu-id="b0570-199">Set Blob Metadata</span><span class="sxs-lookup"><span data-stu-id="b0570-199">Set Blob Metadata</span></span> |<span data-ttu-id="b0570-200">Solo proprietario</span><span class="sxs-lookup"><span data-stu-id="b0570-200">Owner only</span></span> |<span data-ttu-id="b0570-201">Solo proprietario</span><span class="sxs-lookup"><span data-stu-id="b0570-201">Owner only</span></span> |
| <span data-ttu-id="b0570-202">Put Block</span><span class="sxs-lookup"><span data-stu-id="b0570-202">Put Block</span></span> |<span data-ttu-id="b0570-203">Solo proprietario</span><span class="sxs-lookup"><span data-stu-id="b0570-203">Owner only</span></span> |<span data-ttu-id="b0570-204">Solo proprietario</span><span class="sxs-lookup"><span data-stu-id="b0570-204">Owner only</span></span> |
| <span data-ttu-id="b0570-205">Get Block List (solo blocchi con commit)</span><span class="sxs-lookup"><span data-stu-id="b0570-205">Get Block List (committed blocks only)</span></span> |<span data-ttu-id="b0570-206">Tutti</span><span class="sxs-lookup"><span data-stu-id="b0570-206">All</span></span> |<span data-ttu-id="b0570-207">Tutti</span><span class="sxs-lookup"><span data-stu-id="b0570-207">All</span></span> |
| <span data-ttu-id="b0570-208">Get Block List (solo blocchi senza commit o tutti i blocchi)</span><span class="sxs-lookup"><span data-stu-id="b0570-208">Get Block List (uncommitted blocks only or all blocks)</span></span> |<span data-ttu-id="b0570-209">Solo proprietario</span><span class="sxs-lookup"><span data-stu-id="b0570-209">Owner only</span></span> |<span data-ttu-id="b0570-210">Solo proprietario</span><span class="sxs-lookup"><span data-stu-id="b0570-210">Owner only</span></span> |
| <span data-ttu-id="b0570-211">Put Block List</span><span class="sxs-lookup"><span data-stu-id="b0570-211">Put Block List</span></span> |<span data-ttu-id="b0570-212">Solo proprietario</span><span class="sxs-lookup"><span data-stu-id="b0570-212">Owner only</span></span> |<span data-ttu-id="b0570-213">Solo proprietario</span><span class="sxs-lookup"><span data-stu-id="b0570-213">Owner only</span></span> |
| <span data-ttu-id="b0570-214">Delete Blob</span><span class="sxs-lookup"><span data-stu-id="b0570-214">Delete Blob</span></span> |<span data-ttu-id="b0570-215">Solo proprietario</span><span class="sxs-lookup"><span data-stu-id="b0570-215">Owner only</span></span> |<span data-ttu-id="b0570-216">Solo proprietario</span><span class="sxs-lookup"><span data-stu-id="b0570-216">Owner only</span></span> |
| <span data-ttu-id="b0570-217">Copy Blob</span><span class="sxs-lookup"><span data-stu-id="b0570-217">Copy Blob</span></span> |<span data-ttu-id="b0570-218">Solo proprietario</span><span class="sxs-lookup"><span data-stu-id="b0570-218">Owner only</span></span> |<span data-ttu-id="b0570-219">Solo proprietario</span><span class="sxs-lookup"><span data-stu-id="b0570-219">Owner only</span></span> |
| <span data-ttu-id="b0570-220">Snapshot Blob</span><span class="sxs-lookup"><span data-stu-id="b0570-220">Snapshot Blob</span></span> |<span data-ttu-id="b0570-221">Solo proprietario</span><span class="sxs-lookup"><span data-stu-id="b0570-221">Owner only</span></span> |<span data-ttu-id="b0570-222">Solo proprietario</span><span class="sxs-lookup"><span data-stu-id="b0570-222">Owner only</span></span> |
| <span data-ttu-id="b0570-223">Lease Blob</span><span class="sxs-lookup"><span data-stu-id="b0570-223">Lease Blob</span></span> |<span data-ttu-id="b0570-224">Solo proprietario</span><span class="sxs-lookup"><span data-stu-id="b0570-224">Owner only</span></span> |<span data-ttu-id="b0570-225">Solo proprietario</span><span class="sxs-lookup"><span data-stu-id="b0570-225">Owner only</span></span> |
| <span data-ttu-id="b0570-226">Put Page</span><span class="sxs-lookup"><span data-stu-id="b0570-226">Put Page</span></span> |<span data-ttu-id="b0570-227">Solo proprietario</span><span class="sxs-lookup"><span data-stu-id="b0570-227">Owner only</span></span> |<span data-ttu-id="b0570-228">Solo proprietario</span><span class="sxs-lookup"><span data-stu-id="b0570-228">Owner only</span></span> |
| <span data-ttu-id="b0570-229">Get Page Ranges</span><span class="sxs-lookup"><span data-stu-id="b0570-229">Get Page Ranges</span></span> |<span data-ttu-id="b0570-230">Tutti</span><span class="sxs-lookup"><span data-stu-id="b0570-230">All</span></span> |<span data-ttu-id="b0570-231">Tutti</span><span class="sxs-lookup"><span data-stu-id="b0570-231">All</span></span> |
| <span data-ttu-id="b0570-232">Append Blob</span><span class="sxs-lookup"><span data-stu-id="b0570-232">Append Blob</span></span> |<span data-ttu-id="b0570-233">Solo proprietario</span><span class="sxs-lookup"><span data-stu-id="b0570-233">Owner only</span></span> |<span data-ttu-id="b0570-234">Solo proprietario</span><span class="sxs-lookup"><span data-stu-id="b0570-234">Owner only</span></span> |

## <a name="next-steps"></a><span data-ttu-id="b0570-235">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b0570-235">Next steps</span></span>

* [<span data-ttu-id="b0570-236">Autenticazione per hello servizi di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="b0570-236">Authentication for hello Azure Storage Services</span></span>](https://msdn.microsoft.com/library/azure/dd179428.aspx)
* [<span data-ttu-id="b0570-237">Uso delle firme di accesso condiviso</span><span class="sxs-lookup"><span data-stu-id="b0570-237">Using Shared Access Signatures (SAS)</span></span>](storage-dotnet-shared-access-signature-part-1.md)
* [<span data-ttu-id="b0570-238">Delega dell'accesso con una firma di accesso condiviso</span><span class="sxs-lookup"><span data-stu-id="b0570-238">Delegating Access with a Shared Access Signature</span></span>](https://msdn.microsoft.com/library/azure/ee395415.aspx)
