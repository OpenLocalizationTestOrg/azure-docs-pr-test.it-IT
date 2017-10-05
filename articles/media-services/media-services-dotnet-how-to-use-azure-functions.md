---
title: Sviluppare le Funzioni di Azure con Servizi multimediali
description: In questo argomento viene illustrato come avviare lo sviluppo di Funzioni di Azure con Servizi multimediali tramite il Portale di Azure.
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
ms.openlocfilehash: 35d539855572fef6c00de614a4e57738a8abd075
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
#<a name="develop-azure-functions-with-media-services"></a><span data-ttu-id="1d278-103">Sviluppare le Funzioni di Azure con Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="1d278-103">Develop Azure Functions with Media Services</span></span>

<span data-ttu-id="1d278-104">In questo argomento viene illustrato come iniziare a creare le Funzioni di Azure che usano i Servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="1d278-104">This topic shows you how to get started with creating Azure Functions that use Media Services.</span></span> <span data-ttu-id="1d278-105">La funzione di Azure definita in questo argomento consente di monitorare un contenitore di account di archiviazione denominato **input** per i nuovi file MP4.</span><span class="sxs-lookup"><span data-stu-id="1d278-105">The Azure Function defined in this topic monitors a storage account container named **input** for new MP4 files.</span></span> <span data-ttu-id="1d278-106">Una volta rilasciato un file nel contenitore di archiviazione, il trigger BLOB eseguirà la funzione.</span><span class="sxs-lookup"><span data-stu-id="1d278-106">Once a file is dropped into the storage container, the blob trigger will execute the function.</span></span>

<span data-ttu-id="1d278-107">Se si vuole esplorare e distribuire le Funzioni di Azure esistenti che usano i Servizi multimediali di Azure, estrarre [Media Services Azure Functions](https://github.com/Azure-Samples/media-services-dotnet-functions-integration) (Funzioni di Azure di Servizi multimediali).</span><span class="sxs-lookup"><span data-stu-id="1d278-107">If you want to explore and deploy existing Azure Functions that use Azure Media Services, check out [Media Services Azure Functions](https://github.com/Azure-Samples/media-services-dotnet-functions-integration).</span></span> <span data-ttu-id="1d278-108">Questo repository contiene esempi che usano Servizi multimediali per visualizzare i flussi di lavoro correlati all'inserimento di contenuto direttamente dall'archiviazione BLOB, alla codifica e alla scrittura del contenuto nell'archiviazione BLOB.</span><span class="sxs-lookup"><span data-stu-id="1d278-108">This repository contains examples that use Media Services to show workflows related to ingesting content directly from blob storage, encoding, and writing content back to blob storage.</span></span> <span data-ttu-id="1d278-109">Include inoltre esempi su come monitorare le notifiche dei processi tramite i webhook e le code di Azure.</span><span class="sxs-lookup"><span data-stu-id="1d278-109">It also includes examples of how to monitor job notifications via WebHooks and Azure Queues.</span></span> <span data-ttu-id="1d278-110">È inoltre possibile sviluppare le funzioni in base agli esempi nel repository [Funzioni di Azure dei Servizi multimediali](https://github.com/Azure-Samples/media-services-dotnet-functions-integration).</span><span class="sxs-lookup"><span data-stu-id="1d278-110">You can also develop your Functions based on the examples in the [Media Services Azure Functions](https://github.com/Azure-Samples/media-services-dotnet-functions-integration) repository.</span></span> <span data-ttu-id="1d278-111">Per distribuire le funzioni, premere il pulsante **Distribuisci in Azure**.</span><span class="sxs-lookup"><span data-stu-id="1d278-111">To deploy the functions, press the **Deploy to Azure** button.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1d278-112">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="1d278-112">Prerequisites</span></span>

- <span data-ttu-id="1d278-113">Per poter creare la prima funzione, è necessario avere un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="1d278-113">Before you can create your first function, you need to have an active Azure account.</span></span> <span data-ttu-id="1d278-114">Se non si possiede già un account Azure, [sono disponibili account gratuiti](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="1d278-114">If you don't already have an Azure account, [free accounts are available](https://azure.microsoft.com/free/).</span></span>
- <span data-ttu-id="1d278-115">Se si intende creare le Funzioni di Azure per eseguire azioni sull'account dei Servizi multimediali di Azure o ascoltare gli eventi inviati dai Servizi multimediali, è necessario creare un account AMS, come descritto [qui](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="1d278-115">If you are going to create Azure Functions that perform actions on your Azure Media Services (AMS) account or listen to events sent by Media Services, you should create an AMS account, as described [here](media-services-portal-create-account.md).</span></span>
- <span data-ttu-id="1d278-116">Comprensione della [modalità d'uso delle funzioni di Azure](../azure-functions/functions-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1d278-116">Understanding of [how to use Azure functions](../azure-functions/functions-overview.md).</span></span> <span data-ttu-id="1d278-117">Inoltre, esaminare:</span><span class="sxs-lookup"><span data-stu-id="1d278-117">Also, review:</span></span>
    - [<span data-ttu-id="1d278-118">Associazioni HTTP e webhook in Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="1d278-118">Azure functions HTTP and webhook bindings</span></span>](../azure-functions/functions-triggers-bindings.md)
    - [<span data-ttu-id="1d278-119">Come configurare le impostazioni dell'app per le funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="1d278-119">How to configure Azure Function app settings</span></span>](../azure-functions/functions-how-to-use-azure-function-app-settings.md)
    
## <a name="considerations"></a><span data-ttu-id="1d278-120">Considerazioni</span><span class="sxs-lookup"><span data-stu-id="1d278-120">Considerations</span></span>

-  <span data-ttu-id="1d278-121">Le funzioni di Azure in esecuzione con piano a consumo hanno un timeout di 5 minuti.</span><span class="sxs-lookup"><span data-stu-id="1d278-121">Azure Functions running under the Consumption plan have 5 minutes timeout limit.</span></span>

## <a name="create-a-function-app"></a><span data-ttu-id="1d278-122">Creare un'app per le funzioni</span><span class="sxs-lookup"><span data-stu-id="1d278-122">Create a function app</span></span>

1. <span data-ttu-id="1d278-123">Passare al [portale di Azure](http://portal.azure.com) e accedere con il proprio account Azure.</span><span class="sxs-lookup"><span data-stu-id="1d278-123">Go to the [Azure portal](http://portal.azure.com) and sign-in with your Azure account.</span></span>
2. <span data-ttu-id="1d278-124">Creare un'app per le funzioni come descritto [qui](../azure-functions/functions-create-function-app-portal.md).</span><span class="sxs-lookup"><span data-stu-id="1d278-124">Create a function app as described [here](../azure-functions/functions-create-function-app-portal.md).</span></span>

>[!NOTE]
> <span data-ttu-id="1d278-125">Un account di archiviazione specificato nella variabile di ambiente **StorageConnection** (vedere il passaggio successivo) deve essere nella stessa area dell'app.</span><span class="sxs-lookup"><span data-stu-id="1d278-125">A storage account that you specify in the **StorageConnection** environment variable (see the next step) should be in the same region as your app.</span></span>

## <a name="configure-function-app-settings"></a><span data-ttu-id="1d278-126">Configurare le impostazioni dell'app per le funzioni</span><span class="sxs-lookup"><span data-stu-id="1d278-126">Configure function app settings</span></span>

<span data-ttu-id="1d278-127">Quando si sviluppano le funzioni di Servizi multimediali, è utile aggiungere variabili di ambiente che verranno usati nelle funzioni.</span><span class="sxs-lookup"><span data-stu-id="1d278-127">When developing Media Services functions, it is handy to add environment variables that will be used throughout your functions.</span></span> <span data-ttu-id="1d278-128">Per configurare le impostazioni dell'app, fare clic sul collegamento Configurare le impostazioni dell'app.</span><span class="sxs-lookup"><span data-stu-id="1d278-128">To configure app settings, click the Configure App Settings link.</span></span> <span data-ttu-id="1d278-129">Per altre informazioni, vedere [Come configurare le impostazioni dell'app per le funzioni di Azure](../azure-functions/functions-how-to-use-azure-function-app-settings.md).</span><span class="sxs-lookup"><span data-stu-id="1d278-129">For more information, see  [How to configure Azure Function app settings](../azure-functions/functions-how-to-use-azure-function-app-settings.md).</span></span> 

<span data-ttu-id="1d278-130">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="1d278-130">For example:</span></span>

![Impostazioni](./media/media-services-azure-functions/media-services-azure-functions001.png)

<span data-ttu-id="1d278-132">Per la funzione definita in questo articolo si presuppongono le seguenti variabili di ambiente nelle impostazioni dell'app:</span><span class="sxs-lookup"><span data-stu-id="1d278-132">The function, defined in this article, assumes you have the following environment variables in your app settings:</span></span>

<span data-ttu-id="1d278-133">**AMSAccount**: *nome dell'account AMS* (ad esempio testams)</span><span class="sxs-lookup"><span data-stu-id="1d278-133">**AMSAccount** : *AMS account name* (e.g. testams)</span></span>

<span data-ttu-id="1d278-134">**AMSKey** : *chiave dell'account AMS* (ad esempio, IHOySnH+XX3LGPfraE5fKPl0EnzvEPKkOPKCr59aiMM=)</span><span class="sxs-lookup"><span data-stu-id="1d278-134">**AMSKey** : *AMS account key* (e.g. IHOySnH+XX3LGPfraE5fKPl0EnzvEPKkOPKCr59aiMM=)</span></span>

<span data-ttu-id="1d278-135">**MediaServicesStorageAccountName** : *nome dell'account di archiviazione* (ad esempio, testamsstorage)</span><span class="sxs-lookup"><span data-stu-id="1d278-135">**MediaServicesStorageAccountName** : *storage account name* (e.g., testamsstorage)</span></span>

<span data-ttu-id="1d278-136">**MediaServicesStorageAccountKey** : *chiave dell'account di archiviazione* (ad esempio, xx7RN7mvpcipkuXvn5g7jwxnKh5MwYQ/awZAzkSIxQA8tmCtn93rqobjgjt41Wb0zwTZWeWQHY5kSZF0XXXXXX==)</span><span class="sxs-lookup"><span data-stu-id="1d278-136">**MediaServicesStorageAccountKey** : *storage account key* (e.g., xx7RN7mvpcipkuXvn5g7jwxnKh5MwYQ/awZAzkSIxQA8tmCtn93rqobjgjt41Wb0zwTZWeWQHY5kSZF0XXXXXX==)</span></span>

<span data-ttu-id="1d278-137">**StorageConnection** : *connessione di archiviazione* (ad esempio, DefaultEndpointsProtocol=https;AccountName=testamsstorage;AccountKey=xx7RN7mvpcipkuXvn5g7jwxnKh5MwYQ/awZAzkSIxQA8tmCtn93rqobjgjt41Wb0zwTZWeWQHY5kSZF0XXXXX==)</span><span class="sxs-lookup"><span data-stu-id="1d278-137">**StorageConnection** : *storage connection* (e.g., DefaultEndpointsProtocol=https;AccountName=testamsstorage;AccountKey=xx7RN7mvpcipkuXvn5g7jwxnKh5MwYQ/awZAzkSIxQA8tmCtn93rqobjgjt41Wb0zwTZWeWQHY5kSZF0XXXXX==)</span></span>

## <a name="create-a-function"></a><span data-ttu-id="1d278-138">Creare una funzione</span><span class="sxs-lookup"><span data-stu-id="1d278-138">Create a function</span></span>

<span data-ttu-id="1d278-139">In seguito alla distribuzione dell'app per le funzioni, questa verrà visualizzata tra le Funzioni di Azure dei **Servizi app**.</span><span class="sxs-lookup"><span data-stu-id="1d278-139">Once your function app is deployed, you can find it among **App Services** Azure Functions.</span></span>

1. <span data-ttu-id="1d278-140">Selezionare l'app per le funzioni e fare clic su **Nuova funzione**.</span><span class="sxs-lookup"><span data-stu-id="1d278-140">Select your function app and click **New Function**.</span></span>
2. <span data-ttu-id="1d278-141">Scegliere il linguaggio **C#** e lo scenario **Elaborazione dati**.</span><span class="sxs-lookup"><span data-stu-id="1d278-141">Choose the **C#** language and **Data Processing** scenario.</span></span>
3. <span data-ttu-id="1d278-142">Scegliere il modello **BlobTrigger**.</span><span class="sxs-lookup"><span data-stu-id="1d278-142">Choose **BlobTrigger** template.</span></span> <span data-ttu-id="1d278-143">Questa funzione verrà attivata ogni volta che viene caricato un BLOB nel contenitore di **input**.</span><span class="sxs-lookup"><span data-stu-id="1d278-143">This function will be triggered whenever a blob is uploaded into the **input** container.</span></span> <span data-ttu-id="1d278-144">Il nome **input** è specificato nel **percorso**, nel passaggio successivo.</span><span class="sxs-lookup"><span data-stu-id="1d278-144">The **input** name is specified in the **Path**, in the next step.</span></span>

    ![input](./media/media-services-azure-functions/media-services-azure-functions004.png)

4. <span data-ttu-id="1d278-146">Dopo aver selezionato **BlobTrigger**, altri controlli verranno visualizzati nella pagina.</span><span class="sxs-lookup"><span data-stu-id="1d278-146">Once you select **BlobTrigger**, some more controls will appear on the page.</span></span>

    ![input](./media/media-services-azure-functions/media-services-azure-functions005.png)

4. <span data-ttu-id="1d278-148">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="1d278-148">Click **Create**.</span></span> 


## <a name="files"></a><span data-ttu-id="1d278-149">File</span><span class="sxs-lookup"><span data-stu-id="1d278-149">Files</span></span>

<span data-ttu-id="1d278-150">La funzione di Azure è associata al file del codice e ad altri file descritti in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="1d278-150">Your Azure function is associated with code files and other files that are described in this section.</span></span> <span data-ttu-id="1d278-151">Per impostazione predefinita, una funzione è associata ai file **function.json** e **run.csx** (C#).</span><span class="sxs-lookup"><span data-stu-id="1d278-151">By default, a function is associated with **function.json** and **run.csx** (C#) files.</span></span> <span data-ttu-id="1d278-152">Sarà necessario aggiungere un file **project.json**.</span><span class="sxs-lookup"><span data-stu-id="1d278-152">You will need to add a **project.json** file.</span></span> <span data-ttu-id="1d278-153">La parte successiva di questa sezione illustra le definizioni per questi file.</span><span class="sxs-lookup"><span data-stu-id="1d278-153">The rest of this section shows the definitions for these files.</span></span>

![input](./media/media-services-azure-functions/media-services-azure-functions003.png)

### <a name="functionjson"></a><span data-ttu-id="1d278-155">function.json</span><span class="sxs-lookup"><span data-stu-id="1d278-155">function.json</span></span>

<span data-ttu-id="1d278-156">Il file function.json definisce le associazioni di funzione e altre impostazioni di configurazione.</span><span class="sxs-lookup"><span data-stu-id="1d278-156">The function.json file defines the function bindings and other configuration settings.</span></span> <span data-ttu-id="1d278-157">Il runtime usa questo file per determinare gli eventi da monitorare e come passare i dati e restituirli dall'esecuzione di funzioni.</span><span class="sxs-lookup"><span data-stu-id="1d278-157">The runtime uses this file to determine the events to monitor and how to pass data into and return data from function execution.</span></span> <span data-ttu-id="1d278-158">Per altre informazioni rivedere [Associazioni HTTP e webhook in Funzioni di Azure](../azure-functions/functions-reference.md#function-code).</span><span class="sxs-lookup"><span data-stu-id="1d278-158">For more information, see [Azure functions HTTP and webhook bindings](../azure-functions/functions-reference.md#function-code).</span></span>

>[!NOTE]
><span data-ttu-id="1d278-159">Impostare la proprietà **disattivato** su **vero** per impedire l'esecuzione della funzione.</span><span class="sxs-lookup"><span data-stu-id="1d278-159">Set the **disabled** property to **true** to prevent the function from being executed.</span></span> 


<span data-ttu-id="1d278-160">Di seguito è riportato un esempio di file **function.json**.</span><span class="sxs-lookup"><span data-stu-id="1d278-160">Here is an example of **function.json** file.</span></span>

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

### <a name="projectjson"></a><span data-ttu-id="1d278-161">project.json</span><span class="sxs-lookup"><span data-stu-id="1d278-161">project.json</span></span>

<span data-ttu-id="1d278-162">Il file project.json contiene dipendenze.</span><span class="sxs-lookup"><span data-stu-id="1d278-162">The project.json file contains dependencies.</span></span> <span data-ttu-id="1d278-163">Di seguito è riportato un esempio del file **project.json** che include i pacchetti di Servizi multimediali di Azure .NET da Nuget.</span><span class="sxs-lookup"><span data-stu-id="1d278-163">Here is an example of **project.json** file that includes the required .NET Azure Media Services packages from Nuget.</span></span> <span data-ttu-id="1d278-164">Si noti che i numeri di versione cambieranno con gli aggiornamenti più recenti per i pacchetti, pertanto è consigliabile confermare le versioni più recenti.</span><span class="sxs-lookup"><span data-stu-id="1d278-164">Note that the version numbers will change with latest updates to the packages, so you should confirm the most recent versions.</span></span> 

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
    
### <a name="runcsx"></a><span data-ttu-id="1d278-165">run.csx</span><span class="sxs-lookup"><span data-stu-id="1d278-165">run.csx</span></span>

<span data-ttu-id="1d278-166">Questo è il codice C# per la funzione.</span><span class="sxs-lookup"><span data-stu-id="1d278-166">This is the C# code for your function.</span></span>  <span data-ttu-id="1d278-167">La funzione definita di seguito monitora un contenitore dell'account di archiviazione denominato **input** (cioè quello specificato nel percorso) per i nuovi file MP4.</span><span class="sxs-lookup"><span data-stu-id="1d278-167">The function defined below monitors a storage account container named **input** (that is what was specified in the path) for new MP4 files.</span></span> <span data-ttu-id="1d278-168">Una volta rilasciato un file nel contenitore di archiviazione, il trigger BLOB eseguirà la funzione.</span><span class="sxs-lookup"><span data-stu-id="1d278-168">Once a file is dropped into the storage container, the blob trigger will execute the function.</span></span>
    
<span data-ttu-id="1d278-169">L'esempio viene definito in questa sezione illustra</span><span class="sxs-lookup"><span data-stu-id="1d278-169">The example defined in this section demonstrates</span></span> 

1. <span data-ttu-id="1d278-170">come inserire un asset in un account di Servizi multimediali (copiando un BLOB in un asset AMS) e</span><span class="sxs-lookup"><span data-stu-id="1d278-170">how to ingest an asset into a Media Services account (by coping a blob into an AMS asset) and</span></span> 
2. <span data-ttu-id="1d278-171">come inviare un processo di codifica che usa il set di impostazioni "Flusso adattivo" di Media Encoder Standard.</span><span class="sxs-lookup"><span data-stu-id="1d278-171">how to submit an encoding job that uses Media Encoder Standard's "Adaptive Streaming" preset .</span></span>

<span data-ttu-id="1d278-172">Nello scenario reale, è probabile che l'utente desideri tenere traccia dello stato dei processi e quindi pubblicare l'asset codificato.</span><span class="sxs-lookup"><span data-stu-id="1d278-172">In the real life scenario, you most likely want to track job progress and then publish your encoded asset.</span></span> <span data-ttu-id="1d278-173">Per altre informazioni, vedere [Usare i webhook di Azure per monitorare le notifiche dei processi di Servizi multimediali con .NET](media-services-dotnet-check-job-progress-with-webhooks.md).</span><span class="sxs-lookup"><span data-stu-id="1d278-173">For more information, see [Use Azure WebHooks to monitor Media Services job notifications](media-services-dotnet-check-job-progress-with-webhooks.md).</span></span> <span data-ttu-id="1d278-174">Per altri esempi, vedere [Funzioni di Azure dei Servizi multimediali](https://github.com/Azure-Samples/media-services-dotnet-functions-integration).</span><span class="sxs-lookup"><span data-stu-id="1d278-174">For more examples, see [Media Services Azure Functions](https://github.com/Azure-Samples/media-services-dotnet-functions-integration).</span></span>  

<span data-ttu-id="1d278-175">Al termine dell'operazione di definizione della funzione fare clic su **Salva ed esegui**.</span><span class="sxs-lookup"><span data-stu-id="1d278-175">Once you are done defining your function click **Save and Run**.</span></span>

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
        // NOTE that the variables {fileName} here come from the path setting in function.json
        // and are passed into the  Run method signature above. We can use this to make decisions on what type of file
        // was dropped into the input container for the function. 

        // No need to do any Retry strategy in this function, By default, the SDK calls a function up to 5 times for a 
        // given blob. If the fifth try fails, the SDK adds a message to a queue named webjobs-blobtrigger-poison.

        log.Info($"C# Blob trigger function processed: {fileName}.mp4");
        log.Info($"Using Azure Media Services account : {_mediaServicesAccountName}");


        try
        {
        // Create and cache the Media Services credentials in a static class variable.
        _cachedCredentials = new MediaServicesCredentials(
                _mediaServicesAccountName,
                _mediaServicesAccountKey);

        // Used the chached credentials to create CloudMediaContext.
        _context = new CloudMediaContext(_cachedCredentials);

        // Step 1:  Copy the Blob into a new Input Asset for the Job
        // ***NOTE: Ideally we would have a method to ingest a Blob directly here somehow. 
        // using code from this sample - https://azure.microsoft.com/en-us/documentation/articles/media-services-copying-existing-blob/

        StorageCredentials mediaServicesStorageCredentials =
            new StorageCredentials(_storageAccountName, _storageAccountKey);

        IAsset newAsset = CreateAssetFromBlob(myBlob, fileName, log).GetAwaiter().GetResult();

        // Step 2: Create an Encoding Job

        // Declare a new encoding job with the Standard encoder
        IJob job = _context.Jobs.Create("Azure Function - MES Job");

        // Get a media processor reference, and pass to it the name of the 
        // processor to use for the specific task.
        IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

        // Create a task with the encoding details, using a custom preset
        ITask task = job.Tasks.AddNew("Encode with Adaptive Streaming",
            processor,
            "Adaptive Streaming",
            TaskOptions.None); 

        // Specify the input asset to be encoded.
        task.InputAssets.Add(newAsset);

        // Add an output asset to contain the results of the job. 
        // This output is specified as AssetCreationOptions.None, which 
        // means the output asset is not encrypted. 
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
    /// Creates a new asset and copies blobs from the specifed storage account.
    /// </summary>
    /// <param name="blob">The specified blob.</param>
    /// <returns>The new asset.</returns>
    public static async Task<IAsset> CreateAssetFromBlobAsync(CloudBlockBlob blob, string assetName, TraceWriter log)
    {
         //Get a reference to the storage account that is associated with the Media Services account. 
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

        // Get the destination asset container reference
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

        // Get hold of the destination blob
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
##<a name="test-your-function"></a><span data-ttu-id="1d278-176">Testare la funzione</span><span class="sxs-lookup"><span data-stu-id="1d278-176">Test your function</span></span>

<span data-ttu-id="1d278-177">Per testare la funzione, è necessario caricare un file MP4 nel contenitore **input** dell'account di archiviazione specificato nella stringa di connessione.</span><span class="sxs-lookup"><span data-stu-id="1d278-177">To test your function, you need to upload an MP4 file into the **input** container of the storage account that you specified in the connection string.</span></span>  

## <a name="next-step"></a><span data-ttu-id="1d278-178">Passaggio successivo</span><span class="sxs-lookup"><span data-stu-id="1d278-178">Next step</span></span>

<span data-ttu-id="1d278-179">A questo punto, si è pronti per iniziare a sviluppare un'applicazione di Servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="1d278-179">At this point, you are ready to start developing a Media Services application.</span></span> 
 
<span data-ttu-id="1d278-180">Per altri dettagli ed esempi o soluzioni complete di uso di Funzioni di Azure e delle App per la logica con Servizi multimediali di Azure per creare flussi di lavoro di creazione di contenuto personalizzato, vedere l'[Esempio di integrazione delle funzioni di Servizi multimediali .NET su GitHub](https://github.com/Azure-Samples/media-services-dotnet-functions-integration)</span><span class="sxs-lookup"><span data-stu-id="1d278-180">For more details and complete samples/solutions of using Azure Functions and Logic Apps with Azure Media Services to create custom content creation workflows, see the [Media Services .NET Functions Integraiton Sample on GitHub](https://github.com/Azure-Samples/media-services-dotnet-functions-integration)</span></span>

<span data-ttu-id="1d278-181">Vedere anche [Usare i webhook di Azure per monitorare le notifiche dei processi di Servizi multimediali con .NET](media-services-dotnet-check-job-progress-with-webhooks.md).</span><span class="sxs-lookup"><span data-stu-id="1d278-181">Also, see [Use Azure WebHooks to monitor Media Services job notifications with .NET](media-services-dotnet-check-job-progress-with-webhooks.md).</span></span> 

## <a name="media-services-learning-paths"></a><span data-ttu-id="1d278-182">Percorsi di apprendimento di Media Services</span><span class="sxs-lookup"><span data-stu-id="1d278-182">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="1d278-183">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="1d278-183">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

