---
title: aaaOverview di nozioni di base di Service Bus di Azure | Documenti Microsoft
description: Tooconnect software tooother applicazioni Azure del Bus di servizio di toousing un'introduzione.
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 12654cdd-82ab-4b95-b56f-08a5a8bbc6f9
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/15/2017
ms.author: sethm
ms.openlocfilehash: 1abd5cf310ef06ba35e1e2489a7c0a07e1797736
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-service-bus"></a>Bus di servizio di Azure

Se un'applicazione o un servizio viene eseguito nel cloud hello o in locale, è spesso necessario toointeract con altre applicazioni o servizi. tooprovide toodo un modo utile su vasta scala, offerte di Microsoft Azure Service Bus. In questo articolo esamina questa tecnologia, che descrivono cosa e perché potrebbe essere necessario toouse è.

## <a name="service-bus-fundamentals"></a>Dati fondamentali del bus di servizio

A seconda delle situazioni, possono essere necessari stili di comunicazione diversi. In alcuni casi, consentendo alle applicazioni di inviare e ricevere messaggi tramite una coda semplice è la soluzione migliore hello. In altre situazioni, una coda ordinaria non è sufficiente e l'uso di una coda con un meccanismo di pubblicazione e sottoscrizione risulta la soluzione più adatta. In alcuni casi, è sufficiente una connessione tra applicazioni e le code non sono necessarie. Bus di servizio fornisce tutte le tre opzioni, l'abilitazione di toointeract le applicazioni in diversi modi.

Bus di servizio è un servizio cloud multi-tenant, il che significa che il servizio di hello è condiviso da più utenti. Ogni utente, ad esempio uno sviluppatore di applicazioni, crea un *dello spazio dei nomi*, quindi definisce i meccanismi di comunicazione hello necessari all'interno di tale spazio dei nomi. La Figura 1 mostra l'aspetto di questa architettura.

![][1]

**Figura 1: Service Bus fornisce un servizio multi-tenant per la connessione di applicazioni tramite cloud hello.**

All'interno di uno spazio dei nomi è possibile utilizzare una o più istanze di tre meccanismi di comunicazione diversi, ognuno dei quali consente di connettere le applicazioni in modo diverso. sono disponibili Hello:

* *Code*: consentono la comunicazione unidirezionale. Ogni coda funge da intermediario (talvolta è infatti denominata *broker*) che archivia i messaggi inviati fino a quando non vengono ricevuti. Ogni messaggio viene ricevuto da un singolo destinatario.
* *Argomenti*: garantiscono la comunicazione unidirezionale mediante *sottoscrizioni*. Un singolo argomento può avere più sottoscrizioni. Ad esempio una coda, un argomento funziona come un broker, ma ogni sottoscrizione è possibile usare facoltativamente un filtro tooreceive solo i messaggi che soddisfano criteri specifici.
* *Inoltri*: forniscono funzionalità di comunicazione bidirezionale. Diversamente da code e argomenti, un inoltro non archivia i messaggi in elaborazione, perché non si tratta di un broker. In alternativa, appena li passa sull'applicazione di destinazione toohello.

Quando si crea una coda, un argomento o un inoltro, occorre assegnargli un nome. In combinazione con la chiamata dello spazio dei nomi, questo nome crea un identificatore univoco per l'oggetto hello. Le applicazioni è possono fornire questo tooService nome Bus, quindi utilizzare tale coda, argomento o inoltro toocommunicate tra loro. 

toouse uno di questi oggetti in uno scenario di inoltro hello, le applicazioni di Windows possono utilizzare Windows Communication Foundation (WCF). Questo servizio è noto come [inoltro WCF](../service-bus-relay/relay-what-is-it.md). Per le code e gli argomenti, le applicazioni Windows possono usare API del sistema di messaggistica definite dal bus di servizio. toomake questi oggetti toouse più semplice da applicazioni non Windows, Microsoft fornisce SDK per Java, Node.js e altri linguaggi. È anche possibile accedere a code e argomenti tramite le [API REST](/rest/api/servicebus/) su HTTP. 

È importante toounderstand che anche se Service Bus stesso viene eseguito nel cloud hello (vale a dire nel Data Center di Microsoft Azure), applicazioni che lo utilizzano possono essere eseguite ovunque. È possibile utilizzare applicazioni tooconnect Bus di servizio in esecuzione in Azure, ad esempio, o le applicazioni in esecuzione il proprio Data Center. È inoltre possibile utilizzare il tooconnect un'applicazione in esecuzione in Azure o in un'altra piattaforma cloud con un'applicazione locale o con Tablet e telefoni. È anche possibile tooconnect elettrodomestici, sensori e i dispositivi tooa centrale o applicazioni tooone altri. Bus di servizio è un meccanismo di comunicazione nel cloud hello accessibile praticamente ovunque. Come utilizzare dipende dal quale le applicazioni devono toodo.

## <a name="queues"></a>Code

Si supponga che si decide di due applicazioni tooconnect mediante una coda del Bus di servizio. Nella figura 2 è illustrato questo scenario.

![][2]

**Figura 2: le code del bus di servizio forniscono un servizio di accodamento asincrono unidirezionale.**

il processo di Hello è semplice: un mittente invia una coda di Service Bus di messaggi tooa e un ricevitore preleva il messaggio in un secondo momento. Una coda può avere un singolo ricevitore, come illustrato nella Figura 2, O, più applicazioni possono leggere da hello stessa coda. In quest'ultimo caso hello, ogni messaggio viene letto da un solo destinatario. Per un servizio multicast è invece consigliabile usare un argomento.

Ogni messaggio è costituito da due parti: un set di proprietà, ognuno costituito da una coppia chiave-valore, e un payload dei messaggi. payload Hello può essere anche XML, testo o binario. Modalità di utilizzo dipende da un'applicazione sta tentando di toodo. Ad esempio, un'applicazione che invia un messaggio su un recente vendita potrebbe includere proprietà hello **venditore = "Ava"** e **quantità = 10000**. corpo del messaggio Hello potrebbe contenere un'immagine acquisita del contratto della vendita hello o, in caso contrario, rimanere vuoto.

Un ricevitore può leggere un messaggio da una coda del bus di servizio in due modi. Hello prima opzione, chiamato  *[ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode)*, rimuove un messaggio dalla coda hello e vengono eliminati immediatamente. Questa opzione è semplice, ma se ricevitore hello blocco prima del completamento dell'elaborazione del messaggio hello del messaggio hello viene perso. Perché è stato rimosso dalla coda di hello, nessun altro ricevitore può accedervi. 

seconda opzione, Hello  *[PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode)*, toohelp questo problema è stato progettato. Ad esempio **ReceiveAndDelete**, **PeekLock** lettura rimuove un messaggio dalla coda hello. Non viene eliminato il messaggio hello, tuttavia. In alternativa, blocca il messaggio hello, rendendolo ricevitori tooother invisibile, quindi attende che uno dei tre eventi:

* Se i processi di ricevitore hello hello messaggio correttamente, viene chiamato [complete ()](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete), e coda hello Elimina messaggio hello. 
* Se il ricevitore hello decide che non può elaborare correttamente il messaggio hello, chiama [Abandon()](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Abandon). coda Hello quindi rimuove il blocco di hello dal messaggio hello e rende disponibili tooother ricevitori.
* Se il ricevitore hello chiamate nessuno di questi metodi all'interno di un periodo di tempo configurabile (per impostazione predefinita, 60 secondi), si presuppone coda hello hello ricevitore non è riuscito. In questo caso, si comporta come se fosse stato chiamato ricevitore hello **abbandonare**, rendendo hello tooother disponibili dei destinatari dei messaggi.

Si noti che può verificarsi qui: hello stesso messaggio potrebbe essere recapitato due volte, ad esempio tootwo di destinatari diversi. Le applicazioni che usano le code del bus di servizio devono prevedere questa eventualità. rilevamento duplicati toomake più semplice, ogni messaggio è univoco [MessageID](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_MessageId) proprietà che, per impostazione predefinita, rimane hello uguali indipendentemente da quante volte il messaggio hello viene letta da una coda. 

Le code risultano utili in un numero limitato di situazioni. Che consentono alle applicazioni toocommunicate anche quando non vengono eseguiti in hello stesso tempo un elemento che è particolarmente utile con batch e applicazioni per dispositivi mobili. Una coda con più ricevitori garantisce inoltre il bilanciamento del carico automatico, in quanto i messaggi vengono distribuiti tra i vari ricevitori.

## <a name="topics"></a>Argomenti

Utile come se fossero, le code non sono sempre soluzione hello. Talvolta, sono più indicati gli argomenti del bus di servizio. Nella figura 3 viene illustrato questo concetto.

![][3]

**Figura 3: Basata su filtro hello che specifica di un'applicazione di sottoscrizione, la ricezione di alcuni o tutti i messaggi hello inviati tooa argomento del Bus di servizio.**

Oggetto *argomento* è simile nella coda di tooa molti modi. I mittenti inviare argomento tooa messaggi hello stesso modo in cui l'invio di messaggi tooa coda e aspetto tali messaggi hello come per le code. Hello differenza è che gli argomenti abilitano ogni toocreate applicazione ricevente un proprio *sottoscrizione* definendo un *filtro*. Un sottoscrittore vengono quindi visualizzati solo i messaggi di hello che corrisponderanno al filtro. Nella figura 3, ad esempio, sono mostrati un mittente e un argomento con tre sottoscrittori, ognuno con il relativo filtro:

* Sottoscrittore 1 riceve solo i messaggi che contengono proprietà hello *venditore = "Ava"*.
* Server di sottoscrizione 2 riceve i messaggi che contengono proprietà hello *venditore = "Ruby"* e/o contenere un *quantità* proprietà il cui valore è maggiore di 100.000. Ad esempio Ruby è hello responsabile delle vendite, in modo desiderate toosee tutte le vendite di grandi dimensioni indipendentemente dal fatto che li rende e proprie vendite.
* Sottoscrittore 3 è impostato il filtro troppo*True*, il che significa che riceve tutti i messaggi. Ad esempio, l'applicazione potrebbe essere responsabile della gestione di un itinerario di controllo e pertanto deve toosee tutti i messaggi hello.

Come con le code, argomento tooa i sottoscrittori possa leggere i messaggi utilizzando [ReceiveAndDelete o PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode). A differenza delle code, tuttavia, un singolo messaggio inviato tooa argomento può essere ricevuto da più sottoscrizioni. Questo approccio, comunemente denominato *di pubblicazione e sottoscrizione* (o *pub/sub*), è utile quando più applicazioni sono interessate a hello messaggi stesso. Mediante la definizione di filtro destra hello, ogni sottoscrittore può usufruire solo parte di hello del flusso di messaggi hello talmente toosee.

## <a name="relays"></a>Inoltri

Le code e gli argomenti consentono la comunicazione asincrona unidirezionale tramite un broker. Il traffico scorre in una sola direzione e non esiste una connessione diretta tra mittenti e ricevitori. Talvolta questo potrebbe non essere sufficiente, ad esempio Si supponga che le applicazioni devono tooboth inviare e ricevere messaggi, o forse si desidera un collegamento diretto tra di essi e non è necessario un toostore i messaggi di Service broker. scenari di tooaddress come questo, Service Bus fornisce *inoltra*, come illustrato nella figura 4.

![][4]

**Figura 4: l'inoltro del bus di servizio garantisce la comunicazione sincrona bidirezionale tra applicazioni.**

Hello tooask domanda sugli inoltri è: perché utilizzare una? Anche se non occorre code, motivo per cui rendere le applicazioni di comunicare tramite un servizio cloud, anziché solo interagire direttamente? risposte Hello sono che comunica direttamente può essere difficile quanto si pensi.

Si supponga tooconnect due applicazioni locali sia in esecuzione in data center aziendale. Ognuna di queste applicazioni è protetta da firewall ed è probabile che ogni data center usi il processo NAT (Network Address Translation). Hello firewall blocca i dati in entrata su tutte tranne alcune porte, NAT e implica che ogni applicazione è in esecuzione sul computer di hello non dispone di un indirizzo IP fisso che è possibile accedere direttamente dal Data Center hello esterno. Senza l'assistenza aggiuntiva, la connessione di queste applicazioni su hello rete internet pubblica risulta problematico.

L'inoltro del bus di servizio di Azure può risultare utile. toocommunicate bidirezionale attraverso un servizio di inoltro, ogni applicazione stabilisce una connessione TCP in uscita con il Bus di servizio, quindi li mantiene aperta. Tutte le comunicazioni tra due applicazioni hello viene trasmessa queste connessioni. Poiché ogni connessione è stata stabilita all'interno di hello datacenter, hello firewall consente l'applicazione tooeach di traffico in ingresso senza aprire nuove porte. Questo approccio si ottiene anche problema NAT hello, perché ogni applicazione dispone di un endpoint coerenza nel cloud hello in tutta la comunicazione hello. Mediante lo scambio di dati tramite inoltro hello, applicazioni hello possono evitare problemi di hello che in caso contrario renderebbe comunicazione difficile. 

toouse Bus di servizio inoltra, le applicazioni si basano su hello Windows Communication Foundation (WCF). Bus di servizio fornisce associazioni di WCF che rendono più semplice per toointeract di applicazioni di Windows tramite gli inoltri. Le applicazioni che già utilizzano WCF possono in genere specificare una di queste associazioni, quindi comunicare tooeach altri attraverso un servizio di inoltro. Diversamente da code e argomenti, l'uso degli inoltri da applicazioni non Windows, anche se possibile, richiede alcune operazioni di programmazione dato che non sono disponibili librerie standard.

Diversamente da code e argomenti, le applicazioni non creano inoltri in modo esplicito. Quando un'applicazione tooreceive messaggi stabilisce una connessione TCP con il Bus di servizio, un inoltro viene invece creato automaticamente. Quando viene eliminato connessione hello, inoltro hello viene eliminato. tooenable un inoltro hello toofind di applicazione creato da un listener specifico, Service Bus fornisce un registro di sistema che consente applicazioni toolocate un inoltro specifico in base al nome.

Gli inoltri sono la soluzione ideale hello quando è necessaria una comunicazione diretta tra applicazioni. ad esempio un sistema di prenotazione di una compagnia aerea in esecuzione in un data center locale al quale devono poter accedere banchi del check-in, dispositivi mobili e altri computer. Le applicazioni in esecuzione in tutti questi sistemi possono avvalersi inoltri del Bus di servizio in hello cloud toocommunicate, ogni volta che potrebbe essere in esecuzione.

## <a name="summary"></a>Riepilogo

La connessione di applicazioni è sempre stato parte della creazione di soluzioni complete e tooincrease impostazione dell'intervallo hello scenari che richiedono le applicazioni e servizi toocommunicate tra loro più applicazioni e dispositivi sono connesso toohello internet. Fornendo tecnologie basate su cloud per ottenere la comunicazione tramite code, argomenti e inoltri, Bus di servizio ha come obiettivo toomake questo tooimplement più semplice funzione essenziale e più diffusi.

## <a name="next-steps"></a>Passaggi successivi

Ora che si sono appreso i principi fondamentali di hello del Bus di servizio di Azure, seguire questi ulteriori toolearn di collegamenti.

* Come toouse [code del Bus di servizio](service-bus-dotnet-get-started-with-queues.md)
* Come toouse [argomenti del Bus di servizio](service-bus-dotnet-how-to-use-topics-subscriptions.md)
* Come toouse [inoltro del Bus di servizio](../service-bus-relay/service-bus-dotnet-how-to-use-relay.md)
* [Esempi relativi al bus di servizio](service-bus-samples.md)

[1]: ./media/service-bus-fundamentals-hybrid-solutions/SvcBus_01_architecture.png
[2]: ./media/service-bus-fundamentals-hybrid-solutions/SvcBus_02_queues.png
[3]: ./media/service-bus-fundamentals-hybrid-solutions/SvcBus_03_topicsandsubscriptions.png
[4]: ./media/service-bus-fundamentals-hybrid-solutions/SvcBus_04_relay.png
