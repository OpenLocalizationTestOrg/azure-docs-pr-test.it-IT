---
title: un asset con Media Encoder Standard usando .NET aaaEncode | Documenti Microsoft
description: Questo argomento viene illustrato come toouse .NET tooencode un asset con Media Encoder standard.
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 03431b64-5518-478a-a1c2-1de345999274
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: juliako;anilmur
ms.openlocfilehash: 25e274c3b67168f4afc8b8ab04af2d654c9dd6e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="encode-an-asset-with-media-encoder-standard-using-net"></a>Codificare un asset con Media Encoder Standard mediante .NET
I processi di codifica sono una delle operazioni di elaborazione più comune di hello in servizi multimediali. Viene creato codifica file multimediali tooconvert di processi da un tooanother codifica. Quando si codifica, è possibile utilizzare il codificatore multimediale incorporato di servizi multimediali hello. È inoltre possibile utilizzare un codificatore fornito da un partner di servizi multimediali. i codificatori di terze parti sono disponibili tramite hello Azure Marketplace. 

Questo argomento viene illustrato come toouse .NET tooencode gli asset con Media codificatore Standard (MES). Media Encoder Standard viene configurato usando uno dei set di impostazioni di codificatore hello descritto [qui](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409).

È consigliabile tooalways codificare i file di origine in un set MP4 a velocità in bit adattiva, quindi convertire hello set toohello formato desiderato utilizzando hello [creazione dinamica dei pacchetti](media-services-dynamic-packaging-overview.md). 

Se l'asset di output è protetto con crittografia di archiviazione, è necessario configurare i criteri di distribuzione degli asset. Per altre informazioni, vedere [Procedura: Configurare i criteri di distribuzione degli asset](media-services-dotnet-configure-asset-delivery-policy.md).

> [!NOTE]
> Produce MES un file di output con un nome contenente hello primi 32 caratteri del hello Nome file di input. nome di Hello è basato su quello specificato nel file preimpostato hello. Ad esempio, "FileName": "{Basename}_{Index}{Extension}". {Nome} viene sostituito da hello primi 32 caratteri del nome di file di input hello.
> 
> 

### <a name="mes-formats"></a>Formati MES
[Codec e formati](media-services-media-encoder-standard-formats.md)

### <a name="mes-presets"></a>Impostazioni predefinite MES
Media Encoder Standard viene configurato usando uno dei set di impostazioni di codificatore hello descritto [qui](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409).

### <a name="input-and-output-metadata"></a>Metadati di input e output
Quando si codifica un asset di input o asset mediante MES, si ottiene un asset di output in hello corretto completamento di tale codifica attività. Hello output contenente video, audio, anteprime, manifesto, e così via in base a hello set di impostazioni codifica che è utilizzare.

asset di output di Hello contiene anche un file con i metadati sull'asset di input hello. nome del file XML dei metadati di hello Hello ha hello seguente formato: < asset_id > <id_asset>_metadata.XML (ad esempio, d 57-8 41114ad3-eb5e - 4c 92-5354e2b7d4a4_metadata.xml), dove < asset_id > è il valore di AssetId hello dell'asset di input hello. Hello schema dei metadati input XML è descritta [qui](media-services-input-metadata-schema.md).

asset di output di Hello contiene anche un file con i metadati sull'asset di output di hello. nome del file XML dei metadati di hello Hello ha hello seguente formato: < deve > <nome_file_origine>_manifest.XML (ad esempio, BigBuckBunny_manifest.xml). schema di Hello questi metadati di output XML è descritta [qui](media-services-output-metadata-schema.md).

Se si desidera tooexamine hello due file di metadati, è possibile creare un localizzatore SAS e scaricare computer locale tooyour di file hello. È possibile trovare un esempio di come toocreate un localizzatore SAS e scaricare un file tramite hello di servizi multimediali .NET SDK Extensions.

## <a name="download-sample"></a>Scaricare un esempio
È possibile ottenere ed eseguire un esempio che illustra come tooencode con MES da [qui](https://azure.microsoft.com/documentation/samples/media-services-dotnet-on-demand-encoding-with-media-encoder-standard/).

## <a name="net-sample-code"></a>Codice di esempio .NET

esempio di codice seguente Hello utilizza hello tooperform Media Services .NET SDK seguenti attività:

* Creare un processo di codifica.
* Ottiene un codificatore Media Encoder Standard toohello di riferimento.
* Specificare hello toouse [il flusso adattivo](media-services-autogen-bitrate-ladder-with-mes.md) predefinito. 
* Aggiungere un singolo processo di toohello codifica di attività. 
* Specificare l'input hello toobe asset codificato.
* Creare un asset di output che conterrà l'asset codificato hello.
* Aggiungere un avanzamento del processo hello toocheck gestore dell'evento.
* Inviare il processo di hello.

#### <a name="create-and-configure-a-visual-studio-project"></a>Creare e configurare un progetto di Visual Studio

Configurare l'ambiente di sviluppo e di popolare il file app. config hello con informazioni di connessione, come descritto in [lo sviluppo di servizi multimediali con .NET](media-services-dotnet-how-to-use.md). 

#### <a name="example"></a>Esempio 

        using System;
        using System.Linq;
        using System.Configuration;
        using System.IO;
        using System.Threading;
        using Microsoft.WindowsAzure.MediaServices.Client;

        namespace MediaEncoderStandardSample
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

                    // Create a task with hello encoding details, using a string preset.
                    // In this case "Adaptive Streaming" preset is used.
                    ITask task = job.Tasks.AddNew("My encoding task",
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

## <a name="media-services-learning-paths"></a>Percorsi di apprendimento di Servizi multimediali
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornire commenti e suggerimenti
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a>Passaggi successivi
[La modalità anteprima toogenerate con Media Encoder Standard .NET](media-services-dotnet-generate-thumbnail-with-mes.md)
[codifica Panoramica di servizi multimediali](media-services-encode-asset.md)

