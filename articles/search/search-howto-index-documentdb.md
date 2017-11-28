---
title: aaaIndexing un'origine dati DB Cosmos per ricerca di Azure | Documenti Microsoft
description: In questo articolo illustra come toocreate un indicizzatore di ricerca di Azure con DB Cosmos come origine dati.
services: search
documentationcenter: 
author: chaosrealm
manager: pablocas
editor: 
ms.assetid: 
ms.service: search
ms.devlang: rest-api
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: search
ms.date: 08/10/2017
ms.author: eugenesh
ms.openlocfilehash: 195c9bc026ee1591679dc425ef083a32a3c86be6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connecting-cosmos-db-with-azure-search-using-indexers"></a>Connessione di Cosmos DB con Ricerca di Azure tramite indicizzatori

Se si desidera una ricerca ottima esperienza tooimplement sui dati Cosmos DB, è possibile utilizzare dati di toopull un indicizzatore di ricerca di Azure in un indice di ricerca di Azure. In questo articolo verrà illustrato come toointegrate DB Cosmos Azure con ricerca di Azure senza la necessità di un'infrastruttura di indicizzazione toomaintain codice toowrite.

tooset di un indicizzatore Cosmos DB, è necessario disporre di un [servizio di ricerca di Azure](search-create-service-portal.md)e creare un indice, l'origine dati e infine indicizzatore hello. È possibile creare questi oggetti tramite hello [portale](search-import-data-portal.md), [.NET SDK](/dotnet/api/microsoft.azure.search), o [API REST](/rest/api/searchservice/) per tutti i linguaggi non .NET. 

Se non si scelga portale hello, hello [importazione guidata dati](search-import-data-portal.md) in modo semplificato la creazione di hello di tutte queste risorse.

> [!NOTE]
> COSMOS DB è hello prossima generazione di DocumentDB. Anche se il nome di prodotto hello viene modificato, la sintassi è hello stesso come in precedenza. Continuare toospecify `documentdb` come indicato in questo articolo di indicizzatore. 

> [!TIP]
> È possibile avviare hello **importare dati** guidata da hello Cosmos DB dashboard toosimplify l'indicizzazione dell'origine dati. Nella finestra di navigazione a sinistra, andare troppo**raccolte** > **aggiungere ricerca di Azure** tooget avviato.

<a name="Concepts"></a>
## <a name="azure-search-indexer-concepts"></a>Concetti relativi all'indicizzatore di Ricerca di Azure
Azure supporta la ricerca hello creazione e gestione di origini dati (inclusi DB Cosmos) e gli indicizzatori che operano su tali origini dati.

Oggetto **origine dati** specifica hello tooindex di dati, credenziali e i criteri per l'identificazione delle modifiche ai dati hello (ad esempio i documenti modificati o eliminati all'interno di raccolta). origine dati Hello è definita come risorsa indipendente in modo che può essere utilizzato da più indicizzatori.

Un **indicizzatore** descrive hello flusso dei dati dall'origine dati in un indice di ricerca di destinazione. Un indicizzatore consente di:

* Eseguire una copia occasionale dei dati di hello toopopulate un indice.
* Un indice con le modifiche nell'origine dati hello in una pianificazione di sincronizzazione. pianificazione di Hello fa parte della definizione di indicizzatore hello.
* Richiamare l'indice di tooan aggiornamenti su richiesta in base alle esigenze.

<a name="CreateDataSource"></a>
## <a name="step-1-create-a-data-source"></a>Passaggio 1: Creare un'origine dati
toocreate un'origine dati, effettuare un POST:

    POST https://[service name].search.windows.net/datasources?api-version=2016-09-01
    Content-Type: application/json
    api-key: [Search service admin key]

    {
        "name": "mydocdbdatasource",
        "type": "documentdb",
        "credentials": {
            "connectionString": "AccountEndpoint=https://myDocDbEndpoint.documents.azure.com;AccountKey=myDocDbAuthKey;Database=myDocDbDatabaseId"
        },
        "container": { "name": "myDocDbCollectionId", "query": null },
        "dataChangeDetectionPolicy": {
            "@odata.type": "#Microsoft.Azure.Search.HighWaterMarkChangeDetectionPolicy",
            "highWaterMarkColumnName": "_ts"
        }
    }

corpo Hello della richiesta di hello contiene hello definizione dell'origine dati che deve includere hello seguenti campi:

* **nome**: scegliere qualsiasi nome toorepresent database DB Cosmos.
* **type**: deve essere `documentdb`.
* **Credenziali**
  
  * **connectionString**: obbligatorio. Specificare il database Azure Cosmos DB tooyour di hello connessione info in hello seguente formato:`AccountEndpoint=<Cosmos DB endpoint url>;AccountKey=<Cosmos DB auth key>;Database=<Cosmos DB database id>`
* **contenitore**:
  
  * **name**: obbligatorio. Specificare l'id di hello di hello Cosmos DB raccolta toobe indicizzato.
  * **query**: facoltativa. È possibile specificare un tooflatten query un documento JSON arbitrario in uno schema flat che ricerca di Azure può essere indicizzata.
* **dataChangeDetectionPolicy**: consigliato. Vedere la sezione [Indicizzazione di documenti modificati](#DataChangeDetectionPolicy).
* **dataDeletionDetectionPolicy**: facoltativo. Vedere la sezione [Indicizzazione di documenti eliminati](#DataDeletionDetectionPolicy).

### <a name="using-queries-tooshape-indexed-data"></a>Utilizzando le query tooshape indicizzata dati
È possibile specificare un tooflatten query Cosmos DB due proprietà annidate o matrici, proiettare le proprietà JSON e filtrare hello toobe di dati indicizzati. 

Documento di esempio:

    {
        "userId": 10001,
        "contact": {
            "firstName": "andy",
            "lastName": "hoh"
        },
        "company": "microsoft",
        "tags": ["azure", "documentdb", "search"]
    }

Query di filtro:

    SELECT * FROM c WHERE c.company = "microsoft" and c._ts >= @HighWaterMark ORDER BY c._ts

Query di appiattimento:

    SELECT c.id, c.userId, c.contact.firstName, c.contact.lastName, c.company, c._ts FROM c WHERE c._ts >= @HighWaterMark ORDER BY c._ts
    
    
Query di proiezione:

    SELECT VALUE { "id":c.id, "Name":c.contact.firstName, "Company":c.company, "_ts":c._ts } FROM c WHERE c._ts >= @HighWaterMark ORDER BY c._ts


Query di appiattimento matrici:

    SELECT c.id, c.userId, tag, c._ts FROM c JOIN tag IN c.tags WHERE c._ts >= @HighWaterMark ORDER BY c._ts

<a name="CreateIndex"></a>
## <a name="step-2-create-an-index"></a>Passaggio 2: Creare un indice
Creare un indice di Ricerca di Azure di destinazione, se non ne è già disponibile uno. È possibile creare un indice utilizzando hello [interfaccia utente del portale Azure](search-create-index-portal.md), hello [creare API REST di indice](/rest/api/searchservice/create-index) o [classe Index](/dotnet/api/microsoft.azure.search.models.index).

Hello di esempio seguente viene creato un indice con un campo id e la descrizione:

    POST https://[service name].search.windows.net/indexes?api-version=2016-09-01
    Content-Type: application/json
    api-key: [Search service admin key]

    {
       "name": "mysearchindex",
       "fields": [{
         "name": "id",
         "type": "Edm.String",
         "key": true,
         "searchable": false
       }, {
         "name": "description",
         "type": "Edm.String",
         "filterable": false,
         "sortable": false,
         "facetable": false,
         "suggestions": true
       }]
     }

Verificare che hello dello schema dell'indice di destinazione è compatibile con schema hello hello JSON dei documenti di origine o di output di hello la proiezione di query personalizzata.

> [!NOTE]
> Per le raccolte partizionate, chiave di documento predefinite hello è Cosmos DB `_rid` proprietà, che viene rinominato troppo`rid` in ricerca di Azure. I valori `_rid` di Cosmos DB contengono inoltre caratteri non validi per le chiavi di Ricerca di Azure. Per questo motivo, hello `_rid` i valori sono con codificata Base64.
> 
> 

### <a name="mapping-between-json-data-types-and-azure-search-data-types"></a>Mapping tra tipi di dati JSON e tipi di dati di Ricerca di Azure
| TIPO DI DATI JSON | TIPI DI CAMPI DELL'INDICE DI DESTINAZIONE COMPATIBILI |
| --- | --- |
| Booleano |Edm.Boolean, Edm.String |
| Numeri che rappresentano numeri interi |Edm.Int32, Edm.Int64, Edm.String |
| Numeri che rappresentano numeri a virgola mobile |Edm.Double, Edm.String |
| String |Edm.String |
| Matrici di tipi primitivi, ad esempio ["a", "b", "c"] |Collection(Edm.String) |
| Stringhe che rappresentano date |Edm.DateTimeOffset, Edm.String |
| Oggetti GeoJSON, ad esempio { "type": "Point", "coordinates": [long, lat] } |Edm.GeographyPoint |
| Altri oggetti JSON |N/D |

<a name="CreateIndexer"></a>
## <a name="step-3-create-an-indexer"></a>Passaggio 3: Creare un indicizzatore

Dopo avere creato hello indice e l'origine dati, si è pronti toocreate indicizzatore di hello:

    POST https://[service name].search.windows.net/indexers?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
      "name" : "mydocdbindexer",
      "dataSourceName" : "mydocdbdatasource",
      "targetIndexName" : "mysearchindex",
      "schedule" : { "interval" : "PT2H" }
    }

Questo indicizzatore viene eseguito ogni due ore (intervallo di pianificazione è impostata troppo "PT2H"). un indicizzatore toorun ogni 30 minuti, impostare l'intervallo di hello troppo "PT30M". intervallo supportato di Hello minimo è 5 minuti. Hello pianificazione è facoltativa: Se omesso, viene eseguito un indicizzatore solo una volta al momento della creazione. Tuttavia, è possibile eseguire un indicizzatore su richiesta in qualsiasi momento.   

Per ulteriori informazioni su hello creare API di indicizzatore, estrarre [indicizzatore creare](https://docs.microsoft.com/rest/api/searchservice/create-indexer).

<a id="RunIndexer"></a>
### <a name="running-indexer-on-demand"></a>Esecuzione di un indicizzatore su richiesta
In aggiunta toorunning periodicamente in base alla pianificazione, un indicizzatore può anche essere richiamato su richiesta:

    POST https://[service name].search.windows.net/indexers/[indexer name]/run?api-version=2016-09-01
    api-key: [Search service admin key]

> [!NOTE]
> Quando eseguire API restituisce correttamente, chiamata all'indicizzatore hello è stata pianificata, ma l'elaborazione effettiva hello avviene in modo asincrono. 

È possibile monitorare lo stato dell'indicizzatore hello nel portale di hello o utilizzando hello ottenere indicizzatore stato API, che verranno descritti successivamente. 

<a name="GetIndexerStatus"></a>
### <a name="getting-indexer-status"></a>Ottenere lo stato dell'indicizzatore
È possibile recuperare cronologia hello di stato e l'esecuzione di un indicizzatore:

    GET https://[service name].search.windows.net/indexers/[indexer name]/status?api-version=2016-09-01
    api-key: [Search service admin key]

risposta Hello contiene stato complessivo dell'indicizzatore, chiamata di hello indicizzatore ultimo (o in corso) e la cronologia di hello delle chiamate recenti.

    {
        "status":"running",
        "lastResult": {
            "status":"success",
            "errorMessage":null,
            "startTime":"2014-11-26T03:37:18.853Z",
            "endTime":"2014-11-26T03:37:19.012Z",
            "errors":[],
            "itemsProcessed":11,
            "itemsFailed":0,
            "initialTrackingState":null,
            "finalTrackingState":null
         },
        "executionHistory":[ {
            "status":"success",
             "errorMessage":null,
            "startTime":"2014-11-26T03:37:18.853Z",
            "endTime":"2014-11-26T03:37:19.012Z",
            "errors":[],
            "itemsProcessed":11,
            "itemsFailed":0,
            "initialTrackingState":null,
            "finalTrackingState":null
        }]
    }

Cronologia di esecuzione contiene backup toohello 50 ultime esecuzioni completate, che vengono ordinate in ordine cronologico inverso (in modo esecuzione più recente di hello per primo in risposta hello).

<a name="DataChangeDetectionPolicy"></a>
## <a name="indexing-changed-documents"></a>Indicizzazione di documenti modificati
scopo di Hello dei dati di modifica dei criteri di rilevamento è tooefficiently identificare gli elementi di dati modificati. Attualmente, i criteri di hello è supportato solo sono hello `High Water Mark` criteri utilizzando hello `_ts` proprietà (timestamp) fornita da DB Cosmos, specificata come indicato di seguito:

    {
        "@odata.type" : "#Microsoft.Azure.Search.HighWaterMarkChangeDetectionPolicy",
        "highWaterMarkColumnName" : "_ts"
    }

Usa questo criterio è fortemente consigliato prestazioni indicizzatore buona tooensure. 

Se si utilizza una query personalizzata, assicurarsi che tale hello `_ts` proprietà viene proiettata da query hello.

<a name="IncrementalProgress"></a>
### <a name="incremental-progress-and-custom-queries"></a>Avanzamento incrementale e query personalizzate
Stato di avanzamento incrementale durante l'indicizzazione assicura che se l'esecuzione dell'indicizzatore è stato interrotto da errori temporanei o il limite di tempo di esecuzione, indicizzatore hello può prelevare dove era stata interrotta successivo viene eseguito, anziché l'intera raccolta hello toore indice da zero. Questo approccio risulta particolarmente importante in caso di indicizzazione di raccolte di grandi dimensioni. 

tooenable lo stato incrementale quando si utilizza una query personalizzata, assicurarsi che la query Ordina risultati hello base hello `_ts` colonna. In questo modo periodico controllo verso il basso che ricerca di Azure utilizza lo stato incrementale tooprovide in presenza di hello di errori.   

In alcuni casi, anche se la query contiene un `ORDER BY [collection alias]._ts` clausola, ricerca di Azure potrebbe non derivare query hello viene ordinato in base hello `_ts`. In ricerca di Azure è possibile indicare che i risultati vengono ordinati usando hello `assumeOrderByHighWaterMarkColumn` proprietà di configurazione. toospecify Questo hint, creare o aggiornare l'indicizzatore come segue: 

    {
     ... other indexer definition properties
     "parameters" : {
            "configuration" : { "assumeOrderByHighWaterMarkColumn" : true } }
    } 

<a name="DataDeletionDetectionPolicy"></a>
## <a name="indexing-deleted-documents"></a>Indicizzazione di documenti eliminati
Quando le righe vengono eliminate dalla raccolta di hello, in genere si toodelete le righe dall'indice di ricerca hello anche. scopo di Hello di criteri di rilevamento di eliminazione di dati è tooefficiently identificare gli elementi dati eliminati. Attualmente, i criteri di hello è supportato solo sono hello `Soft Delete` criteri (l'eliminazione è contrassegnata con un flag di qualche), che viene specificata come segue:

    {
        "@odata.type" : "#Microsoft.Azure.Search.SoftDeleteColumnDeletionDetectionPolicy",
        "softDeleteColumnName" : "hello property that specifies whether a document was deleted",
        "softDeleteMarkerValue" : "hello value that identifies a document as deleted"
    }

Se si utilizza una query personalizzata, assicurarsi che tale proprietà hello a cui fa riferimento `softDeleteColumnName` viene proiettato da query hello.

Hello di esempio seguente crea un'origine dati con un criterio di eliminazione temporanea:

    POST https://[Search service name].search.windows.net/datasources?api-version=2016-09-01
    Content-Type: application/json
    api-key: [Search service admin key]

    {
        "name": "mydocdbdatasource",
        "type": "documentdb",
        "credentials": {
            "connectionString": "AccountEndpoint=https://myDocDbEndpoint.documents.azure.com;AccountKey=myDocDbAuthKey;Database=myDocDbDatabaseId"
        },
        "container": { "name": "myDocDbCollectionId" },
        "dataChangeDetectionPolicy": {
            "@odata.type": "#Microsoft.Azure.Search.HighWaterMarkChangeDetectionPolicy",
            "highWaterMarkColumnName": "_ts"
        },
        "dataDeletionDetectionPolicy": {
            "@odata.type": "#Microsoft.Azure.Search.SoftDeleteColumnDeletionDetectionPolicy",
            "softDeleteColumnName": "isDeleted",
            "softDeleteMarkerValue": "true"
        }
    }

## <a name="NextSteps"></a>Passaggi successivi
Congratulazioni. Si è appreso come toointegrate DB Cosmos Azure con ricerca di Azure hello indicizzatore per Cosmos DB.

* toolearn come ulteriori informazioni su Azure Cosmos DB, vedere hello [pagina servizio Cosmos DB](https://azure.microsoft.com/services/documentdb/).
* toolearn come più sulla ricerca di Azure, vedere hello [pagina del servizio di ricerca](https://azure.microsoft.com/services/search/).
