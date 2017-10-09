---
title: aaaAzure Bus di servizio associati spazi dei nomi | Documenti Microsoft
description: Dettagli di implementazione e costi relativi allo spazio dei nomi associato
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 2440c8d3-ed2e-47e0-93cf-ab7fbb855d2e
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/2017
ms.author: sethm
ms.openlocfilehash: 4c44b2b95d2228e1ad8075b52634d88a1593d3b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="paired-namespace-implementation-details-and-cost-implications"></a>Dettagli di implementazione e implicazioni in termini di costi relativi allo spazio dei nomi associato
Hello [PairNamespaceAsync] [ PairNamespaceAsync] (metodo), utilizzando un [SendAvailabilityPairedNamespaceOptions] [ SendAvailabilityPairedNamespaceOptions] dell'istanza, esegue attività visibili per conto dell'utente. Poiché vi sono costi considerazioni quando si utilizza la funzione hello, è utile toounderstand quelle attività, in modo che si prevede che il comportamento di hello in tal caso. Hello API coinvolge hello segue il comportamento automatico per conto dell'utente:

* Creazione di code di backlog.
* Creazione di un [MessageSender] [ MessageSender] oggetto che discute tooqueues o argomenti.
* Quando un'entità di messaggistica non è disponibile, invia messaggi di ping toohello entità in un tentativo toodetect quando l'entità diventa nuovamente disponibile.
* Crea facoltativamente un set di "message pump" che sposta i messaggi da hello code primario toohello code di backlog.
* Le coordinate di chiusura o errore di hello primario e secondario [MessagingFactory] [ MessagingFactory] istanze.

In generale, hello funziona nel modo seguente: quando l'entità primaria hello è integro, si verifica alcuna modifica di comportamento. Quando hello [FailoverInterval] [ FailoverInterval] allo scadere dell'intervallo di durata, ed entità primaria hello non vede invia riesce dopo non temporaneo [MessagingException] [ MessagingException] o [TimeoutException][TimeoutException], si verifica hello seguente comportamento:

1. Inviare operazioni toohello primario entità sono disabilitate e ping sistema hello hello entità primaria finché i ping possono essere recapitati.
2. Viene selezionata una coda di backlog casuale.
3. [BrokeredMessage] [ BrokeredMessage] gli oggetti sono indirizzato toohello scelto coda di backlog.
4. Se un toohello operazione trasmissione scelto coda di backlog, coda viene estratta dalla rotazione hello e viene selezionata una nuova coda. Tutti i mittenti hello [MessagingFactory] [ MessagingFactory] istanza informazioni di errore hello.

Hello nelle figure seguenti illustrano sequenza hello. In primo luogo, il mittente hello invia messaggi.

![Spazi dei nomi associati][0]

Alla coda primaria toohello toosend errore, il mittente hello inizia a inviare messaggi tooa scelta casualmente coda di backlog. Contemporaneamente avvia un'attività di ping.

![Spazi dei nomi associati][1]

A questo punto i messaggi hello sono ancora nella coda secondaria hello e non sono stati recapitati coda primaria toohello. Quando la coda primaria hello è di nuovo integra, almeno un processo deve essere in esecuzione il sifone hello. sifone Hello recapita i messaggi hello da hello tutti vari backlog entità di destinazione appropriate toohello code (code e argomenti).

![Spazi dei nomi associati][2]

Hello parte restante di questo argomento sono descritti i dettagli specifici di hello del funzionamento di queste parti.

## <a name="creation-of-backlog-queues"></a>Creazione di code di backlog
Hello [SendAvailabilityPairedNamespaceOptions] [ SendAvailabilityPairedNamespaceOptions] oggetto passato toohello [PairNamespaceAsync] [ PairNamespaceAsync] metodo indica hello numero di backlog code si desidera toouse. Ogni coda di backlog viene quindi creata con hello impostare le proprietà seguenti in modo esplicito (tutti gli altri valori vengono impostati toohello [QueueDescription] [ QueueDescription] impostazioni predefinite):

| Path | [spazio dei nomi primario]/x-servicebus-transfer/[indice] dove [indice] è un valore espresso in [0, BacklogQueueCount] |
| --- | --- |
| MaxSizeInMegabytes |5120 |
| MaxDeliveryCount |int.MaxValue |
| DefaultMessageTimeToLive |TimeSpan.MaxValue |
| AutoDeleteOnIdle |TimeSpan.MaxValue |
| LockDuration |1 minuto |
| EnableDeadLetteringOnMessageExpiration |true |
| EnableBatchedOperations |true |

Ad esempio, prima coda di backlog hello creato per lo spazio dei nomi **contoso** denominato `contoso/x-servicebus-transfer/0`.

Quando si creano le code di hello, codice hello controlla innanzitutto toosee se esiste una coda. Se non esiste una coda di hello, quindi hello coda viene creata. codice Hello non pulizia code di backlog "aggiuntive". In particolare, se hello applicazione hello spazio dei nomi primario **contoso** richiede cinque code di backlog, ma una coda di backlog con il percorso di hello `contoso/x-servicebus-transfer/7` esiste, tale coda aggiuntiva è presente ma non viene utilizzato. sistema di Hello consente in modo esplicito tooexist code di backlog aggiuntive che non usata. Come proprietario dello spazio dei nomi di hello, è responsabile per la pulizia delle code di backlog inutilizzate o indesiderate. motivo di Hello per questa decisione è che il Bus di servizio non è possibile conoscere lo scopo dell'esistenza per tutte le code di hello nello spazio dei nomi. Inoltre, se una coda esistente con il nome specificato hello, ma non soddisfa hello presuppone [QueueDescription][QueueDescription], i motivi sono personalizzate per modificare le impostazioni predefinite di hello. Viene resa alcuna garanzia per le code di backlog toohello le modifiche apportate dal codice. Apportare tootest che le modifiche attentamente.

## <a name="custom-messagesender"></a>MessageSender personalizzato
Quando si inviano, tutti i messaggi passano attraverso un interno [MessageSender] [ MessageSender] oggetto che si comporta in genere quando tutto funziona e reindirizza le code di backlog toohello quando operazioni "break". Se viene rilevato un errore non temporaneo, viene avviato un timer. Dopo un [TimeSpan] [ TimeSpan] periodo costituito hello [FailoverInterval] [ FailoverInterval] valore della proprietà durante il quale non vengono inviati i messaggi riuscito , viene avviato il failover hello. A questo punto, hello verificherà quanto segue per ogni entità:

* Esegue un'operazione di ping ogni [PingPrimaryInterval] [ PingPrimaryInterval] toocheck se entità hello è disponibile. Al termine di questa attività, tutto il codice client che utilizza entità hello immediatamente inizia a inviare nuovi messaggi toohello principale dello spazio dei nomi.
* Richieste future toosend toothat stessa entità da qualsiasi altro mittente comporterà hello [BrokeredMessage] [ BrokeredMessage] inviati toobe modificato toosit nella coda di backlog hello. alcune proprietà modifica Hello rimuove hello [BrokeredMessage] [ BrokeredMessage] dell'oggetto e li archivia in un' posizione. Hello seguenti proprietà vengono eliminate e aggiunte in un nuovo alias, consentire hello e Service Bus SDK tooprocess messaggi in modo uniforme:

| Nome proprietà precedente | Nuovo nome proprietà |
| --- | --- |
| SessionId |x-ms-sessionid |
| TimeToLive |x-ms-timetolive |
| ScheduledEnqueueTimeUtc |x-ms-path |

percorso di destinazione originale Hello viene memorizzato anche il messaggio hello come una proprietà denominata x-ms-path. Questa progettazione consente i messaggi per molte entità toocoexist in un'unica coda di backlog. proprietà Hello vengono ritrasferite dal sifone hello.

Hello personalizzato [MessageSender] [ MessageSender] oggetto può verificarsi problemi quando i messaggi raggiungono il limite di 256 KB hello e viene avviato il failover. Hello personalizzato [MessageSender] [ MessageSender] oggetto archivia i messaggi per tutte le code e gli argomenti nelle code di backlog hello. Questo oggetto sono presenti messaggi da numerose code primarie nelle code di backlog hello. toohandle bilanciamento del carico tra più client che non conoscono in modo casuale ogni altra hello SDK seleziona una coda di backlog per ogni [QueueClient] [ QueueClient] o [TopicClient] [ TopicClient] vengono create nel codice.

## <a name="pings"></a>Ping
Un messaggio ping è un oggetto vuoto [BrokeredMessage] [ BrokeredMessage] con il relativo [ContentType] [ ContentType] tooapplication/vnd.ms-bus di servizio-ping impostata. e un [TimeToLive] [ TimeToLive] valore di 1 secondo. Questo ping presenta una caratteristica particolare nel Bus di servizio: hello server non recapita mai un ping quando un chiamante qualsiasi richiede un [BrokeredMessage][BrokeredMessage]. Di conseguenza, non sarà mai necessario toolearn come tooreceive e ignorare questi messaggi. Ogni entità (argomento o coda univoca) per ogni [MessagingFactory] [ MessagingFactory] istanza per ogni client verrà eseguito il ping quando vengono considerate come toobe non disponibile. Per impostazione predefinita, ciò accade una volta al minuto. Messaggi di ping sono considerati messaggi del Bus di servizio regolari toobe e possono comportare costi per i messaggi e della larghezza di banda. Non appena il client di hello rilevano che il sistema hello è disponibile, i messaggi hello l'interruzione.

## <a name="hello-syphon"></a>sifone Hello
Almeno un programma eseguibile in un'applicazione hello deve eseguire attivamente il sifone hello. sifone Hello esegue long polling ricezione durata di 15 minuti. Quando sono disponibili tutte le entità e si dispone di 10 code di backlog, hello applicazione che ospita le chiamate sifone hello hello ricezione operazione 40 volte all'ora, 960 volte al giorno e 28800 volte in 30 giorni. Quando hello sifone Sposta attivamente i messaggi dalla coda principale di hello backlog toohello, ogni messaggio esperienze hello spese (costi standard relativi alle dimensioni del messaggio e la larghezza di banda si applicano a tutte le fasi) seguenti:

1. Inviare toohello backlog.
2. Ricezione da backlog hello.
3. Inviare toohello primario.
4. Ricevere da hello primario.

## <a name="closefault-behavior"></a>Comportamento di chiusura o errore
All'interno di un'applicazione che ospita il sifone hello, una volta hello primario o secondario [MessagingFactory] [ MessagingFactory] si verifica un errore o viene chiuso senza il relativo partner anche viene verificato un errore o chiuso e hello sifone rileva questo stato , il sifone hello opera. Se altri hello [MessagingFactory] [ MessagingFactory] non è stato chiuso entro cinque secondi, hello sifone restituisce un errore hello ancora aperto [MessagingFactory] [ MessagingFactory] .

## <a name="next-steps"></a>Passaggi successivi
Per informazioni dettagliate sulla messaggistica asincrona del bus di servizio, vedere [Modelli di messaggistica asincrona e disponibilità elevata][Asynchronous messaging patterns and high availability]. 

[PairNamespaceAsync]: /dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_PairNamespaceAsync_Microsoft_ServiceBus_Messaging_PairedNamespaceOptions_
[SendAvailabilityPairedNamespaceOptions]: /dotnet/api/microsoft.servicebus.messaging.sendavailabilitypairednamespaceoptions
[MessageSender]: /dotnet/api/microsoft.servicebus.messaging.messagesender
[MessagingFactory]: /dotnet/api/microsoft.servicebus.messaging.messagingfactory
[FailoverInterval]: /dotnet/api/microsoft.servicebus.messaging.pairednamespaceoptions#Microsoft_ServiceBus_Messaging_PairedNamespaceOptions_FailoverInterval
[MessagingException]: /dotnet/api/microsoft.servicebus.messaging.messagingexception
[TimeoutException]: https://msdn.microsoft.com/library/azure/system.timeoutexception.aspx
[BrokeredMessage]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage
[QueueDescription]: /dotnet/api/microsoft.servicebus.messaging.queuedescription
[TimeSpan]: https://msdn.microsoft.com/library/azure/system.timespan.aspx
[PingPrimaryInterval]: /dotnet/api/microsoft.servicebus.messaging.sendavailabilitypairednamespaceoptions#Microsoft_ServiceBus_Messaging_SendAvailabilityPairedNamespaceOptions_PingPrimaryInterval
[QueueClient]: /dotnet/api/microsoft.servicebus.messaging.queueclient
[TopicClient]: /dotnet/api/microsoft.servicebus.messaging.topicclient
[ContentType]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_ContentType
[TimeToLive]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_TimeToLive
[Asynchronous messaging patterns and high availability]: service-bus-async-messaging.md
[0]: ./media/service-bus-paired-namespaces/IC673405.png
[1]: ./media/service-bus-paired-namespaces/IC673406.png
[2]: ./media/service-bus-paired-namespaces/IC673407.png
