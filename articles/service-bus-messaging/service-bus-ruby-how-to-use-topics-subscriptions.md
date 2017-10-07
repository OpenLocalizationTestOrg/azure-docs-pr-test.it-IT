---
title: gli argomenti del Bus di servizio toouse aaaHow (Ruby) | Documenti Microsoft
description: Informazioni su come toouse Bus di servizio di argomenti e sottoscrizioni in Azure. Gli esempi di codice sono scritti per applicazioni Ruby.
services: service-bus-messaging
documentationcenter: ruby
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 3ef2295e-7c5f-4c54-a13b-a69c8045d4b6
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: ruby
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm
ms.openlocfilehash: 236d6495825e68e336c23e1b500d0764ee512e49
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-topics-and-subscriptions-with-ruby"></a>Il Bus di servizio toouse argomenti e sottoscrizioni con Ruby
 
[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

Questo articolo viene descritto come toouse Bus di servizio di argomenti e sottoscrizioni dalle applicazioni Ruby. Hello scenari trattati includono **la creazione di argomenti e sottoscrizioni, la creazione di filtri di sottoscrizione, l'invio di messaggi** argomento tooa **la ricezione di messaggi da una sottoscrizione**, e  **l'eliminazione di argomenti e sottoscrizioni**. Per ulteriori informazioni su argomenti e sottoscrizioni, vedere hello [passaggi successivi](#next-steps) sezione.

[!INCLUDE [howto-service-bus-topics](../../includes/howto-service-bus-topics.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

[!INCLUDE [service-bus-ruby-setup](../../includes/service-bus-ruby-setup.md)]

## <a name="create-a-topic"></a>Creare un argomento
Hello **Azure::ServiceBusService** consente toowork con argomenti. Hello codice seguente viene creato un **Azure::ServiceBusService** oggetto. un argomento, toocreate utilizzare hello `create_topic()` metodo. Hello di esempio seguente crea un argomento o stampa se sono presenti errori di hello.

```ruby
azure_service_bus_service = Azure::ServiceBus::ServiceBusService.new(sb_host, { signer: signer})
begin
  topic = azure_service_bus_service.create_queue("test-topic")
rescue
  puts $!
end
```

È inoltre possibile passare un **Azure::ServiceBus::Topic** oggetto con opzioni aggiuntive, che consentono di determinare le impostazioni dell'argomento predefinito toooverride, ad esempio dimensioni toolive o massimo in una coda in fase di messaggio. Hello esempio seguente viene illustrata l'impostazione massima della coda hello dimensioni too5 GB e l'ora too1 toolive minuto:

```ruby
topic = Azure::ServiceBus::Topic.new("test-topic")
topic.max_size_in_megabytes = 5120
topic.default_message_time_to_live = "PT1M"

topic = azure_service_bus_service.create_topic(topic)
```

## <a name="create-subscriptions"></a>Creare sottoscrizioni
Le sottoscrizioni dell'argomento vengono inoltre create con hello **Azure::ServiceBusService** oggetto. Le sottoscrizioni sono denominate e possono avere un filtro facoltativo che limita il set di hello di messaggi recapitati coda virtuale toohello della sottoscrizione.

Le sottoscrizioni sono permanenti e continueranno tooexist finché uno non o hello argomento sono associati, vengono eliminati. Se l'applicazione contiene la logica toocreate una sottoscrizione, deve verificare se hello sottoscrizione esiste già con metodo getSubscription hello.

### <a name="create-a-subscription-with-hello-default-matchall-filter"></a>Creare una sottoscrizione con filtro predefinito (MatchAll) hello
Hello **MatchAll** filtro è hello predefinito che viene utilizzato se viene specificato alcun filtro quando viene creata una nuova sottoscrizione. Quando hello **MatchAll** filtro viene utilizzato, l'argomento di toohello pubblicati tutti i messaggi vengono inseriti nella coda virtuale della sottoscrizione hello. esempio Hello crea una sottoscrizione denominata "tutti i messaggi" e utilizza hello predefinito **MatchAll** filtro.

```ruby
subscription = azure_service_bus_service.create_subscription("test-topic", "all-messages")
```

### <a name="create-subscriptions-with-filters"></a>Creare sottoscrizioni con i filtri
È inoltre possibile definire filtri che consentono di toospecify cui i messaggi inviati tooa argomento visualizzati all'interno di una sottoscrizione specifica.

tipo di filtro supportato dalle sottoscrizioni più flessibile Hello è hello **Azure::ServiceBus::SqlFilter**, che implementa un subset di SQL92. I filtri SQL operano sulle proprietà hello dei messaggi hello argomento toohello pubblicato. Per ulteriori informazioni sulle espressioni hello che possono essere utilizzate con un filtro SQL, vedere hello [SqlFilter](service-bus-messaging-sql-filter.md) sintassi.

È possibile aggiungere filtri tooa sottoscrizione utilizzando hello `create_rule()` metodo hello **Azure::ServiceBusService** oggetto. Questo metodo consente tooadd nuovi filtri tooan sottoscrizione.

Poiché il filtro predefinito hello viene applicato automaticamente tooall nuove sottoscrizioni, è innanzitutto necessario rimuovere filtro predefinito hello o hello **MatchAll** sostituirà gli altri filtri che è possibile specificare. È possibile rimuovere una regola predefinita hello utilizzando hello `delete_rule()` metodo hello **Azure::ServiceBusService** oggetto.

esempio Hello crea una sottoscrizione denominata "alta messaggi" con un **Azure::ServiceBus::SqlFilter** che seleziona solo i messaggi con un oggetto personalizzato `message_number` maggiore di 3:

```ruby
subscription = azure_service_bus_service.create_subscription("test-topic", "high-messages")
azure_service_bus_service.delete_rule("test-topic", "high-messages", "$Default")

rule = Azure::ServiceBus::Rule.new("high-messages-rule")
rule.topic = "test-topic"
rule.subscription = "high-messages"
rule.filter = Azure::ServiceBus::SqlFilter.new({
  :sql_expression => "message_number > 3" })
rule = azure_service_bus_service.create_rule(rule)
```

Analogamente, hello esempio seguente viene creata una sottoscrizione denominata `low-messages` con un **Azure::ServiceBus::SqlFilter** che seleziona solo i messaggi che hanno un `message_number` proprietà minore o uguale too3:

```ruby
subscription = azure_service_bus_service.create_subscription("test-topic", "low-messages")
azure_service_bus_service.delete_rule("test-topic", "low-messages", "$Default")

rule = Azure::ServiceBus::Rule.new("low-messages-rule")
rule.topic = "test-topic"
rule.subscription = "low-messages"
rule.filter = Azure::ServiceBus::SqlFilter.new({
  :sql_expression => "message_number <= 3" })
rule = azure_service_bus_service.create_rule(rule)
```

Quando viene inviato un messaggio ora troppo`test-topic`, è sempre essere recapitato tooreceivers sottoscritto toohello `all-messages` sottoscrizione dell'argomento e recapitati in modo selettivo tooreceivers sottoscritto toohello `high-messages` e `low-messages` (sottoscrizioni di argomento in base al contenuto del messaggio hello).

## <a name="send-messages-tooa-topic"></a>Inviare l'argomento tooa messaggi
un argomento del Bus di servizio tooa messaggio toosend, l'applicazione deve usare hello `send_topic_message()` metodo hello **Azure::ServiceBusService** oggetto. I messaggi inviati gli argomenti del Bus tooService sono istanze di hello **Azure::ServiceBus::BrokeredMessage** oggetti. **Azure::ServiceBus::BrokeredMessage** oggetti dispongono di un set di proprietà standard (ad esempio `label` e `time_to_live`), un dizionario di proprietà specifiche dell'applicazione personalizzate usate toohold e un corpo di dati di tipo stringa. Un'applicazione può impostare il corpo di hello del messaggio hello passando un toohello valore stringa `send_topic_message()` necessari (metodo) e le proprietà standard verranno popolate dai valori predefiniti.

Hello esempio seguente viene illustrato come test toosend cinque messaggi troppo`test-topic`. Si noti che hello `message_number` valore della proprietà personalizzata di ogni messaggio varia iterazione hello del ciclo di hello (ciò determina la sottoscrizione riceve):

```ruby
5.times do |i|
  message = Azure::ServiceBus::BrokeredMessage.new("test message " + i,
    { :message_number => i })
  azure_service_bus_service.send_topic_message("test-topic", message)
end
```

Argomenti del Bus di servizio supportano una dimensione massima di 256 KB in hello [livello Standard](service-bus-premium-messaging.md) hello a 1 MB e [livello Premium](service-bus-premium-messaging.md). intestazione Hello, che include standard hello e le proprietà personalizzate dell'applicazione, può avere una dimensione massima di 64 KB. Non è previsto alcun limite per il numero di hello di messaggi contenuti in un argomento, ma è un limite alla dimensione totale di hello di messaggi hello utilizzate da un argomento. Questa dimensione dell'argomento viene definita al momento della creazione, con un limite massimo di 5 GB.

## <a name="receive-messages-from-a-subscription"></a>Ricevere messaggi da una sottoscrizione
I messaggi vengono ricevuti da una sottoscrizione utilizzando hello `receive_subscription_message()` metodo hello **Azure::ServiceBusService** oggetto. Per impostazione predefinita, i messaggi sono read(peak) e bloccato senza eliminarla dalla sottoscrizione hello. È possibile leggere ed eliminare il messaggio hello dalla sottoscrizione hello dall'impostazione hello `peek_lock` opzione troppo**false**.

comportamento predefinito di Hello rende hello durante la lettura e l'eliminazione di un'operazione in due fasi, che rende possibile toosupport applicazioni che non sono in grado di tollerare messaggi mancanti. Quando il Bus di servizio riceve una richiesta, individua hello successivo messaggio toobe utilizzati Blocca tooprevent altri consumer di ricezione e lo restituisce quindi toohello applicazione. Dopo l'applicazione hello completa l'elaborazione messaggio hello o archiviarlo in modo affidabile per l'elaborazione futura, completa hello seconda fase di hello ricevere processo chiamando `delete_subscription_message()` (metodo) e fornendo toobe messaggio hello eliminato come parametro. Hello `delete_subscription_message()` metodo contrassegna il messaggio hello come usato, ma verrà rimosso dalla sottoscrizione hello.

Se hello `:peek_lock` parametro è impostato troppo**false**, durante la lettura e l'eliminazione del messaggio hello diventa modello più semplice hello e adatto per scenari in cui un'applicazione in grado di tollerare non elabora un messaggio di evento hello di un errore. toounderstand, si consideri uno scenario in cui problemi relativi ai consumer hello hello di ricezione richiesta e quindi si blocca prima dell'elaborazione. Poiché verrà contrassegnato messaggio come usato, quindi quando un'applicazione hello viene riavviata e inizia a usare nuovamente i messaggi hello del Bus di servizio, risulterà perso messaggio hello che è stato consumato toohello precedente arresto anomalo del sistema.

Hello esempio seguente viene illustrato come è possibile ricevere messaggi e trasformati utilizzando `receive_subscription_message()`. esempio Hello innanzitutto riceve ed elimina un messaggio da hello `low-messages` sottoscrizione utilizzando `:peek_lock` impostare troppo**false**, quindi riceve un altro messaggio da hello `high-messages` e quindi Elimina hello messaggio utilizzando `delete_subscription_message()`:

```ruby
message = azure_service_bus_service.receive_subscription_message(
  "test-topic", "low-messages", { :peek_lock => false })
message = azure_service_bus_service.receive_subscription_message(
  "test-topic", "high-messages")
azure_service_bus_service.delete_subscription_message(message)
```

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a>Come si blocca toohandle applicazione e i messaggi illeggibili
Bus di servizio offre funzionalità toohelp che normalmente possibile correggere gli errori nell'applicazione o problemi di elaborazione di un messaggio. Se un'applicazione ricevente è in grado di tooprocess hello messaggio per qualche motivo, quindi è possibile chiamare hello `unlock_subscription_message()` metodo hello **Azure::ServiceBusService** oggetto. Questa condizione provoca hello toounlock Bus di servizio all'interno di sottoscrizione hello del messaggio e renderlo disponibile toobe nuovamente ricevuto sia da hello stesso consumo dell'applicazione o da un'altra applicazione consumer.

È inoltre disponibile un timeout associato a un messaggio bloccato all'interno di sottoscrizione hello e se un'applicazione hello ha esito negativo messaggio hello tooprocess prima hello scadenza del timeout (ad esempio, se si blocca l'applicazione hello), quindi il Bus di servizio sbloccherà il messaggio hello automaticamente e renderlo disponibile toobe nuovamente ricevuto.

In hello evento hello applicazione si blocca dopo l'elaborazione messaggio hello ma prima di hello `delete_subscription_message()` metodo viene chiamato, il messaggio hello è applicazione toohello consegnati nuovamente quando viene riavviata. Spesso si tratta di *almeno una volta elaborazione*; ovvero, ogni messaggio verrà elaborato almeno una volta ma in hello determinate situazioni potrebbe essere recapitato nuovamente stesso messaggio. Se hello scenario non tollera la doppia elaborazione, gli sviluppatori di applicazioni devono aggiungere logica aggiuntiva tootheir applicazione toohandle duplicato il recapito dei messaggi. Questa logica viene spesso ottenuta utilizzando hello `message_id` proprietà di messaggio hello che rimangono costante tra i tentativi di recapito.

## <a name="delete-topics-and-subscriptions"></a>Eliminare argomenti e sottoscrizioni
Argomenti e sottoscrizioni sono persistenti e deve essere in modo esplicito tramite hello eliminato [portale di Azure] [ Azure portal] o a livello di codice. Hello riportato di seguito come argomento di hello toodelete denominati `test-topic`.

```ruby
azure_service_bus_service.delete_topic("test-topic")
```

L'eliminazione di un argomento elimina anche le sottoscrizioni che sono registrate con l'argomento hello. Le sottoscrizioni possono essere eliminate anche in modo indipendente. Hello codice seguente viene illustrato come sottoscrizione hello toodelete denominati `high-messages` da hello `test-topic` argomento:

```ruby
azure_service_bus_service.delete_subscription("test-topic", "high-messages")
```

## <a name="next-steps"></a>Passaggi successivi
Ora che si è appreso i concetti di base di hello di argomenti del Bus di servizio, seguire questi ulteriori toolearn di collegamenti.

* Vedere [Code, argomenti e sottoscrizioni](service-bus-queues-topics-subscriptions.md).
* Materiale di riferimento dell'API per [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter).
* Visitare hello [Azure SDK per Ruby](https://github.com/Azure/azure-sdk-for-ruby) repository in GitHub.

[Azure portal]: https://portal.azure.com
