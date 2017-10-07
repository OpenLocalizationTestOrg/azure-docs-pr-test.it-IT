---
title: Hub di eventi aaaAzure eccezioni di messaggistica | Documenti Microsoft
description: Elenco delle eccezioni di messaggistica di Hub eventi di Azure e relative azioni consigliate.
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 2c6273de-0106-47e5-b45d-59040e51f2c5
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: 9c164e76612c26607219f08407f689aaab4050a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="event-hubs-messaging-exceptions"></a>Eccezioni della messaggistica di Hub eventi
In questo articolo sono elencate alcune delle eccezioni hello generate da hello Azure Service Bus API, che includono gli hub di eventi di messaggistica. Questo riferimento è soggetto toochange, quindi cercare nuovamente gli aggiornamenti.

## <a name="exception-categories"></a>Categorie di eccezioni
le API di hub eventi Hello generare le eccezioni che possono rientrano nelle seguenti categorie di hello, insieme azione hello associato è possibile eseguire tootry toofix li.

1. Errore nella codifica dell'utente: [System.ArgumentException](https://msdn.microsoft.com/library/system.argumentexception.aspx), [System.InvalidOperationException](https://msdn.microsoft.com/library/system.invalidoperationexception.aspx), [System.OperationCanceledException](https://msdn.microsoft.com/library/system.operationcanceledexception.aspx), [System.Runtime.Serialization.SerializationException](https://msdn.microsoft.com/library/system.runtime.serialization.serializationexception.aspx). Azione generale: provare toofix hello codice prima di procedere.
2. Errore di configurazione/installazione: [Microsoft.ServiceBus.Messaging.MessagingEntityNotFoundException](/dotnet/api/microsoft.servicebus.messaging.messagingentitynotfoundexception), [Microsoft.Azure.EventHubs.MessagingEntityNotFoundException](/dotnet/api/microsoft.azure.eventhubs.messagingentitynotfoundexception), [System.UnauthorizedAccessException](https://msdn.microsoft.com/library/system.unauthorizedaccessexception.aspx). Azione generale: controllare la configurazione e modificarla, se necessario.
3. Eccezioni temporanee: [Microsoft.ServiceBus.Messaging.MessagingException](/dotnet/api/microsoft.servicebus.messaging.messagingexception), [Microsoft.ServiceBus.Messaging.ServerBusyException](#serverbusyexception), [Microsoft.Azure.EventHubs.ServerBusyException](#serverbusyexception), [Microsoft.ServiceBus.Messaging.MessagingCommunicationException](/dotnet/api/microsoft.servicebus.messaging.messagingcommunicationexception). Azione generale: hello riprovare o inviare notifiche agli utenti.
4. Altre eccezioni: [System.Transactions.TransactionException](https://msdn.microsoft.com/library/system.transactions.transactionexception.aspx), [System.TimeoutException](#timeoutexception), [Microsoft.ServiceBus.Messaging.MessageLockLostException](/dotnet/api/microsoft.servicebus.messaging.messagelocklostexception), [Microsoft.ServiceBus.Messaging.SessionLockLostException](/dotnet/api/microsoft.servicebus.messaging.sessionlocklostexception). Azione generale: tipo di eccezione specifico toohello; consultare la tabella toohello nella seguente sezione hello. 

## <a name="exception-types"></a>Tipi di eccezioni
Hello nella tabella seguente elenca messaggistica i tipi di eccezione e le cause e Azione suggerita di note che è possibile eseguire.

| **Tipo di eccezione** | **Descrizione/Causa/Esempi** | **Azione suggerita** | **Nota sulla ripetizione automatica/immediata** |
| --- | --- | --- | --- |
| [TimeoutException](https://msdn.microsoft.com/library/system.timeoutexception.aspx) |Hello server non ha risposto toohello richiesto operazione all'interno di hello specificato, controllato dai [OperationTimeout](/dotnet/api/microsoft.servicebus.messaging.messagingfactorysettings#Microsoft_ServiceBus_Messaging_MessagingFactorySettings_OperationTimeout). server Hello potrebbe essere stata completata l'operazione di richiesta di hello. Questa situazione può verificarsi a causa di toonetwork o altri ritardi di infrastruttura. |Verificare la coerenza dello stato del sistema hello e ripetere se necessario.<br /> Vedere [TimeoutException](#timeoutexception). |Riprova utili in alcuni casi; aggiungere toocode logica di ripetizione. |
| [InvalidOperationException](https://msdn.microsoft.com/library/system.invalidoperationexception.aspx) |Hello ha richiesto l'operazione dell'utente non è consentita all'interno di server hello o un servizio. Messaggio di eccezione hello per informazioni dettagliate, vedere. Ad esempio, [completa](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete) genera questa eccezione se è stato ricevuto il messaggio hello in [ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode) modalità. |Controllare il codice hello e la documentazione di hello. Verificare che hello ha richiesto l'operazione è valida. |Ripetere l'operazione non serve. |
| [OperationCanceledException](https://msdn.microsoft.com/library/system.operationcanceledexception.aspx) |Viene eseguito un tentativo effettuato tooinvoke un'operazione su un oggetto che è già stata chiusa, interrotta o eliminata. In rari casi, transazione di ambiente hello è già stata eliminata. |Controllare il codice hello e assicurarsi che non vengono richiamate le operazioni su un oggetto eliminato. |Ripetere l'operazione non serve. |
| [UnauthorizedAccessException](https://msdn.microsoft.com/library/system.unauthorizedaccessexception.aspx) |Hello [TokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider) oggetto non è stato possibile acquisire un token, hello token non è valido o hello token non contiene hello attestazioni necessarie tooperform hello operazione. |Assicurarsi che i provider di token hello viene creato con i valori corretti di hello. Controllare la configurazione di hello di hello servizio controllo di accesso. |Riprova utili in alcuni casi; aggiungere toocode logica di ripetizione. |
| [ArgumentException](https://msdn.microsoft.com/library/system.argumentexception.aspx)<br /> [ArgumentNullException](https://msdn.microsoft.com/library/system.argumentnullexception.aspx)<br />[ArgumentOutOfRangeException](https://msdn.microsoft.com/library/system.argumentoutofrangeexception.aspx) |Metodo di toohello uno o più argomenti forniti non sono validi. Hello URI fornito troppo[NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) o [crea](/dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_Create_System_Collections_Generic_IEnumerable_System_Uri__) contiene ai segmenti di percorso. schema URI Hello fornito troppo[NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) o [crea](/dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_Create_System_Collections_Generic_IEnumerable_System_Uri__) non è valido. valore della proprietà Hello è maggiore di 32KB. |Controllare il codice chiamante hello e verificare che gli argomenti di hello siano corretti. |Ripetere l'operazione non serve. |
| [Microsoft.ServiceBus.Messaging.MessagingEntityNotFoundException](/dotnet/api/microsoft.servicebus.messaging.messagingentitynotfoundexception) <br /> [Microsoft.Azure.EventHubs.MessagingEntityNotFoundException](/dotnet/api/microsoft.azure.eventhubs.messagingentitynotfoundexception) |Entità associato all'operazione hello non esiste o è stato eliminato. |Verificare che l'entità hello esiste. |Ripetere l'operazione non serve. |
| [MessageNotFoundException](/dotnet/api/microsoft.servicebus.messaging.messagenotfoundexception) |Tenta di tooreceive un messaggio con un numero di sequenza particolare. Non è stato trovato questo messaggio. |Verificare che il messaggio hello non è già stato ricevuto. Controllare toosee coda di messaggi non recapitabili hello se il messaggio hello è stato superato. |Ripetere l'operazione non serve. |
| [MessagingCommunicationException](/dotnet/api/microsoft.servicebus.messaging.messagingcommunicationexception) |Client non è in grado di tooestablish tooEvent una connessione Hub. |Verificare che il nome di host hello fornito sia corretto e hello host è raggiungibile. |Se sono presenti problemi di connettività intermittente, può essere utile ripetere l'operazione. |
| [Microsoft.ServiceBus.Messaging.ServerBusyException](/dotnet/api/microsoft.servicebus.messaging.serverbusyexception) <br /> [Microsoft.Azure.EventHubs.ServerBusyException](/dotnet/api/microsoft.azure.eventhubs.serverbusyexception) |Servizio non è richiesta hello in grado di tooprocess in questo momento. |Client può attendere un periodo di tempo, quindi ripetere l'operazione di hello. <br /> Vedere [ServerBusyException](#serverbusyexception). |Il client può riprovare dopo un determinato intervallo. Se viene generata un'eccezione diversa, controllare il comportamento di ripetizione del tentativo della nuova eccezione. |
| [MessageLockLostException](/dotnet/api/microsoft.servicebus.messaging.messagelocklostexception) |Token di blocco associato al messaggio hello è scaduto o non viene trovato il token di blocco hello. |Eliminare il messaggio hello. |Ripetere l'operazione non serve. |
| [SessionLockLostException](/dotnet/api/microsoft.servicebus.messaging.sessionlocklostexception) |È stato perso il blocco associato a questa sessione. | Interrompere hello [MessageSession](/dotnet/api/microsoft.servicebus.messaging.messagesession) oggetto. |Ripetere l'operazione non serve. |
| [MessagingException](/dotnet/api/microsoft.servicebus.messaging.messagingexception) |Eccezione generata in hello seguenti casi di messaggistica generica: viene effettuato un tentativo di toocreate un [QueueClient](/dotnet/api/microsoft.servicebus.messaging.queueclient) con un nome o percorso al quale appartiene il tipo di entità diversa tooa (ad esempio, un argomento). Il tentativo è ingrandita toosend un messaggio a 256KB. server Hello o un servizio ha rilevato un errore durante l'elaborazione della richiesta di hello. Vedere il messaggio di eccezione hello per informazioni dettagliate. Si tratta in genere di un'eccezione temporanea. |Controllare il codice hello e assicurarsi che solo gli oggetti serializzabili vengono usati per il corpo del messaggio hello o usare un serializzatore personalizzato. Controllare la documentazione di hello per i tipi di valore hello supportato di proprietà hello e solo i tipi di utilizzo è supportato. Controllare hello [IsTransient](/dotnet/api/microsoft.servicebus.messaging.messagingexception#Microsoft_ServiceBus_Messaging_MessagingException_IsTransient) proprietà. Se è **true**, è possibile ritentare l'operazione di hello. |Il comportamento di ripetizione dei tentativi non è definito e ripetere l'operazione può non essere utile. |
| [MessagingEntityAlreadyExistsException](/dotnet/api/microsoft.servicebus.messaging.messagingentityalreadyexistsexception) |Tentativo toocreate un'entità con un nome che è già utilizzato da un'altra entità nello spazio dei nomi del servizio. |Eliminare un'entità esistente hello o scegliere un nome diverso per hello entità toobe creato. |Ripetere l'operazione non serve. |
| [QuotaExceededException](/dotnet/api/microsoft.servicebus.messaging.quotaexceededexception) |entità di messaggistica Hello ha raggiunto la dimensione massima consentita. Questa situazione può verificarsi se hello massimo di ricevitori (ovvero 5) è già stato aperto un livello di gruppo per ogni consumer. |Liberare spazio nell'entità hello dal relativo code secondarie o di ricezione di messaggi da entità hello. <br /> Vedere [QuotaExceededException](#quotaexceededexception) |Riprova potrebbe risultare utile se i messaggi sono state rimosse in hello frattempo. |
|  | | | |
| [SessionCannotBeLockedException](/dotnet/api/microsoft.servicebus.messaging.sessioncannotbelockedexception) |Tentativo di tooaccept che una sessione con un ID di sessione specifiche, ma la sessione hello è attualmente bloccata da un altro client. |Verificare che la sessione hello è sbloccata da altri client. |Se è stata rilasciata sessione hello in hello provvisorio potrebbero contribuire a tentativi. |
| [TransactionSizeExceededException](/dotnet/api/microsoft.servicebus.messaging.transactionsizeexceededexception) |Troppe operazioni fanno parte della transazione hello. |Ridurre il numero di hello delle operazioni che fanno parte di questa transazione. |Ripetere l'operazione non serve. |
| [MessagingEntityDisabledException](/dotnet/api/microsoft.servicebus.messaging.messagingentitydisabledexception) |È stata inoltrata una richiesta per un'operazione di runtime su un'entità disattivata. |Attivare entità hello. |Se è stata attivata entità hello in hello provvisorio potrebbero contribuire a tentativi. |
| [Microsoft.ServiceBus.Messaging.MessageSizeExceededException](/dotnet/api/microsoft.servicebus.messaging.messagesizeexceededexception) <br /> [Microsoft.Azure.EventHubs.MessageSizeExceededException](/dotnet/api/microsoft.azure.eventhubs.messagesizeexceededexception) | Un payload del messaggio supera il limite di 256 KB hello. Si noti che il limite hello 256K è hello dimensione totale dei messaggi, che può includere le proprietà di sistema e il sovraccarico di .NET. |Ridurre le dimensioni di hello del payload dei messaggi hello, quindi ripetere l'operazione di hello. |Ripetere l'operazione non serve. |
| [TransactionException](https://msdn.microsoft.com/library/system.transactions.transactionexception.aspx) |transazione di ambiente Hello (*Current*) non è valido. È possibile che nel frattempo sia stata interrotta o completata. L'eccezione interna può fornire informazioni aggiuntive. | |Ripetere l'operazione non serve. |
| [TransactionInDoubtException](https://msdn.microsoft.com/library/system.transactions.transactionindoubtexception.aspx) |In una transazione in dubbio, viene tentata un'operazione o viene effettuato un tentativo di transazione hello toocommit, hello diventa in dubbio. |L'applicazione deve gestire questa eccezione (come un caso speciale), come transazione hello potrebbe essere stato già eseguito il commit. |- |

## <a name="quotaexceededexception"></a>QuotaExceededException
[QuotaExceededException](/dotnet/api/microsoft.servicebus.messaging.quotaexceededexception) indica che è stata superata la quota di un'entità specifica.

Questa situazione può verificarsi se il numero massimo di hello di ricevitori (5) è già stato aperto un livello di gruppo per ogni consumer.

### <a name="event-hubs"></a>Hub eventi
Hub eventi ha un limite di 20 gruppi di utenti per Hub eventi. Quando si tenta di toocreate altre, si riceve un [QuotaExceededException](/dotnet/api/microsoft.servicebus.messaging.quotaexceededexception). 

## <a name="timeoutexception"></a>TimeoutException
Oggetto [TimeoutException](https://msdn.microsoft.com/library/system.timeoutexception.aspx) indica che un'operazione avviata dall'utente richiede più di hello timeout dell'operazione. 

Per gli hub di eventi, il timeout di hello è specificato come parte della stringa di connessione hello o tramite [ServiceBusConnectionStringBuilder](/dotnet/api/microsoft.servicebus.servicebusconnectionstringbuilder). messaggio di errore Hello stesso può variare, ma contiene sempre il valore di timeout hello specificato per l'operazione corrente hello. 

### <a name="common-causes"></a>Cause comuni
Per questo errore, esistono due cause comuni: una configurazione errata o un errore temporaneo del servizio.

1. **Configurazione errata** hello timeout dell'operazione potrebbe essere troppo piccolo per la condizione operativa hello. il valore predefinito Hello per timeout dell'operazione hello in SDK client hello è 60 secondi. Verificare toosee se il codice ha il valore di hello impostato toosomething troppo piccolo. Si noti la condizione di hello della rete hello e l'utilizzo della CPU può influire hello tempo richiesto per toocomplete una particolare operazione, in modo hello timeout dell'operazione non deve essere impostato valore estremamente ridotto tooa.
2. **Errore del servizio temporaneo** talvolta hello servizio hub eventi possa verificarsi ritardi nell'elaborazione delle richieste, ad esempio, durante i periodi di traffico elevato. In questi casi, è possibile ritentare l'operazione dopo un ritardo, fino a quando non hello operazione ha esito positivo. Hello stessa operazione non riesce dopo diversi tentativi, visitare hello [sito lo stato dei servizi Azure](https://azure.microsoft.com/status/) toosee se sono presenti eventuali interruzioni di servizio noto.

## <a name="serverbusyexception"></a>ServerBusyException

[Microsoft.ServiceBus.Messaging.ServerBusyException](/dotnet/api/microsoft.servicebus.messaging.serverbusyexception) o [Microsoft.Azure.EventHubs.ServerBusyException](/dotnet/api/microsoft.azure.eventhubs.serverbusyexception) indicano che il server è sovraccarico. Esistono due codici di errore relativi a questa eccezione.

### <a name="error-code-50002"></a>Codice di errore 50002

Questo errore può verificarsi per uno dei due motivi:

1. carico Hello non viene distribuito uniformemente tra tutte le partizioni, hello Hub eventi e le limitazioni di unità locale della velocità effettiva di una partizione riscontri hello.
    
    Risoluzione: Rivedere la strategia di distribuzione partizione hello o tentativo [EventHubClient.Send(eventDataWithOutPartitionKey)](/dotnet/api/microsoft.servicebus.messaging.eventhubclient#Microsoft_ServiceBus_Messaging_EventHubClient_Send_Microsoft_ServiceBus_Messaging_EventData_) informazioni utili.

2. spazio dei nomi di Hello hub eventi non dispone di unità di velocità effettiva sufficiente (è possibile controllare hello **metriche** pannello nel Pannello di spazio dei nomi di hub eventi in hello [portale di Azure](https://portal.azure.com) tooconfirm). Si noti che il portale di hello Mostra le informazioni aggregate (1 minuto), ma è misurare la velocità effettiva hello in tempo reale, pertanto è solo una stima.

    Risoluzione: Aumentando la velocità effettiva di hello consente unità nello spazio dei nomi hello. È possibile farlo nel portale hello hello **scala** pannello del pannello dello spazio dei nomi di hello hub eventi.

### <a name="error-code-50001"></a>Codice errore 50001

Questo errore si verifica raramente. Cui si verifica quando il contenitore di hello in esecuzione di codice per lo spazio dei nomi è basso sulla CPU, caricare gli hub di eventi non più di pochi secondi prima di hello Avvia servizio di bilanciamento.


## <a name="next-steps"></a>Passaggi successivi
Sono disponibili ulteriori informazioni sugli hub di eventi visitando hello seguenti collegamenti:

* [Panoramica di Hub eventi](event-hubs-what-is-event-hubs.md)
* [Create an Event Hub](event-hubs-create.md) (Creare un Hub eventi)
* [Domande frequenti su Hub eventi](event-hubs-faq.md)
