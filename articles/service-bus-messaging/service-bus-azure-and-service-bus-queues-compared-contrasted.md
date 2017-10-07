---
title: le code di archiviazione aaaAzure e code del Bus di servizio - confronto e contrapposizioni | Documenti Microsoft
description: Analizza i punti in comune e le differenze tra i due tipi di code offerti da Azure.
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: tysonn
ms.assetid: f07301dc-ca9b-465c-bd5b-a0f99bab606b
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 08/07/2017
ms.author: sethm
ms.openlocfilehash: f8b915e73ea3c82d823a96bf23c8c9e24c96aa42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="storage-queues-and-service-bus-queues---compared-and-contrasted"></a>Analogie e differenze tra le code di archiviazione e le code del bus di servizio
Questo articolo vengono analizzate le differenze di hello e le analogie tra tipi di hello due di code offerte attualmente da Microsoft Azure: code di archiviazione e le code del Bus di servizio. Utilizzando queste informazioni, è possibile confrontare e contrapporre rispettive tecnologie hello ed essere in grado di toomake una decisione più oculata circa la migliore soluzione adatta alle proprie esigenze.

## <a name="introduction"></a>Introduzione
Azure supporta due tipi di meccanismi di code: **code di archiviazione** e **code del bus di servizio**.

**Le code di archiviazione**, che fanno parte di hello [archiviazione di Azure](https://azure.microsoft.com/services/storage/) infrastruttura, funzionalità una semplice interfaccia basata su REST GET/PUT/visualizzazione, che offre affidabili e persistenti all'interno e tra i servizi di messaggistica.

Le **code del bus di servizio** fanno parte di un'infrastruttura di [messaggistica di Azure](https://azure.microsoft.com/services/service-bus/) più ampia che supporta accodamento, pubblicazione/sottoscrizione e modelli di integrazione più avanzati. Per ulteriori informazioni sulle code/argomenti/sottoscrizioni del Bus di servizio, vedere hello [Panoramica del Bus di servizio](service-bus-messaging-overview.md).

Anche se entrambe le tecnologie di accodamento sono disponibili contemporaneamente, le code di archiviazione sono state introdotte per prime, come meccanismo dedicato di archiviazione code basato sui servizi di Archiviazione di Azure. Le code del Bus di servizio si avvalgono di hello più ampia di "messaggistica" infrastruttura progettata toointegrate applicazioni o componenti dell'applicazione che possono estendersi su più protocolli di comunicazione, contratti dati, domini trusted e/o ambienti di rete.

## <a name="technology-selection-considerations"></a>Considerazioni sulla selezione della tecnologia
Le code di archiviazione sia le code del Bus di servizio sono implementazioni di Accodamento messaggi hello servizio attualmente disponibile in Microsoft Azure. Ogni dispone di un set di funzionalità leggermente diverso, ovvero è possibile scegliere uno o altri hello o entrambe, a seconda delle esigenze di hello della particolare soluzione o del problema aziendale o tecnico da risolvere.

Quando si stabilisce la tecnologia di Accodamento soddisfa scopo hello per una determinata soluzione, gli sviluppatori e architetti di soluzioni devono considerare hello riportato di seguito. Per ulteriori informazioni, vedere la sezione successiva di hello.

Gli architetti e gli sviluppatori di soluzioni **dovrebbero considerare l'uso delle code di Azure** quando:

* L'applicazione è necessario archiviare oltre 80 GB di messaggi in una coda, in cui i messaggi hello hanno una durata inferiore a 7 giorni.
* L'applicazione desidera tootrack lo stato di avanzamento per l'elaborazione di un messaggio all'interno della coda di hello. Ciò è utile se si blocca lavoro hello l'elaborazione di un messaggio. Un processo di lavoro successivo può quindi utilizzare tale toocontinue informazioni in cui dal processo di lavoro precedente hello interrotta.
* È necessario che i log sul lato server di tutte le transazioni hello eseguite nelle code.

Gli architetti e gli sviluppatori di soluzioni **dovrebbero considerare l'uso delle code del bus di servizio** quando:

* La soluzione deve essere in grado di tooreceive messaggi senza coda hello toopoll. Con il Bus di servizio, questo può essere ottenuto con hello utilizzare di polling prolungato hello operazione utilizzando i protocolli basati su TCP hello che supporta il Bus di servizio di ricezione.
* La soluzione richiede hello coda tooprovide un garantito first-in-first-out (FIFO) recapito ordinato.
* Si vuole una configurazione simmetrica in Azure e su Windows Server (cloud privato). Per altre informazioni, vedere [Bus di servizio per Windows Server](https://msdn.microsoft.com/library/dn282144.aspx).
* La soluzione deve essere in grado di toosupport il rilevamento duplicato automatico.
* Si desidera visualizzare i messaggi tooprocess applicazione come flussi paralleli di esecuzione prolungata (i messaggi sono associati a un flusso utilizzando hello [SessionId](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.sessionid?view=azureservicebus-4.0.0#Microsoft_ServiceBus_Messaging_BrokeredMessage_SessionId) proprietà messaggio hello). In questo modello ciascun nodo hello utilizzano applicazioni in competizione per i flussi, come toomessages anziché. Quando un flusso viene assegnato tooa utilizzo nodo, il nodo di hello può esaminare lo stato di hello hello flusso dello stato dell'applicazione mediante transazioni.
* Per la soluzione sono necessari atomicità e comportamento transazionale in caso di invio o ricezione di più messaggi da una coda.
* Hello time-to-live (TTL) caratterizzano il carico di lavoro specifici dell'applicazione hello può superare il periodo di 7 giorni hello.
* L'applicazione gestisce i messaggi che possono superare i 64 KB, ma verrà probabilmente non approccio hello limite di 256 KB.
* Si gestiscono tooprovide un requisito toohello di modello un accesso basato sui ruoli, code e autorizzazioni/diritti diversi per mittenti e destinatari.
* Le dimensioni della coda non supereranno gli 80 GB.
* Si desidera toouse hello AMQP 1.0 basato su standard protocollo di messaggistica. Per altre informazioni su AMQP, vedere [Panoramica di AMQP per il bus di servizio](service-bus-amqp-overview.md).
* È possibile prevedere un'eventuale migrazione dalla Point to Point basati su coda comunicazione tooa modello di scambio messaggi che consente l'integrazione di destinatari aggiuntivi (sottoscrittori), ognuno dei quali vengono ricevute copie separate di alcuni o tutti i messaggi inviati toohello coda. Hello quest'ultimo fa riferimento a funzionalità di pubblicazione/sottoscrizione toohello livello nativo fornita dal Bus di servizio.
* La soluzione di messaggistica deve essere in grado di toosupport garanzia di recapito hello "At-Most-Once" senza necessità di hello di componenti aggiuntivi dell'infrastruttura di toobuild hello.
* Desideri toopublish in grado di toobe e utilizzare batch di messaggi.

## <a name="comparing-storage-queues-and-service-bus-queues"></a>Confronto tra code di archiviazione e code del bus di servizio
tabelle Hello hello le sezioni seguenti forniscono un raggruppamento logico delle funzionalità di coda e consentono di confrontare, a colpo d'occhio, hello funzionalità disponibili nelle code di archiviazione e le code del Bus di servizio.

## <a name="foundational-capabilities"></a>Funzionalità fondamentali
In questa sezione vengono confrontate alcune delle funzionalità Accodamento con hello fondamentali fornite dalle code di archiviazione e le code del Bus di servizio.

| Criteri di confronto | Code di archiviazione | Code del bus di servizio |
| --- | --- | --- |
| Garanzia di ordinamento |**No** <br/><br>Per ulteriori informazioni, vedere la nota prima di hello nella sezione "Informazioni aggiuntive" hello.</br> |**Sì - First-In-First-Out (FIFO)**<br/><br>(tramite l'utilizzo di hello di sessioni di messaggistica) |
| Garanzia di recapito |**At-Least-Once** |**At-Least-Once**<br/><br/>**At-Most-Once** |
| Supporto per l'operazione atomica |**No** |**Sì**<br/><br/> |
| Comportamento di ricezione |**Non-blocking**<br/><br/>(viene completata immediatamente se non vengono trovati altri messaggi) |**Blocking with/without timeout**<br/><br/>(offre polling prolungato o hello ["Tecnica Comet"](http://go.microsoft.com/fwlink/?LinkId=613759))<br/><br/>**Non-blocking**<br/><br/>(tramite hello utilizzo di .NET API solo gestito) |
| API di tipo push |**No** |**Sì**<br/><br/>Interfaccia API di .NET per sessioni [OnMessage](/dotnet/api/microsoft.servicebus.messaging.queueclient.onmessage#Microsoft_ServiceBus_Messaging_QueueClient_OnMessage_System_Action_Microsoft_ServiceBus_Messaging_BrokeredMessage__) e **OnMessage**. |
| Modalità di ricezione |**Visualizzazione e lease** |**Visualizzazione e blocco**<br/><br/>**Ricezione ed eliminazione** |
| Modalità di accesso esclusivo |**Basato sul lease** |**Basato sul blocco** |
| Durata lease/blocco |**30 secondi (impostazione predefinita)**<br/><br/>**7 giorni (durata massima)** (è possibile rinnovare o rilasciare un lease di messaggio utilizzando hello [UpdateMessage](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.updatemessage.aspx) API.) |**60 secondi (impostazione predefinita)**<br/><br/>È possibile rinnovare un blocco di messaggio mediante hello [RenewLock](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.renewlock#Microsoft_ServiceBus_Messaging_BrokeredMessage_RenewLock) API. |
| Precisione lease/blocco |**Livello di messaggio**<br/><br/>(ogni messaggio può avere un valore di timeout diverso, è possibile aggiornare come necessario durante l'elaborazione di messaggi hello, utilizzando hello [UpdateMessage](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.updatemessage.aspx) API) |**Livello di coda**<br/><br/>(ogni coda dispone di tooall di precisione applicata un blocco dei messaggi, ma è possibile rinnovare il blocco di hello mediante hello [RenewLock](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.renewlock#Microsoft_ServiceBus_Messaging_BrokeredMessage_RenewLock) API.) |
| Ricezione in batch |**Sì**<br/><br/>(in modo esplicito specificando il numero di messaggio durante il recupero dei messaggi, tooa massimo di 32 messaggi) |**Sì**<br/><br/>(in modo implicito l'abilitazione di una proprietà di prelettura o utilizzare in modo esplicito tramite hello delle transazioni) |
| Invio in batch |**No** |**Sì**<br/><br/>(tramite l'utilizzo di hello di transazioni o invio in batch sul lato client) |

### <a name="additional-information"></a>Informazioni aggiuntive
* In genere i messaggi nelle code di archiviazione sono ordinati in base al principio FIFO (First-In-First-Out), ma in alcuni casi possono risultare non in ordine, ad esempio quando la durata del timeout di visibilità di un messaggio scade a seguito dell'arresto anomalo di un'applicazione client durante l'elaborazione. Scadenza del timeout di visibilità hello, hello messaggio diventa nuovamente visibile nella coda di hello per un altro lavoro toodequeue è. A questo punto, messaggio appena visibile hello può essere posizionato nella coda di hello (toobe rimosso di nuovo) dopo un messaggio originariamente accodato dopo di esso.
* Hello garantito che il modello FIFO nelle code del Bus di servizio richiede l'uso di hello di sessioni di messaggistica. In hello evento hello applicazione si blocca durante l'elaborazione di un messaggio ricevuto in hello **visualizzazione e blocco** modalità, hello successivo un destinatario di code accetta una sessione di messaggistica, verrà avviato con un messaggio di errore hello dopo il Time-to-live (TTL) periodo scade.
* Le code di archiviazione sono toosupport progettato standard scenari di accodamento, ad esempio disaccoppiamento scalabilità tooincrease componenti dell'applicazione e tolleranza di errore, caricare livellamento e i flussi del processo.
* Le code del Bus di servizio supportano hello *At-Least-Once* garanzia di recapito. Inoltre, hello *At-Most-Once* semantica possono essere supportate con stato applicazione hello toostore lo stato della sessione e ricezione di messaggi mediante transazioni tooatomically e aggiornare lo stato della sessione hello.
* Le code di archiviazione offrono un modello di programmazione uniforme e coerente tra code, tabelle e BLOB, sia per i team di sviluppo che per i team operativi.
* Le code del Bus di servizio forniscono supporto per le transazioni locali nel contesto di hello di una singola coda.
* Hello **ricevere ed eliminare** modalità supportata dal Bus di servizio offre hello tooreduce possibilità di hello messaggistica conteggio delle operazioni (e relativo costo) in cambio di una garanzia di recapito.
* Le code di archiviazione forniscono lease con lease hello tooextend di hello possibilità per i messaggi. Ciò consente agli utenti di hello lease brevi toomaintain sui messaggi. Pertanto, se si blocca un thread di lavoro, il messaggio hello può essere rapidamente elaborato nuovamente da un altro processo di lavoro. Un thread di lavoro, inoltre, è possibile estendere a lease hello in un messaggio se è necessario tooprocess superiore a quella corrente hello lease ora.
* Le code di archiviazione offrono un timeout di visibilità che è possibile impostare durante hello inserimento o annullamento dell'accodamento di un messaggio. Inoltre, è possibile aggiornare un messaggio con valori di lease diversi in fase di esecuzione e aggiornamento diversi valori nei messaggi nella hello stessa coda. Timeout blocchi Bus di servizio sono definiti nei metadati di coda hello. Tuttavia, è possibile rinnovare il blocco di hello dal chiamante hello [RenewLock](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.renewlock#Microsoft_ServiceBus_Messaging_BrokeredMessage_RenewLock) metodo.
* timeout massimo Hello per un blocco di operazione di ricezione nelle code del Bus di servizio è di 24 giorni. I timeout basati su REST, tuttavia, hanno un valore massimo di 55 secondi.
* Invio in batch sul lato client fornite dal Bus di servizio consente un toobatch client coda più messaggi in una singola operazione di invio. L'invio in batch è disponibile solo per le operazioni di invio asincrone.
* Funzionalità, ad esempio limite massimo di 200 TB hello di code di archiviazione (più quando gli account vengono virtualizzati) e un numero illimitato rendono la piattaforma ideale per i provider SaaS.
* Le code di archiviazione forniscono un meccanismo di controllo di accesso delegato flessibile ed efficiente.

## <a name="advanced-capabilities"></a>Funzionalità avanzate
Questa sezione confronta le funzionalità avanzate fornite dalle code di archiviazione e dalle code del bus di servizio.

| Criteri di confronto | Code di archiviazione | Code del bus di servizio |
| --- | --- | --- |
| Recapito pianificato |**Sì** |**Sì** |
| Mancato recapito automatico dei messaggi |**No** |**Sì** |
| Valore TTL di accodamento aumentato |**Sì**<br/><br/>(tramite aggiornamento sul posto del timeout di visibilità) |**Sì**<br/><br/>(specificato tramite una funzione API dedicata) |
| Supporto messaggi non elaborabili |**Sì** |**Sì** |
| Aggiornamento sul posto |**Sì** |**Sì** |
| Log delle transazioni sul lato server |**Sì** |**No** |
| Metriche di archiviazione |**Sì**<br/><br/>**Metrica al minuto**: specifica metriche in tempo reale relative a disponibilità, TPS, numero di chiamate API, numero di errori e molto altro, aggregate per minuto e segnalate entro pochi minuti rispetto agli eventi in fase di produzione. Per altre informazioni, vedere [About Storage Analytics Metrics](/rest/api/storageservices/fileservices/About-Storage-Analytics-Metrics) (Informazioni sulle metriche di analisi dell'archiviazione). |**Sì**<br/><br/>(query in blocco tramite chiamate a [GetQueues](/dotnet/api/microsoft.servicebus.namespacemanager.getqueues#Microsoft_ServiceBus_NamespaceManager_GetQueues)) |
| Gestione dello stato |**No** |**Sì**<br/><br/>[Microsoft.ServiceBus.Messaging.EntityStatus.Active](/dotnet/api/microsoft.servicebus.messaging.entitystatus.active), [Microsoft.ServiceBus.Messaging.EntityStatus.Disabled](/dotnet/api/microsoft.servicebus.messaging.entitystatus.disabled), [Microsoft.ServiceBus.Messaging.EntityStatus.SendDisabled](/dotnet/api/microsoft.servicebus.messaging.entitystatus.senddisabled), [Microsoft.ServiceBus.Messaging.EntityStatus.ReceiveDisabled](/dotnet/api/microsoft.servicebus.messaging.entitystatus.receivedisabled) |
| Inoltro automatico dei messaggi |**No** |**Sì** |
| Funzione di eliminazione della coda |**Sì** |**No** |
| Gruppi di messaggi |**No** |**Sì**<br/><br/>(tramite l'utilizzo di hello di sessioni di messaggistica) |
| Stato dell'applicazione per gruppo di messaggi |**No** |**Sì** |
| Rilevamento duplicati |**No** |**Sì**<br/><br/>(configurabile sul lato mittente hello) |
| Esplorazione di gruppi di messaggi |**No** |**Sì** |
| Recupero delle sessioni di messaggistica per ID |**No** |**Sì** |

### <a name="additional-information"></a>Informazioni aggiuntive
* Entrambe le tecnologie di accodamento consentono un toobe messaggio pianificata per il recapito in un secondo momento.
* Inoltro automatico consente a migliaia di code tooauto in avanti i relativi messaggi tooa singola coda, da quale applicazione ricevente hello utilizza messaggio hello. È possibile utilizzare questo meccanismo tooachieve sicurezza, il flusso di controllo e isolare archiviazione tra ogni server di pubblicazione del messaggio.
* Le code di archiviazione offrono supporto per l'aggiornamento del contenuto del messaggio. È possibile utilizzare questa funzionalità per rendere persistenti le informazioni sullo stato e gli aggiornamenti di stato di avanzamento incrementale nel messaggio hello in modo che possa essere elaborato da hello ultimo checkpoint noto anziché dall'inizio. Con le code di Service Bus, è possibile abilitare hello stesso scenario tramite l'utilizzo di hello di sessioni di messaggistica. Le sessioni consentono di toosave e recuperare lo stato di elaborazione dell'applicazione hello (tramite [SetState](/dotnet/api/microsoft.servicebus.messaging.messagesession.setstate#Microsoft_ServiceBus_Messaging_MessageSession_SetState_System_IO_Stream_) e [GetState](/dotnet/api/microsoft.servicebus.messaging.messagesession.getstate#Microsoft_ServiceBus_Messaging_MessageSession_GetState)).
* [Il recapito](service-bus-dead-letter-queues.md), che è supportata dalle code di Service Bus, solo può essere utile per isolare i messaggi che non possono essere elaborati correttamente dall'applicazione ricevente hello o quando i messaggi non recapitati a causa di tooan scaduto proprietà di (durata TTL) Time-to-live. il valore di durata (TTL) Hello specifica quanto tempo il messaggio rimane nella coda di hello. Con il Bus di servizio, il messaggio hello sarà spostato tooa coda speciale denominata coda $DeadLetterQueue scadere del periodo TTL hello.
* i messaggi "poison" toofind nelle code di archiviazione, quando un'applicazione hello messaggio di annullamento dell'accodamento esamina hello  **[DequeueCount](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueuemessage.dequeuecount.aspx)**  proprietà del messaggio hello. Se **DequeueCount** è maggiore di una determinata soglia, un'applicazione hello Sposta hello messaggio tooan definito dall'applicazione "" non recapitabili.
* Le code di archiviazione consentono di tooobtain un log dettagliato di tutte le transazioni hello eseguite hello coda, nonché le metriche aggregate. Queste opzioni sono entrambe utili per il debug e per comprendere in che modo l'applicazione usa le code di archiviazione. Sono inoltre utili per l'ottimizzazione delle prestazioni dell'applicazione e riducendo i costi di hello di utilizzo delle code.
* il concetto di Hello di "sessioni di messaggistica" supportato dal Bus di servizio consente i messaggi che appartengono tooa determinati toobe gruppo logico associato a un ricevitore specificato, che a sua volta crea un'affinità di sessione simili tra i messaggi e i rispettivi ricevitori. È possibile abilitare questa funzionalità avanzata in Bus di servizio per l'impostazione hello [SessionID](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.sessionid#Microsoft_ServiceBus_Messaging_BrokeredMessage_SessionId) proprietà in un messaggio. Ricevitori possono quindi restare in attesa su un ID di sessione specifico e ricevere messaggi che condividono hello specificato identificatore di sessione.
* Hello funzionalità di rilevamento di duplicazione supportata dalle code del Bus di servizio automaticamente rimuove i messaggi duplicati inviati tooa coda o argomento, in base al valore di hello di hello [MessageId](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.messageid#Microsoft_ServiceBus_Messaging_BrokeredMessage_MessageId) proprietà.

## <a name="capacity-and-quotas"></a>Capacità e quote
Questa sezione vengono confrontate le code di archiviazione e le code del Bus di servizio dalla prospettiva di hello di [capacità e alle quote](service-bus-quotas.md) che possono applicare.

| Criteri di confronto | Code di archiviazione | Code del bus di servizio |
| --- | --- | --- |
| Dimensioni massime della coda |**500 TB**<br/><br/>(limitata tooa [singolo capacità di account di archiviazione](../storage/common/storage-introduction.md#queue-storage)) |**1 GB too80 GB**<br/><br/>(definite al momento della creazione di una coda e [abilitazione del partizionamento](service-bus-partitioning.md) – vedere la sezione "Informazioni aggiuntive" hello) |
| Dimensioni massime del messaggio |**64 KB**<br/><br/>(48 KB quando si usa una codifica **Base64**)<br/><br/>Azure supporta messaggi di grandi dimensioni grazie alla combinazione di code e BLOB, a quel punto è possibile accodare backup too200GB per un singolo elemento. |**256 KB** o **1 MB**<br/><br/>(inclusi l'intestazione e il corpo, dimensioni massime dell'intestazione: 64 KB).<br/><br/>Dipende hello [livello di servizio](service-bus-premium-messaging.md). |
| Durata TTL massima del messaggio |**7 giorni** |**`TimeSpan.Max`** |
| Numero massimo di code |**Illimitato** |**10.000**<br/><br/>(per spazio dei nomi del servizio, può essere aumentato) |
| Numero massimo di client concorrenti |**Illimitato** |**Illimitato**<br/><br/>(limite di 100 connessioni simultanee solo la comunicazione basata sul protocollo tooTCP) |

### <a name="additional-information"></a>Informazioni aggiuntive
* Bus di servizio impone l'applicazione dei limiti di dimensione della coda. dimensioni massime della coda Hello viene specificata al momento della creazione della coda di hello e possono avere un valore compreso tra 1 e 80 GB. Se viene raggiunto valore delle dimensioni coda hello impostato al momento della creazione della coda di hello, altri messaggi in arrivo verranno rifiutati e verrà restituita un'eccezione dalla chiamata di codice hello. Per altre informazioni sulle quote nel bus di servizio, vedere [Quote del bus di servizio](service-bus-quotas.md).
* In hello [livello Standard](service-bus-premium-messaging.md), è possibile creare le code del Bus di servizio in dimensioni di 1, 2, 3, 4 o 5 GB (valore predefinito di hello è 1 GB). Nel livello Premium hello, è possibile creare code too80 GB di dimensioni. Nello Standard livello, con il partizionamento abilitato (ovvero di hello (impostazione predefinita), Bus di servizio crea 16 partizioni per ogni GB specificato. Di conseguenza, se si crea una coda è di 5 GB di dimensioni, con 16 partizioni le dimensioni massime della coda di hello diventa (5 * 16) = 80 GB. È possibile visualizzare dimensioni massime di hello della coda o argomento partizionato esaminando relativa voce nel hello [portale di Azure][Azure portal]. Nel livello Premium hello, vengono create solo 2 partizioni per ogni coda.
* Con le code di archiviazione, se hello contenuto del messaggio non è XML-safe, quindi deve essere **Base64** codificato. Se si **Base64**-codificare il messaggio hello, può essere payload dell'utente hello too48 KB, anziché 64 KB.
* Con le code del bus di servizio, ogni messaggio archiviato in una coda è costituito da due parti: un'intestazione e un corpo. dimensione totale di Hello del messaggio non può superare hello massima del messaggio dimensioni supportate dal livello di servizio hello.
* Quando i client comunicano con le code del Bus di servizio tramite il protocollo TCP hello, numero massimo di hello di coda di Service Bus singola tooa di connessioni simultanee è too100 limitato. Questo numero è condiviso tra mittenti e destinatari. Se viene raggiunta questa quota, le successive richieste per le connessioni aggiuntive verranno rifiutate e verrà restituita un'eccezione dalla chiamata di codice hello. Questo limite non viene imposto sul client che si connettono le code di toohello utilizzando API basata su REST.
* Se sono necessari più di 10.000 code in un singolo spazio dei nomi Service Bus, è possibile contattare il team di supporto tecnico di Azure hello e richiedere un aumento. tooscale più di 10.000 code con il Bus di servizio, è inoltre possibile creare ulteriori spazi dei nomi utilizzando hello [portale di Azure][Azure portal].

## <a name="management-and-operations"></a>Gestione e operazioni
Questa sezione vengono confrontate le funzionalità di gestione hello fornite dalle code di archiviazione e le code del Bus di servizio.

| Criteri di confronto | Code di archiviazione | Code del bus di servizio |
| --- | --- | --- |
| Protocollo di gestione |**REST su HTTP/HTTPS** |**REST su HTTPS** |
| Protocollo runtime |**REST su HTTP/HTTPS** |**REST su HTTPS**<br/><br/>**Standard AMQP 1.0 (TCP con TLS)** |
| API .NET |**Sì**<br/><br/>(API client di archiviazione .NET) |**Sì**<br/><br/>(API del bus di servizio .NET) |
| C++ nativo |**Sì** |**Sì** |
| API Java |**Sì** |**Sì** |
| API PHP |**Sì** |**Sì** |
| API Node.js |**Sì** |**Sì** |
| Supporto metadati arbitrario |**Sì** |**No** |
| Regole di denominazione delle code |**Backup too63 caratteri**<br/><br/>(le lettere del nome di una coda devono essere minuscole). |**Backup too260 caratteri**<br/><br/>(i percorsi e i nomi di code non fanno distinzione tra maiuscole e minuscole). |
| Funzione di recupero della lunghezza della coda |**Sì**<br/><br/>(Valore indicativo se i messaggi scadono oltre hello TTL senza essere eliminati.) |**Sì**<br/><br/>(Valore esatto e temporizzato). |
| Funzione di visualizzazione |**Sì** |**Sì** |

### <a name="additional-information"></a>Informazioni aggiuntive
* Le code di archiviazione forniscono supporto per gli attributi arbitrari che possono essere applicati toohello descrizione della coda, sotto forma di hello di coppie nome/valore.
* Entrambe le tecnologie di coda offrono hello possibilità toopeek un messaggio senza toolock it, che può essere utile quando si implementa uno strumento di esplorazione di coda.
* Hello .NET del Bus di servizio negoziata messaggistica API sfruttano full duplex connessioni TCP per migliorare le prestazioni quando confrontati tooREST su HTTP e supportano un protocollo standard AMQP 1.0 hello.
* I nomi delle code di archiviazione possono avere una lunghezza compresa tra 3 e 63 caratteri e contenere lettere minuscole, numeri e trattini. Per altre informazioni, vedere [Naming Queues and Metadata](/rest/api/storageservices/fileservices/Naming-Queues-and-Metadata) (Denominazione di code e metadati).
* I nomi delle code Service Bus sono backup too260 caratteri e dispone di regole di denominazione meno restrittive. I nomi delle code del bus di servizio possono contenere lettere, numeri, punti, trattini e caratteri di sottolineatura.

## <a name="authentication-and-authorization"></a>Autenticazione e autorizzazione
In questa sezione descrive le funzionalità di autenticazione e autorizzazione hello supportate dalle code di archiviazione e le code del Bus di servizio.

| Criteri di confronto | Code di archiviazione | Code del bus di servizio |
| --- | --- | --- |
| Autenticazione |**Chiave simmetrica** |**Chiave simmetrica** |
| Modello di protezione |Accesso delegato tramite token di firma di accesso condiviso. |SAS |
| Federazione del provider di identità |**No** |**Sì** |

### <a name="additional-information"></a>Informazioni aggiuntive
* Tooeither ogni richiesta di tecnologie di Accodamento messaggi hello devono essere autenticate. Le code pubbliche con accesso anonimo non sono supportate. L'uso di [SAS](service-bus-sas.md) consente di ovviare a questo inconveniente tramite la pubblicazione di una firma SAS di sola scrittura, di sola lettura o anche di accesso completo.
* Hello schema di autenticazione fornito dall'archiviazione code prevede l'uso di hello di una chiave simmetrica, ovvero un codice HMAC (hash basato su messaggio Authentication Code) calcolato con l'algoritmo SHA-256 hello e codificato come un **Base64** stringa. Per ulteriori informazioni sul protocollo rispettivi hello, vedere [l'autenticazione per i servizi di archiviazione Azure hello](/rest/api/storageservices/fileservices/Authentication-for-the-Azure-Storage-Services). Le code del bus di servizio supportano un modello simile mediante l'uso di chiavi simmetriche. Per altre informazioni, vedere [Autenticazione della firma di accesso condiviso con il bus di servizio](service-bus-sas.md).

## <a name="conclusion"></a>Conclusioni
Acquisendo una comprensione più approfondita delle tecnologie di hello due, saranno in grado di toomake una decisione più oculata in cui accodare toouse tecnologia e quando. Hello decisione su quando le code di archiviazione toouse o Service Bus Accoda chiaramente dipende da numerosi fattori. Queste possono dipendere soprattutto hello singole esigenze dell'applicazione e la relativa architettura. Se l'applicazione utilizza già le funzionalità di base hello di Microsoft Azure, è preferibile toochoose le code di archiviazione, soprattutto se si richiede la comunicazione di base e la messaggistica tra servizi o alle code necessità che possono essere maggiori di 80 GB di dimensione.

Poiché offrono numerose funzionalità avanzate quali sessioni, transazioni rilevamento duplicati, mancato recapito automatico dei messaggi e funzionalità di pubblicazione e sottoscrizione permanente, le code del bus di servizio possono rappresentare la soluzione migliore quando si sviluppa un'applicazione ibrida o se l'applicazione in uso richiede comunque tali funzionalità.

## <a name="next-steps"></a>Passaggi successivi
Hello gli articoli seguenti fornisce ulteriori linee guida e informazioni sull'utilizzo di code di archiviazione o le code del Bus di servizio.

* [Introduzione alle code del bus di servizio](service-bus-dotnet-get-started-with-queues.md)
* [Come tooUse hello servizio di archiviazione code](../storage/queues/storage-dotnet-how-to-use-queues.md)
* [Procedure consigliate per il miglioramento delle prestazioni tramite la messaggistica negoziata del bus di servizio](service-bus-performance-improvements.md)
* [Introduzione alle code e agli argomenti del bus di servizio di Azure (post di blog)](http://www.code-magazine.com/article.aspx?quickid=1112041)
* [Hello tooService Guida per gli sviluppatori Bus](http://www.cloudcasts.net/devguide/Default.aspx?id=11030)
* [Utilizzo del servizio di Accodamento messaggi hello in Azure](http://www.developerfusion.com/article/120197/using-the-queuing-service-in-windows-azure/)

[Azure portal]: https://portal.azure.com

