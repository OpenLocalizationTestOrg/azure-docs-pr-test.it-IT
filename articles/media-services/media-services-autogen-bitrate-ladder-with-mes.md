---
title: Usare Azure Media Encoder Standard per generare automaticamente un bitrate ladder | Microsoft Docs
description: "In questo argomento viene illustrato come usare Media Encoder Standard (MES) per generare automaticamente un bitrate ladder in base alla risoluzione di input e alla velocità in bit. La risoluzione di input e la velocità in bit non vengono mai superate. Ad esempio, se l'input è 720p a 3 Mbps, l'output resterà al massimo a 720p e inizierà a una velocità inferiore a 3 Mbps."
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
ms.openlocfilehash: b5616aa9f8b15ab576d914fbae89a56f64c27f4a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
#  <a name="use-azure-media-encoder-standard-to-auto-generate-a-bitrate-ladder"></a><span data-ttu-id="bd961-105">Usare Azure Media Encoder Standard per generare automaticamente un bitrate ladder</span><span class="sxs-lookup"><span data-stu-id="bd961-105">Use Azure Media Encoder Standard to auto-generate a bitrate ladder</span></span>

## <a name="overview"></a><span data-ttu-id="bd961-106">Panoramica</span><span class="sxs-lookup"><span data-stu-id="bd961-106">Overview</span></span>

<span data-ttu-id="bd961-107">In questo argomento viene illustrato come usare Media Encoder Standard (MES) per generare automaticamente un bitrate ladder (coppia risoluzione-velocità in bit) in base alla risoluzione di input e alla velocità in bit.</span><span class="sxs-lookup"><span data-stu-id="bd961-107">This topic shows how to use Media Encoder Standard (MES) to auto-generate a bitrate ladder (bitrate-resolution pairs) based on the input resolution and bitrate.</span></span> <span data-ttu-id="bd961-108">Il set di impostazioni generate automaticamente non supererà mai la risoluzione di input e la velocità in bit.</span><span class="sxs-lookup"><span data-stu-id="bd961-108">The auto-generated preset will never exceed the input resolution and bitrate.</span></span> <span data-ttu-id="bd961-109">Ad esempio, se l'input è 720p a 3 Mbps, l'output resterà al massimo a 720p e inizierà a una velocità inferiore a 3 Mbps.</span><span class="sxs-lookup"><span data-stu-id="bd961-109">For example, if the input is 720p at 3Mbps, output will remain 720p at best, and will start at rates lower than 3Mbps.</span></span>

### <a name="encoding-for-streaming-only"></a><span data-ttu-id="bd961-110">Codifica solo per lo streaming</span><span class="sxs-lookup"><span data-stu-id="bd961-110">Encoding for Streaming Only</span></span>

<span data-ttu-id="bd961-111">Se si intende codificare il video di origine solo per lo streaming, è necessario usare il set di impostazioni "Flusso adattivo" quando si crea un'attività di codifica.</span><span class="sxs-lookup"><span data-stu-id="bd961-111">If your intent is to encode your source video only for streaming, then you shoud use the "Adaptive Streaming" preset when creating an encoding task.</span></span> <span data-ttu-id="bd961-112">Quando si usa il set di impostazioni **Flusso adattivo** il codificatore MES userà in modo intelligente un bitrate ladder.</span><span class="sxs-lookup"><span data-stu-id="bd961-112">When using the **Adaptive Streaming** preset, the MES encoder will intelligently cap a bitrate ladder.</span></span> <span data-ttu-id="bd961-113">Tuttavia, non sarà possibile controllare i costi di codifica, poiché il servizio determina il numero di livelli da usare e la risoluzione.</span><span class="sxs-lookup"><span data-stu-id="bd961-113">However, you will not be able to control the encoding costs, since the service determines how many layers to use and at what resolution.</span></span> <span data-ttu-id="bd961-114">È possibile vedere esempi dei livelli di output prodotti da MES in seguito alla codifica con il set di impostazioni **Flusso adattivo** alla fine di questo argomento.</span><span class="sxs-lookup"><span data-stu-id="bd961-114">You can see examples of output layers produced by MES as a result of encoding with the **Adaptive Streaming** preset at the end of this topic.</span></span> <span data-ttu-id="bd961-115">L'asset di output conterrà i file MP4 in cui audio e video non sono di tipo Interleaved.</span><span class="sxs-lookup"><span data-stu-id="bd961-115">The output Asset will contain MP4 files where audio and video are not interleaved.</span></span>

### <a name="encoding-for-streaming-and-progressive-download"></a><span data-ttu-id="bd961-116">Codifica per streaming e download progressivo</span><span class="sxs-lookup"><span data-stu-id="bd961-116">Encoding for Streaming and Progressive Download</span></span>

<span data-ttu-id="bd961-117">Se si intende codificare un video di origine per lo streaming e per produrre file MP4 per il download progressivo, è necessario usare il set di impostazioni "Content Adaptive Multiple Bitrate MP4" durante la creazione di un'attività di codifica.</span><span class="sxs-lookup"><span data-stu-id="bd961-117">If your intent is to encode your source video for streaming as well as to produce MP4 files for progressive download, then you shoud use the "Content Adaptive Multiple Bitrate MP4" preset when creating an encoding task.</span></span> <span data-ttu-id="bd961-118">Quando si usa il set di impostazioni **Content Adaptive Multiple Bitrate MP4**, il codificatore MES applicherà la stessa logica di codifica illustrata in precedenza, ma ora l'asset di output conterrà file MP4 in cui audio e video sono di tipo Interleaved.</span><span class="sxs-lookup"><span data-stu-id="bd961-118">When using the **Content Adaptive Multiple Bitrate MP4** preset, the MES encoder will apply the same encoding logic as above, but now the output asset will contain MP4 files where audio and video are interleaved.</span></span> <span data-ttu-id="bd961-119">È possibile usare uno di questi file MP4 (ad esempio la versione con bitrate più elevato) come file di download progressivo.</span><span class="sxs-lookup"><span data-stu-id="bd961-119">You can use one of these MP4 files (for example, the highest bitrate version) as a progressive download file.</span></span>

## <span data-ttu-id="bd961-120"><a id="encoding_with_dotnet"></a>Codifica con l’SDK .NET dei servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="bd961-120"><a id="encoding_with_dotnet"></a>Encoding with Media Services .NET SDK</span></span>

<span data-ttu-id="bd961-121">Il seguente codice usa l'SDK .NET di Servizi multimediali per eseguire le seguenti attività: </span><span class="sxs-lookup"><span data-stu-id="bd961-121">The following code example uses Media Services .NET SDK to perform the following tasks:</span></span>

- <span data-ttu-id="bd961-122">Creare un processo di codifica.</span><span class="sxs-lookup"><span data-stu-id="bd961-122">Create an encoding job.</span></span>
- <span data-ttu-id="bd961-123">Ottenere un riferimento al codificatore Media Encoder Standard.</span><span class="sxs-lookup"><span data-stu-id="bd961-123">Get a reference to the Media Encoder Standard encoder.</span></span>
- <span data-ttu-id="bd961-124">Aggiungere un'attività di codifica al processo e specificare l'uso del set di impostazioni **Flusso adattivo**.</span><span class="sxs-lookup"><span data-stu-id="bd961-124">Add an encoding task to the job and specify to use the **Adaptive Streaming** preset.</span></span> 
- <span data-ttu-id="bd961-125">Creare un asset di output che conterrà l'asset codificato.</span><span class="sxs-lookup"><span data-stu-id="bd961-125">Create an output asset that will contain the encoded asset.</span></span>
- <span data-ttu-id="bd961-126">Aggiungere un gestore eventi per controllare l'avanzamento del processo.</span><span class="sxs-lookup"><span data-stu-id="bd961-126">Add an event handler to check the job progress.</span></span>
- <span data-ttu-id="bd961-127">Inviare il processo.</span><span class="sxs-lookup"><span data-stu-id="bd961-127">Submit the job.</span></span>

#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="bd961-128">Creare e configurare un progetto di Visual Studio</span><span class="sxs-lookup"><span data-stu-id="bd961-128">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="bd961-129">Configurare l'ambiente di sviluppo e popolare il file app.config con le informazioni di connessione, come descritto in [Sviluppo di applicazioni di Servizi multimediali con .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="bd961-129">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="bd961-130">Esempio</span><span class="sxs-lookup"><span data-stu-id="bd961-130">Example</span></span>

    using System;
    using System.Configuration;
    using System.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Threading;

    namespace AdaptiveStreamingMESPresest
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

            // Get an uploaded asset.
            var asset = _context.Assets.FirstOrDefault();

            // Encode and generate the output using the "Adaptive Streaming" preset.
            EncodeToAdaptiveBitrateMP4Set(asset);

            Console.ReadLine();
        }

        static public IAsset EncodeToAdaptiveBitrateMP4Set(IAsset asset)
        {
            // Declare a new job.
            IJob job = _context.Jobs.Create("Media Encoder Standard Job");

            // Get a media processor reference, and pass to it the name of the 
            // processor to use for the specific task.
            IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

            // Create a task
            ITask task = job.Tasks.AddNew("Media Encoder Standard encoding task",
            processor,
            "Adaptive Streaming",
            TaskOptions.None);

            // Specify the input asset to be encoded.
            task.InputAssets.Add(asset);
            // Add an output asset to contain the results of the job. 
            // This output is specified as AssetCreationOptions.None, which 
            // means the output asset is not encrypted. 
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

## <span data-ttu-id="bd961-131"><a id="output"></a>Output</span><span class="sxs-lookup"><span data-stu-id="bd961-131"><a id="output"></a>Output</span></span>

<span data-ttu-id="bd961-132">Questa sezione mostra tre esempi dei livelli di output prodotti da MES in seguito alla codifica con il set di impostazioni **Flusso adattivo**.</span><span class="sxs-lookup"><span data-stu-id="bd961-132">This section shows three examples of output layers produced by MES as a result of encoding with the **Adaptive Streaming** preset.</span></span> 

### <a name="example-1"></a><span data-ttu-id="bd961-133">Esempio 1</span><span class="sxs-lookup"><span data-stu-id="bd961-133">Example 1</span></span>
<span data-ttu-id="bd961-134">L'origine con altezza "1080" e una frequenza frame "29.970" produce 6 livelli video:</span><span class="sxs-lookup"><span data-stu-id="bd961-134">Source with height "1080" and framerate "29.970" produces 6 video layers:</span></span>

|<span data-ttu-id="bd961-135">Livello</span><span class="sxs-lookup"><span data-stu-id="bd961-135">Layer</span></span>|<span data-ttu-id="bd961-136">Altezza:</span><span class="sxs-lookup"><span data-stu-id="bd961-136">Height</span></span>|<span data-ttu-id="bd961-137">Larghezza</span><span class="sxs-lookup"><span data-stu-id="bd961-137">Width</span></span>|<span data-ttu-id="bd961-138">Bitrate (Kbps)</span><span class="sxs-lookup"><span data-stu-id="bd961-138">Bitrate(kbps)</span></span>|
|---|---|---|---|
|<span data-ttu-id="bd961-139">1</span><span class="sxs-lookup"><span data-stu-id="bd961-139">1</span></span>|<span data-ttu-id="bd961-140">1080</span><span class="sxs-lookup"><span data-stu-id="bd961-140">1080</span></span>|<span data-ttu-id="bd961-141">1920</span><span class="sxs-lookup"><span data-stu-id="bd961-141">1920</span></span>|<span data-ttu-id="bd961-142">6780</span><span class="sxs-lookup"><span data-stu-id="bd961-142">6780</span></span>|
|<span data-ttu-id="bd961-143">2</span><span class="sxs-lookup"><span data-stu-id="bd961-143">2</span></span>|<span data-ttu-id="bd961-144">720</span><span class="sxs-lookup"><span data-stu-id="bd961-144">720</span></span>|<span data-ttu-id="bd961-145">1280</span><span class="sxs-lookup"><span data-stu-id="bd961-145">1280</span></span>|<span data-ttu-id="bd961-146">3520</span><span class="sxs-lookup"><span data-stu-id="bd961-146">3520</span></span>|
|<span data-ttu-id="bd961-147">3</span><span class="sxs-lookup"><span data-stu-id="bd961-147">3</span></span>|<span data-ttu-id="bd961-148">540</span><span class="sxs-lookup"><span data-stu-id="bd961-148">540</span></span>|<span data-ttu-id="bd961-149">960</span><span class="sxs-lookup"><span data-stu-id="bd961-149">960</span></span>|<span data-ttu-id="bd961-150">2210</span><span class="sxs-lookup"><span data-stu-id="bd961-150">2210</span></span>|
|<span data-ttu-id="bd961-151">4</span><span class="sxs-lookup"><span data-stu-id="bd961-151">4</span></span>|<span data-ttu-id="bd961-152">360</span><span class="sxs-lookup"><span data-stu-id="bd961-152">360</span></span>|<span data-ttu-id="bd961-153">640</span><span class="sxs-lookup"><span data-stu-id="bd961-153">640</span></span>|<span data-ttu-id="bd961-154">1150</span><span class="sxs-lookup"><span data-stu-id="bd961-154">1150</span></span>|
|<span data-ttu-id="bd961-155">5</span><span class="sxs-lookup"><span data-stu-id="bd961-155">5</span></span>|<span data-ttu-id="bd961-156">270</span><span class="sxs-lookup"><span data-stu-id="bd961-156">270</span></span>|<span data-ttu-id="bd961-157">480</span><span class="sxs-lookup"><span data-stu-id="bd961-157">480</span></span>|<span data-ttu-id="bd961-158">720</span><span class="sxs-lookup"><span data-stu-id="bd961-158">720</span></span>|
|<span data-ttu-id="bd961-159">6</span><span class="sxs-lookup"><span data-stu-id="bd961-159">6</span></span>|<span data-ttu-id="bd961-160">180</span><span class="sxs-lookup"><span data-stu-id="bd961-160">180</span></span>|<span data-ttu-id="bd961-161">320</span><span class="sxs-lookup"><span data-stu-id="bd961-161">320</span></span>|<span data-ttu-id="bd961-162">380</span><span class="sxs-lookup"><span data-stu-id="bd961-162">380</span></span>|

### <a name="example-2"></a><span data-ttu-id="bd961-163">Esempio 2</span><span class="sxs-lookup"><span data-stu-id="bd961-163">Example 2</span></span>
<span data-ttu-id="bd961-164">L'origine con altezza "720" e una frequenza frame "23.970" produce 5 livelli video:</span><span class="sxs-lookup"><span data-stu-id="bd961-164">Source with height "720" and framerate "23.970" produces 5 video layers:</span></span>

|<span data-ttu-id="bd961-165">Livello</span><span class="sxs-lookup"><span data-stu-id="bd961-165">Layer</span></span>|<span data-ttu-id="bd961-166">Altezza:</span><span class="sxs-lookup"><span data-stu-id="bd961-166">Height</span></span>|<span data-ttu-id="bd961-167">Larghezza</span><span class="sxs-lookup"><span data-stu-id="bd961-167">Width</span></span>|<span data-ttu-id="bd961-168">Bitrate (Kbps)</span><span class="sxs-lookup"><span data-stu-id="bd961-168">Bitrate(kbps)</span></span>|
|---|---|---|---|
|<span data-ttu-id="bd961-169">1</span><span class="sxs-lookup"><span data-stu-id="bd961-169">1</span></span>|<span data-ttu-id="bd961-170">720</span><span class="sxs-lookup"><span data-stu-id="bd961-170">720</span></span>|<span data-ttu-id="bd961-171">1280</span><span class="sxs-lookup"><span data-stu-id="bd961-171">1280</span></span>|<span data-ttu-id="bd961-172">2940</span><span class="sxs-lookup"><span data-stu-id="bd961-172">2940</span></span>|
|<span data-ttu-id="bd961-173">2</span><span class="sxs-lookup"><span data-stu-id="bd961-173">2</span></span>|<span data-ttu-id="bd961-174">540</span><span class="sxs-lookup"><span data-stu-id="bd961-174">540</span></span>|<span data-ttu-id="bd961-175">960</span><span class="sxs-lookup"><span data-stu-id="bd961-175">960</span></span>|<span data-ttu-id="bd961-176">1850</span><span class="sxs-lookup"><span data-stu-id="bd961-176">1850</span></span>|
|<span data-ttu-id="bd961-177">3</span><span class="sxs-lookup"><span data-stu-id="bd961-177">3</span></span>|<span data-ttu-id="bd961-178">360</span><span class="sxs-lookup"><span data-stu-id="bd961-178">360</span></span>|<span data-ttu-id="bd961-179">640</span><span class="sxs-lookup"><span data-stu-id="bd961-179">640</span></span>|<span data-ttu-id="bd961-180">960</span><span class="sxs-lookup"><span data-stu-id="bd961-180">960</span></span>|
|<span data-ttu-id="bd961-181">4</span><span class="sxs-lookup"><span data-stu-id="bd961-181">4</span></span>|<span data-ttu-id="bd961-182">270</span><span class="sxs-lookup"><span data-stu-id="bd961-182">270</span></span>|<span data-ttu-id="bd961-183">480</span><span class="sxs-lookup"><span data-stu-id="bd961-183">480</span></span>|<span data-ttu-id="bd961-184">600</span><span class="sxs-lookup"><span data-stu-id="bd961-184">600</span></span>|
|<span data-ttu-id="bd961-185">5</span><span class="sxs-lookup"><span data-stu-id="bd961-185">5</span></span>|<span data-ttu-id="bd961-186">180</span><span class="sxs-lookup"><span data-stu-id="bd961-186">180</span></span>|<span data-ttu-id="bd961-187">320</span><span class="sxs-lookup"><span data-stu-id="bd961-187">320</span></span>|<span data-ttu-id="bd961-188">320</span><span class="sxs-lookup"><span data-stu-id="bd961-188">320</span></span>|

### <a name="example-3"></a><span data-ttu-id="bd961-189">Esempio 3</span><span class="sxs-lookup"><span data-stu-id="bd961-189">Example 3</span></span>
<span data-ttu-id="bd961-190">L'origine con altezza "360" e una frequenza frame "29.970" produce 3 livelli video:</span><span class="sxs-lookup"><span data-stu-id="bd961-190">Source with height "360" and framerate "29.970" produces 3 video layers:</span></span>

|<span data-ttu-id="bd961-191">Livello</span><span class="sxs-lookup"><span data-stu-id="bd961-191">Layer</span></span>|<span data-ttu-id="bd961-192">Altezza:</span><span class="sxs-lookup"><span data-stu-id="bd961-192">Height</span></span>|<span data-ttu-id="bd961-193">Larghezza</span><span class="sxs-lookup"><span data-stu-id="bd961-193">Width</span></span>|<span data-ttu-id="bd961-194">Bitrate (Kbps)</span><span class="sxs-lookup"><span data-stu-id="bd961-194">Bitrate(kbps)</span></span>|
|---|---|---|---|
|<span data-ttu-id="bd961-195">1</span><span class="sxs-lookup"><span data-stu-id="bd961-195">1</span></span>|<span data-ttu-id="bd961-196">360</span><span class="sxs-lookup"><span data-stu-id="bd961-196">360</span></span>|<span data-ttu-id="bd961-197">640</span><span class="sxs-lookup"><span data-stu-id="bd961-197">640</span></span>|<span data-ttu-id="bd961-198">700</span><span class="sxs-lookup"><span data-stu-id="bd961-198">700</span></span>|
|<span data-ttu-id="bd961-199">2</span><span class="sxs-lookup"><span data-stu-id="bd961-199">2</span></span>|<span data-ttu-id="bd961-200">270</span><span class="sxs-lookup"><span data-stu-id="bd961-200">270</span></span>|<span data-ttu-id="bd961-201">480</span><span class="sxs-lookup"><span data-stu-id="bd961-201">480</span></span>|<span data-ttu-id="bd961-202">440</span><span class="sxs-lookup"><span data-stu-id="bd961-202">440</span></span>|
|<span data-ttu-id="bd961-203">3</span><span class="sxs-lookup"><span data-stu-id="bd961-203">3</span></span>|<span data-ttu-id="bd961-204">180</span><span class="sxs-lookup"><span data-stu-id="bd961-204">180</span></span>|<span data-ttu-id="bd961-205">320</span><span class="sxs-lookup"><span data-stu-id="bd961-205">320</span></span>|<span data-ttu-id="bd961-206">230</span><span class="sxs-lookup"><span data-stu-id="bd961-206">230</span></span>|
## <a name="media-services-learning-paths"></a><span data-ttu-id="bd961-207">Percorsi di apprendimento di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="bd961-207">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="bd961-208">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="bd961-208">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="bd961-209">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="bd961-209">See Also</span></span>
[<span data-ttu-id="bd961-210">Panoramica sulla codifica dei servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="bd961-210">Media Services Encoding Overview</span></span>](media-services-encode-asset.md)

