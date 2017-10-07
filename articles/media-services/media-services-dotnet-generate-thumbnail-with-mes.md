---
title: anteprime toogenerate aaaHow Media Encoder Standard con .NET
description: Questo argomento viene illustrato come toouse .NET tooencode un asset e generare anteprime in hello contemporaneamente utilizzando Media Encoder Standard.
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: b8dab73a-1d91-4b6d-9741-a92ad39fc3f7
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: juliako
ms.openlocfilehash: 23d3e4d9bf64a688d45499c045f19d2792167990
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toogenerate-thumbnails-using-media-encoder-standard-with-net"></a><span data-ttu-id="68f67-103">Come anteprime toogenerate Media Encoder Standard con .NET</span><span class="sxs-lookup"><span data-stu-id="68f67-103">How toogenerate thumbnails using Media Encoder Standard with .NET</span></span>

<span data-ttu-id="68f67-104">È possibile utilizzare uno o più anteprime toogenerate Media Encoder Standard dall'input del video in [JPEG](https://en.wikipedia.org/wiki/JPEG), [PNG](https://en.wikipedia.org/wiki/Portable_Network_Graphics), o [BMP](https://en.wikipedia.org/wiki/BMP_file_format) formati di file di immagine.</span><span class="sxs-lookup"><span data-stu-id="68f67-104">You can use Media Encoder Standard toogenerate one or more thumbnails from your input video in [JPEG](https://en.wikipedia.org/wiki/JPEG), [PNG](https://en.wikipedia.org/wiki/Portable_Network_Graphics), or [BMP](https://en.wikipedia.org/wiki/BMP_file_format) image file formats.</span></span> <span data-ttu-id="68f67-105">È possibile inviare attività che producono solo immagini oppure combinare la generazione di anteprime con la codifica.</span><span class="sxs-lookup"><span data-stu-id="68f67-105">You can submit Tasks that produce only images, or you can combine thumbnail generation with encoding.</span></span> <span data-ttu-id="68f67-106">Questo argomento offre alcuni set di impostazioni di anteprima XML e JSON di esempio per questi scenari.</span><span class="sxs-lookup"><span data-stu-id="68f67-106">This topic provides a few sample XML and JSON thumbnail presets for such scenarios.</span></span> <span data-ttu-id="68f67-107">Alla fine di hello di hello argomento, è un [codice di esempio](#code_sample) che mostra come toouse hello Media Services .NET SDK tooaccomplish hello attività di codifica.</span><span class="sxs-lookup"><span data-stu-id="68f67-107">At hello end of hello topic, there is a [sample code](#code_sample) that shows how toouse hello Media Services .NET SDK tooaccomplish hello encoding task.</span></span>

<span data-ttu-id="68f67-108">Per ulteriori informazioni sugli elementi hello utilizzati nel set di impostazioni di esempio, è necessario rivedere [schema Media Encoder Standard](media-services-mes-schema.md).</span><span class="sxs-lookup"><span data-stu-id="68f67-108">For more details on hello elements that are used in sample presets, you should review [Media Encoder Standard schema](media-services-mes-schema.md).</span></span>

<span data-ttu-id="68f67-109">Verificare che hello tooreview [considerazioni](media-services-dotnet-generate-thumbnail-with-mes.md#considerations) sezione.</span><span class="sxs-lookup"><span data-stu-id="68f67-109">Make sure tooreview hello [Considerations](media-services-dotnet-generate-thumbnail-with-mes.md#considerations) section.</span></span>

## <a name="example--single-png-file"></a><span data-ttu-id="68f67-110">Esempio: singolo file PNG</span><span class="sxs-lookup"><span data-stu-id="68f67-110">Example – single PNG file</span></span>

<span data-ttu-id="68f67-111">Hello seguente JSON e XML predefinito può essere utilizzato tooproduce un singolo output PNG file fuori hello innanzitutto alcuni secondi del video di input hello, in cui il codificatore hello effettua un tentativo di sforzo individuare un frame "interessante".</span><span class="sxs-lookup"><span data-stu-id="68f67-111">hello following JSON and XML preset can be used tooproduce a single output PNG file out of hello first few seconds of hello input video, where hello encoder makes a best-effort attempt at finding an “interesting” frame.</span></span> <span data-ttu-id="68f67-112">Si noti che sono state impostate le dimensioni dell'immagine di output di hello % too100, vale a dire che questi corrisponderà dimensioni hello del video di input di hello.</span><span class="sxs-lookup"><span data-stu-id="68f67-112">Note that hello output image dimensions have been set too100%, meaning these will match hello dimensions of hello input video.</span></span> <span data-ttu-id="68f67-113">Si noti anche come l'impostazione "Format" hello "Output" è necessario utilizzare hello toomatch di "PngLayers" nella sezione "Codec" hello.</span><span class="sxs-lookup"><span data-stu-id="68f67-113">Note also how hello “Format” setting in “Outputs” is required toomatch hello use of “PngLayers” in hello “Codecs” section.</span></span> 

### <a name="json-preset"></a><span data-ttu-id="68f67-114">Set di impostazioni JSON</span><span class="sxs-lookup"><span data-stu-id="68f67-114">JSON preset</span></span>

    {
      "Version": 1.0,
      "Codecs": [
        {
          "PngLayers": [
            {
              "Type": "PngLayer",
              "Width": "100%",
              "Height": "100%"
            }
          ],
          "Start": "{Best}",
          "Type": "PngImage"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}_{Index}{Extension}",
          "Format": {
            "Type": "PngFormat"
          }
        }
      ]
    }
    
### <a name="xml-preset"></a><span data-ttu-id="68f67-115">Set di impostazioni XML</span><span class="sxs-lookup"><span data-stu-id="68f67-115">XML preset</span></span>

    <?xml version="1.0" encoding="utf-16"?>
    <Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
      <Encoding>
        <PngImage Start="{Best}">
          <PngLayers>
            <PngLayer>
              <Width>100%</Width>
              <Height>100%</Height>
            </PngLayer>
          </PngLayers>
        </PngImage>
      </Encoding>
      <Outputs>
        <Output FileName="{Basename}_{Index}{Extension}">
          <PngFormat />
        </Output>
      </Outputs>
    </Preset>

## <a name="example--a-series-of-jpeg-images"></a><span data-ttu-id="68f67-116">Esempio: serie di immagini JPEG</span><span class="sxs-lookup"><span data-stu-id="68f67-116">Example – a series of JPEG images</span></span>

<span data-ttu-id="68f67-117">Hello seguente JSON e XML predefinito può essere utilizzato tooproduce un set di immagini con timestamp % 5, 10 15%,..., 95% della sequenza temporale input hello, in cui hello dimensione dell'immagine è specificato toobe un quarto di hello video di input.</span><span class="sxs-lookup"><span data-stu-id="68f67-117">hello following JSON and XML preset can be used tooproduce a set of 10 images at timestamps of 5%, 15%, …, 95% of hello input timeline, where hello image size is specified toobe one quarter that of hello input video.</span></span>

### <a name="json-preset"></a><span data-ttu-id="68f67-118">Set di impostazioni JSON</span><span class="sxs-lookup"><span data-stu-id="68f67-118">JSON preset</span></span>

    {
      "Version": 1.0,
      "Codecs": [
        {
          "JpgLayers": [
            {
              "Quality": 90,
              "Type": "JpgLayer",
              "Width": "25%",
              "Height": "25%"
            }
          ],
          "Start": "5%",
          "Step": "1",
          "Range": "1",
          "Type": "JpgImage"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}_{Index}{Extension}",
          "Format": {
            "Type": "JpgFormat"
          }
        }
      ]
    }

### <a name="xml-preset"></a><span data-ttu-id="68f67-119">Set di impostazioni XML</span><span class="sxs-lookup"><span data-stu-id="68f67-119">XML preset</span></span>
    
    <?xml version="1.0" encoding="utf-16"?>
    <Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
      <Encoding>
        <JpgImage Start="5%" Step="10%" Range="96%">
          <JpgLayers>
            <JpgLayer>
              <Width>25%</Width>
              <Height>25%</Height>
              <Quality>90</Quality>
            </JpgLayer>
          </JpgLayers>
        </JpgImage>
      </Encoding>
      <Outputs>
        <Output FileName="{Basename}_{Index}{Extension}">
          <JpgFormat />
        </Output>
      </Outputs>
    </Preset>

## <a name="example--one-image-at-a-specific-timestamp"></a><span data-ttu-id="68f67-120">Esempio: un'immagine in corrispondenza di un timestamp specifico</span><span class="sxs-lookup"><span data-stu-id="68f67-120">Example – one image at a specific timestamp</span></span>

<span data-ttu-id="68f67-121">è possibile tooproduce utilizzata una singola immagine JPEG in hello secondo 30 contrassegnare del video di input hello Hello seguente set di impostazioni JSON e XML.</span><span class="sxs-lookup"><span data-stu-id="68f67-121">hello following JSON and XML preset can be used tooproduce a single JPEG image at hello 30 second mark of hello input video.</span></span> <span data-ttu-id="68f67-122">Questa impostazione predefinita prevede che più di 30 secondi nella durata toobe input hello (avrà esito negativo processo hello else).</span><span class="sxs-lookup"><span data-stu-id="68f67-122">This preset expects hello input toobe more than 30 seconds in duration (else hello job will fail).</span></span>

### <a name="json-preset"></a><span data-ttu-id="68f67-123">Set di impostazioni JSON</span><span class="sxs-lookup"><span data-stu-id="68f67-123">JSON preset</span></span>

    {
      "Version": 1.0,
      "Codecs": [
        {
          "JpgLayers": [
            {
              "Quality": 90,
              "Type": "JpgLayer",
              "Width": "25%",
              "Height": "25%"
            }
          ],
          "Start": "00:00:30",
          "Step": "1",
          "Range": "1",
          "Type": "JpgImage"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}_{Index}{Extension}",
          "Format": {
            "Type": "JpgFormat"
          }
        }
      ]
    }
    
### <a name="xml-preset"></a><span data-ttu-id="68f67-124">Set di impostazioni XML</span><span class="sxs-lookup"><span data-stu-id="68f67-124">XML preset</span></span>
    
    <?xml version="1.0" encoding="utf-16"?>
    <Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
      <Encoding>
        <JpgImage Start="00:00:30" Step="00:00:02" Range="00:00:01">
          <JpgLayers>
            <JpgLayer>
              <Width>25%</Width>
              <Height>25%</Height>
              <Quality>90</Quality>
            </JpgLayer>
          </JpgLayers>
        </JpgImage>
      </Encoding>
      <Outputs>
        <Output FileName="{Basename}_{Index}{Extension}">
          <JpgFormat />
        </Output>
      </Outputs>
    </Preset>

## <span data-ttu-id="68f67-125"><a id="code_sample"></a>Esempio: codificare il video e generare l'anteprima</span><span class="sxs-lookup"><span data-stu-id="68f67-125"><a id="code_sample"></a>Example – encode video and generate thumbnail</span></span>

<span data-ttu-id="68f67-126">esempio di codice seguente Hello utilizza hello tooperform Media Services .NET SDK seguenti attività:</span><span class="sxs-lookup"><span data-stu-id="68f67-126">hello following code example uses Media Services .NET SDK tooperform hello following tasks:</span></span>

* <span data-ttu-id="68f67-127">Creare un processo di codifica.</span><span class="sxs-lookup"><span data-stu-id="68f67-127">Create an encoding job.</span></span>
* <span data-ttu-id="68f67-128">Ottiene un codificatore Media Encoder Standard toohello di riferimento.</span><span class="sxs-lookup"><span data-stu-id="68f67-128">Get a reference toohello Media Encoder Standard encoder.</span></span>
* <span data-ttu-id="68f67-129">Hello carico predefinito [XML](media-services-dotnet-generate-thumbnail-with-mes.md#xml) o [JSON](media-services-dotnet-generate-thumbnail-with-mes.md#json) contenenti hello codifica preimpostato, nonché le informazioni necessarie toogenerate anteprime.</span><span class="sxs-lookup"><span data-stu-id="68f67-129">Load hello preset [XML](media-services-dotnet-generate-thumbnail-with-mes.md#xml) or [JSON](media-services-dotnet-generate-thumbnail-with-mes.md#json) that contain hello encoding preset as well as information needed toogenerate thumbnails.</span></span> <span data-ttu-id="68f67-130">È possibile salvare questo [XML](media-services-dotnet-generate-thumbnail-with-mes.md#xml) o [JSON](media-services-dotnet-generate-thumbnail-with-mes.md#json) in hello un file e utilizzare file hello tooload di codice seguente.</span><span class="sxs-lookup"><span data-stu-id="68f67-130">You can save this  [XML](media-services-dotnet-generate-thumbnail-with-mes.md#xml) or [JSON](media-services-dotnet-generate-thumbnail-with-mes.md#json) in a file and use hello following code tooload hello file.</span></span>
  
        // Load hello XML (or JSON) from hello local file.
        string configuration = File.ReadAllText(fileName);  
* <span data-ttu-id="68f67-131">Aggiungere un singolo processo di toohello codifica di attività.</span><span class="sxs-lookup"><span data-stu-id="68f67-131">Add a single encoding task toohello job.</span></span> 
* <span data-ttu-id="68f67-132">Specificare l'input hello toobe asset codificato.</span><span class="sxs-lookup"><span data-stu-id="68f67-132">Specify hello input asset toobe encoded.</span></span>
* <span data-ttu-id="68f67-133">Creare un asset di output che conterrà l'asset codificato hello.</span><span class="sxs-lookup"><span data-stu-id="68f67-133">Create an output asset that will contain hello encoded asset.</span></span>
* <span data-ttu-id="68f67-134">Aggiungere un avanzamento del processo hello toocheck gestore dell'evento.</span><span class="sxs-lookup"><span data-stu-id="68f67-134">Add an event handler toocheck hello job progress.</span></span>
* <span data-ttu-id="68f67-135">Inviare il processo di hello.</span><span class="sxs-lookup"><span data-stu-id="68f67-135">Submit hello job.</span></span>

<span data-ttu-id="68f67-136">Vedere hello [lo sviluppo di servizi multimediali con .NET](media-services-dotnet-how-to-use.md) argomento per istruzioni su come tooset dell'ambiente di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="68f67-136">See hello [Media Services development with .NET](media-services-dotnet-how-to-use.md) topic for directions on how tooset up your dev environment.</span></span>

        using System;
        using System.Configuration;
        using System.IO;
        using System.Linq;
        using Microsoft.WindowsAzure.MediaServices.Client;
        using System.Threading;

        namespace EncodeAndGenerateThumbnails
        {
        class Program
        {
            // Read values from hello App.config file.
            private static readonly string _AADTenantDomain =
            ConfigurationManager.AppSettings["AADTenantDomain"];
            private static readonly string _RESTAPIEndpoint =
            ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

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

            // Encode and generate hello thumbnails.
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

            // Load hello XML (or JSON) from hello local file.
            string configuration = File.ReadAllText("ThumbnailPreset_JSON.json");

            // Create a task
            ITask task = job.Tasks.AddNew("Media Encoder Standard encoding task",
                processor,
                configuration,
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

## <span data-ttu-id="68f67-137"><a id="json"></a>Anteprima JSON predefinito</span><span class="sxs-lookup"><span data-stu-id="68f67-137"><a id="json"></a>Thumbnail JSON preset</span></span>
<span data-ttu-id="68f67-138">Per informazioni sullo schema, vedere [questo](https://msdn.microsoft.com/library/mt269962.aspx) argomento.</span><span class="sxs-lookup"><span data-stu-id="68f67-138">For information about schema, see [this](https://msdn.microsoft.com/library/mt269962.aspx) topic.</span></span>

    {
      "Version": 1.0,
      "Codecs": [
        {
          "KeyFrameInterval": "00:00:02",
          "SceneChangeDetection": "true",
          "H264Layers": [
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 4500,
              "MaxBitrate": 4500,
              "BufferWindow": "00:00:05",
              "Width": 1280,
              "Height": 720,
              "ReferenceFrames": 3,
              "EntropyMode": "Cabac",
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"
    
            }
          ],
          "Type": "H264Video"
        },
        {
          "JpgLayers": [
            {
              "Quality": 90,
              "Type": "JpgLayer",
              "Width": "100%",
              "Height": "100%"
            }
          ],
          "Start": "{Best}",
          "Type": "JpgImage"
        },
        {
          "Channels": 2,
          "SamplingRate": 48000,
          "Bitrate": 128,
          "Type": "AACAudio"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}_{Index}{Extension}",
          "Format": {
            "Type": "JpgFormat"
          }
        },
        {
          "FileName": "{Basename}_{Resolution}_{VideoBitrate}.mp4",
          "Format": {
            "Type": "MP4Format"
          }
        }
      ]
    }

## <span data-ttu-id="68f67-139"><a id="xml"></a>Anteprima XML predefinito</span><span class="sxs-lookup"><span data-stu-id="68f67-139"><a id="xml"></a>Thumbnail XML preset</span></span>
<span data-ttu-id="68f67-140">Per informazioni sullo schema, vedere [questo](https://msdn.microsoft.com/library/mt269962.aspx) argomento.</span><span class="sxs-lookup"><span data-stu-id="68f67-140">For information about schema, see [this](https://msdn.microsoft.com/library/mt269962.aspx) topic.</span></span>
    
    <?xml version="1.0" encoding="utf-16"?>
    <Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
      <Encoding>
        <H264Video>
          <KeyFrameInterval>00:00:02</KeyFrameInterval>
          <SceneChangeDetection>true</SceneChangeDetection>
          <H264Layers>
            <H264Layer>
              <Bitrate>4500</Bitrate>
              <Width>1280</Width>
              <Height>720</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>3</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cabac</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>4500</MaxBitrate>
            </H264Layer>
          </H264Layers>
        </H264Video>
        <AACAudio>
          <Profile>AACLC</Profile>
          <Channels>2</Channels>
          <SamplingRate>48000</SamplingRate>
          <Bitrate>128</Bitrate>
        </AACAudio>
        <JpgImage Start="{Best}">
          <JpgLayers>
            <JpgLayer>
              <Width>100%</Width>
              <Height>100%/Height>
              <Quality>90</Quality>
            </JpgLayer>
          </JpgLayers>
        </JpgImage>
      </Encoding>
      <Outputs>
        <Output FileName="{Basename}_{Resolution}_{VideoBitrate}.mp4">
          <MP4Format />
        </Output>
        <Output FileName="{Basename}_{Index}{Extension}">
          <JpgFormat />
        </Output>
      </Outputs>
    </Preset>

## <a name="considerations"></a><span data-ttu-id="68f67-141">Considerazioni</span><span class="sxs-lookup"><span data-stu-id="68f67-141">Considerations</span></span>
<span data-ttu-id="68f67-142">si applica Hello seguenti considerazioni:</span><span class="sxs-lookup"><span data-stu-id="68f67-142">hello following considerations apply:</span></span>

* <span data-ttu-id="68f67-143">utilizzo di Hello del timestamp esplicito per Inizio passaggio/intervallo presuppone che tale origine di input hello è lungo almeno 1 minuto.</span><span class="sxs-lookup"><span data-stu-id="68f67-143">hello use of explicit timestamps for Start/Step/Range assumes that hello input source is at least 1 minute long.</span></span>
* <span data-ttu-id="68f67-144">Gli elementi Jpg/Png/BmpImage hanno gli attributi inizio, passaggio e intervallo della stringa, che possono essere interpretati come:</span><span class="sxs-lookup"><span data-stu-id="68f67-144">Jpg/Png/BmpImage elements have Start, Step and Range string attributes – these can be interpreted as:</span></span>
  
  * <span data-ttu-id="68f67-145">Se sono numeri interi non negativi, numero di frame, ad esempio</span><span class="sxs-lookup"><span data-stu-id="68f67-145">Frame Number if they are non-negative integers, eg.</span></span> <span data-ttu-id="68f67-146">"Start": "120",</span><span class="sxs-lookup"><span data-stu-id="68f67-146">"Start": "120",</span></span>
  * <span data-ttu-id="68f67-147">Durata toosource relativo se espresso come presenta il suffisso %, ad esempio.</span><span class="sxs-lookup"><span data-stu-id="68f67-147">Relative toosource duration if expressed as %-suffixed, eg.</span></span> <span data-ttu-id="68f67-148">"Start": "15%", OPPURE</span><span class="sxs-lookup"><span data-stu-id="68f67-148">"Start": "15%", OR</span></span>
  * <span data-ttu-id="68f67-149">Timestamp se espresso come HH:MM:SS</span><span class="sxs-lookup"><span data-stu-id="68f67-149">Timestamp if expressed as HH:MM:SS…</span></span> <span data-ttu-id="68f67-150">(formato).</span><span class="sxs-lookup"><span data-stu-id="68f67-150">format.</span></span> <span data-ttu-id="68f67-151">ed esempio</span><span class="sxs-lookup"><span data-stu-id="68f67-151">Eg.</span></span> <span data-ttu-id="68f67-152">"Start" : "00:01:00"</span><span class="sxs-lookup"><span data-stu-id="68f67-152">"Start" : "00:01:00"</span></span>
    
    <span data-ttu-id="68f67-153">È possibile combinare e associare le notazioni a piacimento.</span><span class="sxs-lookup"><span data-stu-id="68f67-153">You can mix and match notations as you please.</span></span>
    
    <span data-ttu-id="68f67-154">Inizio supporta inoltre anche una Macro speciale: {ottimale}, che tenta di toodetermine hello primo "interessante" frame di contenuto hello Nota: (passaggio e intervallo vengono ignorati quando l'avvio viene impostato troppo {migliore})</span><span class="sxs-lookup"><span data-stu-id="68f67-154">Additionally, Start also supports a special Macro:{Best}, which attempts toodetermine hello first “interesting” frame of hello content NOTE: (Step and Range are ignored when Start is set too{Best})</span></span>
  * <span data-ttu-id="68f67-155">Impostazioni predefinite: Start: {Best}</span><span class="sxs-lookup"><span data-stu-id="68f67-155">Defaults: Start:{Best}</span></span>
* <span data-ttu-id="68f67-156">Formato di output deve toobe forniti in modo esplicito per ogni formato di immagine: Jpg o Png/BmpFormat.</span><span class="sxs-lookup"><span data-stu-id="68f67-156">Output format needs toobe explicitly provided for each Image format: Jpg/Png/BmpFormat.</span></span> <span data-ttu-id="68f67-157">Se presente, MES corrisponderanno JpgVideo tooJpgFormat e così via.</span><span class="sxs-lookup"><span data-stu-id="68f67-157">When present, MES will match JpgVideo tooJpgFormat and so on.</span></span> <span data-ttu-id="68f67-158">OutputFormat introduce una nuova immagine codec specifico (macro): {indice}, che richiede toobe presente (una volta e una sola volta) per formati di output di immagine.</span><span class="sxs-lookup"><span data-stu-id="68f67-158">OutputFormat introduces a new image-codec specific Macro: {Index}, which needs toobe present (once and only once) for image output formats.</span></span>

## <a name="next-steps"></a><span data-ttu-id="68f67-159">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="68f67-159">Next steps</span></span>

<span data-ttu-id="68f67-160">È possibile controllare hello [lo stato di avanzamento del processo](media-services-check-job-progress.md) hello durante il processo di codifica è in sospeso.</span><span class="sxs-lookup"><span data-stu-id="68f67-160">You can check hello [job progress](media-services-check-job-progress.md) while hello encoding job is pending.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="68f67-161">Percorsi di apprendimento di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="68f67-161">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="68f67-162">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="68f67-162">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="68f67-163">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="68f67-163">See Also</span></span>
[<span data-ttu-id="68f67-164">Panoramica sulla codifica dei servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="68f67-164">Media Services Encoding Overview</span></span>](media-services-encode-asset.md)

