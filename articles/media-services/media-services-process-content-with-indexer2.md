---
title: File multimediali con Azure Media Indexer 2 anteprima aaaIndexing | Documenti Microsoft
description: Azure Media Indexer consente toomake contenuto dei file multimediali ricercabili e toogenerate una trascrizione full-text per sottotitoli codificati e parole chiave. In questo argomento viene illustrato come visualizzare in anteprima toouse Media Indexer 2.
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 85d25525-a498-44eb-ae3a-2ca5ceb8e53d
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/31/2017
ms.author: adsolank;juliako;
ms.openlocfilehash: f83fa0db58b828ffa29933d68ce108b4906dcd78
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="indexing-media-files-with-azure-media-indexer-2-preview"></a>Indicizzazione dei file multimediali con Azure Media Indexer 2 Preview
## <a name="overview"></a>Panoramica
Hello **anteprima di Azure Media Indexer 2** processore di contenuti multimediali (MP) consente di file multimediali toomake e ricerche di contenuto, nonché generare tracce sottotitoli codificate chiuse. Toohello confrontata la versione precedente di [Azure Media Indexer](media-services-index-content.md), **anteprima di Azure Media Indexer 2** consente di eseguire un'indicizzazione più rapida e offre un più ampio supporto lingua. Le lingue supportate includono l'italiano, l'inglese, il francese, il tedesco, lo spagnolo, il portoghese, il giapponese, il cinese, mandarino semplificato, e l'arabo.

Hello **anteprima di Azure Media Indexer 2** Management Pack è attualmente in anteprima.

Questo argomento viene illustrato come l'indicizzazione toocreate processi con **anteprima di Azure Media Indexer 2**.

> [!NOTE]
> si applica Hello seguenti considerazioni:
> 
> Indexer 2 non è supportato in Azure Cina e in Azure per enti pubblici.
> 
> Quando l'indicizzazione dei contenuti, assicurarsi di toouse che i file multimediali con contenuto vocale molto chiaro (senza musica, rumore, effetti o fruscio del microfono). Alcuni esempi di contenuto appropriato includono riunioni registrate, lezioni o presentazioni. Hello contenuto seguente potrebbe non essere adatto per l'indicizzazione: film, programmi televisivi, qualsiasi valore con una combinazione di audio ed effetti sonori e, registrato di scarsa qualità contenuto con rumore di fondo (fruscio).
> 
> 

In questo argomento fornisce informazioni dettagliate sulle **anteprima di Azure Media Indexer 2** e Mostra come toouse con Media Services SDK per .NET

## <a name="input-and-output-files"></a>File di input e output
### <a name="input-files"></a>File di input
File audio o video

### <a name="output-files"></a>File di output
Un processo di indicizzazione possa generare file di sottotitoli nel hello seguenti formati:  

* **SAMI**
* **TTML**
* **WebVTT**

Chiuso i file di didascalia (CC) in questi formati possono essere utilizzati toomake audio e video file toopeople accessibile con problemi uditivi.

## <a name="task-configuration-preset"></a>Configurazione delle attività (set di impostazioni)
Quando si crea un'attività di indicizzazione con **Azure Media Indexer 2 Preview**, è necessario specificare un set di impostazioni di configurazione.

Hello JSON seguente imposta i parametri disponibili.

    {
      "version":"1.0",
      "Features":
        [
           {
           "Options": {
                "Formats":["WebVtt","ttml"],
                "Language":"enUs",
                "Type":"RecoOptions"
           },
           "Type":"SpReco"
        }]
    }

## <a name="supported-languages"></a>Lingue supportate
Anteprima di Azure Media Indexer 2 supporta discorso in testo per hello seguenti linguaggi (specificando il nome di lingua hello nella configurazione dell'attività hello, il codice di 4 caratteri tra parentesi quadre, come illustrato di seguito):

* Inglese [EnUs]
* Spagnolo [EsEs]
* Cinese (mandarino, semplificato) [ZhCn]
* Francese [FrFr]
* Tedesco [DeDe]
* Italiano [ItIt]
* Portoghese [PtBr]
* Arabo (egiziano) [ArEg]
* Giapponese [JaJp]
* Russo [RuRu]
* Inglese britannico [EnGb]
* Spagnolo messicano [EsMx] 

## <a name="supported-file-types"></a>Tipi di file supportati

Per informazioni sui tipi di file supportati, vedere hello [codec/formati supportati](media-services-media-encoder-standard-formats.md#input-containerfile-formats) sezione.

## <a name="net-sample-code"></a>Codice di esempio .NET

esempio Hello programma mostra come:

1. Creare un asset e caricare un file multimediale nell'asset hello.
2. Creare un processo con un'attività di indicizzazione in base a un file di configurazione che contiene i seguenti set di impostazioni json hello.
   
        {
          "version":"1.0",
          "Features":
            [
               {
               "Options": {
                    "Formats":["WebVtt","ttml"],
                    "Language":"enUs",
                    "Type":"RecoOptions"
               },
               "Type":"SpReco"
            }]
        }
3. Scaricare i file di output di hello. 
   
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

    namespace IndexContent
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

                // Run indexing job.
                var asset = RunIndexingJob(@"C:\supportFiles\Indexer\BigBuckBunny.mp4",
                                            @"C:\supportFiles\Indexer\config.json");

                // Download hello job output asset.
                DownloadAsset(asset, @"C:\supportFiles\Indexer\Output");
            }

            static IAsset RunIndexingJob(string inputMediaFilePath, string configurationFile)
            {
                // Create an asset and upload hello input media file toostorage.
                IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
                    "My Indexing Input Asset",
                    AssetCreationOptions.None);

                // Declare a new job.
                IJob job = _context.Jobs.Create("My Indexing Job");

                // Get a reference tooAzure Media Indexer 2 Preview.
                string MediaProcessorName = "Azure Media Indexer 2 Preview";

                var processor = GetLatestMediaProcessorByName(MediaProcessorName);

                // Read configuration from hello specified file.
                string configuration = File.ReadAllText(configurationFile);

                // Create a task with hello encoding details, using a string preset.
                ITask task = job.Tasks.AddNew("My Indexing Task",
                    processor,
                    configuration,
                    TaskOptions.None);

                // Specify hello input asset toobe indexed.
                task.InputAssets.Add(asset);

                // Add an output asset toocontain hello results of hello job.
                task.OutputAssets.AddNew("My Indexing Output Asset", AssetCreationOptions.None);

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

[Demo di Analisi servizi multimediali di Azure](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

