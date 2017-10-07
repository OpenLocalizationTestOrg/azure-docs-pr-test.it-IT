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
#<a name="develop-azure-functions-with-media-services"></a><span data-ttu-id="ab6ca-103">Sviluppare le Funzioni di Azure con Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="ab6ca-103">Develop Azure Functions with Media Services</span></span>

<span data-ttu-id="ab6ca-104">Questo argomento viene illustrato come tooget iniziare con la creazione di funzioni di Azure che utilizzano i servizi di supporto.</span><span class="sxs-lookup"><span data-stu-id="ab6ca-104">This topic shows you how tooget started with creating Azure Functions that use Media Services.</span></span> <span data-ttu-id="ab6ca-105">Hello Azure funzione definito in questo argomento consente di monitorare un contenitore di account di archiviazione denominato **input** per i nuovi file MP4.</span><span class="sxs-lookup"><span data-stu-id="ab6ca-105">hello Azure Function defined in this topic monitors a storage account container named **input** for new MP4 files.</span></span> <span data-ttu-id="ab6ca-106">Una volta che viene rilasciato un file in un contenitore di archiviazione hello, trigger blob hello eseguirà la funzione hello.</span><span class="sxs-lookup"><span data-stu-id="ab6ca-106">Once a file is dropped into hello storage container, hello blob trigger will execute hello function.</span></span>

<span data-ttu-id="ab6ca-107">Se si desidera tooexplore e distribuire le funzioni di Azure esistenti che utilizzano servizi multimediali di Azure, consultare [funzioni di Azure Media Services](https://github.com/Azure-Samples/media-services-dotnet-functions-integration).</span><span class="sxs-lookup"><span data-stu-id="ab6ca-107">If you want tooexplore and deploy existing Azure Functions that use Azure Media Services, check out [Media Services Azure Functions](https://github.com/Azure-Samples/media-services-dotnet-functions-integration).</span></span> <span data-ttu-id="ab6ca-108">Il repository contiene esempi che utilizzano servizi multimediali tooshow flussi di lavoro correlati tooingesting contenuto direttamente dall'archiviazione blob, codifica e la scrittura del contenuto nuovamente tooblob archiviazione.</span><span class="sxs-lookup"><span data-stu-id="ab6ca-108">This repository contains examples that use Media Services tooshow workflows related tooingesting content directly from blob storage, encoding, and writing content back tooblob storage.</span></span> <span data-ttu-id="ab6ca-109">Include inoltre esempi di come toomonitor processo le notifiche tramite Webhook e le code di Azure.</span><span class="sxs-lookup"><span data-stu-id="ab6ca-109">It also includes examples of how toomonitor job notifications via WebHooks and Azure Queues.</span></span> <span data-ttu-id="ab6ca-110">È inoltre possibile sviluppare le funzioni in base negli esempi di hello hello [funzioni di Azure Media Services](https://github.com/Azure-Samples/media-services-dotnet-functions-integration) repository.</span><span class="sxs-lookup"><span data-stu-id="ab6ca-110">You can also develop your Functions based on hello examples in hello [Media Services Azure Functions](https://github.com/Azure-Samples/media-services-dotnet-functions-integration) repository.</span></span> <span data-ttu-id="ab6ca-111">le funzioni hello toodeploy, premere hello **distribuire tooAzure** pulsante.</span><span class="sxs-lookup"><span data-stu-id="ab6ca-111">toodeploy hello functions, press hello **Deploy tooAzure** button.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ab6ca-112">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="ab6ca-112">Prerequisites</span></span>

- <span data-ttu-id="ab6ca-113">Prima di creare la prima funzione, è necessario un account di Azure attivo toohave.</span><span class="sxs-lookup"><span data-stu-id="ab6ca-113">Before you can create your first function, you need toohave an active Azure account.</span></span> <span data-ttu-id="ab6ca-114">Se non si possiede un account di Azure, [sono disponibili account gratuiti](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="ab6ca-114">If you don't already have an Azure account, [free accounts are available](https://azure.microsoft.com/free/).</span></span>
- <span data-ttu-id="ab6ca-115">Se si intende toocreate Azure funzioni che eseguono azioni per l'account di servizi multimediali di Azure (AMS) o ascolto tooevents inviati da servizi multimediali, è necessario creare un account di sistema AMS, come descritto [qui](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="ab6ca-115">If you are going toocreate Azure Functions that perform actions on your Azure Media Services (AMS) account or listen tooevents sent by Media Services, you should create an AMS account, as described [here](media-services-portal-create-account.md).</span></span>
- <span data-ttu-id="ab6ca-116">Comprensione delle [come toouse Azure funzioni](../azure-functions/functions-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ab6ca-116">Understanding of [how toouse Azure functions](../azure-functions/functions-overview.md).</span></span> <span data-ttu-id="ab6ca-117">Inoltre, esaminare:</span><span class="sxs-lookup"><span data-stu-id="ab6ca-117">Also, review:</span></span>
    - [<span data-ttu-id="ab6ca-118">Associazioni HTTP e webhook in Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="ab6ca-118">Azure functions HTTP and webhook bindings</span></span>](../azure-functions/functions-triggers-bindings.md)
    - [<span data-ttu-id="ab6ca-119">Come tooconfigure le impostazioni dell'app di Azure (funzione)</span><span class="sxs-lookup"><span data-stu-id="ab6ca-119">How tooconfigure Azure Function app settings</span></span>](../azure-functions/functions-how-to-use-azure-function-app-settings.md)
    
## <a name="considerations"></a><span data-ttu-id="ab6ca-120">Considerazioni</span><span class="sxs-lookup"><span data-stu-id="ab6ca-120">Considerations</span></span>

-  <span data-ttu-id="ab6ca-121">Funzioni di Azure in esecuzione nel piano di consumo hello hanno il timeout di 5 minuti limitare.</span><span class="sxs-lookup"><span data-stu-id="ab6ca-121">Azure Functions running under hello Consumption plan have 5 minutes timeout limit.</span></span>

## <a name="create-a-function-app"></a><span data-ttu-id="ab6ca-122">Creare un'app per le funzioni</span><span class="sxs-lookup"><span data-stu-id="ab6ca-122">Create a function app</span></span>

1. <span data-ttu-id="ab6ca-123">Passare toohello [portale di Azure](http://portal.azure.com) e Accedi con l'account di Azure.</span><span class="sxs-lookup"><span data-stu-id="ab6ca-123">Go toohello [Azure portal](http://portal.azure.com) and sign-in with your Azure account.</span></span>
2. <span data-ttu-id="ab6ca-124">Creare un'app per le funzioni come descritto [qui](../azure-functions/functions-create-function-app-portal.md).</span><span class="sxs-lookup"><span data-stu-id="ab6ca-124">Create a function app as described [here](../azure-functions/functions-create-function-app-portal.md).</span></span>

>[!NOTE]
> <span data-ttu-id="ab6ca-125">Un account di archiviazione specificato nel hello **StorageConnection** variabile di ambiente (vedere il passaggio successivo hello) deve essere hello stessa area dell'app.</span><span class="sxs-lookup"><span data-stu-id="ab6ca-125">A storage account that you specify in hello **StorageConnection** environment variable (see hello next step) should be in hello same region as your app.</span></span>

## <a name="configure-function-app-settings"></a><span data-ttu-id="ab6ca-126">Configurare le impostazioni dell'app per le funzioni</span><span class="sxs-lookup"><span data-stu-id="ab6ca-126">Configure function app settings</span></span>

<span data-ttu-id="ab6ca-127">Quando si sviluppano le funzioni di servizi multimediali, è utile tooadd le variabili di ambiente che verranno utilizzate nel corso delle funzioni.</span><span class="sxs-lookup"><span data-stu-id="ab6ca-127">When developing Media Services functions, it is handy tooadd environment variables that will be used throughout your functions.</span></span> <span data-ttu-id="ab6ca-128">le impostazioni dell'app tooconfigure, fare clic su collegamento Configura impostazioni App hello.</span><span class="sxs-lookup"><span data-stu-id="ab6ca-128">tooconfigure app settings, click hello Configure App Settings link.</span></span> <span data-ttu-id="ab6ca-129">Per ulteriori informazioni, vedere [come impostazioni dell'app Azure funzione tooconfigure](../azure-functions/functions-how-to-use-azure-function-app-settings.md).</span><span class="sxs-lookup"><span data-stu-id="ab6ca-129">For more information, see  [How tooconfigure Azure Function app settings](../azure-functions/functions-how-to-use-azure-function-app-settings.md).</span></span> 

<span data-ttu-id="ab6ca-130">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="ab6ca-130">For example:</span></span>

![Impostazioni](./media/media-services-azure-functions/media-services-azure-functions001.png)

<span data-ttu-id="ab6ca-132">funzione Hello, definita in questo articolo, si suppone che hello le variabili di ambiente nelle impostazioni di app seguenti:</span><span class="sxs-lookup"><span data-stu-id="ab6ca-132">hello function, defined in this article, assumes you have hello following environment variables in your app settings:</span></span>

<span data-ttu-id="ab6ca-133">**AMSAccount**: *nome dell'account AMS* (ad esempio testams)</span><span class="sxs-lookup"><span data-stu-id="ab6ca-133">**AMSAccount** : *AMS account name* (e.g. testams)</span></span>

<span data-ttu-id="ab6ca-134">**AMSKey** : *chiave dell'account AMS* (ad esempio, IHOySnH+XX3LGPfraE5fKPl0EnzvEPKkOPKCr59aiMM=)</span><span class="sxs-lookup"><span data-stu-id="ab6ca-134">**AMSKey** : *AMS account key* (e.g. IHOySnH+XX3LGPfraE5fKPl0EnzvEPKkOPKCr59aiMM=)</span></span>

<span data-ttu-id="ab6ca-135">**MediaServicesStorageAccountName** : *nome dell'account di archiviazione* (ad esempio, testamsstorage)</span><span class="sxs-lookup"><span data-stu-id="ab6ca-135">**MediaServicesStorageAccountName** : *storage account name* (e.g., testamsstorage)</span></span>

<span data-ttu-id="ab6ca-136">**MediaServicesStorageAccountKey** : *chiave dell'account di archiviazione* (ad esempio, xx7RN7mvpcipkuXvn5g7jwxnKh5MwYQ/awZAzkSIxQA8tmCtn93rqobjgjt41Wb0zwTZWeWQHY5kSZF0XXXXXX==)</span><span class="sxs-lookup"><span data-stu-id="ab6ca-136">**MediaServicesStorageAccountKey** : *storage account key* (e.g., xx7RN7mvpcipkuXvn5g7jwxnKh5MwYQ/awZAzkSIxQA8tmCtn93rqobjgjt41Wb0zwTZWeWQHY5kSZF0XXXXXX==)</span></span>

<span data-ttu-id="ab6ca-137">**StorageConnection** : *connessione di archiviazione* (ad esempio, DefaultEndpointsProtocol=https;AccountName=testamsstorage;AccountKey=xx7RN7mvpcipkuXvn5g7jwxnKh5MwYQ/awZAzkSIxQA8tmCtn93rqobjgjt41Wb0zwTZWeWQHY5kSZF0XXXXX==)</span><span class="sxs-lookup"><span data-stu-id="ab6ca-137">**StorageConnection** : *storage connection* (e.g., DefaultEndpointsProtocol=https;AccountName=testamsstorage;AccountKey=xx7RN7mvpcipkuXvn5g7jwxnKh5MwYQ/awZAzkSIxQA8tmCtn93rqobjgjt41Wb0zwTZWeWQHY5kSZF0XXXXX==)</span></span>

## <a name="create-a-function"></a><span data-ttu-id="ab6ca-138">Creare una funzione</span><span class="sxs-lookup"><span data-stu-id="ab6ca-138">Create a function</span></span>

<span data-ttu-id="ab6ca-139">In seguito alla distribuzione dell'app per le funzioni, questa verrà visualizzata tra le Funzioni di Azure dei **Servizi app**.</span><span class="sxs-lookup"><span data-stu-id="ab6ca-139">Once your function app is deployed, you can find it among **App Services** Azure Functions.</span></span>

1. <span data-ttu-id="ab6ca-140">Selezionare l'app per le funzioni e fare clic su **Nuova funzione**.</span><span class="sxs-lookup"><span data-stu-id="ab6ca-140">Select your function app and click **New Function**.</span></span>
2. <span data-ttu-id="ab6ca-141">Scegliere hello **c#** language e **l'elaborazione dati** scenario.</span><span class="sxs-lookup"><span data-stu-id="ab6ca-141">Choose hello **C#** language and **Data Processing** scenario.</span></span>
3. <span data-ttu-id="ab6ca-142">Scegliere il modello **BlobTrigger**.</span><span class="sxs-lookup"><span data-stu-id="ab6ca-142">Choose **BlobTrigger** template.</span></span> <span data-ttu-id="ab6ca-143">Questa funzione verrà attivata ogni volta che un blob viene caricato nel hello **input** contenitore.</span><span class="sxs-lookup"><span data-stu-id="ab6ca-143">This function will be triggered whenever a blob is uploaded into hello **input** container.</span></span> <span data-ttu-id="ab6ca-144">Hello **input** nome è specificato in hello **percorso**, nel passaggio successivo hello.</span><span class="sxs-lookup"><span data-stu-id="ab6ca-144">hello **input** name is specified in hello **Path**, in hello next step.</span></span>

    ![input](./media/media-services-azure-functions/media-services-azure-functions004.png)

4. <span data-ttu-id="ab6ca-146">Dopo aver selezionato **BlobTrigger**, hello pagina verranno visualizzati altri controlli.</span><span class="sxs-lookup"><span data-stu-id="ab6ca-146">Once you select **BlobTrigger**, some more controls will appear on hello page.</span></span>

    ![input](./media/media-services-azure-functions/media-services-azure-functions005.png)

4. <span data-ttu-id="ab6ca-148">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="ab6ca-148">Click **Create**.</span></span> 


## <a name="files"></a><span data-ttu-id="ab6ca-149">File</span><span class="sxs-lookup"><span data-stu-id="ab6ca-149">Files</span></span>

<span data-ttu-id="ab6ca-150">La funzione di Azure è associata al file del codice e ad altri file descritti in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="ab6ca-150">Your Azure function is associated with code files and other files that are described in this section.</span></span> <span data-ttu-id="ab6ca-151">Per impostazione predefinita, una funzione è associata ai file **function.json** e **run.csx** (C#).</span><span class="sxs-lookup"><span data-stu-id="ab6ca-151">By default, a function is associated with **function.json** and **run.csx** (C#) files.</span></span> <span data-ttu-id="ab6ca-152">Sarà necessario tooadd un **Project** file.</span><span class="sxs-lookup"><span data-stu-id="ab6ca-152">You will need tooadd a **project.json** file.</span></span> <span data-ttu-id="ab6ca-153">resto Hello di questa sezione mostra le definizioni di hello per questi file.</span><span class="sxs-lookup"><span data-stu-id="ab6ca-153">hello rest of this section shows hello definitions for these files.</span></span>

![input](./media/media-services-azure-functions/media-services-azure-functions003.png)

### <a name="functionjson"></a><span data-ttu-id="ab6ca-155">function.json</span><span class="sxs-lookup"><span data-stu-id="ab6ca-155">function.json</span></span>

<span data-ttu-id="ab6ca-156">file function.json Hello definisce l'associazione di funzione hello e altre impostazioni di configurazione.</span><span class="sxs-lookup"><span data-stu-id="ab6ca-156">hello function.json file defines hello function bindings and other configuration settings.</span></span> <span data-ttu-id="ab6ca-157">Hello runtime utilizza questo toomonitor gli eventi di file toodetermine hello e come toopass e dati restituiti dalla funzionano esecuzione.</span><span class="sxs-lookup"><span data-stu-id="ab6ca-157">hello runtime uses this file toodetermine hello events toomonitor and how toopass data into and return data from function execution.</span></span> <span data-ttu-id="ab6ca-158">Per altre informazioni rivedere [Associazioni HTTP e webhook in Funzioni di Azure](../azure-functions/functions-reference.md#function-code).</span><span class="sxs-lookup"><span data-stu-id="ab6ca-158">For more information, see [Azure functions HTTP and webhook bindings](../azure-functions/functions-reference.md#function-code).</span></span>

>[!NOTE]
><span data-ttu-id="ab6ca-159">Set hello **disabilitato** proprietà troppo**true** funzione hello tooprevent venga eseguito.</span><span class="sxs-lookup"><span data-stu-id="ab6ca-159">Set hello **disabled** property too**true** tooprevent hello function from being executed.</span></span> 


<span data-ttu-id="ab6ca-160">Di seguito è riportato un esempio di file **function.json**.</span><span class="sxs-lookup"><span data-stu-id="ab6ca-160">Here is an example of **function.json** file.</span></span>

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

### <a name="projectjson"></a><span data-ttu-id="ab6ca-161">project.json</span><span class="sxs-lookup"><span data-stu-id="ab6ca-161">project.json</span></span>

<span data-ttu-id="ab6ca-162">file Project JSON Hello contiene dipendenze.</span><span class="sxs-lookup"><span data-stu-id="ab6ca-162">hello project.json file contains dependencies.</span></span> <span data-ttu-id="ab6ca-163">Di seguito è riportato un esempio di **Project** pacchetti di file che include i servizi multimediali di Azure .NET hello richiesto da Nuget.</span><span class="sxs-lookup"><span data-stu-id="ab6ca-163">Here is an example of **project.json** file that includes hello required .NET Azure Media Services packages from Nuget.</span></span> <span data-ttu-id="ab6ca-164">Si noti che i numeri di versione di hello verranno modificate con gli aggiornamenti più recenti toohello pacchetti, pertanto è necessario verificare le versioni più recenti di hello.</span><span class="sxs-lookup"><span data-stu-id="ab6ca-164">Note that hello version numbers will change with latest updates toohello packages, so you should confirm hello most recent versions.</span></span> 

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
    
### <a name="runcsx"></a><span data-ttu-id="ab6ca-165">run.csx</span><span class="sxs-lookup"><span data-stu-id="ab6ca-165">run.csx</span></span>

<span data-ttu-id="ab6ca-166">Si tratta di codice hello c# per la funzione.</span><span class="sxs-lookup"><span data-stu-id="ab6ca-166">This is hello C# code for your function.</span></span>  <span data-ttu-id="ab6ca-167">funzione Hello definita sotto monitoraggi un contenitore di account di archiviazione denominato **input** (che è ciò che è stato specificato nel percorso hello) per i nuovi file MP4.</span><span class="sxs-lookup"><span data-stu-id="ab6ca-167">hello function defined below monitors a storage account container named **input** (that is what was specified in hello path) for new MP4 files.</span></span> <span data-ttu-id="ab6ca-168">Una volta che viene rilasciato un file in un contenitore di archiviazione hello, trigger blob hello eseguirà la funzione hello.</span><span class="sxs-lookup"><span data-stu-id="ab6ca-168">Once a file is dropped into hello storage container, hello blob trigger will execute hello function.</span></span>
    
<span data-ttu-id="ab6ca-169">esempio Hello definita in questa sezione viene illustrato</span><span class="sxs-lookup"><span data-stu-id="ab6ca-169">hello example defined in this section demonstrates</span></span> 

1. <span data-ttu-id="ab6ca-170">come tooingest un asset in servizi multimediali di un account (copiando un blob in un asset AMS) e</span><span class="sxs-lookup"><span data-stu-id="ab6ca-170">how tooingest an asset into a Media Services account (by coping a blob into an AMS asset) and</span></span> 
2. <span data-ttu-id="ab6ca-171">come toosubmit un processo di codifica che utilizza "Il flusso adattivo" del Media Encoder Standard predefinito.</span><span class="sxs-lookup"><span data-stu-id="ab6ca-171">how toosubmit an encoding job that uses Media Encoder Standard's "Adaptive Streaming" preset .</span></span>

<span data-ttu-id="ab6ca-172">In uno scenario reale hello, è probabile che si desidera che lo stato del processo tootrack e quindi si pubblica l'asset codificato.</span><span class="sxs-lookup"><span data-stu-id="ab6ca-172">In hello real life scenario, you most likely want tootrack job progress and then publish your encoded asset.</span></span> <span data-ttu-id="ab6ca-173">Per ulteriori informazioni, vedere [servizi multimediali di Azure usare i Webhook toomonitor processo notifiche](media-services-dotnet-check-job-progress-with-webhooks.md).</span><span class="sxs-lookup"><span data-stu-id="ab6ca-173">For more information, see [Use Azure WebHooks toomonitor Media Services job notifications](media-services-dotnet-check-job-progress-with-webhooks.md).</span></span> <span data-ttu-id="ab6ca-174">Per altri esempi, vedere [Funzioni di Azure dei Servizi multimediali](https://github.com/Azure-Samples/media-services-dotnet-functions-integration).</span><span class="sxs-lookup"><span data-stu-id="ab6ca-174">For more examples, see [Media Services Azure Functions](https://github.com/Azure-Samples/media-services-dotnet-functions-integration).</span></span>  

<span data-ttu-id="ab6ca-175">Al termine dell'operazione di definizione della funzione fare clic su **Salva ed esegui**.</span><span class="sxs-lookup"><span data-stu-id="ab6ca-175">Once you are done defining your function click **Save and Run**.</span></span>

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
##<a name="test-your-function"></a><span data-ttu-id="ab6ca-176">Testare la funzione</span><span class="sxs-lookup"><span data-stu-id="ab6ca-176">Test your function</span></span>

<span data-ttu-id="ab6ca-177">tootest della funzione, è necessario un file MP4 in hello tooupload **input** contenitore hello dell'account di archiviazione specificato nella stringa di connessione hello.</span><span class="sxs-lookup"><span data-stu-id="ab6ca-177">tootest your function, you need tooupload an MP4 file into hello **input** container of hello storage account that you specified in hello connection string.</span></span>  

## <a name="next-step"></a><span data-ttu-id="ab6ca-178">Passaggio successivo</span><span class="sxs-lookup"><span data-stu-id="ab6ca-178">Next step</span></span>

<span data-ttu-id="ab6ca-179">A questo punto, si è pronti toostart lo sviluppo di un'applicazione di servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="ab6ca-179">At this point, you are ready toostart developing a Media Services application.</span></span> 
 
<span data-ttu-id="ab6ca-180">Per ulteriori dettagli ed esempi/soluzioni complete dell'utilizzo di funzioni di Azure e la logica App con i flussi di lavoro di servizi multimediali di Azure toocreate creazione di contenuto personalizzato, vedere hello [esempio integrazione funzioni Media Services .NET su GitHub](https://github.com/Azure-Samples/media-services-dotnet-functions-integration)</span><span class="sxs-lookup"><span data-stu-id="ab6ca-180">For more details and complete samples/solutions of using Azure Functions and Logic Apps with Azure Media Services toocreate custom content creation workflows, see hello [Media Services .NET Functions Integraiton Sample on GitHub](https://github.com/Azure-Samples/media-services-dotnet-functions-integration)</span></span>

<span data-ttu-id="ab6ca-181">Vedere anche [notifiche con .NET di servizi multimediali di Azure usare i Webhook toomonitor processo](media-services-dotnet-check-job-progress-with-webhooks.md).</span><span class="sxs-lookup"><span data-stu-id="ab6ca-181">Also, see [Use Azure WebHooks toomonitor Media Services job notifications with .NET](media-services-dotnet-check-job-progress-with-webhooks.md).</span></span> 

## <a name="media-services-learning-paths"></a><span data-ttu-id="ab6ca-182">Percorsi di apprendimento di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="ab6ca-182">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="ab6ca-183">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="ab6ca-183">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

