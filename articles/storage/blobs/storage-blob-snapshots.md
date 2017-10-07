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
# <a name="create-a-blob-snapshot"></a>Creare uno snapshot del BLOB

Uno snapshot è una versione di sola lettura di un BLOB eseguito in un determinato momento. Gli snapshot sono utili per il backup dei BLOB. Dopo aver creato uno snapshot, è possibile leggerlo, copiarlo o eliminarlo, ma non modificarlo.

Uno snapshot di un blob di blob di base tooits identiche, ad eccezione di blob hello URI ha un **DateTime** valore aggiunto ora toohello blob URI tooindicate hello in cui hello dello snapshot. Ad esempio, se l'URI del blob di una pagina è `http://storagesample.core.blob.windows.net/mydrives/myvhd`, hello snapshot URI è simile a troppo`http://storagesample.core.blob.windows.net/mydrives/myvhd?snapshot=2011-03-09T01:42:34.9360000Z`.

> [!NOTE]
> Tutti gli snapshot condividono l'URI del blob base hello. Hello solo distinzione tra i blob di base hello e snapshot hello è hello aggiunto **DateTime** valore.
>

Un BLOB può avere un numero qualsiasi di snapshot. Gli snapshot vengono mantenuti fino all'eliminazione esplicita. Uno snapshot non può sopravvivere al relativo BLOB di base. È possibile enumerare gli snapshot di hello associati hello blob di base tootrack degli snapshot correnti.

Quando si crea uno snapshot di un blob, hello proprietà del sistema del blob vengono copiati toohello snapshot con hello stessi valori. metadati del blob base Hello sono copiato toohello dello snapshot, a meno che non si specificano i metadati separato per hello durante la creazione di snapshot.

Un lease associati al blob di base hello non influenzano snapshot hello. Non è possibile acquisire un lease in uno snapshot.

Un file VHD è usato toostore hello le informazioni e lo stato per un disco di macchina virtuale. È possibile scollegare un disco da all'interno di hello VM o arrestare hello macchina virtuale e quindi eseguire uno snapshot del file di disco rigido virtuale. È possibile utilizzare tale file di snapshot successive tooretrieve hello disco rigido virtuale del file in tale punto nel tempo e ricreare hello macchina virtuale.

Se la crittografia del servizio di archiviazione (SSE) è abilitata per l'account di archiviazione hello in quale hello blob si trova, quindi verranno crittografate a riposo alle istantanee del blob.

## <a name="create-a-snapshot"></a>Creare uno snapshot
Hello esempio di codice seguente viene illustrato come toocreate uno snapshot utilizzando hello [Azure Storage Client Library per .NET](https://www.nuget.org/packages/WindowsAzure.Storage/). In questo esempio consente di specificare metadati aggiuntivi per snapshot hello quando viene creato.

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

## <a name="copy-snapshots"></a>Copiare gli snapshot
Le operazioni di copia che interessano BLOB e snapshot si attengono alle seguenti regole:

* È possibile copiare uno snapshot sul relativo BLOB di base. La promozione di una posizione toohello snapshot del blob di base hello, è possibile ripristinare una versione precedente di un blob. Hello snapshot viene mantenuto, ma i blob di base hello viene sovrascritta con una copia modificabile di snapshot di hello.
* È possibile copiare un blob di destinazione tooa snapshot con un nome diverso. blob di destinazione risultante Hello è un blob scrivibile e non è uno snapshot.
* Quando viene copiato un blob di origine, gli snapshot del blob di origine hello non sono copiati toohello destinazione. Quando un blob di destinazione viene sovrascritto con una copia, gli snapshot associati al blob di destinazione originale hello rimangono invariati.
* Quando si crea uno snapshot di un blob in blocchi, elenco dei blocchi eseguito il commit del blob hello è anche snapshot toohello copiato. Eventuali blocchi di cui non è stato eseguito il commit non vengono copiati.

## <a name="specify-an-access-condition"></a>Specificare una condizione di accesso
Quando si chiama [CreateSnapshotAsync][dotnet_CreateSnapshotAsync], è possibile specificare una condizione di accesso in modo che hello snapshot viene creato solo se viene soddisfatta una condizione. toospecify una condizione di accesso, utilizzare hello [AccessCondition] [ dotnet_AccessCondition] parametro. Se non specificato hello condizione non viene soddisfatta, hello snapshot non viene creato e hello servizio Blob restituisce il codice di stato [HTTPStatusCode][dotnet_HTTPStatusCode]. PreconditionFailed.

## <a name="delete-snapshots"></a>Eliminare gli snapshot
È possibile eliminare un blob con snapshot a meno che non vengono eliminati anche gli snapshot hello. È possibile eliminare uno snapshot singolarmente o consente di eliminare tutti gli snapshot quando viene eliminato il blob di origine hello. Se si tenta di toodelete un blob che presenta ancora degli snapshot, viene generato un errore.

Hello seguente esempio di codice viene illustrato come toodelete un blob e i relativi snapshot in .NET, in cui `blockBlob` è un oggetto di tipo [CloudBlockBlob][dotnet_CloudBlockBlob]:

```csharp
await blockBlob.DeleteIfExistsAsync(DeleteSnapshotsOption.IncludeSnapshots, null, null, null);
```

## <a name="snapshots-with-azure-premium-storage"></a>Snapshot con archiviazione Premium di Azure
Quando si utilizzano snapshot con archiviazione Premium, si applica hello seguenti regole:

* numero massimo di Hello di snapshot per ogni blob di pagine in un account di archiviazione premium è 100. Se tale limite viene superato, hello operazione Snapshot Blob restituisce il codice errore 409 (`SnapshotCountExceeded`).
* È possibile creare uno snapshot di un BLOB di pagine in un account di archiviazione Premium una volta ogni 10 minuti. Se la velocità viene superata, hello operazione Snapshot Blob restituisce il codice errore 409 (`SnapshotOperationRateExceeded`).
* tooread uno snapshot, è possibile utilizzare toocopy operazione di copia Blob hello un blob di pagine tooanother snapshot nell'account hello. blob di destinazione Hello hello operazione di copia non deve includere snapshot esistenti. Se il blob di destinazione hello include snapshot, quindi hello operazione Copy Blob restituisce il codice errore 409 (`SnapshotsPresent`).

## <a name="return-hello-absolute-uri-tooa-snapshot"></a>Snapshot tooa URI assoluto di hello restituito
Questo esempio di codice c# crea uno snapshot e scrive hello URI assoluto per la posizione primaria hello.

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

## <a name="understand-how-snapshots-accrue-charges"></a>Informazioni sull'incremento dei costi dovuto agli snapshot
Creazione di uno snapshot, che è una copia di sola lettura di un blob, può comportare account tooyour costi di archiviazione dati aggiuntivi. Quando si progetta l'applicazione, è importante toobe conoscenza di come questi potrebbe delle spese in modo che è possibile ridurre i costi.

### <a name="important-billing-considerations"></a>Considerazioni importanti sulla fatturazione
Hello seguente elenco include i punti chiave tooconsider durante la creazione di uno snapshot.

* L'account di archiviazione comporta addebiti per blocchi univoci o pagine, siano essi in blob hello o nello snapshot hello. L'account non comporta costi aggiuntivi per gli snapshot associati a un blob finché non si aggiorna il blob hello in cui sono basate. Dopo aver aggiornato i blob di base hello, è diverso dai relativi snapshot. In questo caso, vengono addebitati i hello blocchi o pagine univoche in ogni blob o snapshot.
* Quando si sostituisce un blocco all'interno di un BLOB in blocchi, tale blocco viene successivamente addebitato come blocco univoco. Questo vale anche se il blocco di hello è hello stesso ID del blocco e hello stesso dati perché sono nello snapshot hello. Dopo il blocco di hello viene eseguito il commit, diverso dalla relativa controparte nello snapshot e verranno addebitati i dati. Hello che ciò vale anche per una pagina in un blob di pagine viene aggiornato con dati identici.
* Sostituzione di un blob in blocchi dal chiamante hello [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [UploadFromStream] [ dotnet_UploadFromStream], o [UploadFromByteArray] [ dotnet_UploadFromByteArray] metodo sostituisce tutti i blocchi nel blob hello. Se si dispone di uno snapshot associato al blob, tutti i blocchi nel blob di base hello e snapshot divergono e verrà addebitato per tutti i blocchi di hello in entrambi i BLOB. Questo vale anche se i dati di hello in blob di base hello e snapshot hello rimangono identici.
* Hello servizio Blob di Azure non dispone di un toodetermine indica se due blocchi contengono dati identici. Ogni blocco caricato e il commit viene considerato univoco, anche se dispone di hello stessi dati e hello stesso blocco di ID. Poiché le spese aumentano per blocchi univoci, è importante tooconsider che l'aggiornamento di un blob che presenta uno snapshot comporta altri blocchi univoci e costi aggiuntivi.

### <a name="minimize-cost-with-snapshot-management"></a>Ridurre al minimo i costi con la gestione degli snapshot

È consigliabile gestire attentamente gli snapshot tooavoid costi aggiuntivi. È possibile seguire queste procedure consigliate toohelp ridurre al minimo i costi associati hello archiviando hello gli snapshot:

* Eliminare e ricreare gli snapshot associati a un blob quando si aggiorna il blob di hello, anche se si sta aggiornando con dati identici, a meno che la progettazione dell'applicazione è necessario mantenere gli snapshot. L'eliminazione e ricreazione degli snapshot del blob hello, è possibile garantire che gli snapshot e blob hello non siano diversi.
* Se si gestiscono snapshot per un blob, evitare di chiamare [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [ UploadFromStream][dotnet_UploadFromStream], o [UploadFromByteArray] [ dotnet_UploadFromByteArray] blob hello tooupdate. Questi metodi sostituiscono tutti i blocchi di hello in blob hello, provocando il blob di base e relativi toodiverge snapshot in modo significativo. Invece hello minor numero possibile di blocchi di aggiornamento tramite hello [PutBlock] [ dotnet_PutBlock] e [PutBlockList] [ dotnet_PutBlockList] metodi.

### <a name="snapshot-billing-scenarios"></a>Scenari di fatturazione degli snapshot
Hello gli scenari seguenti viene illustrato come delle spese per un blob in blocchi e i relativi snapshot.

**Scenario 1**

Nello scenario 1, i blob di base hello non è stato aggiornato dopo hello dello snapshot, pertanto le spese vengono addebitate solo per i blocchi univoci 1, 2 e 3.

![Risorse di archiviazione di Azure](./media/storage-blob-snapshots/storage-blob-snapshots-billing-scenario-1.png)

**Scenario 2**

Nello scenario 2, hello blob di base è stato aggiornato, ma non è stato snapshot hello. Il blocco 3 è stato aggiornato e anche se contiene hello stessi dati e hello lo stesso ID, è hello non uguale al blocco 3 nello snapshot hello. Di conseguenza, l'account di hello vengono addebitati quattro blocchi.

![Risorse di archiviazione di Azure](./media/storage-blob-snapshots/storage-blob-snapshots-billing-scenario-2.png)

**Scenario 3**

Nello scenario 3, hello blob di base è stato aggiornato, ma non è stato snapshot hello. Il blocco 3 è stato sostituito con il blocco 4 nel blob di base hello ma hello snapshot riflette ancora il blocco 3. Di conseguenza, l'account di hello vengono addebitati quattro blocchi.

![Risorse di archiviazione di Azure](./media/storage-blob-snapshots/storage-blob-snapshots-billing-scenario-3.png)

**Scenario 4**

Nello scenario 4, i blob di base hello è stato completamente aggiornato e contiene nessuno dei blocchi originali. Di conseguenza, hello viene addebitato per tutti e otto i blocchi univoci. Questo scenario può verificarsi se si utilizza un metodo di aggiornamento, ad esempio [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [ UploadFromStream][dotnet_UploadFromStream], o [UploadFromByteArray][dotnet_UploadFromByteArray], poiché questi metodi sostituiscono tutto il contenuto di hello di un blob.

![Risorse di archiviazione di Azure](./media/storage-blob-snapshots/storage-blob-snapshots-billing-scenario-4.png)

## <a name="next-steps"></a>Passaggi successivi

* Altre informazioni sull'utilizzo di snapshot di dischi di macchina virtuale (VM) sono disponibili in [Eseguire il backup dei dischi di VM non gestiti con snapshot incrementali](../../virtual-machines/windows/incremental-snapshots.md).

* Per altri esempi di codice che usano l'archiviazione BLOB, vedere [Esempi di codice per Azure](https://azure.microsoft.com/documentation/samples/?service=storage&term=blob). È possibile scaricare un'applicazione di esempio ed eseguirlo o esaminare il codice hello su GitHub.

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