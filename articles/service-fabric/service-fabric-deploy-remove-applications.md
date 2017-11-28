---
title: distribuzione di applicazioni di Service Fabric aaaAzure | Documenti Microsoft
description: Come toodeploy e rimuovere le applicazioni nell'infrastruttura del servizio tramite PowerShell.
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: b120ffbf-f1e3-4b26-a492-347c29f8f66b
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/01/2017
ms.author: ryanwi
ms.openlocfilehash: 3de9c6a937ee7b29bf9ec86d6e9e631487797507
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-remove-applications-using-powershell"></a><span data-ttu-id="561a6-103">Distribuire e rimuovere applicazioni con PowerShell</span><span class="sxs-lookup"><span data-stu-id="561a6-103">Deploy and remove applications using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="561a6-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="561a6-104">PowerShell</span></span>](service-fabric-deploy-remove-applications.md)
> * [<span data-ttu-id="561a6-105">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="561a6-105">Visual Studio</span></span>](service-fabric-publish-app-remote-cluster.md)
> * [<span data-ttu-id="561a6-106">API client Fabric</span><span class="sxs-lookup"><span data-stu-id="561a6-106">FabricClient APIs</span></span>](service-fabric-deploy-remove-applications-fabricclient.md)
> 
> 

<br/>

<span data-ttu-id="561a6-107">Dopo aver creato il [pacchetto di un tipo di applicazione][10], è possibile distribuirlo in un cluster di Azure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="561a6-107">Once an [application type has been packaged][10], it's ready for deployment into an Azure Service Fabric cluster.</span></span> <span data-ttu-id="561a6-108">Distribuzione coinvolge hello tre passaggi:</span><span class="sxs-lookup"><span data-stu-id="561a6-108">Deployment involves hello following three steps:</span></span>

1. <span data-ttu-id="561a6-109">Caricare l'archivio di immagini toohello pacchetto applicazione hello</span><span class="sxs-lookup"><span data-stu-id="561a6-109">Upload hello application package toohello image store</span></span>
2. <span data-ttu-id="561a6-110">Registrare il tipo di applicazione hello</span><span class="sxs-lookup"><span data-stu-id="561a6-110">Register hello application type</span></span>
3. <span data-ttu-id="561a6-111">Creare l'istanza dell'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="561a6-111">Create hello application instance</span></span>

<span data-ttu-id="561a6-112">Dopo che un'applicazione viene distribuita e cluster hello è in esecuzione un'istanza, è possibile eliminare l'istanza dell'applicazione hello e il relativo tipo di applicazione.</span><span class="sxs-lookup"><span data-stu-id="561a6-112">After an application is deployed and an instance is running in hello cluster, you can delete hello application instance and its application type.</span></span> <span data-ttu-id="561a6-113">Rimuovi toocompletely un'applicazione dal cluster hello prevede hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="561a6-113">toocompletely remove an application from hello cluster involves hello following steps:</span></span>

1. <span data-ttu-id="561a6-114">Rimuovere hello esegue l'istanza dell'applicazione (o eliminare)</span><span class="sxs-lookup"><span data-stu-id="561a6-114">Remove (or delete) hello running application instance</span></span>
2. <span data-ttu-id="561a6-115">Annullare la registrazione del tipo di applicazione hello se non è più necessario</span><span class="sxs-lookup"><span data-stu-id="561a6-115">Unregister hello application type if you no longer need it</span></span>
3. <span data-ttu-id="561a6-116">Rimuovere il pacchetto di applicazione hello dall'archivio immagini hello</span><span class="sxs-lookup"><span data-stu-id="561a6-116">Remove hello application package from hello image store</span></span>

<span data-ttu-id="561a6-117">Se si utilizza [Visual Studio per la distribuzione e debug di applicazioni](service-fabric-publish-app-remote-cluster.md) nel cluster di sviluppo locale, tutti i passaggi precedenti di hello vengono gestite automaticamente tramite uno script di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="561a6-117">If you use [Visual Studio for deploying and debugging applications](service-fabric-publish-app-remote-cluster.md) on your local development cluster, all hello preceding steps are handled automatically through a PowerShell script.</span></span>  <span data-ttu-id="561a6-118">Questo script è presente in hello *script* nella cartella del progetto di applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="561a6-118">This script is found in hello *Scripts* folder of hello application project.</span></span> <span data-ttu-id="561a6-119">In questo articolo vengono fornite informazioni su cosa fa lo script in modo che sia possibile eseguire hello stesse operazioni all'esterno di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="561a6-119">This article provides background on what that script is doing so that you can perform hello same operations outside of Visual Studio.</span></span> 
 
## <a name="connect-toohello-cluster"></a><span data-ttu-id="561a6-120">Connettere il cluster toohello</span><span class="sxs-lookup"><span data-stu-id="561a6-120">Connect toohello cluster</span></span>
<span data-ttu-id="561a6-121">Prima di eseguire qualsiasi comando di PowerShell in questo articolo, iniziano sempre con [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) tooconnect toohello cluster di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="561a6-121">Before you run any PowerShell commands in this article, always start by using [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) tooconnect toohello Service Fabric cluster.</span></span> <span data-ttu-id="561a6-122">cluster di sviluppo locale di toohello di tooconnect, eseguire hello seguente:</span><span class="sxs-lookup"><span data-stu-id="561a6-122">tooconnect toohello local development cluster, run hello following:</span></span>

```powershell
PS C:\>Connect-ServiceFabricCluster
```

<span data-ttu-id="561a6-123">Per esempi di connessione remota tooa del cluster o cluster protetti tramite Azure Active Directory, X509 certificati o Active Directory di Windows vedere [Connetti tooa sicura cluster](service-fabric-connect-to-secure-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="561a6-123">For examples of connecting tooa remote cluster or cluster secured using Azure Active Directory, X509 certificates, or Windows Active Directory see [Connect tooa secure cluster](service-fabric-connect-to-secure-cluster.md).</span></span>

## <a name="upload-hello-application-package"></a><span data-ttu-id="561a6-124">Caricare il pacchetto di applicazione hello</span><span class="sxs-lookup"><span data-stu-id="561a6-124">Upload hello application package</span></span>
<span data-ttu-id="561a6-125">Caricamento del pacchetto dell'applicazione hello lo inserisce in un percorso accessibile dai componenti interni di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="561a6-125">Uploading hello application package puts it in a location that's accessible by internal Service Fabric components.</span></span>
<span data-ttu-id="561a6-126">Se si desidera pacchetto dell'applicazione hello di tooverify localmente, utilizzare hello [Test ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="561a6-126">If you want tooverify hello application package locally, use hello [Test-ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="561a6-127">Hello [copia ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) comando caricamenti hello archivio di immagini cluster toohello pacchetto di applicazione.</span><span class="sxs-lookup"><span data-stu-id="561a6-127">hello [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) command uploads hello application package toohello cluster image store.</span></span>
<span data-ttu-id="561a6-128">Hello **Get ImageStoreConnectionStringFromClusterManifest** cmdlet, che fa parte del modulo PowerShell di Service Fabric SDK hello, è immagine hello tooget utilizzati archiviare la stringa di connessione.</span><span class="sxs-lookup"><span data-stu-id="561a6-128">hello **Get-ImageStoreConnectionStringFromClusterManifest** cmdlet, which is part of hello Service Fabric SDK PowerShell module, is used tooget hello image store connection string.</span></span>  <span data-ttu-id="561a6-129">modulo SDK di hello di tooimport, eseguire:</span><span class="sxs-lookup"><span data-stu-id="561a6-129">tooimport hello SDK module, run:</span></span>

```powershell
Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
```

<span data-ttu-id="561a6-130">Si supponga di compilare e assemblare un'applicazione denominata *MyApplication* in Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="561a6-130">Suppose you build and package an application named *MyApplication* in Visual Studio 2015.</span></span> <span data-ttu-id="561a6-131">Per impostazione predefinita, nome del tipo applicazione hello elencati in ApplicationManifest.xml hello è "MyApplicationType".</span><span class="sxs-lookup"><span data-stu-id="561a6-131">By default, hello application type name listed in hello ApplicationManifest.xml is "MyApplicationType".</span></span>  <span data-ttu-id="561a6-132">Hello pacchetto di applicazione, che contiene un manifesto dell'applicazione hello, i manifesti del servizio e i pacchetti di configurazione/codice/dati, si trova *C:\Users\<username\>\Documents\Visual 2015\Projects\ Studio MyApplication\MyApplication\pkg\Debug*.</span><span class="sxs-lookup"><span data-stu-id="561a6-132">hello application package, which contains hello necessary application manifest, service manifests, and code/config/data packages, is located in *C:\Users\<username\>\Documents\Visual Studio 2015\Projects\MyApplication\MyApplication\pkg\Debug*.</span></span> 

<span data-ttu-id="561a6-133">Hello comando riportato di seguito elenca hello contenuto del pacchetto di applicazione hello:</span><span class="sxs-lookup"><span data-stu-id="561a6-133">hello following command lists hello contents of hello application package:</span></span>

```powershell
PS C:\> $path = 'C:\Users\<user\>\Documents\Visual Studio 2015\Projects\MyApplication\MyApplication\pkg\Debug'
PS C:\> tree /f $path
Folder PATH listing for volume OSDisk
Volume serial number is 0459-2393
C:\USERS\USER\DOCUMENTS\VISUAL STUDIO 2015\PROJECTS\MYAPPLICATION\MYAPPLICATION\PKG\DEBUG
│   ApplicationManifest.xml
│
└───Stateless1Pkg
    │   ServiceManifest.xml
    │
    ├───Code
    │       Microsoft.ServiceFabric.Data.dll
    │       Microsoft.ServiceFabric.Data.Interfaces.dll
    │       Microsoft.ServiceFabric.Internal.dll
    │       Microsoft.ServiceFabric.Internal.Strings.dll
    │       Microsoft.ServiceFabric.Services.dll
    │       ServiceFabricServiceModel.dll
    │       Stateless1.exe
    │       Stateless1.exe.config
    │       Stateless1.pdb
    │       System.Fabric.dll
    │       System.Fabric.Strings.dll
    │
    └───Config
            Settings.xml
```

<span data-ttu-id="561a6-134">Se il pacchetto di applicazione hello è di grandi dimensioni e/o dispone di molti file, è possibile [comprimerli](service-fabric-package-apps.md#compress-a-package).</span><span class="sxs-lookup"><span data-stu-id="561a6-134">If hello application package is large and/or has many files, you can [compress it](service-fabric-package-apps.md#compress-a-package).</span></span> <span data-ttu-id="561a6-135">la compressione di Hello riduce hello dimensioni e il numero di hello dei file.</span><span class="sxs-lookup"><span data-stu-id="561a6-135">hello compression reduces hello size and hello number of files.</span></span>
<span data-ttu-id="561a6-136">effetto collaterale Hello è che la registrazione e annullamento della registrazione di hello tipo di applicazione sono più veloci.</span><span class="sxs-lookup"><span data-stu-id="561a6-136">hello side effect is that registering and un-registering hello application type are faster.</span></span> <span data-ttu-id="561a6-137">Tempo di caricamento può risultare più lenta attualmente, specialmente se si include pacchetto hello toocompress della fase di hello.</span><span class="sxs-lookup"><span data-stu-id="561a6-137">Upload time may be slower currently, especially if you include hello time toocompress hello package.</span></span> 

<span data-ttu-id="561a6-138">un pacchetto, utilizzare toocompress hello stesso [copia ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) comando.</span><span class="sxs-lookup"><span data-stu-id="561a6-138">toocompress a package, use hello same [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) command.</span></span> <span data-ttu-id="561a6-139">La compressione può essere eseguita separato dal caricamento con hello `SkipCopy` flag o insieme hello operazione di caricamento.</span><span class="sxs-lookup"><span data-stu-id="561a6-139">Compression can be done separate from upload, by using hello `SkipCopy` flag, or together with hello upload operation.</span></span> <span data-ttu-id="561a6-140">L'applicazione della compressione a un pacchetto compresso è no-op.</span><span class="sxs-lookup"><span data-stu-id="561a6-140">Applying compression on a compressed package is no-op.</span></span>
<span data-ttu-id="561a6-141">un pacchetto compresso, utilizzare toouncompress hello stesso [copia ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) con hello `UncompressPackage` passare.</span><span class="sxs-lookup"><span data-stu-id="561a6-141">toouncompress a compressed package, use hello same [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) command with hello `UncompressPackage` switch.</span></span>

<span data-ttu-id="561a6-142">Hello cmdlet seguente comprime i pacchetti hello senza copiarlo toohello archivio di immagini.</span><span class="sxs-lookup"><span data-stu-id="561a6-142">hello following cmdlet compresses hello package without copying it toohello image store.</span></span> <span data-ttu-id="561a6-143">pacchetto di Hello include ora i file ZIP per hello `Code` e `Config` pacchetti.</span><span class="sxs-lookup"><span data-stu-id="561a6-143">hello package now includes zipped files for hello `Code` and `Config` packages.</span></span> <span data-ttu-id="561a6-144">Hello hello servizio manifesti dell'applicazione e non compressi, perché sono necessari per molte operazioni interne (ad esempio la condivisione, l'applicazione nome e la versione estrazione del tipo per alcune convalide di pacchetto).</span><span class="sxs-lookup"><span data-stu-id="561a6-144">hello application and hello service manifests are not zipped, because they are needed for many internal operations (like package sharing, application type name and version extraction for certain validations).</span></span> <span data-ttu-id="561a6-145">Compressione manifesti hello renderebbe queste operazioni inefficienti.</span><span class="sxs-lookup"><span data-stu-id="561a6-145">Zipping hello manifests would make these operations inefficient.</span></span>

```
PS C:\> Copy-ServiceFabricApplicationPackage -ApplicationPackagePath $path -CompressPackage -SkipCopy
PS C:\> tree /f $path
Folder PATH listing for volume OSDisk
Volume serial number is 0459-2393
C:\USERS\USER\DOCUMENTS\VISUAL STUDIO 2015\PROJECTS\MYAPPLICATION\MYAPPLICATION\PKG\DEBUG
|   ApplicationManifest.xml
|
└───Stateless1Pkg
       Code.zip
       Config.zip
       ServiceManifest.xml
```

<span data-ttu-id="561a6-146">Per i pacchetti di applicazione di grandi dimensioni, la compressione di hello richiede tempo.</span><span class="sxs-lookup"><span data-stu-id="561a6-146">For large application packages, hello compression takes time.</span></span> <span data-ttu-id="561a6-147">Per ottenere risultati ottimali, usare un'unità SSD rapida.</span><span class="sxs-lookup"><span data-stu-id="561a6-147">For best results, use a fast SSD drive.</span></span> <span data-ttu-id="561a6-148">Hello la compressione e la dimensione di hello del pacchetto compresso hello anche variano in base al contenuto del pacchetto hello.</span><span class="sxs-lookup"><span data-stu-id="561a6-148">hello compression times and hello size of hello compressed package also differ based on hello package content.</span></span>
<span data-ttu-id="561a6-149">Ad esempio, ecco le statistiche della compressione per alcuni pacchetti, che mostrano iniziale hello e hello dimensione compressa del pacchetto, con il tempo di compressione hello.</span><span class="sxs-lookup"><span data-stu-id="561a6-149">For example, here is compression statistics for some packages, which show hello initial and hello compressed package size, with hello compression time.</span></span>

|<span data-ttu-id="561a6-150">Dimensioni iniziali (MB)</span><span class="sxs-lookup"><span data-stu-id="561a6-150">Initial size (MB)</span></span>|<span data-ttu-id="561a6-151">Numero di file</span><span class="sxs-lookup"><span data-stu-id="561a6-151">File count</span></span>|<span data-ttu-id="561a6-152">Tempo di compressione</span><span class="sxs-lookup"><span data-stu-id="561a6-152">Compression Time</span></span>|<span data-ttu-id="561a6-153">Dimensioni pacchetto compresso (MB)</span><span class="sxs-lookup"><span data-stu-id="561a6-153">Compressed package size (MB)</span></span>|
|----------------:|---------:|---------------:|---------------------------:|
|<span data-ttu-id="561a6-154">100</span><span class="sxs-lookup"><span data-stu-id="561a6-154">100</span></span>|<span data-ttu-id="561a6-155">100</span><span class="sxs-lookup"><span data-stu-id="561a6-155">100</span></span>|<span data-ttu-id="561a6-156">00:00:03.3547592</span><span class="sxs-lookup"><span data-stu-id="561a6-156">00:00:03.3547592</span></span>|<span data-ttu-id="561a6-157">60</span><span class="sxs-lookup"><span data-stu-id="561a6-157">60</span></span>|
|<span data-ttu-id="561a6-158">512</span><span class="sxs-lookup"><span data-stu-id="561a6-158">512</span></span>|<span data-ttu-id="561a6-159">100</span><span class="sxs-lookup"><span data-stu-id="561a6-159">100</span></span>|<span data-ttu-id="561a6-160">00:00:16.3850303</span><span class="sxs-lookup"><span data-stu-id="561a6-160">00:00:16.3850303</span></span>|<span data-ttu-id="561a6-161">307</span><span class="sxs-lookup"><span data-stu-id="561a6-161">307</span></span>|
|<span data-ttu-id="561a6-162">1024</span><span class="sxs-lookup"><span data-stu-id="561a6-162">1024</span></span>|<span data-ttu-id="561a6-163">500</span><span class="sxs-lookup"><span data-stu-id="561a6-163">500</span></span>|<span data-ttu-id="561a6-164">00:00:32.5907950</span><span class="sxs-lookup"><span data-stu-id="561a6-164">00:00:32.5907950</span></span>|<span data-ttu-id="561a6-165">615</span><span class="sxs-lookup"><span data-stu-id="561a6-165">615</span></span>|
|<span data-ttu-id="561a6-166">2048</span><span class="sxs-lookup"><span data-stu-id="561a6-166">2048</span></span>|<span data-ttu-id="561a6-167">1000</span><span class="sxs-lookup"><span data-stu-id="561a6-167">1000</span></span>|<span data-ttu-id="561a6-168">00:01:04.3775554</span><span class="sxs-lookup"><span data-stu-id="561a6-168">00:01:04.3775554</span></span>|<span data-ttu-id="561a6-169">1231</span><span class="sxs-lookup"><span data-stu-id="561a6-169">1231</span></span>|
|<span data-ttu-id="561a6-170">5012</span><span class="sxs-lookup"><span data-stu-id="561a6-170">5012</span></span>|<span data-ttu-id="561a6-171">100</span><span class="sxs-lookup"><span data-stu-id="561a6-171">100</span></span>|<span data-ttu-id="561a6-172">00:02:45.2951288</span><span class="sxs-lookup"><span data-stu-id="561a6-172">00:02:45.2951288</span></span>|<span data-ttu-id="561a6-173">3074</span><span class="sxs-lookup"><span data-stu-id="561a6-173">3074</span></span>|

<span data-ttu-id="561a6-174">Una volta che un pacchetto compresso, può essere caricato tooone o più Service Fabric cluster come necessario.</span><span class="sxs-lookup"><span data-stu-id="561a6-174">Once a package is compressed, it can be uploaded tooone or multiple Service Fabric clusters as needed.</span></span> <span data-ttu-id="561a6-175">il meccanismo di distribuzione Hello è lo stesso per i pacchetti compressi e non compressi.</span><span class="sxs-lookup"><span data-stu-id="561a6-175">hello deployment mechanism is same for compressed and uncompressed packages.</span></span> <span data-ttu-id="561a6-176">Se il pacchetto di hello è compresso, viene archiviata come tale nell'archivio di immagini cluster hello ed è non compressi in nodo hello prima di eseguita un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="561a6-176">If hello package is compressed, it is stored as such in hello cluster image store and it's uncompressed on hello node before hello application is run.</span></span>


<span data-ttu-id="561a6-177">Hello esempio Carica archivio immagine toohello pacchetti hello in una cartella denominata "MyApplicationV1":</span><span class="sxs-lookup"><span data-stu-id="561a6-177">hello following example uploads hello package toohello image store, into a folder named "MyApplicationV1":</span></span>

```powershell
PS C:\> Copy-ServiceFabricApplicationPackage -ApplicationPackagePath $path -ApplicationPackagePathInImageStore MyApplicationV1 -ImageStoreConnectionString (Get-ImageStoreConnectionStringFromClusterManifest(Get-ServiceFabricClusterManifest)) -TimeoutSec 1800
```

<span data-ttu-id="561a6-178">Hello **Get ImageStoreConnectionStringFromClusterManifest** cmdlet, che fa parte del modulo PowerShell di Service Fabric SDK hello, è immagine hello tooget utilizzati archiviare la stringa di connessione.</span><span class="sxs-lookup"><span data-stu-id="561a6-178">hello **Get-ImageStoreConnectionStringFromClusterManifest** cmdlet, which is part of hello Service Fabric SDK PowerShell module, is used tooget hello image store connection string.</span></span>  <span data-ttu-id="561a6-179">modulo SDK di hello di tooimport, eseguire:</span><span class="sxs-lookup"><span data-stu-id="561a6-179">tooimport hello SDK module, run:</span></span>

```powershell
Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
```

<span data-ttu-id="561a6-180">Se non si specifica hello *- ApplicationPackagePathInImageStore* parametro, il pacchetto di applicazione hello viene copiato nella cartella "Debug" hello in archivio immagini hello.</span><span class="sxs-lookup"><span data-stu-id="561a6-180">If you do not specify hello *-ApplicationPackagePathInImageStore* parameter, hello application package is copied into hello "Debug" folder in hello image store.</span></span>

<span data-ttu-id="561a6-181">Hello tempo tooupload un pacchetto diverso in base a più fattori.</span><span class="sxs-lookup"><span data-stu-id="561a6-181">hello time it takes tooupload a package differs depending on multiple factors.</span></span> <span data-ttu-id="561a6-182">Alcuni di questi fattori sono il numero di hello di file nel pacchetto di hello, dimensione del pacchetto hello e delle dimensioni del file hello.</span><span class="sxs-lookup"><span data-stu-id="561a6-182">Some of these factors are hello number of files in hello package, hello package size, and hello file sizes.</span></span> <span data-ttu-id="561a6-183">velocità della rete tra il computer di origine hello e cluster di Service Fabric hello Hello influisce anche sull'ora di caricamento hello.</span><span class="sxs-lookup"><span data-stu-id="561a6-183">hello network speed between hello source machine and hello Service Fabric cluster also impacts hello upload time.</span></span> <span data-ttu-id="561a6-184">Hello timeout predefinito per [copia ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) è 30 minuti.</span><span class="sxs-lookup"><span data-stu-id="561a6-184">hello default timeout for [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) is 30 minutes.</span></span>
<span data-ttu-id="561a6-185">A seconda del hello fattori descritti, è possibile tooincrease hello timeout.</span><span class="sxs-lookup"><span data-stu-id="561a6-185">Depending on hello described factors, you may have tooincrease hello timeout.</span></span> <span data-ttu-id="561a6-186">Se la compressione di pacchetti hello in hello copia chiamata, è necessario tooalso prendere in considerazione il tempo di compressione hello.</span><span class="sxs-lookup"><span data-stu-id="561a6-186">If you are compressing hello package in hello copy call, you need tooalso consider hello compression time.</span></span>

<span data-ttu-id="561a6-187">Vedere [comprendere una stringa di connessione di archivio immagine hello](service-fabric-image-store-connection-string.md) informazioni supplementari sull'archivio di immagini hello e immagine archiviare una stringa di connessione.</span><span class="sxs-lookup"><span data-stu-id="561a6-187">See [Understand hello image store connection string](service-fabric-image-store-connection-string.md) for supplementary information about hello image store and image store connection string.</span></span>

## <a name="register-hello-application-package"></a><span data-ttu-id="561a6-188">Registrare il pacchetto di applicazione hello</span><span class="sxs-lookup"><span data-stu-id="561a6-188">Register hello application package</span></span>
<span data-ttu-id="561a6-189">tipo di applicazione Hello e versione dichiarati nel manifesto dell'applicazione hello diventano disponibile per l'utilizzo quando il pacchetto di applicazione hello viene registrato.</span><span class="sxs-lookup"><span data-stu-id="561a6-189">hello application type and version declared in hello application manifest become available for use when hello application package is registered.</span></span> <span data-ttu-id="561a6-190">sistema Hello legge pacchetto hello caricato nel passaggio precedente hello, verifica i pacchetti hello, elabora i contenuti del pacchetto hello e Copia percorso di sistema interno tooan pacchetto hello elaborato.</span><span class="sxs-lookup"><span data-stu-id="561a6-190">hello system reads hello package uploaded in hello previous step, verifies hello package, processes hello package contents, and copies hello processed package tooan internal system location.</span></span>  

<span data-ttu-id="561a6-191">Eseguire hello [registro ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) tooregister cmdlet hello tipo di applicazione in cluster hello e renderlo disponibile per la distribuzione:</span><span class="sxs-lookup"><span data-stu-id="561a6-191">Run hello [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) cmdlet tooregister hello application type in hello cluster and make it available for deployment:</span></span>

```powershell
PS C:\> Register-ServiceFabricApplicationType MyApplicationV1
Register application type succeeded
```

<span data-ttu-id="561a6-192">"MyApplicationV1" è la cartella hello in archivio immagini hello in cui si trova il pacchetto di applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="561a6-192">"MyApplicationV1" is hello folder in hello image store where hello application package is located.</span></span> <span data-ttu-id="561a6-193">tipo di applicazione Hello con nome "MyApplicationType" e la versione "1.0.0" (entrambi trovati nel manifesto dell'applicazione hello) è stato registrato nel cluster hello.</span><span class="sxs-lookup"><span data-stu-id="561a6-193">hello application type with name "MyApplicationType" and version "1.0.0" (both are found in hello application manifest) is now registered in hello cluster.</span></span>

<span data-ttu-id="561a6-194">Hello [registro ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) comando restituisce solo dopo che il sistema di hello dispone di pacchetto dell'applicazione hello registrato correttamente.</span><span class="sxs-lookup"><span data-stu-id="561a6-194">hello [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) command returns only after hello system has successfully registered hello application package.</span></span> <span data-ttu-id="561a6-195">Registrazione accetta quanto tempo dipende dalla dimensione hello e il contenuto del pacchetto di applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="561a6-195">How long registration takes depends on hello size and contents of hello application package.</span></span> <span data-ttu-id="561a6-196">Se necessario, hello **- TimeoutSec** parametro può essere utilizzato toosupply un timeout più lungo (timeout di hello predefinito è 60 secondi).</span><span class="sxs-lookup"><span data-stu-id="561a6-196">If needed, hello **-TimeoutSec** parameter can be used toosupply a longer timeout (hello default timeout is 60 seconds).</span></span>

<span data-ttu-id="561a6-197">Se si dispone di un'applicazione di grandi dimensioni del pacchetto o se si verificano i timeout, utilizzare hello **- Async** parametro.</span><span class="sxs-lookup"><span data-stu-id="561a6-197">If you have a large application package or if you are experiencing timeouts, use hello **-Async** parameter.</span></span> <span data-ttu-id="561a6-198">comando Hello restituisce quando cluster hello accetta comando register hello e l'elaborazione di hello continua in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="561a6-198">hello command returns when hello cluster accepts hello register command, and hello processing continues as needed.</span></span>
<span data-ttu-id="561a6-199">Hello [Get ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) comando Elenca tutte le versioni di tipo applicazione registrata correttamente e il relativo stato di registrazione.</span><span class="sxs-lookup"><span data-stu-id="561a6-199">hello [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) command lists all successfully registered application type versions and their registration status.</span></span> <span data-ttu-id="561a6-200">È possibile utilizzare questo comando toodetermine quando viene eseguita la registrazione di hello.</span><span class="sxs-lookup"><span data-stu-id="561a6-200">You can use this command toodetermine when hello registration is done.</span></span>

```powershell
PS C:\> Get-ServiceFabricApplicationType

ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
Status                 : Available
DefaultParameters      : { "Stateless1_InstanceCount" = "-1" }
```

## <a name="create-hello-application"></a><span data-ttu-id="561a6-201">Creare un'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="561a6-201">Create hello application</span></span>
<span data-ttu-id="561a6-202">È possibile creare un'istanza di un'applicazione da qualsiasi versione di tipo di applicazione che è stato registrato correttamente tramite hello [New ServiceFabricApplication](/powershell/module/servicefabric/new-servicefabricapplication?view=azureservicefabricps) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="561a6-202">You can instantiate an application from any application type version that has been registered successfully by using hello [New-ServiceFabricApplication](/powershell/module/servicefabric/new-servicefabricapplication?view=azureservicefabricps) cmdlet.</span></span> <span data-ttu-id="561a6-203">nome Hello di ogni applicazione deve iniziare con hello *"fabric:"* dello schema e deve essere univoco per ogni istanza dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="561a6-203">hello name of each application must start with hello *"fabric:"* scheme and must be unique for each application instance.</span></span> <span data-ttu-id="561a6-204">Vengono creati anche i servizi predefiniti definiti nel manifesto dell'applicazione hello del tipo di applicazione di destinazione hello.</span><span class="sxs-lookup"><span data-stu-id="561a6-204">Any default services defined in hello application manifest of hello target application type are also created.</span></span>

```powershell
PS C:\> New-ServiceFabricApplication fabric:/MyApp MyApplicationType 1.0.0

ApplicationName        : fabric:/MyApp
ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
ApplicationParameters  : {}
```
<span data-ttu-id="561a6-205">Per qualsiasi versione di un tipo di applicazione registrato, è possibile creare più istanze dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="561a6-205">Multiple application instances can be created for any given version of a registered application type.</span></span> <span data-ttu-id="561a6-206">Ogni istanza viene eseguita in isolamento, con un proprio processo e una propria directory di lavoro.</span><span class="sxs-lookup"><span data-stu-id="561a6-206">Each application instance runs in isolation, with its own work directory and process.</span></span>

<span data-ttu-id="561a6-207">toosee denominato App e servizi sono in esecuzione in cluster hello, eseguire hello [Get ServiceFabricApplication](/powershell/servicefabric/vlatest/get-servicefabricapplication) e [Get ServiceFabricService](/powershell/module/servicefabric/get-servicefabricservice?view=azureservicefabricps) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="561a6-207">toosee which named apps and services are running in hello cluster, run hello [Get-ServiceFabricApplication](/powershell/servicefabric/vlatest/get-servicefabricapplication) and [Get-ServiceFabricService](/powershell/module/servicefabric/get-servicefabricservice?view=azureservicefabricps) cmdlets:</span></span>

```powershell
PS C:\> Get-ServiceFabricApplication  

ApplicationName        : fabric:/MyApp
ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
ApplicationStatus      : Ready
HealthState            : Ok
ApplicationParameters  : {}

PS C:\> Get-ServiceFabricApplication | Get-ServiceFabricService

ServiceName            : fabric:/MyApp/Stateless1
ServiceKind            : Stateless
ServiceTypeName        : Stateless1Type
IsServiceGroup         : False
ServiceManifestVersion : 1.0.0
ServiceStatus          : Active
HealthState            : Ok
```

## <a name="remove-an-application"></a><span data-ttu-id="561a6-208">Rimuovere un'applicazione</span><span class="sxs-lookup"><span data-stu-id="561a6-208">Remove an application</span></span>
<span data-ttu-id="561a6-209">Quando un'istanza di applicazione non è più necessario, è possibile rimuoverlo in modo permanente in base al nome utilizzando hello [Remove ServiceFabricApplication](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="561a6-209">When an application instance is no longer needed, you can permanently remove it by name using hello [Remove-ServiceFabricApplication](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps) cmdlet.</span></span> <span data-ttu-id="561a6-210">[Remove-ServiceFabricApplication](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps) rimuove automaticamente tutti i servizi che appartengono toohello applicazione nonché, in modo permanente la rimozione di tutti gli stati di servizio.</span><span class="sxs-lookup"><span data-stu-id="561a6-210">[Remove-ServiceFabricApplication](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps) automatically removes all services that belong toohello application as well, permanently removing all service state.</span></span> 

> [!WARNING]
> <span data-ttu-id="561a6-211">Tale operazione non può essere annullata e lo stato dell'applicazione non può essere recuperato.</span><span class="sxs-lookup"><span data-stu-id="561a6-211">This operation cannot be reversed, and application state cannot be recovered.</span></span>

```powershell
PS C:\> Remove-ServiceFabricApplication fabric:/MyApp

Confirm
Continue with this operation?
[Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"):
Remove application instance succeeded

PS C:\> Get-ServiceFabricApplication
```

## <a name="unregister-an-application-type"></a><span data-ttu-id="561a6-212">Annullare la registrazione di un tipo di applicazione</span><span class="sxs-lookup"><span data-stu-id="561a6-212">Unregister an application type</span></span>
<span data-ttu-id="561a6-213">Quando una particolare versione di un tipo di applicazione non è più necessario, si deve annullare la registrazione di tipo di applicazione hello utilizzando hello [Unregister-ServiceFabricApplicationType](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="561a6-213">When a particular version of an application type is no longer needed, you should unregister hello application type using hello [Unregister-ServiceFabricApplicationType](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) cmdlet.</span></span> <span data-ttu-id="561a6-214">Annullamento della registrazione dell'applicazione non utilizzati tipi versioni spazio di archiviazione utilizzato dall'archivio immagini hello.</span><span class="sxs-lookup"><span data-stu-id="561a6-214">Unregistering unused application types releases storage space used by hello image store.</span></span> <span data-ttu-id="561a6-215">È possibile annullare la registrazione di un tipo di applicazione solo se non sono state create istanze di applicazioni basate su di esso o non vi sono aggiornamenti di applicazioni in sospeso che vi fanno riferimento.</span><span class="sxs-lookup"><span data-stu-id="561a6-215">An application type can be unregistered as long as no applications are instantiated against it and no pending application upgrades are referencing it.</span></span>

<span data-ttu-id="561a6-216">Eseguire [Get ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) i tipi di applicazione hello toosee attualmente registrato nel cluster di hello:</span><span class="sxs-lookup"><span data-stu-id="561a6-216">Run [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) toosee hello application types currently registered in hello cluster:</span></span>

```powershell
PS C:\> Get-ServiceFabricApplicationType

ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
Status                 : Available
DefaultParameters      : { "Stateless1_InstanceCount" = "-1" }
```

<span data-ttu-id="561a6-217">Eseguire [Unregister-ServiceFabricApplicationType](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) toounregister un tipo specifico di applicazione:</span><span class="sxs-lookup"><span data-stu-id="561a6-217">Run [Unregister-ServiceFabricApplicationType](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) toounregister a specific application type:</span></span>

```powershell
PS C:\> Unregister-ServiceFabricApplicationType MyApplicationType 1.0.0
```

## <a name="remove-an-application-package-from-hello-image-store"></a><span data-ttu-id="561a6-218">Rimuovere un pacchetto di applicazioni dall'archivio immagini hello</span><span class="sxs-lookup"><span data-stu-id="561a6-218">Remove an application package from hello image store</span></span>
<span data-ttu-id="561a6-219">Quando un pacchetto di applicazione non è più necessario, è possibile eliminarlo dal hello immagine archivio toofree le risorse di sistema.</span><span class="sxs-lookup"><span data-stu-id="561a6-219">When an application package is no longer needed, you can delete it from hello image store toofree up system resources.</span></span>

```powershell
PS C:\>Remove-ServiceFabricApplicationPackage -ApplicationPackagePathInImageStore MyApplicationV1 -ImageStoreConnectionString (Get-ImageStoreConnectionStringFromClusterManifest(Get-ServiceFabricClusterManifest))
```

## <a name="troubleshooting"></a><span data-ttu-id="561a6-220">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="561a6-220">Troubleshooting</span></span>
### <a name="copy-servicefabricapplicationpackage-asks-for-an-imagestoreconnectionstring"></a><span data-ttu-id="561a6-221">Copy-ServiceFabricApplicationPackage chiede un parametro ImageStoreConnectionString</span><span class="sxs-lookup"><span data-stu-id="561a6-221">Copy-ServiceFabricApplicationPackage asks for an ImageStoreConnectionString</span></span>
<span data-ttu-id="561a6-222">ambiente di Service Fabric SDK Hello dovrebbe già disporre hello corretto impostare valori predefiniti.</span><span class="sxs-lookup"><span data-stu-id="561a6-222">hello Service Fabric SDK environment should already have hello correct defaults set up.</span></span> <span data-ttu-id="561a6-223">Ma se necessario, hello ImageStoreConnectionString per tutti i comandi debba corrispondere valore hello tale hello dell'infrastruttura del servizio cluster utilizza.</span><span class="sxs-lookup"><span data-stu-id="561a6-223">But if needed, hello ImageStoreConnectionString for all commands should match hello value that hello Service Fabric cluster is using.</span></span> <span data-ttu-id="561a6-224">È possibile trovare hello ImageStoreConnectionString nel manifesto del cluster hello, recuperati tramite hello [Get ServiceFabricClusterManifest](/powershell/module/servicefabric/get-servicefabricclustermanifest?view=azureservicefabricps) e i comandi Get-ImageStoreConnectionStringFromClusterManifest:</span><span class="sxs-lookup"><span data-stu-id="561a6-224">You can find hello ImageStoreConnectionString in hello cluster manifest, retrieved using hello [Get-ServiceFabricClusterManifest](/powershell/module/servicefabric/get-servicefabricclustermanifest?view=azureservicefabricps) and Get-ImageStoreConnectionStringFromClusterManifest commands:</span></span>

```powershell
PS C:\> Get-ImageStoreConnectionStringFromClusterManifest(Get-ServiceFabricClusterManifest)
```

<span data-ttu-id="561a6-225">Hello **Get ImageStoreConnectionStringFromClusterManifest** cmdlet, che fa parte del modulo PowerShell di Service Fabric SDK hello, è immagine hello tooget utilizzati archiviare la stringa di connessione.</span><span class="sxs-lookup"><span data-stu-id="561a6-225">hello **Get-ImageStoreConnectionStringFromClusterManifest** cmdlet, which is part of hello Service Fabric SDK PowerShell module, is used tooget hello image store connection string.</span></span>  <span data-ttu-id="561a6-226">modulo SDK di hello di tooimport, eseguire:</span><span class="sxs-lookup"><span data-stu-id="561a6-226">tooimport hello SDK module, run:</span></span>

```powershell
Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
```

<span data-ttu-id="561a6-227">Hello ImageStoreConnectionString viene trovato nel manifesto del cluster hello:</span><span class="sxs-lookup"><span data-stu-id="561a6-227">hello ImageStoreConnectionString is found in hello cluster manifest:</span></span>

```xml
<ClusterManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Name="Server-Default-SingleNode" Version="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">

    [...]

    <Section Name="Management">
      <Parameter Name="ImageStoreConnectionString" Value="file:D:\ServiceFabric\Data\ImageStore" />
    </Section>

    [...]
```

<span data-ttu-id="561a6-228">Vedere [comprendere una stringa di connessione di archivio immagine hello](service-fabric-image-store-connection-string.md) informazioni supplementari sull'archivio di immagini hello e immagine archiviare una stringa di connessione.</span><span class="sxs-lookup"><span data-stu-id="561a6-228">See [Understand hello image store connection string](service-fabric-image-store-connection-string.md) for supplementary information about hello image store and image store connection string.</span></span>

### <a name="deploy-large-application-package"></a><span data-ttu-id="561a6-229">Distribuire un pacchetto dell'applicazione di grandi dimensioni</span><span class="sxs-lookup"><span data-stu-id="561a6-229">Deploy large application package</span></span>
<span data-ttu-id="561a6-230">Problema: [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) raggiunge il timeout per un pacchetto dell'applicazione di grandi dimensioni (nell'ordine di GB).</span><span class="sxs-lookup"><span data-stu-id="561a6-230">Issue: [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) times out for a large application package (order of GB).</span></span>
<span data-ttu-id="561a6-231">Soluzione:</span><span class="sxs-lookup"><span data-stu-id="561a6-231">Try:</span></span>
- <span data-ttu-id="561a6-232">Specificare un timeout maggiore per il comando [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps), con il parametro `TimeoutSec`.</span><span class="sxs-lookup"><span data-stu-id="561a6-232">Specify a larger timeout for [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) command, with `TimeoutSec` parameter.</span></span> <span data-ttu-id="561a6-233">Per impostazione predefinita, il timeout di hello è 30 minuti.</span><span class="sxs-lookup"><span data-stu-id="561a6-233">By default, hello timeout is 30 minutes.</span></span>
- <span data-ttu-id="561a6-234">Controllare la connessione di rete hello tra il computer di origine e il cluster.</span><span class="sxs-lookup"><span data-stu-id="561a6-234">Check hello network connection between your source machine and cluster.</span></span> <span data-ttu-id="561a6-235">Se hello connessione è lenta, considerare l'utilizzo di un computer con una connessione di rete migliorata.</span><span class="sxs-lookup"><span data-stu-id="561a6-235">If hello connection is slow, consider using a machine with a better network connection.</span></span>
<span data-ttu-id="561a6-236">Se hello client macchina si trova in un'altra area di cluster hello, considerare l'uso di un computer client in un'area più vicino o stesso come cluster hello.</span><span class="sxs-lookup"><span data-stu-id="561a6-236">If hello client machine is in another region than hello cluster, consider using a client machine in a closer or same region as hello cluster.</span></span>
- <span data-ttu-id="561a6-237">Controllare se si stiano raggiungendo le limitazioni esterne.</span><span class="sxs-lookup"><span data-stu-id="561a6-237">Check if you are hitting external throttling.</span></span> <span data-ttu-id="561a6-238">Ad esempio, quando l'archivio immagini hello è configurato toouse azure storage, caricamento può essere limitato.</span><span class="sxs-lookup"><span data-stu-id="561a6-238">For example, when hello image store is configured toouse azure storage, upload may be throttled.</span></span>

<span data-ttu-id="561a6-239">Problema: Il pacchetto è stato caricato completamente ma si è verificato un timeout di [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps). Soluzione:</span><span class="sxs-lookup"><span data-stu-id="561a6-239">Issue: Upload package completed successfully, but [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) times out. Try:</span></span>
- <span data-ttu-id="561a6-240">[Comprimere il pacchetto di hello](service-fabric-package-apps.md#compress-a-package) prima della copia toohello archivio di immagini.</span><span class="sxs-lookup"><span data-stu-id="561a6-240">[Compress hello package](service-fabric-package-apps.md#compress-a-package) before copying toohello image store.</span></span>
<span data-ttu-id="561a6-241">la compressione di Hello riduce le dimensioni di hello e hello diversi file, che a sua volta riduce hello quantità di traffico e di lavoro di Service Fabric devono eseguire.</span><span class="sxs-lookup"><span data-stu-id="561a6-241">hello compression reduces hello size and hello number of files, which in turn reduces hello amount of traffic and work that Service Fabric must perform.</span></span> <span data-ttu-id="561a6-242">operazione di caricamento Hello potrebbe risultare più lenta (in particolare se si include il tempo di compressione hello), ma il tipo di applicazione hello registrare e annullare la registrazione sono più veloci.</span><span class="sxs-lookup"><span data-stu-id="561a6-242">hello upload operation may be slower (especially if you include hello compression time), but register and un-register hello application type are faster.</span></span>
- <span data-ttu-id="561a6-243">Specificare un timeout maggiore per il comando [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps), con il parametro `TimeoutSec`.</span><span class="sxs-lookup"><span data-stu-id="561a6-243">Specify a larger timeout for [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) with `TimeoutSec` parameter.</span></span>
- <span data-ttu-id="561a6-244">Specificare lo switch `Async` per [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="561a6-244">Specify `Async` switch for [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps).</span></span> <span data-ttu-id="561a6-245">comando Hello restituisce quando cluster hello accetta comandi hello e registrazione di hello del tipo di applicazione hello continua in modo asincrono.</span><span class="sxs-lookup"><span data-stu-id="561a6-245">hello command returns when hello cluster accepts hello command and hello registration of hello application type continues asynchronously.</span></span> <span data-ttu-id="561a6-246">Per questo motivo, non è toospecify è necessario un timeout superiore in questo caso.</span><span class="sxs-lookup"><span data-stu-id="561a6-246">For this reason, there is no need toospecify a higher timeout in this case.</span></span> <span data-ttu-id="561a6-247">Hello [Get ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) comando Elenca tutte le versioni di tipo applicazione registrata correttamente e il relativo stato di registrazione.</span><span class="sxs-lookup"><span data-stu-id="561a6-247">hello [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) command lists all successfully registered application type versions and their registration status.</span></span> <span data-ttu-id="561a6-248">È possibile utilizzare questo comando toodetermine quando viene eseguita la registrazione di hello.</span><span class="sxs-lookup"><span data-stu-id="561a6-248">You can use this command toodetermine when hello registration is done.</span></span>

```powershell
PS C:\> Get-ServiceFabricApplicationType

ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
Status                 : Available
DefaultParameters      : { "Stateless1_InstanceCount" = "-1" }
```

### <a name="deploy-application-package-with-many-files"></a><span data-ttu-id="561a6-249">Distribuire un pacchetto di applicazione con numerosi file</span><span class="sxs-lookup"><span data-stu-id="561a6-249">Deploy application package with many files</span></span>
<span data-ttu-id="561a6-250">Problema: Si verifica un timeout di [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) per un pacchetto di applicazione con molti file (nell'ordine di migliaia).</span><span class="sxs-lookup"><span data-stu-id="561a6-250">Issue: [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) times out for an application package with many files (order of thousands).</span></span>
<span data-ttu-id="561a6-251">Soluzione:</span><span class="sxs-lookup"><span data-stu-id="561a6-251">Try:</span></span>
- <span data-ttu-id="561a6-252">[Comprimere il pacchetto di hello](service-fabric-package-apps.md#compress-a-package) prima della copia toohello archivio di immagini.</span><span class="sxs-lookup"><span data-stu-id="561a6-252">[Compress hello package](service-fabric-package-apps.md#compress-a-package) before copying toohello image store.</span></span> <span data-ttu-id="561a6-253">la compressione di Hello riduce il numero di hello di file.</span><span class="sxs-lookup"><span data-stu-id="561a6-253">hello compression reduces hello number of files.</span></span>
- <span data-ttu-id="561a6-254">Specificare un timeout maggiore per il comando [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps), con il parametro `TimeoutSec`.</span><span class="sxs-lookup"><span data-stu-id="561a6-254">Specify a larger timeout for [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) with `TimeoutSec` parameter.</span></span>
- <span data-ttu-id="561a6-255">Specificare lo switch `Async` per [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="561a6-255">Specify `Async` switch for [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps).</span></span> <span data-ttu-id="561a6-256">comando Hello restituisce quando cluster hello accetta comandi hello e registrazione di hello del tipo di applicazione hello continua in modo asincrono.</span><span class="sxs-lookup"><span data-stu-id="561a6-256">hello command returns when hello cluster accepts hello command and hello registration of hello application type continues asynchronously.</span></span>
<span data-ttu-id="561a6-257">Per questo motivo, non è toospecify è necessario un timeout superiore in questo caso.</span><span class="sxs-lookup"><span data-stu-id="561a6-257">For this reason, there is no need toospecify a higher timeout in this case.</span></span> <span data-ttu-id="561a6-258">Hello [Get ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) comando Elenca tutte le versioni di tipo applicazione registrata correttamente e il relativo stato di registrazione.</span><span class="sxs-lookup"><span data-stu-id="561a6-258">hello [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) command lists all successfully registered application type versions and their registration status.</span></span> <span data-ttu-id="561a6-259">È possibile utilizzare questo comando toodetermine quando viene eseguita la registrazione di hello.</span><span class="sxs-lookup"><span data-stu-id="561a6-259">You can use this command toodetermine when hello registration is done.</span></span>

```powershell
PS C:\> Get-ServiceFabricApplicationType

ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
Status                 : Available
DefaultParameters      : { "Stateless1_InstanceCount" = "-1" }
```

## <a name="next-steps"></a><span data-ttu-id="561a6-260">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="561a6-260">Next steps</span></span>
[<span data-ttu-id="561a6-261">Aggiornamento di un'applicazione di infrastruttura di servizi</span><span class="sxs-lookup"><span data-stu-id="561a6-261">Service Fabric application upgrade</span></span>](service-fabric-application-upgrade.md)

[<span data-ttu-id="561a6-262">Introduzione all'integrità di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="561a6-262">Service Fabric health introduction</span></span>](service-fabric-health-introduction.md)

[<span data-ttu-id="561a6-263">Eseguire la diagnosi e la risoluzione dei problemi di un servizio di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="561a6-263">Diagnose and troubleshoot a Service Fabric service</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[<span data-ttu-id="561a6-264">Modellare un'applicazione in Service Fabric</span><span class="sxs-lookup"><span data-stu-id="561a6-264">Model an application in Service Fabric</span></span>](service-fabric-application-model.md)

<!--Link references--In actual articles, you only need a single period before hello slash-->
[10]: service-fabric-application-model.md
[11]: service-fabric-application-upgrade.md
