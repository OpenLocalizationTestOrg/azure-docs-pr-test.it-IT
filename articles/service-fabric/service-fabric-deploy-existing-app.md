---
title: aaaDeploy un tooAzure eseguibile esistente Service Fabric | Documenti Microsoft
description: "Procedura dettagliata sulla modalità di distribuzione di cluster di Service Fabric tooa toopackage un'applicazione esistente come un eseguibile guest, pertanto può essere"
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: d799c1c6-75eb-4b8a-9f94-bf4f3dadf4c3
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 07/02/2017
ms.author: mfussell;mikhegn
ms.openlocfilehash: 5599802bdb6bda2407a138d77e12148ccb64f437
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-guest-executable-tooservice-fabric"></a>Distribuire un tooService eseguibile guest dell'infrastruttura
In Azure Service Fabric distribuito come servizio è possibile eseguire qualsiasi tipo di codice, ad esempio Node.js, Java, e C++. Service Fabric si riferisce tipi toothese di servizi come file eseguibili di guest.

Gli eseguibili guest vengono considerati da Service Fabric come servizi senza stato. Di conseguenza, vengono inseriti nei nodi di un cluster in base alla disponibilità e ad altre metriche. Questo articolo viene descritto come toopackage e distribuire un cluster di Service Fabric tooa eseguibile guest, tramite Visual Studio o un'utilità della riga di comando.

In questo articolo è coprire hello passaggi toopackage un eseguibile guest e distribuirlo tooService dell'infrastruttura.  

## <a name="benefits-of-running-a-guest-executable-in-service-fabric"></a>Vantaggi dell'esecuzione di un'eseguibile guest in Service Fabric
Esistono diversi vantaggi toorunning un eseguibile in un cluster di Service Fabric guest:

* Disponibilità elevata. Le applicazioni eseguite in Service Fabric sono rese altamente disponibili. Service Fabric garantisce che siano in esecuzione istanze dell'applicazione.
* Monitoraggio dell’integrità. Il monitoraggio dell'integrità di Service Fabric rileva se un'applicazione è in esecuzione e fornisce informazioni di diagnostica in caso di errore.   
* Gestione del ciclo di vita delle applicazioni. Oltre a fornire gli aggiornamenti senza tempi di inattività, Service Fabric fornisce una versione precedente di rollback automatico toohello se è presente un evento di stato errato segnalato durante un aggiornamento.    
* Densità. È possibile eseguire più applicazioni in un cluster, non è più necessario hello per ogni applicazione di toorun il proprio hardware.
* Individuabilità: Tramite REST è possibile chiamare toofind servizio di Service Fabric denominazione hello altri servizi in cluster hello. 

## <a name="samples"></a>Esempi
* [Esempio per la creazione di un pacchetto e distribuzione di un file guest eseguibile](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [Esempio di guest due file eseguibili (c# e nodejs) comunicano tramite il servizio di denominazione hello tramite REST](https://github.com/Azure-Samples/service-fabric-dotnet-containers)

## <a name="overview-of-application-and-service-manifest-files"></a>Panoramica dei file manifesto dell'applicazione e del servizio
Come parte della distribuzione di un eseguibile guest, è sui pacchetti di Service Fabric toounderstand utile hello e modello di distribuzione come descritto in [modello applicativo](service-fabric-application-model.md). un modello di Service Fabric pacchetti Hello si basa su due file XML: hello manifesti dell'applicazione e servizi. Hello definizione dello schema per hello ServiceManifest.xml e ApplicationManifest.xml file viene installata con hello Service Fabric SDK in *C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.

* **Manifesto dell'applicazione** manifesto dell'applicazione hello è un'applicazione hello toodescribe utilizzato. Elenca servizi hello che lo compongono e altri parametri che vengono utilizzati toodefine devono essere distribuiti come uno o più servizi, ad esempio il numero di hello di istanze.

  In Service Fabric un'applicazione è un'unità di distribuzione e aggiornamento. Un'applicazione può essere aggiornata come una singola unità in cui vengono gestiti i potenziali errori e i potenziali ripristini dello stato precedente. Service Fabric garantisce che il processo di aggiornamento hello sia l'esito è positivo, in alternativa, se l'aggiornamento di hello non riesce, non lasciare applicazione hello in uno stato sconosciuto o instabile.
* **Manifesto del servizio** manifesto del servizio hello descrive i componenti di hello di un servizio. Include i dati, ad esempio hello nome e tipo di servizio e il codice e la configurazione. Hello manifesto del servizio sono inclusi alcuni parametri aggiuntivi che possono essere utilizzati servizio hello tooconfigure dopo la distribuzione.

## <a name="application-package-file-structure"></a>Struttura del file del pacchetto dell'applicazione
toodeploy un tooService applicazione Fabric, un'applicazione hello deve seguire una struttura di directory predefinito. Hello Ecco un esempio di tale struttura.

```
|-- ApplicationPackageRoot
    |-- GuestService1Pkg
        |-- Code
            |-- existingapp.exe
        |-- Config
            |-- Settings.xml
        |-- Data
        |-- ServiceManifest.xml
    |-- ApplicationManifest.xml
```

Hello ApplicationPackageRoot contiene file ApplicationManifest XML hello che definisce un'applicazione hello. Una sottodirectory per ogni servizio incluso in un'applicazione hello è toocontain utilizzati tutti gli elementi necessari per il servizio hello di hello. Le sottodirectory sono hello ServiceManifest.xml e, in genere, hello seguenti:

* *Code*. Questa directory contiene codice hello del servizio.
* *Config*. Questa directory contiene un file Settings (e altri file, se necessario) che il servizio di hello può accedere al runtime tooretrieve specifiche impostazioni di configurazione.
* *Dati*. Si tratta di un'ulteriore directory toostore locale dati aggiuntivi che potrebbe essere necessario servizio hello. Dati dovrebbero essere utilizzati toostore temporaneo solo dati. Service Fabric non directory dei dati toohello le modifiche non copia o di replica se il servizio di hello deve toobe ripristinato (ad esempio, durante il failover).

> [!NOTE]
> Non si dispone di hello toocreate `config` e `data` directory se non sono necessarie.
>
>

## <a name="package-an-existing-executable"></a>Creare il pacchetto di un eseguibile esistente
Quando il pacchetto di un eseguibile guest, è possibile scegliere entrambi toouse un modello di progetto di Visual Studio o troppo[creare manualmente il pacchetto di applicazione hello](#manually). Utilizzando Visual Studio, hello struttura del pacchetto dell'applicazione e i file manifesto vengono creati per il nuovo modello di progetto hello.

> [!TIP]
> toopackage modo più semplice di Hello un eseguibile in un servizio di Windows esistente è toouse Visual Studio e su Linux toouse Yeoman
>

## <a name="use-visual-studio-toopackage-and-deploy-an-existing-executable"></a>Utilizzare Visual Studio toopackage e distribuire un eseguibile esistente
Visual Studio fornisce un'infrastruttura a servizio toohelp modello di servizio si distribuisce un cluster di Service Fabric tooa eseguibile guest.

1. Scegliere **File** > **Nuovo progetto** e creare un'applicazione di Service Fabric.
2. Scegliere **eseguibile Guest** come modello di servizio hello.
3. Fare clic su **Sfoglia** cartella hello tooselect e compilare il resto di hello del servizio di hello parametri toocreate hello eseguibile.
   * *Comportamento del pacchetto di codice*. È possibile toocopy set tutto il contenuto hello del toohello cartella progetto di Visual Studio, questa opzione è utile se hello eseguibile non cambia. Se si prevede che toochange eseguibile hello e si desidera hello possibilità toopick le nuove compilazioni in modo dinamico, è possibile scegliere invece toolink toohello cartella. Quando si crea il progetto di applicazione hello in Visual Studio, è possibile utilizzare cartelle collegate. Questo collega toohello un percorso di origine dal progetto hello, rendendo possibile il si tooupdate hello guest eseguibile di destinazione di origine. Tali aggiornamenti diventano parte del pacchetto di applicazione hello in fase di compilazione.
   * *Programma* eseguibile hello che deve essere eseguito il servizio di hello toostart specifica.
   * *Argomenti* specifica gli argomenti di hello che devono essere passati toohello eseguibile. Può essere un elenco di parametri con argomenti.
   * *Cartella di lavoro* specifica cartella di lavoro hello per processo hello che verrà avviato toobe. È possibile specificare tre valori:
     * `CodeBase`Specifica la directory di lavoro hello toobe impostare toohello directory del codice nel pacchetto di applicazione hello (`Code` directory visualizzata nella hello precedente struttura di file).
     * `CodePackage`Specifica la directory di lavoro hello toobe impostare toohello radice del pacchetto di applicazione hello (`GuestService1Pkg` mostrato nella precedente struttura di file hello).
     * `Work`Specifica che il file hello vengono inserito in una sottodirectory denominata lavoro.
4. Assegnare un nome al servizio e fare clic su **OK**.
5. Se il servizio deve disporre di un endpoint per la comunicazione, è ora possibile aggiungere hello protocollo, porta e il file ServiceManifest.xml toohello del tipo. Ad esempio: `<Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000" UriScheme="http" PathSuffix="myapp/" Type="Input" />`.
6. È possibile utilizzare il pacchetto di hello e azione di pubblicazione sul cluster locale eseguendo il debug delle soluzioni di hello in Visual Studio. Quando si è pronti, è possibile pubblicare hello applicazione tooa remota del cluster o archiviare hello soluzione toosource controllo del codice.
7. Passare come toohello fine di questo articolo di toosee tooview il servizio eseguibile guest in esecuzione in Service Fabric Explorer.

## <a name="use-yoeman-toopackage-and-deploy-an-existing-executable-on-linux"></a>Utilizzare Yoeman toopackage e distribuire un eseguibile esistente in Linux

procedura di Hello per la creazione e distribuzione di un eseguibile in Linux guest è hello come distribuzione di un'applicazione csharp o java.

1. In un terminale digitare `yo azuresfguest`.
2. Assegnare un nome all'applicazione.
3. Nome del servizio e fornire dettagli hello, incluso il percorso dell'eseguibile hello e devono essere richiamato con i parametri di hello.

Yeoman crea un pacchetto di applicazione con un'applicazione hello appropriato e i file manifesto insieme a installare e disinstallare gli script.

<a id="manually"></a>

## <a name="manually-package-and-deploy-an-existing-executable"></a>Creare manualmente il pacchetto e distribuire un eseguibile esistente
il processo di Hello di assemblaggio manualmente un eseguibile guest è basato su hello seguendo i passaggi generali:

1. Creare una struttura di directory hello del pacchetto.
2. Aggiungere il file di codice e la configurazione dell'applicazione hello.
3. Modificare i file manifesto del servizio hello.
4. Modificare i file manifesto dell'applicazione hello.

<!--
>[AZURE.NOTE] We do provide a packaging tool that allows you toocreate hello ApplicationPackage automatically. hello tool is currently in preview. You can download it from [here](http://aka.ms/servicefabricpacktool).
-->

### <a name="create-hello-package-directory-structure"></a>Creare una struttura di directory del pacchetto hello
Iniziare creando una struttura di directory hello, come descritto nella precedente sezione hello "Struttura di file del pacchetto di applicazione."

### <a name="add-hello-applications-code-and-configuration-files"></a>Aggiungere il file di codice e la configurazione dell'applicazione hello
Dopo aver creato la struttura di directory hello, è possibile aggiungere file di codice e la configurazione dell'applicazione hello nella directory di codice e configurazione di hello. È anche possibile creare directory aggiuntive o più sottodirectory nella directory di configurazione o del codice hello.

Service Fabric un `xcopy` del contenuto di hello di hello directory radice dell'applicazione pertanto non c'è nessun toouse struttura predefinita diversa da creare due directory superiore, codice e le impostazioni. (ma se si desidera, è possibile scegliere nomi diversi, Altri dettagli sono nella sezione successiva hello.)

> [!NOTE]
> Assicurarsi di includere tutti i file hello e le dipendenze che hello esigenze dell'applicazione. Service Fabric copia hello contenuto del pacchetto di applicazione hello in tutti i nodi nel cluster hello in cui i servizi dell'applicazione hello sono toobe corso distribuito. pacchetto di Hello contiene tutto il codice hello che un'applicazione hello deve toorun. Non presupporre che le dipendenze di hello siano già installate.
>
>

### <a name="edit-hello-service-manifest-file"></a>Modificare i file manifesto del servizio hello
passaggio successivo Hello è hello tooedit hello servizio file manifesto tooinclude con le seguenti informazioni:

* nome Hello hello del tipo di servizio. Questo è un ID di Service Fabric utilizzato tooidentify un servizio.
* comando toouse toolaunch hello applicazione Hello (ExeHost).
* Tutti gli script che deve eseguire toobe tooset di un'applicazione hello (SetupEntrypoint).

Hello seguito è riportato un esempio di un `ServiceManifest.xml` file:

```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Name="NodeApp" Version="1.0.0.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <ServiceTypes>
      <StatelessServiceType ServiceTypeName="NodeApp" UseImplicitHost="true"/>
   </ServiceTypes>
   <CodePackage Name="code" Version="1.0.0.0">
      <SetupEntryPoint>
         <ExeHost>
             <Program>scripts\launchConfig.cmd</Program>
         </ExeHost>
      </SetupEntryPoint>
      <EntryPoint>
         <ExeHost>
            <Program>node.exe</Program>
            <Arguments>bin/www</Arguments>
            <WorkingFolder>CodePackage</WorkingFolder>
         </ExeHost>
      </EntryPoint>
   </CodePackage>
   <Resources>
      <Endpoints>
         <Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000" Type="Input" />
      </Endpoints>
   </Resources>
</ServiceManifest>
```

Nelle sezioni che seguono Hello prese in parti diverse di hello del file hello che è necessario tooupdate.

#### <a name="update-servicetypes"></a>Aggiornare ServiceTypes
```xml
<ServiceTypes>
  <StatelessServiceType ServiceTypeName="NodeApp" UseImplicitHost="true" />
</ServiceTypes>
```

* È possibile scegliere qualsiasi nome per `ServiceTypeName`. viene utilizzato il valore di Hello in hello `ApplicationManifest.xml` tooidentify hello servizio file.
* Specificare `UseImplicitHost="true"`. Questo attributo indica a Service Fabric che servizio hello è basato su un'app autonoma, quindi tutti i Service Fabric deve toodo toolaunch come un processo e monitorare l'integrità.

#### <a name="update-codepackage"></a>Aggiornare CodePackage
elemento CodePackage Hello Specifica percorso hello (e versione) del codice del servizio hello.

```xml
<CodePackage Name="Code" Version="1.0.0.0">
```

Hello `Name` elemento è utilizzato toospecify hello nome della directory hello nel pacchetto di applicazione hello che contiene il codice del servizio hello. `CodePackage`dispone anche di hello `version` attributo. Questo può essere utilizzato toospecify hello versione del codice hello e possono anche essere utilizzato il codice del servizio di hello tooupgrade tramite l'infrastruttura di gestione del ciclo di vita dell'applicazione hello in Service Fabric.

#### <a name="optional-update-setupentrypoint"></a>Facoltativo: aggiornare SetupEntrypoint
```xml
<SetupEntryPoint>
   <ExeHost>
       <Program>scripts\launchConfig.cmd</Program>
   </ExeHost>
</SetupEntryPoint>
```
elemento SetupEntryPoint Hello è toospecify usato qualsiasi file eseguibile o batch che deve essere eseguito prima che il codice del servizio hello viene avviato. È un passaggio facoltativo, in modo che non sia toobe inclusa se non esiste alcuna inizializzazione necessaria. Hello SetupEntryPoint viene eseguita ogni volta che viene riavviato il servizio di hello.

Non è un solo SetupEntryPoint, gli script di installazione necessario toobe raggruppati in un file batch solo se il programma di installazione dell'applicazione hello richiede più script. Hello SetupEntryPoint può eseguire qualsiasi tipo di file: file eseguibili, file batch e i cmdlet di PowerShell. Per altri dettagli, vedere l'articolo su come [configurare SetupEntryPoint](service-fabric-application-runas-security.md).

In hello sopra riportato, hello SetupEntryPoint viene eseguito un file batch denominato `LaunchConfig.cmd` che è situato nella hello `scripts` sottodirectory della directory di codice hello (presupponendo che hello cartella di lavoro viene impostato tooCodeBase).

#### <a name="update-entrypoint"></a>Aggiornare EntryPoint
```xml
<EntryPoint>
  <ExeHost>
    <Program>node.exe</Program>
    <Arguments>bin/www</Arguments>
    <WorkingFolder>CodeBase</WorkingFolder>
  </ExeHost>
</EntryPoint>
```

Hello `EntryPoint` elemento nel file manifesto del servizio hello è toospecify utilizzati come servizio hello toolaunch. Hello `ExeHost` elemento specifica hello eseguibile (e argomenti) che deve essere utilizzato il servizio di hello toolaunch.

* `Program`Specifica il nome di hello del file eseguibile hello che deve avviare il servizio di hello.
* `Arguments`Specifica gli argomenti di hello che devono essere passati toohello eseguibile. Può essere un elenco di parametri con argomenti.
* `WorkingFolder`Specifica la directory di lavoro hello per processo hello che verrà avviato toobe. È possibile specificare tre valori:
  * `CodeBase`Specifica la directory di lavoro hello toobe impostare toohello directory del codice nel pacchetto di applicazione hello (`Code` directory hello precedente struttura di file).
  * `CodePackage`Specifica la directory di lavoro hello toobe impostare toohello radice del pacchetto di applicazione hello (`GuestService1Pkg` in hello precedente struttura di file).
    * `Work`Specifica che il file hello vengono inserito in una sottodirectory denominata lavoro.

cartella di lavoro Hello è directory di lavoro utile tooset hello corretto in modo che i percorsi relativi possono essere utilizzati da uno script di inizializzazione o di applicazione hello.

#### <a name="update-endpoints-and-register-with-naming-service-for-communication"></a>Aggiornare gli endpoint e registrarli nel servizio di denominazione per la comunicazione
```xml
<Endpoints>
   <Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000" Type="Input" />
</Endpoints>

```
In hello sopra riportato, hello `Endpoint` elemento specifica endpoint hello che un'applicazione hello può restare in ascolto. In questo esempio hello applicazione Node.js è in ascolto sul protocollo http sulla porta 3000.

Inoltre è possibile chiedere toopublish Service Fabric questo toohello endpoint servizio di denominazione in modo da altri servizi possono individuare servizio toothis indirizzo endpoint di hello. In questo modo toocommunicate in grado di toobe tra i servizi che sono file eseguibili di guest.
Hello pubblicato indirizzo dell'endpoint è formato hello `UriScheme://IPAddressOrFQDN:Port/PathSuffix`. `UriScheme` e `PathSuffix` sono attributi facoltativi. `IPAddressOrFQDN`è hello indirizzo IP o nome di dominio completo del nodo hello questo eseguibile vengono inserito in e viene calcolato automaticamente.

In hello riportato di seguito, una volta i servizi di hello viene distribuito, in Service Fabric Explorer visualizzato un endpoint simile troppo`http://10.1.4.92:3000/myapp/` pubblicati per l'istanza del servizio hello. Oppure, se si tratta di un computer locale, viene visualizzato `http://localhost:3000/myapp/`.

```xml
<Endpoints>
   <Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000"  UriScheme="http" PathSuffix="myapp/" Type="Input" />
</Endpoints>
```
È possibile utilizzare questi indirizzi con [proxy inverso](service-fabric-reverseproxy.md) toocommunicate tra servizi.

### <a name="edit-hello-application-manifest-file"></a>Modificare i file manifesto dell'applicazione hello
Dopo aver configurato hello `Servicemanifest.xml` file, è necessario toomake toohello alcune modifiche `ApplicationManifest.xml` file tooensure che hello vengono utilizzati il tipo di servizio e il nome corretto.

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="NodeAppType" ApplicationTypeVersion="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="NodeApp" ServiceManifestVersion="1.0.0.0" />
   </ServiceManifestImport>
</ApplicationManifest>
```

#### <a name="servicemanifestimport"></a>ServiceManifestImport
In hello `ServiceManifestImport` elemento, è possibile specificare uno o più servizi che si desidera tooinclude nell'app hello. Con cui vengono fatto riferimento servizi `ServiceManifestName`, che specifica il nome di hello della directory hello dove hello `ServiceManifest.xml` file si trova.

```xml
<ServiceManifestImport>
  <ServiceManifestRef ServiceManifestName="NodeApp" ServiceManifestVersion="1.0.0.0" />
</ServiceManifestImport>
```

## <a name="set-up-logging"></a>Configurare la registrazione
Per gli eseguibili di guest, è utile toobe toosee in grado di console registri toofind out se gli script di configurazione e applicazione hello mostrano eventuali errori.
È possibile configurare il reindirizzamento della console in hello `ServiceManifest.xml` file utilizzando hello `ConsoleRedirection` elemento.

> [!WARNING]
> Non utilizzare mai criterio di reindirizzamento console hello in un'applicazione che viene distribuita nell'ambiente di produzione, perché ciò può influire sul failover dell'applicazione hello. Usare questa opzione *solo* a scopo di sviluppo e debug locale.  
>
>

```xml
<EntryPoint>
  <ExeHost>
    <Program>node.exe</Program>
    <Arguments>bin/www</Arguments>
    <WorkingFolder>CodeBase</WorkingFolder>
    <ConsoleRedirection FileRetentionCount="5" FileMaxSizeInKb="2048"/>
  </ExeHost>
</EntryPoint>
```

`ConsoleRedirection`può essere una directory di lavoro tooa tooredirect utilizzato console output (stdout e stderr). In questo modo che non siano presenti errori durante l'installazione di hello o l'esecuzione di un'applicazione hello in cluster di Service Fabric hello tooverify possibilità hello.

`FileRetentionCount`Determina il numero di file viene salvato nella directory di lavoro hello. Un valore pari a 5, ad esempio, significa che i file di log hello per le esecuzioni precedenti cinque hello vengono archiviati nella directory di lavoro hello.

`FileMaxSizeInKb`Specifica dimensioni massime di hello hello dei file di log.

File di log vengono salvati in una directory di lavoro del servizio hello. toodetermine dove hello trovano i file, utilizzare toodetermine Service Fabric Explorer sia in esecuzione il servizio di hello nodo e la directory di lavoro viene utilizzata. Più avanti in questo articolo verrà illustrato questo processo.

## <a name="deployment"></a>Distribuzione
ultimo passaggio Hello è troppo[distribuire l'applicazione](service-fabric-deploy-remove-applications.md). Hello seguente mostra uno script di PowerShell come toodeploy il cluster di sviluppo locale toohello applicazione, quindi avviare un nuovo servizio Service Fabric.

```PowerShell

Connect-ServiceFabricCluster localhost:19000

Write-Host 'Copying application package...'
Copy-ServiceFabricApplicationPackage -ApplicationPackagePath 'C:\Dev\MultipleApplications' -ImageStoreConnectionString 'file:C:\SfDevCluster\Data\ImageStoreShare' -ApplicationPackagePathInImageStore 'nodeapp'

Write-Host 'Registering application type...'
Register-ServiceFabricApplicationType -ApplicationPathInImageStore 'nodeapp'

New-ServiceFabricApplication -ApplicationName 'fabric:/nodeapp' -ApplicationTypeName 'NodeAppType' -ApplicationTypeVersion 1.0

New-ServiceFabricService -ApplicationName 'fabric:/nodeapp' -ServiceName 'fabric:/nodeapp/nodeappservice' -ServiceTypeName 'NodeApp' -Stateless -PartitionSchemeSingleton -InstanceCount 1

```

>[!TIP]
> [Comprimere il pacchetto di hello](service-fabric-package-apps.md#compress-a-package) prima della copia di archivio di immagini toohello se il pacchetto di hello è grande o dispone di molti file. Per altre informazioni, leggere [qui](service-fabric-deploy-remove-applications.md#upload-the-application-package).
>

Un servizio Service Fabric può essere distribuito in varie "configurazioni", Ad esempio, può essere distribuito come una o più istanze, o può essere distribuito in modo che vi è un'istanza del servizio hello in ogni nodo del cluster di Service Fabric hello.

Hello `InstanceCount` parametro di hello `New-ServiceFabricService` cmdlet viene utilizzato toospecify il numero di istanze del servizio hello deve essere avviato nel cluster di Service Fabric hello. È possibile impostare hello `InstanceCount` valore, a seconda di tipo hello dell'applicazione che si desidera distribuire. gli scenari più comuni di Hello due sono:

* `InstanceCount = "1"`. In questo caso, solo un'istanza del servizio hello viene distribuita in cluster di hello. Utilità di pianificazione dell'infrastruttura servizio determina quale servizio hello nodo verrà distribuita in toobe.
* `InstanceCount ="-1"`. In questo caso, un'istanza del servizio hello viene distribuita in ogni nodo nel cluster di Service Fabric hello. risultato Hello è la presenza di istanze (un unico) del servizio di hello per ogni nodo nel cluster hello.

Infatti un'utile configurazione per le applicazioni front-end (ad esempio, un endpoint REST), le applicazioni client necessitano troppo "connettersi" tooany dei nodi di hello nell'endpoint di hello cluster toouse hello. Questa configurazione è utilizzabile anche quando, ad esempio, tutti i nodi del cluster di Service Fabric hello sono connessi tooa bilanciamento del carico. Il traffico client può quindi essere distribuito in servizio hello in esecuzione in tutti i nodi del cluster di hello.

## <a name="check-your-running-application"></a>Verificare l'applicazione in esecuzione
In Service Fabric Explorer, identificare il nodo hello in cui è in esecuzione il servizio di hello. In questo esempio è in esecuzione in Node1:

![Nodo in cui è in esecuzione il servizio](./media/service-fabric-deploy-existing-app/nodeappinsfx.png)

Se si passa toohello nodo e passare toohello applicazione, viene visualizzato informazioni essenziali nodo hello, incluso il percorso su disco.

![Percorso sul disco](./media/service-fabric-deploy-existing-app/locationondisk2.png)

Se si seleziona toohello directory tramite Esplora Server, è possibile trovare la directory di lavoro hello e la cartella di registro del servizio di hello, come illustrato nella seguente schermata hello: 

![Percorso del log](./media/service-fabric-deploy-existing-app/loglocation.png)

## <a name="next-steps"></a>Passaggi successivi
In questo articolo, si è appreso come toopackage un eseguibile guest e distribuirlo tooService dell'infrastruttura. Vedere i seguenti articoli per le informazioni correlate e attività hello.

* [Esempio per la creazione del package e distribuzione di un eseguibile guest](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started), tra cui una versione preliminare toohello collegamento dello strumento di creazione di pacchetti hello
* [Esempio di guest due file eseguibili (c# e nodejs) comunicano tramite il servizio di denominazione hello tramite REST](https://github.com/Azure-Samples/service-fabric-dotnet-containers)
* [Distribuire più eseguibili guest](service-fabric-deploy-multiple-apps.md)
* [Creare la prima applicazione Service Fabric in Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md)
