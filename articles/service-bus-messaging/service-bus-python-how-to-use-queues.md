---
title: Accoda aaaHow toouse Azure Service Bus con Python | Documenti Microsoft
description: Informazioni su come code di toouse Azure Service Bus da Python.
services: service-bus-messaging
documentationcenter: python
author: sethmanheim
manager: timlt
editor: 
ms.assetid: b95ee5cd-3b31-459c-a7f3-cf8bcf77858b
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm;lmazuel
ms.openlocfilehash: bceb84d04ff3445c3087a9c246c583d6630f07af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-queues-with-python"></a>La modalità di code toouse Bus di servizio con Python

[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

Questo articolo viene descritto come toouse code del Bus di servizio. esempi di Hello sono scritti in Python e utilizzare hello [pacchetto Python Azure Service Bus][Python Azure Service Bus package]. Hello scenari trattati includono **la creazione delle code, inviando e ricevendo messaggi**, e **l'eliminazione di code**.

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

> [!NOTE]
> tooinstall Python o hello [pacchetto Python Azure Service Bus][Python Azure Service Bus package], vedere hello [Guida all'installazione di Python](../python-how-to-install.md).
> 
> 

## <a name="create-a-queue"></a>Creare una coda
Hello **ServiceBusService** consente toowork con le code. Aggiungere hello codice superiore hello di qualsiasi file Python in cui si desidera accedere tooprogrammatically Bus di servizio seguente:

```python
from azure.servicebus import ServiceBusService, Message, Queue
```

Hello codice seguente viene creata una **ServiceBusService** oggetto. Sostituire, `mynamespace`, `sharedaccesskeyname` e `sharedaccesskey` con lo spazio dei nomi e il nome e il valore della chiave di firma di accesso condiviso.

```python
bus_service = ServiceBusService(
    service_namespace='mynamespace',
    shared_access_key_name='sharedaccesskeyname',
    shared_access_key_value='sharedaccesskey')
```

Hello valori per nome hello SAS e il valore sono reperibile in hello [portale di Azure] [ Azure portal] informazioni di connessione, o in Visual Studio hello **proprietà** riquadro durante la selezione Hello dello spazio dei nomi Service Bus in Esplora Server (come illustrato nella sezione precedente hello).

```python
bus_service.create_queue('taskqueue')
```

Hello `create_queue` metodo supporta inoltre opzioni aggiuntive, che consentono di impostazioni di coda toooverride predefinite, ad esempio messaggio toolive TTL (time) o dimensione massima della coda. Hello esempio seguente imposta GB too5 dimensioni massime della coda di hello e minuto too1 valore TTL di hello:

```python
queue_options = Queue()
queue_options.max_size_in_megabytes = '5120'
queue_options.default_message_time_to_live = 'PT1M'

bus_service.create_queue('taskqueue', queue_options)
```

## <a name="send-messages-tooa-queue"></a>Messaggi tooa coda di invio
una coda di Service Bus di messaggi tooa toosend, l'applicazione chiama hello `send_queue_message` metodo hello **ServiceBusService** oggetto.

Hello esempio seguente viene illustrato come toosend una coda toohello test denominati `taskqueue` utilizzando `send_queue_message`:

```python
msg = Message(b'Test Message')
bus_service.send_queue_message('taskqueue', msg)
```

Le code del Bus di servizio supportano una dimensione massima di 256 KB in hello [livello Standard](service-bus-premium-messaging.md) hello a 1 MB e [livello Premium](service-bus-premium-messaging.md). intestazione Hello, che include standard hello e le proprietà personalizzate dell'applicazione, può avere una dimensione massima di 64 KB. Non è previsto alcun limite per il numero di hello di messaggi contenuti in una coda, ma è un limite alla dimensione totale di hello di messaggi hello mantenuto da una coda. Questa dimensione della coda viene definita al momento della creazione, con un limite massimo di 5 GB. Per altre informazioni sulle quote, vedere [Quote del bus di servizio][Service Bus quotas].

## <a name="receive-messages-from-a-queue"></a>Ricevere messaggi da una coda
I messaggi vengono ricevuti da una coda utilizzando hello `receive_queue_message` metodo hello **ServiceBusService** oggetto:

```python
msg = bus_service.receive_queue_message('taskqueue', peek_lock=False)
print(msg.body)
```

I messaggi vengono eliminati dalla coda di hello quando vengono letti quando hello parametro `peek_lock` è troppo**False**. È possibile leggere (anteprima) e bloccare il messaggio hello senza eliminarla dalla coda hello dall'impostazione parametro hello `peek_lock` troppo**True**.

Hello comportamento di lettura e l'eliminazione del messaggio hello come parte di hello l'operazione di ricezione è il modello più semplice di hello e adatto per scenari in cui un'applicazione in grado di tollerare non elabora un messaggio di evento hello di un errore. toounderstand, si consideri uno scenario in cui problemi relativi ai consumer hello hello di ricezione richiesta e quindi si blocca prima dell'elaborazione. Poiché verrà contrassegnato messaggio come usato, quindi quando un'applicazione hello viene riavviata e inizia a usare nuovamente i messaggi hello del Bus di servizio, risulterà perso messaggio hello che è stato consumato toohello precedente arresto anomalo del sistema.

Se hello `peek_lock` parametro è impostato troppo**True**, hello ricezione diventa un'operazione in due fasi, che rende possibile toosupport applicazioni che non sono in grado di tollerare messaggi mancanti. Quando il Bus di servizio riceve una richiesta, individua hello successivo messaggio toobe utilizzati Blocca tooprevent altri consumer di ricezione e lo restituisce quindi toohello applicazione. Dopo l'applicazione hello completa l'elaborazione messaggio hello o archiviarlo in modo affidabile per l'elaborazione futura, completa hello seconda fase di hello processo di ricezione dal chiamante hello **eliminare** metodo hello **messaggio** oggetto. Hello **eliminare** metodo contrassegna il messaggio hello come usato, ma verrà rimosso dalla coda hello.

```python
msg = bus_service.receive_queue_message('taskqueue', peek_lock=True)
print(msg.body)

msg.delete()
```

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a>Come si blocca toohandle applicazione e i messaggi illeggibili
Bus di servizio offre funzionalità toohelp che normalmente possibile correggere gli errori nell'applicazione o problemi di elaborazione di un messaggio. Se un'applicazione ricevente è in grado di tooprocess hello messaggio per qualche motivo, quindi è possibile chiamare hello **sbloccare** metodo hello **messaggio** oggetto. Ciò causerà messaggio hello toounlock di Bus di servizio all'interno di coda hello e renderlo disponibile toobe nuovamente ricevuto, sia da hello stesso consumo dell'applicazione o da un'altra applicazione consumer.

È inoltre disponibile un timeout associato a un messaggio bloccato all'interno di coda hello e se hello ha esito negativo dell'applicazione hello tooprocess hello messaggio prima della scadenza del timeout (ad esempio, se si blocca l'applicazione hello), quindi il Bus di servizio sbloccherà il messaggio hello e renderlo disponibile toobe nuovamente ricevuto.

In hello evento hello applicazione si blocca dopo l'elaborazione messaggio hello ma prima di hello **eliminare** metodo viene chiamato, quindi il messaggio hello sarà applicazione toohello consegnati nuovamente quando si riavvia. Spesso si tratta di **almeno una volta elaborazione**, vale a dire, ogni messaggio verrà elaborato almeno una volta ma in hello determinate situazioni potrebbe essere recapitato nuovamente stesso messaggio. Se hello scenario non tollera la doppia elaborazione, gli sviluppatori di applicazioni devono aggiungere logica aggiuntiva tootheir applicazione toohandle duplicato il recapito dei messaggi. Questa operazione viene spesso eseguita utilizzando hello **MessageId** proprietà di messaggio hello che rimangono costante tra i tentativi di recapito.

## <a name="next-steps"></a>Passaggi successivi
Ora che si è appreso i concetti di base di hello di code del Bus di servizio, vedere questi toolearn articoli più.

* [Code, argomenti e sottoscrizioni del bus di servizio][Queues, topics, and subscriptions]

[Azure portal]: https://portal.azure.com
[Python Azure Service Bus package]: https://pypi.python.org/pypi/azure-servicebus  
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[Service Bus quotas]: service-bus-quotas.md

