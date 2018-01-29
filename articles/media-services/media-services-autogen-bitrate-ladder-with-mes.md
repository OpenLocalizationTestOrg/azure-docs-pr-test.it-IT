---
title: Usare Azure Media Encoder Standard per generare automaticamente un bitrate ladder | Microsoft Docs
description: "In questo argomento viene illustrato come usare Media Encoder Standard (MES) per generare automaticamente un bitrate ladder in base alla risoluzione di input e alla velocità in bit. La risoluzione di input e la velocità in bit non vengono mai superate. Ad esempio, se l'input è 720p a 3 Mbps, l'output resterà al massimo a 720p e inizierà a una velocità inferiore a 3 Mbps."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/10/2017
ms.author: juliako
ms.openlocfilehash: 4ffced8e11f05d214995f9fc8506dd7c6c7deaa5
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/11/2017
---
#  <a name="use-azure-media-encoder-standard-to-auto-generate-a-bitrate-ladder"></a>Usare Azure Media Encoder Standard per generare automaticamente un bitrate ladder

## <a name="overview"></a>Panoramica

In questo articolo viene illustrato come utilizzare Media codificatore Standard (MES) per generare automaticamente una scala di velocità in bit (coppie di risoluzione a velocità in bit) in base alla risoluzione di input e velocità in bit. Il set di impostazioni generate automaticamente non supererà mai la risoluzione di input e la velocità in bit. Ad esempio, se l'input è 720p 3 Mbps, output rimane nella migliore delle ipotesi 720p e inizierà a velocità inferiore a 3 Mbps.

### <a name="encoding-for-streaming-only"></a>Codifica solo per lo streaming

Se si intende codificare un video di origine solo per lo streaming, è necessario utilizzare il "il flusso adattivo" predefinito durante la creazione di un'attività di codifica. Quando si usa il set di impostazioni **Flusso adattivo** il codificatore MES userà in modo intelligente un bitrate ladder. Tuttavia, non sarà possibile controllare i costi di codifica, poiché il servizio determina il numero di livelli da usare e la risoluzione. È possibile visualizzare esempi dei livelli di output prodotti da MES in seguito alla codifica con il **il flusso adattivo** predefinito alla fine di questo articolo. L'output di che file MP4 contenente audio e video non viene interfacciato.

### <a name="encoding-for-streaming-and-progressive-download"></a>Codifica per streaming e download progressivo

Se si intende per codificare un video di origine per i flussi, nonché per produrre file MP4 per il download progressivo, è necessario utilizzare il "contenuto adattivo più velocità in bit MP4" predefinito durante la creazione di un'attività di codifica. Quando si utilizza il **contenuto file MP4 a velocità in bit adattiva più** predefinito, il codificatore MES applica la stessa logica di codifica come illustrato in precedenza, ma ora l'asset di output conterrà i file MP4 in audio e video è alternato. È possibile usare uno di questi file MP4 (ad esempio la versione con bitrate più elevato) come file di download progressivo.

## <a id="encoding_with_dotnet"></a>Codifica con l’SDK .NET dei servizi multimediali

Il seguente codice usa l'SDK .NET di Servizi multimediali per eseguire le seguenti attività: 

- Creare un processo di codifica.
- Ottenere un riferimento al codificatore Media Encoder Standard.
- Aggiungere un'attività di codifica al processo e specificare l'uso del set di impostazioni **Flusso adattivo**. 
- Creare un asset di output che contenga l'asset codificato.
- Aggiungere un gestore eventi per controllare l'avanzamento del processo.
- Inviare il processo.

#### <a name="create-and-configure-a-visual-studio-project"></a>Creare e configurare un progetto di Visual Studio

Configurare l'ambiente di sviluppo e popolare il file app.config con le informazioni di connessione, come descritto in [Sviluppo di applicazioni di Servizi multimediali con .NET](media-services-dotnet-how-to-use.md). 

#### <a name="example"></a>Esempio

```
using System;
using System.Configuration;
using System.Linq;
using Microsoft.WindowsAzure.MediaServices.Client;
using System.Threading;

namespace AdaptiveStreamingMESPresest
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

            // Get an uploaded asset.
            var asset = _context.Assets.FirstOrDefault();

            // Encode and generate the output using the "Adaptive Streaming" preset.
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

            // Create a task
            ITask task = job.Tasks.AddNew("Media Encoder Standard encoding task",
            processor,
            "Adaptive Streaming",
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
```

## <a id="output"></a>Output

Questa sezione mostra tre esempi dei livelli di output prodotti da MES in seguito alla codifica con il set di impostazioni **Flusso adattivo**. 

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

