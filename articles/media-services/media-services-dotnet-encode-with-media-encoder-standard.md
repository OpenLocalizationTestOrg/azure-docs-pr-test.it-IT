---
title: un asset con Media Encoder Standard usando .NET aaaEncode | Documenti Microsoft
description: Questo argomento viene illustrato come toouse .NET tooencode un asset con Media Encoder standard.
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
ms.openlocfilehash: 25e274c3b67168f4afc8b8ab04af2d654c9dd6e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="encode-an-asset-with-media-encoder-standard-using-net"></a><span data-ttu-id="325cf-103">Codificare un asset con Media Encoder Standard mediante .NET</span><span class="sxs-lookup"><span data-stu-id="325cf-103">Encode an asset with Media Encoder Standard using .NET</span></span>
<span data-ttu-id="325cf-104">I processi di codifica sono una delle operazioni di elaborazione più comune di hello in servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="325cf-104">Encoding jobs are one of hello most common processing operations in Media Services.</span></span> <span data-ttu-id="325cf-105">Viene creato codifica file multimediali tooconvert di processi da un tooanother codifica.</span><span class="sxs-lookup"><span data-stu-id="325cf-105">You create encoding jobs tooconvert media files from one encoding tooanother.</span></span> <span data-ttu-id="325cf-106">Quando si codifica, è possibile utilizzare il codificatore multimediale incorporato di servizi multimediali hello.</span><span class="sxs-lookup"><span data-stu-id="325cf-106">When you encode, you can use hello Media Services built-in Media Encoder.</span></span> <span data-ttu-id="325cf-107">È inoltre possibile utilizzare un codificatore fornito da un partner di servizi multimediali. i codificatori di terze parti sono disponibili tramite hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="325cf-107">You can also use an encoder provided by a Media Services partner; third party encoders are available through hello Azure Marketplace.</span></span> 

<span data-ttu-id="325cf-108">Questo argomento viene illustrato come toouse .NET tooencode gli asset con Media codificatore Standard (MES).</span><span class="sxs-lookup"><span data-stu-id="325cf-108">This topic shows how toouse .NET tooencode your assets with Media Encoder Standard (MES).</span></span> <span data-ttu-id="325cf-109">Media Encoder Standard viene configurato usando uno dei set di impostazioni di codificatore hello descritto [qui](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="325cf-109">Media Encoder Standard is configured using one of hello encoder presets described [here](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409).</span></span>

<span data-ttu-id="325cf-110">È consigliabile tooalways codificare i file di origine in un set MP4 a velocità in bit adattiva, quindi convertire hello set toohello formato desiderato utilizzando hello [creazione dinamica dei pacchetti](media-services-dynamic-packaging-overview.md).</span><span class="sxs-lookup"><span data-stu-id="325cf-110">It is recommended tooalways encode your source files into an adaptive bitrate MP4 set and then convert hello set toohello desired format using hello [Dynamic Packaging](media-services-dynamic-packaging-overview.md).</span></span> 

<span data-ttu-id="325cf-111">Se l'asset di output è protetto con crittografia di archiviazione, è necessario configurare i criteri di distribuzione degli asset.</span><span class="sxs-lookup"><span data-stu-id="325cf-111">If your output asset is storage encrypted, you must configure asset delivery policy.</span></span> <span data-ttu-id="325cf-112">Per altre informazioni, vedere [Procedura: Configurare i criteri di distribuzione degli asset](media-services-dotnet-configure-asset-delivery-policy.md).</span><span class="sxs-lookup"><span data-stu-id="325cf-112">For more information see [Configuring asset delivery policy](media-services-dotnet-configure-asset-delivery-policy.md).</span></span>

> [!NOTE]
> <span data-ttu-id="325cf-113">Produce MES un file di output con un nome contenente hello primi 32 caratteri del hello Nome file di input.</span><span class="sxs-lookup"><span data-stu-id="325cf-113">MES produces an output file with a name that contains hello first 32 characters of hello input file name.</span></span> <span data-ttu-id="325cf-114">nome di Hello è basato su quello specificato nel file preimpostato hello.</span><span class="sxs-lookup"><span data-stu-id="325cf-114">hello name is based on what is specified in hello preset file.</span></span> <span data-ttu-id="325cf-115">Ad esempio, "FileName": "{Basename}_{Index}{Extension}".</span><span class="sxs-lookup"><span data-stu-id="325cf-115">For example, "FileName": "{Basename}_{Index}{Extension}".</span></span> <span data-ttu-id="325cf-116">{Nome} viene sostituito da hello primi 32 caratteri del nome di file di input hello.</span><span class="sxs-lookup"><span data-stu-id="325cf-116">{Basename} is replaced by hello first 32 characters of hello input file name.</span></span>
> 
> 

### <a name="mes-formats"></a><span data-ttu-id="325cf-117">Formati MES</span><span class="sxs-lookup"><span data-stu-id="325cf-117">MES Formats</span></span>
[<span data-ttu-id="325cf-118">Codec e formati</span><span class="sxs-lookup"><span data-stu-id="325cf-118">Formats and codecs</span></span>](media-services-media-encoder-standard-formats.md)

### <a name="mes-presets"></a><span data-ttu-id="325cf-119">Impostazioni predefinite MES</span><span class="sxs-lookup"><span data-stu-id="325cf-119">MES Presets</span></span>
<span data-ttu-id="325cf-120">Media Encoder Standard viene configurato usando uno dei set di impostazioni di codificatore hello descritto [qui](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="325cf-120">Media Encoder Standard is configured using one of hello encoder presets described [here](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409).</span></span>

### <a name="input-and-output-metadata"></a><span data-ttu-id="325cf-121">Metadati di input e output</span><span class="sxs-lookup"><span data-stu-id="325cf-121">Input and output metadata</span></span>
<span data-ttu-id="325cf-122">Quando si codifica un asset di input o asset mediante MES, si ottiene un asset di output in hello corretto completamento di tale codifica attività.</span><span class="sxs-lookup"><span data-stu-id="325cf-122">When you encode an input asset (or assets) using MES, you get an output asset at hello successful completion of that encode task.</span></span> <span data-ttu-id="325cf-123">Hello output contenente video, audio, anteprime, manifesto, e così via in base a hello set di impostazioni codifica che è utilizzare.</span><span class="sxs-lookup"><span data-stu-id="325cf-123">hello output asset contains video, audio, thumbnails, manifest, etc. based on hello encoding preset you use.</span></span>

<span data-ttu-id="325cf-124">asset di output di Hello contiene anche un file con i metadati sull'asset di input hello.</span><span class="sxs-lookup"><span data-stu-id="325cf-124">hello output asset also contains a file with metadata about hello input asset.</span></span> <span data-ttu-id="325cf-125">nome del file XML dei metadati di hello Hello ha hello seguente formato: < asset_id > <id_asset>_metadata.XML (ad esempio, d 57-8 41114ad3-eb5e - 4c 92-5354e2b7d4a4_metadata.xml), dove < asset_id > è il valore di AssetId hello dell'asset di input hello.</span><span class="sxs-lookup"><span data-stu-id="325cf-125">hello name of hello metadata XML file has hello following format: <asset_id>_metadata.xml (for example, 41114ad3-eb5e-4c57-8d92-5354e2b7d4a4_metadata.xml), where <asset_id> is hello AssetId value of hello input asset.</span></span> <span data-ttu-id="325cf-126">Hello schema dei metadati input XML è descritta [qui](media-services-input-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="325cf-126">hello schema of this input metadata XML is described [here](media-services-input-metadata-schema.md).</span></span>

<span data-ttu-id="325cf-127">asset di output di Hello contiene anche un file con i metadati sull'asset di output di hello.</span><span class="sxs-lookup"><span data-stu-id="325cf-127">hello output asset also contains a file with metadata about hello output asset.</span></span> <span data-ttu-id="325cf-128">nome del file XML dei metadati di hello Hello ha hello seguente formato: < deve > <nome_file_origine>_manifest.XML (ad esempio, BigBuckBunny_manifest.xml).</span><span class="sxs-lookup"><span data-stu-id="325cf-128">hello name of hello metadata XML file has hello following format: <source_file_name>_manifest.xml (for example, BigBuckBunny_manifest.xml).</span></span> <span data-ttu-id="325cf-129">schema di Hello questi metadati di output XML è descritta [qui](media-services-output-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="325cf-129">hello schema of this output metadata XML is described [here](media-services-output-metadata-schema.md).</span></span>

<span data-ttu-id="325cf-130">Se si desidera tooexamine hello due file di metadati, è possibile creare un localizzatore SAS e scaricare computer locale tooyour di file hello.</span><span class="sxs-lookup"><span data-stu-id="325cf-130">If you want tooexamine either of hello two metadata files, you can create a SAS locator and download hello file tooyour local computer.</span></span> <span data-ttu-id="325cf-131">È possibile trovare un esempio di come toocreate un localizzatore SAS e scaricare un file tramite hello di servizi multimediali .NET SDK Extensions.</span><span class="sxs-lookup"><span data-stu-id="325cf-131">You can find an example on how toocreate a SAS locator and download a file Using hello Media Services .NET SDK Extensions.</span></span>

## <a name="download-sample"></a><span data-ttu-id="325cf-132">Scaricare un esempio</span><span class="sxs-lookup"><span data-stu-id="325cf-132">Download sample</span></span>
<span data-ttu-id="325cf-133">È possibile ottenere ed eseguire un esempio che illustra come tooencode con MES da [qui](https://azure.microsoft.com/documentation/samples/media-services-dotnet-on-demand-encoding-with-media-encoder-standard/).</span><span class="sxs-lookup"><span data-stu-id="325cf-133">You can get and run a sample that shows how tooencode with MES from [here](https://azure.microsoft.com/documentation/samples/media-services-dotnet-on-demand-encoding-with-media-encoder-standard/).</span></span>

## <a name="net-sample-code"></a><span data-ttu-id="325cf-134">Codice di esempio .NET</span><span class="sxs-lookup"><span data-stu-id="325cf-134">.NET sample code</span></span>

<span data-ttu-id="325cf-135">esempio di codice seguente Hello utilizza hello tooperform Media Services .NET SDK seguenti attività:</span><span class="sxs-lookup"><span data-stu-id="325cf-135">hello following code example uses Media Services .NET SDK tooperform hello following tasks:</span></span>

* <span data-ttu-id="325cf-136">Creare un processo di codifica.</span><span class="sxs-lookup"><span data-stu-id="325cf-136">Create an encoding job.</span></span>
* <span data-ttu-id="325cf-137">Ottiene un codificatore Media Encoder Standard toohello di riferimento.</span><span class="sxs-lookup"><span data-stu-id="325cf-137">Get a reference toohello Media Encoder Standard encoder.</span></span>
* <span data-ttu-id="325cf-138">Specificare hello toouse [il flusso adattivo](media-services-autogen-bitrate-ladder-with-mes.md) predefinito.</span><span class="sxs-lookup"><span data-stu-id="325cf-138">Specify toouse hello [Adaptive Streaming](media-services-autogen-bitrate-ladder-with-mes.md) preset.</span></span> 
* <span data-ttu-id="325cf-139">Aggiungere un singolo processo di toohello codifica di attività.</span><span class="sxs-lookup"><span data-stu-id="325cf-139">Add a single encoding task toohello job.</span></span> 
* <span data-ttu-id="325cf-140">Specificare l'input hello toobe asset codificato.</span><span class="sxs-lookup"><span data-stu-id="325cf-140">Specify hello input asset toobe encoded.</span></span>
* <span data-ttu-id="325cf-141">Creare un asset di output che conterrà l'asset codificato hello.</span><span class="sxs-lookup"><span data-stu-id="325cf-141">Create an output asset that will contain hello encoded asset.</span></span>
* <span data-ttu-id="325cf-142">Aggiungere un avanzamento del processo hello toocheck gestore dell'evento.</span><span class="sxs-lookup"><span data-stu-id="325cf-142">Add an event handler toocheck hello job progress.</span></span>
* <span data-ttu-id="325cf-143">Inviare il processo di hello.</span><span class="sxs-lookup"><span data-stu-id="325cf-143">Submit hello job.</span></span>

#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="325cf-144">Creare e configurare un progetto di Visual Studio</span><span class="sxs-lookup"><span data-stu-id="325cf-144">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="325cf-145">Configurare l'ambiente di sviluppo e di popolare il file app. config hello con informazioni di connessione, come descritto in [lo sviluppo di servizi multimediali con .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="325cf-145">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="325cf-146">Esempio</span><span class="sxs-lookup"><span data-stu-id="325cf-146">Example</span></span> 

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

                    // Create a task with hello encoding details, using a string preset.
                    // In this case "Adaptive Streaming" preset is used.
                    ITask task = job.Tasks.AddNew("My encoding task",
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

## <a name="media-services-learning-paths"></a><span data-ttu-id="325cf-147">Percorsi di apprendimento di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="325cf-147">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="325cf-148">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="325cf-148">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a><span data-ttu-id="325cf-149">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="325cf-149">Next steps</span></span>
<span data-ttu-id="325cf-150">[La modalità anteprima toogenerate con Media Encoder Standard .NET](media-services-dotnet-generate-thumbnail-with-mes.md)
[codifica Panoramica di servizi multimediali](media-services-encode-asset.md)</span><span class="sxs-lookup"><span data-stu-id="325cf-150">[How toogenerate thumbnail using Media Encoder Standard with .NET](media-services-dotnet-generate-thumbnail-with-mes.md)
[Media Services Encoding Overview](media-services-encode-asset.md)</span></span>

