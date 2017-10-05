---
title: Codificare un asset con Media Encoder Standard mediante .NET | Microsoft Docs
description: Questo argomento illustra come usare .NET per codificare un asset con Media Encoder Standard.
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 03431b64-5518-478a-a1c2-1de345999274
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: juliako;anilmur
ms.openlocfilehash: 929592368501c54277748bf46b2160c9058db3fb
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="encode-an-asset-with-media-encoder-standard-using-net"></a><span data-ttu-id="0316d-103">Codificare un asset con Media Encoder Standard mediante .NET</span><span class="sxs-lookup"><span data-stu-id="0316d-103">Encode an asset with Media Encoder Standard using .NET</span></span>
<span data-ttu-id="0316d-104">I processi di codifica sono tra le operazioni di elaborazione più frequenti in Servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="0316d-104">Encoding jobs are one of the most common processing operations in Media Services.</span></span> <span data-ttu-id="0316d-105">Questi processi vengono creati per convertire i file multimediali da una codifica all'altra.</span><span class="sxs-lookup"><span data-stu-id="0316d-105">You create encoding jobs to convert media files from one encoding to another.</span></span> <span data-ttu-id="0316d-106">Durante la codifica è possibile usare il codificatore multimediale incorporato in Servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="0316d-106">When you encode, you can use the Media Services built-in Media Encoder.</span></span> <span data-ttu-id="0316d-107">È inoltre possibile usare un codificatore fornito da un partner di Servizi multimediali. I codificatori di terze parti sono disponibili tramite Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="0316d-107">You can also use an encoder provided by a Media Services partner; third party encoders are available through the Azure Marketplace.</span></span> 

<span data-ttu-id="0316d-108">Questo argomento illustra come usare .NET per codificare gli asset con Media Encoder Standard (MES).</span><span class="sxs-lookup"><span data-stu-id="0316d-108">This topic shows how to use .NET to encode your assets with Media Encoder Standard (MES).</span></span> <span data-ttu-id="0316d-109">Media Encoder Standard viene configurato mediante un set di impostazioni descritto [qui](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="0316d-109">Media Encoder Standard is configured using one of the encoder presets described [here](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409).</span></span>

<span data-ttu-id="0316d-110">È consigliabile codificare sempre i file di origine con un set MP4 a velocità in bit adattiva e quindi convertire il set nel formato desiderato mediante la [creazione dinamica dei pacchetti](media-services-dynamic-packaging-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0316d-110">It is recommended to always encode your source files into an adaptive bitrate MP4 set and then convert the set to the desired format using the [Dynamic Packaging](media-services-dynamic-packaging-overview.md).</span></span> 

<span data-ttu-id="0316d-111">Se l'asset di output è protetto con crittografia di archiviazione, è necessario configurare i criteri di distribuzione degli asset.</span><span class="sxs-lookup"><span data-stu-id="0316d-111">If your output asset is storage encrypted, you must configure asset delivery policy.</span></span> <span data-ttu-id="0316d-112">Per altre informazioni, vedere [Procedura: Configurare i criteri di distribuzione degli asset](media-services-dotnet-configure-asset-delivery-policy.md).</span><span class="sxs-lookup"><span data-stu-id="0316d-112">For more information see [Configuring asset delivery policy](media-services-dotnet-configure-asset-delivery-policy.md).</span></span>

> [!NOTE]
> <span data-ttu-id="0316d-113">MES produce un file di output con un nome contenente i primi 32 caratteri del nome del file di input.</span><span class="sxs-lookup"><span data-stu-id="0316d-113">MES produces an output file with a name that contains the first 32 characters of the input file name.</span></span> <span data-ttu-id="0316d-114">Il nome è basato su quanto specificato nel file preimpostato.</span><span class="sxs-lookup"><span data-stu-id="0316d-114">The name is based on what is specified in the preset file.</span></span> <span data-ttu-id="0316d-115">Ad esempio, "FileName": "{Basename}_{Index}{Extension}".</span><span class="sxs-lookup"><span data-stu-id="0316d-115">For example, "FileName": "{Basename}_{Index}{Extension}".</span></span> <span data-ttu-id="0316d-116">{Basename} viene sostituito dai primi 32 caratteri del nome del file di input.</span><span class="sxs-lookup"><span data-stu-id="0316d-116">{Basename} is replaced by the first 32 characters of the input file name.</span></span>
> 
> 

### <a name="mes-formats"></a><span data-ttu-id="0316d-117">Formati MES</span><span class="sxs-lookup"><span data-stu-id="0316d-117">MES Formats</span></span>
[<span data-ttu-id="0316d-118">Codec e formati</span><span class="sxs-lookup"><span data-stu-id="0316d-118">Formats and codecs</span></span>](media-services-media-encoder-standard-formats.md)

### <a name="mes-presets"></a><span data-ttu-id="0316d-119">Impostazioni predefinite MES</span><span class="sxs-lookup"><span data-stu-id="0316d-119">MES Presets</span></span>
<span data-ttu-id="0316d-120">Media Encoder Standard viene configurato mediante un set di impostazioni descritto [qui](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="0316d-120">Media Encoder Standard is configured using one of the encoder presets described [here](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409).</span></span>

### <a name="input-and-output-metadata"></a><span data-ttu-id="0316d-121">Metadati di input e output</span><span class="sxs-lookup"><span data-stu-id="0316d-121">Input and output metadata</span></span>
<span data-ttu-id="0316d-122">Quando si codifica un asset di input (o asset) tramite MES, al completamento dell'attività di codifica si ottiene un asset di output.</span><span class="sxs-lookup"><span data-stu-id="0316d-122">When you encode an input asset (or assets) using MES, you get an output asset at the successful completion of that encode task.</span></span> <span data-ttu-id="0316d-123">L'asset di output contiene video, audio, anteprime, manifesto e così via a seconda del set di impostazioni di codifica che si usa.</span><span class="sxs-lookup"><span data-stu-id="0316d-123">The output asset contains video, audio, thumbnails, manifest, etc. based on the encoding preset you use.</span></span>

<span data-ttu-id="0316d-124">L'asset di output include anche un file contenente i metadati dell'asset di input.</span><span class="sxs-lookup"><span data-stu-id="0316d-124">The output asset also contains a file with metadata about the input asset.</span></span> <span data-ttu-id="0316d-125">Il nome del file XML dei metadati ha il seguente formato: <asset_id>_metadata.xml (ad esempio, 41114ad3-eb5e-4c57-8d92-5354e2b7d4a4_metadata.xml), dove <asset_id> è il valore AssetId dell'asset di input.</span><span class="sxs-lookup"><span data-stu-id="0316d-125">The name of the metadata XML file has the following format: <asset_id>_metadata.xml (for example, 41114ad3-eb5e-4c57-8d92-5354e2b7d4a4_metadata.xml), where <asset_id> is the AssetId value of the input asset.</span></span> <span data-ttu-id="0316d-126">Lo schema di questo file XML di metadati di input è descritto [qui](media-services-input-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="0316d-126">The schema of this input metadata XML is described [here](media-services-input-metadata-schema.md).</span></span>

<span data-ttu-id="0316d-127">L'asset di output include anche un file contenente i metadati dell'asset di output.</span><span class="sxs-lookup"><span data-stu-id="0316d-127">The output asset also contains a file with metadata about the output asset.</span></span> <span data-ttu-id="0316d-128">Il nome del file XML dei metadati ha il seguente formato: <nome_file_origine>_manifest.xml (ad esempio BigBuckBunny_manifest.xml).</span><span class="sxs-lookup"><span data-stu-id="0316d-128">The name of the metadata XML file has the following format: <source_file_name>_manifest.xml (for example, BigBuckBunny_manifest.xml).</span></span> <span data-ttu-id="0316d-129">Lo schema del file XML dei metadati di output viene descritto [qui](media-services-output-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="0316d-129">The schema of this output metadata XML is described [here](media-services-output-metadata-schema.md).</span></span>

<span data-ttu-id="0316d-130">Se si desidera esaminare uno dei due file di metadati, è possibile creare un localizzatore SAS e scaricare il file nel computer locale.</span><span class="sxs-lookup"><span data-stu-id="0316d-130">If you want to examine either of the two metadata files, you can create a SAS locator and download the file to your local computer.</span></span> <span data-ttu-id="0316d-131">È possibile trovare un esempio su come creare un localizzatore SAS e scaricare un file tramite le estensioni dell'SDK .NET di Servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="0316d-131">You can find an example on how to create a SAS locator and download a file Using the Media Services .NET SDK Extensions.</span></span>

## <a name="download-sample"></a><span data-ttu-id="0316d-132">Scaricare un esempio</span><span class="sxs-lookup"><span data-stu-id="0316d-132">Download sample</span></span>
<span data-ttu-id="0316d-133">È possibile ottenere ed eseguire da [qui](https://azure.microsoft.com/documentation/samples/media-services-dotnet-on-demand-encoding-with-media-encoder-standard/) un esempio che mostra come codificare con MES.</span><span class="sxs-lookup"><span data-stu-id="0316d-133">You can get and run a sample that shows how to encode with MES from [here](https://azure.microsoft.com/documentation/samples/media-services-dotnet-on-demand-encoding-with-media-encoder-standard/).</span></span>

## <a name="net-sample-code"></a><span data-ttu-id="0316d-134">Codice di esempio .NET</span><span class="sxs-lookup"><span data-stu-id="0316d-134">.NET sample code</span></span>

<span data-ttu-id="0316d-135">Il seguente codice usa l'SDK .NET di Servizi multimediali per eseguire le seguenti attività: </span><span class="sxs-lookup"><span data-stu-id="0316d-135">The following code example uses Media Services .NET SDK to perform the following tasks:</span></span>

* <span data-ttu-id="0316d-136">Creare un processo di codifica.</span><span class="sxs-lookup"><span data-stu-id="0316d-136">Create an encoding job.</span></span>
* <span data-ttu-id="0316d-137">Ottenere un riferimento al codificatore Media Encoder Standard.</span><span class="sxs-lookup"><span data-stu-id="0316d-137">Get a reference to the Media Encoder Standard encoder.</span></span>
* <span data-ttu-id="0316d-138">Specificare l'uso del set di impostazioni [Flusso adattivo](media-services-autogen-bitrate-ladder-with-mes.md).</span><span class="sxs-lookup"><span data-stu-id="0316d-138">Specify to use the [Adaptive Streaming](media-services-autogen-bitrate-ladder-with-mes.md) preset.</span></span> 
* <span data-ttu-id="0316d-139">Aggiungere una singola attività di codifica al processo.</span><span class="sxs-lookup"><span data-stu-id="0316d-139">Add a single encoding task to the job.</span></span> 
* <span data-ttu-id="0316d-140">Specificare l’asset di input da codificare.</span><span class="sxs-lookup"><span data-stu-id="0316d-140">Specify the input asset to be encoded.</span></span>
* <span data-ttu-id="0316d-141">Creare un asset di output che conterrà l'asset codificato.</span><span class="sxs-lookup"><span data-stu-id="0316d-141">Create an output asset that will contain the encoded asset.</span></span>
* <span data-ttu-id="0316d-142">Aggiungere un gestore eventi per controllare l'avanzamento del processo.</span><span class="sxs-lookup"><span data-stu-id="0316d-142">Add an event handler to check the job progress.</span></span>
* <span data-ttu-id="0316d-143">Inviare il processo.</span><span class="sxs-lookup"><span data-stu-id="0316d-143">Submit the job.</span></span>

#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="0316d-144">Creare e configurare un progetto di Visual Studio</span><span class="sxs-lookup"><span data-stu-id="0316d-144">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="0316d-145">Configurare l'ambiente di sviluppo e popolare il file app.config con le informazioni di connessione, come descritto in [Sviluppo di applicazioni di Servizi multimediali con .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="0316d-145">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="0316d-146">Esempio</span><span class="sxs-lookup"><span data-stu-id="0316d-146">Example</span></span> 

        using System;
        using System.Linq;
        using System.Configuration;
        using System.IO;
        using System.Threading;
        using Microsoft.WindowsAzure.MediaServices.Client;

        namespace MediaEncoderStandardSample
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

                    // Create a task with the encoding details, using a string preset.
                    // In this case "Adaptive Streaming" preset is used.
                    ITask task = job.Tasks.AddNew("My encoding task",
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

## <a name="media-services-learning-paths"></a><span data-ttu-id="0316d-147">Percorsi di apprendimento di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="0316d-147">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="0316d-148">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="0316d-148">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a><span data-ttu-id="0316d-149">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0316d-149">Next steps</span></span>
<span data-ttu-id="0316d-150">[Come generare l'anteprima mediante Media Encoder Standard con .NET](media-services-dotnet-generate-thumbnail-with-mes.md)
[Panoramica della codifica dei servizi multimediali](media-services-encode-asset.md)</span><span class="sxs-lookup"><span data-stu-id="0316d-150">[How to generate thumbnail using Media Encoder Standard with .NET](media-services-dotnet-generate-thumbnail-with-mes.md)
[Media Services Encoding Overview](media-services-encode-asset.md)</span></span>

