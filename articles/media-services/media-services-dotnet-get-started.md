---
title: aaaGet avviato con la distribuzione di contenuti su richiesta usando .NET | Documenti Microsoft
description: In questa esercitazione vengono illustrati i passaggi hello dell'implementazione di un'applicazione di recapito del contenuto su richiesta con servizi multimediali di Azure usando .NET.
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 388b8928-9aa9-46b1-b60a-a918da75bd7b
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 07/31/2017
ms.author: juliako
ms.openlocfilehash: 4ca9394bd581e1d9062e5a008a410b2c058e017e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-delivering-content-on-demand-using-net-sdk"></a>Introduzione alla distribuzione di contenuti su richiesta utilizzando .NET SDK
[!INCLUDE [media-services-selector-get-started](../../includes/media-services-selector-get-started.md)]

In questa esercitazione vengono illustrati i passaggi hello dell'implementazione di un servizio di distribuzione di contenuti video on Demand (VoD) base con l'applicazione di servizi multimediali di Azure (AMS) utilizzando hello Azure Media Services .NET SDK.

## <a name="prerequisites"></a>Prerequisiti

di seguito Hello sono esercitazione hello toocomplete necessarie:

* Un account Azure. Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).
* Account di Servizi multimediali. toocreate un account di servizi multimediali, vedere [come un Account di servizi multimediali tooCreate](media-services-portal-create-account.md).
* .NET Framework 4.0 o versione successiva.
* Visual Studio.

In questa esercitazione include hello seguenti attività:

1. Avviare lo streaming di endpoint (tramite hello portale di Azure).
2. Creare e configurare un progetto di Visual Studio.
3. Connettere l'account di servizi multimediali toohello.
2. Caricare un file video.
3. Codificare il file di origine hello in un set di file MP4 a velocità in bit adattiva.
4. Pubblicare l'asset hello e get streaming e l'URL di download progressivo.  
5. Riprodurre i contenuti.

## <a name="overview"></a>Panoramica
In questa esercitazione vengono illustrati i passaggi hello di implementazione di un'applicazione di distribuzione di contenuti video on Demand (VoD) usando Azure Media Services SDK (AMS) per .NET.

esercitazione Hello introduce hello base servizi multimediali del flusso di lavoro e gli oggetti di programmazione più comuni di hello e attività necessarie per lo sviluppo di servizi multimediali. Al termine di hello di esercitazione hello, si verrà toostream in grado o un file multimediale di esempio che caricati, con codifica e scaricato il download progressivo.

### <a name="ams-model"></a>Modello AMS

Hello immagine seguente mostra alcuni degli oggetti hello più comunemente utilizzato quando si sviluppano applicazioni VoD sul modello di Media Services OData hello.

Fare clic su tooview immagine hello le dimensioni massime.  

<a href="./media/media-services-dotnet-get-started/media-services-overview-object-model.png" target="_blank"><img src="./media/media-services-dotnet-get-started/media-services-overview-object-model-small.png"></a> 

È possibile visualizzare l'intero modello hello [qui](https://media.windows.net/API/$metadata?api-version=2.15).  

## <a name="start-streaming-endpoints-using-hello-azure-portal"></a>Avviare lo streaming di endpoint che utilizzano hello portale di Azure

Quando si lavora con uno degli scenari più comuni di hello recapita video tramite velocità in bit adattive servizi multimediali di Azure. Servizi multimediali fornisce creazione dinamica dei pacchetti, che consente di toodeliver la velocità in bit adattiva contenuto MP4 in formato con codificata in streaming formati supportati da servizi multimediali (MPEG DASH, HLS, Smooth Streaming) just-in-time, senza che sia necessario toostore preconfezionata versioni di ciascuno di questi formati di streaming.

>[!NOTE]
>Quando viene creato l'account di sistema AMS un **predefinito** endpoint di streaming viene aggiunto l'account tooyour in hello **arrestato** stato. lo streaming del contenuto e intraprendere sfruttare creazione dinamica dei pacchetti e la crittografia dinamica, toostart hello endpoint di streaming da cui si desidera in hello del contenuto toostream è toobe **esecuzione** stato.

toostart hello endpoint di streaming, hello seguenti:

1. Accedere all'indirizzo hello [portale di Azure](https://portal.azure.com/).
2. Nella finestra Impostazioni hello, fare clic su endpoint di Streaming.
3. Fare clic su predefinito hello endpoint di streaming.

    verrà visualizzata la finestra Dettagli dell'ENDPOINT di STREAMING predefinito Hello.

4. Fare clic sull'icona di avvio hello.
5. Fare clic su toosave pulsante di hello Salva le modifiche.

## <a name="create-and-configure-a-visual-studio-project"></a>Creare e configurare un progetto di Visual Studio

1. Configurare l'ambiente di sviluppo e di popolare il file app. config hello con informazioni di connessione, come descritto in [lo sviluppo di servizi multimediali con .NET](media-services-dotnet-how-to-use.md). 
2. Creare una nuova cartella (cartella può essere un punto qualsiasi nell'unità locale) e copiare un file MP4 che si desidera tooencode e flusso o il download progressivo. In questo esempio viene utilizzato il percorso di "C:\VideoFiles" hello.

## <a name="connect-toohello-media-services-account"></a>Connettere l'account di servizi multimediali toohello

Quando si usa servizi multimediali con .NET, è necessario utilizzare hello **CloudMediaContext** classe per la maggior parte dei servizi multimediali di attività di programmazione: connessione account servizi tooMedia; la creazione, aggiornamento, l'accesso e l'eliminazione seguente hello oggetti: asset, file di asset, processi, i criteri di accesso, i localizzatori, e così via.

Sovrascrivere classe Program predefinita di hello con hello seguente codice. Hello codice viene illustrato come connessione hello tooread valori dal file app. config hello e come hello toocreate **CloudMediaContext** oggetto in ordine tooconnect tooMedia servizi. Per ulteriori informazioni, vedere [connessione toohello API di servizi multimediali](media-services-use-aad-auth-to-access-ams-api.md).

Verificare che tooupdate hello file nome e percorso toowhere che è il file di supporto.

Hello **Main** funzione chiama i metodi che verranno definiti più avanti in questa sezione.

> [!NOTE]
> Verranno recuperati gli errori di compilazione finché non si aggiunge le definizioni per tutte le funzioni hello.

    class Program
    {
        // Read values from hello App.config file.
        private static readonly string _AADTenantDomain =
        ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
        ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

        private static CloudMediaContext _context = null;

        static void Main(string[] args)
        {
        try
        {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

            // Add calls toomethods defined in this section.
            // Make sure tooupdate hello file name and path toowhere you have your media file.
            IAsset inputAsset =
            UploadFile(@"C:\VideoFiles\BigBuckBunny.mp4", AssetCreationOptions.None);

            IAsset encodedAsset =
            EncodeToAdaptiveBitrateMP4s(inputAsset, AssetCreationOptions.None);

            PublishAssetGetURLs(encodedAsset);
        }
        catch (Exception exception)
        {
            // Parse hello XML error message in hello Media Services response and create a new
            // exception with its content.
            exception = MediaServicesExceptionParser.Parse(exception);

            Console.Error.WriteLine(exception.Message);
        }
        finally
        {
            Console.ReadLine();
        }
        }
    }

## <a name="create-a-new-asset-and-upload-a-video-file"></a>Creare un nuovo asset e caricare un file video

In Servizi multimediali i file digitali vengono caricati (o inseriti) in un asset. Hello **Asset** entità può contenere video, audio, immagini, raccolte di anteprime, testo, tracce e sottotitoli file (e relativi metadati hello.)  Una volta caricati i file hello, il contenuto è archiviato in modo sicuro nel cloud hello per continuare l'elaborazione e il flusso. file Hello in asset hello sono denominati **file di Asset**.

Hello **UploadFile** metodo definito riportato di seguito chiama **CreateFromFile** (definito in .NET SDK Extensions). **CreateFromFile** crea un nuovo asset in cui hello viene caricato il file di origine specificato.

Hello **CreateFromFile** metodo accetta **AssetCreationOptions** che consente di specificare una delle seguenti opzioni di creazione di asset hello:

* **None** : non viene usata alcuna crittografia. Questo è il valore di predefinito hello. Quando si usa questa opzione, il contenuto non è protetto durante il transito, né nell'archiviazione locale.
  Se si prevede di toodeliver un file MP4 tramite download progressivo, usare questa opzione.
* **StorageEncrypted** -utilizzare questa opzione tooencrypt il contenuto non crittografato in locale utilizzando la crittografia di Advanced Encryption Standard (AES)-256 bit, che quindi lo carica tooAzure archiviazione dove viene archiviato in forma crittografata. Gli asset protetti con crittografia di archiviazione vengono decrittografati automaticamente e inseriti in un file crittografato sistema precedente tooencoding e, facoltativamente, crittografare nuovamente toouploading precedente come nuovo asset di output. Hello primario per la crittografia di archiviazione viene usata quando si desidera toosecure i file multimediali di input di alta qualità con la crittografia avanzata inattivi sul disco.
* **CommonEncryptionProtected** : usare questa opzione per caricare contenuti già crittografati e protetti con Common Encryption o PlayReady DRM (ad esempio, Smooth Streaming protetto con PlayReady DRM).
* **EnvelopeEncryptionProtected** : usare questa opzione se si stanno caricando contenuti HLS crittografati con AES. Si noti che i file hello devono sono stati codificati e crittografati da Transform Manager.

Hello **CreateFromFile** metodo consente inoltre di specificare un callback in ordine tooreport hello lo stato di caricamento del file hello.

Nell'esempio seguente di hello, viene specificato **Nessuno** per le opzioni di asset hello.

Aggiungere hello seguente classe Program toohello di metodo.

    static public IAsset UploadFile(string fileName, AssetCreationOptions options)
    {
        IAsset inputAsset = _context.Assets.CreateFromFile(
            fileName,
            options,
            (af, p) =>
            {
                Console.WriteLine("Uploading '{0}' - Progress: {1:0.##}%", af.Name, p.Progress);
            });

        Console.WriteLine("Asset {0} created.", inputAsset.Id);

        return inputAsset;
    }


## <a name="encode-hello-source-file-into-a-set-of-adaptive-bitrate-mp4-files"></a>Codificare il file di origine hello in un set di file MP4 a velocità in bit adattiva
Dopo l'inserimento di asset in servizi multimediali, supporto può essere codificato, transmux filigrana e così via, prima di consegnarlo tooclients. Queste attività vengono pianificate e vengono eseguite più background ruolo istanze tooensure ad alte prestazioni e disponibilità. Queste attività sono denominate processi, e ogni processo è costituito da attività atomiche che hello operazioni effettive sul file di Asset hello.

Come accennato in precedenza, quando si lavora con servizi multimediali di Azure, uno degli scenari più comuni di hello recapita velocità in bit adattive tooyour client. Servizi multimediali può pacchetto in modo dinamico un set di file MP4 a velocità in bit adattiva in uno dei seguenti formati hello: MPEG DASH, Smooth Streaming e HTTP Live Streaming (HLS).

Il vantaggio di tootake creazione dinamica dei pacchetti, è necessario tooencode o eseguire la transcodifica il file mezzanine (origine) in un set di file MP4 o file Smooth Streaming a velocità in bit adattiva.  

Hello seguente codice mostra come toosubmit una codifica del processo. processo Hello contiene un'attività che specifica i file in formato intermedio di hello tootranscode in un set di velocità in bit adattiva MP4s utilizzando **Media Encoder Standard**. codice Hello invia il processo di hello e attende finché viene completato.

Una volta completato il processo di hello, si è in grado di toostream l'asset o eseguire il download progressivo file MP4 che sono stati creati come risultato di transcodifica.

Aggiungere hello seguente classe Program toohello di metodo.

    static public IAsset EncodeToAdaptiveBitrateMP4s(IAsset asset, AssetCreationOptions options)
    {

        // Prepare a job with a single task tootranscode hello specified asset
        // into a multi-bitrate asset.

        IJob job = _context.Jobs.CreateWithSingleTask(
            "Media Encoder Standard",
            "Adaptive Streaming",
            asset,
            "Adaptive Bitrate MP4",
            options);

        Console.WriteLine("Submitting transcoding job...");


        // Submit hello job and wait until it is completed.
        job.Submit();

        job = job.StartExecutionProgressTask(
            j =>
            {
                Console.WriteLine("Job state: {0}", j.State);
                Console.WriteLine("Job progress: {0:0.##}%", j.GetOverallProgress());
            },
            CancellationToken.None).Result;

        Console.WriteLine("Transcoding job finished.");

        IAsset outputAsset = job.OutputMediaAssets[0];

        return outputAsset;
    }

## <a name="publish-hello-asset-and-get-urls-for-streaming-and-progressive-download"></a>Pubblicare l'asset hello e ottenere l'URL per il download progressivo e streaming

toostream o scarica un asset, è innanzitutto necessario troppo "pubblicarlo" tramite la creazione di un indicatore di posizione. I localizzatori forniscono accesso toofiles contenuti in hello asset. Servizi multimediali sono supportati due tipi di localizzatori: OnDemandOrigin localizzatori, supporto toostream utilizzato (ad esempio, MPEG DASH, HLS o Smooth Streaming) e localizzatori di firma di accesso (SAS), utilizzato file multimediali toodownload (per ulteriori informazioni sulla firma di accesso condiviso localizzatori vedere [questo](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/) blog).

### <a name="some-details-about-url-formats"></a>Alcuni dettagli sui formati di URL

Dopo aver creato i localizzatori hello, è possibile generare gli URL hello è toostream usato o scaricare i file. in questa esercitazione: esempio Hello restituiscono gli URL che è possibile incollare nel browser appropriato. Questa sezione fornisce brevi esempi dei diversi formati.

#### <a name="a-streaming-url-for-mpeg-dash-has-hello-following-format"></a>Un URL di streaming per MPEG DASH è hello seguente formato:

{nome endpoint di streaming-nome account servizi multimediali}.streaming.mediaservices.windows.net/{ID localizzatore}/{nome file}.ism/Manifest**(format=mpd-time-csf)**

#### <a name="a-streaming-url-for-hls-has-hello-following-format"></a>Un URL di streaming per HLS è hello seguente formato:

{nome endpoint di streaming-nome account servizi multimediali}.streaming.mediaservices.windows.net/{ID localizzatore}/{nome file}.ism/Manifest**(format=m3u8-aapl)**

#### <a name="a-streaming-url-for-smooth-streaming-has-hello-following-format"></a>Un URL di streaming per Smooth Streaming è hello seguente formato:

{nome endpoint di streaming-nome account servizi multimediali}.streaming.mediaservices.windows.net/{ID localizzatore}/{nome file}.ism/Manifest


#### <a name="a-sas-url-used-toodownload-files-has-hello-following-format"></a>Un file toodownload URL SAS usato è hello seguente formato:

{nome contenitore BLOB}/{nome asset}/{nome file}/{firma di accesso condiviso}

Le estensioni di Media Services .NET SDK forniscono metodi helper utili che restituiscono formattato gli URL per hello risorsa pubblicata.

il codice seguente Hello utilizza localizzatori toocreate .NET SDK Extensions e streaming tooget e progressivo URL di download. codice Hello Mostra anche come toodownload file tooa di cartella locale.

Aggiungere hello seguente classe Program toohello di metodo.

    static public void PublishAssetGetURLs(IAsset asset)
    {
        // Publish hello output asset by creating an Origin locator for adaptive streaming,
        // and a SAS locator for progressive download.

        _context.Locators.Create(
            LocatorType.OnDemandOrigin,
            asset,
            AccessPermissions.Read,
            TimeSpan.FromDays(30));

        _context.Locators.Create(
            LocatorType.Sas,
            asset,
            AccessPermissions.Read,
            TimeSpan.FromDays(30));


        IEnumerable<IAssetFile> mp4AssetFiles = asset
                .AssetFiles
                .ToList()
                .Where(af => af.Name.EndsWith(".mp4", StringComparison.OrdinalIgnoreCase));

        // Get hello Smooth Streaming, HLS and MPEG-DASH URLs for adaptive streaming,
        // and hello Progressive Download URL.
        Uri smoothStreamingUri = asset.GetSmoothStreamingUri();
        Uri hlsUri = asset.GetHlsUri();
        Uri mpegDashUri = asset.GetMpegDashUri();

        // Get hello URls for progressive download for each MP4 file that was generated as a result
        // of encoding.
        List<Uri> mp4ProgressiveDownloadUris = mp4AssetFiles.Select(af => af.GetSasUri()).ToList();


        // Display  hello streaming URLs.
        Console.WriteLine("Use hello following URLs for adaptive streaming: ");
        Console.WriteLine(smoothStreamingUri);
        Console.WriteLine(hlsUri);
        Console.WriteLine(mpegDashUri);
        Console.WriteLine();

        // Display hello URLs for progressive download.
        Console.WriteLine("Use hello following URLs for progressive download.");
        mp4ProgressiveDownloadUris.ForEach(uri => Console.WriteLine(uri + "\n"));
        Console.WriteLine();

        // Download hello output asset tooa local folder.
        string outputFolder = "job-output";
        if (!Directory.Exists(outputFolder))
        {
            Directory.CreateDirectory(outputFolder);
        }

        Console.WriteLine();
        Console.WriteLine("Downloading output asset files tooa local folder...");
        asset.DownloadToFolder(
            outputFolder,
            (af, p) =>
            {
                Console.WriteLine("Downloading '{0}' - Progress: {1:0.##}%", af.Name, p.Progress);
            });

        Console.WriteLine("Output asset files available at '{0}'.", Path.GetFullPath(outputFolder));
    }

## <a name="test-by-playing-your-content"></a>Testare riproducendo i contenuti.

Dopo aver eseguito il programma hello definito nella sezione precedente di hello, hello URL verrà visualizzato nella finestra di console hello seguente toohello simile.

URL per streaming adattivo:

Smooth Streaming

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest

HLS

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest(format=m3u8-aapl)

MPEG DASH

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest(format=mpd-time-csf)

URL per download progressivo (audio e video).

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_650kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_400kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_3400kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_2250kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_1500kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_1000kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_AAC_und_ch2_56kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z


toostream video, incollare l'URL nella casella di testo URL hello in hello [lettore servizi multimediali di Azure](http://amsplayer.azurewebsites.net/azuremediaplayer.html).

tootest progressivo scaricare, incollare un URL in un browser (ad esempio, Internet Explorer, Chrome o Safari).

Per ulteriori informazioni, vedere hello seguenti argomenti:

- [Riproduzione di contenuti con i lettori esistenti](media-services-playback-content-with-existing-players.md)
- [Sviluppo di applicazioni di lettore video](media-services-develop-video-players.md)
- [Integrazione di uno streaming video adattivo MPEG-DASH in un'applicazione HTML5 con DASH.js](media-services-embed-mpeg-dash-in-html5.md)

## <a name="download-sample"></a>Scaricare un esempio
esempio di codice seguente Hello contiene codice hello creato in questa esercitazione: [esempio](https://azure.microsoft.com/documentation/samples/media-services-dotnet-on-demand-encoding-with-media-encoder-standard/).

## <a name="next-steps"></a>Passaggi successivi

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornire commenti e suggerimenti
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]



<!-- Anchors. -->


<!-- URLs. -->
[Web Platform Installer]: http://go.microsoft.com/fwlink/?linkid=255386
[Portal]: http://manage.windowsazure.com/
