---
title: aaaHow toouse archiviazione delle code da Node.js | Documenti Microsoft
description: Informazioni su come toouse hello Azure coda servizio toocreate e le code di delete e insert, ottenere ed eliminare i messaggi. Gli esempi sono scritti in Node.js.
services: storage
documentationcenter: nodejs
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: a8a92db0-4333-43dd-a116-28b3147ea401
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 12/08/2016
ms.author: robinsh
ms.openlocfilehash: 7e9778da4efa69f2e9d8fd480b9b6f5ace85951e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-queue-storage-from-nodejs"></a>Come toouse archiviazione delle code da Node.js
[!INCLUDE [storage-selector-queue-include](../../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-check-out-samples-all](../../../includes/storage-check-out-samples-all.md)]

## <a name="overview"></a>Panoramica
Questa guida viene illustrato come gli scenari comuni di tooperform utilizzando hello servizio di Accodamento di Microsoft Azure. esempi di Hello vengono scritti utilizzando hello API Node.js. Hello scenari trattati includono **inserimento**, **visualizzazione**, **recupero**, e **eliminazione** coda di messaggi, nonché  **Creazione ed eliminazione di code**.

[!INCLUDE [storage-queue-concepts-include](../../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-nodejs-application"></a>Creazione di un'applicazione Node.js
Creare un'applicazione Node.js vuota. Per istruzioni di creazione di un'applicazione Node.js, vedere [creare un'app web Node.js in Azure App Service](../../app-service-web/app-service-web-get-started-nodejs.md), [compilare e distribuire un tooan di applicazione del servizio Cloud di Azure Node.js](../../cloud-services/cloud-services-nodejs-develop-deploy-app.md) utilizzando Windows PowerShell o [ Compilare e distribuire un tooAzure di app web Node. js utilizzando WebMatrix](https://www.microsoft.com/web/webmatrix/).

## <a name="configure-your-application-tooaccess-storage"></a>Configurare l'applicazione tooAccess archiviazione
toouse archiviazione di Azure, è necessario hello Azure Storage SDK per Node.js, che include un set di librerie di praticità che comunicano con servizi REST di archiviazione hello.

### <a name="use-node-package-manager-npm-tooobtain-hello-package"></a>Utilizzare un pacchetto di hello tooobtain nodo Package Manager (NPM)
1. Utilizzare un'interfaccia della riga di comando, ad esempio **PowerShell** (Windows), **Terminal** (Mac), o **Bash** (Unix), passare toohello cartella in cui è stato creato l'applicazione di esempio.
2. Tipo **npm installare archiviazione di azure** nella finestra di comando hello. Output del comando hello è simile toohello esempio seguente.
 
    ```
    azure-storage@0.5.0 node_modules\azure-storage
    +-- extend@1.2.1
    +-- xmlbuilder@0.4.3
    +-- mime@1.2.11
    +-- node-uuid@1.4.3
    +-- validator@3.22.2
    +-- underscore@1.4.4
    +-- readable-stream@1.0.33 (string_decoder@0.10.31, isarray@0.0.1, inherits@2.0.1, core-util-is@1.0.1)
    +-- xml2js@0.2.7 (sax@0.5.2)
    +-- request@2.57.0 (caseless@0.10.0, aws-sign2@0.5.0, forever-agent@0.6.1, stringstream@0.0.4, oauth-sign@0.8.0, tunnel-agent@0.4.1, isstream@0.1.2, json-stringify-safe@5.0.1, bl@0.9.4, combined-stream@1.0.5, qs@3.1.0, mime-types@2.0.14, form-data@0.2.0, http-signature@0.11.0, tough-cookie@2.0.0, hawk@2.3.1, har-validator@1.8.0)
    ```

3. È possibile eseguire manualmente hello **ls** comando tooverify che un **nodo\_moduli** cartella è stata creata. Questa cartella si troverà hello **archiviazione di azure** pacchetto che contiene le librerie di hello necessarie per accedere all'archiviazione.

### <a name="import-hello-package"></a>Importa pacchetto di hello
Utilizzando blocco note o un altro editor di testo, aggiungere hello seguente toohello superiore di **server.js** file dell'applicazione hello in cui si intende toouse archiviazione:

```
var azure = require('azure-storage');
```

## <a name="setup-an-azure-storage-connection"></a>Configurare una connessione di archiviazione di Azure
modulo Hello azure verrà lette le variabili di ambiente hello AZURE\_archiviazione\_ACCOUNT e AZURE\_archiviazione\_accesso\_chiave o AZURE\_archiviazione\_connessione \_Stringa per le informazioni necessarie tooconnect tooyour account di archiviazione di Azure. Se non vengono impostate queste variabili di ambiente, è necessario specificare le informazioni sull'account hello quando si chiama **createQueueService**.

Per un esempio di impostazione delle variabili di ambiente hello in hello [portale Azure](https://portal.azure.com) per un sito Web di Azure, vedere [Node.js app web utilizzando] hello del servizio tabelle di Azure.

## <a name="how-to-create-a-queue"></a>Procedura: creare una coda
Hello codice seguente viene creata una **QueueService** oggetto, che consente di toowork con le code.

```
var queueSvc = azure.createQueueService();
```

Hello utilizzare **createQueueIfNotExists** metodo, che restituisce la coda specificata hello se già esistente o crea una nuova coda con il nome specificato hello se non esiste già.

```
queueSvc.createQueueIfNotExists('myqueue', function(error, result, response){
  if(!error){
    // Queue created or exists
  }
});
```

Se viene creata la coda hello, `result.created` è true. Se non esiste, la coda hello `result.created` è false.

### <a name="filters"></a>Filtri
Operazioni di filtro facoltative possono essere applicato toooperations eseguita utilizzando **QueueService**. Le operazioni di filtro possono includere la registrazione, la ripetizione automatica dei tentativi e così via. I filtri sono oggetti che implementano un metodo con firma hello:

```
function handle (requestOptions, next)
```

Dopo aver eseguito il pre-elaborazione sulle opzioni di richiesta di hello, metodo hello deve toocall "Avanti" passaggio di un callback con hello seguente firma:

```
function (returnObject, finalCallback, next)
```

In questo callback e dopo l'elaborazione di hello returnObject (risposta hello dal server di hello richiesta toohello), il callback di hello richiede tooeither richiamare successivamente se esiste l'elaborazione di altri filtri toocontinue o semplicemente richiamare finalCallback tooend in caso contrario di hello chiamata del servizio.

Due filtri, che implementano la logica di ripetizione sono inclusi in Azure SDK per Node.js, hello **ExponentialRetryPolicyFilter** e **LinearRetryPolicyFilter**. Hello seguito creato un **QueueService** oggetto che utilizza hello **ExponentialRetryPolicyFilter**:

```
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var queueSvc = azure.createQueueService().withFilter(retryOperations);
```

## <a name="how-to-insert-a-message-into-a-queue"></a>Procedura: inserire un messaggio in una coda
un messaggio in una coda, utilizzare hello tooinsert **createMessage** per creare un nuovo messaggio e aggiungerlo toohello coda.

```
queueSvc.createMessage('myqueue', "Hello world!", function(error, result, response){
  if(!error){
    // Message inserted
  }
});
```

## <a name="how-to-peek-at-hello-next-message"></a>Procedura: Leggere hello messaggio successivo
È possibile anche visualizzare il messaggio hello nella parte anteriore hello di una coda senza rimuoverlo dalla coda hello dal chiamante hello **peekMessages** metodo. Per impostazione predefinita, **peekMessages** visualizza un singolo messaggio.

```
queueSvc.peekMessages('myqueue', function(error, result, response){
  if(!error){
    // Message text is in messages[0].messageText
  }
});
```

Hello `result` contiene il messaggio hello.

> [!NOTE]
> Utilizzando **peekMessages** quando non sono presenti messaggi nella coda di hello non restituirà un errore, tuttavia non verrà restituito alcun messaggio.
> 
> 

## <a name="how-to-dequeue-hello-next-message"></a>Procedura: Rimozione dalla coda hello messaggio successivo
L'elaborazione di un messaggio prevede un processo a due fasi:

1. Rimozione dalla coda il messaggio hello.
2. Eliminare il messaggio hello.

Utilizzare un messaggio, toodequeue **getMessages**. In questo modo, i messaggi hello invisibile nella coda di hello, pertanto nessun altro client possa elaborarli. Dopo l'applicazione ha elaborato un messaggio, chiamare **deleteMessage** toodelete dalla coda hello. Hello di esempio seguente ottiene un messaggio, quindi eliminarlo:

```
queueSvc.getMessages('myqueue', function(error, result, response){
  if(!error){
    // Message text is in messages[0].messageText
    var message = result[0];
    queueSvc.deleteMessage('myqueue', message.messageId, message.popReceipt, function(error, response){
      if(!error){
        //message deleted
      }
    });
  }
});
```

> [!NOTE]
> Per impostazione predefinita, un messaggio è nascosto solo per 30 secondi, trascorso il quale è visibile tooother client. È possibile specificare un valore diverso usando `options.visibilityTimeout` con **getMessages**.
> 
> [!NOTE]
> Utilizzando **getMessages** quando non sono presenti messaggi nella coda di hello non restituirà un errore, tuttavia non verrà restituito alcun messaggio.
> 
> 

## <a name="how-to-change-hello-contents-of-a-queued-message"></a>Procedura: Modificare il contenuto di hello di un messaggio in coda
È possibile modificare il contenuto di hello di un messaggio sul posto nel hello coda tramite **updateMessage**. Hello di esempio seguente aggiorna il testo hello di un messaggio:

```
queueSvc.getMessages('myqueue', function(error, result, response){
  if(!error){
    // Got hello message
    var message = result[0];
    queueSvc.updateMessage('myqueue', message.messageId, message.popReceipt, 10, {messageText: 'new text'}, function(error, result, response){
      if(!error){
        // Message updated successfully
      }
    });
  }
});
```

## <a name="how-to-additional-options-for-dequeuing-messages"></a>Procedura: opzioni aggiuntive per rimuovere i messaggi dalla coda
È possibile personalizzare il recupero di messaggi da una coda in due modi:

* `options.numOfMessages`-Recuperare un batch di messaggi (in alto too32).
* `options.visibilityTimeout` - consente di impostare un timeout di invisibilità più lungo o più breve.

esempio Hello utilizza hello **getMessages** messaggi tooget 15 metodo in un'unica chiamata. Quindi, ogni messaggio viene elaborato con un ciclo for. Imposta inoltre hello invisibilità timeout toofive in minuti per tutti i messaggi restituiti da questo metodo.

```
queueSvc.getMessages('myqueue', {numOfMessages: 15, visibilityTimeout: 5 * 60}, function(error, result, response){
  if(!error){
    // Messages retreived
    for(var index in result){
      // text is available in result[index].messageText
      var message = result[index];
      queueSvc.deleteMessage(queueName, message.messageId, message.popReceipt, function(error, response){
        if(!error){
          // Message deleted
        }
      });
    }
  }
});
```

## <a name="how-to-get-hello-queue-length"></a>Procedura: Recuperare hello lunghezza coda
Hello **getQueueMetadata** restituisce i metadati sulla coda di hello, ad esempio il numero approssimativo di messaggi in attesa nella coda di hello hello.

```
queueSvc.getQueueMetadata('myqueue', function(error, result, response){
  if(!error){
    // Queue length is available in result.approximateMessageCount
  }
});
```

## <a name="how-to-list-queues"></a>Procedura: Elenco di code
un elenco di code, utilizzare tooretrieve **listQueuesSegmented**. tooretrieve un elenco filtrato tramite un prefisso specifico, utilizzare **listQueuesSegmentedWithPrefix**.

```
queueSvc.listQueuesSegmented(null, function(error, result, response){
  if(!error){
    // result.entries contains hello list of queues
  }
});
```

Se non è possibile restituire tutte le code, `result.continuationToken` può essere utilizzato come primo parametro di hello **listQueuesSegmented** o hello secondo parametro di **listQueuesSegmentedWithPrefix** tooretrieve altri risultati.

## <a name="how-to-delete-a-queue"></a>Procedura: eliminare una coda
toodelete una coda e tutti i messaggi hello in esso contenuti, chiamare il **deleteQueue** metodo hello dell'oggetto di coda.

```
queueSvc.deleteQueue(queueName, function(error, response){
  if(!error){
    // Queue has been deleted
  }
});
```

utilizzare tutti i messaggi da una coda senza eliminarla, tooclear **clearMessages**.

## <a name="how-to-work-with-shared-access-signatures"></a>Procedura: usare le firme di accesso condiviso di Azure
Le firme di accesso condiviso (SAS) sono un tooqueues di accesso granulare tooprovide in modo sicuro senza fornire il nome account di archiviazione o chiavi. Firma di accesso condiviso è spesso le code di tooyour accesso tooprovide utilizzati limitate, ad esempio per consentire a un'app mobile toosubmit messaggi.

Un'applicazione attendibile, ad esempio un servizio basato su cloud genera una firma di accesso condiviso utilizzando hello **generateSharedAccessSignature** di hello **QueueService**e fornisce tooan applicazione non attendibile o semi-trusted. Si prenda ad esempio un'app per dispositivi mobili. Hello firma di accesso condiviso viene generato utilizzando un criterio, che descrive l'avvio di hello e fine in cui hello firma di accesso condiviso è valido, nonché hello titolare SAS toohello concesso livello di accesso.

Hello di esempio seguente genera un nuovo criterio di accesso condiviso che consente la coda toohello SAS titolare tooadd messaggi hello e scade 100 minuti dopo il tempo di hello che viene creato.

```
var startDate = new Date();
var expiryDate = new Date(startDate);
expiryDate.setMinutes(startDate.getMinutes() + 100);
startDate.setMinutes(startDate.getMinutes() - 100);

var sharedAccessPolicy = {
  AccessPolicy: {
    Permissions: azure.QueueUtilities.SharedAccessPermissions.ADD,
    Start: startDate,
    Expiry: expiryDate
  }
};

var queueSAS = queueSvc.generateSharedAccessSignature('myqueue', sharedAccessPolicy);
var host = queueSvc.host;
```

Si noti che le informazioni sull'host hello deve essere fornito, come richiesto quando titolare SAS hello tenta anche coda hello tooaccess.

Hello applicazione client, quindi Usa hello SAS con **QueueServiceWithSAS** operazioni tooperform coda hello. Hello di esempio seguente si connette toohello coda e crea un messaggio.

```
var sharedQueueService = azure.createQueueServiceWithSas(host, queueSAS);
sharedQueueService.createMessage('myqueue', 'Hello world from SAS!', function(error, result, response){
  if(!error){
    //message added
  }
});
```

Poiché hello firma di accesso condiviso è stato generato con Aggiungi accesso, se un tentativo sono stato apportato tooread, aggiornare o eliminare i messaggi, verrebbe restituito un errore.

### <a name="access-control-lists"></a>Elenchi di controllo di accesso
È inoltre possibile utilizzare un criterio di accesso hello tooset elenco di controllo di accesso (ACL) per una firma di accesso condiviso. Ciò è utile se si desidera tooallow coda hello di più client tooaccess, ma forniscono criteri di accesso diversi per ogni client.

Un elenco di controllo di accesso viene implementato usando una matrice di criteri di accesso, con un ID associato a ogni criterio. Hello di esempio seguente definisce due criteri; uno per "user1" e uno per 'Utente2':

```
var sharedAccessPolicy = {
  user1: {
    Permissions: azure.QueueUtilities.SharedAccessPermissions.PROCESS,
    Start: startDate,
    Expiry: expiryDate
  },
  user2: {
    Permissions: azure.QueueUtilities.SharedAccessPermissions.ADD,
    Start: startDate,
    Expiry: expiryDate
  }
};
```

Hello seguente esempio ottiene hello gli ACL per **myqueue**, quindi vengono aggiunti nuovi criteri hello utilizzando **setQueueAcl**. Risultato:

```
var extend = require('extend');
queueSvc.getQueueAcl('myqueue', function(error, result, response) {
  if(!error){
    var newSignedIdentifiers = extend(true, result.signedIdentifiers, sharedAccessPolicy);
    queueSvc.setQueueAcl('myqueue', newSignedIdentifiers, function(error, result, response){
      if(!error){
        // ACL set
      }
    });
  }
});
```

Una volta hello che ACL è stato impostato, è quindi possibile creare una firma di accesso condiviso in base all'ID di hello per un criterio. Hello di esempio seguente crea una nuova firma di accesso condiviso per 'Utente2':

```
queueSAS = queueSvc.generateSharedAccessSignature('myqueue', { Id: 'user2' });
```

## <a name="next-steps"></a>Passaggi successivi
Ora che si sono appreso i concetti fondamentali di hello dell'archiviazione delle code, seguire questi toolearn collegamenti sulle attività di archiviazione più complesse.

* Visitare hello [Azure Storage Blog del Team] [Blog del Team di archiviazione di Azure].
* Visitare hello [Azure Storage SDK per nodo] [ Azure Storage SDK for Node] repository in GitHub.

[Azure Storage SDK for Node]: https://github.com/Azure/azure-storage-node
[using hello REST API]: http://msdn.microsoft.com/library/azure/hh264518.aspx
[Azure Portal]: https://portal.azure.com
[Creare un'app Web Node.js in Servizio app di Azure](../../app-service-web/app-service-web-get-started-nodejs.md)   
[App web Node. js utilizzando hello del servizio tabelle di Azure](../../app-service-web/storage-nodejs-use-table-storage-web-site.md)
  


[Compilare e distribuire un tooan applicazione Node.js servizio Cloud di Azure](../../cloud-services/cloud-services-nodejs-develop-deploy-app.md)   
[Azure Blog del Team di archiviazione]: http://blogs.msdn.com/b/windowsazurestorage/ [compilare e distribuire un tooAzure di app web Node. js utilizzando WebMatrix]: https://www.microsoft.com/web/webmatrix/   
