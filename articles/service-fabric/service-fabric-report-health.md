---
title: "report sull'integrità di Service Fabric personalizzato aaaAdd | Documenti Microsoft"
description: "Viene descritto come toosend personalizzato integrità segnala tooAzure entità di integrità dell'infrastruttura di servizio. Offre consigli per la progettazione e l'implementazione di report efficaci relativi all'integrità."
services: service-fabric
documentationcenter: .net
author: oanapl
manager: timlt
editor: 
ms.assetid: 0a00a7d2-510e-47d0-8aa8-24c851ea847f
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/19/2017
ms.author: oanapl
ms.openlocfilehash: 12c9f664e2a457b4e1e8f340873ca60ebcefb097
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="add-custom-service-fabric-health-reports"></a>Aggiungere report sull'integrità di Service Fabric personalizzati
Azure Service Fabric introduce un [modello di integrità](service-fabric-health-introduction.md) progettato tooflag integro cluster e le condizioni di applicazione per entità specifiche. utilizza il modello di integrità Hello **reporters integrità** (componenti di sistema e watchdog). obiettivo di Hello è ripristino e diagnostica rapida e semplice. Gli autori del servizio necessario toothink anticipo sull'integrità. Qualsiasi condizione che può influire sull'integrità deve essere segnalati, soprattutto se ciò consente di chiudere toohello radice dei problemi di flag. informazioni sull'integrità Hello risparmiare tempo e impegno sull'analisi e di debug. Hello utilità è particolarmente evidente quando il servizio di hello è attivo e in esecuzione su larga scala nel cloud hello (privata o Azure).

monitoraggio di Hello Service Fabric reporters identificato le condizioni di interesse. Generano report su tali condizioni in base alla visualizzazione locale. Hello [archivio integrità](service-fabric-health-introduction.md#health-store) aggrega i dati di integrità inviati da toodetermine reporters tutte le entità sono integra globale. modello di Hello è previsto toobe RTF, flessibili e semplici toouse. qualità Hello di report sull'integrità hello determina la precisione di visualizzazione dell'integrità del cluster hello hello hello. I falsi positivi che visualizzano erroneamente problemi di non integrità possono influire negativamente sugli aggiornamenti o su altri servizi che usano i dati di integrità, come ad esempio i servizi di ripristino e i meccanismi di avviso. Pertanto, valutare diversi aspetti sono tooprovide necessari report che consentono di acquisire le condizioni di interesse in hello migliore dei modi possibili.

toodesign e implementare report, watchdog e sistema componenti di integrità devono:

* Definire la condizione di hello che sono interessati, modo hello che viene monitorato e hello impatto sulle funzionalità di cluster o l'applicazione hello. In base a queste informazioni, stabilire hello report proprietà e l'integrità stato di integrità.
* Determinare hello [entità](service-fabric-health-introduction.md#health-entities-and-hierarchy) che si riferisce hello report.
* Determinare reporting hello in cui viene eseguita dall'interno hello watchdog servizio o da un interno o esterno.
* Definire il reporter hello tooidentify di origine utilizzata.
* Scegliere una strategia di creazione di report (periodicamente o in caso di transizioni). Hello consigliato consiste periodicamente, ed è necessario semplificare il codice è meno soggetto tooerrors.
* Determinare il tempo report hello per le condizioni non integro devono rimanere nell'archivio integrità hello e la modalità deve essere cancellato. Utilizza queste informazioni, decidere di comportamento in fase di hello report toolive e Rimuovi alla scadenza.

Come indicato, i report possono essere creati da:

* Hello monitorati replica del servizio Service Fabric.
* Watchdog interni distribuiti come servizio di Service Fabric, ad esempio un servizio senza stato di Service Fabric che monitora le condizioni e genera i report. watchdog Hello può essere distribuito un tutti i nodi o può essere creata toohello monitorato servizio.
* Watchdog interno, ma eseguire nei nodi di Service Fabric hello *non* implementati come servizi di Service Fabric.
* Esterno watchdogs risorsa hello probe da *esterno* cluster di Service Fabric hello (ad esempio, servizio di monitoraggio come Gomez).

> [!NOTE]
> Viene fornita, hello cluster hello viene popolato con i rapporti di stati inviati dai componenti di sistema hello. Per altre informazioni, vedere [Uso dei report sull'integrità del sistema per la risoluzione dei problemi](service-fabric-understand-and-troubleshoot-with-system-health-reports.md). Hello report utente devono essere inviati [entità integrità](service-fabric-health-introduction.md#health-entities-and-hierarchy) che sono già stati creati dal sistema hello.
> 
> 

Una volta hello Progettazione report di integrità è deselezionata, i rapporti di stato è possibile inviare facilmente. È possibile utilizzare [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient) tooreport integrità se non è cluster hello [sicura](service-fabric-cluster-security.md) o se il client di infrastruttura hello dispone di privilegi di amministratore. Creazione di report possono essere eseguite tramite hello API da utilizzando [FabricClient.HealthManager.ReportHealth](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.reporthealth), PowerShell o tramite REST. Sono disponibili controlli di configurazione che riuniscono i report in batch per migliorare le prestazioni.

> [!NOTE]
> Segnalare l'integrità è sincrono e rappresenta solo hello attività di convalida sul lato client hello. Hello fatto che hello report è accettata dal client di integrità hello o hello `Partition` o `CodePackageActivationContext` oggetti non significa che viene applicato nell'archivio di hello. Viene inviato in modo asincrono e possibilmente in batch con altri report. elaborazione nel server di hello Hello ancora potrebbe non riuscire: numero di sequenza hello potrebbe essere non aggiornato, entità hello su quale hello report deve essere applicato è stato eliminato, e così via.
> 
> 

## <a name="health-client"></a>Client di integrità
Hello rapporti di stato vengono inviati tramite un client di integrità, che si trova all'interno del client fabric hello toohello dell'archivio integrità. Hello integrità client può essere configurato con hello seguenti impostazioni:

* **HealthReportSendInterval**: ritardo hello tra report di hello tempo hello è aggiunto toohello client e hello ora dell'invio dell'archivio integrità toohello. Report toobatch utilizzati in un singolo messaggio, anziché inviare un messaggio per ogni report. Hello batch migliora le prestazioni. Impostazione predefinita: 30 secondi.
* **HealthReportRetrySendInterval**: intervallo hello in cui hello client integrità reinvia accumulato integrità segnala toohello dell'archivio integrità. Impostazione predefinita: 30 secondi.
* **HealthOperationTimeout**: il periodo di timeout hello per un messaggio di rapporto inviato toohello dell'archivio integrità. Se un messaggio scade, hello integrità client eseguirà dei tentativi, fino a quando l'archivio integrità hello conferma che il report hello è stato elaborato. Valore predefinito: due minuti.

> [!NOTE]
> Quando vengono eseguite in batch report hello del client fabric hello deve essere mantenuto attivo per almeno hello tooensure HealthReportSendInterval che vengono inviati. Se il messaggio hello viene perso o dell'archivio integrità hello non è possibile applicare a causa di errori tootransient, del client fabric hello deve essere mantenuto attivi toogive più tooretry una possibilità.
> 
> 

memorizzazione nel buffer Hello client hello accetta l'univocità hello dei report hello in considerazione. Ad esempio, se un particolare reporter non valido il reporting 100 rapporti al secondo su hello stessa proprietà di hello stessa entità, i report vengono sostituiti con l'ultima versione di hello hello. Al massimo una tale relazione esiste nella coda di hello client. Se l'invio in batch è configurata, il numero di hello dei report inviati archivio integrità toohello è solo una per l'intervallo di trasmissione. Questo report è hello ultimo aggiunto, che riflette lo stato più recente di hello dell'entità hello.
Specificare i parametri di configurazione quando `FabricClient` viene creato passando [FabricClientSettings](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclientsettings) con hello valori desiderati per le voci di salute.

Hello esempio seguente viene creato un client di infrastruttura e specifica che devono essere inviati i report di hello quando vengono aggiunte. In caso di timeout ed errori che supportano nuovi tentativi, questi vengono eseguiti ogni 40 secondi.

```csharp
var clientSettings = new FabricClientSettings()
{
    HealthOperationTimeout = TimeSpan.FromSeconds(120),
    HealthReportSendInterval = TimeSpan.FromSeconds(0),
    HealthReportRetrySendInterval = TimeSpan.FromSeconds(40),
};
var fabricClient = new FabricClient(clientSettings);
```

Si consiglia di mantenere le impostazioni di client, impostare dell'infrastruttura predefinito hello `HealthReportSendInterval` too30 secondi. Questa impostazione garantisce prestazioni ottimali toobatching scadenza. Per i report critici che devono essere inviati il prima possibile, usare `HealthReportSendOptions` con il flag Immediate `true` nell'API [FabricClient.HealthClient.ReportHealth](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.reporthealth). Report immediato ignorare hello intervallo di invio in batch. Questo flag viene utilizzato con cautela; Vogliamo tootake vantaggio del client di integrità hello batch ogni volta che è possibile. Invio immediato è utile anche quando la chiusura del client fabric hello (ad esempio, il processo di hello ha rilevato stato non valido e deve tooshut effetti collaterali tooprevent verso il basso). Assicura una trasmissione sforzo di hello accumulato report. Quando un report viene aggiunto con il flag di controllo immediato, il client di integrità hello invia in batch tutti i report di hello accumulato dall'ultimo invio.

Quando viene creato un cluster di tooa connessione tramite PowerShell, è possibile specificare parametri stessi. Hello di esempio seguente avvia un cluster locale tooa di connessione:

```powershell
PS C:\> Connect-ServiceFabricCluster -HealthOperationTimeoutInSec 120 -HealthReportSendIntervalInSec 0 -HealthReportRetrySendIntervalInSec 40
True

ConnectionEndpoint   :
FabricClientSettings : {
                       ClientFriendlyName                   : PowerShell-1944858a-4c6d-465f-89c7-9021c12ac0bb
                       PartitionLocationCacheLimit          : 100000
                       PartitionLocationCacheBucketCount    : 1024
                       ServiceChangePollInterval            : 00:02:00
                       ConnectionInitializationTimeout      : 00:00:02
                       KeepAliveInterval                    : 00:00:20
                       HealthOperationTimeout               : 00:02:00
                       HealthReportSendInterval             : 00:00:00
                       HealthReportRetrySendInterval        : 00:00:40
                       NotificationGatewayConnectionTimeout : 00:00:00
                       NotificationCacheUpdateTimeout       : 00:00:00
                       }
GatewayInformation   : {
                       NodeAddress                          : localhost:19000
                       NodeId                               : 1880ec88a3187766a6da323399721f53
                       NodeInstanceId                       : 130729063464981219
                       NodeName                             : Node.1
                       }
```

Allo stesso modo tooAPI, i report possono essere inviati tramite `-Immediate` passare toobe inviato immediatamente, indipendentemente dal hello `HealthReportSendInterval` valore.

Per REST, hello report vengono inviati i gateway di Service Fabric toohello, che dispone di un client di infrastruttura interni. Per impostazione predefinita, il client è configurato toosend report in batch ogni 30 secondi. È possibile modificare l'intervallo di batch di hello con impostazione di configurazione di cluster hello `HttpGatewayHealthReportSendInterval` su `HttpGateway`. Come accennato, un'opzione migliore è toosend hello report con `Immediate` true. 

> [!NOTE]
> tooensure che servizi non autorizzati non supporta la segnalazione dello stato con entità hello nel cluster hello, configurare le richieste di hello server tooaccept solo da client protetto. Hello `FabricClient` utilizzato per il report deve essere sicurezza abilitata toobe toocommunicate in grado di cluster hello (ad esempio, con l'autenticazione Kerberos o certificati). Per altre informazioni, vedere la pagina relativa alla [sicurezza del cluster](service-fabric-cluster-security.md).
> 
> 

## <a name="report-from-within-low-privilege-services"></a>Report dai servizi con privilegi limitati
Se i servizi di Service Fabric non sono in cluster toohello accesso di amministratore, è possibile segnalare l'integrità su entità di contesto corrente di hello tramite `Partition` o `CodePackageActivationContext`.

* Per i servizi senza stati, utilizzare [IStatelessServicePartition.ReportInstanceHealth](https://docs.microsoft.com/dotnet/api/system.fabric.istatelessservicepartition.reportinstancehealth) tooreport nell'istanza del servizio corrente hello.
* Per i servizi con stati, utilizzare [IStatefulServicePartition.ReportReplicaHealth](https://docs.microsoft.com/dotnet/api/system.fabric.istatefulservicepartition.reportreplicahealth) tooreport nella replica corrente.
* Utilizzare [IServicePartition.ReportPartitionHealth](https://docs.microsoft.com/dotnet/api/system.fabric.iservicepartition.reportpartitionhealth) tooreport nell'entità di partizione corrente hello.
* Utilizzare [CodePackageActivationContext.ReportApplicationHealth](https://docs.microsoft.com/dotnet/api/system.fabric.codepackageactivationcontext.reportapplicationhealth) tooreport sull'applicazione corrente.
* Utilizzare [CodePackageActivationContext.ReportDeployedApplicationHealth](https://docs.microsoft.com/dotnet/api/system.fabric.codepackageactivationcontext.reportdeployedapplicationhealth) tooreport sull'applicazione corrente di hello distribuita nel nodo corrente hello.
* Utilizzare [CodePackageActivationContext.ReportDeployedServicePackageHealth](https://docs.microsoft.com/dotnet/api/system.fabric.codepackageactivationcontext.reportdeployedservicepackagehealth) tooreport in un pacchetto del servizio per un'applicazione hello distribuito nel nodo corrente hello.

> [!NOTE]
> Internamente, hello `Partition` hello e `CodePackageActivationContext` contengono un client di integrità configurato con le impostazioni predefinite. Come illustrato per hello [client integrità](service-fabric-report-health.md#health-client), i report vengono eseguiti in batch e inviati un timer. gli oggetti di Hello devono essere mantenuti attivi toohave un report di hello toosend possibilità.
> 
> 

È possibile specificare `HealthReportSendOptions` quando si inviano i report tramite le API di integrità `Partition` e `CodePackageActivationContext`. Per i report critici che devono essere inviati il prima possibile, usare `HealthReportSendOptions` con il flag Immediate `true`. Report immediato ignorare hello intervallo del client interno integrità hello di invio in batch. Come accennato in precedenza, è possibile utilizzare questo flag con cautela; Vogliamo tootake vantaggio del client di integrità hello batch ogni volta che è possibile.

## <a name="design-health-reporting"></a>Creare report sull'integrità
Hello primo passaggio nella generazione di report di alta qualità è identificazione condizioni hello che possono influire sull'integrità hello del servizio hello. Qualsiasi condizione che contribuisce di problemi di flag in cluster o il servizio di hello quando inizia-- o, ancora meglio, prima che si verifichi un problema, possono salvare miliardi di dollari. vantaggi di Hello includono i tempi di inattività, un minor numero di ore notturne impiegato per l'analisi e la riparazione di problemi e soddisfazione del cliente.

Dopo avere identificate le condizioni di hello, i writer watchdog necessario toofigure out hello toomonitor di modo migliore per bilanciamento tra overhead e utilità. Si consideri, ad esempio, un servizio che esegue calcoli complessi usando alcuni file temporanei in una condivisione. Viene quindi monitorare hello condivisione tooensure che sia disponibile spazio sufficiente. Può restare in attesa di notifiche relative a modifiche di file o directory. È possibile restituire un avviso se viene raggiunta una soglia iniziale e segnala un errore se la condivisione hello è piena. Un avviso, è possibile avviare un sistema di correzione pulizia dei vecchi file nella condivisione di hello. In caso di errore, un sistema di riparazione potrebbe spostare nodo tooanother replica del servizio hello. Si noti come stati condizione hello vengono descritti in termini di integrità: hello lo stato di hello condizione che può essere considerato Integro (ok) o non integro (avviso o errore).

Dopo aver impostati i dettagli relativi al monitoraggio hello, un writer di watchdog deve toofigure out come tooimplement hello watchdog. Se le condizioni di hello possono essere determinate dall'interno del servizio di hello, watchdog hello possono far parte del servizio hello monitorato. Ad esempio, codice del servizio hello può controllare l'utilizzo della condivisione hello e quindi report ogni volta che tenta di toowrite un file. Hello vantaggio di questo approccio è che reporting è semplice. Prestare attenzione bug watchdog tooprevent impedendo che influiscano sulle funzionalità del servizio hello.

I rapporti in servizio hello monitorato non è sempre possibile. Un controllo all'interno del servizio hello potrebbe non essere toodetect in grado di condizioni di hello. Potrebbe non disporre di hello logica o dati toomake hello determinazione. il monitoraggio delle condizioni di hello sovraccarico Hello è elevato. le condizioni di Hello anche potrebbero non essere servizio tooa specifico, ma invece influiscono sulle interazioni tra i servizi. Un'altra opzione è toohave watchdog cluster hello come processo separato. watchdog Hello monitorare le condizioni di hello e report, senza influire su servizi principali di hello in alcun modo. Ad esempio, potrebbe essere implementato questi watchdog come servizi senza stati in hello stessa applicazione, distribuita in tutti i nodi o hello stessi nodi come servizio hello.

In alcuni casi, un controllo in esecuzione in cluster hello non è un'opzione. Se hello monitorato è disponibilità hello o funzionalità del servizio hello come visualizzato agli utenti, è migliore watchdog di hello toohave in hello nello stesso punto come client utente hello. Non esiste, testano le operazioni di hello in hello stesso consente agli utenti chiamarle. Ad esempio, è possibile disporre di un controllo che si trova all'esterno del cluster hello e invia le richieste di servizio toohello controlla la latenza di hello e la correttezza dei risultati di hello. Ad esempio, per un servizio calcolatrice, verificare se l'operazione 2+2 restituisce 4 in tempi ragionevoli.

Una volta i dettagli di watchdog hello sono stati completati, è necessario decidere su un ID di origine che lo identifichi. Se più watchdog di hello stesso tipo sono persone che vivono in hello cluster, si deve segnalare diverse entità o, se si riferiscono hello stessa entità, l'ID di origine diversa di utilizzare o proprietà. In questo modo, i report possono coesistere. proprietà Hello del rapporto di stato hello deve acquisire condizione hello monitorato. (Ad esempio hello precedente, potrebbe essere proprietà hello **ShareSize**.) Se più report applica toohello stessa condizione, hello proprietà deve contenere alcune informazioni dinamiche che consente di toocoexist di report. Ad esempio, più condivisioni necessario toobe monitorati, può essere il nome di proprietà hello **ShareSize sharename**.

> [!NOTE]
> Eseguire *non* utilizzare informazioni di stato tookeep archivio integrità hello. Solo le informazioni correlate di integrità devono essere segnalate come integrità, come la valutazione dell'integrità informazioni hello impatto di un'entità. archivio integrità Hello non è stata progettata come archivio di uso generale. Usa tooaggregate logica di valutazione salute tutti i dati in stato di integrità hello. L'invio di informazioni correlate toohealth (ad esempio segnalazione dello stato con uno stato di integrità di OK) non influisce sulla hello aggregato dello stato di integrità, ma può influire negativamente sulle prestazioni di hello dell'archivio integrità hello.
> 
> 

il punto di decisione Avanti Hello è tooreport quali entità. La maggior parte del tempo di hello, condizione hello chiaramente idetifies hello entità. Scegliere l'entità hello con granularità possibili migliore. Se una condizione influisce su tutte le repliche in una partizione, report sulla partizione di hello, non sul servizio hello. Esistono tuttavia casi particolari che richiedono maggiore attenzione. Se la condizione hello influisce su un'entità, ad esempio una replica, ma hello desiderio è toohave hello condizione contrassegnati per più di durata hello del ciclo di vita di replica, quindi deve essere segnalato nella partizione hello. In caso contrario, quando viene eliminato replica hello, archivio integrità hello Pulisce tutti i relativi report. Durata hello delle entità hello e report hello necessario valutare i writer di watchdog. È necessario specificare chiaramente quando rimuovere un report da un archivio, ad esempio quando un errore segnalato per un'entità non si verifica più.

Esaminiamo un esempio che riunisce punti hello descritto. Si consideri un'applicazione di Service Fabric composta da un servizio master con stato persistente e servizi secondari senza stato distribuiti in tutti i nodi, ovvero un tipo di servizio secondario per ogni tipo di attività. master Hello dispone di una coda di elaborazione che contiene i comandi toobe eseguita dal database secondari. repliche secondarie Hello eseguire le richieste in ingresso hello e l'invio acknowledgement indietro segnali. Una condizione che può essere necessario monitorare è lunghezza hello della coda di elaborazione principale hello. Se lunghezza coda master hello raggiunge una soglia, viene segnalato un avviso. avviso di Hello indica che le repliche secondarie hello non è possibile gestire il carico di hello. Se la coda hello raggiunge la lunghezza massima di hello e i comandi vengono eliminati, viene restituito un errore, come hello servizio non è possibile ripristinare. Hello i report possono essere proprietà hello **QueueStatus**. watchdog Hello si trova all'interno del servizio hello e vengono inviata periodicamente nella replica primaria master hello. tempo di Hello toolive è due minuti, e vengono inviato periodicamente ogni 30 secondi. Se si arresta hello primario, i report di hello viene pulito automaticamente dall'archivio. Se la replica del servizio hello è attivo, ma si verifica il deadlock o altri problemi, hello scadenza nell'archivio integrità hello di report. In questo caso, l'entità hello viene valutata in errore.

Un'altra condizione che può essere monitorata è il tempo di esecuzione delle attività. Hello master distribuisce le attività secondarie toohello in base al tipo di attività hello. A seconda della progettazione di hello, master hello Impossibile eseguire il polling di database secondari hello per lo stato dell'attività. Anche potrebbe attendere repliche secondarie toosend indietro riconoscimento segnala quando vengono eseguite. Nel secondo caso hello, prestare attenzione toodetect situazioni in cui vengono persi datati secondari o i messaggi. Un'opzione è per hello master toosend un toohello richiesta ping stessa secondaria, che consente di inviare nuovamente il relativo stato. Se viene ricevuto nessuno stato, master hello considera un errore e ripianifica l'attività hello. Questo comportamento presuppone che l'attività hello idempotente.

condizione Hello monitorato può essere convertiti come un avviso se l'attività hello è stata eseguita in un certo periodo di tempo (**t1**, ad esempio 10 minuti). Se l'attività hello non è stato completato nel tempo (**t2**, ad esempio 20 minuti), condizione hello monitorato può essere convertiti come errore. Questo tipo di report può essere creato in diversi modi:

* replica primaria master Hello report periodicamente su se stesso. È possibile avere una proprietà per tutte le attività in sospeso nella coda di hello. Se almeno una delle attività richiede più tempo, hello segnalare lo stato di proprietà hello **PendingTasks** è un avviso o errore, come appropriato. Se non sono presenti attività in sospeso o tutte le attività ha avviato l'esecuzione, lo stato di report hello è OK. attività Hello sono persistenti. Se hello primario diventa inattiva, primario hello appena promosso può continuare tooreport correttamente.
* Un altro processo watchdog (in cloud hello o esterne) Controlla attività hello (da esterno, basato sul risultato dell'attività hello desiderato) toosee se vengono completati. Se non si rispettano le soglie di hello, nel servizio master hello viene inviato un report. Un report viene inviato anche a ogni attività che include come identificatore di attività, hello **PendingTask + taskId**. I report dovranno essere inviati solo sugli stati non integri. Impostare ora toolive tooa alcuni minuti e contrassegnare hello report toobe rimosso dopo la scadenza tooensure pulizia.
* Hello secondario che esegue un'attività segnala quando sono necessari più di toorun previsto. Report sull'istanza del servizio hello sulla proprietà hello **PendingTasks**. report Hello individua l'istanza del servizio hello che presenta problemi, ma non acquisisce i situazione hello in interruzione e istanza hello. i report di Hello vengono puliti quindi. Report sulle servizio secondario hello. Se hello secondario viene completata l'attività hello, istanza secondaria hello Cancella report hello dall'archivio hello. report di Hello non acquisisce situazione hello in cui il messaggio di riconoscimento hello viene perso e attività hello non è stato completato dal punto di vista di hello master.

Tuttavia hello reporting avviene hello casi sopra descritti, i report di hello vengono acquisiti in integrità dell'applicazione quando viene valutata l'integrità.

## <a name="report-periodically-vs-on-transition"></a>Report periodici e report in caso di transizione a confronto
Tramite integrità hello modello di report, watchdog puoi inviare report periodicamente o sulle transizioni. Hello consigliato per watchdog reporting è periodicamente, poiché il codice hello tooerrors molto più semplice e meno soggetto. watchdog Hello deve cercare toobe semplice come tooavoid possibili bug che attivano i report non corretti. Eventuali report che segnalano erroneamente la *mancata integrità* influiscono sulla valutazione dell'integrità e sugli scenari basati sull'integrità, inclusi gli aggiornamenti. Corretto *integro* problemi in cluster hello, che non si desidera nascondere i report.

Per la segnalazione periodica, watchdog hello può essere implementata con un timer. Un callback del timer, watchdog hello consentono di controllare lo stato di hello e inviare un report in base allo stato corrente di hello. Non vi è alcun toosee necessità quale report è stato inviato in precedenza o effettuare qualsiasi ottimizzazioni in termini di messaggistica. Hello integrità client dispone di logica toohelp con prestazioni di invio in batch. Mentre il client di integrità hello viene mantenuto attivo, riprovare a eseguire internamente fino a quando il report hello viene riconosciuto dall'archivio integrità hello o watchdog hello genera un report più recente con hello stessa entità, proprietà e origine.

La creazione di report in caso di transizioni richiede una gestione attenta dello stato. watchdog Hello controlla alcune condizioni e segnala solo al variare delle condizioni di hello. Hello capovolta di questo approccio è che sono necessari un minor numero di report. svantaggio Hello è che la logica di watchdog hello hello è complessa. watchdog Hello mantenga le condizioni di hello o report di hello, in modo che possano essere ispezionato toodetermine cambiamenti di stato. In caso di failover, prestare attenzione con report aggiunto, ma non ancora inviati toohello dell'archivio integrità. numero di sequenza Hello deve essere crescente. In caso contrario, i report di hello vengono rifiutati come non aggiornata. In casi rari hello in cui si verifica la perdita di dati, la sincronizzazione potrebbe essere necessario tra stato hello del reporter hello e lo stato di hello dell'archivio integrità hello.

La creazione di report relativi alle transizioni risulta utile per i servizi che inviano report relativi a se stessi, tramite `Partition` o `CodePackageActivationContext`. Hello quando l'oggetto locale (replica o un servizio distribuito pacchetto / applicazione distribuita) viene rimosso, vengono rimossi anche tutti i relativi report. La pulizia automatica vengono ridotti i hello necessità di sincronizzazione tra reporter e archivio integrità. Se il report di hello è per la partizione padre o l'applicazione padre, prestare attenzione per i report non aggiornato failover tooavoid nell'archivio integrità hello. La logica, è necessario aggiungere stato corretto di toomaintain hello e report crittografato hello dall'archivio quando non è più necessario.

## <a name="implement-health-reporting"></a>Implementare report sull'integrità
Una volta hello dettagli entità e i report sono chiare, l'invio di rapporti di stato può essere eseguita tramite API di hello, PowerShell o REST.

### <a name="api"></a>API
tooreport tramite hello API, è necessario un tipo di entità toohello specifico report di integrità desiderati tooreport su toocreate. Fornire hello report tooa integrità client. In alternativa, creare informazioni di stato e passarlo toocorrect metodi per il reporting in `Partition` o `CodePackageActivationContext` tooreport sulle entità corrente.

Hello riportato di seguito periodica reporting da un controllo all'interno di cluster hello. watchdog Hello controlla se è possibile accedere da una risorsa esterna all'interno di un nodo. risorsa Hello è richiesta da un manifesto del servizio all'interno di un'applicazione hello. Se la risorsa hello è disponibile, hello altri servizi all'interno di un'applicazione hello possono comunque funzionare correttamente. Di conseguenza, i report di hello viene inviato nell'entità di pacchetto del servizio distribuito hello ogni 30 secondi.

```csharp
private static Uri ApplicationName = new Uri("fabric:/WordCount");
private static string ServiceManifestName = "WordCount.Service";
private static string NodeName = FabricRuntime.GetNodeContext().NodeName;
private static Timer ReportTimer = new Timer(new TimerCallback(SendReport), null, 30 * 1000, 30 * 1000);
private static FabricClient Client = new FabricClient(new FabricClientSettings() { HealthReportSendInterval = TimeSpan.FromSeconds(0) });

public static void SendReport(object obj)
{
    // Test whether hello resource can be accessed from hello node
    HealthState healthState = this.TestConnectivityToExternalResource();

    // Send report on deployed service package, as hello connectivity is needed by hello specific service manifest
    // and can be different on different nodes
    var deployedServicePackageHealthReport = new DeployedServicePackageHealthReport(
        ApplicationName,
        ServiceManifestName,
        NodeName,
        new HealthInformation("ExternalSourceWatcher", "Connectivity", healthState));

    // TODO: handle exception. Code omitted for snippet brevity.
    // Possible exceptions: FabricException with error codes
    // FabricHealthStaleReport (non-retryable, hello report is already queued on hello health client),
    // FabricHealthMaxReportsReached (retryable; user should retry with exponential delay until hello report is accepted).
    Client.HealthManager.ReportHealth(deployedServicePackageHealthReport);
}
```

### <a name="powershell"></a>PowerShell
Inviare report sull'integrità con **Send-ServiceFabric*TipoEntità*HealthReport**.

Hello riportato di seguito periodica reporting sui valori della CPU in un nodo. report Hello devono essere inviati ogni 30 secondi, e hanno un tempo toolive di due minuti. Se scadono, reporter hello presenta problemi, in modo nodo hello viene valutata in errore. Quando hello della CPU è superiore alla soglia specificata, report hello ha uno stato di integrità di avviso. Quando hello della CPU rimane superiore alla soglia specificata per più di tempo hello configurato, verrà segnalato come errore. In caso contrario, reporter hello invia uno stato di integrità di OK.

```powershell
PS C:\> Send-ServiceFabricNodeHealthReport -NodeName Node.1 -HealthState Warning -SourceId PowershellWatcher -HealthProperty CPU -Description "CPU is above 80% threshold" -TimeToLiveSec 120

PS C:\> Get-ServiceFabricNodeHealth -NodeName Node.1
NodeName              : Node.1
AggregatedHealthState : Warning
UnhealthyEvaluations  :
                        Unhealthy event: SourceId='PowershellWatcher', Property='CPU', HealthState='Warning', ConsiderWarningAsError=false.

HealthEvents          :
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 5
                        SentAt                : 4/21/2015 8:01:17 AM
                        ReceivedAt            : 4/21/2015 8:02:12 AM
                        TTL                   : Infinite
                        Description           : Fabric node is up.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : ->Ok = 4/21/2015 8:02:12 AM

                        SourceId              : PowershellWatcher
                        Property              : CPU
                        HealthState           : Warning
                        SequenceNumber        : 130741236814913394
                        SentAt                : 4/21/2015 9:01:21 PM
                        ReceivedAt            : 4/21/2015 9:01:21 PM
                        TTL                   : 00:02:00
                        Description           : CPU is above 80% threshold
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : ->Warning = 4/21/2015 9:01:21 PM
```

Hello esempio seguente segnala un avviso temporaneo in una replica. Ottiene innanzitutto hello ID di partizione e quindi hello ID replica del servizio di hello che è interessato. Invia quindi un report da **PowershellWatcher** sulla proprietà hello **ResourceDependency**. report Hello è di particolare interesse per due minuti e viene rimosso dall'archivio hello automaticamente.

```powershell
PS C:\> $partitionId = (Get-ServiceFabricPartition -ServiceName fabric:/WordCount/WordCount.Service).PartitionId

PS C:\> $replicaId = (Get-ServiceFabricReplica -PartitionId $partitionId | where {$_.ReplicaRole -eq "Primary"}).ReplicaId

PS C:\> Send-ServiceFabricReplicaHealthReport -PartitionId $partitionId -ReplicaId $replicaId -HealthState Warning -SourceId PowershellWatcher -HealthProperty ResourceDependency -Description "hello external resource that hello primary is using has been rebooted at 4/21/2015 9:01:21 PM. Expect processing delays for a few minutes." -TimeToLiveSec 120 -RemoveWhenExpired

PS C:\> Get-ServiceFabricReplicaHealth  -PartitionId $partitionId -ReplicaOrInstanceId $replicaId


PartitionId           : 8f82daff-eb68-4fd9-b631-7a37629e08c0
ReplicaId             : 130740415594605869
AggregatedHealthState : Warning
UnhealthyEvaluations  :
                        Unhealthy event: SourceId='PowershellWatcher', Property='ResourceDependency', HealthState='Warning', ConsiderWarningAsError=false.

HealthEvents          :
                        SourceId              : System.RA
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 130740768777734943
                        SentAt                : 4/21/2015 8:01:17 AM
                        ReceivedAt            : 4/21/2015 8:02:12 AM
                        TTL                   : Infinite
                        Description           : Replica has been created.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : ->Ok = 4/21/2015 8:02:12 AM

                        SourceId              : PowershellWatcher
                        Property              : ResourceDependency
                        HealthState           : Warning
                        SequenceNumber        : 130741243777723555
                        SentAt                : 4/21/2015 9:12:57 PM
                        ReceivedAt            : 4/21/2015 9:12:57 PM
                        TTL                   : 00:02:00
                        Description           : hello external resource that hello primary is using has been rebooted at 4/21/2015 9:01:21 PM. Expect processing delays for a few minutes.
                        RemoveWhenExpired     : True
                        IsExpired             : False
                        Transitions           : ->Warning = 4/21/2015 9:12:32 PM
```

### <a name="rest"></a>REST
Inviare i rapporti di stato tramite REST con le richieste POST che passare entità toohello desiderato e nella descrizione del report integrità hello hello corpo. Ad esempio, vedere come toosend REST [report sull'integrità del cluster](https://docs.microsoft.com/rest/api/servicefabric/report-the-health-of-a-cluster) o [rapporti di stato del servizio](https://docs.microsoft.com/rest/api/servicefabric/report-the-health-of-a-service). Sono supportate tutte le entità.

## <a name="next-steps"></a>Passaggi successivi
In base ai dati di integrità hello, gli autori del servizio e gli amministratori di cluster/applicazione possono essere considerato di informazioni di hello tooconsume modi. Ad esempio possibile impostare avvisi basati sui problemi gravi toocatch lo stato di integrità prima che essi provocare interruzioni. Gli amministratori possono anche impostare i problemi di riparazione sistemi toofix automaticamente.

[Introduzione tooService integrità infrastruttura monitoraggio](service-fabric-health-introduction.md)

[Come visualizzare i report sull'integrità di Service Fabric](service-fabric-view-entities-aggregated-health.md)

[Come tooreport e controllo del servizio integrità](service-fabric-diagnostics-how-to-report-and-check-service-health.md)

[Uso dei report sull'integrità del sistema per la risoluzione dei problemi](service-fabric-understand-and-troubleshoot-with-system-health-reports.md)

[Monitorare e diagnosticare servizi in locale](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[Aggiornamento di un'applicazione di infrastruttura di servizi](service-fabric-application-upgrade.md)

