---
title: Introduzione alla distribuzione di contenuto su richiesta con .NET | Documentazione di Microsoft
description: Questa esercitazione illustra il processo di implementazione di un'applicazione di distribuzione di contenuti su richiesta con Servizi multimediali di Azure tramite .NET.
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
ms.openlocfilehash: f0be787ba1ccee067fb1d7e6a6554be32f886089
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-delivering-content-on-demand-using-net-sdk"></a><span data-ttu-id="ddbfd-103">Introduzione alla distribuzione di contenuti su richiesta utilizzando .NET SDK</span><span class="sxs-lookup"><span data-stu-id="ddbfd-103">Get started with delivering content on demand using .NET SDK</span></span>
[!INCLUDE [media-services-selector-get-started](../../includes/media-services-selector-get-started.md)]

<span data-ttu-id="ddbfd-104">Questa esercitazione illustra il processo di implementazione di un servizio per la distribuzione di contenuto video on demand (VoD) di base con l'applicazione Servizi multimediali di Azure (AMS) usando Azure Media Services .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="ddbfd-104">This tutorial walks you through the steps of implementing a basic Video-on-Demand (VoD) content delivery service with Azure Media Services (AMS) application using the Azure Media Services .NET SDK.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ddbfd-105">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="ddbfd-105">Prerequisites</span></span>

<span data-ttu-id="ddbfd-106">Per completare l'esercitazione è necessario quanto segue:</span><span class="sxs-lookup"><span data-stu-id="ddbfd-106">The following are required to complete the tutorial:</span></span>

* <span data-ttu-id="ddbfd-107">Un account Azure.</span><span class="sxs-lookup"><span data-stu-id="ddbfd-107">An Azure account.</span></span> <span data-ttu-id="ddbfd-108">Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ddbfd-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="ddbfd-109">Account di Servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="ddbfd-109">A Media Services account.</span></span> <span data-ttu-id="ddbfd-110">Per creare un account Servizi multimediali, vedere [Creare un account Servizi multimediali di Azure con il portale di Azure](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="ddbfd-110">To create a Media Services account, see [How to Create a Media Services Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="ddbfd-111">.NET Framework 4.0 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="ddbfd-111">.NET Framework 4.0 or later.</span></span>
* <span data-ttu-id="ddbfd-112">Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ddbfd-112">Visual Studio.</span></span>

<span data-ttu-id="ddbfd-113">Questa esercitazione include le attività seguenti:</span><span class="sxs-lookup"><span data-stu-id="ddbfd-113">This tutorial includes the following tasks:</span></span>

1. <span data-ttu-id="ddbfd-114">Avviare l'endpoint di streaming usando il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="ddbfd-114">Start streaming endpoint (using the Azure portal).</span></span>
2. <span data-ttu-id="ddbfd-115">Creare e configurare un progetto di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ddbfd-115">Create and configure a Visual Studio project.</span></span>
3. <span data-ttu-id="ddbfd-116">Connettersi all'account di Servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="ddbfd-116">Connect to the Media Services account.</span></span>
2. <span data-ttu-id="ddbfd-117">Caricare un file video.</span><span class="sxs-lookup"><span data-stu-id="ddbfd-117">Upload a video file.</span></span>
3. <span data-ttu-id="ddbfd-118">Codificare il file di origine in un set di file MP4 a velocità in bit adattiva.</span><span class="sxs-lookup"><span data-stu-id="ddbfd-118">Encode the source file into a set of adaptive bitrate MP4 files.</span></span>
4. <span data-ttu-id="ddbfd-119">Pubblicare l'asset e ottenere gli URL di streaming e di download progressivo.</span><span class="sxs-lookup"><span data-stu-id="ddbfd-119">Publish the asset and get streaming and progressive download URLs.</span></span>  
5. <span data-ttu-id="ddbfd-120">Riprodurre i contenuti.</span><span class="sxs-lookup"><span data-stu-id="ddbfd-120">Play your content.</span></span>

## <a name="overview"></a><span data-ttu-id="ddbfd-121">Panoramica</span><span class="sxs-lookup"><span data-stu-id="ddbfd-121">Overview</span></span>
<span data-ttu-id="ddbfd-122">Questa esercitazione illustra il processo di implementazione di un'applicazione di distribuzione di contenuti Video on Demand (VoD) usando l'SDK di Servizi multimediali di Azure per .NET.</span><span class="sxs-lookup"><span data-stu-id="ddbfd-122">This tutorial walks you through the steps of implementing a Video-on-Demand (VoD) content delivery application using Azure Media Services (AMS) SDK for .NET.</span></span>

<span data-ttu-id="ddbfd-123">L'esercitazione descrive il flusso di lavoro di base di Servizi multimediali nonché gli oggetti e le attività di programmazione usati più di frequente per lo sviluppo basato su Servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="ddbfd-123">The tutorial introduces the basic Media Services workflow and the most common programming objects and tasks required for Media Services development.</span></span> <span data-ttu-id="ddbfd-124">Al termine dell'esercitazione sarà possibile eseguire lo streaming o il download progressivo di un file multimediale di esempio caricato, codificato e scaricato.</span><span class="sxs-lookup"><span data-stu-id="ddbfd-124">At the completion of the tutorial, you will be able to stream or progressively download a sample media file that you uploaded, encoded, and downloaded.</span></span>

### <a name="ams-model"></a><span data-ttu-id="ddbfd-125">Modello AMS</span><span class="sxs-lookup"><span data-stu-id="ddbfd-125">AMS model</span></span>

<span data-ttu-id="ddbfd-126">L'immagine seguente illustra alcuni degli oggetti più comuni usati durante lo sviluppo di applicazioni VoD rispetto al modello OData di Servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="ddbfd-126">The following image shows some of the most commonly used objects when developing VoD applications against the Media Services OData model.</span></span>

<span data-ttu-id="ddbfd-127">Fare clic sull'immagine per visualizzarla a schermo intero.</span><span class="sxs-lookup"><span data-stu-id="ddbfd-127">Click the image to view it full size.</span></span>  

<a href="./media/media-services-dotnet-get-started/media-services-overview-object-model.png" target="_blank"><img src="./media/media-services-dotnet-get-started/media-services-overview-object-model-small.png"></a> 

<span data-ttu-id="ddbfd-128">È possibile visualizzare il modello completo [qui](https://media.windows.net/API/$metadata?api-version=2.15).</span><span class="sxs-lookup"><span data-stu-id="ddbfd-128">You can view the whole model [here](https://media.windows.net/API/$metadata?api-version=2.15).</span></span>  

## <a name="start-streaming-endpoints-using-the-azure-portal"></a><span data-ttu-id="ddbfd-129">Avviare endpoint di streaming usando il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="ddbfd-129">Start streaming endpoints using the Azure portal</span></span>

<span data-ttu-id="ddbfd-130">Uno degli scenari più frequenti dell'uso di Servizi multimediali di Azure riguarda la distribuzione di contenuto video in streaming a bitrate adattivo.</span><span class="sxs-lookup"><span data-stu-id="ddbfd-130">When working with Azure Media Services one of the most common scenarios is delivering video via adaptive bitrate streaming.</span></span> <span data-ttu-id="ddbfd-131">Servizi multimediali include la funzionalità per la creazione dinamica dei pacchetti, che consente di distribuire contenuto con codifica MP4 a bitrate adattivo nei formati supportati da Servizi multimediali, come MPEG DASH, HLS e Smooth Streaming in modalità JIT, senza dover archiviare le versioni predefinite di ognuno di questi formati di streaming.</span><span class="sxs-lookup"><span data-stu-id="ddbfd-131">Media Services provides dynamic packaging, which allows you to deliver your adaptive bitrate MP4 encoded content in streaming formats supported by Media Services (MPEG DASH, HLS, Smooth Streaming) just-in-time, without you having to store pre-packaged versions of each of these streaming formats.</span></span>

>[!NOTE]
><span data-ttu-id="ddbfd-132">Quando l'account AMS viene creato, un endpoint di streaming **predefinito** viene aggiunto all'account con stato **Arrestato**.</span><span class="sxs-lookup"><span data-stu-id="ddbfd-132">When your AMS account is created a **default** streaming endpoint is added to your account in the **Stopped** state.</span></span> <span data-ttu-id="ddbfd-133">Per avviare lo streaming del contenuto e sfruttare i vantaggi della creazione dinamica dei pacchetti e della crittografia dinamica, l'endpoint di streaming da cui si vuole trasmettere il contenuto deve essere nello stato **In esecuzione**.</span><span class="sxs-lookup"><span data-stu-id="ddbfd-133">To start streaming your content and take advantage of dynamic packaging and dynamic encryption, the streaming endpoint from which you want to stream content has to be in the **Running** state.</span></span>

<span data-ttu-id="ddbfd-134">Per avviare l'endpoint di streaming, eseguire queste operazioni:</span><span class="sxs-lookup"><span data-stu-id="ddbfd-134">To start the streaming endpoint, do the following:</span></span>

1. <span data-ttu-id="ddbfd-135">Accedere al [portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="ddbfd-135">Log in at the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="ddbfd-136">Nella finestra Impostazioni fare clic su Endpoint di streaming.</span><span class="sxs-lookup"><span data-stu-id="ddbfd-136">In the Settings window, click Streaming endpoints.</span></span>
3. <span data-ttu-id="ddbfd-137">Fare clic sull'endpoint di streaming predefinito.</span><span class="sxs-lookup"><span data-stu-id="ddbfd-137">Click the default streaming endpoint.</span></span>

    <span data-ttu-id="ddbfd-138">Verrà visualizzata la finestra DETTAGLI ENDPOINT DI STREAMING PREDEFINITO.</span><span class="sxs-lookup"><span data-stu-id="ddbfd-138">The DEFAULT STREAMING ENDPOINT DETAILS window appears.</span></span>

4. <span data-ttu-id="ddbfd-139">Fare clic sull'icona di avvio.</span><span class="sxs-lookup"><span data-stu-id="ddbfd-139">Click the Start icon.</span></span>
5. <span data-ttu-id="ddbfd-140">Fare clic sul pulsante Salva per salvare le modifiche apportate.</span><span class="sxs-lookup"><span data-stu-id="ddbfd-140">Click the Save button to save your changes.</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="ddbfd-141">Creare e configurare un progetto di Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ddbfd-141">Create and configure a Visual Studio project</span></span>

1. <span data-ttu-id="ddbfd-142">Configurare l'ambiente di sviluppo e popolare il file app.config con le informazioni di connessione, come descritto in [Sviluppo di applicazioni di Servizi multimediali con .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="ddbfd-142">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 
2. <span data-ttu-id="ddbfd-143">Creare una nuova cartella, in un punto qualsiasi nell'unità locale, e copiare un file con estensione mp4 di cui eseguire codifica e streaming o il download progressivo.</span><span class="sxs-lookup"><span data-stu-id="ddbfd-143">Create a new folder (folder can be anywhere on your local drive) and copy an .mp4 file that you want to encode and stream or progressively download.</span></span> <span data-ttu-id="ddbfd-144">In questo esempio viene usato il percorso "C:\VideoFiles".</span><span class="sxs-lookup"><span data-stu-id="ddbfd-144">In this example, the "C:\VideoFiles" path is used.</span></span>

## <a name="connect-to-the-media-services-account"></a><span data-ttu-id="ddbfd-145">Connettersi all'account di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="ddbfd-145">Connect to the Media Services account</span></span>

<span data-ttu-id="ddbfd-146">Quando si usa Servizi multimediali con .NET, è necessario usare la classe **CloudMediaContext** per la maggior parte delle attività di programmazione di Servizi multimediali: connessione all'account di Servizi multimediali, creazione, aggiornamento, accesso ed eliminazione dei seguenti oggetti: asset, file di asset, processi, criteri di accesso, localizzatori e così via.</span><span class="sxs-lookup"><span data-stu-id="ddbfd-146">When using Media Services with .NET, you must use the **CloudMediaContext** class for most Media Services programming tasks: connecting to Media Services account; creating, updating, accessing, and deleting the following objects: assets, asset files, jobs, access policies, locators, etc.</span></span>

<span data-ttu-id="ddbfd-147">Sovrascrivere la classe predefinita Program con il codice seguente.</span><span class="sxs-lookup"><span data-stu-id="ddbfd-147">Overwrite the default Program class with the following code.</span></span> <span data-ttu-id="ddbfd-148">Il codice mostra come leggere i valori di connessione dal file App.config e come creare l'oggetto **CloudMediaContext** per connettersi a Servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="ddbfd-148">The code demonstrates how to read the connection values from the App.config file and how to create the **CloudMediaContext** object in order to connect to Media Services.</span></span> <span data-ttu-id="ddbfd-149">Per altre informazioni, vedere la [connessione all'API Servizi multimediali](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="ddbfd-149">For more information, see [connecting to the Media Services API](media-services-use-aad-auth-to-access-ams-api.md).</span></span>

<span data-ttu-id="ddbfd-150">Assicurarsi di aggiornare il nome file e il percorso in cui salvare il file multimediale.</span><span class="sxs-lookup"><span data-stu-id="ddbfd-150">Make sure to update the file name and path to where you have your media file.</span></span>

<span data-ttu-id="ddbfd-151">La funzione **Main** chiama metodi che verranno definiti più in dettaglio in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="ddbfd-151">The **Main** function calls methods that will be defined further in this section.</span></span>

> [!NOTE]
> <span data-ttu-id="ddbfd-152">Verranno visualizzati errori di compilazione finché si aggiungono definizioni per tutte le funzioni.</span><span class="sxs-lookup"><span data-stu-id="ddbfd-152">You will be getting compilation errors until you add definitions for all the functions.</span></span>

    class Program
    {
        // Read values from the App.config file.
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

            // Add calls to methods defined in this section.
            // Make sure to update the file name and path to where you have your media file.
            IAsset inputAsset =
            UploadFile(@"C:\VideoFiles\BigBuckBunny.mp4", AssetCreationOptions.None);

            IAsset encodedAsset =
            EncodeToAdaptiveBitrateMP4s(inputAsset, AssetCreationOptions.None);

            PublishAssetGetURLs(encodedAsset);
        }
        catch (Exception exception)
        {
            // Parse the XML error message in the Media Services response and create a new
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

## <a name="create-a-new-asset-and-upload-a-video-file"></a><span data-ttu-id="ddbfd-153">Creare un nuovo asset e caricare un file video</span><span class="sxs-lookup"><span data-stu-id="ddbfd-153">Create a new asset and upload a video file</span></span>

<span data-ttu-id="ddbfd-154">In Servizi multimediali i file digitali vengono caricati (o inseriti) in un asset.</span><span class="sxs-lookup"><span data-stu-id="ddbfd-154">In Media Services, you upload (or ingest) your digital files into an asset.</span></span> <span data-ttu-id="ddbfd-155">L'entità **Asset** può contenere video, audio, immagini, raccolte di anteprime, tracce di testo e file di sottotitoli codificati, oltre ai metadati relativi a questi file.  Dopo aver caricato i file, i contenuti vengono archiviati in modo sicuro nel cloud per altre operazioni di elaborazione e streaming.</span><span class="sxs-lookup"><span data-stu-id="ddbfd-155">The **Asset** entity can contain video, audio, images, thumbnail collections, text tracks, and closed caption files (and the metadata about these files.)  Once the files are uploaded, your content is stored securely in the cloud for further processing and streaming.</span></span> <span data-ttu-id="ddbfd-156">I file nell'asset sono denominati **File di asset**.</span><span class="sxs-lookup"><span data-stu-id="ddbfd-156">The files in the asset are called **Asset Files**.</span></span>

<span data-ttu-id="ddbfd-157">Il metodo **UploadFile** definito di seguito chiama **CreateFromFile**, definito in .NET SDK Extensions.</span><span class="sxs-lookup"><span data-stu-id="ddbfd-157">The **UploadFile** method defined below calls **CreateFromFile** (defined in .NET SDK Extensions).</span></span> <span data-ttu-id="ddbfd-158">**CreateFromFile** crea un nuovo asset in cui viene caricato il file di origine specificato.</span><span class="sxs-lookup"><span data-stu-id="ddbfd-158">**CreateFromFile** creates a new asset into which the specified source file is uploaded.</span></span>

<span data-ttu-id="ddbfd-159">Il metodo **CreateFromFile** acquisisce **AssetCreationOptions**, che consente di specificare una delle opzioni di creazione seguenti:</span><span class="sxs-lookup"><span data-stu-id="ddbfd-159">The **CreateFromFile** method takes **AssetCreationOptions** which lets you specify one of the following asset creation options:</span></span>

* <span data-ttu-id="ddbfd-160">**None** : non viene usata alcuna crittografia.</span><span class="sxs-lookup"><span data-stu-id="ddbfd-160">**None** - No encryption is used.</span></span> <span data-ttu-id="ddbfd-161">Si tratta del valore predefinito.</span><span class="sxs-lookup"><span data-stu-id="ddbfd-161">This is the default value.</span></span> <span data-ttu-id="ddbfd-162">Quando si usa questa opzione, il contenuto non è protetto durante il transito, né nell'archiviazione locale.</span><span class="sxs-lookup"><span data-stu-id="ddbfd-162">Note that when using this option, your content is not protected in transit or at rest in storage.</span></span>
  <span data-ttu-id="ddbfd-163">Se si pianifica la distribuzione di un file MP4 con il download progressivo, usare questa opzione.</span><span class="sxs-lookup"><span data-stu-id="ddbfd-163">If you plan to deliver an MP4 using progressive download, use this option.</span></span>
* <span data-ttu-id="ddbfd-164">**StorageEncrypted** : usare questa opzione per crittografare localmente il contenuto non crittografato applicando la crittografia AES (Advanced Encryption Standard) a 256 bit e quindi caricarlo nel servizio Archiviazione di Azure, in cui viene archiviato in forma crittografata.</span><span class="sxs-lookup"><span data-stu-id="ddbfd-164">**StorageEncrypted** - Use this option to encrypt your clear content locally using Advanced Encryption Standard (AES)-256 bit encryption, which then uploads it to Azure Storage where it is stored encrypted at rest.</span></span> <span data-ttu-id="ddbfd-165">Gli asset protetti con la crittografia di archiviazione vengono decrittografati automaticamente e inseriti in un file system crittografato prima della codifica, quindi ricrittografati facoltativamente prima di essere ricaricati di nuovo come nuovo asset di output.</span><span class="sxs-lookup"><span data-stu-id="ddbfd-165">Assets protected with Storage Encryption are automatically unencrypted and placed in an encrypted file system prior to encoding, and optionally re-encrypted prior to uploading back as a new output asset.</span></span> <span data-ttu-id="ddbfd-166">La crittografia di archiviazione viene usata principalmente quando si vogliono proteggere i file multimediali con input di alta qualità con una crittografia avanzata sul disco locale.</span><span class="sxs-lookup"><span data-stu-id="ddbfd-166">The primary use case for Storage Encryption is when you want to secure your high-quality input media files with strong encryption at rest on disk.</span></span>
* <span data-ttu-id="ddbfd-167">**CommonEncryptionProtected** : usare questa opzione per caricare contenuti già crittografati e protetti con Common Encryption o PlayReady DRM (ad esempio, Smooth Streaming protetto con PlayReady DRM).</span><span class="sxs-lookup"><span data-stu-id="ddbfd-167">**CommonEncryptionProtected** - Use this option if you are uploading content that has already been encrypted and protected with Common Encryption or PlayReady DRM (for example, Smooth Streaming protected with PlayReady DRM).</span></span>
* <span data-ttu-id="ddbfd-168">**EnvelopeEncryptionProtected** : usare questa opzione se si stanno caricando contenuti HLS crittografati con AES.</span><span class="sxs-lookup"><span data-stu-id="ddbfd-168">**EnvelopeEncryptionProtected** – Use this option if you are uploading HLS encrypted with AES.</span></span> <span data-ttu-id="ddbfd-169">I file devono essere stati codificati e crittografati da Transform Manager.</span><span class="sxs-lookup"><span data-stu-id="ddbfd-169">Note that the files must have been encoded and encrypted by Transform Manager.</span></span>

<span data-ttu-id="ddbfd-170">Il metodo **CreateFromFile** consente anche di specificare un callback per visualizzare l'avanzamento del caricamento del file.</span><span class="sxs-lookup"><span data-stu-id="ddbfd-170">The **CreateFromFile** method also lets you specify a callback in order to report the upload progress of the file.</span></span>

<span data-ttu-id="ddbfd-171">Nell'esempio seguente è specificato **None** per le opzioni dell'asset.</span><span class="sxs-lookup"><span data-stu-id="ddbfd-171">In the following example, we specify **None** for the asset options.</span></span>

<span data-ttu-id="ddbfd-172">Aggiungere il seguente metodo alla classe Program.</span><span class="sxs-lookup"><span data-stu-id="ddbfd-172">Add the following method to the Program class.</span></span>

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


## <a name="encode-the-source-file-into-a-set-of-adaptive-bitrate-mp4-files"></a><span data-ttu-id="ddbfd-173">Codificare il file di origine in un set di file MP4 a velocità in bit adattiva</span><span class="sxs-lookup"><span data-stu-id="ddbfd-173">Encode the source file into a set of adaptive bitrate MP4 files</span></span>
<span data-ttu-id="ddbfd-174">Dopo aver inserito gli asset in Servizi multimediali, i file multimediali possono essere codificati, sottoposti a transmux e all'applicazione di filigrana e così via prima di essere distribuiti ai client.</span><span class="sxs-lookup"><span data-stu-id="ddbfd-174">After ingesting assets into Media Services, media can be encoded, transmuxed, watermarked, and so on, before it is delivered to clients.</span></span> <span data-ttu-id="ddbfd-175">Queste attività vengono pianificate ed eseguite in più istanze del ruolo in background per assicurare prestazioni e disponibilità elevate.</span><span class="sxs-lookup"><span data-stu-id="ddbfd-175">These activities are scheduled and run against multiple background role instances to ensure high performance and availability.</span></span> <span data-ttu-id="ddbfd-176">Queste attività vengono chiamate processi. Ogni processo è formato da attività atomiche che svolgono le procedure effettive nel file di asset.</span><span class="sxs-lookup"><span data-stu-id="ddbfd-176">These activities are called Jobs, and each Job is composed of atomic Tasks that do the actual work on the Asset file.</span></span>

<span data-ttu-id="ddbfd-177">Come indicato prima, quando si usa Servizi multimediali di Azure, uno degli scenari più frequenti consiste nella distribuzione di contenuti in streaming a velocità in bit adattiva ai client.</span><span class="sxs-lookup"><span data-stu-id="ddbfd-177">As was mentioned earlier, when working with Azure Media Services, one of the most common scenarios is delivering adaptive bitrate streaming to your clients.</span></span> <span data-ttu-id="ddbfd-178">Servizi multimediali può creare dinamicamente un pacchetto di un set di file MP4 a velocità in bit adattiva in uno dei formati seguenti: HTTP Live Streaming (HLS), Smooth Streaming e MPEG DASH.</span><span class="sxs-lookup"><span data-stu-id="ddbfd-178">Media Services can dynamically package a set of adaptive bitrate MP4 files into one of the following formats: HTTP Live Streaming (HLS), Smooth Streaming, and MPEG DASH.</span></span>

<span data-ttu-id="ddbfd-179">Per sfruttare la creazione dinamica dei pacchetti è necessario codificare o transcodificare il file in formato intermedio (di origine) in un set di file MP4 o Smooth Streaming a bitrate adattivo.</span><span class="sxs-lookup"><span data-stu-id="ddbfd-179">To take advantage of dynamic packaging, you need to encode or transcode your mezzanine (source) file into a set of adaptive bitrate MP4 files or adaptive bitrate Smooth Streaming files.</span></span>  

<span data-ttu-id="ddbfd-180">Il seguente codice mostra come inviare un processo di codifica.</span><span class="sxs-lookup"><span data-stu-id="ddbfd-180">The following code shows how to submit an encoding job.</span></span> <span data-ttu-id="ddbfd-181">Il processo contiene un'attività che indica di transcodificare il file in formato intermedio in un set di file MP4 a velocità in bit adattiva con **Media Encoder Standard**.</span><span class="sxs-lookup"><span data-stu-id="ddbfd-181">The job contains one task that specifies to transcode the mezzanine file into a set of adaptive bitrate MP4s using **Media Encoder Standard**.</span></span> <span data-ttu-id="ddbfd-182">Il codice invia il processo e ne attende il completamento.</span><span class="sxs-lookup"><span data-stu-id="ddbfd-182">The code submits the job and waits until it is completed.</span></span>

<span data-ttu-id="ddbfd-183">Al termine, è possibile eseguire lo streaming dell'asset o il download progressivo dei file MP4 creati con la transcodifica.</span><span class="sxs-lookup"><span data-stu-id="ddbfd-183">Once the job is completed, you would be able to stream your asset or progressively download MP4 files that were created as a result of transcoding.</span></span>

<span data-ttu-id="ddbfd-184">Aggiungere il seguente metodo alla classe Program.</span><span class="sxs-lookup"><span data-stu-id="ddbfd-184">Add the following method to the Program class.</span></span>

    static public IAsset EncodeToAdaptiveBitrateMP4s(IAsset asset, AssetCreationOptions options)
    {

        // Prepare a job with a single task to transcode the specified asset
        // into a multi-bitrate asset.

        IJob job = _context.Jobs.CreateWithSingleTask(
            "Media Encoder Standard",
            "Adaptive Streaming",
            asset,
            "Adaptive Bitrate MP4",
            options);

        Console.WriteLine("Submitting transcoding job...");


        // Submit the job and wait until it is completed.
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

## <a name="publish-the-asset-and-get-urls-for-streaming-and-progressive-download"></a><span data-ttu-id="ddbfd-185">Pubblicare l'asset e ottenere gli URL di streaming e di download progressivo</span><span class="sxs-lookup"><span data-stu-id="ddbfd-185">Publish the asset and get URLs for streaming and progressive download</span></span>

<span data-ttu-id="ddbfd-186">Per eseguire lo streaming o il download di un asset è necessario prima "pubblicarlo" creando un localizzatore.</span><span class="sxs-lookup"><span data-stu-id="ddbfd-186">To stream or download an asset, you first need to "publish" it by creating a locator.</span></span> <span data-ttu-id="ddbfd-187">I localizzatori forniscono l'accesso ai file contenuti nell'asset.</span><span class="sxs-lookup"><span data-stu-id="ddbfd-187">Locators provide access to files contained in the asset.</span></span> <span data-ttu-id="ddbfd-188">Servizi multimediali supporta due tipi di localizzatori: localizzatori OnDemandOrigin, usati per lo streaming dei file multimediali (ad esempio, MPEG DASH, HLS o Smooth Streaming) e localizzatori di firma di accesso condiviso, usati per scaricare i file multimediali. Per altre informazioni sui localizzatori di firma di accesso condiviso, vedere [questo](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/) blog.</span><span class="sxs-lookup"><span data-stu-id="ddbfd-188">Media Services supports two types of locators: OnDemandOrigin locators, used to stream media (for example, MPEG DASH, HLS, or Smooth Streaming) and Access Signature (SAS) locators, used to download media files (for more information about SAS locators see [this](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/) blog).</span></span>

### <a name="some-details-about-url-formats"></a><span data-ttu-id="ddbfd-189">Alcuni dettagli sui formati di URL</span><span class="sxs-lookup"><span data-stu-id="ddbfd-189">Some details about URL formats</span></span>

<span data-ttu-id="ddbfd-190">Dopo aver creato i localizzatori, è possibile compilare gli URL usati per eseguire lo streaming o il download dei file.</span><span class="sxs-lookup"><span data-stu-id="ddbfd-190">After you create the locators, you can build the URLs that would be used to stream or download your files.</span></span> <span data-ttu-id="ddbfd-191">L'esempio in questa esercitazione restituirà URL che possono essere incollati nei browser appropriati.</span><span class="sxs-lookup"><span data-stu-id="ddbfd-191">The sample in this tutorial will output URLs that you can paste in appropriate browsers.</span></span> <span data-ttu-id="ddbfd-192">Questa sezione fornisce brevi esempi dei diversi formati.</span><span class="sxs-lookup"><span data-stu-id="ddbfd-192">This section just gives short examples of what different formats look like.</span></span>

#### <a name="a-streaming-url-for-mpeg-dash-has-the-following-format"></a><span data-ttu-id="ddbfd-193">Un URL di streaming per MPEG DASH ha il seguente formato:</span><span class="sxs-lookup"><span data-stu-id="ddbfd-193">A streaming URL for MPEG DASH has the following format:</span></span>

<span data-ttu-id="ddbfd-194">{nome endpoint di streaming-nome account servizi multimediali}.streaming.mediaservices.windows.net/{ID localizzatore}/{nome file}.ism/Manifest**(format=mpd-time-csf)**</span><span class="sxs-lookup"><span data-stu-id="ddbfd-194">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest**(format=mpd-time-csf)**</span></span>

#### <a name="a-streaming-url-for-hls-has-the-following-format"></a><span data-ttu-id="ddbfd-195">Un URL di streaming per HLS ha il seguente formato:</span><span class="sxs-lookup"><span data-stu-id="ddbfd-195">A streaming URL for HLS has the following format:</span></span>

<span data-ttu-id="ddbfd-196">{nome endpoint di streaming-nome account servizi multimediali}.streaming.mediaservices.windows.net/{ID localizzatore}/{nome file}.ism/Manifest**(format=m3u8-aapl)**</span><span class="sxs-lookup"><span data-stu-id="ddbfd-196">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest**(format=m3u8-aapl)**</span></span>

#### <a name="a-streaming-url-for-smooth-streaming-has-the-following-format"></a><span data-ttu-id="ddbfd-197">Un URL di streaming per Smooth Streaming ha il seguente formato:</span><span class="sxs-lookup"><span data-stu-id="ddbfd-197">A streaming URL for Smooth Streaming has the following format:</span></span>

<span data-ttu-id="ddbfd-198">{nome endpoint di streaming-nome account servizi multimediali}.streaming.mediaservices.windows.net/{ID localizzatore}/{nome file}.ism/Manifest</span><span class="sxs-lookup"><span data-stu-id="ddbfd-198">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest</span></span>


#### <a name="a-sas-url-used-to-download-files-has-the-following-format"></a><span data-ttu-id="ddbfd-199">Un URL di firma di accesso condiviso usato per scaricare i file ha il seguente formato:</span><span class="sxs-lookup"><span data-stu-id="ddbfd-199">A SAS URL used to download files has the following format:</span></span>

<span data-ttu-id="ddbfd-200">{nome contenitore BLOB}/{nome asset}/{nome file}/{firma di accesso condiviso}</span><span class="sxs-lookup"><span data-stu-id="ddbfd-200">{blob container name}/{asset name}/{file name}/{SAS signature}</span></span>

<span data-ttu-id="ddbfd-201">Le estensioni dell'SDK di Servizi multimediali per .NET forniscono pratici metodi di supporto che restituiscono URL formattati per l'asset pubblicato.</span><span class="sxs-lookup"><span data-stu-id="ddbfd-201">Media Services .NET SDK extensions provide convenient helper methods that return formatted URLs for the published asset.</span></span>

<span data-ttu-id="ddbfd-202">Il codice seguente usa le estensioni dell'SDK per .NET per creare i localizzatori e ottenere URL per lo streaming e il download progressivo.</span><span class="sxs-lookup"><span data-stu-id="ddbfd-202">The following code uses .NET SDK Extensions to create locators and to get streaming and progressive download URLs.</span></span> <span data-ttu-id="ddbfd-203">Il codice mostra anche come scaricare i file in una cartella locale.</span><span class="sxs-lookup"><span data-stu-id="ddbfd-203">The code also shows how to download files to a local folder.</span></span>

<span data-ttu-id="ddbfd-204">Aggiungere il seguente metodo alla classe Program.</span><span class="sxs-lookup"><span data-stu-id="ddbfd-204">Add the following method to the Program class.</span></span>

    static public void PublishAssetGetURLs(IAsset asset)
    {
        // Publish the output asset by creating an Origin locator for adaptive streaming,
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

        // Get the Smooth Streaming, HLS and MPEG-DASH URLs for adaptive streaming,
        // and the Progressive Download URL.
        Uri smoothStreamingUri = asset.GetSmoothStreamingUri();
        Uri hlsUri = asset.GetHlsUri();
        Uri mpegDashUri = asset.GetMpegDashUri();

        // Get the URls for progressive download for each MP4 file that was generated as a result
        // of encoding.
        List<Uri> mp4ProgressiveDownloadUris = mp4AssetFiles.Select(af => af.GetSasUri()).ToList();


        // Display  the streaming URLs.
        Console.WriteLine("Use the following URLs for adaptive streaming: ");
        Console.WriteLine(smoothStreamingUri);
        Console.WriteLine(hlsUri);
        Console.WriteLine(mpegDashUri);
        Console.WriteLine();

        // Display the URLs for progressive download.
        Console.WriteLine("Use the following URLs for progressive download.");
        mp4ProgressiveDownloadUris.ForEach(uri => Console.WriteLine(uri + "\n"));
        Console.WriteLine();

        // Download the output asset to a local folder.
        string outputFolder = "job-output";
        if (!Directory.Exists(outputFolder))
        {
            Directory.CreateDirectory(outputFolder);
        }

        Console.WriteLine();
        Console.WriteLine("Downloading output asset files to a local folder...");
        asset.DownloadToFolder(
            outputFolder,
            (af, p) =>
            {
                Console.WriteLine("Downloading '{0}' - Progress: {1:0.##}%", af.Name, p.Progress);
            });

        Console.WriteLine("Output asset files available at '{0}'.", Path.GetFullPath(outputFolder));
    }

## <a name="test-by-playing-your-content"></a><span data-ttu-id="ddbfd-205">Testare riproducendo i contenuti.</span><span class="sxs-lookup"><span data-stu-id="ddbfd-205">Test by playing your content</span></span>

<span data-ttu-id="ddbfd-206">Dopo aver eseguito il programma definito nella sezione precedente, nella finestra della console vengono visualizzati URL simili al seguente.</span><span class="sxs-lookup"><span data-stu-id="ddbfd-206">Once you run the program defined in the previous section, the URLs similar to the following will be displayed in the console window.</span></span>

<span data-ttu-id="ddbfd-207">URL per streaming adattivo:</span><span class="sxs-lookup"><span data-stu-id="ddbfd-207">Adaptive streaming URLs:</span></span>

<span data-ttu-id="ddbfd-208">Smooth Streaming</span><span class="sxs-lookup"><span data-stu-id="ddbfd-208">Smooth Streaming</span></span>

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest

<span data-ttu-id="ddbfd-209">HLS</span><span class="sxs-lookup"><span data-stu-id="ddbfd-209">HLS</span></span>

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest(format=m3u8-aapl)

<span data-ttu-id="ddbfd-210">MPEG DASH</span><span class="sxs-lookup"><span data-stu-id="ddbfd-210">MPEG DASH</span></span>

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest(format=mpd-time-csf)

<span data-ttu-id="ddbfd-211">URL per download progressivo (audio e video).</span><span class="sxs-lookup"><span data-stu-id="ddbfd-211">Progressive download URLs (audio and video).</span></span>

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_650kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_400kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_3400kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_2250kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_1500kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_1000kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_AAC_und_ch2_56kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z


<span data-ttu-id="ddbfd-212">Per eseguire lo streaming del video, incollare l'URL nella casella di testo URL in [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span><span class="sxs-lookup"><span data-stu-id="ddbfd-212">To stream your video, paste your URL in the URL textbox in the [Azure Media Services Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span>

<span data-ttu-id="ddbfd-213">Per testare il download progressivo, incollare un URL in un browser (ad esempio, IE, Chrome, Safari).</span><span class="sxs-lookup"><span data-stu-id="ddbfd-213">To test progressive download, paste a URL into a browser (for example, Internet Explorer, Chrome, or Safari).</span></span>

<span data-ttu-id="ddbfd-214">Per ulteriori informazioni, vedere gli argomenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="ddbfd-214">For more information, see the following topics:</span></span>

- [<span data-ttu-id="ddbfd-215">Riproduzione di contenuti con i lettori esistenti</span><span class="sxs-lookup"><span data-stu-id="ddbfd-215">Playing your content with existing players</span></span>](media-services-playback-content-with-existing-players.md)
- [<span data-ttu-id="ddbfd-216">Sviluppo di applicazioni di lettore video</span><span class="sxs-lookup"><span data-stu-id="ddbfd-216">Develop video player applications</span></span>](media-services-develop-video-players.md)
- [<span data-ttu-id="ddbfd-217">Integrazione di uno streaming video adattivo MPEG-DASH in un'applicazione HTML5 con DASH.js</span><span class="sxs-lookup"><span data-stu-id="ddbfd-217">Embedding a MPEG-DASH Adaptive Streaming Video in an HTML5 Application with DASH.js</span></span>](media-services-embed-mpeg-dash-in-html5.md)

## <a name="download-sample"></a><span data-ttu-id="ddbfd-218">Scaricare un esempio</span><span class="sxs-lookup"><span data-stu-id="ddbfd-218">Download sample</span></span>
<span data-ttu-id="ddbfd-219">L'esempio di codice seguente contiene il codice creato in questa esercitazione: [esempio](https://azure.microsoft.com/documentation/samples/media-services-dotnet-on-demand-encoding-with-media-encoder-standard/).</span><span class="sxs-lookup"><span data-stu-id="ddbfd-219">The following code sample contains the code that you created in this tutorial: [sample](https://azure.microsoft.com/documentation/samples/media-services-dotnet-on-demand-encoding-with-media-encoder-standard/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ddbfd-220">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ddbfd-220">Next Steps</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="ddbfd-221">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="ddbfd-221">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]



<!-- Anchors. -->


<!-- URLs. -->
[Web Platform Installer]: http://go.microsoft.com/fwlink/?linkid=255386
[Portal]: http://manage.windowsazure.com/
