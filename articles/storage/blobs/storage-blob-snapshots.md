---
title: aaaCreate uno snapshot di sola lettura di un blob in archiviazione di Azure | Documenti Microsoft
description: "Informazioni su come toocreate uno snapshot di un tooback blob dei dati blob in un determinato momento. Comprendere come gli snapshot vengono fatturati e come toouse li toominimize addebiti di capacità."
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
ms.openlocfilehash: 57f2e76b8899b8a513688bf148dd13673141d5bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-blob-snapshot"></a><span data-ttu-id="f46f4-104">Creare uno snapshot del BLOB</span><span class="sxs-lookup"><span data-stu-id="f46f4-104">Create a blob snapshot</span></span>

<span data-ttu-id="f46f4-105">Uno snapshot è una versione di sola lettura di un BLOB eseguito in un determinato momento.</span><span class="sxs-lookup"><span data-stu-id="f46f4-105">A snapshot is a read-only version of a blob that's taken at a point in time.</span></span> <span data-ttu-id="f46f4-106">Gli snapshot sono utili per il backup dei BLOB.</span><span class="sxs-lookup"><span data-stu-id="f46f4-106">Snapshots are useful for backing up blobs.</span></span> <span data-ttu-id="f46f4-107">Dopo aver creato uno snapshot, è possibile leggerlo, copiarlo o eliminarlo, ma non modificarlo.</span><span class="sxs-lookup"><span data-stu-id="f46f4-107">After you create a snapshot, you can read, copy, or delete it, but you cannot modify it.</span></span>

<span data-ttu-id="f46f4-108">Uno snapshot di un blob di blob di base tooits identiche, ad eccezione di blob hello URI ha un **DateTime** valore aggiunto ora toohello blob URI tooindicate hello in cui hello dello snapshot.</span><span class="sxs-lookup"><span data-stu-id="f46f4-108">A snapshot of a blob is identical tooits base blob, except that hello blob URI has a **DateTime** value appended toohello blob URI tooindicate hello time at which hello snapshot was taken.</span></span> <span data-ttu-id="f46f4-109">Ad esempio, se l'URI del blob di una pagina è `http://storagesample.core.blob.windows.net/mydrives/myvhd`, hello snapshot URI è simile a troppo`http://storagesample.core.blob.windows.net/mydrives/myvhd?snapshot=2011-03-09T01:42:34.9360000Z`.</span><span class="sxs-lookup"><span data-stu-id="f46f4-109">For example, if a page blob URI is `http://storagesample.core.blob.windows.net/mydrives/myvhd`, hello snapshot URI is similar too`http://storagesample.core.blob.windows.net/mydrives/myvhd?snapshot=2011-03-09T01:42:34.9360000Z`.</span></span>

> [!NOTE]
> <span data-ttu-id="f46f4-110">Tutti gli snapshot condividono l'URI del blob base hello.</span><span class="sxs-lookup"><span data-stu-id="f46f4-110">All snapshots share hello base blob's URI.</span></span> <span data-ttu-id="f46f4-111">Hello solo distinzione tra i blob di base hello e snapshot hello è hello aggiunto **DateTime** valore.</span><span class="sxs-lookup"><span data-stu-id="f46f4-111">hello only distinction between hello base blob and hello snapshot is hello appended **DateTime** value.</span></span>
>

<span data-ttu-id="f46f4-112">Un BLOB può avere un numero qualsiasi di snapshot.</span><span class="sxs-lookup"><span data-stu-id="f46f4-112">A blob can have any number of snapshots.</span></span> <span data-ttu-id="f46f4-113">Gli snapshot vengono mantenuti fino all'eliminazione esplicita.</span><span class="sxs-lookup"><span data-stu-id="f46f4-113">Snapshots persist until they are explicitly deleted.</span></span> <span data-ttu-id="f46f4-114">Uno snapshot non può sopravvivere al relativo BLOB di base.</span><span class="sxs-lookup"><span data-stu-id="f46f4-114">A snapshot cannot outlive its base blob.</span></span> <span data-ttu-id="f46f4-115">È possibile enumerare gli snapshot di hello associati hello blob di base tootrack degli snapshot correnti.</span><span class="sxs-lookup"><span data-stu-id="f46f4-115">You can enumerate hello snapshots associated with hello base blob tootrack your current snapshots.</span></span>

<span data-ttu-id="f46f4-116">Quando si crea uno snapshot di un blob, hello proprietà del sistema del blob vengono copiati toohello snapshot con hello stessi valori.</span><span class="sxs-lookup"><span data-stu-id="f46f4-116">When you create a snapshot of a blob, hello blob's system properties are copied toohello snapshot with hello same values.</span></span> <span data-ttu-id="f46f4-117">metadati del blob base Hello sono copiato toohello dello snapshot, a meno che non si specificano i metadati separato per hello durante la creazione di snapshot.</span><span class="sxs-lookup"><span data-stu-id="f46f4-117">hello base blob's metadata is also copied toohello snapshot, unless you specify separate metadata for hello snapshot when you create it.</span></span>

<span data-ttu-id="f46f4-118">Un lease associati al blob di base hello non influenzano snapshot hello.</span><span class="sxs-lookup"><span data-stu-id="f46f4-118">Any leases associated with hello base blob do not affect hello snapshot.</span></span> <span data-ttu-id="f46f4-119">Non è possibile acquisire un lease in uno snapshot.</span><span class="sxs-lookup"><span data-stu-id="f46f4-119">You cannot acquire a lease on a snapshot.</span></span>

<span data-ttu-id="f46f4-120">Un file VHD è usato toostore hello le informazioni e lo stato per un disco di macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="f46f4-120">A VHD file is used toostore hello current information and status for a VM disk.</span></span> <span data-ttu-id="f46f4-121">È possibile scollegare un disco da all'interno di hello VM o arrestare hello macchina virtuale e quindi eseguire uno snapshot del file di disco rigido virtuale.</span><span class="sxs-lookup"><span data-stu-id="f46f4-121">You can detach a disk from within hello VM or shut down hello VM, and then take a snapshot of its VHD file.</span></span> <span data-ttu-id="f46f4-122">È possibile utilizzare tale file di snapshot successive tooretrieve hello disco rigido virtuale del file in tale punto nel tempo e ricreare hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="f46f4-122">You can use that snapshot file later tooretrieve hello VHD file at that point in time and recreate hello VM.</span></span>

<span data-ttu-id="f46f4-123">Se la crittografia del servizio di archiviazione (SSE) è abilitata per l'account di archiviazione hello in quale hello blob si trova, quindi verranno crittografate a riposo alle istantanee del blob.</span><span class="sxs-lookup"><span data-stu-id="f46f4-123">If Storage Service Encryption (SSE) is enabled for hello storage account in which hello blob resides, then any snapshots taken of that blob will be encrypted at rest.</span></span>

## <a name="create-a-snapshot"></a><span data-ttu-id="f46f4-124">Creare uno snapshot</span><span class="sxs-lookup"><span data-stu-id="f46f4-124">Create a snapshot</span></span>
<span data-ttu-id="f46f4-125">Hello esempio di codice seguente viene illustrato come toocreate uno snapshot utilizzando hello [Azure Storage Client Library per .NET](https://www.nuget.org/packages/WindowsAzure.Storage/).</span><span class="sxs-lookup"><span data-stu-id="f46f4-125">hello following code example shows how toocreate a snapshot by using hello [Azure Storage Client Library for .NET](https://www.nuget.org/packages/WindowsAzure.Storage/).</span></span> <span data-ttu-id="f46f4-126">In questo esempio consente di specificare metadati aggiuntivi per snapshot hello quando viene creato.</span><span class="sxs-lookup"><span data-stu-id="f46f4-126">This example specifies additional metadata for hello snapshot when it is created.</span></span>

```csharp
private static async Task CreateBlockBlobSnapshot(CloudBlobContainer container)
{
    // Create a new block blob in hello container.
    CloudBlockBlob baseBlob = container.GetBlockBlobReference("sample-base-blob.txt");

    // Add blob metadata.
    baseBlob.Metadata.Add("ApproxBlobCreatedDate", DateTime.UtcNow.ToString());

    try
    {
        // Upload hello blob toocreate it, with its metadata.
        await baseBlob.UploadTextAsync(string.Format("Base blob: {0}", baseBlob.Uri.ToString()));

        // Sleep 5 seconds.
        System.Threading.Thread.Sleep(5000);

        // Create a snapshot of hello base blob.
        // Specify metadata at hello time that hello snapshot is created toospecify unique metadata for hello snapshot.
        // If no metadata is specified when hello snapshot is created, hello base blob's metadata is copied toohello snapshot.
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

## <a name="copy-snapshots"></a><span data-ttu-id="f46f4-127">Copiare gli snapshot</span><span class="sxs-lookup"><span data-stu-id="f46f4-127">Copy snapshots</span></span>
<span data-ttu-id="f46f4-128">Le operazioni di copia che interessano BLOB e snapshot si attengono alle seguenti regole:</span><span class="sxs-lookup"><span data-stu-id="f46f4-128">Copy operations involving blobs and snapshots follow these rules:</span></span>

* <span data-ttu-id="f46f4-129">È possibile copiare uno snapshot sul relativo BLOB di base.</span><span class="sxs-lookup"><span data-stu-id="f46f4-129">You can copy a snapshot over its base blob.</span></span> <span data-ttu-id="f46f4-130">La promozione di una posizione toohello snapshot del blob di base hello, è possibile ripristinare una versione precedente di un blob.</span><span class="sxs-lookup"><span data-stu-id="f46f4-130">By promoting a snapshot toohello position of hello base blob, you can restore an earlier version of a blob.</span></span> <span data-ttu-id="f46f4-131">Hello snapshot viene mantenuto, ma i blob di base hello viene sovrascritta con una copia modificabile di snapshot di hello.</span><span class="sxs-lookup"><span data-stu-id="f46f4-131">hello snapshot remains, but hello base blob is overwritten with a writable copy of hello snapshot.</span></span>
* <span data-ttu-id="f46f4-132">È possibile copiare un blob di destinazione tooa snapshot con un nome diverso.</span><span class="sxs-lookup"><span data-stu-id="f46f4-132">You can copy a snapshot tooa destination blob with a different name.</span></span> <span data-ttu-id="f46f4-133">blob di destinazione risultante Hello è un blob scrivibile e non è uno snapshot.</span><span class="sxs-lookup"><span data-stu-id="f46f4-133">hello resulting destination blob is a writable blob and not a snapshot.</span></span>
* <span data-ttu-id="f46f4-134">Quando viene copiato un blob di origine, gli snapshot del blob di origine hello non sono copiati toohello destinazione.</span><span class="sxs-lookup"><span data-stu-id="f46f4-134">When a source blob is copied, any snapshots of hello source blob are not copied toohello destination.</span></span> <span data-ttu-id="f46f4-135">Quando un blob di destinazione viene sovrascritto con una copia, gli snapshot associati al blob di destinazione originale hello rimangono invariati.</span><span class="sxs-lookup"><span data-stu-id="f46f4-135">When a destination blob is overwritten with a copy, any snapshots associated with hello original destination blob remain intact.</span></span>
* <span data-ttu-id="f46f4-136">Quando si crea uno snapshot di un blob in blocchi, elenco dei blocchi eseguito il commit del blob hello è anche snapshot toohello copiato.</span><span class="sxs-lookup"><span data-stu-id="f46f4-136">When you create a snapshot of a block blob, hello blob's committed block list is also copied toohello snapshot.</span></span> <span data-ttu-id="f46f4-137">Eventuali blocchi di cui non è stato eseguito il commit non vengono copiati.</span><span class="sxs-lookup"><span data-stu-id="f46f4-137">Any uncommitted blocks are not copied.</span></span>

## <a name="specify-an-access-condition"></a><span data-ttu-id="f46f4-138">Specificare una condizione di accesso</span><span class="sxs-lookup"><span data-stu-id="f46f4-138">Specify an access condition</span></span>
<span data-ttu-id="f46f4-139">Quando si chiama [CreateSnapshotAsync][dotnet_CreateSnapshotAsync], è possibile specificare una condizione di accesso in modo che hello snapshot viene creato solo se viene soddisfatta una condizione.</span><span class="sxs-lookup"><span data-stu-id="f46f4-139">When you call [CreateSnapshotAsync][dotnet_CreateSnapshotAsync], you can specify an access condition so that hello snapshot is created only if a condition is met.</span></span> <span data-ttu-id="f46f4-140">toospecify una condizione di accesso, utilizzare hello [AccessCondition] [ dotnet_AccessCondition] parametro.</span><span class="sxs-lookup"><span data-stu-id="f46f4-140">toospecify an access condition, use hello [AccessCondition][dotnet_AccessCondition] parameter.</span></span> <span data-ttu-id="f46f4-141">Se non specificato hello condizione non viene soddisfatta, hello snapshot non viene creato e hello servizio Blob restituisce il codice di stato [HTTPStatusCode][dotnet_HTTPStatusCode]. PreconditionFailed.</span><span class="sxs-lookup"><span data-stu-id="f46f4-141">If hello specified condition is not met, hello snapshot is not created, and hello Blob service returns status code [HTTPStatusCode][dotnet_HTTPStatusCode].PreconditionFailed.</span></span>

## <a name="delete-snapshots"></a><span data-ttu-id="f46f4-142">Eliminare gli snapshot</span><span class="sxs-lookup"><span data-stu-id="f46f4-142">Delete snapshots</span></span>
<span data-ttu-id="f46f4-143">È possibile eliminare un blob con snapshot a meno che non vengono eliminati anche gli snapshot hello.</span><span class="sxs-lookup"><span data-stu-id="f46f4-143">You can't delete a blob with snapshots unless hello snapshots are also deleted.</span></span> <span data-ttu-id="f46f4-144">È possibile eliminare uno snapshot singolarmente o consente di eliminare tutti gli snapshot quando viene eliminato il blob di origine hello.</span><span class="sxs-lookup"><span data-stu-id="f46f4-144">You can delete a snapshot individually, or specify that all snapshots be deleted when hello source blob is deleted.</span></span> <span data-ttu-id="f46f4-145">Se si tenta di toodelete un blob che presenta ancora degli snapshot, viene generato un errore.</span><span class="sxs-lookup"><span data-stu-id="f46f4-145">If you attempt toodelete a blob that still has snapshots, an error results.</span></span>

<span data-ttu-id="f46f4-146">Hello seguente esempio di codice viene illustrato come toodelete un blob e i relativi snapshot in .NET, in cui `blockBlob` è un oggetto di tipo [CloudBlockBlob][dotnet_CloudBlockBlob]:</span><span class="sxs-lookup"><span data-stu-id="f46f4-146">hello following code example shows how toodelete a blob and its snapshots in .NET, where `blockBlob` is an object of type [CloudBlockBlob][dotnet_CloudBlockBlob]:</span></span>

```csharp
await blockBlob.DeleteIfExistsAsync(DeleteSnapshotsOption.IncludeSnapshots, null, null, null);
```

## <a name="snapshots-with-azure-premium-storage"></a><span data-ttu-id="f46f4-147">Snapshot con archiviazione Premium di Azure</span><span class="sxs-lookup"><span data-stu-id="f46f4-147">Snapshots with Azure Premium Storage</span></span>
<span data-ttu-id="f46f4-148">Quando si utilizzano snapshot con archiviazione Premium, si applica hello seguenti regole:</span><span class="sxs-lookup"><span data-stu-id="f46f4-148">When using snapshots with Premium Storage, hello following rules apply:</span></span>

* <span data-ttu-id="f46f4-149">numero massimo di Hello di snapshot per ogni blob di pagine in un account di archiviazione premium è 100.</span><span class="sxs-lookup"><span data-stu-id="f46f4-149">hello maximum number of snapshots per page blob in a premium storage account is 100.</span></span> <span data-ttu-id="f46f4-150">Se tale limite viene superato, hello operazione Snapshot Blob restituisce il codice errore 409 (`SnapshotCountExceeded`).</span><span class="sxs-lookup"><span data-stu-id="f46f4-150">If that limit is exceeded, hello Snapshot Blob operation returns error code 409 (`SnapshotCountExceeded`).</span></span>
* <span data-ttu-id="f46f4-151">È possibile creare uno snapshot di un BLOB di pagine in un account di archiviazione Premium una volta ogni 10 minuti.</span><span class="sxs-lookup"><span data-stu-id="f46f4-151">You can take a snapshot of a page blob in a premium storage account once every 10 minutes.</span></span> <span data-ttu-id="f46f4-152">Se la velocità viene superata, hello operazione Snapshot Blob restituisce il codice errore 409 (`SnapshotOperationRateExceeded`).</span><span class="sxs-lookup"><span data-stu-id="f46f4-152">If that rate is exceeded, hello Snapshot Blob operation returns error code 409 (`SnapshotOperationRateExceeded`).</span></span>
* <span data-ttu-id="f46f4-153">tooread uno snapshot, è possibile utilizzare toocopy operazione di copia Blob hello un blob di pagine tooanother snapshot nell'account hello.</span><span class="sxs-lookup"><span data-stu-id="f46f4-153">tooread a snapshot, you can use hello Copy Blob operation toocopy a snapshot tooanother page blob in hello account.</span></span> <span data-ttu-id="f46f4-154">blob di destinazione Hello hello operazione di copia non deve includere snapshot esistenti.</span><span class="sxs-lookup"><span data-stu-id="f46f4-154">hello destination blob for hello copy operation must not have any existing snapshots.</span></span> <span data-ttu-id="f46f4-155">Se il blob di destinazione hello include snapshot, quindi hello operazione Copy Blob restituisce il codice errore 409 (`SnapshotsPresent`).</span><span class="sxs-lookup"><span data-stu-id="f46f4-155">If hello destination blob does have snapshots, then hello Copy Blob operation returns error code 409 (`SnapshotsPresent`).</span></span>

## <a name="return-hello-absolute-uri-tooa-snapshot"></a><span data-ttu-id="f46f4-156">Snapshot tooa URI assoluto di hello restituito</span><span class="sxs-lookup"><span data-stu-id="f46f4-156">Return hello absolute URI tooa snapshot</span></span>
<span data-ttu-id="f46f4-157">Questo esempio di codice c# crea uno snapshot e scrive hello URI assoluto per la posizione primaria hello.</span><span class="sxs-lookup"><span data-stu-id="f46f4-157">This C# code example creates a snapshot and writes out hello absolute URI for hello primary location.</span></span>

```csharp
//Create hello blob service client object.
const string ConnectionString = "DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key";

CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConnectionString);
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

//Get a reference tooa container.
CloudBlobContainer container = blobClient.GetContainerReference("sample-container");
container.CreateIfNotExists();

//Get a reference tooa blob.
CloudBlockBlob blob = container.GetBlockBlobReference("sampleblob.txt");
blob.UploadText("This is a blob.");

//Create a snapshot of hello blob and write out its primary URI.
CloudBlockBlob blobSnapshot = blob.CreateSnapshot();
Console.WriteLine(blobSnapshot.SnapshotQualifiedStorageUri.PrimaryUri);
```

## <a name="understand-how-snapshots-accrue-charges"></a><span data-ttu-id="f46f4-158">Informazioni sull'incremento dei costi dovuto agli snapshot</span><span class="sxs-lookup"><span data-stu-id="f46f4-158">Understand how snapshots accrue charges</span></span>
<span data-ttu-id="f46f4-159">Creazione di uno snapshot, che è una copia di sola lettura di un blob, può comportare account tooyour costi di archiviazione dati aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="f46f4-159">Creating a snapshot, which is a read-only copy of a blob, can result in additional data storage charges tooyour account.</span></span> <span data-ttu-id="f46f4-160">Quando si progetta l'applicazione, è importante toobe conoscenza di come questi potrebbe delle spese in modo che è possibile ridurre i costi.</span><span class="sxs-lookup"><span data-stu-id="f46f4-160">When designing your application, it is important toobe aware of how these charges might accrue so that you can minimize costs.</span></span>

### <a name="important-billing-considerations"></a><span data-ttu-id="f46f4-161">Considerazioni importanti sulla fatturazione</span><span class="sxs-lookup"><span data-stu-id="f46f4-161">Important billing considerations</span></span>
<span data-ttu-id="f46f4-162">Hello seguente elenco include i punti chiave tooconsider durante la creazione di uno snapshot.</span><span class="sxs-lookup"><span data-stu-id="f46f4-162">hello following list includes key points tooconsider when creating a snapshot.</span></span>

* <span data-ttu-id="f46f4-163">L'account di archiviazione comporta addebiti per blocchi univoci o pagine, siano essi in blob hello o nello snapshot hello.</span><span class="sxs-lookup"><span data-stu-id="f46f4-163">Your storage account incurs charges for unique blocks or pages, whether they are in hello blob or in hello snapshot.</span></span> <span data-ttu-id="f46f4-164">L'account non comporta costi aggiuntivi per gli snapshot associati a un blob finché non si aggiorna il blob hello in cui sono basate.</span><span class="sxs-lookup"><span data-stu-id="f46f4-164">Your account does not incur additional charges for snapshots associated with a blob until you update hello blob on which they are based.</span></span> <span data-ttu-id="f46f4-165">Dopo aver aggiornato i blob di base hello, è diverso dai relativi snapshot.</span><span class="sxs-lookup"><span data-stu-id="f46f4-165">After you update hello base blob, it diverges from its snapshots.</span></span> <span data-ttu-id="f46f4-166">In questo caso, vengono addebitati i hello blocchi o pagine univoche in ogni blob o snapshot.</span><span class="sxs-lookup"><span data-stu-id="f46f4-166">When this happens, you are charged for hello unique blocks or pages in each blob or snapshot.</span></span>
* <span data-ttu-id="f46f4-167">Quando si sostituisce un blocco all'interno di un BLOB in blocchi, tale blocco viene successivamente addebitato come blocco univoco.</span><span class="sxs-lookup"><span data-stu-id="f46f4-167">When you replace a block within a block blob, that block is subsequently charged as a unique block.</span></span> <span data-ttu-id="f46f4-168">Questo vale anche se il blocco di hello è hello stesso ID del blocco e hello stesso dati perché sono nello snapshot hello.</span><span class="sxs-lookup"><span data-stu-id="f46f4-168">This is true even if hello block has hello same block ID and hello same data as it has in hello snapshot.</span></span> <span data-ttu-id="f46f4-169">Dopo il blocco di hello viene eseguito il commit, diverso dalla relativa controparte nello snapshot e verranno addebitati i dati.</span><span class="sxs-lookup"><span data-stu-id="f46f4-169">After hello block is committed again, it diverges from its counterpart in any snapshot, and you will be charged for its data.</span></span> <span data-ttu-id="f46f4-170">Hello che ciò vale anche per una pagina in un blob di pagine viene aggiornato con dati identici.</span><span class="sxs-lookup"><span data-stu-id="f46f4-170">hello same holds true for a page in a page blob that's updated with identical data.</span></span>
* <span data-ttu-id="f46f4-171">Sostituzione di un blob in blocchi dal chiamante hello [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [UploadFromStream] [ dotnet_UploadFromStream], o [UploadFromByteArray] [ dotnet_UploadFromByteArray] metodo sostituisce tutti i blocchi nel blob hello.</span><span class="sxs-lookup"><span data-stu-id="f46f4-171">Replacing a block blob by calling hello [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [UploadFromStream][dotnet_UploadFromStream], or [UploadFromByteArray][dotnet_UploadFromByteArray] method replaces all blocks in hello blob.</span></span> <span data-ttu-id="f46f4-172">Se si dispone di uno snapshot associato al blob, tutti i blocchi nel blob di base hello e snapshot divergono e verrà addebitato per tutti i blocchi di hello in entrambi i BLOB.</span><span class="sxs-lookup"><span data-stu-id="f46f4-172">If you have a snapshot associated with that blob, all blocks in hello base blob and snapshot now diverge, and you will be charged for all hello blocks in both blobs.</span></span> <span data-ttu-id="f46f4-173">Questo vale anche se i dati di hello in blob di base hello e snapshot hello rimangono identici.</span><span class="sxs-lookup"><span data-stu-id="f46f4-173">This is true even if hello data in hello base blob and hello snapshot remain identical.</span></span>
* <span data-ttu-id="f46f4-174">Hello servizio Blob di Azure non dispone di un toodetermine indica se due blocchi contengono dati identici.</span><span class="sxs-lookup"><span data-stu-id="f46f4-174">hello Azure Blob service does not have a means toodetermine whether two blocks contain identical data.</span></span> <span data-ttu-id="f46f4-175">Ogni blocco caricato e il commit viene considerato univoco, anche se dispone di hello stessi dati e hello stesso blocco di ID.</span><span class="sxs-lookup"><span data-stu-id="f46f4-175">Each block that is uploaded and committed is treated as unique, even if it has hello same data and hello same block ID.</span></span> <span data-ttu-id="f46f4-176">Poiché le spese aumentano per blocchi univoci, è importante tooconsider che l'aggiornamento di un blob che presenta uno snapshot comporta altri blocchi univoci e costi aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="f46f4-176">Because charges accrue for unique blocks, it's important tooconsider that updating a blob that has a snapshot results in additional unique blocks and additional charges.</span></span>

### <a name="minimize-cost-with-snapshot-management"></a><span data-ttu-id="f46f4-177">Ridurre al minimo i costi con la gestione degli snapshot</span><span class="sxs-lookup"><span data-stu-id="f46f4-177">Minimize cost with snapshot management</span></span>

<span data-ttu-id="f46f4-178">È consigliabile gestire attentamente gli snapshot tooavoid costi aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="f46f4-178">We recommend managing your snapshots carefully tooavoid extra charges.</span></span> <span data-ttu-id="f46f4-179">È possibile seguire queste procedure consigliate toohelp ridurre al minimo i costi associati hello archiviando hello gli snapshot:</span><span class="sxs-lookup"><span data-stu-id="f46f4-179">You can follow these best practices toohelp minimize hello costs incurred by hello storage of your snapshots:</span></span>

* <span data-ttu-id="f46f4-180">Eliminare e ricreare gli snapshot associati a un blob quando si aggiorna il blob di hello, anche se si sta aggiornando con dati identici, a meno che la progettazione dell'applicazione è necessario mantenere gli snapshot.</span><span class="sxs-lookup"><span data-stu-id="f46f4-180">Delete and re-create snapshots associated with a blob whenever you update hello blob, even if you are updating with identical data, unless your application design requires that you maintain snapshots.</span></span> <span data-ttu-id="f46f4-181">L'eliminazione e ricreazione degli snapshot del blob hello, è possibile garantire che gli snapshot e blob hello non siano diversi.</span><span class="sxs-lookup"><span data-stu-id="f46f4-181">By deleting and re-creating hello blob's snapshots, you can ensure that hello blob and snapshots do not diverge.</span></span>
* <span data-ttu-id="f46f4-182">Se si gestiscono snapshot per un blob, evitare di chiamare [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [ UploadFromStream][dotnet_UploadFromStream], o [UploadFromByteArray] [ dotnet_UploadFromByteArray] blob hello tooupdate.</span><span class="sxs-lookup"><span data-stu-id="f46f4-182">If you are maintaining snapshots for a blob, avoid calling [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [UploadFromStream][dotnet_UploadFromStream], or [UploadFromByteArray][dotnet_UploadFromByteArray] tooupdate hello blob.</span></span> <span data-ttu-id="f46f4-183">Questi metodi sostituiscono tutti i blocchi di hello in blob hello, provocando il blob di base e relativi toodiverge snapshot in modo significativo.</span><span class="sxs-lookup"><span data-stu-id="f46f4-183">These methods replace all of hello blocks in hello blob, causing your base blob and its snapshots toodiverge significantly.</span></span> <span data-ttu-id="f46f4-184">Invece hello minor numero possibile di blocchi di aggiornamento tramite hello [PutBlock] [ dotnet_PutBlock] e [PutBlockList] [ dotnet_PutBlockList] metodi.</span><span class="sxs-lookup"><span data-stu-id="f46f4-184">Instead, update hello fewest possible number of blocks by using hello [PutBlock][dotnet_PutBlock] and [PutBlockList][dotnet_PutBlockList] methods.</span></span>

### <a name="snapshot-billing-scenarios"></a><span data-ttu-id="f46f4-185">Scenari di fatturazione degli snapshot</span><span class="sxs-lookup"><span data-stu-id="f46f4-185">Snapshot billing scenarios</span></span>
<span data-ttu-id="f46f4-186">Hello gli scenari seguenti viene illustrato come delle spese per un blob in blocchi e i relativi snapshot.</span><span class="sxs-lookup"><span data-stu-id="f46f4-186">hello following scenarios demonstrate how charges accrue for a block blob and its snapshots.</span></span>

<span data-ttu-id="f46f4-187">**Scenario 1**</span><span class="sxs-lookup"><span data-stu-id="f46f4-187">**Scenario 1**</span></span>

<span data-ttu-id="f46f4-188">Nello scenario 1, i blob di base hello non è stato aggiornato dopo hello dello snapshot, pertanto le spese vengono addebitate solo per i blocchi univoci 1, 2 e 3.</span><span class="sxs-lookup"><span data-stu-id="f46f4-188">In scenario 1, hello base blob has not been updated after hello snapshot was taken, so charges are incurred only for unique blocks 1, 2, and 3.</span></span>

![Risorse di archiviazione di Azure](./media/storage-blob-snapshots/storage-blob-snapshots-billing-scenario-1.png)

<span data-ttu-id="f46f4-190">**Scenario 2**</span><span class="sxs-lookup"><span data-stu-id="f46f4-190">**Scenario 2**</span></span>

<span data-ttu-id="f46f4-191">Nello scenario 2, hello blob di base è stato aggiornato, ma non è stato snapshot hello.</span><span class="sxs-lookup"><span data-stu-id="f46f4-191">In scenario 2, hello base blob has been updated, but hello snapshot has not.</span></span> <span data-ttu-id="f46f4-192">Il blocco 3 è stato aggiornato e anche se contiene hello stessi dati e hello lo stesso ID, è hello non uguale al blocco 3 nello snapshot hello.</span><span class="sxs-lookup"><span data-stu-id="f46f4-192">Block 3 was updated, and even though it contains hello same data and hello same ID, it is not hello same as block 3 in hello snapshot.</span></span> <span data-ttu-id="f46f4-193">Di conseguenza, l'account di hello vengono addebitati quattro blocchi.</span><span class="sxs-lookup"><span data-stu-id="f46f4-193">As a result, hello account is charged for four blocks.</span></span>

![Risorse di archiviazione di Azure](./media/storage-blob-snapshots/storage-blob-snapshots-billing-scenario-2.png)

<span data-ttu-id="f46f4-195">**Scenario 3**</span><span class="sxs-lookup"><span data-stu-id="f46f4-195">**Scenario 3**</span></span>

<span data-ttu-id="f46f4-196">Nello scenario 3, hello blob di base è stato aggiornato, ma non è stato snapshot hello.</span><span class="sxs-lookup"><span data-stu-id="f46f4-196">In scenario 3, hello base blob has been updated, but hello snapshot has not.</span></span> <span data-ttu-id="f46f4-197">Il blocco 3 è stato sostituito con il blocco 4 nel blob di base hello ma hello snapshot riflette ancora il blocco 3.</span><span class="sxs-lookup"><span data-stu-id="f46f4-197">Block 3 was replaced with block 4 in hello base blob, but hello snapshot still reflects block 3.</span></span> <span data-ttu-id="f46f4-198">Di conseguenza, l'account di hello vengono addebitati quattro blocchi.</span><span class="sxs-lookup"><span data-stu-id="f46f4-198">As a result, hello account is charged for four blocks.</span></span>

![Risorse di archiviazione di Azure](./media/storage-blob-snapshots/storage-blob-snapshots-billing-scenario-3.png)

<span data-ttu-id="f46f4-200">**Scenario 4**</span><span class="sxs-lookup"><span data-stu-id="f46f4-200">**Scenario 4**</span></span>

<span data-ttu-id="f46f4-201">Nello scenario 4, i blob di base hello è stato completamente aggiornato e contiene nessuno dei blocchi originali.</span><span class="sxs-lookup"><span data-stu-id="f46f4-201">In scenario 4, hello base blob has been completely updated and contains none of its original blocks.</span></span> <span data-ttu-id="f46f4-202">Di conseguenza, hello viene addebitato per tutti e otto i blocchi univoci.</span><span class="sxs-lookup"><span data-stu-id="f46f4-202">As a result, hello account is charged for all eight unique blocks.</span></span> <span data-ttu-id="f46f4-203">Questo scenario può verificarsi se si utilizza un metodo di aggiornamento, ad esempio [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [ UploadFromStream][dotnet_UploadFromStream], o [UploadFromByteArray][dotnet_UploadFromByteArray], poiché questi metodi sostituiscono tutto il contenuto di hello di un blob.</span><span class="sxs-lookup"><span data-stu-id="f46f4-203">This scenario can occur if you are using an update method such as [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [UploadFromStream][dotnet_UploadFromStream], or [UploadFromByteArray][dotnet_UploadFromByteArray], because these methods replace all of hello contents of a blob.</span></span>

![Risorse di archiviazione di Azure](./media/storage-blob-snapshots/storage-blob-snapshots-billing-scenario-4.png)

## <a name="next-steps"></a><span data-ttu-id="f46f4-205">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f46f4-205">Next steps</span></span>

* <span data-ttu-id="f46f4-206">Altre informazioni sull'utilizzo di snapshot di dischi di macchina virtuale (VM) sono disponibili in [Eseguire il backup dei dischi di VM non gestiti con snapshot incrementali](../../virtual-machines/windows/incremental-snapshots.md).</span><span class="sxs-lookup"><span data-stu-id="f46f4-206">You can find more information about working with virtual machine (VM) disk snapshots in [Back up Azure unmanaged VM disks with incremental snapshots](../../virtual-machines/windows/incremental-snapshots.md)</span></span>

* <span data-ttu-id="f46f4-207">Per altri esempi di codice che usano l'archiviazione BLOB, vedere [Esempi di codice per Azure](https://azure.microsoft.com/documentation/samples/?service=storage&term=blob).</span><span class="sxs-lookup"><span data-stu-id="f46f4-207">For additional code examples using Blob storage, see [Azure Code Samples](https://azure.microsoft.com/documentation/samples/?service=storage&term=blob).</span></span> <span data-ttu-id="f46f4-208">È possibile scaricare un'applicazione di esempio ed eseguirlo o esaminare il codice hello su GitHub.</span><span class="sxs-lookup"><span data-stu-id="f46f4-208">You can download a sample application and run it, or browse hello code on GitHub.</span></span>

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