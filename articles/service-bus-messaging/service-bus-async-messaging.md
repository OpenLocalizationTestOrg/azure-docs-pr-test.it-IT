---
title: aaaService del Bus di messaggistica asincrona | Documenti Microsoft
description: Descrizione della messaggistica asincrona del bus di servizio di Azure.
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: f1435549-e1f2-40cb-a280-64ea07b39fc7
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/19/2017
ms.author: sethm
ms.openlocfilehash: 5ab6ddf052155a9dd975b413cfaf393119c1999d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="asynchronous-messaging-patterns-and-high-availability"></a>Modelli di messaggistica asincrona e disponibilità elevata

La messaggistica asincrona può essere implementata in molti modi diversi. Con code, argomenti e sottoscrizioni, il bus di servizio di Azure supporta la messaggistica asincrona tramite un meccanismo di archiviazione e inoltro. In condizioni normali (sincrona), inviare messaggi tooqueues e argomenti e ricevere messaggi da code e sottoscrizioni. Le applicazioni create dipendono dalla disponibilità continua di queste entità. Quando viene modificato lo stato dell'entità hello, a causa di tooa diverse circostanze, è necessario un tooprovide modo un'entità a capacità limitata in grado di soddisfare la maggior parte delle esigenze.

Le applicazioni utilizzano in genere tooenable modelli di messaggistica asincrona un numero di scenari di comunicazione. È possibile compilare applicazioni in cui i client possono inviare messaggi tooservices, anche quando non è in esecuzione il servizio di hello. Per le applicazioni che presentano picchi di comunicazioni, una coda può aiutare hello livello caricare fornendo le comunicazioni toobuffer sul posto. Infine, è possibile ottenere un carico semplice ma efficace messaggi toodistribute di bilanciamento del carico tra più computer.

Disponibilità di toomaintain ordine di qualsiasi entità, considerare i modi in cui le entità possono risultare non disponibile per un sistema di messaggistica durevole. In generale, verrà visualizzato entity hello diventano tooapplications disponibile che nelle hello seguenti modi:

* Non è possibile toosend messaggi.
* Non è possibile tooreceive messaggi.
* Entità non è possibile toomanage (creare, recuperare, aggiornare o eliminare entità).
* Servizio hello toocontact non è possibile.

Per ognuno di questi errori, diverse modalità di errore esiste che consentono di gestire di tooperform toocontinue un'applicazione in un certo livello di funzionalità ridotte. Ad esempio, un sistema che può inviare messaggi, ma non riceverli, e continuare comunque a ricevere ordini dai clienti senza però poterli elaborare. Questo argomento illustra i problemi che possono verificarsi e le tecniche per attenuarne gli effetti. Bus di servizio sono state introdotte numerose soluzioni correttive che devono acconsentire esplicitamente e in questo argomento viene inoltre hello utilizzano le regole che controllano hello di queste soluzioni correttive consenso esplicito.

## <a name="reliability-in-service-bus"></a>Affidabilità nel bus di servizio
Esistono diversi modi i problemi di entità e messaggi toohandle e non esistono regole che governano hello uso appropriato di queste soluzioni correttive. linee guida hello toounderstand, è necessario innanzitutto comprendere cosa può avere esito negativo nel Bus di servizio. A causa di toohello progettazione dei sistemi Azure, tutti questi aspetti tendono toobe di breve durata. In generale, hello diverse cause indisponibilità appaiono come segue:

* Limitazione da un sistema esterno dal quale dipende il bus di servizio. La limitazione è generata da interazioni con le risorse di archiviazione e calcolo.
* Problema dovuto a un sistema dal quale dipende il bus di servizio. Ad esempio, problemi che possono verificarsi in una determinata risorsa di archiviazione.
* Errore del bus di servizio in un singolo sottosistema. In questo caso, un nodo di calcolo potrebbe entrare in uno stato incoerente e debba essere riavviato, causando tutte le entità che svolge il saldo tooload tooother nodi. Questa situazione può causare a sua volta un breve periodo di elaborazione lenta dei messaggi.
* Errore del bus di servizio in un data center di Azure. Si tratta di un "Errore irreversibile" durante il quale hello sistema risulta irraggiungibile per vari minuti o alcune ore.

> [!NOTE]
> il termine Hello **archiviazione** può indicare sia archiviazione di Azure e SQL Azure.
> 
> 

Nel bus di servizio sono disponibili diverse misure di prevenzione per questi problemi. Hello le sezioni seguenti descrivono ogni problema e le relative soluzioni correttive.

### <a name="throttling"></a>Limitazione
Nel bus di servizio la limitazione consente la gestione congiunta della frequenza dei messaggi. Ogni singolo nodo del bus di servizio ospita molte entità, Ognuna delle quali effettua richieste sistema hello in termini di CPU, memoria, archiviazione e altri facet. Quando uno di questi facet individua un utilizzo superiore alla soglia predefinita, il bus di servizio può negare una richiesta specifica. Hello chiamante riceve un [ServerBusyException] [ ServerBusyException] e ripetizione di tentativi dopo 10 secondi.

Come prevenzione, codice hello leggere errore hello e bloccare qualsiasi nuovo tentativo del messaggio hello di almeno 10 secondi. Poiché hello errore può verificarsi in varie parti dell'applicazione hello del cliente, è previsto che ogni parte esegua indipendentemente la logica di riesecuzione hello. codice Hello può ridurre la probabilità hello delle limitazioni abilitando il partizionamento su una coda o argomento.

### <a name="issue-for-an-azure-dependency"></a>Problema per una dipendenza di Azure
Anche per altri componenti di Azure possono occasionalmente verificarsi problemi di servizio. Quando, ad esempio, si aggiorna un sistema usato dal bus di servizio, è possibile che il sistema funzioni temporaneamente con capacità limitate. toowork intorno a questi tipi di problemi, Service Bus regolarmente analizza e implementa le misure di attenuazione. È tuttavia possibile che si verifichino effetti collaterali di misure di prevenzione. Ad esempio, toohandle temporaneo problemi con l'archiviazione, Bus di servizio implementa un sistema che consente di toowork operazioni di invio messaggi in modo coerente. A causa di natura toohello di attenuazione hello, un messaggio inviato può richiedere too15 minuti tooappear nella sottoscrizione o coda hello interessato ed essere pronto per un'operazione di ricezione. In genere, la maggior parte delle entità non è interessata da questo problema. Tuttavia, dato il numero di hello di entità di Service Bus in Azure, questa soluzione è talvolta necessario per un piccolo subset di clienti Bus di servizio.

### <a name="service-bus-failure-on-a-single-subsystem"></a>Errore del bus di servizio in un singolo sottosistema
Con qualsiasi altra applicazione, circostanze possono determinare un componente interno di Service Bus toobecome incoerente. Quando rileva il Bus di servizio, vengono raccolti dati dal tooaid applicazione hello diagnostici. Una volta raccolti i dati di hello, un'applicazione hello viene riavviato in tooreturn un tentativo è stato coerente tooa. Questo processo viene eseguito abbastanza velocemente e risultati di un'entità non disponibile per backup tooa toobe alcuni minuti, anche se tipico tempi di inattività sono molto più brevi.

In questi casi, un'applicazione hello client genera un [System. TimeoutException] [ System.TimeoutException] o [MessagingException] [ MessagingException] eccezione. Bus di servizio è inclusa una soluzione per questo problema in forma di hello di logica di ripetizione dei client automatizzata. Una volta allo scadere del periodo tentativi hello e non viene fornito il messaggio hello, è possibile esplorare utilizzando altre funzionalità, ad esempio [associati spazi dei nomi][paired namespaces]. Questi ultimi presentano altri ostacoli che sono illustrati in questo articolo.

### <a name="failure-of-service-bus-within-an-azure-datacenter"></a>Errore del bus di servizio in un data center di Azure
motivo più probabile di Hello di un errore in un Data Center di Azure è una distribuzione di aggiornamento non riuscita del Bus di servizio o un sistema dipendente. Come piattaforma di hello è stata migliorata, probabilità hello di questo tipo di errori è diminuita. Un problema del Data Center può verificarsi anche per i motivi includono hello seguenti:

* Interruzione elettrica (arresto di alimentazione e produzione di energia).
* Connettività (interruzione della connessione Internet tra i client e Azure).

In entrambi i casi, un'emergenza naturale o a causa di hello problema. toowork il problema e assicurarsi che è comunque possibile inviare messaggi, è possibile utilizzare [associati spazi dei nomi] [ paired namespaces] tooenable messaggi toobe inviati tooa seconda posizione, mentre la posizione primaria hello viene reso nuovamente integro. Per altre informazioni, vedere [Procedure consigliate per isolare le applicazioni del bus di servizio da interruzioni ed emergenze del servizio][Best practices for insulating applications against Service Bus outages and disasters].

## <a name="paired-namespaces"></a>Spazi dei nomi associati
Hello [associati spazi dei nomi] [ paired namespaces] funzionalità supporta scenari in cui una distribuzione in un data center o entità del Bus di servizio non è più disponibile. Durante questo evento si verifica raramente, i sistemi distribuiti ancora devono essere preparati toohandle peggiore dei casi. In genere, questo tipo di evento si verifica perché in qualche elemento dal quale dipende il bus di servizio avviene un problema di breve durata. la disponibilità dell'applicazione toomaintain durante un'interruzione, Bus di servizio gli utenti può usare due separati spazi dei nomi, preferibilmente in centri dati toohost le entità di messaggistica. resto Hello di questa sezione utilizza hello seguente terminologia:

* Spazio dei nomi primario: hello dello spazio dei nomi con cui interagisce l'applicazione, per l'invio e operazioni di ricezione.
* Spazio dei nomi secondario: hello dello spazio dei nomi che funge da uno spazio dei nomi primario di toohello backup. La logica dell'applicazione non interagisce con questo spazio dei nomi.
* Intervallo di failover: quantità di hello di errori di normale tooaccept tempo prima di un'applicazione hello passa da hello spazio dei nomi primario toohello secondario dello spazio dei nomi.

Gli spazi dei nomi associati supportano *sendavailability*, Inviare disponibilità conserva messaggi toosend possibilità di hello. toouse sendavailability, l'applicazione deve soddisfare hello seguenti requisiti:

1. I messaggi vengono ricevuti solo dallo spazio dei nomi primario hello.
2. I messaggi inviati tooa coda o argomento specificato può arrivare senza ordine.
3. I messaggi in una sessione possono arrivare senza un ordine preciso. Questa è un'interruzione rispetto alla normale funzionalità delle sessioni, Ciò significa che l'applicazione usa le sessioni toologically raggruppare i messaggi.
4. Lo stato della sessione viene mantenuto solo nello spazio dei nomi primario hello.
5. la coda primaria Hello può portare in linea e iniziare ad accettare messaggi prima che la coda secondaria hello offre tutti i messaggi in coda primaria hello.

Hello le sezioni seguenti descrivono hello API, le modalità di implementazione delle API hello e codice di esempio mostra che usa la funzionalità di hello. Si noti che a questa funzionalità sono associati costi di fatturazione.

### <a name="hello-messagingfactorypairnamespaceasync-api"></a>Hello API messagingfactory. Pairnamespaceasync
funzionalità di spazi dei nomi abbinati Hello include hello [PairNamespaceAsync] [ PairNamespaceAsync] metodo hello [Microsoft.ServiceBus.Messaging.MessagingFactory] [ Microsoft.ServiceBus.Messaging.MessagingFactory] classe:

```csharp
public Task PairNamespaceAsync(PairedNamespaceOptions options);
```

Al termine dell'attività hello, hello l'associazione dello spazio dei nomi è completo e pronto tooact al momento per qualsiasi [MessageReceiver][MessageReceiver], [QueueClient] [ QueueClient], o [TopicClient] [ TopicClient] creato con hello [MessagingFactory] [ MessagingFactory] istanza. [Microsoft.ServiceBus.Messaging.PairedNamespaceOptions] [ Microsoft.ServiceBus.Messaging.PairedNamespaceOptions] è la classe base hello per hello diversi tipi di associazione che sono disponibili con un [MessagingFactory] [ MessagingFactory] oggetto. Attualmente, hello solo derivata è denominata [SendAvailabilityPairedNamespaceOptions][SendAvailabilityPairedNamespaceOptions], che implementa i requisiti di disponibilità di trasmissione hello. La classe [SendAvailabilityPairedNamespaceOptions][SendAvailabilityPairedNamespaceOptions] include un set di costruttori che si basano tra loro. Analizzando di costruttore hello con hello la maggior parte dei parametri, è possibile comprendere il comportamento di hello di hello altri costruttori.

```csharp
public SendAvailabilityPairedNamespaceOptions(
    NamespaceManager secondaryNamespaceManager,
    MessagingFactory messagingFactory,
    int backlogQueueCount,
    TimeSpan failoverInterval,
    bool enableSyphon)
```

Questi parametri sono hello seguenti significati:

* *secondaryNamespaceManager*: un oggetto inizializzato [NamespaceManager] [ NamespaceManager] istanza per spazio dei nomi secondario hello che hello [PairNamespaceAsync] [ PairNamespaceAsync] metodo può utilizzare tooset spazio dei nomi secondario hello. gestione dello spazio dei nomi Hello è code nello spazio dei nomi hello e assicurarsi che esistano le code di backlog necessarie hello toomake elenco hello tooobtain utilizzato. Se le code non esistono, vengono create. [NamespaceManager] [ NamespaceManager] richiede hello possibilità toocreate un token con hello **Gestisci** attestazione.
* *messagingFactory*: hello [MessagingFactory] [ MessagingFactory] istanza per spazio dei nomi secondario hello. Hello [MessagingFactory] [ MessagingFactory] oggetto è toosend utilizzato e, se hello [EnableSyphon] [ EnableSyphon] impostata troppo**true** , ricevere messaggi dalle code di backlog hello.
* *backlogqueuecount*: numero di hello del backlog Accoda toocreate. Il valore deve essere almeno 1. Quando si inviano backlog toohello messaggi, viene scelta casualmente una di queste code. Se si imposta too1 valore hello, solo una coda può quindi mai essere utilizzata. Quando ciò si verifica e hello unica coda di backlog genera errori, il client di hello non è in grado di tootry un'altra coda e potrebbe non riuscire toosend il messaggio. È consigliabile impostare questo valore toosome più grande valore e predefinito hello valore too10. È possibile modificare questo tooa superiore oppure un valore inferiore a seconda della quantità di dati, l'applicazione invia al giorno. Ogni coda di backlog può contenere too5 GB di messaggi.
* *failoverInterval*: hello quantità di tempo durante i quali vengono accettati gli errori di spazio dei nomi primario hello prima di passare qualsiasi entità singola su spazio dei nomi secondario toohello. I failover si verificano su un'entità alla volta. Le entità in un singolo spazio dei nomi di solito risiedono in nodi diversi del bus di servizio. Un errore in un'entità non implica che si verifichi in un'altra entità. È possibile impostare questo valore troppo[TimeSpan] [ System.TimeSpan.Zero] toohello toofailover secondario immediatamente dopo il primo errore non temporaneo. Gli errori che attivano il timer di failover hello sono stati [MessagingException] [ MessagingException] in cui hello [IsTransient] [ IsTransient] proprietà è false, o [System. TimeoutException][System.TimeoutException]. Altre eccezioni, ad esempio [UnauthorizedAccessException] [ UnauthorizedAccessException] non causano il failover, perché indicano che il client hello è configurato in modo non corretto. Oggetto [ServerBusyException] [ ServerBusyException] causa il failover perché hello è toowait 10 secondi, quindi invia il messaggio hello nuovamente.
* *enableSyphon*: indica che l'associazione specificata deve sifone messaggi dallo spazio dei nomi primario di back-toohello spazio dei nomi secondario hello. In generale, le applicazioni che inviano i messaggi devono impostare questo valore troppo**false**; le applicazioni che ricevono i messaggi devono impostare questo valore troppo**true**. Hello questo accade spesso, sono presenti destinatari dei messaggi è inferiore a quello dei mittenti. In base al numero di hello di ricevitori, è possibile scegliere toohave un'attività del sifone hello handle di istanza singola applicazione. All'uso di più destinatari sono associati costi di fatturazione per ogni coda di backlog.

toouse hello codice, creare un database primario [MessagingFactory] [ MessagingFactory] istanza, un database secondario [MessagingFactory] [ MessagingFactory] istanza, un database secondario [NamespaceManager] [ NamespaceManager] istanza e un [SendAvailabilityPairedNamespaceOptions] [ SendAvailabilityPairedNamespaceOptions] istanza. chiamata di Hello può essere semplice come riportato di seguito hello:

```csharp
SendAvailabilityPairedNamespaceOptions sendAvailabilityOptions = new SendAvailabilityPairedNamespaceOptions(secondaryNamespaceManager, secondary);
primary.PairNamespaceAsync(sendAvailabilityOptions).Wait();
```

Hello quando l'attività restituita da hello [PairNamespaceAsync] [ PairNamespaceAsync] metodo viene completato, tutto ciò che viene configurato e pronto toouse. Prima che venga restituito attività hello, si potrebbe non aver completato tutte attività in background hello necessarie per l'abbinamento toowork destra hello. Di conseguenza, non deve iniziare l'invio di messaggi fino a quando l'attività hello restituisce. Se si sono verificati eventuali errori, ad esempio credenziali errate o code di backlog per errore toocreate hello, tali eccezioni verranno generate al termine dell'attività hello. Restituisce l'attività hello, verificare che le code di hello sono state trovate o create esaminando hello [backlogqueuecount] [ BacklogQueueCount] proprietà il [SendAvailabilityPairedNamespaceOptions] [ SendAvailabilityPairedNamespaceOptions] istanza. Per hello codice precedente, questa operazione viene visualizzata come indicato di seguito:

```csharp
if (sendAvailabilityOptions.BacklogQueueCount < 1)
{
    // Handle case where no queues were created.
}
```

## <a name="next-steps"></a>Passaggi successivi
Dopo aver appreso nozioni di base di hello di messaggistica asincrona nel Bus di servizio, leggere ulteriori informazioni su [associati spazi dei nomi][paired namespaces].

[ServerBusyException]: /dotnet/api/microsoft.servicebus.messaging.serverbusyexception
[System.TimeoutException]: https://msdn.microsoft.com/library/system.timeoutexception.aspx
[MessagingException]: /dotnet/api/microsoft.servicebus.messaging.messagingexception
[Best practices for insulating applications against Service Bus outages and disasters]: service-bus-outages-disasters.md
[Microsoft.ServiceBus.Messaging.MessagingFactory]: /dotnet/api/microsoft.servicebus.messaging.messagingfactory
[MessageReceiver]: /dotnet/api/microsoft.servicebus.messaging.messagereceiver
[QueueClient]: /dotnet/api/microsoft.servicebus.messaging.queueclient
[TopicClient]: /dotnet/api/microsoft.servicebus.messaging.topicclient
[Microsoft.ServiceBus.Messaging.PairedNamespaceOptions]: /dotnet/api/microsoft.servicebus.messaging.pairednamespaceoptions
[MessagingFactory]: /dotnet/api/microsoft.servicebus.messaging.messagingfactory
[SendAvailabilityPairedNamespaceOptions]: /dotnet/api/microsoft.servicebus.messaging.sendavailabilitypairednamespaceoptions
[NamespaceManager]: /dotnet/api/microsoft.servicebus.namespacemanager
[PairNamespaceAsync]: /dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_PairNamespaceAsync_Microsoft_ServiceBus_Messaging_PairedNamespaceOptions_
[EnableSyphon]: /dotnet/api/microsoft.servicebus.messaging.sendavailabilitypairednamespaceoptions#Microsoft_ServiceBus_Messaging_SendAvailabilityPairedNamespaceOptions_EnableSyphon
[System.TimeSpan.Zero]: https://msdn.microsoft.com/library/system.timespan.zero.aspx
[IsTransient]: /dotnet/api/microsoft.servicebus.messaging.messagingexception#Microsoft_ServiceBus_Messaging_MessagingException_IsTransient
[UnauthorizedAccessException]: https://msdn.microsoft.com/library/system.unauthorizedaccessexception.aspx
[BacklogQueueCount]: /dotnet/api/microsoft.servicebus.messaging.sendavailabilitypairednamespaceoptions?redirectedfrom=MSDN#Microsoft_ServiceBus_Messaging_SendAvailabilityPairedNamespaceOptions_BacklogQueueCount
[paired namespaces]: service-bus-paired-namespaces.md
