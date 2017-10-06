---
title: "tooauto Azure Media Encoder Standard aaaUse-generare una scala di velocità in bit | Documenti Microsoft"
description: "Questo argomento viene illustrato come toouse Media codificatore Standard (MES) tooauto-generare una scala di velocità in bit in base alla risoluzione di input hello e alla velocità in bit. velocità in bit e la risoluzione di input hello mai essere superati. Ad esempio, se l'input hello è 720p 3 Mbps, l'output verrà rimangono nella migliore delle ipotesi 720p e inizierà a velocità inferiore a 3 Mbps."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 63ed95da-1b82-44b0-b8ff-eebd535bc5c7
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: juliako
ms.openlocfilehash: 5437f54ac28c42ddd4f9d1986549d6da6261c5da
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
#  <a name="use-azure-media-encoder-standard-tooauto-generate-a-bitrate-ladder"></a>Usare Azure Media Encoder Standard tooauto-generare una scala di velocità in bit

## <a name="overview"></a>Panoramica

Questo argomento viene illustrato come toouse Media codificatore Standard (MES) tooauto-generare una scala di velocità in bit (coppie di risoluzione a velocità in bit) in base alla risoluzione di input hello e alla velocità in bit. Hello predefinito generato automaticamente non supererà mai velocità in bit e la risoluzione di hello di input. Ad esempio, se l'input hello è 720p 3 Mbps, l'output verrà rimangono nella migliore delle ipotesi 720p e inizierà a velocità inferiore a 3 Mbps.

### <a name="encoding-for-streaming-only"></a>Codifica solo per lo streaming

Se si tooencode l'origine video solo per i flussi, quindi si è necessario utilizzare "Streaming adattivo" hello predefinito durante la creazione di un'attività di codifica. Quando si utilizza hello **il flusso adattivo** codificatore MES hello verrà predefinito, in modo intelligente chiudere una scala di velocità in bit. Tuttavia, non sarà in grado di toocontrol hello codifica i costi, poiché il servizio di hello determina quanti livelli toouse e la risoluzione. È possibile visualizzare esempi dei livelli di output prodotti da MES in seguito alla codifica con hello **il flusso adattivo** predefinito alla fine di hello di questo argomento. Hello output Asset conterrà i file MP4 in audio e video non sono interlacciati.

### <a name="encoding-for-streaming-and-progressive-download"></a>Codifica per streaming e download progressivo

Se si tooencode del video di origine per i flussi e i file MP4 tooproduce per il download progressivo, quindi si è necessario utilizzare "Contenuto adattivo più velocità in bit MP4" hello predefinito durante la creazione di un'attività di codifica. Quando si utilizza hello **contenuto file MP4 a velocità in bit adattiva più** preimpostato, codificatore MES hello applicherà hello stessa logica codifica, come illustrato in precedenza, ma ora asset di output di hello conterrà MP4 di file audio e video sono interleave. È possibile utilizzare uno di questi file MP4 (ad esempio, hello versione più recente a velocità in bit) come un file di download progressivo.

## <a id="encoding_with_dotnet"></a>Codifica con l’SDK .NET dei servizi multimediali

esempio di codice seguente Hello utilizza hello tooperform Media Services .NET SDK seguenti attività:

- Creare un processo di codifica.
- Ottiene un codificatore Media Encoder Standard toohello di riferimento.
- Aggiungere un processo di codifica attività toohello e specificare hello toouse **il flusso adattivo** predefinito. 
- Creare un asset di output che conterrà l'asset codificato hello.
- Aggiungere un avanzamento del processo hello toocheck gestore dell'evento.
- Inviare il processo di hello.

#### <a name="create-and-configure-a-visual-studio-project"></a>Creare e configurare un progetto di Visual Studio

Configurare l'ambiente di sviluppo e di popolare il file app. config hello con informazioni di connessione, come descritto in [lo sviluppo di servizi multimediali con .NET](media-services-dotnet-how-to-use.md). 

#### <a name="example"></a>Esempio

    using System;
    using System.Configuration;
    using System.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Threading;

    namespace AdaptiveStreamingMESPresest
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

            // Create a task
            ITask task = job.Tasks.AddNew("Media Encoder Standard encoding task",
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

## <a id="output"></a>Output

Questa sezione vengono illustrate tre esempi di livelli di output prodotti da MES in seguito alla codifica con hello **il flusso adattivo** predefinito. 

### <a name="example-1"></a>Esempio 1
L'origine con altezza "1080" e una frequenza frame "29.970" produce 6 livelli video:

|Livello|Altezza:|Larghezza|Bitrate (Kbps)|
|---|---|---|---|
|1|1080|1920|6780|
|2|720|1280|3520|
|3|540|960|2210|
|4|360|640|1150|
|5|270|480|720|
|6|180|320|380|

### <a name="example-2"></a>Esempio 2
L'origine con altezza "720" e una frequenza frame "23.970" produce 5 livelli video:

|Livello|Altezza:|Larghezza|Bitrate (Kbps)|
|---|---|---|---|
|1|720|1280|2940|
|2|540|960|1850|
|3|360|640|960|
|4|270|480|600|
|5|180|320|320|

### <a name="example-3"></a>Esempio 3
L'origine con altezza "360" e una frequenza frame "29.970" produce 3 livelli video:

|Livello|Altezza:|Larghezza|Bitrate (Kbps)|
|---|---|---|---|
|1|360|640|700|
|2|270|480|440|
|3|180|320|230|
## <a name="media-services-learning-paths"></a>Percorsi di apprendimento di Servizi multimediali
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornire commenti e suggerimenti
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>Vedere anche
[Panoramica sulla codifica dei servizi multimediali](media-services-encode-asset.md)

