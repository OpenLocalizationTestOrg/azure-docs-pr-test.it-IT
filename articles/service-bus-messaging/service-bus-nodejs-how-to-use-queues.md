---
title: le code di aaaHow toouse Bus di servizio in Node.js | Documenti Microsoft
description: Informazioni su come code toouse Bus di servizio in Azure da un'app Node.js.
services: service-bus-messaging
documentationcenter: nodejs
author: sethmanheim
manager: timlt
editor: 
ms.assetid: a87a00f9-9aba-4c49-a0df-f900a8b67b3f
ms.service: service-bus-messaging
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm
ms.openlocfilehash: c55354b2061c41aba1093cc3f12ce2a1bc37a3cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-queues-with-nodejs"></a>La modalità di code toouse Bus di servizio con Node.js

[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

In questo articolo viene descritto come toouse Bus di servizio code con Node.js. esempi di Hello scritte in JavaScript e usare il modulo di Node.js Azure hello. Hello scenari trattati includono **la creazione delle code**, **inviando e ricevendo messaggi**, e **l'eliminazione di code**. Per ulteriori informazioni sulle code, vedere hello [passaggi successivi](#next-steps) sezione.

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="create-a-nodejs-application"></a>Creare un'applicazione Node.js
Creare un'applicazione Node.js vuota. Per istruzioni su come toocreate un'applicazione Node.js, vedere [creare e distribuire un tooan di applicazione del sito Web di Azure Node.js][Create and deploy a Node.js application tooan Azure Website], o [servizio Cloud Node.js] [ Node.js Cloud Service] tramite Windows PowerShell.

## <a name="configure-your-application-toouse-service-bus"></a>Configurare il toouse applicazione Bus di servizio
toouse Service Bus di Azure, scaricare e usare il pacchetto di Node.js Azure hello. Il pacchetto include un set di librerie che comunicano con servizi di Service Bus REST hello.

### <a name="use-node-package-manager-npm-tooobtain-hello-package"></a>Utilizzare un pacchetto di hello tooobtain nodo Package Manager (NPM)
1. Hello utilizzare **Windows PowerShell per Node.js** toohello toonavigate finestra di comando **c:\\nodo\\sbqueues\\WebRole1** cartella in cui è stato creato il applicazione di esempio.
2. Tipo **npm installare azure** nella finestra di comando hello, che dovrebbe restituire seguente toohello simili di output:

    ```
    azure@0.7.5 node_modules\azure
        ├── dateformat@1.0.2-1.2.3
        ├── xmlbuilder@0.4.2
        ├── node-uuid@1.2.0
        ├── mime@1.2.9
        ├── underscore@1.4.4
        ├── validator@1.1.1
        ├── tunnel@0.0.2
        ├── wns@0.5.3
        ├── xml2js@0.2.7 (sax@0.5.2)
        └── request@2.21.0 (json-stringify-safe@4.0.0, forever-agent@0.5.0, aws-sign@0.3.0, tunnel-agent@0.3.0, oauth-sign@0.3.0, qs@0.6.5, cookie-jar@0.3.0, node-uuid@1.4.0, http-signature@0.9.11, form-data@0.0.8, hawk@0.13.1)
    ```
3. È possibile eseguire manualmente hello **ls** comando tooverify che un **node_modules** cartella è stata creata. All'interno di tale hello Trova cartella **azure** pacchetto che contiene le librerie di hello necessarie tooaccess code del Bus di servizio.

### <a name="import-hello-module"></a>Modulo di importazione hello
Utilizzando blocco note o un altro editor di testo, aggiungere hello seguente toohello cima hello **server.js** file dell'applicazione hello:

```javascript
var azure = require('azure');
```

### <a name="set-up-an-azure-service-bus-connection"></a>Configurare una connessione del bus di servizio di Azure
modulo di Azure Hello legge la variabile di ambiente hello `AZURE_SERVICEBUS_CONNECTION_STRING` tooobtain informazioni necessarie tooconnect tooService Bus. Se questa variabile di ambiente non è impostata, è necessario specificare le informazioni sull'account hello quando si chiama `createServiceBusService`.

Per un esempio di impostazione delle variabili di ambiente di hello in un file di configurazione per un servizio Cloud di Azure, vedere [servizio Cloud Node.js con archiviazione][Node.js Cloud Service with Storage].

Per un esempio di impostazione delle variabili di ambiente hello in hello [portale di Azure] [ Azure portal] per un sito Web di Azure, vedere [applicazione Web Node.js con archiviazione] [ Node.js Web Application with Storage].

## <a name="create-a-queue"></a>Creare una coda
Hello **ServiceBusService** consente toowork con le code del Bus di servizio. Hello codice seguente viene creata una **ServiceBusService** oggetto. Aggiungerlo parte superiore di hello di hello **server.js** file hello tooimport di istruzione hello modulo di Azure:

```javascript
var serviceBusService = azure.createServiceBusService();
```

Chiamando `createQueueIfNotExists` su hello **ServiceBusService** oggetto, viene creata una nuova coda con il nome specificato hello o hello specificato coda viene restituita (se presente). codice Hello seguente usa `createQueueIfNotExists` toocreate o connettersi coda toohello denominata `myqueue`:

```javascript
serviceBusService.createQueueIfNotExists('myqueue', function(error){
    if(!error){
        // Queue exists
    }
});
```

Hello `createServiceBusService` metodo supporta inoltre opzioni aggiuntive, che consentono di impostazioni di coda toooverride predefinite, ad esempio dimensioni toolive o massimo in una coda in fase di messaggio. Hello esempio seguente imposta GB too5 dimensioni massime della coda di hello e un valore di (durata TTL) toolive ora di 1 minuto:

```javascript
var queueOptions = {
      MaxSizeInMegabytes: '5120',
      DefaultMessageTimeToLive: 'PT1M'
    };

serviceBusService.createQueueIfNotExists('myqueue', queueOptions, function(error){
    if(!error){
        // Queue exists
    }
});
```

### <a name="filters"></a>Filtri
Operazioni di filtro facoltative possono essere applicato toooperations eseguita utilizzando **ServiceBusService**. Le operazioni di filtro possono includere la registrazione, la ripetizione automatica dei tentativi e così via. I filtri sono oggetti che implementano un metodo con firma hello:

```javascript
function handle (requestOptions, next)
```

Dopo aver eseguito il pre-elaborazione sulle opzioni di richiesta di hello, è necessario chiamare il metodo hello `next`, passando un callback con hello seguente firma:

```javascript
function (returnObject, finalCallback, next)
```

In questo callback e dopo l'elaborazione hello `returnObject` (hello risposta dal server di hello richiesta toohello), deve richiamare il callback di hello `next` se esiste toocontinue l'elaborazione di altri filtri, o semplicemente richiamare `finalCallback`, che termina chiamata del servizio Hello.

Due filtri, che implementano la logica di ripetizione sono inclusi in Azure SDK per Node.js, hello `ExponentialRetryPolicyFilter` e `LinearRetryPolicyFilter`. Hello codice seguente viene creata una `ServiceBusService` oggetto che utilizza hello `ExponentialRetryPolicyFilter`:

```javascript
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var serviceBusService = azure.createServiceBusService().withFilter(retryOperations);
```

## <a name="send-messages-tooa-queue"></a>Messaggi tooa coda di invio
una coda di Service Bus di messaggi tooa toosend, l'applicazione chiama hello `sendQueueMessage` metodo hello **ServiceBusService** oggetto. I messaggi inviati troppo (e ricevuti da) Bus di servizio, le code sono **BrokeredMessage** oggetti e di disporre di un set di proprietà standard (ad esempio **etichetta** e **TimeToLive**), dizionario di proprietà specifiche dell'applicazione personalizzate usate toohold e un corpo di dati applicazione arbitrari. Un'applicazione può impostare il corpo di hello del messaggio hello passando una stringa come messaggio hello. Le proprietà standard necessarie vengono popolate con i valori predefiniti.

Hello esempio seguente viene illustrato come toosend una coda toohello test denominati `myqueue` utilizzando `sendQueueMessage`:

```javascript
var message = {
    body: 'Test message',
    customProperties: {
        testproperty: 'TestValue'
    }};
serviceBusService.sendQueueMessage('myqueue', message, function(error){
    if(!error){
        // message sent
    }
});
```

Le code del Bus di servizio supportano una dimensione massima di 256 KB in hello [livello Standard](service-bus-premium-messaging.md) hello a 1 MB e [livello Premium](service-bus-premium-messaging.md). intestazione Hello, che include standard hello e le proprietà personalizzate dell'applicazione, può avere una dimensione massima di 64 KB. Non è previsto alcun limite per il numero di hello di messaggi contenuti in una coda, ma è un limite alla dimensione totale di hello di messaggi hello mantenuto da una coda. Questa dimensione della coda viene definita al momento della creazione, con un limite massimo di 5 GB. Per altre informazioni sulle quote, vedere [Quote del bus di servizio][Service Bus quotas].

## <a name="receive-messages-from-a-queue"></a>Ricevere messaggi da una coda
I messaggi vengono ricevuti da una coda utilizzando hello `receiveQueueMessage` metodo hello **ServiceBusService** oggetto. Per impostazione predefinita, i messaggi vengono eliminati dalla coda di hello quando vengono letti; Tuttavia, è possibile leggere (anteprima) e bloccare il messaggio hello senza eliminarla dalla coda hello dal parametro facoltativo hello impostazione `isPeekLock` troppo**true**.

Hello il comportamento predefinito di lettura e l'eliminazione del messaggio hello come parte di hello l'operazione di ricezione è il modello più semplice di hello e adatto per scenari in cui un'applicazione in grado di tollerare non elabora un messaggio di evento hello di un errore. toounderstand, si consideri uno scenario in cui problemi relativi ai consumer hello hello di ricezione richiesta e quindi si blocca prima dell'elaborazione. Poiché verrà contrassegnato messaggio come usato, quindi quando un'applicazione hello viene riavviata e inizia a usare nuovamente i messaggi hello del Bus di servizio, risulterà perso messaggio hello che è stato consumato toohello precedente arresto anomalo del sistema.

Se hello `isPeekLock` parametro è impostato troppo**true**, hello ricezione diventa un'operazione in due fasi, che rende possibile toosupport applicazioni che non sono in grado di tollerare messaggi mancanti. Quando il Bus di servizio riceve una richiesta, individua hello successivo messaggio toobe utilizzati Blocca tooprevent altri consumer di ricezione e lo restituisce quindi toohello applicazione. Dopo l'applicazione hello completa l'elaborazione messaggio hello o archiviarlo in modo affidabile per l'elaborazione futura, completa hello seconda fase di hello ricevere processo chiamando `deleteMessage` (metodo) e fornendo toobe messaggio hello eliminato come parametro. Hello `deleteMessage` metodo contrassegna il messaggio hello come usato e la rimuove dalla coda hello.

Hello esempio seguente viene illustrato come tooreceive ed elaborare messaggi utilizzando `receiveQueueMessage`. Hello esempio riceve un messaggio viene eliminato e quindi riceve un messaggio utilizzando `isPeekLock` impostare troppo**true**, quindi Elimina hello messaggio utilizzando `deleteMessage`:

```javascript
serviceBusService.receiveQueueMessage('myqueue', function(error, receivedMessage){
    if(!error){
        // Message received and deleted
    }
});
serviceBusService.receiveQueueMessage('myqueue', { isPeekLock: true }, function(error, lockedMessage){
    if(!error){
        // Message received and locked
        serviceBusService.deleteMessage(lockedMessage, function (deleteError){
            if(!deleteError){
                // Message deleted
            }
        });
    }
});
```

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a>Come si blocca toohandle applicazione e i messaggi illeggibili
Bus di servizio offre funzionalità toohelp che normalmente possibile correggere gli errori nell'applicazione o problemi di elaborazione di un messaggio. Se un'applicazione ricevente è in grado di tooprocess hello messaggio per qualche motivo, quindi è possibile chiamare hello `unlockMessage` metodo hello **ServiceBusService** oggetto. Ciò causerà Bus di servizio toounlock il messaggio nella coda di hello e renderlo disponibile toobe nuovamente ricevuto, sia da hello stesso consumo dell'applicazione o da un'altra applicazione consumer.

È inoltre disponibile un timeout associato a un messaggio bloccato all'interno di coda hello e se hello ha esito negativo dell'applicazione hello tooprocess hello messaggio prima della scadenza del timeout (ad esempio, se si blocca l'applicazione hello), quindi il Bus di servizio sbloccherà il messaggio hello e renderlo disponibile toobe nuovamente ricevuto.

In hello evento hello applicazione si blocca dopo l'elaborazione messaggio hello ma prima di hello `deleteMessage` metodo viene chiamato, quindi il messaggio hello sarà applicazione toohello consegnati nuovamente quando si riavvia. Spesso si tratta di *almeno una volta elaborazione*, vale a dire, ogni messaggio verrà elaborato almeno una volta ma in hello determinate situazioni potrebbe essere recapitato nuovamente stesso messaggio. Se hello scenario non tollera la doppia elaborazione, gli sviluppatori di applicazioni devono aggiungere logica aggiuntiva tootheir applicazione toohandle duplicato il recapito dei messaggi. Questa operazione viene spesso eseguita utilizzando hello **MessageId** proprietà di messaggio hello che rimangono costante tra i tentativi di recapito.

## <a name="next-steps"></a>Passaggi successivi
toolearn più sulle code, vedere hello seguenti risorse.

* [Code, argomenti e sottoscrizioni del bus di servizio][Queues, topics, and subscriptions]
* Repository [Azure SDK per Node][Azure SDK for Node] su GitHub
* [Centro per sviluppatori di Node.js](https://azure.microsoft.com/develop/nodejs/)

[Azure SDK for Node]: https://github.com/Azure/azure-sdk-for-node
[Azure portal]: https://portal.azure.com

[Node.js Cloud Service]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[Create and deploy a Node.js application tooan Azure Website]: ../app-service-web/app-service-web-get-started-nodejs.md
[Node.js Cloud Service with Storage]:../cosmos-db/table-storage-cloud-service-nodejs.md
[Node.js Web Application with Storage]:../cosmos-db/table-storage-how-to-use-nodejs.md
[Service Bus quotas]: service-bus-quotas.md
