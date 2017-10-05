---
title: Distribuire un'applicazione Node.js che usa MongoDB | Documentazione Microsoft
description: "Procedura dettagliata sulla creazione di pacchetti di più eseguibili guest da distribuire in un cluster di Azure Service Fabric"
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
ms.openlocfilehash: b71723034e5f663986c49481072bfd6779d3d57b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-multiple-guest-executables"></a><span data-ttu-id="13e40-103">Distribuire più eseguibili guest</span><span class="sxs-lookup"><span data-stu-id="13e40-103">Deploy multiple guest executables</span></span>
<span data-ttu-id="13e40-104">Questo articolo descrive come creare pacchetti di più eseguibili guest e in che modo distribuirli in Azure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="13e40-104">This article shows how to package and deploy multiple guest executables to Azure Service Fabric.</span></span> <span data-ttu-id="13e40-105">Per la creazione e la distribuzione di un pacchetto di Service Fabric, consultare l'articolo [Distribuire un eseguibile guest in Service Fabric](service-fabric-deploy-existing-app.md).</span><span class="sxs-lookup"><span data-stu-id="13e40-105">For building and deploying a single Service Fabric package read how to [deploy a guest executable to Service Fabric](service-fabric-deploy-existing-app.md).</span></span>

<span data-ttu-id="13e40-106">Questa procedura dettagliata illustra come distribuire un'applicazione con un front-end di Node.js che usa MongoDB come archivio dati, ma può essere adottata per qualsiasi applicazione che presenta dipendenze da un'altra applicazione.</span><span class="sxs-lookup"><span data-stu-id="13e40-106">While this walkthrough shows how to deploy an application with a Node.js front end that uses MongoDB as the data store, you can apply the steps to any application that has dependencies on another application.</span></span>   

<span data-ttu-id="13e40-107">È possibile usare Visual Studio per generare il pacchetto dell'applicazione che contiene più eseguibili guest.</span><span class="sxs-lookup"><span data-stu-id="13e40-107">You can use Visual Studio to produce the application package that contains multiple guest executables.</span></span> <span data-ttu-id="13e40-108">Vedere [Uso di Visual Studio per creare il pacchetto di un'applicazione esistente](service-fabric-deploy-existing-app.md).</span><span class="sxs-lookup"><span data-stu-id="13e40-108">See [Using Visual Studio to package an existing application](service-fabric-deploy-existing-app.md).</span></span> <span data-ttu-id="13e40-109">Dopo aver aggiunto il primo eseguibile guest, fare clic con il tasto destro sul progetto dell'applicazione e selezionare **Aggiungi -> Nuovo servizio Service Fabric** per aggiungere il secondo progetto eseguibile guest alla soluzione.</span><span class="sxs-lookup"><span data-stu-id="13e40-109">After you have added the first guest executable, right click on the application project and select the **Add->New Service Fabric service** to add the second guest executable project to the solution.</span></span> <span data-ttu-id="13e40-110">Nota: se si sceglie il collegamento all'origine nel progetto di Visual Studio, la compilazione della soluzione di Visual Studio assicura che il pacchetto dell'applicazione venga aggiornato in base alle modifiche nell'origine.</span><span class="sxs-lookup"><span data-stu-id="13e40-110">Note: If you choose to link the source in the Visual Studio project, building the Visual Studio solution, will make sure that your application package is up to date with changes in the source.</span></span> 

## <a name="samples"></a><span data-ttu-id="13e40-111">Esempi</span><span class="sxs-lookup"><span data-stu-id="13e40-111">Samples</span></span>
* [<span data-ttu-id="13e40-112">Esempio per la creazione di un pacchetto e distribuzione di un file guest eseguibile</span><span class="sxs-lookup"><span data-stu-id="13e40-112">Sample for packaging and deploying a guest executable</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [<span data-ttu-id="13e40-113">Esempio di due eseguibili guest (C# e nodejs) che comunicano tramite il servizio Naming usando REST</span><span class="sxs-lookup"><span data-stu-id="13e40-113">Sample of two guest executables (C# and nodejs) communicating via the Naming service using REST</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-containers)

## <a name="manually-package-the-multiple-guest-executable-application"></a><span data-ttu-id="13e40-114">Creare manualmente i pacchetti dell'applicazione eseguibile guest multipla</span><span class="sxs-lookup"><span data-stu-id="13e40-114">Manually package the multiple guest executable application</span></span>
<span data-ttu-id="13e40-115">In alternativa, è possibile distribuire manualmente l'eseguibile guest.</span><span class="sxs-lookup"><span data-stu-id="13e40-115">Alternatively you can manually package the guest executable.</span></span> <span data-ttu-id="13e40-116">Per quanto riguarda la creazione di pacchetti manuale, l'articolo descrive l'uso dello strumento di packaging di Service Fabric, disponibile all'indirizzo [http://aka.ms/servicefabricpacktool](http://aka.ms/servicefabricpacktool).</span><span class="sxs-lookup"><span data-stu-id="13e40-116">For the manual packaging, this article uses the Service Fabric packaging tool, which is available at [http://aka.ms/servicefabricpacktool](http://aka.ms/servicefabricpacktool).</span></span>

### <a name="packaging-the-nodejs-application"></a><span data-ttu-id="13e40-117">Creazione di un pacchetto dell'applicazione Node.js</span><span class="sxs-lookup"><span data-stu-id="13e40-117">Packaging the Node.js application</span></span>
<span data-ttu-id="13e40-118">Questo articolo presuppone che Node.js non sia installato nei nodi del cluster di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="13e40-118">This article assumes that Node.js is not installed on the nodes in the Service Fabric cluster.</span></span> <span data-ttu-id="13e40-119">Sarà quindi necessario aggiungere Node.exe alla directory radice dell'applicazione nodo prima della creazione del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="13e40-119">As a consequence, you need to add Node.exe to the root directory of your node application before packaging.</span></span> <span data-ttu-id="13e40-120">La struttura di directory dell'applicazione Node.js (che usa il framework Web Express e il motore per la creazione di modelli Jade) dovrebbe essere simile alla seguente:</span><span class="sxs-lookup"><span data-stu-id="13e40-120">The directory structure of the Node.js application (using Express web framework and Jade template engine) should look similar to the one below:</span></span>

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

<span data-ttu-id="13e40-121">Il passaggio successivo consiste nella creazione di un pacchetto per l'applicazione Node.js.</span><span class="sxs-lookup"><span data-stu-id="13e40-121">As a next step, you create an application package for the Node.js application.</span></span> <span data-ttu-id="13e40-122">Il codice seguente crea un pacchetto dell'applicazione dell'infrastruttura di servizi contenente l'applicazione Node.js.</span><span class="sxs-lookup"><span data-stu-id="13e40-122">The code below creates a Service Fabric application package that contains the Node.js application.</span></span>

```
.\ServiceFabricAppPackageUtil.exe /source:'[yourdirectory]\MyNodeApplication' /target:'[yourtargetdirectory] /appname:NodeService /exe:'node.exe' /ma:'bin/www' /AppType:NodeAppType
```

<span data-ttu-id="13e40-123">Di seguito è riportata una descrizione dei parametri in uso:</span><span class="sxs-lookup"><span data-stu-id="13e40-123">Below is a description of the parameters that are being used:</span></span>

* <span data-ttu-id="13e40-124">**/source** : punta alla directory dell'applicazione da includere nel pacchetto.</span><span class="sxs-lookup"><span data-stu-id="13e40-124">**/source** points to the directory of the application that should be packaged.</span></span>
* <span data-ttu-id="13e40-125">**/target** : definisce la directory in cui creare il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="13e40-125">**/target** defines the directory in which the package should be created.</span></span> <span data-ttu-id="13e40-126">Questa directory deve essere diversa dalla directory di origine.</span><span class="sxs-lookup"><span data-stu-id="13e40-126">This directory has to be different from the source directory.</span></span>
* <span data-ttu-id="13e40-127">**/appname** : definisce il nome dell'applicazione esistente.</span><span class="sxs-lookup"><span data-stu-id="13e40-127">**/appname** defines the application name of the existing application.</span></span> <span data-ttu-id="13e40-128">È importante comprendere che questo nome equivale al nome del servizio nel manifesto e non al nome dell'applicazione di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="13e40-128">It's important to understand that this translates to the service name in the manifest, and not to the Service Fabric application name.</span></span>
* <span data-ttu-id="13e40-129">**/exe**: definisce il file eseguibile che dovrebbe essere avviato da Service Fabric, in questo caso `node.exe`.</span><span class="sxs-lookup"><span data-stu-id="13e40-129">**/exe** defines the executable that Service Fabric is supposed to launch, in this case `node.exe`.</span></span>
* <span data-ttu-id="13e40-130">**/ma** : definisce l'argomento usato per avviare il file eseguibile.</span><span class="sxs-lookup"><span data-stu-id="13e40-130">**/ma** defines the argument that is being used to launch the executable.</span></span> <span data-ttu-id="13e40-131">Poiché Node.js non è installato, è necessario che Service Fabric avvii il server Web Node.js eseguendo `node.exe bin/www`.</span><span class="sxs-lookup"><span data-stu-id="13e40-131">As Node.js is not installed, Service Fabric needs to launch the Node.js web server by executing `node.exe bin/www`.</span></span>  <span data-ttu-id="13e40-132">`/ma:'bin/www'` indica allo strumento di creazione pacchetti di usare `bin/ma` come argomento per node.exe.</span><span class="sxs-lookup"><span data-stu-id="13e40-132">`/ma:'bin/www'` tells the packaging tool to use `bin/ma` as the argument for node.exe.</span></span>
* <span data-ttu-id="13e40-133">**/AppType** : definisce il nome del tipo di applicazione di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="13e40-133">**/AppType** defines the Service Fabric application type name.</span></span>

<span data-ttu-id="13e40-134">Se si passa alla directory specificata nel parametro /target, si noterà che lo strumento ha creato un pacchetto di Service Fabric pienamente funzionante, come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="13e40-134">If you browse to the directory that was specified in the /target parameter, you can see that the tool has created a fully functioning Service Fabric package as shown below:</span></span>

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
<span data-ttu-id="13e40-135">Il file ServiceManifest.xml generato include ora una sezione che descrive come avviare il server Web Node.js, come illustrato nel frammento di codice seguente:</span><span class="sxs-lookup"><span data-stu-id="13e40-135">The generated ServiceManifest.xml now has a section that describes how the Node.js web server should be launched, as shown in the code snippet below:</span></span>

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
<span data-ttu-id="13e40-136">In questo esempio il server Web Node.js resta in ascolto sulla porta 3000 ed è quindi necessario aggiornare le informazioni sull'endpoint nel file ServiceManifest.xml, come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="13e40-136">In this sample, the Node.js web server listens to port 3000, so you need to update the endpoint information in the ServiceManifest.xml file as shown below.</span></span>   

```xml
<Resources>
      <Endpoints>
         <Endpoint Name="NodeServiceEndpoint" Protocol="http" Port="3000" Type="Input" />
      </Endpoints>
</Resources>
```
### <a name="packaging-the-mongodb-application"></a><span data-ttu-id="13e40-137">Creazione di un pacchetto dell'applicazione MongoDB</span><span class="sxs-lookup"><span data-stu-id="13e40-137">Packaging the MongoDB application</span></span>
<span data-ttu-id="13e40-138">Dopo aver creato il pacchetto dell'applicazione Node.js, è possibile proseguire e creare il pacchetto di MongoDB.</span><span class="sxs-lookup"><span data-stu-id="13e40-138">Now that you have packaged the Node.js application, you can go ahead and package MongoDB.</span></span> <span data-ttu-id="13e40-139">Come accennato in precedenza, i passaggi da eseguire a questo punto non sono specifici di Node.js e MongoDB,</span><span class="sxs-lookup"><span data-stu-id="13e40-139">As mentioned before, the steps that you go through now are not specific to Node.js and MongoDB.</span></span> <span data-ttu-id="13e40-140">ma si applicano a tutte le applicazioni di cui deve essere creato un pacchetto come singola applicazione di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="13e40-140">In fact, they apply to all applications that are meant to be packaged together as one Service Fabric application.</span></span>  

<span data-ttu-id="13e40-141">Per creare un pacchetto di MongoDB, è opportuno assicurarsi di aver creato un pacchetto di Mongod.exe e Mongo.exe.</span><span class="sxs-lookup"><span data-stu-id="13e40-141">To package MongoDB, you want to make sure you package Mongod.exe and Mongo.exe.</span></span> <span data-ttu-id="13e40-142">Entrambi i file binari si trovano nella directory `bin` della directory di installazione di MongoDB.</span><span class="sxs-lookup"><span data-stu-id="13e40-142">Both binaries are located in the `bin` directory of your MongoDB installation directory.</span></span> <span data-ttu-id="13e40-143">La struttura di directory è simile alla seguente.</span><span class="sxs-lookup"><span data-stu-id="13e40-143">The directory structure looks similar to the one below.</span></span>

```
|-- MongoDB
    |-- bin
        |-- mongod.exe
        |-- mongo.exe
        |-- anybinary.exe
```
<span data-ttu-id="13e40-144">Service Fabric deve avviare MongoDB con un comando simile al seguente ed è quindi necessario usare il parametro `/ma` quando si crea il pacchetto di MongoDB.</span><span class="sxs-lookup"><span data-stu-id="13e40-144">Service Fabric needs to start MongoDB with a command similar to the one below, so you need to use the `/ma` parameter when packaging MongoDB.</span></span>

```
mongod.exe --dbpath [path to data]
```
> [!NOTE]
> <span data-ttu-id="13e40-145">Se la directory dei dati di MongoDB viene inserita nella directory locale del nodo e si verifica un errore nel nodo, i dati non vengono mantenuti.</span><span class="sxs-lookup"><span data-stu-id="13e40-145">The data is not being preserved in the case of a node failure if you put the MongoDB data directory on the local directory of the node.</span></span> <span data-ttu-id="13e40-146">È quindi consigliabile usare un'archiviazione durevole o implementare un set di repliche di MongoDB per evitare la perdita di dati.</span><span class="sxs-lookup"><span data-stu-id="13e40-146">You should either use durable storage or implement a MongoDB replica set in order to prevent data loss.</span></span>  
>
>

<span data-ttu-id="13e40-147">In PowerShell o nella shell dei comandi verrà eseguito lo strumento di creazione di pacchetti con i parametri seguenti:</span><span class="sxs-lookup"><span data-stu-id="13e40-147">In PowerShell or the command shell, we run the packaging tool with the following parameters:</span></span>

```
.\ServiceFabricAppPackageUtil.exe /source: [yourdirectory]\MongoDB' /target:'[yourtargetdirectory]' /appname:MongoDB /exe:'bin\mongod.exe' /ma:'--dbpath [path to data]' /AppType:NodeAppType
```

<span data-ttu-id="13e40-148">Per aggiungere MongoDB al pacchetto dell'applicazione di Service Fabric, è necessario assicurarsi che il parametro /target punti alla stessa directory che contiene già il manifesto dell'applicazione insieme all'applicazione Node.js</span><span class="sxs-lookup"><span data-stu-id="13e40-148">In order to add MongoDB to your Service Fabric application package, you need to make sure that the /target parameter points to the same directory that already contains the application manifest along with the Node.js application.</span></span> <span data-ttu-id="13e40-149">e che il nome usato sia lo stesso dell'elemento ApplicationType.</span><span class="sxs-lookup"><span data-stu-id="13e40-149">You also need to make sure that you are using the same ApplicationType name.</span></span>

<span data-ttu-id="13e40-150">Passare alla directory ed esaminare gli elementi creati dallo strumento.</span><span class="sxs-lookup"><span data-stu-id="13e40-150">Let's browse to the directory and examine what the tool has created.</span></span>

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
<span data-ttu-id="13e40-151">Come si può vedere, lo strumento ha aggiunto una nuova cartella MongoDB alla directory contenente i file binari di MongoDB.</span><span class="sxs-lookup"><span data-stu-id="13e40-151">As you can see, the tool added a new folder, MongoDB, to the directory that contains the MongoDB binaries.</span></span> <span data-ttu-id="13e40-152">Se si apre il file `ApplicationManifest.xml` , si può notare che il pacchetto contiene ora l'applicazione Node.js e MongoDB.</span><span class="sxs-lookup"><span data-stu-id="13e40-152">If you open the `ApplicationManifest.xml` file, you can see that the package now contains both the Node.js application and MongoDB.</span></span> <span data-ttu-id="13e40-153">Il codice seguente illustra il contenuto del manifesto dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="13e40-153">The code below shows the content of the application manifest.</span></span>

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

### <a name="publishing-the-application"></a><span data-ttu-id="13e40-154">Pubblicare l'applicazione</span><span class="sxs-lookup"><span data-stu-id="13e40-154">Publishing the application</span></span>
<span data-ttu-id="13e40-155">L'ultimo passaggio consiste nella pubblicazione dell'applicazione nel cluster locale di Service Fabric usando gli script di PowerShell seguenti:</span><span class="sxs-lookup"><span data-stu-id="13e40-155">The last step is to publish the application to the local Service Fabric cluster by using the PowerShell scripts below:</span></span>

```
Connect-ServiceFabricCluster localhost:19000

Write-Host 'Copying application package...'
Copy-ServiceFabricApplicationPackage -ApplicationPackagePath '[yourtargetdirectory]' -ImageStoreConnectionString 'file:C:\SfDevCluster\Data\ImageStoreShare' -ApplicationPackagePathInImageStore 'NodeAppType'

Write-Host 'Registering application type...'
Register-ServiceFabricApplicationType -ApplicationPathInImageStore 'NodeAppType'

New-ServiceFabricApplication -ApplicationName 'fabric:/NodeApp' -ApplicationTypeName 'NodeAppType' -ApplicationTypeVersion 1.0  
```

<span data-ttu-id="13e40-156">Dopo aver pubblicato l'applicazione nel cluster locale, è possibile accedere all'applicazione Node.js nella porta specificata nel manifesto del servizio dell'applicazione Node.js, ad esempio http://localhost:3000.</span><span class="sxs-lookup"><span data-stu-id="13e40-156">Once the application is successfully published to the local cluster, you can access the Node.js application on the port that we have entered in the service manifest of the Node.js application--for example http://localhost:3000.</span></span>

<span data-ttu-id="13e40-157">In questa esercitazione si è appreso come distribuire facilmente due applicazioni esistenti come una singola applicazione di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="13e40-157">In this tutorial, you have seen how to easily package two existing applications as one Service Fabric application.</span></span> <span data-ttu-id="13e40-158">e come distribuirle in Service Fabric in modo da sfruttare i vantaggi di alcune delle funzionalità di Service Fabric, come la disponibilità elevata e l'integrazione con il sistema di integrità.</span><span class="sxs-lookup"><span data-stu-id="13e40-158">You have also learned how to deploy it to Service Fabric so that it can benefit from some of the Service Fabric features, such as high availability and health system integration.</span></span>


## <a name="adding-more-guest-executables-to-an-existing-application-using-yeoman-on-linux"></a><span data-ttu-id="13e40-159">Aggiunta di più eseguibili guest a un'applicazione esistente usando Yeoman in Linux</span><span class="sxs-lookup"><span data-stu-id="13e40-159">Adding more guest executables to an existing application using Yeoman on Linux</span></span>

<span data-ttu-id="13e40-160">Per aggiungere un altro servizio a un'applicazione già creata mediante `yo`, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="13e40-160">To add another service to an application already created using `yo`, perform the following steps:</span></span> 
1. <span data-ttu-id="13e40-161">Modificare la directory impostandola sulla radice dell'applicazione esistente.</span><span class="sxs-lookup"><span data-stu-id="13e40-161">Change directory to the root of the existing application.</span></span>  <span data-ttu-id="13e40-162">Ad esempio, `cd ~/YeomanSamples/MyApplication`, se `MyApplication` è l'applicazione creata da Yeoman.</span><span class="sxs-lookup"><span data-stu-id="13e40-162">For example, `cd ~/YeomanSamples/MyApplication`, if `MyApplication` is the application created by Yeoman.</span></span>
2. <span data-ttu-id="13e40-163">Eseguire `yo azuresfguest:AddService` e specificare i dettagli necessari.</span><span class="sxs-lookup"><span data-stu-id="13e40-163">Run `yo azuresfguest:AddService` and provide the necessary details.</span></span>

## <a name="next-steps"></a><span data-ttu-id="13e40-164">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="13e40-164">Next steps</span></span>
* <span data-ttu-id="13e40-165">Per avere informazioni sulla distribuzione di contenitori, consultare [Panoramica di Service Fabric e contenitori](service-fabric-containers-overview.md)</span><span class="sxs-lookup"><span data-stu-id="13e40-165">Learn about deploying containers with [Service Fabric and containers overview](service-fabric-containers-overview.md)</span></span>
* [<span data-ttu-id="13e40-166">Esempio per la creazione di un pacchetto e distribuzione di un file guest eseguibile</span><span class="sxs-lookup"><span data-stu-id="13e40-166">Sample for packaging and deploying a guest executable</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [<span data-ttu-id="13e40-167">Esempio di due eseguibili guest (C# e nodejs) che comunicano tramite il servizio Naming usando REST</span><span class="sxs-lookup"><span data-stu-id="13e40-167">Sample of two guest executables (C# and nodejs) communicating via the Naming service using REST</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-containers)
