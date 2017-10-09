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
# <a name="get-started-with-delivering-content-on-demand-using-net-sdk"></a><span data-ttu-id="d0e8a-103">Introduzione alla distribuzione di contenuti su richiesta utilizzando .NET SDK</span><span class="sxs-lookup"><span data-stu-id="d0e8a-103">Get started with delivering content on demand using .NET SDK</span></span>
[!INCLUDE [media-services-selector-get-started](../../includes/media-services-selector-get-started.md)]

<span data-ttu-id="d0e8a-104">In questa esercitazione vengono illustrati i passaggi hello dell'implementazione di un servizio di distribuzione di contenuti video on Demand (VoD) base con l'applicazione di servizi multimediali di Azure (AMS) utilizzando hello Azure Media Services .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="d0e8a-104">This tutorial walks you through hello steps of implementing a basic Video-on-Demand (VoD) content delivery service with Azure Media Services (AMS) application using hello Azure Media Services .NET SDK.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d0e8a-105">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="d0e8a-105">Prerequisites</span></span>

<span data-ttu-id="d0e8a-106">di seguito Hello sono esercitazione hello toocomplete necessarie:</span><span class="sxs-lookup"><span data-stu-id="d0e8a-106">hello following are required toocomplete hello tutorial:</span></span>

* <span data-ttu-id="d0e8a-107">Un account Azure.</span><span class="sxs-lookup"><span data-stu-id="d0e8a-107">An Azure account.</span></span> <span data-ttu-id="d0e8a-108">Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d0e8a-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="d0e8a-109">Account di Servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="d0e8a-109">A Media Services account.</span></span> <span data-ttu-id="d0e8a-110">toocreate un account di servizi multimediali, vedere [come un Account di servizi multimediali tooCreate](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="d0e8a-110">toocreate a Media Services account, see [How tooCreate a Media Services Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="d0e8a-111">.NET Framework 4.0 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="d0e8a-111">.NET Framework 4.0 or later.</span></span>
* <span data-ttu-id="d0e8a-112">Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d0e8a-112">Visual Studio.</span></span>

<span data-ttu-id="d0e8a-113">In questa esercitazione include hello seguenti attività:</span><span class="sxs-lookup"><span data-stu-id="d0e8a-113">This tutorial includes hello following tasks:</span></span>

1. <span data-ttu-id="d0e8a-114">Avviare lo streaming di endpoint (tramite hello portale di Azure).</span><span class="sxs-lookup"><span data-stu-id="d0e8a-114">Start streaming endpoint (using hello Azure portal).</span></span>
2. <span data-ttu-id="d0e8a-115">Creare e configurare un progetto di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d0e8a-115">Create and configure a Visual Studio project.</span></span>
3. <span data-ttu-id="d0e8a-116">Connettere l'account di servizi multimediali toohello.</span><span class="sxs-lookup"><span data-stu-id="d0e8a-116">Connect toohello Media Services account.</span></span>
2. <span data-ttu-id="d0e8a-117">Caricare un file video.</span><span class="sxs-lookup"><span data-stu-id="d0e8a-117">Upload a video file.</span></span>
3. <span data-ttu-id="d0e8a-118">Codificare il file di origine hello in un set di file MP4 a velocità in bit adattiva.</span><span class="sxs-lookup"><span data-stu-id="d0e8a-118">Encode hello source file into a set of adaptive bitrate MP4 files.</span></span>
4. <span data-ttu-id="d0e8a-119">Pubblicare l'asset hello e get streaming e l'URL di download progressivo.</span><span class="sxs-lookup"><span data-stu-id="d0e8a-119">Publish hello asset and get streaming and progressive download URLs.</span></span>  
5. <span data-ttu-id="d0e8a-120">Riprodurre i contenuti.</span><span class="sxs-lookup"><span data-stu-id="d0e8a-120">Play your content.</span></span>

## <a name="overview"></a><span data-ttu-id="d0e8a-121">Panoramica</span><span class="sxs-lookup"><span data-stu-id="d0e8a-121">Overview</span></span>
<span data-ttu-id="d0e8a-122">In questa esercitazione vengono illustrati i passaggi hello di implementazione di un'applicazione di distribuzione di contenuti video on Demand (VoD) usando Azure Media Services SDK (AMS) per .NET.</span><span class="sxs-lookup"><span data-stu-id="d0e8a-122">This tutorial walks you through hello steps of implementing a Video-on-Demand (VoD) content delivery application using Azure Media Services (AMS) SDK for .NET.</span></span>

<span data-ttu-id="d0e8a-123">esercitazione Hello introduce hello base servizi multimediali del flusso di lavoro e gli oggetti di programmazione più comuni di hello e attività necessarie per lo sviluppo di servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="d0e8a-123">hello tutorial introduces hello basic Media Services workflow and hello most common programming objects and tasks required for Media Services development.</span></span> <span data-ttu-id="d0e8a-124">Al termine di hello di esercitazione hello, si verrà toostream in grado o un file multimediale di esempio che caricati, con codifica e scaricato il download progressivo.</span><span class="sxs-lookup"><span data-stu-id="d0e8a-124">At hello completion of hello tutorial, you will be able toostream or progressively download a sample media file that you uploaded, encoded, and downloaded.</span></span>

### <a name="ams-model"></a><span data-ttu-id="d0e8a-125">Modello AMS</span><span class="sxs-lookup"><span data-stu-id="d0e8a-125">AMS model</span></span>

<span data-ttu-id="d0e8a-126">Hello immagine seguente mostra alcuni degli oggetti hello più comunemente utilizzato quando si sviluppano applicazioni VoD sul modello di Media Services OData hello.</span><span class="sxs-lookup"><span data-stu-id="d0e8a-126">hello following image shows some of hello most commonly used objects when developing VoD applications against hello Media Services OData model.</span></span>

<span data-ttu-id="d0e8a-127">Fare clic su tooview immagine hello le dimensioni massime.</span><span class="sxs-lookup"><span data-stu-id="d0e8a-127">Click hello image tooview it full size.</span></span>  

<a href="./media/media-services-dotnet-get-started/media-services-overview-object-model.png" target="_blank"><img src="./media/media-services-dotnet-get-started/media-services-overview-object-model-small.png"></a> 

<span data-ttu-id="d0e8a-128">È possibile visualizzare l'intero modello hello [qui](https://media.windows.net/API/$metadata?api-version=2.15).</span><span class="sxs-lookup"><span data-stu-id="d0e8a-128">You can view hello whole model [here](https://media.windows.net/API/$metadata?api-version=2.15).</span></span>  

## <a name="start-streaming-endpoints-using-hello-azure-portal"></a><span data-ttu-id="d0e8a-129">Avviare lo streaming di endpoint che utilizzano hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="d0e8a-129">Start streaming endpoints using hello Azure portal</span></span>

<span data-ttu-id="d0e8a-130">Quando si lavora con uno degli scenari più comuni di hello recapita video tramite velocità in bit adattive servizi multimediali di Azure.</span><span class="sxs-lookup"><span data-stu-id="d0e8a-130">When working with Azure Media Services one of hello most common scenarios is delivering video via adaptive bitrate streaming.</span></span> <span data-ttu-id="d0e8a-131">Servizi multimediali fornisce creazione dinamica dei pacchetti, che consente di toodeliver la velocità in bit adattiva contenuto MP4 in formato con codificata in streaming formati supportati da servizi multimediali (MPEG DASH, HLS, Smooth Streaming) just-in-time, senza che sia necessario toostore preconfezionata versioni di ciascuno di questi formati di streaming.</span><span class="sxs-lookup"><span data-stu-id="d0e8a-131">Media Services provides dynamic packaging, which allows you toodeliver your adaptive bitrate MP4 encoded content in streaming formats supported by Media Services (MPEG DASH, HLS, Smooth Streaming) just-in-time, without you having toostore pre-packaged versions of each of these streaming formats.</span></span>

>[!NOTE]
><span data-ttu-id="d0e8a-132">Quando viene creato l'account di sistema AMS un **predefinito** endpoint di streaming viene aggiunto l'account tooyour in hello **arrestato** stato.</span><span class="sxs-lookup"><span data-stu-id="d0e8a-132">When your AMS account is created a **default** streaming endpoint is added tooyour account in hello **Stopped** state.</span></span> <span data-ttu-id="d0e8a-133">lo streaming del contenuto e intraprendere sfruttare creazione dinamica dei pacchetti e la crittografia dinamica, toostart hello endpoint di streaming da cui si desidera in hello del contenuto toostream è toobe **esecuzione** stato.</span><span class="sxs-lookup"><span data-stu-id="d0e8a-133">toostart streaming your content and take advantage of dynamic packaging and dynamic encryption, hello streaming endpoint from which you want toostream content has toobe in hello **Running** state.</span></span>

<span data-ttu-id="d0e8a-134">toostart hello endpoint di streaming, hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="d0e8a-134">toostart hello streaming endpoint, do hello following:</span></span>

1. <span data-ttu-id="d0e8a-135">Accedere all'indirizzo hello [portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="d0e8a-135">Log in at hello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="d0e8a-136">Nella finestra Impostazioni hello, fare clic su endpoint di Streaming.</span><span class="sxs-lookup"><span data-stu-id="d0e8a-136">In hello Settings window, click Streaming endpoints.</span></span>
3. <span data-ttu-id="d0e8a-137">Fare clic su predefinito hello endpoint di streaming.</span><span class="sxs-lookup"><span data-stu-id="d0e8a-137">Click hello default streaming endpoint.</span></span>

    <span data-ttu-id="d0e8a-138">verrà visualizzata la finestra Dettagli dell'ENDPOINT di STREAMING predefinito Hello.</span><span class="sxs-lookup"><span data-stu-id="d0e8a-138">hello DEFAULT STREAMING ENDPOINT DETAILS window appears.</span></span>

4. <span data-ttu-id="d0e8a-139">Fare clic sull'icona di avvio hello.</span><span class="sxs-lookup"><span data-stu-id="d0e8a-139">Click hello Start icon.</span></span>
5. <span data-ttu-id="d0e8a-140">Fare clic su toosave pulsante di hello Salva le modifiche.</span><span class="sxs-lookup"><span data-stu-id="d0e8a-140">Click hello Save button toosave your changes.</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="d0e8a-141">Creare e configurare un progetto di Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d0e8a-141">Create and configure a Visual Studio project</span></span>

1. <span data-ttu-id="d0e8a-142">Configurare l'ambiente di sviluppo e di popolare il file app. config hello con informazioni di connessione, come descritto in [lo sviluppo di servizi multimediali con .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="d0e8a-142">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 
2. <span data-ttu-id="d0e8a-143">Creare una nuova cartella (cartella può essere un punto qualsiasi nell'unità locale) e copiare un file MP4 che si desidera tooencode e flusso o il download progressivo.</span><span class="sxs-lookup"><span data-stu-id="d0e8a-143">Create a new folder (folder can be anywhere on your local drive) and copy an .mp4 file that you want tooencode and stream or progressively download.</span></span> <span data-ttu-id="d0e8a-144">In questo esempio viene utilizzato il percorso di "C:\VideoFiles" hello.</span><span class="sxs-lookup"><span data-stu-id="d0e8a-144">In this example, hello "C:\VideoFiles" path is used.</span></span>

## <a name="connect-toohello-media-services-account"></a><span data-ttu-id="d0e8a-145">Connettere l'account di servizi multimediali toohello</span><span class="sxs-lookup"><span data-stu-id="d0e8a-145">Connect toohello Media Services account</span></span>

<span data-ttu-id="d0e8a-146">Quando si usa servizi multimediali con .NET, è necessario utilizzare hello **CloudMediaContext** classe per la maggior parte dei servizi multimediali di attività di programmazione: connessione account servizi tooMedia; la creazione, aggiornamento, l'accesso e l'eliminazione seguente hello oggetti: asset, file di asset, processi, i criteri di accesso, i localizzatori, e così via.</span><span class="sxs-lookup"><span data-stu-id="d0e8a-146">When using Media Services with .NET, you must use hello **CloudMediaContext** class for most Media Services programming tasks: connecting tooMedia Services account; creating, updating, accessing, and deleting hello following objects: assets, asset files, jobs, access policies, locators, etc.</span></span>

<span data-ttu-id="d0e8a-147">Sovrascrivere classe Program predefinita di hello con hello seguente codice.</span><span class="sxs-lookup"><span data-stu-id="d0e8a-147">Overwrite hello default Program class with hello following code.</span></span> <span data-ttu-id="d0e8a-148">Hello codice viene illustrato come connessione hello tooread valori dal file app. config hello e come hello toocreate **CloudMediaContext** oggetto in ordine tooconnect tooMedia servizi.</span><span class="sxs-lookup"><span data-stu-id="d0e8a-148">hello code demonstrates how tooread hello connection values from hello App.config file and how toocreate hello **CloudMediaContext** object in order tooconnect tooMedia Services.</span></span> <span data-ttu-id="d0e8a-149">Per ulteriori informazioni, vedere [connessione toohello API di servizi multimediali](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="d0e8a-149">For more information, see [connecting toohello Media Services API](media-services-use-aad-auth-to-access-ams-api.md).</span></span>

<span data-ttu-id="d0e8a-150">Verificare che tooupdate hello file nome e percorso toowhere che è il file di supporto.</span><span class="sxs-lookup"><span data-stu-id="d0e8a-150">Make sure tooupdate hello file name and path toowhere you have your media file.</span></span>

<span data-ttu-id="d0e8a-151">Hello **Main** funzione chiama i metodi che verranno definiti più avanti in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="d0e8a-151">hello **Main** function calls methods that will be defined further in this section.</span></span>

> [!NOTE]
> <span data-ttu-id="d0e8a-152">Verranno recuperati gli errori di compilazione finché non si aggiunge le definizioni per tutte le funzioni hello.</span><span class="sxs-lookup"><span data-stu-id="d0e8a-152">You will be getting compilation errors until you add definitions for all hello functions.</span></span>

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

## <a name="create-a-new-asset-and-upload-a-video-file"></a><span data-ttu-id="d0e8a-153">Creare un nuovo asset e caricare un file video</span><span class="sxs-lookup"><span data-stu-id="d0e8a-153">Create a new asset and upload a video file</span></span>

<span data-ttu-id="d0e8a-154">In Servizi multimediali i file digitali vengono caricati (o inseriti) in un asset.</span><span class="sxs-lookup"><span data-stu-id="d0e8a-154">In Media Services, you upload (or ingest) your digital files into an asset.</span></span> <span data-ttu-id="d0e8a-155">Hello **Asset** entità può contenere video, audio, immagini, raccolte di anteprime, testo, tracce e sottotitoli file (e relativi metadati hello.)  Una volta caricati i file hello, il contenuto è archiviato in modo sicuro nel cloud hello per continuare l'elaborazione e il flusso.</span><span class="sxs-lookup"><span data-stu-id="d0e8a-155">hello **Asset** entity can contain video, audio, images, thumbnail collections, text tracks, and closed caption files (and hello metadata about these files.)  Once hello files are uploaded, your content is stored securely in hello cloud for further processing and streaming.</span></span> <span data-ttu-id="d0e8a-156">file Hello in asset hello sono denominati **file di Asset**.</span><span class="sxs-lookup"><span data-stu-id="d0e8a-156">hello files in hello asset are called **Asset Files**.</span></span>

<span data-ttu-id="d0e8a-157">Hello **UploadFile** metodo definito riportato di seguito chiama **CreateFromFile** (definito in .NET SDK Extensions).</span><span class="sxs-lookup"><span data-stu-id="d0e8a-157">hello **UploadFile** method defined below calls **CreateFromFile** (defined in .NET SDK Extensions).</span></span> <span data-ttu-id="d0e8a-158">**CreateFromFile** crea un nuovo asset in cui hello viene caricato il file di origine specificato.</span><span class="sxs-lookup"><span data-stu-id="d0e8a-158">**CreateFromFile** creates a new asset into which hello specified source file is uploaded.</span></span>

<span data-ttu-id="d0e8a-159">Hello **CreateFromFile** metodo accetta **AssetCreationOptions** che consente di specificare una delle seguenti opzioni di creazione di asset hello:</span><span class="sxs-lookup"><span data-stu-id="d0e8a-159">hello **CreateFromFile** method takes **AssetCreationOptions** which lets you specify one of hello following asset creation options:</span></span>

* <span data-ttu-id="d0e8a-160">**None** : non viene usata alcuna crittografia.</span><span class="sxs-lookup"><span data-stu-id="d0e8a-160">**None** - No encryption is used.</span></span> <span data-ttu-id="d0e8a-161">Questo è il valore di predefinito hello.</span><span class="sxs-lookup"><span data-stu-id="d0e8a-161">This is hello default value.</span></span> <span data-ttu-id="d0e8a-162">Quando si usa questa opzione, il contenuto non è protetto durante il transito, né nell'archiviazione locale.</span><span class="sxs-lookup"><span data-stu-id="d0e8a-162">Note that when using this option, your content is not protected in transit or at rest in storage.</span></span>
  <span data-ttu-id="d0e8a-163">Se si prevede di toodeliver un file MP4 tramite download progressivo, usare questa opzione.</span><span class="sxs-lookup"><span data-stu-id="d0e8a-163">If you plan toodeliver an MP4 using progressive download, use this option.</span></span>
* <span data-ttu-id="d0e8a-164">**StorageEncrypted** -utilizzare questa opzione tooencrypt il contenuto non crittografato in locale utilizzando la crittografia di Advanced Encryption Standard (AES)-256 bit, che quindi lo carica tooAzure archiviazione dove viene archiviato in forma crittografata.</span><span class="sxs-lookup"><span data-stu-id="d0e8a-164">**StorageEncrypted** - Use this option tooencrypt your clear content locally using Advanced Encryption Standard (AES)-256 bit encryption, which then uploads it tooAzure Storage where it is stored encrypted at rest.</span></span> <span data-ttu-id="d0e8a-165">Gli asset protetti con crittografia di archiviazione vengono decrittografati automaticamente e inseriti in un file crittografato sistema precedente tooencoding e, facoltativamente, crittografare nuovamente toouploading precedente come nuovo asset di output.</span><span class="sxs-lookup"><span data-stu-id="d0e8a-165">Assets protected with Storage Encryption are automatically unencrypted and placed in an encrypted file system prior tooencoding, and optionally re-encrypted prior toouploading back as a new output asset.</span></span> <span data-ttu-id="d0e8a-166">Hello primario per la crittografia di archiviazione viene usata quando si desidera toosecure i file multimediali di input di alta qualità con la crittografia avanzata inattivi sul disco.</span><span class="sxs-lookup"><span data-stu-id="d0e8a-166">hello primary use case for Storage Encryption is when you want toosecure your high-quality input media files with strong encryption at rest on disk.</span></span>
* <span data-ttu-id="d0e8a-167">**CommonEncryptionProtected** : usare questa opzione per caricare contenuti già crittografati e protetti con Common Encryption o PlayReady DRM (ad esempio, Smooth Streaming protetto con PlayReady DRM).</span><span class="sxs-lookup"><span data-stu-id="d0e8a-167">**CommonEncryptionProtected** - Use this option if you are uploading content that has already been encrypted and protected with Common Encryption or PlayReady DRM (for example, Smooth Streaming protected with PlayReady DRM).</span></span>
* <span data-ttu-id="d0e8a-168">**EnvelopeEncryptionProtected** : usare questa opzione se si stanno caricando contenuti HLS crittografati con AES.</span><span class="sxs-lookup"><span data-stu-id="d0e8a-168">**EnvelopeEncryptionProtected** – Use this option if you are uploading HLS encrypted with AES.</span></span> <span data-ttu-id="d0e8a-169">Si noti che i file hello devono sono stati codificati e crittografati da Transform Manager.</span><span class="sxs-lookup"><span data-stu-id="d0e8a-169">Note that hello files must have been encoded and encrypted by Transform Manager.</span></span>

<span data-ttu-id="d0e8a-170">Hello **CreateFromFile** metodo consente inoltre di specificare un callback in ordine tooreport hello lo stato di caricamento del file hello.</span><span class="sxs-lookup"><span data-stu-id="d0e8a-170">hello **CreateFromFile** method also lets you specify a callback in order tooreport hello upload progress of hello file.</span></span>

<span data-ttu-id="d0e8a-171">Nell'esempio seguente di hello, viene specificato **Nessuno** per le opzioni di asset hello.</span><span class="sxs-lookup"><span data-stu-id="d0e8a-171">In hello following example, we specify **None** for hello asset options.</span></span>

<span data-ttu-id="d0e8a-172">Aggiungere hello seguente classe Program toohello di metodo.</span><span class="sxs-lookup"><span data-stu-id="d0e8a-172">Add hello following method toohello Program class.</span></span>

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


## <a name="encode-hello-source-file-into-a-set-of-adaptive-bitrate-mp4-files"></a><span data-ttu-id="d0e8a-173">Codificare il file di origine hello in un set di file MP4 a velocità in bit adattiva</span><span class="sxs-lookup"><span data-stu-id="d0e8a-173">Encode hello source file into a set of adaptive bitrate MP4 files</span></span>
<span data-ttu-id="d0e8a-174">Dopo l'inserimento di asset in servizi multimediali, supporto può essere codificato, transmux filigrana e così via, prima di consegnarlo tooclients.</span><span class="sxs-lookup"><span data-stu-id="d0e8a-174">After ingesting assets into Media Services, media can be encoded, transmuxed, watermarked, and so on, before it is delivered tooclients.</span></span> <span data-ttu-id="d0e8a-175">Queste attività vengono pianificate e vengono eseguite più background ruolo istanze tooensure ad alte prestazioni e disponibilità.</span><span class="sxs-lookup"><span data-stu-id="d0e8a-175">These activities are scheduled and run against multiple background role instances tooensure high performance and availability.</span></span> <span data-ttu-id="d0e8a-176">Queste attività sono denominate processi, e ogni processo è costituito da attività atomiche che hello operazioni effettive sul file di Asset hello.</span><span class="sxs-lookup"><span data-stu-id="d0e8a-176">These activities are called Jobs, and each Job is composed of atomic Tasks that do hello actual work on hello Asset file.</span></span>

<span data-ttu-id="d0e8a-177">Come accennato in precedenza, quando si lavora con servizi multimediali di Azure, uno degli scenari più comuni di hello recapita velocità in bit adattive tooyour client.</span><span class="sxs-lookup"><span data-stu-id="d0e8a-177">As was mentioned earlier, when working with Azure Media Services, one of hello most common scenarios is delivering adaptive bitrate streaming tooyour clients.</span></span> <span data-ttu-id="d0e8a-178">Servizi multimediali può pacchetto in modo dinamico un set di file MP4 a velocità in bit adattiva in uno dei seguenti formati hello: MPEG DASH, Smooth Streaming e HTTP Live Streaming (HLS).</span><span class="sxs-lookup"><span data-stu-id="d0e8a-178">Media Services can dynamically package a set of adaptive bitrate MP4 files into one of hello following formats: HTTP Live Streaming (HLS), Smooth Streaming, and MPEG DASH.</span></span>

<span data-ttu-id="d0e8a-179">Il vantaggio di tootake creazione dinamica dei pacchetti, è necessario tooencode o eseguire la transcodifica il file mezzanine (origine) in un set di file MP4 o file Smooth Streaming a velocità in bit adattiva.</span><span class="sxs-lookup"><span data-stu-id="d0e8a-179">tootake advantage of dynamic packaging, you need tooencode or transcode your mezzanine (source) file into a set of adaptive bitrate MP4 files or adaptive bitrate Smooth Streaming files.</span></span>  

<span data-ttu-id="d0e8a-180">Hello seguente codice mostra come toosubmit una codifica del processo.</span><span class="sxs-lookup"><span data-stu-id="d0e8a-180">hello following code shows how toosubmit an encoding job.</span></span> <span data-ttu-id="d0e8a-181">processo Hello contiene un'attività che specifica i file in formato intermedio di hello tootranscode in un set di velocità in bit adattiva MP4s utilizzando **Media Encoder Standard**.</span><span class="sxs-lookup"><span data-stu-id="d0e8a-181">hello job contains one task that specifies tootranscode hello mezzanine file into a set of adaptive bitrate MP4s using **Media Encoder Standard**.</span></span> <span data-ttu-id="d0e8a-182">codice Hello invia il processo di hello e attende finché viene completato.</span><span class="sxs-lookup"><span data-stu-id="d0e8a-182">hello code submits hello job and waits until it is completed.</span></span>

<span data-ttu-id="d0e8a-183">Una volta completato il processo di hello, si è in grado di toostream l'asset o eseguire il download progressivo file MP4 che sono stati creati come risultato di transcodifica.</span><span class="sxs-lookup"><span data-stu-id="d0e8a-183">Once hello job is completed, you would be able toostream your asset or progressively download MP4 files that were created as a result of transcoding.</span></span>

<span data-ttu-id="d0e8a-184">Aggiungere hello seguente classe Program toohello di metodo.</span><span class="sxs-lookup"><span data-stu-id="d0e8a-184">Add hello following method toohello Program class.</span></span>

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

## <a name="publish-hello-asset-and-get-urls-for-streaming-and-progressive-download"></a><span data-ttu-id="d0e8a-185">Pubblicare l'asset hello e ottenere l'URL per il download progressivo e streaming</span><span class="sxs-lookup"><span data-stu-id="d0e8a-185">Publish hello asset and get URLs for streaming and progressive download</span></span>

<span data-ttu-id="d0e8a-186">toostream o scarica un asset, è innanzitutto necessario troppo "pubblicarlo" tramite la creazione di un indicatore di posizione.</span><span class="sxs-lookup"><span data-stu-id="d0e8a-186">toostream or download an asset, you first need too"publish" it by creating a locator.</span></span> <span data-ttu-id="d0e8a-187">I localizzatori forniscono accesso toofiles contenuti in hello asset.</span><span class="sxs-lookup"><span data-stu-id="d0e8a-187">Locators provide access toofiles contained in hello asset.</span></span> <span data-ttu-id="d0e8a-188">Servizi multimediali sono supportati due tipi di localizzatori: OnDemandOrigin localizzatori, supporto toostream utilizzato (ad esempio, MPEG DASH, HLS o Smooth Streaming) e localizzatori di firma di accesso (SAS), utilizzato file multimediali toodownload (per ulteriori informazioni sulla firma di accesso condiviso localizzatori vedere [questo](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/) blog).</span><span class="sxs-lookup"><span data-stu-id="d0e8a-188">Media Services supports two types of locators: OnDemandOrigin locators, used toostream media (for example, MPEG DASH, HLS, or Smooth Streaming) and Access Signature (SAS) locators, used toodownload media files (for more information about SAS locators see [this](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/) blog).</span></span>

### <a name="some-details-about-url-formats"></a><span data-ttu-id="d0e8a-189">Alcuni dettagli sui formati di URL</span><span class="sxs-lookup"><span data-stu-id="d0e8a-189">Some details about URL formats</span></span>

<span data-ttu-id="d0e8a-190">Dopo aver creato i localizzatori hello, è possibile generare gli URL hello è toostream usato o scaricare i file.</span><span class="sxs-lookup"><span data-stu-id="d0e8a-190">After you create hello locators, you can build hello URLs that would be used toostream or download your files.</span></span> <span data-ttu-id="d0e8a-191">in questa esercitazione: esempio Hello restituiscono gli URL che è possibile incollare nel browser appropriato.</span><span class="sxs-lookup"><span data-stu-id="d0e8a-191">hello sample in this tutorial will output URLs that you can paste in appropriate browsers.</span></span> <span data-ttu-id="d0e8a-192">Questa sezione fornisce brevi esempi dei diversi formati.</span><span class="sxs-lookup"><span data-stu-id="d0e8a-192">This section just gives short examples of what different formats look like.</span></span>

#### <a name="a-streaming-url-for-mpeg-dash-has-hello-following-format"></a><span data-ttu-id="d0e8a-193">Un URL di streaming per MPEG DASH è hello seguente formato:</span><span class="sxs-lookup"><span data-stu-id="d0e8a-193">A streaming URL for MPEG DASH has hello following format:</span></span>

<span data-ttu-id="d0e8a-194">{nome endpoint di streaming-nome account servizi multimediali}.streaming.mediaservices.windows.net/{ID localizzatore}/{nome file}.ism/Manifest**(format=mpd-time-csf)**</span><span class="sxs-lookup"><span data-stu-id="d0e8a-194">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest**(format=mpd-time-csf)**</span></span>

#### <a name="a-streaming-url-for-hls-has-hello-following-format"></a><span data-ttu-id="d0e8a-195">Un URL di streaming per HLS è hello seguente formato:</span><span class="sxs-lookup"><span data-stu-id="d0e8a-195">A streaming URL for HLS has hello following format:</span></span>

<span data-ttu-id="d0e8a-196">{nome endpoint di streaming-nome account servizi multimediali}.streaming.mediaservices.windows.net/{ID localizzatore}/{nome file}.ism/Manifest**(format=m3u8-aapl)**</span><span class="sxs-lookup"><span data-stu-id="d0e8a-196">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest**(format=m3u8-aapl)**</span></span>

#### <a name="a-streaming-url-for-smooth-streaming-has-hello-following-format"></a><span data-ttu-id="d0e8a-197">Un URL di streaming per Smooth Streaming è hello seguente formato:</span><span class="sxs-lookup"><span data-stu-id="d0e8a-197">A streaming URL for Smooth Streaming has hello following format:</span></span>

<span data-ttu-id="d0e8a-198">{nome endpoint di streaming-nome account servizi multimediali}.streaming.mediaservices.windows.net/{ID localizzatore}/{nome file}.ism/Manifest</span><span class="sxs-lookup"><span data-stu-id="d0e8a-198">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest</span></span>


#### <a name="a-sas-url-used-toodownload-files-has-hello-following-format"></a><span data-ttu-id="d0e8a-199">Un file toodownload URL SAS usato è hello seguente formato:</span><span class="sxs-lookup"><span data-stu-id="d0e8a-199">A SAS URL used toodownload files has hello following format:</span></span>

<span data-ttu-id="d0e8a-200">{nome contenitore BLOB}/{nome asset}/{nome file}/{firma di accesso condiviso}</span><span class="sxs-lookup"><span data-stu-id="d0e8a-200">{blob container name}/{asset name}/{file name}/{SAS signature}</span></span>

<span data-ttu-id="d0e8a-201">Le estensioni di Media Services .NET SDK forniscono metodi helper utili che restituiscono formattato gli URL per hello risorsa pubblicata.</span><span class="sxs-lookup"><span data-stu-id="d0e8a-201">Media Services .NET SDK extensions provide convenient helper methods that return formatted URLs for hello published asset.</span></span>

<span data-ttu-id="d0e8a-202">il codice seguente Hello utilizza localizzatori toocreate .NET SDK Extensions e streaming tooget e progressivo URL di download.</span><span class="sxs-lookup"><span data-stu-id="d0e8a-202">hello following code uses .NET SDK Extensions toocreate locators and tooget streaming and progressive download URLs.</span></span> <span data-ttu-id="d0e8a-203">codice Hello Mostra anche come toodownload file tooa di cartella locale.</span><span class="sxs-lookup"><span data-stu-id="d0e8a-203">hello code also shows how toodownload files tooa local folder.</span></span>

<span data-ttu-id="d0e8a-204">Aggiungere hello seguente classe Program toohello di metodo.</span><span class="sxs-lookup"><span data-stu-id="d0e8a-204">Add hello following method toohello Program class.</span></span>

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

## <a name="test-by-playing-your-content"></a><span data-ttu-id="d0e8a-205">Testare riproducendo i contenuti.</span><span class="sxs-lookup"><span data-stu-id="d0e8a-205">Test by playing your content</span></span>

<span data-ttu-id="d0e8a-206">Dopo aver eseguito il programma hello definito nella sezione precedente di hello, hello URL verrà visualizzato nella finestra di console hello seguente toohello simile.</span><span class="sxs-lookup"><span data-stu-id="d0e8a-206">Once you run hello program defined in hello previous section, hello URLs similar toohello following will be displayed in hello console window.</span></span>

<span data-ttu-id="d0e8a-207">URL per streaming adattivo:</span><span class="sxs-lookup"><span data-stu-id="d0e8a-207">Adaptive streaming URLs:</span></span>

<span data-ttu-id="d0e8a-208">Smooth Streaming</span><span class="sxs-lookup"><span data-stu-id="d0e8a-208">Smooth Streaming</span></span>

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest

<span data-ttu-id="d0e8a-209">HLS</span><span class="sxs-lookup"><span data-stu-id="d0e8a-209">HLS</span></span>

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest(format=m3u8-aapl)

<span data-ttu-id="d0e8a-210">MPEG DASH</span><span class="sxs-lookup"><span data-stu-id="d0e8a-210">MPEG DASH</span></span>

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest(format=mpd-time-csf)

<span data-ttu-id="d0e8a-211">URL per download progressivo (audio e video).</span><span class="sxs-lookup"><span data-stu-id="d0e8a-211">Progressive download URLs (audio and video).</span></span>

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_650kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_400kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_3400kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_2250kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_1500kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_1000kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_AAC_und_ch2_56kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z


<span data-ttu-id="d0e8a-212">toostream video, incollare l'URL nella casella di testo URL hello in hello [lettore servizi multimediali di Azure](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span><span class="sxs-lookup"><span data-stu-id="d0e8a-212">toostream your video, paste your URL in hello URL textbox in hello [Azure Media Services Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span>

<span data-ttu-id="d0e8a-213">tootest progressivo scaricare, incollare un URL in un browser (ad esempio, Internet Explorer, Chrome o Safari).</span><span class="sxs-lookup"><span data-stu-id="d0e8a-213">tootest progressive download, paste a URL into a browser (for example, Internet Explorer, Chrome, or Safari).</span></span>

<span data-ttu-id="d0e8a-214">Per ulteriori informazioni, vedere hello seguenti argomenti:</span><span class="sxs-lookup"><span data-stu-id="d0e8a-214">For more information, see hello following topics:</span></span>

- [<span data-ttu-id="d0e8a-215">Riproduzione di contenuti con i lettori esistenti</span><span class="sxs-lookup"><span data-stu-id="d0e8a-215">Playing your content with existing players</span></span>](media-services-playback-content-with-existing-players.md)
- [<span data-ttu-id="d0e8a-216">Sviluppo di applicazioni di lettore video</span><span class="sxs-lookup"><span data-stu-id="d0e8a-216">Develop video player applications</span></span>](media-services-develop-video-players.md)
- [<span data-ttu-id="d0e8a-217">Integrazione di uno streaming video adattivo MPEG-DASH in un'applicazione HTML5 con DASH.js</span><span class="sxs-lookup"><span data-stu-id="d0e8a-217">Embedding a MPEG-DASH Adaptive Streaming Video in an HTML5 Application with DASH.js</span></span>](media-services-embed-mpeg-dash-in-html5.md)

## <a name="download-sample"></a><span data-ttu-id="d0e8a-218">Scaricare un esempio</span><span class="sxs-lookup"><span data-stu-id="d0e8a-218">Download sample</span></span>
<span data-ttu-id="d0e8a-219">esempio di codice seguente Hello contiene codice hello creato in questa esercitazione: [esempio](https://azure.microsoft.com/documentation/samples/media-services-dotnet-on-demand-encoding-with-media-encoder-standard/).</span><span class="sxs-lookup"><span data-stu-id="d0e8a-219">hello following code sample contains hello code that you created in this tutorial: [sample](https://azure.microsoft.com/documentation/samples/media-services-dotnet-on-demand-encoding-with-media-encoder-standard/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d0e8a-220">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d0e8a-220">Next Steps</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="d0e8a-221">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="d0e8a-221">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]



<!-- Anchors. -->


<!-- URLs. -->
[Web Platform Installer]: http://go.microsoft.com/fwlink/?linkid=255386
[Portal]: http://manage.windowsazure.com/
