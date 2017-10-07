---
title: eccezioni di messaggistica Bus di servizio aaaAzure | Documenti Microsoft
description: Elenco delle eccezioni di messaggistica del bus di servizio e relative azioni consigliate.
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 3d8526fe-6e47-4119-9f3e-c56d916a98f9
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/06/2017
ms.author: sethm
ms.openlocfilehash: 0a206b7bbc808c1190044c1dfd6ffd47b9d454fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-messaging-exceptions"></a>Eccezioni di messaggistica del bus di servizio
Questo articolo vengono elencati alcuni le eccezioni generate dal Bus di servizio di Microsoft Azure hello API di messaggistica. Questo riferimento è soggetto toochange, quindi cercare nuovamente gli aggiornamenti.

## <a name="exception-categories"></a>Categorie di eccezioni
le API di messaggistica Hello generano le eccezioni che possono rientrano nelle seguenti categorie di hello, insieme azione hello associato è possibile eseguire tootry toofix li. Si noti che le cause di un'eccezione e il significato di hello possono variare in base al tipo di hello di entità di messaggistica (code o argomenti o hub eventi):

1. Errore nella codifica dell'utente ([System.ArgumentException](https://msdn.microsoft.com/library/system.argumentexception.aspx), [System.InvalidOperationException](https://msdn.microsoft.com/library/system.invalidoperationexception.aspx), [System.OperationCanceledException](https://msdn.microsoft.com/library/system.operationcanceledexception.aspx), [System.Runtime.Serialization.SerializationException](https://msdn.microsoft.com/library/system.runtime.serialization.serializationexception.aspx)). Azione generale: provare toofix hello codice prima di procedere.
2. Errore di configurazione/installazione ([Microsoft.ServiceBus.Messaging.MessagingEntityNotFoundException](/dotnet/api/microsoft.servicebus.messaging.messagingentitynotfoundexception), [System.UnauthorizedAccessException](https://msdn.microsoft.com/library/system.unauthorizedaccessexception.aspx). Azione generale: controllare la configurazione e modificarla, se necessario.
3. Eccezioni temporanee ([Microsoft.ServiceBus.Messaging.MessagingException](/dotnet/api/microsoft.servicebus.messaging.messagingexception), [Microsoft.ServiceBus.Messaging.ServerBusyException](/dotnet/api/microsoft.servicebus.messaging.serverbusyexception), [Microsoft.ServiceBus.Messaging.MessagingCommunicationException](/dotnet/api/microsoft.servicebus.messaging.messagingcommunicationexception)). Azione generale: hello riprovare o inviare notifiche agli utenti.
4. Altre eccezioni ([System.Transactions.TransactionException](https://msdn.microsoft.com/library/system.transactions.transactionexception.aspx), [System.TimeoutException](https://msdn.microsoft.com/library/system.timeoutexception.aspx), [Microsoft.ServiceBus.Messaging.MessageLockLostException](/dotnet/api/microsoft.servicebus.messaging.messagelocklostexception), [Microsoft.ServiceBus.Messaging.SessionLockLostException](/dotnet/api/microsoft.servicebus.messaging.sessionlocklostexception)). Azione generale: tipo di eccezione specifico toohello; consultare la tabella toohello nella seguente sezione hello. 

## <a name="exception-types"></a>Tipi di eccezioni
Hello nella tabella seguente elenca messaggistica i tipi di eccezione e le cause e Azione suggerita di note che è possibile eseguire.

| **Tipo di eccezione** | **Descrizione/Causa/Esempi** | **Azione suggerita** | **Nota sulla ripetizione automatica/immediata** |
| --- | --- | --- | --- |
| [TimeoutException](https://msdn.microsoft.com/library/system.timeoutexception.aspx) |Hello server non ha risposto toohello richiesto operazione all'interno di hello specificato controllato dal [OperationTimeout](/dotnet/api/microsoft.servicebus.messaging.messagingfactorysettings#Microsoft_ServiceBus_Messaging_MessagingFactorySettings_OperationTimeout). server Hello potrebbe essere stata completata l'operazione di richiesta di hello. Questa situazione può verificarsi a causa di toonetwork o altri ritardi di infrastruttura. |Verificare la coerenza dello stato del sistema hello e ripetere se necessario. Vedere [Eccezioni di timeout](#timeoutexception). |Riprova utili in alcuni casi; aggiungere toocode logica di ripetizione. |
| [InvalidOperationException](https://msdn.microsoft.com/library/system.invalidoperationexception.aspx) |Hello ha richiesto l'operazione dell'utente non è consentita all'interno di server hello o un servizio. Messaggio di eccezione hello per informazioni dettagliate, vedere. Ad esempio, [completa](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete) genererà questa eccezione se è stato ricevuto il messaggio hello in [ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode) modalità. |Controllare il codice hello e la documentazione di hello. Verificare che hello ha richiesto l'operazione è valida. |Ripetere l'operazione non serve. |
| [OperationCanceledException](https://msdn.microsoft.com/library/system.operationcanceledexception.aspx) |Viene eseguito un tentativo effettuato tooinvoke un'operazione su un oggetto che è già stata chiusa, interrotta o eliminata. In rari casi, transazione di ambiente hello è già stata eliminata. |Controllare il codice hello e assicurarsi che non vengono richiamate le operazioni su un oggetto eliminato. |Ripetere l'operazione non serve. |
| [UnauthorizedAccessException](https://msdn.microsoft.com/library/system.unauthorizedaccessexception.aspx) |Hello [TokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider) oggetto non è stato possibile acquisire un token, hello token non è valido o hello token non contiene hello attestazioni necessarie tooperform hello operazione. |Assicurarsi che i provider di token hello viene creato con i valori corretti di hello. Controllare la configurazione di hello di hello servizio controllo di accesso. |Riprova utili in alcuni casi; aggiungere toocode logica di ripetizione. |
| [ArgumentException](https://msdn.microsoft.com/library/system.argumentexception.aspx)<br /> [ArgumentNullException](https://msdn.microsoft.com/library/system.argumentnullexception.aspx)<br />[ArgumentOutOfRangeException](https://msdn.microsoft.com/library/system.argumentoutofrangeexception.aspx) |Metodo di toohello uno o più argomenti forniti non sono validi.<br /> Hello URI fornito troppo[NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) o [crea](/dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_Create_System_Collections_Generic_IEnumerable_System_Uri__) contiene ai segmenti di percorso.<br /> schema URI Hello fornito troppo[NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) o [crea](/dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_Create_System_Collections_Generic_IEnumerable_System_Uri__) non è valido. <br />valore della proprietà Hello è maggiore di 32KB. |Controllare il codice chiamante hello e verificare che gli argomenti di hello siano corretti. |Ripetere l'operazione non serve. |
| [MessagingEntityNotFoundException](/dotnet/api/microsoft.servicebus.messaging.messagingentitynotfoundexception) |Entità associato all'operazione hello non esiste o è stato eliminato. |Verificare che l'entità hello esiste. |Ripetere l'operazione non serve. |
| [MessageNotFoundException](/dotnet/api/microsoft.servicebus.messaging.messagenotfoundexception) |Tenta di tooreceive un messaggio con un numero di sequenza particolare. Non è stato trovato questo messaggio. |Verificare che il messaggio hello non è già stato ricevuto. Controllare toosee coda di messaggi non recapitabili hello se il messaggio hello è stato superato. |Ripetere l'operazione non serve. |
| [MessagingCommunicationException](/dotnet/api/microsoft.servicebus.messaging.messagingcommunicationexception) |Client non è in grado di tooestablish tooService una connessione Bus. |Verificare che il nome di host hello fornito sia corretto e hello host è raggiungibile. |Se sono presenti problemi di connettività intermittente, può essere utile ripetere l'operazione. |
| [ServerBusyException](/dotnet/api/microsoft.servicebus.messaging.serverbusyexception) |Servizio non è richiesta hello in grado di tooprocess in questo momento. |Client può attendere un periodo di tempo, quindi ripetere l'operazione di hello. |Il client può riprovare dopo un determinato intervallo. Se viene generata un'eccezione diversa, controllare il comportamento di ripetizione del tentativo della nuova eccezione. |
| [MessageLockLostException](/dotnet/api/microsoft.servicebus.messaging.messagelocklostexception) |Token di blocco associato al messaggio hello è scaduto o non viene trovato il token di blocco hello. |Eliminare il messaggio hello. |Ripetere l'operazione non serve. |
| [SessionLockLostException](/dotnet/api/microsoft.servicebus.messaging.sessionlocklostexception) |È stato perso il blocco associato a questa sessione. |Interrompere hello [MessageSession](/dotnet/api/microsoft.servicebus.messaging.messagesession) oggetto. |Ripetere l'operazione non serve. |
| [MessagingException](/dotnet/api/microsoft.servicebus.messaging.messagingexception) |Generico messaggistica eccezione generata in hello seguenti casi:<br /> Viene effettuato un tentativo di toocreate un [QueueClient](/dotnet/api/microsoft.servicebus.messaging.queueclient) con un nome o percorso al quale appartiene il tipo di entità diversa tooa (ad esempio, un argomento).<br />  Il tentativo è ingrandita toosend un messaggio a 256KB. server Hello o un servizio ha rilevato un errore durante l'elaborazione della richiesta di hello. Vedere il messaggio di eccezione hello per informazioni dettagliate. Si tratta in genere di un'eccezione temporanea. |Controllare il codice hello e assicurarsi che solo gli oggetti serializzabili vengono usati per il corpo del messaggio hello o usare un serializzatore personalizzato. Controllare la documentazione di hello per i tipi di valore hello supportato di proprietà hello e solo i tipi di utilizzo è supportato. Controllare hello [IsTransient](/dotnet/api/microsoft.servicebus.messaging.messagingexception#Microsoft_ServiceBus_Messaging_MessagingException_IsTransient) proprietà. Se è **true**, è possibile ritentare l'operazione di hello. |Il comportamento di ripetizione dei tentativi non è definito e ripetere l'operazione può non essere utile. |
| [MessagingEntityAlreadyExistsException](/dotnet/api/microsoft.servicebus.messaging.messagingentityalreadyexistsexception) |Tentativo toocreate un'entità con un nome che è già utilizzato da un'altra entità nello spazio dei nomi del servizio. |Eliminare un'entità esistente hello o scegliere un nome diverso per hello entità toobe creato. |Ripetere l'operazione non serve. |
| [QuotaExceededException](/dotnet/api/microsoft.servicebus.messaging.quotaexceededexception) |Hello entità di messaggistica ha raggiunto la dimensione massima consentita oppure è stato superato numero massimo di hello dello spazio dei nomi tooa connessioni. |Liberare spazio nell'entità hello dal relativo code secondarie o di ricezione di messaggi da entità hello. Vedere [QuotaExceededException](#quotaexceededexception). |Riprova potrebbe risultare utile se i messaggi sono state rimosse in hello frattempo. |
| [RuleActionException](/dotnet/api/microsoft.servicebus.messaging.ruleactionexception) |Bus di servizio restituisce l'eccezione, se si tenta di toocreate un'azione di regola non valida. Bus di servizio si connette, questo messaggio di eccezione tooa superato se si verifica un errore durante l'elaborazione di azione della regola per il messaggio hello. |Controllare l'azione della regola hello la correttezza. |Ripetere l'operazione non serve. |
| [FilterException](/dotnet/api/microsoft.servicebus.messaging.filterexception) |Bus di servizio restituisce l'eccezione, se si tenta di toocreate un filtro non valido. Bus di servizio si connette, questo messaggio di eccezione tooa superato se si è verificato un errore durante l'elaborazione di filtro hello per il messaggio. |Controllare il filtro hello la correttezza. |Ripetere l'operazione non serve. |
| [SessionCannotBeLockedException](/dotnet/api/microsoft.servicebus.messaging.sessioncannotbelockedexception) |Tentativo di tooaccept che una sessione con un ID di sessione specifiche, ma la sessione hello è attualmente bloccata da un altro client. |Verificare che la sessione hello è sbloccata da altri client. |Se è stata rilasciata sessione hello in hello provvisorio potrebbero contribuire a tentativi. |
| [TransactionSizeExceededException](/dotnet/api/microsoft.servicebus.messaging.transactionsizeexceededexception) |Troppe operazioni fanno parte della transazione hello. |Ridurre il numero di hello delle operazioni che fanno parte di questa transazione. |Ripetere l'operazione non serve. |
| [MessagingEntityDisabledException](/dotnet/api/microsoft.servicebus.messaging.messagingentitydisabledexception) |È stata inoltrata una richiesta per un'operazione di runtime su un'entità disattivata. |Attivare entità hello. |Se è stata attivata entità hello in hello provvisorio potrebbero contribuire a tentativi. |
| [NoMatchingSubscriptionException](/dotnet/api/microsoft.servicebus.messaging.nomatchingsubscriptionexception) |Se si invia un argomento di tooa messaggio che ha abilitato il filtro preliminare e nessuno dei filtri hello corrisponde, Bus di servizio restituisce l'eccezione. |Assicurarsi che almeno un filtro corrisponda. |Ripetere l'operazione non serve. |
| [MessageSizeExceededException](/dotnet/api/microsoft.servicebus.messaging.messagesizeexceededexception) |Un payload del messaggio supera il limite di 256 KB hello. Notare che tale limite di 256 KB hello hello dimensione totale dei messaggi, che può includere le proprietà di sistema e l'eventuale overhead .NET. |Ridurre le dimensioni di hello del payload dei messaggi hello, quindi ripetere l'operazione di hello. |Ripetere l'operazione non serve. |
| [TransactionException](https://msdn.microsoft.com/library/system.transactions.transactionexception.aspx) |transazione di ambiente Hello (*Current*) non è valido. È possibile che nel frattempo sia stata interrotta o completata. L'eccezione interna può fornire informazioni aggiuntive. | |Ripetere l'operazione non serve. |
| [TransactionInDoubtException](https://msdn.microsoft.com/library/system.transactions.transactionindoubtexception.aspx) |In una transazione in dubbio, viene tentata un'operazione o viene effettuato un tentativo di transazione hello toocommit, hello diventa in dubbio. |L'applicazione deve gestire questa eccezione (come un caso speciale), come transazione hello potrebbe essere stato già eseguito il commit. |- |

## <a name="quotaexceededexception"></a>QuotaExceededException
[QuotaExceededException](/dotnet/api/microsoft.servicebus.messaging.quotaexceededexception) indica che è stata superata la quota di un'entità specifica.

### <a name="queues-and-topics"></a>Code e argomenti
Per le code e argomenti, si tratta spesso di dimensioni hello della coda di hello. proprietà messaggio di errore Hello conterrà ulteriori dettagli, come in hello di esempio seguente:

```
Microsoft.ServiceBus.Messaging.QuotaExceededException
Message: hello maximum entity size has been reached or exceeded for Topic: ‘xxx-xxx-xxx’. 
    Size of entity in bytes:1073742326, Max entity size in bytes:
1073741824..TrackingId:xxxxxxxxxxxxxxxxxxxxxxxxxx, TimeStamp:3/15/2013 7:50:18 AM
```

il messaggio Hello indica che tale argomento hello superato il limite di dimensione, in questo caso 1 GB (limite di dimensione predefinito hello). 

### <a name="namespaces"></a>Spazi dei nomi

Per gli spazi dei nomi, [QuotaExceededException](/dotnet/api/microsoft.servicebus.messaging.quotaexceededexception) può indicare che un'applicazione ha superato numero massimo di hello dello spazio dei nomi tooa connessioni. ad esempio:

```
Microsoft.ServiceBus.Messaging.QuotaExceededException: ConnectionsQuotaExceeded for namespace xxx.
<tracking-id-guid>_G12 ---> 
System.ServiceModel.FaultException`1[System.ServiceModel.ExceptionDetail]: 
ConnectionsQuotaExceeded for namespace xxx.
```

#### <a name="common-causes"></a>Cause comuni
Esistono due cause più comuni di questo errore: hello coda di messaggi non recapitabili e dei destinatari dei messaggi non funzionante.

1. **Coda di messaggi non recapitabili** un lettore non è possibile eseguire toocomplete messaggi e messaggi hello vengono restituiti toohello coda/argomento quando scade il blocco di hello. Questa situazione può verificarsi se il lettore hello rileva un'eccezione che ne impedisce la chiamata [BrokeredMessage.Complete](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.brokeredmessage.complete.aspx). Dopo che un messaggio è stato letto 10 volte, per impostazione predefinita viene spostato toohello non recapitabili. Questo comportamento è controllato da hello [QueueDescription.MaxDeliveryCount](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.queuedescription.maxdeliverycount.aspx) proprietà e ha un valore predefinito di 10. Come messaggi accumuleranno nella coda non recapitabili hello, spazio occupato.
   
    problema di hello tooresolve, messaggi hello completa e di lettura dalla coda di messaggi non recapitabili hello, come si sarebbe da un'altra coda. Hello [QueueClient](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.queueclient.aspx) classe contiene anche un [FormatDeadLetterPath](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.queueclient.formatdeadletterpath.aspx) il percorso della coda di messaggi non recapitabili hello di metodo toohelp formato.
2. **Interruzione da parte del destinatario** : un destinatario ha interrotto la ricezione di messaggi da una coda o da una sottoscrizione. Hello tooidentify modo tratta toolook in hello [QueueDescription.MessageCountDetails](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.queuedescription.messagecountdetails.aspx) proprietà, che consente di visualizzare hello composizione completa di messaggi hello. Se hello [ActiveMessageCount](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.messagecountdetails.activemessagecount.aspx) proprietà è elevato o crescente e quindi messaggi hello non vengono letti più velocemente sta scritti.

### <a name="event-hubs"></a>Hub eventi
Hub eventi ha un limite di 20 gruppi di utenti per Hub eventi. Quando si tenta di toocreate altre, si riceve un [QuotaExceededException](/dotnet/api/microsoft.servicebus.messaging.quotaexceededexception). 

## <a name="timeoutexception"></a>TimeoutException
Oggetto [TimeoutException](https://msdn.microsoft.com/library/system.timeoutexception.aspx) indica che un'operazione avviata dall'utente richiede più di hello timeout dell'operazione. 

È necessario controllare il valore di hello di hello [ServicePointManager. DefaultConnectionLimit](https://msdn.microsoft.com/library/system.net.servicepointmanager.defaultconnectionlimit) proprietà, come raggiunge questo limite può essere causato anche un [TimeoutException](https://msdn.microsoft.com/library/system.timeoutexception.aspx).

### <a name="queues-and-topics"></a>Code e argomenti
Per le code e argomenti, non viene specificato il timeout di hello in hello [MessagingFactorySettings.OperationTimeout](/dotnet/api/microsoft.servicebus.messaging.messagingfactorysettings#Microsoft_ServiceBus_Messaging_MessagingFactorySettings_OperationTimeout) proprietà, come parte della stringa di connessione hello o tramite [ServiceBusConnectionStringBuilder](/dotnet/api/microsoft.servicebus.servicebusconnectionstringbuilder). messaggio di errore Hello stesso può variare, ma contiene sempre il valore di timeout hello specificato per l'operazione corrente hello. 

### <a name="event-hubs"></a>Hub eventi
Per gli hub di eventi, il timeout di hello è specificato come parte della stringa di connessione hello o tramite [ServiceBusConnectionStringBuilder](/dotnet/api/microsoft.servicebus.servicebusconnectionstringbuilder). messaggio di errore Hello stesso può variare, ma contiene sempre il valore di timeout hello specificato per l'operazione corrente hello. 

### <a name="common-causes"></a>Cause comuni
Per questo errore, esistono due cause comuni: una configurazione errata o un errore temporaneo del servizio.

1. **Configurazione errata** hello timeout dell'operazione potrebbe essere troppo piccolo per la condizione operativa hello. il valore predefinito Hello per timeout dell'operazione hello in SDK client hello è 60 secondi. Verificare toosee se il codice ha il valore di hello impostato toosomething troppo piccolo. Si noti la condizione di hello della rete hello e l'utilizzo della CPU può influire hello tempo richiesto per toocomplete una particolare operazione, in modo hello timeout dell'operazione non deve essere impostato valore estremamente ridotto tooa.
2. **Errore del servizio temporaneo** talvolta hello servizio Bus di servizio può subire ritardi nell'elaborazione delle richieste, ad esempio, durante i periodi di traffico elevato. In questi casi, è possibile ritentare l'operazione dopo un ritardo, fino a quando non hello operazione ha esito positivo. Hello stessa operazione non riesce dopo diversi tentativi, visitare hello [sito lo stato dei servizi Azure](https://azure.microsoft.com/status/) toosee se sono presenti eventuali interruzioni di servizio noto.

## <a name="next-steps"></a>Passaggi successivi

Per riferimento di API .NET di Service Bus hello completo, vedere hello [riferimenti alle API .NET di Azure](/dotnet/api/overview/azure/servicebus).

toolearn ulteriori informazioni sulla [Bus di servizio](https://azure.microsoft.com/services/service-bus/), vedere i seguenti argomenti hello.

* [Panoramica della messaggistica del bus di servizio](service-bus-messaging-overview.md)
* [Dati fondamentali del bus di servizio](service-bus-fundamentals-hybrid-solutions.md)
* [Architettura del bus di servizio](service-bus-architecture.md)

