---
title: "tooauto Azure Media Encoder Standard aaaUse-generare una scala di velocità in bit | Documenti Microsoft"
description: "Questo argomento viene illustrato come toouse Media codificatore Standard (MES) tooauto-generare una scala di velocità in bit in base alla risoluzione di input hello e alla velocità in bit. velocità in bit e la risoluzione di input hello mai essere superati. Ad esempio, se l'input hello è 720p 3 Mbps, l'output verrà rimangono nella migliore delle ipotesi 720p e inizierà a velocità inferiore a 3 Mbps."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 63ed95da-1b82-44b0-b8ff-eebd535bc5c7
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: juliako
ms.openlocfilehash: 5437f54ac28c42ddd4f9d1986549d6da6261c5da
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
#  <a name="use-azure-media-encoder-standard-tooauto-generate-a-bitrate-ladder"></a><span data-ttu-id="00b49-105">Usare Azure Media Encoder Standard tooauto-generare una scala di velocità in bit</span><span class="sxs-lookup"><span data-stu-id="00b49-105">Use Azure Media Encoder Standard tooauto-generate a bitrate ladder</span></span>

## <a name="overview"></a><span data-ttu-id="00b49-106">Panoramica</span><span class="sxs-lookup"><span data-stu-id="00b49-106">Overview</span></span>

<span data-ttu-id="00b49-107">Questo argomento viene illustrato come toouse Media codificatore Standard (MES) tooauto-generare una scala di velocità in bit (coppie di risoluzione a velocità in bit) in base alla risoluzione di input hello e alla velocità in bit.</span><span class="sxs-lookup"><span data-stu-id="00b49-107">This topic shows how toouse Media Encoder Standard (MES) tooauto-generate a bitrate ladder (bitrate-resolution pairs) based on hello input resolution and bitrate.</span></span> <span data-ttu-id="00b49-108">Hello predefinito generato automaticamente non supererà mai velocità in bit e la risoluzione di hello di input.</span><span class="sxs-lookup"><span data-stu-id="00b49-108">hello auto-generated preset will never exceed hello input resolution and bitrate.</span></span> <span data-ttu-id="00b49-109">Ad esempio, se l'input hello è 720p 3 Mbps, l'output verrà rimangono nella migliore delle ipotesi 720p e inizierà a velocità inferiore a 3 Mbps.</span><span class="sxs-lookup"><span data-stu-id="00b49-109">For example, if hello input is 720p at 3Mbps, output will remain 720p at best, and will start at rates lower than 3Mbps.</span></span>

### <a name="encoding-for-streaming-only"></a><span data-ttu-id="00b49-110">Codifica solo per lo streaming</span><span class="sxs-lookup"><span data-stu-id="00b49-110">Encoding for Streaming Only</span></span>

<span data-ttu-id="00b49-111">Se si tooencode l'origine video solo per i flussi, quindi si è necessario utilizzare "Streaming adattivo" hello predefinito durante la creazione di un'attività di codifica.</span><span class="sxs-lookup"><span data-stu-id="00b49-111">If your intent is tooencode your source video only for streaming, then you shoud use hello "Adaptive Streaming" preset when creating an encoding task.</span></span> <span data-ttu-id="00b49-112">Quando si utilizza hello **il flusso adattivo** codificatore MES hello verrà predefinito, in modo intelligente chiudere una scala di velocità in bit.</span><span class="sxs-lookup"><span data-stu-id="00b49-112">When using hello **Adaptive Streaming** preset, hello MES encoder will intelligently cap a bitrate ladder.</span></span> <span data-ttu-id="00b49-113">Tuttavia, non sarà in grado di toocontrol hello codifica i costi, poiché il servizio di hello determina quanti livelli toouse e la risoluzione.</span><span class="sxs-lookup"><span data-stu-id="00b49-113">However, you will not be able toocontrol hello encoding costs, since hello service determines how many layers toouse and at what resolution.</span></span> <span data-ttu-id="00b49-114">È possibile visualizzare esempi dei livelli di output prodotti da MES in seguito alla codifica con hello **il flusso adattivo** predefinito alla fine di hello di questo argomento.</span><span class="sxs-lookup"><span data-stu-id="00b49-114">You can see examples of output layers produced by MES as a result of encoding with hello **Adaptive Streaming** preset at hello end of this topic.</span></span> <span data-ttu-id="00b49-115">Hello output Asset conterrà i file MP4 in audio e video non sono interlacciati.</span><span class="sxs-lookup"><span data-stu-id="00b49-115">hello output Asset will contain MP4 files where audio and video are not interleaved.</span></span>

### <a name="encoding-for-streaming-and-progressive-download"></a><span data-ttu-id="00b49-116">Codifica per streaming e download progressivo</span><span class="sxs-lookup"><span data-stu-id="00b49-116">Encoding for Streaming and Progressive Download</span></span>

<span data-ttu-id="00b49-117">Se si tooencode del video di origine per i flussi e i file MP4 tooproduce per il download progressivo, quindi si è necessario utilizzare "Contenuto adattivo più velocità in bit MP4" hello predefinito durante la creazione di un'attività di codifica.</span><span class="sxs-lookup"><span data-stu-id="00b49-117">If your intent is tooencode your source video for streaming as well as tooproduce MP4 files for progressive download, then you shoud use hello "Content Adaptive Multiple Bitrate MP4" preset when creating an encoding task.</span></span> <span data-ttu-id="00b49-118">Quando si utilizza hello **contenuto file MP4 a velocità in bit adattiva più** preimpostato, codificatore MES hello applicherà hello stessa logica codifica, come illustrato in precedenza, ma ora asset di output di hello conterrà MP4 di file audio e video sono interleave.</span><span class="sxs-lookup"><span data-stu-id="00b49-118">When using hello **Content Adaptive Multiple Bitrate MP4** preset, hello MES encoder will apply hello same encoding logic as above, but now hello output asset will contain MP4 files where audio and video are interleaved.</span></span> <span data-ttu-id="00b49-119">È possibile utilizzare uno di questi file MP4 (ad esempio, hello versione più recente a velocità in bit) come un file di download progressivo.</span><span class="sxs-lookup"><span data-stu-id="00b49-119">You can use one of these MP4 files (for example, hello highest bitrate version) as a progressive download file.</span></span>

## <span data-ttu-id="00b49-120"><a id="encoding_with_dotnet"></a>Codifica con l’SDK .NET dei servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="00b49-120"><a id="encoding_with_dotnet"></a>Encoding with Media Services .NET SDK</span></span>

<span data-ttu-id="00b49-121">esempio di codice seguente Hello utilizza hello tooperform Media Services .NET SDK seguenti attività:</span><span class="sxs-lookup"><span data-stu-id="00b49-121">hello following code example uses Media Services .NET SDK tooperform hello following tasks:</span></span>

- <span data-ttu-id="00b49-122">Creare un processo di codifica.</span><span class="sxs-lookup"><span data-stu-id="00b49-122">Create an encoding job.</span></span>
- <span data-ttu-id="00b49-123">Ottiene un codificatore Media Encoder Standard toohello di riferimento.</span><span class="sxs-lookup"><span data-stu-id="00b49-123">Get a reference toohello Media Encoder Standard encoder.</span></span>
- <span data-ttu-id="00b49-124">Aggiungere un processo di codifica attività toohello e specificare hello toouse **il flusso adattivo** predefinito.</span><span class="sxs-lookup"><span data-stu-id="00b49-124">Add an encoding task toohello job and specify toouse hello **Adaptive Streaming** preset.</span></span> 
- <span data-ttu-id="00b49-125">Creare un asset di output che conterrà l'asset codificato hello.</span><span class="sxs-lookup"><span data-stu-id="00b49-125">Create an output asset that will contain hello encoded asset.</span></span>
- <span data-ttu-id="00b49-126">Aggiungere un avanzamento del processo hello toocheck gestore dell'evento.</span><span class="sxs-lookup"><span data-stu-id="00b49-126">Add an event handler toocheck hello job progress.</span></span>
- <span data-ttu-id="00b49-127">Inviare il processo di hello.</span><span class="sxs-lookup"><span data-stu-id="00b49-127">Submit hello job.</span></span>

#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="00b49-128">Creare e configurare un progetto di Visual Studio</span><span class="sxs-lookup"><span data-stu-id="00b49-128">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="00b49-129">Configurare l'ambiente di sviluppo e di popolare il file app. config hello con informazioni di connessione, come descritto in [lo sviluppo di servizi multimediali con .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="00b49-129">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="00b49-130">Esempio</span><span class="sxs-lookup"><span data-stu-id="00b49-130">Example</span></span>

    using System;
    using System.Configuration;
    using System.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Threading;

    namespace AdaptiveStreamingMESPresest
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
            task.OutputAssets.AddNew("Output asset",
            AssetCreationOptions.None);

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

## <span data-ttu-id="00b49-131"><a id="output"></a>Output</span><span class="sxs-lookup"><span data-stu-id="00b49-131"><a id="output"></a>Output</span></span>

<span data-ttu-id="00b49-132">Questa sezione vengono illustrate tre esempi di livelli di output prodotti da MES in seguito alla codifica con hello **il flusso adattivo** predefinito.</span><span class="sxs-lookup"><span data-stu-id="00b49-132">This section shows three examples of output layers produced by MES as a result of encoding with hello **Adaptive Streaming** preset.</span></span> 

### <a name="example-1"></a><span data-ttu-id="00b49-133">Esempio 1</span><span class="sxs-lookup"><span data-stu-id="00b49-133">Example 1</span></span>
<span data-ttu-id="00b49-134">L'origine con altezza "1080" e una frequenza frame "29.970" produce 6 livelli video:</span><span class="sxs-lookup"><span data-stu-id="00b49-134">Source with height "1080" and framerate "29.970" produces 6 video layers:</span></span>

|<span data-ttu-id="00b49-135">Livello</span><span class="sxs-lookup"><span data-stu-id="00b49-135">Layer</span></span>|<span data-ttu-id="00b49-136">Altezza:</span><span class="sxs-lookup"><span data-stu-id="00b49-136">Height</span></span>|<span data-ttu-id="00b49-137">Larghezza</span><span class="sxs-lookup"><span data-stu-id="00b49-137">Width</span></span>|<span data-ttu-id="00b49-138">Bitrate (Kbps)</span><span class="sxs-lookup"><span data-stu-id="00b49-138">Bitrate(kbps)</span></span>|
|---|---|---|---|
|<span data-ttu-id="00b49-139">1</span><span class="sxs-lookup"><span data-stu-id="00b49-139">1</span></span>|<span data-ttu-id="00b49-140">1080</span><span class="sxs-lookup"><span data-stu-id="00b49-140">1080</span></span>|<span data-ttu-id="00b49-141">1920</span><span class="sxs-lookup"><span data-stu-id="00b49-141">1920</span></span>|<span data-ttu-id="00b49-142">6780</span><span class="sxs-lookup"><span data-stu-id="00b49-142">6780</span></span>|
|<span data-ttu-id="00b49-143">2</span><span class="sxs-lookup"><span data-stu-id="00b49-143">2</span></span>|<span data-ttu-id="00b49-144">720</span><span class="sxs-lookup"><span data-stu-id="00b49-144">720</span></span>|<span data-ttu-id="00b49-145">1280</span><span class="sxs-lookup"><span data-stu-id="00b49-145">1280</span></span>|<span data-ttu-id="00b49-146">3520</span><span class="sxs-lookup"><span data-stu-id="00b49-146">3520</span></span>|
|<span data-ttu-id="00b49-147">3</span><span class="sxs-lookup"><span data-stu-id="00b49-147">3</span></span>|<span data-ttu-id="00b49-148">540</span><span class="sxs-lookup"><span data-stu-id="00b49-148">540</span></span>|<span data-ttu-id="00b49-149">960</span><span class="sxs-lookup"><span data-stu-id="00b49-149">960</span></span>|<span data-ttu-id="00b49-150">2210</span><span class="sxs-lookup"><span data-stu-id="00b49-150">2210</span></span>|
|<span data-ttu-id="00b49-151">4</span><span class="sxs-lookup"><span data-stu-id="00b49-151">4</span></span>|<span data-ttu-id="00b49-152">360</span><span class="sxs-lookup"><span data-stu-id="00b49-152">360</span></span>|<span data-ttu-id="00b49-153">640</span><span class="sxs-lookup"><span data-stu-id="00b49-153">640</span></span>|<span data-ttu-id="00b49-154">1150</span><span class="sxs-lookup"><span data-stu-id="00b49-154">1150</span></span>|
|<span data-ttu-id="00b49-155">5</span><span class="sxs-lookup"><span data-stu-id="00b49-155">5</span></span>|<span data-ttu-id="00b49-156">270</span><span class="sxs-lookup"><span data-stu-id="00b49-156">270</span></span>|<span data-ttu-id="00b49-157">480</span><span class="sxs-lookup"><span data-stu-id="00b49-157">480</span></span>|<span data-ttu-id="00b49-158">720</span><span class="sxs-lookup"><span data-stu-id="00b49-158">720</span></span>|
|<span data-ttu-id="00b49-159">6</span><span class="sxs-lookup"><span data-stu-id="00b49-159">6</span></span>|<span data-ttu-id="00b49-160">180</span><span class="sxs-lookup"><span data-stu-id="00b49-160">180</span></span>|<span data-ttu-id="00b49-161">320</span><span class="sxs-lookup"><span data-stu-id="00b49-161">320</span></span>|<span data-ttu-id="00b49-162">380</span><span class="sxs-lookup"><span data-stu-id="00b49-162">380</span></span>|

### <a name="example-2"></a><span data-ttu-id="00b49-163">Esempio 2</span><span class="sxs-lookup"><span data-stu-id="00b49-163">Example 2</span></span>
<span data-ttu-id="00b49-164">L'origine con altezza "720" e una frequenza frame "23.970" produce 5 livelli video:</span><span class="sxs-lookup"><span data-stu-id="00b49-164">Source with height "720" and framerate "23.970" produces 5 video layers:</span></span>

|<span data-ttu-id="00b49-165">Livello</span><span class="sxs-lookup"><span data-stu-id="00b49-165">Layer</span></span>|<span data-ttu-id="00b49-166">Altezza:</span><span class="sxs-lookup"><span data-stu-id="00b49-166">Height</span></span>|<span data-ttu-id="00b49-167">Larghezza</span><span class="sxs-lookup"><span data-stu-id="00b49-167">Width</span></span>|<span data-ttu-id="00b49-168">Bitrate (Kbps)</span><span class="sxs-lookup"><span data-stu-id="00b49-168">Bitrate(kbps)</span></span>|
|---|---|---|---|
|<span data-ttu-id="00b49-169">1</span><span class="sxs-lookup"><span data-stu-id="00b49-169">1</span></span>|<span data-ttu-id="00b49-170">720</span><span class="sxs-lookup"><span data-stu-id="00b49-170">720</span></span>|<span data-ttu-id="00b49-171">1280</span><span class="sxs-lookup"><span data-stu-id="00b49-171">1280</span></span>|<span data-ttu-id="00b49-172">2940</span><span class="sxs-lookup"><span data-stu-id="00b49-172">2940</span></span>|
|<span data-ttu-id="00b49-173">2</span><span class="sxs-lookup"><span data-stu-id="00b49-173">2</span></span>|<span data-ttu-id="00b49-174">540</span><span class="sxs-lookup"><span data-stu-id="00b49-174">540</span></span>|<span data-ttu-id="00b49-175">960</span><span class="sxs-lookup"><span data-stu-id="00b49-175">960</span></span>|<span data-ttu-id="00b49-176">1850</span><span class="sxs-lookup"><span data-stu-id="00b49-176">1850</span></span>|
|<span data-ttu-id="00b49-177">3</span><span class="sxs-lookup"><span data-stu-id="00b49-177">3</span></span>|<span data-ttu-id="00b49-178">360</span><span class="sxs-lookup"><span data-stu-id="00b49-178">360</span></span>|<span data-ttu-id="00b49-179">640</span><span class="sxs-lookup"><span data-stu-id="00b49-179">640</span></span>|<span data-ttu-id="00b49-180">960</span><span class="sxs-lookup"><span data-stu-id="00b49-180">960</span></span>|
|<span data-ttu-id="00b49-181">4</span><span class="sxs-lookup"><span data-stu-id="00b49-181">4</span></span>|<span data-ttu-id="00b49-182">270</span><span class="sxs-lookup"><span data-stu-id="00b49-182">270</span></span>|<span data-ttu-id="00b49-183">480</span><span class="sxs-lookup"><span data-stu-id="00b49-183">480</span></span>|<span data-ttu-id="00b49-184">600</span><span class="sxs-lookup"><span data-stu-id="00b49-184">600</span></span>|
|<span data-ttu-id="00b49-185">5</span><span class="sxs-lookup"><span data-stu-id="00b49-185">5</span></span>|<span data-ttu-id="00b49-186">180</span><span class="sxs-lookup"><span data-stu-id="00b49-186">180</span></span>|<span data-ttu-id="00b49-187">320</span><span class="sxs-lookup"><span data-stu-id="00b49-187">320</span></span>|<span data-ttu-id="00b49-188">320</span><span class="sxs-lookup"><span data-stu-id="00b49-188">320</span></span>|

### <a name="example-3"></a><span data-ttu-id="00b49-189">Esempio 3</span><span class="sxs-lookup"><span data-stu-id="00b49-189">Example 3</span></span>
<span data-ttu-id="00b49-190">L'origine con altezza "360" e una frequenza frame "29.970" produce 3 livelli video:</span><span class="sxs-lookup"><span data-stu-id="00b49-190">Source with height "360" and framerate "29.970" produces 3 video layers:</span></span>

|<span data-ttu-id="00b49-191">Livello</span><span class="sxs-lookup"><span data-stu-id="00b49-191">Layer</span></span>|<span data-ttu-id="00b49-192">Altezza:</span><span class="sxs-lookup"><span data-stu-id="00b49-192">Height</span></span>|<span data-ttu-id="00b49-193">Larghezza</span><span class="sxs-lookup"><span data-stu-id="00b49-193">Width</span></span>|<span data-ttu-id="00b49-194">Bitrate (Kbps)</span><span class="sxs-lookup"><span data-stu-id="00b49-194">Bitrate(kbps)</span></span>|
|---|---|---|---|
|<span data-ttu-id="00b49-195">1</span><span class="sxs-lookup"><span data-stu-id="00b49-195">1</span></span>|<span data-ttu-id="00b49-196">360</span><span class="sxs-lookup"><span data-stu-id="00b49-196">360</span></span>|<span data-ttu-id="00b49-197">640</span><span class="sxs-lookup"><span data-stu-id="00b49-197">640</span></span>|<span data-ttu-id="00b49-198">700</span><span class="sxs-lookup"><span data-stu-id="00b49-198">700</span></span>|
|<span data-ttu-id="00b49-199">2</span><span class="sxs-lookup"><span data-stu-id="00b49-199">2</span></span>|<span data-ttu-id="00b49-200">270</span><span class="sxs-lookup"><span data-stu-id="00b49-200">270</span></span>|<span data-ttu-id="00b49-201">480</span><span class="sxs-lookup"><span data-stu-id="00b49-201">480</span></span>|<span data-ttu-id="00b49-202">440</span><span class="sxs-lookup"><span data-stu-id="00b49-202">440</span></span>|
|<span data-ttu-id="00b49-203">3</span><span class="sxs-lookup"><span data-stu-id="00b49-203">3</span></span>|<span data-ttu-id="00b49-204">180</span><span class="sxs-lookup"><span data-stu-id="00b49-204">180</span></span>|<span data-ttu-id="00b49-205">320</span><span class="sxs-lookup"><span data-stu-id="00b49-205">320</span></span>|<span data-ttu-id="00b49-206">230</span><span class="sxs-lookup"><span data-stu-id="00b49-206">230</span></span>|
## <a name="media-services-learning-paths"></a><span data-ttu-id="00b49-207">Percorsi di apprendimento di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="00b49-207">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="00b49-208">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="00b49-208">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="00b49-209">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="00b49-209">See Also</span></span>
[<span data-ttu-id="00b49-210">Panoramica sulla codifica dei servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="00b49-210">Media Services Encoding Overview</span></span>](media-services-encode-asset.md)

