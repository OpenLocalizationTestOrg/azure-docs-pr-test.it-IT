---
title: un'applicazione Node.js che usa MongoDB aaaDeploy | Documenti Microsoft
description: "Procedura dettagliata sulla toopackage cluster più guest eseguibili toodeploy tooan Azure Service Fabric"
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: b76bb756-c1ba-49f9-9666-e9807cf8f92f
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/02/2017
ms.author: msfussell;mikhegn
ms.openlocfilehash: 2775080f0d9d42d6ba15cca911e23067106be26d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-multiple-guest-executables"></a><span data-ttu-id="83992-103">Distribuire più eseguibili guest</span><span class="sxs-lookup"><span data-stu-id="83992-103">Deploy multiple guest executables</span></span>
<span data-ttu-id="83992-104">Questo articolo viene illustrato come toopackage e distribuire più guest eseguibili tooAzure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="83992-104">This article shows how toopackage and deploy multiple guest executables tooAzure Service Fabric.</span></span> <span data-ttu-id="83992-105">Compilazione e distribuzione di un singolo pacchetto di Service Fabric leggere come troppo[distribuire un tooService eseguibile guest infrastruttura](service-fabric-deploy-existing-app.md).</span><span class="sxs-lookup"><span data-stu-id="83992-105">For building and deploying a single Service Fabric package read how too[deploy a guest executable tooService Fabric](service-fabric-deploy-existing-app.md).</span></span>

<span data-ttu-id="83992-106">Durante questa procedura dettagliata illustra come un'applicazione con un front-end Node.js che usa MongoDB come archivio dati hello toodeploy, è possibile applicare hello passaggi tooany le applicazioni con dipendenze da un'altra applicazione.</span><span class="sxs-lookup"><span data-stu-id="83992-106">While this walkthrough shows how toodeploy an application with a Node.js front end that uses MongoDB as hello data store, you can apply hello steps tooany application that has dependencies on another application.</span></span>   

<span data-ttu-id="83992-107">È possibile utilizzare Visual Studio tooproduce hello pacchetto di applicazione contiene più file eseguibili di guest.</span><span class="sxs-lookup"><span data-stu-id="83992-107">You can use Visual Studio tooproduce hello application package that contains multiple guest executables.</span></span> <span data-ttu-id="83992-108">Vedere [toopackage tramite Visual Studio un'applicazione esistente](service-fabric-deploy-existing-app.md).</span><span class="sxs-lookup"><span data-stu-id="83992-108">See [Using Visual Studio toopackage an existing application](service-fabric-deploy-existing-app.md).</span></span> <span data-ttu-id="83992-109">Dopo aver aggiunto eseguibile guest prima hello, fare clic sul progetto di applicazione hello e seleziona hello **Aggiungi -> servizio nuova Service Fabric** tooadd hello secondo guest eseguibile toohello soluzione del progetto.</span><span class="sxs-lookup"><span data-stu-id="83992-109">After you have added hello first guest executable, right click on hello application project and select hello **Add->New Service Fabric service** tooadd hello second guest executable project toohello solution.</span></span> <span data-ttu-id="83992-110">Nota: Se si sceglie l'origine di hello toolink nel progetto di Visual Studio, hello soluzione Visual Studio, hello garantisce che il pacchetto dell'applicazione è toodate con le modifiche nell'origine hello.</span><span class="sxs-lookup"><span data-stu-id="83992-110">Note: If you choose toolink hello source in hello Visual Studio project, building hello Visual Studio solution, will make sure that your application package is up toodate with changes in hello source.</span></span> 

## <a name="samples"></a><span data-ttu-id="83992-111">Esempi</span><span class="sxs-lookup"><span data-stu-id="83992-111">Samples</span></span>
* [<span data-ttu-id="83992-112">Esempio per la creazione di un pacchetto e distribuzione di un file guest eseguibile</span><span class="sxs-lookup"><span data-stu-id="83992-112">Sample for packaging and deploying a guest executable</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [<span data-ttu-id="83992-113">Esempio di guest due file eseguibili (c# e nodejs) comunicano tramite il servizio di denominazione hello tramite REST</span><span class="sxs-lookup"><span data-stu-id="83992-113">Sample of two guest executables (C# and nodejs) communicating via hello Naming service using REST</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-containers)

## <a name="manually-package-hello-multiple-guest-executable-application"></a><span data-ttu-id="83992-114">Manualmente i pacchetti hello applicazione eseguibile guest multiple</span><span class="sxs-lookup"><span data-stu-id="83992-114">Manually package hello multiple guest executable application</span></span>
<span data-ttu-id="83992-115">In alternativa è possibile creare manualmente un pacchetto guest hello eseguibile.</span><span class="sxs-lookup"><span data-stu-id="83992-115">Alternatively you can manually package hello guest executable.</span></span> <span data-ttu-id="83992-116">Per la creazione del pacchetto manuale hello, in questo articolo Usa strumento di creazione di pacchetti di hello Service Fabric, è disponibile all'indirizzo [http://aka.ms/servicefabricpacktool](http://aka.ms/servicefabricpacktool).</span><span class="sxs-lookup"><span data-stu-id="83992-116">For hello manual packaging, this article uses hello Service Fabric packaging tool, which is available at [http://aka.ms/servicefabricpacktool](http://aka.ms/servicefabricpacktool).</span></span>

### <a name="packaging-hello-nodejs-application"></a><span data-ttu-id="83992-117">Hello pacchetti applicazione Node.js</span><span class="sxs-lookup"><span data-stu-id="83992-117">Packaging hello Node.js application</span></span>
<span data-ttu-id="83992-118">Questo articolo si presuppone che non è installato Node.js sui nodi nel cluster di Service Fabric hello hello.</span><span class="sxs-lookup"><span data-stu-id="83992-118">This article assumes that Node.js is not installed on hello nodes in hello Service Fabric cluster.</span></span> <span data-ttu-id="83992-119">Di conseguenza, è necessario tooadd Node.exe toohello radice dell'applicazione nodo prima della creazione del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="83992-119">As a consequence, you need tooadd Node.exe toohello root directory of your node application before packaging.</span></span> <span data-ttu-id="83992-120">struttura di directory Hello di un'applicazione hello Node.js (tramite un framework web Express e motore del modello Jade) dovrebbe essere simile toohello uno di seguito:</span><span class="sxs-lookup"><span data-stu-id="83992-120">hello directory structure of hello Node.js application (using Express web framework and Jade template engine) should look similar toohello one below:</span></span>

```
|-- NodeApplication
    |-- bin
        |-- www
    |-- node_modules
        |-- .bin
        |-- express
        |-- jade
        |-- etc.
    |-- public
        |-- images
        |-- etc.
    |-- routes
        |-- index.js
        |-- users.js
    |-- views
        |-- index.jade
        |-- etc.
    |-- app.js
    |-- package.json
    |-- node.exe
```

<span data-ttu-id="83992-121">Come passaggio successivo, si crea un pacchetto di applicazione per hello applicazione Node.js.</span><span class="sxs-lookup"><span data-stu-id="83992-121">As a next step, you create an application package for hello Node.js application.</span></span> <span data-ttu-id="83992-122">codice Hello seguente crea un pacchetto di applicazione di Service Fabric che contiene un'applicazione hello Node.js.</span><span class="sxs-lookup"><span data-stu-id="83992-122">hello code below creates a Service Fabric application package that contains hello Node.js application.</span></span>

```
.\ServiceFabricAppPackageUtil.exe /source:'[yourdirectory]\MyNodeApplication' /target:'[yourtargetdirectory] /appname:NodeService /exe:'node.exe' /ma:'bin/www' /AppType:NodeAppType
```

<span data-ttu-id="83992-123">Di seguito è riportata una descrizione dei parametri di hello in uso:</span><span class="sxs-lookup"><span data-stu-id="83992-123">Below is a description of hello parameters that are being used:</span></span>

* <span data-ttu-id="83992-124">**/Source** punti toohello directory dell'applicazione hello che deve essere incluso nel pacchetto.</span><span class="sxs-lookup"><span data-stu-id="83992-124">**/source** points toohello directory of hello application that should be packaged.</span></span>
* <span data-ttu-id="83992-125">**/target** definisce hello directory nella quale hello pacchetto deve essere creato.</span><span class="sxs-lookup"><span data-stu-id="83992-125">**/target** defines hello directory in which hello package should be created.</span></span> <span data-ttu-id="83992-126">La directory ha toobe diversa dalla directory di origine hello.</span><span class="sxs-lookup"><span data-stu-id="83992-126">This directory has toobe different from hello source directory.</span></span>
* <span data-ttu-id="83992-127">**/appname** definisce il nome dell'applicazione hello di un'applicazione hello esistente.</span><span class="sxs-lookup"><span data-stu-id="83992-127">**/appname** defines hello application name of hello existing application.</span></span> <span data-ttu-id="83992-128">È importante toounderstand che questo si traduce il nome del servizio toohello nel manifesto hello e non nome dell'applicazione Service Fabric toohello.</span><span class="sxs-lookup"><span data-stu-id="83992-128">It's important toounderstand that this translates toohello service name in hello manifest, and not toohello Service Fabric application name.</span></span>
* <span data-ttu-id="83992-129">**/exe** definisce hello eseguibile che Service Fabric dovrebbe toolaunch, in questo caso `node.exe`.</span><span class="sxs-lookup"><span data-stu-id="83992-129">**/exe** defines hello executable that Service Fabric is supposed toolaunch, in this case `node.exe`.</span></span>
* <span data-ttu-id="83992-130">**/ma** definisce hello argomento che viene utilizzato toolaunch hello eseguibile.</span><span class="sxs-lookup"><span data-stu-id="83992-130">**/ma** defines hello argument that is being used toolaunch hello executable.</span></span> <span data-ttu-id="83992-131">Node.js non è installato, Service Fabric deve server web Node.js di hello toolaunch eseguendo `node.exe bin/www`.</span><span class="sxs-lookup"><span data-stu-id="83992-131">As Node.js is not installed, Service Fabric needs toolaunch hello Node.js web server by executing `node.exe bin/www`.</span></span>  <span data-ttu-id="83992-132">`/ma:'bin/www'`indica toouse strumento di creazione di pacchetti hello `bin/ma` come argomento di hello per node.exe.</span><span class="sxs-lookup"><span data-stu-id="83992-132">`/ma:'bin/www'` tells hello packaging tool toouse `bin/ma` as hello argument for node.exe.</span></span>
* <span data-ttu-id="83992-133">**/ AppType** definisce nome tipo dell'applicazione di Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="83992-133">**/AppType** defines hello Service Fabric application type name.</span></span>

<span data-ttu-id="83992-134">Se si seleziona una directory specificata nel parametro /target hello toohello, è possibile visualizzare che tale strumento hello è creato un pacchetto di Service Fabric completamente funziona, come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="83992-134">If you browse toohello directory that was specified in hello /target parameter, you can see that hello tool has created a fully functioning Service Fabric package as shown below:</span></span>

```
|--[yourtargetdirectory]
    |-- NodeApplication
        |-- C
              |-- bin
              |-- data
              |-- node_modules
              |-- public
              |-- routes
              |-- views
              |-- app.js
              |-- package.json
              |-- node.exe
        |-- config
              |--Settings.xml
        |-- ServiceManifest.xml
    |-- ApplicationManifest.xml
```
<span data-ttu-id="83992-135">Hello ServiceManifest.xml generato include ora una sezione che descrive come server web Node.js di hello devono essere avviati, come illustrato nel frammento di codice hello seguente:</span><span class="sxs-lookup"><span data-stu-id="83992-135">hello generated ServiceManifest.xml now has a section that describes how hello Node.js web server should be launched, as shown in hello code snippet below:</span></span>

```xml
<CodePackage Name="C" Version="1.0">
    <EntryPoint>
        <ExeHost>
            <Program>node.exe</Program>
            <Arguments>'bin/www'</Arguments>
            <WorkingFolder>CodePackage</WorkingFolder>
        </ExeHost>
    </EntryPoint>
</CodePackage>
```
<span data-ttu-id="83992-136">In questo esempio, server web Node.js di hello è in ascolto tooport 3000, pertanto è necessario tooupdate hello informazioni sull'endpoint hello ServiceManifest.xml come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="83992-136">In this sample, hello Node.js web server listens tooport 3000, so you need tooupdate hello endpoint information in hello ServiceManifest.xml file as shown below.</span></span>   

```xml
<Resources>
      <Endpoints>
         <Endpoint Name="NodeServiceEndpoint" Protocol="http" Port="3000" Type="Input" />
      </Endpoints>
</Resources>
```
### <a name="packaging-hello-mongodb-application"></a><span data-ttu-id="83992-137">Hello pacchetti applicazione di MongoDB</span><span class="sxs-lookup"><span data-stu-id="83992-137">Packaging hello MongoDB application</span></span>
<span data-ttu-id="83992-138">Ora che è stata compressa un'applicazione hello Node.js, è possibile procedere e pacchetti di MongoDB.</span><span class="sxs-lookup"><span data-stu-id="83992-138">Now that you have packaged hello Node.js application, you can go ahead and package MongoDB.</span></span> <span data-ttu-id="83992-139">Come già accennato, hello passaggi che attraversano ora non sono specifiche tooNode.js e MongoDB.</span><span class="sxs-lookup"><span data-stu-id="83992-139">As mentioned before, hello steps that you go through now are not specific tooNode.js and MongoDB.</span></span> <span data-ttu-id="83992-140">Infatti, si applicano tooall applicazioni che sono destinate toobe riuniti insieme come una sola applicazione di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="83992-140">In fact, they apply tooall applications that are meant toobe packaged together as one Service Fabric application.</span></span>  

<span data-ttu-id="83992-141">toopackage MongoDB, si desidera che crei Mongod.exe e Mongo.exe toomake.</span><span class="sxs-lookup"><span data-stu-id="83992-141">toopackage MongoDB, you want toomake sure you package Mongod.exe and Mongo.exe.</span></span> <span data-ttu-id="83992-142">Entrambi i file binari si trovano in hello `bin` directory della directory di installazione di MongoDB.</span><span class="sxs-lookup"><span data-stu-id="83992-142">Both binaries are located in hello `bin` directory of your MongoDB installation directory.</span></span> <span data-ttu-id="83992-143">struttura di directory Hello è simile toohello uno sotto.</span><span class="sxs-lookup"><span data-stu-id="83992-143">hello directory structure looks similar toohello one below.</span></span>

```
|-- MongoDB
    |-- bin
        |-- mongod.exe
        |-- mongo.exe
        |-- anybinary.exe
```
<span data-ttu-id="83992-144">Service Fabric deve toostart MongoDB con un toohello simile comando uno riportato di seguito, pertanto è necessario hello toouse `/ma` parametro durante l'assemblaggio di MongoDB.</span><span class="sxs-lookup"><span data-stu-id="83992-144">Service Fabric needs toostart MongoDB with a command similar toohello one below, so you need toouse hello `/ma` parameter when packaging MongoDB.</span></span>

```
mongod.exe --dbpath [path toodata]
```
> [!NOTE]
> <span data-ttu-id="83992-145">dati Hello non viene mantenuti nel caso di hello di un errore del nodo se directory dei dati MongoDB hello è stato inserito nella directory locale di hello del nodo hello.</span><span class="sxs-lookup"><span data-stu-id="83992-145">hello data is not being preserved in hello case of a node failure if you put hello MongoDB data directory on hello local directory of hello node.</span></span> <span data-ttu-id="83992-146">Utilizzare l'archiviazione durevole o implementare una replica di MongoDB Imposta ordine tooprevent perdita di dati.</span><span class="sxs-lookup"><span data-stu-id="83992-146">You should either use durable storage or implement a MongoDB replica set in order tooprevent data loss.</span></span>  
>
>

<span data-ttu-id="83992-147">Nella shell dei comandi di PowerShell o hello, Esegui lo strumento di creazione di pacchetti hello con hello seguenti parametri:</span><span class="sxs-lookup"><span data-stu-id="83992-147">In PowerShell or hello command shell, we run hello packaging tool with hello following parameters:</span></span>

```
.\ServiceFabricAppPackageUtil.exe /source: [yourdirectory]\MongoDB' /target:'[yourtargetdirectory]' /appname:MongoDB /exe:'bin\mongod.exe' /ma:'--dbpath [path toodata]' /AppType:NodeAppType
```

<span data-ttu-id="83992-148">In ordine tooadd MongoDB tooyour Service Fabric pacchetto di applicazione, è necessario che tale parametro /target hello punta toohello toomake stessa directory che contiene già manifesto dell'applicazione hello insieme a un'applicazione hello Node.js.</span><span class="sxs-lookup"><span data-stu-id="83992-148">In order tooadd MongoDB tooyour Service Fabric application package, you need toomake sure that hello /target parameter points toohello same directory that already contains hello application manifest along with hello Node.js application.</span></span> <span data-ttu-id="83992-149">È inoltre necessario assicurarsi che si sta utilizzando toomake hello ApplicationType omonima.</span><span class="sxs-lookup"><span data-stu-id="83992-149">You also need toomake sure that you are using hello same ApplicationType name.</span></span>

<span data-ttu-id="83992-150">Consente di sfogliare la directory toohello ed esaminare lo strumento hello è stato creato.</span><span class="sxs-lookup"><span data-stu-id="83992-150">Let's browse toohello directory and examine what hello tool has created.</span></span>

```
|--[yourtargetdirectory]
    |-- MyNodeApplication
    |-- MongoDB
        |-- C
            |--bin
                |-- mongod.exe
                |-- mongo.exe
                |-- etc.
        |-- config
            |--Settings.xml
        |-- ServiceManifest.xml
    |-- ApplicationManifest.xml
```
<span data-ttu-id="83992-151">Come si può notare, lo strumento hello aggiunta una nuova directory toohello cartella, MongoDB, che contiene i file binari di hello MongoDB.</span><span class="sxs-lookup"><span data-stu-id="83992-151">As you can see, hello tool added a new folder, MongoDB, toohello directory that contains hello MongoDB binaries.</span></span> <span data-ttu-id="83992-152">Se si apre hello `ApplicationManifest.xml` file, è possibile notare che il pacchetto hello ora contiene sia un'applicazione Node.js hello e MongoDB.</span><span class="sxs-lookup"><span data-stu-id="83992-152">If you open hello `ApplicationManifest.xml` file, you can see that hello package now contains both hello Node.js application and MongoDB.</span></span> <span data-ttu-id="83992-153">codice Hello riportato di seguito visualizza hello il contenuto del manifesto dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="83992-153">hello code below shows hello content of hello application manifest.</span></span>

```xml
<ApplicationManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="MyNodeApp" ApplicationTypeVersion="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="MongoDB" ServiceManifestVersion="1.0" />
   </ServiceManifestImport>
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="NodeService" ServiceManifestVersion="1.0" />
   </ServiceManifestImport>
   <DefaultServices>
      <Service Name="MongoDBService">
         <StatelessService ServiceTypeName="MongoDB">
            <SingletonPartition />
         </StatelessService>
      </Service>
      <Service Name="NodeServiceService">
         <StatelessService ServiceTypeName="NodeService">
            <SingletonPartition />
         </StatelessService>
      </Service>
   </DefaultServices>
</ApplicationManifest>  
```

### <a name="publishing-hello-application"></a><span data-ttu-id="83992-154">Pubblicazione dell'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="83992-154">Publishing hello application</span></span>
<span data-ttu-id="83992-155">ultimo passaggio Hello è toopublish hello applicazione toohello dell'infrastruttura del servizio cluster locale usando gli script di PowerShell hello riportato di seguito:</span><span class="sxs-lookup"><span data-stu-id="83992-155">hello last step is toopublish hello application toohello local Service Fabric cluster by using hello PowerShell scripts below:</span></span>

```
Connect-ServiceFabricCluster localhost:19000

Write-Host 'Copying application package...'
Copy-ServiceFabricApplicationPackage -ApplicationPackagePath '[yourtargetdirectory]' -ImageStoreConnectionString 'file:C:\SfDevCluster\Data\ImageStoreShare' -ApplicationPackagePathInImageStore 'NodeAppType'

Write-Host 'Registering application type...'
Register-ServiceFabricApplicationType -ApplicationPathInImageStore 'NodeAppType'

New-ServiceFabricApplication -ApplicationName 'fabric:/NodeApp' -ApplicationTypeName 'NodeAppType' -ApplicationTypeVersion 1.0  
```

<span data-ttu-id="83992-156">Al termine dell'applicazione hello cluster locale toohello pubblicati correttamente, è possibile accedere a un'applicazione hello Node.js sulla porta hello che è stato immesso nel manifesto del servizio di un'applicazione hello Node.js, ad esempio http://localhost:3000 hello.</span><span class="sxs-lookup"><span data-stu-id="83992-156">Once hello application is successfully published toohello local cluster, you can access hello Node.js application on hello port that we have entered in hello service manifest of hello Node.js application--for example http://localhost:3000.</span></span>

<span data-ttu-id="83992-157">In questa esercitazione è stato illustrato come tooeasily pacchetto due applicazioni esistente come un'applicazione di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="83992-157">In this tutorial, you have seen how tooeasily package two existing applications as one Service Fabric application.</span></span> <span data-ttu-id="83992-158">Inoltre, si è appreso come toodeploy è tooService dell'infrastruttura in modo che può trarre vantaggio dall'hello alcune funzionalità di Service Fabric, ad esempio l'integrazione di sistema di integrità e disponibilità elevata.</span><span class="sxs-lookup"><span data-stu-id="83992-158">You have also learned how toodeploy it tooService Fabric so that it can benefit from some of hello Service Fabric features, such as high availability and health system integration.</span></span>


## <a name="adding-more-guest-executables-tooan-existing-application-using-yeoman-on-linux"></a><span data-ttu-id="83992-159">Aggiunta di ulteriori guest eseguibili tooan applicazione esistente tramite Yeoman in Linux</span><span class="sxs-lookup"><span data-stu-id="83992-159">Adding more guest executables tooan existing application using Yeoman on Linux</span></span>

<span data-ttu-id="83992-160">tooadd già un'altra applicazione tooan di servizio creato utilizzando `yo`, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="83992-160">tooadd another service tooan application already created using `yo`, perform hello following steps:</span></span> 
1. <span data-ttu-id="83992-161">Cambiare directory toohello principale di un'applicazione hello esistente.</span><span class="sxs-lookup"><span data-stu-id="83992-161">Change directory toohello root of hello existing application.</span></span>  <span data-ttu-id="83992-162">Ad esempio, `cd ~/YeomanSamples/MyApplication`, se `MyApplication` è un'applicazione hello creata da Yeoman.</span><span class="sxs-lookup"><span data-stu-id="83992-162">For example, `cd ~/YeomanSamples/MyApplication`, if `MyApplication` is hello application created by Yeoman.</span></span>
2. <span data-ttu-id="83992-163">Eseguire `yo azuresfguest:AddService` e fornire i dettagli necessari hello.</span><span class="sxs-lookup"><span data-stu-id="83992-163">Run `yo azuresfguest:AddService` and provide hello necessary details.</span></span>

## <a name="next-steps"></a><span data-ttu-id="83992-164">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="83992-164">Next steps</span></span>
* <span data-ttu-id="83992-165">Per avere informazioni sulla distribuzione di contenitori, consultare [Panoramica di Service Fabric e contenitori](service-fabric-containers-overview.md)</span><span class="sxs-lookup"><span data-stu-id="83992-165">Learn about deploying containers with [Service Fabric and containers overview](service-fabric-containers-overview.md)</span></span>
* [<span data-ttu-id="83992-166">Esempio per la creazione di un pacchetto e distribuzione di un file guest eseguibile</span><span class="sxs-lookup"><span data-stu-id="83992-166">Sample for packaging and deploying a guest executable</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [<span data-ttu-id="83992-167">Esempio di guest due file eseguibili (c# e nodejs) comunicano tramite il servizio di denominazione hello tramite REST</span><span class="sxs-lookup"><span data-stu-id="83992-167">Sample of two guest executables (C# and nodejs) communicating via hello Naming service using REST</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-containers)
