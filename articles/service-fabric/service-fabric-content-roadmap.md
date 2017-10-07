---
title: informazioni su Azure Service Fabric aaaLearn | Documenti Microsoft
description: "Informazioni sui concetti di base hello e le aree principali di Azure Service Fabric. Viene fornita una panoramica di Service Fabric estesa e la modalità toocreate microservizi."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/14/2017
ms.author: ryanwi
ms.openlocfilehash: 7fe8de777755be11635912613bb5b970e3fe3ea3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="so-you-want-toolearn-about-service-fabric"></a>Pertanto si toolearn sull'infrastruttura di servizio?
Azure Service Fabric è una piattaforma di sistemi distribuiti che rende facile toopackage, distribuire e gestire microservizi scalabili e affidabili.  Tuttavia, Service Fabric presenta una superficie di grandi dimensioni, ed è molto toolearn.  In questo articolo offre un riepilogo di Service Fabric e vengono descritti i concetti di base hello, modelli di programmazione, ciclo di vita dell'applicazione, test, i cluster e il monitoraggio dello stato. Hello lettura [Panoramica](service-fabric-overview.md) e [quali sono microservizi?](service-fabric-overview-microservices.md) per un'introduzione e come Service Fabric possano essere utilizzati toocreate microservizi. In questo articolo non contiene un elenco completo di contenuto, ma collegare toooverview e ottenere gli articoli avviati per ogni area di Service Fabric. 

## <a name="core-concepts"></a>Concetti principali
[Terminologia di Service Fabric](service-fabric-technical-overview.md), [modello applicativo](service-fabric-application-model.md), e [supportati i modelli di programmazione](service-fabric-choose-framework.md) forniscono ulteriori concetti e le descrizioni, ma Ecco nozioni di base hello.

<table><tr><th>Concetti principali</th><th>Fase di progettazione</th><th>Fase di esecuzione</th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=tbuZM46yC_5206218965">
<img src="./media/service-fabric-content-roadmap/CoreConceptsVid.png" WIDTH="240" HEIGHT="162"></a></td>
<td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=tlkI046yC_2906218965"><img src="./media/service-fabric-content-roadmap/RunTimeVid.png" WIDTH="240" HEIGHT="162"></a></td>
<td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=x7CVH56yC_1406218965">
<img src="./media/service-fabric-content-roadmap/RunTimeVid.png" WIDTH="240" HEIGHT="162"></a></td></tr>
</table>

### <a name="design-time-application-type-service-type-application-package-and-manifest-service-package-and-manifest"></a>Fase di progettazione: tipo di applicazione, tipo di servizio, manifesto e pacchetto dell'applicazione, manifesto e pacchetto del servizio
Un tipo di applicazione è hello. nome/versione assegnata tooa raccolta dei tipi di servizio. Questo viene definito in un file *ApplicationManifest.xml* incorporato in una directory del pacchetto dell'applicazione. Hello pacchetto di applicazione che viene quindi copiato archivio di immagini del cluster di Service Fabric toohello. È quindi possibile creare un'applicazione denominata da questo tipo di applicazione, che quindi viene eseguito all'interno di cluster hello. 

Un tipo di servizio è hello. nome/versione assegnato pacchetti di codice, i pacchetti di dati e pacchetti di configurazione del servizio tooa. Questo viene definito in un file ServiceManifest.xml incorporato in una directory del pacchetto del servizio. Hello directory del pacchetto del servizio viene quindi fatto riferimento da un pacchetto di applicazione *ApplicationManifest.xml* file. All'interno di cluster hello, dopo la creazione di un'applicazione denominata, è possibile creare un servizio denominato da una delle hello tipi di servizio del tipo di applicazione. Un tipo di servizio è descritto dal relativo file *ServiceManifest.xml*. tipo di servizio Hello è costituito da impostazioni di configurazione del servizio codice eseguibile, vengono caricate in fase di esecuzione, e i dati statici che viene utilizzati dal servizio hello.

![Tipi di applicazioni di Service Fabric e tipi di servizio][cluster-imagestore-apptypes]

pacchetto di applicazione Hello è una directory del disco contenente del tipo di applicazione hello *ApplicationManifest.xml* file, che fa riferimento a pacchetti hello del servizio per ogni tipo di servizio che costituisce il tipo di applicazione hello. Ad esempio, un pacchetto di applicazione per un tipo di applicazione di posta elettronica potrebbe contenere riferimenti tooa coda servizio pacchetto, un pacchetto del servizio front-end e un pacchetto del servizio di database. i file nella directory del pacchetto di applicazione hello Hello sono archivio di immagini del cluster di Service Fabric toohello copiato. 

Un pacchetto del servizio è una directory del disco contenente del tipo di servizio hello *ServiceManifest.xml* file, che fa riferimento a codice hello, dati statici e i pacchetti di configurazione per il tipo di servizio hello. i file nella directory del pacchetto del servizio hello Hello fanno riferimento del tipo di applicazione hello *ApplicationManifest.xml* file. Ad esempio, un pacchetto del servizio potrebbe fare riferimento a codice toohello, i dati statici e i pacchetti di configurazione che costituiscono un servizio di database.

### <a name="run-time-clusters-and-nodes-named-applications-named-services-partitions-and-replicas"></a>Fase di esecuzione: cluster e nodi, applicazioni denominate, servizi denominati, partizioni e repliche
Un [cluster di Service Fabric](service-fabric-deploy-anywhere.md) è un set di computer fisici o macchine virtuali connesse tramite rete in cui vengono distribuiti e gestiti i microservizi. I cluster possono essere ridimensionati toothousands macchine.

Un computer o una macchina virtuale che fa parte di un cluster viene chiamato nodo. A ogni nodo viene assegnato un nome (stringa). I nodi presentano delle caratteristiche, ad esempio le proprietà di posizionamento. In ogni computer o macchina virtuale è disponibile un servizio di avvio automatico di Windows, `FabricHost.exe`, che viene eseguito all'avvio e che a sua volta avvia due eseguibili: `Fabric.exe` e `FabricGateway.exe`. Questi due eseguibili costituiscono dal nodo hello. Negli scenari di sviluppo o test è possibile ospitare più nodi in un singolo PC o una singola VM eseguendo più istanze di `Fabric.exe` e `FabricGateway.exe`.

Un'applicazione denominata è una raccolta di servizi denominati che esegue una o più funzioni specifiche. Un servizio esegue una funzione completa e autonoma (avvio ed esecuzione indipendenti da altri servizi) ed è costituito da codice, configurazione e dati. Un pacchetto di applicazione, dopo aver copiato toohello archivio di immagini, creerai un'istanza di un'applicazione hello all'interno di cluster hello specificando il tipo di applicazione del pacchetto di applicazione hello (mediante il relativo nome/versione). A ogni istanza del tipo di applicazione viene assegnato un nome URI simile a *fabric:/MyNamedApp*. All'interno di un cluster è possibile creare più applicazioni denominate da un singolo tipo di applicazione. È anche possibile creare applicazioni denominate da tipi di applicazione diversi. L'amministrazione e il controllo delle versioni sono gestiti in modo indipendente per ogni applicazione.

Dopo aver creato un'applicazione denominata, è possibile creare un'istanza di uno dei relativi tipi di servizio (un servizio denominato) all'interno di cluster hello specificando il tipo di servizio hello (mediante il relativo nome/versione). A ogni istanza del tipo di servizio viene assegnato un nome URI con un ambito definito dall'URI della relativa applicazione denominata. Ad esempio, se si crea un servizio all'interno di un'applicazione denominata "MyNamedApp" denominato "MyDatabase", URI hello aspetto: *fabric: / MyNamedApp/MyDatabase*. All'interno di un'applicazione denominata è possibile creare uno o più servizi denominati. Ogni servizio denominato può avere uno schema di partizione e numeri di istanze/repliche specifici. 

Sono disponibili due tipi di servizi: con e senza stato. I servizi senza stato archiviano lo stato permanente in un servizio di archiviazione esterno, ad esempio Archiviazione di Azure, database SQL di Azure o Azure Cosmos DB. Utilizzare un servizio senza stato quando il servizio di hello non dispone di alcun archivio permanente affatto. Un servizio con stato utilizza Service Fabric toomanage lo stato del servizio tramite il relativo raccolte affidabile o Reliable Actors modelli di programmazione. 

Quando si crea un servizio denominato, è necessario specificare uno schema di partizione. I servizi con grandi quantità di stato divisione dei dati hello tra partizioni. Ogni partizione è responsabile di una parte di hello stato completo nello stato del servizio di hello, che viene distribuito tra i nodi del cluster hello. All'interno di una partizione, per i servizi denominati senza stato sono presenti istanze mentre per i servizi denominati con stato sono presenti repliche. In genere i servizi denominati senza stato avranno sempre una sola partizione, dal momento che non hanno uno stato interno. I servizi denominati con stato gestiscono il proprio stato all'interno delle repliche e ogni partizione contiene un set di repliche dedicato. Operazioni di lettura e scrittura vengono eseguite in una replica (denominata hello primario). Le modifiche toostate da operazioni di scrittura replicati toomultiple altre repliche (denominati repliche secondarie attive). 

Hello diagramma seguente mostra la relazione hello tra applicazioni e le istanze del servizio, partizioni e repliche.

![Partizioni e repliche in un servizio][cluster-application-instances]

### <a name="partitioning-scaling-and-availability"></a>Partizionamento, scalabilità e disponibilità
[Partizionamento](service-fabric-concepts-partitioning.md) non è univoco tooService dell'infrastruttura. Una forma molto conosciuta di partizionamento è il partizionamento dei dati o partizionamento orizzontale. Informazioni sullo stato dei servizi con grandi quantità di stato divisione dei dati hello tra partizioni. Ogni partizione è responsabile di una parte di hello stato completo nello stato del servizio hello. 

repliche di Hello di ogni partizione vengono distribuite tra i nodi del cluster di hello, che consente lo stato del servizio denominata troppo[scala](service-fabric-concepts-scalability.md). Come dati hello devono aumentare, le partizioni di aumento delle dimensioni e dell'infrastruttura di servizio eseguito il ribilanciamento delle partizioni tra utilizzo efficiente di toomake nodi delle risorse hardware. Se si aggiunge di nuovo cluster di nodi toohello, Service Fabric verrà ribilanciare le repliche delle partizioni hello hello aumentato in nodi. Generale consente di migliorare le prestazioni dell'applicazione e riduce la contesa tra toomemory di accesso. Se non vengono utilizzati i nodi nel cluster hello hello in modo efficiente, è possibile ridurre il numero di hello di nodi nel cluster hello. Service Fabric eseguito nuovamente il ribilanciamento delle repliche di partizione hello in serie hello ridotto di nodi toomake migliorare l'utilizzo dell'hardware hello in ogni nodo.

All'interno di una partizione, per i servizi denominati senza stato sono presenti istanze mentre per i servizi denominati con stato sono presenti repliche. In genere i servizi denominati senza stato avranno sempre una sola partizione, dal momento che non hanno uno stato interno. le istanze di partizione Hello forniscono per [disponibilità](service-fabric-availability-services.md). Se un'istanza, le altre istanze toooperate continuano a funzionare normalmente e quindi Service Fabric crea una nuova istanza. I servizi denominati con stato gestiscono il proprio stato all'interno delle repliche e ogni partizione contiene un set di repliche dedicato. Operazioni di lettura e scrittura vengono eseguite in una replica (denominata hello primario). Le modifiche toostate da operazioni di scrittura replicati toomultiple altre repliche (denominati repliche secondarie attive). Una replica avrà esito negativo, Service Fabric crea una nuova replica da repliche esistenti hello.

## <a name="stateless-and-stateful-microservices-for-service-fabric"></a>Microservizi con e senza stato per Service Fabric
Service Fabric consente applicazioni toobuild costituiti microservizi o contenitori. Uno stato modificabile all'esterno di una richiesta e la risposta dal servizio hello non conservano microservizi senza stati (ad esempio i gateway di protocollo e il proxy web). I ruoli di lavoro di Servizi cloud di Azure sono un esempio di servizio senza stato. Informazioni sullo stato microservizi (ad esempio gli account utente, database, i dispositivi, carrelli della spesa e code) mantengono uno stato modificabile, autorevole oltre hello richiesta e la risposta. Le attuali applicazioni su scala Internet sono costituite da una combinazione di microservizi con e senza stato. 

Una chiave differentation con Service Fabric è incentrato sulla generazione di servizi con stati, con hello [compilato nei modelli di programmazione ](service-fabric-choose-framework.md) o con i servizi con stati nei contenitori. Hello [scenari applicativi](service-fabric-application-scenarios.md) vengono descritti gli scenari di hello in cui vengono utilizzati i servizi con stato.

Perché è presente con stato microservizi insieme a quelli senza stati? Hello per due motivi principali sono:

* È possibile compilare una velocità effettiva elevata, bassa latenza, l'elaborazione a tolleranza di errore delle transazioni online (OLTP) di servizi da mantenere codice e dati chiudere hello nello stesso computer. Alcuni esempi sono le vetrine interattive, le ricerche, i sistemi Internet delle cose (IoT), i sistemi di trading, l'elaborazione delle carte di credito, i sistemi di rilevamento di frodi e la gestione dei record personali.
* È possibile semplificare la progettazione dell'applicazione. Con stati microservizi rimuovere necessità hello per le code aggiuntive e memorizza nella cache, che sono in genere i requisiti di tooaddress hello disponibilità e la latenza di un'applicazione puramente senza stata. Naturalmente, i servizi con stati sono a disponibilità elevata e a bassa latenza, riducendo il numero di hello di toomanage lo spostamento di parti dell'applicazione nel suo complesso.

## <a name="supported-programming-models"></a>Modelli di programmazione supportati
Infrastruttura del servizio sono disponibili più modi toowrite e gestire i servizi. Servizi possono utilizzare hello API dei servizi dell'infrastruttura tootake appieno le funzionalità della piattaforma hello e Framework. I servizi possono essere anche qualsiasi programma eseguibile compilato scritto in qualsiasi linguaggio e ospitato in un cluster di Service Fabric. Per altre informazioni, vedere l'articolo relativo ai [modelli di programmazione supportati](service-fabric-choose-framework.md).

### <a name="containers"></a>Contenitori
Per impostazione predefinita, Service Fabric distribuisce e attiva i servizi come processi. Service Fabric può anche distribuire servizi in [contenitori](service-fabric-containers-overview.md). Inoltre, è possibile combinare i servizi nei processi e servizi in contenitori hello stessa applicazione. Service Fabric supporta la distribuzione di contenitori di Linux e contenitori di Windows in Windows Server 2016. È possibile distribuire applicazioni esistenti, servizi senza stato o servizi con stato in contenitori. 

### <a name="reliable-services"></a>Reliable Services
[Servizi affidabili](service-fabric-reliable-services-introduction.md) è un framework semplice per la scrittura di servizi che si integrano con la piattaforma Service Fabric hello e trarre vantaggio dal set completo di hello di funzionalità della piattaforma. Servizi affidabili possono essere eseguiti senza stato (simile toomost servizio piattaforme, ad esempio server web o ruoli di lavoro in servizi Cloud di Azure), in cui lo stato viene mantenuto in una soluzione esterna, ad esempio database di Azure o l'archiviazione tabelle di Azure. Servizi affidabili possono inoltre essere con stato, in cui lo stato mantenuto direttamente nel servizio hello utilizzando raccolte affidabile. Lo stato viene reso [altamente disponibile](service-fabric-availability-services.md) tramite la replica e distribuito tramite [partizionamento](service-fabric-concepts-partitioning.md), il tutto gestito automaticamente da Service Fabric.

### <a name="reliable-actors"></a>Reliable Actors
Basato su servizi affidabili, hello [Reliable Actor](service-fabric-reliable-actors-introduction.md) framework è un framework di un'applicazione che implementa il pattern Actor virtuale hello, basato sul modello di progettazione di hello attore. il framework di Reliable Actor Hello utilizza unità indipendenti di calcolo e di stato con l'esecuzione a thread singolo chiamati attori. Hello Reliable Actor framework fornisce compilato in comunicazione per gli attori e la persistenza dello stato predefinito e le configurazioni di scalabilità orizzontale.

### <a name="aspnet-core"></a>ASP.NET Core
Service Fabric è integrato con [ASP.NET Core](service-fabric-reliable-services-communication-aspnetcore.md) come modello di programmazione di prima classe per la creazione di applicazioni Web e API

### <a name="guest-executables"></a>Eseguibili guest
Un [eseguibile guest](service-fabric-deploy-existing-app.md) è un eseguibile arbitrario esistente, scritto in un qualsiasi linguaggio, ospitato in un cluster di Service Fabric insieme ad altri servizi. Gli eseguibili guest non si integrano direttamente con le API di Service Fabric. Tuttavia sono ancora trarre vantaggio dalle funzionalità hello offerte della piattaforma, ad esempio stato personalizzato e caricare report e individuazione del servizio chiamando le API REST. Gli eseguibili guest dispongono anche di supporto completo del ciclo di vita dell'applicazione. 

## <a name="application-lifecycle"></a>Ciclo di vita dell'applicazione
Come con altre piattaforme, un'applicazione in Service Fabric solitamente passa attraverso hello seguenti fasi: progettazione, sviluppo, test, distribuzione, aggiornamento, manutenzione e la rimozione. Service Fabric fornisce supporto di livello superiore per hello intero ciclo di vita delle applicazioni cloud, dallo sviluppo, distribuzione, gestione quotidiana e la rimozione delle autorizzazioni tooeventual di manutenzione. modello di servizio Hello consente diversi ruoli diversi tooparticipate in modo indipendente nel ciclo di vita dell'applicazione hello. [Ciclo di vita dell'applicazione Service Fabric](service-fabric-application-lifecycle.md) fornisce una panoramica di hello API e come vengono utilizzati da diversi ruoli di hello durante le fasi del ciclo di vita dell'applicazione hello Service Fabric hello. 

ciclo di vita di Hello intera app può essere gestito mediante [i cmdlet di PowerShell](/powershell/module/ServiceFabric/), [API c#](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient), [API Java](/java/api/system.fabric._application_management_client), e [API REST](/rest/api/servicefabric/). È possibile anche configurare pipeline di distribuzione/integrazione continua con strumenti quali [Visual Studio Team Services](service-fabric-set-up-continuous-integration.md) o [Jenkins](service-fabric-cicd-your-linux-java-application-with-jenkins.md).

Hello video Microsoft Virtual Academy seguente viene descritto come toomanage ciclo di vita dell'applicazione:<center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=My3Ka56yC_6106218965">
<img src="./media/service-fabric-content-roadmap/AppLifecycleVid.png" WIDTH="360" HEIGHT="244">
</a></center>

## <a name="test-applications-and-services"></a>Testare applicazioni e servizi
toocreate realmente a livello di cloud services, è tooverify critiche che le applicazioni e servizi in grado di resistere errori reali. Hello errore Analysis Services è progettato per il test di servizi che vengono compilati in Service Fabric. Con hello [errore Analysis Service](service-fabric-testability-overview.md), è possibile provocare errori significativi ed eseguire gli scenari dei test completa rispetto alle applicazioni. Questi errori e gli scenari di esercizio e convalidare hello numerosi Stati e transizioni che un servizio si verifica in tutta la durata, in modo controllato, sicuro e coerenza.

Le [azioni](service-fabric-testability-actions.md) vengono usate su un servizio a scopo di test mediante singoli errori. Uno sviluppatore del servizio è possibile utilizzare queste informazioni come blocchi predefiniti toowrite complicato scenari. Esempi di errori simulati sono:

* Riavviare toosimulate un nodo qualsiasi numero di situazioni in cui viene riavviato un computer o macchina virtuale.
* Spostare una replica del servizio con stato toosimulate il bilanciamento del carico, il failover o aggiornamento dell'applicazione.
* Richiamare perdita del quorum in un toocreate di servizio con stato una situazione in cui le operazioni di scrittura non possono continuare perché non vi sono dati abbastanza nuovi tooaccept repliche "backup" o "secondario".
* Richiamare la perdita di dati in un toocreate di servizio con stato una situazione in cui tutti gli stati in memoria sono completamente cancellati out.

Gli [scenari](service-fabric-testability-scenarios.md) sono operazioni complesse costituite da una o più azioni. Hello errore Analysis Services sono disponibili due scenari completi predefiniti:

* [Scenario CHAOS](service-fabric-controlled-chaos.md)-simula errori interleaved, continui (normale e anomali) in cluster hello per periodi prolungati di tempo.
* [Scenario di failover](service-fabric-testability-scenarios.md#failover-test)-una versione di uno scenario di test chaos hello destinato a una partizione di servizio specifico mantenendo invariata altri servizi.

## <a name="clusters"></a>Cluster
Un [cluster di Service Fabric](service-fabric-deploy-anywhere.md) è un set di computer fisici o macchine virtuali connesse tramite rete in cui vengono distribuiti e gestiti i microservizi. I cluster possono essere ridimensionati toothousands macchine. Un computer o una VM che fa parte di un cluster è chiamato nodo del cluster. A ogni nodo viene assegnato un nome (stringa). I nodi presentano delle caratteristiche, ad esempio le proprietà di posizionamento. In ogni computer o VM è disponibile un servizio di avvio automatico, `FabricHost.exe`, che viene eseguito all'avvio e che a sua volta avvia due eseguibili: Fabric.exe e FabricGateway.exe. Questi due eseguibili costituiscono dal nodo hello. Negli scenari di test è possibile ospitare più nodi in un singolo PC o una singola macchina virtuale eseguendo più istanze di `Fabric.exe` e `FabricGateway.exe`.

È possibile creare cluster di Service Fabric su qualsiasi macchina virtuale o computer che esegue Windows Server o Linux. Si sono in grado di toodeploy ed esecuzione di applicazioni di Service Fabric in qualsiasi ambiente in cui si dispone di un set di computer Windows Server o Linux che sono collegate tra loro: locale, in Microsoft Azure o su qualsiasi provider di cloud.

Hello video Microsoft Virtual Academy seguente vengono descritti i cluster di Service Fabric:<center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=tbuZM46yC_5206218965">
<img src="./media/service-fabric-content-roadmap/ClusterOverview.png" WIDTH="360" HEIGHT="244">
</a></center>

### <a name="clusters-on-azure"></a>Cluster in Azure
I cluster di Service Fabric in esecuzione in Azure forniscono l'integrazione con altre funzionalità di Azure e servizi, che rende le operazioni e gestione di cluster hello più semplice e affidabile. Un cluster è una risorsa di Azure Resource Manager, pertanto è possibile modellare i cluster come qualsiasi altra risorsa in Azure. Gestione risorse consente anche una gestione semplificata di tutte le risorse usate dal cluster hello come singola unità. I cluster in Azure sono integrati con la diagnostica di Azure e Log Analytics. Poiché i tipi di nodo del cluster sono [set di scalabilità di macchina virtuale](/azure/virtual-machine-scale-sets/index), la funzionalità di scalabilità automatica è incorporata.

È possibile creare un cluster in Azure tramite hello [portale di Azure](service-fabric-cluster-creation-via-portal.md), da un [modello](service-fabric-cluster-creation-via-arm.md), o da [Visual Studio](service-fabric-cluster-creation-via-visual-studio.md).

Anteprima di Hello di Service Fabric in Linux consente toobuild, distribuire e gestire applicazioni a disponibilità elevata, estremamente scalabile in Linux, esattamente come in Windows. Framework di Service Fabric Hello (servizi affidabili e Reliable Actors) sono disponibili in Java su Linux, in aggiunta tooC # (.NET Core). È anche possibile compilare [servizi eseguibili guest](service-fabric-deploy-existing-app.md) con qualsiasi linguaggio o framework. Inoltre, anteprima hello supporta anche l'orchestrazione contenitori Docker. Contenitori di docker è possono eseguire file eseguibili guest o i servizi di Service Fabric nativi, che utilizzano il framework di Service Fabric hello. Per altre informazioni, vedere [Service Fabric in Linux](service-fabric-linux-overview.md).

Poiché Service Fabric in Linux è un'anteprima, alcune funzionalità sono supportate in Windows, ma non in Linux. leggere più, toolearn [differenze tra Service Fabric in Linux e Windows](service-fabric-linux-windows-differences.md).

### <a name="standalone-clusters"></a>Cluster autonomi
Service Fabric fornisce un pacchetto di installazione per si toocreate autonoma dell'infrastruttura del servizio cluster locale o su qualsiasi provider di cloud. Autonomo cluster si hello libertà toohost un cluster, ogni volta che si desidera assegnare. Se i dati sono soggetto toocompliance o restrizioni alle normative, o si desidera tookeep dati locale, è possibile ospitare la propria cluster e le applicazioni. Applicazioni di Service Fabric è possono eseguire in più ambienti di hosting senza modifiche, viene mantenuta la conoscenza di compilazione di applicazioni da un tooanother ambiente host. 

[Creare il primo cluster autonomo di Service Fabric](service-fabric-get-started-standalone-cluster.md)

I cluster Linux autonomi non sono ancora supportati.

### <a name="cluster-security"></a>Sicurezza del cluster
I cluster devono essere utenti di tooprevent protetto non autorizzato dalla connessione tooyour cluster, in particolare quando dispone i carichi di lavoro in esecuzione su di esso. Sebbene sia possibile toocreate un cluster non protetto, in questo modo consente agli utenti anonimi tooconnect tooit se gli endpoint di gestione sono esposti toohello rete internet pubblica. Non è possibile toolater Abilita protezione in un cluster non protetta: protezione del cluster è abilitata al momento della creazione del cluster.

scenari di sicurezza cluster Hello sono:
* Sicurezza da nodo a nodo
* Sicurezza da client a nodo
* Controllo degli accessi in base al ruolo

Per altre informazioni, vedere [Proteggere un cluster](service-fabric-cluster-security.md).

### <a name="scaling"></a>Ridimensionamento
Se si aggiunge di nuovo cluster di nodi toohello, Service Fabric eseguito il ribilanciamento delle istanze e le repliche delle partizioni hello hello aumentato in nodi. Generale consente di migliorare le prestazioni dell'applicazione e riduce la contesa tra toomemory di accesso. Se non vengono utilizzati i nodi nel cluster hello hello in modo efficiente, è possibile ridurre il numero di hello di nodi nel cluster hello. Service Fabric eseguito nuovamente il ribilanciamento delle repliche di partizione hello e istanze in numero hello ridotto di nodi toomake meglio di hardware hello in ogni nodo. È possibile scalare i cluster in Azure [manualmente](service-fabric-cluster-scale-up-down.md) o [a livello di codice](service-fabric-cluster-programmatic-scaling.md). I cluster autonomi possono essere scalati [manualmente](service-fabric-cluster-windows-server-add-remove-nodes.md).

### <a name="cluster-upgrades"></a>Aggiornamenti dei cluster
Periodicamente, vengono rilasciate nuove versioni del runtime di Service Fabric hello. Eseguire gli aggiornamenti del runtime o dell'infrastruttura nel cluster in modo che sia sempre in esecuzione una [versione supportata](service-fabric-support.md). Toofabric consente inoltre di aggiornare, è inoltre possibile aggiornare la configurazione del cluster, ad esempio i certificati o alle porte dell'applicazione.

Un cluster di Service Fabric è una risorsa di proprietà dell'utente parzialmente gestita da Microsoft. Microsoft è responsabile dell'applicazione di patch hello sottostante del sistema operativo e l'esecuzione di aggiornamenti dell'infrastruttura nel cluster. È possibile impostare gli aggiornamenti, l'infrastruttura di cluster tooreceive automatico quando Microsoft rilascia una nuova versione, o scegliere tooselect una versione supportata dell'infrastruttura che si desidera. Gli aggiornamenti dell'infrastruttura e la configurazione possono essere impostati tramite hello portale di Azure o tramite Gestione risorse. Per altre informazioni, vedere [Aggiornare un cluster di Service Fabric](service-fabric-cluster-upgrade.md). 

Un cluster autonomo è una risorsa che si possiede interamente. È responsabile per l'applicazione di patch hello sottostante del sistema operativo e avviare gli aggiornamenti dell'infrastruttura. Se il cluster è possibile connettersi troppo[https://www.microsoft.com/download](https://www.microsoft.com/download), è possibile impostare il download di tooautomatically cluster e il provisioning hello nuova Service Fabric pacchetto di runtime. È quindi avvia l'aggiornamento di hello. Se il cluster non può accedere [https://www.microsoft.com/download](https://www.microsoft.com/download), è possibile scaricare manualmente il nuovo pacchetto di runtime hello da un computer connesso a internet e quindi avviare l'aggiornamento di hello. Per altre informazioni, vedere [Aggiornare il cluster autonomo di Azure Service Fabric in Windows Server](service-fabric-cluster-upgrade-windows-server.md).

## <a name="health-monitoring"></a>Monitoraggio dell’integrità
Service Fabric introduce un [modello di integrità](service-fabric-health-introduction.md) progettato tooflag integro cluster e le condizioni di applicazione per entità specifiche (ad esempio i nodi del cluster e le repliche del servizio). modello di integrità Hello utilizza reporters integrità (componenti di sistema e watchdog). obiettivo di Hello è ripristino e diagnostica rapida e semplice. Gli autori del servizio necessario toothink anticipo sull'integrità e la modalità troppo[Progettazione report di integrità](service-fabric-report-health.md#design-health-reporting). Qualsiasi condizione che può influire sull'integrità deve essere segnalati, soprattutto se ciò consente di chiudere toohello radice dei problemi di flag. informazioni sull'integrità Hello risparmiare tempo e impegno nel debug e analisi una volta hello servizio sia attivo e in esecuzione su larga scala nell'ambiente di produzione.

monitoraggio di Hello Service Fabric reporters identificato le condizioni di interesse. Generano report su tali condizioni in base alla visualizzazione locale. Hello [archivio integrità](service-fabric-health-introduction.md#health-store) aggrega i dati di integrità inviati da toodetermine reporters tutte le entità sono integra globale. modello di Hello è previsto toobe RTF, flessibili e semplici toouse. qualità Hello di report sull'integrità hello determina la precisione di visualizzazione dell'integrità del cluster hello hello hello. I falsi positivi che visualizzano erroneamente problemi di non integrità possono influire negativamente sugli aggiornamenti o su altri servizi che usano i dati di integrità, come ad esempio i servizi di ripristino e i meccanismi di avviso. Pertanto, valutare diversi aspetti sono tooprovide necessari report che consentono di acquisire le condizioni di interesse in hello migliore dei modi possibili.

I report possono essere creati da:
* Hello monitorati replica del servizio Service Fabric o istanza.
* Watchdog interni distribuiti come servizio di Service Fabric, ad esempio un servizio senza stato di Service Fabric che monitora le condizioni e genera i report. watchdog Hello possono essere distribuiti in tutti i nodi o può essere creata toohello monitorato servizio.
* Watchdog interno che eseguite nei nodi di Service Fabric hello tuttavia non sono implementati come servizi di Service Fabric.
* Esterno watchdogs probe hello risorsa dal cluster di Service Fabric hello esterno (ad esempio, servizio di monitoraggio come Gomez).

Predefinito hello, i componenti di Service Fabric report integrità di tutte le entità nel cluster hello. I [report sull'integrità del sistema](service-fabric-understand-and-troubleshoot-with-system-health-reports.md) forniscono la visibilità delle funzionalità del cluster e dell'applicazione e contrassegnano i problemi riscontrati a livello di integrità. Per servizi e applicazioni, rapporti di integrità di sistema verificare che le entità vengono implementate e corretto dal punto di vista di hello del runtime di Service Fabric hello. i report di Hello non forniscono un monitoraggio integrità hello logica di business del servizio hello o rilevare i processi bloccati. la logica del servizio di tooadd integrità informazioni tooyour specifico, [implementare report di integrità personalizzato](service-fabric-report-health.md) nei servizi.

Infrastruttura del servizio sono disponibili diversi metodi troppo[visualizzare rapporti di stato](service-fabric-view-entities-aggregated-health.md) aggregati nell'archivio integrità hello:
* [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) o altri strumenti di visualizzazione.
* Query sull'integrità (tramite [PowerShell](/powershell/module/ServiceFabric/), hello [c# FabricClient APIs](/api/system.fabric.fabricclient.healthclient) e [Java FabricClient APIs](/java/api/system.fabric._health_client), o [API REST](/rest/api/servicefabric)).
* Query generale che restituiscono un elenco di entità che include l'integrità come una delle proprietà di hello (tramite PowerShell, API hello o REST).

Hello che seguente Microsoft Virtual Academy video descrive modello di integrità di Service Fabric hello e modalità di utilizzo:<center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=tevZw56yC_1906218965">
<img src="./media/service-fabric-content-roadmap/HealthIntroVid.png" WIDTH="360" HEIGHT="244">
</a></center>

## <a name="next-steps"></a>Passaggi successivi
* Informazioni su come toocreate un [cluster in Azure](service-fabric-cluster-creation-via-portal.md) o [autonomo cluster in Windows](service-fabric-cluster-creation-for-windows-server.md).
* Provare a creare un servizio utilizzando hello [servizi affidabili](service-fabric-reliable-services-quick-start.md) o [Reliable Actors](service-fabric-reliable-actors-get-started.md) modelli di programmazione.
* Informazioni su come troppo[esegue la migrazione da servizi Cloud](service-fabric-cloud-services-migration-differences.md).
* Informazioni su troppo[monitoraggio e diagnosi servizi](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md). 
* Informazioni su troppo[testare le App e servizi](service-fabric-testability-overview.md).
* Informazioni su troppo[gestire e orchestrare le risorse cluster](service-fabric-cluster-resource-manager-introduction.md).
* Esaminare hello [esempi di Service Fabric](http://aka.ms/servicefabricsamples).
* Informazioni sulle [opzioni di supporto di Service Fabric](service-fabric-support.md).
* Hello lettura [blog del team](https://blogs.msdn.microsoft.com/azureservicefabric/) per gli articoli e gli annunci.


[cluster-application-instances]: media/service-fabric-content-roadmap/cluster-application-instances.png
[cluster-imagestore-apptypes]: ./media/service-fabric-content-roadmap/cluster-imagestore-apptypes.png
