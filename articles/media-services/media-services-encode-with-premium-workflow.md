---
title: Codifica avanzata con il flusso di lavoro Premium del codificatore multimediale | Microsoft Docs
description: Informazioni su come codificare con il flusso di lavoro Premium del codificatore multimediale. Negli esempi di codice, scritti in C#, viene usato Media Services SDK per .NET.
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 0f4c87ac-810a-4d42-8df8-923dff2016c6
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: juliako
ms.openlocfilehash: 2b03853bf07e05c07fd730d5e8a8563963887921
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="advanced-encoding-with-media-encoder-premium-workflow"></a><span data-ttu-id="5bbc6-104">Codifica avanzata con il flusso di lavoro Premium del codificatore multimediale</span><span class="sxs-lookup"><span data-stu-id="5bbc6-104">Advanced encoding with Media Encoder Premium Workflow</span></span>
> [!NOTE]
> <span data-ttu-id="5bbc6-105">Il processore di contenuti multimediali del flusso di lavoro Premium del codificatore multimediale descritto in questo argomento non è disponibile in Cina.</span><span class="sxs-lookup"><span data-stu-id="5bbc6-105">Media Encoder Premium Workflow media processor discussed in this topic is not available in China.</span></span>
>
>

<span data-ttu-id="5bbc6-106">Per domande relative al codificatore Premium, inviare mepd tramite un messaggio di posta elettronica a Microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="5bbc6-106">For premium encoder questions, email mepd at Microsoft.com.</span></span>

## <a name="overview"></a><span data-ttu-id="5bbc6-107">Panoramica</span><span class="sxs-lookup"><span data-stu-id="5bbc6-107">Overview</span></span>
<span data-ttu-id="5bbc6-108">Servizi multimediali di Microsoft Azure offre il processore di contenuti multimediali **Flusso di lavoro Premium del codificatore multimediale** .</span><span class="sxs-lookup"><span data-stu-id="5bbc6-108">Microsoft Azure Media Services is introducing the **Media Encoder Premium Workflow** media processor.</span></span> <span data-ttu-id="5bbc6-109">Questo processore offre funzionalità di codifica avanzata per i flussi di lavoro Premium su richiesta.</span><span class="sxs-lookup"><span data-stu-id="5bbc6-109">This processor offers advance encoding capabilities for your premium on-demand workflows.</span></span>

<span data-ttu-id="5bbc6-110">Gli argomenti seguenti includono informazioni dettagliate sul **flusso di lavoro Premium del codificatore multimediale**:</span><span class="sxs-lookup"><span data-stu-id="5bbc6-110">The following topics outline details related to **Media Encoder Premium Workflow**:</span></span>

* <span data-ttu-id="5bbc6-111">[Formati supportati da Flusso di lavoro Premium del codificatore multimediale](media-services-premium-workflow-encoder-formats.md) : vengono illustrati formati file e codec supportati da **Flusso di lavoro Premium del codificatore multimediale**.</span><span class="sxs-lookup"><span data-stu-id="5bbc6-111">[Formats Supported by the Media Encoder Premium Workflow](media-services-premium-workflow-encoder-formats.md) – Discusses the file formats and codecs supported by **Media Encoder Premium Workflow**.</span></span>
* <span data-ttu-id="5bbc6-112">[Panoramica e confronto dei codificatori multimediali su richiesta di Azure](media-services-encode-asset.md) mette a confronto le funzionalità di codifica del **flusso di lavoro Premium del codificatore multimediale** e di **Media Encoder Standard**.</span><span class="sxs-lookup"><span data-stu-id="5bbc6-112">[Overview and comparison of Azure on demand media encoders](media-services-encode-asset.md) compares the encoding capabilities of **Media Encoder Premium Workflow** and **Media Encoder Standard**.</span></span>

<span data-ttu-id="5bbc6-113">Questo argomento illustra come codificare con il **flusso di lavoro Premium del codificatore multimediale** mediante .NET.</span><span class="sxs-lookup"><span data-stu-id="5bbc6-113">This topic demonstrates how to encode with **Media Encoder Premium Workflow** using .NET.</span></span>

<span data-ttu-id="5bbc6-114">Le attività di codifica per **Flusso di lavoro Premium del codificatore multimediale** richiedono un file di configurazione separato, denominato file del flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="5bbc6-114">Encoding tasks for the **Media Encoder Premium Workflow** require a separate configuration file, called a Workflow file.</span></span> <span data-ttu-id="5bbc6-115">Questi file con estensione workflow vengono creati mediante lo strumento [Progettazione flussi di lavoro](media-services-workflow-designer.md) .</span><span class="sxs-lookup"><span data-stu-id="5bbc6-115">These files have a .workflow extension and are created using the [Workflow Designer](media-services-workflow-designer.md) tool.</span></span>

<span data-ttu-id="5bbc6-116">I file del flusso di lavoro predefiniti sono disponibili anche [qui](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows).</span><span class="sxs-lookup"><span data-stu-id="5bbc6-116">You can also get the default workflow files [here](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows).</span></span> <span data-ttu-id="5bbc6-117">Nella cartella è presente anche una descrizione dei file.</span><span class="sxs-lookup"><span data-stu-id="5bbc6-117">The folder also contains the description of these files.</span></span>

<span data-ttu-id="5bbc6-118">I file del flusso di lavoro devono essere caricati come asset nel proprio account di Servizi multimediali e questo asset deve essere passato all'attività di codifica.</span><span class="sxs-lookup"><span data-stu-id="5bbc6-118">The workflow files need to be uploaded to your Media Services account as an Asset, and this Asset should be passed in to the encoding Task.</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="5bbc6-119">Creare e configurare un progetto di Visual Studio</span><span class="sxs-lookup"><span data-stu-id="5bbc6-119">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="5bbc6-120">Configurare l'ambiente di sviluppo e popolare il file app.config con le informazioni di connessione, come descritto in [Sviluppo di applicazioni di Servizi multimediali con .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="5bbc6-120">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

## <a name="encoding-example"></a><span data-ttu-id="5bbc6-121">Esempio di codifica</span><span class="sxs-lookup"><span data-stu-id="5bbc6-121">Encoding example</span></span>

<span data-ttu-id="5bbc6-122">Il seguente esempio dimostra come codificare con **Flusso di lavoro Premium del codificatore multimediale**.</span><span class="sxs-lookup"><span data-stu-id="5bbc6-122">The following example demonstrates how to encode with **Media Encoder Premium Workflow**.</span></span>

<span data-ttu-id="5bbc6-123">Vengono eseguiti questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="5bbc6-123">The following steps are performed:</span></span>

1. <span data-ttu-id="5bbc6-124">Creare un asset e caricare un file del flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="5bbc6-124">Create an asset and upload a workflow file.</span></span>
2. <span data-ttu-id="5bbc6-125">Creare un asset e caricare un file multimediale di origine.</span><span class="sxs-lookup"><span data-stu-id="5bbc6-125">Create an asset and upload a source media file.</span></span>
3. <span data-ttu-id="5bbc6-126">Ottenere il processore di contenuti multimediali "Flusso di lavoro Premium del codificatore multimediale".</span><span class="sxs-lookup"><span data-stu-id="5bbc6-126">Get the "Media Encoder Premium Workflow" media processor.</span></span>
4. <span data-ttu-id="5bbc6-127">Creare un processo e un'attività.</span><span class="sxs-lookup"><span data-stu-id="5bbc6-127">Create a job and a task.</span></span>

    <span data-ttu-id="5bbc6-128">Nella maggior parte dei casi, la stringa di configurazione per l'attività è vuota (come nell'esempio seguente).</span><span class="sxs-lookup"><span data-stu-id="5bbc6-128">In most cases, the configuration string for the task is empty (like in the following example).</span></span> <span data-ttu-id="5bbc6-129">Esistono alcuni scenari avanzati in cui è necessario impostare dinamicamente le proprietà di runtime. In questo caso, specificare una stringa XML nell'attività di codifica.</span><span class="sxs-lookup"><span data-stu-id="5bbc6-129">There are some advanced scenarios (that require you to to set runtime properties dynamically) in which case you would provide an XML string to the encoding task.</span></span> <span data-ttu-id="5bbc6-130">Esempi di tali scenari sono: creazione di un overlay, unione sequenziale o parallela di supporti e aggiunta di sottotitoli.</span><span class="sxs-lookup"><span data-stu-id="5bbc6-130">Examples of such scenarios are: creating an overlay, parallel or sequential media stitching, subtitling.</span></span>
5. <span data-ttu-id="5bbc6-131">Aggiungere due asset di input all'attività.</span><span class="sxs-lookup"><span data-stu-id="5bbc6-131">Add two input assets to the task.</span></span>

    1. <span data-ttu-id="5bbc6-132">In primo luogo, l'asset del flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="5bbc6-132">1st – the workflow asset.</span></span>
    2. <span data-ttu-id="5bbc6-133">In secondo luogo, l'asset video.</span><span class="sxs-lookup"><span data-stu-id="5bbc6-133">2nd – the video asset.</span></span>

    >[!NOTE]
    ><span data-ttu-id="5bbc6-134">La risorsa del flusso di lavoro deve essere aggiunta all'attività prima della risorsa del file multimediale.</span><span class="sxs-lookup"><span data-stu-id="5bbc6-134">The workflow asset must be added to the task before the media asset.</span></span>
   <span data-ttu-id="5bbc6-135">La stringa di configurazione per questa attività deve essere vuota.</span><span class="sxs-lookup"><span data-stu-id="5bbc6-135">The configuration string for this task should be empty.</span></span>
   
6. <span data-ttu-id="5bbc6-136">Inviare il processo di codifica.</span><span class="sxs-lookup"><span data-stu-id="5bbc6-136">Submit the encoding job.</span></span>

        using System;
        using System.Linq;
        using System.Configuration;
        using System.IO;
        using System.Threading;
        using System.Threading.Tasks;
        using Microsoft.WindowsAzure.MediaServices.Client;

        namespace MediaEncoderPremiumWorkflowSample
        {
            class Program
            {
                private static readonly string _AADTenantDomain =
                    ConfigurationManager.AppSettings["AADTenantDomain"];
                private static readonly string _RESTAPIEndpoint =
                    ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

                // Field for service context.
                private static CloudMediaContext _context = null;

                private static readonly string _supportFiles =
                    Path.GetFullPath(@"../..\Media");

                private static readonly string _workflowFilePath =
                    Path.GetFullPath(_supportFiles + @"\H264 Progressive Download MP4.workflow");

                private static readonly string _singleMP4InputFilePath =
                    Path.GetFullPath(_supportFiles + @"\BigBuckBunny.mp4");

                static void Main(string[] args)
                {
                    var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
                    var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

                    _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

                    var workflowAsset = CreateAssetAndUploadSingleFile(_workflowFilePath);
                    var videoAsset = CreateAssetAndUploadSingleFile(_singleMP4InputFilePath);
                    IAsset outputAsset = CreateEncodingJob(workflowAsset, videoAsset);

                }

                static public IAsset CreateAssetAndUploadSingleFile(string singleFilePath)
                {
                    var assetName = "UploadSingleFile_" + DateTime.UtcNow.ToString();
                    var asset = _context.Assets.Create(assetName, AssetCreationOptions.None);

                    var fileName = Path.GetFileName(singleFilePath);

                    var assetFile = asset.AssetFiles.Create(fileName);

                    Console.WriteLine("Created assetFile {0}", assetFile.Name);

                    Console.WriteLine("Upload {0}", assetFile.Name);

                    assetFile.Upload(singleFilePath);
                    Console.WriteLine("Done uploading {0}", assetFile.Name);

                    return asset;
                }

                static public IAsset CreateEncodingJob(IAsset workflow, IAsset video)
                {
                    // Declare a new job.
                    IJob job = _context.Jobs.Create("Premium Workflow encoding job");
                    // Get a media processor reference, and pass to it the name of the
                    // processor to use for the specific task.
                    IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Premium Workflow");

                    // Create a task with the encoding details, using a string preset.
                    ITask task = job.Tasks.AddNew("Premium Workflow encoding task",
                        processor,
                        "",
                        TaskOptions.None);

                    // Specify the input asset to be encoded.
                    task.InputAssets.Add(workflow);
                    task.InputAssets.Add(video); // we add one asset
                                                 // Add an output asset to contain the results of the job.
                                                 // This output is specified as AssetCreationOptions.None, which
                                                 // means the output asset is not encrypted.
                    task.OutputAssets.AddNew("Output asset",
                        AssetCreationOptions.None);

                    // Use the following event handler to check job progress.  
                    job.StateChanged += new
                            EventHandler<JobStateChangedEventArgs>(StateChanged);

                    // Launch the job.
                    job.Submit();

                    // Check job execution and wait for job to finish.
                    Task progressJobTask = job.GetExecutionProgressTask(CancellationToken.None);
                    progressJobTask.Wait();

                    // If job state is Error the event handling
                    // method for job progress should log errors.  Here we check
                    // for error state and exit if needed.
                    if (job.State == JobState.Error)
                    {
                        throw new Exception("\nExiting method due to job error.");
                    }

                    return job.OutputMediaAssets[0];
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

<span data-ttu-id="5bbc6-137">Per domande relative al codificatore Premium, inviare mepd tramite un messaggio di posta elettronica a Microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="5bbc6-137">For premium encoder questions, email mepd at Microsoft.com.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="5bbc6-138">Percorsi di apprendimento di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="5bbc6-138">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="5bbc6-139">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="5bbc6-139">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
