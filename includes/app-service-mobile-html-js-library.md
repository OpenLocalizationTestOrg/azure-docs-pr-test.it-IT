## <a name="create-client"></a>Creare una connessione client
Creare una connessione client creando un oggetto `WindowsAzure.MobileServiceClient` .  Sostituire `appUrl` con tooyour l'URL App per dispositivi mobili.

```
var client = WindowsAzure.MobileServiceClient(appUrl);
```

## <a name="table-reference"></a>Usare le tabelle
tooaccess o l'aggiornamento dati, creare una tabella di riferimento toohello back-end. Sostituire `tableName` con nome hello della tabella

```
var table = client.getTable(tableName);
```

Dopo aver creato un riferimento a tabella, saranno disponibili le operazioni seguenti:

* [Query sulla tabella](#querying)
  * [Filtro dei dati](#table-filter)
  * [Paging dei dati](#table-paging)
  * [Ordinamento dei dati](#sorting-data)
* [Inserimento dei dati](#inserting)
* [Modifica dei dati](#modifying)
* [Eliminazione dei dati](#deleting)

### <a name="querying"></a>Procedura: Eseguire query su un riferimento a tabella
Dopo aver creato un riferimento alla tabella, è possibile utilizzarlo per i dati nel server di hello tooquery.  Le query vengono eseguite in un linguaggio "simile a LINQ".
tooreturn tutti i dati dalla tabella hello, utilizzare hello seguente codice:

```
/**
 * Process hello results that are received by a call tootable.read()
 *
 * @param {Object} results hello results as a pseudo-array
 * @param {int} results.length hello length of hello results array
 * @param {Object} results[] hello individual results
 */
function success(results) {
   var numItemsRead = results.length;

   for (var i = 0 ; i < results.length ; i++) {
       var row = results[i];
       // Each row is an object - hello properties are hello columns
   }
}

function failure(error) {
    throw new Error('Error loading data: ', error);
}

table
    .read()
    .then(success, failure);
```

funzione di successo Hello viene chiamata con risultati hello.  Non utilizzare `for (var i in results)` in caso di esito positivo hello funzionare come che verranno scorrere informazioni incluse nei risultati di hello quando altre funzioni di query (ad esempio `.includeTotalCount()`) vengono utilizzati.

Per ulteriori informazioni sulla sintassi delle Query hello, vedere hello [documentazione oggetto Query].

#### <a name="table-filter"></a>Filtraggio dei dati nel server hello
È possibile utilizzare un `where` clausola in riferimento alla tabella hello:

```
table
    .where({ userId: user.userId, complete: false })
    .read()
    .then(success, failure);
```

È inoltre possibile utilizzare una funzione che filtra l'oggetto hello.  In questo caso, hello `this` variabile viene assegnato l'oggetto corrente da toothe filtrato.  Hello di codice seguente è funzionalmente equivalente toohello precedente esempio:

```
function filterByUserId(currentUserId) {
    return this.userId === currentUserId && this.complete === false;
}

table
    .where(filterByUserId, user.userId)
    .read()
    .then(success, failure);
```

#### <a name="table-paging"></a>Paging dei dati
Utilizzare hello `take()` e `skip()` metodi.  Ad esempio, se si desidera tabella hello toosplit in record 100 righe:

```
var totalCount = 0, pages = 0;

// Step 1 - get hello total number of records
table.includeTotalCount().take(0).read(function (results) {
    totalCount = results.totalCount;
    pages = Math.floor(totalCount/100) + 1;
    loadPage(0);
}, failure);

function loadPage(pageNum) {
    let skip = pageNum * 100;
    table.skip(skip).take(100).read(function (results) {
        for (var i = 0 ; i < results.length ; i++) {
            var row = results[i];
            // Process each row
        }
    }
}
```

Hello `.includeTotalCount()` metodo è usato tooadd oggetto totalCount campo toohello risultati.  Il campo totalCount viene riempito con numero totale di hello di record che verrebbe restituito se il paging non viene utilizzato.

È quindi possibile utilizzare una variabile di pagine hello e alcuni tooprovide pulsanti dell'interfaccia utente un elenco di pagina. Utilizzare `loadPage()` caricare nuovi record di hello per ogni pagina.  Implementare la memorizzazione nella cache toospeed toorecords di accesso che sono già stati caricati.

#### <a name="sorting-data"></a>Procedura: Restituire i dati ordinati
Hello utilizzare `.orderBy()` o `.orderByDescending()` metodi di query:

```
table
    .orderBy('name')
    .read()
    .then(success, failure);
```

Per ulteriori informazioni sull'oggetto Query hello, vedere hello [documentazione oggetto Query].

### <a name="inserting"></a>Procedura: Inserire dati
Creare un oggetto JavaScript con una data hello appropriate e chiamare `table.insert()` in modo asincrono:

```javascript
var newItem = {
    name: 'My Name',
    signupDate: new Date()
};

table
    .insert(newItem)
    .done(function (insertedItem) {
        var id = insertedItem.id;
    }, failure);
```

Nell'inserimento ha esito positivo, hello inserito viene restituita con hello altri campi che sono necessari per operazioni di sincronizzazione.  Aggiornare la cache con queste informazioni per gli aggiornamenti successivi.

Hello Azure Mobile App Node.js Server SDK supporta lo schema dinamico per scopi di sviluppo.  Lo Schema dinamico modo, si tooadd colonne toohello tabella specificandoli in un'operazione insert o update.  È consigliabile disattivare lo schema dinamico prima di spostare tooproduction l'applicazione.

### <a name="modifying"></a>Procedura: Modificare dati
Toohello simile `.insert()` metodo, deve creare un oggetto di aggiornamento e quindi chiamare `.update()`.  Hello Aggiorna oggetto deve contenere ID hello toobe di hello record aggiornato: hello ID ottenuto durante la lettura dei record di hello o quando si chiama `.insert()`.

```javascript
var updateItem = {
    id: '7163bc7a-70b2-4dde-98e9-8818969611bd',
    name: 'My New Name'
};

table
    .update(updateItem)
    .done(function (updatedItem) {
        // You can now update your cached copy
    }, failure);
```

### <a name="deleting"></a>Procedura: Eliminare dati
toodelete un record, chiamata hello `.del()` metodo.  Passare un riferimento all'oggetto ID hello:

```
table
    .del({ id: '7163bc7a-70b2-4dde-98e9-8818969611bd' })
    .done(function () {
        // Record is now deleted - update your cache
    }, failure);
```
