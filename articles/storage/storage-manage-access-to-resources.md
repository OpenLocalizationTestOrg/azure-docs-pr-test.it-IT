---
title: Abilitare l'accesso in lettura pubblico per contenitori e BLOB in Archiviazione BLOB di Azure | Microsoft Docs
description: Informazioni su come rendere disponibili per l'accesso anonimo contenitori e BLOB e su come accedervi a livello di programmazione.
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
ms.openlocfilehash: c7b83667b58649c156a62fa68cebd854c13e2cba
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="manage-anonymous-read-access-to-containers-and-blobs"></a><span data-ttu-id="56eaa-103">Gestire l'accesso in lettura anonimo a contenitori e BLOB</span><span class="sxs-lookup"><span data-stu-id="56eaa-103">Manage anonymous read access to containers and blobs</span></span>
<span data-ttu-id="56eaa-104">È possibile abilitare l'accesso in lettura pubblico anonimo a un contenitore e ai relativi BLOB in Archiviazione BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="56eaa-104">You can enable anonymous, public read access to a container and its blobs in Azure Blob storage.</span></span> <span data-ttu-id="56eaa-105">Ciò permette di concedere l'accesso in sola lettura a queste risorse senza condividere la chiave dell'account e senza richiedere una firma di accesso condiviso (SAS).</span><span class="sxs-lookup"><span data-stu-id="56eaa-105">By doing so, you can grant read-only access to these resources without sharing your account key, and without requiring a shared access signature (SAS).</span></span>

<span data-ttu-id="56eaa-106">L'accesso in lettura pubblico è ideale per scenari in cui si vuole che BLOB specifici siano sempre disponibili per l'accesso in lettura anonimo.</span><span class="sxs-lookup"><span data-stu-id="56eaa-106">Public read access is best for scenarios where you want certain blobs to always be available for anonymous read access.</span></span> <span data-ttu-id="56eaa-107">Per un controllo più accurato, è possibile creare una firma di accesso condiviso.</span><span class="sxs-lookup"><span data-stu-id="56eaa-107">For more fine-grained control, you can create a shared access signature.</span></span> <span data-ttu-id="56eaa-108">Le firme di accesso condiviso consentono di fornire accesso limitato usando autorizzazioni diverse, per un periodo di tempo specifico.</span><span class="sxs-lookup"><span data-stu-id="56eaa-108">Shared access signatures enable you to provide restricted access using different permissions, for a specific time period.</span></span> <span data-ttu-id="56eaa-109">Per altre informazioni sulla creazione di firme di accesso condiviso, vedere [Uso delle firme di accesso condiviso](storage-dotnet-shared-access-signature-part-1.md).</span><span class="sxs-lookup"><span data-stu-id="56eaa-109">For more information about creating shared access signatures, see [Using shared access signatures (SAS) in Azure Storage](storage-dotnet-shared-access-signature-part-1.md).</span></span>

## <a name="grant-anonymous-users-permissions-to-containers-and-blobs"></a><span data-ttu-id="56eaa-110">Concedere le autorizzazioni agli utenti anonimi per contenitori e BLOB</span><span class="sxs-lookup"><span data-stu-id="56eaa-110">Grant anonymous users permissions to containers and blobs</span></span>
<span data-ttu-id="56eaa-111">Per impostazione predefinita, solo il proprietario dell'account di archiviazione può accedere a un contenitore e ai BLOB in esso contenuti.</span><span class="sxs-lookup"><span data-stu-id="56eaa-111">By default, a container and any blobs within it may be accessed only by the owner of the storage account.</span></span> <span data-ttu-id="56eaa-112">Se si desidera assegnare a utenti anonimi autorizzazioni di lettura per un contenitore e i relativi BLOB, è possibile impostare le autorizzazioni del contenitore per consentire l'accesso pubblico.</span><span class="sxs-lookup"><span data-stu-id="56eaa-112">To give anonymous users read permissions to a container and its blobs, you can set the container permissions to allow public access.</span></span> <span data-ttu-id="56eaa-113">Gli utenti anonimi possono leggere i BLOB presenti in un contenitore accessibile pubblicamente senza effettuare l'autenticazione della richiesta.</span><span class="sxs-lookup"><span data-stu-id="56eaa-113">Anonymous users can read blobs within a publicly accessible container without authenticating the request.</span></span>

<span data-ttu-id="56eaa-114">È possibile configurare un contenitore con le autorizzazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="56eaa-114">You can configure a container with the following permissions:</span></span>

* <span data-ttu-id="56eaa-115">**Nessun accesso in lettura pubblico:** solo il proprietario dell'account di archiviazione può accedere al contenitore e ai relativi BLOB.</span><span class="sxs-lookup"><span data-stu-id="56eaa-115">**No public read access:** The container and its blobs can be accessed only by the storage account owner.</span></span> <span data-ttu-id="56eaa-116">Questa è l'impostazione predefinita per tutti i nuovi contenitori.</span><span class="sxs-lookup"><span data-stu-id="56eaa-116">This is the default for all new containers.</span></span>
* <span data-ttu-id="56eaa-117">**Accesso in lettura pubblico solo per i BLOB:** i dati del BLOB all'interno del contenitore possono essere letti tramite richiesta anonima, ma i dati del contenitore non sono disponibili.</span><span class="sxs-lookup"><span data-stu-id="56eaa-117">**Public read access for blobs only:** Blobs within the container can be read by anonymous request, but container data is not available.</span></span> <span data-ttu-id="56eaa-118">I client anonimi non possono enumerare i BLOB all'interno del contenitore.</span><span class="sxs-lookup"><span data-stu-id="56eaa-118">Anonymous clients cannot enumerate the blobs within the container.</span></span>
* <span data-ttu-id="56eaa-119">**Accesso in lettura pubblico completo:** i dati del BLOB e del contenitore possono essere letti tramite richiesta anonima.</span><span class="sxs-lookup"><span data-stu-id="56eaa-119">**Full public read access:** All container and blob data can be read by anonymous request.</span></span> <span data-ttu-id="56eaa-120">I client possono enumerare i BLOB all'interno del contenitore tramite richiesta anonima, ma non sono in grado di enumerare i contenitori all'interno dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="56eaa-120">Clients can enumerate blobs within the container by anonymous request, but cannot enumerate containers within the storage account.</span></span>

<span data-ttu-id="56eaa-121">È possibile impostare le autorizzazioni per il contenitore usando gli strumenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="56eaa-121">You can use the following to set container permissions:</span></span>

* [<span data-ttu-id="56eaa-122">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="56eaa-122">Azure portal</span></span>](https://portal.azure.com)
* [<span data-ttu-id="56eaa-123">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="56eaa-123">Azure PowerShell</span></span>](storage-powershell-guide-full.md#how-to-manage-azure-blobs)
* [<span data-ttu-id="56eaa-124">Interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="56eaa-124">Azure CLI 2.0</span></span>](storage-azure-cli.md#create-and-manage-blobs)
* <span data-ttu-id="56eaa-125">A livello di programmazione, usando una delle librerie client di archiviazione o l'API REST.</span><span class="sxs-lookup"><span data-stu-id="56eaa-125">Programmatically, by using one of the storage client libraries or the REST API</span></span>

### <a name="set-container-permissions-in-the-azure-portal"></a><span data-ttu-id="56eaa-126">Impostare le autorizzazioni per in contenitore nel portale di Azure</span><span class="sxs-lookup"><span data-stu-id="56eaa-126">Set container permissions in the Azure portal</span></span>
<span data-ttu-id="56eaa-127">Per impostare le autorizzazioni per il contenitore nel [portale di Azure](https://portal.azure.com), seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="56eaa-127">To set container permissions in the [Azure portal](https://portal.azure.com), follow these steps:</span></span>

1. <span data-ttu-id="56eaa-128">Selezionare il pannello **Account di archiviazione** nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="56eaa-128">Open your **Storage account** blade in the portal.</span></span> <span data-ttu-id="56eaa-129">È possibile trovare l'account di archiviazione selezionando **Account di archiviazione** nel pannello del menu principale del portale.</span><span class="sxs-lookup"><span data-stu-id="56eaa-129">You can find your storage account by selecting **Storage accounts** in the main portal menu blade.</span></span>
1. <span data-ttu-id="56eaa-130">Nel pannello del menu, in **SERVIZIO BLOB** selezionare **Contenitori**.</span><span class="sxs-lookup"><span data-stu-id="56eaa-130">Under **BLOB SERVICE** on the menu blade, select **Containers**.</span></span>
1. <span data-ttu-id="56eaa-131">Fare clic con il pulsante destro del mouse sulla riga del contenitore o selezionare i puntini di sospensione per aprire il **menu di scelta rapida** del contenitore.</span><span class="sxs-lookup"><span data-stu-id="56eaa-131">Right-click on the container row or select the ellipsis to open the container's **Context menu**.</span></span>
1. <span data-ttu-id="56eaa-132">In questo menu selezionare **Criteri di accesso**.</span><span class="sxs-lookup"><span data-stu-id="56eaa-132">Select **Access policy** in the context menu.</span></span>
1. <span data-ttu-id="56eaa-133">Nel menu a discesa selezionare un **Tipo di accesso**.</span><span class="sxs-lookup"><span data-stu-id="56eaa-133">Select an **Access type** from the drop down menu.</span></span>

    ![Finestra di dialogo Modifica metadati contenitore](./media/storage-manage-access-to-resources/storage-manage-access-to-resources-0.png)

### <a name="set-container-permissions-with-net"></a><span data-ttu-id="56eaa-135">Impostare le autorizzazioni per il contenitore con .NET</span><span class="sxs-lookup"><span data-stu-id="56eaa-135">Set container permissions with .NET</span></span>
<span data-ttu-id="56eaa-136">Per impostare le autorizzazioni per un contenitore con C# e la libreria client di archiviazione per .NET, recuperare prima di tutto le autorizzazioni esistenti per il contenitore eseguendo una chiamata al metodo **GetPermissions**.</span><span class="sxs-lookup"><span data-stu-id="56eaa-136">To set permissions for a container using C# and the Storage Client Library for .NET, first retrieve the container's existing permissions by calling the **GetPermissions** method.</span></span> <span data-ttu-id="56eaa-137">Impostare quindi la proprietà **PublicAccess** per l'oggetto **BlobContainerPermissions** restituito dal metodo **GetPermissions**.</span><span class="sxs-lookup"><span data-stu-id="56eaa-137">Then set the **PublicAccess** property for the **BlobContainerPermissions** object that is returned by the **GetPermissions** method.</span></span> <span data-ttu-id="56eaa-138">Infine, chiamare il metodo **SetPermissions** con le autorizzazioni aggiornate.</span><span class="sxs-lookup"><span data-stu-id="56eaa-138">Finally, call the **SetPermissions** method with the updated permissions.</span></span>

<span data-ttu-id="56eaa-139">L'esempio seguente imposta le autorizzazioni per il contenitore per l'accesso in lettura pubblico completo.</span><span class="sxs-lookup"><span data-stu-id="56eaa-139">The following example sets the container's permissions to full public read access.</span></span> <span data-ttu-id="56eaa-140">Per impostare le autorizzazioni per l'accesso in lettura pubblico solo per i BLOB, impostare la proprietà **PublicAccess** su **BlobContainerPublicAccessType.Blob**.</span><span class="sxs-lookup"><span data-stu-id="56eaa-140">To set permissions to public read access for blobs only, set the **PublicAccess** property to **BlobContainerPublicAccessType.Blob**.</span></span> <span data-ttu-id="56eaa-141">Per rimuovere tutte le autorizzazioni per gli utenti anonimi, impostare la proprietà su **BlobContainerPublicAccessType.Off**.</span><span class="sxs-lookup"><span data-stu-id="56eaa-141">To remove all permissions for anonymous users, set the property to **BlobContainerPublicAccessType.Off**.</span></span>

```csharp
public static void SetPublicContainerPermissions(CloudBlobContainer container)
{
    BlobContainerPermissions permissions = container.GetPermissions();
    permissions.PublicAccess = BlobContainerPublicAccessType.Container;
    container.SetPermissions(permissions);
}
```

## <a name="access-containers-and-blobs-anonymously"></a><span data-ttu-id="56eaa-142">Accesso anonimo a contenitori e BLOB</span><span class="sxs-lookup"><span data-stu-id="56eaa-142">Access containers and blobs anonymously</span></span>
<span data-ttu-id="56eaa-143">Un client che accede a contenitori e BLOB in modo anonimo può usare costruttori che non richiedono credenziali.</span><span class="sxs-lookup"><span data-stu-id="56eaa-143">A client that accesses containers and blobs anonymously can use constructors that do not require credentials.</span></span> <span data-ttu-id="56eaa-144">L'esempio seguente mostra alcuni modi diversi per fare riferimento a risorse del servizio BLOB in modo anonimo.</span><span class="sxs-lookup"><span data-stu-id="56eaa-144">The following examples show a few different ways to reference Blob service resources anonymously.</span></span>

### <a name="create-an-anonymous-client-object"></a><span data-ttu-id="56eaa-145">Creare un oggetto client anonimo</span><span class="sxs-lookup"><span data-stu-id="56eaa-145">Create an anonymous client object</span></span>
<span data-ttu-id="56eaa-146">È possibile creare un nuovo oggetto client del servizio per l'accesso anonimo, specificando l'endpoint del servizio BLOB per l'account.</span><span class="sxs-lookup"><span data-stu-id="56eaa-146">You can create a new service client object for anonymous access by providing the Blob service endpoint for the account.</span></span> <span data-ttu-id="56eaa-147">Tuttavia, è necessario conoscere anche il nome di un contenitore in tale account disponibile per l'accesso anonimo.</span><span class="sxs-lookup"><span data-stu-id="56eaa-147">However, you must also know the name of a container in that account that's available for anonymous access.</span></span>

```csharp
public static void CreateAnonymousBlobClient()
{
    // Create the client object using the Blob service endpoint.
    CloudBlobClient blobClient = new CloudBlobClient(new Uri(@"https://storagesample.blob.core.windows.net"));

    // Get a reference to a container that's available for anonymous access.
    CloudBlobContainer container = blobClient.GetContainerReference("sample-container");

    // Read the container's properties. Note this is only possible when the container supports full public read access.
    container.FetchAttributes();
    Console.WriteLine(container.Properties.LastModified);
    Console.WriteLine(container.Properties.ETag);
}
```

### <a name="reference-a-container-anonymously"></a><span data-ttu-id="56eaa-148">Fare riferimento a un contenitore in modo anonimo</span><span class="sxs-lookup"><span data-stu-id="56eaa-148">Reference a container anonymously</span></span>
<span data-ttu-id="56eaa-149">Se si conosce l'URL per un contenitore disponibile in modo anonimo, è possibile usarlo per fare riferimento direttamente al contenitore.</span><span class="sxs-lookup"><span data-stu-id="56eaa-149">If you have the URL to a container that is anonymously available, you can use it to reference the container directly.</span></span>

```csharp
public static void ListBlobsAnonymously()
{
    // Get a reference to a container that's available for anonymous access.
    CloudBlobContainer container = new CloudBlobContainer(new Uri(@"https://storagesample.blob.core.windows.net/sample-container"));

    // List blobs in the container.
    foreach (IListBlobItem blobItem in container.ListBlobs())
    {
        Console.WriteLine(blobItem.Uri);
    }
}
```

### <a name="reference-a-blob-anonymously"></a><span data-ttu-id="56eaa-150">Fare riferimento a un BLOB in modo anonimo</span><span class="sxs-lookup"><span data-stu-id="56eaa-150">Reference a blob anonymously</span></span>
<span data-ttu-id="56eaa-151">Se si conosce l'URL per un BLOB disponibile per l'accesso anonimo, è possibile fare riferimento direttamente al BLOB con tale URL:</span><span class="sxs-lookup"><span data-stu-id="56eaa-151">If you have the URL to a blob that is available for anonymous access, you can reference the blob directly using that URL:</span></span>

```csharp
public static void DownloadBlobAnonymously()
{
    CloudBlockBlob blob = new CloudBlockBlob(new Uri(@"https://storagesample.blob.core.windows.net/sample-container/logfile.txt"));
    blob.DownloadToFile(@"C:\Temp\logfile.txt", System.IO.FileMode.Create);
}
```

## <a name="features-available-to-anonymous-users"></a><span data-ttu-id="56eaa-152">Funzionalità disponibili per utenti anonimi</span><span class="sxs-lookup"><span data-stu-id="56eaa-152">Features available to anonymous users</span></span>
<span data-ttu-id="56eaa-153">Nella tabella seguente sono riportate le operazioni che possono essere richiamate da utenti anonimi quando l'ACL di un contenitore è impostato per consentire l'accesso pubblico.</span><span class="sxs-lookup"><span data-stu-id="56eaa-153">The following table shows which operations may be called by anonymous users when a container's ACL is set to allow public access.</span></span>

| <span data-ttu-id="56eaa-154">Operazione REST</span><span class="sxs-lookup"><span data-stu-id="56eaa-154">REST Operation</span></span> | <span data-ttu-id="56eaa-155">Autorizzazione con accesso in lettura pubblico completo</span><span class="sxs-lookup"><span data-stu-id="56eaa-155">Permission with full public read access</span></span> | <span data-ttu-id="56eaa-156">Autorizzazione con accesso in lettura pubblico solo per BLOB</span><span class="sxs-lookup"><span data-stu-id="56eaa-156">Permission with public read access for blobs only</span></span> |
| --- | --- | --- |
| <span data-ttu-id="56eaa-157">List Containers</span><span class="sxs-lookup"><span data-stu-id="56eaa-157">List Containers</span></span> |<span data-ttu-id="56eaa-158">Solo proprietario</span><span class="sxs-lookup"><span data-stu-id="56eaa-158">Owner only</span></span> |<span data-ttu-id="56eaa-159">Solo proprietario</span><span class="sxs-lookup"><span data-stu-id="56eaa-159">Owner only</span></span> |
| <span data-ttu-id="56eaa-160">Create Container</span><span class="sxs-lookup"><span data-stu-id="56eaa-160">Create Container</span></span> |<span data-ttu-id="56eaa-161">Solo proprietario</span><span class="sxs-lookup"><span data-stu-id="56eaa-161">Owner only</span></span> |<span data-ttu-id="56eaa-162">Solo proprietario</span><span class="sxs-lookup"><span data-stu-id="56eaa-162">Owner only</span></span> |
| <span data-ttu-id="56eaa-163">Get Container Properties</span><span class="sxs-lookup"><span data-stu-id="56eaa-163">Get Container Properties</span></span> |<span data-ttu-id="56eaa-164">Tutti</span><span class="sxs-lookup"><span data-stu-id="56eaa-164">All</span></span> |<span data-ttu-id="56eaa-165">Solo proprietario</span><span class="sxs-lookup"><span data-stu-id="56eaa-165">Owner only</span></span> |
| <span data-ttu-id="56eaa-166">Get Container Metadata</span><span class="sxs-lookup"><span data-stu-id="56eaa-166">Get Container Metadata</span></span> |<span data-ttu-id="56eaa-167">Tutti</span><span class="sxs-lookup"><span data-stu-id="56eaa-167">All</span></span> |<span data-ttu-id="56eaa-168">Solo proprietario</span><span class="sxs-lookup"><span data-stu-id="56eaa-168">Owner only</span></span> |
| <span data-ttu-id="56eaa-169">Set Container Metadata</span><span class="sxs-lookup"><span data-stu-id="56eaa-169">Set Container Metadata</span></span> |<span data-ttu-id="56eaa-170">Solo proprietario</span><span class="sxs-lookup"><span data-stu-id="56eaa-170">Owner only</span></span> |<span data-ttu-id="56eaa-171">Solo proprietario</span><span class="sxs-lookup"><span data-stu-id="56eaa-171">Owner only</span></span> |
| <span data-ttu-id="56eaa-172">Get Container ACL</span><span class="sxs-lookup"><span data-stu-id="56eaa-172">Get Container ACL</span></span> |<span data-ttu-id="56eaa-173">Solo proprietario</span><span class="sxs-lookup"><span data-stu-id="56eaa-173">Owner only</span></span> |<span data-ttu-id="56eaa-174">Solo proprietario</span><span class="sxs-lookup"><span data-stu-id="56eaa-174">Owner only</span></span> |
| <span data-ttu-id="56eaa-175">Set Container ACL</span><span class="sxs-lookup"><span data-stu-id="56eaa-175">Set Container ACL</span></span> |<span data-ttu-id="56eaa-176">Solo proprietario</span><span class="sxs-lookup"><span data-stu-id="56eaa-176">Owner only</span></span> |<span data-ttu-id="56eaa-177">Solo proprietario</span><span class="sxs-lookup"><span data-stu-id="56eaa-177">Owner only</span></span> |
| <span data-ttu-id="56eaa-178">Delete Container</span><span class="sxs-lookup"><span data-stu-id="56eaa-178">Delete Container</span></span> |<span data-ttu-id="56eaa-179">Solo proprietario</span><span class="sxs-lookup"><span data-stu-id="56eaa-179">Owner only</span></span> |<span data-ttu-id="56eaa-180">Solo proprietario</span><span class="sxs-lookup"><span data-stu-id="56eaa-180">Owner only</span></span> |
| <span data-ttu-id="56eaa-181">List Blobs</span><span class="sxs-lookup"><span data-stu-id="56eaa-181">List Blobs</span></span> |<span data-ttu-id="56eaa-182">Tutti</span><span class="sxs-lookup"><span data-stu-id="56eaa-182">All</span></span> |<span data-ttu-id="56eaa-183">Solo proprietario</span><span class="sxs-lookup"><span data-stu-id="56eaa-183">Owner only</span></span> |
| <span data-ttu-id="56eaa-184">Put Blob</span><span class="sxs-lookup"><span data-stu-id="56eaa-184">Put Blob</span></span> |<span data-ttu-id="56eaa-185">Solo proprietario</span><span class="sxs-lookup"><span data-stu-id="56eaa-185">Owner only</span></span> |<span data-ttu-id="56eaa-186">Solo proprietario</span><span class="sxs-lookup"><span data-stu-id="56eaa-186">Owner only</span></span> |
| <span data-ttu-id="56eaa-187">Get Blob</span><span class="sxs-lookup"><span data-stu-id="56eaa-187">Get Blob</span></span> |<span data-ttu-id="56eaa-188">Tutti</span><span class="sxs-lookup"><span data-stu-id="56eaa-188">All</span></span> |<span data-ttu-id="56eaa-189">Tutti</span><span class="sxs-lookup"><span data-stu-id="56eaa-189">All</span></span> |
| <span data-ttu-id="56eaa-190">Get Blob Properties</span><span class="sxs-lookup"><span data-stu-id="56eaa-190">Get Blob Properties</span></span> |<span data-ttu-id="56eaa-191">Tutti</span><span class="sxs-lookup"><span data-stu-id="56eaa-191">All</span></span> |<span data-ttu-id="56eaa-192">Tutti</span><span class="sxs-lookup"><span data-stu-id="56eaa-192">All</span></span> |
| <span data-ttu-id="56eaa-193">Set Blob Properties</span><span class="sxs-lookup"><span data-stu-id="56eaa-193">Set Blob Properties</span></span> |<span data-ttu-id="56eaa-194">Solo proprietario</span><span class="sxs-lookup"><span data-stu-id="56eaa-194">Owner only</span></span> |<span data-ttu-id="56eaa-195">Solo proprietario</span><span class="sxs-lookup"><span data-stu-id="56eaa-195">Owner only</span></span> |
| <span data-ttu-id="56eaa-196">Get Blob Metadata</span><span class="sxs-lookup"><span data-stu-id="56eaa-196">Get Blob Metadata</span></span> |<span data-ttu-id="56eaa-197">Tutti</span><span class="sxs-lookup"><span data-stu-id="56eaa-197">All</span></span> |<span data-ttu-id="56eaa-198">Tutti</span><span class="sxs-lookup"><span data-stu-id="56eaa-198">All</span></span> |
| <span data-ttu-id="56eaa-199">Set Blob Metadata</span><span class="sxs-lookup"><span data-stu-id="56eaa-199">Set Blob Metadata</span></span> |<span data-ttu-id="56eaa-200">Solo proprietario</span><span class="sxs-lookup"><span data-stu-id="56eaa-200">Owner only</span></span> |<span data-ttu-id="56eaa-201">Solo proprietario</span><span class="sxs-lookup"><span data-stu-id="56eaa-201">Owner only</span></span> |
| <span data-ttu-id="56eaa-202">Put Block</span><span class="sxs-lookup"><span data-stu-id="56eaa-202">Put Block</span></span> |<span data-ttu-id="56eaa-203">Solo proprietario</span><span class="sxs-lookup"><span data-stu-id="56eaa-203">Owner only</span></span> |<span data-ttu-id="56eaa-204">Solo proprietario</span><span class="sxs-lookup"><span data-stu-id="56eaa-204">Owner only</span></span> |
| <span data-ttu-id="56eaa-205">Get Block List (solo blocchi con commit)</span><span class="sxs-lookup"><span data-stu-id="56eaa-205">Get Block List (committed blocks only)</span></span> |<span data-ttu-id="56eaa-206">Tutti</span><span class="sxs-lookup"><span data-stu-id="56eaa-206">All</span></span> |<span data-ttu-id="56eaa-207">Tutti</span><span class="sxs-lookup"><span data-stu-id="56eaa-207">All</span></span> |
| <span data-ttu-id="56eaa-208">Get Block List (solo blocchi senza commit o tutti i blocchi)</span><span class="sxs-lookup"><span data-stu-id="56eaa-208">Get Block List (uncommitted blocks only or all blocks)</span></span> |<span data-ttu-id="56eaa-209">Solo proprietario</span><span class="sxs-lookup"><span data-stu-id="56eaa-209">Owner only</span></span> |<span data-ttu-id="56eaa-210">Solo proprietario</span><span class="sxs-lookup"><span data-stu-id="56eaa-210">Owner only</span></span> |
| <span data-ttu-id="56eaa-211">Put Block List</span><span class="sxs-lookup"><span data-stu-id="56eaa-211">Put Block List</span></span> |<span data-ttu-id="56eaa-212">Solo proprietario</span><span class="sxs-lookup"><span data-stu-id="56eaa-212">Owner only</span></span> |<span data-ttu-id="56eaa-213">Solo proprietario</span><span class="sxs-lookup"><span data-stu-id="56eaa-213">Owner only</span></span> |
| <span data-ttu-id="56eaa-214">Delete Blob</span><span class="sxs-lookup"><span data-stu-id="56eaa-214">Delete Blob</span></span> |<span data-ttu-id="56eaa-215">Solo proprietario</span><span class="sxs-lookup"><span data-stu-id="56eaa-215">Owner only</span></span> |<span data-ttu-id="56eaa-216">Solo proprietario</span><span class="sxs-lookup"><span data-stu-id="56eaa-216">Owner only</span></span> |
| <span data-ttu-id="56eaa-217">Copy Blob</span><span class="sxs-lookup"><span data-stu-id="56eaa-217">Copy Blob</span></span> |<span data-ttu-id="56eaa-218">Solo proprietario</span><span class="sxs-lookup"><span data-stu-id="56eaa-218">Owner only</span></span> |<span data-ttu-id="56eaa-219">Solo proprietario</span><span class="sxs-lookup"><span data-stu-id="56eaa-219">Owner only</span></span> |
| <span data-ttu-id="56eaa-220">Snapshot Blob</span><span class="sxs-lookup"><span data-stu-id="56eaa-220">Snapshot Blob</span></span> |<span data-ttu-id="56eaa-221">Solo proprietario</span><span class="sxs-lookup"><span data-stu-id="56eaa-221">Owner only</span></span> |<span data-ttu-id="56eaa-222">Solo proprietario</span><span class="sxs-lookup"><span data-stu-id="56eaa-222">Owner only</span></span> |
| <span data-ttu-id="56eaa-223">Lease Blob</span><span class="sxs-lookup"><span data-stu-id="56eaa-223">Lease Blob</span></span> |<span data-ttu-id="56eaa-224">Solo proprietario</span><span class="sxs-lookup"><span data-stu-id="56eaa-224">Owner only</span></span> |<span data-ttu-id="56eaa-225">Solo proprietario</span><span class="sxs-lookup"><span data-stu-id="56eaa-225">Owner only</span></span> |
| <span data-ttu-id="56eaa-226">Put Page</span><span class="sxs-lookup"><span data-stu-id="56eaa-226">Put Page</span></span> |<span data-ttu-id="56eaa-227">Solo proprietario</span><span class="sxs-lookup"><span data-stu-id="56eaa-227">Owner only</span></span> |<span data-ttu-id="56eaa-228">Solo proprietario</span><span class="sxs-lookup"><span data-stu-id="56eaa-228">Owner only</span></span> |
| <span data-ttu-id="56eaa-229">Get Page Ranges</span><span class="sxs-lookup"><span data-stu-id="56eaa-229">Get Page Ranges</span></span> |<span data-ttu-id="56eaa-230">Tutti</span><span class="sxs-lookup"><span data-stu-id="56eaa-230">All</span></span> |<span data-ttu-id="56eaa-231">Tutti</span><span class="sxs-lookup"><span data-stu-id="56eaa-231">All</span></span> |
| <span data-ttu-id="56eaa-232">Append Blob</span><span class="sxs-lookup"><span data-stu-id="56eaa-232">Append Blob</span></span> |<span data-ttu-id="56eaa-233">Solo proprietario</span><span class="sxs-lookup"><span data-stu-id="56eaa-233">Owner only</span></span> |<span data-ttu-id="56eaa-234">Solo proprietario</span><span class="sxs-lookup"><span data-stu-id="56eaa-234">Owner only</span></span> |

## <a name="next-steps"></a><span data-ttu-id="56eaa-235">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="56eaa-235">Next steps</span></span>

* [<span data-ttu-id="56eaa-236">Autenticazione per i servizi di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="56eaa-236">Authentication for the Azure Storage Services</span></span>](https://msdn.microsoft.com/library/azure/dd179428.aspx)
* [<span data-ttu-id="56eaa-237">Uso delle firme di accesso condiviso</span><span class="sxs-lookup"><span data-stu-id="56eaa-237">Using Shared Access Signatures (SAS)</span></span>](storage-dotnet-shared-access-signature-part-1.md)
* [<span data-ttu-id="56eaa-238">Delega dell'accesso con una firma di accesso condiviso</span><span class="sxs-lookup"><span data-stu-id="56eaa-238">Delegating Access with a Shared Access Signature</span></span>](https://msdn.microsoft.com/library/azure/ee395415.aspx)
