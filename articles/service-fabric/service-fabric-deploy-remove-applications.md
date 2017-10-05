---
title: Distribuzione dell'applicazione Azure Service Fabric | Microsoft Docs
description: Come distribuire e rimuovere applicazioni in Service Fabric con PowerShell.
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
ms.openlocfilehash: edef23a8cdab7fd0bef54456f0caabb9db273bf9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-and-remove-applications-using-powershell"></a><span data-ttu-id="f16b0-103">Distribuire e rimuovere applicazioni con PowerShell</span><span class="sxs-lookup"><span data-stu-id="f16b0-103">Deploy and remove applications using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f16b0-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f16b0-104">PowerShell</span></span>](service-fabric-deploy-remove-applications.md)
> * [<span data-ttu-id="f16b0-105">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f16b0-105">Visual Studio</span></span>](service-fabric-publish-app-remote-cluster.md)
> * [<span data-ttu-id="f16b0-106">API client Fabric</span><span class="sxs-lookup"><span data-stu-id="f16b0-106">FabricClient APIs</span></span>](service-fabric-deploy-remove-applications-fabricclient.md)
> 
> 

<br/>

<span data-ttu-id="f16b0-107">Dopo aver creato il [pacchetto di un tipo di applicazione][10], è possibile distribuirlo in un cluster di Azure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="f16b0-107">Once an [application type has been packaged][10], it's ready for deployment into an Azure Service Fabric cluster.</span></span> <span data-ttu-id="f16b0-108">La distribuzione prevede i tre passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="f16b0-108">Deployment involves the following three steps:</span></span>

1. <span data-ttu-id="f16b0-109">Caricamento del pacchetto dell'applicazione nell'archivio di immagini</span><span class="sxs-lookup"><span data-stu-id="f16b0-109">Upload the application package to the image store</span></span>
2. <span data-ttu-id="f16b0-110">Registrare il tipo di applicazione</span><span class="sxs-lookup"><span data-stu-id="f16b0-110">Register the application type</span></span>
3. <span data-ttu-id="f16b0-111">Creare l'istanza dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="f16b0-111">Create the application instance</span></span>

<span data-ttu-id="f16b0-112">Dopo che un'applicazione è stata distribuita e un'istanza è in esecuzione nel cluster, è possibile eliminare l'istanza dell'applicazione e il tipo di applicazione corrispondente.</span><span class="sxs-lookup"><span data-stu-id="f16b0-112">After an application is deployed and an instance is running in the cluster, you can delete the application instance and its application type.</span></span> <span data-ttu-id="f16b0-113">Per rimuovere completamente un'applicazione dal cluster, sono necessari i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="f16b0-113">To completely remove an application from the cluster involves the following steps:</span></span>

1. <span data-ttu-id="f16b0-114">Rimuovere (o eliminare) l'istanza dell'applicazione in esecuzione</span><span class="sxs-lookup"><span data-stu-id="f16b0-114">Remove (or delete) the running application instance</span></span>
2. <span data-ttu-id="f16b0-115">Annullare la registrazione del tipo di applicazione se non è più necessario</span><span class="sxs-lookup"><span data-stu-id="f16b0-115">Unregister the application type if you no longer need it</span></span>
3. <span data-ttu-id="f16b0-116">Rimuovere il pacchetto applicazione da Image Store.</span><span class="sxs-lookup"><span data-stu-id="f16b0-116">Remove the application package from the image store</span></span>

<span data-ttu-id="f16b0-117">Se si usa [Visual Studio per eseguire la distribuzione e il debug delle applicazioni](service-fabric-publish-app-remote-cluster.md) nel cluster di sviluppo locale, tutti i passaggi precedenti vengono gestiti automaticamente tramite uno script di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f16b0-117">If you use [Visual Studio for deploying and debugging applications](service-fabric-publish-app-remote-cluster.md) on your local development cluster, all the preceding steps are handled automatically through a PowerShell script.</span></span>  <span data-ttu-id="f16b0-118">Questo script è disponibile nella cartella *Scripts* del progetto dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="f16b0-118">This script is found in the *Scripts* folder of the application project.</span></span> <span data-ttu-id="f16b0-119">Questo articolo illustra le operazioni eseguite da tali script per consentirne l'esecuzione anche all'esterno di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f16b0-119">This article provides background on what that script is doing so that you can perform the same operations outside of Visual Studio.</span></span> 
 
## <a name="connect-to-the-cluster"></a><span data-ttu-id="f16b0-120">Connettersi al cluster</span><span class="sxs-lookup"><span data-stu-id="f16b0-120">Connect to the cluster</span></span>
<span data-ttu-id="f16b0-121">Prima di eseguire qualsiasi comando PowerShell incluso in questo articolo, iniziare sempre usando [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) per connettersi al cluster di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="f16b0-121">Before you run any PowerShell commands in this article, always start by using [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) to connect to the Service Fabric cluster.</span></span> <span data-ttu-id="f16b0-122">Per connettersi al cluster di sviluppo locale eseguire le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="f16b0-122">To connect to the local development cluster, run the following:</span></span>

```powershell
PS C:\>Connect-ServiceFabricCluster
```

<span data-ttu-id="f16b0-123">Per alcuni esempi di connessione a un cluster remoto o a un cluster protetto mediante Azure Active Directory, certificati X509 o Windows Active Directory, vedere [Connettersi a un cluster sicuro](service-fabric-connect-to-secure-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="f16b0-123">For examples of connecting to a remote cluster or cluster secured using Azure Active Directory, X509 certificates, or Windows Active Directory see [Connect to a secure cluster](service-fabric-connect-to-secure-cluster.md).</span></span>

## <a name="upload-the-application-package"></a><span data-ttu-id="f16b0-124">Caricare il pacchetto applicazione</span><span class="sxs-lookup"><span data-stu-id="f16b0-124">Upload the application package</span></span>
<span data-ttu-id="f16b0-125">Quando si carica il pacchetto dell’applicazione, la si inserisce in un percorso accessibile ai componenti interni di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="f16b0-125">Uploading the application package puts it in a location that's accessible by internal Service Fabric components.</span></span>
<span data-ttu-id="f16b0-126">Se si desidera verificare il pacchetto dell'applicazione in locale, usare il cmdlet [Test-ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="f16b0-126">If you want to verify the application package locally, use the [Test-ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="f16b0-127">Il comando [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) consente di caricare il pacchetto dell'applicazione nell'archivio di immagini del cluster.</span><span class="sxs-lookup"><span data-stu-id="f16b0-127">The [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) command uploads the application package to the cluster image store.</span></span>
<span data-ttu-id="f16b0-128">Il cmdlet **Get-ImageStoreConnectionStringFromClusterManifest** , che fa parte del modulo PowerShell Service Fabric SDK, viene usato per ottenere la stringa di connessione dell'archivio immagini.</span><span class="sxs-lookup"><span data-stu-id="f16b0-128">The **Get-ImageStoreConnectionStringFromClusterManifest** cmdlet, which is part of the Service Fabric SDK PowerShell module, is used to get the image store connection string.</span></span>  <span data-ttu-id="f16b0-129">Per importare il modulo SDK, eseguire:</span><span class="sxs-lookup"><span data-stu-id="f16b0-129">To import the SDK module, run:</span></span>

```powershell
Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
```

<span data-ttu-id="f16b0-130">Si supponga di compilare e assemblare un'applicazione denominata *MyApplication* in Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="f16b0-130">Suppose you build and package an application named *MyApplication* in Visual Studio 2015.</span></span> <span data-ttu-id="f16b0-131">Per impostazione predefinita, il nome del tipo di applicazione elencato nel file ApplicationManifest.xml è "MyApplicationType".</span><span class="sxs-lookup"><span data-stu-id="f16b0-131">By default, the application type name listed in the ApplicationManifest.xml is "MyApplicationType".</span></span>  <span data-ttu-id="f16b0-132">Il pacchetto dell'applicazione, che contiene il manifesto dell'applicazione necessario, i manifesti dei servizi e i pacchetti di codice, configurazione e dati, si trova in *C:\Users\<username\>\Documents\Visual Studio 2015\Projects\MyApplication\MyApplication\pkg\Debug*.</span><span class="sxs-lookup"><span data-stu-id="f16b0-132">The application package, which contains the necessary application manifest, service manifests, and code/config/data packages, is located in *C:\Users\<username\>\Documents\Visual Studio 2015\Projects\MyApplication\MyApplication\pkg\Debug*.</span></span> 

<span data-ttu-id="f16b0-133">Il comando seguente elenca il contenuto del pacchetto dell'applicazione:</span><span class="sxs-lookup"><span data-stu-id="f16b0-133">The following command lists the contents of the application package:</span></span>

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

<span data-ttu-id="f16b0-134">Se il pacchetto dell'applicazione è di grandi dimensioni e/o dispone di molti file, è possibile [comprimerlo](service-fabric-package-apps.md#compress-a-package).</span><span class="sxs-lookup"><span data-stu-id="f16b0-134">If the application package is large and/or has many files, you can [compress it](service-fabric-package-apps.md#compress-a-package).</span></span> <span data-ttu-id="f16b0-135">La compressione riduce le dimensioni e il numero di file.</span><span class="sxs-lookup"><span data-stu-id="f16b0-135">The compression reduces the size and the number of files.</span></span>
<span data-ttu-id="f16b0-136">L'effetto collaterale è che la registrazione e l'annullamento della registrazione del tipo di applicazione sono più veloci.</span><span class="sxs-lookup"><span data-stu-id="f16b0-136">The side effect is that registering and un-registering the application type are faster.</span></span> <span data-ttu-id="f16b0-137">Il tempo di caricamento potrebbe attualmente risultare più lento, specialmente se si include il tempo per comprimere il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="f16b0-137">Upload time may be slower currently, especially if you include the time to compress the package.</span></span> 

<span data-ttu-id="f16b0-138">Per comprimere un pacchetto, usare il medesimo comando [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="f16b0-138">To compress a package, use the same [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) command.</span></span> <span data-ttu-id="f16b0-139">La compressione può avere luogo separatamente dal caricamento, tramite il flag `SkipCopy`, oppure contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="f16b0-139">Compression can be done separate from upload, by using the `SkipCopy` flag, or together with the upload operation.</span></span> <span data-ttu-id="f16b0-140">L'applicazione della compressione a un pacchetto compresso è no-op.</span><span class="sxs-lookup"><span data-stu-id="f16b0-140">Applying compression on a compressed package is no-op.</span></span>
<span data-ttu-id="f16b0-141">Per decomprimere un pacchetto compresso, usare il medesimo comando [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) con lo switch `UncompressPackage`.</span><span class="sxs-lookup"><span data-stu-id="f16b0-141">To uncompress a compressed package, use the same [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) command with the `UncompressPackage` switch.</span></span>

<span data-ttu-id="f16b0-142">Il cmdlet seguente comprime il pacchetto senza copiarlo nell'archivio immagini.</span><span class="sxs-lookup"><span data-stu-id="f16b0-142">The following cmdlet compresses the package without copying it to the image store.</span></span> <span data-ttu-id="f16b0-143">Ora il pacchetto include i file compressi per i pacchetti `Code` e `Config`.</span><span class="sxs-lookup"><span data-stu-id="f16b0-143">The package now includes zipped files for the `Code` and `Config` packages.</span></span> <span data-ttu-id="f16b0-144">I manifesti dell'applicazione e del servizio non sono compressi in quanto necessari per numerose operazioni interne, come la condivisione dei pacchetti e l'estrazione del nome e della versione del tipo di applicazione per determinate convalide.</span><span class="sxs-lookup"><span data-stu-id="f16b0-144">The application and the service manifests are not zipped, because they are needed for many internal operations (like package sharing, application type name and version extraction for certain validations).</span></span> <span data-ttu-id="f16b0-145">La compressione dei manifesti renderebbe inefficienti tali operazioni.</span><span class="sxs-lookup"><span data-stu-id="f16b0-145">Zipping the manifests would make these operations inefficient.</span></span>

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

<span data-ttu-id="f16b0-146">Per i pacchetti di applicazione di grandi dimensioni, la compressione richiede tempo.</span><span class="sxs-lookup"><span data-stu-id="f16b0-146">For large application packages, the compression takes time.</span></span> <span data-ttu-id="f16b0-147">Per ottenere risultati ottimali, usare un'unità SSD rapida.</span><span class="sxs-lookup"><span data-stu-id="f16b0-147">For best results, use a fast SSD drive.</span></span> <span data-ttu-id="f16b0-148">Anche i tempi di compressione e la dimensione del pacchetto compresso variano in base al contenuto del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="f16b0-148">The compression times and the size of the compressed package also differ based on the package content.</span></span>
<span data-ttu-id="f16b0-149">Ad esempio, ecco le statistiche della compressione per alcuni pacchetti, che mostrano le dimensioni del pacchetto iniziale e di quello compresso, insieme al tempo di compressione.</span><span class="sxs-lookup"><span data-stu-id="f16b0-149">For example, here is compression statistics for some packages, which show the initial and the compressed package size, with the compression time.</span></span>

|<span data-ttu-id="f16b0-150">Dimensioni iniziali (MB)</span><span class="sxs-lookup"><span data-stu-id="f16b0-150">Initial size (MB)</span></span>|<span data-ttu-id="f16b0-151">Numero di file</span><span class="sxs-lookup"><span data-stu-id="f16b0-151">File count</span></span>|<span data-ttu-id="f16b0-152">Tempo di compressione</span><span class="sxs-lookup"><span data-stu-id="f16b0-152">Compression Time</span></span>|<span data-ttu-id="f16b0-153">Dimensioni pacchetto compresso (MB)</span><span class="sxs-lookup"><span data-stu-id="f16b0-153">Compressed package size (MB)</span></span>|
|----------------:|---------:|---------------:|---------------------------:|
|<span data-ttu-id="f16b0-154">100</span><span class="sxs-lookup"><span data-stu-id="f16b0-154">100</span></span>|<span data-ttu-id="f16b0-155">100</span><span class="sxs-lookup"><span data-stu-id="f16b0-155">100</span></span>|<span data-ttu-id="f16b0-156">00:00:03.3547592</span><span class="sxs-lookup"><span data-stu-id="f16b0-156">00:00:03.3547592</span></span>|<span data-ttu-id="f16b0-157">60</span><span class="sxs-lookup"><span data-stu-id="f16b0-157">60</span></span>|
|<span data-ttu-id="f16b0-158">512</span><span class="sxs-lookup"><span data-stu-id="f16b0-158">512</span></span>|<span data-ttu-id="f16b0-159">100</span><span class="sxs-lookup"><span data-stu-id="f16b0-159">100</span></span>|<span data-ttu-id="f16b0-160">00:00:16.3850303</span><span class="sxs-lookup"><span data-stu-id="f16b0-160">00:00:16.3850303</span></span>|<span data-ttu-id="f16b0-161">307</span><span class="sxs-lookup"><span data-stu-id="f16b0-161">307</span></span>|
|<span data-ttu-id="f16b0-162">1024</span><span class="sxs-lookup"><span data-stu-id="f16b0-162">1024</span></span>|<span data-ttu-id="f16b0-163">500</span><span class="sxs-lookup"><span data-stu-id="f16b0-163">500</span></span>|<span data-ttu-id="f16b0-164">00:00:32.5907950</span><span class="sxs-lookup"><span data-stu-id="f16b0-164">00:00:32.5907950</span></span>|<span data-ttu-id="f16b0-165">615</span><span class="sxs-lookup"><span data-stu-id="f16b0-165">615</span></span>|
|<span data-ttu-id="f16b0-166">2048</span><span class="sxs-lookup"><span data-stu-id="f16b0-166">2048</span></span>|<span data-ttu-id="f16b0-167">1000</span><span class="sxs-lookup"><span data-stu-id="f16b0-167">1000</span></span>|<span data-ttu-id="f16b0-168">00:01:04.3775554</span><span class="sxs-lookup"><span data-stu-id="f16b0-168">00:01:04.3775554</span></span>|<span data-ttu-id="f16b0-169">1231</span><span class="sxs-lookup"><span data-stu-id="f16b0-169">1231</span></span>|
|<span data-ttu-id="f16b0-170">5012</span><span class="sxs-lookup"><span data-stu-id="f16b0-170">5012</span></span>|<span data-ttu-id="f16b0-171">100</span><span class="sxs-lookup"><span data-stu-id="f16b0-171">100</span></span>|<span data-ttu-id="f16b0-172">00:02:45.2951288</span><span class="sxs-lookup"><span data-stu-id="f16b0-172">00:02:45.2951288</span></span>|<span data-ttu-id="f16b0-173">3074</span><span class="sxs-lookup"><span data-stu-id="f16b0-173">3074</span></span>|

<span data-ttu-id="f16b0-174">Una volta compresso, un pacchetto può essere caricato in uno o più cluster di Service Fabric in base alle necessità.</span><span class="sxs-lookup"><span data-stu-id="f16b0-174">Once a package is compressed, it can be uploaded to one or multiple Service Fabric clusters as needed.</span></span> <span data-ttu-id="f16b0-175">Il meccanismo di distribuzione è lo stesso per i pacchetti compressi e non.</span><span class="sxs-lookup"><span data-stu-id="f16b0-175">The deployment mechanism is same for compressed and uncompressed packages.</span></span> <span data-ttu-id="f16b0-176">Se il pacchetto è compresso, viene archiviato come tale nell'archivio immagini del cluster e viene decompresso nel nodo prima dell'esecuzione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="f16b0-176">If the package is compressed, it is stored as such in the cluster image store and it's uncompressed on the node before the application is run.</span></span>


<span data-ttu-id="f16b0-177">L'esempio seguente carica il pacchetto nell'archivio di immagini, in una cartella denominata "MyApplicationV1":</span><span class="sxs-lookup"><span data-stu-id="f16b0-177">The following example uploads the package to the image store, into a folder named "MyApplicationV1":</span></span>

```powershell
PS C:\> Copy-ServiceFabricApplicationPackage -ApplicationPackagePath $path -ApplicationPackagePathInImageStore MyApplicationV1 -ImageStoreConnectionString (Get-ImageStoreConnectionStringFromClusterManifest(Get-ServiceFabricClusterManifest)) -TimeoutSec 1800
```

<span data-ttu-id="f16b0-178">Il cmdlet **Get-ImageStoreConnectionStringFromClusterManifest** , che fa parte del modulo PowerShell Service Fabric SDK, viene usato per ottenere la stringa di connessione dell'archivio immagini.</span><span class="sxs-lookup"><span data-stu-id="f16b0-178">The **Get-ImageStoreConnectionStringFromClusterManifest** cmdlet, which is part of the Service Fabric SDK PowerShell module, is used to get the image store connection string.</span></span>  <span data-ttu-id="f16b0-179">Per importare il modulo SDK, eseguire:</span><span class="sxs-lookup"><span data-stu-id="f16b0-179">To import the SDK module, run:</span></span>

```powershell
Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
```

<span data-ttu-id="f16b0-180">Se non si specifica il parametro *-ApplicationPackagePathInImageStore*, il pacchetto dell'applicazione viene copiato nella cartella "Debug" dell'archivio immagini.</span><span class="sxs-lookup"><span data-stu-id="f16b0-180">If you do not specify the *-ApplicationPackagePathInImageStore* parameter, the application package is copied into the "Debug" folder in the image store.</span></span>

<span data-ttu-id="f16b0-181">Il tempo necessario per caricare un pacchetto varia in base a diversi fattori.</span><span class="sxs-lookup"><span data-stu-id="f16b0-181">The time it takes to upload a package differs depending on multiple factors.</span></span> <span data-ttu-id="f16b0-182">Tra questi, ad esempio, il numero di file nel pacchetto, le dimensioni del pacchetto stesso e dei file singoli.</span><span class="sxs-lookup"><span data-stu-id="f16b0-182">Some of these factors are the number of files in the package, the package size, and the file sizes.</span></span> <span data-ttu-id="f16b0-183">Anche la velocità di rete tra il computer di origine e il cluster di Service Fabric influisce sul tempo di caricamento.</span><span class="sxs-lookup"><span data-stu-id="f16b0-183">The network speed between the source machine and the Service Fabric cluster also impacts the upload time.</span></span> <span data-ttu-id="f16b0-184">Il timeout predefinito per [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) è di 30 minuti.</span><span class="sxs-lookup"><span data-stu-id="f16b0-184">The default timeout for [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) is 30 minutes.</span></span>
<span data-ttu-id="f16b0-185">In base ai fattori descritti, potrebbe essere necessario aumentare il timeout.</span><span class="sxs-lookup"><span data-stu-id="f16b0-185">Depending on the described factors, you may have to increase the timeout.</span></span> <span data-ttu-id="f16b0-186">Se si sta eseguendo la compressione del pacchetto nella chiamata di copia, è necessario considerare anche il tempo di compressione.</span><span class="sxs-lookup"><span data-stu-id="f16b0-186">If you are compressing the package in the copy call, you need to also consider the compression time.</span></span>

<span data-ttu-id="f16b0-187">Per informazioni agguntive sull'archivio di immagini e ImageStoreConnectionString, vedere [Understand the image store connection string](service-fabric-image-store-connection-string.md) (Comprendere la stringa di connessione dell'archivio di immagini).</span><span class="sxs-lookup"><span data-stu-id="f16b0-187">See [Understand the image store connection string](service-fabric-image-store-connection-string.md) for supplementary information about the image store and image store connection string.</span></span>

## <a name="register-the-application-package"></a><span data-ttu-id="f16b0-188">Registrare il pacchetto applicazione</span><span class="sxs-lookup"><span data-stu-id="f16b0-188">Register the application package</span></span>
<span data-ttu-id="f16b0-189">Quando si registra il pacchetto dell'applicazione, il tipo e la versione dell'applicazione dichiarati nel manifesto di quest'ultima diventano disponibili per l'uso.</span><span class="sxs-lookup"><span data-stu-id="f16b0-189">The application type and version declared in the application manifest become available for use when the application package is registered.</span></span> <span data-ttu-id="f16b0-190">Il sistema leggerà il pacchetto caricato al passaggio precedente, lo verificherà, ne elaborerà il contenuto e infine copierà il pacchetto elaborato in un percorso di sistema interno.</span><span class="sxs-lookup"><span data-stu-id="f16b0-190">The system reads the package uploaded in the previous step, verifies the package, processes the package contents, and copies the processed package to an internal system location.</span></span>  

<span data-ttu-id="f16b0-191">Eseguire il cmdlet [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) per registrare il tipo di applicazione nel cluster e renderlo disponibile per la distribuzione:</span><span class="sxs-lookup"><span data-stu-id="f16b0-191">Run the [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) cmdlet to register the application type in the cluster and make it available for deployment:</span></span>

```powershell
PS C:\> Register-ServiceFabricApplicationType MyApplicationV1
Register application type succeeded
```

<span data-ttu-id="f16b0-192">"MyApplicationV1" è la cartella nell'archivio immagini in cui si trova il pacchetto dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="f16b0-192">"MyApplicationV1" is the folder in the image store where the application package is located.</span></span> <span data-ttu-id="f16b0-193">Il tipo di applicazione con il nome "MyApplicationType" e la versione "1.0.0" (entrambi si trovano nel manifesto dell'applicazione) è registrato nel cluster.</span><span class="sxs-lookup"><span data-stu-id="f16b0-193">The application type with name "MyApplicationType" and version "1.0.0" (both are found in the application manifest) is now registered in the cluster.</span></span>

<span data-ttu-id="f16b0-194">Il comando [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) restituirà il controllo solo dopo che il sistema avrà registrato correttamente il pacchetto dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="f16b0-194">The [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) command returns only after the system has successfully registered the application package.</span></span> <span data-ttu-id="f16b0-195">La durata della registrazione dipende dalla dimensione e dal contenuto del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="f16b0-195">How long registration takes depends on the size and contents of the application package.</span></span> <span data-ttu-id="f16b0-196">Se necessario, è possibile usare il parametro **-TimeoutSec** per specificare un intervallo di tempo più esteso per il timeout. Il timeout predefinito è di 60 secondi.</span><span class="sxs-lookup"><span data-stu-id="f16b0-196">If needed, the **-TimeoutSec** parameter can be used to supply a longer timeout (the default timeout is 60 seconds).</span></span>

<span data-ttu-id="f16b0-197">Se si dispone di un pacchetto dell'applicazione di grandi dimensioni o se si verificano timeout, usare il parametro **-Async**.</span><span class="sxs-lookup"><span data-stu-id="f16b0-197">If you have a large application package or if you are experiencing timeouts, use the **-Async** parameter.</span></span> <span data-ttu-id="f16b0-198">Il comando restituisce un valore quando il cluster accetta il comando di registrazione e l'elaborazione continua come da richiesta.</span><span class="sxs-lookup"><span data-stu-id="f16b0-198">The command returns when the cluster accepts the register command, and the processing continues as needed.</span></span>
<span data-ttu-id="f16b0-199">Il comando [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) elenca tutte le versioni del tipo di applicazione registrate correttamente e il loro stato di registrazione.</span><span class="sxs-lookup"><span data-stu-id="f16b0-199">The [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) command lists all successfully registered application type versions and their registration status.</span></span> <span data-ttu-id="f16b0-200">È possibile usare questo comando per determinare quando viene eseguita la registrazione.</span><span class="sxs-lookup"><span data-stu-id="f16b0-200">You can use this command to determine when the registration is done.</span></span>

```powershell
PS C:\> Get-ServiceFabricApplicationType

ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
Status                 : Available
DefaultParameters      : { "Stateless1_InstanceCount" = "-1" }
```

## <a name="create-the-application"></a><span data-ttu-id="f16b0-201">Creazione dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="f16b0-201">Create the application</span></span>
<span data-ttu-id="f16b0-202">È possibile creare un'istanza di un'applicazione da qualsiasi versione del tipo di applicazione registrata mediante il cmdlet [New-ServiceFabricApplication](/powershell/module/servicefabric/new-servicefabricapplication?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="f16b0-202">You can instantiate an application from any application type version that has been registered successfully by using the [New-ServiceFabricApplication](/powershell/module/servicefabric/new-servicefabricapplication?view=azureservicefabricps) cmdlet.</span></span> <span data-ttu-id="f16b0-203">Il nome di ogni applicazione deve iniziare con lo schema *"fabric:"* e deve essere univoco per ogni istanza dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="f16b0-203">The name of each application must start with the *"fabric:"* scheme and must be unique for each application instance.</span></span> <span data-ttu-id="f16b0-204">Vengono creati anche i servizi predefiniti specificati nel manifesto dell'applicazione del tipo di applicazione di destinazione.</span><span class="sxs-lookup"><span data-stu-id="f16b0-204">Any default services defined in the application manifest of the target application type are also created.</span></span>

```powershell
PS C:\> New-ServiceFabricApplication fabric:/MyApp MyApplicationType 1.0.0

ApplicationName        : fabric:/MyApp
ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
ApplicationParameters  : {}
```
<span data-ttu-id="f16b0-205">Per qualsiasi versione di un tipo di applicazione registrato, è possibile creare più istanze dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="f16b0-205">Multiple application instances can be created for any given version of a registered application type.</span></span> <span data-ttu-id="f16b0-206">Ogni istanza viene eseguita in isolamento, con un proprio processo e una propria directory di lavoro.</span><span class="sxs-lookup"><span data-stu-id="f16b0-206">Each application instance runs in isolation, with its own work directory and process.</span></span>

<span data-ttu-id="f16b0-207">Per vedere quali app e servizi sono in esecuzione nel cluster, eseguire i cmdlet [Get-ServiceFabricApplication](/powershell/servicefabric/vlatest/get-servicefabricapplication) e [Get-ServiceFabricService](/powershell/module/servicefabric/get-servicefabricservice?view=azureservicefabricps):</span><span class="sxs-lookup"><span data-stu-id="f16b0-207">To see which named apps and services are running in the cluster, run the [Get-ServiceFabricApplication](/powershell/servicefabric/vlatest/get-servicefabricapplication) and [Get-ServiceFabricService](/powershell/module/servicefabric/get-servicefabricservice?view=azureservicefabricps) cmdlets:</span></span>

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

## <a name="remove-an-application"></a><span data-ttu-id="f16b0-208">Rimuovere un'applicazione</span><span class="sxs-lookup"><span data-stu-id="f16b0-208">Remove an application</span></span>
<span data-ttu-id="f16b0-209">Quando un'istanza dell'applicazione non è più necessaria, è possibile rimuoverla definitivamente per nome usando il cmdlet [Remove-ServiceFabricApplication](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="f16b0-209">When an application instance is no longer needed, you can permanently remove it by name using the [Remove-ServiceFabricApplication](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps) cmdlet.</span></span> <span data-ttu-id="f16b0-210">[Remove-ServiceFabricApplication](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps) rimuove automaticamente anche tutti i servizi appartenenti all'applicazione, nonché il relativo stato di servizio.</span><span class="sxs-lookup"><span data-stu-id="f16b0-210">[Remove-ServiceFabricApplication](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps) automatically removes all services that belong to the application as well, permanently removing all service state.</span></span> 

> [!WARNING]
> <span data-ttu-id="f16b0-211">Tale operazione non può essere annullata e lo stato dell'applicazione non può essere recuperato.</span><span class="sxs-lookup"><span data-stu-id="f16b0-211">This operation cannot be reversed, and application state cannot be recovered.</span></span>

```powershell
PS C:\> Remove-ServiceFabricApplication fabric:/MyApp

Confirm
Continue with this operation?
[Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"):
Remove application instance succeeded

PS C:\> Get-ServiceFabricApplication
```

## <a name="unregister-an-application-type"></a><span data-ttu-id="f16b0-212">Annullare la registrazione di un tipo di applicazione</span><span class="sxs-lookup"><span data-stu-id="f16b0-212">Unregister an application type</span></span>
<span data-ttu-id="f16b0-213">Quando una determinata versione di un tipo di applicazione non è più necessaria, è consigliabile annullare la registrazione del tipo di applicazione usando il cmdlet [Unregister-ServiceFabricApplicationType](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="f16b0-213">When a particular version of an application type is no longer needed, you should unregister the application type using the [Unregister-ServiceFabricApplicationType](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) cmdlet.</span></span> <span data-ttu-id="f16b0-214">L'annullamento della registrazione dei tipi di applicazione inutilizzati rilascia lo spazio di archiviazione utilizzato dell'archivio di immagini.</span><span class="sxs-lookup"><span data-stu-id="f16b0-214">Unregistering unused application types releases storage space used by the image store.</span></span> <span data-ttu-id="f16b0-215">È possibile annullare la registrazione di un tipo di applicazione solo se non sono state create istanze di applicazioni basate su di esso o non vi sono aggiornamenti di applicazioni in sospeso che vi fanno riferimento.</span><span class="sxs-lookup"><span data-stu-id="f16b0-215">An application type can be unregistered as long as no applications are instantiated against it and no pending application upgrades are referencing it.</span></span>

<span data-ttu-id="f16b0-216">Eseguire [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) per vedere i tipi di applicazione attualmente registrati nel cluster:</span><span class="sxs-lookup"><span data-stu-id="f16b0-216">Run [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) to see the application types currently registered in the cluster:</span></span>

```powershell
PS C:\> Get-ServiceFabricApplicationType

ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
Status                 : Available
DefaultParameters      : { "Stateless1_InstanceCount" = "-1" }
```

<span data-ttu-id="f16b0-217">Eseguire [Unregister-ServiceFabricApplicationType](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) per annullare la registrazione di un tipo di applicazione specifico:</span><span class="sxs-lookup"><span data-stu-id="f16b0-217">Run [Unregister-ServiceFabricApplicationType](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) to unregister a specific application type:</span></span>

```powershell
PS C:\> Unregister-ServiceFabricApplicationType MyApplicationType 1.0.0
```

## <a name="remove-an-application-package-from-the-image-store"></a><span data-ttu-id="f16b0-218">Rimuovere il pacchetto di un'applicazione dall'archivio di immagini</span><span class="sxs-lookup"><span data-stu-id="f16b0-218">Remove an application package from the image store</span></span>
<span data-ttu-id="f16b0-219">Quando il pacchetto di un'applicazione non è più necessario, è possibile eliminarlo dall'archivio di immagini per liberare risorse di sistema.</span><span class="sxs-lookup"><span data-stu-id="f16b0-219">When an application package is no longer needed, you can delete it from the image store to free up system resources.</span></span>

```powershell
PS C:\>Remove-ServiceFabricApplicationPackage -ApplicationPackagePathInImageStore MyApplicationV1 -ImageStoreConnectionString (Get-ImageStoreConnectionStringFromClusterManifest(Get-ServiceFabricClusterManifest))
```

## <a name="troubleshooting"></a><span data-ttu-id="f16b0-220">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="f16b0-220">Troubleshooting</span></span>
### <a name="copy-servicefabricapplicationpackage-asks-for-an-imagestoreconnectionstring"></a><span data-ttu-id="f16b0-221">Copy-ServiceFabricApplicationPackage chiede un parametro ImageStoreConnectionString</span><span class="sxs-lookup"><span data-stu-id="f16b0-221">Copy-ServiceFabricApplicationPackage asks for an ImageStoreConnectionString</span></span>
<span data-ttu-id="f16b0-222">Nell'ambiente Service Fabric SDK dovrebbero già essere configurate le impostazioni predefinite corrette.</span><span class="sxs-lookup"><span data-stu-id="f16b0-222">The Service Fabric SDK environment should already have the correct defaults set up.</span></span> <span data-ttu-id="f16b0-223">Tuttavia, se necessario, ImageStoreConnectionString per tutti i comandi deve corrispondere al valore che viene usato dal cluster Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="f16b0-223">But if needed, the ImageStoreConnectionString for all commands should match the value that the Service Fabric cluster is using.</span></span> <span data-ttu-id="f16b0-224">È possibile trovare ImageStoreConnectionString nel manifesto del cluster, recuperato tramite i comandi [Get-ServiceFabricClusterManifest](/powershell/module/servicefabric/get-servicefabricclustermanifest?view=azureservicefabricps) e Get-ImageStoreConnectionStringFromClusterManifest:</span><span class="sxs-lookup"><span data-stu-id="f16b0-224">You can find the ImageStoreConnectionString in the cluster manifest, retrieved using the [Get-ServiceFabricClusterManifest](/powershell/module/servicefabric/get-servicefabricclustermanifest?view=azureservicefabricps) and Get-ImageStoreConnectionStringFromClusterManifest commands:</span></span>

```powershell
PS C:\> Get-ImageStoreConnectionStringFromClusterManifest(Get-ServiceFabricClusterManifest)
```

<span data-ttu-id="f16b0-225">Il cmdlet **Get-ImageStoreConnectionStringFromClusterManifest** , che fa parte del modulo PowerShell Service Fabric SDK, viene usato per ottenere la stringa di connessione dell'archivio immagini.</span><span class="sxs-lookup"><span data-stu-id="f16b0-225">The **Get-ImageStoreConnectionStringFromClusterManifest** cmdlet, which is part of the Service Fabric SDK PowerShell module, is used to get the image store connection string.</span></span>  <span data-ttu-id="f16b0-226">Per importare il modulo SDK, eseguire:</span><span class="sxs-lookup"><span data-stu-id="f16b0-226">To import the SDK module, run:</span></span>

```powershell
Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
```

<span data-ttu-id="f16b0-227">ImageStoreConnectionString è disponibile nel manifesto del cluster:</span><span class="sxs-lookup"><span data-stu-id="f16b0-227">The ImageStoreConnectionString is found in the cluster manifest:</span></span>

```xml
<ClusterManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Name="Server-Default-SingleNode" Version="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">

    [...]

    <Section Name="Management">
      <Parameter Name="ImageStoreConnectionString" Value="file:D:\ServiceFabric\Data\ImageStore" />
    </Section>

    [...]
```

<span data-ttu-id="f16b0-228">Per informazioni agguntive sull'archivio di immagini e ImageStoreConnectionString, vedere [Understand the image store connection string](service-fabric-image-store-connection-string.md) (Comprendere la stringa di connessione dell'archivio di immagini).</span><span class="sxs-lookup"><span data-stu-id="f16b0-228">See [Understand the image store connection string](service-fabric-image-store-connection-string.md) for supplementary information about the image store and image store connection string.</span></span>

### <a name="deploy-large-application-package"></a><span data-ttu-id="f16b0-229">Distribuire un pacchetto dell'applicazione di grandi dimensioni</span><span class="sxs-lookup"><span data-stu-id="f16b0-229">Deploy large application package</span></span>
<span data-ttu-id="f16b0-230">Problema: [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) raggiunge il timeout per un pacchetto dell'applicazione di grandi dimensioni (nell'ordine di GB).</span><span class="sxs-lookup"><span data-stu-id="f16b0-230">Issue: [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) times out for a large application package (order of GB).</span></span>
<span data-ttu-id="f16b0-231">Soluzione:</span><span class="sxs-lookup"><span data-stu-id="f16b0-231">Try:</span></span>
- <span data-ttu-id="f16b0-232">Specificare un timeout maggiore per il comando [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps), con il parametro `TimeoutSec`.</span><span class="sxs-lookup"><span data-stu-id="f16b0-232">Specify a larger timeout for [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) command, with `TimeoutSec` parameter.</span></span> <span data-ttu-id="f16b0-233">Il timeout è di 30 minuti per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="f16b0-233">By default, the timeout is 30 minutes.</span></span>
- <span data-ttu-id="f16b0-234">Controllare la connessione di rete tra il computer di origine e il cluster.</span><span class="sxs-lookup"><span data-stu-id="f16b0-234">Check the network connection between your source machine and cluster.</span></span> <span data-ttu-id="f16b0-235">Se la connessione è lenta, provare a usare una macchina con una connessione di rete più veloce.</span><span class="sxs-lookup"><span data-stu-id="f16b0-235">If the connection is slow, consider using a machine with a better network connection.</span></span>
<span data-ttu-id="f16b0-236">Se il computer client si trova in un'area diversa dal cluster, si consiglia di usare un computer cliente in un'area più vicina o nella stessa area del cluster.</span><span class="sxs-lookup"><span data-stu-id="f16b0-236">If the client machine is in another region than the cluster, consider using a client machine in a closer or same region as the cluster.</span></span>
- <span data-ttu-id="f16b0-237">Controllare se si stiano raggiungendo le limitazioni esterne.</span><span class="sxs-lookup"><span data-stu-id="f16b0-237">Check if you are hitting external throttling.</span></span> <span data-ttu-id="f16b0-238">Ad esempio, quando l'archivio immagini è configurato per usare l'archiviazione di Azure, il caricamento potrebbe essere limitato.</span><span class="sxs-lookup"><span data-stu-id="f16b0-238">For example, when the image store is configured to use azure storage, upload may be throttled.</span></span>

<span data-ttu-id="f16b0-239">Problema: Il pacchetto è stato caricato completamente ma si è verificato un timeout di [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="f16b0-239">Issue: Upload package completed successfully, but [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) times out.</span></span>
<span data-ttu-id="f16b0-240">Soluzione:</span><span class="sxs-lookup"><span data-stu-id="f16b0-240">Try:</span></span>
- <span data-ttu-id="f16b0-241">[Comprimere il pacchetto](service-fabric-package-apps.md#compress-a-package) prima di copiarlo nell'archivio immagini.</span><span class="sxs-lookup"><span data-stu-id="f16b0-241">[Compress the package](service-fabric-package-apps.md#compress-a-package) before copying to the image store.</span></span>
<span data-ttu-id="f16b0-242">La compressione riduce le dimensioni e il numero di file, cosa che a sua volta riduce il traffico e le operazioni di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="f16b0-242">The compression reduces the size and the number of files, which in turn reduces the amount of traffic and work that Service Fabric must perform.</span></span> <span data-ttu-id="f16b0-243">L'operazione di caricamento potrebbe risultare più lenta (specialmente se si include il tempo di compressione), ma registrazione e relativo annullamento del tipo dell'applicazione saranno più veloci.</span><span class="sxs-lookup"><span data-stu-id="f16b0-243">The upload operation may be slower (especially if you include the compression time), but register and un-register the application type are faster.</span></span>
- <span data-ttu-id="f16b0-244">Specificare un timeout maggiore per il comando [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps), con il parametro `TimeoutSec`.</span><span class="sxs-lookup"><span data-stu-id="f16b0-244">Specify a larger timeout for [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) with `TimeoutSec` parameter.</span></span>
- <span data-ttu-id="f16b0-245">Specificare lo switch `Async` per [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="f16b0-245">Specify `Async` switch for [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps).</span></span> <span data-ttu-id="f16b0-246">Il comando viene completato quando il cluster accetta il comando e la registrazione del tipo di applicazione continua in modo asincrono.</span><span class="sxs-lookup"><span data-stu-id="f16b0-246">The command returns when the cluster accepts the command and the registration of the application type continues asynchronously.</span></span> <span data-ttu-id="f16b0-247">Per questo motivo, in questo caso non è necessario specificare un timeout maggiore.</span><span class="sxs-lookup"><span data-stu-id="f16b0-247">For this reason, there is no need to specify a higher timeout in this case.</span></span> <span data-ttu-id="f16b0-248">Il comando [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) elenca tutte le versioni del tipo di applicazione registrate correttamente e il loro stato di registrazione.</span><span class="sxs-lookup"><span data-stu-id="f16b0-248">The [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) command lists all successfully registered application type versions and their registration status.</span></span> <span data-ttu-id="f16b0-249">È possibile usare questo comando per determinare quando viene eseguita la registrazione.</span><span class="sxs-lookup"><span data-stu-id="f16b0-249">You can use this command to determine when the registration is done.</span></span>

```powershell
PS C:\> Get-ServiceFabricApplicationType

ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
Status                 : Available
DefaultParameters      : { "Stateless1_InstanceCount" = "-1" }
```

### <a name="deploy-application-package-with-many-files"></a><span data-ttu-id="f16b0-250">Distribuire un pacchetto di applicazione con numerosi file</span><span class="sxs-lookup"><span data-stu-id="f16b0-250">Deploy application package with many files</span></span>
<span data-ttu-id="f16b0-251">Problema: Si verifica un timeout di [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) per un pacchetto di applicazione con molti file (nell'ordine di migliaia).</span><span class="sxs-lookup"><span data-stu-id="f16b0-251">Issue: [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) times out for an application package with many files (order of thousands).</span></span>
<span data-ttu-id="f16b0-252">Soluzione:</span><span class="sxs-lookup"><span data-stu-id="f16b0-252">Try:</span></span>
- <span data-ttu-id="f16b0-253">[Comprimere il pacchetto](service-fabric-package-apps.md#compress-a-package) prima di copiarlo nell'archivio immagini.</span><span class="sxs-lookup"><span data-stu-id="f16b0-253">[Compress the package](service-fabric-package-apps.md#compress-a-package) before copying to the image store.</span></span> <span data-ttu-id="f16b0-254">La compressione riduce il numero dei file.</span><span class="sxs-lookup"><span data-stu-id="f16b0-254">The compression reduces the number of files.</span></span>
- <span data-ttu-id="f16b0-255">Specificare un timeout maggiore per il comando [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps), con il parametro `TimeoutSec`.</span><span class="sxs-lookup"><span data-stu-id="f16b0-255">Specify a larger timeout for [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) with `TimeoutSec` parameter.</span></span>
- <span data-ttu-id="f16b0-256">Specificare lo switch `Async` per [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="f16b0-256">Specify `Async` switch for [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps).</span></span> <span data-ttu-id="f16b0-257">Il comando viene completato quando il cluster accetta il comando e la registrazione del tipo di applicazione continua in modo asincrono.</span><span class="sxs-lookup"><span data-stu-id="f16b0-257">The command returns when the cluster accepts the command and the registration of the application type continues asynchronously.</span></span>
<span data-ttu-id="f16b0-258">Per questo motivo, in questo caso non è necessario specificare un timeout maggiore.</span><span class="sxs-lookup"><span data-stu-id="f16b0-258">For this reason, there is no need to specify a higher timeout in this case.</span></span> <span data-ttu-id="f16b0-259">Il comando [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) elenca tutte le versioni del tipo di applicazione registrate correttamente e il loro stato di registrazione.</span><span class="sxs-lookup"><span data-stu-id="f16b0-259">The [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) command lists all successfully registered application type versions and their registration status.</span></span> <span data-ttu-id="f16b0-260">È possibile usare questo comando per determinare quando viene eseguita la registrazione.</span><span class="sxs-lookup"><span data-stu-id="f16b0-260">You can use this command to determine when the registration is done.</span></span>

```powershell
PS C:\> Get-ServiceFabricApplicationType

ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
Status                 : Available
DefaultParameters      : { "Stateless1_InstanceCount" = "-1" }
```

## <a name="next-steps"></a><span data-ttu-id="f16b0-261">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f16b0-261">Next steps</span></span>
[<span data-ttu-id="f16b0-262">Aggiornamento di un'applicazione di infrastruttura di servizi</span><span class="sxs-lookup"><span data-stu-id="f16b0-262">Service Fabric application upgrade</span></span>](service-fabric-application-upgrade.md)

[<span data-ttu-id="f16b0-263">Introduzione all'integrità di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="f16b0-263">Service Fabric health introduction</span></span>](service-fabric-health-introduction.md)

[<span data-ttu-id="f16b0-264">Eseguire la diagnosi e la risoluzione dei problemi di un servizio di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="f16b0-264">Diagnose and troubleshoot a Service Fabric service</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[<span data-ttu-id="f16b0-265">Modellare un'applicazione in Service Fabric</span><span class="sxs-lookup"><span data-stu-id="f16b0-265">Model an application in Service Fabric</span></span>](service-fabric-application-model.md)

<!--Link references--In actual articles, you only need a single period before the slash-->
[10]: service-fabric-application-model.md
[11]: service-fabric-application-upgrade.md
