---
title: i caratteri tipografici aaaRedact con Azure Media Analitica | Documenti Microsoft
description: "In questo argomento viene illustrato come è rivolto tooredact con analitica multimediali di Azure."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 5b6d8b8c-5f4d-4fef-b3d6-dc22c6b5a0f5
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/31/2017
ms.author: juliako;
ms.openlocfilehash: 1f5688a8c6374151c526a9c702b904d8c3e46164
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="redact-faces-with-azure-media-analytics"></a>Offuscare i volti con Analisi Servizi multimediali di Azure
## <a name="overview"></a>Panoramica
**Azure Media Redactor** è un [Azure Media Analitica](media-services-analytics-overview.md) processore di contenuti multimediali (MP) che offre redazione faccia scalabile nel cloud hello. Adattamento faccia consente si toomodify video in facce tooblur ordine dei singoli utenti selezionati. È opportuno toouse hello faccia redazione servizio pubblica sicurezza e i supporti di notizie negli scenari in. Pochi minuti di riprese che contiene più caratteri tipografici possono richiedere ore tooredact manualmente, ma con questa faccia hello servizio processo di adattamento richiederà solo alcuni semplici passaggi. Per altre informazioni, vedere [questo](https://azure.microsoft.com/blog/azure-media-redactor/) blog.

In questo argomento fornisce informazioni dettagliate sulle **Azure Media Redactor** e Mostra come toouse con Media Services SDK per .NET.

Hello **Azure Media Redactor** Management Pack è attualmente in anteprima. È disponibile in tutte le aree di Azure pubbliche, nonché nei data center cinesi e del governo degli USA. Al momento questa versione di anteprima è disponibile gratuitamente. 

## <a name="face-redaction-modes"></a>Modalità per l'offuscamento dei volti
Adattamento facciale works rilevando facce in ogni frame di video e rilevamento viso hello oggetto entrambi avanti e indietro nel tempo, in modo che hello stessa persona può essere sfocatura dagli altri angoli anche. Hello il processo di adattamento automatico è molto complesso e non producono sempre 100% dell'output desiderata per questo motivo che Analitica supporti sono disponibili un paio di modi output finale di toomodify hello.

In modalità automatica tooa aggiunta, è un flusso di lavoro in due passaggi che consente di hello selezione/deserializzare-selection di facce trovate tramite un elenco di ID. Inoltre, toomake arbitrario per hello regolazioni frame MP utilizza un file di metadati in formato JSON. Il flusso di lavoro è suddiviso nelle modalità **analisi** e **offuscamento**. È possibile combinare due modalità di hello in un unico passaggio che esegue entrambe le attività in un processo. Questa modalità è detta **combinata**.

### <a name="combined-mode"></a>Modalità combinata
Questa modalità produce automaticamente un file mp4 offuscato senza alcun input manuale.

| Fase | File Name | Note |
| --- | --- | --- |
| Asset di input |foo.bar |Video in formato WMV, MOV o MP4 |
| Configurazione di input |Set di impostazioni di configurazione del processo |{'version':'1.0', 'options': {'mode':'combined'}} |
| Asset di output |foo_redacted.mp4 |Video con sfocatura applicata |

#### <a name="input-example"></a>Esempio di input:
[Guardare il video](http://ampdemo.azureedge.net/?url=http%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fed99001d-72ee-4f91-9fc0-cd530d0adbbc%2FDancing.mp4)

#### <a name="output-example"></a>Esempio di output:
[Guardare il video](http://ampdemo.azureedge.net/?url=http%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fc6608001-e5da-429b-9ec8-d69d8f3bfc79%2Fdance_redacted.mp4)

### <a name="analyze-mode"></a>Modalità analisi
Hello **analizzare** passaggio del flusso di lavoro in due passaggi hello accetta un input video e produce un file JSON di percorsi faccia e immagini jpg di ogni rilevato tipo di carattere.

| Fase | File Name | Note |
| --- | --- | --- |
| Asset di input |foo.bar |Video in formato WMV, MPV o MP4 |
| Configurazione di input |Set di impostazioni di configurazione del processo |{'version':'1.0', 'options': {'mode':'analyze'}} |
| Asset di output |foo_annotations.json |Dati di annotazione delle posizioni dei volti in formato JSON, Questo può essere modificato dal hello utente toomodify hello sfocatura rettangoli di selezione. Vedere l'esempio di seguito. |
| Asset di output |foo_thumb%06d.jpg [foo_thumb000001.jpg, foo_thumb000002.jpg] |Un'immagine jpg ritagliata di ogni rilevato tipo di carattere, in cui il numero di hello indica labelId hello del carattere tipografico hello |

#### <a name="output-example"></a>Esempio di output:

    {
      "version": 1,
      "timescale": 24000,
      "offset": 0,
      "framerate": 23.976,
      "width": 1280,
      "height": 720,
      "fragments": [
        {
          "start": 0,
          "duration": 48048,
          "interval": 1001,
          "events": [
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [
              {
                "index": 13,
                "id": 1138,
                "x": 0.29537,
                "y": -0.18987,
                "width": 0.36239,
                "height": 0.80335
              },
              {
                "index": 13,
                "id": 2028,
                "x": 0.60427,
                "y": 0.16098,
                "width": 0.26958,
                "height": 0.57943
              }
            ],

    … truncated

### <a name="redact-mode"></a>Modalità offuscamento
secondo passaggio del flusso di lavoro hello di Hello accetta un numero maggiore di input che devono essere combinati in un singolo asset.

Questo include un elenco di ID tooblur video originale hello e annotazioni hello JSON. Questa modalità utilizza hello annotazioni tooapply sfocatura nel video di input hello.

Hello output di analisi hello non include video originale hello. Hello video deve toobe caricato nell'asset di input per l'attività in modalità Redact hello hello e selezionato come file primario hello.

| Fase | File Name | Note |
| --- | --- | --- |
| Asset di input |foo.bar |Video in formato WMV, MPV o MP4. Stesso video del passaggio 1. |
| Asset di input |foo_annotations.json |File di metadati delle annotazioni della prima fase, con modifiche facoltative. |
| Asset di input |foo_IDList.txt (facoltativo) |Elenco del carattere tipografico tooredact ID separati da facoltativa nuova riga. Se viene lasciato vuoto, vengono sfocati tutti i volti. |
| Configurazione di input |Set di impostazioni di configurazione del processo |{'version':'1.0', 'options': {'mode':'redact'}} |
| Asset di output |foo_redacted.mp4 |Video con sfocatura applicata in base alle annotazioni. |

#### <a name="example-output"></a>Output di esempio
Questo è l'output di hello da un IDList con un ID selezionato.

[Guardare il video](http://ampdemo.azureedge.net/?url=http%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fad6e24a2-4f9c-46ee-9fa7-bf05e20d19ac%2Fdance_redacted1.mp4)

Esempio foo_IDList.txt
 
     1
     2
     3

## <a name="blur-types"></a>Tipi di sfocature

In hello **combinata** o **Redact** modalità, sono disponibili 5 sfocatura diverse modalità, è possibile scegliere tra mediante la configurazione di input JSON hello: **bassa**, **Med**, **Elevata**, **Debug**, e **nero**. Per impostazione predefinita, viene usata **Med**.

È possibile trovare esempi di hello sfocatura tipi più avanti.

### <a name="example-json"></a>JSON di esempio:

    {'version':'1.0', 'options': {'Mode': 'Combined', 'BlurType': 'High'}}

#### <a name="low"></a>Basso

![Basso](./media/media-services-face-redaction/blur1.png)
 
#### <a name="med"></a>Med

![Med](./media/media-services-face-redaction/blur2.png)

#### <a name="high"></a>Alto

![Alto](./media/media-services-face-redaction/blur3.png)

#### <a name="debug"></a>Debug

![Debug](./media/media-services-face-redaction/blur4.png)

#### <a name="black"></a>Nero

![Nero](./media/media-services-face-redaction/blur5.png)

## <a name="elements-of-hello-output-json-file"></a>Elementi hello JSON del file di output

Hello redazione MP fornisce il rilevamento di percorso faccia ad alta precisione e rilevamento in grado di rilevare il too64 viso umana in un frame video. Volti frontali forniscono risultati ottimali hello, mentre i caratteri tipografici lato e facce di piccole dimensioni (minore o uguale a too24x24 pixel) rappresentano una sfida.

[!INCLUDE [media-services-analytics-output-json](../../includes/media-services-analytics-output-json.md)]

## <a name="net-sample-code"></a>Codice di esempio .NET

esempio Hello programma mostra come:

1. Creare un asset e caricare un file multimediale nell'asset hello.
2. Creare un processo con un'attività di adattamento faccia basata su un file di configurazione che contiene i seguenti set di impostazioni json hello. 
   
        {'version':'1.0', 'options': {'mode':'combined'}}
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

    namespace FaceRedaction
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

            // Run hello FaceRedaction job.
            var asset = RunFaceRedactionJob(@"C:\supportFiles\FaceRedaction\SomeFootage.mp4",
                        @"C:\supportFiles\FaceRedaction\config.json");

            // Download hello job output asset.
            DownloadAsset(asset, @"C:\supportFiles\FaceRedaction\Output");
        }

        static IAsset RunFaceRedactionJob(string inputMediaFilePath, string configurationFile)
        {
            // Create an asset and upload hello input media file toostorage.
            IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
            "My Face Redaction Input Asset",
            AssetCreationOptions.None);

            // Declare a new job.
            IJob job = _context.Jobs.Create("My Face Redaction Job");

            // Get a reference tooAzure Media Redactor.
            string MediaProcessorName = "Azure Media Redactor";

            var processor = GetLatestMediaProcessorByName(MediaProcessorName);

            // Read configuration from hello specified file.
            string configuration = File.ReadAllText(configurationFile);

            // Create a task with hello encoding details, using a string preset.
            ITask task = job.Tasks.AddNew("My Face Redaction Task",
            processor,
            configuration,
            TaskOptions.None);

            // Specify hello input asset.
            task.InputAssets.Add(asset);

            // Add an output asset toocontain hello results of hello job.
            task.OutputAssets.AddNew("My Face Redaction Output Asset", AssetCreationOptions.None);

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

## <a name="next-steps"></a>Passaggi successivi

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornire commenti e suggerimenti
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a>Collegamenti correlati
[Panoramica di Analisi servizi multimediali di Azure](media-services-analytics-overview.md)

[Demo di Analisi servizi multimediali di Azure](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

