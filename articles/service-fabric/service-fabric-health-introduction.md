---
title: Nell'infrastruttura del servizio di monitoraggio aaaHealth | Documenti Microsoft
description: Un'introduzione toohello Azure Service Fabric. monitoraggio dello stato di modello, che fornisce il monitoraggio dei cluster hello e relativi servizi e applicazioni.
services: service-fabric
documentationcenter: .net
author: oanapl
manager: timlt
editor: 
ms.assetid: 1d979210-b1eb-4022-be24-799fd9d8e003
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/19/2017
ms.author: oanapl
ms.openlocfilehash: 904f36374ca6ca7e4caa1d43c92584e7e4c50087
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooservice-fabric-health-monitoring"></a>Il monitoraggio dello stato dell'infrastruttura di introduzione tooService
Con Azure Service Fabric è stato introdotto un modello di integrità che offre funzionalità di valutazione e reporting dell'integrità dettagliate, flessibili ed estendibili. modello Hello consente il monitoraggio in tempo quasi reale dello stato di hello del cluster di hello e servizi hello in esecuzione. Questo consente di ottenere facilmente informazioni relative all'integrità e correggere i potenziali problemi prima che si propaghino a catena e causino un numero elevato di interruzioni. Nel tipico modello di hello, servizi di inviare i report in base a osservazioni locale e che le informazioni aggregate tooprovide una vista complessiva del cluster a livello.

I componenti di Service Fabric utilizzano questo tooreport modello di integrità RTF lo stato corrente. È possibile utilizzare hello stesso stato di tooreport meccanismo dalle applicazioni. Investendo nella creazione di report sull'integrità di alta qualità con acquisizione delle proprie condizioni personalizzate, è possibile rilevare e risolvere i problemi dell'applicazione in esecuzione con maggiore facilità.

Hello che seguente Microsoft Virtual Academy video descrive anche modello di integrità di Service Fabric hello e modalità di utilizzo:<center><a target="_blank" href="https://mva.microsoft.com/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=tevZw56yC_1906218965">
<img src="./media/service-fabric-health-introduction/HealthIntroVid.png" WIDTH="360" HEIGHT="244">
</a></center>

> [!NOTE]
> Abbiamo iniziato hello integrità sottosistema tooaddress la necessità di aggiornamenti monitorati. Service Fabric fornisce aggiornamenti dell'applicazione e i cluster monitorati che non garantiscono disponibilità completa, i tempi di inattività e toono minimo l'intervento dell'utente. tooachieve questi obiettivi, l'aggiornamento di hello controlla lo stato in base a configurata i criteri di aggiornamento. Un aggiornamento può continuare solo quando l'integrità rientra nelle soglie desiderate. In caso contrario, l'aggiornamento di hello è sia eseguito automaticamente il rollback o sospesa toogive amministratori i problemi di hello toofix una possibilità. toolearn ulteriori informazioni sugli aggiornamenti dell'applicazione, vedere [questo articolo](service-fabric-application-upgrade.md).
> 
> 

## <a name="health-store"></a>Archivio integrità
archivio integrità Hello mantiene informazioni relative alla integrità entità cluster hello per assicurare un semplice recupero e valutazione. Viene implementato come un'infrastruttura del servizio persistente scalabilità e disponibilità elevata tooensure di servizio con stato. archivio integrità Hello fa parte di hello **fabric: / sistema** applicazione e è disponibile quando hello cluster sia attivo e in esecuzione.

## <a name="health-entities-and-hierarchy"></a>Entità e gerarchia di integrità
entità integrità Hello sono organizzate in una gerarchia logica che acquisisce le interazioni e le dipendenze tra entità diverse. archivio integrità Hello compila automaticamente le entità di integrità e della gerarchia in base ai report ricevuti dai componenti di Service Fabric.

entità integrità Hello rispecchiano le entità di Service Fabric hello. (Ad esempio, **entità applicazione integrità** corrisponde a un'istanza dell'applicazione durante la distribuzione in cluster hello, **entità nodo integrità** corrisponde a un nodo di cluster Service Fabric.) acquisisce gerarchia integrità hello interazioni di Hello di entità di sistema hello e è la base di hello per la valutazione dell'integrità avanzate. Per informazioni sui concetti chiave di Service Fabric, vedere la [panoramica tecnica di Service Fabric](service-fabric-technical-overview.md). Per altre informazioni sull'applicazione, vedere il [modello di applicazione di Service Fabric](service-fabric-application-model.md).

gerarchia e le entità di integrità hello consente hello cluster e le applicazioni toobe segnalato in modo efficace, eseguire il debug e monitorati. fornisce un accurato, il modello di integrità Hello *granulare* integrità hello di hello molte parti mobili cluster hello.

![Entità di integrità.][1]
entità integrità Hello, organizzate in una gerarchia in base alle relazioni padre-figlio.

[1]: ./media/service-fabric-health-introduction/servicefabric-health-hierarchy.png

entità integrità Hello sono:

* **Cluster**. Rappresenta l'integrità di hello di un cluster di Service Fabric. Report sull'integrità del cluster descrivere le condizioni che influiscono sull'intero cluster hello. Queste condizioni interessano più entità nello hello cluster o cluster di hello stesso. In base a condizione di hello, reporter hello non è possibile limitare problema hello verso il basso tooone o più figli non integri. Gli esempi includono cervello hello del cluster di hello divisione a causa di problemi di comunicazione o di partizionamento toonetwork.
* **Nodo**. Rappresenta l'integrità di hello di un nodo di Service Fabric. Rapporti di stato nodo descrivono le condizioni che influiscono sulle funzionalità di nodo hello. In genere influiscono tutte le entità hello distribuito in esecuzione su di esso. Ad esempio, un nodo con spazio su disco non sufficiente o con problemi relativi ad altre proprietà a livello di computer, come la memoria o le connessioni, oppure la presenza di un nodo non attivo. entità nodo Hello è identificato dal nome del nodo hello (stringa).
* **Applicazione**. Rappresenta l'integrità di hello di un'istanza di applicazione in esecuzione in cluster hello. Integrità applicazione segnala descrivere le condizioni che influiscono sulla hello andamento di un'applicazione hello. Essi non è possibile restringere l'ambito tooindividual figli (servizi o applicazioni distribuite). Ad esempio l'interazione di hello end-to-end tra servizi diversi in un'applicazione hello. entità applicazione Hello è identificata dal nome dell'applicazione hello (URI).
* **Servizio**. Rappresenta l'integrità di hello di un servizio in esecuzione in cluster hello. Stato servizio segnala descrivere le condizioni che influiscono sulla hello integrità complessiva del servizio hello. reporter Hello non è possibile restringere partizione non integro di hello problema tooan o replica. Ad esempio, indicano una configurazione del servizio, una porta o una condivisione file esterna, che causa problemi a tutte le partizioni. entità servizio Hello è identificata dal nome del servizio hello (URI).
* **Partizione**. Rappresenta una partizione del servizio di integrità hello. Report sull'integrità partizione descrivere le condizioni che influiscono sulla hello intero set di repliche. Ad esempio quando il numero di hello di repliche è inferiore al conteggio di destinazione e quando una partizione è perso il quorum. entità partizione Hello è identificato dalla partizione hello ID (GUID).
* **Replica**. Rappresenta l'integrità di hello di una replica del servizio con stato o un'istanza del servizio senza stato. replica Hello è l'unità più piccola hello watchdog e componenti di sistema possono segnalare per un'applicazione. Per i servizi con stati, gli esempi includono una replica primaria che non è possibile replicare le operazioni toosecondaries e replica lenta. Un'istanza senza stato può segnalare se le risorse si stanno esaurendo o se presenta problemi di connettività. entità di replica Hello è identificato da hello partizione ID (GUID) e hello replica o istanza ID (long).
* **Applicazione distribuita**. Rappresenta hello integrità di un *applicazione in esecuzione su un nodo*. Rapporti di stato di applicazione distribuita descrivono applicazione toohello specifiche condizioni nel nodo hello che non è possibile restringere l'ambito tooservice pacchetti distribuiti in hello stesso nodo. Ad esempio errori quando non è possibile scaricare il pacchetto di applicazione su tale nodo e problemi a configurare l'entità di sicurezza dell'applicazione nel nodo hello. un'applicazione Hello distribuito viene identificata dal nome dell'applicazione (URI) e il nome di nodo (stringa).
* **Pacchetto servizio distribuito**. Rappresenta hello stato di un pacchetto del servizio in esecuzione in un nodo nel cluster hello. Viene descritto pacchetto del servizio tooa specifiche condizioni che non interessano hello altri pacchetti del servizio su hello stesso nodo per hello stessa applicazione. Ad esempio un pacchetto di codice in pacchetto del servizio hello che non può essere avviato e di un pacchetto di configurazione che non può essere letto. pacchetto del servizio distribuito Hello è identificato dal nome dell'applicazione (URI), il nome di nodo (stringa), il nome del manifesto del servizio (string) e ID di attivazione del pacchetto di servizio (stringa).

granularità di Hello hello del modello di integrità rende facile toodetect e correggere i problemi. Ad esempio, se un servizio non risponde, è possibile tooreport che hello istanza dell'applicazione non è integro. Creazione di relazioni che livello non è ideale, tuttavia, poiché il problema di hello non potrebbe risentirne tutti i servizi di hello all'interno dell'applicazione. report Hello deve essere applicato toohello integro servizio o una partizione figlio specifici tooa, se informazioni punta toothat partizione. dati Hello automaticamente superfici tramite la gerarchia di hello e una partizione non integro vengono resi visibili i livelli di servizio e di applicazione. Questa aggregazione consente toopinpoint e risolvere più rapidamente causa radice di hello del problema hello.

gerarchia di integrità Hello è composto da relazioni padre-figlio. Un cluster è costituito da nodi e applicazioni. Le applicazioni hanno servizi e applicazioni distribuite e le applicazioni distribuite hanno pacchetti del servizio distribuiti. I servizi dispongono di partizioni e ogni partizione dispone di una o più repliche. Tra i nodi e le entità distribuite esiste una relazione speciale. Un nodo di tipo non integro come riportato dal relativo componente di sistema di autorità, hello Failover Manager service, influisce su hello distribuito applicazioni, pacchetti del servizio e le repliche distribuite in esso.

gerarchia di integrità Hello rappresenta lo stato più recente di hello del sistema hello in base ai report di integrità più recente hello, ovvero informazioni quasi in tempo reale.
Watchdog interni ed esterni può creare report hello stesse entità in base a logica specifica dell'applicazione o condizioni monitorate personalizzate. Report utente coesistere con i report di sistema hello.

Pianificare tooinvest in modalità progettazione di un servizio cloud di grandi dimensioni è toohealth tooreport e rispondere durante hello. Questo approvano dedicano rende toodebug più semplice di hello del servizio, monitorare e gestire.

## <a name="health-states"></a>Stati di integrità
Service Fabric utilizza tre toodescribe di stati di integrità se un'entità è integro o non: OK, avviso e errore. Tutti i report inviati archivio integrità toohello deve specificare uno di questi stati. risultato della valutazione salute Hello è uno di questi stati.

Hello possibili [gli stati di integrità](https://docs.microsoft.com/dotnet/api/system.fabric.health.healthstate) sono:

* **OK**. entità Hello è integro. Non vengono segnalati problemi noti per l'entità o i relativi elementi figlio (se esistenti).
* **Avviso**. entità Hello presenta alcuni problemi, ma possono comunque funzionare correttamente. Ad esempio, si verificano ritardi che però non causano ancora problemi funzionali. In alcuni casi, la condizione di avviso hello potrebbe essere risolto automaticamente senza l'intervento dell'esterno. In questi casi, i report sull'integrità forniscono informazioni e visibilità sulla situazione. In altri casi, la condizione di avviso hello potrebbe peggiorare un problema grave senza intervento dell'utente.
* **Error**. entità Hello è integro. È opportuno intervenire stato hello toofix dell'entità di hello, perché non può funzionare correttamente.
* **Unknown**. entità Hello non esiste nell'archivio integrità hello. È possibile ottenere questo risultato dalle query distribuita hello che uniscono i risultati da più componenti. Ad esempio, query di elenco hello get nodo diventa troppo**FailoverManager**, **ClusterManager**, e **HealthManager**; dell'applicazione di ottenere query di elenco diventa troppo **ClusterManager** e **HealthManager**. Tali query uniscono i risultati provenienti da più componenti di sistema. Se un altro componente di sistema restituisce un'entità che non è presente nell'archivio integrità, hello risultati sottoposti a merge sono unknown lo stato di integrità. Un'entità non è nell'archivio perché non sono ancora stati elaborati i rapporti di stato o entità hello è stato pulito dopo l'eliminazione.

## <a name="health-policies"></a>Criteri di integrità
archivio integrità Hello applica toodetermine di criteri di integrità se un'entità è integro in base ai relativi report e i relativi elementi figlio.

> [!NOTE]
> Criteri di integrità possono essere specificati nel manifesto del cluster hello (per la valutazione dell'integrità del cluster e nodo) o nel manifesto dell'applicazione hello (per la valutazione dell'applicazione e i relativi elementi figlio). Le richieste di valutazione dell'integrità possono anche passare criteri personalizzati, usati solo per la valutazione in questione.
> 
> 

Per impostazione predefinita, Service Fabric Applica regole strict (tutti gli elementi devono essere integri) per la relazione gerarchica di hello padre-figlio. Se uno degli elementi figlio di hello dispone di un evento non integro, padre di hello è considerato non integro.

### <a name="cluster-health-policy"></a>Criteri di integrità del cluster
Hello [criteri di integrità del cluster](https://docs.microsoft.com/dotnet/api/system.fabric.health.clusterhealthpolicy) è l'integrità del cluster hello tooevaluate utilizzati stati di integrità dello stato e di nodo. è possibile definire criteri Hello nel manifesto del cluster hello. Se non è presente, viene utilizzato il criterio predefinito hello (zero tollerati errori).
criteri di integrità del cluster Hello contengono:

* [ConsiderWarningAsError](https://docs.microsoft.com/dotnet/api/system.fabric.health.clusterhealthpolicy.considerwarningaserror). Specifica se l'integrità di avviso tootreat segnalare come errori durante la valutazione dell'integrità. Valore predefinito: false.
* [MaxPercentUnhealthyApplications](https://docs.microsoft.com/dotnet/api/system.fabric.health.clusterhealthpolicy.maxpercentunhealthyapplications). Specifica hello percentuale massima di sfasamento di applicazioni che possono essere integro prima di cluster hello è considerato in errore.
* [MaxPercentUnhealthyNodes](https://docs.microsoft.com/dotnet/api/system.fabric.health.clusterhealthpolicy.maxpercentunhealthynodes). Specifica hello percentuale massima di sfasamento di nodi che possono essere integro prima di cluster hello è considerato in errore. Nei cluster di grandi dimensioni, alcuni nodi sono sempre verso il basso o out per operazioni di ripristino, pertanto questa percentuale deve essere configurato tootolerate che.
* [ApplicationTypeHealthPolicyMap](https://docs.microsoft.com/dotnet/api/system.fabric.health.clusterhealthpolicy.applicationtypehealthpolicymap). mappa dei criteri di integrità tipi di Hello applicazione può essere utilizzato durante i tipi di applicazioni speciali toodescribe di valutazione di cluster integrità. Per impostazione predefinita, tutte le applicazioni vengono inserite in un pool e valutate con MaxPercentUnhealthyApplications. Se alcuni tipi di applicazioni devono essere gestiti in modo diverso, è possibile sottratta pool globale hello. Al contrario, vengono confrontate le percentuali di hello associate con il nome del tipo di applicazione nella mappa hello. Ad esempio, in un cluster esistono migliaia di applicazioni di tipi diversi e alcune istanze di applicazioni di controllo di un tipo di applicazione speciale. applicazioni di controllo Hello non devono essere mai in errore. È possibile specificare globale MaxPercentUnhealthyApplications too20% tootolerate alcuni errori, ma per hello "ControlApplicationType" tipo di applicazione imposta too0 MaxPercentUnhealthyApplications hello. In questo modo, se alcune delle hello molte applicazioni non sono integri, ma di sotto percentuale non integra globale hello, sarebbe cluster hello valutata tooWarning. Uno stato di integrità Warning non influisce sull'aggiornamento del cluster o su altri tipi di monitoraggio attivati dallo stato di integrità Error. Ma anche un controllo dell'applicazione in errore renderebbe cluster non è integro, che attiva il rollback o sospende l'aggiornamento del cluster hello, a seconda della configurazione di aggiornamento hello.
  Per i tipi di applicazione hello definiti nella mappa hello, tutte le istanze dell'applicazione vengono estratti dalla pool globale di hello delle applicazioni. Vengono valutate in base al numero totale di hello delle applicazioni di tipo di applicazione hello, utilizzando hello MaxPercentUnhealthyApplications specifico da hello eseguire il mapping. Tutte le altre hello delle applicazioni hello rimangono nel pool globale hello e vengono valutate con MaxPercentUnhealthyApplications.

Hello di esempio seguente è tratto da un manifesto del cluster. toodefine le voci della mappa di tipo di applicazione hello, nome del parametro hello prefisso con "ApplicationTypeMaxPercentUnhealthyApplications-", seguito dal nome del tipo di applicazione hello.

```xml
<FabricSettings>
  <Section Name="HealthManager/ClusterHealthPolicy">
    <Parameter Name="ConsiderWarningAsError" Value="False" />
    <Parameter Name="MaxPercentUnhealthyApplications" Value="20" />
    <Parameter Name="MaxPercentUnhealthyNodes" Value="20" />
    <Parameter Name="ApplicationTypeMaxPercentUnhealthyApplications-ControlApplicationType" Value="0" />
  </Section>
</FabricSettings>
```

### <a name="application-health-policy"></a>Criteri di integrità dell'applicazione
Hello [criteri di integrità delle applicazioni](https://docs.microsoft.com/dotnet/api/system.fabric.health.applicationhealthpolicy) descrive valutazione hello di aggregazione di eventi e gli stati di figlio come avviene per le applicazioni e i relativi elementi figlio. Può essere definito nel manifesto dell'applicazione hello, **ApplicationManifest.xml**, nel pacchetto di applicazione hello. Se non è stato specificato alcun criterio, Service Fabric si presuppone che entità hello non integro se lo stato di integrità di avviso o errore hello ha un rapporto di stato o un elemento figlio.
criteri configurabili Hello sono:

* [ConsiderWarningAsError](https://docs.microsoft.com/dotnet/api/system.fabric.health.applicationhealthpolicy.considerwarningaserror.aspx). Specifica se l'integrità di avviso tootreat segnalare come errori durante la valutazione dell'integrità. Valore predefinito: false.
* [MaxPercentUnhealthyDeployedApplications](https://docs.microsoft.com/dotnet/api/system.fabric.health.applicationhealthpolicy.maxpercentunhealthydeployedapplications). Specifica la percentuale massima di hello, che è consentito delle applicazioni distribuite che possono essere integro prima di un'applicazione hello è considerata in errore. Questa percentuale viene calcolata dividendo il numero di hello delle applicazioni distribuite non integro per il numero di hello di nodi applicazioni hello attualmente distribuite in cluster hello. calcolo Hello Arrotonda tootolerate un errore in un numero limitato di nodi. Percentuale predefinita: zero.
* [DefaultServiceTypeHealthPolicy](https://docs.microsoft.com/dotnet/api/system.fabric.health.applicationhealthpolicy.defaultservicetypehealthpolicy). Specifica hello tipo integrità criterio del servizio predefinito, che sostituisce i criteri di integrità hello predefinito per tutti i tipi di servizio in un'applicazione hello.
* [ServiceTypeHealthPolicyMap](https://docs.microsoft.com/dotnet/api/system.fabric.health.applicationhealthpolicy.servicetypehealthpolicymap). Fornisce una mappa dei criteri di integrità del servizio per tipo di servizio. Questi criteri sostituiscono hello predefinito servizio tipo criteri di integrità per ogni tipo di servizio specificato. Ad esempio, se un'applicazione dispone di un tipo di servizio senza stato gateway e un tipo di servizio con stato motore, è possibile configurare criteri di integrità hello di valutazione in modo diverso. Quando si specificano i criteri per ogni tipo di servizio, è possibile ottenere un controllo più granulare di integrità hello del servizio hello.

### <a name="service-type-health-policy"></a>Criteri di integrità del tipo di servizio
Hello [criteri di integrità del tipo di servizio](https://docs.microsoft.com/dotnet/api/system.fabric.health.servicetypehealthpolicy) specifica la modalità tooevaluate e aggregazione hello servizi e hello figli dei servizi. criteri di Hello contengono:

* [MaxPercentUnhealthyPartitionsPerService](https://docs.microsoft.com/dotnet/api/system.fabric.health.servicetypehealthpolicy.maxpercentunhealthypartitionsperservice). Specifica la percentuale di hello massimo consentito di partizioni non integre prima di un servizio viene considerato non integro. Percentuale predefinita: zero.
* [MaxPercentUnhealthyReplicasPerPartition](https://docs.microsoft.com/dotnet/api/system.fabric.health.servicetypehealthpolicy.maxpercentunhealthyreplicasperpartition). Specifica la percentuale hello massimo consentito di repliche non integre prima che una partizione è considerata non integra. Percentuale predefinita: zero.
* [MaxPercentUnhealthyServices](https://docs.microsoft.com/dotnet/api/system.fabric.health.servicetypehealthpolicy.maxpercentunhealthyservices). Specifica la percentuale di hello massimo consentito di servizi non integri prima di un'applicazione hello viene considerata non integra. Percentuale predefinita: zero.

Hello di esempio seguente è tratto da un manifesto dell'applicazione:

```xml
    <Policies>
        <HealthPolicy ConsiderWarningAsError="true" MaxPercentUnhealthyDeployedApplications="20">
            <DefaultServiceTypeHealthPolicy
                   MaxPercentUnhealthyServices="0"
                   MaxPercentUnhealthyPartitionsPerService="10"
                   MaxPercentUnhealthyReplicasPerPartition="0"/>
            <ServiceTypeHealthPolicy ServiceTypeName="FrontEndServiceType"
                   MaxPercentUnhealthyServices="0"
                   MaxPercentUnhealthyPartitionsPerService="20"
                   MaxPercentUnhealthyReplicasPerPartition="0"/>
            <ServiceTypeHealthPolicy ServiceTypeName="BackEndServiceType"
                   MaxPercentUnhealthyServices="20"
                   MaxPercentUnhealthyPartitionsPerService="0"
                   MaxPercentUnhealthyReplicasPerPartition="0">
            </ServiceTypeHealthPolicy>
        </HealthPolicy>
    </Policies>
```

## <a name="health-evaluation"></a>Valutazione dell'integrità
Gli utenti e i servizi automatizzati possono valutare l'integrità di qualsiasi entità in qualsiasi momento. tooevaluate integrità di un'entità, le aggregazioni di archivio integrità hello integrità di tutti i report sull'entità hello e restituisce tutti gli elementi figlio (se applicabile). algoritmo di aggregazione di Hello integrità utilizza criteri di integrità che specificano come rapporti di integrità tooevaluate e come gli stati di integrità di figlio tooaggregate (se applicabile).

### <a name="health-report-aggregation"></a>Aggregazione dei report sull'integrità
Per una stessa entità possono essere disponibili più report sull'integrità inviati da generatori diversi (componenti di sistema o watchdog) relativamente a proprietà diverse. Usa aggregazione Hello hello criteri di integrità associati, in particolare hello ConsiderWarningAsError membro dell'applicazione o criteri di integrità del cluster. Specifica ConsiderWarningAsError come tooevaluate avvisi.

Hello stato aggregato di integrità viene attivato da hello *peggiore* integrità report sull'entità hello. Se è presente il rapporto di stato di almeno un errore, hello stato di integrità aggregato è un errore.

![Aggregazione dei report sull'integrità con report di tipo Error.][2]

Un'entità di integrità con uno o più report sull'integrità di tipo Error viene valutata come Error. Hello stesso vale per un rapporto di stato scaduti, indipendentemente dallo stato di integrità.

[2]: ./media/service-fabric-health-introduction/servicefabric-health-report-eval-error.png

Se sono presenti alcun report di errore e uno o più avvisi, hello stato di integrità aggregato è un avviso o errore, a seconda di flag di hello ConsiderWarningAsError criteri.

![Aggregazione dei report sull'integrità con report di tipo Warning e ConsiderWarningAsError impostato su false.][3]

Aggregazione di report di integrità con i report di avviso e ConsiderWarningAsError imposta toofalse (impostazione predefinita).

[3]: ./media/service-fabric-health-introduction/servicefabric-health-report-eval-warning.png

### <a name="child-health-aggregation"></a>Aggregazione dell'integrità degli elementi figlio
Hello stato di integrità aggregato di un'entità riflette gli stati di integrità figlio hello (se applicabile). algoritmo di Hello per l'aggregazione di stati di integrità figlio utilizza hello integrità criteri applicabili in base al tipo di entità hello.

![Aggregazione dell'integrità delle entità figlio.][4]

Aggregazione degli elementi figlio in base ai criteri di integrità.

[4]: ./media/service-fabric-health-introduction/servicefabric-health-hierarchy-eval.png

Dopo che archivio integrità hello ha valutato tutti gli elementi figlio hello, aggrega i relativi stati di integrità in base alla percentuale massima di hello configurato figli non integri. Questa percentuale viene ricavata dal criterio hello in base al tipo di entità e figlio hello.

* Se tutti gli elementi figlio sono stati OK, lo stato di integrità aggregato figlio hello è accettabile.
* Se gli elementi figlio hanno OK e stati di avviso, lo stato di integrità aggregato figlio hello è di avviso.
* Se sono presenti elementi figlio con gli stati di errore che non rispettano massimo hello percentuale di elementi figlio non integri consentita, hello stato di integrità aggregato è un errore.
* Se gli elementi figlio hello con errore stati riguardo hello massima percentuale di elementi figlio non integri consentita hello di avviso dello stato di integrità aggregato.

## <a name="health-reporting"></a>Creazione di report sull'integrità
I componenti di sistema, le applicazioni Fabric di sistema e i watchdog interni/esterni possono generare report in relazione alle entità di Service Fabric. rendere reporters Hello *locale* determinazioni di integrità hello di entità hello monitorata, in base alle condizioni di hello sottoposti a monitoraggio. Non è necessario toolook in qualsiasi stato globale o aggregare i dati. Hello desiderato comportamento è reporters semplice toohave e organismi non complessi che devono toolook in molte operazioni tooinfer toosend quali informazioni.

archivio integrità toohello di dati di integrità di toosend, il reporter deve entità hello interessato tooidentify e creare un rapporto di stato. report utilizzo hello hello toosend [FabricClient.HealthClient.ReportHealth](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.reporthealth) API, segnalare l'integrità API esposte in hello `Partition` o `CodePackageActivationContext` oggetti, i cmdlet di PowerShell o REST.

### <a name="health-reports"></a>Report sull'integrità
Hello [rapporti di stato](https://docs.microsoft.com/dotnet/api/system.fabric.health.healthreport) per ognuna delle entità hello cluster hello contengono hello le seguenti informazioni:

* **SourceId**. Stringa che identifica in modo univoco il reporter hello dell'evento di integrità hello.
* **Entity identifier**. Identifica l'entità hello in cui viene applicato il report hello. È diverso in base a hello [tipo di entità](service-fabric-health-introduction.md#health-entities-and-hierarchy):
  
  * Cluster. Nessuna.
  * Node. Nome del nodo (stringa).
  * Application. Nome dell'applicazione (URI). Rappresenta il nome di hello dell'istanza dell'applicazione hello distribuito in cluster hello.
  * Service. Nome del servizio (URI). Rappresenta il nome di hello hello di istanze del servizio distribuito in cluster hello.
  * Partition. ID della partizione (GUID). Rappresenta l'identificatore univoco della partizione hello.
  * Replica. ID replica di servizio con stato Hello o ID istanza del servizio senza stato hello (INT64).
  * DeployedApplication. Nome dell'applicazione (URI) e nome del nodo (stringa).
  * DeployedServicePackage. Nome dell'applicazione (URI), nome del nodo (stringa) e nome del manifesto del servizio (stringa).
* **Property**. Oggetto *stringa* (non un'enumerazione predefinita), che consente il reporter hello integrità hello toocategorize evento per una proprietà specifica dell'entità hello. Ad esempio, un reporter può segnalare l'integrità hello della proprietà "Archiviazione" hello nodo01 e reporter B può segnalare l'integrità di hello della proprietà "Connettività" hello nodo01. Nell'archivio integrità hello, questi report vengono considerati come gli eventi di integrità separato per hello nodo01 entità.
* **Description**. Una stringa che consente un tooprovide reporter informazioni dettagliate sull'evento di integrità hello. **SourceId**, **proprietà**, e **HealthState** deve descrivere completamente report hello. Descrizione Hello aggiunge leggibile informazioni sui report hello. testo Hello rende più semplice per amministratori e utenti report di integrità di hello toounderstand.
* **HealthState**. Un [enumerazione](service-fabric-health-introduction.md#health-states) che descrive lo stato di integrità hello del report hello. Hello i valori accettati sono OK, avviso e errore.
* **TimeToLive**. Timespan che indica quanto tempo rapporto di stato hello è valido. Insieme a **RemoveWhenExpired**, informa dell'archivio integrità hello come tooevaluate scaduto eventi. Per impostazione predefinita, il valore di hello è infinito e report hello è sempre valido.
* **RemoveWhenExpired**. Valore booleano. Se impostato tootrue, hello integrità scaduti dall'archivio integrità hello viene rimosso automaticamente i report e report hello non influisce sulla valutazione dell'integrità di entità. Utilizzato quando il report hello è valido per un determinato periodo di tempo solo e reporter hello non necessario tooexplicitly deselezionarla. È inoltre utilizzato dall'archivio integrità hello toodelete report (ad esempio, un controllo viene modificato e interrompe l'invio di report con origine precedente e proprietà). Può inviare un report con una breve TimeToLive insieme RemoveWhenExpired tooclear dello stato precedente dall'archivio integrità hello. Se il valore di hello è impostato toofalse, hello report scaduto viene considerato un errore nella valutazione dell'integrità hello. valore false Hello segnala archivio integrità toohello che tale origine hello deve segnalare periodicamente su questa proprietà. In caso contrario, deve essere presente un problema con watchdog hello. integrità del watchdog Hello viene acquisito da prendere in considerazione evento hello come un errore.
* **SequenceNumber**. Un numero intero positivo che deve toobe crescenti, rappresenta l'ordine di hello dei report hello. Viene usato da hello archivio toodetect obsoleti rapporti di stato che vengono ricevute in ritardo a causa di ritardi di rete o altri problemi. Un report viene rifiutato se il numero di sequenza di hello è minore o uguale numero toohello applicato più di recente per hello stessa entità, origine e proprietà. Se non è specificato, il numero di sequenza hello viene generato automaticamente. È necessario tooput nel numero di sequenza hello solo quando si segnalano in transizioni di stato. In questo caso, origine hello deve tooremember i report che inviato e mantenere le informazioni di hello per il ripristino in caso di failover.

SourceId, l'identificatore dell'entità, Property e HealthState sono dati obbligatori per tutti i report sull'integrità. Hello SourceId stringa non è consentito toostart con prefisso hello "**System.**", che è riservato per i report di sistema. Per hello stessa entità, è presente un solo report per hello stessa origine e proprietà. Più report per hello stessa origine e di override di proprietà tra loro, il lato client integrità hello (se vengono eseguite in batch) o sul lato dell'archivio integrità hello. sostituzione di Hello è in base ai numeri di sequenza; i report più recenti (con numeri di sequenza superiore) sostituiscono i report meno recenti.

### <a name="health-events"></a>Eventi di integrità
Internamente, archivio integrità hello mantiene [eventi di integrità](https://docs.microsoft.com/dotnet/api/system.fabric.health.healthevent), che contiene tutte le informazioni hello hello report e i metadati aggiuntivi. metadati Hello includono ora hello report hello è stato assegnato il client di integrità toohello e l'ora di hello che è stato modificato sul lato server hello. gli eventi di integrità Hello vengono restituiti da [query sull'integrità](service-fabric-view-entities-aggregated-health.md#health-queries).

Hello aggiunto metadati contengono:

* **SourceUtcTimestamp**. report di hello tempo Hello è stato specificato il client di integrità toohello (Coordinated Universal Time).
* **LastModifiedUtcTimestamp**. report di hello Hello ora dell'ultima modifica sul lato server hello (Coordinated Universal Time).
* **IsExpired**. Un flag tooindicate se report hello è scaduto quando è stata eseguita la query hello dall'archivio integrità hello. Un evento può risultare scaduto solo se RemoveWhenExpired è false. In caso contrario, l'evento hello non viene restituito dalla query e viene rimosso dall'archivio di hello.
* **LastOkTransitionAt**, **LastWarningTransitionAt**, **LastErrorTransitionAt**. ultima ora per le transizioni OK/avviso/errore Hello. Questi campi forniscono una cronologia hello delle transizioni di stato di integrità hello per evento hello.

campi di transizione dello stato di Hello è utilizzabile per gli avvisi più intelligenti o informazioni sull'evento di integrità "cronologici". Consentono l'uso di scenari simili ai seguenti:

* Avviso quando lo stato di una proprietà è impostato su Warning/Error da più di X minuti. Verifica la condizione di hello per un periodo di tempo consente di evitare gli avvisi in condizioni temporanee. Ad esempio, un avviso se lo stato di integrità hello è stato avviso per più di cinque minuti può essere convertito in (HealthState = = avviso e l'ora - LastWarningTransitionTime > 5 minuti).
* Avviso solo alle condizioni che sono stati modificati in hello ultima X minuti. Se un report era già in errore prima hello specificato di tempo, può essere ignorato perché è già stato segnalato in precedenza.
* Se una proprietà si alterna tra lo stato Warning e lo stato Error, determinare per quanto tempo è risultata non integra, ovvero non OK. Ad esempio, un avviso se la proprietà hello non è stato integro per più di cinque minuti può essere convertito in (HealthState! = Ok e ora - LastOkTransitionTime > 5 minuti).

## <a name="example-report-and-evaluate-application-health"></a>Esempio: Report e valutazione dell'integrità dell'applicazione
esempio Hello invia un rapporto di stato tramite PowerShell in un'applicazione hello **fabric: / WordCount** dall'origine hello **MyWatchdog**. rapporto di stato Hello contiene informazioni sulla proprietà di integrità hello "disponibilità" in uno stato di errore, con la proprietà TimeToLive infinito. Quindi viene eseguita una query dello stato dell'applicazione hello, che restituisce aggregati di errori di stato di integrità e hello segnalati gli eventi di stato nell'elenco di hello di eventi di integrità.

```powershell
PS C:\> Send-ServiceFabricApplicationHealthReport –ApplicationName fabric:/WordCount –SourceId "MyWatchdog" –HealthProperty "Availability" –HealthState Error

PS C:\> Get-ServiceFabricApplicationHealth fabric:/WordCount -ExcludeHealthStatistics


ApplicationName                 : fabric:/WordCount
AggregatedHealthState           : Error
UnhealthyEvaluations            :
                                  Error event: SourceId='MyWatchdog', Property='Availability'.

ServiceHealthStates             :
                                  ServiceName           : fabric:/WordCount/WordCountService
                                  AggregatedHealthState : Error

                                  ServiceName           : fabric:/WordCount/WordCountWebService
                                  AggregatedHealthState : Ok

DeployedApplicationHealthStates :
                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_0
                                  AggregatedHealthState : Ok

                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_2
                                  AggregatedHealthState : Ok

                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_3
                                  AggregatedHealthState : Ok

                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_4
                                  AggregatedHealthState : Ok

                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_1
                                  AggregatedHealthState : Ok

HealthEvents                    :
                                  SourceId              : System.CM
                                  Property              : State
                                  HealthState           : Ok
                                  SequenceNumber        : 360
                                  SentAt                : 3/22/2016 7:56:53 PM
                                  ReceivedAt            : 3/22/2016 7:56:53 PM
                                  TTL                   : Infinite
                                  Description           : Application has been created.
                                  RemoveWhenExpired     : False
                                  IsExpired             : False
                                  Transitions           : Error->Ok = 3/22/2016 7:56:53 PM, LastWarning = 1/1/0001 12:00:00 AM

                                  SourceId              : MyWatchdog
                                  Property              : Availability
                                  HealthState           : Error
                                  SequenceNumber        : 131032204762818013
                                  SentAt                : 3/23/2016 3:27:56 PM
                                  ReceivedAt            : 3/23/2016 3:27:56 PM
                                  TTL                   : Infinite
                                  Description           :
                                  RemoveWhenExpired     : False
                                  IsExpired             : False
                                  Transitions           : Ok->Error = 3/23/2016 3:27:56 PM, LastWarning = 1/1/0001 12:00:00 AM
```

## <a name="health-model-usage"></a>Uso del modello di integrità
modello di integrità Hello consente di servizi cloud e hello sottostante tooscale piattaforma Service Fabric, poiché il monitoraggio e l'integrità determinazioni sono distribuite tra monitor hello all'interno di cluster hello.
Altri sistemi dispongono di un servizio singolo, centralizzato a livello del cluster hello che analizza tutti hello *potenzialmente* utili informazioni generate dai servizi. Questo approccio ne impedisce la scalabilità Non consente inoltre le informazioni specifiche di toocollect toohelp identificare i problemi e i potenziali problemi come toohello Chiudi causa possibile.

modello di integrità Hello viene utilizzato frequentemente per il monitoraggio e diagnosi, per la valutazione di integrità del cluster e l'applicazione e per aggiornamenti monitorati. Altri servizi utilizzano integrità dati tooperform automatica consente di ripristinare, generazione della cronologia di integrità del cluster e rilasciare gli avvisi in determinate condizioni.

## <a name="next-steps"></a>Passaggi successivi
[Come visualizzare i report sull'integrità di Service Fabric](service-fabric-view-entities-aggregated-health.md)

[Uso dei report sull'integrità del sistema per la risoluzione dei problemi](service-fabric-understand-and-troubleshoot-with-system-health-reports.md)

[Come tooreport e controllo del servizio integrità](service-fabric-diagnostics-how-to-report-and-check-service-health.md)

[Aggiungere report sull'integrità di Service Fabric personalizzati](service-fabric-report-health.md)

[Monitorare e diagnosticare servizi in locale](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[Aggiornamento di un'applicazione di infrastruttura di servizi](service-fabric-application-upgrade.md)

