---
title: Personalizzazione dei set di impostazioni di Media Encoder Standard | Documentazione Microsoft
description: "Questo argomento illustra come eseguire la codifica avanzata personalizzando i set di impostazioni delle attività di Media Encoder Standard. Questo argomento illustra come usare Media Services .NET SDK per creare un processo e un'attività di codifica. Illustra anche come specificare set di impostazioni personalizzati per il processo di codifica."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: ec95392f-d34a-4c22-a6df-5274eaac445b
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: juliako
ms.openlocfilehash: b4d25f07349043da8cb745930fde3371c98f9960
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="customizing-media-encoder-standard-presets"></a><span data-ttu-id="a4876-105">Personalizzazione dei set di impostazioni di Media Encoder Standard</span><span class="sxs-lookup"><span data-stu-id="a4876-105">Customizing Media Encoder Standard presets</span></span>

## <a name="overview"></a><span data-ttu-id="a4876-106">Panoramica</span><span class="sxs-lookup"><span data-stu-id="a4876-106">Overview</span></span>

<span data-ttu-id="a4876-107">Questo argomento illustra come eseguire le attività di codifica avanzata con Media Encoder Standard usando un set di impostazioni personalizzato.</span><span class="sxs-lookup"><span data-stu-id="a4876-107">This topic shows how to perform advanced encoding with Media Encoder Standard (MES) using a custom preset.</span></span> <span data-ttu-id="a4876-108">In questo argomento viene usato .NET per creare un'attività di codifica e un processo che la esegue.</span><span class="sxs-lookup"><span data-stu-id="a4876-108">The topic uses .NET to create an encoding task and a job that executes this task.</span></span>  

<span data-ttu-id="a4876-109">L'argomento illustra come personalizzare un set di impostazioni partendo dal set di impostazioni [Codec video H.264 a bitrate multiplo con risoluzione 720p](media-services-mes-preset-H264-Multiple-Bitrate-720p.md) e riducendo il numero di livelli.</span><span class="sxs-lookup"><span data-stu-id="a4876-109">In this topic you will see how to customize a preset by taking the [H264 Multiple Bitrate 720p](media-services-mes-preset-H264-Multiple-Bitrate-720p.md) preset and reducing the number of layers.</span></span> <span data-ttu-id="a4876-110">L'argomento [Personalizzazione dei set di impostazioni di Media Encoder Standard](media-services-advanced-encoding-with-mes.md) illustra i set di impostazioni personalizzati che è possibile usare per eseguire attività di codifica avanzata.</span><span class="sxs-lookup"><span data-stu-id="a4876-110">The [Customizing Media Encoder Standard presets](media-services-advanced-encoding-with-mes.md) topic demonstrates custom presets that can be used to perform advanced encoding tasks.</span></span>

## <span data-ttu-id="a4876-111"><a id="customizing_presets"></a> Personalizzazione di un set di impostazioni di Media Encoder Standard</span><span class="sxs-lookup"><span data-stu-id="a4876-111"><a id="customizing_presets"></a> Customizing a MES preset</span></span>

### <a name="original-preset"></a><span data-ttu-id="a4876-112">Set di impostazioni originale</span><span class="sxs-lookup"><span data-stu-id="a4876-112">Original preset</span></span>

<span data-ttu-id="a4876-113">Salvare il codice JSON definito nell'argomento [Codec video H.264 a bitrate multiplo con risoluzione 720p](media-services-mes-preset-H264-Multiple-Bitrate-720p.md) in un file con estensione json.</span><span class="sxs-lookup"><span data-stu-id="a4876-113">Save the JSON defined in the [H264 Multiple Bitrate 720p](media-services-mes-preset-H264-Multiple-Bitrate-720p.md) topic in some file with .json extension.</span></span> <span data-ttu-id="a4876-114">Ad esempio, **CustomPreset_JSON.json**.</span><span class="sxs-lookup"><span data-stu-id="a4876-114">For example, **CustomPreset_JSON.json**.</span></span>

### <a name="customized-preset"></a><span data-ttu-id="a4876-115">Set di impostazioni personalizzato</span><span class="sxs-lookup"><span data-stu-id="a4876-115">Customized preset</span></span>

<span data-ttu-id="a4876-116">Aprire il file **CustomPreset_JSON.json** e rimuovere i primi tre livelli da **H264Layers** in modo che il file sia simile al seguente.</span><span class="sxs-lookup"><span data-stu-id="a4876-116">Open the **CustomPreset_JSON.json** file and remove first three layers from **H264Layers** so your file looks like this.</span></span>

    
    {  
      "Version": 1.0,  
      "Codecs": [  
        {  
          "KeyFrameInterval": "00:00:02",  
          "H264Layers": [  
            {  
              "Profile": "Auto",  
              "Level": "auto",  
              "Bitrate": 1000,  
              "MaxBitrate": 1000,  
              "BufferWindow": "00:00:05",  
              "Width": 640,  
              "Height": 360,  
              "BFrames": 3,  
              "ReferenceFrames": 3,  
              "AdaptiveBFrame": true,  
              "Type": "H264Layer",  
              "FrameRate": "0/1"  
            },  
            {  
              "Profile": "Auto",  
              "Level": "auto",  
              "Bitrate": 650,  
              "MaxBitrate": 650,  
              "BufferWindow": "00:00:05",  
              "Width": 640,  
              "Height": 360,  
              "BFrames": 3,  
              "ReferenceFrames": 3,  
              "AdaptiveBFrame": true,  
              "Type": "H264Layer",  
              "FrameRate": "0/1"  
            },  
            {  
              "Profile": "Auto",  
              "Level": "auto",  
              "Bitrate": 400,  
              "MaxBitrate": 400,  
              "BufferWindow": "00:00:05",  
              "Width": 320,  
              "Height": 180,  
              "BFrames": 3,  
              "ReferenceFrames": 3,  
              "AdaptiveBFrame": true,  
              "Type": "H264Layer",  
              "FrameRate": "0/1"  
            }  
          ],  
          "Type": "H264Video"  
        },  
        {  
          "Profile": "AACLC",  
          "Channels": 2,  
          "SamplingRate": 48000,  
          "Bitrate": 128,  
          "Type": "AACAudio"  
        }  
      ],  
      "Outputs": [  
        {  
          "FileName": "{Basename}_{Width}x{Height}_{VideoBitrate}.mp4",  
          "Format": {  
            "Type": "MP4Format"  
          }  
        }  
      ]  
    }  
    

## <span data-ttu-id="a4876-117"><a id="encoding_with_dotnet"></a>Codifica con l’SDK .NET dei servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="a4876-117"><a id="encoding_with_dotnet"></a>Encoding with Media Services .NET SDK</span></span>

<span data-ttu-id="a4876-118">Il seguente codice usa l'SDK .NET di Servizi multimediali per eseguire le seguenti attività: </span><span class="sxs-lookup"><span data-stu-id="a4876-118">The following code example uses Media Services .NET SDK to perform the following tasks:</span></span>

- <span data-ttu-id="a4876-119">Creare un processo di codifica.</span><span class="sxs-lookup"><span data-stu-id="a4876-119">Create an encoding job.</span></span>
- <span data-ttu-id="a4876-120">Ottenere un riferimento al codificatore Media Encoder Standard.</span><span class="sxs-lookup"><span data-stu-id="a4876-120">Get a reference to the Media Encoder Standard encoder.</span></span>
- <span data-ttu-id="a4876-121">Caricare il set di impostazioni personalizzato JSON creato nella sezione precedente.</span><span class="sxs-lookup"><span data-stu-id="a4876-121">Load the custom JSON preset that you created in the previous section.</span></span> 
  
        // Load the JSON from the local file.
        string configuration = File.ReadAllText(fileName);  

- <span data-ttu-id="a4876-122">Aggiungere un'attività di codifica al processo.</span><span class="sxs-lookup"><span data-stu-id="a4876-122">Add an encoding task to the job.</span></span> 
- <span data-ttu-id="a4876-123">Specificare l’asset di input da codificare.</span><span class="sxs-lookup"><span data-stu-id="a4876-123">Specify the input asset to be encoded.</span></span>
- <span data-ttu-id="a4876-124">Creare un asset di output che conterrà l'asset codificato.</span><span class="sxs-lookup"><span data-stu-id="a4876-124">Create an output asset that will contain the encoded asset.</span></span>
- <span data-ttu-id="a4876-125">Aggiungere un gestore eventi per controllare l'avanzamento del processo.</span><span class="sxs-lookup"><span data-stu-id="a4876-125">Add an event handler to check the job progress.</span></span>
- <span data-ttu-id="a4876-126">Inviare il processo.</span><span class="sxs-lookup"><span data-stu-id="a4876-126">Submit the job.</span></span>
   
#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="a4876-127">Creare e configurare un progetto di Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a4876-127">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="a4876-128">Configurare l'ambiente di sviluppo e popolare il file app.config con le informazioni di connessione, come descritto in [Sviluppo di applicazioni di Servizi multimediali con .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="a4876-128">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="a4876-129">Esempio</span><span class="sxs-lookup"><span data-stu-id="a4876-129">Example</span></span>   

    using System;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Threading;

    namespace CustomizeMESPresests
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

        private static readonly string _mediaFiles =
            Path.GetFullPath(@"../..\Media");

        private static readonly string _singleMP4File =
            Path.Combine(_mediaFiles, @"BigBuckBunny.mp4");

        static void Main(string[] args)
        {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

            // Get an uploaded asset.
            var asset = _context.Assets.FirstOrDefault();

            // Encode and generate the output using custom presets.
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

            // Load the XML (or JSON) from the local file.
            string configuration = File.ReadAllText("CustomPreset_JSON.json");

            // Create a task
            ITask task = job.Tasks.AddNew("Media Encoder Standard encoding task",
            processor,
            configuration,
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

## <a name="media-services-learning-paths"></a><span data-ttu-id="a4876-130">Percorsi di apprendimento di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="a4876-130">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="a4876-131">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="a4876-131">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="a4876-132">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="a4876-132">See Also</span></span>
[<span data-ttu-id="a4876-133">Panoramica sulla codifica dei servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="a4876-133">Media Services Encoding Overview</span></span>](media-services-encode-asset.md)

