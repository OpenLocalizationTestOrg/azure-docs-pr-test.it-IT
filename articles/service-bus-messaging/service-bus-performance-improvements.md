---
title: procedure consigliate aaaBest per migliorare le prestazioni utilizzando Azure Service Bus | Documenti Microsoft
description: Viene descritto come toouse prestazioni toooptimize del Bus di servizio quando si scambiano negoziata messaggi.
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: e756c15d-31fc-45c0-8df4-0bca0da10bb2
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/10/2017
ms.author: sethm
ms.openlocfilehash: 52764d227757cbb11246675878933f21685817f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-for-performance-improvements-using-service-bus-messaging"></a>Procedure consigliate per il miglioramento delle prestazioni tramite la messaggistica del bus di servizio

Questo articolo viene descritto come toouse [messaggistica del Bus di servizio di Azure](https://azure.microsoft.com/services/service-bus/) negoziata di toooptimize prestazioni durante lo scambio di messaggi. prima parte di Hello di questo argomento descrive i meccanismi diversi hello offerti toohelp aumento delle prestazioni. seconda parte Hello fornisce indicazioni su come toouse Bus di servizio in modo che può offrire hello prestazioni ottimali in un determinato scenario.

In questo argomento, il termine di hello "client" si riferisce tooany entità che accede a Bus di servizio. Un client può assumere il ruolo di hello di un mittente o ricevitore. il termine di Hello "mittente" viene usato per un client di coda o argomento Bus di servizio che invia messaggi tooa Bus di servizio coda o argomento. il termine Hello "ricevente" si riferisce tooa client coda o sottoscrizione del Bus di servizio che riceve i messaggi da una coda di Service Bus o la sottoscrizione.

Queste sezioni presentano alcuni concetti che Service Bus Usa toohelp incrementare le prestazioni.

## <a name="protocols"></a>Protocolli
Bus di servizio consente ai client toosend e ricevere messaggi tramite uno dei tre protocolli:

1. Advanced Message Queuing Protocol (AMQP)
2. Service Bus Messaging Protocol (SBMP)
3. HTTP

AMQP e SBMP sono più efficienti, perché mantengono hello connessione tooService Bus, purché le factory di messaggistica hello. Implementa anche le operazioni di invio in batch e prelettura. A meno che non indicato in modo esplicito, tutto il contenuto in questo argomento si presuppone l'uso di hello di AMQP o SBMP.

## <a name="reusing-factories-and-clients"></a>Riutilizzo di factory e client
Gli oggetti client del bus di servizio, ad esempio [QueueClient][QueueClient] o [MessageSender][MessageSender], vengono creati tramite un oggetto [MessagingFactory][MessagingFactory] che offre anche la gestione interna delle connessioni. È consigliabile non chiudere le factory di messaggistica o coda, argomento e sottoscrizione client dopo aver inviare un messaggio e quindi ricrearli quando si invia il messaggio hello successivo. Chiusura di una factory di messaggistica Elimina hello connessione toohello servizio service Bus e una nuova connessione viene stabilita quando si ricreano factory hello. Tentativo di stabilire che una connessione è un'operazione dispendiosa, che è possibile evitare riutilizzando hello stessa factory e client, gli oggetti per più operazioni. È possibile utilizzare hello [QueueClient] [ QueueClient] oggetto per l'invio di messaggi da più thread e le operazioni asincrone simultanee. 

## <a name="concurrent-operations"></a>Operazioni simultanee
L'esecuzione di un'operazione (invio, ricezione, eliminazione e così via) richiede tempo. Questo tempo include l'elaborazione di hello dell'operazione hello dal servizio Bus di servizio hello latenza toohello aggiunta di hello richiesta e risposta di hello. numero di hello tooincrease di operazioni per volta, le operazioni vengano eseguite simultaneamente. È possibile farlo in diversi modi:

* **Operazioni asincrone**: client hello Pianifica operazioni eseguendo operazioni asincrone. la richiesta successiva Hello sia stata avviata prima hello precedente richiesta è stata completata. Hello Ecco un esempio di un'operazione asincrona di invio:
  
 ```csharp
  BrokeredMessage m1 = new BrokeredMessage(body);
  BrokeredMessage m2 = new BrokeredMessage(body);
  
  Task send1 = queueClient.SendAsync(m1).ContinueWith((t) => 
    {
      Console.WriteLine("Sent message #1");
    });
  Task send2 = queueClient.SendAsync(m2).ContinueWith((t) => 
    {
      Console.WriteLine("Sent message #2");
    });
  Task.WaitAll(send1, send2);
  Console.WriteLine("All messages sent");
  ```
  
  Ecco un esempio di operazione di ricezione in modalità asincrona:
  
  ```csharp
  Task receive1 = queueClient.ReceiveAsync().ContinueWith(ProcessReceivedMessage);
  Task receive2 = queueClient.ReceiveAsync().ContinueWith(ProcessReceivedMessage);
  
  Task.WaitAll(receive1, receive2);
  Console.WriteLine("All messages received");
  
  async void ProcessReceivedMessage(Task<BrokeredMessage> t)
  {
    BrokeredMessage m = t.Result;
    Console.WriteLine("{0} received", m.Label);
    await m.CompleteAsync();
    Console.WriteLine("{0} complete", m.Label);
  }
  ```
* **Più factory**: tutti i client (mittenti in aggiunta tooreceivers) che vengono creati hello stessa factory condivisione di una connessione TCP. velocità effettiva massima del messaggio Hello è limitata dal numero di hello di operazioni che può essere eseguita per questa connessione TCP. velocità effettiva di Hello che può essere ottenuta con una singola factory varia notevolmente con tempi di round trip TCP e le dimensioni di messaggio. tooobtain una velocità effettiva superiore, è consigliabile usare più factory di messaggistica.

## <a name="receive-mode"></a>Modalità di ricezione
Quando si crea un client di coda o sottoscrizione, è possibile specificare una modalità di ricezione: *PeekLock* o *ReceiveAndDelete*. modalità di ricezione predefinita Hello è [PeekLock][PeekLock]. Quando si opera in questa modalità, hello client invia una richiesta tooreceive un messaggio dal Bus di servizio. Dopo che il client hello ha ricevuto il messaggio hello, invia un messaggio hello toocomplete di richiesta.

Quando l'impostazione di hello modalità di ricezione troppo[ReceiveAndDelete][ReceiveAndDelete], entrambi i passaggi vengono combinati in una singola richiesta. Questo riduce hello al numero complessivo di operazioni e può migliorare hello velocità effettiva complessiva di messaggio. Questo miglioramento delle prestazioni comporta il rischio di hello di perdita dei messaggi.

Il bus di servizio non supporta le transazioni per le operazioni receive-and-delete. Inoltre, la semantica di blocco di visualizzazione è necessaria per gli scenari in cui hello client desidera toodefer o [recapitabili](service-bus-dead-letter-queues.md) un messaggio.

## <a name="client-side-batching"></a>Invio in batch sul lato client
Invio in batch sul lato client consente a una coda o argomento client toodelay hello l'invio di un messaggio per un determinato periodo di tempo. Se il client di hello invia altri messaggi durante questo periodo di tempo, trasmette messaggi hello in un unico batch. Invio in batch sul lato client comporta un toobatch client coda o sottoscrizione più **completa** le richieste in un'unica richiesta. L'invio in batch è disponibile solo per le operazioni asincrone **Send** e **Complete**. Operazioni sincrone vengono immediatamente inviate toohello servizio service Bus. L'invio in batch non si verifica per le operazioni di anteprima (peek) o ricezione né tra più client.

Per impostazione predefinita, i client usano un intervallo di invio in batch di 20 ms. È possibile modificare l'impostazione hello intervallo batch di hello [BatchFlushInterval] [ BatchFlushInterval] proprietà prima di creare hello factory di messaggistica. Questa impostazione interessa tutti i client creati da questa factory.

invio in batch toodisable, impostare hello [BatchFlushInterval] [ BatchFlushInterval] proprietà troppo**TimeSpan**. ad esempio:

```csharp
MessagingFactorySettings mfs = new MessagingFactorySettings();
mfs.TokenProvider = tokenProvider;
mfs.NetMessagingTransportSettings.BatchFlushInterval = TimeSpan.FromSeconds(0.05);
MessagingFactory messagingFactory = MessagingFactory.Create(namespaceUri, mfs);
```

L'invio in batch non influisce sul numero di hello di operazioni di messaggistica fatturabili ed è disponibile solo per hello protocollo client di Service Bus. Hello protocollo HTTP non supporta l'invio in batch.

## <a name="batching-store-access"></a>Invio in batch per l'accesso all'archivio
tooincrease hello velocità effettiva di una coda, argomento o sottoscrizione, Bus di servizio invia in batch più messaggi quando scrive archivio interno tooits. Se abilitato in una coda o un argomento, la scrittura di messaggi nell'archivio di hello verrà inseriti nel batch. Se abilitato in una coda o sottoscrizione, l'eliminazione di messaggi dall'archivio di hello verranno inseriti nel batch. Se l'accesso in batch all'archivio è abilitato per un'entità, Bus di servizio ritarda un'operazione di scrittura relativa all'entità da backup too20ms store. Operazioni di archiviazione aggiuntive che si verificano durante questo intervallo vengono aggiunti toohello batch. L'accesso in batch all'archivio influisce solo sulle operazioni **Send** e **Complete** e non sulle operazioni di ricezione. L'accesso in batch all'archivio è una proprietà di un'entità. L'invio in batch si verifica per tutte le entità per cui è abilitato l'accesso in batch all'archivio.

Quando si crea una nuova coda, un nuovo argomento o una nuova sottoscrizione, l'accesso in batch all'archivio è abilitato per impostazione predefinita. accesso a store, set hello in batch di toodisable [EnableBatchedOperations] [ EnableBatchedOperations] proprietà troppo**false** prima di creare entità hello. ad esempio:

```csharp
QueueDescription qd = new QueueDescription();
qd.EnableBatchedOperations = false;
Queue q = namespaceManager.CreateQueue(qd);
```

Accesso in batch all'archivio non influisce sul numero di hello di operazioni di messaggistica fatturabili ed è una proprietà di una coda, argomento o sottoscrizione. È indipendente di hello modalità e hello protocollo usato tra un client e hello servizio Bus di servizio di ricezione.

## <a name="prefetching"></a>Prelettura
La prelettura consente hello coda o sottoscrizione client tooload altri messaggi dal servizio hello quando esegue un'operazione di ricezione. client Hello archivia questi messaggi in una cache locale. Hello dimensione della cache di hello è determinata da hello [Prefetchcount] [ QueueClient.PrefetchCount] o [prefetchcount su] [ SubscriptionClient.PrefetchCount] proprietà. Ogni client che abilita la prelettura mantiene la propria cache. La cache non è condivisa tra i client. Se hello client avvia un'operazione di ricezione e la cache è vuota, il servizio di hello trasmette un batch di messaggi. dimensione di Hello del batch hello pari hello dimensione della cache di hello o 256 KB, a seconda del valore minore. Se hello client avvia un'operazione di ricezione e della cache di hello contiene un messaggio, il messaggio hello viene eseguito dalla cache di hello.

Quando un messaggio viene sottoposto a prelettura, messaggio hello di blocchi servizio hello caricate in background. In questo modo, messaggio di prelettura hello non può essere ricevuto da un ricevitore diverso. Se il ricevitore di hello non può completare il messaggio hello prima della scadenza del blocco di hello, messaggio hello diventa ricevitori tooother disponibili. copia di Hello eseguita la prelettura del messaggio hello rimane nella cache di hello. Hello ricevitore che usa hello scaduta memorizzata nella cache copia riceverà un'eccezione durante il tentativo di toocomplete tale messaggio. Per impostazione predefinita, il blocco di messaggio hello scade dopo 60 secondi. Questo valore può essere estesa too5 minuti. utilizzo di hello tooprevent messaggi scaduti, la dimensione della cache di hello deve essere sempre inferiore al numero di hello di messaggi che possono essere utilizzati da un client nell'intervallo di timeout di blocco hello.

Quando si usa hello scadenza del blocco predefinito di 60 secondi, il valore per una buona [prefetchcount su] [ SubscriptionClient.PrefetchCount] hello 20 volte massimo elaborazione frequenze di tutti i ricevitori della factory hello. Ad esempio, una factory crei 3 ricevitori e ogni ricevitore può elaborare i messaggi too10 al secondo. conteggio di Hello prelettura non deve superare 20 X 3 X 10 = 600. Per impostazione predefinita, [Prefetchcount] [ QueueClient.PrefetchCount] è too0 set, il che significa che nessun altro messaggio viene recuperato dal servizio hello.

La prelettura dei messaggi aumenta hello velocità effettiva globale per una coda o sottoscrizione perché riduce hello al numero complessivo di operazioni di messaggio, o round trip. Recupero del primo messaggio hello, tuttavia, richiede più tempo (a causa delle dimensioni del messaggio toohello aumentato). Ricezione di messaggi sottoposti a prelettura sarà essere più veloce perché questi messaggi sono stati già scaricati dal client hello.

proprietà di (durata TTL) time-to-live Hello di un messaggio viene controllata dal server hello in fase di hello server hello invia client toohello di messaggio hello. client Hello selezionare proprietà di durata (TTL) del messaggio hello quando viene ricevuto il messaggio hello. Al contrario, il messaggio hello può essere ricevuto anche se ha superato durata (TTL) del messaggio hello mentre il messaggio hello è memorizzata nella cache dal client hello.

La prelettura non influisce sul numero di hello di operazioni di messaggistica fatturabili ed è disponibile solo per hello protocollo client di Service Bus. Hello protocollo HTTP non supporta la prelettura. Questa funzionalità è disponibile per le operazioni di ricezione sincrone e asincrone.

## <a name="express-queues-and-topics"></a>Code e argomenti rapidi

Entità Express abilitare scenari di riduzione della latenza e velocità effettiva elevata e sono supportate solo nel livello di messaggistica Standard hello. Le entità create nelle [spazi dei nomi Premium](service-bus-premium-messaging.md) hello express opzione non è supportata. Con le entità rapide, se viene inviato un messaggio tooa coda o argomento, il messaggio hello non viene archiviato immediatamente nell'archivio di messaggistica hello. ma viene memorizzato nella cache in memoria. Se il messaggio rimane nella coda di hello per più di pochi secondi, viene scritta automaticamente toostable archiviazione, pertanto la protezione da perdita a causa di un'interruzione di tooan. Scrittura di messaggi hello in una cache di memoria aumentano la velocità effettiva e riducono la latenza poiché non esiste alcun toostable accesso spazio di archiviazione nel messaggio hello in fase di hello viene inviato. I messaggi usati entro pochi secondi non vengono scritte toohello archivio messaggi. Hello di esempio seguente crea un argomento rapido.

```csharp
TopicDescription td = new TopicDescription(TopicName);
td.EnableExpress = true;
namespaceManager.CreateTopic(td);
```

Se un messaggio contenente informazioni critiche che non devono andare perdute viene inviato entità express tooan, mittente hello possibile forzare il Bus di servizio tooimmediately mantenere archiviazione toostable dei messaggi hello dall'impostazione hello [ForcePersistence] [ ForcePersistence] proprietà troppo**true**.

> [!NOTE]
> Le entità express non supportano le transazioni.

## <a name="use-of-partitioned-queues-or-topics"></a>Uso di code o argomenti partizionati
Internamente, viene utilizzato il Bus di servizio hello stesso nodo e tooprocess di archivio di messaggistica e archiviazione tutti i messaggi per un'entità di messaggistica (coda o argomento). Una coda o argomento partizionato, su hello invece viene distribuito tra più nodi e archivi di messaggistica. Le code e gli argomenti partizionati non solo registrano una velocità effettiva superiore rispetto a quella delle code e degli argomenti normali, ma presentano anche una maggiore disponibilità. toocreate un'entità partizionata, hello set [proprietà EnablePartitioning] [ EnablePartitioning] proprietà troppo**true**, come illustrato nell'esempio seguente hello. Per altre informazioni sulle entità partizionate, vedere le [entità di messaggistica partizionate][Partitioned messaging entities].

```csharp
// Create partitioned queue.
QueueDescription qd = new QueueDescription(QueueName);
qd.EnablePartitioning = true;
namespaceManager.CreateQueue(qd);
```

## <a name="use-of-multiple-queues"></a>Uso di più code

Se non è possibile toouse che una coda o argomento o partizionato hello previsto carico non può essere gestito da una singola coda o argomento partizionato, è necessario utilizzare più entità di messaggistica. Quando si usano più entità, creare un client dedicato per ogni entità, anziché utilizzare hello stesso client per tutte le entità.

## <a name="development-and-testing-features"></a>Funzionalità di sviluppo e test

Il bus di servizio presenta una funzionalità che viene usata in particolare per lo sviluppo e che **non deve mai essere usata nelle configurazioni di produzione**: [TopicDescription.EnableFilteringMessagesBeforePublishing][].

Nuove regole o i filtri vengono aggiunti toohello argomento, è possibile utilizzare [TopicDescription.EnableFilteringMessagesBeforePublishing][] tooverify che hello nuova espressione di filtro funziona come previsto.

## <a name="scenarios"></a>Scenari
Hello nelle sezioni seguenti descrivono tipici scenari di messaggistica e descrive le impostazioni Bus di servizio hello preferito. La velocità effettiva è classificata come bassa (minore di 1 messaggio al secondo), moderata (maggiore o uguale a 1 messaggio al secondo ma minore di 100 messaggi al secondo) ed elevata (maggiore o uguale a 100 messaggi al secondo). Hello numero di client è classificato come ridotto (5 o meno), moderato (più di 5 ma minore di o too20 uguale) e grandi dimensioni (oltre 20).

### <a name="high-throughput-queue"></a>Coda ad alta velocità effettiva
Obiettivo: Ottimizzare la velocità effettiva di hello di una singola coda. numero di Hello di mittenti e ricevitori è limitato.

* Usare una coda partizionata per migliorare prestazioni e disponibilità.
* hello tooincrease complessivo velocità di invio nella coda di hello, utilizzare più mittenti toocreate factory. Per ogni mittente usare operazioni asincrone o più thread.
* hello tooincrease complessivo velocità di ricezione dalla coda di hello, utilizzare più ricevitori toocreate factory di messaggio.
* Usare il vantaggio tootake operazioni asincrone di invio in batch sul lato client.
* Impostare hello batch numero di intervallo too50ms tooreduce hello di trasmissioni tramite il protocollo client Bus di servizio. Se vengono usati più mittenti, aumentare hello too100ms intervallo di invio in batch.
* Lasciare abilitato l'accesso in batch all'archivio. In questo modo aumenta hello complessiva frequenza in cui i messaggi possono essere scritti nella coda di hello.
* Impostare i tempi di too20 di hello prefetch count velocità di elaborazione massima hello di tutti i ricevitori della factory. In questo modo si riduce il numero di hello di trasmissioni tramite il protocollo client Bus di servizio.

### <a name="multiple-high-throughput-queues"></a>Code multiple ad alta velocità effettiva
Obiettivo: aumentare la velocità effettiva complessiva di più code. velocità effettiva di Hello di una singola coda è moderata o elevata.

velocità effettiva massima di tooobtain tra più code, utilizza le impostazioni di hello descritte la velocità effettiva hello toomaximize di una singola coda. Inoltre, utilizzare i client toocreate factory diverse che inviano o ricevono da code diverse.

### <a name="low-latency-queue"></a>Coda a bassa latenza
Obiettivo: ridurre la latenza end-to-end di una coda o di un argomento. numero di Hello di mittenti e ricevitori è limitato. velocità effettiva di Hello di hello coda è ridotta o moderata.

* Usare una coda partizionata migliorare la disponibilità.
* Disabilitare l'invio in batch sul lato client. client Hello invia immediatamente un messaggio.
* Disabilitare l'accesso in batch all'archivio. servizio Hello scrive immediatamente l'archivio di toohello messaggi hello.
* Se si utilizza un singolo client, impostare hello prefetch count too20 volte hello velocità di elaborazione del ricevitore hello. Se più messaggi arrivano nella coda di hello hello stesso tempo, hello protocollo client di Service Bus trasmette tutto a hello contemporaneamente. Quando il client di hello riceve il messaggio successivo hello, che il messaggio è già nella cache locale hello. cache di Hello dovrebbe essere basso.
* Se si utilizza più client, impostare hello prefetch count too0. In questo modo, l'utente hello secondo client può ricevere secondo messaggio hello mentre il primo client hello sta ancora elaborando primo messaggio hello.

### <a name="queue-with-a-large-number-of-senders"></a>Coda con un numero elevato di mittenti
Obiettivo: aumentare la velocità effettiva di una coda o di un argomento con un numero elevato di mittenti. Ogni mittente invia messaggi con una velocità moderata. numero di Hello di ricevitori è limitato.

Bus di servizio consente di tooa di connessioni simultanee too1000 entità di messaggistica (o 5000 con AMQP). Questo limite viene applicato a livello di spazio dei nomi hello e dal limite hello di connessioni simultanee per spazio dei nomi sono limitate in code o argomenti/sottoscrizioni. Per le code, questo numero è condiviso tra mittenti e ricevitori. Se tutte le connessioni di 1000 sono necessari per i mittenti, è necessario sostituire coda hello con un argomento e una singola sottoscrizione. Un argomento accetta too1000 connessioni simultanee dai mittenti, mentre la sottoscrizione hello accetta un ulteriori connessioni simultanee di 1000 dai ricevitori. Se sono necessari più di 1000 mittenti simultanei mittenti hello per l'invio di messaggi toohello protocollo di Service Bus tramite HTTP.

velocità effettiva toomaximize, hello seguenti:

* Usare una coda partizionata per migliorare prestazioni e disponibilità.
* Se ogni mittente si trova in un processo diverso, usare solo una singola factory per processo.
* Usare il vantaggio tootake operazioni asincrone di invio in batch sul lato client.
* Utilizzare il valore predefinito hello batch intervallo di 20 ms tooreduce hello numero di trasmissioni tramite il protocollo client Bus di servizio.
* Lasciare abilitato l'accesso in batch all'archivio. In questo modo aumenta hello complessiva frequenza in cui possono essere scritti i messaggi in coda hello o un argomento.
* Impostare i tempi di too20 di hello prefetch count velocità di elaborazione massima hello di tutti i ricevitori della factory. In questo modo si riduce il numero di hello di trasmissioni tramite il protocollo client Bus di servizio.

### <a name="queue-with-a-large-number-of-receivers"></a>Coda con un numero elevato di ricevitori
Obiettivo: Hello ottimizzare la velocità di una coda o sottoscrizione con un numero elevato di ricevitori di ricezione. Ogni ricevitore riceve messaggi a una velocità moderata. numero di Hello di mittenti è limitato.

Bus di servizio consente di entità di tooan too1000 connessioni simultanee. Se una coda richiede più di 1000 ricevitori, è necessario sostituire coda hello con un argomento e più sottoscrizioni. Ogni sottoscrizione può supportare le connessioni simultanee too1000. In alternativa, ricevitori possono accedere coda hello tramite hello protocollo HTTP.

velocità effettiva toomaximize, hello seguenti:

* Usare una coda partizionata per migliorare prestazioni e disponibilità.
* Se ogni ricevitore si trova in un processo diverso, usare solo una singola factory per processo.
* I ricevitori possono usare operazioni sincrone o asincrone. Specificato con gravità moderata hello velocità di un singolo ricevitore di ricezione, invio in batch sul lato client di una richiesta Complete non influisce sulla velocità effettiva del ricevitore.
* Lasciare abilitato l'accesso in batch all'archivio. Hello questo modo si riduce il carico complessivo dell'entità hello. Riduce inoltre hello velocità con cui possono essere scritti i messaggi in coda hello o un argomento.
* Impostare valore piccola tooa hello prefetch count (ad esempio PrefetchCount = 10). In questo modo si evita che i ricevitori rimangano inattivi mentre per altri è presente un numero elevato di messaggi memorizzati nella cache.

### <a name="topic-with-a-small-number-of-subscriptions"></a>Argomento con un numero limitato di sottoscrizioni
Obiettivo: Ottimizzare la velocità effettiva di hello di un argomento con un numero limitato di sottoscrizioni. Un messaggio viene ricevuto da molte sottoscrizioni, ovvero hello combinato ricezione velocità su tutte le sottoscrizioni è maggiore velocità di invio hello. numero di Hello di mittenti è limitato. numero di Hello di ricevitori per sottoscrizione è limitato.

velocità effettiva toomaximize, hello seguenti:

* Usare un argomento partizionato per migliorare prestazioni e disponibilità.
* hello tooincrease complessivo velocità di invio in argomento hello, utilizzare più mittenti toocreate factory. Per ogni mittente usare operazioni asincrone o più thread.
* hello tooincrease complessivo velocità di ricezione da una sottoscrizione, utilizzare più ricevitori toocreate factory di messaggio. Per ogni ricevitore usare operazioni asincrone o più thread.
* Usare il vantaggio tootake operazioni asincrone di invio in batch sul lato client.
* Utilizzare il valore predefinito hello batch intervallo di 20 ms tooreduce hello numero di trasmissioni tramite il protocollo client Bus di servizio.
* Lasciare abilitato l'accesso in batch all'archivio. In questo modo aumenta hello complessiva frequenza in cui i messaggi possono essere scritti in argomento hello.
* Impostare i tempi di too20 di hello prefetch count velocità di elaborazione massima hello di tutti i ricevitori della factory. In questo modo si riduce il numero di hello di trasmissioni tramite il protocollo client Bus di servizio.

### <a name="topic-with-a-large-number-of-subscriptions"></a>Argomento con un numero elevato di sottoscrizioni
Obiettivo: Ottimizzare la velocità effettiva di hello di un argomento con un numero elevato di sottoscrizioni. Un messaggio viene ricevuto da molte sottoscrizioni, ovvero hello combinato ricezione velocità su tutte le sottoscrizioni è maggiori rispetto alla velocità di invio hello. numero di Hello di mittenti è limitato. numero di Hello di ricevitori per sottoscrizione è limitato.

Gli argomenti con un numero elevato di sottoscrizioni in genere espongono una velocità effettiva globale ridotta se tutti i messaggi vengono indirizzati tooall sottoscrizioni. Ciò è causato dal fatto di hello che ogni messaggio viene ricevuto più volte e tutti i messaggi contenuti in un argomento e tutte le relative sottoscrizioni vengono archiviate in hello stesso archivio. Si presuppone che il numero di hello di mittenti e numero di ricevitori per sottoscrizione è piccoli. Bus di servizio supporta backup too2, 000 sottoscrizioni per argomento.

velocità effettiva toomaximize, hello seguenti:

* Usare un argomento partizionato per migliorare prestazioni e disponibilità.
* Usare il vantaggio tootake operazioni asincrone di invio in batch sul lato client.
* Utilizzare il valore predefinito hello batch intervallo di 20 ms tooreduce hello numero di trasmissioni tramite il protocollo client Bus di servizio.
* Lasciare abilitato l'accesso in batch all'archivio. In questo modo aumenta hello complessiva frequenza in cui i messaggi possono essere scritti in argomento hello.
* Impostare i tempi di hello prefetch count too20 ricezione hello previsto frequenza in secondi. In questo modo si riduce il numero di hello di trasmissioni tramite il protocollo client Bus di servizio.

## <a name="next-steps"></a>Passaggi successivi
toolearn più sull'ottimizzazione delle prestazioni del Bus di servizio, vedere [le entità di messaggistica partizionate][Partitioned messaging entities].

[QueueClient]: /dotnet/api/microsoft.servicebus.messaging.queueclient
[MessageSender]: /dotnet/api/microsoft.servicebus.messaging.messagesender
[MessagingFactory]: /dotnet/api/microsoft.servicebus.messaging.messagingfactory
[PeekLock]: /dotnet/api/microsoft.servicebus.messaging.receivemode
[ReceiveAndDelete]: /dotnet/api/microsoft.servicebus.messaging.receivemode
[BatchFlushInterval]: /dotnet/api/microsoft.servicebus.messaging.netmessagingtransportsettings.batchflushinterval#Microsoft_ServiceBus_Messaging_NetMessagingTransportSettings_BatchFlushInterval
[EnableBatchedOperations]: /dotnet/api/microsoft.servicebus.messaging.queuedescription.enablebatchedoperations#Microsoft_ServiceBus_Messaging_QueueDescription_EnableBatchedOperations
[QueueClient.PrefetchCount]: /dotnet/api/microsoft.servicebus.messaging.queueclient.prefetchcount#Microsoft_ServiceBus_Messaging_QueueClient_PrefetchCount
[SubscriptionClient.PrefetchCount]: /dotnet/api/microsoft.servicebus.messaging.subscriptionclient.prefetchcount#Microsoft_ServiceBus_Messaging_SubscriptionClient_PrefetchCount
[ForcePersistence]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage.forcepersistence#Microsoft_ServiceBus_Messaging_BrokeredMessage_ForcePersistence
[EnablePartitioning]: /dotnet/api/microsoft.servicebus.messaging.queuedescription.enablepartitioning#Microsoft_ServiceBus_Messaging_QueueDescription_EnablePartitioning
[Partitioned messaging entities]: service-bus-partitioning.md
[TopicDescription.EnableFilteringMessagesBeforePublishing]: /dotnet/api/microsoft.servicebus.messaging.topicdescription.enablefilteringmessagesbeforepublishing#Microsoft_ServiceBus_Messaging_TopicDescription_EnableFilteringMessagesBeforePublishing
