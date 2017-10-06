---
title: ripristino di emergenza di Service Fabric aaaAzure | Documenti Microsoft
description: "Azure Service Fabric offre hello toodeal necessarie di funzionalità con tutti i tipi di situazioni di emergenza. Questo articolo vengono descritti i tipi di hello di emergenze che possono verificarsi e come toodeal con essi."
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: ab49c4b9-74a8-4907-b75b-8d2ee84c6d90
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 04b8348fb63e8a1c76a8f722c4c8255b339908e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="disaster-recovery-in-azure-service-fabric"></a>Ripristino di emergenza in Azure Service Fabric
Una parte fondamentale della distribuzione a disponibilità elevata consiste nel garantire la resistenza dei servizi a tutti i tipi di errori. Ciò è particolarmente importante per gli errori imprevisti e incontrollabili. Questo articolo descrive alcune modalità di errore comuni che possono generare situazioni di emergenza se non organizzate e gestite correttamente. Inoltre illustrate tootake le misure di attenuazione e le azioni se si è verificata un'emergenza comunque. obiettivo di Hello è toolimit o eliminare il rischio di hello del tempo di inattività o perdita di dati quando si verificano errori, pianificati o in caso contrario, si verificano.

## <a name="avoiding-disaster"></a>Evitare situazioni di emergenza
Obiettivo principale di Service Fabric è toohelp l'ambiente sia i servizi in modo che i tipi di errore comuni non sono emergenze del modello. 

Esistono, in generale, due tipi di scenari di emergenza/errore:

1. Errori hardware o software
2. Errori operativi

### <a name="hardware-and-software-faults"></a>Errori hardware e software
Gli errori hardware e software sono imprevedibili. gli errori toosurvive modo più semplici Hello è in esecuzione più copie del servizio hello occupate attraverso i limiti di errore hardware o software. Ad esempio, se il servizio viene eseguito solo su un determinato computer, quindi hello errore di un computer è una situazione di emergenza per il servizio. Hello semplice tooavoid questo tipo di emergenza è tooensure che hello sia effettivamente in esecuzione su più computer. Test è errore hello tooensure necessarie di una macchina non interrotta hello in esecuzione del servizio. Pianificazione della capacità garantisce un'istanza di sostituzione possono essere creata in un' posizione e che la riduzione della capacità non eseguire l'overload hello rimanenti servizi. Hello stesso modello funziona indipendentemente dal fatto che si sta tentando errore hello tooavoid di. Ad esempio, Se si teme errore hello di una rete SAN, si esegue tra più nomi alternativi del soggetto. Se si teme la perdita di hello di un rack di server, di eseguire in più rack. Se si ritiene che la perdita di hello dei centri dati, il servizio deve essere eseguito in più aree di Azure o Data Center. 

Quando si esegue questo tipo di modalità estesi, si è ancora soggetto toosome tipi di errori simultanei, ma solo errori anche più di un determinato tipo (ad esempio: un singolo errore collegamento di una macchina virtuale o di rete) vengono gestiti automaticamente (e pertanto non è più di "emergenza"). Service Fabric fornisce molti meccanismi per l'espansione di cluster hello e gli handle di restituzione di nodi con errori e i servizi. Service Fabric inoltre consente di eseguire molte istanze dei servizi in ordine tooavoid questi tipi di errori non pianificati da attivare in emergenze reale.

È possibile motivi per cui eseguire una toospan sufficientemente grande distribuzione negli errori non praticabile. Ad esempio, potrebbe richiedere altre risorse hardware che non si è disposti toopay per toohello relativa probabilità di errore. Quando si lavora con le applicazioni distribuite, è possibile che gli hop di comunicazione o i costi di replica di stato aggiuntivi su distanze geografiche causino una latenza inaccettabile. La posizione di questa linea di confine varia per ogni applicazione. Per gli errori software, in particolare, errore hello potrebbe essere in servizio hello che si sta tentando di tooscale. In questo caso più copie non impediscano emergenza hello, poiché la condizione di errore hello è correlata a tutte le istanze di hello.

### <a name="operational-faults"></a>Errori operativi
Anche se il servizio viene eseguito lo spanning tutto il mondo hello con molti ridondanze, è comunque possibile sperimentare disastrosi eventi. Ad esempio, se un utente riconfigura nome dns hello servizio hello, accidentalmente o eliminarlo definitive. Si supponga, ad esempio, di disporre di un servizio di Service Fabric con stato e che un utente lo abbia eliminato inavvertitamente. A meno che non esistano alcune riduzione dei rischi, che il servizio e tutte le hello stato è finalmente disponibile. Questi tipi di emergenze operative ("errori") richiedono mitigazioni e procedure per il ripristino diverse rispetto ai normali errori imprevisti. 

questi tipi di errori operational tooavoid modi migliori Hello devono
1. limitare l'ambiente di accesso operativi toohello
2. controllare rigorosamente le operazioni pericolose
3. imporre l'automazione, impedire manuale o modifiche fuori banda e convalidare le modifiche specifiche su ambiente effettivo hello prima dell'applicazione delle loro
4. assicurarsi che le operazioni distruttive siano "soft". Le operazioni soft non hanno effetto immediato o possono essere annullate entro un intervallo di tempo.

Service Fabric fornisce alcuni meccanismi errori operational tooprevent, ad esempio fornire [basata sui ruoli](service-fabric-cluster-security-roles.md) controllo dell'accesso per le operazioni del cluster. La maggior parte di questi errori operativi richiede tuttavia attività organizzative e altri sistemi. Service Fabric offre alcuni meccanismi per resistere agli errori operativi, i più noti dei quali sono il backup e il ripristino per i servizi con stato.

## <a name="managing-failures"></a>Gestione degli errori
obiettivo di Hello di Service Fabric è quasi sempre la gestione automatica degli errori. Tuttavia, in ordine toohandle alcuni tipi di errori, è necessario utilizzare codice aggiuntivo. Altri tipi di errori _non_ devono essere risolti automaticamente per motivi di continuità e sicurezza aziendali. 

### <a name="handling-single-failures"></a>Gestione di errori singoli
I computer singoli possono essere soggetti a errori per ogni genere di motivo. Alcuni di questi sono causati dall'hardware, ad esempio i guasti agli alimentatori e all'hardware di rete. Altri errori sono nel software. Sono inclusi errori di sistema operativo effettiva hello e servizio hello stesso. Service Fabric rileva automaticamente questi tipi di errori, inclusi i casi in cui la macchina hello diventa isolata dagli altri computer a causa di problemi di toonetwork.

Indipendentemente dal tipo di hello del servizio, in esecuzione una sola istanza risultati tempi di inattività per il servizio se tale singola copia di codice hello non riesce per qualsiasi motivo. 

In ordine toohandle qualsiasi errore, hello più semplice possibile è tooensure che i servizi eseguiti in più di un nodo per impostazione predefinita. Per i servizi senza stato questo risultato si ottiene con un `InstanceCount` maggiore di 1. Per i servizi con stati, indicazione minimo hello è sempre un `TargetReplicaSetSize` e `MinReplicaSetSize` almeno 3. L'esecuzione di più copie del codice del servizio assicura al servizio la capacità di gestire qualsiasi errore automaticamente. 

### <a name="handling-coordinated-failures"></a>Gestione di errori coordinati
Coordinati gli errori possono verificarsi in un cluster a causa di tooeither pianificata o errori dell'infrastruttura non pianificato e le modifiche o modifiche software pianificato. Service Fabric crea le zone di infrastruttura che sperimentano errori coordinati come domini di errore. Le aree che sperimentano le modifiche software coordinate vengono modellate come domini di aggiornamento. Altre informazioni sui domini di errore e di aggiornamento sono disponibili in [questo documento](service-fabric-cluster-resource-manager-cluster-description.md) che descrive la definizione e la topologia del cluster.

Per impostazione predefinita, Service Fabric considera i domini di errore e di aggiornamento quando si pianificano le posizioni di esecuzione dei servizi. Per impostazione predefinita, Service Fabric prova tooensure i servizi eseguiti in diversi domini di errore e di aggiornamento in modo se le modifiche pianificate o i servizi rimangono disponibili. 

Ad esempio, si supponga che una fonte di alimentazione in errore determina un rack di toofail macchine contemporaneamente. Con più copie del servizio hello perdita hello di molti computer è in esecuzione nel dominio di errore diventa infatti un altro esempio di errore solo per un determinato servizio. Ecco perché la gestione di domini di errore è critico tooensuring elevata disponibilità dei servizi. Quando si esegue Azure Service Fabric, i domini di errore vengono gestiti automaticamente. In altri ambienti potrebbero non esserlo. Se si sta creando cluster in locale, toomap verificare e pianificare correttamente il layout di dominio di errore.

Domini di aggiornamento sono utili per la modellazione delle aree in cui software verrà aggiornato toobe in hello stesso tempo. Per questo motivo, domini di aggiornamento anche spesso definiscono i limiti di hello in software è disattivato durante gli aggiornamenti pianificati. Gli aggiornamenti di Service Fabric e i servizi seguono hello stesso modello. Per ulteriori informazioni sul modello di integrità di Service Fabric hello che consente di evitare modifiche accidentali conseguenze cluster hello e il servizio, i domini di aggiornamento gli aggiornamenti in sequenza, vedere questi documenti:

 - [Aggiornamento dell'applicazione](service-fabric-application-upgrade.md)
 - [Esercitazione sull'aggiornamento di un'applicazione ](service-fabric-application-upgrade-tutorial.md)
 - [Service Fabric Health Model](service-fabric-health-introduction.md) (Modello di integrità di Service Fabric)

È possibile visualizzare il layout di hello del cluster tramite fornita nella mappa del cluster hello [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md):

<center>
![Nodi distribuiti nei domini di errore in Service Fabric Explorer][sfx-cluster-map]
</center>

> [!NOTE]
> Modellazione di aree di errore, aggiornamenti in sequenza, l'esecuzione di molte istanze di servizio codice e stato, posizionamento regole tooensure i servizi eseguito tra domini di errore e di aggiornamento e il monitoraggio dello stato predefinito sono solo **alcuni** di hello funzionalità che fornisce Service Fabric in problemi operativi di ordine tookeep normale e gli errori di attivazione in situazioni di emergenza. 
>

### <a name="handling-simultaneous-hardware-or-software-failures"></a>Gestione di errori hardware o software simultanei
Si è parlato finora degli errori singoli. Come si può notare, sono facilmente toohandle per i servizi senza stato mantenendo più copie di codice hello (e stato) in esecuzione in errore e domini di aggiornamento. I servizi possono essere interessati anche da più errori casuali simultanei. Si tratta probabilmente emergenza effettivo di tooan toolead.


### <a name="random-failures-leading-tooservice-failures"></a>Errori casuali iniziali tooservice errori
Si supponga che il servizio hello aveva un `InstanceCount` di 5 e diversi nodi tali istanze in esecuzione tutti non è riuscito a hello stesso tempo. Service Fabric risponde creando automaticamente istanze sostitutive in altri nodi. Creazione di sostituzioni fino a quando non è nuovamente disponibile il servizio hello tooits desiderato conteggio delle istanze continuerà. Ad esempio, si supponga che si è verificato un servizio senza stato con un `InstanceCount`-1, ovvero viene eseguito in tutti i nodi del cluster hello validi. Si supponga che alcuni di tali istanze sono state toofail. In questo caso, Service Fabric nota che il servizio di hello non è nello stato desiderato e tenta di istanze di hello toocreate sui nodi di hello in cui sono disponibili. 

Per i servizi con stati situazione hello varia a seconda se il servizio hello ha uno stato persistente o non. Dipende inoltre quanti repliche hello servizio e il numero non è riuscito. La determinazione di una situazione di emergenza per un servizio con stato e la relativa gestione seguono tre fasi:

1. Determinazione di una eventuale perdita del quorum
 - Una perdita del quorum è qualsiasi momento la maggioranza delle repliche hello di un servizio con stato non sono attivi in hello stessa durata, comprendenti hello primario.
2. Determinare se la perdita di quorum hello è permanente
 - La maggior parte del tempo di hello, gli errori sono temporanei. I processi, i nodi e le VM vengono riavviati e le partizioni di rete vengono corrette. In alcuni casi invece gli errori sono permanenti. 
    - Per i servizi senza stato persistente, un errore di uno o più quorum di repliche determina _immediatamente_ una perdita del quorum permanente. Quando Service Fabric rileva perdita del quorum in un servizio con stato non persistente, procede immediatamente dataloss toostep 3 dichiarando (potenziali). Procedere toodataloss è utile perché Service Fabric sa che è presente alcun punto in attesa per il backup di hello repliche toocome, perché anche se essi sono stati recuperati potrebbero essere vuote.
    - Per i servizi permanenti con stati, un errore di più di un quorum di repliche causa toostart Service Fabric in attesa di hello nuovamente toocome di repliche e quorum di ripristino. Di conseguenza, un'interruzione del servizio per qualsiasi _scrive_ toohello interessata partizione (o "set di repliche") del servizio hello. Le operazioni di lettura restano invece ancora possibili con una minore garanzia di coerenza. quantità di tempo di attesa di Service Fabric per toobe quorum ripristinato predefinita Hello è infinito, poiché è un evento dataloss (potenzialmente) e comporta altri rischi di procedere. Eseguire l'override hello predefinito `QuorumLossWaitDuration` valore, è possibile ma non è consigliato. In questo momento, invece tutte le attività devono essere apportate hello toorestore verso il basso le repliche. È necessario riportare hello nodi che sono inattivi back backup e garantire che è possibile rimontare unità hello in cui sono archiviati lo stato permanente locale hello. Se perdita del quorum hello è causata da un errore di processo, Service Fabric tenta processi hello toorecreate e riavviare automaticamente le repliche di hello in essi contenuti. Se l'operazione non riesce, Service Fabric segnala errori di integrità. Se questi possono essere risolti repliche hello in genere tornare. In alcuni casi, tuttavia, repliche hello non possono essere riportate. Ad esempio, le unità hello tutti non è riuscito o macchine hello fisicamente eliminati definitivamente in qualche modo. In questi casi ci si trova in presenza di un evento di perdita del quorum permanente. tootell Service Fabric toostop in attesa di hello verso il basso toocome repliche, un amministratore di cluster è necessario determinare quali partizioni dei quali servizi sono interessati e chiamare hello `Repair-ServiceFabricPartition -PartitionId` o ` System.Fabric.FabricClient.ClusterManagementClient.RecoverPartitionAsync(Guid partitionId)` API.  Questa API consente di specificare l'ID di hello di hello partizione toomove fuori QuorumLoss e in dataloss potenziale.

> [!NOTE]
> È _mai_ toouse provvisoria questa API diverso nella modalità in partizioni specifiche. 
>

3. Determinazione se vi è stata una effettiva perdita di dati e ripristino da backup
  - Quando Service Fabric chiama hello `OnDataLossAsync` è sempre il metodo _sospetti_ dataloss. Service Fabric assicura che la chiamata viene recapitata toohello _migliore_ replica rimanente. Si tratta indipendentemente da quale replica avanzamento hello la maggior parte delle. Hello motivo diciamo sempre _sospetti_ dataloss è che è possibile che la replica rimanenti hello ha effettivamente tutti stesso stato hello primario aveva quando è arrestato. Tuttavia, senza toocompare tale stato è, non è valida per Service Fabric o operatori tooknow con certezza. A questo punto, Service Fabric conosce hello altre repliche non sono confermata. Che è stata effettuata quando si è arrestato in attesa di tooresolve di perdita di quorum hello stesso decisione di hello. Hello migliore per il servizio hello è in genere toofreeze e attendere un intervento amministrativo specifico. Pertanto, cosa che un'implementazione tipica di hello `OnDataLossAsync` metodo eseguire?
  - Registra prima di tutto che è stato generato un evento `OnDataLossAsync` e genera tutti i necessari avvisi amministrativi.
   - In genere a questo punto, toopause e attendere ulteriormente le decisioni e azioni manuali toobe eseguita. Infatti, anche se sono disponibili backup può essere necessario toobe preparato. Ad esempio, se i due servizi diversi coordinano informazioni, questi backup potrebbe essere necessario toobe modificato in ordine tooensure che dopo il ripristino di hello si verifica che le informazioni di hello questi due servizi interessano è coerente. 
  - Spesso è anche alcuni altri dati di telemetria o di scarico dal servizio hello. Questi metadati possono essere contenuti in altri servizi o in registri. Queste informazioni possono essere utilizzati toodetermine necessari se si sono verificati eventuali chiamate ricevuto ed elaborato in hello primario che non erano presenti in una determinata replica di backup o replicato toothis hello. Prima di ripristino è possibile, questi potrebbe essere necessario toobe toohello riprodotta o è stato aggiunto backup.  
   - Confronti di hello rimanenti toothat lo stato della replica contenuti in tutti i backup disponibili. Se l'utilizzo di raccolte affidabile di hello Service Fabric quindi sono disponibili strumenti e processi disponibile per questa operazione, descritti in [questo articolo](service-fabric-reliable-services-backup-restore.md). obiettivo di Hello è toosee se lo stato di hello all'interno di replica hello è sufficiente o anche il backup di hello potrebbe mancare.
  - Una volta in cui viene eseguito confronto hello e se è stata completata ripristino necessarie hello, codice del servizio hello deve restituire true se sono state apportate le modifiche di stato. Se replica hello determinato che era hello meglio disponibili copia dello stato di hello e non apportata alcuna modifica, restituisce false. True indica che qualsiasi _altra_ replica rimanente potrebbe ora essere incoerente con questa. Le repliche rimanenti verranno eliminate e ricreate da questa replica. False indica che non stato sono state apportate modifiche, pertanto hello consente di mantenere cosa hanno altre repliche. 

È estremamente importante che gli autori del servizio applichino gli scenari di errore e di potenziale perdita di dati prima che i servizi vengano distribuiti nell'ambiente di produzione. tooprotect contro il possibilità hello di dataloss, è importante tooperiodically [eseguire il backup dello stato di hello](service-fabric-reliable-services-backup-restore.md) di qualsiasi del Negozio con ridondanza geografica tooa servizi con stato. È anche necessario assicurarsi di aver toorestore possibilità hello è. Poiché i backup di numerosi servizi diversi vengono eseguiti in momenti diversi, è necessario tooensure dopo il ripristino dei servizi dispongano di una visualizzazione coerenza tra loro. Ad esempio, si consideri una situazione in cui un servizio genera un numero e archivia e la invia tooanother servizio che viene inoltre archiviato. Dopo un ripristino, è possibile riscontrare che secondo servizio hello è il numero di hello differenza hello prima di tutto, poiché il backup non include tale operazione.

Se si scopre che hello rimanenti le repliche sono insufficienti toocontinue da in uno scenario dataloss e non è possibile ricostruire lo stato del servizio dalla telemetria o di scarico, frequenza di hello dei backup determina l'obiettivo del punto di ripristino (RPO) migliore . Service Fabric include molti strumenti per testare vari scenari di errore, tra cui il quorum permanente e la perdita di dati che richiede il ripristino da un backup. Questi scenari sono inclusi come parte di strumenti di testabilità dell'infrastruttura servizio gestito da hello errore Analysis Services. Altre informazioni su questi strumenti e criteri sono disponibili [qui](service-fabric-testability-overview.md). 

> [!NOTE]
> Servizi di sistema possono inoltre subire una perdita di quorum, con un impatto hello viene toohello specifico servizio in questione. Ad esempio perdita del quorum nel servizio di denominazione hello influisce sulla risoluzione dei nomi, mentre perdita del quorum nel servizio di gestione failover hello blocca i failover e la creazione del nuovo servizio. Mentre i servizi di sistema di Service Fabric hello seguono hello stesso schema come i servizi per la gestione dello stato, non è consigliabile che è consigliabile tentare toomove loro fuori perdita del Quorum e in dataloss potenziale. indicazione di Hello è invece troppo[seek supporto](service-fabric-support.md) toodetermine una soluzione destinata tooyour specifica situazione.  In genere è preferibile toosimply attesa finché hello verso il basso le repliche restituite.
>

## <a name="availability-of-hello-service-fabric-cluster"></a>Disponibilità del cluster di Service Fabric hello
In generale, i cluster di Service Fabric hello stesso è un ambiente ampiamente distribuito senza singoli punti di errore. Un errore di un qualsiasi nodo non comporta la disponibilità o problemi di affidabilità per cluster hello, principalmente perché servizi di sistema di Service Fabric hello seguono hello stesse linee guida fornite in precedenza: essere sempre eseguiti con tre o più repliche per impostazione predefinita e tutti i nodi vengono eseguiti i servizi di sistema che sono senza stati. rete di Service Fabric sottostante Hello e livelli di rilevamento di errori sono completamente distribuiti. La maggior parte dei servizi di sistema può essere ricompilati dai metadati cluster hello o sapere come tooresynchronize lo stato da altre posizioni. disponibilità Hello hello cluster potrebbe essere compromessa se servizi di sistema visualizzato in quorum perdita situazioni come quelle descritte sopra. In questi casi potrebbe non essere in grado di tooperform determinate operazioni nel cluster hello come avviare un aggiornamento o la distribuzione di nuovi servizi, ma i cluster hello stesso sia ancora attivo. Servizi in esecuzione rimarrà in esecuzione in queste condizioni a meno che non richiedono operazioni di scrittura toohello sistema servizi toocontinue funzionante. Ad esempio, in caso di perdita di quorum hello gestione Failover tutti i servizi continuerà toorun, ma tutti i servizi che non soddisfano non saranno in grado di tooautomatically riavvio, poiché questo richiede il coinvolgimento di hello di hello gestione Failover. 

### <a name="failures-of-a-datacenter-or-azure-region"></a>Errori di un data center o un'area di Azure
In rari casi, può diventare temporaneamente disponibile a causa di un data center fisico tooloss di alimentazione o connettività di rete. In questi casi i cluster e i servizi di Service Fabric presenti nel data center o nell'area di Azure non saranno disponibili. _I dati saranno tuttavia preservati_. Per i cluster in esecuzione in Azure, è possibile visualizzare gli aggiornamenti su interruzioni in hello [pagina stato Azure][azure-status-dashboard]. In hello altamente improbabile che un centro dati fisico è completamente o parzialmente eliminato definitivamente, tutti i cluster di Service Fabric ospitati non esiste o servizi hello in essi contenuti potrebbero essere persi. Sono inclusi tutti gli stati di cui non è stato eseguito il backup al di fuori del data center o dell'area.

È presente due diverse strategie per il superamento hello errore permanente o prolungato di un singolo Data Center o area geografica. 

1. Eseguire cluster di Service Fabric distinti in più aree e usare un qualche sistema per il failover e il failback tra questi ambienti. Questo tipo di modello multi-cluster attivo-attivo o attivo-passivo richiede codice di gestione e operativo aggiuntivo. È inoltre necessario coordinamento dei backup da servizi di hello in un Data Center o area geografica in modo che siano disponibili in altri Data Center o in aree quando uno ha esito negativo. 
2. Eseguire un singolo cluster di Service Fabric che si estende su più data center o più aree. Hello minimi delle configurazioni supportate per questo oggetto è tre aree o Data Center. Hello numero consigliato di aree o Data Center è cinque. Questo modello richiede una topologia di cluster più complessa. Tuttavia, hello vantaggio di questo modello è che un errore di un Data Center o area geografica viene convertito da una situazione di emergenza in un errore normale. Questi errori possono essere gestiti dai meccanismi hello che funzionano per i cluster in una singola regione. I domini di errore, i domini di aggiornamento e le regole di posizionamento di Service Fabric assicurano che i carichi di lavoro vengano distribuiti in modo da essere in grado di tollerare gli errori normali. Per altre informazioni sui criteri che aiutano a far funzionare i servizi in questo tipo di cluster, leggere l'articolo relativo ai [criteri di posizionamento](service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies.md).

### <a name="random-failures-leading-toocluster-failures"></a>Errori casuali iniziali toocluster errori
Service Fabric esiste il concetto di hello di nodi. Si tratta di nodi che gestiscono la disponibilità di hello del cluster sottostante hello. Questi nodi consentono tooensure hello cluster rimane backup mediante la definizione di lease con gli altri nodi e che funge da spareggi durante determinati tipi di errori di rete. Se errori casuali rimuove una maggioranza dei nodi seme hello cluster hello e non portare indietro, cluster hello automaticamente arrestato. In Azure, i nodi vengono gestiti automaticamente: vengono distribuiti in domini di aggiornamento e di errore disponibile hello e se un nodo singolo valore di inizializzazione viene rimosso dal cluster hello al suo posto verrà creato un altro. 

Nel cluster di Service Fabric autonomo e Azure, "Tipo di nodo primario" hello è hello uno che esegue il seeding di hello. Quando si definisce un tipo di nodo primario, Service Fabric automaticamente sfrutterà numero hello di nodi forniti tramite la creazione di nodi too9 e 9 repliche di ciascuno dei servizi di sistema hello. Se un set di errori casuali accetta contemporaneamente out la maggior parte di tali repliche del servizio di sistema, servizi di sistema hello verranno attivata la perdita del quorum, come descritto sopra. Se la maggioranza dei nodi seme hello viene persa, cluster hello verrà arrestato subito dopo.

## <a name="next-steps"></a>Passaggi successivi
- Informazioni su come toosimulate diversi errori utilizzando hello [framework testabilità](service-fabric-testability-overview.md)
- Lettura di altre risorse sul ripristino di emergenza e sulla disponibilità elevata. Microsoft ha pubblicato molti documenti su questi argomenti. Mentre alcuni di questi documenti si riferiscono toospecific tecniche per l'uso in altri prodotti, contengono molte procedure consigliate generali che è possibile applicare nel contesto di Service Fabric hello anche:
  - [Elenco di controllo della disponibilità](../best-practices-availability-checklist.md)
  - [Esercitazione nel ripristino di emergenza](../sql-database/sql-database-disaster-recovery-drills.md)
  - [Ripristino di emergenza e disponibilità elevata per le applicazioni Azure][dr-ha-guide]
- Informazioni sulle [opzioni di supporto di Service Fabric](service-fabric-support.md)

<!-- External links -->

[repair-partition-ps]: https://msdn.microsoft.com/library/mt163522.aspx
[azure-status-dashboard]:https://azure.microsoft.com/status/
[azure-regions]: https://azure.microsoft.com/regions/
[dr-ha-guide]: https://msdn.microsoft.com/library/azure/dn251004.aspx


<!-- Images -->

[sfx-cluster-map]: ./media/service-fabric-disaster-recovery/sfx-clustermap.png
