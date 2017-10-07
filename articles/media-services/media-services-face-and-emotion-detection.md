---
title: aaaDetect faccia ed emozioni con Azure Media Analitica | Documenti Microsoft
description: "In questo argomento viene illustrato come è rivolto toodetect ed emozioni con Azure Media Analitica."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 5ca4692c-23f1-451d-9d82-cbc8bf0fd707
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/18/2017
ms.author: milanga;juliako;
ms.openlocfilehash: f58d81d82dde08a694cdb4d92c6bab6a40a9c157
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="detect-face-and-emotion-with-azure-media-analytics"></a>Rilevare volti ed emozioni con Analisi servizi multimediali di Azure
## <a name="overview"></a>Panoramica
Hello **Azure Media faccia Rilevatore** processore di contenuti multimediali (MP) consente di toocount, i movimenti di avanzamento e anche la partecipazione di destinatari misuratore e reazione tramite facciale. Questo servizio contiene due funzionalità: 

* **Rilevamento volti**
  
    Il Rilevamento volti rileva e monitora i volti umani all'interno di un video. Più caratteri tipografici possono essere rilevati e successivamente essere rilevate man mano che vengono spostati, con hello ora e il percorso dei metadati restituiti in un file JSON. Durante il rilevamento, verrà eseguito un tentativo toogive un toohello ID coerenza stesso faccia mentre persona hello è spostamento sullo schermo, anche se è nascosto o lasciare brevemente il frame di hello.
  
  > [!NOTE]
  > Questo servizio non esegue il riconoscimento facciale. Persona che lascia frame hello o diventa nascosto per troppo tempo verrà assegnato un nuovo ID quando viene restituita.
  > 
  > 
* **Rilevamento emozioni**
  
    Rilevamento emozioni è un componente facoltativo di hello processore di contenuti multimediali di rilevamento viso restituisce analisi su più attributi affettivi da facce hello rilevate, tra cui "Happiness", sadness, paura, anger e altro ancora. 

Hello **Azure Media faccia Rilevatore** Management Pack è attualmente in anteprima.

In questo argomento fornisce informazioni dettagliate sulle **Azure Media faccia Rilevatore** e Mostra come toouse con Media Services SDK per .NET.

## <a name="face-detector-input-files"></a>File di input di Rilevamento volti
File video. Attualmente, è supportato i seguenti formati hello: MOV o MP4 e WMV.

## <a name="face-detector-output-files"></a>File di output di Rilevamento volti
API di rilevamento e il rilevamento di faccia Hello fornisce il rilevamento di percorso faccia ad alta precisione e il rilevamento in grado di rilevare il too64 viso umana in un video. Volti frontali forniscono risultati ottimali hello, mentre i caratteri tipografici lato e facce di piccole dimensioni (minore o uguale a too24x24 pixel) potrebbe non essere accurata.

Hello facce rilevate e di rilevamento vengono restituite con le coordinate (sinistro, superiore, larghezza e altezza) che indica la posizione hello di facce nell'immagine di hello in pixel, nonché di un viso ID numerico che indica il rilevamento di tale persona hello. Numeri di ID tipo di carattere sono tooreset soggetta a circostanze quando frontale hello viene smarrito o sovrapposta nel frame hello, risultante in alcune persone più ID di assegnazione.

## <a id="output_elements"></a>Elementi hello JSON del file di output

[!INCLUDE [media-services-analytics-output-json](../../includes/media-services-analytics-output-json.md)]

Rilevatore faccia utilizza tecniche di frammentazione (in cui i metadati di hello possono essere suddiviso in blocchi basati sul tempo ed è possibile scaricare solo gli elementi necessari) e la segmentazione (in cui gli eventi di hello sono suddivise in caso di ricevono troppo grande). Alcune semplici calcoli consentono di trasformare i dati di hello. Se ad esempio un evento è iniziato in corrispondenza di 6300 (scatti), con una scala cronologica di 2997 (scatti al secondo) e una frequenza di fotogrammi di 29,97 (fotogrammi al secondo):

* Inizio/Scala cronologica = 2,1 secondi
* Secondi x frequenza di fotogrammi = 63 fotogrammi

## <a name="face-detection-input-and-output-example"></a>Esempio di input e output di rilevamento volti
### <a name="input-video"></a>Video di input
[Video di input](http://ampdemo.azureedge.net/azuremediaplayer.html?url=https%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fc8834d9f-0b49-4b38-bcaf-ece2746f1972%2FMicrosoft%20Convergence%202015%20%20Keynote%20Highlights.ism%2Fmanifest&amp;autoplay=false)

### <a name="task-configuration-preset"></a>Configurazione delle attività (set di impostazioni)
Quando si crea un'attività con **Rilevamento multimediale volti di Azure**, è necessario specificare un set di impostazioni di configurazione. Hello seguente set di impostazioni di configurazione è solo per il rilevamento di tipo di carattere.

    {
      "version":"1.0",
      "options":{
          "TrackingMode": "Fast"
      }
    }

#### <a name="attribute-descriptions"></a>Descrizioni degli attributi
| Nome attributo | Descrizione |
| --- | --- |
| Mode |Fast: velocità di elaborazione elevata, ma meno accurata (impostazione predefinita).|

### <a name="json-output"></a>Output JSON
esempio dell'output JSON seguente Hello è stato troncato.

    {
    "version": 1,
    "timescale": 30000,
    "offset": 0,
    "framerate": 29.97,
    "width": 1280,
    "height": 720,
    "fragments": [
        {
        "start": 0,
        "duration": 60060
        },
        {
        "start": 60060,
        "duration": 60060,
        "interval": 1001,
        "events": [
            [
            {
                "id": 0,
                "x": 0.519531,
                "y": 0.180556,
                "width": 0.0867188,
                "height": 0.154167
            }
            ],
            [
            {
                "id": 0,
                "x": 0.517969,
                "y": 0.181944,
                "width": 0.0867188,
                "height": 0.154167
            }
            ],
            [
            {
                "id": 0,
                "x": 0.517187,
                "y": 0.183333,
                "width": 0.0851562,
                "height": 0.151389
            }
            ],

        . . . 

## <a name="emotion-detection-input-and-output-example"></a>Esempio di input e output di Rilevamento emozioni
### <a name="input-video"></a>Video di input
[Video di input](http://ampdemo.azureedge.net/azuremediaplayer.html?url=https%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fc8834d9f-0b49-4b38-bcaf-ece2746f1972%2FMicrosoft%20Convergence%202015%20%20Keynote%20Highlights.ism%2Fmanifest&amp;autoplay=false)

### <a name="task-configuration-preset"></a>Configurazione delle attività (set di impostazioni)
Quando si crea un'attività con **Rilevamento multimediale volti di Azure**, è necessario specificare un set di impostazioni di configurazione. Hello seguente set di impostazioni di configurazione specifica toocreate che JSON basato sul rilevamento emozioni hello.

    {
      "version": "1.0",
      "options": {
        "aggregateEmotionWindowMs": "987",
        "mode": "aggregateEmotion",
        "aggregateEmotionIntervalMs": "342"
      }
    }


#### <a name="attribute-descriptions"></a>Descrizioni degli attributi
| Nome attributo | Descrizione |
| --- | --- |
| Mode |Faces: solo rilevamento viso.<br/>PerFaceEmotion: restituisce un'emozione in modo indipendente per ogni rilevamento viso.<br/>AggregateEmotion: restituzione dei valori medi delle emozioni per tutti i volti nel fotogramma. |
| AggregateEmotionWindowMs |Va usato se è selezionata la modalità AggregateEmotion. Specifica il periodo di hello del video tooproduce usato ogni risultato aggregato, in millisecondi. |
| AggregateEmotionIntervalMs |Va usato se è selezionata la modalità AggregateEmotion. Specifica con quale aggregazione tooproduce frequenza risultati. |

#### <a name="aggregate-defaults"></a>Impostazioni predefinite degli aggregati
Di seguito sono consigliati i valori per la finestra di aggregazione hello e le impostazioni dell'intervallo. Il valore di AggregateEmotionWindowMs non deve essere maggiore del valore di AggregateEmotionIntervalMs.

|| Impostazioni predefinite | Min(s) | Max(s) |
|--- | --- | --- | --- |
| AggregateEmotionWindowMs |0,5 |2 |0,25|
| AggregateEmotionIntervalMs |0,5 |1 |0,25|

### <a name="json-output"></a>Output JSON
Output JSON per l'emozione aggregata (troncato):

    {
     "version": 1,
     "timescale": 30000,
     "offset": 0,
     "framerate": 29.97,
     "width": 1280,
     "height": 720,
     "fragments": [
       {
         "start": 0,
         "duration": 60060,
         "interval": 15015,
         "events": [
           [
             {
               "windowFaceDistribution": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               },
               "windowMeanScores": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               }
             }
           ],
           [
             {
               "windowFaceDistribution": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               },
               "windowMeanScores": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               }
             }
           ],
           [
             {
               "windowFaceDistribution": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               },
               "windowMeanScores": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               }
             }
           ],
           [
             {
               "windowFaceDistribution": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               },
               "windowMeanScores": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               }
             }
           ]
         ]
       },
       {
         "start": 60060,
         "duration": 60060,
         "interval": 15015,
         "events": [
           [
             {
               "windowFaceDistribution": {
                 "neutral": 1,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               },
               "windowMeanScores": {
                 "neutral": 0.688541,
                 "happiness": 0.0586323,
                 "surprise": 0.227184,
                 "sadness": 0.00945675,
                 "anger": 0.00592107,
                 "disgust": 0.00154993,
                 "fear": 0.00450447,
                 "contempt": 0.0042109
               }
             }
           ],
           [
             {
               "windowFaceDistribution": {
                 "neutral": 1,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,

## <a name="limitations"></a>Limitazioni
* formati video input Hello supportato includono MP4, MOV e WMV.
* intervallo di dimensioni faccia rilevabili Hello è too2048x2048 24 x 24 pixel. i caratteri tipografici Hello da questo intervallo non venga rilevati.
* Per ogni video, numero massimo di hello di facce restituito è 64.
* Non è possibile rilevare alcuni volti a causa di problemi di tootechnical; ad esempio grandi faccia angoli (head-posa) e occlusione di grandi dimensioni. Volti frontali e di prossimità anteriore avere risultati migliori hello.

## <a name="net-sample-code"></a>Codice di esempio .NET

esempio Hello programma mostra come:

1. Creare un asset e caricare un file multimediale nell'asset hello.
2. Creare un processo con un'attività di rilevamento viso in base a un file di configurazione che contiene i seguenti set di impostazioni json hello. 
   
        {
            "version": "1.0"
        }
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

    namespace FaceDetection
    {
        class Program
        {
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

                // Run hello FaceDetection job.
                var asset = RunFaceDetectionJob(@"C:\supportFiles\FaceDetection\BigBuckBunny.mp4",
                                            @"C:\supportFiles\FaceDetection\config.json");

                // Download hello job output asset.
                DownloadAsset(asset, @"C:\supportFiles\FaceDetection\Output");
            }

            static IAsset RunFaceDetectionJob(string inputMediaFilePath, string configurationFile)
            {
                // Create an asset and upload hello input media file toostorage.
                IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
                    "My Face Detection Input Asset",
                    AssetCreationOptions.None);

                // Declare a new job.
                IJob job = _context.Jobs.Create("My Face Detection Job");

                // Get a reference tooAzure Media Face Detector.
                string MediaProcessorName = "Azure Media Face Detector";

                var processor = GetLatestMediaProcessorByName(MediaProcessorName);

                // Read configuration from hello specified file.
                string configuration = File.ReadAllText(configurationFile);

                // Create a task with hello encoding details, using a string preset.
                ITask task = job.Tasks.AddNew("My Face Detection Task",
                    processor,
                    configuration,
                    TaskOptions.None);

                // Specify hello input asset.
                task.InputAssets.Add(asset);

                // Add an output asset toocontain hello results of hello job.
                task.OutputAssets.AddNew("My Face Detectoion Output Asset", AssetCreationOptions.None);

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

[Demo di Analisi servizi multimediali di Azure](http://amslabs.azurewebsites.net/demos/Analytics.html)

