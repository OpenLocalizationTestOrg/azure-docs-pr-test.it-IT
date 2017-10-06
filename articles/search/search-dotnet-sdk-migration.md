---
title: aaaUpgrading toohello Azure Search .NET SDK versione 1.1 | Documenti Microsoft
description: L'aggiornamento toohello Azure Search .NET SDK versione 1.1
services: search
documentationcenter: 
author: brjohnstmsft
manager: pablocas
editor: 
ms.assetid: 66f89958-a320-4a24-87f9-69315848909f
ms.service: search
ms.devlang: dotnet
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 01/11/2017
ms.author: brjohnst
ms.openlocfilehash: 291ae5731546e47b3c22c721d3552a79bdea80c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="upgrading-toohello-azure-search-net-sdk-version-3"></a>L'aggiornamento toohello Azure Search .NET SDK versione 3
Se si usa versione 2.0 per l'anteprima o meno recenti di hello [Azure Search .NET SDK](https://aka.ms/search-sdk), in questo articolo consentirà di aggiornare la versione di toouse applicazione 3.

Per una procedura dettagliata più generale di hello SDK inclusi esempi, vedere [come toouse ricerca di Azure da un'applicazione .NET](search-howto-dotnet-sdk.md).

Versione 3 di hello Azure Search .NET SDK include alcune modifiche apportate da versioni precedenti. ma per lo più secondarie, quindi il codice potrà essere modificato facilmente. Vedere [tooupgrade passaggi](#UpgradeSteps) per istruzioni su come toochange la versione del SDK nuovo codice toouse hello.

> [!NOTE]
> Se si utilizza una versione 1.0.2-preview o precedente, è necessario eseguire prima l'aggiornamento tooversion 1.1 e quindi Aggiorna tooversion 3. Vedere [appendice: passaggi tooupgrade tooversion 1.1](#UpgradeStepsV1) per le istruzioni.
>
> L'istanza del servizio di ricerca di Azure supporta più versioni API REST, tra cui hello più recente. È possibile continuare toouse una versione quando non è più hello più recente, ma è consigliabile eseguire la migrazione la versione più recente del codice toouse hello. Quando si utilizza l'API REST di hello, è necessario specificare una versione dell'API hello in ogni richiesta tramite il parametro api-version hello. Quando si utilizza hello .NET SDK, versione di hello di hello SDK in uso determina versione corrispondente di hello di hello API REST. Se si utilizza un SDK precedente, è possibile continuare toorun che il codice senza apportare modifiche anche se il servizio di hello è la versione aggiornata toosupport un'API più recente.

<a name="WhatsNew"></a>

## <a name="whats-new-in-version-3"></a>Novità della versione 3
Versione 3 di hello destinazioni Azure Search .NET SDK di hello ultima versione disponibile in genere di hello API REST di ricerca di Azure, in particolare 2016-09-01. In questo modo è possibile toouse numerose nuove funzionalità di ricerca di Azure da un'applicazione .NET, inclusi hello seguenti:

* [Analizzatori personalizzati](https://aka.ms/customanalyzers)
* Supporto per gli indicizzatori di [Archiviazione BLOB di Azure](search-howto-indexing-azure-blob-storage.md) e [Archiviazione tabelle di Azure](search-howto-indexing-azure-tables.md)
* Personalizzazione dell'indicizzatore tramite [mapping dei campi](search-indexer-field-mappings.md)
* ETag supporta tooenable provvisoria simultanee l'aggiornamento di indicizzare le origini dati, gli indicizzatori e definizioni
* Supporto per la creazione di definizioni di campo di indice in modo dichiarativo decorando la classe di modello e utilizzando la nuova hello `FieldBuilder` classe.
* Supporto per .NET Core e .NET Portable Profile 111

<a name="UpgradeSteps"></a>

## <a name="steps-tooupgrade"></a>Passaggi tooupgrade
Innanzitutto, aggiornare il riferimento di NuGet per `Microsoft.Azure.Search` utilizzando una Console di gestione pacchetti NuGet hello o facendo clic sul riferimenti del progetto e selezionare "Gestisci pacchetti NuGet..." in Visual Studio.

Una volta NuGet è stato scaricato hello nuovi pacchetti e le relative dipendenze, ricompilare il progetto. A seconda della struttura del codice, la ricompilazione potrebbe essere eseguita correttamente. In questo caso, si è pronto toogo!

Se la compilazione non riesce, verrà visualizzato un errore di compilazione hello seguente:

    Program.cs(31,45,31,86): error CS0266: Cannot implicitly convert type 'Microsoft.Azure.Search.ISearchIndexClient' too'Microsoft.Azure.Search.SearchIndexClient'. An explicit conversion exists (are you missing a cast?)

passaggio successivo Hello è toofix l'errore di compilazione. Vedere [modifiche di rilievo nella versione 3](#ListOfChanges) per informazioni dettagliate sulle cause di errore hello e come toofix è.

Si può vedere compilazione aggiuntive avvisi correlati tooobsolete metodi o proprietà. gli avvisi di Hello include istruzioni su quali toouse invece di hello funzionalità deprecata. Ad esempio, se l'applicazione usa hello `IndexingParameters.Base64EncodeKeys` proprietà, è necessario ottenere un avviso per segnalare che`"This property is obsolete. Please create a field mapping using 'FieldMapping.Base64Encode' instead."`

Una volta che è stato risolto eventuali errori di compilazione, è possibile apportare modifiche tooyour applicazione tootake sfruttare nuove funzionalità se si desidera. Vengono descritti in dettaglio le nuove funzionalità hello SDK [novità nella versione 3](#WhatsNew).

<a name="ListOfChanges"></a>

## <a name="breaking-changes-in-version-3"></a>Modifiche di rilievo nella versione 3
Non esiste un numero ridotto di modifiche di rilievo nella versione 3 che potrebbero richiedere codice cambia inoltre toorebuilding l'applicazione.

### <a name="indexesgetclient-return-type"></a>Tipo restituito Indexes.GetClient
Hello `Indexes.GetClient` dispone di un nuovo tipo restituito. In precedenza, restituiva `SearchIndexClient`, ma questo è stato modificato troppo`ISearchIndexClient` nella versione 2.0 per l'anteprima e che modifica si riflette direttamente tooversion 3. Si tratta di toosupport clienti che desiderano hello toomock `GetClient` metodo per gli unit test restituendo un'implementazione fittizia del `ISearchIndexClient`.

#### <a name="example"></a>Esempio
Se il codice è simile a questo:

```csharp
SearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");
```

È possibile modificarla toothis toofix eventuali errori di compilazione:

```csharp
ISearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");
```

### <a name="analyzername-datatype-and-others-are-no-longer-implicitly-convertible-toostrings"></a>AnalyzerName, tipo di dati e altri utenti non sono più toostrings convertibile in modo implicito
Esistono molti tipi di hello Azure Search .NET SDK che derivano da `ExtensibleEnum`. In precedenza questi tipi sono stati tutti implicitamente convertibile tootype `string`. Tuttavia, in cui è stato individuato un bug in hello `Object.Equals` implementazione di queste classi e correzione bug hello necessario disabilitare la conversione implicita. Conversione esplicita troppo`string` è comunque consentita.

#### <a name="example"></a>Esempio
Se il codice è simile a questo:

```csharp
var customTokenizerName = TokenizerName.Create("my_tokenizer"); 
var customTokenFilterName = TokenFilterName.Create("my_tokenfilter"); 
var customCharFilterName = CharFilterName.Create("my_charfilter"); 
 
var index = new Index();
index.Analyzers = new Analyzer[] 
{ 
    new CustomAnalyzer( 
        "my_analyzer",  
        customTokenizerName,  
        new[] { customTokenFilterName },  
        new[] { customCharFilterName }), 
}; 
```

È possibile modificarla toothis toofix eventuali errori di compilazione:

```csharp
const string CustomTokenizerName = "my_tokenizer"; 
const string CustomTokenFilterName = "my_tokenfilter"; 
const string CustomCharFilterName = "my_charfilter"; 
 
var index = new Index();
index.Analyzers = new Analyzer[] 
{ 
    new CustomAnalyzer( 
        "my_analyzer",  
        CustomTokenizerName,  
        new TokenFilterName[] { CustomTokenFilterName },  
        new CharFilterName[] { CustomCharFilterName })
}; 
```

### <a name="removed-obsolete-members"></a>Rimuovere i membri obsoleti

È possibile visualizzare le proprietà sono state contrassegnate come obsolete nella versione 2.0 per l'anteprima e viene successivamente rimosso nella versione 3 o toomethods correlati gli errori di compilazione. Se si verificano questi errori, ecco come tooresolve loro:

- Se l'errore riguarda il costruttore `ScoringParameter(string name, string value)`, sostituirlo con `ScoringParameter(string name, IEnumerable<string> values)`
- Se si utilizza hello `ScoringParameter.Value` proprietà, utilizzare hello `ScoringParameter.Values` proprietà o hello `ToString` metodo invece.
- Se si utilizza hello `SearchRequestOptions.RequestId` proprietà, utilizzare hello `ClientRequestId` proprietà invece.

### <a name="removed-preview-features"></a>Funzionalità di anteprima rimosse

Se si esegue l'aggiornamento dalla versione 2.0 preview tooversion 3, tenere presente che JSON e CSV l'analisi di supporto per gli indicizzatori di Blob è stato rimosso dal momento che queste funzionalità sono ancora in anteprima. In particolare, hello dei seguenti metodi di hello `IndexingParametersExtensions` classe sono state rimosse:

- `ParseJson`
- `ParseJsonArrays`
- `ParseDelimitedTextFiles`

Se l'applicazione ha una dipendenza rigida da queste funzionalità, non sarà in grado di tooupgrade tooversion 3 di hello Azure Search .NET SDK. È possibile continuare toouse versione 2.0 per l'anteprima. Tenere presente, tuttavia, che **non è consigliabile usare SDK in anteprima nelle applicazioni di produzione**. Le funzionalità di anteprima sono destinate esclusivamente alla valutazione e sono soggette a modifiche.

## <a name="conclusion"></a>Conclusioni
Per ulteriori dettagli sull'utilizzo di hello Azure Search .NET SDK, vedere il nostro aggiornato di recente [procedure](search-howto-dotnet-sdk.md).

Invitiamo i commenti e suggerimenti su hello SDK. Se si verificano problemi, è disponibile tooask ci per informazioni su hello [forum MSDN di ricerca di Azure](https://social.msdn.microsoft.com/Forums/azure/home?forum=azuresearch). Se si trova un bug, è possibile segnalare un problema in hello [repository GitHub di Azure .NET SDK](https://github.com/Azure/azure-sdk-for-net/issues). Verificare che tooprefix con il titolo del problema "Search SDK:".

Grazie per avere usato Ricerca di Azure.

<a name="UpgradeStepsV1"></a>

## <a name="appendix-steps-tooupgrade-tooversion-11"></a>Appendice: Passaggi tooupgrade tooversion 1.1
> [!NOTE]
> Questa sezione si applica solo toousers di hello Azure Search .NET SDK versione 1.0.2-preview e precedenti.
> 
> 

Innanzitutto, aggiornare il riferimento di NuGet per `Microsoft.Azure.Search` utilizzando una Console di gestione pacchetti NuGet hello o facendo clic sul riferimenti del progetto e selezionare "Gestisci pacchetti NuGet..." in Visual Studio.

Una volta NuGet è stato scaricato hello nuovi pacchetti e le relative dipendenze, ricompilare il progetto.

Se fosse in precedenza usando versione 1.0.0-preview, 1.0.1-preview o 1.0.2-preview, compilazione hello dovrebbe avere esito positivo e si è pronto toogo!

Se in precedenza si utilizzava 0.13.0-preview versione o versioni precedenti, dovrebbe essere simile hello seguente errori di compilazione:

    Program.cs(137,56,137,62): error CS0117: 'Microsoft.Azure.Search.Models.IndexBatch' does not contain a definition for 'Create'
    Program.cs(137,99,137,105): error CS0117: 'Microsoft.Azure.Search.Models.IndexAction' does not contain a definition for 'Create'
    Program.cs(146,41,146,54): error CS1061: 'Microsoft.Azure.Search.IndexBatchException' does not contain a definition for 'IndexResponse' and no extension method 'IndexResponse' accepting a first argument of type 'Microsoft.Azure.Search.IndexBatchException' could be found (are you missing a using directive or an assembly reference?)
    Program.cs(163,13,163,42): error CS0246: hello type or namespace name 'DocumentSearchResponse' could not be found (are you missing a using directive or an assembly reference?)

passaggio successivo Hello è uno degli errori di compilazione di hello toofix. La maggior parte sarà necessario modificare alcuni nomi di classe e metodo che sono stati rinominati in hello SDK. [Elenco di modifiche di rilievo nella versione 1.1](#ListOfChangesV1) contiene l'elenco delle modifiche dei nomi.

Se si utilizza le classi personalizzate toomodel i documenti e tali classi dispongono di proprietà di tipi primitivi non nullable (ad esempio, `int` o `bool` in c#), è presente una correzione di bug nella versione 1.1 hello di hello SDK di cui è necessario essere consapevoli. Per altri dettagli, vedere [Correzioni di bug nella versione 1.1](#BugFixesV1) .

Infine, dopo che è stato risolto eventuali errori di compilazione, è possibile apportare modifiche di tooyour applicazione tootake sfruttare nuove funzionalità se si desidera.

<a name="ListOfChangesV1"></a>

### <a name="list-of-breaking-changes-in-version-11"></a>Elenco di modifiche di rilievo nella versione 1.1
Hello seguente elenco viene ordinato in base probabilità hello che hello modifica influirà sul codice dell'applicazione.

#### <a name="indexbatch-and-indexaction-changes"></a>Modifiche a IndexBatch e IndexAction
`IndexBatch.Create`è stato rinominato troppo`IndexBatch.New` e non dispone più di un `params` argomento. È possibile usare `IndexBatch.New` per i batch che combinano tipi diversi di azioni (unioni, eliminazioni e così via). Inoltre, sono disponibili nuovi metodi statici per la creazione di batch in cui tutte le azioni hello sono hello stesso: `Delete`, `Merge`, `MergeOrUpload`, e `Upload`.

`IndexAction` non include più costruttori pubblici e le proprietà ora sono non modificabili. È consigliabile utilizzare i nuovi metodi statici hello per la creazione di azioni per scopi diversi: `Delete`, `Merge`, `MergeOrUpload`, e `Upload`. `IndexAction.Create` è stato rimosso. Se si usa l'overload di hello che accetta solo un documento, assicurarsi che toouse `Upload` invece.

##### <a name="example"></a>Esempio
Se il codice è simile a questo:

    var batch = IndexBatch.Create(documents.Select(doc => IndexAction.Create(doc)));
    indexClient.Documents.Index(batch);

È possibile modificarla toothis toofix eventuali errori di compilazione:

    var batch = IndexBatch.New(documents.Select(doc => IndexAction.Upload(doc)));
    indexClient.Documents.Index(batch);

Se si desidera, è possibile semplificare ulteriormente la toothis:

    var batch = IndexBatch.Upload(documents);
    indexClient.Documents.Index(batch);

#### <a name="indexbatchexception-changes"></a>Modifiche a IndexBatchException
Hello `IndexBatchException.IndexResponse` proprietà è stata rinominata troppo`IndexingResults`, e il tipo è ora `IList<IndexingResult>`.

##### <a name="example"></a>Esempio
Se il codice è simile a questo:

    catch (IndexBatchException e)
    {
        Console.WriteLine(
            "Failed tooindex some of hello documents: {0}",
            String.Join(", ", e.IndexResponse.Results.Where(r => !r.Succeeded).Select(r => r.Key)));
    }

È possibile modificarla toothis toofix eventuali errori di compilazione:

    catch (IndexBatchException e)
    {
        Console.WriteLine(
            "Failed tooindex some of hello documents: {0}",
            String.Join(", ", e.IndexingResults.Where(r => !r.Succeeded).Select(r => r.Key)));
    }

<a name="OperationMethodChanges"></a>

#### <a name="operation-method-changes"></a>Modifiche ai metodi delle operazioni
Ogni operazione hello Azure Search .NET SDK viene esposto come un set di overload del metodo per i chiamanti sincroni e asincroni. Hello firme e separazione di questi overload del metodo è stato modificato nella versione 1.1.

Ad esempio, hello operazione "Get statistiche dell'indice" nelle versioni precedenti di hello SDK esposte queste firme:

In `IIndexOperations`:

    // Asynchronous operation with all parameters
    Task<IndexGetStatisticsResponse> GetStatisticsAsync(
        string indexName,
        CancellationToken cancellationToken);

In `IndexOperationsExtensions`:

    // Asynchronous operation with only required parameters
    public static Task<IndexGetStatisticsResponse> GetStatisticsAsync(
        this IIndexOperations operations,
        string indexName);

    // Synchronous operation with only required parameters
    public static IndexGetStatisticsResponse GetStatistics(
        this IIndexOperations operations,
        string indexName);

le firme di metodo Hello per hello stessa operazione nella versione 1.1 è simile a questo:

In `IIndexesOperations`:

    // Asynchronous operation with lower-level HTTP features exposed
    Task<AzureOperationResponse<IndexGetStatisticsResult>> GetStatisticsWithHttpMessagesAsync(
        string indexName,
        SearchRequestOptions searchRequestOptions = default(SearchRequestOptions),
        Dictionary<string, List<string>> customHeaders = null,
        CancellationToken cancellationToken = default(CancellationToken));

In `IndexesOperationsExtensions`:

    // Simplified asynchronous operation
    public static Task<IndexGetStatisticsResult> GetStatisticsAsync(
        this IIndexesOperations operations,
        string indexName,
        SearchRequestOptions searchRequestOptions = default(SearchRequestOptions),
        CancellationToken cancellationToken = default(CancellationToken));

    // Simplified synchronous operation
    public static IndexGetStatisticsResult GetStatistics(
        this IIndexesOperations operations,
        string indexName,
        SearchRequestOptions searchRequestOptions = default(SearchRequestOptions));

A partire dalla versione 1.1, hello Azure Search .NET SDK consente di organizzare i metodi di operazione in modo diverso:

* I parametri facoltativi ora vengono modellati come parametri predefiniti invece che come overload dei metodi aggiuntivi. Questo riduce il numero di hello degli overload del metodo, talvolta significativa.
* metodi di estensione Hello nascondono ora molti dettagli estranei hello HTTP dal chiamante hello. Ad esempio, le versioni precedenti di hello SDK ha restituito un oggetto di risposta con codice di stato HTTP, viene spesso non mi serviva toocheck quanto i metodi di operazione generare `CloudException` per qualsiasi codice di stato che indica un errore. salve nuovi oggetti modello restituire metodi di estensione, il salvataggio di hello evitare toounwrap nel codice.
* Al contrario, hello interfacce core ora espongono metodi che offrono maggiore controllo a livello di hello HTTP se è necessario. È ora possibile passare toobe di intestazioni HTTP personalizzate incluse nelle richieste e hello nuovo `AzureOperationResponse<T>` restituire tipo consente l'accesso diretto toohello `HttpRequestMessage` e `HttpResponseMessage` per l'operazione di hello. `AzureOperationResponse`è definito in hello `Microsoft.Rest.Azure` dello spazio dei nomi e lo sostituisce `Hyak.Common.OperationResponse`.

#### <a name="scoringparameters-changes"></a>Modifiche a ScoringParameters
Una nuova classe denominata `ScoringParameter` è stato aggiunto in toomake SDK più recente di hello profili di tooscoring parametri tooprovide più semplici in una query di ricerca. In precedenza hello `ScoringProfiles` proprietà di hello `SearchParameters` digitata come classe `IList<string>`; Ora è digitato come `IList<ScoringParameter>`.

##### <a name="example"></a>Esempio
Se il codice è simile a questo:

    var sp = new SearchParameters();
    sp.ScoringProfile = "jobsScoringFeatured";      // Use a scoring profile
    sp.ScoringParameters = new[] { "featuredParam-featured", "mapCenterParam-" + lon + "," + lat };

È possibile modificarla toothis toofix eventuali errori di compilazione: 

    var sp = new SearchParameters();
    sp.ScoringProfile = "jobsScoringFeatured";      // Use a scoring profile
    sp.ScoringParameters =
        new[]
        {
            new ScoringParameter("featuredParam", new[] { "featured" }),
            new ScoringParameter("mapCenterParam", GeographyPoint.Create(lat, lon))
        };

#### <a name="model-class-changes"></a>Modifiche alle classi di modelli
A causa di modifiche alla firma digitale toohello descritto in [le modifiche al metodo di operazione](#OperationMethodChanges), molte classi di hello `Microsoft.Azure.Search.Models` dello spazio dei nomi sono stati rinominati o rimossi. ad esempio:

* `IndexDefinitionResponse` è stata sostituita da `AzureOperationResponse<Index>`
* `DocumentSearchResponse`è stato rinominato troppo`DocumentSearchResult`
* `IndexResult`è stato rinominato troppo`IndexingResult`
* `Documents.Count()`Restituisce un `long` con numero di documenti hello anziché di un`DocumentCountResponse`
* `IndexGetStatisticsResponse`è stato rinominato troppo`IndexGetStatisticsResult`
* `IndexListResponse`è stato rinominato troppo`IndexListResult`

toosummarize, `OperationResponse`-le classi derivate che esisteva solo toowrap un oggetto modello sono state rimosse. Hello altre classi hanno il suffisso modificato da `Response` troppo`Result`.

##### <a name="example"></a>Esempio
Se il codice è simile a questo:

    IndexerGetStatusResponse statusResponse = null;

    try
    {
        statusResponse = _searchClient.Indexers.GetStatus(indexer.Name);
    }
    catch (Exception ex)
    {
        Console.WriteLine("Error polling for indexer status: {0}", ex.Message);
        return;
    }

    IndexerExecutionResult lastResult = statusResponse.ExecutionInfo.LastResult;

È possibile modificarla toothis toofix eventuali errori di compilazione:

    IndexerExecutionInfo status = null;

    try
    {
        status = _searchClient.Indexers.GetStatus(indexer.Name);
    }
    catch (Exception ex)
    {
        Console.WriteLine("Error polling for indexer status: {0}", ex.Message);
        return;
    }

    IndexerExecutionResult lastResult = status.LastResult;

##### <a name="response-classes-and-ienumerable"></a>Classi di risposte e IEnumerable
Un'altra modifica che può avere effetto sul codice è che le classi di risposte contenenti raccolte non implementano più `IEnumerable<T>`. Al contrario, è possibile accedere direttamente la proprietà di raccolta hello. Ad esempio, se il codice è simile a questo:

    DocumentSearchResponse<Hotel> response = indexClient.Documents.Search<Hotel>(searchText, sp);
    foreach (SearchResult<Hotel> result in response)
    {
        Console.WriteLine(result.Document);
    }

È possibile modificarla toothis toofix eventuali errori di compilazione:

    DocumentSearchResult<Hotel> response = indexClient.Documents.Search<Hotel>(searchText, sp);
    foreach (SearchResult<Hotel> result in response.Results)
    {
        Console.WriteLine(result.Document);
    }

##### <a name="special-case-for-web-applications"></a>Caso speciale per le applicazioni Web
Se si dispone di un'applicazione web che serializza `DocumentSearchResponse` direttamente i risultati della ricerca di toosend toohello browser, sarà necessario toochange il codice o risultati hello non serializzerà correttamente. Ad esempio, se il codice è simile a questo:

    public ActionResult Search(string q = "")
    {
        // If blank search, assume they want toosearch everything
        if (string.IsNullOrWhiteSpace(q))
            q = "*";

        return new JsonResult
        {
            JsonRequestBehavior = JsonRequestBehavior.AllowGet,
            Data = _featuresSearch.Search(q)
        };
    }

È possibile modificarlo tramite il recupero hello `.Results` proprietà di hello ricerca risposta toofix ricerca risultati per il rendering:

    public ActionResult Search(string q = "")
    {
        // If blank search, assume they want toosearch everything
        if (string.IsNullOrWhiteSpace(q))
            q = "*";

        return new JsonResult
        {
            JsonRequestBehavior = JsonRequestBehavior.AllowGet,
            Data = _featuresSearch.Search(q).Results
        };
    }

Sarà necessario toolook in questo caso nel codice manualmente. **compilatore hello non segnalerà** perché `JsonResult.Data` è di tipo `object`.

#### <a name="cloudexception-changes"></a>Modifiche a CloudException
Hello `CloudException` classe è stata spostata da hello `Hyak.Common` toohello dello spazio dei nomi `Microsoft.Rest.Azure` dello spazio dei nomi. Inoltre, il relativo `Error` proprietà è stata rinominata troppo`Body`.

#### <a name="searchserviceclient-and-searchindexclient-changes"></a>Modifiche a SearchServiceClient e SearchIndexClient
tipo di hello Hello `Credentials` proprietà è stata modificata da `SearchCredentials` tooits classe base, `ServiceClientCredentials`. Se è necessario hello tooaccess `SearchCredentials` di un `SearchIndexClient` o `SearchServiceClient`, usare hello nuovo `SearchCredentials` proprietà.

Nelle versioni precedenti del SDK, hello `SearchServiceClient` e `SearchIndexClient` ha costruttori che ha richiesto un `HttpClient` parametro. Questi sono stati sostituiti con costruttori che accettano `HttpClientHandler` e una matrice di oggetti `DelegatingHandler`. Questo rende più semplice tooinstall gestori personalizzati toopre-elaborano le richieste HTTP se necessario.

Infine, hello costruttori che ha richiesto un `Uri` e `SearchCredentials` sono stati modificati. Ad esempio, se il codice è simile a questo:

    var client =
        new SearchServiceClient(
            new SearchCredentials("abc123"),
            new Uri("http://myservice.search.windows.net"));

È possibile modificarla toothis toofix eventuali errori di compilazione:

    var client =
        new SearchServiceClient(
            new Uri("http://myservice.search.windows.net"),
            new SearchCredentials("abc123"));

Si noti che il tipo di hello di hello credenziali parametro ha modificato anche troppo`ServiceClientCredentials`. Si tratta di tooaffect improbabile che il codice dal `SearchCredentials` è derivato da `ServiceClientCredentials`.

#### <a name="passing-a-request-id"></a>Passaggio di un ID richiesta
Nelle versioni precedenti di hello SDK, è possibile impostare un ID di richiesta su hello `SearchServiceClient` o `SearchIndexClient` e potrebbe essere incluso in ogni toohello richiesta API REST. Ciò è utile per la risoluzione dei problemi con il servizio di ricerca se è necessario il supporto toocontact. Tuttavia, è più utile tooset ID richiesta univoco per ogni operazione anziché toouse hello lo stesso ID per tutte le operazioni. Per questo motivo, hello `SetClientRequestId` metodi di `SearchServiceClient` e `SearchIndexClient` sono state rimosse. In alternativa, è possibile passare un metodo dell'operazione richiesta ID tooeach tramite hello facoltativo `SearchRequestOptions` parametro.

> [!NOTE]
> In una versione futura di hello SDK, verranno aggiunti un nuovo meccanismo per impostare un ID di richiesta a livello globale in client hello gli oggetti che è coerenza con l'approccio di hello utilizzato da altri SDK di Azure.
> 
> 

#### <a name="example"></a>Esempio
Se il codice è simile a questo:

    client.SetClientRequestId(Guid.NewGuid());
    ...
    long count = client.Documents.Count();

È possibile modificarla toothis toofix eventuali errori di compilazione:

    long count = client.Documents.Count(new SearchRequestOptions(requestId: Guid.NewGuid()));

#### <a name="interface-name-changes"></a>Modifiche ai nomi delle interfacce
nomi di interfaccia di Hello operazione gruppo hanno tutti toobe modificate coerente con i nomi delle proprietà corrispondenti:

* tipo di Hello `ISearchServiceClient.Indexes` è stato rinominato da `IIndexOperations` troppo`IIndexesOperations`.
* tipo di Hello `ISearchServiceClient.Indexers` è stato rinominato da `IIndexerOperations` troppo`IIndexersOperations`.
* tipo di Hello `ISearchServiceClient.DataSources` è stato rinominato da `IDataSourceOperations` troppo`IDataSourcesOperations`.
* tipo di Hello `ISearchIndexClient.Documents` è stato rinominato da `IDocumentOperations` troppo`IDocumentsOperations`.

Questa modifica è tooaffect improbabile che il codice a meno che non è stato creato le simulazioni di queste interfacce per scopi di test.

<a name="BugFixesV1"></a>

### <a name="bug-fixes-in-version-11"></a>Correzioni di bug nella versione 1.1
Si è verificato un bug nelle versioni precedenti di hello Azure Search .NET SDK di tooserialization relative classi di modello personalizzato. bug Hello può verificarsi se una classe di modello personalizzato è stato creato con una proprietà di un tipo di valore non nullable.

#### <a name="steps-tooreproduce"></a>Passaggi tooreproduce
Creare una classe di modelli personalizzata con una proprietà di tipo di valore non nullable. Ad esempio, aggiungere una proprietà pubblica `UnitCount` di tipo `int` invece che `int?`.

Se un documento con il valore predefinito hello di quel tipo di indice (ad esempio, 0 per `int`), campo hello sarà null in ricerca di Azure. Se successivamente esegue la ricerca per il documento, hello `Search` chiamata genererà `JsonSerializationException` che segnala che che non è possibile convertire `null` troppo`int`.

Inoltre, i filtri potrebbero non funzionare come previsto dopo la scrittura di indice toohello anziché il valore previsto hello null.

#### <a name="fix-details"></a>Dettagli della correzione
Questo problema è stato risolto nella versione 1.1 di hello SDK. Se è presente una classe di modelli come questa:

    public class Model
    {
        public string Key { get; set; }

        public int IntValue { get; set; }
    }

e si imposta `IntValue` too0, che valore è ora correttamente serializzato come 0 in transito hello e archiviato come indice hello 0. Anche il round trip funziona come previsto.

È compatibile con questo approccio richiede una toobe problema potenziale: se si utilizza un tipo di modello con una proprietà che non ammette valori null, è necessario troppo**garantire** che nessun documenti nell'indice contengono un valore null per il campo corrispondente hello. Hello SDK né hello API REST di ricerca di Azure consentirà si tooenforce questo.

Non è un problema di ipotetica: si consideri uno scenario in cui aggiungere un nuovo campo tooan esistente indice di tipo `Edm.Int32`. Dopo aver aggiornato la definizione dell'indice hello, tutti i documenti avrà un valore null per il nuovo campo (poiché tutti i tipi nullable in ricerca di Azure). Se si utilizza una classe di modello con un non-nullable `int` proprietà per il campo, si otterrà un `JsonSerializationException` simile durante il tentativo di tooretrieve documenti:

    Error converting value {null} tootype 'System.Int32'. Path 'IntValue'.

Per questo motivo, è ancora consigliabile usare tipi nullable nelle classi di modelli.

Per ulteriori informazioni su questa correzione di bug e hello, vedere [questo problema in GitHub](https://github.com/Azure/azure-sdk-for-net/issues/1063).

