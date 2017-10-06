---
title: aaaUse Azure Media Video anteprime tooCreate un riepilogo di Video | Documenti Microsoft
description: "Riepilogo video consentono di creare riepiloghi dei video lunghi selezionando automaticamente interessanti frammenti video di origine hello. Ciò è utile quando si desidera tooprovide una rapida panoramica delle quali tooexpect in un video di lunga durata."
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
ms.openlocfilehash: 0a8f0bba6c12a948b940114fe4937e675688a8c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-media-video-thumbnails-toocreate-a-video-summarization"></a><span data-ttu-id="db779-104">Utilizzare le anteprime di Azure Media Video tooCreate un riepilogo di Video</span><span class="sxs-lookup"><span data-stu-id="db779-104">Use Azure Media Video Thumbnails tooCreate a Video Summarization</span></span>
## <a name="overview"></a><span data-ttu-id="db779-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="db779-105">Overview</span></span>
<span data-ttu-id="db779-106">Hello **anteprime Video di Azure Media** toocreate un riepilogo di un video utile toocustomers che si desidera toopreview un riepilogo di un video di lunga durata che consente il processore di contenuti multimediali (MP).</span><span class="sxs-lookup"><span data-stu-id="db779-106">hello **Azure Media Video Thumbnails** media processor (MP) enables you toocreate a summary of a video that is useful toocustomers who just want toopreview a summary of a long video.</span></span> <span data-ttu-id="db779-107">Ad esempio, i clienti potrebbe essere necessario toosee un breve "riepilogo video" quando si posiziona su un'immagine di anteprima.</span><span class="sxs-lookup"><span data-stu-id="db779-107">For example, customers might want toosee a short "summary video" when they hover over a thumbnail.</span></span> <span data-ttu-id="db779-108">Modificando i parametri di hello di **Azure Media Video anteprime** tramite un set di impostazioni di configurazione, è possibile utilizzare il rilevamento di ripresa potente hello del Management Pack e concatenazione tecnologia tooalgorithmically generare una secondaria descrittiva.</span><span class="sxs-lookup"><span data-stu-id="db779-108">By tweaking hello parameters of **Azure Media Video Thumbnails** through a configuration preset, you can use hello MP's powerful shot detection and concatenation technology tooalgorithmically generate a descriptive subclip.</span></span>  

<span data-ttu-id="db779-109">Hello **anteprima di Azure Media Video** Management Pack è attualmente in anteprima.</span><span class="sxs-lookup"><span data-stu-id="db779-109">hello **Azure Media Video Thumbnail** MP is currently in Preview.</span></span>

<span data-ttu-id="db779-110">In questo argomento fornisce informazioni dettagliate sulle **anteprima di Azure Media Video** e Mostra come toouse con Media Services SDK per .NET.</span><span class="sxs-lookup"><span data-stu-id="db779-110">This topic gives details about  **Azure Media Video Thumbnail** and shows how toouse it with Media Services SDK for .NET.</span></span>

## <a name="limitations"></a><span data-ttu-id="db779-111">Limitazioni</span><span class="sxs-lookup"><span data-stu-id="db779-111">Limitations</span></span>

<span data-ttu-id="db779-112">In alcuni casi, se il video non è costituito da diverse scene, output di hello sarà solo un'unica operazione.</span><span class="sxs-lookup"><span data-stu-id="db779-112">In some cases, if your video is not comprised of different scenes, hello output will only be a single shot.</span></span>

## <a name="video-summary-example"></a><span data-ttu-id="db779-113">Esempio di riepilogo video</span><span class="sxs-lookup"><span data-stu-id="db779-113">Video summary example</span></span>
<span data-ttu-id="db779-114">Di seguito sono riportati alcuni esempi di effettuare il processore di contenuti multimediali Azure Media Video anteprime hello:</span><span class="sxs-lookup"><span data-stu-id="db779-114">Here are some examples of what hello Azure Media Video Thumbnails media processor can do:</span></span>

### <a name="original-video"></a><span data-ttu-id="db779-115">Video originale</span><span class="sxs-lookup"><span data-stu-id="db779-115">Original video</span></span>
[<span data-ttu-id="db779-116">Video originale</span><span class="sxs-lookup"><span data-stu-id="db779-116">Original video</span></span>](http://ampdemo.azureedge.net/azuremediaplayer.html?url=https%3A%2F%2Fnimbuscdn-nimbuspm.streaming.mediaservices.windows.net%2Faed33834-ec2d-4788-88b5-a4505b3d032c%2FMicrosoft%27s%20HoloLens%20Live%20Demonstration.ism%2Fmanifest)

### <a name="video-thumbnail-result"></a><span data-ttu-id="db779-117">Risultato dell'anteprima video</span><span class="sxs-lookup"><span data-stu-id="db779-117">Video thumbnail result</span></span>
[<span data-ttu-id="db779-118">Risultato dell'anteprima video</span><span class="sxs-lookup"><span data-stu-id="db779-118">Video thumbnail result</span></span>](http://ampdemo.azureedge.net/azuremediaplayer.html?url=http%3A%2F%2Fnimbuscdn-nimbuspm.streaming.mediaservices.windows.net%2Ff5c91052-4232-41d4-b531-062e07b6a9ae%2FHololens%2520Demo_VideoThumbnails_MotionThumbnail.mp4)

## <a name="task-configuration-preset"></a><span data-ttu-id="db779-119">Configurazione delle attività (set di impostazioni)</span><span class="sxs-lookup"><span data-stu-id="db779-119">Task configuration (preset)</span></span>
<span data-ttu-id="db779-120">Quando si crea un'attività di anteprima video con **anteprime video multimediali di Azure**, è necessario specificare un set di impostazioni di configurazione.</span><span class="sxs-lookup"><span data-stu-id="db779-120">When creating a video thumbnail task with **Azure Media Video Thumbnails**, you must specify a configuration preset.</span></span> <span data-ttu-id="db779-121">Hello anteprima nell'esempio precedente è stato creato con hello seguente configurazione di base JSON:</span><span class="sxs-lookup"><span data-stu-id="db779-121">hello above thumbnail sample was created with hello following basic JSON configuration:</span></span>

    {"version":"1.0"}

<span data-ttu-id="db779-122">Attualmente, è possibile modificare hello seguenti parametri:</span><span class="sxs-lookup"><span data-stu-id="db779-122">Currently, you can change hello following parameters:</span></span>

| <span data-ttu-id="db779-123">Param</span><span class="sxs-lookup"><span data-stu-id="db779-123">Param</span></span> | <span data-ttu-id="db779-124">Descrizione</span><span class="sxs-lookup"><span data-stu-id="db779-124">Description</span></span> |
| --- | --- |
| <span data-ttu-id="db779-125">outputAudio</span><span class="sxs-lookup"><span data-stu-id="db779-125">outputAudio</span></span> |<span data-ttu-id="db779-126">Specifica se consentire o meno video risultante hello contiene audio.</span><span class="sxs-lookup"><span data-stu-id="db779-126">Specifies whether or not hello resultant video contains any audio.</span></span> <br/><span data-ttu-id="db779-127">I valori consentiti sono: true o false.</span><span class="sxs-lookup"><span data-stu-id="db779-127">Allowed values are: True or False.</span></span> <span data-ttu-id="db779-128">Il valore predefinito è true.</span><span class="sxs-lookup"><span data-stu-id="db779-128">Default is True.</span></span> |
| <span data-ttu-id="db779-129">fadeInFadeOut</span><span class="sxs-lookup"><span data-stu-id="db779-129">fadeInFadeOut</span></span> |<span data-ttu-id="db779-130">Specifica che ha eseguito la transizione dissolvenza vengono utilizzati tra le anteprime di movimento separato hello.</span><span class="sxs-lookup"><span data-stu-id="db779-130">Specifies whether or not fade transitions are used between hello separate motion thumbnails.</span></span>  <br/><span data-ttu-id="db779-131">I valori consentiti sono: true o false.</span><span class="sxs-lookup"><span data-stu-id="db779-131">Allowed values are: True or False.</span></span>  <span data-ttu-id="db779-132">Il valore predefinito è true.</span><span class="sxs-lookup"><span data-stu-id="db779-132">Default is True.</span></span> |
| <span data-ttu-id="db779-133">maxMotionThumbnailDurationInSecs</span><span class="sxs-lookup"><span data-stu-id="db779-133">maxMotionThumbnailDurationInSecs</span></span> |<span data-ttu-id="db779-134">Numero intero che specifica quanto tempo hello intero risultante video deve essere.</span><span class="sxs-lookup"><span data-stu-id="db779-134">Integer that specifies how long hello entire resultant video shall be.</span></span>  <span data-ttu-id="db779-135">Il valore predefinito dipende dalla durata del video originale.</span><span class="sxs-lookup"><span data-stu-id="db779-135">Default depends on original video duration.</span></span> |

<span data-ttu-id="db779-136">Hello nella tabella seguente vengono descritti durata predefinita di hello, quando **maxMotionThumbnailInSecs** non viene utilizzato.</span><span class="sxs-lookup"><span data-stu-id="db779-136">hello following table describes hello default duration, when **maxMotionThumbnailInSecs** is not used.</span></span>

|  |  |  |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="db779-137">Durata del video</span><span class="sxs-lookup"><span data-stu-id="db779-137">Video duration</span></span> |<span data-ttu-id="db779-138">d < 3 min</span><span class="sxs-lookup"><span data-stu-id="db779-138">d < 3 min</span></span> |<span data-ttu-id="db779-139">3 minuti. < d < 15 minuti</span><span class="sxs-lookup"><span data-stu-id="db779-139">3 min < d < 15 min</span></span> |
| <span data-ttu-id="db779-140">Durata dell'anteprima</span><span class="sxs-lookup"><span data-stu-id="db779-140">Thumbnail duration</span></span> |<span data-ttu-id="db779-141">15 sec (2-3 scene)</span><span class="sxs-lookup"><span data-stu-id="db779-141">15 sec (2-3 scenes)</span></span> |<span data-ttu-id="db779-142">30 sec (3-5 scene)</span><span class="sxs-lookup"><span data-stu-id="db779-142">30 sec (3-5 scenes)</span></span> |

<span data-ttu-id="db779-143">Hello JSON seguente imposta i parametri disponibili.</span><span class="sxs-lookup"><span data-stu-id="db779-143">hello following JSON sets available parameters.</span></span>

    {
        "version": "1.0",
        "options": {
            "outputAudio": "true",
            "maxMotionThumbnailDurationInSecs": "10",
            "fadeInFadeOut": "true"
        }
    }

## <a name="net-sample-code"></a><span data-ttu-id="db779-144">Codice di esempio .NET</span><span class="sxs-lookup"><span data-stu-id="db779-144">.NET sample code</span></span>

<span data-ttu-id="db779-145">esempio Hello programma mostra come:</span><span class="sxs-lookup"><span data-stu-id="db779-145">hello following program shows how to:</span></span>

1. <span data-ttu-id="db779-146">Creare un asset e caricare un file multimediale nell'asset hello.</span><span class="sxs-lookup"><span data-stu-id="db779-146">Create an asset and upload a media file into hello asset.</span></span>
2. <span data-ttu-id="db779-147">Crea un processo con un'attività di anteprima video in base a un file di configurazione che contiene i seguenti set di impostazioni json hello.</span><span class="sxs-lookup"><span data-stu-id="db779-147">Creates a job with a video thumbnail task based on a configuration file that contains hello following json preset.</span></span> 
   
        {                
            "version": "1.0",
            "options": {
                "outputAudio": "true",
                "maxMotionThumbnailDurationInSecs": "30",
                "fadeInFadeOut": "false"
            }
        }
3. <span data-ttu-id="db779-148">Scarica i file di output di hello.</span><span class="sxs-lookup"><span data-stu-id="db779-148">Downloads hello output files.</span></span> 

#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="db779-149">Creare e configurare un progetto di Visual Studio</span><span class="sxs-lookup"><span data-stu-id="db779-149">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="db779-150">Configurare l'ambiente di sviluppo e di popolare il file app. config hello con informazioni di connessione, come descritto in [lo sviluppo di servizi multimediali con .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="db779-150">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="db779-151">Esempio</span><span class="sxs-lookup"><span data-stu-id="db779-151">Example</span></span>

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
            // Read values from hello App.config file.
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


                // Run hello thumbnail job.
                var asset = RunVideoThumbnailJob(@"C:\supportFiles\VideoThumbnail\BigBuckBunny.mp4",
                                            @"C:\supportFiles\VideoThumbnail\config.json");

                // Download hello job output asset.
                DownloadAsset(asset, @"C:\supportFiles\VideoThumbnail\Output");
            }

            static IAsset RunVideoThumbnailJob(string inputMediaFilePath, string configurationFile)
            {
                // Create an asset and upload hello input media file toostorage.
                IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
                    "My Video Thumbnail Input Asset",
                    AssetCreationOptions.None);

                // Declare a new job.
                IJob job = _context.Jobs.Create("My Video Thumbnail Job");

                // Get a reference tooAzure Media Video Thumbnails.
                string MediaProcessorName = "Azure Media Video Thumbnails";

                var processor = GetLatestMediaProcessorByName(MediaProcessorName);

                // Read configuration from hello specified file.
                string configuration = File.ReadAllText(configurationFile);

                // Create a task with hello encoding details, using a string preset.
                ITask task = job.Tasks.AddNew("My Video Thumbnail Task",
                    processor,
                    configuration,
                    TaskOptions.None);

                // Specify hello input asset.
                task.InputAssets.Add(asset);

                // Add an output asset toocontain hello results of hello job.
                task.OutputAssets.AddNew("My Video Thumbnail Output Asset", AssetCreationOptions.None);

                // Use hello following event handler toocheck job progress.  
                job.StateChanged += new EventHandler<JobStateChangedEventArgs>(StateChanged);

                // Launch hello job.
                job.Submit();

                // Check job execution and wait for job toofinish.
                Task progressJobTask = job.GetExecutionProgressTask(CancellationToken.None);

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

### <a name="video-thumbnail-output"></a><span data-ttu-id="db779-152">Output di anteprima video</span><span class="sxs-lookup"><span data-stu-id="db779-152">Video thumbnail output</span></span>
[<span data-ttu-id="db779-153">Output di anteprima video</span><span class="sxs-lookup"><span data-stu-id="db779-153">Video thumbnail output</span></span>](http://ampdemo.azureedge.net/azuremediaplayer.html?url=http%3A%2F%2Fnimbuscdn-nimbuspm.streaming.mediaservices.windows.net%2Fd06f24dc-bc81-488e-a8d0-348b7dc41b56%2FHololens%2520Demo_VideoThumbnails_MotionThumbnail.mp4)

## <a name="media-services-learning-paths"></a><span data-ttu-id="db779-154">Percorsi di apprendimento di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="db779-154">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="db779-155">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="db779-155">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="db779-156">Collegamenti correlati</span><span class="sxs-lookup"><span data-stu-id="db779-156">Related links</span></span>
[<span data-ttu-id="db779-157">Panoramica di Analisi servizi multimediali di Azure</span><span class="sxs-lookup"><span data-stu-id="db779-157">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

[<span data-ttu-id="db779-158">Demo di Analisi servizi multimediali di Azure</span><span class="sxs-lookup"><span data-stu-id="db779-158">Azure Media Analytics demos</span></span>](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

