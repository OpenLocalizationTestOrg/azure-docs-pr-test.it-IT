---
title: aaaAMQP 1.0 in Azure Service Bus e hub di eventi Guida protocollo | Documenti Microsoft
description: Protocollo Guida tooexpressions e una descrizione di AMQP 1.0 in Azure Service Bus e hub di eventi
services: service-bus-messaging,event-hubs
documentationcenter: .net
author: clemensv
manager: timlt
editor: 
ms.assetid: d2d3d540-8760-426a-ad10-d5128ce0ae24
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/07/2017
ms.author: clemensv;hillaryc;sethm
ms.openlocfilehash: 882ce0fc84af11d9f61bc95dc3e4db0b67b2b020
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# Guida al protocollo AMQP 1.0 nel bus di servizio e in Hub eventi di Azure

Hello Advanced Message Queuing protocollo 1.0 è un protocollo di trasferimento e framing standardizzato per in modo asincrono, in modo sicuro e affidabile il trasferimento dei messaggi tra due parti. È hello principale protocollo di messaggistica del Bus di servizio di Azure e hub di eventi di Azure. Entrambi i servizi supportano anche HTTPS. protocollo SBMP proprietario Hello che è anche supportato è obsoleta a favore AMQP.

AMQP 1.0 è risultato hello di collaborazione di settore ampia che riunire middleware fornitori, ad esempio Microsoft e Red Hat, con molti utenti middleware messaggistica, ad esempio JP Morgan Chase che rappresenta il settore di servizi finanziari hello. forum di standardizzazione tecniche Hello per le specifiche del protocollo e l'estensione AMQP hello è OASIS, e ha ottenuto l'approvazione formale come standard internazionale come standard ISO/IEC 19494.

## Obiettivi

In questo articolo vengono riepilogati i concetti di base hello della specifica di messaggistica hello AMQP 1.0 insieme a un set ridotto di bozze di specifiche di estensione che sono attualmente finalizzato in comitato tecnico di OASIS AMQP hello brevemente e illustra il funzionamento di Azure Service Bus implementa e si basa su queste specifiche.

obiettivo di Hello è per tutti gli sviluppatori che utilizzano qualsiasi stack client AMQP 1.0 esistente in qualsiasi toobe di piattaforma in grado di toointeract con Azure Service Bus tramite AMQP 1.0.

Gli stack generici AMQP 1.0 comuni, ad esempio Apache Proton o AMQP.NET Lite, implementano già tutti i gesti principali di AMQP 1.0. I movimenti fondamentali talvolta vengono eseguito il wrapping con un'API di livello superiore; Proton di Apache offre anche due, hello imperativo API Messenger e hello reattivo reattore API.

In hello seguente discussione, si presuppone che Gestione hello di gestione di collegamenti e hello dei trasferimenti di frame e il controllo di flusso, sessioni e connessioni AMQP vengono gestite dallo stack rispettivi hello (ad esempio Apache Proton-C) e non richiedono quantità eventuali specifiche attenzione da parte di sviluppatori di applicazioni. Si supponga di astrattamente di esistenza hello di alcune API primitive quali tooconnect possibilità hello e toocreate qualche forma di *mittente* e *ricevitore* astrazione oggetti, quindi la forma della `send()`e `receive()` operazioni, rispettivamente.

Durante l'analisi delle funzionalità avanzate del bus di servizio di Azure, ad esempio l'esplorazione dei messaggi o la gestione delle sessioni, questi aspetti vengono illustrati dal punto di vista di AMQP, ma anche dal punto di vista della pseudo-implementazione a più livelli sopra questa presupposta astrazione di API.

## Informazioni su AMQP

AMQP è un protocollo di frame e di trasferimento. Un protocollo di frame fornisce una struttura per i flussi di dati in ogni direzione di una connessione di rete. struttura Hello fornisce limite per i blocchi distinti di dati, denominato *frame*, toobe scambiati tra parti hello connesso. funzionalità di trasferimento Hello assicurarsi che entrambe le parti in comunicazione possono stabilire una comprensione condivisa su quando i trasferimenti devono essere considerati completato e quando i frame devono essere trasferiti.

A differenza delle versioni precedenti scaduti bozza prodotte dal gruppo di lavoro AMQP hello che sono ancora in uso da alcuni gestori di messaggi, del gruppo di lavoro hello finale e standard AMQP 1.0 al protocollo prescrivono presenza hello di qualsiasi topologia specifico o un gestore di messaggi per le entità all'interno di un gestore di messaggi.

Hello protocollo può essere usato per la comunicazione peer-to-peer simmetrica, per l'interazione con i gestori di messaggi che supportano il code e le entità di pubblicazione/sottoscrizione, come Azure Service Bus. Può anche essere utilizzato per l'interazione con l'infrastruttura di messaggistica in modelli di interazione hello sono diverse dalle code regolari, come accade hello con hub eventi di Azure. Un Hub eventi funge da una coda quando gli eventi vengono inviati tooit, ma più agisce come un servizio di archiviazione seriale quando gli eventi vengono letti da esso. è piuttosto simile a un'unità nastro. client Hello preleva un offset nel flusso di dati disponibili hello e viene quindi servito tutti gli eventi da tale offset toohello più recente disponibile.

Hello protocollo AMQP 1.0 è progettato toobe estensibile, consentendo specifiche tooenhance ulteriormente le funzionalità. specifiche estensione tre Hello illustrate in questo documento illustrare questo concetto. Per la comunicazione tramite HTTPS/WebSocket infrastruttura configurazione delle porte TCP AMQP native hello in cui potrebbe essere difficile, specifica un'associazione definisce come toolayer AMQP tramite WebSockets. Per l'interazione con l'infrastruttura di messaggistica hello in una richiesta/risposta modo per scopi di gestione o funzionalità tooprovide avanzate, specifiche di gestione di hello AMQP definisce le primitive di hello necessaria l'interazione di base. Per l'integrazione del modello di autorizzazione federato, hello specifiche di sicurezza basato su attestazioni AMQP definisce come tooassociate e rinnovare il token di autorizzazione associato ai collegamenti.

## Scenari AMQP di base

Questa sezione viene illustrato l'utilizzo di base hello del protocollo AMQP 1.0 con Azure Service Bus, che include la creazione di connessioni, sessioni e i collegamenti e il trasferimento di messaggi tooand dalle entità di Service Bus quali code, argomenti e sottoscrizioni.

Hello più rilevanti origine toolearn sull'uso di AMQP è specifica di hello AMQP 1.0, ma è stata scritta specifica hello implementazione Guida tooprecisely e non il protocollo di hello tooteach. Questa sezione è incentrata sull'introduzione della terminologia necessaria per descrivere l'uso di AMQP 1.0 da parte del bus di servizio. Per una più completa tooAMQP introduzione, nonché una descrizione più ampia di AMQP 1.0, è possibile esaminare [questo corso video][this video course].

### Connessioni e sessioni

AMQP chiamate hello comunicazione programmi *contenitori*; tali contengono *nodi*che hello comunicano le entità all'interno di tali contenitori. Una coda può essere un nodo di questo tipo. Consente di AMQP per il demultiplexing, pertanto una singola connessione può essere utilizzata per tutti i percorsi di comunicazione tra nodi. ad esempio, un'applicazione client può ricevere simultaneamente da una coda e coda di invio tooanother su hello stessa connessione di rete.

![][1]

connessione di rete Hello è ancorata pertanto nel contenitore hello. Viene avviato dal contenitore hello nel ruolo di client hello effettua un contenitore tooa connessione di socket TCP in uscita nel ruolo di ricevitore hello, che rimane in ascolto di e accetta le connessioni TCP in ingresso. l'handshake della connessione Hello include la negoziazione della versione del protocollo hello, dichiarazione o negoziazione Usa hello Transport Level Security (TLS/SSL) e un handshake di autenticazione/autorizzazione nell'ambito di connessione hello basato su SASL.

Service Bus di Azure richiede l'uso di hello di TLS in qualsiasi momento. Supporta le connessioni sulla porta TCP 5671, quale hello connessione TCP prima sovrapposta con TLS prima di immettere l'handshake del protocollo AMQP di hello e supporta anche connessioni sulla porta TCP 5672 in base al quale il server hello offre immediatamente un aggiornamento obbligatorio di Utilizza modello previsto AMQP hello tooTLS di connessione. associazione di WebSocket AMQP Hello crea un tunnel sulla porta TCP 443 che viene quindi 5671 connessioni tooAMQP equivalente.

Dopo aver impostato la connessione hello e TLS, Bus di servizio sono disponibili due opzioni di meccanismo SASL:

* NORMALE SASL viene comunemente utilizzato per il passaggio di server di tooa credenziali nome utente e password. Il bus di servizio non ha account, ma [regole di sicurezza di accesso condiviso](service-bus-sas.md) denominate, che conferiscono diritti e sono associate a una chiave. nome Hello di una regola viene utilizzato come nome utente hello e una chiave di hello (come testo con codifica base64) viene usato come password hello. diritti di Hello associati hello scelto regola controllano le operazioni di hello consentite sulla connessione hello.
* SASL anonimo viene utilizzato per ignorare l'autorizzazione SASL quando il client di hello desidera toouse hello sicurezza basato su attestazioni (CBS) modello è descritto più avanti. Con questa opzione, una connessione client è possibile stabilire in modo anonimo per un breve periodo di tempo durante cui hello client può interagire solo con endpoint CBS hello e deve completare l'handshake CBS hello.

Dopo aver stabilita la connessione di trasporto hello, contenitori hello ognuno dichiarano la dimensione massima hello sono disposti toohandle e dopo un timeout di inattività viene unilateralmente verrà disconnesso se è presente alcuna attività per la connessione hello.

I contenitori dichiarano anche il numero di canali simultanei supportati. Un canale è un percorso di trasferimento unidirezionale in uscita, virtuale su connessione hello. Una sessione accetta un canale di ciascun percorso di comunicazione hello contenitori interconnesse tooform un bidirezionale.

Le sessioni hanno un modello di controllo di flusso basato sulla finestra. Quando viene creata una sessione, ogni parte dichiara il numero di frame è tooaccept disposti nella relativa finestra di ricezione. Come trasferire hello parti exchange frame, frame riempimento che finestra e i trasferimenti arrestata quando finestra hello è pieno e fino a quando la finestra hello reimpostata o estesa tramite hello *flusso performative* (*performative*è hello AMQP termine per i movimenti a livello di protocollo scambiati tra parti hello due).

Questo modello basato su window è quasi equivalente toohello concetto TCP del controllo di flusso basato su window, ma a livello di sessione hello all'interno di socket hello. Hello concetto del protocollo di consentire a più sessioni simultanee esiste in modo che il traffico di priorità alta potrebbe rushed oltre limitato normale traffico, come in una corsia express autostrada.

Il bus di servizio di Azure usa attualmente esattamente una sessione per ogni connessione. Dimensione frame Bus di servizio massima Hello è 262.144 byte (256 KB) per Bus di servizio Standard e hub di eventi. È pari a 1.048.576 (1 MB) per il bus di servizio Premium. Bus di servizio non impone alcun particolare windows limitazione a livello di sessione, ma reimposta hello finestra regolarmente come parte del controllo di flusso a livello di collegamenti (vedere [hello nella sezione successiva](#links)).

Le connessioni, le sessioni e i canali sono temporanei. Se la connessione sottostante hello viene compresso, le connessioni, devono essere ristabilite tunnel TLS, il contesto di autorizzazione SASL e sessioni.

### Collegamenti

AMQP trasferisce i messaggi sui collegamenti. Un collegamento è un percorso di comunicazione creato in una sessione che consente il trasferimento dei messaggi in una direzione; negoziazione di stato di trasferimento Hello è su collegamento hello e bidirezionali tra parti hello connesso.

![][2]

È possibile creare collegamenti da un contenitore in qualsiasi momento e in una sessione esistente, che si differenziano dai molti altri protocolli, tra HTTP e MQTT, dove avvio hello di trasferimenti e il percorso di trasferimento è un privilegio esclusivo di creazione di parti di hello AMQP connessione socket Hello.

contenitore di avvio di collegamento Hello viene richiesto un collegamento hello opposto tooaccept contenitore e sceglie un ruolo del mittente o ricevitore. Pertanto, contenitore può avviare la creazione unidirezionale o i percorsi di comunicazione bidirezionale, con quest'ultimo hello modellata come coppie di collegamenti.

I collegamenti sono denominati e sono associati ai nodi. Come indicato nella inizio hello, i nodi sono hello comunicazione entità all'interno di un contenitore.

Bus di servizio, un nodo è una coda secondaria dei messaggi non recapitabili di una coda o sottoscrizione, un argomento, una sottoscrizione o coda tooa direttamente equivalente. nome del nodo Hello utilizzato in AMQP è pertanto hello relativo nome entità hello all'interno dello spazio dei nomi di hello Bus di servizio. Se una coda è denominata **myqueue**, tale nome corrisponde anche al nome del nodo AMQP. Una sottoscrizione dell'argomento segue convenzione API HTTP hello in base che verrà ordinata in una raccolta di risorse "sottoscrizioni" e di conseguenza, una sottoscrizione **sub** o un argomento **mytopic** con nome di nodo hello AMQP **sottoscrizioni/mytopic/sub**.

client in connessione Hello è anche necessario toouse un nome di nodo locale per la creazione di collegamenti Bus di servizio non è ricchi di indicazioni sui tali nomi di nodo e non interpretati. Stack client AMQP 1.0 in genere utilizza una tooassure di schema che questi nomi di nodo temporaneo siano univoci nell'ambito di hello del client hello.

### Trasferimenti

Dopo la creazione di un collegamento, è possibile trasferire i messaggi su tale collegamento. In AMQP, il trasferimento viene eseguito con un movimento protocollo esplicita (hello *trasferimento* performative) che consente di spostare un messaggio dal mittente tooreceiver su un collegamento. Un trasferimento è completato quando si è "compensato", vale a dire che entrambe le parti hanno stabilito una comprensione condivisa risultato hello di trasferimento.

![][3]

Nel caso più semplice di hello, mittente hello possibile toosend messaggi "pre-compensati", vale a dire che non è interessato risultato hello client hello e ricevitore hello non fornisce alcun commenti e suggerimenti sul risultato di hello dell'operazione di hello. Questa modalità è supportata dal Bus di servizio a livello di protocollo AMQP hello, ma non esposte in una qualsiasi delle API client hello.

Hello case regolare è che i messaggi vengono inviati liquidati e ricevitore hello indica quindi accettazione o rifiuto utilizzando hello *disposition* performative. Rifiuto si verifica quando il ricevitore hello non può accettare messaggi hello per qualsiasi motivo e il messaggio di rifiuto hello contiene informazioni sul motivo hello, che è una struttura di errore definita da AMQP. Se i messaggi vengono rifiutati a causa di errori toointernal all'interno di Service Bus, il servizio di hello restituisce informazioni aggiuntive all'interno di tale struttura che può essere utilizzato per fornire diagnostica personale toosupport hint se la presentazione di richieste di supporto. Informazioni dettagliate sugli errori sono disponibili più avanti.

Una forma speciale di rifiuto è hello *rilasciato* stato, che non indica il destinatario hello dispone di alcun trasferimento toohello obiezione tecnico, ma anche con la consueta risoluzione alcun interesse non hello trasferimento. Case esistenza, ad esempio, quando un messaggio viene recapitato tooa client del Bus di servizio e client hello sceglie troppo "abbandonare" messaggio hello perché non è possibile eseguire lavoro hello risultanti dall'elaborazione del messaggio hello; recapito dei messaggi Hello stesso non è valido. Una variante di tale stato è hello *modificato* stato che consente di messaggio toohello modifiche man mano che viene rilasciata. Questo stato non viene attualmente usato dal bus di servizio.

Hello protocollo AMQP 1.0 definisce una disposizione ulteriore stato denominato *ricevuto*, in particolare che consente di ripristino di collegamento toohandle. Ripristino di collegamento consente di ricostituire stato hello di un collegamento e in sospeso recapiti su una nuova connessione e di sessione, quando la connessione precedente hello e sessione verranno perse.

Bus di servizio non supporta il ripristino di collegamento; Se il client hello perde hello connessione tooService Bus con un messaggio non liquidato trasferire in sospeso, il trasferimento dei messaggi viene perso e hello client devono riconnettersi, ristabilire il collegamento hello e ripetere il trasferimento di hello.

Di conseguenza, Bus di servizio e hub di eventi "at least once" supporta i trasferimenti in mittente hello può essere garantita per il messaggio hello che sia stata archiviata e accettata, ma non supportano "una sola volta" i trasferimenti di hello livello AMQP, in cui il sistema hello tenta toorecover collegamento Hello e continuare la duplicazione toonegotiate hello recapito stato tooavoid di trasferimento messaggi hello.

Invia toocompensate per possibile duplicato, Bus di servizio supporta il rilevamento dei duplicati come funzionalità facoltativa su code e argomenti. I record di rilevamento dei duplicati hello gli ID di messaggio di tutti i messaggi in arrivo durante un intervallo di tempo definito dall'utente, quindi automaticamente Elimina che tutti i messaggi inviati con hello stessi ID di messaggio durante la stessa finestra.

### Controllo di flusso

Inoltre il controllo di flusso a livello di sessione toohello modello descritto in precedenza, ogni collegamento dispone di un proprio modello di controllo di flusso. Controllo di flusso a livello di sessione protegge contenitore hello dalla presenza di troppi frame in toohandle una volta, il controllo di flusso a livello di collegamenti inserisce un'applicazione hello responsabile quanti messaggi che si desiderano toohandle da un collegamento e quando.

![][4]

Su un collegamento, i trasferimenti possono accadere solo quando hello mittente disponga di sufficiente *collegamento credito*. Il credito di collegamento è un contatore impostato da un ricevitore di hello utilizzando hello *flusso* performative, ovvero con ambito tooa collegamento. Quando il mittente hello viene assegnato il credito di collegamento, tenta toouse backup la carta di credito per il recapito dei messaggi. Ogni decrementa di recapito messaggio hello credito rimanente di collegamento da 1. Quando si esaurisca credito collegamento hello, arrestare recapiti.

Quando il Bus di servizio è nel ruolo di ricevitore hello, mittente hello immediatamente fornisce con carta di credito collegamento quantità, in modo che i messaggi possono essere inviati immediatamente. Come viene usato il credito di collegamento, Bus di servizio invia occasionalmente un *flusso* toohello performative mittente tooupdate hello collegamento saldo.

Nel ruolo di mittente hello, Bus di servizio invia messaggi toouse di carta di credito qualsiasi collegamento in sospeso.

Una chiamata di "ricezione" a livello di hello API si traduce in un *flusso* performative inviati tooService utilizza Bus dal client hello e Bus di servizio che prima del credito da prendere hello disponibili, sblocco del messaggio dalla coda di hello, blocco, e il trasferimento. Se sono presenti messaggi disponibili per il recapito, eventuali crediti in sospeso da qualsiasi collegamento stabilire con particolare entità rimane registrato nell'ordine di arrivo, e i messaggi sono bloccati e trasferiti man mano che diventano disponibili, toouse eventuali crediti in sospeso.

blocco Hello in un messaggio viene rilasciato quando il trasferimento di hello è compensato in uno stato terminale hello *accettato*, *rifiutato*, o *rilasciato*. messaggio Hello viene rimosso dal Bus di servizio quando è stato terminale hello *accettato*. E continua dunque nel Bus di servizio e viene recapitato ricevitore successivo toohello quando il trasferimento di hello raggiunge uno qualsiasi dei hello altri Stati. Bus di servizio messaggio hello viene spostato automaticamente nella coda di messaggi non recapitabili dell'entità di hello quando raggiunge hello numero massimo di recapiti consentito per l'entità hello scadenza toorepeated rifiuti o di versioni.

Anche se hello API del Bus di servizio non esporre direttamente tale opzione oggi, un client di protocollo AMQP di livello inferiore è possibile utilizzare hello collegamento credito tooturn hello "pull-style" interazione tra i modelli di rilascio di un'unità di carta di credito per ogni richiesta di ricezione in un modello "push-style" mediante l'emissione di un numero elevato di collegamento crediti e ricevere i messaggi man mano che diventano disponibili senza ulteriori interazioni. Push è supportato tramite hello [MessagingFactory.PrefetchCount](/dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_PrefetchCount) o [MessageReceiver.PrefetchCount](/dotnet/api/microsoft.servicebus.messaging.messagereceiver#Microsoft_ServiceBus_Messaging_MessageReceiver_PrefetchCount) le impostazioni delle proprietà. Se diverso da zero, client AMQP hello utilizza come credito collegamento hello.

In questo contesto, è importante toounderstand che hello clock per impostare la scadenza del blocco di hello messaggio hello all'interno delle entità hello hello inizia quando hello messaggio non viene eseguito da entità hello, non quando il messaggio hello viene inserito in transito hello. Ogni volta che i client hello indica messaggi tooreceive conformità eseguendo il credito di collegamento, pertanto toobe previsto pull attivamente i messaggi attraverso la rete hello ed essere pronto toohandle li. In caso contrario il blocco di messaggio hello potrebbe essere scaduto prima che il messaggio hello anche venga recapitato. Utilizzare Hello collegamento carta di credito del controllo di flusso deve riflettere direttamente hello conformità immediato toodeal con i messaggi disponibili inviati toohello ricevitore.

In sintesi, hello sezioni seguenti forniscono una panoramica del flusso performative hello schematica durante le interazioni di API diverse. Ogni sezione descrive un'operazione logica diversa. Alcune interazioni possono essere "differite", ovvero essere eseguite solo quando richieste. Creazione di un mittente del messaggio non comporta l'interazione di una rete finché primo messaggio hello viene inviato o richiesto.

frecce Hello hello nella tabella seguente mostrano la direzione di flusso performative di hello.

#### Creare il ricevitore dei messaggi

| Client | BUS DI SERVIZIO |
| --- | --- |
| --> attach(<br/>name={nome collegamento},<br/>handle={handle numerico},<br/>role=**receiver**,<br/>source={nome entità},<br/>target={ID collegamento client}<br/>) |Client collega tooentity come ricevitore |
| Associare l'estremità del collegamento hello le risposte di Service Bus |<-- attach(<br/>name={nome collegamento},<br/>handle={handle numerico},<br/>role=**sender**,<br/>source={nome entità},<br/>target={ID collegamento client}<br/>) |

#### Creare il mittente dei messaggi

| Client | BUS DI SERVIZIO |
| --- | --- |
| --> attach(<br/>name={nome collegamento},<br/>handle={handle numerico},<br/>role=**sender**,<br/>source={ID collegamento client},<br/>target={nome entità}<br/>) |Nessuna azione |
| Nessuna azione |<-- attach(<br/>name={nome collegamento},<br/>handle={handle numerico},<br/>role=**receiver**,<br/>source={ID collegamento client},<br/>target={nome entità}<br/>) |

#### Creare il mittente dei messaggi (errore)

| Client | BUS DI SERVIZIO |
| --- | --- |
| --> attach(<br/>name={nome collegamento},<br/>handle={handle numerico},<br/>role=**sender**,<br/>source={ID collegamento client},<br/>target={nome entità}<br/>) |Nessuna azione |
| Nessuna azione |<-- attach(<br/>name={nome collegamento},<br/>handle={handle numerico},<br/>role=**receiver**,<br/>source=null,<br/>target=null<br/>)<br/><br/><-- detach(<br/>handle={handle numerico},<br/>closed=**true**,<br/>error={informazioni errore}<br/>) |

#### Chiudere il ricevitore/mittente dei messaggi

| Client | BUS DI SERVIZIO |
| --- | --- |
| --> detach(<br/>handle={handle numerico},<br/>closed=**true**<br/>) |Nessuna azione |
| Nessuna azione |<-- detach(<br/>handle={handle numerico},<br/>closed=**true**<br/>) |

#### Inviare (operazione riuscita)

| Client | BUS DI SERVIZIO |
| --- | --- |
| --> transfer(<br/>delivery-id={handle numerico},<br/>delivery-tag={handle binario},<br/>settled=**false**,,more=**false**,<br/>state=**null**,<br/>resume=**false**<br/>) |Nessuna azione |
| Nessuna azione |<-- disposition(<br/>role=receiver,<br/>first={ID consegna},<br/>last={ID consegna},<br/>settled=**true**,<br/>state=**accepted**<br/>) |

#### Inviare (errore)

| Client | BUS DI SERVIZIO |
| --- | --- |
| --> transfer(<br/>delivery-id={handle numerico},<br/>delivery-tag={handle binario},<br/>settled=**false**,,more=**false**,<br/>state=**null**,<br/>resume=**false**<br/>) |Nessuna azione |
| Nessuna azione |<-- disposition(<br/>role=receiver,<br/>first={ID consegna},<br/>last={ID consegna},<br/>settled=**true**,<br/>state=**rejected**(<br/>error={informazioni errore}<br/>)<br/>) |

#### Ricevere

| Client | BUS DI SERVIZIO |
| --- | --- |
| --> flow(<br/>link-credit=1<br/>) |Nessuna azione |
| Nessuna azione |< transfer(<br/>delivery-id={handle numerico},<br/>delivery-tag={handle binario},<br/>settled=**false**,<br/>more=**false**,<br/>state=**null**,<br/>resume=**false**<br/>) |
| --> disposition(<br/>role=**receiver**,<br/>first={ID consegna},<br/>last={ID consegna},<br/>settled=**true**,<br/>state=**accepted**<br/>) |Nessuna azione |

#### Ricevere più messaggi

| Client | BUS DI SERVIZIO |
| --- | --- |
| --> flow(<br/>link-credit=3<br/>) |Nessuna azione |
| Nessuna azione |< transfer(<br/>delivery-id={handle numerico},<br/>delivery-tag={handle binario},<br/>settled=**false**,<br/>more=**false**,<br/>state=**null**,<br/>resume=**false**<br/>) |
| Nessuna azione |< transfer(<br/>delivery-id={hanlde numerico+1},<br/>delivery-tag={handle binario},<br/>settled=**false**,<br/>more=**false**,<br/>state=**null**,<br/>resume=**false**<br/>) |
| Nessuna azione |< transfer(<br/>delivery-id={handle numerico+2},<br/>delivery-tag={handle binario},<br/>settled=**false**,<br/>more=**false**,<br/>state=**null**,<br/>resume=**false**<br/>) |
| --> disposition(<br/>role=receiver,<br/>first={ID consegna},<br/>last={ID consegna+2},<br/>settled=**true**,<br/>state=**accepted**<br/>) |Nessuna azione |

### Messaggi

Hello nelle sezioni seguenti illustrano le proprietà delle sezioni di messaggio hello standard AMQP vengono utilizzate dal Bus di servizio e il relativo mapping toohello set di API di Service Bus.

#### intestazione

| Nome campo | Utilizzo | Nome API |
| --- | --- | --- |
| durable |- |- |
| priority |- |- |
| ttl |Tempo toolive per questo messaggio |[TimeToLive](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_TimeToLive) |
| first-acquirer |- |- |
| delivery-count |- |[DeliveryCount](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_DeliveryCount) |

#### properties

| Nome campo | Utilizzo | Nome API |
| --- | --- | --- |
| message-id |Identificatore freeform definito dall'applicazione per questo messaggio. Usato per il rilevamento dei duplicati. |[MessageId](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_MessageId) |
| user-id |Identificatore dell'utente definito dall'applicazione, non interpretato dal bus di servizio. |Non è accessibile tramite hello API del Bus di servizio. |
| Anche|Identificatore della destinazione definito dall'applicazione, non interpretato dal bus di servizio. |[To](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_To) |
| subject |Identificatore dello scopo del messaggio definito dall'applicazione, non interpretato dal bus di servizio. |[Label](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Label) |
| risposta troppo|Indicatore del percorso di risposta definito dall'applicazione, non interpretato dal bus di servizio. |[ReplyTo](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_ReplyTo) |
| correlation-id |Identificatore della correlazione definito dall'applicazione, non interpretato dal bus di servizio. |[CorrelationId](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_CorrelationId) |
| content-type |Indicatore di tipo di contenuto definito dall'applicazione per corpo hello, non è stato interpretato dal Bus di servizio. |[ContentType](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_ContentType) |
| content-encoding |Definito dall'applicazione codifica contenuto indicatore per il corpo di hello, non è stato interpretato dal Bus di servizio. |Non è accessibile tramite hello API del Bus di servizio. |
| absolute-expiry-time |Dichiara in cui hello immediata assoluto messaggio scade. Viene ignorato nell'input (viene osservato il valore TTL dell'intestazione), viene considerato autorevole nell'output. |[ExpiresAtUtc](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_ExpiresAtUtc) |
| creation-time |Dichiara al quale hello ora messaggio è stato creato. Non usato dal bus di servizio |Non è accessibile tramite hello API del Bus di servizio. |
| group-id |Identificatore definito dall'applicazione per un set correlato di messaggi. Usato per le sessioni del bus di servizio. |[SessionId](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_SessionId) |
| group-sequence |Contatore numero di sequenza relativo hello del messaggio hello all'interno di una sessione di identificazione. Ignorato dal bus di servizio. |Non è accessibile tramite hello API del Bus di servizio. |
| reply-to-group-id |- |[ReplyToSessionId](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_ReplyToSessionId) |

## Funzionalità avanzate del bus di servizio

Questa sezione descrive le funzionalità avanzate di Service Bus di Azure basate su Bozza estensioni tooAMQP, attualmente sviluppate in hello comitato tecnico OASIS per AMQP. Bus di servizio implementa hello versioni più recenti di questi progetti di testi e adotta modifiche introdotte come le bozze raggiungono lo stato standard.

> [!NOTE]
> Le operazioni avanzate per la messaggistica del bus di servizio sono supportate tramite un modello di richiesta/risposta. Hello dettagli di queste operazioni sono descritti nel documento hello [AMQP 1.0 nel Bus di servizio: operazioni basate su richiesta-risposta](service-bus-amqp-request-response.md).
> 
> 

### Gestione di AMQP

Hello specifica management AMQP è hello prima delle estensioni di bozza hello descritte di seguito. Questa specifica definisce un set di livelli più alti hello protocollo AMQP movimenti di protocollo che consentono le interazioni con l'infrastruttura di messaggistica tramite AMQP hello. Specifica di Hello definisce operazioni generiche, ad esempio *creare*, *leggere*, *aggiornare*, e *eliminare* per la gestione delle entità all'interno di un infrastruttura di messaggistica e un set di operazioni di query.

Tutti i movimenti richiedono un'interazione di richiesta/risposta tra client hello e infrastruttura di messaggistica hello e pertanto vengono definiti specification hello come toomodel che l'interazione di schema nella parte superiore AMQP: hello si connette toohello messaggistica infrastruttura, avvia una sessione e quindi crea una coppia di collegamenti. Su un collegamento, funge da client hello mittente e su altri hello funge da destinatario, creando così una coppia di collegamenti che possono agire come un canale bidirezionale.

| Operazione logica | Client | Bus di servizio |
| --- | --- | --- |
| Creare un percorso di richiesta/risposta |--> attach(<br/>name={*nome collegamento*},<br/>handle={*handle numerico*},<br/>role=**sender**,<br/>source=**null**,<br/>target="myentity/$management"<br/>) |Nessuna azione |
| Creare un percorso di richiesta/risposta |Nessuna azione |\<-- attach(<br/>name={*nome collegamento*},<br/>handle={*handle numerico*},<br/>role=**receiver**,<br/>source=null,<br/>target="myentity"<br/>) |
| Creare un percorso di richiesta/risposta |--> attach(<br/>name={*nome collegamento*},<br/>handle={*handle numerico*},<br/>role=**receiver**,<br/>source="myentity/$management",<br/>target="myclient$id"<br/>) | |
| Creare un percorso di richiesta/risposta |Nessuna azione |\<-- attach(<br/>name={*nome collegamento*},<br/>handle={*handle numerico*},<br/>role=**sender**,<br/>source="myentity",<br/>target="myclient$id"<br/>) |

Quando tale coppia di collegamenti in posizione centralizzata, l'implementazione di richiesta/risposta di hello è semplice: una richiesta è un messaggio inviato tooan entità all'interno dell'infrastruttura di messaggistica hello che riconosce questo modello. Nel messaggio di richiesta, hello *risposta* campo hello *proprietà* sezione è impostata toohello *destinazione* identificatore hello collegamento su cui risposta hello toodeliver. Hello gestione entità elabora la richiesta di hello e recapita hello reply su hello collegarla cui *destinazione* identificatore corrisponde a quello indicato hello *risposta* identificatore.

modello di Hello richiede ovviamente che contenitore client hello e hello generato dal client identificatore hello risposta destinazione sono univoci per tutti i client e, per motivi di sicurezza toopredict inoltre difficile.

gli scambi di messaggi Hello utilizzato per il protocollo di gestione di hello e per tutti gli altri protocolli che hello utilizzare stesso schema si verificano a livello di applicazione hello; non definiscono nuovi i movimenti a livello di protocollo AMQP. Questo approccio è intenzionale e consente alle applicazioni di sfruttare immediatamente i vantaggi di queste estensioni con gli stack conformi ad AMQP 1.0.

Bus di servizio non attualmente implementare qualsiasi funzionalità di base hello delle specifiche di gestione di hello, ma il modello di richiesta/risposta hello definito dalla specifica di gestione di hello è fondamentale per la funzionalità di sicurezza basato su attestazioni hello e per quasi tutti Hello avanzate funzionalità illustrate in sezioni che seguono hello.

### Autorizzazione basata sulle attestazioni

bozza di specifica di Hello AMQP autorizzazione basata su attestazioni (CBS) si basa sul modello di richiesta/risposta hello gestione specifica e descrive un modello generalizzato per la modalità toouse federata i token di sicurezza con AMQP.

modello di sicurezza predefinito Hello di AMQP descritto nell'introduzione di hello è basato su SASL e si integra con l'handshake della connessione AMQP hello. Utilizzo SASL ha il vantaggio hello che fornisce un modello estendibile per cui sono stati definiti un set di meccanismi da cui può trarre vantaggio qualsiasi protocollo che formalmente tende a SASL come seguire. Tra questi meccanismi sono "PLAIN" per il trasferimento dei nomi utente e password, la protezione a livello di tooTLS toobind "Esterno", "Anonimo" tooexpress hello assenza autenticazione/autorizzazione esplicita e una vasta gamma di meccanismi aggiuntivi che consentono passaggio di credenziali di autenticazione e/o di autorizzazione o token.

L'integrazione di AMQP con SASL presenta due svantaggi:

* Tutti i token e le credenziali sono con ambito toohello connessione. Un'infrastruttura di messaggistica potrebbe essere tooprovide differenziata di controllo di accesso per singolo per ogni entità. ad esempio, consentendo la connessione hello di un token toosend tooqueue A, ma non tooqueue B. Con il contesto di autorizzazione hello ancorato nella connessione hello, è toouse non è possibile una sola connessione e utilizzare ancora i token di accesso diversi per una coda e coda B.
* I token di accesso sono in genere validi solo per un periodo limitato di tempo. La validità richiede hello utente tooperiodically riacquisire token e fornisce un toorefuse di autorità emittente del token toohello opportunità rilasciando un token aggiornato se sono state modificate le autorizzazioni di accesso dell'utente hello. Le connessioni AMQP possono durare per periodi di tempo lunghi. Hello SASL modello solo fornisce una possibilità tooset un token in fase di connessione, il che significa che hello sia l'infrastruttura di messaggistica ha client hello toodisconnect scadenza del token hello o deve rischio di hello tooaccept di consentire la comunicazione continua con un client che dispone di diritti di accesso sono stati revocati in hello provvisorio.

Hello specifica CBS AMQP, implementato dal Bus di servizio, consente una soluzione elegante per entrambi i problemi: i token di accesso tooassociate con ogni nodo e i token prima che scadano, senza interrompere il flusso dei messaggi hello tooupdate consente a un client.

CBS definisce un nodo di gestione virtuale, denominato *$cbs*, toobe fornite dall'infrastruttura di messaggistica hello. nodo Gestione Hello accetta per conto di eventuali altri nodi nell'infrastruttura di messaggistica hello.

combinazione di protocollo Hello è uno scambio di richiesta/risposta come definito dalla specifica di gestione di hello. Che indica hello client stabilisce una coppia di collegamenti con hello *$cbs* nodo e quindi passa una richiesta sul hello collegamento in uscita, quindi attende la risposta hello in hello collegamento in ingresso.

messaggio di richiesta di Hello ha hello le proprietà delle applicazioni seguenti:

| Chiave | Facoltativo | Tipo di valore | Contenuti del valore |
| --- | --- | --- | --- |
| operation |No |string |**put-token** |
| type |No |string |tipo di Hello del token hello richiesta put. |
| name |No |string |token di hello toowhich "audience" Hello applica. |
| expiration |Sì |timestamp |ora di scadenza Hello del token hello. |

Hello *nome* proprietà identifica entità hello con cui hello token deve essere associata. Bus di servizio del hello percorso toohello coda o argomento/sottoscrizione. Hello *tipo* proprietà identifica il tipo di token hello:

| Tipo di token | Descrizione del token | Tipo di corpo | Note |
| --- | --- | --- | --- |
| amqp:jwt |Token Web JSON (JWT) |Valore AMQP (stringa) |Non ancora disponibile. |
| amqp:swt |Token Web semplice (SWT) |Valore AMQP (stringa) |Supportato solo per token Web semplici emessi da AAD/ACS |
| servicebus.windows.net:sastoken |Token SAS del bus di servizio |Valore AMQP (stringa) |- |

I token conferiscono diritti. Il bus di servizio riconosce tre diritti fondamentali: "Send" per consentire l'invio, "Listen" per consentire la ricezione e "Manage" per consentire la modifica delle entità. I token Web semplici emessi da AAD/ACS includono esplicitamente questi diritti come attestazioni. Token SAS Bus di servizio vedere toorules configurato in hello dello spazio dei nomi o entità e tali regole sono configurate con i diritti. Token di firma hello con chiave hello associata a tale regola rende rispettivi diritti di hello token hello express. token Hello associato a un'entità mediante *put token* hello consente connesso toointeract client con entità hello diritti token hello. Un collegamento in cui il client hello assume hello *mittente* ruolo richiede hello "Trasmissione" a destra; l'aggiunta di hello *ricevitore* ruolo richiede il diritto di "Ascolto" hello.

messaggio di risposta Hello offre i seguenti hello *proprietà applicazione* valori

| Chiave | Facoltativo | Tipo di valore | Contenuti del valore |
| --- | --- | --- | --- |
| status-code |No |int |Codice di risposta HTTP **[RFC2616]**. |
| status-description |Sì |string |Descrizione dello stato di hello. |

Hello client può chiamare *put token* ripetutamente e per qualsiasi entità dell'infrastruttura di messaggistica hello. token Hello sono client corrente toohello con ambito e ancorato nella connessione corrente hello, significato hello server Elimina tutti i token mantenuti quando si elimina connessione hello.

implementazione del Bus di servizio corrente Hello consente solo di CBS in combinazione con hello metodo SASL "Anonimo". Una connessione SSL/TLS deve essere sempre presente handshake SASL toohello precedente.

Hello meccanismo anonimo deve pertanto essere supportato da hello scelto client AMQP 1.0. Indica l'accesso anonimo che hello l'handshake della connessione iniziale, ad esempio la creazione della sessione iniziale hello avviene senza conoscere chi sta creando una connessione hello il Bus di servizio.

Una volta stabilita la connessione hello e sessione, associare hello collega toohello *$cbs* nodo e l'invio di hello *put token* richiesta sono hello solo operazioni consentite. Un token valido deve essere impostato correttamente utilizzando un *put token* richiesta per un nodo di entità all'interno di 20 secondi dopo aver stabilita la connessione hello, in caso contrario hello unilateralmente disconnessione dal Bus di servizio.

client hello è successivamente responsabile per tenere traccia della scadenza del token. Quando un token scade, Bus di servizio viene eliminato immediatamente tutti i collegamenti nella entità corrispondente di hello connessione toohello. tooprevent, hello client può sostituire il token hello per nodo hello con uno nuovo in qualsiasi momento tramite hello virtuale *$cbs* nodo di gestione con hello stesso *put token* di movimento e senza recupero in hello modo di payload hello il traffico che i flussi in diversi collegamenti.

## Passaggi successivi

toolearn ulteriori informazioni su AMQP, visitare hello seguenti collegamenti:

* [Panoramica di AMQP per il bus di servizio]
* [Supporto di AMQP 1.0 per code e argomenti partizionati del bus di servizio]
* [AMQP nel bus di servizio per Windows Server]

[this video course]: https://www.youtube.com/playlist?list=PLmE4bZU0qx-wAP02i0I7PJWvDWoCytEjD
[1]: ./media/service-bus-amqp-protocol-guide/amqp1.png
[2]: ./media/service-bus-amqp-protocol-guide/amqp2.png
[3]: ./media/service-bus-amqp-protocol-guide/amqp3.png
[4]: ./media/service-bus-amqp-protocol-guide/amqp4.png

[Panoramica di AMQP per il bus di servizio]: service-bus-amqp-overview.md
[Supporto di AMQP 1.0 per code e argomenti partizionati del bus di servizio]: service-bus-partitioned-queues-and-topics-amqp-overview.md
[AMQP nel bus di servizio per Windows Server]: https://msdn.microsoft.com/library/dn574799.aspx
