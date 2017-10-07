---
title: Movimenti aaaDetect con Azure Media Analitica | Documenti Microsoft
description: Hello consente di processore (MP) rilevatore di movimento multimediali di Azure media tooefficiently si identificano le sezioni di interesse all'interno di un video in caso contrario lungo e procede senza interruzioni.
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: d144f813-1a55-442f-a895-5c4cb6d0aeae
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/31/2017
ms.author: milanga;juliako;
ms.openlocfilehash: cb431375c92222053ed2239dd4e45767524dab68
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="detect-motions-with-azure-media-analytics"></a>Rilevare i movimenti con Analisi servizi multimediali di Azure
## <a name="overview"></a>Panoramica
Hello **rilevatore di movimento di Azure Media** Abilita processore (MP) supporti tooefficiently si identificano le sezioni di interesse all'interno di un video in caso contrario lungo e procede senza interruzioni. Rilevamento del movimento utilizzabile in camera statico riprese tooidentify sezioni del video hello in cui viene effettuato lo spostamento. Genera un file JSON che contiene i metadati con i timestamp e hello delimitazione area in cui si è verificato l'evento hello.

Mirata feed video di sicurezza, questa tecnologia è in grado di toocategorize movimento in eventi rilevanti e falsi positivi, ad esempio shadows e modifiche di illuminazione. Ciò consente gli avvisi di sicurezza toogenerate dai feed di fotocamera senza viene posta indesiderata con gli eventi non rilevanti infiniti, pur essendo momenti tooextract in grado di interesse da video sorveglianza estremamente lunghi.

Hello **rilevatore di movimento di Azure Media** Management Pack è attualmente in anteprima.

In questo argomento fornisce informazioni dettagliate sulle **rilevatore di movimento di Azure Media** e Mostra come toouse con Media Services SDK per .NET

## <a name="motion-detector-input-files"></a>File di input di Rilevatore di movimento
File video. Attualmente, è supportato i seguenti formati hello: MOV o MP4 e WMV.

## <a name="task-configuration-preset"></a>Configurazione delle attività (set di impostazioni)
Quando si crea un'attività con **Azure Media Motion Detector**è necessario specificare un set di impostazioni di configurazione. 

### <a name="parameters"></a>parameters
È possibile utilizzare hello seguenti parametri:

| Nome | Opzioni | Descrizione | Default |
| --- | --- | --- | --- |
| sensitivityLevel |Stringa:'low', 'medium', 'high' |Imposta livello di sensibilità hello in quali corse viene segnalato. Modificare questa quantità tooadjust di falsi positivi. |'medium' |
| frameSamplingValue |Intero positivo |Imposta la frequenza di hello in cui viene eseguito il algoritmo. 1 indica a ogni fotogramma, 2 a un fotogramma su due e così via. |1 |
| detectLightChange |Booleano: 'true', 'false' |Imposta se vengono segnalate chiare modifiche nei risultati di hello |'False' |
| mergeTimeThreshold |Xs-time: Hh:mm:ss<br/>Esempio: 00:00:03 |Specifica l'intervallo di tempo hello tra gli eventi di movimento in cui verranno combinati e segnalati come 1 2 eventi. |00:00:00 |
| detectionZones |Matrice di zone di rilevamento:<br/>- La zona di rilevamento è una matrice di 3 o più punti<br/>-Punto è un x e y coordinate da too1 0. |Descrive l'elenco di hello di rilevamento poligonale zone toobe utilizzato.<br/>Risultati verranno visualizzati con le zone hello come ID, con un primo being 'id' hello: 0 |Singola zona che copre l'intera cornice hello. |

### <a name="json-example"></a>Esempio di JSON
    {
      "version": "1.0",
      "options": {
        "sensitivityLevel": "medium",
        "frameSamplingValue": 1,
        "detectLightChange": "False",
        "mergeTimeThreshold":
        "00:00:02",
        "detectionZones": [
          [
            {"x": 0, "y": 0},
            {"x": 0.5, "y": 0},
            {"x": 0, "y": 1}
           ],
          [
            {"x": 0.3, "y": 0.3},
            {"x": 0.55, "y": 0.3},
            {"x": 0.8, "y": 0.3},
            {"x": 0.8, "y": 0.55},
            {"x": 0.8, "y": 0.8},
            {"x": 0.55, "y": 0.8},
            {"x": 0.3, "y": 0.8},
            {"x": 0.3, "y": 0.55}
          ]
        ]
      }
    }


## <a name="motion-detector-output-files"></a>File di output di Rilevatore di movimento
Un processo di rilevamento del movimento restituirà un file JSON in asset di output di hello che descrive gli avvisi di movimento hello e le relative categorie all'interno di hello video. file Hello conterrà informazioni hello ora e la durata di movimento in video hello rilevati.

API rilevamento movimento Hello fornisce indicatori quando sono presenti oggetti in movimento in uno sfondo fixed video (ad esempio, un sistema di sorveglianza video). Hello rilevatore di movimento è sottoposto a training tooreduce falsi allarmi, ad esempio modifiche di ombreggiatura e illuminazione. Limitazioni di algoritmi hello correnti includono video visione di notte, oggetti semi-trasparenti e oggetti di piccole dimensioni.

### <a id="output_elements"></a>Elementi hello JSON del file di output
> [!NOTE]
> Nella versione più recente di hello, formato JSON di Output di hello è stato modificato e potrebbe rappresentare una modifica di rilievo per alcuni clienti.
> 
> 

Hello nella tabella seguente vengono descritti gli elementi hello JSON del file di output.

| Elemento | Descrizione |
| --- | --- |
| Versione |Si riferisce toohello versione di hello API Video. la versione corrente di Hello è 2. |
| Scala cronologica |"Tick" al secondo del video hello. |
| Offset |offset ora Hello per i timestamp nel "tick". Nella versione 1.0 delle API Video, questo valore è sempre 0. Negli scenari futuri supportati questo valore potrebbe cambiare. |
| Frequenza fotogrammi |Fotogrammi al secondo di hello video. |
| Larghezza, altezza |Si riferisce toohello larghezza e altezza di hello video in pixel. |
| Inizia |Hello avviare timestamp in "tick". |
| Duration |lunghezza Hello dell'evento hello, in "tick". |
| Interval |intervallo di Hello di ogni voce nell'evento hello, "tick". |
| Events |Ogni frammento di evento contiene movimento hello rilevati entro tale periodo di tempo. |
| Tipo |Nella versione corrente di hello, è sempre '2' per il movimento generico. Questa etichetta offre movimento in Video API hello flessibilità toocategorize nelle versioni future. |
| RegionID |Come spiegato in precedenza, in questa versione questo valore è sempre 0. Questa etichetta offre API Video hello flessibilità toofind il movimento in diverse aree geografiche nelle versioni future. |
| Regioni |Si riferisce area toohello nel video in cui si è interessati movimento. <br/><br/>-"id" rappresenta l'area dell'area hello: in questa versione è presente uno solo, ID 0. <br/>-"type" rappresenta la forma hello dell'area di hello è rilevante per il movimento. Sono attualmente supportati "rectangle" e "polygon".<br/> Se è stato specificato "rettangolo", area hello ha dimensioni x, Y, larghezza e altezza. Hello X e Y coordinate rappresentano coordinate XY superiore sinistro di hello dell'area di hello in una scala normalizzata di too1.0 0,0. altezza e larghezza hello rappresentano dimensione hello dell'area di hello in una scala normalizzata di too1.0 0,0. Nella versione corrente di hello, X, Y, larghezza e altezza sono sempre pari a 0, 0 e 1, 1. <br/>Se si specifica "poligono", l'area hello ha dimensioni in punti. <br/> |
| Frammenti |metadati Hello sono suddivise denominate frammenti di segmenti diversi. Ogni frammento contiene un inizio, una durata, un numero di intervallo e uno o più eventi. Un frammento privo di eventi significa che non è stato rilevato alcun movimento in corrispondenza dell'ora di inizio e della durata. |
| Parentesi quadre [] |Ogni parentesi rappresenta un intervallo nell'evento hello. Le parentesi vuote in un intervallo indicano che è non stato rilevato alcun movimento. |
| locations |Questa nuova voce nell'elenco eventi è indicato il percorso di hello in cui si è verificato il movimento hello. Questo è più specifico zone hello. |

Hello seguito è riportato un esempio di output JSON

    {
      "version": 2,
      "timescale": 23976,
      "offset": 0,
      "framerate": 24,
      "width": 1280,
      "height": 720,
      "regions": [
        {
          "id": 0,
          "type": "polygon",
          "points": [{'x': 0, 'y': 0},
            {'x': 0.5, 'y': 0},
            {'x': 0, 'y': 1}]
        }
      ],
      "fragments": [
        {
          "start": 0,
          "duration": 226765
        },
        {
          "start": 226765,
          "duration": 47952,
          "interval": 999,
          "events": [
            [
              {
                "type": 2,
                "typeName": "motion",
                "locations": [
                  {
                    "x": 0.004184,
                    "y": 0.007463,
                    "width": 0.991667,
                    "height": 0.985185
                  }
                ],
                "regionId": 0
              }
            ],

    …
## <a name="limitations"></a>Limitazioni
* formati video input Hello supportato includono MP4, MOV e WMV.
* Il rilevamento di movimento è ottimizzato per i video a sfondo fisso. algoritmo di Hello è incentrata sulla riduzione falsi allarmi, ad esempio, le modifiche di illuminazione e ombreggiature.
* Non è possibile rilevare alcuni movimento a causa di problemi di tootechnical; ad esempio video visione di notte, oggetti semi-trasparenti e oggetti di piccole dimensioni.

## <a name="net-sample-code"></a>Codice di esempio .NET

esempio Hello programma mostra come:

1. Creare un asset e caricare un file multimediale nell'asset hello.
2. Creare un processo con un'attività di rilevamento movimento in video in base a un file di configurazione che contiene i seguenti set di impostazioni json hello. 
   
        {
          "Version": "1.0",
          "Options": {
            "SensitivityLevel": "medium",
            "FrameSamplingValue": 1,
            "DetectLightChange": "False",
            "MergeTimeThreshold":
            "00:00:02",
            "DetectionZones": [
              [
                {"x": 0, "y": 0},
                {"x": 0.5, "y": 0},
                {"x": 0, "y": 1}
               ],
              [
                {"x": 0.3, "y": 0.3},
                {"x": 0.55, "y": 0.3},
                {"x": 0.8, "y": 0.3},
                {"x": 0.8, "y": 0.55},
                {"x": 0.8, "y": 0.8},
                {"x": 0.55, "y": 0.8},
                {"x": 0.3, "y": 0.8},
                {"x": 0.3, "y": 0.55}
              ]
            ]
          }
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

    namespace VideoMotionDetection
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

                // Run hello VideoMotionDetection job.
                var asset = RunVideoMotionDetectionJob(@"C:\supportFiles\VideoMotionDetection\BigBuckBunny.mp4",
                                            @"C:\supportFiles\VideoMotionDetection\config.json");

                // Download hello job output asset.
                DownloadAsset(asset, @"C:\supportFiles\VideoMotionDetection\Output");
            }

            static IAsset RunVideoMotionDetectionJob(string inputMediaFilePath, string configurationFile)
            {
                // Create an asset and upload hello input media file toostorage.
                IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
                    "My Video Motion Detection Input Asset",
                    AssetCreationOptions.None);

                // Declare a new job.
                IJob job = _context.Jobs.Create("My Video Motion Detection Job");

                // Get a reference tooAzure Media Motion Detector.
                string MediaProcessorName = "Azure Media Motion Detector";

                var processor = GetLatestMediaProcessorByName(MediaProcessorName);

                // Read configuration from hello specified file.
                string configuration = File.ReadAllText(configurationFile);

                // Create a task with hello encoding details, using a string preset.
                ITask task = job.Tasks.AddNew("My Video Motion Detection Task",
                    processor,
                    configuration,
                    TaskOptions.None);

                // Specify hello input asset.
                task.InputAssets.Add(asset);

                // Add an output asset toocontain hello results of hello job.
                task.OutputAssets.AddNew("My Video Motion Detectoion Output Asset", AssetCreationOptions.None);

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
[Blog di Azure Media Motion Detector](https://azure.microsoft.com/blog/motion-detector-update/)

[Panoramica di Analisi servizi multimediali di Azure](media-services-analytics-overview.md)

[Demo di Analisi servizi multimediali di Azure](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

