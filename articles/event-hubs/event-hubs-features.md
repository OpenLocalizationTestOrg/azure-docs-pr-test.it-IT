---
title: "Panoramica delle funzionalità aaaAzure hub eventi | Documenti Microsoft"
description: "Panoramica e informazioni dettagliate sulle funzionalità di Hub eventi di Azure"
services: event-hubs
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/17/2017
ms.author: sethm
ms.openlocfilehash: 8094e48abc8455ed725d4d5d3f9895f431441e2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="event-hubs-features-overview"></a>Panoramica delle funzionalità di Hub eventi

Hub eventi di Azure è una servizio di elaborazione degli eventi scalabile che inserisce ed elabora grandi volumi di eventi e dati, con bassa latenza e affidabilità elevata. Vedere [che cos'è l'hub di eventi?](event-hubs-what-is-event-hubs.md) per una panoramica di alto livello di servizio hello.

In questo articolo si basa sulle informazioni hello hello [Panoramica](event-hubs-what-is-event-hubs.md)e vengono forniti dettagli tecnici e implementazione sui componenti di hub eventi e funzionalità.

## <a name="event-publishers"></a>Publisher di eventi

Qualsiasi entità che invia l'hub di eventi tooan dati è un producer di eventi o *publisher di eventi*. Gli autori di eventi possono pubblicare eventi usando HTTPS o AMQP 1.0. I Publisher di eventi utilizzare un tooidentify token di firma di accesso condiviso (SAS) stessi tooan hub eventi e possono avere un'identità univoca o utilizzare un token di firma di accesso condiviso comune.

### <a name="publishing-an-event"></a>Pubblicazione di un evento

È possibile pubblicare un evento tramite AMQP 1.0 o HTTPS. Hub eventi fornisce [classi e le librerie client](event-hubs-dotnet-framework-api-overview.md) per la pubblicazione di hub di eventi eventi tooan da client .NET. Per altre piattaforme e runtime, è possibile utilizzare qualsiasi client AMQP 1.0, ad esempio [Apache Qpid](http://qpid.apache.org/). È possibile pubblicare eventi singolarmente o in batch. Una singola pubblicazione (istanza dei dati dell'evento) ha un limite di 256 KB, indipendentemente dal fatto che si tratti di un singolo evento o di un batch. La pubblicazione di eventi di dimensioni superiori alla soglia determina un errore. È una procedura consigliata per i server di pubblicazione toobe consapevoli delle partizioni all'interno di hub eventi hello e specificare tooonly un *chiave di partizione* (introdotto nella sezione successiva hello) o la propria identità tramite il token di firma di accesso condiviso.

Hello scelta toouse AMQP e HTTPS è toohello specifico scenario di utilizzo. AMQP richiede stabilimento hello di un socket bidirezionale persistente in aggiunta tootransport livello security (TLS) o SSL/TLS. AMQP è maggiori costi di rete durante l'inizializzazione di sessione hello, tuttavia, HTTPS richiede un sovraccarico SSL aggiuntivo per ogni richiesta. AMQP offre prestazioni più elevate per i server di pubblicazione più attivi.

![Hub eventi](./media/event-hubs-features/partition_keys.png)

Hub eventi garantisce che tutti gli eventi che condividono un valore di chiave di partizione vengano recapitati in ordine e toohello stessa partizione. Se le chiavi di partizione vengono utilizzate con i criteri di server di pubblicazione, quindi hello identità dell'editore hello e valore hello hello della chiave di partizione deve corrispondere. In caso contrario, si verifica un errore.

### <a name="publisher-policy"></a>Criteri di autore

Hub eventi consente un controllo granulare degli autori di eventi tramite *criteri di autore*. Criteri dei Publisher sono funzionalità di runtime progettate toofacilitate un numero elevato di server di pubblicazione di eventi indipendente. Con i criteri dei publisher, ogni server di pubblicazione viene usato un identificatore univoco durante la pubblicazione di hub di eventi eventi tooan, tramite hello meccanismo seguente:

```
//[my namespace].servicebus.windows.net/[event hub name]/publishers/[my publisher name]
```

Non si dispone di nomi di server di pubblicazione toocreate anticipatamente, ma il token di firma di accesso condiviso hello usato per la pubblicazione di un evento, in identità dei publisher indipendenti tooensure ordine devono corrispondere. Quando si utilizzano i criteri dei publisher, hello **PartitionKey** toohello nome del server di pubblicazione è impostato. toowork al correttamente, tali valori devono corrispondere.

## <a name="capture"></a>Acquisizione

[Acquisizione di hub eventi](event-hubs-capture-overview.md) consente tooautomatically acquisizione hello flusso di dati in hub eventi e salvarlo tooyour scelta di un account di archiviazione Blob o un account del servizio di Azure Data Lake. È possibile abilitare l'acquisizione dal portale di Azure hello e specificare una dimensione minima e l'acquisizione di hello tooperform finestra ora. Utilizza acquisizione hub eventi, specificare il proprio account di archiviazione Blob di Azure e un contenitore o account di servizio di Azure Data Lake, ovvero hello toostore utilizzati i dati acquisiti. Dati acquisiti viene scritto nel formato di Apache Avro hello.

## <a name="partitions"></a>Partitions

Hub eventi fornisce flusso di messaggi tramite un modello consumer partizionato in cui ogni consumer legge solo un sottoinsieme specifico o una partizione, hello del flusso di messaggi. Questo modello consente la scalabilità orizzontale per l'elaborazione di eventi e fornisce altre funzionalità incentrate sul flusso non disponibili in code e argomenti.

Una partizione è una sequenza ordinata di eventi contenuta in un hub eventi. Quando gli eventi più recenti arrivano, vengono aggiunti toohello fine di questa sequenza. Una partizione può essere considerata come "registro commit".

![Hub eventi](./media/event-hubs-features/partition.png)

Hub eventi conserva i dati per un periodo di conservazione configurato che è applicabile a tutte le partizioni nell'hub eventi hello. Gli eventi scadono su base temporale; non è possibile eliminarli in modo esplicito. Poiché le partizioni sono indipendenti e contengono una sequenza specifica di dati, presentano spesso velocità di crescita diverse.

![Hub eventi](./media/event-hubs-features/multiple_partitions.png)

numero di Hello di partizioni specificato al momento della creazione e deve essere compreso tra 2 e 32. il numero di partizioni Hello non modificabile, pertanto è consigliabile a lungo termine scalabilità quando si imposta il numero di partizioni. Le partizioni sono un meccanismo di organizzazione dei dati che si riferisce toohello parallelismo downstream necessario nelle applicazioni consumer. Hello numero di partizioni in un hub eventi è direttamente correlato toohello numero di lettori simultanei previsto toohave. È possibile aumentare il numero di hello di partizioni di là 32 contattando il team di hello hub eventi.

Mentre le partizioni siano identificabili e possono essere inviate toodirectly, inviare direttamente tooa partizione non è consigliata. In alternativa, è possibile utilizzare costrutti di livello superiore introdotti in hello [publisher di eventi](#event-publishers) e [capacità](#capacity) sezioni. 

Le partizioni vengono riempite con una sequenza di dati di evento che contengono il corpo di hello dell'evento hello, un contenitore delle proprietà definite dall'utente e i metadati, ad esempio l'offset nella partizione di hello e il relativo numero di sequenza flusso hello.

Per ulteriori informazioni sulle partizioni e compromesso hello tra disponibilità e affidabilità, vedere hello [Guida alla programmazione di hub eventi](event-hubs-programming-guide.md#partition-key) hello e [disponibilità e la coerenza in hub eventi](event-hubs-availability-and-consistency.md) articolo .

### <a name="partition-key"></a>Chiave di partizione

È possibile utilizzare un [chiave di partizione](event-hubs-programming-guide.md#partition-key) toomap dati dell'evento in ingresso in partizioni specifiche a scopo di hello di organizzazione dei dati. chiave di partizione Hello è un valore fornito dal mittente passato a un hub di eventi. Viene elaborato tramite una funzione di hashing statica, che crea l'assegnazione della partizione hello. Se non si specifica una chiave di partizione quando si pubblica un evento, viene usata un'assegnazione round robin.

publisher di eventi Hello è consapevole solo della chiave di partizione e non gli eventi di hello toowhich di hello partizione vengono pubblicati. Questa separazione della chiave e partizione isola mittente hello tooknow troppo sull'elaborazione a valle di hello. Una per ogni dispositivo o utente univoco identità rende una buona chiave di partizione, ma gli altri attributi, ad esempio area geografica possono essere anche usato toogroup eventi correlati in un'unica partizione.

## <a name="sas-tokens"></a>Token di firma di accesso condiviso

Hub eventi Usa *firme di accesso condiviso*, che sono disponibili a livello di hub eventi e di spazio dei nomi di hello. Un token SAS viene generato da una chiave SAS ed è un hash SHA di un URL, codificato in un formato specifico. Usa nome hello della chiave di hello (criterio) e del token hello, hub eventi può rigenerare l'hash hello e pertanto autenticare il mittente di hello. In genere, i token di firma di accesso condiviso per gli autori di eventi vengono creati con privilegi solo di **invio** per un hub eventi specifico. Questo meccanismo di URL token di firma di accesso condiviso è hello base introdotte in criteri dell'editore hello identificazione del publisher. Per altre informazioni sull'uso di SAS, vedere [Autenticazione della firma di accesso condiviso con il bus di servizio](../service-bus-messaging/service-bus-sas.md).

## <a name="event-consumers"></a>Consumer di eventi

Qualsiasi entità che legge i dati dell'evento da un hub eventi è un *consumer eventi*. Tutti i consumer di hub eventi si connettono tramite una sessione AMQP 1.0 hello e gli eventi vengono recapitati tramite sessione hello man mano che diventano disponibili. client Hello non è necessario toopoll per la disponibilità dei dati.

### <a name="consumer-groups"></a>Gruppi di utenti

meccanismo di pubblicazione/sottoscrizione Hello degli hub di eventi viene abilitato tramite *gruppi di consumer*. Un gruppo di consumer è una vista (stato, posizione o offset) di un intero hub eventi. Gruppi di consumer consentono a più applicazioni consumer tooeach dispone di una vista separata del flusso di eventi hello e flusso di hello tooread in modo indipendente in base alle proprie esigenze e con i propri offset.

In un flusso di architettura di elaborazione, ogni applicazione downstream equivale tooa gruppo di consumer. Se si desidera toowrite archiviazione toolong termine dei dati evento, tale applicazione del writer di archiviazione è un gruppo di consumer. L'elaborazione di eventi complessi può essere quindi eseguita da un altro gruppo di consumer separato. È possibile accedere alla partizioni solo tramite un gruppo di consumer. In una partizione per un gruppo di consumer ci possono essere al massimo cinque lettori simultanei; è tuttavia **consigliabile che in una partizione per un gruppo di consumer ci sia solo un ricevitore attivo**. In un hub eventi è sempre un gruppo di consumer predefinito e creare i gruppi di consumer too20 per un hub di eventi di livello Standard.

Hello negli esempi seguenti vengono convenzione dell'URI gruppo consumer hello:

```http
//[my namespace].servicebus.windows.net/[event hub name]/[Consumer Group #1]
//[my namespace].servicebus.windows.net/[event hub name]/[Consumer Group #2]
```

Hello figura seguente viene illustrata l'architettura dell'elaborazione di flusso hub eventi hello:

![Hub eventi](./media/event-hubs-features/event_hubs_architecture.png)

### <a name="stream-offsets"></a>Offset di flusso

Un *offset* hello posizione di un evento all'interno di una partizione. Un offset può essere considerato come un cursore sul lato client. offset Hello è un byte la numerazione dell'evento hello. Questo offset consente toospecify di consumer (lettore) un punto nel flusso di eventi hello da cui desiderano eseguire la lettura degli eventi toobegin un evento. È possibile specificare offset hello come timestamp o come un valore di offset. I consumer sono responsabili per l'archiviazione dei valori di offset all'esterno di hello servizio hub eventi. All'interno di una partizione, ogni evento include un offset.

![Hub eventi](./media/event-hubs-features/partition_offset.png)

### <a name="checkpointing"></a>Checkpoint

*Checkpoint* è un processo mediante il quale i lettori contrassegnano o eseguono il commit della propria posizione all'interno di una sequenza di eventi di partizione. Creazione di checkpoint hello responsabilità del consumer hello e viene eseguita in una base per ogni partizione all'interno di un gruppo di consumer. Questa responsabilità significa che per ogni gruppo di consumer, ogni reader della partizione deve tenere traccia della posizione corrente nel flusso di eventi hello e può informare il servizio di hello quando il flusso di dati hello considera completo.

Se un reader si disconnette da una partizione, quando si riconnette inizia a leggere al checkpoint hello che è stato inviato in precedenza dall'ultimo reader hello della partizione in tale gruppo di consumer. Quando hello reader si connette, passa questo toohello offset evento hub toospecify hello percorso in cui lettura toostart. In questo modo, è possibile utilizzare checkpoint tooboth contrassegnare gli eventi come "completamento" per le applicazioni downstream, e si verifica resilienza tooprovide se un failover tra reader in esecuzione in computer diversi. È possibile tooreturn tooolder dati specificando un offset inferiore da questo processo di creazione di checkpoint. Tramite questo meccanismo il checkpoint consente sia la resilienza del failover che la riproduzione del flusso di eventi.

### <a name="common-consumer-tasks"></a>Attività comuni del consumer

Tutti i consumer di Hub eventi si connettono tramite una sessione AMQP 1.0 e un canale di comunicazione bidirezionale in grado di riconoscere lo stato. Ogni partizione dispone di una sessione AMQP 1.0 che facilita il trasporto hello di eventi isolati dalla partizione.

#### <a name="connect-tooa-partition"></a>Connettersi tooa partizione

Quando ci si connette toopartitions, è comune toouse pratica leasing partizioni toospecific connessioni di meccanismo toocoordinate lettore. In questo modo, è possibile per ogni partizione in un consumer gruppo toohave un solo reader attivo. Creazione di checkpoint, leasing e la gestione di lettori sono semplificati tramite hello [EventProcessorHost](/dotnet/api/microsoft.servicebus.messaging.eventprocessorhost) classe per i client .NET. Host processore di eventi Hello è un agente consumer intelligente.

#### <a name="read-events"></a>Leggere gli eventi

Dopo una sessione AMQP 1.0 e il collegamento viene aperta per una partizione specifica, gli eventi vengono recapitati client toohello AMQP 1.0 dal servizio hub eventi hello. Questo meccanismo di recapito permette una velocità effettiva più elevata e una latenza più bassa rispetto ai meccanismi basati su pull, ad esempio HTTP GET. Come gli eventi vengono inviati toohello client, ogni istanza di dati di evento contiene metadati importanti, come numero di sequenza e offset hello che vengono utilizzati toofacilitate checkpoint nella sequenza di eventi hello.

Dati evento:
* Offset
* Numero di sequenza
* Corpo
* Proprietà utente
* Proprietà di sistema

È l'offset di hello toomanage responsabilità.

## <a name="capacity"></a>Capacity

Hub eventi presenta un'architettura parallela altamente scalabile e vi sono alcuni fattori chiave tooconsider, durante il ridimensionamento e scalabilità.

### <a name="throughput-units"></a>Unità elaborate

capacità di Hello velocità effettiva degli hub di eventi è controllata dal *unità di velocità effettiva*. Le unità elaborate sono unità di capacità pre-acquistate. Un'unità di velocità effettiva singolo include hello seguenti capacità:

* In entrata: backup too1 MB al secondo o 1000 eventi al secondo (a seconda del valore per primo)
* In uscita: backup too2 MB al secondo

Oltrepassato la capacità di hello di hello acquistata unità di velocità effettiva, in entrata è limitato e un [ServerBusyException](/dotnet/api/microsoft.servicebus.messaging.serverbusyexception) viene restituito. In uscita non genera eccezioni di limitazione delle richieste, ma è comunque limitata toohello capacità di hello unità di velocità effettiva acquistata. Se si ricevono eccezioni relative alla velocità pubblicazione o sono previsti volumi in uscita maggiori toosee, essere toocheck che il numero di unità di velocità effettiva acquistate per spazio dei nomi hello. È possibile gestire le unità di velocità effettiva in hello **scala** pannello degli spazi dei nomi hello in hello [portale di Azure](https://portal.azure.com). È inoltre possibile gestire le unità di velocità effettiva a livello di programmazione utilizzando hello [API degli hub di eventi](event-hubs-api-overview.md).

Le unità elaborate vengo o fatturate su base oraria e sono pre-acquistate. Una volta acquistate, le unità elaborate vengono fatturate per un minimo di un'ora. Backup too20 unità di velocità effettiva possono essere acquistate per uno spazio dei nomi dell'hub eventi e vengono condivise tra tutti gli hub eventi hello dello spazio dei nomi.

È possibile acquistare ulteriori unità di velocità effettiva in blocchi di 20 unità di velocità effettiva too100, contattando il supporto tecnico di Azure. Inoltre, è possibile acquistare blocchi di 100 unità elaborate.

È consigliabile bilanciare la velocità effettiva unità e le partizioni tooachieve una scalabilità ottimale. Una singola partizione ha una scala massima di una unità elaborata. Hello numero di unità di velocità effettiva deve essere minore o uguale toohello numero di partizioni in un hub eventi.

Per informazioni dettagliate sui prezzi di Hub eventi, vedere [Prezzi di Hub eventi ](https://azure.microsoft.com/pricing/details/event-hubs/).

## <a name="next-steps"></a>Passaggi successivi

Per ulteriori informazioni sugli hub di eventi, visitare hello seguenti collegamenti:

* Iniziare con un'[esercitazione di Hub eventi][Event Hubs tutorial]
* [Guida alla programmazione di Hub eventi](event-hubs-programming-guide.md)
* [Disponibilità e coerenza nell'Hub eventi](event-hubs-availability-and-consistency.md)
* [Domande frequenti su Hub eventi](event-hubs-faq.md)
* [Esempi di Hub eventi][]

[Event Hubs tutorial]: event-hubs-dotnet-standard-getstarted-send.md
[Esempi di Hub eventi]: https://github.com/Azure/azure-event-hubs/tree/master/samples
