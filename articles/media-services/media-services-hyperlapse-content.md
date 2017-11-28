---
title: File multimediali con Azure Media Hyperlapse aaaHyperlapse | Documenti Microsoft
description: Azure Media Hyperlapse crea fluidi video in time-lapse da contenuti registrati in prima persona o da fotocamere d'azione. Questo argomento viene illustrato come toouse Media Indexer.
services: media-services
documentationcenter: 
author: asolanki
manager: johndeu
editor: 
ms.assetid: 37d54db6-9cf3-4ae9-b3c6-0d29c744e965
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/02/2017
ms.author: adsolank
ms.openlocfilehash: 85bb07206d0ca2f5b2fd0767e6ed4904195d3ab6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="hyperlapse-media-files-with-azure-media-hyperlapse"></a><span data-ttu-id="fc902-104">File multimediali di Hyperlapse con Azure Media Hyperlapse</span><span class="sxs-lookup"><span data-stu-id="fc902-104">Hyperlapse Media Files with Azure Media Hyperlapse</span></span>
<span data-ttu-id="fc902-105">Azure Media Hyperlapse è un processore di contenuti multimediali che crea fluidi video in time-lapse da contenuti registrati in prima persona o da fotocamere d'azione.</span><span class="sxs-lookup"><span data-stu-id="fc902-105">Azure Media Hyperlapse is a Media Processor (MP) that creates smooth time-lapsed videos from first-person or action-camera content.</span></span>  <span data-ttu-id="fc902-106">Hello troppo di pari livello basato su cloud[desktop Hyperlapse Pro Microsoft Research e basato sul telefono cellulare Hyperlapse](http://aka.ms/hyperlapse), Hyperlapse Microsoft per servizi multimediali di Azure Usa hello larga scala hello multimediali di Azure Media Services L'elaborazione di piattaforma toohorizontally scalare e parallelizzare bulk elaborazione con Hyperlapse.</span><span class="sxs-lookup"><span data-stu-id="fc902-106">hello cloud-based sibling too[Microsoft Research's desktop Hyperlapse Pro and phone-based Hyperlapse Mobile](http://aka.ms/hyperlapse), Microsoft Hyperlapse for Azure Media Services utilizes hello massive scale of hello Azure Media Services Media Processing platform toohorizontally scale and parallelize bulk Hyperlapse processing.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fc902-107">Microsoft Hyperlapse è progettato toowork migliore in prima persona contenuto con una fotocamera mobile.</span><span class="sxs-lookup"><span data-stu-id="fc902-107">Microsoft Hyperlapse is designed toowork best on first-person content with a moving camera.</span></span>  <span data-ttu-id="fc902-108">Sebbene ancora videocamera può comunque funzionare, hello prestazioni e qualità di hello processore di contenuti multimediali di Azure Media Hyperlapse non può essere garantite per altri tipi di contenuto.</span><span class="sxs-lookup"><span data-stu-id="fc902-108">Although still-camera footage can still work, hello performance and quality of hello Azure Media Hyperlapse Media Processor cannot be guaranteed for other types of content.</span></span>  <span data-ttu-id="fc902-109">informazioni su Microsoft Hyperlapse per servizi multimediali di Azure toolearn e vedere alcuni video di esempio, estrarre hello [post di blog introduttivo](http://aka.ms/azurehyperlapseblog) dalla versione di anteprima pubblica di hello.</span><span class="sxs-lookup"><span data-stu-id="fc902-109">toolearn more about Microsoft Hyperlapse for Azure Media Services and see some example videos, check out hello [introductory blog post](http://aka.ms/azurehyperlapseblog) from hello public preview.</span></span>
> 
> 

<span data-ttu-id="fc902-110">Un Azure Media Hyperlapse processo accetta come input un file di asset MP4, MOV o WMV insieme a un file di configurazione che specifica i frame del video devono essere tempo trascorso e velocità toowhat (ad esempio 10.000 primo frame x 2).</span><span class="sxs-lookup"><span data-stu-id="fc902-110">An Azure Media Hyperlapse job takes as input an MP4, MOV, or WMV asset file along with a configuration file that specifies which frames of video should be time-lapsed and toowhat speed (e.g. first 10,000 frames at 2x).</span></span>  <span data-ttu-id="fc902-111">output di Hello è una copia trasformata stabilizzare e tempo trascorso di video di input hello.</span><span class="sxs-lookup"><span data-stu-id="fc902-111">hello output is a stabilized and time-lapsed rendition of hello input video.</span></span>

<span data-ttu-id="fc902-112">Per aggiornamenti di Azure Media Hyperlapse hello più recenti, vedere [blog di servizi multimediali](https://azure.microsoft.com/blog/topics/media-services/).</span><span class="sxs-lookup"><span data-stu-id="fc902-112">For hello latest Azure Media Hyperlapse updates, see [Media Services blogs](https://azure.microsoft.com/blog/topics/media-services/).</span></span>

## <a name="hyperlapse-an-asset"></a><span data-ttu-id="fc902-113">Eseguire Hyperlapse su un asset</span><span class="sxs-lookup"><span data-stu-id="fc902-113">Hyperlapse an asset</span></span>
<span data-ttu-id="fc902-114">Innanzitutto è necessario tooupload il tooAzure di file di input desiderata servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="fc902-114">First you will need tooupload your desired input file tooAzure Media Services.</span></span>  <span data-ttu-id="fc902-115">altre informazioni sulle toolearn hello concetti fondamentali per il caricamento e la gestione del contenuto, leggere hello [articolo di gestione dei contenuti](media-services-portal-vod-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="fc902-115">toolearn more about hello concepts involved with uploading and managing content, read hello [content management article](media-services-portal-vod-get-started.md).</span></span>

### <span data-ttu-id="fc902-116"><a id="configuration"></a>Set di impostazioni di configurazione per Hyperlapse</span><span class="sxs-lookup"><span data-stu-id="fc902-116"><a id="configuration"></a>Configuration Preset for Hyperlapse</span></span>
<span data-ttu-id="fc902-117">Una volta il contenuto nell'account di servizi multimediali, sarà necessario tooconstruct set di impostazioni di configurazione.</span><span class="sxs-lookup"><span data-stu-id="fc902-117">Once your content is in your Media Services account, you will need tooconstruct your configuration preset.</span></span>  <span data-ttu-id="fc902-118">Hello nella tabella seguente vengono illustrati i campi di hello specificato dall'utente:</span><span class="sxs-lookup"><span data-stu-id="fc902-118">hello following table explains hello user-specified fields:</span></span>

| <span data-ttu-id="fc902-119">Campo</span><span class="sxs-lookup"><span data-stu-id="fc902-119">Field</span></span> | <span data-ttu-id="fc902-120">Descrizione</span><span class="sxs-lookup"><span data-stu-id="fc902-120">Description</span></span> |
| --- | --- |
| <span data-ttu-id="fc902-121">StartFrame</span><span class="sxs-lookup"><span data-stu-id="fc902-121">StartFrame</span></span> |<span data-ttu-id="fc902-122">frame Hello al quale Microsoft Hyperlapse hello deve iniziare l'elaborazione.</span><span class="sxs-lookup"><span data-stu-id="fc902-122">hello frame upon which hello Microsoft Hyperlapse processing should begin.</span></span> |
| <span data-ttu-id="fc902-123">NumFrames</span><span class="sxs-lookup"><span data-stu-id="fc902-123">NumFrames</span></span> |<span data-ttu-id="fc902-124">numero di Hello di frame tooprocess</span><span class="sxs-lookup"><span data-stu-id="fc902-124">hello number of frames tooprocess</span></span> |
| <span data-ttu-id="fc902-125">Velocità</span><span class="sxs-lookup"><span data-stu-id="fc902-125">Speed</span></span> |<span data-ttu-id="fc902-126">fattore di Hello con cui toospeed i video di input hello.</span><span class="sxs-lookup"><span data-stu-id="fc902-126">hello factor with which toospeed up hello input video.</span></span> |

<span data-ttu-id="fc902-127">Hello Ecco un esempio di file di configurazione conformi in XML e JSON:</span><span class="sxs-lookup"><span data-stu-id="fc902-127">hello following is an example of a conformant configuration file in XML and JSON:</span></span>

<span data-ttu-id="fc902-128">**Set di impostazioni XML:**</span><span class="sxs-lookup"><span data-stu-id="fc902-128">**XML preset:**</span></span>

    <?xml version="1.0" encoding="utf-16"?>
    <Preset xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
        <Sources>
            <Source StartFrame="0" NumFrames="10000" />
        </Sources>
        <Options>
            <Speed>12</Speed>
        </Options>
    </Preset>

<span data-ttu-id="fc902-129">**Set di impostazioni JSON:**</span><span class="sxs-lookup"><span data-stu-id="fc902-129">**JSON preset:**</span></span>

    {
        "Version":1.0,
        "Sources": [
            {
                "StartFrame":0,
                "NumFrames":2147483647
            }
        ],
        "Options": {
            "Speed":1,
            "Stabilize":false
        }
    }

### <span data-ttu-id="fc902-130"><a id="sample_code"></a>Microsoft Hyperlapse con hello AMS .NET SDK</span><span class="sxs-lookup"><span data-stu-id="fc902-130"><a id="sample_code"></a> Microsoft Hyperlapse with hello AMS .NET SDK</span></span>
<span data-ttu-id="fc902-131">Hello metodo seguente carica un file multimediale come asset e crea un processo con hello processore di contenuti multimediali di Azure Media Hyperlapse.</span><span class="sxs-lookup"><span data-stu-id="fc902-131">hello following method uploads a media file as an asset and creates a job with hello Azure Media Hyperlapse Media Processor.</span></span>

> [!NOTE]
> <span data-ttu-id="fc902-132">Hai già un CloudMediaContext nell'ambito con hello nome "contesto" per toowork questo codice.</span><span class="sxs-lookup"><span data-stu-id="fc902-132">You should already have a CloudMediaContext in scope with hello name "context" for this code toowork.</span></span>  <span data-ttu-id="fc902-133">ulteriori informazioni, leggere hello toolearn [articolo di gestione dei contenuti](media-services-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="fc902-133">toolearn more about this, read hello [content management article](media-services-dotnet-get-started.md).</span></span>
> 
> [!NOTE]
> <span data-ttu-id="fc902-134">argomento stringa Hello "hyperConfig" è previsto toobe preimpostata di una configurazione conforme a JSON o XML come descritto in precedenza.</span><span class="sxs-lookup"><span data-stu-id="fc902-134">hello string argument "hyperConfig" is expected toobe a conformant configuration preset in either JSON or XML as described above.</span></span>
> 
> 

        static bool RunHyperlapseJob(string input, string output, string hyperConfig)
        {
            // create asset with input file
            IAsset asset = context
            .Assets
            .CreateAssetAndUploadSingleFile(input, "My Hyperlapse Input", AssetCreationOptions.None);

            // grab instances of Azure Media Hyperlapse MP
            IMediaProcessor mp = context
            .MediaProcessors
            .GetLatestMediaProcessorByName("Azure Media Hyperlapse");

            // create Job with Hyperlapse task
            IJob job = context
            .Jobs
            .Create(String.Format("Hyperlapse {0}", input));

            if (String.IsNullOrEmpty(hyperConfig))
            {
            // config cannot be empty
            return false;
            }

            hyperConfig = File.ReadAllText(hyperConfig);

            ITask hyperlapseTask = job.Tasks.AddNew("Hyperlapse task",
            mp,
            hyperConfig,
            TaskOptions.None);
            hyperlapseTask.InputAssets.Add(asset);
            hyperlapseTask.OutputAssets.AddNew("Hyperlapse output",
            AssetCreationOptions.None);

            job.Submit();

            // Create progress printing and querying tasks
            Task progressPrintTask = new Task(() =>
            {

            IJob jobQuery = null;
            do
            {
                var progressContext = context;
                jobQuery = progressContext.Jobs
                .Where(j => j.Id == job.Id)
                .First();
                Console.WriteLine(string.Format("{0}\t{1}\t{2}",
                DateTime.Now,
                jobQuery.State,
                jobQuery.Tasks[0].Progress));
                Thread.Sleep(10000);
            }
            while (jobQuery.State != JobState.Finished &&
                                   jobQuery.State != JobState.Error &&
                                   jobQuery.State != JobState.Canceled);
                });
                
            progressPrintTask.Start();

            Task progressJobTask = job.GetExecutionProgressTask(
                                                 CancellationToken.None);
            progressJobTask.Wait();

            // If job state is Error, hello event handling
            // method for job progress should log errors.  Here we check
            // for error state and exit if needed.
            if (job.State == JobState.Error)
            {
                ErrorDetail error = job.Tasks.First().ErrorDetails.First();
                Console.WriteLine(string.Format("Error: {0}. {1}",
                                                error.Code,
                                                error.Message));  
                return false;                  
            }

        DownloadAsset(job.OutputMediaAssets.First(), output);
        return true;
    }

    static void DownloadAsset(IAsset asset, string outputDirectory)
    {
        foreach (IAssetFile file in asset.AssetFiles)
        {
            file.Download(Path.Combine(outputDirectory, file.Name));
        }
    }


    static IAsset CreateAssetAndUploadSingleFile(string filePath, string assetName, AssetCreationOptions options)
    {
        IAsset asset = context.Assets.Create(assetName, options);

        var assetFile = asset.AssetFiles.Create(Path.GetFileName(filePath));
        assetFile.Upload(filePath);

        return asset;
    }

    static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
    {
        var processor = context.MediaProcessors
        .Where(p => p.Name == mediaProcessorName)
        .ToList()
        .OrderBy(p => new Version(p.Version))
        .LastOrDefault();

        if (processor == null)
            throw new ArgumentException(string.Format("Unknown media processor",
                                                       mediaProcessorName));

        return processor;
    }

### <span data-ttu-id="fc902-135"><a id="file_types"></a>Tipi di file supportati</span><span class="sxs-lookup"><span data-stu-id="fc902-135"><a id="file_types"></a>Supported File types</span></span>
* <span data-ttu-id="fc902-136">MP4</span><span class="sxs-lookup"><span data-stu-id="fc902-136">MP4</span></span>
* <span data-ttu-id="fc902-137">MOV</span><span class="sxs-lookup"><span data-stu-id="fc902-137">MOV</span></span>
* <span data-ttu-id="fc902-138">WMV</span><span class="sxs-lookup"><span data-stu-id="fc902-138">WMV</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="fc902-139">Percorsi di apprendimento di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="fc902-139">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="fc902-140">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="fc902-140">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="fc902-141">Collegamenti correlati</span><span class="sxs-lookup"><span data-stu-id="fc902-141">Related links</span></span>
[<span data-ttu-id="fc902-142">Panoramica di Analisi servizi multimediali di Azure</span><span class="sxs-lookup"><span data-stu-id="fc902-142">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

[<span data-ttu-id="fc902-143">Demo di Analisi servizi multimediali di Azure</span><span class="sxs-lookup"><span data-stu-id="fc902-143">Azure Media Analytics demos</span></span>](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

