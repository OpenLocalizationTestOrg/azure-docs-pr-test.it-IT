## <span data-ttu-id="ad08c-101"><a name="create-client"></a>Creare una connessione client</span><span class="sxs-lookup"><span data-stu-id="ad08c-101"><a name="create-client"></a>Create a client connection</span></span>
<span data-ttu-id="ad08c-102">Creare una connessione client creando un oggetto `WindowsAzure.MobileServiceClient` .</span><span class="sxs-lookup"><span data-stu-id="ad08c-102">Create a client connection by creating a `WindowsAzure.MobileServiceClient` object.</span></span>  <span data-ttu-id="ad08c-103">Sostituire `appUrl` con tooyour l'URL App per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="ad08c-103">Replace `appUrl` with the URL tooyour Mobile App.</span></span>

```
var client = WindowsAzure.MobileServiceClient(appUrl);
```

## <span data-ttu-id="ad08c-104"><a name="table-reference"></a>Usare le tabelle</span><span class="sxs-lookup"><span data-stu-id="ad08c-104"><a name="table-reference"></a>Work with tables</span></span>
<span data-ttu-id="ad08c-105">tooaccess o l'aggiornamento dati, creare una tabella di riferimento toohello back-end.</span><span class="sxs-lookup"><span data-stu-id="ad08c-105">tooaccess or update data, create a reference toohello backend table.</span></span> <span data-ttu-id="ad08c-106">Sostituire `tableName` con nome hello della tabella</span><span class="sxs-lookup"><span data-stu-id="ad08c-106">Replace `tableName` with hello name of your table</span></span>

```
var table = client.getTable(tableName);
```

<span data-ttu-id="ad08c-107">Dopo aver creato un riferimento a tabella, saranno disponibili le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="ad08c-107">Once you have a table reference, you can work further with your table:</span></span>

* [<span data-ttu-id="ad08c-108">Query sulla tabella</span><span class="sxs-lookup"><span data-stu-id="ad08c-108">Query a Table</span></span>](#querying)
  * [<span data-ttu-id="ad08c-109">Filtro dei dati</span><span class="sxs-lookup"><span data-stu-id="ad08c-109">Filtering Data</span></span>](#table-filter)
  * [<span data-ttu-id="ad08c-110">Paging dei dati</span><span class="sxs-lookup"><span data-stu-id="ad08c-110">Paging through Data</span></span>](#table-paging)
  * [<span data-ttu-id="ad08c-111">Ordinamento dei dati</span><span class="sxs-lookup"><span data-stu-id="ad08c-111">Sorting Data</span></span>](#sorting-data)
* [<span data-ttu-id="ad08c-112">Inserimento dei dati</span><span class="sxs-lookup"><span data-stu-id="ad08c-112">Inserting Data</span></span>](#inserting)
* [<span data-ttu-id="ad08c-113">Modifica dei dati</span><span class="sxs-lookup"><span data-stu-id="ad08c-113">Modifying Data</span></span>](#modifying)
* [<span data-ttu-id="ad08c-114">Eliminazione dei dati</span><span class="sxs-lookup"><span data-stu-id="ad08c-114">Deleting Data</span></span>](#deleting)

### <span data-ttu-id="ad08c-115"><a name="querying"></a>Procedura: Eseguire query su un riferimento a tabella</span><span class="sxs-lookup"><span data-stu-id="ad08c-115"><a name="querying"></a>How to: Query a table reference</span></span>
<span data-ttu-id="ad08c-116">Dopo aver creato un riferimento alla tabella, è possibile utilizzarlo per i dati nel server di hello tooquery.</span><span class="sxs-lookup"><span data-stu-id="ad08c-116">Once you have a table reference, you can use it tooquery for data on hello server.</span></span>  <span data-ttu-id="ad08c-117">Le query vengono eseguite in un linguaggio "simile a LINQ".</span><span class="sxs-lookup"><span data-stu-id="ad08c-117">Queries are made in a "LINQ-like" language.</span></span>
<span data-ttu-id="ad08c-118">tooreturn tutti i dati dalla tabella hello, utilizzare hello seguente codice:</span><span class="sxs-lookup"><span data-stu-id="ad08c-118">tooreturn all data from hello table, use hello following code:</span></span>

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

<span data-ttu-id="ad08c-119">funzione di successo Hello viene chiamata con risultati hello.</span><span class="sxs-lookup"><span data-stu-id="ad08c-119">hello success function is called with hello results.</span></span>  <span data-ttu-id="ad08c-120">Non utilizzare `for (var i in results)` in caso di esito positivo hello funzionare come che verranno scorrere informazioni incluse nei risultati di hello quando altre funzioni di query (ad esempio `.includeTotalCount()`) vengono utilizzati.</span><span class="sxs-lookup"><span data-stu-id="ad08c-120">Do not use `for (var i in results)` in hello success function as that will iterate over information that is included in hello results when other query functions (such as `.includeTotalCount()`) are used.</span></span>

<span data-ttu-id="ad08c-121">Per ulteriori informazioni sulla sintassi delle Query hello, vedere hello [documentazione oggetto Query].</span><span class="sxs-lookup"><span data-stu-id="ad08c-121">For more information on hello Query syntax, see hello [Query object documentation].</span></span>

#### <span data-ttu-id="ad08c-122"><a name="table-filter"></a>Filtraggio dei dati nel server hello</span><span class="sxs-lookup"><span data-stu-id="ad08c-122"><a name="table-filter"></a>Filtering data on hello server</span></span>
<span data-ttu-id="ad08c-123">È possibile utilizzare un `where` clausola in riferimento alla tabella hello:</span><span class="sxs-lookup"><span data-stu-id="ad08c-123">You can use a `where` clause on hello table reference:</span></span>

```
table
    .where({ userId: user.userId, complete: false })
    .read()
    .then(success, failure);
```

<span data-ttu-id="ad08c-124">È inoltre possibile utilizzare una funzione che filtra l'oggetto hello.</span><span class="sxs-lookup"><span data-stu-id="ad08c-124">You can also use a function that filters hello object.</span></span>  <span data-ttu-id="ad08c-125">In questo caso, hello `this` variabile viene assegnato l'oggetto corrente da toothe filtrato.</span><span class="sxs-lookup"><span data-stu-id="ad08c-125">In this case, hello `this` variable is assigned toothe current object being filtered.</span></span>  <span data-ttu-id="ad08c-126">Hello di codice seguente è funzionalmente equivalente toohello precedente esempio:</span><span class="sxs-lookup"><span data-stu-id="ad08c-126">hello following code is functionally equivalent toohello prior example:</span></span>

```
function filterByUserId(currentUserId) {
    return this.userId === currentUserId && this.complete === false;
}

table
    .where(filterByUserId, user.userId)
    .read()
    .then(success, failure);
```

#### <span data-ttu-id="ad08c-127"><a name="table-paging"></a>Paging dei dati</span><span class="sxs-lookup"><span data-stu-id="ad08c-127"><a name="table-paging"></a>Paging through data</span></span>
<span data-ttu-id="ad08c-128">Utilizzare hello `take()` e `skip()` metodi.</span><span class="sxs-lookup"><span data-stu-id="ad08c-128">Utilize hello `take()` and `skip()` methods.</span></span>  <span data-ttu-id="ad08c-129">Ad esempio, se si desidera tabella hello toosplit in record 100 righe:</span><span class="sxs-lookup"><span data-stu-id="ad08c-129">For example, if you wish toosplit hello table into 100-row records:</span></span>

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

<span data-ttu-id="ad08c-130">Hello `.includeTotalCount()` metodo è usato tooadd oggetto totalCount campo toohello risultati.</span><span class="sxs-lookup"><span data-stu-id="ad08c-130">hello `.includeTotalCount()` method is used tooadd a totalCount field toohello results object.</span></span>  <span data-ttu-id="ad08c-131">Il campo totalCount viene riempito con numero totale di hello di record che verrebbe restituito se il paging non viene utilizzato.</span><span class="sxs-lookup"><span data-stu-id="ad08c-131">The totalCount field is filled with hello total number of records that would be returned if no paging is used.</span></span>

<span data-ttu-id="ad08c-132">È quindi possibile utilizzare una variabile di pagine hello e alcuni tooprovide pulsanti dell'interfaccia utente un elenco di pagina. Utilizzare `loadPage()` caricare nuovi record di hello per ogni pagina.</span><span class="sxs-lookup"><span data-stu-id="ad08c-132">You can then use hello pages variable and some UI buttons tooprovide a page list; use `loadPage()` to load hello new records for each page.</span></span>  <span data-ttu-id="ad08c-133">Implementare la memorizzazione nella cache toospeed toorecords di accesso che sono già stati caricati.</span><span class="sxs-lookup"><span data-stu-id="ad08c-133">Implement caching toospeed access toorecords that have already been loaded.</span></span>

#### <span data-ttu-id="ad08c-134"><a name="sorting-data"></a>Procedura: Restituire i dati ordinati</span><span class="sxs-lookup"><span data-stu-id="ad08c-134"><a name="sorting-data"></a>How to: Return sorted data</span></span>
<span data-ttu-id="ad08c-135">Hello utilizzare `.orderBy()` o `.orderByDescending()` metodi di query:</span><span class="sxs-lookup"><span data-stu-id="ad08c-135">Use hello `.orderBy()` or `.orderByDescending()` query methods:</span></span>

```
table
    .orderBy('name')
    .read()
    .then(success, failure);
```

<span data-ttu-id="ad08c-136">Per ulteriori informazioni sull'oggetto Query hello, vedere hello [documentazione oggetto Query].</span><span class="sxs-lookup"><span data-stu-id="ad08c-136">For more information on hello Query object, see hello [Query object documentation].</span></span>

### <span data-ttu-id="ad08c-137"><a name="inserting"></a>Procedura: Inserire dati</span><span class="sxs-lookup"><span data-stu-id="ad08c-137"><a name="inserting"></a>How to: Insert data</span></span>
<span data-ttu-id="ad08c-138">Creare un oggetto JavaScript con una data hello appropriate e chiamare `table.insert()` in modo asincrono:</span><span class="sxs-lookup"><span data-stu-id="ad08c-138">Create a JavaScript object with hello appropriate date and call `table.insert()` asynchronously:</span></span>

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

<span data-ttu-id="ad08c-139">Nell'inserimento ha esito positivo, hello inserito viene restituita con hello altri campi che sono necessari per operazioni di sincronizzazione.</span><span class="sxs-lookup"><span data-stu-id="ad08c-139">On successful insertion, hello inserted item is returned with hello additional fields that are required for sync operations.</span></span>  <span data-ttu-id="ad08c-140">Aggiornare la cache con queste informazioni per gli aggiornamenti successivi.</span><span class="sxs-lookup"><span data-stu-id="ad08c-140">Update your own cache with this information for later updates.</span></span>

<span data-ttu-id="ad08c-141">Hello Azure Mobile App Node.js Server SDK supporta lo schema dinamico per scopi di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="ad08c-141">hello Azure Mobile Apps Node.js Server SDK supports dynamic schema for development purposes.</span></span>  <span data-ttu-id="ad08c-142">Lo Schema dinamico modo, si tooadd colonne toohello tabella specificandoli in un'operazione insert o update.</span><span class="sxs-lookup"><span data-stu-id="ad08c-142">Dynamic Schema allows you tooadd columns toohello table by specifying them in an insert or update operation.</span></span>  <span data-ttu-id="ad08c-143">È consigliabile disattivare lo schema dinamico prima di spostare tooproduction l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="ad08c-143">We recommend that you turn off dynamic schema before moving your application tooproduction.</span></span>

### <span data-ttu-id="ad08c-144"><a name="modifying"></a>Procedura: Modificare dati</span><span class="sxs-lookup"><span data-stu-id="ad08c-144"><a name="modifying"></a>How to: Modify data</span></span>
<span data-ttu-id="ad08c-145">Toohello simile `.insert()` metodo, deve creare un oggetto di aggiornamento e quindi chiamare `.update()`.</span><span class="sxs-lookup"><span data-stu-id="ad08c-145">Similar toohello `.insert()` method, you should create an Update object and then call `.update()`.</span></span>  <span data-ttu-id="ad08c-146">Hello Aggiorna oggetto deve contenere ID hello toobe di hello record aggiornato: hello ID ottenuto durante la lettura dei record di hello o quando si chiama `.insert()`.</span><span class="sxs-lookup"><span data-stu-id="ad08c-146">hello update object must contain hello ID of hello record toobe updated - hello ID is obtained when reading hello record or when calling `.insert()`.</span></span>

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

### <span data-ttu-id="ad08c-147"><a name="deleting"></a>Procedura: Eliminare dati</span><span class="sxs-lookup"><span data-stu-id="ad08c-147"><a name="deleting"></a>How to: Delete data</span></span>
<span data-ttu-id="ad08c-148">toodelete un record, chiamata hello `.del()` metodo.</span><span class="sxs-lookup"><span data-stu-id="ad08c-148">toodelete a record, call hello `.del()` method.</span></span>  <span data-ttu-id="ad08c-149">Passare un riferimento all'oggetto ID hello:</span><span class="sxs-lookup"><span data-stu-id="ad08c-149">Pass hello ID in an object reference:</span></span>

```
table
    .del({ id: '7163bc7a-70b2-4dde-98e9-8818969611bd' })
    .done(function () {
        // Record is now deleted - update your cache
    }, failure);
```
