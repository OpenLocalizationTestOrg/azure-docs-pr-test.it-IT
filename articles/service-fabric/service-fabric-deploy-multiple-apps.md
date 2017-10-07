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
# <a name="deploy-multiple-guest-executables"></a>Distribuire più eseguibili guest
Questo articolo viene illustrato come toopackage e distribuire più guest eseguibili tooAzure Service Fabric. Compilazione e distribuzione di un singolo pacchetto di Service Fabric leggere come troppo[distribuire un tooService eseguibile guest infrastruttura](service-fabric-deploy-existing-app.md).

Durante questa procedura dettagliata illustra come un'applicazione con un front-end Node.js che usa MongoDB come archivio dati hello toodeploy, è possibile applicare hello passaggi tooany le applicazioni con dipendenze da un'altra applicazione.   

È possibile utilizzare Visual Studio tooproduce hello pacchetto di applicazione contiene più file eseguibili di guest. Vedere [toopackage tramite Visual Studio un'applicazione esistente](service-fabric-deploy-existing-app.md). Dopo aver aggiunto eseguibile guest prima hello, fare clic sul progetto di applicazione hello e seleziona hello **Aggiungi -> servizio nuova Service Fabric** tooadd hello secondo guest eseguibile toohello soluzione del progetto. Nota: Se si sceglie l'origine di hello toolink nel progetto di Visual Studio, hello soluzione Visual Studio, hello garantisce che il pacchetto dell'applicazione è toodate con le modifiche nell'origine hello. 

## <a name="samples"></a>Esempi
* [Esempio per la creazione di un pacchetto e distribuzione di un file guest eseguibile](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [Esempio di guest due file eseguibili (c# e nodejs) comunicano tramite il servizio di denominazione hello tramite REST](https://github.com/Azure-Samples/service-fabric-dotnet-containers)

## <a name="manually-package-hello-multiple-guest-executable-application"></a>Manualmente i pacchetti hello applicazione eseguibile guest multiple
In alternativa è possibile creare manualmente un pacchetto guest hello eseguibile. Per la creazione del pacchetto manuale hello, in questo articolo Usa strumento di creazione di pacchetti di hello Service Fabric, è disponibile all'indirizzo [http://aka.ms/servicefabricpacktool](http://aka.ms/servicefabricpacktool).

### <a name="packaging-hello-nodejs-application"></a>Hello pacchetti applicazione Node.js
Questo articolo si presuppone che non è installato Node.js sui nodi nel cluster di Service Fabric hello hello. Di conseguenza, è necessario tooadd Node.exe toohello radice dell'applicazione nodo prima della creazione del pacchetto. struttura di directory Hello di un'applicazione hello Node.js (tramite un framework web Express e motore del modello Jade) dovrebbe essere simile toohello uno di seguito:

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

Come passaggio successivo, si crea un pacchetto di applicazione per hello applicazione Node.js. codice Hello seguente crea un pacchetto di applicazione di Service Fabric che contiene un'applicazione hello Node.js.

```
.\ServiceFabricAppPackageUtil.exe /source:'[yourdirectory]\MyNodeApplication' /target:'[yourtargetdirectory] /appname:NodeService /exe:'node.exe' /ma:'bin/www' /AppType:NodeAppType
```

Di seguito è riportata una descrizione dei parametri di hello in uso:

* **/Source** punti toohello directory dell'applicazione hello che deve essere incluso nel pacchetto.
* **/target** definisce hello directory nella quale hello pacchetto deve essere creato. La directory ha toobe diversa dalla directory di origine hello.
* **/appname** definisce il nome dell'applicazione hello di un'applicazione hello esistente. È importante toounderstand che questo si traduce il nome del servizio toohello nel manifesto hello e non nome dell'applicazione Service Fabric toohello.
* **/exe** definisce hello eseguibile che Service Fabric dovrebbe toolaunch, in questo caso `node.exe`.
* **/ma** definisce hello argomento che viene utilizzato toolaunch hello eseguibile. Node.js non è installato, Service Fabric deve server web Node.js di hello toolaunch eseguendo `node.exe bin/www`.  `/ma:'bin/www'`indica toouse strumento di creazione di pacchetti hello `bin/ma` come argomento di hello per node.exe.
* **/ AppType** definisce nome tipo dell'applicazione di Service Fabric hello.

Se si seleziona una directory specificata nel parametro /target hello toohello, è possibile visualizzare che tale strumento hello è creato un pacchetto di Service Fabric completamente funziona, come illustrato di seguito:

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
Hello ServiceManifest.xml generato include ora una sezione che descrive come server web Node.js di hello devono essere avviati, come illustrato nel frammento di codice hello seguente:

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
In questo esempio, server web Node.js di hello è in ascolto tooport 3000, pertanto è necessario tooupdate hello informazioni sull'endpoint hello ServiceManifest.xml come illustrato di seguito.   

```xml
<Resources>
      <Endpoints>
         <Endpoint Name="NodeServiceEndpoint" Protocol="http" Port="3000" Type="Input" />
      </Endpoints>
</Resources>
```
### <a name="packaging-hello-mongodb-application"></a>Hello pacchetti applicazione di MongoDB
Ora che è stata compressa un'applicazione hello Node.js, è possibile procedere e pacchetti di MongoDB. Come già accennato, hello passaggi che attraversano ora non sono specifiche tooNode.js e MongoDB. Infatti, si applicano tooall applicazioni che sono destinate toobe riuniti insieme come una sola applicazione di Service Fabric.  

toopackage MongoDB, si desidera che crei Mongod.exe e Mongo.exe toomake. Entrambi i file binari si trovano in hello `bin` directory della directory di installazione di MongoDB. struttura di directory Hello è simile toohello uno sotto.

```
|-- MongoDB
    |-- bin
        |-- mongod.exe
        |-- mongo.exe
        |-- anybinary.exe
```
Service Fabric deve toostart MongoDB con un toohello simile comando uno riportato di seguito, pertanto è necessario hello toouse `/ma` parametro durante l'assemblaggio di MongoDB.

```
mongod.exe --dbpath [path toodata]
```
> [!NOTE]
> dati Hello non viene mantenuti nel caso di hello di un errore del nodo se directory dei dati MongoDB hello è stato inserito nella directory locale di hello del nodo hello. Utilizzare l'archiviazione durevole o implementare una replica di MongoDB Imposta ordine tooprevent perdita di dati.  
>
>

Nella shell dei comandi di PowerShell o hello, Esegui lo strumento di creazione di pacchetti hello con hello seguenti parametri:

```
.\ServiceFabricAppPackageUtil.exe /source: [yourdirectory]\MongoDB' /target:'[yourtargetdirectory]' /appname:MongoDB /exe:'bin\mongod.exe' /ma:'--dbpath [path toodata]' /AppType:NodeAppType
```

In ordine tooadd MongoDB tooyour Service Fabric pacchetto di applicazione, è necessario che tale parametro /target hello punta toohello toomake stessa directory che contiene già manifesto dell'applicazione hello insieme a un'applicazione hello Node.js. È inoltre necessario assicurarsi che si sta utilizzando toomake hello ApplicationType omonima.

Consente di sfogliare la directory toohello ed esaminare lo strumento hello è stato creato.

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
Come si può notare, lo strumento hello aggiunta una nuova directory toohello cartella, MongoDB, che contiene i file binari di hello MongoDB. Se si apre hello `ApplicationManifest.xml` file, è possibile notare che il pacchetto hello ora contiene sia un'applicazione Node.js hello e MongoDB. codice Hello riportato di seguito visualizza hello il contenuto del manifesto dell'applicazione hello.

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

### <a name="publishing-hello-application"></a>Pubblicazione dell'applicazione hello
ultimo passaggio Hello è toopublish hello applicazione toohello dell'infrastruttura del servizio cluster locale usando gli script di PowerShell hello riportato di seguito:

```
Connect-ServiceFabricCluster localhost:19000

Write-Host 'Copying application package...'
Copy-ServiceFabricApplicationPackage -ApplicationPackagePath '[yourtargetdirectory]' -ImageStoreConnectionString 'file:C:\SfDevCluster\Data\ImageStoreShare' -ApplicationPackagePathInImageStore 'NodeAppType'

Write-Host 'Registering application type...'
Register-ServiceFabricApplicationType -ApplicationPathInImageStore 'NodeAppType'

New-ServiceFabricApplication -ApplicationName 'fabric:/NodeApp' -ApplicationTypeName 'NodeAppType' -ApplicationTypeVersion 1.0  
```

Al termine dell'applicazione hello cluster locale toohello pubblicati correttamente, è possibile accedere a un'applicazione hello Node.js sulla porta hello che è stato immesso nel manifesto del servizio di un'applicazione hello Node.js, ad esempio http://localhost:3000 hello.

In questa esercitazione è stato illustrato come tooeasily pacchetto due applicazioni esistente come un'applicazione di Service Fabric. Inoltre, si è appreso come toodeploy è tooService dell'infrastruttura in modo che può trarre vantaggio dall'hello alcune funzionalità di Service Fabric, ad esempio l'integrazione di sistema di integrità e disponibilità elevata.


## <a name="adding-more-guest-executables-tooan-existing-application-using-yeoman-on-linux"></a>Aggiunta di ulteriori guest eseguibili tooan applicazione esistente tramite Yeoman in Linux

tooadd già un'altra applicazione tooan di servizio creato utilizzando `yo`, eseguire hello alla procedura seguente: 
1. Cambiare directory toohello principale di un'applicazione hello esistente.  Ad esempio, `cd ~/YeomanSamples/MyApplication`, se `MyApplication` è un'applicazione hello creata da Yeoman.
2. Eseguire `yo azuresfguest:AddService` e fornire i dettagli necessari hello.

## <a name="next-steps"></a>Passaggi successivi
* Per avere informazioni sulla distribuzione di contenitori, consultare [Panoramica di Service Fabric e contenitori](service-fabric-containers-overview.md)
* [Esempio per la creazione di un pacchetto e distribuzione di un file guest eseguibile](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [Esempio di guest due file eseguibili (c# e nodejs) comunicano tramite il servizio di denominazione hello tramite REST](https://github.com/Azure-Samples/service-fabric-dotnet-containers)
