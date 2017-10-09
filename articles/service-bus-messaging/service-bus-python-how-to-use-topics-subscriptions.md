---
title: gli argomenti del Bus di servizio di Azure toouse aaaHow con Python | Documenti Microsoft
description: Informazioni su come toouse Azure Service Bus argomenti e sottoscrizioni da Python.
services: service-bus-messaging
documentationcenter: python
author: sethmanheim
manager: timlt
editor: 
ms.assetid: c4f1d76c-7567-4b33-9193-3788f82934e4
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm
ms.openlocfilehash: 1171cbe8061bb3d73e2ce92ecc0cf45afae37054
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-topics-and-subscriptions-with-python"></a>Il Bus di servizio toouse argomenti e sottoscrizioni con Python

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

Questo articolo viene descritto come toouse Bus di servizio di argomenti e sottoscrizioni. esempi di Hello sono scritti in Python e utilizzare hello [pacchetto Python di Azure SDK][Azure Python package]. Hello scenari trattati includono **la creazione di argomenti e sottoscrizioni**, **creazione filtri di sottoscrizione**, **invio argomento tooa messaggi**, **ricezione i messaggi da una sottoscrizione**, e **l'eliminazione di argomenti e sottoscrizioni**. Per ulteriori informazioni su argomenti e sottoscrizioni, vedere hello [passaggi successivi](#next-steps) sezione.

[!INCLUDE [howto-service-bus-topics](../../includes/howto-service-bus-topics.md)]

> [!NOTE] 
> Se è necessario tooinstall Python o hello [pacchetto Python Azure][Azure Python package], vedere hello [Guida all'installazione di Python](../python-how-to-install.md).

## <a name="create-a-topic"></a>Creare un argomento
Hello **ServiceBusService** consente toowork con argomenti. Aggiungere il seguente hello superiore hello di qualsiasi file Python in cui si desidera accedere tooprogrammatically Bus di servizio:

```python
from azure.servicebus import ServiceBusService, Message, Topic, Rule, DEFAULT_RULE_NAME
```

Hello codice seguente viene creata una **ServiceBusService** oggetto. Sostituire `mynamespace`, `sharedaccesskeyname` e `sharedaccesskey` con lo spazio dei nomi effettivo e il nome e il valore della chiave di firma di accesso condiviso.

```python
bus_service = ServiceBusService(
    service_namespace='mynamespace',
    shared_access_key_name='sharedaccesskeyname',
    shared_access_key_value='sharedaccesskey')
```

È possibile ottenere i valori hello per nome della chiave SAS hello e il valore da hello [portale di Azure][Azure portal].

```python
bus_service.create_topic('mytopic')
```

Hello `create_topic` metodo supporta inoltre opzioni aggiuntive, che consentono di determinare le impostazioni dell'argomento predefinito toooverride, ad esempio dimensioni argomento toolive o massimo in fase di messaggio. Hello esempio seguente imposta hello massima dell'argomento dimensioni too5 GB e un valore di (durata TTL) toolive ora di 1 minuto:

```python
topic_options = Topic()
topic_options.max_size_in_megabytes = '5120'
topic_options.default_message_time_to_live = 'PT1M'

bus_service.create_topic('mytopic', topic_options)
```

## <a name="create-subscriptions"></a>Creare sottoscrizioni
Tootopics le sottoscrizioni vengono creati anche con hello **ServiceBusService** oggetto. Le sottoscrizioni sono denominate e possono avere un filtro facoltativo che limita il set di hello di messaggi recapitati coda virtuale toohello della sottoscrizione.

> [!NOTE]
> Le sottoscrizioni sono permanenti e continueranno tooexist finché uno non o hello toowhich argomento sono state sottoscritte, vengono eliminati.
> 
> 

### <a name="create-a-subscription-with-hello-default-matchall-filter"></a>Creare una sottoscrizione con filtro predefinito (MatchAll) hello
Hello **MatchAll** filtro è hello predefinito che viene utilizzato se viene specificato alcun filtro quando viene creata una nuova sottoscrizione. Quando hello **MatchAll** filtro viene utilizzato, l'argomento di toohello pubblicati tutti i messaggi vengono inseriti nella coda virtuale della sottoscrizione hello. esempio Hello crea una sottoscrizione denominata `AllMessages` e utilizza hello predefinito **MatchAll** filtro.

```python
bus_service.create_subscription('mytopic', 'AllMessages')
```

### <a name="create-subscriptions-with-filters"></a>Creare sottoscrizioni con i filtri
È inoltre possibile definire filtri che consentono di toospecify cui i messaggi inviati tooa argomento visualizzati all'interno di una sottoscrizione di argomento specifico.

Hello più flessibile il tipo di filtro supportato dalle sottoscrizioni è un **SqlFilter**, che implementa un subset di SQL92. I filtri SQL operano sulle proprietà hello dei messaggi hello argomento toohello pubblicato. Per ulteriori informazioni sulle espressioni hello che può essere utilizzato con un filtro SQL, vedere hello [SqlFilter.SqlExpression] [ SqlFilter.SqlExpression] sintassi.

È possibile aggiungere filtri tooa sottoscrizione utilizzando hello **creare\_regola** metodo hello **ServiceBusService** oggetto. Questo metodo consente tooadd nuovi filtri tooan sottoscrizione.

> [!NOTE]
> Poiché il filtro predefinito hello viene applicato automaticamente tooall nuove sottoscrizioni, è necessario innanzitutto rimuovere filtro predefinito hello o hello **MatchAll** sostituirà gli altri filtri che è possibile specificare. È possibile rimuovere una regola predefinita hello utilizzando hello `delete_rule` metodo hello **ServiceBusService** oggetto.
> 
> 

esempio Hello crea una sottoscrizione denominata `HighMessages` con un **SqlFilter** che seleziona solo i messaggi con un oggetto personalizzato `messagenumber` maggiore di 3:

```python
bus_service.create_subscription('mytopic', 'HighMessages')

rule = Rule()
rule.filter_type = 'SqlFilter'
rule.filter_expression = 'messagenumber > 3'

bus_service.create_rule('mytopic', 'HighMessages', 'HighMessageFilter', rule)
bus_service.delete_rule('mytopic', 'HighMessages', DEFAULT_RULE_NAME)
```

Analogamente, hello esempio seguente viene creata una sottoscrizione denominata `LowMessages` con un **SqlFilter** che seleziona solo i messaggi che hanno un `messagenumber` proprietà minore o uguale too3:

```python
bus_service.create_subscription('mytopic', 'LowMessages')

rule = Rule()
rule.filter_type = 'SqlFilter'
rule.filter_expression = 'messagenumber <= 3'

bus_service.create_rule('mytopic', 'LowMessages', 'LowMessageFilter', rule)
bus_service.delete_rule('mytopic', 'LowMessages', DEFAULT_RULE_NAME)
```

A questo punto, quando viene inviato un messaggio troppo`mytopic` viene sempre recapitato tooreceivers sottoscritto toohello **AllMessages** sottoscrizione dell'argomento e recapitati in modo selettivo tooreceivers sottoscritto toohello **HighMessages**  e **LowMessages** le sottoscrizioni dell'argomento (a seconda di contenuto del messaggio hello).

## <a name="send-messages-tooa-topic"></a>Inviare l'argomento tooa messaggi
un argomento del Bus di servizio tooa messaggio toosend, l'applicazione deve usare hello `send_topic_message` metodo hello **ServiceBusService** oggetto.

Hello esempio seguente viene illustrato come test toosend cinque messaggi troppo`mytopic`. Si noti che hello `messagenumber` valore della proprietà di ogni messaggio varia iterazione hello del ciclo di hello (ciò determina le sottoscrizioni che ricevano):

```python
for i in range(5):
    msg = Message('Msg {0}'.format(i).encode('utf-8'), custom_properties={'messagenumber':i})
    bus_service.send_topic_message('mytopic', msg)
```

Argomenti del Bus di servizio supportano una dimensione massima di 256 KB in hello [livello Standard](service-bus-premium-messaging.md) hello a 1 MB e [livello Premium](service-bus-premium-messaging.md). intestazione Hello, che include standard hello e le proprietà personalizzate dell'applicazione, può avere una dimensione massima di 64 KB. Non è previsto alcun limite per il numero di hello di messaggi contenuti in un argomento, ma è un limite alla dimensione totale di hello di messaggi hello utilizzate da un argomento. Questa dimensione dell'argomento viene definita al momento della creazione, con un limite massimo di 5 GB. Per altre informazioni sulle quote, vedere [Quote del bus di servizio][Service Bus quotas].

## <a name="receive-messages-from-a-subscription"></a>Ricevere messaggi da una sottoscrizione
I messaggi vengono ricevuti da una sottoscrizione utilizzando hello `receive_subscription_message` metodo hello **ServiceBusService** oggetto:

```python
msg = bus_service.receive_subscription_message('mytopic', 'LowMessages', peek_lock=False)
print(msg.body)
```

I messaggi vengono eliminati dalla sottoscrizione hello quando vengono letti quando hello parametro `peek_lock` è troppo**False**. È possibile leggere (anteprima) e bloccare il messaggio hello senza eliminarla dalla coda hello dall'impostazione parametro hello `peek_lock` troppo**True**.

Hello comportamento di lettura e l'eliminazione del messaggio hello come parte di hello l'operazione di ricezione è il modello più semplice di hello e adatto per scenari in cui un'applicazione in grado di tollerare non elabora un messaggio di evento hello di un errore. toounderstand, si consideri uno scenario in cui problemi relativi ai consumer hello hello di ricezione richiesta e quindi si blocca prima dell'elaborazione. Poiché verrà contrassegnato messaggio come usato, quindi quando un'applicazione hello viene riavviata e inizia a usare nuovamente i messaggi hello del Bus di servizio, risulterà perso messaggio hello che è stato consumato toohello precedente arresto anomalo del sistema.

Se hello `peek_lock` parametro è impostato troppo**True**, hello ricezione diventa un'operazione in due fasi, che rende possibile toosupport applicazioni che non sono in grado di tollerare messaggi mancanti. Quando il Bus di servizio riceve una richiesta, individua hello successivo messaggio toobe utilizzati Blocca tooprevent altri consumer di ricezione e lo restituisce quindi toohello applicazione. Dopo l'applicazione hello completa l'elaborazione messaggio hello o archiviarlo in modo affidabile per l'elaborazione futura, completa hello seconda fase di hello ricevere processo chiamando `delete` metodo hello **messaggio** oggetto. Hello `delete` metodo contrassegna il messaggio hello come usato e la rimuove dalla sottoscrizione hello.

```python
msg = bus_service.receive_subscription_message('mytopic', 'LowMessages', peek_lock=True)
print(msg.body)

msg.delete()
```

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a>Come si blocca toohandle applicazione e i messaggi illeggibili
Bus di servizio offre funzionalità toohelp che normalmente possibile correggere gli errori nell'applicazione o problemi di elaborazione di un messaggio. Se un'applicazione ricevente è in grado di tooprocess hello messaggio per qualche motivo, quindi è possibile chiamare hello `unlock` metodo hello **messaggio** oggetto. Ciò causerà messaggio hello toounlock di Bus di servizio all'interno di sottoscrizione hello e renderlo disponibile toobe nuovamente ricevuto, sia da hello stesso consumo dell'applicazione o da un'altra applicazione consumer.

È inoltre disponibile un timeout associato a un messaggio bloccato all'interno di sottoscrizione hello e se un'applicazione hello ha esito negativo messaggio hello tooprocess prima hello scadenza del timeout (ad esempio, se si blocca l'applicazione hello), quindi il Bus di servizio Sblocca messaggio hello automaticamente e lo rende disponibile toobe nuovamente ricevuto.

In hello evento hello applicazione si blocca dopo l'elaborazione messaggio hello ma prima di hello `delete` metodo viene chiamato, quindi il messaggio hello sarà applicazione toohello consegnati nuovamente quando si riavvia. Spesso si tratta di *almeno una volta elaborazione*, vale a dire, ogni messaggio verrà elaborato almeno una volta ma in hello determinate situazioni potrebbe essere recapitato nuovamente stesso messaggio. Se hello scenario non tollera la doppia elaborazione, gli sviluppatori di applicazioni devono aggiungere logica aggiuntiva tootheir applicazione toohandle duplicato il recapito dei messaggi. Questa operazione viene spesso eseguita utilizzando hello **MessageId** proprietà di messaggio hello che rimangono costante tra i tentativi di recapito.

## <a name="delete-topics-and-subscriptions"></a>Eliminare argomenti e sottoscrizioni
Argomenti e sottoscrizioni sono persistenti e deve essere in modo esplicito tramite hello eliminato [portale di Azure] [ Azure portal] o a livello di codice. Hello riportato di seguito come argomento di hello toodelete denominati `mytopic`:

```python
bus_service.delete_topic('mytopic')
```

L'eliminazione di un argomento elimina anche le sottoscrizioni che sono registrate con l'argomento hello. Le sottoscrizioni possono essere eliminate anche in modo indipendente. Hello codice seguente viene illustrato come toodelete una sottoscrizione denominata `HighMessages` da hello `mytopic` argomento:

```python
bus_service.delete_subscription('mytopic', 'HighMessages')
```

## <a name="next-steps"></a>Passaggi successivi
Ora che si è appreso i concetti di base di hello di argomenti del Bus di servizio, seguire questi ulteriori toolearn di collegamenti.

* Vedere [Code, argomenti e sottoscrizioni del bus di servizio][Queues, topics, and subscriptions].
* Informazioni di riferimento per [SqlFilter.SqlExpression][SqlFilter.SqlExpression].

[Azure portal]: https://portal.azure.com
[Azure Python package]: https://pypi.python.org/pypi/azure  
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[SqlFilter.SqlExpression]: service-bus-messaging-sql-filter.md
[Service Bus quotas]: service-bus-quotas.md 
