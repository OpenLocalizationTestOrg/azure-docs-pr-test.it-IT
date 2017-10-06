---
title: aaaHow toouse archiviazione tabelle di Azure da Node.js | Documenti Microsoft
description: Archiviare dati strutturati in un cloud di hello tramite l'archiviazione tabelle di Azure, un archivio dati NoSQL.
services: cosmos-db
documentationcenter: nodejs
author: mimig1
manager: jhubbard
editor: tysonn
ms.assetid: fc2e33d2-c5da-4861-8503-53fdc25750de
ms.service: cosmos-db
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 12/08/2016
ms.author: mimig
ms.openlocfilehash: 21022491a9a21a5365628de93582ea3a325ed869
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-table-storage-from-nodejs"></a>Come toouse archiviazione tabelle di Azure da Node.js
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a>Panoramica
Questo argomento viene illustrato come gli scenari comuni di tooperform utilizzando hello tabelle di Azure del servizio in un'applicazione Node.js.

esempi di codice Hello in questo argomento si presume che un'applicazione Node.js. Per informazioni su come toocreate un'applicazione Node.js in Azure, vedere uno degli argomenti seguenti:

* [Creare un'app Web Node.js nel servizio app di Azure](../app-service-web/app-service-web-get-started-nodejs.md)
* [Compilare e distribuire un tooAzure di app web Node. js con WebMatrix](../app-service-web/web-sites-nodejs-use-webmatrix.md)
* [Compilare e distribuire un tooan di applicazione del servizio Cloud di Azure Node.js](../cloud-services/cloud-services-nodejs-develop-deploy-app.md) (tramite Windows PowerShell)

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="configure-your-application-tooaccess-azure-storage"></a>Configurare l'archiviazione di Azure di tooaccess applicazione
toouse archiviazione di Azure, è necessario hello Azure Storage SDK per Node.js, che include un set di librerie di praticità che comunicano con servizi REST di archiviazione hello.

### <a name="use-node-package-manager-npm-tooinstall-hello-package"></a>Utilizzare un pacchetto di hello tooinstall nodo Package Manager (NPM)
1. Utilizzare un'interfaccia della riga di comando, ad esempio **PowerShell** (Windows), **Terminal** (Mac), o **Bash** (Unix) e passare toohello cartella in cui viene creata l'applicazione.
2. Tipo **npm installare archiviazione di azure** nella finestra di comando hello. Output del comando hello è simile toohello esempio seguente.

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
3. È possibile eseguire manualmente hello **ls** comando tooverify che un **nodo\_moduli** cartella è stata creata. Questa cartella si troverà hello **archiviazione di azure** pacchetto che contiene le librerie di hello tooaccess archiviazione necessarie.

### <a name="import-hello-package"></a>Importa pacchetto di hello
Aggiungere i seguenti hello cima toohello codice hello **server.js** file dell'applicazione:

```nodejs
var azure = require('azure-storage');
```

## <a name="set-up-an-azure-storage-connection"></a>Configurare una connessione di archiviazione di Azure
modulo Hello azure verrà lette le variabili di ambiente hello AZURE\_archiviazione\_ACCOUNT e AZURE\_archiviazione\_accesso\_chiave o AZURE\_archiviazione\_connessione \_Stringa per le informazioni necessarie tooconnect tooyour account di archiviazione di Azure. Se non vengono impostate queste variabili di ambiente, è necessario specificare le informazioni sull'account hello quando si chiama **TableService**.

Per un esempio di impostazione delle variabili di ambiente hello in hello [portale di Azure](https://portal.azure.com) per un sito Web di Azure, vedere [app web Node. js utilizzando hello del servizio tabelle di Azure](../app-service-web/storage-nodejs-use-table-storage-web-site.md).

## <a name="create-a-table"></a>Creare una tabella
Hello codice seguente viene creata una **TableService** dell'oggetto e lo usa toocreate una nuova tabella. Aggiungere il seguente hello parte superiore di hello di **server.js**.

```nodejs
var tableSvc = azure.createTableService();
```

Hello chiamata troppo**createTableIfNotExists** creerà una nuova tabella con il nome specificato hello se non esiste già. Hello esempio seguente viene creata una nuova tabella denominata "mytable" Se non esiste già:

```nodejs
tableSvc.createTableIfNotExists('mytable', function(error, result, response){
  if(!error){
    // Table exists or created
  }
});
```

Hello `result.created` sarà `true` se viene creata una nuova tabella, e `false` hello tabella esiste già. Hello `response` contengono informazioni sulla richiesta di hello.

### <a name="filters"></a>Filtri
Operazioni di filtro facoltative possono essere applicato toooperations eseguita utilizzando **TableService**. Le operazioni di filtro possono includere la registrazione, la ripetizione automatica dei tentativi e così via. I filtri sono oggetti che implementano un metodo con firma hello:

```nodejs
function handle (requestOptions, next)
```

Dopo aver eseguito il pre-elaborazione sulle opzioni di richiesta di hello, metodo hello deve toocall "Avanti", il passaggio di un callback con hello seguente firma:

```nodejs
function (returnObject, finalCallback, next)
```

In questo callback e dopo l'elaborazione di hello returnObject (risposta hello dal server di hello richiesta toohello), il callback di hello richiede tooeither richiamare successivamente se esiste l'elaborazione di altri filtri toocontinue o semplicemente richiamare finalCallback hello tooend in caso contrario chiamata del servizio.

Due filtri, che implementano la logica di ripetizione sono inclusi in Azure SDK per Node.js, hello **ExponentialRetryPolicyFilter** e **LinearRetryPolicyFilter**. Hello seguito creato un **TableService** oggetto che utilizza hello **ExponentialRetryPolicyFilter**:

```nodejs
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var tableSvc = azure.createTableService().withFilter(retryOperations);
```

## <a name="add-an-entity-tooa-table"></a>Aggiungere una tabella tooa entità
tooadd un'entità, creare innanzitutto un oggetto che definisce le proprietà dell'entità. Tutte le entità devono contenere un **PartitionKey** e **RowKey**, che sono identificatori univoci per l'entità hello.

* **PartitionKey** -determina partizione hello archiviati in entità hello
* **RowKey** : in modo univoco identifica hello entità all'interno della partizione hello

Sia **PartitionKey** che **RowKey** devono essere valori stringa. Per ulteriori informazioni, vedere [hello comprensione modello di dati del servizio tabelle](http://msdn.microsoft.com/library/azure/dd179338.aspx).

Hello Ecco un esempio di definizione di un'entità. **dueDate** è definito come tipo di **Edm.DateTime**. Specifica il tipo hello è facoltativo e tipi verranno dedotto se non specificati.

```nodejs
var task = {
  PartitionKey: {'_':'hometasks'},
  RowKey: {'_': '1'},
  description: {'_':'take out hello trash'},
  dueDate: {'_':new Date(2015, 6, 20), '$':'Edm.DateTime'}
};
```

> [!NOTE]
> Per ogni record è anche presente un campo **Timestamp** , impostato da Azure quando viene inserita o aggiornata un'entità.
>
>

È inoltre possibile utilizzare hello **entityGenerator** toocreate entità. esempio Hello crea hello stessa entità di attività utilizzando hello **entityGenerator**.

```nodejs
var entGen = azure.TableUtilities.entityGenerator;
var task = {
  PartitionKey: entGen.String('hometasks'),
  RowKey: entGen.String('1'),
  description: entGen.String('take out hello trash'),
  dueDate: entGen.DateTime(new Date(Date.UTC(2015, 6, 20))),
};
```

una tabella, tooyour entità tooadd passare hello entità oggetto toohello **insertEntity** metodo.

```nodejs
tableSvc.insertEntity('mytable',task, function (error, result, response) {
  if(!error){
    // Entity inserted
  }
});
```

Se ha esito positivo, operazione hello `result` conterrà hello [ETag](http://en.wikipedia.org/wiki/HTTP_ETag) di hello inserire record e `response` conterrà informazioni sull'operazione hello.

Esempio di risposta:

```nodejs
{ '.metadata': { etag: 'W/"datetime\'2015-02-25T01%3A22%3A22.5Z\'"' } }
```

> [!NOTE]
> Per impostazione predefinita, **insertEntity** non restituisce entità hello inserito come parte di hello `response` informazioni. Se si prevede di eseguire altre operazioni su questa entità o si desiderano informazioni hello toocache, può essere utile toohave restituita come parte di hello `result`. A tale scopo, abilitare **echoContent** come segue:
>
> `tableSvc.insertEntity('mytable', task, {echoContent: true}, function (error, result, response) {...}`
>
>

## <a name="update-an-entity"></a>Aggiornare un'entità
Esistono più tooupdate disponibili di metodi un'entità esistente:

* **replaceEntity** : aggiorna un'entità esistente sostituendola
* **mergeEntity** -aggiorna un'entità esistente unendo nuovi valori della proprietà di entità esistente hello
* **insertOrReplaceEntity** : aggiorna un'entità esistente sostituendola. Se non esiste alcuna entità, ne verrà inserita una nuova.
* **insertOrMergeEntity** -aggiorna un'entità esistente mediante l'unione di nuovi valori della proprietà in hello esistente. Se non esiste alcuna entità, ne verrà inserita una nuova.

Hello esempio seguente viene illustrato l'aggiornamento di un'entità mediante **replaceEntity**:

```nodejs
tableSvc.replaceEntity('mytable', updatedTask, function(error, result, response){
  if(!error) {
    // Entity updated
  }
});
```

> [!NOTE]
> Per impostazione predefinita, l'aggiornamento di un'entità non verifica toosee se i dati di hello in corso l'aggiornamento sono stati modificati in precedenza da un altro processo. toosupport aggiornamenti simultanei:
>
> 1. Ottenere hello ETag dell'oggetto hello in corso l'aggiornamento. Viene restituito come parte di hello `response` per qualsiasi operazione associati all'entità e possono essere recuperati tramite `response['.metadata'].etag`.
> 2. Quando si esegue un'operazione di aggiornamento su un'entità, aggiungere le informazioni di ETag hello precedentemente recuperati toohello nuova entità. ad esempio:
>
>       entity2['.metadata'].etag = currentEtag;
> 3. Eseguire l'operazione di aggiornamento hello. Se l'entità di hello è stata modificata poiché è stato recuperato valore ETag hello, ad esempio un'altra istanza dell'applicazione, un `error` verranno restituite che informa che condizione aggiornamento hello specificato nella richiesta di hello non è stata soddisfatta.
>
>

Con **replaceEntity** e **mergeEntity**, se l'entità hello in corso di aggiornamento non esiste, l'operazione di aggiornamento hello avrà esito negativo. Pertanto se si desidera toostore un'entità indipendentemente dal fatto se esiste già, utilizzare **insertOrReplaceEntity** o **insertOrMergeEntity**.

Hello `result` per l'aggiornamento ha esito positivo operazioni conterrà hello **Etag** di hello aggiornato l'entità.

## <a name="work-with-groups-of-entities"></a>Usare i gruppi di entità
A volte risulta più toosubmit senso più operazioni contemporaneamente in un batch tooensure atomica elaborazione dal server hello. tooaccomplish utilizzati, hello **TableBatch** classe toocreate un batch e quindi utilizzare hello **executeBatch** metodo **TableService** tooperform hello operazioni in batch.

 Hello di esempio seguente viene illustrato l'invio di due entità in un batch:

```nodejs
var task1 = {
  PartitionKey: {'_':'hometasks'},
  RowKey: {'_': '1'},
  description: {'_':'Take out hello trash'},
  dueDate: {'_':new Date(2015, 6, 20)}
};
var task2 = {
  PartitionKey: {'_':'hometasks'},
  RowKey: {'_': '2'},
  description: {'_':'Wash hello dishes'},
  dueDate: {'_':new Date(2015, 6, 20)}
};

var batch = new azure.TableBatch();

batch.insertEntity(task1, {echoContent: true});
batch.insertEntity(task2, {echoContent: true});

tableSvc.executeBatch('mytable', batch, function (error, result, response) {
  if(!error) {
    // Batch completed
  }
});
```

Per le operazioni batch ha esito positivo, `result` conterrà informazioni per ogni operazione nel batch hello.

### <a name="work-with-batched-operations"></a>Uso delle operazioni in batch
Aggiungere le operazioni batch tooa può essere controllato da visualizzazione hello `operations` proprietà. È inoltre possibile utilizzare hello toowork metodi con le operazioni seguenti:

* **clear** : cancella tutte le operazioni da un batch.
* **getOperations** -Ottiene un'operazione batch hello
* **hasOperations** -restituisce true se il batch hello contiene operazioni
* **removeOperations** : rimuove un'operazione.
* **dimensioni** -restituisce hello numero di operazioni in batch hello

## <a name="retrieve-an-entity-by-key"></a>Recuperare un'entità in base alla chiave
un'entità specifica in base a hello tooreturn **PartitionKey** e **RowKey**, utilizzare hello **retrieveEntity** metodo.

```nodejs
tableSvc.retrieveEntity('mytable', 'hometasks', '1', function(error, result, response){
  if(!error){
    // result contains hello entity
  }
});
```

Dopo aver completata questa operazione `result` conterrà entità hello.

## <a name="query-a-set-of-entities"></a>Eseguire query su un set di entità
tooquery una tabella, utilizzare hello **TableQuery** oggetto toobuild di un'espressione di query utilizzando hello clausole seguenti:

* **Selezionare** -hello campi toobe restituito dalla query hello
* **dove** : hello dove clausola

  * **and**: una condizione where`and`.
  * **or**: una condizione where `or`.
* **inizio** -numero di elementi toofetch hello

Hello esempio seguente viene compilata una query che verrà restituiti hello primi cinque elementi con un PartitionKey di 'hometasks'.

```nodejs
var query = new azure.TableQuery()
  .top(5)
  .where('PartitionKey eq ?', 'hometasks');
```

Poiché **select** non viene usato, vengono restituiti tutti i campi. una tabella, utilizzare query hello tooperform **queryEntities**. Hello seguente viene utilizzata questa entità tooreturn query da "mytable".

```nodejs
tableSvc.queryEntities('mytable',query, null, function(error, result, response) {
  if(!error) {
    // query was successful
  }
});
```

Se ha esito positivo, `result.entries` conterrà una matrice di entità che soddisfano la query hello. Se non è possibile tooreturn query hello tutte le entità, `result.continuationToken` sarà non*null* e può essere utilizzato come terzo parametro del hello **queryEntities** tooretrieve altri risultati. Per le query iniziale hello, utilizzare *null* per terzo parametro hello.

### <a name="query-a-subset-of-entity-properties"></a>Eseguire query su un subset di proprietà di entità
Una tabella di tooa query è possibile recuperare un numero ridotto di campi da un'entità.
Questa tecnica permette di ridurre la larghezza di banda e di migliorare le prestazioni della query, in particolare per entità di grandi dimensioni. Hello utilizzare **selezionare** clausola e passare i nomi di hello campi toobe hello restituiti. Ad esempio, hello query seguente restituirà solo hello **descrizione** e **dueDate** campi.

```nodejs
var query = new azure.TableQuery()
  .select(['description', 'dueDate'])
  .top(5)
  .where('PartitionKey eq ?', 'hometasks');
```

## <a name="delete-an-entity"></a>Eliminare un'entità
È possibile eliminare un'entità utilizzando le relative chiavi di riga e di partizione. In questo esempio hello **Attività1** oggetto contiene hello **RowKey** e **PartitionKey** valori di hello entità toobe eliminato. L'oggetto hello è passato toohello **deleteEntity** metodo.

```nodejs
var task = {
  PartitionKey: {'_':'hometasks'},
  RowKey: {'_': '1'}
};

tableSvc.deleteEntity('mytable', task, function(error, response){
  if(!error) {
    // Entity deleted
  }
});
```

> [!NOTE]
> È consigliabile utilizzare valori eTag durante l'eliminazione di elementi, tooensure che hello elemento non è stato modificato da un altro processo. Vedere [Aggiornare un'entità](#update-an-entity) per informazioni sull'uso di ETag.
>
>

## <a name="delete-a-table"></a>Eliminare una tabella
Hello di codice seguente elimina una tabella da un account di archiviazione.

```nodejs
tableSvc.deleteTable('mytable', function(error, response){
    if(!error){
        // Table deleted
    }
});
```

Se non si è certi se la tabella hello esiste, utilizzare **deleteTableIfExists**.

## <a name="use-continuation-tokens"></a>Utilizzare i token di continuazione
Quando si esegue una query di tabelle di grandi quantità di risultati, ricercare i token di continuazione. Potrebbero essere disponibili per la query che si potrebbero non essere consapevoli se toorecognize non compilato quando è presente un token di continuazione grandi quantità di dati.

risultati Hello restituiti durante l'esecuzione di query su set di entità dell'oggetto un `continuationToken` proprietà quando è presente un token di questo tipo. È quindi possibile utilizzare questo durante l'esecuzione di un toomove toocontinue query tra le entità di partizione e la tabella hello.

Quando si eseguono query, è possibile specificare un parametro continuationToken tra l'istanza dell'oggetto query hello e funzione di callback hello:

```nodejs
var nextContinuationToken = null;
dc.table.queryEntities(tableName,
    query,
    nextContinuationToken,
    function (error, results) {
        if (error) throw error;

        // iterate through results.entries with results

        if (results.continuationToken) {
            nextContinuationToken = results.continuationToken;
        }

    });
```

Se si analizza hello `continuationToken` oggetto, sono disponibili le proprietà, ad esempio `nextPartitionKey`, `nextRowKey` e `targetLocation`, che può essere utilizzato tooiterate tramite tutti i risultati di hello.

È inoltre disponibile un esempio di continuazione in repository di hello Azure Storage Node.js su GitHub. Cercare `examples/samples/continuationsample.js`.

## <a name="work-with-shared-access-signatures"></a>Usare le firme di accesso condiviso di Azure
Firme di accesso condiviso (SAS) sono un tootables di accesso granulare tooprovide in modo sicuro senza fornire il nome account di archiviazione o chiavi. Firma di accesso condiviso è spesso i dati tooyour di accesso utilizzato tooprovide limitate, ad esempio per consentire a un'app mobile tooquery record.

Un'applicazione attendibile, ad esempio un servizio basato su cloud genera una firma di accesso condiviso utilizzando hello **generateSharedAccessSignature** di hello **TableService**e fornisce tooan applicazione non attendibile o semi-trusted ad esempio un'app per dispositivi mobili. Hello firma di accesso condiviso viene generato utilizzando un criterio, che descrive l'avvio di hello e fine in cui hello firma di accesso condiviso è valido, nonché hello titolare SAS toohello concesso livello di accesso.

Hello esempio seguente genera un nuovo criterio di accesso condiviso che consentirà di hello tabella hello SAS titolare tooquery ("r") e scade 100 minuti dopo il tempo di hello che viene creato.

```nodejs
var startDate = new Date();
var expiryDate = new Date(startDate);
expiryDate.setMinutes(startDate.getMinutes() + 100);
startDate.setMinutes(startDate.getMinutes() - 100);

var sharedAccessPolicy = {
  AccessPolicy: {
    Permissions: azure.TableUtilities.SharedAccessPermissions.QUERY,
    Start: startDate,
    Expiry: expiryDate
  },
};

var tableSAS = tableSvc.generateSharedAccessSignature('mytable', sharedAccessPolicy);
var host = tableSvc.host;
```

Si noti che le informazioni sull'host hello deve essere fornito, come richiesto quando titolare SAS hello tenta anche tabella hello tooaccess.

Hello applicazione client, quindi Usa hello SAS con **TableServiceWithSAS** tooperform operazioni sulla tabella hello. Hello di esempio seguente si connette toohello tabella ed esegue una query.

```nodejs
var sharedTableService = azure.createTableServiceWithSas(host, tableSAS);
var query = azure.TableQuery()
  .where('PartitionKey eq ?', 'hometasks');

sharedTableService.queryEntities(query, null, function(error, result, response) {
  if(!error) {
    // result contains hello entities
  }
});
```

Poiché hello firma di accesso condiviso è stato generato con il solo accesso query, se un tentativo sono stato apportato tooinsert, aggiornare o eliminare le entità, verrà restituito un errore.

### <a name="access-control-lists"></a>Elenchi di controllo di accesso
È inoltre possibile utilizzare un criterio di accesso hello tooset elenco di controllo di accesso (ACL) per una firma di accesso condiviso. Ciò è utile se si desiderano tooallow più tabelle di hello tooaccess client, ma forniscono criteri di accesso diversi per ogni client.

Un elenco di controllo di accesso viene implementato usando una matrice di criteri di accesso, con un ID associato a ogni criterio. Hello di esempio seguente definisce due criteri, uno per "user1" e uno per 'Utente2':

```nodejs
var sharedAccessPolicy = {
  user1: {
    Permissions: azure.TableUtilities.SharedAccessPermissions.QUERY,
    Start: startDate,
    Expiry: expiryDate
  },
  user2: {
    Permissions: azure.TableUtilities.SharedAccessPermissions.ADD,
    Start: startDate,
    Expiry: expiryDate
  }
};
```

Hello seguente esempio ottiene hello gli ACL per hello **hometasks** tabella e quindi aggiunge nuovi criteri hello utilizzando **setTableAcl**. Risultato:

```nodejs
var extend = require('extend');
tableSvc.getTableAcl('hometasks', function(error, result, response) {
if(!error){
    var newSignedIdentifiers = extend(true, result.signedIdentifiers, sharedAccessPolicy);
    tableSvc.setTableAcl('hometasks', newSignedIdentifiers, function(error, result, response){
      if(!error){
        // ACL set
      }
    });
  }
});
```

Una volta hello che ACL è stato impostato, è quindi possibile creare una firma di accesso condiviso in base all'ID di hello per un criterio. Hello di esempio seguente crea una nuova firma di accesso condiviso per 'Utente2':

```nodejs
tableSAS = tableSvc.generateSharedAccessSignature('hometasks', { Id: 'user2' });
```

## <a name="next-steps"></a>Passaggi successivi
Per ulteriori informazioni, vedere hello seguenti risorse.

* [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) è un'app autonoma, disponibile da Microsoft che consente di toowork visivamente i dati di archiviazione di Azure in Windows, macOS e Linux.
* [Azure Storage SDK per Node](https://github.com/Azure/azure-storage-node) su GitHub.
* [Centro per sviluppatori di Node. js](/develop/nodejs/)
* [Creare e distribuire un tooan applicazione Node.js sito Web di Azure](../app-service-web/app-service-web-get-started-nodejs.md)
