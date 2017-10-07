---
title: aaaAdvanced codifica con flusso di lavoro Premium del codificatore multimediale | Documenti Microsoft
description: Informazioni su come tooencode con flusso di lavoro Premium del codificatore multimediale. Esempi di codice sono scritti in c# e utilizzano hello Media Services SDK per .NET.
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 0f4c87ac-810a-4d42-8df8-923dff2016c6
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: juliako
ms.openlocfilehash: 5a1c3d019a5c8fbf9bda2da751a7eff4c4907d97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-encoding-with-media-encoder-premium-workflow"></a>Codifica avanzata con il flusso di lavoro Premium del codificatore multimediale
> [!NOTE]
> Il processore di contenuti multimediali del flusso di lavoro Premium del codificatore multimediale descritto in questo argomento non è disponibile in Cina.
>
>

Per domande relative al codificatore Premium, inviare mepd tramite un messaggio di posta elettronica a Microsoft.com.

## <a name="overview"></a>Panoramica
Servizi multimediali di Microsoft Azure ha introdotto hello **flusso di lavoro Premium del codificatore multimediale** processore di contenuti multimediali. Questo processore offre funzionalità di codifica avanzata per i flussi di lavoro Premium su richiesta.

Negli argomenti seguenti vengono Hello descrive i dettagli correlati troppo**flusso di lavoro Premium del codificatore multimediale**:

* [Formati supportati dal flusso di lavoro Premium del codificatore multimediale hello](media-services-premium-workflow-encoder-formats.md) : vengono illustrati i formati di file hello e codec supportati da **flusso di lavoro Premium del codificatore multimediale**.
* [Panoramica e un confronto di Azure in codificatori media richiesta](media-services-encode-asset.md) Confronta hello le funzionalità di codifica di **flusso di lavoro Premium del codificatore multimediale** e **Media Encoder Standard**.

Questo argomento viene illustrato come tooencode con **flusso di lavoro Premium del codificatore multimediale** usando .NET.

Codifica di attività per hello **flusso di lavoro Premium del codificatore multimediale** richiedono un file di configurazione separato, denominato file del flusso di lavoro. Tali file hanno estensione .workflow e vengono creati utilizzando hello [Progettazione flussi di lavoro](media-services-workflow-designer.md) strumento.

È inoltre possibile ottenere predefinito hello i file del flusso di lavoro [qui](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows). cartella Hello contiene inoltre descrizione hello di questi file.

file di flusso di lavoro Hello devono toobe caricato tooyour di account di servizi multimediali come Asset, e questo Asset deve essere passato nell'attività di codifica toohello.

## <a name="create-and-configure-a-visual-studio-project"></a>Creare e configurare un progetto di Visual Studio

Configurare l'ambiente di sviluppo e di popolare il file app. config hello con informazioni di connessione, come descritto in [lo sviluppo di servizi multimediali con .NET](media-services-dotnet-how-to-use.md). 

## <a name="encoding-example"></a>Esempio di codifica

Hello esempio seguente viene illustrato come tooencode con **flusso di lavoro Premium del codificatore multimediale**.

viene eseguita Hello alla procedura seguente:

1. Creare un asset e caricare un file del flusso di lavoro.
2. Creare un asset e caricare un file multimediale di origine.
3. Ottenere processore di contenuti multimediali hello "Media Encoder Premium del flusso di lavoro".
4. Creare un processo e un'attività.

    Nella maggior parte dei casi, la stringa di configurazione per l'attività hello hello è vuota (come nel seguente esempio hello). Esistono alcuni scenari avanzati (che richiedono in modo dinamico la proprietà di runtime tootooset) in questo caso è necessario fornire un'attività di codifica toohello di stringa XML. Esempi di tali scenari sono: creazione di un overlay, unione sequenziale o parallela di supporti e aggiunta di sottotitoli.
5. Aggiungere due attività di toohello asset di input.

    1. 1 ° – asset di hello del flusso di lavoro.
    2. 2 – asset video hello.

    >[!NOTE]
    >asset del flusso di lavoro Hello devono essere aggiunti toohello attività prima di asset di file multimediali hello.
   stringa di configurazione Hello per questa attività deve essere vuota.
   
6. Inviare il processo di codifica hello.

        using System;
        using System.Linq;
        using System.Configuration;
        using System.IO;
        using System.Threading;
        using System.Threading.Tasks;
        using Microsoft.WindowsAzure.MediaServices.Client;

        namespace MediaEncoderPremiumWorkflowSample
        {
            class Program
            {
                private static readonly string _AADTenantDomain =
                    ConfigurationManager.AppSettings["AADTenantDomain"];
                private static readonly string _RESTAPIEndpoint =
                    ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

                // Field for service context.
                private static CloudMediaContext _context = null;

                private static readonly string _supportFiles =
                    Path.GetFullPath(@"../..\Media");

                private static readonly string _workflowFilePath =
                    Path.GetFullPath(_supportFiles + @"\H264 Progressive Download MP4.workflow");

                private static readonly string _singleMP4InputFilePath =
                    Path.GetFullPath(_supportFiles + @"\BigBuckBunny.mp4");

                static void Main(string[] args)
                {
                    var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
                    var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

                    _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

                    var workflowAsset = CreateAssetAndUploadSingleFile(_workflowFilePath);
                    var videoAsset = CreateAssetAndUploadSingleFile(_singleMP4InputFilePath);
                    IAsset outputAsset = CreateEncodingJob(workflowAsset, videoAsset);

                }

                static public IAsset CreateAssetAndUploadSingleFile(string singleFilePath)
                {
                    var assetName = "UploadSingleFile_" + DateTime.UtcNow.ToString();
                    var asset = _context.Assets.Create(assetName, AssetCreationOptions.None);

                    var fileName = Path.GetFileName(singleFilePath);

                    var assetFile = asset.AssetFiles.Create(fileName);

                    Console.WriteLine("Created assetFile {0}", assetFile.Name);

                    Console.WriteLine("Upload {0}", assetFile.Name);

                    assetFile.Upload(singleFilePath);
                    Console.WriteLine("Done uploading {0}", assetFile.Name);

                    return asset;
                }

                static public IAsset CreateEncodingJob(IAsset workflow, IAsset video)
                {
                    // Declare a new job.
                    IJob job = _context.Jobs.Create("Premium Workflow encoding job");
                    // Get a media processor reference, and pass tooit hello name of the
                    // processor toouse for hello specific task.
                    IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Premium Workflow");

                    // Create a task with hello encoding details, using a string preset.
                    ITask task = job.Tasks.AddNew("Premium Workflow encoding task",
                        processor,
                        "",
                        TaskOptions.None);

                    // Specify hello input asset toobe encoded.
                    task.InputAssets.Add(workflow);
                    task.InputAssets.Add(video); // we add one asset
                                                 // Add an output asset toocontain hello results of hello job.
                                                 // This output is specified as AssetCreationOptions.None, which
                                                 // means hello output asset is not encrypted.
                    task.OutputAssets.AddNew("Output asset",
                        AssetCreationOptions.None);

                    // Use hello following event handler toocheck job progress.  
                    job.StateChanged += new
                            EventHandler<JobStateChangedEventArgs>(StateChanged);

                    // Launch hello job.
                    job.Submit();

                    // Check job execution and wait for job toofinish.
                    Task progressJobTask = job.GetExecutionProgressTask(CancellationToken.None);
                    progressJobTask.Wait();

                    // If job state is Error hello event handling
                    // method for job progress should log errors.  Here we check
                    // for error state and exit if needed.
                    if (job.State == JobState.Error)
                    {
                        throw new Exception("\nExiting method due toojob error.");
                    }

                    return job.OutputMediaAssets[0];
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

Per domande relative al codificatore Premium, inviare mepd tramite un messaggio di posta elettronica a Microsoft.com.

## <a name="media-services-learning-paths"></a>Percorsi di apprendimento di Servizi multimediali
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornire commenti e suggerimenti
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
