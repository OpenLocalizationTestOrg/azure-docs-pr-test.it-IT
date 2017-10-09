---
title: "un'attività di codifica di servizi multimediali di Azure che genera l'errore fMP4 blocchi aaaCreate | Documenti Microsoft"
description: "Questo argomento viene illustrato come toocreate un'attività di codifica che genera l'errore fMP4 blocchi. Quando questa attività viene utilizzata con hello Media Encoder Standard o di flusso di lavoro Premium del codificatore multimediale codificatore, hello asset di output conterrà i blocchi fMP4 anziché file ISO MP4."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: b7029ac5-eadd-4a2f-8111-1fc460828981
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: juliako
ms.openlocfilehash: 388f3ccb9865b5c4e159af86d5a9ee2f4e3f6120
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
#  <a name="create-an-encoding-task-that-generates-fmp4-chunks"></a><span data-ttu-id="2d7bd-104">Creare un'attività di codifica che genera blocchi fMP4</span><span class="sxs-lookup"><span data-stu-id="2d7bd-104">Create an encoding task that generates fMP4 chunks</span></span>

## <a name="overview"></a><span data-ttu-id="2d7bd-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="2d7bd-105">Overview</span></span>

<span data-ttu-id="2d7bd-106">Questo argomento viene illustrato come un'attività di codifica che genera l'errore toocreate MP4 frammentato (fMP4) blocchi anziché file ISO MP4.</span><span class="sxs-lookup"><span data-stu-id="2d7bd-106">This topic shows how toocreate an encoding task that generates fragmented MP4 (fMP4) chunks instead of ISO MP4 files.</span></span> <span data-ttu-id="2d7bd-107">toogenerate fMP4 blocchi, utilizzare hello **Media Encoder Standard** o **flusso di lavoro Premium del codificatore multimediale** toocreate codificatore una codifica di attività e specificare anche  **AssetFormatOption.AdaptiveStreaming** opzione, come illustrato nel frammento di codice seguente:</span><span class="sxs-lookup"><span data-stu-id="2d7bd-107">toogenerate fMP4 chunks, use hello **Media Encoder Standard** or **Media Encoder Premium Workflow** encoder toocreate an encoding task and also specify **AssetFormatOption.AdaptiveStreaming** option, as shown in this code snippet:</span></span>  
    
    task.OutputAssets.AddNew(@"Output Asset containing fMP4 chunks", 
            options: AssetCreationOptions.None, 
            formatOption: AssetFormatOption.AdaptiveStreaming);


## <span data-ttu-id="2d7bd-108"><a id="encoding_with_dotnet"></a>Codifica con l’SDK .NET dei servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="2d7bd-108"><a id="encoding_with_dotnet"></a>Encoding with Media Services .NET SDK</span></span>

<span data-ttu-id="2d7bd-109">esempio di codice seguente Hello utilizza hello tooperform Media Services .NET SDK seguenti attività:</span><span class="sxs-lookup"><span data-stu-id="2d7bd-109">hello following code example uses Media Services .NET SDK tooperform hello following tasks:</span></span>

- <span data-ttu-id="2d7bd-110">Creare un processo di codifica.</span><span class="sxs-lookup"><span data-stu-id="2d7bd-110">Create an encoding job.</span></span>
- <span data-ttu-id="2d7bd-111">Ottenere un riferimento toohello **Media Encoder Standard** codificatore.</span><span class="sxs-lookup"><span data-stu-id="2d7bd-111">Get a reference toohello **Media Encoder Standard** encoder.</span></span>
- <span data-ttu-id="2d7bd-112">Aggiungere un processo di codifica attività toohello e specificare hello toouse **il flusso adattivo** predefinito.</span><span class="sxs-lookup"><span data-stu-id="2d7bd-112">Add an encoding task toohello job and specify toouse hello **Adaptive Streaming** preset.</span></span> 
- <span data-ttu-id="2d7bd-113">Creare un asset di output che contiene blocchi fMP4 e un file con estensione ISM.</span><span class="sxs-lookup"><span data-stu-id="2d7bd-113">Create an output asset that will contain fMP4 chunks and an .ism file.</span></span>
- <span data-ttu-id="2d7bd-114">Aggiungere un avanzamento del processo hello toocheck gestore dell'evento.</span><span class="sxs-lookup"><span data-stu-id="2d7bd-114">Add an event handler toocheck hello job progress.</span></span>
- <span data-ttu-id="2d7bd-115">Inviare il processo di hello.</span><span class="sxs-lookup"><span data-stu-id="2d7bd-115">Submit hello job.</span></span>

#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="2d7bd-116">Creare e configurare un progetto di Visual Studio</span><span class="sxs-lookup"><span data-stu-id="2d7bd-116">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="2d7bd-117">Configurare l'ambiente di sviluppo e di popolare il file app. config hello con informazioni di connessione, come descritto in [lo sviluppo di servizi multimediali con .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="2d7bd-117">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="2d7bd-118">Esempio</span><span class="sxs-lookup"><span data-stu-id="2d7bd-118">Example</span></span>

    using System;
    using System.Configuration;
    using System.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Threading;

    namespace AdaptiveStreaming
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

            // Get an uploaded asset.
            var asset = _context.Assets.FirstOrDefault();

            // Encode and generate hello output using hello "Adaptive Streaming" preset.
            EncodeToAdaptiveBitrateMP4Set(asset);

            Console.ReadLine();
        }
        static public IAsset EncodeToAdaptiveBitrateMP4Set(IAsset asset)
        {
            // Declare a new job.
            IJob job = _context.Jobs.Create("Media Encoder Standard Job");

            // Get a media processor reference, and pass tooit hello name of hello 
            // processor toouse for hello specific task.
            IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

            // Create a task
            ITask task = job.Tasks.AddNew("Media Encoder Standard encoding task",
            processor,
            "Adaptive Streaming",
            TaskOptions.None);

            // Specify hello input asset toobe encoded.
            task.InputAssets.Add(asset);

            // Add an output asset toocontain hello results of hello job. 

            // This output is specified as AssetCreationOptions.None, which 
            // means hello output asset is not encrypted. 
            // It is also specified toouse AssetFormatOption.AdaptiveStreaming, 
            // which means hello output asset will contain fMP4 chunks.

            task.OutputAssets.AddNew(@"Output Asset containing fMP4 chunks",
            options: AssetCreationOptions.None,
            formatOption: AssetFormatOption.AdaptiveStreaming);

            job.StateChanged += new EventHandler<JobStateChangedEventArgs>(JobStateChanged);
            job.Submit();
            job.GetExecutionProgressTask(CancellationToken.None).Wait();

            return job.OutputMediaAssets[0];
        }
        private static void JobStateChanged(object sender, JobStateChangedEventArgs e)
        {
            Console.WriteLine("Job state changed event:");
            Console.WriteLine("  Previous state: " + e.PreviousState);
            Console.WriteLine("  Current state: " + e.CurrentState);
            switch (e.CurrentState)
            {
            case JobState.Finished:
                Console.WriteLine();
                Console.WriteLine("Job is finished. Please wait while local tasks or downloads complete...");
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
                break;
            default:
                break;
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
        }
    }

## <a name="media-services-learning-paths"></a><span data-ttu-id="2d7bd-119">Percorsi di apprendimento di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="2d7bd-119">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="2d7bd-120">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="2d7bd-120">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="2d7bd-121">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="2d7bd-121">See Also</span></span>
[<span data-ttu-id="2d7bd-122">Panoramica sulla codifica dei servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="2d7bd-122">Media Services Encoding Overview</span></span>](media-services-encode-asset.md)

