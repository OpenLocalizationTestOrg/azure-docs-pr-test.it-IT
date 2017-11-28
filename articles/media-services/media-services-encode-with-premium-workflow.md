---
title: aaaAdvanced codifica con flusso di lavoro Premium del codificatore multimediale | Documenti Microsoft
description: Informazioni su come tooencode con flusso di lavoro Premium del codificatore multimediale. Esempi di codice sono scritti in c# e utilizzano hello Media Services SDK per .NET.
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
ms.openlocfilehash: 5a1c3d019a5c8fbf9bda2da751a7eff4c4907d97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-encoding-with-media-encoder-premium-workflow"></a><span data-ttu-id="ffe15-104">Codifica avanzata con il flusso di lavoro Premium del codificatore multimediale</span><span class="sxs-lookup"><span data-stu-id="ffe15-104">Advanced encoding with Media Encoder Premium Workflow</span></span>
> [!NOTE]
> <span data-ttu-id="ffe15-105">Il processore di contenuti multimediali del flusso di lavoro Premium del codificatore multimediale descritto in questo argomento non è disponibile in Cina.</span><span class="sxs-lookup"><span data-stu-id="ffe15-105">Media Encoder Premium Workflow media processor discussed in this topic is not available in China.</span></span>
>
>

<span data-ttu-id="ffe15-106">Per domande relative al codificatore Premium, inviare mepd tramite un messaggio di posta elettronica a Microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="ffe15-106">For premium encoder questions, email mepd at Microsoft.com.</span></span>

## <a name="overview"></a><span data-ttu-id="ffe15-107">Panoramica</span><span class="sxs-lookup"><span data-stu-id="ffe15-107">Overview</span></span>
<span data-ttu-id="ffe15-108">Servizi multimediali di Microsoft Azure ha introdotto hello **flusso di lavoro Premium del codificatore multimediale** processore di contenuti multimediali.</span><span class="sxs-lookup"><span data-stu-id="ffe15-108">Microsoft Azure Media Services is introducing hello **Media Encoder Premium Workflow** media processor.</span></span> <span data-ttu-id="ffe15-109">Questo processore offre funzionalità di codifica avanzata per i flussi di lavoro Premium su richiesta.</span><span class="sxs-lookup"><span data-stu-id="ffe15-109">This processor offers advance encoding capabilities for your premium on-demand workflows.</span></span>

<span data-ttu-id="ffe15-110">Negli argomenti seguenti vengono Hello descrive i dettagli correlati troppo**flusso di lavoro Premium del codificatore multimediale**:</span><span class="sxs-lookup"><span data-stu-id="ffe15-110">hello following topics outline details related too**Media Encoder Premium Workflow**:</span></span>

* <span data-ttu-id="ffe15-111">[Formati supportati dal flusso di lavoro Premium del codificatore multimediale hello](media-services-premium-workflow-encoder-formats.md) : vengono illustrati i formati di file hello e codec supportati da **flusso di lavoro Premium del codificatore multimediale**.</span><span class="sxs-lookup"><span data-stu-id="ffe15-111">[Formats Supported by hello Media Encoder Premium Workflow](media-services-premium-workflow-encoder-formats.md) – Discusses hello file formats and codecs supported by **Media Encoder Premium Workflow**.</span></span>
* <span data-ttu-id="ffe15-112">[Panoramica e un confronto di Azure in codificatori media richiesta](media-services-encode-asset.md) Confronta hello le funzionalità di codifica di **flusso di lavoro Premium del codificatore multimediale** e **Media Encoder Standard**.</span><span class="sxs-lookup"><span data-stu-id="ffe15-112">[Overview and comparison of Azure on demand media encoders](media-services-encode-asset.md) compares hello encoding capabilities of **Media Encoder Premium Workflow** and **Media Encoder Standard**.</span></span>

<span data-ttu-id="ffe15-113">Questo argomento viene illustrato come tooencode con **flusso di lavoro Premium del codificatore multimediale** usando .NET.</span><span class="sxs-lookup"><span data-stu-id="ffe15-113">This topic demonstrates how tooencode with **Media Encoder Premium Workflow** using .NET.</span></span>

<span data-ttu-id="ffe15-114">Codifica di attività per hello **flusso di lavoro Premium del codificatore multimediale** richiedono un file di configurazione separato, denominato file del flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="ffe15-114">Encoding tasks for hello **Media Encoder Premium Workflow** require a separate configuration file, called a Workflow file.</span></span> <span data-ttu-id="ffe15-115">Tali file hanno estensione .workflow e vengono creati utilizzando hello [Progettazione flussi di lavoro](media-services-workflow-designer.md) strumento.</span><span class="sxs-lookup"><span data-stu-id="ffe15-115">These files have a .workflow extension and are created using hello [Workflow Designer](media-services-workflow-designer.md) tool.</span></span>

<span data-ttu-id="ffe15-116">È inoltre possibile ottenere predefinito hello i file del flusso di lavoro [qui](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows).</span><span class="sxs-lookup"><span data-stu-id="ffe15-116">You can also get hello default workflow files [here](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows).</span></span> <span data-ttu-id="ffe15-117">cartella Hello contiene inoltre descrizione hello di questi file.</span><span class="sxs-lookup"><span data-stu-id="ffe15-117">hello folder also contains hello description of these files.</span></span>

<span data-ttu-id="ffe15-118">file di flusso di lavoro Hello devono toobe caricato tooyour di account di servizi multimediali come Asset, e questo Asset deve essere passato nell'attività di codifica toohello.</span><span class="sxs-lookup"><span data-stu-id="ffe15-118">hello workflow files need toobe uploaded tooyour Media Services account as an Asset, and this Asset should be passed in toohello encoding Task.</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="ffe15-119">Creare e configurare un progetto di Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ffe15-119">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="ffe15-120">Configurare l'ambiente di sviluppo e di popolare il file app. config hello con informazioni di connessione, come descritto in [lo sviluppo di servizi multimediali con .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="ffe15-120">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

## <a name="encoding-example"></a><span data-ttu-id="ffe15-121">Esempio di codifica</span><span class="sxs-lookup"><span data-stu-id="ffe15-121">Encoding example</span></span>

<span data-ttu-id="ffe15-122">Hello esempio seguente viene illustrato come tooencode con **flusso di lavoro Premium del codificatore multimediale**.</span><span class="sxs-lookup"><span data-stu-id="ffe15-122">hello following example demonstrates how tooencode with **Media Encoder Premium Workflow**.</span></span>

<span data-ttu-id="ffe15-123">viene eseguita Hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="ffe15-123">hello following steps are performed:</span></span>

1. <span data-ttu-id="ffe15-124">Creare un asset e caricare un file del flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="ffe15-124">Create an asset and upload a workflow file.</span></span>
2. <span data-ttu-id="ffe15-125">Creare un asset e caricare un file multimediale di origine.</span><span class="sxs-lookup"><span data-stu-id="ffe15-125">Create an asset and upload a source media file.</span></span>
3. <span data-ttu-id="ffe15-126">Ottenere processore di contenuti multimediali hello "Media Encoder Premium del flusso di lavoro".</span><span class="sxs-lookup"><span data-stu-id="ffe15-126">Get hello "Media Encoder Premium Workflow" media processor.</span></span>
4. <span data-ttu-id="ffe15-127">Creare un processo e un'attività.</span><span class="sxs-lookup"><span data-stu-id="ffe15-127">Create a job and a task.</span></span>

    <span data-ttu-id="ffe15-128">Nella maggior parte dei casi, la stringa di configurazione per l'attività hello hello è vuota (come nel seguente esempio hello).</span><span class="sxs-lookup"><span data-stu-id="ffe15-128">In most cases, hello configuration string for hello task is empty (like in hello following example).</span></span> <span data-ttu-id="ffe15-129">Esistono alcuni scenari avanzati (che richiedono in modo dinamico la proprietà di runtime tootooset) in questo caso è necessario fornire un'attività di codifica toohello di stringa XML.</span><span class="sxs-lookup"><span data-stu-id="ffe15-129">There are some advanced scenarios (that require you tootooset runtime properties dynamically) in which case you would provide an XML string toohello encoding task.</span></span> <span data-ttu-id="ffe15-130">Esempi di tali scenari sono: creazione di un overlay, unione sequenziale o parallela di supporti e aggiunta di sottotitoli.</span><span class="sxs-lookup"><span data-stu-id="ffe15-130">Examples of such scenarios are: creating an overlay, parallel or sequential media stitching, subtitling.</span></span>
5. <span data-ttu-id="ffe15-131">Aggiungere due attività di toohello asset di input.</span><span class="sxs-lookup"><span data-stu-id="ffe15-131">Add two input assets toohello task.</span></span>

    1. <span data-ttu-id="ffe15-132">1 ° – asset di hello del flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="ffe15-132">1st – hello workflow asset.</span></span>
    2. <span data-ttu-id="ffe15-133">2 – asset video hello.</span><span class="sxs-lookup"><span data-stu-id="ffe15-133">2nd – hello video asset.</span></span>

    >[!NOTE]
    ><span data-ttu-id="ffe15-134">asset del flusso di lavoro Hello devono essere aggiunti toohello attività prima di asset di file multimediali hello.</span><span class="sxs-lookup"><span data-stu-id="ffe15-134">hello workflow asset must be added toohello task before hello media asset.</span></span>
   <span data-ttu-id="ffe15-135">stringa di configurazione Hello per questa attività deve essere vuota.</span><span class="sxs-lookup"><span data-stu-id="ffe15-135">hello configuration string for this task should be empty.</span></span>
   
6. <span data-ttu-id="ffe15-136">Inviare il processo di codifica hello.</span><span class="sxs-lookup"><span data-stu-id="ffe15-136">Submit hello encoding job.</span></span>

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
                    // Get a media processor reference, and pass tooit hello name of the
                    // processor toouse for hello specific task.
                    IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Premium Workflow");

                    // Create a task with hello encoding details, using a string preset.
                    ITask task = job.Tasks.AddNew("Premium Workflow encoding task",
                        processor,
                        "",
                        TaskOptions.None);

                    // Specify hello input asset toobe encoded.
                    task.InputAssets.Add(workflow);
                    task.InputAssets.Add(video); // we add one asset
                                                 // Add an output asset toocontain hello results of hello job.
                                                 // This output is specified as AssetCreationOptions.None, which
                                                 // means hello output asset is not encrypted.
                    task.OutputAssets.AddNew("Output asset",
                        AssetCreationOptions.None);

                    // Use hello following event handler toocheck job progress.  
                    job.StateChanged += new
                            EventHandler<JobStateChangedEventArgs>(StateChanged);

                    // Launch hello job.
                    job.Submit();

                    // Check job execution and wait for job toofinish.
                    Task progressJobTask = job.GetExecutionProgressTask(CancellationToken.None);
                    progressJobTask.Wait();

                    // If job state is Error hello event handling
                    // method for job progress should log errors.  Here we check
                    // for error state and exit if needed.
                    if (job.State == JobState.Error)
                    {
                        throw new Exception("\nExiting method due toojob error.");
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

<span data-ttu-id="ffe15-137">Per domande relative al codificatore Premium, inviare mepd tramite un messaggio di posta elettronica a Microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="ffe15-137">For premium encoder questions, email mepd at Microsoft.com.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="ffe15-138">Percorsi di apprendimento di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="ffe15-138">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="ffe15-139">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="ffe15-139">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
