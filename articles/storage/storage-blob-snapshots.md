---
title: Creare uno snapshot di sola lettura di un BLOB in Archiviazione di Azure | Microsoft Docs
description: "Scoprire come creare snapshot di un BLOB per eseguire il backup dei dati BLOB in un determinato momento. Comprendere come vengono fatturati gli snapshot e come utilizzarli per ridurre i costi di capacità."
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 3710705d-e127-4b01-8d0f-29853fb06d0d
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/11/2017
ms.author: marsma
ms.openlocfilehash: 6ebb77f4ec5f1887e5c55bf1c8c64224a9233654
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-blob-snapshot"></a><span data-ttu-id="05508-104">Creare uno snapshot del BLOB</span><span class="sxs-lookup"><span data-stu-id="05508-104">Create a blob snapshot</span></span>

<span data-ttu-id="05508-105">Uno snapshot è una versione di sola lettura di un BLOB eseguito in un determinato momento.</span><span class="sxs-lookup"><span data-stu-id="05508-105">A snapshot is a read-only version of a blob that's taken at a point in time.</span></span> <span data-ttu-id="05508-106">Gli snapshot sono utili per il backup dei BLOB.</span><span class="sxs-lookup"><span data-stu-id="05508-106">Snapshots are useful for backing up blobs.</span></span> <span data-ttu-id="05508-107">Dopo aver creato uno snapshot, è possibile leggerlo, copiarlo o eliminarlo, ma non modificarlo.</span><span class="sxs-lookup"><span data-stu-id="05508-107">After you create a snapshot, you can read, copy, or delete it, but you cannot modify it.</span></span>

<span data-ttu-id="05508-108">Uno snapshot di un BLOB è identico al relativo BLOB di base, ad eccezione del fatto che all'URI del BLOB viene aggiunto un valore **DateTime** per indicare data e ora di acquisizione dello snapshot.</span><span class="sxs-lookup"><span data-stu-id="05508-108">A snapshot of a blob is identical to its base blob, except that the blob URI has a **DateTime** value appended to the blob URI to indicate the time at which the snapshot was taken.</span></span> <span data-ttu-id="05508-109">Ad esempio, se un URI del BLOB di pagine è `http://storagesample.core.blob.windows.net/mydrives/myvhd`, l'URI dello snapshot è simile a `http://storagesample.core.blob.windows.net/mydrives/myvhd?snapshot=2011-03-09T01:42:34.9360000Z`.</span><span class="sxs-lookup"><span data-stu-id="05508-109">For example, if a page blob URI is `http://storagesample.core.blob.windows.net/mydrives/myvhd`, the snapshot URI is similar to `http://storagesample.core.blob.windows.net/mydrives/myvhd?snapshot=2011-03-09T01:42:34.9360000Z`.</span></span>

> [!NOTE]
> <span data-ttu-id="05508-110">Tutti gli snapshot condividono l'URI del BLOB di base.</span><span class="sxs-lookup"><span data-stu-id="05508-110">All snapshots share the base blob's URI.</span></span> <span data-ttu-id="05508-111">L'unica distinzione tra il BLOB di base e lo snapshot è il valore **DateTime** aggiunto.</span><span class="sxs-lookup"><span data-stu-id="05508-111">The only distinction between the base blob and the snapshot is the appended **DateTime** value.</span></span>
>

<span data-ttu-id="05508-112">Un BLOB può avere un numero qualsiasi di snapshot.</span><span class="sxs-lookup"><span data-stu-id="05508-112">A blob can have any number of snapshots.</span></span> <span data-ttu-id="05508-113">Gli snapshot vengono mantenuti fino all'eliminazione esplicita.</span><span class="sxs-lookup"><span data-stu-id="05508-113">Snapshots persist until they are explicitly deleted.</span></span> <span data-ttu-id="05508-114">Uno snapshot non può sopravvivere al relativo BLOB di base.</span><span class="sxs-lookup"><span data-stu-id="05508-114">A snapshot cannot outlive its base blob.</span></span> <span data-ttu-id="05508-115">È possibile enumerare gli snapshot associati al BLOB di base per tenere traccia degli snapshot correnti.</span><span class="sxs-lookup"><span data-stu-id="05508-115">You can enumerate the snapshots associated with the base blob to track your current snapshots.</span></span>

<span data-ttu-id="05508-116">Quando si crea uno snapshot di un BLOB, le proprietà di sistema del BLOB vengono copiate nello snapshot con gli stessi valori.</span><span class="sxs-lookup"><span data-stu-id="05508-116">When you create a snapshot of a blob, the blob's system properties are copied to the snapshot with the same values.</span></span> <span data-ttu-id="05508-117">Anche i metadati del BLOB di base vengono copiati nello snapshot, se non si specificano metadati separati per lo snapshot durante la creazione.</span><span class="sxs-lookup"><span data-stu-id="05508-117">The base blob's metadata is also copied to the snapshot, unless you specify separate metadata for the snapshot when you create it.</span></span>

<span data-ttu-id="05508-118">Eventuali lease associati al BLOB di base non vengono copiati nello snapshot.</span><span class="sxs-lookup"><span data-stu-id="05508-118">Any leases associated with the base blob do not affect the snapshot.</span></span> <span data-ttu-id="05508-119">Non è possibile acquisire un lease in uno snapshot.</span><span class="sxs-lookup"><span data-stu-id="05508-119">You cannot acquire a lease on a snapshot.</span></span>

<span data-ttu-id="05508-120">Un file di disco rigido virtuale viene usato per archiviare lo stato e le informazioni correnti per il disco della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="05508-120">A VHD file is used to store the current information and status for a VM disk.</span></span> <span data-ttu-id="05508-121">È possibile scollegare il disco dall'interno della macchina virtuale o arrestare la macchina virtuale e quindi creare uno snapshot del relativo file di disco rigido virtuale.</span><span class="sxs-lookup"><span data-stu-id="05508-121">You can detach a disk from within the VM or shut down the VM, and then take a snapshot of its VHD file.</span></span> <span data-ttu-id="05508-122">È possibile usare il file di snapshot successivamente per recuperare il file di disco rigido virtuale in quel determinato momento e ricreare la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="05508-122">You can use that snapshot file later to retrieve the VHD file at that point in time and recreate the VM.</span></span>

<span data-ttu-id="05508-123">Se la Crittografia del servizio di archiviazione (SSE) è abilitata per l'account di archiviazione in cui si trova il BLOB, per gli snapshot del BLOB verrà eseguita la crittografia dei dati inattivi.</span><span class="sxs-lookup"><span data-stu-id="05508-123">If Storage Service Encryption (SSE) is enabled for the storage account in which the blob resides, then any snapshots taken of that blob will be encrypted at rest.</span></span>

## <a name="create-a-snapshot"></a><span data-ttu-id="05508-124">Creare uno snapshot</span><span class="sxs-lookup"><span data-stu-id="05508-124">Create a snapshot</span></span>
<span data-ttu-id="05508-125">L'esempio seguente illustra come creare uno snapshot usando la [libreria client di Archiviazione di Azure per .NET](https://www.nuget.org/packages/WindowsAzure.Storage/).</span><span class="sxs-lookup"><span data-stu-id="05508-125">The following code example shows how to create a snapshot by using the [Azure Storage Client Library for .NET](https://www.nuget.org/packages/WindowsAzure.Storage/).</span></span> <span data-ttu-id="05508-126">Questo esempio specifica metadati aggiuntivi per lo snapshot al momento della creazione.</span><span class="sxs-lookup"><span data-stu-id="05508-126">This example specifies additional metadata for the snapshot when it is created.</span></span>

```csharp
private static async Task CreateBlockBlobSnapshot(CloudBlobContainer container)
{
    // Create a new block blob in the container.
    CloudBlockBlob baseBlob = container.GetBlockBlobReference("sample-base-blob.txt");

    // Add blob metadata.
    baseBlob.Metadata.Add("ApproxBlobCreatedDate", DateTime.UtcNow.ToString());

    try
    {
        // Upload the blob to create it, with its metadata.
        await baseBlob.UploadTextAsync(string.Format("Base blob: {0}", baseBlob.Uri.ToString()));

        // Sleep 5 seconds.
        System.Threading.Thread.Sleep(5000);

        // Create a snapshot of the base blob.
        // Specify metadata at the time that the snapshot is created to specify unique metadata for the snapshot.
        // If no metadata is specified when the snapshot is created, the base blob's metadata is copied to the snapshot.
        Dictionary<string, string> metadata = new Dictionary<string, string>();
        metadata.Add("ApproxSnapshotCreatedDate", DateTime.UtcNow.ToString());
        await baseBlob.CreateSnapshotAsync(metadata, null, null, null);
    }
    catch (StorageException e)
    {
        Console.WriteLine(e.Message);
        Console.ReadLine();
        throw;
    }
}
```

## <a name="copy-snapshots"></a><span data-ttu-id="05508-127">Copiare gli snapshot</span><span class="sxs-lookup"><span data-stu-id="05508-127">Copy snapshots</span></span>
<span data-ttu-id="05508-128">Le operazioni di copia che interessano BLOB e snapshot si attengono alle seguenti regole:</span><span class="sxs-lookup"><span data-stu-id="05508-128">Copy operations involving blobs and snapshots follow these rules:</span></span>

* <span data-ttu-id="05508-129">È possibile copiare uno snapshot sul relativo BLOB di base.</span><span class="sxs-lookup"><span data-stu-id="05508-129">You can copy a snapshot over its base blob.</span></span> <span data-ttu-id="05508-130">Promuovendo uno snapshot alla posizione del BLOB di base, è possibile ripristinare la versione precedente di un BLOB.</span><span class="sxs-lookup"><span data-stu-id="05508-130">By promoting a snapshot to the position of the base blob, you can restore an earlier version of a blob.</span></span> <span data-ttu-id="05508-131">Lo snapshot resta, ma il BLOB di base viene sovrascritto con una copia scrivibile dello snapshot.</span><span class="sxs-lookup"><span data-stu-id="05508-131">The snapshot remains, but the base blob is overwritten with a writable copy of the snapshot.</span></span>
* <span data-ttu-id="05508-132">È possibile copiare uno snapshot in un BLOB di destinazione con un nome diverso.</span><span class="sxs-lookup"><span data-stu-id="05508-132">You can copy a snapshot to a destination blob with a different name.</span></span> <span data-ttu-id="05508-133">Il BLOB di destinazione risultante è un BLOB scrivibile, non uno snapshot.</span><span class="sxs-lookup"><span data-stu-id="05508-133">The resulting destination blob is a writable blob and not a snapshot.</span></span>
* <span data-ttu-id="05508-134">Quando si copia un BLOB di origine, gli snapshot del BLOB di origine non vengono copiati nella destinazione.</span><span class="sxs-lookup"><span data-stu-id="05508-134">When a source blob is copied, any snapshots of the source blob are not copied to the destination.</span></span> <span data-ttu-id="05508-135">Quando un BLOB di destinazione viene sovrascritto con una copia, gli eventuali snapshot associati al BLOB di destinazione originale rimangono invariati.</span><span class="sxs-lookup"><span data-stu-id="05508-135">When a destination blob is overwritten with a copy, any snapshots associated with the original destination blob remain intact.</span></span>
* <span data-ttu-id="05508-136">Quando si crea uno snapshot di un BLOB in blocchi, anche l'elenco di blocchi di cui è stato eseguito il commit del BLOB viene copiato nello snapshot.</span><span class="sxs-lookup"><span data-stu-id="05508-136">When you create a snapshot of a block blob, the blob's committed block list is also copied to the snapshot.</span></span> <span data-ttu-id="05508-137">Eventuali blocchi di cui non è stato eseguito il commit non vengono copiati.</span><span class="sxs-lookup"><span data-stu-id="05508-137">Any uncommitted blocks are not copied.</span></span>

## <a name="specify-an-access-condition"></a><span data-ttu-id="05508-138">Specificare una condizione di accesso</span><span class="sxs-lookup"><span data-stu-id="05508-138">Specify an access condition</span></span>
<span data-ttu-id="05508-139">Quando si chiama [CreateSnapshotAsync][dotnet_CreateSnapshotAsync], è possibile specificare una condizione di accesso in modo da creare lo snapshot solo se viene soddisfatta tale condizione.</span><span class="sxs-lookup"><span data-stu-id="05508-139">When you call [CreateSnapshotAsync][dotnet_CreateSnapshotAsync], you can specify an access condition so that the snapshot is created only if a condition is met.</span></span> <span data-ttu-id="05508-140">Per specificare una condizione di accesso, usare il parametro [AccessCondition][dotnet_AccessCondition].</span><span class="sxs-lookup"><span data-stu-id="05508-140">To specify an access condition, use the [AccessCondition][dotnet_AccessCondition] parameter.</span></span> <span data-ttu-id="05508-141">Se la condizione specificata non viene soddisfatta, lo snapshot non viene creato e il servizio BLOB restituisce il codice di stato [HTTPStatusCode][dotnet_HTTPStatusCode].PreconditionFailed.</span><span class="sxs-lookup"><span data-stu-id="05508-141">If the specified condition is not met, the snapshot is not created, and the Blob service returns status code [HTTPStatusCode][dotnet_HTTPStatusCode].PreconditionFailed.</span></span>

## <a name="delete-snapshots"></a><span data-ttu-id="05508-142">Eliminare gli snapshot</span><span class="sxs-lookup"><span data-stu-id="05508-142">Delete snapshots</span></span>
<span data-ttu-id="05508-143">Non è possibile eliminare un BLOB contenente snapshot a meno che non si eliminino anche gli snapshot.</span><span class="sxs-lookup"><span data-stu-id="05508-143">You can't delete a blob with snapshots unless the snapshots are also deleted.</span></span> <span data-ttu-id="05508-144">È possibile eliminare uno snapshot singolarmente o specificare di eliminare tutti gli snapshot quando si elimina il BLOB di origine.</span><span class="sxs-lookup"><span data-stu-id="05508-144">You can delete a snapshot individually, or specify that all snapshots be deleted when the source blob is deleted.</span></span> <span data-ttu-id="05508-145">Se si tenta di eliminare un BLOB per il quale esistono ancora degli snapshot, viene restituito un errore.</span><span class="sxs-lookup"><span data-stu-id="05508-145">If you attempt to delete a blob that still has snapshots, an error results.</span></span>

<span data-ttu-id="05508-146">L'esempio seguente illustra come eliminare un BLOB e i relativi snapshot in .NET, dove `blockBlob` è un oggetto di tipo [CloudBlockBlob][dotnet_CloudBlockBlob]:</span><span class="sxs-lookup"><span data-stu-id="05508-146">The following code example shows how to delete a blob and its snapshots in .NET, where `blockBlob` is an object of type [CloudBlockBlob][dotnet_CloudBlockBlob]:</span></span>

```csharp
await blockBlob.DeleteIfExistsAsync(DeleteSnapshotsOption.IncludeSnapshots, null, null, null);
```

## <a name="snapshots-with-azure-premium-storage"></a><span data-ttu-id="05508-147">Snapshot con archiviazione Premium di Azure</span><span class="sxs-lookup"><span data-stu-id="05508-147">Snapshots with Azure Premium Storage</span></span>
<span data-ttu-id="05508-148">Per usare snapshot con Archiviazione Premium è necessario attenersi alle regole seguenti:</span><span class="sxs-lookup"><span data-stu-id="05508-148">When using snapshots with Premium Storage, the following rules apply:</span></span>

* <span data-ttu-id="05508-149">Il numero massimo di snapshot per BLOB di pagine in un account di archiviazione Premium è 100.</span><span class="sxs-lookup"><span data-stu-id="05508-149">The maximum number of snapshots per page blob in a premium storage account is 100.</span></span> <span data-ttu-id="05508-150">Se si supera questo limite, l'operazione Snapshot BLOB restituisce il codice errore 409 (`SnapshotCountExceeded`).</span><span class="sxs-lookup"><span data-stu-id="05508-150">If that limit is exceeded, the Snapshot Blob operation returns error code 409 (`SnapshotCountExceeded`).</span></span>
* <span data-ttu-id="05508-151">È possibile creare uno snapshot di un BLOB di pagine in un account di archiviazione Premium una volta ogni 10 minuti.</span><span class="sxs-lookup"><span data-stu-id="05508-151">You can take a snapshot of a page blob in a premium storage account once every 10 minutes.</span></span> <span data-ttu-id="05508-152">Se si supera questa frequenza, l'operazione Snapshot BLOB restituisce il codice errore 409 (`SnapshotOperationRateExceeded`).</span><span class="sxs-lookup"><span data-stu-id="05508-152">If that rate is exceeded, the Snapshot Blob operation returns error code 409 (`SnapshotOperationRateExceeded`).</span></span>
* <span data-ttu-id="05508-153">Per leggere uno snapshot, è possibile usare l'operazione Copy BLOB per copiare uno snapshot in un altro BLOB di pagine nell'account.</span><span class="sxs-lookup"><span data-stu-id="05508-153">To read a snapshot, you can use the Copy Blob operation to copy a snapshot to another page blob in the account.</span></span> <span data-ttu-id="05508-154">Il BLOB di destinazione per l'operazione di copia non deve contenere snapshot.</span><span class="sxs-lookup"><span data-stu-id="05508-154">The destination blob for the copy operation must not have any existing snapshots.</span></span> <span data-ttu-id="05508-155">Se il BLOB di destinazione contiene snapshot, l'operazione Copy BLOB restituisce il codice errore 409 (`SnapshotsPresent`).</span><span class="sxs-lookup"><span data-stu-id="05508-155">If the destination blob does have snapshots, then the Copy Blob operation returns error code 409 (`SnapshotsPresent`).</span></span>

## <a name="return-the-absolute-uri-to-a-snapshot"></a><span data-ttu-id="05508-156">Restituire l'URI assoluto a uno snapshot</span><span class="sxs-lookup"><span data-stu-id="05508-156">Return the absolute URI to a snapshot</span></span>
<span data-ttu-id="05508-157">Questo esempio di codice C# consente di creare uno snapshot e scrive l'URI assoluto per la posizione primaria.</span><span class="sxs-lookup"><span data-stu-id="05508-157">This C# code example creates a snapshot and writes out the absolute URI for the primary location.</span></span>

```csharp
//Create the blob service client object.
const string ConnectionString = "DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key";

CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConnectionString);
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

//Get a reference to a container.
CloudBlobContainer container = blobClient.GetContainerReference("sample-container");
container.CreateIfNotExists();

//Get a reference to a blob.
CloudBlockBlob blob = container.GetBlockBlobReference("sampleblob.txt");
blob.UploadText("This is a blob.");

//Create a snapshot of the blob and write out its primary URI.
CloudBlockBlob blobSnapshot = blob.CreateSnapshot();
Console.WriteLine(blobSnapshot.SnapshotQualifiedStorageUri.PrimaryUri);
```

## <a name="understand-how-snapshots-accrue-charges"></a><span data-ttu-id="05508-158">Informazioni sull'incremento dei costi dovuto agli snapshot</span><span class="sxs-lookup"><span data-stu-id="05508-158">Understand how snapshots accrue charges</span></span>
<span data-ttu-id="05508-159">La creazione di uno snapshot, una copia di sola lettura di un BLOB, può dar luogo a costi di archiviazione dei dati aggiuntivi sul conto.</span><span class="sxs-lookup"><span data-stu-id="05508-159">Creating a snapshot, which is a read-only copy of a blob, can result in additional data storage charges to your account.</span></span> <span data-ttu-id="05508-160">Nel progettare l'applicazione, è importante essere coscienti di come i costi possono aumentare, in modo da poterli ridurre al minimo.</span><span class="sxs-lookup"><span data-stu-id="05508-160">When designing your application, it is important to be aware of how these charges might accrue so that you can minimize costs.</span></span>

### <a name="important-billing-considerations"></a><span data-ttu-id="05508-161">Considerazioni importanti sulla fatturazione</span><span class="sxs-lookup"><span data-stu-id="05508-161">Important billing considerations</span></span>
<span data-ttu-id="05508-162">Nell'elenco seguente sono inclusi i punti principali da considerare quando si crea uno snapshot.</span><span class="sxs-lookup"><span data-stu-id="05508-162">The following list includes key points to consider when creating a snapshot.</span></span>

* <span data-ttu-id="05508-163">Sono previsti costi per l'account di archiviazione per blocchi univoci o pagine, sia che si trovino nel BLOB che nello snapshot.</span><span class="sxs-lookup"><span data-stu-id="05508-163">Your storage account incurs charges for unique blocks or pages, whether they are in the blob or in the snapshot.</span></span> <span data-ttu-id="05508-164">Non sono previsti costi aggiuntivi per gli snapshot associati a un BLOB finché il BLOB su cui si basano non viene aggiornato.</span><span class="sxs-lookup"><span data-stu-id="05508-164">Your account does not incur additional charges for snapshots associated with a blob until you update the blob on which they are based.</span></span> <span data-ttu-id="05508-165">Dopo aver aggiornato il BLOB di base, questo differisce dai relativi snapshot.</span><span class="sxs-lookup"><span data-stu-id="05508-165">After you update the base blob, it diverges from its snapshots.</span></span> <span data-ttu-id="05508-166">In questo caso, vengono addebitati costi per i blocchi univoci o le pagine in ogni BLOB o snapshot.</span><span class="sxs-lookup"><span data-stu-id="05508-166">When this happens, you are charged for the unique blocks or pages in each blob or snapshot.</span></span>
* <span data-ttu-id="05508-167">Quando si sostituisce un blocco all'interno di un BLOB in blocchi, tale blocco viene successivamente addebitato come blocco univoco.</span><span class="sxs-lookup"><span data-stu-id="05508-167">When you replace a block within a block blob, that block is subsequently charged as a unique block.</span></span> <span data-ttu-id="05508-168">Ciò è vero persino se il blocco ha lo stesso ID blocco e la stessa data che ha nello snapshot.</span><span class="sxs-lookup"><span data-stu-id="05508-168">This is true even if the block has the same block ID and the same data as it has in the snapshot.</span></span> <span data-ttu-id="05508-169">Una volta che il blocco viene inviato nuovamente, differisce dalla controparte in ogni snapshot e all'utente verrà addebitato un costo per i relativi dati.</span><span class="sxs-lookup"><span data-stu-id="05508-169">After the block is committed again, it diverges from its counterpart in any snapshot, and you will be charged for its data.</span></span> <span data-ttu-id="05508-170">Lo stesso vale per una pagina in un BLOB di pagine che viene aggiornata con dati identici.</span><span class="sxs-lookup"><span data-stu-id="05508-170">The same holds true for a page in a page blob that's updated with identical data.</span></span>
* <span data-ttu-id="05508-171">Se si sostituisce un BLOB in blocchi tramite chiamata al metodo [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [UploadFromStream][dotnet_UploadFromStream] o [UploadFromByteArray][dotnet_UploadFromByteArray], il metodo sostituisce tutti i blocchi nel BLOB.</span><span class="sxs-lookup"><span data-stu-id="05508-171">Replacing a block blob by calling the [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [UploadFromStream][dotnet_UploadFromStream], or [UploadFromByteArray][dotnet_UploadFromByteArray] method replaces all blocks in the blob.</span></span> <span data-ttu-id="05508-172">Se è presente uno snapshot associato al BLOB, tutti i blocchi del BLOB di base e lo snapshot a questo punto differiranno e all'utente verranno addebitati i costi di tutti i blocchi in entrambi i BLOB.</span><span class="sxs-lookup"><span data-stu-id="05508-172">If you have a snapshot associated with that blob, all blocks in the base blob and snapshot now diverge, and you will be charged for all the blocks in both blobs.</span></span> <span data-ttu-id="05508-173">Questo vale persino se i dati nel BLOB di base e nello snapshot restano identici.</span><span class="sxs-lookup"><span data-stu-id="05508-173">This is true even if the data in the base blob and the snapshot remain identical.</span></span>
* <span data-ttu-id="05508-174">Il servizio BLOB di Azure non dispone dei mezzi per determinare se due blocchi contengono dati identici.</span><span class="sxs-lookup"><span data-stu-id="05508-174">The Azure Blob service does not have a means to determine whether two blocks contain identical data.</span></span> <span data-ttu-id="05508-175">Ogni blocco che viene caricato e inviato viene trattato come univoco, persino se contiene gli stessi dati e ha lo stesso ID blocco.</span><span class="sxs-lookup"><span data-stu-id="05508-175">Each block that is uploaded and committed is treated as unique, even if it has the same data and the same block ID.</span></span> <span data-ttu-id="05508-176">Poiché i costi aumentano per i blocchi univoci, è importante considerare che se si aggiorna un BLOB contenente uno snapshot, si generano altri blocchi univoci e i costi aggiuntivi aumentano.</span><span class="sxs-lookup"><span data-stu-id="05508-176">Because charges accrue for unique blocks, it's important to consider that updating a blob that has a snapshot results in additional unique blocks and additional charges.</span></span>

### <a name="minimize-cost-with-snapshot-management"></a><span data-ttu-id="05508-177">Ridurre al minimo i costi con la gestione degli snapshot</span><span class="sxs-lookup"><span data-stu-id="05508-177">Minimize cost with snapshot management</span></span>

<span data-ttu-id="05508-178">Si consiglia di gestire gli snapshot con attenzione per evitare costi supplementari.</span><span class="sxs-lookup"><span data-stu-id="05508-178">We recommend managing your snapshots carefully to avoid extra charges.</span></span> <span data-ttu-id="05508-179">È possibile seguire queste procedure consigliate per ridurre al minimo i costi che sorgono con l'archiviazione degli snapshot:</span><span class="sxs-lookup"><span data-stu-id="05508-179">You can follow these best practices to help minimize the costs incurred by the storage of your snapshots:</span></span>

* <span data-ttu-id="05508-180">Eliminare e ricreare gli snapshot associati a un BLOB ogni volta che si aggiorna il BLOB, persino se l'aggiornamento viene eseguito con dati identici, a meno che la progettazione dell'applicazione non richieda di mantenerli.</span><span class="sxs-lookup"><span data-stu-id="05508-180">Delete and re-create snapshots associated with a blob whenever you update the blob, even if you are updating with identical data, unless your application design requires that you maintain snapshots.</span></span> <span data-ttu-id="05508-181">Se si eliminano e si ricreano gli snapshot del BLOB, ci si garantisce che il BLOB e gli snapshot non differiscano.</span><span class="sxs-lookup"><span data-stu-id="05508-181">By deleting and re-creating the blob's snapshots, you can ensure that the blob and snapshots do not diverge.</span></span>
* <span data-ttu-id="05508-182">Quando si gestiscono gli snapshot per un BLOB, evitare di chiamare il metodo [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [UploadFromStream][dotnet_UploadFromStream] o [UploadFromByteArray][dotnet_UploadFromByteArray] per aggiornare il BLOB.</span><span class="sxs-lookup"><span data-stu-id="05508-182">If you are maintaining snapshots for a blob, avoid calling [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [UploadFromStream][dotnet_UploadFromStream], or [UploadFromByteArray][dotnet_UploadFromByteArray] to update the blob.</span></span> <span data-ttu-id="05508-183">Questi metodi sostituiscono tutti i blocchi nel BLOB, creando così delle differenze significative tra il BLOB di base e gli snapshot.</span><span class="sxs-lookup"><span data-stu-id="05508-183">These methods replace all of the blocks in the blob, causing your base blob and its snapshots to diverge significantly.</span></span> <span data-ttu-id="05508-184">Aggiornare invece il minor numero possibile di blocchi usando i metodi [PutBlock][dotnet_PutBlock] e [PutBlockList][dotnet_PutBlockList].</span><span class="sxs-lookup"><span data-stu-id="05508-184">Instead, update the fewest possible number of blocks by using the [PutBlock][dotnet_PutBlock] and [PutBlockList][dotnet_PutBlockList] methods.</span></span>

### <a name="snapshot-billing-scenarios"></a><span data-ttu-id="05508-185">Scenari di fatturazione degli snapshot</span><span class="sxs-lookup"><span data-stu-id="05508-185">Snapshot billing scenarios</span></span>
<span data-ttu-id="05508-186">Gli scenari seguenti dimostrano in che modo aumentano i costi per un BLOB in blocchi e i relativi snapshot.</span><span class="sxs-lookup"><span data-stu-id="05508-186">The following scenarios demonstrate how charges accrue for a block blob and its snapshots.</span></span>

<span data-ttu-id="05508-187">**Scenario 1**</span><span class="sxs-lookup"><span data-stu-id="05508-187">**Scenario 1**</span></span>

<span data-ttu-id="05508-188">Nello Scenario 1, il BLOB di base non è stato aggiornato da quanto è stato scattato lo snapshot, pertanto i costi sono relativi sono ai blocchi univoci 1, 2 e 3.</span><span class="sxs-lookup"><span data-stu-id="05508-188">In scenario 1, the base blob has not been updated after the snapshot was taken, so charges are incurred only for unique blocks 1, 2, and 3.</span></span>

![Risorse di archiviazione di Azure](./media/storage-blob-snapshots/storage-blob-snapshots-billing-scenario-1.png)

<span data-ttu-id="05508-190">**Scenario 2**</span><span class="sxs-lookup"><span data-stu-id="05508-190">**Scenario 2**</span></span>

<span data-ttu-id="05508-191">Nello Scenario 2, il BLOB di base è stato aggiornato, ma lo snapshot no.</span><span class="sxs-lookup"><span data-stu-id="05508-191">In scenario 2, the base blob has been updated, but the snapshot has not.</span></span> <span data-ttu-id="05508-192">Il blocco 3 è stato aggiornato, e sebbene contenga gli stessi dati e lo stesso ID, non è lo stesso del blocco 3 nello snapshot.</span><span class="sxs-lookup"><span data-stu-id="05508-192">Block 3 was updated, and even though it contains the same data and the same ID, it is not the same as block 3 in the snapshot.</span></span> <span data-ttu-id="05508-193">Di conseguenza, all'account vengono addebitati quattro blocchi.</span><span class="sxs-lookup"><span data-stu-id="05508-193">As a result, the account is charged for four blocks.</span></span>

![Risorse di archiviazione di Azure](./media/storage-blob-snapshots/storage-blob-snapshots-billing-scenario-2.png)

<span data-ttu-id="05508-195">**Scenario 3**</span><span class="sxs-lookup"><span data-stu-id="05508-195">**Scenario 3**</span></span>

<span data-ttu-id="05508-196">Nello Scenario 3, il BLOB di base è stato aggiornato, ma lo snapshot no.</span><span class="sxs-lookup"><span data-stu-id="05508-196">In scenario 3, the base blob has been updated, but the snapshot has not.</span></span> <span data-ttu-id="05508-197">Il blocco 3 è stato sostituito con il blocco 4 nel BLOB di base, ma lo snapshot continua a riflettere il blocco 3.</span><span class="sxs-lookup"><span data-stu-id="05508-197">Block 3 was replaced with block 4 in the base blob, but the snapshot still reflects block 3.</span></span> <span data-ttu-id="05508-198">Di conseguenza, all'account vengono addebitati quattro blocchi.</span><span class="sxs-lookup"><span data-stu-id="05508-198">As a result, the account is charged for four blocks.</span></span>

![Risorse di archiviazione di Azure](./media/storage-blob-snapshots/storage-blob-snapshots-billing-scenario-3.png)

<span data-ttu-id="05508-200">**Scenario 4**</span><span class="sxs-lookup"><span data-stu-id="05508-200">**Scenario 4**</span></span>

<span data-ttu-id="05508-201">Nello Scenario 4, il BLOB di base è stato completamente aggiornato e non contiene nessuno dei blocchi originali.</span><span class="sxs-lookup"><span data-stu-id="05508-201">In scenario 4, the base blob has been completely updated and contains none of its original blocks.</span></span> <span data-ttu-id="05508-202">Di conseguenza, all'account vengono addebitati tutti gli otto blocchi univoci.</span><span class="sxs-lookup"><span data-stu-id="05508-202">As a result, the account is charged for all eight unique blocks.</span></span> <span data-ttu-id="05508-203">Questo scenario può verificarsi se si usa un metodo di aggiornamento come [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [UploadFromStream][dotnet_UploadFromStream] o [UploadFromByteArray][dotnet_UploadFromByteArray], in quanto questi metodi sostituiscono tutto il contenuto di un BLOB.</span><span class="sxs-lookup"><span data-stu-id="05508-203">This scenario can occur if you are using an update method such as [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [UploadFromStream][dotnet_UploadFromStream], or [UploadFromByteArray][dotnet_UploadFromByteArray], because these methods replace all of the contents of a blob.</span></span>

![Risorse di archiviazione di Azure](./media/storage-blob-snapshots/storage-blob-snapshots-billing-scenario-4.png)

## <a name="next-steps"></a><span data-ttu-id="05508-205">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="05508-205">Next steps</span></span>

* <span data-ttu-id="05508-206">Altre informazioni sull'utilizzo di snapshot di dischi di macchina virtuale (VM) sono disponibili in [Eseguire il backup dei dischi di VM non gestiti con snapshot incrementali](storage-incremental-snapshots.md).</span><span class="sxs-lookup"><span data-stu-id="05508-206">You can find more information about working with virtual machine (VM) disk snapshots in [Back up Azure unmanaged VM disks with incremental snapshots](storage-incremental-snapshots.md)</span></span>

* <span data-ttu-id="05508-207">Per altri esempi di codice che usano l'archiviazione BLOB, vedere [Esempi di codice per Azure](https://azure.microsoft.com/documentation/samples/?service=storage&term=blob).</span><span class="sxs-lookup"><span data-stu-id="05508-207">For additional code examples using Blob storage, see [Azure Code Samples](https://azure.microsoft.com/documentation/samples/?service=storage&term=blob).</span></span> <span data-ttu-id="05508-208">È possibile scaricare un'applicazione di esempio ed eseguirla oppure esaminare il codice in GitHub.</span><span class="sxs-lookup"><span data-stu-id="05508-208">You can download a sample application and run it, or browse the code on GitHub.</span></span>

[dotnet_AccessCondition]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.accesscondition.aspx
[dotnet_CloudBlockBlob]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblockblob.aspx
[dotnet_CreateSnapshotAsync]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblockblob.createsnapshotasync.aspx
[dotnet_HTTPStatusCode]: https://msdn.microsoft.com/library/system.net.httpstatuscode(v=vs.110).aspx
[dotnet_PutBlockList]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblockblob.putblocklist.aspx
[dotnet_PutBlock]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblockblob.putblock.aspx
[dotnet_UploadFromByteArray]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblockblob.uploadfrombytearray.aspx
[dotnet_UploadFromFile]: https://msdn.microsoft.com/library/azure/mt705654.aspx
[dotnet_UploadFromStream]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblockblob.uploadfromstream.aspx
[dotnet_UploadText]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblockblob.uploadtext.aspx