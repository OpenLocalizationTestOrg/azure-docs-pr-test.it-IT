---
title: "hello aaaPlanning capacità di cluster di Service Fabric | Documenti Microsoft"
description: "Considerazioni sulla pianificazione della capacità del cluster Service Fabric. Nodetypes, livelli di affidabilità e durata"
services: service-fabric
documentationcenter: .net
author: ChackDan
manager: timlt
editor: 
ms.assetid: 4c584f4a-cb1f-400c-b61f-1f797f11c982
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/24/2017
ms.author: chackdan
ms.openlocfilehash: 83272ce7fefe698eef755cf66493c2874cc3b120
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-cluster-capacity-planning-considerations"></a>Considerazioni sulla pianificazione della capacità del cluster Service Fabric
La pianificazione della capacità è un passaggio importante per qualsiasi distribuzione di produzione. Ecco alcuni degli elementi di hello di aver tooconsider come parte del processo.

* numero di Hello del nodo tipi toostart di esigenze del cluster out con
* proprietà Hello di ogni tipo di nodo (dimensioni, primario e per internet, numero di macchine virtuali e così via).
* Hello e affidabilità caratteristiche del cluster di hello

Ogni aspetto verrà ora esaminato brevemente.

## <a name="hello-number-of-node-types-your-cluster-needs-toostart-out-with"></a>numero di Hello del nodo tipi toostart di esigenze del cluster out con
È innanzitutto necessario toofigure quali cluster hello si sta creando verrà utilizzato per toobe e quali tipi di applicazioni si intende toodeploy in questo cluster. Se non si cancella dal scopo hello del cluster di hello, probabilmente non ancora pronti tooenter hello pianificazione processo.

Stabilire il numero di hello di tipi di nodo che del cluster deve toostart out con.  Ogni tipo di nodo è mappato tooa Set di scalabilità della macchina virtuale. Ogni tipo di nodo può quindi essere aumentato o ridotto in modo indipendente, avere diversi set di porte aperte e avere metriche per la capacità diverse. Pertanto la decisione hello del numero di hello di tipi di nodo essenzialmente un po' toohello seguenti considerazioni:

* L'applicazione dispone di più servizi e uno di essi necessario toobe pubblico o con connessione internet? Le applicazioni tipiche contengono un servizio gateway front-end che riceve l'input da un client e uno o più servizi back-end che comunicano con i servizi front-end hello. In questo caso quindi si finirà per avere almeno due tipi di nodi.
* I servizi (che costituiscono l'applicazione) hanno esigenze diverse per l'infrastruttura, ad esempio cicli di CPU più elevati o una quantità maggiore di RAM? Ad esempio, supponiamo che un'applicazione hello che si desidera toodeploy contiene un servizio front-end e un servizio back-end. Hello front-end servizio può essere eseguito in più piccole macchine virtuali (dimensioni di macchina virtuale come D2) che dispongono delle porte aperte toohello internet.  servizio back-end Hello, tuttavia, è toorun esigenze e richiedono un utilizzo intensivo di calcolo in macchine virtuali di dimensioni maggiori (con dimensioni di macchina virtuale come D4, D6, D15) che non sono internet affiancate.
  
  In questo esempio, anche se è possibile decidere tooput tutti hello servizi nei tipi di nodo, è consigliabile che vengono inseriti in un cluster con due tipi di nodo.  In questo modo per ogni proprietà distinct toohave del tipo di nodo, ad esempio la connessione a internet o di dimensioni della macchina virtuale. numero di Hello di macchine virtuali può essere ridimensionata in modo indipendente, nonché.  
* Poiché non è possibile prevedere hello futuro, passare con fatti che si conoscono e decidere il numero di hello di tipi di nodo che le applicazioni devono toostart con. Sarà sempre possibile aggiungere o rimuovere i tipi di nodi in seguito. Un cluster di Service Fabric deve avere almeno un tipo di nodo.

## <a name="hello-properties-of-each-node-type"></a>proprietà Hello di ogni tipo di nodo
Hello **tipo di nodo** può essere considerata tooroles equivalente in servizi Cloud. Tipi di nodo definiscono dimensioni di macchina virtuale hello, hello numero di macchine virtuali e le relative proprietà. Ogni tipo di nodo definito in un cluster di Service Fabric viene configurato come set di scalabilità di macchine virtuali distinto. Set di scalabilità della macchina virtuale è una risorsa di calcolo di Azure, è possibile utilizzare toodeploy e gestire una raccolta di macchine virtuali come un set. Essendo definito come set di scalabilità di macchine virtuali distinto, ogni tipo di nodo può essere aumentato o ridotto in modo indipendente, avere diversi set di porte aperte e avere metriche per la capacità diverse.

Lettura [questo documento](service-fabric-cluster-nodetypes.md) per ulteriori informazioni sulla relazione hello del set di scalabilità della macchina toovirtual Nodetypes, come tooRDP in una delle istanze di hello, aprire nuove porte e così via.

Il cluster può avere più di un tipo di nodo, ma il tipo di nodo primario hello (primo definiti nel portale di hello hello) deve avere almeno cinque macchine virtuali per cluster utilizzati per i carichi di lavoro (o almeno tre macchine virtuali per i cluster di test). Se si sta creando un modello di gestione delle risorse cluster di hello, quindi cercare **è primario** attributo nella definizione di tipo di nodo hello. tipo di nodo primario Hello è il tipo di nodo hello in cui vengono collocati i servizi di sistema di Service Fabric.  

### <a name="primary-node-type"></a>Tipo di nodo primario
Per un cluster con più tipi di nodo, è necessario toochoose uno di essi toobe primario. Ecco le caratteristiche di hello di un tipo di nodo primario:

* Hello **dimensioni minime delle macchine virtuali** per il tipo di nodo primario hello è determinato da hello **il livello di durabilità** prescelto. valore predefinito di Hello per il livello di durabilità hello è Bronzo. Per informazioni dettagliate su quale livello di durabilità hello e hello valori che possono essere necessari, scorrere verso il basso.  
* Hello **numero minimo di macchine virtuali** per il tipo di nodo primario hello è determinato da hello **livello di affidabilità** prescelto. valore predefinito di Hello per il livello di affidabilità hello è Silver. Per informazioni dettagliate su quale livello di affidabilità hello e hello valori che possono essere necessari, scorrere verso il basso. 


* servizi di sistema di Service Fabric Hello (ad esempio, il servizio di gestione Cluster hello o il servizio di archiviazione di immagini) vengono inseriti nel tipo di nodo primario hello e l'affidabilità di hello in tal caso e durabilità dei cluster hello è determinata dal hello livello valore e durabilità livello di affidabilità valore selezionato per il tipo di nodo primario hello.

![Screenshot di un cluster con due tipi di nodo ][SystemServices]

### <a name="non-primary-node-type"></a>Tipo di nodo non primario
Per un cluster con più tipi di nodo, vi è un tipo di nodo primario e li hello restanti sono non primario. Ecco le caratteristiche di hello di un tipo di nodo non primario:

* dimensioni minime Hello di macchine virtuali per questo tipo di nodo sono determinata dal livello di durabilità hello che prescelto. valore predefinito di Hello per il livello di durabilità hello è Bronzo. Per informazioni dettagliate su quale livello di durabilità hello e hello valori che possono essere necessari, scorrere verso il basso.  
* numero minimo Hello di macchine virtuali per questo tipo di nodo può essere uno. Tuttavia è consigliabile scegliere questo numero in base al numero di hello delle repliche di hello applicazioni e servizi che si desidera toorun in questo tipo di nodo. numero di Hello di macchine virtuali in un tipo di nodo può essere aumentato dopo aver distribuito il cluster hello.

## <a name="hello-durability-characteristics-of-hello-cluster"></a>caratteristiche di durabilità Hello del cluster di hello
il livello di durabilità Hello è usato tooindicate toohello hello privilegi contenenti le macchine virtuali con l'infrastruttura di Azure sottostante hello. Nel tipo di nodo primario hello, questo privilegio consente a Service Fabric toopause qualsiasi richiesta infrastruttura livello macchina virtuale (ad esempio, un riavvio della VM, ricreare l'immagine macchina virtuale o migrazione della macchina virtuale) che influire sui requisiti di quorum hello per servizi di sistema hello e i servizi con stati. Nei tipi di nodo non primario hello, questo privilegio consente a Service Fabric toopause delle richieste di infrastruttura livello macchina virtuale come riavvio della VM, ricreare l'immagine VM, migrazione della macchina virtuale e così via, influire sui requisiti di quorum hello per i servizi con stati in esecuzione.

Questo privilegio è espresso nell'hello seguenti valori:

* Oro - infrastruttura hello processi possono essere sospeso per una durata di due ore per UD. La durata Gold può essere abilitata solo per gli SKU VM con tutti i nodi come D15_V2, G5 e così via.
* Argento - hello i processi di infrastruttura può essere sospeso per una durata di 10 minuti per UD ed è disponibili in tutte le macchine virtuali standard del singolo core e versioni successive.
* Bronze: nessun privilegio. Questa è l'impostazione predefinita di hello. Usare solo questo livello di durabilità per i tipi di nodi che eseguono _solo_ carichi di lavoro senza stato. 

> [!WARNING]
> NodeTypes in esecuzione con durabilità Bronze _senza privilegi_. Ciò significa che i processi di infrastruttura che influiscono sui carichi di lavoro senza stato non verranno interrotti o posticipati. È possibile che tali processi possano ancora influire sui carichi di lavoro, provocando un tempo di inattività o altri problemi. Per qualsiasi tipo di carico di lavoro di produzione, è consigliata almeno l'esecuzione con Silver. 
> 

Si ottiene il livello di durabilità toochoose per ognuno dei tipi di nodo. È possibile scegliere un tipo di nodo toohave un livello di durabilità oro o argento e hello altri presenti hello bronzo dello stesso cluster. **è necessario mantenere un numero minimo di 5 nodi per qualsiasi tipo di nodo che ha una durata di oro o silver**. 

**Vantaggi dell'uso di livelli di durabilità Silver o Gold**
 
1. Riduce il numero di hello di passaggi necessari in un'operazione di scala (ovvero, la disattivazione del nodo e Remove-ServiceFabricNodeState viene chiamato automaticamente)
2. Riduce il rischio di hello di perdita di dati a causa di operazioni di infrastruttura di Azure o tooa avviato dall'utente sul posto VM SKU operazione di modifica.
     
**Svantaggi dell'uso di livelli di durabilità Silver o Gold**
 
1. Le distribuzioni tooyour Set di scalabilità della macchina virtuale e altre risorse di Azure correlate) possono essere ritardati, il timeout o possono essere bloccati interamente da problemi del cluster o a livello di infrastruttura hello. 
2. Aumenta hello numero di [gli eventi del ciclo di vita di replica](service-fabric-reliable-services-advanced-usage.md#stateful-service-replica-lifecycle ) (ad esempio, lo scambio primario) a causa di disattivazioni nodo tooautomated durante le operazioni dell'infrastruttura di Azure.

### <a name="recommendations-on-when-toouse-silver-or-gold-durability-levels"></a>Indicazioni su quando i livelli durabilità argento o oro toouse

Durabilità utilizzare argento o oro per i tipi di tutti i nodi con stato di tale host dei servizi è prevede tooscale (riduce il numero di istanze VM) di frequente, e si preferisce che le operazioni di distribuzione deve essere ritardata a favore di semplificare queste operazioni di scala. scenari di scalabilità orizzontale Hello (aggiunta di istanze di macchine virtuali) non vengono riprodotti nella scelta del livello di durabilità hello, solo scala aggiuntivo.

### <a name="operational-recommendations-for-hello-node-type-that-you-have-set-toosilver-or-gold-durability-level"></a>Indicazioni operative per il nodo hello digitare di aver impostato la durabilità toosilver o oro livello.

1. Mantenere integri i cluster e le applicazioni in qualsiasi momento e assicurarsi che le applicazioni rispondano tooall [eventi del ciclo di vita di replica del servizio](service-fabric-reliable-services-advanced-usage.md#stateful-service-replica-lifecycle) (ad esempio, replica di compilazione è bloccato) in modo tempestivo.
2. Adottare toomake modalità più sicura una modifica della SKU VM (scalabilità verso l'alto o verso il basso): la modifica di hello SKU VM di un Set di scalabilità della macchina virtuale è di per sé un'operazione non affidabile e pertanto deve essere evitati se possibile. Ecco il processo di hello è possibile seguire i problemi comuni tooavoid.
    - **Per non primario nodetypes:** è consigliabile creare Set di scalabilità a nuova macchina virtuale, modificare hello posizionamento vincolo tooinclude hello nuovo Set di scalabilità della macchina virtuale/nodo tipo di servizio e quindi lo riducono hello Set di scalabilità della macchina virtuale precedente istanza conteggio too0, un nodo alla volta (è assicurarsi che la rimozione di nodi di hello non influiscono sull'affidabilità di hello del cluster hello toomake).
    - **Per tipo di nodo primario hello:** si consiglia di non modificare SKU VM di tipo di nodo primario hello. Se hello motivo per il nuovo SKU hello è la capacità, si consiglia di aggiungere più istanze o, se possibile, creare un nuovo cluster. Se è possibile scegliere, quindi apportare modifiche toohello impostare modello di macchina virtuale scala definizione tooreflect hello SKU di nuovo. Se il cluster con un solo tipo di nodo, quindi assicurarsi che tutte le applicazioni con state rispondano tooall [eventi del ciclo di vita di replica del servizio](service-fabric-reliable-services-advanced-usage.md#stateful-service-replica-lifecycle) (ad esempio, replica di compilazione è bloccato) in modo tempestivo e che la replica del servizio ricompilare durata è inferiore a cinque minuti (livello di durabilità Silver). 


> [!WARNING]
> Hello la modifica delle dimensioni per il set di scalabilità di macchine Virtuali non è in esecuzione almeno argento durabilità SKU della macchina virtuale non è consigliata. La modifica delle dimensioni della SKU della macchina virtuale è un'operazione dell'infrastruttura sul posto distruttiva per i dati. Senza almeno alcuni monitor o il possibilità toodelay questa modifica, è possibile che operazione hello può causare dataloss per i servizi con stati o altri problemi operativi unforseen, anche per i carichi di lavoro senza stati. 
> 
    
3. Mantenere un numero minimo di cinque nodi per tutti i set di scalabilità di macchine virtuali con ruolo di gestione abilitato.
4. Non eliminare istanze di VM casuali. Usare sempre la funzionalità di riduzione delle prestazioni del set di scalabilità di macchine virtuali. l'eliminazione di Hello casuale istanze di macchina virtuale ha un potenziale creazione mettendolo in hello istanza delle macchine Virtuali distribuite in UD e FD. Questo squilibrio potrebbe influire negativamente sulle hello sistemi possibilità tooproperly bilanciamento del carico tra le repliche di hello servizio o le istanze del servizio.
6. Se utilizza la scalabilità automatica, quindi impostare le regole di hello in modo che la scala (rimozione di istanze di macchine Virtuali) vengono eseguite solo un nodo alla volta. La riduzione delle prestazioni di più di un'istanza per volta non è sicura.
7. Se la scalabilità verso il basso un tipo di nodo primario, non dovrebbe essere scalato mai superiore a quale livello di affidabilità hello consente verso il basso.


## <a name="hello-reliability-characteristics-of-hello-cluster"></a>caratteristiche di affidabilità Hello del cluster di hello
Hello livello di affidabilità viene utilizzato il numero hello tooset delle repliche hello dei servizi di sistema che si desidera toorun in questo cluster sul tipo di nodo primario hello. Hello numero maggiore di hello delle repliche, hello più affidabili servizi di sistema hello del cluster.  

livello di affidabilità Hello può assumere hello seguenti valori:

* Platinum - esecuzione hello di servizi di sistema con un conteggio di set di replica di destinazione di 9
* Oro - esecuzione hello di servizi di sistema con un numero di set di replica di destinazione di 7
* Argento - esecuzione hello di servizi di sistema con un conteggio di set di replica di destinazione di 5 
* Bronzo, servizi di sistema hello esecuzione con un numero di set di replica di destinazione di 3

> [!NOTE]
> livello di affidabilità Hello che scelto determina numero minimo di hello dei nodi che deve avere il tipo di nodo primario. 
> 
> 


### <a name="recommendations-for-hello-reliability-tier"></a>Suggerimenti per il livello di affidabilità hello.

 Quando si aumenta o diminuisce hello delle dimensioni del cluster (somma hello delle istanze di macchina virtuale in tutti i tipi di nodo), è necessario aggiornare l'affidabilità di hello del cluster da un livello tooanother. Questa operazione attiva hello gli aggiornamenti necessari toochange hello sistema Servizi replica set numero dei cluster. Attendere l'aggiornamento di hello in corso toocomplete prima di apportare qualsiasi cluster di toohello altre modifiche, ad esempio l'aggiunta di nodi.  È possibile monitorare lo stato di avanzamento hello di Service Fabric Explorer o eseguendo l'aggiornamento di hello [Get ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps)

Ecco la raccomandazione hello sulla scelta a livello di affidabilità hello.

| **Dimensione del cluster** | **Livello di affidabilità** |
| --- | --- |
| 1 |Non specificare hello parametro livello di affidabilità, verrà calcolata sistema hello |
| 3 |Bronze |
| 5 o 6|Silver |
| 7 o 8 |Gold |
| Da 9 in su |Platinum |




## <a name="primary-node-type---capacity-guidance"></a>Tipo di nodo primario: guida alla capacità

Sezione vengono fornite indicazioni hello per la pianificazione della capacità di tipo di nodo primario hello

1. **Numero di VM istanze toorun qualsiasi carico di lavoro di produzione in Azure:** è necessario specificare una dimensione di tipo di nodo primario minima di 5. 
2. **Numero di VM istanze toorun test dei carichi di lavoro in Azure** è possibile specificare una dimensione di tipo nodo primario minimo di 1 o 3. Hello un cluster di nodi, viene eseguito con una configurazione speciale e pertanto, la scalabilità all'esterno di tale cluster non è supportata. un nodo cluster, Hello non ha affidabilità e nel modello di gestione delle risorse, è necessario tooremove/non specificare che la configurazione (non impostando il valore di configurazione di hello non è sufficiente). Se si configura il cluster di un nodo hello impostati mediante portale, quindi configurazione hello viene automaticamente preso in considerazione. I cluster a uno e tre nodi non sono supportati per l'esecuzione di carichi di lavoro di produzione. 
3. **VM SKU:** tipo di nodo primario è in esecuzione servizi di sistema hello, hello SKU VM prescelto, deve tengono in hello account complessiva picco di carico è pianificare tooplace in cluster hello. Ecco un tooillustrate analogia cosa si intende qui - ritiene del tipo di nodo primario hello come i "polmoni" cosa offre cervello tooyour ossigeno, e pertanto se cervello hello non ottiene sufficiente ossigeno, il corpo subisce. 

Esigenze di capacità hello di un cluster è determinato dal carico di lavoro si prevede di toorun cluster hello, è possibile fornire con qualitativa si basa sulle linee guida per il carico di lavoro specifico, tuttavia qui hello indicazioni generali toohelp iniziare

Per i carichi di lavoro di produzione 


- Hello consiglia VM SKU Standard D3 o D3_V2 Standard o con un minimo di 14 GB di unità SSD locale.
- utilizzo di Hello minima supportata VM SKU è D1 Standard o D1_V2 Standard o con un minimo di 14 GB di unità SSD locale. 
- Gli SKU per VM con core parziali, ad esempio Standard A0, non sono supportati per i carichi di lavoro di produzione.
- Lo SKU Standard A1 non è supportato per i carichi di lavoro di produzione per motivi di prestazioni.


## <a name="non-primary-node-type---capacity-guidance-for-stateful-workloads"></a>Tipo di nodo non primario: guida alla capacità per carichi di lavoro con stato

Questa guida è per i carichi di lavoro con utilizzo di Service fabric [raccolte affidabile o reliable Actors](service-fabric-choose-framework.md) in esecuzione nel tipo di nodo non primario hello.


**Numero di istanze delle VM:** è consigliabile eseguire i carichi di lavoro di produzione con stato con un numero di repliche di destinazione di almeno 5 istanze. Nello stato stabile viene quindi creata una replica (da un set di repliche) in ogni dominio di errore e in ogni dominio di aggiornamento. concetto di livello di affidabilità intero Hello per il tipo di nodo primario hello è un modo toospecify questa impostazione per servizi di sistema. Pertanto hello stessa considerazione si applica anche tooyour i servizi con stato.

Pertanto per i carichi di lavoro, dimensione minima consigliata non - nodo primario hello è 5, se si eseguono i carichi di lavoro con stati in essa contenuti.


**VM SKU:** questo è il tipo di nodo hello in cui sono in esecuzione i servizi dell'applicazione, pertanto hello VM SKU scelto, è necessario prendere in considerazione hello punta il si prevede di tooplace in ogni nodo. salve le esigenze di capacità di hello nodetype, varia a seconda del carico di lavoro che si prevede di toorun cluster hello, pertanto, non possiamo fornirti con qualitativa si basa sulle linee guida per il carico di lavoro specifico, è tuttavia qui hello indicazioni generali toohelp iniziare

Per i carichi di lavoro di produzione 

- Hello consiglia VM SKU Standard D3 o D3_V2 Standard o con un minimo di 14 GB di unità SSD locale.
- utilizzo di Hello minima supportata VM SKU è D1 Standard o D1_V2 Standard o con un minimo di 14 GB di unità SSD locale. 
- Gli SKU per VM con core parziali, ad esempio Standard A0, non sono supportati per i carichi di lavoro di produzione.
- Lo SKU Standard A1 in particolare non è supportato per i carichi di lavoro di produzione per motivi di prestazioni.


## <a name="non-primary-node-type---capacity-guidance-for-stateless-workloads"></a>Tipo di nodo non primario: guida alla capacità per carichi di lavoro senza stato

Questa Guida di carichi di lavoro senza stati che eseguono nodetype non primario hello.

**Numero di istanze di macchina virtuale:** per i carichi di lavoro che sono senza stati, dimensione del tipo di nodo principale di non - hello minimo supportato è 2. In questo modo è toorun è due senza stato istanze dell'applicazione e consentendo la toosurvive servizio hello perdita di un'istanza di macchina virtuale. 

> [!NOTE]
> Se il cluster è in esecuzione in una versione dell'infrastruttura service 5.6 minore, a causa di difetto tooa hello fase di esecuzione (il problema viene risolto in 5.6), la scalabilità verso il basso un tooless di tipo di nodo non primario di 5, comporta l'attivazione non è integro, fino a quando si chiama l'integrità del cluster [ Remove-ServiceFabricNodeState cmd](https://docs.microsoft.com/powershell/servicefabric/vlatest/Remove-ServiceFabricNodeState) con il nome di nodo appropriato hello. Per altre informazioni, vedere [Aumentare o ridurre il numero di istanze del cluster di Service Fabric](service-fabric-cluster-scale-up-down.md).
> 
>

**VM SKU:** questo è il tipo di nodo hello in cui sono in esecuzione i servizi dell'applicazione, pertanto hello VM SKU scelto, è necessario prendere in considerazione hello punta il si prevede di tooplace in ogni nodo. salve le esigenze di capacità di hello nodetype, varia a seconda del carico di lavoro che si prevede di toorun cluster hello, pertanto, non possiamo fornirti con qualitativa si basa sulle linee guida per il carico di lavoro specifico, è tuttavia qui hello indicazioni generali toohelp iniziare

Per i carichi di lavoro di produzione 


- Hello consiglia VM SKU Standard D3 o D3_V2 Standard o equivalente. 
- utilizzo di Hello minima supportata VM SKU è D1 Standard o D1_V2 Standard o equivalente. 
- Gli SKU per VM con core parziali, ad esempio Standard A0, non sono supportati per i carichi di lavoro di produzione.
- Lo SKU Standard A1 non è supportato per i carichi di lavoro di produzione per motivi di prestazioni.

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->

## <a name="next-steps"></a>Passaggi successivi
Una volta fine pianificazione della capacità e configurare un cluster, leggere hello seguenti:

* [Sicurezza di un cluster di Service Fabric](service-fabric-cluster-security.md)
* [Introduzione al monitoraggio dell'integrità di Service Fabric](service-fabric-health-introduction.md)
* [Relazione di scalabilità della macchina tooVirtual Nodetypes impostata](service-fabric-cluster-nodetypes.md)

<!--Image references-->
[SystemServices]: ./media/service-fabric-cluster-capacity/SystemServices.png
