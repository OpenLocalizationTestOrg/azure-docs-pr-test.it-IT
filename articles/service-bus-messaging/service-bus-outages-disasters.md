---
title: aaaInsulating applicazioni di Azure Service Bus da interruzioni e situazioni di emergenza | Documenti Microsoft
description: "Descrive tecniche che è possibile utilizzare applicazioni tooprotect su una potenziale interruzione del servizio Bus di servizio."
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: tysonn
ms.assetid: fd9fa8ab-f4c4-43f7-974f-c876df1614d4
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/12/2017
ms.author: sethm
ms.openlocfilehash: 349b4968456c9f15375753d83495246f5a3ddfdb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-for-insulating-applications-against-service-bus-outages-and-disasters"></a>Procedure consigliate per isolare le applicazioni del bus di servizio da interruzioni ed emergenze del servizio
Applicazioni mission-critical devono funzionare in modo continuo, anche in presenza di hello di interruzioni impreviste o situazioni di emergenza. Questo argomento descrive le tecniche che è possibile utilizzare applicazioni di Service Bus tooprotect rispetto a un potenziale interruzione del servizio o di emergenza.

Un'interruzione del servizio è definito come hello la temporanea indisponibilità del Bus di servizio di Azure. un'interruzione di Hello può interessare alcuni componenti del Bus di servizio, ad esempio un archivio di messaggistica o hello anche l'intero Data Center. Dopo che è stato risolto il problema di hello, Bus di servizio diventa nuovamente disponibile. In genere, un'interruzione non determina la perdita di messaggi o di altri dati. Un esempio di errore di un componente è indisponibilità hello di un particolare archivio di messaggistica. Un esempio di un'interruzione del Data Center è un'interruzione dell'alimentazione del Data Center hello o un commutatore di rete difettosa Data Center. Un'interruzione può durare da pochi minuti tooa alcuni giorni.

Una situazione di emergenza è definito come perdita definitiva di hello di un'unità di scala di Bus di servizio o un Data Center. Data Center di Hello può o può non nuovamente disponibile. In genere, un'emergenza determina la perdita di alcuni o di tutti i messaggi o di altri dati. Un'emergenza può essere causata, ad esempio, da un incendio, un'inondazione o un terremoto.

## <a name="current-architecture"></a>Architettura corrente
Bus di servizio Usa più archivi toostore messaggi di messaggistica vengono inviati tooqueues o argomenti. Argomento o una coda non partizionato viene assegnato tooone archivio messaggi. Se l'archivio di messaggistica in questione non è disponibile, tutte le operazioni eseguite sulla coda o sull'argomento avranno esito negativo.

Tutte le entità del bus di servizio (code, argomenti, inoltri) risiedono in uno spazio dei nomi di servizio che è affiliato a un data center. Bus di servizio non abilitare la replica geografica automatica dei dati, né consentire toospan un spazio dei nomi più Data Center.

## <a name="protecting-against-acs-outages"></a>Protezione da interruzioni del servizio di controllo di accesso (ACS)
Se si usano credenziali ACS e il servizio ACS non è disponibile, i client non possono più ottenere i token. I client che dispone di un token in fase di hello che ACS si arresta possono continuare toouse Bus di servizio fino alla scadenza di token hello. durata del token Hello predefinito è 3 ore.

tooprotect da interruzioni di ACS, usare i token di firma di accesso condiviso (SAS). In questo caso, hello client esegue l'autenticazione direttamente con il Bus di servizio firmando un token coniato con una chiave privata. TooACS chiamate non sono più necessari. Per altre informazioni sulla configurazione dei token di firma di accesso condiviso, vedere [Autenticazione e autorizzazione del bus di servizio][Service Bus authentication].

## <a name="protecting-queues-and-topics-against-messaging-store-failures"></a>Protezione di code e argomenti da errori degli archivi di messaggistica
Argomento o una coda non partizionato viene assegnato tooone archivio messaggi. Se l'archivio di messaggistica in questione non è disponibile, tutte le operazioni eseguite sulla coda o sull'argomento avranno esito negativo. Oggetto partizionata hello coda, invece, è costituito da più frammenti. ciascuno dei quali memorizzato in un archivio di messaggistica differente. Quando viene inviato un messaggio tooa coda o argomento partizionato, Bus di servizio assegna tooone messaggio hello di frammenti di hello. Se l'archivio di messaggistica corrispondente hello è disponibile, Bus di servizio scrive hello tooa diversi frammento di messaggio, se possibile. Per altre informazioni sulle entità partizionate, vedere le [entità di messaggistica partizionate][Partitioned messaging entities].

## <a name="protecting-against-datacenter-outages-or-disasters"></a>Protezione da interruzioni o emergenze dei data center
tooallow per un failover tra due Data Center, è possibile creare uno spazio dei nomi service Bus di servizio in ogni Data Center. Ad esempio, hello spazio dei nomi service Bus di servizio **contosoPrimary.servicebus.windows.net** potrebbe trovarsi in area Stati Uniti centro Nord hello e **contosoSecondary.servicebus.windows.net**potrebbe trovarsi nell'area Stati Uniti centro-meridionali hello. Se un'entità di messaggistica di Service Bus deve rimanere accessibile in presenza di hello di un'interruzione del Data Center, è possibile creare tale entità in entrambi gli spazi dei nomi.

Per ulteriori informazioni, vedere "Errore di Service Bus in un Data Center di Azure" sezione hello [disponibilità elevata e modelli di messaggistica asincrona][Asynchronous messaging patterns and high availability].

## <a name="protecting-relay-endpoints-against-datacenter-outages-or-disasters"></a>Protezione degli endpoint di inoltro da interruzioni o emergenze dei data center
La replica geografica degli endpoint di inoltro consente a un servizio che espone un endpoint inoltro per toobe raggiungibile in presenza di hello di interruzioni del Bus di servizio. tooachieve-replica geografica, servizio hello deve creare due endpoint di inoltro in spazi dei nomi diversi. spazi dei nomi Hello devono trovarsi in Data Center diversi e due endpoint hello devono avere nomi diversi. Ad esempio, un endpoint primario può essere raggiunto in **contosoPrimary.servicebus.windows.net/myPrimaryService**, mentre il corrispettivo endpoint secondario può essere raggiunto in **contosoSecondary.servicebus.windows.net/mySecondaryService**.

servizio di Hello è quindi in ascolto su entrambi gli endpoint e un client può richiamare il servizio di hello tramite degli endpoint. Un'applicazione client in modo casuale sceglie uno di hello inoltri come endpoint primario hello e invia il relativo endpoint attivo toohello di richiesta. Se l'operazione di hello ha esito negativo con un codice di errore, questo errore indica che tale endpoint di inoltro hello non è disponibile. un'applicazione Hello viene aperto un endpoint del canale toohello backup ed emette nuovamente richiesta hello. A questo punto hello attivo e gli endpoint di backup hello cambiano di ruolo: un'applicazione hello client considera toobe endpoint attivo precedente hello hello nuovo endpoint di backup e toobe endpoint di backup precedente hello hello nuovo endpoint attivo. Se entrambe esito negativo delle operazioni di invio, i ruoli di hello di due entità hello rimangono invariati e viene restituito un errore.

Hello [-replica geografica con il Bus di servizio di inoltro dei messaggi] [ Geo-replication with Service Bus relayed Messages] esempio viene illustrato come tooreplicate inoltra.

## <a name="protecting-queues-and-topics-against-datacenter-outages-or-disasters"></a>Protezione delle code e degli argomenti da interruzioni o emergenze dei data center
resilienza tooachieve per interruzioni dei Data Center durante l'uso di messaggistica negoziata, Bus di servizio supporta due approcci: *active* e *passivo* replica. Per ciascun approccio, se una determinata coda o un argomento deve rimanere accessibile in presenza di hello di un'interruzione del Data Center, è possibile crearlo in entrambi gli spazi dei nomi. Entrambe le entità possono avere hello stesso nome. Ad esempio, una coda primaria può essere raggiunta in **contosoPrimary.servicebus.windows.net/myQueue**, mentre la rispettiva coda secondaria può essere raggiunta in **contosoSecondary.servicebus.windows.net/myQueue**.

Se un'applicazione hello non richiede la comunicazione mittente-ricevitore permanente, un'applicazione hello possibile implementare una coda durevole lato client tooprevent perdita e tooshield hello mittente da eventuali errori temporanei di Bus di servizio.

## <a name="active-replication"></a>Replica attiva
La replica attiva usa entità in entrambi gli spazi dei nomi per ogni operazione. Qualsiasi client che invia un messaggio inviato due copie di hello stesso messaggio. prima copia Hello viene inviata l'entità primaria toohello (ad esempio, **contosoPrimary.servicebus.windows.net/sales**), e seconda copia di hello del messaggio hello viene inviato l'entità secondaria toohello (ad esempio,  **contosoSecondary.servicebus.windows.net/sales**).

Un client riceve messaggi da entrambe le code. i processi di ricevitore Hello hello prima copia di un messaggio e copia secondo hello viene eliminato. toosuppress messaggi duplicati, il mittente hello deve contrassegnare ciascun messaggio con un identificatore univoco. Entrambe le copie del messaggio devono essere contrassegnate con hello stesso identificatore. È possibile utilizzare hello [BrokeredMessage.MessageId] [ BrokeredMessage.MessageId] o [BrokeredMessage.Label] [ BrokeredMessage.Label] proprietà o un hello tootag proprietà personalizzata Messaggio. ricevitore Hello deve gestire un elenco dei messaggi già ricevuti.

Hello [replica geografica con i messaggi negoziati di Service Bus] [ Geo-replication with Service Bus Brokered Messages] illustra replica attiva delle entità di messaggistica.

> [!NOTE]
> Hello replica attiva raddoppia il numero di hello di operazioni, pertanto questo approccio può comportare costi toohigher.
> 
> 

## <a name="passive-replication"></a>Replica passiva
In caso di errore senza hello, replica passiva viene usata solo una delle due entità di messaggistica hello. Un client invia l'entità attiva toohello di messaggio hello. Se hello sull'entità attiva hello esito negativo con un codice di errore che indica Data Center hello che entità attiva di hello host potrebbe non essere disponibile, il client di hello invia una copia dell'entità di backup toohello messaggio hello. A questo punto hello attiva e le entità di backup hello cambiano di ruolo: client mittente hello considera hello entità attiva toobe hello nuova entità di backup precedente e l'entità di backup precedente hello è nuova entità attiva hello. Se entrambe esito negativo delle operazioni di invio, i ruoli di hello di due entità hello rimangono invariati e viene restituito un errore.

Un client riceve messaggi da entrambe le code. Poiché è probabile che ricevitore hello riceve due copie dello stesso messaggio hello hello ricevitore deve eliminare i messaggi duplicati. È possibile eliminare duplicati nello hello come descritto per la replica attiva.

In genere, la replica passiva è più vantaggiosa di quella attiva perché nella maggior parte dei casi viene eseguita una sola operazione. Latenza, velocità effettiva e il costo sono scenario non replicato toohello identici.

Quando si utilizza la replica passiva, in hello messaggi gli scenari seguenti possono essere persi o ricevuti due volte:

* **Messaggio ritardo o perdita**: si presuppone che hello mittente abbia inviato con una coda di messaggi m1 toohello primaria e coda hello diventa quindi disponibile prima di hello ricezione m1. mittente Hello invia una coda di messaggi successivi m2 toohello secondario. Se la coda primaria hello è temporaneamente non disponibile, il ricevitore hello riceve m1 dopo hello coda torna nuovamente disponibile. In caso di emergenza, il ricevitore hello potrebbe non ricevere mai m1.
* **Ricezione di duplicati**: si presuppone che mittente hello invia una coda di messaggi m toohello primario. Bus di servizio completato elabora m ma ha esito negativo toosend una risposta. Dopo che hello inviare Timeout operazione, il mittente hello invia una copia identica della coda secondaria di toohello m. Se ricevitore hello è la prima copia hello tooreceive in grado di m che la coda primaria hello diventi non disponibile, il ricevitore hello riceve entrambe le copie di m a circa hello contemporaneamente. Ricevitore hello non è la prima copia hello tooreceive in grado di m che la coda primaria hello diventi non disponibile, il ricevitore hello riceverà inizialmente solo hello seconda copia di m, ma riceve quindi una seconda copia di m quando la coda primaria hello diventa disponibile.

Hello [-replica geografica con il Bus di servizio negoziata messaggi] [ Geo-replication with Service Bus Brokered Messages] illustra la replica passiva delle entità di messaggistica.

## <a name="next-steps"></a>Passaggi successivi
toolearn più sul ripristino di emergenza, vedere i seguenti articoli:

* [Continuità aziendale del database SQL di Azure][Azure SQL Database Business Continuity]
* [Progettazione di applicazioni resilienti per Azure][Azure resiliency technical guidance]

[Service Bus Authentication]: service-bus-authentication-and-authorization.md
[Partitioned messaging entities]: service-bus-partitioning.md
[Asynchronous messaging patterns and high availability]: service-bus-async-messaging.md#failure-of-service-bus-within-an-azure-datacenter
[Geo-replication with Service Bus Relayed Messages]: http://code.msdn.microsoft.com/Geo-replication-with-16dbfecd
[BrokeredMessage.MessageId]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_MessageId
[BrokeredMessage.Label]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Label
[Geo-replication with Service Bus Brokered Messages]: http://code.msdn.microsoft.com/Geo-replication-with-f5688664
[Azure SQL Database Business Continuity]: ../sql-database/sql-database-business-continuity.md
[Azure resiliency technical guidance]: /azure/architecture/resiliency
