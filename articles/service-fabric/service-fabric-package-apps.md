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
# <a name="package-an-application"></a>Inserire un'applicazione in un pacchetto
Questo articolo viene descritto come un'applicazione di Service Fabric toopackage e renderlo pronto per la distribuzione.

## <a name="package-layout"></a>Layout del pacchetto
manifesto dell'applicazione Hello, uno o più manifesti di servizio e di altri pacchetti necessari i file devono essere organizzati in un layout specifico per la distribuzione in un cluster di Service Fabric. manifesti di esempio Hello in questo articolo dovrebbe toobe organizzati in hello seguente struttura di directory:

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

cartelle di Hello sono denominate hello toomatch **nome** gli attributi di ogni elemento corrispondente. Ad esempio, se hello manifesto del servizio contiene due pacchetti di codice con i nomi di hello **MyCodeA** e **MyCodeB**, quindi due cartelle con nomi uguali a conterrebbe hello hello file binari necessari per ogni codice pacchetto.

## <a name="use-setupentrypoint"></a>Usare SetupEntryPoint
Scenari tipici per l'utilizzo di **SetupEntryPoint** si verifica se è necessario un file eseguibile prima dell'avvio del servizio hello toorun oppure tooperform un'operazione con privilegi elevati. ad esempio:

* Impostazione e l'inizializzazione di variabili di ambiente hello esigenze eseguibile del servizio. Non è limitato tooonly eseguibili scritti tramite modelli di programmazione di Service Fabric hello. Ad esempio, npm.exe richiede alcune variabili di ambiente configurate per la distribuzione di un'applicazione node.js.
* Impostazione del controllo di accesso mediante l'installazione di certificati di sicurezza.

Per ulteriori informazioni su come hello tooconfigure **SetupEntryPoint**, vedere [configurare criteri di hello per un punto di ingresso del programma di installazione del servizio](service-fabric-application-runas-security.md)

<a id="Package-App"></a>
## <a name="configure"></a>Configurare
### <a name="build-a-package-by-using-visual-studio"></a>Creare un pacchetto mediante Visual Studio
Se si utilizza Visual Studio 2015 toocreate l'applicazione, è possibile utilizzare hello pacchetto tooautomatically comando creare un pacchetto che corrisponde a layout hello descritto in precedenza.

toocreate un pacchetto, fare clic sul progetto dell'applicazione hello in Esplora soluzioni e scegliere il comando di pacchetto hello, come illustrato di seguito:

![Inserire un'applicazione in un pacchetto con Visual Studio][vs-package-command]

Una volta completato pacchetti, è possibile trovare posizione hello del pacchetto di hello in hello **Output** finestra. passaggio di creazione di pacchetti Hello avviene automaticamente quando si distribuisce o il debug dell'applicazione in Visual Studio.

### <a name="build-a-package-by-command-line"></a>Creare un pacchetto dalla riga di comando
È inoltre possibile tooprogrammatically pacchetto di applicazione utilizzando `msbuild.exe`. Quinte hello, Visual Studio è in esecuzione, pertanto è lo stesso output di hello.

```shell
D:\Temp> msbuild HelloWorld.sfproj /t:Package
```

## <a name="test-hello-package"></a>Pacchetto di hello test
È possibile verificare struttura del pacchetto hello in locale tramite PowerShell utilizzando hello [Test ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) comando.
Questo comando consente di verificare i problemi di analisi dei manifesti e tutti i riferimenti. Questo comando si limita a verificare la correttezza strutturale hello di hello directory e file nel pacchetto hello.
Non consente di verificare il contenuto di pacchetto di codice o dati hello oltre verifica che tutti i file necessari siano presenti.

```
PS D:\temp> Test-ServiceFabricApplicationPackage .\MyApplicationType
False
Test-ServiceFabricApplicationPackage : hello EntryPoint MySetup.bat is not found.
FileName: C:\Users\servicefabric\AppData\Local\Temp\TestApplicationPackage_7195781181\nrri205a.e2h\MyApplicationType\MyServiceManifest\ServiceManifest.xml
```

Questo errore viene illustrato tale hello *MySetup.bat* file a cui fa riferimento nel manifesto del servizio hello **SetupEntryPoint** mancante dal pacchetto di codice hello. Dopo l'aggiunta di file mancante hello, verifica dell'applicazione hello ha esito positivo:

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

Se l'applicazione include [parametri applicazione](service-fabric-manage-multiple-environment-app-configuration.md) definiti, è possibile passarli in [Test-ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) per una convalida appropriata.

Se si conosce cluster hello in cui viene distribuita un'applicazione hello, è consigliabile passare nel hello `ImageStoreConnectionString` parametro. In questo caso, pacchetto hello viene convalidato anche in versioni precedenti di un'applicazione hello che sono già in esecuzione nel cluster hello. Ad esempio, la convalida di hello può rilevare se un pacchetto con hello stessa versione ma contenuto diverso è già stato distribuito.  

Dopo che un'applicazione hello viene incluso nel pacchetto correttamente e passa la convalida, valutare in base alle dimensioni hello e numero hello di file se è necessaria la compressione.

## <a name="compress-a-package"></a>Comprimere un pacchetto
Quando un pacchetto è di grandi dimensioni o dispone di molti file, è possibile comprimerlo per velocizzare la distribuzione. La compressione riduce il numero di hello di file e le dimensioni di pacchetto hello.
Per un pacchetto di applicazione compresso, [pacchetto di applicazione di caricamento in corso hello](service-fabric-deploy-remove-applications.md#upload-the-application-package) potrebbe richiedere più confrontati toouploading hello compressi pacchetto (appositamente se il tempo di compressione è inserito), ma [registrazione](service-fabric-deploy-remove-applications.md#register-the-application-package) e [tipo l'annullamento della registrazione dell'applicazione hello](service-fabric-deploy-remove-applications.md#unregister-an-application-type) sono più veloci per un pacchetto di applicazione compresso.

il meccanismo di distribuzione Hello è lo stesso per i pacchetti compressi e non compressi. Se il pacchetto di hello è compresso, viene archiviata come tale nell'archivio di immagini cluster hello ed è non compressi in nodo hello prima di eseguita un'applicazione hello.
la compressione di Hello sostituisce il pacchetto di Service Fabric valido hello con versione compressa hello. cartella Hello deve consentire le autorizzazioni di scrittura. La compressione di un pacchetto già compresso non apporta modifiche.

È possibile comprimere un pacchetto eseguendo il comando di Powershell hello [copia ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) con `CompressPackage` passare. È possibile decomprimere hello del pacchetto con hello stesso comando, mediante `UncompressPackage` passare.

Hello comando seguente consente di comprimere pacchetto hello senza copiarlo toohello archivio di immagini. È possibile copiare un pacchetto compresso di tooone o più cluster di Service Fabric, in base alle esigenze, utilizzando [copia ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) senza hello `SkipCopy` flag.
pacchetto di Hello include ora i file ZIP per hello `code`, `config`, e `data` pacchetti. manifesto dell'applicazione Hello e hello servizio manifesti non compressi, perché sono necessari per molte operazioni interne (ad esempio la condivisione, l'applicazione nome e la versione estrazione del tipo per alcune convalide di pacchetto).
Compressione manifesti hello renderebbe queste operazioni inefficienti.

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

In alternativa, è possibile comprimere e copiare il pacchetto di hello con [copia ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) in un unico passaggio.
Se il pacchetto di hello è grande, fornire un tempo di tooallow sufficientemente elevato per la compressione di pacchetto hello e cluster toohello di caricamento hello.
```
PS D:\temp> Copy-ServiceFabricApplicationPackage -ApplicationPackagePath .\MyApplicationType -ApplicationPackagePathInImageStore MyApplicationType -ImageStoreConnectionString fabric:ImageStore -CompressPackage -TimeoutSec 5400
```

Internamente, Service Fabric calcola i valori di checksum per i pacchetti di applicazione hello per la convalida. Quando si utilizza la compressione, hello checksum vengono calcolate in ogni pacchetto versioni compressa hello.
Se è stata copiata una versione non compressa del pacchetto di applicazione e si desidera che la compressione toouse per hello stesso pacchetto, è necessario modificare le versioni di hello di hello `code`, `config`, e `data` mancata corrispondenza del checksum tooavoid pacchetti. Se i pacchetti hello rimangono invariati, anziché la modifica di versione di hello, è possibile utilizzare [diff provisioning](service-fabric-application-upgrade-advanced.md). Con questa opzione, non includere pacchetto invariato di hello invece farvi riferimento dal manifesto del servizio hello.

Analogamente, se è stata caricata una versione compressa del pacchetto di hello e si desidera toouse un pacchetto non compresso, è necessario aggiornare mancata corrispondenza del checksum hello versioni tooavoid hello.

Hello pacchetto è ora incluso nel pacchetto in modo corretto, convalidare e compressi (se necessario), in modo che sia pronto per [distribuzione](service-fabric-deploy-remove-applications.md) tooone o altre dell'infrastruttura del servizio cluster.

### <a name="compress-packages-when-deploying-using-visual-studio"></a>Comprimere i pacchetti quando si distribuisce con Visual Studio
È possibile indicare i pacchetti di Visual Studio toocompress nella distribuzione, aggiungendo hello `CopyPackageParameters` tooyour elemento profilo di pubblicazione e impostare hello `CompressPackage` attributo troppo`true`.

``` xml
    <PublishProfile xmlns="http://schemas.microsoft.com/2015/05/fabrictools">
        <ClusterConnectionParameters ConnectionEndpoint="mycluster.westus.cloudapp.azure.com" />
        <ApplicationParameterFile Path="..\ApplicationParameters\Cloud.xml" />
        <CopyPackageParameters CompressPackage="true"/>
    </PublishProfile>
```

## <a name="next-steps"></a>Passaggi successivi
[Distribuire e rimuovere le applicazioni] [ 10] viene descritto come le istanze dell'applicazione toomanage toouse PowerShell

[Gestione dei parametri dell'applicazione per più ambienti] [ 11] viene descritto come tooconfigure parametri e variabili di ambiente per le istanze dell'applicazione diverso.

[Configurare i criteri di sicurezza per l'applicazione] [ 12] viene descritto come toorun servizi con accesso toorestrict criteri di sicurezza.

<!--Image references-->
[vs-package-command]: ./media/service-fabric-package-apps/vs-package-command.png

<!--Link references--In actual articles, you only need a single period before hello slash-->
[10]: service-fabric-deploy-remove-applications.md
[11]: service-fabric-manage-multiple-environment-app-configuration.md
[12]: service-fabric-application-runas-security.md
