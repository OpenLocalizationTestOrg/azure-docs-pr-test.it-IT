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
# <a name="how-toogenerate-thumbnails-using-media-encoder-standard-with-net"></a>Come anteprime toogenerate Media Encoder Standard con .NET

È possibile utilizzare uno o più anteprime toogenerate Media Encoder Standard dall'input del video in [JPEG](https://en.wikipedia.org/wiki/JPEG), [PNG](https://en.wikipedia.org/wiki/Portable_Network_Graphics), o [BMP](https://en.wikipedia.org/wiki/BMP_file_format) formati di file di immagine. È possibile inviare attività che producono solo immagini oppure combinare la generazione di anteprime con la codifica. Questo argomento offre alcuni set di impostazioni di anteprima XML e JSON di esempio per questi scenari. Alla fine di hello di hello argomento, è un [codice di esempio](#code_sample) che mostra come toouse hello Media Services .NET SDK tooaccomplish hello attività di codifica.

Per ulteriori informazioni sugli elementi hello utilizzati nel set di impostazioni di esempio, è necessario rivedere [schema Media Encoder Standard](media-services-mes-schema.md).

Verificare che hello tooreview [considerazioni](media-services-dotnet-generate-thumbnail-with-mes.md#considerations) sezione.

## <a name="example--single-png-file"></a>Esempio: singolo file PNG

Hello seguente JSON e XML predefinito può essere utilizzato tooproduce un singolo output PNG file fuori hello innanzitutto alcuni secondi del video di input hello, in cui il codificatore hello effettua un tentativo di sforzo individuare un frame "interessante". Si noti che sono state impostate le dimensioni dell'immagine di output di hello % too100, vale a dire che questi corrisponderà dimensioni hello del video di input di hello. Si noti anche come l'impostazione "Format" hello "Output" è necessario utilizzare hello toomatch di "PngLayers" nella sezione "Codec" hello. 

### <a name="json-preset"></a>Set di impostazioni JSON

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
    
### <a name="xml-preset"></a>Set di impostazioni XML

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

## <a name="example--a-series-of-jpeg-images"></a>Esempio: serie di immagini JPEG

Hello seguente JSON e XML predefinito può essere utilizzato tooproduce un set di immagini con timestamp % 5, 10 15%,..., 95% della sequenza temporale input hello, in cui hello dimensione dell'immagine è specificato toobe un quarto di hello video di input.

### <a name="json-preset"></a>Set di impostazioni JSON

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

### <a name="xml-preset"></a>Set di impostazioni XML
    
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

## <a name="example--one-image-at-a-specific-timestamp"></a>Esempio: un'immagine in corrispondenza di un timestamp specifico

è possibile tooproduce utilizzata una singola immagine JPEG in hello secondo 30 contrassegnare del video di input hello Hello seguente set di impostazioni JSON e XML. Questa impostazione predefinita prevede che più di 30 secondi nella durata toobe input hello (avrà esito negativo processo hello else).

### <a name="json-preset"></a>Set di impostazioni JSON

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
    
### <a name="xml-preset"></a>Set di impostazioni XML
    
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

## <a id="code_sample"></a>Esempio: codificare il video e generare l'anteprima

esempio di codice seguente Hello utilizza hello tooperform Media Services .NET SDK seguenti attività:

* Creare un processo di codifica.
* Ottiene un codificatore Media Encoder Standard toohello di riferimento.
* Hello carico predefinito [XML](media-services-dotnet-generate-thumbnail-with-mes.md#xml) o [JSON](media-services-dotnet-generate-thumbnail-with-mes.md#json) contenenti hello codifica preimpostato, nonché le informazioni necessarie toogenerate anteprime. È possibile salvare questo [XML](media-services-dotnet-generate-thumbnail-with-mes.md#xml) o [JSON](media-services-dotnet-generate-thumbnail-with-mes.md#json) in hello un file e utilizzare file hello tooload di codice seguente.
  
        // Load hello XML (or JSON) from hello local file.
        string configuration = File.ReadAllText(fileName);  
* Aggiungere un singolo processo di toohello codifica di attività. 
* Specificare l'input hello toobe asset codificato.
* Creare un asset di output che conterrà l'asset codificato hello.
* Aggiungere un avanzamento del processo hello toocheck gestore dell'evento.
* Inviare il processo di hello.

Vedere hello [lo sviluppo di servizi multimediali con .NET](media-services-dotnet-how-to-use.md) argomento per istruzioni su come tooset dell'ambiente di sviluppo.

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

## <a id="json"></a>Anteprima JSON predefinito
Per informazioni sullo schema, vedere [questo](https://msdn.microsoft.com/library/mt269962.aspx) argomento.

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

## <a id="xml"></a>Anteprima XML predefinito
Per informazioni sullo schema, vedere [questo](https://msdn.microsoft.com/library/mt269962.aspx) argomento.
    
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

## <a name="considerations"></a>Considerazioni
si applica Hello seguenti considerazioni:

* utilizzo di Hello del timestamp esplicito per Inizio passaggio/intervallo presuppone che tale origine di input hello è lungo almeno 1 minuto.
* Gli elementi Jpg/Png/BmpImage hanno gli attributi inizio, passaggio e intervallo della stringa, che possono essere interpretati come:
  
  * Se sono numeri interi non negativi, numero di frame, ad esempio "Start": "120",
  * Durata toosource relativo se espresso come presenta il suffisso %, ad esempio. "Start": "15%", OPPURE
  * Timestamp se espresso come HH:MM:SS (formato). ed esempio "Start" : "00:01:00"
    
    È possibile combinare e associare le notazioni a piacimento.
    
    Inizio supporta inoltre anche una Macro speciale: {ottimale}, che tenta di toodetermine hello primo "interessante" frame di contenuto hello Nota: (passaggio e intervallo vengono ignorati quando l'avvio viene impostato troppo {migliore})
  * Impostazioni predefinite: Start: {Best}
* Formato di output deve toobe forniti in modo esplicito per ogni formato di immagine: Jpg o Png/BmpFormat. Se presente, MES corrisponderanno JpgVideo tooJpgFormat e così via. OutputFormat introduce una nuova immagine codec specifico (macro): {indice}, che richiede toobe presente (una volta e una sola volta) per formati di output di immagine.

## <a name="next-steps"></a>Passaggi successivi

È possibile controllare hello [lo stato di avanzamento del processo](media-services-check-job-progress.md) hello durante il processo di codifica è in sospeso.

## <a name="media-services-learning-paths"></a>Percorsi di apprendimento di Servizi multimediali
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornire commenti e suggerimenti
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>Vedere anche
[Panoramica sulla codifica dei servizi multimediali](media-services-encode-asset.md)

