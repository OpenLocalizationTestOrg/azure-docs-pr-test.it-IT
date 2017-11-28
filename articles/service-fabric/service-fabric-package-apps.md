---
title: un'app di Azure Service Fabric aaaPackage | Documenti Microsoft
description: Come un'applicazione di Service Fabric prima di distribuire cluster tooa toopackage.
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
ms.openlocfilehash: b3918e1e25e532acdc9440855213e1fa364ea000
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="package-an-application"></a><span data-ttu-id="f6e78-103">Inserire un'applicazione in un pacchetto</span><span class="sxs-lookup"><span data-stu-id="f6e78-103">Package an application</span></span>
<span data-ttu-id="f6e78-104">Questo articolo viene descritto come un'applicazione di Service Fabric toopackage e renderlo pronto per la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="f6e78-104">This article describes how toopackage a Service Fabric application and make it ready for deployment.</span></span>

## <a name="package-layout"></a><span data-ttu-id="f6e78-105">Layout del pacchetto</span><span class="sxs-lookup"><span data-stu-id="f6e78-105">Package layout</span></span>
<span data-ttu-id="f6e78-106">manifesto dell'applicazione Hello, uno o più manifesti di servizio e di altri pacchetti necessari i file devono essere organizzati in un layout specifico per la distribuzione in un cluster di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="f6e78-106">hello application manifest, one or more service manifests, and other necessary package files must be organized in a specific layout for deployment into a Service Fabric cluster.</span></span> <span data-ttu-id="f6e78-107">manifesti di esempio Hello in questo articolo dovrebbe toobe organizzati in hello seguente struttura di directory:</span><span class="sxs-lookup"><span data-stu-id="f6e78-107">hello example manifests in this article would need toobe organized in hello following directory structure:</span></span>

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

<span data-ttu-id="f6e78-108">cartelle di Hello sono denominate hello toomatch **nome** gli attributi di ogni elemento corrispondente.</span><span class="sxs-lookup"><span data-stu-id="f6e78-108">hello folders are named toomatch hello **Name** attributes of each corresponding element.</span></span> <span data-ttu-id="f6e78-109">Ad esempio, se hello manifesto del servizio contiene due pacchetti di codice con i nomi di hello **MyCodeA** e **MyCodeB**, quindi due cartelle con nomi uguali a conterrebbe hello hello file binari necessari per ogni codice pacchetto.</span><span class="sxs-lookup"><span data-stu-id="f6e78-109">For example, if hello service manifest contained two code packages with hello names **MyCodeA** and **MyCodeB**, then two folders with hello same names would contain hello necessary binaries for each code package.</span></span>

## <a name="use-setupentrypoint"></a><span data-ttu-id="f6e78-110">Usare SetupEntryPoint</span><span class="sxs-lookup"><span data-stu-id="f6e78-110">Use SetupEntryPoint</span></span>
<span data-ttu-id="f6e78-111">Scenari tipici per l'utilizzo di **SetupEntryPoint** si verifica se è necessario un file eseguibile prima dell'avvio del servizio hello toorun oppure tooperform un'operazione con privilegi elevati.</span><span class="sxs-lookup"><span data-stu-id="f6e78-111">Typical scenarios for using **SetupEntryPoint** are when you need toorun an executable before hello service starts or you need tooperform an operation with elevated privileges.</span></span> <span data-ttu-id="f6e78-112">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="f6e78-112">For example:</span></span>

* <span data-ttu-id="f6e78-113">Impostazione e l'inizializzazione di variabili di ambiente hello esigenze eseguibile del servizio.</span><span class="sxs-lookup"><span data-stu-id="f6e78-113">Setting up and initializing environment variables that hello service executable needs.</span></span> <span data-ttu-id="f6e78-114">Non è limitato tooonly eseguibili scritti tramite modelli di programmazione di Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="f6e78-114">It is not limited tooonly executables written via hello Service Fabric programming models.</span></span> <span data-ttu-id="f6e78-115">Ad esempio, npm.exe richiede alcune variabili di ambiente configurate per la distribuzione di un'applicazione node.js.</span><span class="sxs-lookup"><span data-stu-id="f6e78-115">For example, npm.exe needs some environment variables configured for deploying a node.js application.</span></span>
* <span data-ttu-id="f6e78-116">Impostazione del controllo di accesso mediante l'installazione di certificati di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="f6e78-116">Setting up access control by installing security certificates.</span></span>

<span data-ttu-id="f6e78-117">Per ulteriori informazioni su come hello tooconfigure **SetupEntryPoint**, vedere [configurare criteri di hello per un punto di ingresso del programma di installazione del servizio](service-fabric-application-runas-security.md)</span><span class="sxs-lookup"><span data-stu-id="f6e78-117">For more information on how tooconfigure hello **SetupEntryPoint**, see [Configure hello policy for a service setup entry point](service-fabric-application-runas-security.md)</span></span>

<a id="Package-App"></a>
## <a name="configure"></a><span data-ttu-id="f6e78-118">Configurare</span><span class="sxs-lookup"><span data-stu-id="f6e78-118">Configure</span></span>
### <a name="build-a-package-by-using-visual-studio"></a><span data-ttu-id="f6e78-119">Creare un pacchetto mediante Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f6e78-119">Build a package by using Visual Studio</span></span>
<span data-ttu-id="f6e78-120">Se si utilizza Visual Studio 2015 toocreate l'applicazione, è possibile utilizzare hello pacchetto tooautomatically comando creare un pacchetto che corrisponde a layout hello descritto in precedenza.</span><span class="sxs-lookup"><span data-stu-id="f6e78-120">If you use Visual Studio 2015 toocreate your application, you can use hello Package command tooautomatically create a package that matches hello layout described above.</span></span>

<span data-ttu-id="f6e78-121">toocreate un pacchetto, fare clic sul progetto dell'applicazione hello in Esplora soluzioni e scegliere il comando di pacchetto hello, come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="f6e78-121">toocreate a package, right-click hello application project in Solution Explorer and choose hello Package command, as shown below:</span></span>

![Inserire un'applicazione in un pacchetto con Visual Studio][vs-package-command]

<span data-ttu-id="f6e78-123">Una volta completato pacchetti, è possibile trovare posizione hello del pacchetto di hello in hello **Output** finestra.</span><span class="sxs-lookup"><span data-stu-id="f6e78-123">When packaging is complete, you can find hello location of hello package in hello **Output** window.</span></span> <span data-ttu-id="f6e78-124">passaggio di creazione di pacchetti Hello avviene automaticamente quando si distribuisce o il debug dell'applicazione in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f6e78-124">hello packaging step occurs automatically when you deploy or debug your application in Visual Studio.</span></span>

### <a name="build-a-package-by-command-line"></a><span data-ttu-id="f6e78-125">Creare un pacchetto dalla riga di comando</span><span class="sxs-lookup"><span data-stu-id="f6e78-125">Build a package by command line</span></span>
<span data-ttu-id="f6e78-126">È inoltre possibile tooprogrammatically pacchetto di applicazione utilizzando `msbuild.exe`.</span><span class="sxs-lookup"><span data-stu-id="f6e78-126">It is also possible tooprogrammatically package up your application using `msbuild.exe`.</span></span> <span data-ttu-id="f6e78-127">Quinte hello, Visual Studio è in esecuzione, pertanto è lo stesso output di hello.</span><span class="sxs-lookup"><span data-stu-id="f6e78-127">Under hello hood, Visual Studio is running it so hello output is same.</span></span>

```shell
D:\Temp> msbuild HelloWorld.sfproj /t:Package
```

## <a name="test-hello-package"></a><span data-ttu-id="f6e78-128">Pacchetto di hello test</span><span class="sxs-lookup"><span data-stu-id="f6e78-128">Test hello package</span></span>
<span data-ttu-id="f6e78-129">È possibile verificare struttura del pacchetto hello in locale tramite PowerShell utilizzando hello [Test ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) comando.</span><span class="sxs-lookup"><span data-stu-id="f6e78-129">You can verify hello package structure locally through PowerShell by using hello [Test-ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) command.</span></span>
<span data-ttu-id="f6e78-130">Questo comando consente di verificare i problemi di analisi dei manifesti e tutti i riferimenti.</span><span class="sxs-lookup"><span data-stu-id="f6e78-130">This command checks for manifest parsing issues and verify all references.</span></span> <span data-ttu-id="f6e78-131">Questo comando si limita a verificare la correttezza strutturale hello di hello directory e file nel pacchetto hello.</span><span class="sxs-lookup"><span data-stu-id="f6e78-131">This command only verifies hello structural correctness of hello directories and files in hello package.</span></span>
<span data-ttu-id="f6e78-132">Non consente di verificare il contenuto di pacchetto di codice o dati hello oltre verifica che tutti i file necessari siano presenti.</span><span class="sxs-lookup"><span data-stu-id="f6e78-132">It doesn't verify any of hello code or data package contents beyond checking that all necessary files are present.</span></span>

```
PS D:\temp> Test-ServiceFabricApplicationPackage .\MyApplicationType
False
Test-ServiceFabricApplicationPackage : hello EntryPoint MySetup.bat is not found.
FileName: C:\Users\servicefabric\AppData\Local\Temp\TestApplicationPackage_7195781181\nrri205a.e2h\MyApplicationType\MyServiceManifest\ServiceManifest.xml
```

<span data-ttu-id="f6e78-133">Questo errore viene illustrato tale hello *MySetup.bat* file a cui fa riferimento nel manifesto del servizio hello **SetupEntryPoint** mancante dal pacchetto di codice hello.</span><span class="sxs-lookup"><span data-stu-id="f6e78-133">This error shows that hello *MySetup.bat* file referenced in hello service manifest **SetupEntryPoint** is missing from hello code package.</span></span> <span data-ttu-id="f6e78-134">Dopo l'aggiunta di file mancante hello, verifica dell'applicazione hello ha esito positivo:</span><span class="sxs-lookup"><span data-stu-id="f6e78-134">After hello missing file is added, hello application verification passes:</span></span>

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

<span data-ttu-id="f6e78-135">Se l'applicazione include [parametri applicazione](service-fabric-manage-multiple-environment-app-configuration.md) definiti, è possibile passarli in [Test-ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) per una convalida appropriata.</span><span class="sxs-lookup"><span data-stu-id="f6e78-135">If your application has [application parameters](service-fabric-manage-multiple-environment-app-configuration.md) defined, you can pass them in [Test-ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) for proper validation.</span></span>

<span data-ttu-id="f6e78-136">Se si conosce cluster hello in cui viene distribuita un'applicazione hello, è consigliabile passare nel hello `ImageStoreConnectionString` parametro.</span><span class="sxs-lookup"><span data-stu-id="f6e78-136">If you know hello cluster where hello application will be deployed, it is recommended you pass in hello `ImageStoreConnectionString` parameter.</span></span> <span data-ttu-id="f6e78-137">In questo caso, pacchetto hello viene convalidato anche in versioni precedenti di un'applicazione hello che sono già in esecuzione nel cluster hello.</span><span class="sxs-lookup"><span data-stu-id="f6e78-137">In this case, hello package is also validated against previous versions of hello application that are already running in hello cluster.</span></span> <span data-ttu-id="f6e78-138">Ad esempio, la convalida di hello può rilevare se un pacchetto con hello stessa versione ma contenuto diverso è già stato distribuito.</span><span class="sxs-lookup"><span data-stu-id="f6e78-138">For example, hello validation can detect whether a package with hello same version but different content was already deployed.</span></span>  

<span data-ttu-id="f6e78-139">Dopo che un'applicazione hello viene incluso nel pacchetto correttamente e passa la convalida, valutare in base alle dimensioni hello e numero hello di file se è necessaria la compressione.</span><span class="sxs-lookup"><span data-stu-id="f6e78-139">Once hello application is packaged correctly and passes validation, evaluate based on hello size and hello number of files if compression is needed.</span></span>

## <a name="compress-a-package"></a><span data-ttu-id="f6e78-140">Comprimere un pacchetto</span><span class="sxs-lookup"><span data-stu-id="f6e78-140">Compress a package</span></span>
<span data-ttu-id="f6e78-141">Quando un pacchetto è di grandi dimensioni o dispone di molti file, è possibile comprimerlo per velocizzare la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="f6e78-141">When a package is large or has many files, you can compress it for faster deployment.</span></span> <span data-ttu-id="f6e78-142">La compressione riduce il numero di hello di file e le dimensioni di pacchetto hello.</span><span class="sxs-lookup"><span data-stu-id="f6e78-142">Compression reduces hello number of files and hello package size.</span></span>
<span data-ttu-id="f6e78-143">Per un pacchetto di applicazione compresso, [pacchetto di applicazione di caricamento in corso hello](service-fabric-deploy-remove-applications.md#upload-the-application-package) potrebbe richiedere più confrontati toouploading hello compressi pacchetto (appositamente se il tempo di compressione è inserito), ma [registrazione](service-fabric-deploy-remove-applications.md#register-the-application-package) e [tipo l'annullamento della registrazione dell'applicazione hello](service-fabric-deploy-remove-applications.md#unregister-an-application-type) sono più veloci per un pacchetto di applicazione compresso.</span><span class="sxs-lookup"><span data-stu-id="f6e78-143">For a compressed application package, [Uploading hello application package](service-fabric-deploy-remove-applications.md#upload-the-application-package) may take longer compared toouploading hello uncompressed package (specially if compression time is factored in), but [registering](service-fabric-deploy-remove-applications.md#register-the-application-package) and [un-registering hello application type](service-fabric-deploy-remove-applications.md#unregister-an-application-type) are faster for a compressed application package.</span></span>

<span data-ttu-id="f6e78-144">il meccanismo di distribuzione Hello è lo stesso per i pacchetti compressi e non compressi.</span><span class="sxs-lookup"><span data-stu-id="f6e78-144">hello deployment mechanism is same for compressed and uncompressed packages.</span></span> <span data-ttu-id="f6e78-145">Se il pacchetto di hello è compresso, viene archiviata come tale nell'archivio di immagini cluster hello ed è non compressi in nodo hello prima di eseguita un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="f6e78-145">If hello package is compressed, it is stored as such in hello cluster image store and it's uncompressed on hello node before hello application is run.</span></span>
<span data-ttu-id="f6e78-146">la compressione di Hello sostituisce il pacchetto di Service Fabric valido hello con versione compressa hello.</span><span class="sxs-lookup"><span data-stu-id="f6e78-146">hello compression replaces hello valid Service Fabric package with hello compressed version.</span></span> <span data-ttu-id="f6e78-147">cartella Hello deve consentire le autorizzazioni di scrittura.</span><span class="sxs-lookup"><span data-stu-id="f6e78-147">hello folder must allow write permissions.</span></span> <span data-ttu-id="f6e78-148">La compressione di un pacchetto già compresso non apporta modifiche.</span><span class="sxs-lookup"><span data-stu-id="f6e78-148">Running compression on an already compressed package yields no changes.</span></span>

<span data-ttu-id="f6e78-149">È possibile comprimere un pacchetto eseguendo il comando di Powershell hello [copia ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) con `CompressPackage` passare.</span><span class="sxs-lookup"><span data-stu-id="f6e78-149">You can compress a package by running hello Powershell command [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) with `CompressPackage` switch.</span></span> <span data-ttu-id="f6e78-150">È possibile decomprimere hello del pacchetto con hello stesso comando, mediante `UncompressPackage` passare.</span><span class="sxs-lookup"><span data-stu-id="f6e78-150">You can uncompress hello package with hello same command, using `UncompressPackage` switch.</span></span>

<span data-ttu-id="f6e78-151">Hello comando seguente consente di comprimere pacchetto hello senza copiarlo toohello archivio di immagini.</span><span class="sxs-lookup"><span data-stu-id="f6e78-151">hello following command compresses hello package without copying it toohello image store.</span></span> <span data-ttu-id="f6e78-152">È possibile copiare un pacchetto compresso di tooone o più cluster di Service Fabric, in base alle esigenze, utilizzando [copia ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) senza hello `SkipCopy` flag.</span><span class="sxs-lookup"><span data-stu-id="f6e78-152">You can copy a compressed package tooone or more Service Fabric clusters, as needed, using [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) without hello `SkipCopy` flag.</span></span>
<span data-ttu-id="f6e78-153">pacchetto di Hello include ora i file ZIP per hello `code`, `config`, e `data` pacchetti.</span><span class="sxs-lookup"><span data-stu-id="f6e78-153">hello package now includes zipped files for hello `code`, `config`, and `data` packages.</span></span> <span data-ttu-id="f6e78-154">manifesto dell'applicazione Hello e hello servizio manifesti non compressi, perché sono necessari per molte operazioni interne (ad esempio la condivisione, l'applicazione nome e la versione estrazione del tipo per alcune convalide di pacchetto).</span><span class="sxs-lookup"><span data-stu-id="f6e78-154">hello application manifest and hello service manifests are not zipped, because they are needed for many internal operations (like package sharing, application type name and version extraction for certain validations).</span></span>
<span data-ttu-id="f6e78-155">Compressione manifesti hello renderebbe queste operazioni inefficienti.</span><span class="sxs-lookup"><span data-stu-id="f6e78-155">Zipping hello manifests would make these operations inefficient.</span></span>

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

<span data-ttu-id="f6e78-156">In alternativa, è possibile comprimere e copiare il pacchetto di hello con [copia ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) in un unico passaggio.</span><span class="sxs-lookup"><span data-stu-id="f6e78-156">Alternatively, you can compress and copy hello package with [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) in one step.</span></span>
<span data-ttu-id="f6e78-157">Se il pacchetto di hello è grande, fornire un tempo di tooallow sufficientemente elevato per la compressione di pacchetto hello e cluster toohello di caricamento hello.</span><span class="sxs-lookup"><span data-stu-id="f6e78-157">If hello package is large, provide a high enough timeout tooallow time for both hello package compression and hello upload toohello cluster.</span></span>
```
PS D:\temp> Copy-ServiceFabricApplicationPackage -ApplicationPackagePath .\MyApplicationType -ApplicationPackagePathInImageStore MyApplicationType -ImageStoreConnectionString fabric:ImageStore -CompressPackage -TimeoutSec 5400
```

<span data-ttu-id="f6e78-158">Internamente, Service Fabric calcola i valori di checksum per i pacchetti di applicazione hello per la convalida.</span><span class="sxs-lookup"><span data-stu-id="f6e78-158">Internally, Service Fabric computes checksums for hello application packages for validation.</span></span> <span data-ttu-id="f6e78-159">Quando si utilizza la compressione, hello checksum vengono calcolate in ogni pacchetto versioni compressa hello.</span><span class="sxs-lookup"><span data-stu-id="f6e78-159">When using compression, hello checksums are computed on hello zipped versions of each package.</span></span>
<span data-ttu-id="f6e78-160">Se è stata copiata una versione non compressa del pacchetto di applicazione e si desidera che la compressione toouse per hello stesso pacchetto, è necessario modificare le versioni di hello di hello `code`, `config`, e `data` mancata corrispondenza del checksum tooavoid pacchetti.</span><span class="sxs-lookup"><span data-stu-id="f6e78-160">If you copied an uncompressed version of your application package, and you want toouse compression for hello same package, you must change hello versions of hello `code`, `config`, and `data` packages tooavoid checksum mismatch.</span></span> <span data-ttu-id="f6e78-161">Se i pacchetti hello rimangono invariati, anziché la modifica di versione di hello, è possibile utilizzare [diff provisioning](service-fabric-application-upgrade-advanced.md).</span><span class="sxs-lookup"><span data-stu-id="f6e78-161">If hello packages are unchanged, instead of changing hello version, you can use [diff provisioning](service-fabric-application-upgrade-advanced.md).</span></span> <span data-ttu-id="f6e78-162">Con questa opzione, non includere pacchetto invariato di hello invece farvi riferimento dal manifesto del servizio hello.</span><span class="sxs-lookup"><span data-stu-id="f6e78-162">With this option, do not include hello unchanged package instead reference it from hello service manifest.</span></span>

<span data-ttu-id="f6e78-163">Analogamente, se è stata caricata una versione compressa del pacchetto di hello e si desidera toouse un pacchetto non compresso, è necessario aggiornare mancata corrispondenza del checksum hello versioni tooavoid hello.</span><span class="sxs-lookup"><span data-stu-id="f6e78-163">Similarly, if you uploaded a compressed version of hello package and you want toouse an uncompressed package, you must update hello versions tooavoid hello checksum mismatch.</span></span>

<span data-ttu-id="f6e78-164">Hello pacchetto è ora incluso nel pacchetto in modo corretto, convalidare e compressi (se necessario), in modo che sia pronto per [distribuzione](service-fabric-deploy-remove-applications.md) tooone o altre dell'infrastruttura del servizio cluster.</span><span class="sxs-lookup"><span data-stu-id="f6e78-164">hello package is now packaged correctly, validated, and compressed (if needed), so it is ready for [deployment](service-fabric-deploy-remove-applications.md) tooone or more Service Fabric clusters.</span></span>

### <a name="compress-packages-when-deploying-using-visual-studio"></a><span data-ttu-id="f6e78-165">Comprimere i pacchetti quando si distribuisce con Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f6e78-165">Compress packages when deploying using Visual Studio</span></span>
<span data-ttu-id="f6e78-166">È possibile indicare i pacchetti di Visual Studio toocompress nella distribuzione, aggiungendo hello `CopyPackageParameters` tooyour elemento profilo di pubblicazione e impostare hello `CompressPackage` attributo troppo`true`.</span><span class="sxs-lookup"><span data-stu-id="f6e78-166">You can instruct Visual Studio toocompress packages on deployment, by adding hello `CopyPackageParameters` element tooyour publish profile, and set hello `CompressPackage` attribute too`true`.</span></span>

``` xml
    <PublishProfile xmlns="http://schemas.microsoft.com/2015/05/fabrictools">
        <ClusterConnectionParameters ConnectionEndpoint="mycluster.westus.cloudapp.azure.com" />
        <ApplicationParameterFile Path="..\ApplicationParameters\Cloud.xml" />
        <CopyPackageParameters CompressPackage="true"/>
    </PublishProfile>
```

## <a name="next-steps"></a><span data-ttu-id="f6e78-167">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f6e78-167">Next steps</span></span>
<span data-ttu-id="f6e78-168">[Distribuire e rimuovere le applicazioni] [ 10] viene descritto come le istanze dell'applicazione toomanage toouse PowerShell</span><span class="sxs-lookup"><span data-stu-id="f6e78-168">[Deploy and remove applications][10] describes how toouse PowerShell toomanage application instances</span></span>

<span data-ttu-id="f6e78-169">[Gestione dei parametri dell'applicazione per più ambienti] [ 11] viene descritto come tooconfigure parametri e variabili di ambiente per le istanze dell'applicazione diverso.</span><span class="sxs-lookup"><span data-stu-id="f6e78-169">[Managing application parameters for multiple environments][11] describes how tooconfigure parameters and environment variables for different application instances.</span></span>

<span data-ttu-id="f6e78-170">[Configurare i criteri di sicurezza per l'applicazione] [ 12] viene descritto come toorun servizi con accesso toorestrict criteri di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="f6e78-170">[Configure security policies for your application][12] describes how toorun services under security policies toorestrict access.</span></span>

<!--Image references-->
[vs-package-command]: ./media/service-fabric-package-apps/vs-package-command.png

<!--Link references--In actual articles, you only need a single period before hello slash-->
[10]: service-fabric-deploy-remove-applications.md
[11]: service-fabric-manage-multiple-environment-app-configuration.md
[12]: service-fabric-application-runas-security.md
