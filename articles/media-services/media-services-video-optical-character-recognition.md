---
title: testo aaaDigitize con Azure Media Analitica OCR | Documenti Microsoft
description: "Azure Media Analitica OCR (OCR) consente di tooconvert contenuto di testo nei file video in testo digitale modificabile, è possibile eseguire ricerca.  Ciò consente l'estrazione di hello tooautomate dei metadati significativo da segnale video di hello del supporto di."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 307c196e-3a50-4f4b-b982-51585448ffc6
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/31/2017
ms.author: juliako
ms.openlocfilehash: 0476c3ba3942b2c5182a34a429909adbf5c75ac9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-media-analytics-tooconvert-text-content-in-video-files-into-digital-text"></a>Utilizzare il contenuto di testo tooconvert Analitica multimediali di Azure nei file video in testo digitale
## <a name="overview"></a>Panoramica
Testo tooextract contenuto dai file video e di generare un testo modificabile, è possibile eseguire ricerca digitale, è necessario utilizzare Azure Media Analitica OCR (optical il riconoscimento di caratteri). Questo processore di contenuti multimediali di Azure rileva il contenuto di testo nei file video e genera file di testo pronti per l'uso. OCR consente si tooautomate hello estrazione dei metadati significativo da segnale video di hello del supporto di.

Se utilizzato in combinazione con un motore di ricerca, è possibile indicizzare i file multimediali dal testo facilmente e migliorare il rilevamento di hello del contenuto. Questa funzione risulta molto utile per i video che contengono un porzione importante di testo, ad esempio una registrazione video o l'acquisizione della schermata di una presentazione. Processore di contenuti multimediali di Azure OCR Hello è ottimizzato per testo digitale.

Hello **Azure Media OCR** processore di contenuti multimediali è attualmente in anteprima.

In questo argomento fornisce informazioni dettagliate sulle **Azure Media OCR** e Mostra come toouse con Media Services SDK per .NET. Per altre informazioni ed esempi, vedere [questo blog](https://azure.microsoft.com/blog/announcing-video-ocr-public-preview-new-config/).

## <a name="ocr-input-files"></a>File di input OCR
File video. Attualmente, è supportato i seguenti formati hello: MOV o MP4 e WMV.

## <a name="task-configuration"></a>Configurazione delle attività
Configurazione delle attività (set di impostazioni). Quando si crea un'attività con **Azure Media OCR**, è necessario specificare un set di impostazioni di configurazione tramite JSON o XML. 

>[!NOTE]
>il motore di riconoscimento Hello accetta solo un'area dell'immagine con minimo 40 pixel toomaximum 32000 come un input valido in entrambe altezza e la larghezza.
>

### <a name="attribute-descriptions"></a>Descrizioni degli attributi
| Nome attributo | Descrizione |
| --- | --- |
|AdvancedOutput| Se si imposta AdvancedOutput tootrue, l'output JSON hello conterrà dati posizionali per ogni singola parola (in aggiunta toophrases e le aree). Se non si desidera toosee questi dettagli set hello flag toofalse. valore predefinito di Hello è false. Per altre informazioni, vedere [questo blog](https://azure.microsoft.com/blog/azure-media-ocr-simplified-output/).|
| Lingua |(facoltativo) descrive lingua hello del testo per cui toolook. Uno dei seguenti hello: rilevamento automatico (predefinito), arabo, due lingue, ChineseTraditional, ceco danese, olandese, inglese, finlandese, francese, tedesco, greco, ungherese, italiano, giapponese, coreano, norvegese, polacco, portoghese, Romeno, russo, SerbianCyrillic, SerbianLatin, slovacco, spagnolo, svedese, turco. |
| TextOrientation |(facoltativo) descrive orientamento hello del testo per cui toolook.  Si fa riferimento a "Left" significa che hello parte superiore di tutte le lettere verso sinistra hello.  Il testo predefinito (simile a quello di un libro) può essere orientato come "Up".  Uno dei seguenti hello: rilevamento automatico (predefinito), verso l'alto, a destra, verso il basso, a sinistra. |
| TimeInterval |(facoltativo) descrive la frequenza di campionamento hello.  Il valore predefinito è ogni 1/2 secondo.<br/>Formato JSON: HH:mm:ss.SSS (impostazione predefinita 00:00:00.500)<br/>Formato XML – durata primitivi W3C XSD (predefinito PT0.5) |
| DetectRegions |(facoltativo) Una matrice di oggetti DetectRegion specificare aree all'interno di fotogrammi video hello del testo toodetect.<br/>Un oggetto DetectRegion è costituito da hello seguenti quattro valori integer:<br/>A sinistra: pixel da hello del margine sinistro<br/>Alto-pixel da hello per il margine superiore<br/>Larghezza: la larghezza dell'area di hello in pixel<br/>Height: altezza dell'area di hello in pixel |

#### <a name="json-preset-example"></a>Esempio di set di impostazioni JSON

    {
        "Version":1.0, 
        "Options": 
        {
            "AdvancedOutput":"true",
            "Language":"English", 
            "TimeInterval":"00:00:01.5",
            "TextOrientation":"Up",
            "DetectRegions": [
                    {
                       "Left": 10,
                       "Top": 10,
                       "Width": 100,
                       "Height": 50
                    }
             ]
        }
    }


#### <a name="xml-preset-example"></a>Esempio di set di impostazioni XML
    <?xml version=""1.0"" encoding=""utf-16""?>
    <VideoOcrPreset xmlns:xsi=""http://www.w3.org/2001/XMLSchema-instance"" xmlns:xsd=""http://www.w3.org/2001/XMLSchema"" Version=""1.0"" xmlns=""http://www.windowsazure.com/media/encoding/Preset/2014/03"">
      <Options>
         <AdvancedOutput>true</AdvancedOutput>
         <Language>English</Language>
         <TimeInterval>PT1.5S</TimeInterval>
         <DetectRegions>
             <DetectRegion>
                   <Left>10</Left>
                   <Top>10</Top>
                   <Width>100</Width>
                   <Height>50</Height>
            </DetectRegion>
       </DetectRegions>
       <TextOrientation>Up</TextOrientation>
      </Options>
    </VideoOcrPreset>

## <a name="ocr-output-files"></a>File di output OCR
output di Hello del processore di contenuti multimediali OCR hello è un file JSON.

### <a name="elements-of-hello-output-json-file"></a>Elementi hello JSON del file di output
output di Hello OCR Video fornisce i dati segmentati ora sui caratteri hello trovati nel video.  È possibile utilizzare gli attributi, ad esempio lingua o toohone orientamento esattamente le parole hello che si è interessati, l'analisi. 

output di Hello contiene hello gli attributi seguenti:

| Elemento | Descrizione |
| --- | --- |
| Scala cronologica |"tick" al secondo del video hello |
| Offset |Differenza di orario dei timestamp Nella versione 1.0 delle API Video, questo valore è sempre 0. |
| Frequenza fotogrammi |Fotogrammi al secondo di hello video |
| width |larghezza del video in pixel hello |
| height |altezza del video in pixel hello |
| Frammenti |Matrice di blocchi basati sull'ora del video in cui hello metadati sono bloccato |
| start |Ora di inizio di un frammento in "scatti" |
| duration |Lunghezza di un frammento in "scatti" |
| interval |intervallo di ogni evento all'interno di hello fornito frammento |
| eventi |Matrice contenente le aree |
| region |Oggetto che rappresenta le parole o le frasi rilevate |
| Linguaggio |lingua del testo hello rilevato all'interno di un'area |
| orientation |orientamento del testo hello rilevato all'interno di un'area |
| lines |Matrice di righe del testo rilevato all'interno di un'area |
| text |testo effettivo Hello |

### <a name="json-output-example"></a>Esempio di output JSON
Hello seguente esempio di output contiene le informazioni generali video hello e più frammenti video. In ogni frammento video, contiene ogni area in cui viene rilevato da MP OCR con lingua hello e l'orientamento del testo. area Hello contiene inoltre ogni riga di word in quest'area con testo della riga hello, la posizione della riga hello e tutte le informazioni di word (il contenuto di word, posizione e confidenza) in questa riga. Hello seguito è riportato un esempio e inserire alcuni commenti in linea.

    {
        "version": 1, 
        "timescale": 90000, 
        "offset": 0, 
        "framerate": 30, 
        "width": 640, 
        "height": 480,  // general video information
        "fragments": [
            {
                "start": 0, 
                "duration": 180000, 
                "interval": 90000,  // hello time information about this fragment
                "events": [
                    [
                       { 
                            "region": { // hello detected region array in this fragment 
                                "language": "English",  // region language
                                "orientation": "Up",  // text orientation
                                "lines": [  // line information array in this region, including hello text and hello position
                                    {
                                        "text": "One Two", 
                                        "left": 10, 
                                        "top": 10, 
                                        "right": 210, 
                                        "bottom": 110, 
                                        "word": [  // word information array in this line
                                            {
                                                "text": "One", 
                                                "left": 10, 
                                                "top": 10, 
                                                "right": 110, 
                                                "bottom": 110, 
                                                "confidence": 900
                                            }, 
                                            {
                                                "text": "Two", 
                                                "left": 110, 
                                                "top": 10, 
                                                "right": 210, 
                                                "bottom": 110, 
                                                "confidence": 910
                                            }
                                        ]
                                    }
                                ]
                            }
                        }
                    ]
                ]
            }
        ]
    }

## <a name="net-sample-code"></a>Codice di esempio .NET

esempio Hello programma mostra come:

1. Creare un asset e caricare un file multimediale nell'asset hello.
2. Creare un processo con un file di configurazione/set di impostazioni OCR.
3. Scaricare i file JSON di output di hello. 
   
#### <a name="create-and-configure-a-visual-studio-project"></a>Creare e configurare un progetto di Visual Studio

Configurare l'ambiente di sviluppo e di popolare il file app. config hello con informazioni di connessione, come descritto in [lo sviluppo di servizi multimediali con .NET](media-services-dotnet-how-to-use.md). 

#### <a name="example"></a>Esempio

    using System;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Threading;
    using System.Threading.Tasks;

    namespace OCR
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

                // Run hello OCR job.
                var asset = RunOCRJob(@"C:\supportFiles\OCR\presentation.mp4",
                                            @"C:\supportFiles\OCR\config.json");

                // Download hello job output asset.
                DownloadAsset(asset, @"C:\supportFiles\OCR\Output");
            }

            static IAsset RunOCRJob(string inputMediaFilePath, string configurationFile)
            {
                // Create an asset and upload hello input media file toostorage.
                IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
                    "My OCR Input Asset",
                    AssetCreationOptions.None);

                // Declare a new job.
                IJob job = _context.Jobs.Create("My OCR Job");

                // Get a reference tooAzure Media OCR.
                string MediaProcessorName = "Azure Media OCR";

                var processor = GetLatestMediaProcessorByName(MediaProcessorName);

                // Read configuration from hello specified file.
                string configuration = File.ReadAllText(configurationFile);

                // Create a task with hello encoding details, using a string preset.
                ITask task = job.Tasks.AddNew("My OCR Task",
                    processor,
                    configuration,
                    TaskOptions.None);

                // Specify hello input asset.
                task.InputAssets.Add(asset);

                // Add an output asset toocontain hello results of hello job.
                task.OutputAssets.AddNew("My OCR Output Asset", AssetCreationOptions.None);

                // Use hello following event handler toocheck job progress.  
                job.StateChanged += new EventHandler<JobStateChangedEventArgs>(StateChanged);

                // Launch hello job.
                job.Submit();

                // Check job execution and wait for job toofinish.
                Task progressJobTask = job.GetExecutionProgressTask(CancellationToken.None);

                progressJobTask.Wait();

                // If job state is Error, hello event handling
                // method for job progress should log errors.  Here we check
                // for error state and exit if needed.
                if (job.State == JobState.Error)
                {
                    ErrorDetail error = job.Tasks.First().ErrorDetails.First();
                    Console.WriteLine(string.Format("Error: {0}. {1}",
                                                    error.Code,
                                                    error.Message));
                    return null;
                }

                return job.OutputMediaAssets[0];
            }

            static IAsset CreateAssetAndUploadSingleFile(string filePath, string assetName, AssetCreationOptions options)
            {
                IAsset asset = _context.Assets.Create(assetName, options);

                var assetFile = asset.AssetFiles.Create(Path.GetFileName(filePath));
                assetFile.Upload(filePath);

                return asset;
            }

            static void DownloadAsset(IAsset asset, string outputDirectory)
            {
                foreach (IAssetFile file in asset.AssetFiles)
                {
                    file.Download(Path.Combine(outputDirectory, file.Name));
                }
            }

            static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
            {
                var processor = _context.MediaProcessors
                    .Where(p => p.Name == mediaProcessorName)
                    .ToList()
                    .OrderBy(p => new Version(p.Version))
                    .LastOrDefault();

                if (processor == null)
                    throw new ArgumentException(string.Format("Unknown media processor",
                                                               mediaProcessorName));

                return processor;
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

        }
    }

## <a name="media-services-learning-paths"></a>Percorsi di apprendimento di Servizi multimediali
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornire commenti e suggerimenti
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a>Collegamenti correlati
[Panoramica di Analisi servizi multimediali di Azure](media-services-analytics-overview.md)

