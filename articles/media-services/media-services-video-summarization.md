---
title: Usare Azure Media Video Thumbnails per creare un riepilogo video | Microsoft Docs
description: "Il riepilogo video consente di creare un riepilogo per video lunghi selezionando in modo automatico frammenti interessanti del video di origine. Questa funzione risulta particolarmente utile quando si intende creare una panoramica rapida dei contenuti offerti nella versione più lunga del video."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: a245529f-3150-4afc-93ec-e40d8a6b761d
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/18/2017
ms.author: milanga;juliako;
ms.openlocfilehash: 5d5afdaf22ffea8f3b77a154acb5d0a8dda74405
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="use-azure-media-video-thumbnails-to-create-a-video-summarization"></a><span data-ttu-id="742cf-104">Uso delle anteprime video multimediali di Azure per creare un riepilogo video</span><span class="sxs-lookup"><span data-stu-id="742cf-104">Use Azure Media Video Thumbnails to Create a Video Summarization</span></span>
## <a name="overview"></a><span data-ttu-id="742cf-105">Overview</span><span class="sxs-lookup"><span data-stu-id="742cf-105">Overview</span></span>
<span data-ttu-id="742cf-106">Il processore multimediale delle **anteprime video multimediali di Azure** processore di contenuti multimediali (MP) consente di creare il riepilogo di un video, utile per i clienti che desiderano solo visualizzare in anteprima il riepilogo di un video di lunga durata.</span><span class="sxs-lookup"><span data-stu-id="742cf-106">The **Azure Media Video Thumbnails** media processor (MP) enables you to create a summary of a video that is useful to customers who just want to preview a summary of a long video.</span></span> <span data-ttu-id="742cf-107">Ad esempio, i clienti potrebbero voler vedere un breve "riepilogo video" quando passano il mouse sull'anteprima.</span><span class="sxs-lookup"><span data-stu-id="742cf-107">For example, customers might want to see a short "summary video" when they hover over a thumbnail.</span></span> <span data-ttu-id="742cf-108">Modificando i parametri delle **anteprime video multimediali di Azure** con un set di impostazioni di configurazione, è possibile usare l'efficiente tecnologia di concatenazione e rilevamento delle schermate offerta dal processore multimediale per generare in modo algoritmico una sottoclip descrittiva.</span><span class="sxs-lookup"><span data-stu-id="742cf-108">By tweaking the parameters of **Azure Media Video Thumbnails** through a configuration preset, you can use the MP's powerful shot detection and concatenation technology to algorithmically generate a descriptive subclip.</span></span>  

<span data-ttu-id="742cf-109">Al momento, il processore multimediale di **anteprime video multimediali di Azure** è disponibile in Anteprima.</span><span class="sxs-lookup"><span data-stu-id="742cf-109">The **Azure Media Video Thumbnail** MP is currently in Preview.</span></span>

<span data-ttu-id="742cf-110">Questo argomento contiene informazioni dettagliate su **Azure Media Video Thumbnails** e illustra come usare questa funzionalità con Media Services .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="742cf-110">This topic gives details about  **Azure Media Video Thumbnail** and shows how to use it with Media Services SDK for .NET.</span></span>

## <a name="limitations"></a><span data-ttu-id="742cf-111">Limitazioni</span><span class="sxs-lookup"><span data-stu-id="742cf-111">Limitations</span></span>

<span data-ttu-id="742cf-112">In alcuni casi, se il video non è costituito da scene differenti, l'output sarà rappresentato da un'unica immagine.</span><span class="sxs-lookup"><span data-stu-id="742cf-112">In some cases, if your video is not comprised of different scenes, the output will only be a single shot.</span></span>

## <a name="video-summary-example"></a><span data-ttu-id="742cf-113">Esempio di riepilogo video</span><span class="sxs-lookup"><span data-stu-id="742cf-113">Video summary example</span></span>
<span data-ttu-id="742cf-114">Di seguito sono riportati alcuni esempi delle attività che il processore multimediale delle anteprime video multimediali di Azure può eseguire:</span><span class="sxs-lookup"><span data-stu-id="742cf-114">Here are some examples of what the Azure Media Video Thumbnails media processor can do:</span></span>

### <a name="original-video"></a><span data-ttu-id="742cf-115">Video originale</span><span class="sxs-lookup"><span data-stu-id="742cf-115">Original video</span></span>
[<span data-ttu-id="742cf-116">Video originale</span><span class="sxs-lookup"><span data-stu-id="742cf-116">Original video</span></span>](http://ampdemo.azureedge.net/azuremediaplayer.html?url=https%3A%2F%2Fnimbuscdn-nimbuspm.streaming.mediaservices.windows.net%2Faed33834-ec2d-4788-88b5-a4505b3d032c%2FMicrosoft%27s%20HoloLens%20Live%20Demonstration.ism%2Fmanifest)

### <a name="video-thumbnail-result"></a><span data-ttu-id="742cf-117">Risultato dell'anteprima video</span><span class="sxs-lookup"><span data-stu-id="742cf-117">Video thumbnail result</span></span>
[<span data-ttu-id="742cf-118">Risultato dell'anteprima video</span><span class="sxs-lookup"><span data-stu-id="742cf-118">Video thumbnail result</span></span>](http://ampdemo.azureedge.net/azuremediaplayer.html?url=http%3A%2F%2Fnimbuscdn-nimbuspm.streaming.mediaservices.windows.net%2Ff5c91052-4232-41d4-b531-062e07b6a9ae%2FHololens%2520Demo_VideoThumbnails_MotionThumbnail.mp4)

## <a name="task-configuration-preset"></a><span data-ttu-id="742cf-119">Configurazione delle attività (set di impostazioni)</span><span class="sxs-lookup"><span data-stu-id="742cf-119">Task configuration (preset)</span></span>
<span data-ttu-id="742cf-120">Quando si crea un'attività di anteprima video con **anteprime video multimediali di Azure**, è necessario specificare un set di impostazioni di configurazione.</span><span class="sxs-lookup"><span data-stu-id="742cf-120">When creating a video thumbnail task with **Azure Media Video Thumbnails**, you must specify a configuration preset.</span></span> <span data-ttu-id="742cf-121">L'esempio precedente dell'anteprima è stato creato con la configurazione JSON di base seguente:</span><span class="sxs-lookup"><span data-stu-id="742cf-121">The above thumbnail sample was created with the following basic JSON configuration:</span></span>

    {"version":"1.0"}

<span data-ttu-id="742cf-122">Al momento, è possibile modificare i parametri seguenti:</span><span class="sxs-lookup"><span data-stu-id="742cf-122">Currently, you can change the following parameters:</span></span>

| <span data-ttu-id="742cf-123">Param</span><span class="sxs-lookup"><span data-stu-id="742cf-123">Param</span></span> | <span data-ttu-id="742cf-124">Descrizione</span><span class="sxs-lookup"><span data-stu-id="742cf-124">Description</span></span> |
| --- | --- |
| <span data-ttu-id="742cf-125">outputAudio</span><span class="sxs-lookup"><span data-stu-id="742cf-125">outputAudio</span></span> |<span data-ttu-id="742cf-126">Specifica se il video finale contiene audio.</span><span class="sxs-lookup"><span data-stu-id="742cf-126">Specifies whether or not the resultant video contains any audio.</span></span> <br/><span data-ttu-id="742cf-127">I valori consentiti sono: true o false.</span><span class="sxs-lookup"><span data-stu-id="742cf-127">Allowed values are: True or False.</span></span> <span data-ttu-id="742cf-128">Il valore predefinito è true.</span><span class="sxs-lookup"><span data-stu-id="742cf-128">Default is True.</span></span> |
| <span data-ttu-id="742cf-129">fadeInFadeOut</span><span class="sxs-lookup"><span data-stu-id="742cf-129">fadeInFadeOut</span></span> |<span data-ttu-id="742cf-130">Specifica se vengono usate transizioni a dissolvenza tra le anteprime di movimento separate.</span><span class="sxs-lookup"><span data-stu-id="742cf-130">Specifies whether or not fade transitions are used between the separate motion thumbnails.</span></span>  <br/><span data-ttu-id="742cf-131">I valori consentiti sono: true o false.</span><span class="sxs-lookup"><span data-stu-id="742cf-131">Allowed values are: True or False.</span></span>  <span data-ttu-id="742cf-132">Il valore predefinito è true.</span><span class="sxs-lookup"><span data-stu-id="742cf-132">Default is True.</span></span> |
| <span data-ttu-id="742cf-133">maxMotionThumbnailDurationInSecs</span><span class="sxs-lookup"><span data-stu-id="742cf-133">maxMotionThumbnailDurationInSecs</span></span> |<span data-ttu-id="742cf-134">Numero intero che specifica quanto tempo deve durare l'intero video finale.</span><span class="sxs-lookup"><span data-stu-id="742cf-134">Integer that specifies how long the entire resultant video shall be.</span></span>  <span data-ttu-id="742cf-135">Il valore predefinito dipende dalla durata del video originale.</span><span class="sxs-lookup"><span data-stu-id="742cf-135">Default depends on original video duration.</span></span> |

<span data-ttu-id="742cf-136">La tabella seguente descrive la durata predefinita, quando **maxMotionThumbnailInSecs** non viene usato.</span><span class="sxs-lookup"><span data-stu-id="742cf-136">The following table describes the default duration, when **maxMotionThumbnailInSecs** is not used.</span></span>

|  |  |  |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="742cf-137">Durata del video</span><span class="sxs-lookup"><span data-stu-id="742cf-137">Video duration</span></span> |<span data-ttu-id="742cf-138">d < 3 min</span><span class="sxs-lookup"><span data-stu-id="742cf-138">d < 3 min</span></span> |<span data-ttu-id="742cf-139">3 minuti. < d < 15 minuti</span><span class="sxs-lookup"><span data-stu-id="742cf-139">3 min < d < 15 min</span></span> |
| <span data-ttu-id="742cf-140">Durata dell'anteprima</span><span class="sxs-lookup"><span data-stu-id="742cf-140">Thumbnail duration</span></span> |<span data-ttu-id="742cf-141">15 sec (2-3 scene)</span><span class="sxs-lookup"><span data-stu-id="742cf-141">15 sec (2-3 scenes)</span></span> |<span data-ttu-id="742cf-142">30 sec (3-5 scene)</span><span class="sxs-lookup"><span data-stu-id="742cf-142">30 sec (3-5 scenes)</span></span> |

<span data-ttu-id="742cf-143">Il codice JSON seguente imposta i parametri disponibili.</span><span class="sxs-lookup"><span data-stu-id="742cf-143">The following JSON sets available parameters.</span></span>

    {
        "version": "1.0",
        "options": {
            "outputAudio": "true",
            "maxMotionThumbnailDurationInSecs": "10",
            "fadeInFadeOut": "true"
        }
    }

## <a name="net-sample-code"></a><span data-ttu-id="742cf-144">Codice di esempio .NET</span><span class="sxs-lookup"><span data-stu-id="742cf-144">.NET sample code</span></span>

<span data-ttu-id="742cf-145">Il programma seguente illustra come:</span><span class="sxs-lookup"><span data-stu-id="742cf-145">The following program shows how to:</span></span>

1. <span data-ttu-id="742cf-146">Creare un asset e caricare un file multimediale nell'asset.</span><span class="sxs-lookup"><span data-stu-id="742cf-146">Create an asset and upload a media file into the asset.</span></span>
2. <span data-ttu-id="742cf-147">Creare un processo con un'attività di anteprima video in base al file di configurazione che contiene il set di impostazioni JSON seguente.</span><span class="sxs-lookup"><span data-stu-id="742cf-147">Creates a job with a video thumbnail task based on a configuration file that contains the following json preset.</span></span> 
   
        {                
            "version": "1.0",
            "options": {
                "outputAudio": "true",
                "maxMotionThumbnailDurationInSecs": "30",
                "fadeInFadeOut": "false"
            }
        }
3. <span data-ttu-id="742cf-148">Scaricare i file di output.</span><span class="sxs-lookup"><span data-stu-id="742cf-148">Downloads the output files.</span></span> 

#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="742cf-149">Creare e configurare un progetto di Visual Studio</span><span class="sxs-lookup"><span data-stu-id="742cf-149">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="742cf-150">Configurare l'ambiente di sviluppo e popolare il file app.config con le informazioni di connessione, come descritto in [Sviluppo di applicazioni di Servizi multimediali con .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="742cf-150">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="742cf-151">Esempio</span><span class="sxs-lookup"><span data-stu-id="742cf-151">Example</span></span>

    using System;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Threading;
    using System.Threading.Tasks;

    namespace VideoSummarization
    {
        class Program
        {
            // Read values from the App.config file.
            private static readonly string _AADTenantDomain =
                ConfigurationManager.AppSettings["AADTenantDomain"];
            private static readonly string _RESTAPIEndpoint =
                ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

            // Field for service context.
            private static CloudMediaContext _context = null;

            static void Main(string[] args)
            {
                var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
                var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

                _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);


                // Run the thumbnail job.
                var asset = RunVideoThumbnailJob(@"C:\supportFiles\VideoThumbnail\BigBuckBunny.mp4",
                                            @"C:\supportFiles\VideoThumbnail\config.json");

                // Download the job output asset.
                DownloadAsset(asset, @"C:\supportFiles\VideoThumbnail\Output");
            }

            static IAsset RunVideoThumbnailJob(string inputMediaFilePath, string configurationFile)
            {
                // Create an asset and upload the input media file to storage.
                IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
                    "My Video Thumbnail Input Asset",
                    AssetCreationOptions.None);

                // Declare a new job.
                IJob job = _context.Jobs.Create("My Video Thumbnail Job");

                // Get a reference to Azure Media Video Thumbnails.
                string MediaProcessorName = "Azure Media Video Thumbnails";

                var processor = GetLatestMediaProcessorByName(MediaProcessorName);

                // Read configuration from the specified file.
                string configuration = File.ReadAllText(configurationFile);

                // Create a task with the encoding details, using a string preset.
                ITask task = job.Tasks.AddNew("My Video Thumbnail Task",
                    processor,
                    configuration,
                    TaskOptions.None);

                // Specify the input asset.
                task.InputAssets.Add(asset);

                // Add an output asset to contain the results of the job.
                task.OutputAssets.AddNew("My Video Thumbnail Output Asset", AssetCreationOptions.None);

                // Use the following event handler to check job progress.  
                job.StateChanged += new EventHandler<JobStateChangedEventArgs>(StateChanged);

                // Launch the job.
                job.Submit();

                // Check job execution and wait for job to finish.
                Task progressJobTask = job.GetExecutionProgressTask(CancellationToken.None);

                progressJobTask.Wait();

                // If job state is Error, the event handling
                // method for job progress should log errors.  Here we check
                // for error state and exit if needed.
                if (job.State == JobState.Error)
                {
                    ErrorDetail error = job.Tasks.First().ErrorDetails.First();
                    Console.WriteLine(string.Format("Error: {0}. {1}",
                                                    error.Code,
                                                    error.Message));
                    return null;
                }

                return job.OutputMediaAssets[0];
            }

            static IAsset CreateAssetAndUploadSingleFile(string filePath, string assetName, AssetCreationOptions options)
            {
                IAsset asset = _context.Assets.Create(assetName, options);

                var assetFile = asset.AssetFiles.Create(Path.GetFileName(filePath));
                assetFile.Upload(filePath);

                return asset;
            }

            static void DownloadAsset(IAsset asset, string outputDirectory)
            {
                foreach (IAssetFile file in asset.AssetFiles)
                {
                    file.Download(Path.Combine(outputDirectory, file.Name));
                }
            }

            static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
            {
                var processor = _context.MediaProcessors
                    .Where(p => p.Name == mediaProcessorName)
                    .ToList()
                    .OrderBy(p => new Version(p.Version))
                    .LastOrDefault();

                if (processor == null)
                    throw new ArgumentException(string.Format("Unknown media processor",
                                                               mediaProcessorName));

                return processor;
            }

            static private void StateChanged(object sender, JobStateChangedEventArgs e)
            {
                Console.WriteLine("Job state changed event:");
                Console.WriteLine("  Previous state: " + e.PreviousState);
                Console.WriteLine("  Current state: " + e.CurrentState);

                switch (e.CurrentState)
                {
                    case JobState.Finished:
                        Console.WriteLine();
                        Console.WriteLine("Job is finished.");
                        Console.WriteLine();
                        break;
                    case JobState.Canceling:
                    case JobState.Queued:
                    case JobState.Scheduled:
                    case JobState.Processing:
                        Console.WriteLine("Please wait...\n");
                        break;
                    case JobState.Canceled:
                    case JobState.Error:
                        // Cast sender as a job.
                        IJob job = (IJob)sender;
                        // Display or log error details as needed.
                        // LogJobStop(job.Id);
                        break;
                    default:
                        break;
                }
            }

        }
    }

### <a name="video-thumbnail-output"></a><span data-ttu-id="742cf-152">Output di anteprima video</span><span class="sxs-lookup"><span data-stu-id="742cf-152">Video thumbnail output</span></span>
[<span data-ttu-id="742cf-153">Output di anteprima video</span><span class="sxs-lookup"><span data-stu-id="742cf-153">Video thumbnail output</span></span>](http://ampdemo.azureedge.net/azuremediaplayer.html?url=http%3A%2F%2Fnimbuscdn-nimbuspm.streaming.mediaservices.windows.net%2Fd06f24dc-bc81-488e-a8d0-348b7dc41b56%2FHololens%2520Demo_VideoThumbnails_MotionThumbnail.mp4)

## <a name="media-services-learning-paths"></a><span data-ttu-id="742cf-154">Percorsi di apprendimento di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="742cf-154">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="742cf-155">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="742cf-155">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="742cf-156">Collegamenti correlati</span><span class="sxs-lookup"><span data-stu-id="742cf-156">Related links</span></span>
[<span data-ttu-id="742cf-157">Panoramica di Analisi servizi multimediali di Azure</span><span class="sxs-lookup"><span data-stu-id="742cf-157">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

[<span data-ttu-id="742cf-158">Demo di Analisi servizi multimediali di Azure</span><span class="sxs-lookup"><span data-stu-id="742cf-158">Azure Media Analytics demos</span></span>](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

