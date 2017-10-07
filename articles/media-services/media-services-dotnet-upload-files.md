---
title: i file in un account di servizi multimediali usando .NET aaaUpload | Documenti Microsoft
description: Informazioni su come tooget multimediali in servizi multimediali tramite la creazione e caricamento di asset.
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: c9c86380-9395-4db8-acea-507c52066f73
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/12/2017
ms.author: juliako
ms.openlocfilehash: 11c8a359b09efe04b54490fd48ac0cd7c366f8b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-into-a-media-services-account-using-net"></a>Caricare file in un account di Servizi multimediali mediante .NET
> [!div class="op_single_selector"]
> * [.NET](media-services-dotnet-upload-files.md)
> * [REST](media-services-rest-upload-files.md)
> * [Portale](media-services-portal-upload-files.md)
> 
> 

In Servizi multimediali i file digitali vengono caricati (o inseriti) in un asset. Hello **Asset** entità può contenere video, audio, immagini, raccolte di anteprime, testo tracce e sottotitoli file (e relativi metadati hello.)  Una volta caricati i file hello, il contenuto è archiviato in modo sicuro nel cloud hello per continuare l'elaborazione e il flusso.

file Hello in asset hello sono denominati **file di Asset**. Hello **AssetFile** istanza e hello effettivo file multimediale sono due oggetti distinti. istanza di AssetFile Hello contiene i metadati relativi a file di supporto hello, mentre i file di supporto hello contiene hello effettivo contenuto multimediale.

> [!NOTE]
> si applica Hello seguenti considerazioni:
> 
> * Servizi multimediali Usa valore hello hello IAssetFile.Name proprietà durante la creazione di URL per hello streaming del contenuto (ad esempio, http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) Per questo motivo, la codifica percentuale non è consentita. valore di hello Hello **nome** proprietà non può avere uno dei seguenti hello [% riservati per la codifica caratteri](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters):! *' ();: @& = + $, /? % # [] ". Inoltre, può essere presente solo uno '.' per l'estensione del nome file hello.
> * lunghezza Hello del nome di hello non deve essere maggiore di 260 caratteri.
> * È una limite toohello dimensione massima supportata per l'elaborazione in servizi multimediali. Vedere [questo](media-services-quotas-and-limitations.md) per informazioni sulla limitazione delle dimensioni del file hello.
> * È previsto un limite di 1.000.000 di criteri per i diversi criteri AMS (ad esempio per i criteri Locator o ContentKeyAuthorizationPolicy). È consigliabile utilizzare hello stesso ID di criteri, se si utilizza sempre hello stesso giorni accesso le autorizzazioni, ad esempio, i criteri per i localizzatori che sono previsti tooremain sul posto per un lungo periodo (non-caricamento criteri). Per altre informazioni, vedere [questo](media-services-dotnet-manage-entities.md#limit-access-policies) argomento.
> 

Quando si creano asset, è possibile specificare le opzioni di crittografia seguenti hello. 

* **None** : non viene usata alcuna crittografia. Questo è il valore di predefinito hello. Quando si usa questa opzione, il contenuto non è protetto durante il transito, né nell'archiviazione locale.
  Se si prevede di toodeliver un file MP4 tramite download progressivo, usare questa opzione. 
* **CommonEncryption** : usare questa opzione per caricare contenuti già crittografati e protetti con Common Encryption o PlayReady DRM (ad esempio, Smooth Streaming protetto con PlayReady DRM).
* **EnvelopeEncrypted** : usare questa opzione se si sta caricando contenuto HLS crittografato con AES. Si noti che i file hello devono sono stati codificati e crittografati da Transform Manager.
* **StorageEncrypted** : consente di crittografare il contenuto non crittografato in locale utilizzando la crittografia AES a 256 bit e quindi lo carica tooAzure archiviazione dove viene archiviato in forma crittografata. Gli asset protetti con crittografia di archiviazione vengono decrittografati automaticamente e inseriti in un file crittografato sistema precedente tooencoding e, facoltativamente, crittografare nuovamente toouploading precedente come nuovo asset di output. Hello primario per la crittografia di archiviazione viene usata quando si desidera toosecure file multimediali di input di alta qualità applicando una crittografia avanzata rest su disco.
  
    Servizi multimediali offre una crittografia di archiviazione su disco per gli asset, non in rete come Digital Rights Management (DRM).
  
    Se l'asset è protetto con crittografia di archiviazione, è necessario configurare i criteri di distribuzione degli asset. Per altre informazioni, vedere [Procedura: Configurare i criteri di distribuzione degli asset](media-services-dotnet-configure-asset-delivery-policy.md).

Se si specifica per toobe l'asset crittografato con una **CommonEncrypted** opzione o un **EnvelopeEncypted** opzione, sarà necessario tooassociate l'asset con un **ContentKey**. Per ulteriori informazioni, vedere [come un'entità ContentKey toocreate](media-services-dotnet-create-contentkey.md). 

Se si specifica per toobe l'asset crittografato con una **StorageEncrypted** opzione, hello Media Services SDK per .NET verranno creati un **StorateEncrypted** **ContentKey** per il Asset.

Questo argomento viene illustrato come toouse Media Services .NET SDK, nonché i file di Media Services .NET SDK extensions tooupload in un asset di servizi multimediali.

## <a name="upload-a-single-file-with-media-services-net-sdk"></a>Caricare un singolo file con SDK di Servizi multimediali per .NET
codice di esempio Hello seguente utilizza tooupload .NET SDK un singolo file. Hello AccessPolicy e Locator vengono creati e distrutti dalla funzione di caricamento hello. 


        static public IAsset CreateAssetAndUploadSingleFile(AssetCreationOptions assetCreationOptions, string singleFilePath)
        {
            if (!File.Exists(singleFilePath))
            {
                Console.WriteLine("File does not exist.");
                return null;
            }

            var assetName = Path.GetFileNameWithoutExtension(singleFilePath);
            IAsset inputAsset = _context.Assets.Create(assetName, assetCreationOptions);

            var assetFile = inputAsset.AssetFiles.Create(Path.GetFileName(singleFilePath));

            Console.WriteLine("Upload {0}", assetFile.Name);

            assetFile.Upload(singleFilePath);
            Console.WriteLine("Done uploading {0}", assetFile.Name);

            return inputAsset;
        }


## <a name="upload-multiple-files-with-media-services-net-sdk"></a>Caricare più file con SDK di Servizi multimediali per .NET
Hello seguente codice mostra come toocreate un asset e caricare più file.

codice Hello hello seguenti:

* Crea un asset vuoto utilizzando il metodo di CreateEmptyAsset hello definito nel passaggio precedente hello.
* Crea un **AccessPolicy** istanza che definisce le autorizzazioni di hello e la durata dell'asset toohello di accesso.
* Crea un **localizzatore** istanza che fornisce l'asset toohello di accesso.
* Crea un'istanza di **BlobTransferClient** . Questo tipo rappresenta un client che agisce sui hello che BLOB di Azure. In questo esempio viene usato lo stato di caricamento di hello client toomonitor hello. 
* Enumera i file nella directory specificata hello e crea un **AssetFile** istanza per ogni file.
* Caricamenti hello file in servizi multimediali usando hello **UploadAsync** metodo. 

> [!NOTE]
> Utilizzare hello UploadAsync metodo tooensure che non siano bloccate hello chiamate e i file hello vengono caricati in parallelo.
> 
> 

        static public IAsset CreateAssetAndUploadMultipleFiles(AssetCreationOptions assetCreationOptions, string folderPath)
        {
            var assetName = "UploadMultipleFiles_" + DateTime.UtcNow.ToString();

            IAsset asset = _context.Assets.Create(assetName, assetCreationOptions);

            var accessPolicy = _context.AccessPolicies.Create(assetName, TimeSpan.FromDays(30),
                                                                AccessPermissions.Write | AccessPermissions.List);

            var locator = _context.Locators.CreateLocator(LocatorType.Sas, asset, accessPolicy);

            var blobTransferClient = new BlobTransferClient();
            blobTransferClient.NumberOfConcurrentTransfers = 20;
            blobTransferClient.ParallelTransferThreadCount = 20;

            blobTransferClient.TransferProgressChanged += blobTransferClient_TransferProgressChanged;

            var filePaths = Directory.EnumerateFiles(folderPath);

            Console.WriteLine("There are {0} files in {1}", filePaths.Count(), folderPath);

            if (!filePaths.Any())
            {
                throw new FileNotFoundException(String.Format("No files in directory, check folderPath: {0}", folderPath));
            }

            var uploadTasks = new List<Task>();
            foreach (var filePath in filePaths)
            {
                var assetFile = asset.AssetFiles.Create(Path.GetFileName(filePath));
                Console.WriteLine("Created assetFile {0}", assetFile.Name);

                // It is recommended toovalidate AccestFiles before upload. 
                Console.WriteLine("Start uploading of {0}", assetFile.Name);
                uploadTasks.Add(assetFile.UploadAsync(filePath, blobTransferClient, locator, CancellationToken.None));
            }

            Task.WaitAll(uploadTasks.ToArray());
            Console.WriteLine("Done uploading hello files");

            blobTransferClient.TransferProgressChanged -= blobTransferClient_TransferProgressChanged;

            locator.Delete();
            accessPolicy.Delete();

            return asset;
        }

    static void  blobTransferClient_TransferProgressChanged(object sender, BlobTransferProgressChangedEventArgs e)
    {
        if (e.ProgressPercentage > 4) // Avoid startup jitter, as hello upload tasks are added.
        {
            Console.WriteLine("{0}% upload competed for {1}.", e.ProgressPercentage, e.LocalFile);
        }
    }



Quando si carica un numero elevato di asset, prendere in considerazione seguente hello.

* Creare un nuovo oggetto **CloudMediaContext** per thread. Hello **CloudMediaContext** classe non è thread-safe.
* Aumentare NumberOfConcurrentTransfers dal valore predefinito di hello valore 2 tooa superiore come 5. L'impostazione di questa proprietà ha effetto su tutte le istanze di **CloudMediaContext**. 
* Mantenere ParallelTransferThreadCount valore hello predefinito 10.

## <a id="ingest_in_bulk"></a>Inserimento di asset in blocco tramite SDK di Servizi multimediali per .NET
Il caricamento di file di asset di grandi dimensioni costituisce un collo di bottiglia nella creazione di asset. Inserimento di asset in blocco o "L'inserimento in blocco", prevede il disaccoppiamento creazione asset dal processo di caricamento hello. toouse un approccio l'inserimento bulk, creare un manifesto (IngestManifest) che descrive l'asset hello e relativi file associati. Utilizzare quindi il metodo di caricamento hello del contenitore blob la scelta tooupload hello i file associati toohello del manifesto. Servizi multimediali di Microsoft Azure controlla il contenitore di blob hello associato manifesto hello. Quando un file è il contenitore di blob caricato toohello, servizi multimediali di Microsoft Azure completa di creazione degli asset hello in base alla configurazione di hello dell'asset hello nel manifesto hello (entità IngestManifestAsset).

toocreate una nuova entità IngestManifest chiamare il metodo di creazione hello esposto da hello raccolta hello CloudMediaContext le entità Ingestmanifest. Questo metodo creerà una nuova entità IngestManifest con nome hello del manifesto specificato.

    IIngestManifest manifest = context.IngestManifests.Create(name);

Creare asset di hello che verrà associato bulk hello entità IngestManifest. Configurare le opzioni di crittografia hello desiderato nel asset hello per l'inserimento in blocco.

    // Create hello assets that will be associated with this bulk ingest manifest
    IAsset destAsset1 = _context.Assets.Create(name + "_asset_1", AssetCreationOptions.None);
    IAsset destAsset2 = _context.Assets.Create(name + "_asset_2", AssetCreationOptions.None);

Un'entità IngestManifestAsset associa un Asset a un IngestManifest in blocco per l'inserimento in blocco. Inoltre, associa hello AssetFiles che costituiranno ogni Asset. toocreate un'entità IngestManifestAsset, utilizzare il metodo di creazione hello contesto hello del server.

Hello esempio seguente viene illustrato aggiungere due nuove entità Ingestmanifestasset che associano le attività di hello creato in precedenza toohello bulk manifesto di inserimento. Ogni entità IngestManifestAsset associa anche un set di file che verrà caricato per ogni asset durante l'inserimento in blocco.  

    string filename1 = _singleInputMp4Path;
    string filename2 = _primaryFilePath;
    string filename3 = _singleInputFilePath;

    IIngestManifestAsset bulkAsset1 =  manifest.IngestManifestAssets.Create(destAsset1, new[] { filename1 });
    IIngestManifestAsset bulkAsset2 =  manifest.IngestManifestAssets.Create(destAsset2, new[] { filename2, filename3 });

È possibile utilizzare qualsiasi applicazione client ad alta velocità in grado di caricare hello asset file toohello contenitore di archiviazione blob URI fornito da hello **IIngestManifest.BlobStorageUriForUpload** proprietà dell'entità IngestManifest hello. Un servizio di caricamento ad alta velocità consigliato è l'applicazione [Aspera On Demand for Azure](https://datamarket.azure.com/application/2cdbc511-cb12-4715-9871-c7e7fbbb82a6). È possibile anche scrivere codice i file di asset hello tooupload come illustrato nell'esempio di codice seguente hello.

    static void UploadBlobFile(string destBlobURI, string filename)
    {
        Task copytask = new Task(() =>
        {
            var storageaccount = new CloudStorageAccount(new StorageCredentials(_storageAccountName, _storageAccountKey), true);
            CloudBlobClient blobClient = storageaccount.CreateCloudBlobClient();
            CloudBlobContainer blobContainer = blobClient.GetContainerReference(destBlobURI);

            string[] splitfilename = filename.Split('\\');
            var blob = blobContainer.GetBlockBlobReference(splitfilename[splitfilename.Length - 1]);

            using (var stream = System.IO.File.OpenRead(filename))
                blob.UploadFromStream(stream);

            lock (consoleWriteLock)
            {
                Console.WriteLine("Upload for {0} completed.", filename);
            }
        });

        copytask.Start();
    }

codice di Hello per caricare il file di asset hello per l'esempio hello usato in questo argomento è illustrato nell'esempio di codice seguente hello.

    UploadBlobFile(manifest.BlobStorageUriForUpload, filename1);
    UploadBlobFile(manifest.BlobStorageUriForUpload, filename2);
    UploadBlobFile(manifest.BlobStorageUriForUpload, filename3);


È possibile determinare lo stato di avanzamento hello hello l'inserimento in blocco per tutti gli asset associati a un **IngestManifest** eseguendo il polling delle proprietà di statistiche hello di hello **IngestManifest**. In informazioni sullo stato di tooupdate ordine, è necessario utilizzare un nuovo **CloudMediaContext** ogni volta che si esegue il polling proprietà Statistics hello.

Hello esempio seguente viene illustrato il polling di un'entità IngestManifest dal relativo **Id**.

    static void MonitorBulkManifest(string manifestID)
    {
       bool bContinue = true;
       while (bContinue)
       {
          CloudMediaContext context = GetContext();
          IIngestManifest manifest = context.IngestManifests.Where(m => m.Id == manifestID).FirstOrDefault();

          if (manifest != null)
          {
             lock(consoleWriteLock)
             {
                Console.WriteLine("\nWaiting on all file uploads.");
                Console.WriteLine("PendingFilesCount  : {0}", manifest.Statistics.PendingFilesCount);
                Console.WriteLine("FinishedFilesCount : {0}", manifest.Statistics.FinishedFilesCount);
                Console.WriteLine("{0}% complete.\n", (float)manifest.Statistics.FinishedFilesCount / (float)(manifest.Statistics.FinishedFilesCount + manifest.Statistics.PendingFilesCount) * 100);

                if (manifest.Statistics.PendingFilesCount == 0)
                {
                   Console.WriteLine("Completed\n");
                   bContinue = false;
                }
             }

             if (manifest.Statistics.FinishedFilesCount < manifest.Statistics.PendingFilesCount)
                Thread.Sleep(60000);
          }
          else // Manifest is null
             bContinue = false;
       }
    }



## <a name="upload-files-using-net-sdk-extensions"></a>Caricare file mediante le estensioni dell'SDK per .NET
esempio Hello riportato di seguito viene illustrato come tooupload un singolo file con estensioni del SDK .NET. In questo caso hello **CreateFromFile** viene usato il metodo, ma è disponibile anche la versione asincrona di hello (**CreateFromFileAsync**). Hello **CreateFromFile** metodo consente di specificare il nome di file hello, opzione di crittografia e un callback in hello tooreport ordine caricare lo stato di avanzamento del file hello.

    static public IAsset UploadFile(string fileName, AssetCreationOptions options)
    {
        IAsset inputAsset = _context.Assets.CreateFromFile(
            fileName,
            options,
            (af, p) =>
            {
                Console.WriteLine("Uploading '{0}' - Progress: {1:0.##}%", af.Name, p.Progress);
            });

        Console.WriteLine("Asset {0} created.", inputAsset.Id);

        return inputAsset;
    }

Hello esempio seguente chiama la funzione UploadFile e specifica la crittografia di archiviazione come opzione di creazione di asset hello.  

    var asset = UploadFile(@"C:\VideoFiles\BigBuckBunny.mp4", AssetCreationOptions.StorageEncrypted);

## <a name="next-steps"></a>Passaggi successivi

Ora è possibile codificare gli asset caricati. Per altre informazioni, vedere [Encode assets](media-services-portal-encode.md)(Codificare gli asset).

È possibile utilizzare anche funzioni Azure tootrigger un processo di codifica in base a un file in arrivo nel contenitore hello configurato. Per altre informazioni, vedere [questo esempio](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ ).

## <a name="media-services-learning-paths"></a>Percorsi di apprendimento di Servizi multimediali
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornire commenti e suggerimenti
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-step"></a>Passaggio successivo
Ora che è stato caricato un asset tooMedia Services, visitare toohello [come un processore di contenuti multimediali tooGet] [ How tooGet a Media Processor] argomento.

[How tooGet a Media Processor]: media-services-get-media-processor.md

