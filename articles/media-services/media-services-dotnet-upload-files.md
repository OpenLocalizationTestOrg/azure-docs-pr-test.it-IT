---
title: i file in un account di servizi multimediali usando .NET aaaUpload | Documenti Microsoft
description: Informazioni su come tooget multimediali in servizi multimediali tramite la creazione e caricamento di asset.
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: c9c86380-9395-4db8-acea-507c52066f73
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/12/2017
ms.author: juliako
ms.openlocfilehash: 11c8a359b09efe04b54490fd48ac0cd7c366f8b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-into-a-media-services-account-using-net"></a><span data-ttu-id="f97bc-103">Caricare file in un account di Servizi multimediali mediante .NET</span><span class="sxs-lookup"><span data-stu-id="f97bc-103">Upload files into a Media Services account using .NET</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f97bc-104">.NET</span><span class="sxs-lookup"><span data-stu-id="f97bc-104">.NET</span></span>](media-services-dotnet-upload-files.md)
> * [<span data-ttu-id="f97bc-105">REST</span><span class="sxs-lookup"><span data-stu-id="f97bc-105">REST</span></span>](media-services-rest-upload-files.md)
> * [<span data-ttu-id="f97bc-106">Portale</span><span class="sxs-lookup"><span data-stu-id="f97bc-106">Portal</span></span>](media-services-portal-upload-files.md)
> 
> 

<span data-ttu-id="f97bc-107">In Servizi multimediali i file digitali vengono caricati (o inseriti) in un asset.</span><span class="sxs-lookup"><span data-stu-id="f97bc-107">In Media Services, you upload (or ingest) your digital files into an asset.</span></span> <span data-ttu-id="f97bc-108">Hello **Asset** entità può contenere video, audio, immagini, raccolte di anteprime, testo tracce e sottotitoli file (e relativi metadati hello.)  Una volta caricati i file hello, il contenuto è archiviato in modo sicuro nel cloud hello per continuare l'elaborazione e il flusso.</span><span class="sxs-lookup"><span data-stu-id="f97bc-108">hello **Asset** entity can contain video, audio, images, thumbnail collections, text tracks and closed caption files (and hello metadata about these files.)  Once hello files are uploaded, your content is stored securely in hello cloud for further processing and streaming.</span></span>

<span data-ttu-id="f97bc-109">file Hello in asset hello sono denominati **file di Asset**.</span><span class="sxs-lookup"><span data-stu-id="f97bc-109">hello files in hello asset are called **Asset Files**.</span></span> <span data-ttu-id="f97bc-110">Hello **AssetFile** istanza e hello effettivo file multimediale sono due oggetti distinti.</span><span class="sxs-lookup"><span data-stu-id="f97bc-110">hello **AssetFile** instance and hello actual media file are two distinct objects.</span></span> <span data-ttu-id="f97bc-111">istanza di AssetFile Hello contiene i metadati relativi a file di supporto hello, mentre i file di supporto hello contiene hello effettivo contenuto multimediale.</span><span class="sxs-lookup"><span data-stu-id="f97bc-111">hello AssetFile instance contains metadata about hello media file, while hello media file contains hello actual media content.</span></span>

> [!NOTE]
> <span data-ttu-id="f97bc-112">si applica Hello seguenti considerazioni:</span><span class="sxs-lookup"><span data-stu-id="f97bc-112">hello following considerations apply:</span></span>
> 
> * <span data-ttu-id="f97bc-113">Servizi multimediali Usa valore hello hello IAssetFile.Name proprietà durante la creazione di URL per hello streaming del contenuto (ad esempio, http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) Per questo motivo, la codifica percentuale non è consentita.</span><span class="sxs-lookup"><span data-stu-id="f97bc-113">Media Services uses hello value of hello IAssetFile.Name property when building URLs for hello streaming content (for example, http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) For this reason, percent-encoding is not allowed.</span></span> <span data-ttu-id="f97bc-114">valore di hello Hello **nome** proprietà non può avere uno dei seguenti hello [% riservati per la codifica caratteri](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters):! *' ();: @& = + $, /? % # [] ".</span><span class="sxs-lookup"><span data-stu-id="f97bc-114">hello value of hello **Name** property cannot have any of hello following [percent-encoding-reserved characters](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters): !*'();:@&=+$,/?%#[]".</span></span> <span data-ttu-id="f97bc-115">Inoltre, può essere presente solo uno '.' per l'estensione del nome file hello.</span><span class="sxs-lookup"><span data-stu-id="f97bc-115">Also, there can only be one '.' for hello file name extension.</span></span>
> * <span data-ttu-id="f97bc-116">lunghezza Hello del nome di hello non deve essere maggiore di 260 caratteri.</span><span class="sxs-lookup"><span data-stu-id="f97bc-116">hello length of hello name should not be greater than 260 characters.</span></span>
> * <span data-ttu-id="f97bc-117">È una limite toohello dimensione massima supportata per l'elaborazione in servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="f97bc-117">There is a limit toohello maximum file size supported for processing in Media Services.</span></span> <span data-ttu-id="f97bc-118">Vedere [questo](media-services-quotas-and-limitations.md) per informazioni sulla limitazione delle dimensioni del file hello.</span><span class="sxs-lookup"><span data-stu-id="f97bc-118">Please see [this](media-services-quotas-and-limitations.md) topic for details about hello file size limitation.</span></span>
> * <span data-ttu-id="f97bc-119">È previsto un limite di 1.000.000 di criteri per i diversi criteri AMS (ad esempio per i criteri Locator o ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="f97bc-119">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="f97bc-120">È consigliabile utilizzare hello stesso ID di criteri, se si utilizza sempre hello stesso giorni accesso le autorizzazioni, ad esempio, i criteri per i localizzatori che sono previsti tooremain sul posto per un lungo periodo (non-caricamento criteri).</span><span class="sxs-lookup"><span data-stu-id="f97bc-120">You should use hello same policy ID if you are always using hello same days / access permissions, for example, policies for locators that are intended tooremain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="f97bc-121">Per altre informazioni, vedere [questo](media-services-dotnet-manage-entities.md#limit-access-policies) argomento.</span><span class="sxs-lookup"><span data-stu-id="f97bc-121">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>
> 

<span data-ttu-id="f97bc-122">Quando si creano asset, è possibile specificare le opzioni di crittografia seguenti hello.</span><span class="sxs-lookup"><span data-stu-id="f97bc-122">When you create assets, you can specify hello following encryption options.</span></span> 

* <span data-ttu-id="f97bc-123">**None** : non viene usata alcuna crittografia.</span><span class="sxs-lookup"><span data-stu-id="f97bc-123">**None** - No encryption is used.</span></span> <span data-ttu-id="f97bc-124">Questo è il valore di predefinito hello.</span><span class="sxs-lookup"><span data-stu-id="f97bc-124">This is hello default value.</span></span> <span data-ttu-id="f97bc-125">Quando si usa questa opzione, il contenuto non è protetto durante il transito, né nell'archiviazione locale.</span><span class="sxs-lookup"><span data-stu-id="f97bc-125">Note that when using this option your content is not protected in transit or at rest in storage.</span></span>
  <span data-ttu-id="f97bc-126">Se si prevede di toodeliver un file MP4 tramite download progressivo, usare questa opzione.</span><span class="sxs-lookup"><span data-stu-id="f97bc-126">If you plan toodeliver an MP4 using progressive download, use this option.</span></span> 
* <span data-ttu-id="f97bc-127">**CommonEncryption** : usare questa opzione per caricare contenuti già crittografati e protetti con Common Encryption o PlayReady DRM (ad esempio, Smooth Streaming protetto con PlayReady DRM).</span><span class="sxs-lookup"><span data-stu-id="f97bc-127">**CommonEncryption** - Use this option if you are uploading content that has already been encrypted and protected with Common Encryption or PlayReady DRM (for example, Smooth Streaming protected with PlayReady DRM).</span></span>
* <span data-ttu-id="f97bc-128">**EnvelopeEncrypted** : usare questa opzione se si sta caricando contenuto HLS crittografato con AES.</span><span class="sxs-lookup"><span data-stu-id="f97bc-128">**EnvelopeEncrypted** – Use this option if you are uploading HLS encrypted with AES.</span></span> <span data-ttu-id="f97bc-129">Si noti che i file hello devono sono stati codificati e crittografati da Transform Manager.</span><span class="sxs-lookup"><span data-stu-id="f97bc-129">Note that hello files must have been encoded and encrypted by Transform Manager.</span></span>
* <span data-ttu-id="f97bc-130">**StorageEncrypted** : consente di crittografare il contenuto non crittografato in locale utilizzando la crittografia AES a 256 bit e quindi lo carica tooAzure archiviazione dove viene archiviato in forma crittografata.</span><span class="sxs-lookup"><span data-stu-id="f97bc-130">**StorageEncrypted** - Encrypts your clear content locally using AES-256 bit encryption and then uploads it tooAzure Storage where it is stored encrypted at rest.</span></span> <span data-ttu-id="f97bc-131">Gli asset protetti con crittografia di archiviazione vengono decrittografati automaticamente e inseriti in un file crittografato sistema precedente tooencoding e, facoltativamente, crittografare nuovamente toouploading precedente come nuovo asset di output.</span><span class="sxs-lookup"><span data-stu-id="f97bc-131">Assets protected with Storage Encryption are automatically unencrypted and placed in an encrypted file system prior tooencoding, and optionally re-encrypted prior toouploading back as a new output asset.</span></span> <span data-ttu-id="f97bc-132">Hello primario per la crittografia di archiviazione viene usata quando si desidera toosecure file multimediali di input di alta qualità applicando una crittografia avanzata rest su disco.</span><span class="sxs-lookup"><span data-stu-id="f97bc-132">hello primary use case for Storage Encryption is when you want toosecure your high quality input media files with strong encryption at rest on disk.</span></span>
  
    <span data-ttu-id="f97bc-133">Servizi multimediali offre una crittografia di archiviazione su disco per gli asset, non in rete come Digital Rights Management (DRM).</span><span class="sxs-lookup"><span data-stu-id="f97bc-133">Media Services provides on-disk storage encryption for your assets, not over-the-wire like Digital Rights Manager (DRM).</span></span>
  
    <span data-ttu-id="f97bc-134">Se l'asset è protetto con crittografia di archiviazione, è necessario configurare i criteri di distribuzione degli asset.</span><span class="sxs-lookup"><span data-stu-id="f97bc-134">If your asset is storage encrypted, you must configure asset delivery policy.</span></span> <span data-ttu-id="f97bc-135">Per altre informazioni, vedere [Procedura: Configurare i criteri di distribuzione degli asset](media-services-dotnet-configure-asset-delivery-policy.md).</span><span class="sxs-lookup"><span data-stu-id="f97bc-135">For more information see [Configuring asset delivery policy](media-services-dotnet-configure-asset-delivery-policy.md).</span></span>

<span data-ttu-id="f97bc-136">Se si specifica per toobe l'asset crittografato con una **CommonEncrypted** opzione o un **EnvelopeEncypted** opzione, sarà necessario tooassociate l'asset con un **ContentKey**.</span><span class="sxs-lookup"><span data-stu-id="f97bc-136">If you specify for your asset toobe encrypted with a **CommonEncrypted** option, or an **EnvelopeEncypted** option, you will need tooassociate your asset with a **ContentKey**.</span></span> <span data-ttu-id="f97bc-137">Per ulteriori informazioni, vedere [come un'entità ContentKey toocreate](media-services-dotnet-create-contentkey.md).</span><span class="sxs-lookup"><span data-stu-id="f97bc-137">For more information, see [How toocreate a ContentKey](media-services-dotnet-create-contentkey.md).</span></span> 

<span data-ttu-id="f97bc-138">Se si specifica per toobe l'asset crittografato con una **StorageEncrypted** opzione, hello Media Services SDK per .NET verranno creati un **StorateEncrypted** **ContentKey** per il Asset.</span><span class="sxs-lookup"><span data-stu-id="f97bc-138">If you specify for your asset toobe encrypted with a **StorageEncrypted** option, hello Media Services SDK for .NET will create a **StorateEncrypted** **ContentKey** for your asset.</span></span>

<span data-ttu-id="f97bc-139">Questo argomento viene illustrato come toouse Media Services .NET SDK, nonché i file di Media Services .NET SDK extensions tooupload in un asset di servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="f97bc-139">This topic shows how toouse Media Services .NET SDK as well as Media Services .NET SDK extensions tooupload files into a Media Services asset.</span></span>

## <a name="upload-a-single-file-with-media-services-net-sdk"></a><span data-ttu-id="f97bc-140">Caricare un singolo file con SDK di Servizi multimediali per .NET</span><span class="sxs-lookup"><span data-stu-id="f97bc-140">Upload a single file with Media Services .NET SDK</span></span>
<span data-ttu-id="f97bc-141">codice di esempio Hello seguente utilizza tooupload .NET SDK un singolo file.</span><span class="sxs-lookup"><span data-stu-id="f97bc-141">hello sample code below uses .NET SDK tooupload a single file.</span></span> <span data-ttu-id="f97bc-142">Hello AccessPolicy e Locator vengono creati e distrutti dalla funzione di caricamento hello.</span><span class="sxs-lookup"><span data-stu-id="f97bc-142">hello AccessPolicy and Locator are created and destroyed by hello Upload function.</span></span> 


        static public IAsset CreateAssetAndUploadSingleFile(AssetCreationOptions assetCreationOptions, string singleFilePath)
        {
            if (!File.Exists(singleFilePath))
            {
                Console.WriteLine("File does not exist.");
                return null;
            }

            var assetName = Path.GetFileNameWithoutExtension(singleFilePath);
            IAsset inputAsset = _context.Assets.Create(assetName, assetCreationOptions);

            var assetFile = inputAsset.AssetFiles.Create(Path.GetFileName(singleFilePath));

            Console.WriteLine("Upload {0}", assetFile.Name);

            assetFile.Upload(singleFilePath);
            Console.WriteLine("Done uploading {0}", assetFile.Name);

            return inputAsset;
        }


## <a name="upload-multiple-files-with-media-services-net-sdk"></a><span data-ttu-id="f97bc-143">Caricare più file con SDK di Servizi multimediali per .NET</span><span class="sxs-lookup"><span data-stu-id="f97bc-143">Upload multiple files with Media Services .NET SDK</span></span>
<span data-ttu-id="f97bc-144">Hello seguente codice mostra come toocreate un asset e caricare più file.</span><span class="sxs-lookup"><span data-stu-id="f97bc-144">hello following code shows how toocreate an asset and upload multiple files.</span></span>

<span data-ttu-id="f97bc-145">codice Hello hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="f97bc-145">hello code does hello following:</span></span>

* <span data-ttu-id="f97bc-146">Crea un asset vuoto utilizzando il metodo di CreateEmptyAsset hello definito nel passaggio precedente hello.</span><span class="sxs-lookup"><span data-stu-id="f97bc-146">Creates an empty asset using hello CreateEmptyAsset method defined in hello previous step.</span></span>
* <span data-ttu-id="f97bc-147">Crea un **AccessPolicy** istanza che definisce le autorizzazioni di hello e la durata dell'asset toohello di accesso.</span><span class="sxs-lookup"><span data-stu-id="f97bc-147">Creates an **AccessPolicy** instance that defines hello permissions and duration of access toohello asset.</span></span>
* <span data-ttu-id="f97bc-148">Crea un **localizzatore** istanza che fornisce l'asset toohello di accesso.</span><span class="sxs-lookup"><span data-stu-id="f97bc-148">Creates a **Locator** instance that provides access toohello asset.</span></span>
* <span data-ttu-id="f97bc-149">Crea un'istanza di **BlobTransferClient** .</span><span class="sxs-lookup"><span data-stu-id="f97bc-149">Creates a **BlobTransferClient** instance.</span></span> <span data-ttu-id="f97bc-150">Questo tipo rappresenta un client che agisce sui hello che BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="f97bc-150">This type represents a client that operates on hello Azure blobs.</span></span> <span data-ttu-id="f97bc-151">In questo esempio viene usato lo stato di caricamento di hello client toomonitor hello.</span><span class="sxs-lookup"><span data-stu-id="f97bc-151">In this example we use hello client toomonitor hello upload progress.</span></span> 
* <span data-ttu-id="f97bc-152">Enumera i file nella directory specificata hello e crea un **AssetFile** istanza per ogni file.</span><span class="sxs-lookup"><span data-stu-id="f97bc-152">Enumerates through files in hello specified directory and creates an **AssetFile** instance for each file.</span></span>
* <span data-ttu-id="f97bc-153">Caricamenti hello file in servizi multimediali usando hello **UploadAsync** metodo.</span><span class="sxs-lookup"><span data-stu-id="f97bc-153">Uploads hello files into Media Services using hello **UploadAsync** method.</span></span> 

> [!NOTE]
> <span data-ttu-id="f97bc-154">Utilizzare hello UploadAsync metodo tooensure che non siano bloccate hello chiamate e i file hello vengono caricati in parallelo.</span><span class="sxs-lookup"><span data-stu-id="f97bc-154">Use hello UploadAsync method tooensure that hello calls are not blocking and hello files are uploaded in parallel.</span></span>
> 
> 

        static public IAsset CreateAssetAndUploadMultipleFiles(AssetCreationOptions assetCreationOptions, string folderPath)
        {
            var assetName = "UploadMultipleFiles_" + DateTime.UtcNow.ToString();

            IAsset asset = _context.Assets.Create(assetName, assetCreationOptions);

            var accessPolicy = _context.AccessPolicies.Create(assetName, TimeSpan.FromDays(30),
                                                                AccessPermissions.Write | AccessPermissions.List);

            var locator = _context.Locators.CreateLocator(LocatorType.Sas, asset, accessPolicy);

            var blobTransferClient = new BlobTransferClient();
            blobTransferClient.NumberOfConcurrentTransfers = 20;
            blobTransferClient.ParallelTransferThreadCount = 20;

            blobTransferClient.TransferProgressChanged += blobTransferClient_TransferProgressChanged;

            var filePaths = Directory.EnumerateFiles(folderPath);

            Console.WriteLine("There are {0} files in {1}", filePaths.Count(), folderPath);

            if (!filePaths.Any())
            {
                throw new FileNotFoundException(String.Format("No files in directory, check folderPath: {0}", folderPath));
            }

            var uploadTasks = new List<Task>();
            foreach (var filePath in filePaths)
            {
                var assetFile = asset.AssetFiles.Create(Path.GetFileName(filePath));
                Console.WriteLine("Created assetFile {0}", assetFile.Name);

                // It is recommended toovalidate AccestFiles before upload. 
                Console.WriteLine("Start uploading of {0}", assetFile.Name);
                uploadTasks.Add(assetFile.UploadAsync(filePath, blobTransferClient, locator, CancellationToken.None));
            }

            Task.WaitAll(uploadTasks.ToArray());
            Console.WriteLine("Done uploading hello files");

            blobTransferClient.TransferProgressChanged -= blobTransferClient_TransferProgressChanged;

            locator.Delete();
            accessPolicy.Delete();

            return asset;
        }

    static void  blobTransferClient_TransferProgressChanged(object sender, BlobTransferProgressChangedEventArgs e)
    {
        if (e.ProgressPercentage > 4) // Avoid startup jitter, as hello upload tasks are added.
        {
            Console.WriteLine("{0}% upload competed for {1}.", e.ProgressPercentage, e.LocalFile);
        }
    }



<span data-ttu-id="f97bc-155">Quando si carica un numero elevato di asset, prendere in considerazione seguente hello.</span><span class="sxs-lookup"><span data-stu-id="f97bc-155">When uploading a large number of assets, consider hello following.</span></span>

* <span data-ttu-id="f97bc-156">Creare un nuovo oggetto **CloudMediaContext** per thread.</span><span class="sxs-lookup"><span data-stu-id="f97bc-156">Create a new **CloudMediaContext** object per thread.</span></span> <span data-ttu-id="f97bc-157">Hello **CloudMediaContext** classe non è thread-safe.</span><span class="sxs-lookup"><span data-stu-id="f97bc-157">hello **CloudMediaContext** class is not thread safe.</span></span>
* <span data-ttu-id="f97bc-158">Aumentare NumberOfConcurrentTransfers dal valore predefinito di hello valore 2 tooa superiore come 5.</span><span class="sxs-lookup"><span data-stu-id="f97bc-158">Increase NumberOfConcurrentTransfers from hello default value of 2 tooa higher value like 5.</span></span> <span data-ttu-id="f97bc-159">L'impostazione di questa proprietà ha effetto su tutte le istanze di **CloudMediaContext**.</span><span class="sxs-lookup"><span data-stu-id="f97bc-159">Setting this property affects all instances of **CloudMediaContext**.</span></span> 
* <span data-ttu-id="f97bc-160">Mantenere ParallelTransferThreadCount valore hello predefinito 10.</span><span class="sxs-lookup"><span data-stu-id="f97bc-160">Keep ParallelTransferThreadCount at hello default value of 10.</span></span>

## <span data-ttu-id="f97bc-161"><a id="ingest_in_bulk"></a>Inserimento di asset in blocco tramite SDK di Servizi multimediali per .NET</span><span class="sxs-lookup"><span data-stu-id="f97bc-161"><a id="ingest_in_bulk"></a>Ingesting Assets in Bulk using Media Services .NET SDK</span></span>
<span data-ttu-id="f97bc-162">Il caricamento di file di asset di grandi dimensioni costituisce un collo di bottiglia nella creazione di asset.</span><span class="sxs-lookup"><span data-stu-id="f97bc-162">Uploading large asset files can be a bottleneck during asset creation.</span></span> <span data-ttu-id="f97bc-163">Inserimento di asset in blocco o "L'inserimento in blocco", prevede il disaccoppiamento creazione asset dal processo di caricamento hello.</span><span class="sxs-lookup"><span data-stu-id="f97bc-163">Ingesting Assets in Bulk or “Bulk Ingesting”, involves decoupling asset creation from hello upload process.</span></span> <span data-ttu-id="f97bc-164">toouse un approccio l'inserimento bulk, creare un manifesto (IngestManifest) che descrive l'asset hello e relativi file associati.</span><span class="sxs-lookup"><span data-stu-id="f97bc-164">toouse a bulk ingesting approach, create a manifest (IngestManifest) that describes hello asset and its associated files.</span></span> <span data-ttu-id="f97bc-165">Utilizzare quindi il metodo di caricamento hello del contenitore blob la scelta tooupload hello i file associati toohello del manifesto.</span><span class="sxs-lookup"><span data-stu-id="f97bc-165">Then use hello upload method of your choice tooupload hello associated files toohello manifest’s blob container.</span></span> <span data-ttu-id="f97bc-166">Servizi multimediali di Microsoft Azure controlla il contenitore di blob hello associato manifesto hello.</span><span class="sxs-lookup"><span data-stu-id="f97bc-166">Microsoft Azure Media Services watches hello blob container associated with hello manifest.</span></span> <span data-ttu-id="f97bc-167">Quando un file è il contenitore di blob caricato toohello, servizi multimediali di Microsoft Azure completa di creazione degli asset hello in base alla configurazione di hello dell'asset hello nel manifesto hello (entità IngestManifestAsset).</span><span class="sxs-lookup"><span data-stu-id="f97bc-167">Once a file is uploaded toohello blob container, Microsoft Azure Media Services completes hello asset creation based on hello configuration of hello asset in hello manifest (IngestManifestAsset).</span></span>

<span data-ttu-id="f97bc-168">toocreate una nuova entità IngestManifest chiamare il metodo di creazione hello esposto da hello raccolta hello CloudMediaContext le entità Ingestmanifest.</span><span class="sxs-lookup"><span data-stu-id="f97bc-168">toocreate a new IngestManifest call hello Create method exposed by hello IngestManifests collection on hello CloudMediaContext.</span></span> <span data-ttu-id="f97bc-169">Questo metodo creerà una nuova entità IngestManifest con nome hello del manifesto specificato.</span><span class="sxs-lookup"><span data-stu-id="f97bc-169">This method will create a new IngestManifest with hello manifest name you provide.</span></span>

    IIngestManifest manifest = context.IngestManifests.Create(name);

<span data-ttu-id="f97bc-170">Creare asset di hello che verrà associato bulk hello entità IngestManifest.</span><span class="sxs-lookup"><span data-stu-id="f97bc-170">Create hello assets that will be associated with hello bulk IngestManifest.</span></span> <span data-ttu-id="f97bc-171">Configurare le opzioni di crittografia hello desiderato nel asset hello per l'inserimento in blocco.</span><span class="sxs-lookup"><span data-stu-id="f97bc-171">Configure hello desired encryption options on hello asset for bulk ingesting.</span></span>

    // Create hello assets that will be associated with this bulk ingest manifest
    IAsset destAsset1 = _context.Assets.Create(name + "_asset_1", AssetCreationOptions.None);
    IAsset destAsset2 = _context.Assets.Create(name + "_asset_2", AssetCreationOptions.None);

<span data-ttu-id="f97bc-172">Un'entità IngestManifestAsset associa un Asset a un IngestManifest in blocco per l'inserimento in blocco.</span><span class="sxs-lookup"><span data-stu-id="f97bc-172">An IngestManifestAsset associates an Asset with a bulk IngestManifest for bulk ingesting.</span></span> <span data-ttu-id="f97bc-173">Inoltre, associa hello AssetFiles che costituiranno ogni Asset.</span><span class="sxs-lookup"><span data-stu-id="f97bc-173">It also associates hello AssetFiles that will make up each Asset.</span></span> <span data-ttu-id="f97bc-174">toocreate un'entità IngestManifestAsset, utilizzare il metodo di creazione hello contesto hello del server.</span><span class="sxs-lookup"><span data-stu-id="f97bc-174">toocreate an IngestManifestAsset, use hello Create method on hello server context.</span></span>

<span data-ttu-id="f97bc-175">Hello esempio seguente viene illustrato aggiungere due nuove entità Ingestmanifestasset che associano le attività di hello creato in precedenza toohello bulk manifesto di inserimento.</span><span class="sxs-lookup"><span data-stu-id="f97bc-175">hello following example demonstrates adding two new IngestManifestAssets that associate hello two assets previously created toohello bulk ingest manifest.</span></span> <span data-ttu-id="f97bc-176">Ogni entità IngestManifestAsset associa anche un set di file che verrà caricato per ogni asset durante l'inserimento in blocco.</span><span class="sxs-lookup"><span data-stu-id="f97bc-176">Each IngestManifestAsset also associates a set of files that will be uploaded for each asset during bulk ingesting.</span></span>  

    string filename1 = _singleInputMp4Path;
    string filename2 = _primaryFilePath;
    string filename3 = _singleInputFilePath;

    IIngestManifestAsset bulkAsset1 =  manifest.IngestManifestAssets.Create(destAsset1, new[] { filename1 });
    IIngestManifestAsset bulkAsset2 =  manifest.IngestManifestAssets.Create(destAsset2, new[] { filename2, filename3 });

<span data-ttu-id="f97bc-177">È possibile utilizzare qualsiasi applicazione client ad alta velocità in grado di caricare hello asset file toohello contenitore di archiviazione blob URI fornito da hello **IIngestManifest.BlobStorageUriForUpload** proprietà dell'entità IngestManifest hello.</span><span class="sxs-lookup"><span data-stu-id="f97bc-177">You can use any high speed client application capable of uploading hello asset files toohello blob storage container URI provided by hello **IIngestManifest.BlobStorageUriForUpload** property of hello IngestManifest.</span></span> <span data-ttu-id="f97bc-178">Un servizio di caricamento ad alta velocità consigliato è l'applicazione [Aspera On Demand for Azure](https://datamarket.azure.com/application/2cdbc511-cb12-4715-9871-c7e7fbbb82a6).</span><span class="sxs-lookup"><span data-stu-id="f97bc-178">One notable high speed upload service is [Aspera On Demand for Azure Application](https://datamarket.azure.com/application/2cdbc511-cb12-4715-9871-c7e7fbbb82a6).</span></span> <span data-ttu-id="f97bc-179">È possibile anche scrivere codice i file di asset hello tooupload come illustrato nell'esempio di codice seguente hello.</span><span class="sxs-lookup"><span data-stu-id="f97bc-179">You can also write code tooupload hello assets files as shown in hello following code example.</span></span>

    static void UploadBlobFile(string destBlobURI, string filename)
    {
        Task copytask = new Task(() =>
        {
            var storageaccount = new CloudStorageAccount(new StorageCredentials(_storageAccountName, _storageAccountKey), true);
            CloudBlobClient blobClient = storageaccount.CreateCloudBlobClient();
            CloudBlobContainer blobContainer = blobClient.GetContainerReference(destBlobURI);

            string[] splitfilename = filename.Split('\\');
            var blob = blobContainer.GetBlockBlobReference(splitfilename[splitfilename.Length - 1]);

            using (var stream = System.IO.File.OpenRead(filename))
                blob.UploadFromStream(stream);

            lock (consoleWriteLock)
            {
                Console.WriteLine("Upload for {0} completed.", filename);
            }
        });

        copytask.Start();
    }

<span data-ttu-id="f97bc-180">codice di Hello per caricare il file di asset hello per l'esempio hello usato in questo argomento è illustrato nell'esempio di codice seguente hello.</span><span class="sxs-lookup"><span data-stu-id="f97bc-180">hello code for uploading hello asset files for hello sample used in this topic is shown in hello following code example.</span></span>

    UploadBlobFile(manifest.BlobStorageUriForUpload, filename1);
    UploadBlobFile(manifest.BlobStorageUriForUpload, filename2);
    UploadBlobFile(manifest.BlobStorageUriForUpload, filename3);


<span data-ttu-id="f97bc-181">È possibile determinare lo stato di avanzamento hello hello l'inserimento in blocco per tutti gli asset associati a un **IngestManifest** eseguendo il polling delle proprietà di statistiche hello di hello **IngestManifest**.</span><span class="sxs-lookup"><span data-stu-id="f97bc-181">You can determine hello progress of hello bulk ingesting for all assets associated with an **IngestManifest** by polling hello Statistics property of hello **IngestManifest**.</span></span> <span data-ttu-id="f97bc-182">In informazioni sullo stato di tooupdate ordine, è necessario utilizzare un nuovo **CloudMediaContext** ogni volta che si esegue il polling proprietà Statistics hello.</span><span class="sxs-lookup"><span data-stu-id="f97bc-182">In order tooupdate progress information, you must use a new **CloudMediaContext** each time you poll hello Statistics property.</span></span>

<span data-ttu-id="f97bc-183">Hello esempio seguente viene illustrato il polling di un'entità IngestManifest dal relativo **Id**.</span><span class="sxs-lookup"><span data-stu-id="f97bc-183">hello following example demonstrates polling an IngestManifest by its **Id**.</span></span>

    static void MonitorBulkManifest(string manifestID)
    {
       bool bContinue = true;
       while (bContinue)
       {
          CloudMediaContext context = GetContext();
          IIngestManifest manifest = context.IngestManifests.Where(m => m.Id == manifestID).FirstOrDefault();

          if (manifest != null)
          {
             lock(consoleWriteLock)
             {
                Console.WriteLine("\nWaiting on all file uploads.");
                Console.WriteLine("PendingFilesCount  : {0}", manifest.Statistics.PendingFilesCount);
                Console.WriteLine("FinishedFilesCount : {0}", manifest.Statistics.FinishedFilesCount);
                Console.WriteLine("{0}% complete.\n", (float)manifest.Statistics.FinishedFilesCount / (float)(manifest.Statistics.FinishedFilesCount + manifest.Statistics.PendingFilesCount) * 100);

                if (manifest.Statistics.PendingFilesCount == 0)
                {
                   Console.WriteLine("Completed\n");
                   bContinue = false;
                }
             }

             if (manifest.Statistics.FinishedFilesCount < manifest.Statistics.PendingFilesCount)
                Thread.Sleep(60000);
          }
          else // Manifest is null
             bContinue = false;
       }
    }



## <a name="upload-files-using-net-sdk-extensions"></a><span data-ttu-id="f97bc-184">Caricare file mediante le estensioni dell'SDK per .NET</span><span class="sxs-lookup"><span data-stu-id="f97bc-184">Upload files using .NET SDK Extensions</span></span>
<span data-ttu-id="f97bc-185">esempio Hello riportato di seguito viene illustrato come tooupload un singolo file con estensioni del SDK .NET.</span><span class="sxs-lookup"><span data-stu-id="f97bc-185">hello example below shows how tooupload a single file using .NET SDK Extensions.</span></span> <span data-ttu-id="f97bc-186">In questo caso hello **CreateFromFile** viene usato il metodo, ma è disponibile anche la versione asincrona di hello (**CreateFromFileAsync**).</span><span class="sxs-lookup"><span data-stu-id="f97bc-186">In this case hello **CreateFromFile** method is used, but hello asynchronous version is also available (**CreateFromFileAsync**).</span></span> <span data-ttu-id="f97bc-187">Hello **CreateFromFile** metodo consente di specificare il nome di file hello, opzione di crittografia e un callback in hello tooreport ordine caricare lo stato di avanzamento del file hello.</span><span class="sxs-lookup"><span data-stu-id="f97bc-187">hello **CreateFromFile** method lets you specify hello file name, encryption option, and a callback in order tooreport hello upload progress of hello file.</span></span>

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

<span data-ttu-id="f97bc-188">Hello esempio seguente chiama la funzione UploadFile e specifica la crittografia di archiviazione come opzione di creazione di asset hello.</span><span class="sxs-lookup"><span data-stu-id="f97bc-188">hello following example calls UploadFile function and specifies storage encryption as hello asset creation option.</span></span>  

    var asset = UploadFile(@"C:\VideoFiles\BigBuckBunny.mp4", AssetCreationOptions.StorageEncrypted);

## <a name="next-steps"></a><span data-ttu-id="f97bc-189">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f97bc-189">Next steps</span></span>

<span data-ttu-id="f97bc-190">Ora è possibile codificare gli asset caricati.</span><span class="sxs-lookup"><span data-stu-id="f97bc-190">You can now encode your uploaded assets.</span></span> <span data-ttu-id="f97bc-191">Per altre informazioni, vedere [Encode assets](media-services-portal-encode.md)(Codificare gli asset).</span><span class="sxs-lookup"><span data-stu-id="f97bc-191">For more information, see [Encode assets](media-services-portal-encode.md).</span></span>

<span data-ttu-id="f97bc-192">È possibile utilizzare anche funzioni Azure tootrigger un processo di codifica in base a un file in arrivo nel contenitore hello configurato.</span><span class="sxs-lookup"><span data-stu-id="f97bc-192">You can also use Azure Functions tootrigger an encoding job based on a file arriving in hello configured container.</span></span> <span data-ttu-id="f97bc-193">Per altre informazioni, vedere [questo esempio](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ ).</span><span class="sxs-lookup"><span data-stu-id="f97bc-193">For more information, see [this sample](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ ).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="f97bc-194">Percorsi di apprendimento di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="f97bc-194">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="f97bc-195">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="f97bc-195">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-step"></a><span data-ttu-id="f97bc-196">Passaggio successivo</span><span class="sxs-lookup"><span data-stu-id="f97bc-196">Next step</span></span>
<span data-ttu-id="f97bc-197">Ora che è stato caricato un asset tooMedia Services, visitare toohello [come un processore di contenuti multimediali tooGet] [ How tooGet a Media Processor] argomento.</span><span class="sxs-lookup"><span data-stu-id="f97bc-197">Now that you have uploaded an asset tooMedia Services, go toohello [How tooGet a Media Processor][How tooGet a Media Processor] topic.</span></span>

[How tooGet a Media Processor]: media-services-get-media-processor.md

