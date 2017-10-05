---
title: Inserire un'applicazione Azure Service Fabric di Azure in un pacchetto | Microsoft Docs
description: Come inserire un'applicazione Service Fabric in un pacchetto prima della distribuzione in un cluster.
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: mani-ramaswamy
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: ryanwi
ms.openlocfilehash: 486a27d7ca576c8fe1552c02eb24ece6b8bb2ba8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="package-an-application"></a><span data-ttu-id="7af16-103">Inserire un'applicazione in un pacchetto</span><span class="sxs-lookup"><span data-stu-id="7af16-103">Package an application</span></span>
<span data-ttu-id="7af16-104">L'articolo descrive come inserire un'applicazione di Service Fabric in un pacchetto e prepararla per la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="7af16-104">This article describes how to package a Service Fabric application and make it ready for deployment.</span></span>

## <a name="package-layout"></a><span data-ttu-id="7af16-105">Layout del pacchetto</span><span class="sxs-lookup"><span data-stu-id="7af16-105">Package layout</span></span>
<span data-ttu-id="7af16-106">Il manifesto dell'applicazione, uno o più manifesti dei servizi e gli altri file del pacchetto necessari devono essere organizzati in un layout specifico per la distribuzione in un cluster di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="7af16-106">The application manifest, one or more service manifests, and other necessary package files must be organized in a specific layout for deployment into a Service Fabric cluster.</span></span> <span data-ttu-id="7af16-107">I manifesti di esempio di questo articolo dovrebbero essere organizzati nella struttura di directory seguente:</span><span class="sxs-lookup"><span data-stu-id="7af16-107">The example manifests in this article would need to be organized in the following directory structure:</span></span>

```
PS D:\temp> tree /f .\MyApplicationType

D:\TEMP\MYAPPLICATIONTYPE
│   ApplicationManifest.xml
│
└───MyServiceManifest
    │   ServiceManifest.xml
    │
    ├───MyCode
    │       MyServiceHost.exe
    │
    ├───MyConfig
    │       Settings.xml
    │
    └───MyData
            init.dat
```

<span data-ttu-id="7af16-108">Le cartelle sono denominate in modo da corrispondere agli attributi **Name** di ogni elemento corrispondente.</span><span class="sxs-lookup"><span data-stu-id="7af16-108">The folders are named to match the **Name** attributes of each corresponding element.</span></span> <span data-ttu-id="7af16-109">Se ad esempio il manifesto del servizio contenesse due pacchetti di codice denominati **MyCodeA** e **MyCodeB**, dovrebbero esistere due cartelle con gli stessi nomi contenenti i file binari necessari per ogni pacchetto di codice.</span><span class="sxs-lookup"><span data-stu-id="7af16-109">For example, if the service manifest contained two code packages with the names **MyCodeA** and **MyCodeB**, then two folders with the same names would contain the necessary binaries for each code package.</span></span>

## <a name="use-setupentrypoint"></a><span data-ttu-id="7af16-110">Usare SetupEntryPoint</span><span class="sxs-lookup"><span data-stu-id="7af16-110">Use SetupEntryPoint</span></span>
<span data-ttu-id="7af16-111">Gli scenari tipici per l'utilizzo di **SetupEntryPoint** sono quando è necessario eseguire un file eseguibile prima dell'avvio del servizio o quando è necessario eseguire un'operazione con privilegi elevati.</span><span class="sxs-lookup"><span data-stu-id="7af16-111">Typical scenarios for using **SetupEntryPoint** are when you need to run an executable before the service starts or you need to perform an operation with elevated privileges.</span></span> <span data-ttu-id="7af16-112">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="7af16-112">For example:</span></span>

* <span data-ttu-id="7af16-113">Impostazione e inizializzazione di variabili di ambiente necessari per il file eseguibile del servizio.</span><span class="sxs-lookup"><span data-stu-id="7af16-113">Setting up and initializing environment variables that the service executable needs.</span></span> <span data-ttu-id="7af16-114">Questo non è limitato solo agli eseguibili scritti tramite i modelli di programmazione di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="7af16-114">It is not limited to only executables written via the Service Fabric programming models.</span></span> <span data-ttu-id="7af16-115">Ad esempio, npm.exe richiede alcune variabili di ambiente configurate per la distribuzione di un'applicazione node.js.</span><span class="sxs-lookup"><span data-stu-id="7af16-115">For example, npm.exe needs some environment variables configured for deploying a node.js application.</span></span>
* <span data-ttu-id="7af16-116">Impostazione del controllo di accesso mediante l'installazione di certificati di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="7af16-116">Setting up access control by installing security certificates.</span></span>

<span data-ttu-id="7af16-117">Per altre informazioni su come configurare **SetupEntryPoint**, vedere [Configurare i criteri per il punto di ingresso dell'installazione del servizio](service-fabric-application-runas-security.md)</span><span class="sxs-lookup"><span data-stu-id="7af16-117">For more information on how to configure the **SetupEntryPoint**, see [Configure the policy for a service setup entry point](service-fabric-application-runas-security.md)</span></span>

<a id="Package-App"></a>
## <a name="configure"></a><span data-ttu-id="7af16-118">Configurare</span><span class="sxs-lookup"><span data-stu-id="7af16-118">Configure</span></span>
### <a name="build-a-package-by-using-visual-studio"></a><span data-ttu-id="7af16-119">Creare un pacchetto mediante Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7af16-119">Build a package by using Visual Studio</span></span>
<span data-ttu-id="7af16-120">Se si usa Visual Studio 2015 per creare un'applicazione, è possibile usare il comando Pacchetto per creare automaticamente un pacchetto corrispondente al layout descritto precedentemente.</span><span class="sxs-lookup"><span data-stu-id="7af16-120">If you use Visual Studio 2015 to create your application, you can use the Package command to automatically create a package that matches the layout described above.</span></span>

<span data-ttu-id="7af16-121">Per creare un pacchetto, fare clic con il pulsante destro sul progetto dell'applicazione in Esplora soluzioni e scegliere il comando Pacchetto, come mostrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="7af16-121">To create a package, right-click the application project in Solution Explorer and choose the Package command, as shown below:</span></span>

![Inserire un'applicazione in un pacchetto con Visual Studio][vs-package-command]

<span data-ttu-id="7af16-123">Dopo avere completato la creazione del pacchetto, è possibile vedere la posizione del pacchetto nella finestra **Output** .</span><span class="sxs-lookup"><span data-stu-id="7af16-123">When packaging is complete, you can find the location of the package in the **Output** window.</span></span> <span data-ttu-id="7af16-124">Il passaggio di creazione del pacchetto viene eseguito automaticamente con la distribuzione o il debug di un'applicazione in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7af16-124">The packaging step occurs automatically when you deploy or debug your application in Visual Studio.</span></span>

### <a name="build-a-package-by-command-line"></a><span data-ttu-id="7af16-125">Creare un pacchetto dalla riga di comando</span><span class="sxs-lookup"><span data-stu-id="7af16-125">Build a package by command line</span></span>
<span data-ttu-id="7af16-126">È anche possibile creare un pacchetto dell'applicazione a livello di codice usando `msbuild.exe`.</span><span class="sxs-lookup"><span data-stu-id="7af16-126">It is also possible to programmatically package up your application using `msbuild.exe`.</span></span> <span data-ttu-id="7af16-127">Tale operazione viene eseguita da Visual Studio e quindi l'output è lo stesso.</span><span class="sxs-lookup"><span data-stu-id="7af16-127">Under the hood, Visual Studio is running it so the output is same.</span></span>

```shell
D:\Temp> msbuild HelloWorld.sfproj /t:Package
```

## <a name="test-the-package"></a><span data-ttu-id="7af16-128">Testare il pacchetto</span><span class="sxs-lookup"><span data-stu-id="7af16-128">Test the package</span></span>
<span data-ttu-id="7af16-129">È possibile verificare la struttura del pacchetto in modalità locale tramite PowerShell usando il comando [Test-ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) .</span><span class="sxs-lookup"><span data-stu-id="7af16-129">You can verify the package structure locally through PowerShell by using the [Test-ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) command.</span></span>
<span data-ttu-id="7af16-130">Questo comando consente di verificare i problemi di analisi dei manifesti e tutti i riferimenti.</span><span class="sxs-lookup"><span data-stu-id="7af16-130">This command checks for manifest parsing issues and verify all references.</span></span> <span data-ttu-id="7af16-131">Questo comando si limita a verificare la correttezza strutturale delle directory e i file nel pacchetto.</span><span class="sxs-lookup"><span data-stu-id="7af16-131">This command only verifies the structural correctness of the directories and files in the package.</span></span>
<span data-ttu-id="7af16-132">Non verifica il codice o i contenuti del pacchetto di dati oltre a controllare che tutti i file necessari siano presenti.</span><span class="sxs-lookup"><span data-stu-id="7af16-132">It doesn't verify any of the code or data package contents beyond checking that all necessary files are present.</span></span>

```
PS D:\temp> Test-ServiceFabricApplicationPackage .\MyApplicationType
False
Test-ServiceFabricApplicationPackage : The EntryPoint MySetup.bat is not found.
FileName: C:\Users\servicefabric\AppData\Local\Temp\TestApplicationPackage_7195781181\nrri205a.e2h\MyApplicationType\MyServiceManifest\ServiceManifest.xml
```

<span data-ttu-id="7af16-133">Questo errore indica che il file *MySetup.bat* a cui viene fatto riferimento nel manifesto del servizio **SetupEntryPoint** manca nel pacchetto di codice.</span><span class="sxs-lookup"><span data-stu-id="7af16-133">This error shows that the *MySetup.bat* file referenced in the service manifest **SetupEntryPoint** is missing from the code package.</span></span> <span data-ttu-id="7af16-134">Dopo aver aggiunto il file mancante, la verifica dell'applicazione ha esito positivo:</span><span class="sxs-lookup"><span data-stu-id="7af16-134">After the missing file is added, the application verification passes:</span></span>

```
PS D:\temp> tree /f .\MyApplicationType

D:\TEMP\MYAPPLICATIONTYPE
│   ApplicationManifest.xml
│
└───MyServiceManifest
    │   ServiceManifest.xml
    │
    ├───MyCode
    │       MyServiceHost.exe
    │       MySetup.bat
    │
    ├───MyConfig
    │       Settings.xml
    │
    └───MyData
            init.dat

PS D:\temp> Test-ServiceFabricApplicationPackage .\MyApplicationType
True
PS D:\temp>
```

<span data-ttu-id="7af16-135">Se l'applicazione include [parametri applicazione](service-fabric-manage-multiple-environment-app-configuration.md) definiti, è possibile passarli in [Test-ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) per una convalida appropriata.</span><span class="sxs-lookup"><span data-stu-id="7af16-135">If your application has [application parameters](service-fabric-manage-multiple-environment-app-configuration.md) defined, you can pass them in [Test-ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) for proper validation.</span></span>

<span data-ttu-id="7af16-136">Se si conosce il cluster in cui verrà distribuita l'applicazione, si consiglia di passarlo nel parametro `ImageStoreConnectionString`.</span><span class="sxs-lookup"><span data-stu-id="7af16-136">If you know the cluster where the application will be deployed, it is recommended you pass in the `ImageStoreConnectionString` parameter.</span></span> <span data-ttu-id="7af16-137">In questo caso, il pacchetto viene convalidato rispetto alle versioni precedenti dell'applicazione già in esecuzione nel cluster.</span><span class="sxs-lookup"><span data-stu-id="7af16-137">In this case, the package is also validated against previous versions of the application that are already running in the cluster.</span></span> <span data-ttu-id="7af16-138">Ad esempio, la convalida può rilevare se sia già stato distribuito un pacchetto con la stessa versione ma con contenuti differenti.</span><span class="sxs-lookup"><span data-stu-id="7af16-138">For example, the validation can detect whether a package with the same version but different content was already deployed.</span></span>  

<span data-ttu-id="7af16-139">Una volta che l'applicazione viene inserita correttamente in un pacchetto e passa la convalida, valutare se sia necessaria la compressione in base alle dimensioni e al numero dei file.</span><span class="sxs-lookup"><span data-stu-id="7af16-139">Once the application is packaged correctly and passes validation, evaluate based on the size and the number of files if compression is needed.</span></span>

## <a name="compress-a-package"></a><span data-ttu-id="7af16-140">Comprimere un pacchetto</span><span class="sxs-lookup"><span data-stu-id="7af16-140">Compress a package</span></span>
<span data-ttu-id="7af16-141">Quando un pacchetto è di grandi dimensioni o dispone di molti file, è possibile comprimerlo per velocizzare la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="7af16-141">When a package is large or has many files, you can compress it for faster deployment.</span></span> <span data-ttu-id="7af16-142">La compressione riduce il numero di file e le dimensioni del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="7af16-142">Compression reduces the number of files and the package size.</span></span>
<span data-ttu-id="7af16-143">Per un pacchetto dell'applicazione compresso, l'operazione di [caricamento](service-fabric-deploy-remove-applications.md#upload-the-application-package) potrebbe richiedere più tempo rispetto al caricamento del pacchetto non compresso, in particolare se è stato eseguito il factoring del tempo di compressione. Tuttavia, le operazioni di [registrazione](service-fabric-deploy-remove-applications.md#register-the-application-package) e [annullamento della registrazione del tipo di applicazione](service-fabric-deploy-remove-applications.md#unregister-an-application-type) sono più veloci per un pacchetto dell'applicazione compresso.</span><span class="sxs-lookup"><span data-stu-id="7af16-143">For a compressed application package, [Uploading the application package](service-fabric-deploy-remove-applications.md#upload-the-application-package) may take longer compared to uploading the uncompressed package (specially if compression time is factored in), but [registering](service-fabric-deploy-remove-applications.md#register-the-application-package) and [un-registering the application type](service-fabric-deploy-remove-applications.md#unregister-an-application-type) are faster for a compressed application package.</span></span>

<span data-ttu-id="7af16-144">Il meccanismo di distribuzione è lo stesso per i pacchetti compressi e per quelli non compressi.</span><span class="sxs-lookup"><span data-stu-id="7af16-144">The deployment mechanism is same for compressed and uncompressed packages.</span></span> <span data-ttu-id="7af16-145">Se il pacchetto è compresso, viene archiviato come tale nell'archivio immagini del cluster e viene decompresso nel nodo prima dell'esecuzione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="7af16-145">If the package is compressed, it is stored as such in the cluster image store and it's uncompressed on the node before the application is run.</span></span>
<span data-ttu-id="7af16-146">La compressione sostituisce il pacchetto di Service Fabric valido con la versione compressa.</span><span class="sxs-lookup"><span data-stu-id="7af16-146">The compression replaces the valid Service Fabric package with the compressed version.</span></span> <span data-ttu-id="7af16-147">La cartella deve fornire le autorizzazioni di scrittura.</span><span class="sxs-lookup"><span data-stu-id="7af16-147">The folder must allow write permissions.</span></span> <span data-ttu-id="7af16-148">La compressione di un pacchetto già compresso non apporta modifiche.</span><span class="sxs-lookup"><span data-stu-id="7af16-148">Running compression on an already compressed package yields no changes.</span></span>

<span data-ttu-id="7af16-149">È possibile comprimere un pacchetto eseguendo il comando [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) con lo switch `CompressPackage`.</span><span class="sxs-lookup"><span data-stu-id="7af16-149">You can compress a package by running the Powershell command [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) with `CompressPackage` switch.</span></span> <span data-ttu-id="7af16-150">È possibile decomprimere il pacchetto con lo stesso comando, usando lo switch `UncompressPackage`.</span><span class="sxs-lookup"><span data-stu-id="7af16-150">You can uncompress the package with the same command, using `UncompressPackage` switch.</span></span>

<span data-ttu-id="7af16-151">Il comando seguente comprime il pacchetto senza copiarlo nell'archivio immagini.</span><span class="sxs-lookup"><span data-stu-id="7af16-151">The following command compresses the package without copying it to the image store.</span></span> <span data-ttu-id="7af16-152">È possibile copiare un pacchetto compresso in uno o più cluster Service Fabric, in base alle esigenze, us il comando [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) senza il flag `SkipCopy`.</span><span class="sxs-lookup"><span data-stu-id="7af16-152">You can copy a compressed package to one or more Service Fabric clusters, as needed, using [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) without the `SkipCopy` flag.</span></span>
<span data-ttu-id="7af16-153">Ora il pacchetto include i file compressi per i pacchetti `code`, `config` e `data`.</span><span class="sxs-lookup"><span data-stu-id="7af16-153">The package now includes zipped files for the `code`, `config`, and `data` packages.</span></span> <span data-ttu-id="7af16-154">Il manifesto dell'applicazione e i manifesti del servizio non sono compressi in quanto necessari per numerose operazioni interne, come la condivisione dei pacchetti e l'estrazione del nome e della versione del tipo di applicazione per determinate convalide.</span><span class="sxs-lookup"><span data-stu-id="7af16-154">The application manifest and the service manifests are not zipped, because they are needed for many internal operations (like package sharing, application type name and version extraction for certain validations).</span></span>
<span data-ttu-id="7af16-155">La compressione dei manifesti renderebbe inefficienti tali operazioni.</span><span class="sxs-lookup"><span data-stu-id="7af16-155">Zipping the manifests would make these operations inefficient.</span></span>

```
PS D:\temp> tree /f .\MyApplicationType

D:\TEMP\MYAPPLICATIONTYPE
│   ApplicationManifest.xml
│
└───MyServiceManifest
    │   ServiceManifest.xml
    │
    ├───MyCode
    │       MyServiceHost.exe
    │       MySetup.bat
    │
    ├───MyConfig
    │       Settings.xml
    │
    └───MyData
            init.dat
PS D:\temp> Copy-ServiceFabricApplicationPackage -ApplicationPackagePath .\MyApplicationType -CompressPackage -SkipCopy

PS D:\temp> tree /f .\MyApplicationType

D:\TEMP\MYAPPLICATIONTYPE
│   ApplicationManifest.xml
│
└───MyServiceManifest
       ServiceManifest.xml
       MyCode.zip
       MyConfig.zip
       MyData.zip

```

<span data-ttu-id="7af16-156">In alternativa è possibile comprimere e copiare il pacchetto con [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) in un unico passaggio.</span><span class="sxs-lookup"><span data-stu-id="7af16-156">Alternatively, you can compress and copy the package with [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) in one step.</span></span>
<span data-ttu-id="7af16-157">Se il pacchetto è grande, specificare un timeout sufficiente per consentire la compressione del pacchetto e il caricamento nel cluster.</span><span class="sxs-lookup"><span data-stu-id="7af16-157">If the package is large, provide a high enough timeout to allow time for both the package compression and the upload to the cluster.</span></span>
```
PS D:\temp> Copy-ServiceFabricApplicationPackage -ApplicationPackagePath .\MyApplicationType -ApplicationPackagePathInImageStore MyApplicationType -ImageStoreConnectionString fabric:ImageStore -CompressPackage -TimeoutSec 5400
```

<span data-ttu-id="7af16-158">Internamente, Service Fabric calcola i checksum per la convalida dei pacchetti dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="7af16-158">Internally, Service Fabric computes checksums for the application packages for validation.</span></span> <span data-ttu-id="7af16-159">Quando si usa la compressione, i checksum vengono calcolati nelle versioni compresse di ciascun pacchetto.</span><span class="sxs-lookup"><span data-stu-id="7af16-159">When using compression, the checksums are computed on the zipped versions of each package.</span></span>
<span data-ttu-id="7af16-160">Se è stata copiata una versione non compressa del pacchetto dell'applicazione e si desidera usare la compressione per il medesimo pacchetto, è necessario modificare la versione dei pacchetti `code`, `config` e `data` per evitare la mancata corrispondenza del checksum.</span><span class="sxs-lookup"><span data-stu-id="7af16-160">If you copied an uncompressed version of your application package, and you want to use compression for the same package, you must change the versions of the `code`, `config`, and `data` packages to avoid checksum mismatch.</span></span> <span data-ttu-id="7af16-161">Se i pacchetti rimangono invariati, anziché cambiare la versione, è possibile usare [diff provisioning](service-fabric-application-upgrade-advanced.md).</span><span class="sxs-lookup"><span data-stu-id="7af16-161">If the packages are unchanged, instead of changing the version, you can use [diff provisioning](service-fabric-application-upgrade-advanced.md).</span></span> <span data-ttu-id="7af16-162">Con questa opzione non si include il pacchetto invariato ma si fa solo riferimento a esso dal manifesto del servizio.</span><span class="sxs-lookup"><span data-stu-id="7af16-162">With this option, do not include the unchanged package instead reference it from the service manifest.</span></span>

<span data-ttu-id="7af16-163">Analogamente, se è stata caricata una versione compressa del pacchetto e si vuole usare un pacchetto non compresso, è necessario aggiornare la versione per evitare la mancata corrispondenza del checksum.</span><span class="sxs-lookup"><span data-stu-id="7af16-163">Similarly, if you uploaded a compressed version of the package and you want to use an uncompressed package, you must update the versions to avoid the checksum mismatch.</span></span>

<span data-ttu-id="7af16-164">Il pacchetto è ora corretto, convalidato e compresso (se necessario). Pertanto, è pronto per la [distribuzione](service-fabric-deploy-remove-applications.md) in uno o più cluster di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="7af16-164">The package is now packaged correctly, validated, and compressed (if needed), so it is ready for [deployment](service-fabric-deploy-remove-applications.md) to one or more Service Fabric clusters.</span></span>

### <a name="compress-packages-when-deploying-using-visual-studio"></a><span data-ttu-id="7af16-165">Comprimere i pacchetti quando si distribuisce con Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7af16-165">Compress packages when deploying using Visual Studio</span></span>
<span data-ttu-id="7af16-166">È possibile indicare a Visual Studio di comprimere i pacchetti in fase di distribuzione, aggiungendo l'elemento `CopyPackageParameters` al profilo di pubblicazione, e di impostare l'attributo `CompressPackage` su `true`.</span><span class="sxs-lookup"><span data-stu-id="7af16-166">You can instruct Visual Studio to compress packages on deployment, by adding the `CopyPackageParameters` element to your publish profile, and set the `CompressPackage` attribute to `true`.</span></span>

``` xml
    <PublishProfile xmlns="http://schemas.microsoft.com/2015/05/fabrictools">
        <ClusterConnectionParameters ConnectionEndpoint="mycluster.westus.cloudapp.azure.com" />
        <ApplicationParameterFile Path="..\ApplicationParameters\Cloud.xml" />
        <CopyPackageParameters CompressPackage="true"/>
    </PublishProfile>
```

## <a name="next-steps"></a><span data-ttu-id="7af16-167">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7af16-167">Next steps</span></span>
<span data-ttu-id="7af16-168">[Distribuire e rimuovere applicazioni con PowerShell][10]: descrive come usare PowerShell per gestire le istanze dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="7af16-168">[Deploy and remove applications][10] describes how to use PowerShell to manage application instances</span></span>

<span data-ttu-id="7af16-169">[Gestire i parametri dell'applicazione per più ambienti][11]: descrive come configurare parametri e variabili di ambiente per istanze di applicazione diverse.</span><span class="sxs-lookup"><span data-stu-id="7af16-169">[Managing application parameters for multiple environments][11] describes how to configure parameters and environment variables for different application instances.</span></span>

<span data-ttu-id="7af16-170">[Configurare i criteri di sicurezza per l'applicazione][12]: descrive come eseguire i servizi nell'ambito dei criteri di sicurezza per limitare l'accesso.</span><span class="sxs-lookup"><span data-stu-id="7af16-170">[Configure security policies for your application][12] describes how to run services under security policies to restrict access.</span></span>

<!--Image references-->
[vs-package-command]: ./media/service-fabric-package-apps/vs-package-command.png

<!--Link references--In actual articles, you only need a single period before the slash-->
[10]: service-fabric-deploy-remove-applications.md
[11]: service-fabric-manage-multiple-environment-app-configuration.md
[12]: service-fabric-application-runas-security.md
