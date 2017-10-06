---
title: gli argomenti del Bus di servizio toouse aaaHow con PHP | Documenti Microsoft
description: Informazioni su come argomenti del Bus di servizio toouse con PHP in Azure.
services: service-bus-messaging
documentationcenter: php
author: sethmanheim
manager: timlt
editor: 
ms.assetid: faaa4bbd-f6ef-42ff-aca7-fc4353976449
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 04/27/2017
ms.author: sethm
ms.openlocfilehash: 0ca8625fa3edc5854c0d6c1c2f6adab6a2d42f91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-topics-and-subscriptions-with-php"></a>Il Bus di servizio toouse argomenti e sottoscrizioni con PHP

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

In questo articolo illustra come toouse Bus di servizio di argomenti e sottoscrizioni. esempi di Hello sono scritti in PHP e utilizzare hello [Azure SDK per PHP](../php-download-sdk.md). Hello scenari trattati includono **la creazione di argomenti e sottoscrizioni**, **creazione filtri di sottoscrizione**, **invio argomento tooa messaggi**, **ricezione i messaggi da una sottoscrizione**, e **l'eliminazione di argomenti e sottoscrizioni**.

[!INCLUDE [howto-service-bus-topics](../../includes/howto-service-bus-topics.md)]

## <a name="create-a-php-application"></a>Creare un'applicazione PHP
Hello solo requisito per la creazione di un'applicazione PHP che accede al servizio Blob di Azure hello è classi tooreference hello [Azure SDK per PHP](../php-download-sdk.md) dall'interno del codice. È possibile utilizzare qualsiasi toocreate di strumenti di sviluppo, l'applicazione o il blocco note.

> [!NOTE]
> L'installazione di PHP deve inoltre disporre hello [estensione OpenSSL](http://php.net/openssl) installato e abilitato.
> 
> 

In questo articolo viene descritto come toouse funzionalità che può essere chiamata all'interno di un'applicazione PHP in locale o nel codice in esecuzione all'interno di un ruolo web di Azure, un ruolo di lavoro o un sito Web del servizio.

## <a name="get-hello-azure-client-libraries"></a>Recuperare le librerie client di Azure hello
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-toouse-service-bus"></a>Configurare il toouse applicazione Bus di servizio
hello toouse API del Bus di servizio:

1. File di riferimento autoloader hello utilizzando hello [require_once] [ require-once] istruzione.
2. Fare riferimento a tutte le eventuali classi utilizzabili.

Hello esempio seguente viene illustrato come tooinclude hello hello di file e riferimento autoloader **ServiceBusService** classe.

> [!NOTE]
> In questo esempio (e altri esempi in questo articolo) presuppone installate le librerie Client di PHP hello per Azure tramite creazione. Se è installato librerie hello manualmente o come un pacchetto di PERA, è necessario fare riferimento hello **WindowsAzure.php** autoloader file.
> 
> 

```php
require_once 'vendor\autoload.php';
use WindowsAzure\Common\ServicesBuilder;
```

In hello seguono esempi, hello `require_once` istruzione verrà sempre visualizzata, ma solo hello classi necessarie per tooexecute esempio hello viene fatto riferimento.

## <a name="set-up-a-service-bus-connection"></a>Configurare una stringa di connessione per il bus di servizio
tooinstantiate un client del Bus di servizio è necessario avere una stringa di connessione valido nel formato seguente:

```
Endpoint=[yourEndpoint];SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[Primary Key]
```

Dove `Endpoint` è in genere in formato di hello `https://[yourNamespace].servicebus.windows.net`.

toocreate qualsiasi client di servizio di Azure, è necessario utilizzare hello `ServicesBuilder` classe. È possibile:

* Passare la connessione hello tooit direttamente di stringa.
* Hello utilizzare **CloudConfigurationManager (CCM)** toocheck origini dati esterne di più origini per la stringa di connessione hello:
  * Per impostazione predefinita viene fornito con il supporto per un'origine esterna, ovvero le variabili ambientali.
  * È possibile aggiungere nuove origini estendendo hello `ConnectionStringSource` classe.

Per esempi di hello descritti di seguito, la stringa di connessione hello viene passata direttamente.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$connectionString = "Endpoint=[yourEndpoint];SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[Primary Key]";

$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);
```

## <a name="create-a-topic"></a>Creare un argomento
È possibile eseguire operazioni di gestione per gli argomenti del Bus di servizio tramite hello `ServiceBusRestProxy` classe. Oggetto `ServiceBusRestProxy` oggetto viene costruito tramite hello `ServicesBuilder::createServiceBusService` metodo factory con una stringa di connessione appropriata che incapsula toomanage autorizzazioni token hello è.

Hello seguente esempio viene illustrato come tooinstantiate un `ServiceBusRestProxy` e chiamare `ServiceBusRestProxy->createTopic` toocreate un argomento denominato `mytopic` all'interno di un `MySBNamespace` dello spazio dei nomi:

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use WindowsAzure\Common\ServiceException;
use WindowsAzure\ServiceBus\Models\TopicInfo;

// Create Service Bus REST proxy.
$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);

try    {        
    // Create topic.
    $topicInfo = new TopicInfo("mytopic");
    $serviceBusRestProxy->createTopic($topicInfo);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here: 
    // https://docs.microsoft.com/rest/api/storageservices/Common-REST-API-Error-Codes
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

> [!NOTE]
> È possibile utilizzare hello `listTopics` metodo `ServiceBusRestProxy` oggetti toocheck se un argomento con un nome specificato esiste già all'interno di uno spazio dei nomi del servizio.
> 
> 

## <a name="create-a-subscription"></a>Creare una sottoscrizione
Le sottoscrizioni dell'argomento vengono inoltre create con hello `ServiceBusRestProxy->createSubscription` metodo. Le sottoscrizioni sono denominate e possono avere un filtro facoltativo che limita il set di hello di messaggi passati coda virtuale toohello della sottoscrizione.

### <a name="create-a-subscription-with-hello-default-matchall-filter"></a>Creare una sottoscrizione con filtro predefinito (MatchAll) hello
Hello **MatchAll** filtro è hello predefinito che viene utilizzato se viene specificato alcun filtro quando viene creata una nuova sottoscrizione. Quando hello **MatchAll** filtro viene utilizzato, l'argomento di toohello pubblicati tutti i messaggi vengono inseriti nella coda virtuale della sottoscrizione hello. esempio Hello crea una sottoscrizione denominata 'mysubscription' e utilizza hello predefinito **MatchAll** filtro.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use WindowsAzure\Common\ServiceException;
use WindowsAzure\ServiceBus\Models\SubscriptionInfo;

// Create Service Bus REST proxy.
$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);

try    {
    // Create subscription.
    $subscriptionInfo = new SubscriptionInfo("mysubscription");
    $serviceBusRestProxy->createSubscription("mytopic", $subscriptionInfo);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here: 
    // https://docs.microsoft.com/rest/api/storageservices/Common-REST-API-Error-Codes
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

### <a name="create-subscriptions-with-filters"></a>Creare sottoscrizioni con i filtri
È inoltre possibile impostare i filtri che consentono di toospecify cui i messaggi inviati tooa argomento deve trovarsi all'interno di una sottoscrizione di argomento specifico. tipo di filtro supportato dalle sottoscrizioni più flessibile Hello è hello [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter), che implementa un subset di SQL92. I filtri SQL operano sulle proprietà hello dei messaggi hello argomento toohello pubblicato. Per altre informazioni su SqlFilters, vedere la sezione relativa alla [proprietà SqlFilter.SqlExpression][sqlfilter].

> [!NOTE]
> Ogni regola su una sottoscrizione elabora i messaggi in ingresso in modo indipendente, aggiungere la sottoscrizione a pagamento risultato toohello messaggi. Inoltre, ogni nuova sottoscrizione ha un valore predefinito **regola** oggetto con un filtro che consente di aggiungere tutti i messaggi dalla sottoscrizione di toohello argomento hello. tooreceive solo i messaggi che corrispondono al filtro, è necessario rimuovere la regola predefinita di hello. È possibile rimuovere una regola predefinita hello utilizzando hello `ServiceBusRestProxy->deleteRule` metodo.
> 
> 

esempio Hello crea una sottoscrizione denominata `HighMessages` con un **SqlFilter** che seleziona solo i messaggi con un oggetto personalizzato `MessageNumber` maggiore di 3. Vedere [argomento tooa di trasmissione messaggi](#send-messages-to-a-topic) per informazioni sull'aggiunta di proprietà personalizzate toomessages.

```php
$subscriptionInfo = new SubscriptionInfo("HighMessages");
$serviceBusRestProxy->createSubscription("mytopic", $subscriptionInfo);

$serviceBusRestProxy->deleteRule("mytopic", "HighMessages", '$Default');

$ruleInfo = new RuleInfo("HighMessagesRule");
$ruleInfo->withSqlFilter("MessageNumber > 3");
$ruleResult = $serviceBusRestProxy->createRule("mytopic", "HighMessages", $ruleInfo);
```

Si noti che questo codice richiede l'uso di hello di uno spazio dei nomi aggiuntivo: `WindowsAzure\ServiceBus\Models\SubscriptionInfo`.

Analogamente, hello esempio seguente viene creata una sottoscrizione denominata `LowMessages` con un `SqlFilter` che seleziona solo i messaggi che hanno un `MessageNumber` proprietà minore o uguale too3.

```php
$subscriptionInfo = new SubscriptionInfo("LowMessages");
$serviceBusRestProxy->createSubscription("mytopic", $subscriptionInfo);

$serviceBusRestProxy->deleteRule("mytopic", "LowMessages", '$Default');

$ruleInfo = new RuleInfo("LowMessagesRule");
$ruleInfo->withSqlFilter("MessageNumber <= 3");
$ruleResult = $serviceBusRestProxy->createRule("mytopic", "LowMessages", $ruleInfo);
```

A questo punto, quando viene inviato un messaggio toohello `mytopic` argomento, viene sempre recapitato tooreceivers sottoscritto toohello `mysubscription` sottoscrizione e recapitati in modo selettivo tooreceivers sottoscritto toohello `HighMessages` e `LowMessages` (sottoscrizioni in base al contenuto del messaggio hello).

## <a name="send-messages-tooa-topic"></a>Inviare l'argomento tooa messaggi
un argomento del Bus di servizio tooa messaggio toosend, l'applicazione chiama hello `ServiceBusRestProxy->sendTopicMessage` metodo. Hello seguente codice mostra come toosend toohello un messaggio `mytopic` argomento creato in precedenza all'interno di `MySBNamespace` dello spazio dei nomi di servizio.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use WindowsAzure\Common\ServiceException;
use WindowsAzure\ServiceBus\Models\BrokeredMessage;

// Create Service Bus REST proxy.
$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);

try    {
    // Create message.
    $message = new BrokeredMessage();
    $message->setBody("my message");

    // Send message.
    $serviceBusRestProxy->sendTopicMessage("mytopic", $message);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here: 
    // https://docs.microsoft.com/rest/api/storageservices/Common-REST-API-Error-Codes
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

I messaggi inviati gli argomenti del Bus tooService sono istanze di hello [BrokeredMessage] [ BrokeredMessage] classe. [BrokeredMessage] [ BrokeredMessage] oggetti dispongono di un set di metodi e proprietà standard, nonché le proprietà che possono essere proprietà specifiche dell'applicazione personalizzate toohold utilizzato. Hello esempio seguente viene illustrato come test toosend 5 messaggi toohello `mytopic` argomento creato in precedenza. Hello `setProperty` metodo è usato tooadd una proprietà personalizzata (`MessageNumber`) tooeach messaggio. Si noti che hello `MessageNumber` valore della proprietà varia per ogni messaggio (è possibile utilizzare questo valore toodetermine ricevano le sottoscrizioni, come illustrato nell'hello [creare una sottoscrizione](#create-a-subscription) sezione):

```php
for($i = 0; $i < 5; $i++){
    // Create message.
    $message = new BrokeredMessage();
    $message->setBody("my message ".$i);

    // Set custom property.
    $message->setProperty("MessageNumber", $i);

    // Send message.
    $serviceBusRestProxy->sendTopicMessage("mytopic", $message);
}
```

Argomenti del Bus di servizio supportano una dimensione massima di 256 KB in hello [livello Standard](service-bus-premium-messaging.md) hello a 1 MB e [livello Premium](service-bus-premium-messaging.md). intestazione Hello, che include standard hello e le proprietà personalizzate dell'applicazione, può avere una dimensione massima di 64 KB. Non è previsto alcun limite per il numero di hello di messaggi contenuti in un argomento, ma è un limite alla dimensione totale di hello di messaggi hello utilizzate da un argomento. Il limite massimo delle dimensioni di un argomento è 5 GB. Per altre informazioni sulle quote, vedere [Quote del bus di servizio][Service Bus quotas].

## <a name="receive-messages-from-a-subscription"></a>Ricevere messaggi da una sottoscrizione
migliore modalità tooreceive messaggi Hello da una sottoscrizione è toouse un `ServiceBusRestProxy->receiveSubscriptionMessage` metodo. Le modalità di ricezione dei messaggi sono due: [*ReceiveAndDelete* e *PeekLock*](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode). **PeekLock** hello predefinito.

Quando si utilizza hello [ReceiveAndDelete](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) , la modalità di ricezione è un'operazione singola cattura; ovvero quando il Bus di servizio riceve una richiesta di lettura per un messaggio in una sottoscrizione, contrassegna il messaggio hello come usato e lo restituisce toohello applicazione. [ReceiveAndDelete](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) * modalità modello più semplice di hello ed è adatta per scenari in cui un'applicazione in grado di tollerare non elabora un messaggio di evento hello di un errore. toounderstand, si consideri uno scenario in cui problemi relativi ai consumer hello hello di ricezione richiesta e quindi si blocca prima dell'elaborazione. Poiché verrà contrassegnato messaggio come usato, quindi quando un'applicazione hello viene riavviata e inizia a usare nuovamente i messaggi hello del Bus di servizio, risulterà perso messaggio hello che è stato consumato toohello precedente arresto anomalo del sistema.

Predefinita hello [PeekLock](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) modalità di ricezione di un messaggio diventa un'operazione in due fasi, che rende possibile toosupport applicazioni che non sono in grado di tollerare messaggi mancanti. Quando il Bus di servizio riceve una richiesta, individua hello successivo messaggio toobe utilizzati Blocca tooprevent altri consumer di ricezione e lo restituisce quindi toohello applicazione. Dopo l'applicazione hello completa l'elaborazione messaggio hello o archiviarlo in modo affidabile per l'elaborazione futura, completa hello seconda fase di hello processo di ricezione, passando il messaggio hello ricevuto troppo`ServiceBusRestProxy->deleteMessage`. Quando il Bus di servizio rileva hello `deleteMessage` chiamata, verrà contrassegnare il messaggio hello come usato e rimuoverlo dalla coda hello.

Hello seguente esempio viene illustrato come tooreceive ed elaborare un messaggio utilizzando [PeekLock](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) modalità (hello predefinita). 

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use WindowsAzure\Common\ServiceException;
use WindowsAzure\ServiceBus\Models\ReceiveMessageOptions;

// Create Service Bus REST proxy.
$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);

try    {
    // Set receive mode tooPeekLock (default is ReceiveAndDelete)
    $options = new ReceiveMessageOptions();
    $options->setPeekLock();

    // Get message.
    $message = $serviceBusRestProxy->receiveSubscriptionMessage("mytopic", "mysubscription", $options);

    echo "Body: ".$message->getBody()."<br />";
    echo "MessageID: ".$message->getMessageId()."<br />";

    /*---------------------------
        Process message here.
    ----------------------------*/

    // Delete message. Not necessary if peek lock is not set.
    echo "Deleting message...<br />";
    $serviceBusRestProxy->deleteMessage($message);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // https://docs.microsoft.com/rest/api/storageservices/Common-REST-API-Error-Codes
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="how-to-handle-application-crashes-and-unreadable-messages"></a>Procedura: Gestire arresti anomali e messaggi illeggibili dell'applicazione
Bus di servizio offre funzionalità toohelp che normalmente possibile correggere gli errori nell'applicazione o problemi di elaborazione di un messaggio. Se un'applicazione ricevente è in grado di tooprocess hello messaggio per qualche motivo, quindi è possibile chiamare hello `unlockMessage` metodo sul messaggio ricevuto (anziché hello `deleteMessage` (metodo)). Ciò causerà messaggio hello toounlock di Bus di servizio all'interno di coda hello e renderlo disponibile toobe nuovamente ricevuto, sia da hello stesso consumo dell'applicazione o da un'altra applicazione consumer.

È inoltre disponibile un timeout associato a un messaggio bloccato all'interno di coda hello e se un'applicazione hello ha esito negativo messaggio hello tooprocess prima hello scadenza del timeout (ad esempio, se si blocca l'applicazione hello), quindi il Bus di servizio sbloccherà il messaggio hello automaticamente e renderlo disponibile toobe nuovamente ricevuto.

In hello evento hello applicazione si blocca dopo l'elaborazione messaggio hello ma prima di hello `deleteMessage` richiesta inviata, quindi messaggio hello sarà applicazione toohello consegnati nuovamente quando viene riavviata. Spesso si tratta di *almeno una volta che* l'elaborazione; ovvero, ogni messaggio viene elaborato almeno una volta ma in hello determinate situazioni potrebbe essere recapitato nuovamente stesso messaggio. Se hello scenario non tollera la doppia elaborazione, gli sviluppatori di applicazioni devono aggiungere logica aggiuntiva tooapplications toohandle duplicato il recapito dei messaggi. Questa operazione viene spesso eseguita utilizzando hello `getMessageId` metodo del messaggio hello, che rimane costante tra i tentativi di recapito.

## <a name="delete-topics-and-subscriptions"></a>Eliminare argomenti e sottoscrizioni
toodelete un argomento o una sottoscrizione, utilizzare hello `ServiceBusRestProxy->deleteTopic` o hello `ServiceBusRestProxy->deleteSubscripton` metodi, rispettivamente. Si noti che anche l'eliminazione di un argomento Elimina le sottoscrizioni che sono registrate con l'argomento hello.

Hello esempio seguente viene illustrato come toodelete un argomento denominato `mytopic` e le relative sottoscrizioni registrate.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\ServiceBus\ServiceBusService;
use WindowsAzure\ServiceBus\ServiceBusSettings;
use WindowsAzure\Common\ServiceException;

// Create Service Bus REST proxy.
$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);

try    {        
    // Delete topic.
    $serviceBusRestProxy->deleteTopic("mytopic");
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here: 
    // https://docs.microsoft.com/rest/api/storageservices/Common-REST-API-Error-Codes
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

Utilizzando hello `deleteSubscription` metodo, è possibile eliminare una sottoscrizione in modo indipendente:

```php
$serviceBusRestProxy->deleteSubscription("mytopic", "mysubscription");
```

## <a name="next-steps"></a>Passaggi successivi
Dopo aver appreso nozioni di base di hello di code del Bus di servizio, vedere [code, argomenti e sottoscrizioni] [ Queues, topics, and subscriptions] per ulteriori informazioni.

[BrokeredMessage]: https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.brokeredmessage
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[sqlfilter]: /dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter
[require-once]: http://php.net/require_once
[Service Bus quotas]: service-bus-quotas.md
