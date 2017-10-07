---
title: Accoda aaaHow toouse Bus di servizio con PHP | Documenti Microsoft
description: Informazioni su come code di toouse Bus di servizio in Azure. Gli esempi di codice sono scritti in PHP.
services: service-bus-messaging
documentationcenter: php
author: sethmanheim
manager: timlt
editor: 
ms.assetid: e29c829b-44c5-4350-8f2e-39e0c380a9f2
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm
ms.openlocfilehash: 8cf233176029b679d172eaf713632087beca5e4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-queues-with-php"></a>La modalità di code toouse Bus di servizio con PHP
[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

Questa guida illustra come toouse code del Bus di servizio. esempi di Hello sono scritti in PHP e utilizzare hello [Azure SDK per PHP](../php-download-sdk.md). Hello scenari trattati includono **la creazione delle code**, **inviando e ricevendo messaggi**, e **l'eliminazione di code**.

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

## <a name="create-a-php-application"></a>Creare un'applicazione PHP
Hello solo requisito per la creazione di un'applicazione PHP che accede al servizio Blob di Azure hello è hello che fanno riferimento a delle classi in hello [Azure SDK per PHP](../php-download-sdk.md) dall'interno del codice. È possibile utilizzare qualsiasi toocreate di strumenti di sviluppo, l'applicazione o il blocco note.

> [!NOTE]
> L'installazione di PHP deve inoltre disporre hello [estensione OpenSSL](http://php.net/openssl) installato e abilitato.
> 
> 

In questa guida si useranno le funzionalità del servizio che possono essere chiamate da un'applicazione PHP in locale o nel codice in esecuzione in un ruolo Web, in un ruolo di lavoro o in un sito Web di Azure.

## <a name="get-hello-azure-client-libraries"></a>Recuperare le librerie client di Azure hello
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-toouse-service-bus"></a>Configurare il toouse applicazione Bus di servizio
coda di Service Bus hello toouse API, hello seguenti:

1. File di riferimento autoloader hello utilizzando hello [require_once] [ require_once] istruzione.
2. Fare riferimento a tutte le eventuali classi utilizzabili.

Hello esempio seguente viene illustrato come tooinclude hello hello di file e riferimento autoloader `ServicesBuilder` classe.

> [!NOTE]
> In questo esempio (e altri esempi in questo articolo) presuppone installate le librerie Client di PHP hello per Azure tramite creazione. Se è installato librerie hello manualmente o come un pacchetto di PERA, è necessario fare riferimento hello **WindowsAzure.php** autoloader file.
> 
> 

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;
```

Negli esempi di hello riportato di seguito, hello `require_once` istruzione verrà sempre visualizzata, ma solo hello classi necessarie per tooexecute esempio hello viene fatto riferimento.

## <a name="set-up-a-service-bus-connection"></a>Configurare una stringa di connessione per il bus di servizio
tooinstantiate un client del Bus di servizio, è necessario disporre prima di tutto una stringa di connessione valido nel formato seguente:

```
Endpoint=[yourEndpoint];SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[Primary Key]
```

Dove `Endpoint` è in genere in formato di hello `[yourNamespace].servicebus.windows.net`.

toocreate qualsiasi client di servizio di Azure, è necessario utilizzare hello `ServicesBuilder` classe. È possibile:

* Passare la connessione hello tooit direttamente di stringa.
* Hello utilizzare **CloudConfigurationManager (CCM)** toocheck origini dati esterne di più origini per la stringa di connessione hello:
  * Per impostazione predefinita viene fornito con il supporto per un'origine esterna, ovvero le variabili ambientali
  * È possibile aggiungere nuove origini estendendo hello `ConnectionStringSource` classe

Per esempi di hello descritti di seguito, la stringa di connessione hello viene passata direttamente.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$connectionString = "Endpoint=[yourEndpoint];SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[Primary Key]";

$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);
```

## <a name="create-a-queue"></a>Creare una coda
È possibile eseguire operazioni di gestione per le code del Bus di servizio tramite hello `ServiceBusRestProxy` classe. Oggetto `ServiceBusRestProxy` oggetto viene costruito tramite hello `ServicesBuilder::createServiceBusService` metodo factory con una stringa di connessione appropriata che incapsula toomanage autorizzazioni token hello è.

Hello seguente esempio viene illustrato come tooinstantiate un `ServiceBusRestProxy` e chiamare `ServiceBusRestProxy->createQueue` toocreate una coda denominata `myqueue` all'interno di un `MySBNamespace` spazio dei nomi servizio:

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use WindowsAzure\Common\ServiceException;
use WindowsAzure\ServiceBus\Models\QueueInfo;

// Create Service Bus REST proxy.
$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);

try    {
    $queueInfo = new QueueInfo("myqueue");

    // Create queue.
    $serviceBusRestProxy->createQueue($queueInfo);
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
> È possibile utilizzare hello `listQueues` metodo `ServiceBusRestProxy` oggetti toocheck se una coda con un nome specificato esiste già all'interno di uno spazio dei nomi.
> 
> 

## <a name="send-messages-tooa-queue"></a>Messaggi tooa coda di invio
una coda di Service Bus di messaggi tooa toosend, l'applicazione chiama hello `ServiceBusRestProxy->sendQueueMessage` metodo. Hello seguente codice mostra come toosend toohello un messaggio `myqueue` coda creata in precedenza all'interno di `MySBNamespace` dello spazio dei nomi di servizio.

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
    $serviceBusRestProxy->sendQueueMessage("myqueue", $message);
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

I messaggi inviate troppo (e ricevute da) code di Service Bus sono istanze di hello [BrokeredMessage] [ BrokeredMessage] classe. [BrokeredMessage] [ BrokeredMessage] oggetti dispongono di un set di metodi e proprietà che sono proprietà specifiche dell'applicazione personalizzate usate toohold e un corpo di dati applicazione arbitrari standard.

Le code del Bus di servizio supportano una dimensione massima di 256 KB in hello [livello Standard](service-bus-premium-messaging.md) hello a 1 MB e [livello Premium](service-bus-premium-messaging.md). intestazione Hello, che include standard hello e le proprietà personalizzate dell'applicazione, può avere una dimensione massima di 64 KB. Non è previsto alcun limite per il numero di hello di messaggi contenuti in una coda, ma è un limite alla dimensione totale di hello di messaggi hello mantenuto da una coda. Il limite massimo della dimensione di una coda è di 5 GB.

## <a name="receive-messages-from-a-queue"></a>Ricevere messaggi da una coda

migliore modalità tooreceive messaggi Hello da una coda è toouse un `ServiceBusRestProxy->receiveQueueMessage` metodo. È possibile ricevere i messaggi in due modi diversi: [*ReceiveAndDelete*](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) e [*PeekLock*](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock). **PeekLock** hello predefinito.

Quando si utilizza [ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) modalità di ricezione è un'operazione singola cattura; vale a dire quando Bus di servizio riceve una richiesta di lettura per un messaggio in una coda, contrassegna il messaggio hello come usato e lo restituisce toohello applicazione. [ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) modalità modello più semplice di hello ed è adatta per scenari in cui un'applicazione in grado di tollerare non elabora un messaggio di evento hello di un errore. toounderstand, si consideri uno scenario in cui problemi relativi ai consumer hello hello di ricezione richiesta e quindi si blocca prima dell'elaborazione. Poiché verrà contrassegnato messaggio come usato, quindi quando un'applicazione hello viene riavviata e inizia a usare nuovamente i messaggi hello del Bus di servizio, risulterà perso messaggio hello che è stato consumato toohello precedente arresto anomalo del sistema.

Predefinita hello [PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock) modalità di ricezione di un messaggio diventa un'operazione in due fasi, che rende possibile toosupport applicazioni che non sono in grado di tollerare messaggi mancanti. Quando Service Bus riceve una richiesta, trova hello successivo messaggio toobe utilizzata, blocca tooprevent altri consumer di ricezione e lo restituisce quindi toohello applicazione. Dopo l'applicazione hello completa l'elaborazione messaggio hello o archiviarlo in modo affidabile per l'elaborazione futura, completa hello seconda fase di hello processo di ricezione, passando il messaggio hello ricevuto troppo`ServiceBusRestProxy->deleteMessage`. Quando il Bus di servizio rileva hello `deleteMessage` chiamata, verrà contrassegnare il messaggio hello come usato e rimuoverlo dalla coda hello.

Hello seguente esempio viene illustrato come tooreceive ed elaborare un messaggio utilizzando [PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock) modalità (hello predefinita).

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use WindowsAzure\Common\ServiceException;
use WindowsAzure\ServiceBus\Models\ReceiveMessageOptions;

// Create Service Bus REST proxy.
$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);

try    {
    // Set hello receive mode tooPeekLock (default is ReceiveAndDelete).
    $options = new ReceiveMessageOptions();
    $options->setPeekLock();

    // Receive message.
    $message = $serviceBusRestProxy->receiveQueueMessage("myqueue", $options);
    echo "Body: ".$message->getBody()."<br />";
    echo "MessageID: ".$message->getMessageId()."<br />";

    /*---------------------------
        Process message here.
    ----------------------------*/

    // Delete message. Not necessary if peek lock is not set.
    echo "Message deleted.<br />";
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

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a>Come si blocca toohandle applicazione e i messaggi illeggibili

Bus di servizio offre funzionalità toohelp che normalmente possibile correggere gli errori nell'applicazione o problemi di elaborazione di un messaggio. Se un'applicazione ricevente è in grado di tooprocess hello messaggio per qualche motivo, quindi è possibile chiamare hello `unlockMessage` metodo sul messaggio ricevuto (anziché hello `deleteMessage` (metodo)). Ciò causerà messaggio hello toounlock di Bus di servizio all'interno di coda hello e renderlo disponibile toobe nuovamente ricevuto, sia da hello stesso consumo dell'applicazione o da un'altra applicazione consumer.

È inoltre disponibile un timeout associato a un messaggio bloccato all'interno di coda hello e se un'applicazione hello ha esito negativo messaggio hello tooprocess prima hello scadenza del timeout (ad esempio, se si blocca l'applicazione hello), quindi il Bus di servizio sbloccherà il messaggio hello automaticamente e renderlo disponibile toobe nuovamente ricevuto.

In hello evento hello applicazione si blocca dopo l'elaborazione messaggio hello ma prima di hello `deleteMessage` richiesta inviata, quindi messaggio hello sarà applicazione toohello consegnati nuovamente quando viene riavviata. Spesso si tratta di *almeno una volta che* l'elaborazione; ovvero, ogni messaggio viene elaborato almeno una volta ma in hello determinate situazioni potrebbe essere recapitato nuovamente stesso messaggio. Se hello scenario non tollera la doppia elaborazione, quindi l'aggiunta di ulteriori logica tooapplications toohandle duplicato il recapito dei messaggi. Questa operazione viene spesso eseguita utilizzando hello `getMessageId` metodo del messaggio hello, che rimane costante tra i tentativi di recapito.

## <a name="next-steps"></a>Passaggi successivi
Dopo aver appreso nozioni di base di hello di code del Bus di servizio, vedere [code, argomenti e sottoscrizioni] [ Queues, topics, and subscriptions] per ulteriori informazioni.

Per ulteriori informazioni, visitare anche hello [Centro sviluppatori PHP](https://azure.microsoft.com/develop/php/).

[BrokeredMessage]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[require_once]: http://php.net/require_once


