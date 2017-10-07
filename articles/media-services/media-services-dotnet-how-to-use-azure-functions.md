---
title: aaaDevelop funzioni di Azure con servizi multimediali
description: Questo argomento viene illustrato come lo sviluppo di funzioni con servizi multimediali di Azure toostart hello portale di Azure.
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 51bdcb01-1846-4e1f-bd90-70020ab471b0
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/21/2017
ms.author: juliako
ms.openlocfilehash: 3b2c2fb498fea399c862dfbdb63033d06cabf6d0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
#<a name="develop-azure-functions-with-media-services"></a>Sviluppare le Funzioni di Azure con Servizi multimediali

Questo argomento viene illustrato come tooget iniziare con la creazione di funzioni di Azure che utilizzano i servizi di supporto. Hello Azure funzione definito in questo argomento consente di monitorare un contenitore di account di archiviazione denominato **input** per i nuovi file MP4. Una volta che viene rilasciato un file in un contenitore di archiviazione hello, trigger blob hello eseguirà la funzione hello.

Se si desidera tooexplore e distribuire le funzioni di Azure esistenti che utilizzano servizi multimediali di Azure, consultare [funzioni di Azure Media Services](https://github.com/Azure-Samples/media-services-dotnet-functions-integration). Il repository contiene esempi che utilizzano servizi multimediali tooshow flussi di lavoro correlati tooingesting contenuto direttamente dall'archiviazione blob, codifica e la scrittura del contenuto nuovamente tooblob archiviazione. Include inoltre esempi di come toomonitor processo le notifiche tramite Webhook e le code di Azure. È inoltre possibile sviluppare le funzioni in base negli esempi di hello hello [funzioni di Azure Media Services](https://github.com/Azure-Samples/media-services-dotnet-functions-integration) repository. le funzioni hello toodeploy, premere hello **distribuire tooAzure** pulsante.

## <a name="prerequisites"></a>Prerequisiti

- Prima di creare la prima funzione, è necessario un account di Azure attivo toohave. Se non si possiede un account di Azure, [sono disponibili account gratuiti](https://azure.microsoft.com/free/).
- Se si intende toocreate Azure funzioni che eseguono azioni per l'account di servizi multimediali di Azure (AMS) o ascolto tooevents inviati da servizi multimediali, è necessario creare un account di sistema AMS, come descritto [qui](media-services-portal-create-account.md).
- Comprensione delle [come toouse Azure funzioni](../azure-functions/functions-overview.md). Inoltre, esaminare:
    - [Associazioni HTTP e webhook in Funzioni di Azure](../azure-functions/functions-triggers-bindings.md)
    - [Come tooconfigure le impostazioni dell'app di Azure (funzione)](../azure-functions/functions-how-to-use-azure-function-app-settings.md)
    
## <a name="considerations"></a>Considerazioni

-  Funzioni di Azure in esecuzione nel piano di consumo hello hanno il timeout di 5 minuti limitare.

## <a name="create-a-function-app"></a>Creare un'app per le funzioni

1. Passare toohello [portale di Azure](http://portal.azure.com) e Accedi con l'account di Azure.
2. Creare un'app per le funzioni come descritto [qui](../azure-functions/functions-create-function-app-portal.md).

>[!NOTE]
> Un account di archiviazione specificato nel hello **StorageConnection** variabile di ambiente (vedere il passaggio successivo hello) deve essere hello stessa area dell'app.

## <a name="configure-function-app-settings"></a>Configurare le impostazioni dell'app per le funzioni

Quando si sviluppano le funzioni di servizi multimediali, è utile tooadd le variabili di ambiente che verranno utilizzate nel corso delle funzioni. le impostazioni dell'app tooconfigure, fare clic su collegamento Configura impostazioni App hello. Per ulteriori informazioni, vedere [come impostazioni dell'app Azure funzione tooconfigure](../azure-functions/functions-how-to-use-azure-function-app-settings.md). 

ad esempio:

![Impostazioni](./media/media-services-azure-functions/media-services-azure-functions001.png)

funzione Hello, definita in questo articolo, si suppone che hello le variabili di ambiente nelle impostazioni di app seguenti:

**AMSAccount**: *nome dell'account AMS* (ad esempio testams)

**AMSKey** : *chiave dell'account AMS* (ad esempio, IHOySnH+XX3LGPfraE5fKPl0EnzvEPKkOPKCr59aiMM=)

**MediaServicesStorageAccountName** : *nome dell'account di archiviazione* (ad esempio, testamsstorage)

**MediaServicesStorageAccountKey** : *chiave dell'account di archiviazione* (ad esempio, xx7RN7mvpcipkuXvn5g7jwxnKh5MwYQ/awZAzkSIxQA8tmCtn93rqobjgjt41Wb0zwTZWeWQHY5kSZF0XXXXXX==)

**StorageConnection** : *connessione di archiviazione* (ad esempio, DefaultEndpointsProtocol=https;AccountName=testamsstorage;AccountKey=xx7RN7mvpcipkuXvn5g7jwxnKh5MwYQ/awZAzkSIxQA8tmCtn93rqobjgjt41Wb0zwTZWeWQHY5kSZF0XXXXX==)

## <a name="create-a-function"></a>Creare una funzione

In seguito alla distribuzione dell'app per le funzioni, questa verrà visualizzata tra le Funzioni di Azure dei **Servizi app**.

1. Selezionare l'app per le funzioni e fare clic su **Nuova funzione**.
2. Scegliere hello **c#** language e **l'elaborazione dati** scenario.
3. Scegliere il modello **BlobTrigger**. Questa funzione verrà attivata ogni volta che un blob viene caricato nel hello **input** contenitore. Hello **input** nome è specificato in hello **percorso**, nel passaggio successivo hello.

    ![input](./media/media-services-azure-functions/media-services-azure-functions004.png)

4. Dopo aver selezionato **BlobTrigger**, hello pagina verranno visualizzati altri controlli.

    ![input](./media/media-services-azure-functions/media-services-azure-functions005.png)

4. Fare clic su **Crea**. 


## <a name="files"></a>File

La funzione di Azure è associata al file del codice e ad altri file descritti in questa sezione. Per impostazione predefinita, una funzione è associata ai file **function.json** e **run.csx** (C#). Sarà necessario tooadd un **Project** file. resto Hello di questa sezione mostra le definizioni di hello per questi file.

![input](./media/media-services-azure-functions/media-services-azure-functions003.png)

### <a name="functionjson"></a>function.json

file function.json Hello definisce l'associazione di funzione hello e altre impostazioni di configurazione. Hello runtime utilizza questo toomonitor gli eventi di file toodetermine hello e come toopass e dati restituiti dalla funzionano esecuzione. Per altre informazioni rivedere [Associazioni HTTP e webhook in Funzioni di Azure](../azure-functions/functions-reference.md#function-code).

>[!NOTE]
>Set hello **disabilitato** proprietà troppo**true** funzione hello tooprevent venga eseguito. 


Di seguito è riportato un esempio di file **function.json**.

    {
    "bindings": [
      {
        "name": "myBlob",
        "type": "blobTrigger",
        "direction": "in",
        "path": "input/{fileName}.mp4",
        "connection": "StorageConnection"
      }
    ],
    "disabled": false
    }

### <a name="projectjson"></a>project.json

file Project JSON Hello contiene dipendenze. Di seguito è riportato un esempio di **Project** pacchetti di file che include i servizi multimediali di Azure .NET hello richiesto da Nuget. Si noti che i numeri di versione di hello verranno modificate con gli aggiornamenti più recenti toohello pacchetti, pertanto è necessario verificare le versioni più recenti di hello. 

    {
      "frameworks": {
        "net46":{
          "dependencies": {
        "windowsazure.mediaservices": "3.8.0.5",
        "windowsazure.mediaservices.extensions": "3.8.0.3"
          }
        }
       }
    }
    
### <a name="runcsx"></a>run.csx

Si tratta di codice hello c# per la funzione.  funzione Hello definita sotto monitoraggi un contenitore di account di archiviazione denominato **input** (che è ciò che è stato specificato nel percorso hello) per i nuovi file MP4. Una volta che viene rilasciato un file in un contenitore di archiviazione hello, trigger blob hello eseguirà la funzione hello.
    
esempio Hello definita in questa sezione viene illustrato 

1. come tooingest un asset in servizi multimediali di un account (copiando un blob in un asset AMS) e 
2. come toosubmit un processo di codifica che utilizza "Il flusso adattivo" del Media Encoder Standard predefinito.

In uno scenario reale hello, è probabile che si desidera che lo stato del processo tootrack e quindi si pubblica l'asset codificato. Per ulteriori informazioni, vedere [servizi multimediali di Azure usare i Webhook toomonitor processo notifiche](media-services-dotnet-check-job-progress-with-webhooks.md). Per altri esempi, vedere [Funzioni di Azure dei Servizi multimediali](https://github.com/Azure-Samples/media-services-dotnet-functions-integration).  

Al termine dell'operazione di definizione della funzione fare clic su **Salva ed esegui**.

    #r "Microsoft.WindowsAzure.Storage"
    #r "Newtonsoft.Json"
    #r "System.Web"

    using System;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    using System.Net;
    using System.Threading;
    using System.Threading.Tasks;
    using System.IO;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Blob;
    using Microsoft.WindowsAzure.Storage.Auth;

    private static readonly string _mediaServicesAccountName = Environment.GetEnvironmentVariable("AMSAccount");
    private static readonly string _mediaServicesAccountKey = Environment.GetEnvironmentVariable("AMSKey");

    static string _storageAccountName = Environment.GetEnvironmentVariable("MediaServicesStorageAccountName");
    static string _storageAccountKey = Environment.GetEnvironmentVariable("MediaServicesStorageAccountKey");

    private static CloudStorageAccount _destinationStorageAccount = null;

    // Field for service context.
    private static CloudMediaContext _context = null;
    private static MediaServicesCredentials _cachedCredentials = null;

    public static void Run(CloudBlockBlob myBlob, string fileName, TraceWriter log)
    {
        // NOTE that hello variables {fileName} here come from hello path setting in function.json
        // and are passed into hello  Run method signature above. We can use this toomake decisions on what type of file
        // was dropped into hello input container for hello function. 

        // No need toodo any Retry strategy in this function, By default, hello SDK calls a function up too5 times for a 
        // given blob. If hello fifth try fails, hello SDK adds a message tooa queue named webjobs-blobtrigger-poison.

        log.Info($"C# Blob trigger function processed: {fileName}.mp4");
        log.Info($"Using Azure Media Services account : {_mediaServicesAccountName}");


        try
        {
        // Create and cache hello Media Services credentials in a static class variable.
        _cachedCredentials = new MediaServicesCredentials(
                _mediaServicesAccountName,
                _mediaServicesAccountKey);

        // Used hello chached credentials toocreate CloudMediaContext.
        _context = new CloudMediaContext(_cachedCredentials);

        // Step 1:  Copy hello Blob into a new Input Asset for hello Job
        // ***NOTE: Ideally we would have a method tooingest a Blob directly here somehow. 
        // using code from this sample - https://azure.microsoft.com/en-us/documentation/articles/media-services-copying-existing-blob/

        StorageCredentials mediaServicesStorageCredentials =
            new StorageCredentials(_storageAccountName, _storageAccountKey);

        IAsset newAsset = CreateAssetFromBlob(myBlob, fileName, log).GetAwaiter().GetResult();

        // Step 2: Create an Encoding Job

        // Declare a new encoding job with hello Standard encoder
        IJob job = _context.Jobs.Create("Azure Function - MES Job");

        // Get a media processor reference, and pass tooit hello name of hello 
        // processor toouse for hello specific task.
        IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

        // Create a task with hello encoding details, using a custom preset
        ITask task = job.Tasks.AddNew("Encode with Adaptive Streaming",
            processor,
            "Adaptive Streaming",
            TaskOptions.None); 

        // Specify hello input asset toobe encoded.
        task.InputAssets.Add(newAsset);

        // Add an output asset toocontain hello results of hello job. 
        // This output is specified as AssetCreationOptions.None, which 
        // means hello output asset is not encrypted. 
        task.OutputAssets.AddNew(fileName, AssetCreationOptions.None);

        job.Submit();
        log.Info("Job Submitted");

        }
        catch (Exception ex)
        {
        log.Error("ERROR: failed.");
        log.Info($"StackTrace : {ex.StackTrace}");
        throw ex;
        }
    }

    private static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
    {
        var processor = _context.MediaProcessors.Where(p => p.Name == mediaProcessorName).
        ToList().OrderBy(p => new Version(p.Version)).LastOrDefault();

        if (processor == null)
        throw new ArgumentException(string.Format("Unknown media processor", mediaProcessorName));

        return processor;
    }


    public static async Task<IAsset> CreateAssetFromBlob(CloudBlockBlob blob, string assetName, TraceWriter log){
        IAsset newAsset = null;

        try{
            Task<IAsset> copyAssetTask = CreateAssetFromBlobAsync(blob, assetName, log);
            newAsset = await copyAssetTask;
            log.Info($"Asset Copied : {newAsset.Id}");
        }
        catch(Exception ex){
            log.Info("Copy Failed");
            log.Info($"ERROR : {ex.Message}");
            throw ex;
        }

        return newAsset;
    }

    /// <summary>
    /// Creates a new asset and copies blobs from hello specifed storage account.
    /// </summary>
    /// <param name="blob">hello specified blob.</param>
    /// <returns>hello new asset.</returns>
    public static async Task<IAsset> CreateAssetFromBlobAsync(CloudBlockBlob blob, string assetName, TraceWriter log)
    {
         //Get a reference toohello storage account that is associated with hello Media Services account. 
        StorageCredentials mediaServicesStorageCredentials =
        new StorageCredentials(_storageAccountName, _storageAccountKey);
        _destinationStorageAccount = new CloudStorageAccount(mediaServicesStorageCredentials, false);

        // Create a new asset. 
        var asset = _context.Assets.Create(blob.Name, AssetCreationOptions.None);
        log.Info($"Created new asset {asset.Name}");

        IAccessPolicy writePolicy = _context.AccessPolicies.Create("writePolicy",
        TimeSpan.FromHours(4), AccessPermissions.Write);
        ILocator destinationLocator = _context.Locators.CreateLocator(LocatorType.Sas, asset, writePolicy);
        CloudBlobClient destBlobStorage = _destinationStorageAccount.CreateCloudBlobClient();

        // Get hello destination asset container reference
        string destinationContainerName = (new Uri(destinationLocator.Path)).Segments[1];
        CloudBlobContainer assetContainer = destBlobStorage.GetContainerReference(destinationContainerName);

        try{
        assetContainer.CreateIfNotExists();
        }
        catch (Exception ex)
        {
        log.Error ("ERROR:" + ex.Message);
        }

        log.Info("Created asset.");

        // Get hold of hello destination blob
        CloudBlockBlob destinationBlob = assetContainer.GetBlockBlobReference(blob.Name);

        // Copy Blob
        try
        {
        using (var stream = await blob.OpenReadAsync()) 
        {            
            await destinationBlob.UploadFromStreamAsync(stream);          
        }

        log.Info("Copy Complete.");

        var assetFile = asset.AssetFiles.Create(blob.Name);
        assetFile.ContentFileSize = blob.Properties.Length;
        assetFile.IsPrimary = true;
        assetFile.Update();
        asset.Update();
        }
        catch (Exception ex)
        {
        log.Error(ex.Message);
        log.Info (ex.StackTrace);
        log.Info ("Copy Failed.");
        throw;
        }

        destinationLocator.Delete();
        writePolicy.Delete();

        return asset;
    }
##<a name="test-your-function"></a>Testare la funzione

tootest della funzione, è necessario un file MP4 in hello tooupload **input** contenitore hello dell'account di archiviazione specificato nella stringa di connessione hello.  

## <a name="next-step"></a>Passaggio successivo

A questo punto, si è pronti toostart lo sviluppo di un'applicazione di servizi multimediali. 
 
Per ulteriori dettagli ed esempi/soluzioni complete dell'utilizzo di funzioni di Azure e la logica App con i flussi di lavoro di servizi multimediali di Azure toocreate creazione di contenuto personalizzato, vedere hello [esempio integrazione funzioni Media Services .NET su GitHub](https://github.com/Azure-Samples/media-services-dotnet-functions-integration)

Vedere anche [notifiche con .NET di servizi multimediali di Azure usare i Webhook toomonitor processo](media-services-dotnet-check-job-progress-with-webhooks.md). 

## <a name="media-services-learning-paths"></a>Percorsi di apprendimento di Servizi multimediali
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornire commenti e suggerimenti
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

