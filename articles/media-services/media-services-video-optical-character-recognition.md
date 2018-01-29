---
title: Digitalizzare il testo con il riconoscimento ottico dei caratteri (OCR) con Analisi Servizi multimediali di Azure | Microsoft Docs
description: "Il riconoscimento ottico dei caratteri (OCR) di Analisi servizi multimediali di Azure consente di convertire il contenuto di testo dei file video in testo digitale modificabile e sui cui è possibile eseguire ricerche.  Ciò consente di automatizzare l'estrazione di metadati importanti dal segnale video del contenuto multimediale."
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
ms.date: 12/09/2017
ms.author: juliako
ms.openlocfilehash: 739e80633f828e8c14f024dc22971e7d8858cf78
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/11/2017
---
# <a name="use-azure-media-analytics-to-convert-text-content-in-video-files-into-digital-text"></a>Usare Analisi Servizi multimediali di Azure per convertire il contenuto di testo dei file video in testo digitale
## <a name="overview"></a>Panoramica
Se è necessario estrarre il contenuto di testo da file video e generare un testo digitale modificabile e in cui sia possibile eseguire ricerche, usare il riconoscimento ottico dei caratteri (OCR) di Analisi servizi multimediali di Azure. Questo processore di contenuti multimediali di Azure rileva il contenuto di testo nei file video e genera file di testo pronti per l'uso. OCR consente di automatizzare l'estrazione di metadati importanti dal segnale video del contenuto multimediale.

Se usato in combinazione con un motore di ricerca, è possibile indicizzare facilmente i file multimediali dal testo e migliorare la scoperta dei contenuti. Questa funzione risulta molto utile per i video che contengono un porzione importante di testo, ad esempio una registrazione video o l'acquisizione della schermata di una presentazione. Il processore di contenuti multimediali OCR di Azure è ottimizzato per il testo digitale.

Il processore di contenuti multimediali **Azure Media OCR** è attualmente disponibile in anteprima.

In questo articolo fornisce informazioni dettagliate sulle **Azure Media OCR** e viene illustrato come usarlo con Media Services SDK per .NET. Per ulteriori informazioni ed esempi, vedere [questo blog](https://azure.microsoft.com/blog/announcing-video-ocr-public-preview-new-config/).

## <a name="ocr-input-files"></a>File di input OCR
File video. Attualmente sono supportati i formati seguenti: MP4, MOV e WMV.

## <a name="task-configuration"></a>Configurazione delle attività
Configurazione delle attività (set di impostazioni). Quando si crea un'attività con **Azure Media OCR**, è necessario specificare un set di impostazioni di configurazione tramite JSON o XML. 

>[!NOTE]
>Il motore OCR accetta solo un'area dell'immagine con un minimo di 40 pixel e un massimo di 32.000 pixel come input valido sia in altezza che in larghezza.
>

### <a name="attribute-descriptions"></a>Descrizioni degli attributi
| Nome attributo | DESCRIZIONE |
| --- | --- |
|AdvancedOutput| Se si imposta AdvancedOutput su true, l'output JSON conterrà dati posizionali per ogni singola parola (oltre alle aree e le frasi). Se non si intende visualizzare i dettagli, impostare il flag su false. Il valore predefinito è False. Per altre informazioni, vedere [questo blog](https://azure.microsoft.com/blog/azure-media-ocr-simplified-output/).|
| Linguaggio |(Facoltativo) Descrive la lingua del testo da cercare. Uno dei seguenti: AutoDetect (default), Arabic, ChineseSimplified, ChineseTraditional, Czech, Danish, Dutch, English, Finnish, French, German, Greek, Hungarian, Italian, Japanese, Korean, Norwegian, Polish, Portuguese, Romanian, Russian, SerbianCyrillic, SerbianLatin, Slovak, Spanish, Swedish, Turkish. |
| TextOrientation |(Facoltativo) Descrive l'orientamento del testo da cercare.  "Left" significa che la parte superiore di tutte le lettere è rivolta verso sinistra.  Il testo predefinito (simile a quello di un libro) può essere orientato come "Up".  Uno dei seguenti: AutoDetect (default), Up, Right, Down, Left. |
| TimeInterval |(Facoltativo) Descrive la frequenza di campionamento.  Il valore predefinito è ogni 1/2 secondo.<br/>Formato JSON: HH:mm:ss.SSS (impostazione predefinita 00:00:00.500)<br/>Formato XML – durata primitivi W3C XSD (predefinito PT0.5) |
| DetectRegions |(Facoltativo) Una matrice di oggetti DetectRegion che specifica le aree del fotogramma video in cui rilevare il testo.<br/>Un oggetto DetectRegion è costituito dai quattro valori interi seguenti:<br/>Left: pixel dal margine sinistro<br/>Top: pixel dal margine superiore<br/>Width: larghezza dell'area in pixel<br/>Height: altezza dell'area in pixel |

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
L'output del processore multimediale OCR è un file JSON.

### <a name="elements-of-the-output-json-file"></a>Elementi del file di output JSON
L'output OCR del video include dati con segmentazione temporale sui caratteri del video.  È possibile usare gli attributi, la lingua o l'orientamento per concentrarsi esattamente sulle parole che si desidera analizzare. 

L'output contiene gli attributi seguenti:

| Elemento | DESCRIZIONE |
| --- | --- |
| Scala cronologica |"Scatti" al secondo del video |
| Offset |Differenza di orario dei timestamp Nella versione 1.0 delle API Video, questo valore è sempre 0. |
| Frequenza fotogrammi |Fotogrammi al secondo del video |
| width |Larghezza del video in pixel |
| height |Altezza del video in pixel |
| Frammenti |Matrice di porzioni temporali di video in cui i metadati sono suddivisi in blocchi |
| start |Ora di inizio di un frammento in "scatti" |
| duration |Lunghezza di un frammento in "scatti" |
| interval |Intervallo di ogni evento all'interno del frammento specificato |
| events |Matrice contenente le aree |
| region |Oggetto che rappresenta le parole o le frasi rilevate |
| Linguaggio |Lingua del testo rilevato all'interno di un'area |
| orientation |Orientamento del testo rilevato all'interno di un'area |
| lines |Matrice di righe del testo rilevato all'interno di un'area |
| text |Il testo effettivo |

### <a name="json-output-example"></a>Esempio di output JSON
Il seguente output contiene le informazioni generali del video e numerosi frammenti video. In ogni frammento video, contiene ogni area, che viene rilevato da MP OCR con la lingua e il relativo orientamento di testo. L'area contiene anche ogni riga di word in quest'area con il testo della riga, la posizione della riga e tutte le informazioni di word (il contenuto di word, posizione e confidenza) in questa riga. Di seguito è riportato un esempio, contenente anche alcuni commenti sulla riga.

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
                "interval": 90000,  // the time information about this fragment
                "events": [
                    [
                       { 
                            "region": { // the detected region array in this fragment 
                                "language": "English",  // region language
                                "orientation": "Up",  // text orientation
                                "lines": [  // line information array in this region, including the text and the position
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

Il programma seguente illustra come:

1. Creare un asset e caricare un file multimediale nell'asset.
2. Creare un processo con un file di configurazione/set di impostazioni OCR.
3. Scaricare i file JSON di output. 
   
#### <a name="create-and-configure-a-visual-studio-project"></a>Creare e configurare un progetto di Visual Studio

Configurare l'ambiente di sviluppo e popolare il file app.config con le informazioni di connessione, come descritto in [Sviluppo di applicazioni di Servizi multimediali con .NET](media-services-dotnet-how-to-use.md). 

#### <a name="example"></a>Esempio

```
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
        // Read values from the App.config file.
        private static readonly string _AADTenantDomain =
            ConfigurationManager.AppSettings["AMSAADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
            ConfigurationManager.AppSettings["AMSRESTAPIEndpoint"];
        private static readonly string _AMSClientId =
            ConfigurationManager.AppSettings["AMSClientId"];
        private static readonly string _AMSClientSecret =
            ConfigurationManager.AppSettings["AMSClientSecret"];

        // Field for service context.
        private static CloudMediaContext _context = null;

        static void Main(string[] args)
        {
            AzureAdTokenCredentials tokenCredentials =
                new AzureAdTokenCredentials(_AADTenantDomain,
                    new AzureAdClientSymmetricKey(_AMSClientId, _AMSClientSecret),
                    AzureEnvironments.AzureCloudEnvironment);

            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

            // Run the OCR job.
            var asset = RunOCRJob(@"C:\supportFiles\OCR\presentation.mp4",
                                        @"C:\supportFiles\OCR\config.json");

            // Download the job output asset.
            DownloadAsset(asset, @"C:\supportFiles\OCR\Output");
        }

        static IAsset RunOCRJob(string inputMediaFilePath, string configurationFile)
        {
            // Create an asset and upload the input media file to storage.
            IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
                "My OCR Input Asset",
                AssetCreationOptions.None);

            // Declare a new job.
            IJob job = _context.Jobs.Create("My OCR Job");

            // Get a reference to Azure Media OCR.
            string MediaProcessorName = "Azure Media OCR";

            var processor = GetLatestMediaProcessorByName(MediaProcessorName);

            // Read configuration from the specified file.
            string configuration = File.ReadAllText(configurationFile);

            // Create a task with the encoding details, using a string preset.
            ITask task = job.Tasks.AddNew("My OCR Task",
                processor,
                configuration,
                TaskOptions.None);

            // Specify the input asset.
            task.InputAssets.Add(asset);

            // Add an output asset to contain the results of the job.
            task.OutputAssets.AddNew("My OCR Output Asset", AssetCreationOptions.None);

            // Use the following event handler to check job progress.  
            job.StateChanged += new EventHandler<JobStateChangedEventArgs>(StateChanged);

            // Launch the job.
            job.Submit();

            // Check job execution and wait for job to finish.
            Task progressJobTask = job.GetExecutionProgressTask(CancellationToken.None);

            progressJobTask.Wait();

            // If job state is Error, the event handling
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
```

## <a name="media-services-learning-paths"></a>Percorsi di apprendimento di Servizi multimediali
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornire commenti e suggerimenti
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a>Collegamenti correlati
[Panoramica di Analisi servizi multimediali di Azure](media-services-analytics-overview.md)

