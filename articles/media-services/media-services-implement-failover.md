---
title: failover aaaImplement streaming con servizi multimediali di Azure | Documenti Microsoft
description: Questo argomento viene illustrato come tooimplement uno scenario di streaming di failover.
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: fc45d849-eb0d-4739-ae91-0ff648113445
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/05/2017
ms.author: juliako
ms.openlocfilehash: ade0bace57f35ab3ed855d3a98f743e08da4f324
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="implement-failover-streaming-with-azure-media-services"></a><span data-ttu-id="e23d7-103">Implementare lo streaming del failover con Servizi multimediali di Azure</span><span class="sxs-lookup"><span data-stu-id="e23d7-103">Implement failover streaming with Azure Media Services</span></span>

<span data-ttu-id="e23d7-104">Questa procedura dettagliata illustra come contenuto toocopy (BLOB) da un asset in un altro ridondanza toohandle ordine per lo streaming su richiesta.</span><span class="sxs-lookup"><span data-stu-id="e23d7-104">This walkthrough demonstrates how toocopy content (blobs) from one asset into another in order toohandle redundancy for on-demand streaming.</span></span> <span data-ttu-id="e23d7-105">Questo scenario è utile se si desidera tooset backup Azure Content Delivery Network toofail sulla tra due Data Center, in caso di interruzione in un Data Center.</span><span class="sxs-lookup"><span data-stu-id="e23d7-105">This scenario is useful if you want tooset up Azure Content Delivery Network toofail over between two datacenters, in case of an outage in one datacenter.</span></span> <span data-ttu-id="e23d7-106">Questa procedura dettagliata Usa hello Azure Media Services SDK, API REST di servizi multimediali di Azure hello e hello toodemonstrate di Azure Storage SDK hello seguenti attività:</span><span class="sxs-lookup"><span data-stu-id="e23d7-106">This walkthrough uses hello Azure Media Services SDK, hello Azure Media Services REST API, and hello Azure Storage SDK toodemonstrate hello following tasks:</span></span>

1. <span data-ttu-id="e23d7-107">Configurare un account di Servizi multimediali nel "Data center A".</span><span class="sxs-lookup"><span data-stu-id="e23d7-107">Set up a Media Services account in "Data Center A."</span></span>
2. <span data-ttu-id="e23d7-108">Caricare in un asset di origine un file in formato intermedio.</span><span class="sxs-lookup"><span data-stu-id="e23d7-108">Upload a mezzanine file into a source asset.</span></span>
3. <span data-ttu-id="e23d7-109">Codificare l'asset hello in velocità più bit MP4 file.</span><span class="sxs-lookup"><span data-stu-id="e23d7-109">Encode hello asset into multi-bit rate MP4 files.</span></span> 
4. <span data-ttu-id="e23d7-110">Creare un localizzatore per la firma di accesso condiviso di sola lettura.</span><span class="sxs-lookup"><span data-stu-id="e23d7-110">Create a read-only shared access signature locator.</span></span> <span data-ttu-id="e23d7-111">Si tratta di contenitore di toohello l'accesso in lettura per la toohave asset hello origine nell'account di archiviazione hello è associata a una risorsa di origine hello.</span><span class="sxs-lookup"><span data-stu-id="e23d7-111">This is for hello source asset toohave read access toohello container in hello storage account that is associated with hello source asset.</span></span>
5. <span data-ttu-id="e23d7-112">Ottenere il nome di contenitore hello dell'asset origine hello dal localizzatore di firma di accesso condiviso di sola lettura hello creato nel passaggio precedente hello.</span><span class="sxs-lookup"><span data-stu-id="e23d7-112">Get hello container name of hello source asset from hello read-only shared access signature locator created in hello previous step.</span></span> <span data-ttu-id="e23d7-113">Questa operazione è necessaria per la copia di BLOB tra account di archiviazione (descritte nell'argomento hello).</span><span class="sxs-lookup"><span data-stu-id="e23d7-113">This is necessary for copying blobs between storage accounts (explained later in hello topic.)</span></span>
6. <span data-ttu-id="e23d7-114">Creare un localizzatore di origine per asset hello che è stato creato dall'attività di codifica hello.</span><span class="sxs-lookup"><span data-stu-id="e23d7-114">Create an origin locator for hello asset that was created by hello encoding task.</span></span> 

<span data-ttu-id="e23d7-115">Quindi, toohandle hello failover:</span><span class="sxs-lookup"><span data-stu-id="e23d7-115">Then, toohandle hello failover:</span></span>

1. <span data-ttu-id="e23d7-116">Configurare un account di Servizi multimediali nel "Data center B".</span><span class="sxs-lookup"><span data-stu-id="e23d7-116">Set up a Media Services account in "Data Center B."</span></span>
2. <span data-ttu-id="e23d7-117">Creare un asset vuoto di destinazione nella destinazione hello account di servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="e23d7-117">Create a target empty asset in hello target Media Services account.</span></span>
3. <span data-ttu-id="e23d7-118">Creare un localizzatore per la firma di accesso condiviso di scrittura.</span><span class="sxs-lookup"><span data-stu-id="e23d7-118">Create a write shared access signature locator.</span></span> <span data-ttu-id="e23d7-119">Si tratta di contenitore di toohello l'accesso in scrittura per la toohave asset vuoto hello destinazione nell'account di archiviazione di destinazione hello è associata a una risorsa di destinazione hello.</span><span class="sxs-lookup"><span data-stu-id="e23d7-119">This is for hello target empty asset toohave write access toohello container in hello target storage account that is associated with hello target asset.</span></span>
4. <span data-ttu-id="e23d7-120">Utilizzano hello Azure Storage SDK toocopy BLOB (file di asset) tra l'account di archiviazione di origine hello in "Data Center A" e l'account di archiviazione di destinazione hello "Data Center b."</span><span class="sxs-lookup"><span data-stu-id="e23d7-120">Use hello Azure Storage SDK toocopy blobs (asset files) between hello source storage account in "Data Center A" and hello target storage account in "Data Center B."</span></span> <span data-ttu-id="e23d7-121">Questi account di archiviazione sono associati a risorse hello di interesse.</span><span class="sxs-lookup"><span data-stu-id="e23d7-121">These storage accounts are associated with hello assets of interest.</span></span>
5. <span data-ttu-id="e23d7-122">Associare oggetti BLOB (file di asset) che sono stati copiati toohello un contenitore di destinazione blob con la risorsa di destinazione hello.</span><span class="sxs-lookup"><span data-stu-id="e23d7-122">Associate blobs (asset files) that were copied toohello target blob container with hello target asset.</span></span> 
6. <span data-ttu-id="e23d7-123">Creare un localizzatore di origine per le risorse hello "Data Center B" e specificare ID localizzatore hello che è stato generato per le risorse hello "Data Center a".</span><span class="sxs-lookup"><span data-stu-id="e23d7-123">Create an origin locator for hello asset in "Data Center B", and specify hello locator ID that was generated for hello asset in "Data Center A."</span></span>

<span data-ttu-id="e23d7-124">In questo modo si hello URL di streaming in cui i percorsi relativi degli URL hello hello sono hello stesso (solo hello base URL sono diversi).</span><span class="sxs-lookup"><span data-stu-id="e23d7-124">This gives you hello streaming URLs where hello relative paths of hello URLs are hello same (only hello base URLs are different).</span></span> 

<span data-ttu-id="e23d7-125">Quindi, toohandle eventuali interruzioni, è possibile creare una rete CDN sopra i localizzatori di origine.</span><span class="sxs-lookup"><span data-stu-id="e23d7-125">Then, toohandle any outages, you can create a Content Delivery Network on top of these origin locators.</span></span> 

<span data-ttu-id="e23d7-126">si applica Hello seguenti considerazioni:</span><span class="sxs-lookup"><span data-stu-id="e23d7-126">hello following considerations apply:</span></span>

* <span data-ttu-id="e23d7-127">versione corrente di Hello di Media Services SDK non supporta a livello di programmazione generazione IAssetFile informazioni che associato a un asset del file di asset.</span><span class="sxs-lookup"><span data-stu-id="e23d7-127">hello current version of Media Services SDK does not support programmatically generating IAssetFile information that would associate an asset with asset files.</span></span> <span data-ttu-id="e23d7-128">Utilizzare invece hello API REST di servizi multimediali CreateFileInfos toodo questo.</span><span class="sxs-lookup"><span data-stu-id="e23d7-128">Instead, use hello CreateFileInfos Media Services REST API toodo this.</span></span> 
* <span data-ttu-id="e23d7-129">Asset crittografato di archiviazione (AssetCreationOptions.StorageEncrypted) non sono supportati per la replica (perché la chiave di crittografia hello è differente in entrambi gli account di servizi multimediali).</span><span class="sxs-lookup"><span data-stu-id="e23d7-129">Storage encrypted assets (AssetCreationOptions.StorageEncrypted) are not supported for replication (because hello encryption key is different in both Media Services accounts).</span></span> 
* <span data-ttu-id="e23d7-130">Se si desidera tootake vantaggio della creazione dinamica dei pacchetti, verificare che sia di hello da cui si desidera toostream endpoint di streaming del contenuto in hello **esecuzione** stato.</span><span class="sxs-lookup"><span data-stu-id="e23d7-130">If you want tootake advantage of dynamic packaging, make sure hello streaming endpoint from which you want toostream  your content is in hello **Running** state.</span></span>

> [!NOTE]
> <span data-ttu-id="e23d7-131">Considerare l'utilizzo di servizi multimediali hello [strumento Replicator](http://replicator.codeplex.com/) come un'alternativa tooimplementing un scenario di streaming manualmente il failover.</span><span class="sxs-lookup"><span data-stu-id="e23d7-131">Consider using hello Media Services [Replicator Tool](http://replicator.codeplex.com/) as an alternative tooimplementing a failover streaming scenario manually.</span></span> <span data-ttu-id="e23d7-132">Questo strumento consente di asset tooreplicate tra due account di servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="e23d7-132">This tool allows you tooreplicate assets across two Media Services accounts.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="e23d7-133">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="e23d7-133">Prerequisites</span></span>
* <span data-ttu-id="e23d7-134">Due account di Servizi multimediali in una sottoscrizione di Azure nuova o esistente.</span><span class="sxs-lookup"><span data-stu-id="e23d7-134">Two Media Services accounts in a new or existing Azure subscription.</span></span> <span data-ttu-id="e23d7-135">Vedere [come un Account di servizi multimediali tooCreate](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="e23d7-135">See [How tooCreate a Media Services Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="e23d7-136">Sistemi operativi: Windows 7, Windows 2008 R2 o Windows 8.</span><span class="sxs-lookup"><span data-stu-id="e23d7-136">Operating system: Windows 7, Windows 2008 R2, or Windows 8.</span></span>
* <span data-ttu-id="e23d7-137">.NET Framework 4.5 o .NET Framework 4.</span><span class="sxs-lookup"><span data-stu-id="e23d7-137">.NET Framework 4.5 or .NET Framework 4.</span></span>
* <span data-ttu-id="e23d7-138">Visual Studio 2010 SP1 o versioni successive (Professional, Premium, Ultimate o Express).</span><span class="sxs-lookup"><span data-stu-id="e23d7-138">Visual Studio 2010 SP1 or later version (Professional, Premium, Ultimate, or Express).</span></span>

## <a name="set-up-your-project"></a><span data-ttu-id="e23d7-139">Configurare il progetto</span><span class="sxs-lookup"><span data-stu-id="e23d7-139">Set up your project</span></span>
<span data-ttu-id="e23d7-140">In questa sezione si crea e si configura un progetto di applicazione console in C#.</span><span class="sxs-lookup"><span data-stu-id="e23d7-140">In this section, you create and set up a C# Console Application project.</span></span>

1. <span data-ttu-id="e23d7-141">Utilizzare Visual Studio toocreate una nuova soluzione contenente il progetto di applicazione Console c# hello.</span><span class="sxs-lookup"><span data-stu-id="e23d7-141">Use Visual Studio toocreate a new solution that contains hello C# Console Application project.</span></span> <span data-ttu-id="e23d7-142">Immettere **HandleRedundancyForOnDemandStreaming** nome hello e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="e23d7-142">Enter **HandleRedundancyForOnDemandStreaming** for hello name, and then click **OK**.</span></span>
2. <span data-ttu-id="e23d7-143">Creare hello **SupportFiles** cartella hello stesso livello come hello **HandleRedundancyForOnDemandStreaming.csproj** file di progetto.</span><span class="sxs-lookup"><span data-stu-id="e23d7-143">Create hello **SupportFiles** folder on hello same level as hello **HandleRedundancyForOnDemandStreaming.csproj** project file.</span></span> <span data-ttu-id="e23d7-144">In hello **SupportFiles** cartella, creare hello **OutputFiles** e **MP4Files** cartelle.</span><span class="sxs-lookup"><span data-stu-id="e23d7-144">Under hello **SupportFiles** folder, create hello **OutputFiles** and **MP4Files** folders.</span></span> <span data-ttu-id="e23d7-145">Copiare un file MP4 in hello **MP4Files** cartella.</span><span class="sxs-lookup"><span data-stu-id="e23d7-145">Copy an .mp4 file into hello **MP4Files** folder.</span></span> <span data-ttu-id="e23d7-146">(In questo esempio hello **BigBuckBunny.mp4** file viene utilizzato.)</span><span class="sxs-lookup"><span data-stu-id="e23d7-146">(In this example, hello **BigBuckBunny.mp4** file is used.)</span></span> 
3. <span data-ttu-id="e23d7-147">Utilizzare **Nuget** tooMedia servizi correlati a tooadd riferimenti tooDLLs.</span><span class="sxs-lookup"><span data-stu-id="e23d7-147">Use **Nuget** tooadd references tooDLLs related tooMedia Services.</span></span> <span data-ttu-id="e23d7-148">Nel **menu principale di Visual Studio** scegliere **STRUMENTI** > **Library Package Manager (Gestione pacchetti libreria)** >  **Console di Gestione pacchetti**.</span><span class="sxs-lookup"><span data-stu-id="e23d7-148">In **Visual Studio Main Menu**, select **TOOLS** > **Library Package Manager** > **Package Manager Console**.</span></span> <span data-ttu-id="e23d7-149">Nella finestra della console hello, digitare **windowsazure. mediaservices Install-Package**, e premere INVIO.</span><span class="sxs-lookup"><span data-stu-id="e23d7-149">In hello console window, type **Install-Package windowsazure.mediaservices**, and press Enter.</span></span>
4. <span data-ttu-id="e23d7-150">Aggiungere gli altri riferimenti necessari per il progetto: System.Configuration, System.Runtime.Serialization e System.Web.</span><span class="sxs-lookup"><span data-stu-id="e23d7-150">Add other references that are required for this project: System.Configuration, System.Runtime.Serialization, and System.Web.</span></span>
5. <span data-ttu-id="e23d7-151">Sostituire **utilizzando** istruzioni che sono stati aggiunti toohello **Programs.cs** file per impostazione predefinita con hello quelli seguenti:</span><span class="sxs-lookup"><span data-stu-id="e23d7-151">Replace **using** statements that were added toohello **Programs.cs** file by default with hello following ones:</span></span>
   
        using System;
        using System.Configuration;
        using System.Globalization;
        using System.IO;
        using System.Net;
        using System.Runtime.Serialization.Json;
        using System.Text;
        using System.Threading;
        using System.Threading.Tasks;
        using System.Web;
        using System.Xml;
        using System.Linq;
        using Microsoft.WindowsAzure;
        using Microsoft.WindowsAzure.MediaServices.Client;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Blob;
        using Microsoft.WindowsAzure.Storage.Auth;
6. <span data-ttu-id="e23d7-152">Aggiungere hello **appSettings** sezione toohello **config** file e aggiornare i valori di hello in base alla servizi multimediali e archiviazione di valori di chiave e il nome.</span><span class="sxs-lookup"><span data-stu-id="e23d7-152">Add hello **appSettings** section toohello **.config** file, and update hello values based on your Media Services and Storage key and name values.</span></span> 
   
        <appSettings>
          <add key="MediaServicesAccountNameSource" value="Media-Services-Account-Name-Source"/>
          <add key="MediaServicesAccountKeySource" value="Media-Services-Account-Key-Source"/>
          <add key="MediaServicesStorageAccountNameSource" value="Media-Services-Storage-Account-Name-Source"/>
          <add key="MediaServicesStorageAccountKeySource" value="Media-Services-Storage-Account-Key-Source"/>
          <add key="MediaServicesAccountNameTarget" value="Media-Services-Account-Name-Target" />
          <add key="MediaServicesAccountKeyTarget" value=" Media-Services-Account-Key-Target" />
          <add key="MediaServicesStorageAccountNameTarget" value=" Media-Services-Storage-Account-Name-Target" />
          <add key="MediaServicesStorageAccountKeyTarget" value=" Media-Services-Storage-Account-Key-Target" />
        </appSettings>

## <a name="add-code-that-handles-redundancy-for-on-demand-streaming"></a><span data-ttu-id="e23d7-153">Aggiungere un codice in grado di gestire la ridondanza per lo streaming on demand</span><span class="sxs-lookup"><span data-stu-id="e23d7-153">Add code that handles redundancy for on-demand streaming</span></span>
<span data-ttu-id="e23d7-154">In questa sezione si crea ridondanza toohandle possibilità di hello.</span><span class="sxs-lookup"><span data-stu-id="e23d7-154">In this section, you create hello ability toohandle redundancy.</span></span>

1. <span data-ttu-id="e23d7-155">Aggiungere hello seguente classe Program toohello di campi a livello di classe.</span><span class="sxs-lookup"><span data-stu-id="e23d7-155">Add hello following class-level fields toohello Program class.</span></span>
       
        // Read values from hello App.config file.
        private static readonly string MediaServicesAccountNameSource = ConfigurationManager.AppSettings["MediaServicesAccountNameSource"];
        private static readonly string MediaServicesAccountKeySource = ConfigurationManager.AppSettings["MediaServicesAccountKeySource"];
        private static readonly string StorageNameSource = ConfigurationManager.AppSettings["MediaServicesStorageAccountNameSource"];
        private static readonly string StorageKeySource = ConfigurationManager.AppSettings["MediaServicesStorageAccountKeySource"];
        
        private static readonly string MediaServicesAccountNameTarget = ConfigurationManager.AppSettings["MediaServicesAccountNameTarget"];
        private static readonly string MediaServicesAccountKeyTarget = ConfigurationManager.AppSettings["MediaServicesAccountKeyTarget"];
        private static readonly string StorageNameTarget = ConfigurationManager.AppSettings["MediaServicesStorageAccountNameTarget"];
        private static readonly string StorageKeyTarget = ConfigurationManager.AppSettings["MediaServicesStorageAccountKeyTarget"];
        
        // Base support files path.  Update this field toopoint toohello base path  
        // for hello local support files folder that you create. 
        private static readonly string SupportFiles = Path.GetFullPath(@"../..\SupportFiles");
        
        // Paths toosupport files (within hello above base path). 
        private static readonly string SingleInputMp4Path = Path.GetFullPath(SupportFiles + @"\MP4Files\BigBuckBunny.mp4");
        private static readonly string OutputFilesFolder = Path.GetFullPath(SupportFiles + @"\OutputFiles");
        
        // Class-level field used tookeep a reference toohello service context.
        static private CloudMediaContext _contextSource = null;
        static private CloudMediaContext _contextTarget = null;
        static private MediaServicesCredentials _cachedCredentialsSource = null;
        static private MediaServicesCredentials _cachedCredentialsTarget = null;

2. <span data-ttu-id="e23d7-156">Sostituire definizione del metodo Main hello predefinito con hello segue quello.</span><span class="sxs-lookup"><span data-stu-id="e23d7-156">Replace hello default Main method definition with hello following one.</span></span> <span data-ttu-id="e23d7-157">Di seguito sono specificate le definizioni dei metodi chiamate da Main.</span><span class="sxs-lookup"><span data-stu-id="e23d7-157">Method definitions that are called from Main are defined below.</span></span>
        
        static void Main(string[] args)
        {
            _cachedCredentialsSource = new MediaServicesCredentials(
                            MediaServicesAccountNameSource,
                            MediaServicesAccountKeySource);
        
            _cachedCredentialsTarget = new MediaServicesCredentials(
                            MediaServicesAccountNameTarget,
                            MediaServicesAccountKeyTarget);
        
            // Get server context.    
            _contextSource = new CloudMediaContext(_cachedCredentialsSource);
            _contextTarget = new CloudMediaContext(_cachedCredentialsTarget);
        
            IAsset assetSingleFile = CreateAssetAndUploadSingleFile(_contextSource,
                                        AssetCreationOptions.None,
                                        SingleInputMp4Path);
        
            IJob job = CreateEncodingJob(_contextSource, assetSingleFile);
        
            if (job.State != JobState.Error)
            {
                IAsset sourceOutputAsset = job.OutputMediaAssets[0];
                // Get hello locator for Smooth Streaming
                var sourceOriginLocator = GetStreamingOriginLocator(_contextSource, sourceOutputAsset);
        
                Console.WriteLine("Locator Id: {0}", sourceOriginLocator.Id);
                
                // 1.Create a read-only SAS locator for hello source asset toohave read access toohello container in hello source Storage account (associated with hello source Media Services account)
                var readSasLocator = GetSasReadLocator(_contextSource, sourceOutputAsset);
        
                // 2.Get hello container name of hello source asset from hello read-only SAS locator created in hello previous step
                string containerName = (new Uri(readSasLocator.Path)).Segments[1];
        
                // 3.Create a target empty asset in hello target Media Services account
                var targetAsset = CreateTargetEmptyAsset(_contextTarget, containerName);
        
                // 4.Create a write SAS locator for hello target empty asset toohave write access toohello container in hello target Storage account (associated with hello target Media Services account)
                ILocator writeSasLocator = CreateSasWriteLocator(_contextTarget, targetAsset);
        
                // Get asset container name.
                string targetContainerName = (new Uri(writeSasLocator.Path)).Segments[1];
        
                // 5.Copy hello blobs in hello source container (source asset) toohello target container (target empty asset)
                CopyBlobsFromDifferentStorage(containerName, targetContainerName, StorageNameSource, StorageKeySource, StorageNameTarget, StorageKeyTarget);
        
                // 6.Use hello CreateFileInfos Media Services REST API tooautomatically generate all hello IAssetFile’s for hello target asset. 
                //      This API call is not supported in hello current Media Services SDK for .NET. 
                CreateFileInfosForAssetWithRest(_contextTarget, targetAsset, MediaServicesAccountNameTarget, MediaServicesAccountKeyTarget);
        
                // Check if hello AssetFiles are now  associated with hello asset.
                Console.WriteLine("Asset files assocated with hello {0} asset:", targetAsset.Name);
                foreach (var af in targetAsset.AssetFiles)
                {
                    Console.WriteLine(af.Name);
                }
        
                // 7.Copy hello Origin locator of hello source asset toohello target asset by using hello same Id
                var replicatedLocatorPath = CreateOriginLocatorWithRest(_contextTarget,
                            MediaServicesAccountNameTarget, MediaServicesAccountKeyTarget,
                            sourceOriginLocator.Id, targetAsset.Id);
        
                // Create a full URL toohello manifest file. Use this for playback
                // in streaming media clients. 
                string originalUrlForClientStreaming = sourceOriginLocator.Path + GetPrimaryFile(sourceOutputAsset).Name + "/manifest";
        
                Console.WriteLine("Original Locator Path: {0}\n", originalUrlForClientStreaming);
        
                string replicatedUrlForClientStreaming = replicatedLocatorPath + GetPrimaryFile(sourceOutputAsset).Name + "/manifest";
        
                Console.WriteLine("Replicated Locator Path: {0}", replicatedUrlForClientStreaming);
        
                readSasLocator.Delete();
                writeSasLocator.Delete();
        }

3. <span data-ttu-id="e23d7-158">Hello le definizioni di metodo che seguono viene chiamato dal metodo Main.</span><span class="sxs-lookup"><span data-stu-id="e23d7-158">hello following method definitions are called from Main.</span></span>

    >[!NOTE]
    ><span data-ttu-id="e23d7-159">È previsto un limite di 1.000.000 di criteri per i diversi criteri di Servizi multimediali (ad esempio per i criteri Locator o ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="e23d7-159">There is a limit of 1,000,000 policies for different Media Services policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="e23d7-160">È consigliabile utilizzare hello stesso ID di criteri, se si utilizza sempre hello stesso giorni e accesso le autorizzazioni.</span><span class="sxs-lookup"><span data-stu-id="e23d7-160">You should use hello same policy ID if you are always using hello same days and access permissions.</span></span> <span data-ttu-id="e23d7-161">Ad esempio, è possibile utilizzare hello ID per i criteri per i localizzatori che sono previsti tooremain sul posto per un lungo periodo (non-caricamento criteri).</span><span class="sxs-lookup"><span data-stu-id="e23d7-161">For example, use hello same ID for policies for locators that are intended tooremain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="e23d7-162">Per altre informazioni, vedere [questo argomento](media-services-dotnet-manage-entities.md#limit-access-policies).</span><span class="sxs-lookup"><span data-stu-id="e23d7-162">For more information, see [this topic](media-services-dotnet-manage-entities.md#limit-access-policies).</span></span>

        public static IAsset CreateAssetAndUploadSingleFile(CloudMediaContext context,
                                                        AssetCreationOptions assetCreationOptions,
                                                        string singleFilePath)
        {
            var assetName = "UploadSingleFile_" + DateTime.UtcNow.ToString();
   
            var asset = context.Assets.Create(assetName, assetCreationOptions);
   
            Console.WriteLine("Asset name: " + asset.Name);
   
            var fileName = Path.GetFileName(singleFilePath);
   
            var assetFile = asset.AssetFiles.Create(fileName);
   
            Console.WriteLine("Created assetFile {0}", assetFile.Name);
   
            Console.WriteLine("Upload {0}", assetFile.Name);
   
            assetFile.Upload(singleFilePath);
            Console.WriteLine("Done uploading of {0}", assetFile.Name);
   
            return asset;
        }
   
        public static IJob CreateEncodingJob(CloudMediaContext context, IAsset asset)
        {
            // Declare a new job.
            IJob job = context.Jobs.Create("My encoding job");
   
            // Get a media processor reference, and pass tooit hello name of hello 
            // processor toouse for hello specific task.
            IMediaProcessor processor = GetLatestMediaProcessorByName(context,
                                                    "Media Encoder Standard");
   
            // Create a task with hello encoding details, using a string preset.
            // In this case "Adaptive Streaming" preset is used.
            ITask task = job.Tasks.AddNew("My encoding task",
                processor,
                "Adaptive Streaming",
                TaskOptions.ProtectedConfiguration);
   
            // Specify hello input asset toobe encoded.
            task.InputAssets.Add(asset);
   
            // Add an output asset toocontain hello results of hello job. 
            // This output is specified as AssetCreationOptions.None, which 
            // means hello output asset is in hello clear (unencrypted). 
            var outputAssetName = "OutputAsset_" + Guid.NewGuid();
            task.OutputAssets.AddNew(outputAssetName,
                AssetCreationOptions.None);
   
            // Use hello following event handler toocheck job progress.  
            job.StateChanged += new
                    EventHandler<JobStateChangedEventArgs>(StateChanged);
   
            // Launch hello job.
            job.Submit();
   
            // Optionally log job details. This displays basic job details
            // toohello console and saves them tooa JobDetails-{JobId}.txt file 
            // in your output folder.
            LogJobDetails(context, job.Id);
   
            // Check job execution and wait for job toofinish. 
            Task progressJobTask = job.GetExecutionProgressTask(CancellationToken.None);
            progressJobTask.Wait();
   
            // Get an updated job reference.
            job = GetJob(context, job.Id);
   
            // Since we hello output asset contains a set of Smooth Streaming files,
            // set hello .ism file toobe hello primary file
            if (job.State != JobState.Error)
                SetPrimaryFile(job.OutputMediaAssets[0]);
   
            return job;
        }
   
        public static ILocator GetStreamingOriginLocator(CloudMediaContext context, IAsset assetToStream)
        {
            // Get a reference toohello streaming manifest file from hello  
            // collection of files in hello asset. 
            IAssetFile manifestFile = GetPrimaryFile(assetToStream);
   
            // Create a 30-day readonly access policy. 
            // You cannot create a streaming locator using an AccessPolicy that includes write or delete permissions.            
   
            IAccessPolicy policy = context.AccessPolicies.Create("Streaming policy",
                TimeSpan.FromDays(30),
                AccessPermissions.Read);
   
            // Create a locator toohello streaming content on an origin. 
            ILocator originLocator = context.Locators.CreateLocator(LocatorType.OnDemandOrigin,
                assetToStream,
                policy,
                DateTime.UtcNow.AddMinutes(-5));
   
            // Return hello locator. 
            return originLocator;
        }
   
        public static ILocator GetSasReadLocator(CloudMediaContext context, IAsset asset)
        {
            IAccessPolicy accessPolicy = context.AccessPolicies.Create("File Download Policy",
                TimeSpan.FromDays(30), AccessPermissions.Read);
   
            ILocator sasLocator = context.Locators.CreateLocator(LocatorType.Sas,
                asset, accessPolicy);
   
            return sasLocator;
        }
   
        public static ILocator CreateSasWriteLocator(CloudMediaContext context, IAsset asset)
        {
   
            IAccessPolicy writePolicy = context.AccessPolicies.Create("Write Policy",
                TimeSpan.FromDays(30), AccessPermissions.Write);
   
            ILocator sasLocator = context.Locators.CreateLocator(LocatorType.Sas,
                asset, writePolicy);
   
            return sasLocator;
        }
   
        public static IAsset CreateTargetEmptyAsset(CloudMediaContext context, string containerName)
        {
            // Create a new asset.
            IAsset assetToBeProcessed = context.Assets.Create(containerName,
                AssetCreationOptions.None);
   
            return assetToBeProcessed;
        }
   
        public static void CreateFileInfosForAssetWithRest(CloudMediaContext context, IAsset asset, string mediaServicesAccountNameTarget,
            string mediaServicesAccountKeyTarget)
        {
            string apiServer = "";
            string scope = "";
            string acsBaseAddress = "";
   
            string acsToken = GetAcsBearerToken(mediaServicesAccountNameTarget,
                                    mediaServicesAccountKeyTarget, scope, acsBaseAddress);
   
            if (!string.IsNullOrEmpty(acsToken))
            {
                CreateFileInfos(apiServer, acsToken, asset.Id);
            }
        }
   
        public static string CreateOriginLocatorWithRest(CloudMediaContext context, string mediaServicesAccountNameTarget,
            string mediaServicesAccountKeyTarget, string locatorIdToReplicate, string targetAssetId)
        {
            //Make sure we are not asking for a duplicate:
            var locator = context.Locators.Where(l => l.Id == locatorIdToReplicate).FirstOrDefault();
            if (locator != null)
                return "";
   
            string locatorNewPath = "";
            string apiServer = "";
            string scope = "";
            string acsBaseAddress = "";
   
            string acsToken = GetAcsBearerToken(mediaServicesAccountNameTarget,
                                    mediaServicesAccountKeyTarget, scope, acsBaseAddress);
   
            if (!string.IsNullOrEmpty(acsToken))
            {
                var asset = context.Assets.Where(a => a.Id == targetAssetId).FirstOrDefault();
   
                // You cannot create a streaming locator using an AccessPolicy that includes write or delete permissions.            
                var accessPolicy = context.AccessPolicies.Create("RestTest", TimeSpan.FromDays(100),
                                                                    AccessPermissions.Read);
                if (asset != null)
                {
                    string redirectedServiceUri = null;
   
                    var xmlResponse = CreateLocator(apiServer, out redirectedServiceUri, acsToken,
                                                                asset.Id, accessPolicy.Id,
                                                                (int)LocatorType.OnDemandOrigin,
                                                                DateTime.UtcNow.AddMinutes(-10), locatorIdToReplicate);
   
                    Console.WriteLine("Redirected to: " + redirectedServiceUri);
                    if (xmlResponse != null)
                    {
                        Console.WriteLine(String.Format("Locator Id: {0}",
                                                        xmlResponse.GetElementsByTagName("Id")[0].InnerText));
                        Console.WriteLine(String.Format("Locator Path: {0}",
                                xmlResponse.GetElementsByTagName("Path")[0].InnerText));

                        locatorNewPath = xmlResponse.GetElementsByTagName("Path")[0].InnerText;
                    }
                }
            }

            return locatorNewPath;
        }

        public static void SetPrimaryFile(IAsset asset)
        {

            var ismAssetFiles = asset.AssetFiles.ToList().
                        Where(f => f.Name.EndsWith(".ism", StringComparison.OrdinalIgnoreCase))
                        .ToArray();

            if (ismAssetFiles.Count() != 1)
                throw new ArgumentException("hello asset should have only one, .ism file");

            ismAssetFiles.First().IsPrimary = true;
            ismAssetFiles.First().Update();
        }

        public static IAssetFile GetPrimaryFile(IAsset asset)
        {
            var theManifest =
                    from f in asset.AssetFiles
                    where f.Name.EndsWith(".ism")
                    select f;

            // Cast hello reference tooa true IAssetFile type. 
            IAssetFile manifestFile = theManifest.First();

            return manifestFile;
        }

        public static IAsset RefreshAsset(CloudMediaContext context, IAsset asset)
        {
            asset = context.Assets.Where(a => a.Id == asset.Id).FirstOrDefault();
            return asset;
        }

        public static void CopyBlobsFromDifferentStorage(string sourceContainerName, string targetContainerName,
                                            string srcAccountName, string srcAccountKey,
                                            string destAccountName, string destAccountKey)
        {
            var srcAccount = new CloudStorageAccount(new StorageCredentials(srcAccountName, srcAccountKey), true);
            var destAccount = new CloudStorageAccount(new StorageCredentials(destAccountName, destAccountKey), true);

            var cloudBlobClient = srcAccount.CreateCloudBlobClient();
            var targetBlobClient = destAccount.CreateCloudBlobClient();

            var sourceContainer = cloudBlobClient.GetContainerReference(sourceContainerName);
            var targetContainer = targetBlobClient.GetContainerReference(targetContainerName);
            targetContainer.CreateIfNotExists();

            string blobToken = sourceContainer.GetSharedAccessSignature(new SharedAccessBlobPolicy()
            {
                // Specify hello expiration time for hello signature.
                SharedAccessExpiryTime = DateTime.Now.AddDays(1),
                // Specify hello permissions granted by hello signature.
                Permissions = SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.Read
            });

            foreach (var sourceBlob in sourceContainer.ListBlobs())
            {
                string fileName = (sourceBlob as ICloudBlob).Name;
                var sourceCloudBlob = sourceContainer.GetBlockBlobReference(fileName);
                sourceCloudBlob.FetchAttributes();

                if (sourceCloudBlob.Properties.Length > 0)
                {
                    // In Azure Media Services, hello files are stored as block blobs. 
                    // Page blobs are not supported by Azure Media Services.  
                    var destinationBlob = targetContainer.GetBlockBlobReference(fileName);
                    destinationBlob.StartCopyFromBlob(new Uri(sourceBlob.Uri.AbsoluteUri + blobToken));

                    while (true)
                    {
                        // hello StartCopyFromBlob is an async operation, 
                        // so we want toocheck if hello copy operation is completed before proceeding. 
                        // toodo that, we call FetchAttributes on hello blob and check hello CopyStatus. 
                        destinationBlob.FetchAttributes();
                        if (destinationBlob.CopyState.Status != CopyStatus.Pending)
                        {
                            break;
                        }
                        //It's still not completed. So wait for some time.
                        System.Threading.Thread.Sleep(1000);
                    }
                }

                Console.WriteLine(fileName);
            }

            Console.WriteLine("Done copying.");
        }

        private static IMediaProcessor GetLatestMediaProcessorByName(CloudMediaContext context, string mediaProcessorName)
        {

            var processor = context.MediaProcessors.Where(p => p.Name == mediaProcessorName).
                ToList().OrderBy(p => new Version(p.Version)).LastOrDefault();

            if (processor == null)
                throw new ArgumentException(string.Format("Unknown media processor", mediaProcessorName));

            return processor;
        }

        // This method is a handler for events that track job progress.   
        private static void StateChanged(object sender, JobStateChangedEventArgs e)
        {
            Console.WriteLine("Job state changed event:");
            Console.WriteLine("  Previous state: " + e.PreviousState);
            Console.WriteLine("  Current state: " + e.CurrentState);

            switch (e.CurrentState)
            {
                case JobState.Finished:
                    Console.WriteLine();
                    Console.WriteLine("********************");
                    Console.WriteLine("Job is finished.");
                    Console.WriteLine("Please wait while local tasks or downloads complete...");
                    Console.WriteLine("********************");
                    Console.WriteLine();
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
                    LogJobStop(null, job.Id);
                    break;
                default:
                    break;
            }
        }

        private static void LogJobStop(CloudMediaContext context, string jobId)
        {
            StringBuilder builder = new StringBuilder();
            IJob job = GetJob(context, jobId);

            builder.AppendLine("\nThe job stopped due toocancellation or an error.");
            builder.AppendLine("***************************");
            builder.AppendLine("Job ID: " + job.Id);
            builder.AppendLine("Job Name: " + job.Name);
            builder.AppendLine("Job State: " + job.State.ToString());
            builder.AppendLine("Job started (server UTC time): " + job.StartTime.ToString());
            // Log job errors if they exist.  
            if (job.State == JobState.Error)
            {
                builder.Append("Error Details: \n");
                foreach (ITask task in job.Tasks)
                {
                    foreach (ErrorDetail detail in task.ErrorDetails)
                    {
                        builder.AppendLine("  Task Id: " + task.Id);
                        builder.AppendLine("    Error Code: " + detail.Code);
                        builder.AppendLine("    Error Message: " + detail.Message + "\n");
                    }
                }
            }
            builder.AppendLine("***************************\n");
            // Write hello output tooa local file and toohello console. hello template 
            // for an error output file is:  JobStop-{JobId}.txt
            string outputFile = OutputFilesFolder + @"\JobStop-" + JobIdAsFileName(job.Id) + ".txt";
            WriteToFile(outputFile, builder.ToString());
            Console.Write(builder.ToString());
        }

        private static void LogJobDetails(CloudMediaContext context, string jobId)
        {
            StringBuilder builder = new StringBuilder();
            IJob job = GetJob(context, jobId);

            builder.AppendLine("\nJob ID: " + job.Id);
            builder.AppendLine("Job Name: " + job.Name);
            builder.AppendLine("Job submitted (client UTC time): " + DateTime.UtcNow.ToString());

            // Write hello output tooa local file and toohello console. hello template 
            // for an error output file is:  JobDetails-{JobId}.txt
            string outputFile = OutputFilesFolder + @"\JobDetails-" + JobIdAsFileName(job.Id) + ".txt";
            WriteToFile(outputFile, builder.ToString());
            Console.Write(builder.ToString());
        }

        // Replace ":" with "_" in Job id values so they can 
        // be used as log file names.  
        private static string JobIdAsFileName(string jobID)
        {
            return jobID.Replace(":", "_");
        }

        // Write method output toohello output files folder.
        private static void WriteToFile(string outFilePath, string fileContent)
        {
            StreamWriter sr = File.CreateText(outFilePath);
            sr.WriteLine(fileContent);
            sr.Close();
        }

        private static IJob GetJob(CloudMediaContext context, string jobId)
        {
            // Use a Linq select query tooget an updated 
            // reference by Id. 
            var jobInstance =
                from j in context.Jobs
                where j.Id == jobId
                select j;

            // Return hello job reference as an Ijob. 
            IJob job = jobInstance.FirstOrDefault();

            return job;
        }

        private static IAsset GetAsset(CloudMediaContext context, string assetId)
        {
            // Use a LINQ Select query tooget an asset.
            var assetInstance =
                from a in context.Assets
                where a.Id == assetId
                select a;

            // Reference hello asset as an IAsset.
            IAsset asset = assetInstance.FirstOrDefault();

            return asset;
        }

        public static void DeleteAllAssets(CloudMediaContext context)
        {
            // Loop through and delete all assets.
            foreach (IAsset asset in context.Assets)
            {
                DeleteLocatorsForAsset(context, asset);

                asset.Delete();
            }
        }

        public static void DeleteLocatorsForAsset(CloudMediaContext context, IAsset asset)
        {
            string assetId = asset.Id;
            var locators = from a in context.Locators
                            where a.AssetId == assetId
                            select a;
            foreach (var locator in locators)
            {
                Console.WriteLine("Deleting locator {0} for asset {1}", locator.Path, assetId);

                locator.Delete();
            }
        }

        public static void DeleteAccessPolicy(CloudMediaContext context, string existingPolicyId)
        {
            // toodelete a specific access policy, get a reference toohello policy.  
            // based on hello policy Id passed toohello method.
            var policyInstance =
                    from p in context.AccessPolicies
                    where p.Id == existingPolicyId
                    select p;

            IAccessPolicy policy = policyInstance.FirstOrDefault();

            policy.Delete();

        }

        //////////////////////////////////////////////////////
        /// hello following methods use REST calls.
        //////////////////////////////////////////////////////

        public static string GetAcsBearerToken(string clientId, string clientSecret, string scope, string accessControlServiceUri)
        {
            if (string.IsNullOrEmpty(clientId))
                throw new ArgumentNullException("clientId");

            if (string.IsNullOrEmpty(clientSecret))
                throw new ArgumentNullException("clientSecret");

            if (string.IsNullOrEmpty(scope))
            {
                scope = "urn:WindowsAzureMediaServices";
            }
            else if (!scope.ToLower().StartsWith("urn:"))
            {
                scope = "urn:" + scope;
            }

            if (string.IsNullOrEmpty(accessControlServiceUri))
            {
                accessControlServiceUri = "https://wamsprodglobal001acs.accesscontrol.windows.net/v2/OAuth2-13";
            }
            else if (!accessControlServiceUri.ToLower().EndsWith("/v2/oauth2-13"))
            {
                accessControlServiceUri = accessControlServiceUri.TrimEnd('/') + "/v2/OAuth2-13";
            }

            HttpWebRequest request = (HttpWebRequest)HttpWebRequest.Create(accessControlServiceUri);
            request.Method = "POST";
            request.ContentType = "application/x-www-form-urlencoded";
            request.KeepAlive = true;
            string acsBearerToken = null;

            var requestBytes = Encoding.ASCII.GetBytes("grant_type=client_credentials&client_id=" +
                clientId + "&client_secret=" + HttpUtility.UrlEncode(clientSecret) +
                "&scope=" + HttpUtility.UrlEncode(scope));
            request.ContentLength = requestBytes.Length;

            var requestStream = request.GetRequestStream();
            requestStream.Write(requestBytes, 0, requestBytes.Length);
            requestStream.Close();

            var response = (HttpWebResponse)request.GetResponse();

            if (response.StatusCode == HttpStatusCode.OK)
            {
                using (Stream responseStream = response.GetResponseStream())
                {
                    using (StreamReader stream = new StreamReader(responseStream))
                    {
                        string responseString = stream.ReadToEnd();
                        var reader = JsonReaderWriterFactory.CreateJsonReader(Encoding.UTF8.GetBytes(responseString),
                            new XmlDictionaryReaderQuotas());

                        while (reader.Read())
                        {
                            if ((reader.Name == "access_token") && (reader.NodeType == XmlNodeType.Element))
                            {
                                if (reader.Read())
                                {
                                    acsBearerToken = reader.Value;
                                    break;
                                }
                            }
                        }
                    }
                }
            }

            return acsBearerToken;
        }

        public static XmlDocument CreateLocator(string mediaServicesApiServerUri,
                                                out string redirectedMediaServicesApiServerUri,
                                                string acsBearerToken, string assetId,
                                                string accessPolicyId, int locatorType,
                                                DateTime startTime, string locatorIdToReplicate = null,
                                                bool autoRedirect = true)
        {
            if (string.IsNullOrEmpty(mediaServicesApiServerUri))
            {
                mediaServicesApiServerUri = "https://media.windows.net/api/";
            }
            if (!mediaServicesApiServerUri.EndsWith("/"))
                mediaServicesApiServerUri = mediaServicesApiServerUri + "/";

            if (string.IsNullOrEmpty(acsBearerToken)) throw new ArgumentNullException("acsBearerToken");
            if (string.IsNullOrEmpty(assetId)) throw new ArgumentNullException("assetId");
            if (string.IsNullOrEmpty(accessPolicyId)) throw new ArgumentNullException("accessPolicyId");

            redirectedMediaServicesApiServerUri = null;
            XmlDocument xmlResponse = null;

            StringBuilder sb = new StringBuilder();
            sb.Append("{ \"AssetId\" : \"" + assetId + "\"");
            sb.Append(", \"AccessPolicyId\" : \"" + accessPolicyId + "\"");
            sb.Append(", \"Type\" : \"" + locatorType + "\"");
            if (startTime != DateTime.MinValue)
                sb.Append(", \"StartTime\" : \"" + startTime.ToString("G", CultureInfo.CreateSpecificCulture("en-us")) + "\"");
            if (!string.IsNullOrEmpty(locatorIdToReplicate))
                sb.Append(", \"Id\" : \"" + locatorIdToReplicate + "\"");
            sb.Append("}");

            string requestbody = sb.ToString();

            try
            {
                var request = GenerateRequest("POST", mediaServicesApiServerUri, "Locators",
                    null, acsBearerToken, requestbody);
                var response = (HttpWebResponse)request.GetResponse();

                switch (response.StatusCode)
                {
                    case HttpStatusCode.MovedPermanently:
                        //Recurse once with hello mediaServicesApiServerUri redirect Location:
                        if (autoRedirect)
                        {
                            redirectedMediaServicesApiServerUri = response.Headers["Location"];
                            string secondRedirection = null;
                            xmlResponse = CreateLocator(redirectedMediaServicesApiServerUri,
                                                        out secondRedirection, acsBearerToken,
                                                        assetId, accessPolicyId, locatorType,
                                                        startTime, locatorIdToReplicate, false);
                        }
                        else
                        {
                            Console.WriteLine("Redirection too{0} failed.",
                                mediaServicesApiServerUri);
                            return null;
                        }
                        break;
                    case HttpStatusCode.Created:
                        using (Stream responseStream = response.GetResponseStream())
                        {
                            using (StreamReader stream = new StreamReader(responseStream))
                            {
                                string responseString = stream.ReadToEnd();
                                var reader = JsonReaderWriterFactory.
                                    CreateJsonReader(Encoding.UTF8.GetBytes(responseString),
                                        new XmlDictionaryReaderQuotas());

                                xmlResponse = new XmlDocument();
                                reader.Read();
                                xmlResponse.LoadXml(reader.ReadInnerXml());
                            }
                        }
                        break;

                    default:
                        Console.WriteLine(response.StatusDescription);
                        break;
                }
            }
            catch (WebException ex)
            {
                Console.WriteLine(ex.Message);
            }

            return xmlResponse;
        }

        public static void CreateFileInfos(string mediaServicesApiServerUri,
                                    string acsBearerToken,
                                    string assetId
                                    )
        {
            if (String.IsNullOrEmpty(mediaServicesApiServerUri))
            {
                mediaServicesApiServerUri = "https://media.windows.net/api/";
            }
            if (!mediaServicesApiServerUri.EndsWith("/"))
                mediaServicesApiServerUri = mediaServicesApiServerUri + "/";

            if (String.IsNullOrEmpty(acsBearerToken)) throw new ArgumentNullException("acsBearerToken");
            if (String.IsNullOrEmpty(assetId)) throw new ArgumentNullException("assetId");


            string id = assetId.Replace(":", "%");

            UriBuilder builder = new UriBuilder(mediaServicesApiServerUri);
            builder.Path = Path.Combine(builder.Path, "CreateFileInfos");
            builder.Query = String.Format(CultureInfo.InvariantCulture, "assetid='{0}'", assetId);

            try
            {
                var request = GenerateRequest("GET", mediaServicesApiServerUri, "CreateFileInfos",
                    String.Format(CultureInfo.InvariantCulture, "assetid='{0}'", assetId), acsBearerToken, null);

                using (HttpWebResponse response = (HttpWebResponse)request.GetResponse())
                {
                    if (response.StatusCode == HttpStatusCode.MovedPermanently)
                    {
                        string redirectedMediaServicesApiUrl = response.Headers["Location"];

                        CreateFileInfos(redirectedMediaServicesApiUrl, acsBearerToken, assetId);
                    }
                    else if ((response.StatusCode != HttpStatusCode.OK) &&
                        (response.StatusCode != HttpStatusCode.Accepted) &&
                        (response.StatusCode != HttpStatusCode.Created) &&
                        (response.StatusCode != HttpStatusCode.NoContent))
                    {
                        // TODO: Throw a more specific exception.
                        throw new Exception("Invalid response received ");
                    }
                }
            }
            catch (WebException ex)
            {
                Console.WriteLine(ex.Message);
            }
        }

        private static HttpWebRequest GenerateRequest(string verb,
                                                        string mediaServicesApiServerUri,
                                                        string resourcePath, string query,
                                                        string acsBearerToken, string requestbody)
        {
            var uriBuilder = new UriBuilder(mediaServicesApiServerUri);
            uriBuilder.Path += resourcePath;
            if (query != null)
            {
                uriBuilder.Query = query;
            }
            HttpWebRequest request = (HttpWebRequest)HttpWebRequest.Create(uriBuilder.Uri);
            request.AllowAutoRedirect = false; //We manage our own redirects.
            request.Method = verb;

            if (resourcePath == "$metadata")
                request.MediaType = "application/xml";
            else
            {
                request.ContentType = "application/json;odata=verbose";
                request.Accept = "application/json;odata=verbose";
            }

            request.Headers.Add("DataServiceVersion", "3.0");
            request.Headers.Add("MaxDataServiceVersion", "3.0");
            request.Headers.Add("x-ms-version", "2.1");
            request.Headers.Add(HttpRequestHeader.Authorization, "Bearer " + acsBearerToken);

            if (requestbody != null)
            {
                var requestBytes = Encoding.ASCII.GetBytes(requestbody);
                request.ContentLength = requestBytes.Length;

                var requestStream = request.GetRequestStream();
                requestStream.Write(requestBytes, 0, requestBytes.Length);
                requestStream.Close();
            }
            else
            {
                request.ContentLength = 0;
            }
            return request;
        }

## <a name="next-steps"></a><span data-ttu-id="e23d7-163">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e23d7-163">Next steps</span></span>
<span data-ttu-id="e23d7-164">È possibile ora usare un richieste tooroute di gestione del traffico tra due Data Center di hello e quindi eseguire il failover in caso di eventuali interruzioni.</span><span class="sxs-lookup"><span data-stu-id="e23d7-164">You can now use a traffic manager tooroute requests between hello two datacenters, and thus fail over in case of any outages.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="e23d7-165">Percorsi di apprendimento di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="e23d7-165">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="e23d7-166">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="e23d7-166">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

