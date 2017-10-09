---
title: eccezioni di inoltro aaaAzure e come tooresolve li | Documenti Microsoft
description: Ottenere un elenco di eccezioni di inoltro di Azure e azioni consigliate da eseguire toohelp risolverli.
services: service-bus-relay
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 5f9dd02c-cce0-43b3-8eb8-744f0c27f38c
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/23/2017
ms.author: sethm
ms.openlocfilehash: de417c8e9e43407ef355fd44f6170cf2cdc46d6d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-relay-exceptions"></a>Eccezioni del servizio di inoltro di Azure

In questo articolo sono elencate alcune eccezioni che potrebbero essere generate da hello Azure inoltro API. Questo riferimento è soggetto toochange, quindi cercare nuovamente gli aggiornamenti.

## <a name="exception-categories"></a>Categorie di eccezioni

le API di inoltro Hello generano eccezioni che potrebbero rientrare in hello seguenti categorie. Sono inoltre elencati suggeriti che consentono di risolvere toohelp eccezioni hello.

*   **Errore nella codifica dell'utente**: [System.ArgumentException](https://msdn.microsoft.com/library/system.argumentexception.aspx), [System.InvalidOperationException](https://msdn.microsoft.com/library/system.invalidoperationexception.aspx), [System.OperationCanceledException](https://msdn.microsoft.com/library/system.operationcanceledexception.aspx), [System.Runtime.Serialization.SerializationException](https://msdn.microsoft.com/library/system.runtime.serialization.serializationexception.aspx). 

    **Azione generale**: provare codice hello toofix prima di procedere.
*   **Errore di installazione/configurazione**: [System.UnauthorizedAccessException](https://msdn.microsoft.com/library/system.unauthorizedaccessexception.aspx). 

    **Azione generale**: controllare la configurazione. Se necessario, modificare la configurazione hello.
*   **Eccezioni temporanee**: [Microsoft.ServiceBus.Messaging.MessagingException](/dotnet/api/microsoft.servicebus.messaging.messagingexception), [Microsoft.ServiceBus.Messaging.ServerBusyException](/dotnet/api/microsoft.servicebus.messaging.serverbusyexception), [Microsoft.ServiceBus.Messaging.MessagingCommunicationException](/dotnet/api/microsoft.servicebus.messaging.messagingcommunicationexception). 

    **Azione generale**: hello riprovare o inviare notifiche agli utenti.
*   **Altre eccezioni**: [System.Transactions.TransactionException](https://msdn.microsoft.com/library/system.transactions.transactionexception.aspx), [System.TimeoutException](https://msdn.microsoft.com/library/system.timeoutexception.aspx). 

    **Azione generale**: tipo di eccezione toohello specifico. Vedere la tabella hello nella seguente sezione hello. 

## <a name="exception-types"></a>Tipi di eccezioni

Hello nella tabella seguente sono elencati i tipi di eccezione messaggistica e le relative cause. Viene inoltre rilevato suggerite azioni da eseguire resolve toohelp eccezioni hello.

| **Tipo di eccezione** | **Descrizione** | **Azione suggerita** | **Nota sulla ripetizione automatica o immediata** |
| --- | --- | --- | --- |
| [Timeout](https://msdn.microsoft.com/library/system.timeoutexception.aspx) |Hello server non ha risposto toohello richiesto operazione all'interno di hello specificato, controllato dai [OperationTimeout](/dotnet/api/microsoft.servicebus.messaging.messagingfactorysettings.operationtimeout). Hello server potrebbe essere stato completato hello richiesto operazione. Questa situazione può verificarsi a causa di toonetwork o altri ritardi di infrastruttura. |Verificare la coerenza dello stato del sistema hello e quindi riprovare, se necessario. Vedere [TimeoutException](#timeoutexception). |Riprova utili in alcuni casi; aggiungere toocode logica di ripetizione. |
| [Operazione non valida](https://msdn.microsoft.com/library/system.invalidoperationexception.aspx) |Hello ha richiesto l'operazione dell'utente non è consentita all'interno di server hello o un servizio. Messaggio di eccezione hello per informazioni dettagliate, vedere. |Controllare il codice hello e la documentazione di hello. Verificare che tale hello ha richiesto l'operazione è valida. |Ripetere l'operazione non serve. |
| [Operazione annullata](https://msdn.microsoft.com/library/system.operationcanceledexception.aspx) |Viene eseguito un tentativo effettuato tooinvoke un'operazione su un oggetto che è già stata chiusa, interrotta o eliminato. In rari casi, transazione di ambiente hello è già stata eliminata. |Controllare il codice hello e assicurarsi che non vengono richiamate le operazioni su un oggetto eliminato. |Ripetere l'operazione non serve. |
| [Accesso non autorizzato](https://msdn.microsoft.com/library/system.unauthorizedaccessexception.aspx) |Hello [TokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider) oggetto non è stato possibile acquisire un token, hello token non è valido o hello token non contiene hello attestazioni necessarie tooperform hello operazione. |Verificare che il provider di token hello viene creato con i valori corretti di hello. Controllare la configurazione di hello di hello servizio controllo di accesso. |Riprova utili in alcuni casi; aggiungere toocode logica di ripetizione. |
| [Eccezione di argomento](https://msdn.microsoft.com/library/system.argumentexception.aspx)<br /> [Argomento Null](https://msdn.microsoft.com/library/system.argumentnullexception.aspx)<br />[Argomento non compreso nell'intervallo](https://msdn.microsoft.com/library/system.argumentoutofrangeexception.aspx) |Uno o più dei seguenti hello si è verificato:<br />Metodo di toohello uno o più argomenti forniti non sono validi.<br /> Hello URI fornito troppo[NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) o [crea](/dotnet/api/microsoft.servicebus.messaging.messagingfactory.create) contiene uno o più segmenti di percorso.<br />schema URI Hello fornito troppo[NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) o [crea](/dotnet/api/microsoft.servicebus.messaging.messagingfactory.create) non è valido. <br />valore della proprietà Hello è maggiore di 32 KB. |Controllare il codice chiamante hello e verificare che gli argomenti di hello siano corretti. |Ripetere l'operazione non serve. |
| [Server occupato](/dotnet/api/microsoft.servicebus.messaging.serverbusyexception) |Servizio non è richiesta hello in grado di tooprocess in questo momento. |client Hello può attendere un periodo di tempo, quindi ripetere l'operazione di hello. |client Hello può riprovare dopo un intervallo specifico. Se un nuovo tentativo genera un'eccezione diversa, controllare il comportamento di ripetizione hello di tale eccezione. |
| [Quota superata](/dotnet/api/microsoft.servicebus.messaging.quotaexceededexception) |entità di messaggistica Hello ha raggiunto la dimensione massima consentita. |Creare spazio nell'entità hello dalla ricezione di messaggi da entità hello o le relative code secondarie. Vedere [QuotaExceededException](#quotaexceededexception). |Riprova potrebbe risultare utile se i messaggi sono state rimosse in hello frattempo. |
| [Dimensione del messaggio superata](/dotnet/api/microsoft.servicebus.messaging.messagesizeexceededexception) |Un payload del messaggio supera il limite di 256 KB hello. Si noti che il limite di 256 KB hello è hello dimensione totale dei messaggi. dimensione totale di messaggi Hello può includere proprietà del sistema e il sovraccarico di Microsoft .NET. |Ridurre le dimensioni di hello del payload dei messaggi hello, quindi ripetere l'operazione di hello. |Ripetere l'operazione non serve. |

## <a name="quotaexceededexception"></a>QuotaExceededException

[QuotaExceededException](/dotnet/api/microsoft.servicebus.messaging.quotaexceededexception) indica che è stata superata la quota di un'entità specifica.

Per l'inoltro, questa eccezione esegue il wrapping di hello [QuotaExceededException](https://msdn.microsoft.com/library/system.servicemodel.quotaexceededexception.aspx), che indica il numero massimo di hello del listener è stato superato per l'endpoint. Viene indicato in hello **MaximumListenersPerEndpoint** valore del messaggio di eccezione hello.

## <a name="timeoutexception"></a>TimeoutException
Oggetto [TimeoutException](https://msdn.microsoft.com/library/system.timeoutexception.aspx) indica che un'operazione avviata dall'utente richiede più di hello timeout dell'operazione. 

Controllare il valore di hello di hello [ServicePointManager. DefaultConnectionLimit](https://msdn.microsoft.com/library/system.net.servicepointmanager.defaultconnectionlimit) proprietà. Il raggiungimento di questo limite può causare una [TimeoutException](https://msdn.microsoft.com/library/system.timeoutexception.aspx).

Per l'inoltro è possibile ricevere eccezioni di timeout alla prima apertura di una connessione di inoltro del mittente. Questa eccezione può essere dovuta a due cause comuni:

*   Hello [OpenTimeout](https://msdn.microsoft.com/library/wcf.opentimeout.aspx) valore potrebbe essere troppo piccolo (se anche da una frazione di secondo).
* Un listener di inoltro locale potrebbe essere non risponde oppure si verifichino problemi di regole firewall che impediscono ai listener di accettare nuove connessioni client, hello e [OpenTimeout](https://msdn.microsoft.com/library/wcf.opentimeout.aspx) valore è minore di circa 20 secondi.

Esempio:

```
'System.TimeoutException’: hello operation did not complete within hello allotted timeout of 00:00:10.
hello time allotted toothis operation may have been a portion of a longer timeout.
```

### <a name="common-causes"></a>Cause comuni
Questo errore può essere dovuto a due cause comuni:

*   **Configurazione non corretta**
    
    timeout dell'operazione Hello potrebbero essere troppo piccole per condizione operativa hello. il valore predefinito Hello per timeout dell'operazione hello in SDK client hello è 60 secondi. Controllare toosee se hello nel codice è impostato toosomething troppo piccolo. Si noti che la condizione hello e utilizzo di CPU della rete hello può influire sulla hello tempo richiesto per un'operazione toocomplete. È consigliabile non tooset hello operazione tooa molto piccolo valore di timeout.
*   **Errore temporaneo del servizio**

    In alcuni casi, il servizio di inoltro hello potrebbe verificarsi ritardi nell'elaborazione delle richieste. Questo può accadere, ad esempio, durante i periodi di traffico elevato. In questo caso, ripetere l'operazione dopo un ritardo, fino a quando non hello operazione ha esito positivo. Se hello stessa operazione continua toofail dopo più tentativi, controllare hello [sito lo stato dei servizi Azure](https://azure.microsoft.com/status/) toosee se sono presenti noti interruzioni del servizio.

## <a name="next-steps"></a>Passaggi successivi
* [Domande frequenti sul servizio di inoltro di Azure](relay-faq.md)
* [Creare uno spazio dei nomi di inoltro](relay-create-namespace-portal.md)
* [Introduzione al servizio di inoltro di Azure e .NET](relay-hybrid-connections-dotnet-get-started.md)
* [Introduzione al servizio di inoltro di Azure e al nodo](relay-hybrid-connections-node-get-started.md)

