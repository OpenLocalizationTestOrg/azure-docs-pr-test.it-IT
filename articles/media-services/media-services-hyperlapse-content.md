---
title: File multimediali con Azure Media Hyperlapse aaaHyperlapse | Documenti Microsoft
description: Azure Media Hyperlapse crea fluidi video in time-lapse da contenuti registrati in prima persona o da fotocamere d'azione. Questo argomento viene illustrato come toouse Media Indexer.
services: media-services
documentationcenter: 
author: asolanki
manager: johndeu
editor: 
ms.assetid: 37d54db6-9cf3-4ae9-b3c6-0d29c744e965
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/02/2017
ms.author: adsolank
ms.openlocfilehash: 85bb07206d0ca2f5b2fd0767e6ed4904195d3ab6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="hyperlapse-media-files-with-azure-media-hyperlapse"></a>File multimediali di Hyperlapse con Azure Media Hyperlapse
Azure Media Hyperlapse è un processore di contenuti multimediali che crea fluidi video in time-lapse da contenuti registrati in prima persona o da fotocamere d'azione.  Hello troppo di pari livello basato su cloud[desktop Hyperlapse Pro Microsoft Research e basato sul telefono cellulare Hyperlapse](http://aka.ms/hyperlapse), Hyperlapse Microsoft per servizi multimediali di Azure Usa hello larga scala hello multimediali di Azure Media Services L'elaborazione di piattaforma toohorizontally scalare e parallelizzare bulk elaborazione con Hyperlapse.

> [!IMPORTANT]
> Microsoft Hyperlapse è progettato toowork migliore in prima persona contenuto con una fotocamera mobile.  Sebbene ancora videocamera può comunque funzionare, hello prestazioni e qualità di hello processore di contenuti multimediali di Azure Media Hyperlapse non può essere garantite per altri tipi di contenuto.  informazioni su Microsoft Hyperlapse per servizi multimediali di Azure toolearn e vedere alcuni video di esempio, estrarre hello [post di blog introduttivo](http://aka.ms/azurehyperlapseblog) dalla versione di anteprima pubblica di hello.
> 
> 

Un Azure Media Hyperlapse processo accetta come input un file di asset MP4, MOV o WMV insieme a un file di configurazione che specifica i frame del video devono essere tempo trascorso e velocità toowhat (ad esempio 10.000 primo frame x 2).  output di Hello è una copia trasformata stabilizzare e tempo trascorso di video di input hello.

Per aggiornamenti di Azure Media Hyperlapse hello più recenti, vedere [blog di servizi multimediali](https://azure.microsoft.com/blog/topics/media-services/).

## <a name="hyperlapse-an-asset"></a>Eseguire Hyperlapse su un asset
Innanzitutto è necessario tooupload il tooAzure di file di input desiderata servizi multimediali.  altre informazioni sulle toolearn hello concetti fondamentali per il caricamento e la gestione del contenuto, leggere hello [articolo di gestione dei contenuti](media-services-portal-vod-get-started.md).

### <a id="configuration"></a>Set di impostazioni di configurazione per Hyperlapse
Una volta il contenuto nell'account di servizi multimediali, sarà necessario tooconstruct set di impostazioni di configurazione.  Hello nella tabella seguente vengono illustrati i campi di hello specificato dall'utente:

| Campo | Descrizione |
| --- | --- |
| StartFrame |frame Hello al quale Microsoft Hyperlapse hello deve iniziare l'elaborazione. |
| NumFrames |numero di Hello di frame tooprocess |
| Velocità |fattore di Hello con cui toospeed i video di input hello. |

Hello Ecco un esempio di file di configurazione conformi in XML e JSON:

**Set di impostazioni XML:**

    <?xml version="1.0" encoding="utf-16"?>
    <Preset xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
        <Sources>
            <Source StartFrame="0" NumFrames="10000" />
        </Sources>
        <Options>
            <Speed>12</Speed>
        </Options>
    </Preset>

**Set di impostazioni JSON:**

    {
        "Version":1.0,
        "Sources": [
            {
                "StartFrame":0,
                "NumFrames":2147483647
            }
        ],
        "Options": {
            "Speed":1,
            "Stabilize":false
        }
    }

### <a id="sample_code"></a>Microsoft Hyperlapse con hello AMS .NET SDK
Hello metodo seguente carica un file multimediale come asset e crea un processo con hello processore di contenuti multimediali di Azure Media Hyperlapse.

> [!NOTE]
> Hai già un CloudMediaContext nell'ambito con hello nome "contesto" per toowork questo codice.  ulteriori informazioni, leggere hello toolearn [articolo di gestione dei contenuti](media-services-dotnet-get-started.md).
> 
> [!NOTE]
> argomento stringa Hello "hyperConfig" è previsto toobe preimpostata di una configurazione conforme a JSON o XML come descritto in precedenza.
> 
> 

        static bool RunHyperlapseJob(string input, string output, string hyperConfig)
        {
            // create asset with input file
            IAsset asset = context
            .Assets
            .CreateAssetAndUploadSingleFile(input, "My Hyperlapse Input", AssetCreationOptions.None);

            // grab instances of Azure Media Hyperlapse MP
            IMediaProcessor mp = context
            .MediaProcessors
            .GetLatestMediaProcessorByName("Azure Media Hyperlapse");

            // create Job with Hyperlapse task
            IJob job = context
            .Jobs
            .Create(String.Format("Hyperlapse {0}", input));

            if (String.IsNullOrEmpty(hyperConfig))
            {
            // config cannot be empty
            return false;
            }

            hyperConfig = File.ReadAllText(hyperConfig);

            ITask hyperlapseTask = job.Tasks.AddNew("Hyperlapse task",
            mp,
            hyperConfig,
            TaskOptions.None);
            hyperlapseTask.InputAssets.Add(asset);
            hyperlapseTask.OutputAssets.AddNew("Hyperlapse output",
            AssetCreationOptions.None);

            job.Submit();

            // Create progress printing and querying tasks
            Task progressPrintTask = new Task(() =>
            {

            IJob jobQuery = null;
            do
            {
                var progressContext = context;
                jobQuery = progressContext.Jobs
                .Where(j => j.Id == job.Id)
                .First();
                Console.WriteLine(string.Format("{0}\t{1}\t{2}",
                DateTime.Now,
                jobQuery.State,
                jobQuery.Tasks[0].Progress));
                Thread.Sleep(10000);
            }
            while (jobQuery.State != JobState.Finished &&
                                   jobQuery.State != JobState.Error &&
                                   jobQuery.State != JobState.Canceled);
                });
                
            progressPrintTask.Start();

            Task progressJobTask = job.GetExecutionProgressTask(
                                                 CancellationToken.None);
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
                return false;                  
            }

        DownloadAsset(job.OutputMediaAssets.First(), output);
        return true;
    }

    static void DownloadAsset(IAsset asset, string outputDirectory)
    {
        foreach (IAssetFile file in asset.AssetFiles)
        {
            file.Download(Path.Combine(outputDirectory, file.Name));
        }
    }


    static IAsset CreateAssetAndUploadSingleFile(string filePath, string assetName, AssetCreationOptions options)
    {
        IAsset asset = context.Assets.Create(assetName, options);

        var assetFile = asset.AssetFiles.Create(Path.GetFileName(filePath));
        assetFile.Upload(filePath);

        return asset;
    }

    static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
    {
        var processor = context.MediaProcessors
        .Where(p => p.Name == mediaProcessorName)
        .ToList()
        .OrderBy(p => new Version(p.Version))
        .LastOrDefault();

        if (processor == null)
            throw new ArgumentException(string.Format("Unknown media processor",
                                                       mediaProcessorName));

        return processor;
    }

### <a id="file_types"></a>Tipi di file supportati
* MP4
* MOV
* WMV

## <a name="media-services-learning-paths"></a>Percorsi di apprendimento di Servizi multimediali
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornire commenti e suggerimenti
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a>Collegamenti correlati
[Panoramica di Analisi servizi multimediali di Azure](media-services-analytics-overview.md)

[Demo di Analisi servizi multimediali di Azure](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

