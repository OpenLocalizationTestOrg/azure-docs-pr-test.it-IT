---
title: aaaHow toouse Azure Service Bus argomenti e sottoscrizioni con Node.js | Documenti Microsoft
description: Informazioni su come toouse Bus di servizio di argomenti e sottoscrizioni in Azure da un'app Node.js.
services: service-bus-messaging
documentationcenter: nodejs
author: sethmanheim
manager: timlt
editor: 
ms.assetid: b9f5db85-7b6c-4cc7-bd2c-bd3087c99875
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm
ms.openlocfilehash: e8f6e7ad6ed16d844c408337ac9e50f990e3fafd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-topics-and-subscriptions-with-nodejs"></a>Il Bus di servizio tooUse argomenti e sottoscrizioni con Node.js

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

Questa guida viene descritto come toouse Bus di servizio di argomenti e sottoscrizioni dalle applicazioni Node.js. Hello scenari trattati includono **la creazione di argomenti e sottoscrizioni**, **creazione filtri di sottoscrizione**, **l'invio di messaggi** tooa argomento **ricezione i messaggi da una sottoscrizione**, e **l'eliminazione di argomenti e sottoscrizioni**. Per ulteriori informazioni su argomenti e sottoscrizioni, vedere hello [passaggi successivi](#next-steps) sezione.

[!INCLUDE [howto-service-bus-topics](../../includes/howto-service-bus-topics.md)]

## <a name="create-a-nodejs-application"></a>Creare un'applicazione Node.js
Creare un'applicazione Node.js vuota. Per istruzioni sulla creazione di un'applicazione Node.js, vedere [creare e distribuire un tooan di applicazione del sito Web di Azure Node.js], [servizio Cloud Node.js] [ Node.js Cloud Service] utilizzando Windows PowerShell o il sito Web con WebMatrix.

## <a name="configure-your-application-toouse-service-bus"></a>Configurare il toouse applicazione Bus di servizio
toouse Service Bus, scaricare il pacchetto di Node.js Azure hello. Il pacchetto include un set di librerie che comunicano con servizi di Service Bus REST hello.

### <a name="use-node-package-manager-npm-tooobtain-hello-package"></a>Utilizzare un pacchetto di hello tooobtain nodo Package Manager (NPM)
1. Utilizzare un'interfaccia della riga di comando, ad esempio **PowerShell** (Windows), **Terminal** (Mac), o **Bash** (Unix), passare toohello cartella in cui è stato creato l'applicazione di esempio.
2. Tipo **npm installare azure** nella finestra di comando hello, che dovrebbe restituire hello seguente output:

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
3. È possibile eseguire manualmente hello **ls** comando tooverify che un **nodo\_moduli** cartella è stata creata. All'interno di tale cartella è possibile trovare il **azure** pacchetto che contiene le librerie di hello necessarie tooaccess argomenti del Bus di servizio.

### <a name="import-hello-module"></a>Modulo di importazione hello
Utilizzando blocco note o un altro editor di testo, aggiungere hello seguente toohello cima hello **server.js** file dell'applicazione hello:

```javascript
var azure = require('azure');
```

### <a name="set-up-a-service-bus-connection"></a>Configurare una stringa di connessione per il bus di servizio
Hello Azure modulo legge le variabili di ambiente hello `AZURE_SERVICEBUS_NAMESPACE` e `AZURE_SERVICEBUS_ACCESS_KEY` per le informazioni necessarie tooconnect tooService Bus. Se non vengono impostate queste variabili di ambiente, è necessario specificare le informazioni sull'account hello quando si chiama `createServiceBusService`.

Per un esempio di impostazione delle variabili di ambiente hello per un servizio Cloud di Azure, vedere [servizio Cloud Node.js con archiviazione][Node.js Cloud Service with Storage].

Per un esempio di impostazione delle variabili di ambiente hello per un sito Web di Azure, vedere [applicazione Web Node.js con archiviazione][Node.js Web Application with Storage].

## <a name="create-a-topic"></a>Creare un argomento
Hello **ServiceBusService** consente toowork con argomenti. Il codice seguente consente di creare un oggetto **ServiceBusService**. Aggiungerlo nella parte superiore di hello **server.js** file, dopo il modulo di hello istruzione tooimport hello azure:

```javascript
var serviceBusService = azure.createServiceBusService();
```

Chiamando `createTopicIfNotExists` su hello **ServiceBusService** oggetto, verrà creato un nuovo argomento con il nome specificato hello o hello specificato verrà restituito l'argomento (se presente). codice Hello seguente usa `createTopicIfNotExists` toocreate o connettersi toohello argomento denominato `MyTopic`:

```javascript
serviceBusService.createTopicIfNotExists('MyTopic',function(error){
    if(!error){
        // Topic was created or exists
        console.log('topic created or exists.');
    }
});
```

Hello `createServiceBusService` metodo supporta inoltre opzioni aggiuntive, che consentono di determinare le impostazioni dell'argomento predefinito toooverride, ad esempio durata messaggio o la dimensione massima dell'argomento. Hello esempio seguente imposta too5GB di dimensione massima dell'argomento hello con un tempo toolive di 1 minuto:

```javascript
var topicOptions = {
        MaxSizeInMegabytes: '5120',
        DefaultMessageTimeToLive: 'PT1M'
    };

serviceBusService.createTopicIfNotExists('MyTopic', topicOptions, function(error){
    if(!error){
        // topic was created or exists
    }
});
```

### <a name="filters"></a>Filtri
Operazioni di filtro facoltative possono essere applicato toooperations eseguita utilizzando **ServiceBusService**. Le operazioni di filtro possono includere la registrazione, la ripetizione automatica dei tentativi e così via. I filtri sono oggetti che implementano un metodo con firma hello:

```javascript
function handle (requestOptions, next)
```

Dopo l'esecuzione di pre-elaborazione sulle opzioni di richiesta di hello, hello chiamate al metodo `next`, passando un callback con hello seguente firma:

```javascript
function (returnObject, finalCallback, next)
```

In questo callback e dopo l'elaborazione hello `returnObject` (hello risposta dal server di hello richiesta toohello), il callback di hello richiede tooeither richiamare successivamente se esiste l'elaborazione di altri filtri toocontinue o richiamare `finalCallback` hello tooend in caso contrario, chiamata del servizio.

Due filtri, che implementano la logica di ripetizione sono inclusi in Azure SDK per Node.js, hello **ExponentialRetryPolicyFilter** e **LinearRetryPolicyFilter**. Hello seguito creato un **ServiceBusService** oggetto che utilizza hello **ExponentialRetryPolicyFilter**:

```javascript
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var serviceBusService = azure.createServiceBusService().withFilter(retryOperations);
```

## <a name="create-subscriptions"></a>Creare sottoscrizioni
Le sottoscrizioni dell'argomento vengono inoltre create con hello **ServiceBusService** oggetto. Le sottoscrizioni sono denominate e possono avere un filtro facoltativo che limita il set di hello di messaggi recapitati coda virtuale toohello della sottoscrizione.

> [!NOTE]
> Le sottoscrizioni sono permanenti e continueranno tooexist finché uno non o hello argomento sono associati, vengono eliminati. Se l'applicazione contiene la logica toocreate una sottoscrizione, deve verificare se hello sottoscrizione esiste già con il `getSubscription` metodo.
>
>

### <a name="create-a-subscription-with-hello-default-matchall-filter"></a>Creare una sottoscrizione con filtro predefinito (MatchAll) hello
Hello **MatchAll** filtro è hello predefinito che viene utilizzato se viene specificato alcun filtro quando viene creata una nuova sottoscrizione. Quando hello **MatchAll** filtro viene utilizzato, l'argomento di toohello pubblicati tutti i messaggi vengono inseriti nella coda virtuale della sottoscrizione. esempio Hello crea una sottoscrizione denominata 'AllMessages' e utilizza hello predefinito **MatchAll** filtro.

```javascript
serviceBusService.createSubscription('MyTopic','AllMessages',function(error){
    if(!error){
        // subscription created
    }
});
```

### <a name="create-subscriptions-with-filters"></a>Creare sottoscrizioni con i filtri
È anche possibile creare filtri che consentono di tooscope cui i messaggi inviati tooa argomento visualizzati all'interno di una sottoscrizione di argomento specifico.

Hello più flessibile il tipo di filtro supportato dalle sottoscrizioni è il **SqlFilter**, che implementa un subset di SQL92. I filtri SQL operano sulle proprietà hello dei messaggi hello argomento toohello pubblicato. Per ulteriori informazioni sulle espressioni hello che possono essere utilizzate con un filtro SQL, vedere hello [SqlFilter.SqlExpression] [ SqlFilter.SqlExpression] sintassi.

È possibile aggiungere filtri tooa sottoscrizione utilizzando hello `createRule` metodo hello **ServiceBusService** oggetto. Questo metodo consente di aggiungere nuovi filtri tooan sottoscrizione.

> [!NOTE]
> Poiché il filtro predefinito hello viene applicato automaticamente tooall nuove sottoscrizioni, è necessario innanzitutto rimuovere filtro predefinito hello o **MatchAll** sostituirà gli altri filtri che è possibile specificare. È possibile rimuovere una regola predefinita hello utilizzando hello `deleteRule` metodo il **ServiceBusService** oggetto.
>
>

esempio Hello crea una sottoscrizione denominata `HighMessages` con un **SqlFilter** che seleziona solo i messaggi con un oggetto personalizzato `messagenumber` maggiore di 3:

```javascript
serviceBusService.createSubscription('MyTopic', 'HighMessages', function (error){
    if(!error){
        // subscription created
        rule.create();
    }
});
var rule={
    deleteDefault: function(){
        serviceBusService.deleteRule('MyTopic',
            'HighMessages',
            azure.Constants.ServiceBusConstants.DEFAULT_RULE_NAME,
            rule.handleError);
    },
    create: function(){
        var ruleOptions = {
            sqlExpressionFilter: 'messagenumber > 3'
        };
        rule.deleteDefault();
        serviceBusService.createRule('MyTopic',
            'HighMessages',
            'HighMessageFilter',
            ruleOptions,
            rule.handleError);
    },
    handleError: function(error){
        if(error){
            console.log(error)
        }
    }
}
```

Analogamente, hello esempio seguente viene creata una sottoscrizione denominata `LowMessages` con un **SqlFilter** che seleziona solo i messaggi che hanno un `messagenumber` proprietà minore o uguale too3:

```javascript
serviceBusService.createSubscription('MyTopic', 'LowMessages', function (error){
    if(!error){
        // subscription created
        rule.create();
    }
});
var rule={
    deleteDefault: function(){
        serviceBusService.deleteRule('MyTopic',
            'LowMessages',
            azure.Constants.ServiceBusConstants.DEFAULT_RULE_NAME,
            rule.handleError);
    },
    create: function(){
        var ruleOptions = {
            sqlExpressionFilter: 'messagenumber <= 3'
        };
        rule.deleteDefault();
        serviceBusService.createRule('MyTopic',
            'LowMessages',
            'LowMessageFilter',
            ruleOptions,
            rule.handleError);
    },
    handleError: function(error){
        if(error){
            console.log(error)
        }
    }
}
```

Quando viene inviato un messaggio ora troppo`MyTopic`, sempre essere recapitato ricevitori sottoscritti toohello `AllMessages` sottoscrizione dell'argomento e recapitati in modo selettivo tooreceivers sottoscritto toohello `HighMessages` e `LowMessages` le sottoscrizioni dell'argomento (in base al contenuto del messaggio hello).

## <a name="how-toosend-messages-tooa-topic"></a>La modalità toosend dei messaggi tooa argomento
un argomento del Bus di servizio tooa messaggio toosend, l'applicazione deve usare il `sendTopicMessage` metodo hello **ServiceBusService** oggetto.
I messaggi inviati sono argomenti del Bus tooService **BrokeredMessage** oggetti.
**BrokeredMessage** oggetti dispongono di un set di proprietà standard (ad esempio `Label` e `TimeToLive`), un dizionario di proprietà specifiche dell'applicazione personalizzate usate toohold e un corpo di dati di tipo stringa. Un'applicazione può impostare il corpo di hello del messaggio hello passando un valore di stringa a messaggi hello `sendTopicMessage` e le necessarie proprietà standard verranno popolate dai valori predefiniti.

Hello esempio seguente viene illustrato come toosend cinque messaggi di prova per `MyTopic`. Si noti che hello `messagenumber` valore della proprietà di ogni messaggio varia iterazione hello del ciclo di hello (per stabilire le sottoscrizioni che ricevano):

```javascript
var message = {
    body: '',
    customProperties: {
        messagenumber: 0
    }
}

for (i = 0;i < 5;i++) {
    message.customProperties.messagenumber=i;
    message.body='This is Message #'+i;
    serviceBusService.sendTopicMessage(topic, message, function(error) {
      if (error) {
        console.log(error);
      }
    });
}
```

Argomenti del Bus di servizio supportano una dimensione massima di 256 KB in hello [livello Standard](service-bus-premium-messaging.md) hello a 1 MB e [livello Premium](service-bus-premium-messaging.md). intestazione Hello, che include standard hello e le proprietà personalizzate dell'applicazione, può avere una dimensione massima di 64 KB. Non è previsto alcun limite per il numero di hello di messaggi contenuti in un argomento, ma è un limite alla dimensione totale di hello di messaggi hello utilizzate da un argomento. Questa dimensione dell'argomento viene definita al momento della creazione, con un limite massimo di 5 GB.

## <a name="receive-messages-from-a-subscription"></a>Ricevere messaggi da una sottoscrizione
I messaggi vengono ricevuti da una sottoscrizione tramite il `receiveSubscriptionMessage` metodo hello **ServiceBusService** oggetto. Per impostazione predefinita, i messaggi vengono eliminati dalla sottoscrizione hello quando vengono letti; Tuttavia, è possibile leggere (anteprima) e bloccare il messaggio hello senza eliminarla dalla sottoscrizione hello dal parametro facoltativo hello impostazione `isPeekLock` troppo**true**.

comportamento predefinito di Hello di lettura e l'eliminazione del messaggio hello come parte dell'operazione di ricezione è il modello più semplice di hello ed è ideale per scenari in cui un'applicazione in grado di tollerare non elabora un messaggio di evento hello di un errore. toounderstand, si consideri uno scenario in cui il hello problemi consumer di ricezione richiesta e quindi si blocca prima dell'elaborazione. Poiché verrà contrassegnato messaggio come usato, quindi quando un'applicazione hello viene riavviata e inizia a usare nuovamente i messaggi hello del Bus di servizio, risulterà perso messaggio hello che è stato consumato toohello precedente arresto anomalo del sistema.

Se hello `isPeekLock` parametro è impostato troppo**true**, hello ricezione diventa un'operazione in due fasi, che rende possibile toosupport applicazioni che non sono in grado di tollerare messaggi mancanti. Quando il Bus di servizio riceve una richiesta, individua hello successivo messaggio toobe utilizzati Blocca tooprevent altri consumer di ricezione e lo restituisce quindi toohello applicazione.
Dopo l'applicazione hello completa l'elaborazione messaggio hello o archiviarlo in modo affidabile per l'elaborazione futura, completa hello seconda fase del processo di ricezione chiamando **deleteMessage** (metodo) e fornendo il toobe messaggio eliminato come parametro. Hello **deleteMessage** metodo contrassegna il messaggio hello come usato, ma verrà rimosso dalla sottoscrizione hello.

Hello esempio seguente viene illustrato come è possibile ricevere messaggi e trasformati utilizzando `receiveSubscriptionMessage`. Hello esempio riceve Elimina un messaggio dalla sottoscrizione 'LowMessages' hello e viene ricevuto un messaggio dalla sottoscrizione di 'HighMessages' hello utilizzando `isPeekLock` impostare tootrue. Elimina quindi il messaggio hello utilizzando `deleteMessage`:

```javascript
serviceBusService.receiveSubscriptionMessage('MyTopic', 'LowMessages', function(error, receivedMessage){
    if(!error){
        // Message received and deleted
        console.log(receivedMessage);
    }
});
serviceBusService.receiveSubscriptionMessage('MyTopic', 'HighMessages', { isPeekLock: true }, function(error, lockedMessage){
    if(!error){
        // Message received and locked
        console.log(lockedMessage);
        serviceBusService.deleteMessage(lockedMessage, function (deleteError){
            if(!deleteError){
                // Message deleted
                console.log('message has been deleted.');
            }
        }
    }
});
```

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a>Come si blocca toohandle applicazione e i messaggi illeggibili
Bus di servizio offre funzionalità toohelp che normalmente possibile correggere gli errori nell'applicazione o problemi di elaborazione di un messaggio. Se un'applicazione ricevente è in grado di tooprocess hello messaggio per qualche motivo, quindi è possibile chiamare hello `unlockMessage` metodo il **ServiceBusService** oggetto. Ciò causerà Bus di servizio toounlock il messaggio all'interno di sottoscrizione hello e renderlo disponibile toobe nuovamente ricevuto, sia da hello stesso consumo dell'applicazione o da un'altra applicazione consumer.

È inoltre disponibile un timeout associato a un messaggio bloccato all'interno della sottoscrizione, e se un'applicazione hello ha esito negativo messaggio hello tooprocess prima il timeout di blocco hello scade (ad esempio, se si blocca l'applicazione hello), quindi il Bus di servizio Sblocca messaggio hello automaticamente e lo rende disponibile toobe nuovamente ricevuto.

In hello evento hello applicazione si blocca dopo l'elaborazione messaggio hello ma prima di hello `deleteMessage` metodo viene chiamato, quindi il messaggio hello sarà applicazione toohello consegnati nuovamente quando si riavvia. Spesso si tratta di *almeno una volta elaborazione*, vale a dire, ogni messaggio verrà elaborato almeno una volta ma in hello determinate situazioni potrebbe essere recapitato nuovamente stesso messaggio. Se hello scenario non tollera la doppia elaborazione, gli sviluppatori di applicazioni devono aggiungere logica aggiuntiva tootheir applicazione toohandle duplicato il recapito dei messaggi. Questa operazione viene spesso eseguita mediante il **MessageId** proprietà di messaggio hello che rimangono costante tra i tentativi di recapito.

## <a name="delete-topics-and-subscriptions"></a>Eliminare argomenti e sottoscrizioni
Argomenti e sottoscrizioni sono persistenti e deve essere in modo esplicito tramite hello eliminato [portale di Azure] [ Azure portal] o a livello di codice.
Hello esempio seguente viene illustrato come argomento di hello toodelete denominati `MyTopic`:

```javascript
serviceBusService.deleteTopic('MyTopic', function (error) {
    if (error) {
        console.log(error);
    }
});
```

L'eliminazione di un argomento eliminerà anche le sottoscrizioni che sono registrate con l'argomento hello. Le sottoscrizioni possono essere eliminate anche in modo indipendente. Nell'esempio seguente viene illustrato come toodelete una sottoscrizione denominata `HighMessages` da hello `MyTopic` argomento:

```javascript
serviceBusService.deleteSubscription('MyTopic', 'HighMessages', function (error) {
    if(error) {
        console.log(error);
    }
});
```

## <a name="next-steps"></a>Passaggi successivi
Ora che si è appreso i concetti di base di hello di argomenti del Bus di servizio, seguire questi ulteriori toolearn di collegamenti.

* Vedere [Code, argomenti e sottoscrizioni del bus di servizio][Queues, topics, and subscriptions].
* Informazioni di riferimento sulle API per [SqlFilter][SqlFilter].
* Visitare hello [Azure SDK per nodo] [ Azure SDK for Node] repository in GitHub.

[Azure SDK for Node]: https://github.com/Azure/azure-sdk-for-node
[Azure portal]: https://portal.azure.com
[SqlFilter.SqlExpression]: service-bus-messaging-sql-filter.md
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[SqlFilter]: /dotnet/api/microsoft.servicebus.messaging.sqlfilter
[Node.js Cloud Service]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[Creare e distribuire un tooan applicazione Node.js sito Web di Azure]: ../app-service-web/app-service-web-get-started-nodejs.md
[Node.js Cloud Service with Storage]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[Node.js Web Application with Storage]:../cosmos-db/table-storage-cloud-service-nodejs.md
