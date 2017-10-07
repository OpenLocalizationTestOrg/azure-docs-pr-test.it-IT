---
title: Accoda aaaHow toouse Azure Service Bus con Ruby | Documenti Microsoft
description: Informazioni su come code di toouse Bus di servizio in Azure. Gli esempi di codice sono scritti in Ruby.
services: service-bus-messaging
documentationcenter: ruby
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 0a11eab2-823f-4cc7-842b-fbbe0f953751
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: ruby
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm
ms.openlocfilehash: 7270154583f98e3372e82efbb967ea7a5acd1686
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-queues-with-ruby"></a>La modalità di code toouse Bus di servizio con Ruby

[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

Questa guida viene descritto come toouse code del Bus di servizio. esempi di Hello sono scritti in Ruby e utilizzano hello Azure indicatore. Hello scenari trattati includono **la creazione delle code, inviando e ricevendo messaggi**, e **l'eliminazione di code**. Per ulteriori informazioni sulle code Service Bus, vedere hello [passaggi successivi](#next-steps) sezione.

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]
   
[!INCLUDE [service-bus-ruby-setup](../../includes/service-bus-ruby-setup.md)]

## <a name="how-toocreate-a-queue"></a>Come toocreate una coda
Hello **Azure::ServiceBusService** consente toowork con le code. toocreate una coda, utilizzare hello `create_queue()` metodo. Hello esempio seguente viene creata una coda o stampa gli eventuali errori.

```ruby
azure_service_bus_service = Azure::ServiceBus::ServiceBusService.new(sb_host, { signer: signer})
begin
  queue = azure_service_bus_service.create_queue("test-queue")
rescue
  puts $!
end
```

È inoltre possibile passare un **Azure::ServiceBus::Queue** dell'oggetto con opzioni aggiuntive, che consente toooverride hello coda le impostazioni predefinite, ad esempio dimensioni toolive o massimo in una coda in fase di messaggio. Hello di esempio seguente viene illustrato come tooset hello GB too5 di dimensioni massime della coda e too1 toolive minuti di tempo:

```ruby
queue = Azure::ServiceBus::Queue.new("test-queue")
queue.max_size_in_megabytes = 5120
queue.default_message_time_to_live = "PT1M"

queue = azure_service_bus_service.create_queue(queue)
```

## <a name="how-toosend-messages-tooa-queue"></a>Come toosend coda dei messaggi di tooa
una coda di Service Bus di messaggi tooa toosend, l'applicazione chiama hello `send_queue_message()` metodo hello **Azure::ServiceBusService** oggetto. I messaggi inviati troppo (e ricevuti da) Bus di servizio, le code sono **Azure::ServiceBus::BrokeredMessage** oggetti e di disporre di un set di proprietà standard (ad esempio `label` e `time_to_live`), un dizionario usato toohold le proprietà personalizzate specifiche dell'applicazione e un corpo di dati applicazione arbitrari. Un'applicazione può impostare il corpo di hello del messaggio hello passando un valore stringa come messaggio hello ed eventuali proprietà standard vengono popolati con i valori predefiniti.

Hello esempio seguente viene illustrato come toosend una coda toohello test denominati `test-queue` utilizzando `send_queue_message()`:

```ruby
message = Azure::ServiceBus::BrokeredMessage.new("test queue message")
message.correlation_id = "test-correlation-id"
azure_service_bus_service.send_queue_message("test-queue", message)
```

Le code del Bus di servizio supportano una dimensione massima di 256 KB in hello [livello Standard](service-bus-premium-messaging.md) hello a 1 MB e [livello Premium](service-bus-premium-messaging.md). intestazione Hello, che include standard hello e le proprietà personalizzate dell'applicazione, può avere una dimensione massima di 64 KB. Non è previsto alcun limite per il numero di hello di messaggi contenuti in una coda, ma è un limite alla dimensione totale di hello di messaggi hello mantenuto da una coda. Questa dimensione della coda viene definita al momento della creazione, con un limite massimo di 5 GB.

## <a name="how-tooreceive-messages-from-a-queue"></a>La modalità tooreceive dei messaggi da una coda
I messaggi vengono ricevuti da una coda utilizzando hello `receive_queue_message()` metodo hello **Azure::ServiceBusService** oggetto. Per impostazione predefinita, vengono letti e bloccati senza essere eliminati dalla coda hello messaggi. Tuttavia, è possibile eliminare i messaggi dalla coda di hello quando vengono letti dall'impostazione hello `:peek_lock` opzione troppo**false**.

comportamento predefinito di Hello rende hello durante la lettura e l'eliminazione di un'operazione in due fasi, che rende possibile toosupport applicazioni che non sono in grado di tollerare messaggi mancanti. Quando il Bus di servizio riceve una richiesta, individua hello successivo messaggio toobe utilizzati Blocca tooprevent altri consumer di ricezione e lo restituisce quindi toohello applicazione. Dopo l'applicazione hello completa l'elaborazione messaggio hello o archiviarlo in modo affidabile per l'elaborazione futura, completa hello seconda fase di hello ricevere processo chiamando `delete_queue_message()` (metodo) e fornendo toobe messaggio hello eliminato come parametro. Hello `delete_queue_message()` metodo contrassegna il messaggio hello come usato, ma verrà rimosso dalla coda hello.

Se hello `:peek_lock` parametro è impostato troppo**false**, durante la lettura e l'eliminazione del messaggio hello diventa modello più semplice hello e adatto per scenari in cui un'applicazione in grado di tollerare non elabora un messaggio di evento hello di un errore. toounderstand, si consideri uno scenario in cui problemi relativi ai consumer hello hello di ricezione richiesta e quindi si blocca prima dell'elaborazione. Perché è contrassegnato come messaggio come usato, quando un'applicazione hello viene riavviata e inizia a usare nuovamente i messaggi hello del Bus di servizio, risulterà perso messaggio hello che è stato consumato toohello precedente arresto anomalo del sistema.

Hello esempio seguente viene illustrato come tooreceive ed elaborare messaggi utilizzando `receive_queue_message()`. esempio Hello innanzitutto riceve ed elimina un messaggio utilizzando `:peek_lock` impostare troppo**false**, riceve un altro messaggio e quindi Elimina hello messaggio utilizzando `delete_queue_message()`:

```ruby
message = azure_service_bus_service.receive_queue_message("test-queue",
  { :peek_lock => false })
message = azure_service_bus_service.receive_queue_message("test-queue")
azure_service_bus_service.delete_queue_message(message)
```

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a>Come si blocca toohandle applicazione e i messaggi illeggibili
Bus di servizio offre funzionalità toohelp che normalmente possibile correggere gli errori nell'applicazione o problemi di elaborazione di un messaggio. Se un'applicazione ricevente è in grado di tooprocess hello messaggio per qualche motivo, quindi è possibile chiamare hello `unlock_queue_message()` metodo hello **Azure::ServiceBusService** oggetto. Questa condizione provoca chiamata hello toounlock Bus di servizio dei messaggi in coda hello e renderlo disponibile toobe nuovamente ricevuto sia da hello stesso consumo dell'applicazione o da un'altra applicazione consumer.

È inoltre disponibile un timeout associato a un messaggio bloccato all'interno di coda hello e se un'applicazione hello ha esito negativo messaggio hello tooprocess prima hello scadenza del timeout (ad esempio, se si blocca l'applicazione hello), quindi il Bus di servizio Sblocca messaggio hello automaticamente e lo rende disponibile toobe nuovamente ricevuto.

In hello evento hello applicazione si blocca dopo l'elaborazione messaggio hello ma prima di hello `delete_queue_message()` metodo viene chiamato, il messaggio hello è applicazione toohello consegnati nuovamente quando viene riavviata. Questo processo viene spesso chiamato *almeno una volta elaborazione*; ovvero, ogni messaggio viene elaborato almeno una volta ma in hello determinate situazioni potrebbe essere recapitato nuovamente stesso messaggio. Se hello scenario non tollera la doppia elaborazione, gli sviluppatori di applicazioni devono aggiungere logica aggiuntiva tootheir applicazione toohandle duplicato il recapito dei messaggi. Questa operazione viene spesso eseguita utilizzando hello `message_id` proprietà del messaggio hello, che rimane costante tra i tentativi di recapito.

## <a name="next-steps"></a>Passaggi successivi
Dopo aver appreso nozioni di base di hello di code del Bus di servizio, seguire questi ulteriori toolearn di collegamenti.

* Panoramica di [code, argomenti e sottoscrizioni](service-bus-queues-topics-subscriptions.md).
* Visitare hello [Azure SDK per Ruby](https://github.com/Azure/azure-sdk-for-ruby) repository in GitHub.

Per un confronto tra le code di Azure Service Bus hello descritte in questo articolo e le code di Azure descritto in hello [come toouse archiviazione delle code da Ruby](../storage/queues/storage-ruby-how-to-use-queue-storage.md) articolo, vedere [code di Azure e code di Azure Service Bus - rispetto e Contrapposizioni](service-bus-azure-and-service-bus-queues-compared-contrasted.md)

