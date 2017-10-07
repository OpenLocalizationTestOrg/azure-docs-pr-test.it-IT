---
title: aaaConnecting Database SQL di Azure tooAzure gli indicizzatori di ricerca con | Documenti Microsoft
description: Informazioni su come toopull dati dal Database SQL di Azure tooan ricerca di Azure un indice utilizzando gli indicizzatori.
services: search
documentationcenter: 
author: chaosrealm
manager: pablocas
editor: 
ms.assetid: e9bbf352-dfff-4872-9b17-b1351aae519f
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 07/13/2017
ms.author: eugenesh
ms.openlocfilehash: b28a11cf18ef994de99e09af90bbfeb171ef3cde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connecting-azure-sql-database-tooazure-search-using-indexers"></a>La connessione di Database SQL di Azure tooAzure ricerca utilizzo degli indicizzatori

Prima di poter eseguire una query nell'[indice di Ricerca di Azure](search-what-is-an-index.md), è necessario inserirvi i propri dati. Se i dati di hello vive in un database SQL di Azure, un **indicizzatore di ricerca di Azure per Database SQL di Azure** (o **indicizzatore di SQL Azure** breve) consente di automatizzare hello processo di indicizzazione, ovvero meno codice toowrite e meno infrastruttura toocare su.

In questo articolo vengono illustrati i meccanismi di hello dell'utilizzo di [indicizzatori](search-indexer-overview.md), ma descrive inoltre le funzionalità disponibile solo con database SQL di Azure (ad esempio, il rilevamento modifiche integrato). 

Nei database SQL tooAzure aggiunta, la ricerca di Azure fornisce gli indicizzatori per [Azure Cosmos DB](search-howto-index-documentdb.md), [archiviazione Blob di Azure](search-howto-indexing-azure-blob-storage.md), e [archiviazione tabelle di Azure](search-howto-indexing-azure-tables.md). supporto toorequest per altre origini dati, fornire commenti e suggerimenti su hello [forum sul feedback su ricerca di Azure](https://feedback.azure.com/forums/263029-azure-search/).

## <a name="indexers-and-data-sources"></a>Indicizzatori e origini dati

Oggetto **origine dati** specifica quali tooindex di dati, le credenziali per l'accesso ai dati e criteri che identificano in modo efficiente le modifiche nei dati hello (nuovo, modificate o eliminate righe). È definita come risorsa indipendente affinché possa essere usata da più indicizzatori.

Un **indicizzatore** è una risorsa che connette una singola origine dati agli indici di ricerca di destinazione. Un indicizzatore viene usato in hello seguenti modi:

* Eseguire una copia occasionale dei dati di hello toopopulate un indice.
* Aggiornamento di un indice con le modifiche nell'origine dati hello in una pianificazione.
* Eseguire tooupdate su richiesta di un indice in base alle esigenze.

Un indicizzatore può utilizzare solo una tabella o vista, ma se si desidera toopopulate più indici di ricerca, è possibile creare più indicizzatori. Per altre informazioni sui concetti, vedere [Operazioni degli indicizzatori: flusso di lavoro tipico](https://docs.microsoft.com/rest/api/searchservice/Indexer-operations#typical-workflow).

È possibile impostare e configurare un indicizzatore SQL di Azure usando:

* Importazione guidata dei dati in hello [portale di Azure](https://portal.azure.com)
* [.NET SDK](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.indexer?view=azure-dotnet) Ricerca di Azure
* [API REST](https://docs.microsoft.com/en-us/rest/api/searchservice/indexer-operations) Ricerca di Azure

In questo articolo, si userà hello API REST toocreate **indicizzatori** e **origini dati**.

## <a name="when-toouse-azure-sql-indexer"></a>Quando toouse indicizzatore di SQL Azure
A seconda di diversi fattori tooyour dati, utilizzare hello dell'indicizzatore di SQL Azure o potrebbe non essere appropriato. Se i dati si adatta hello seguenti requisiti, è possibile utilizzare l'indicizzatore di SQL Azure.

| Criteri | Dettagli |
|----------|---------|
| I dati provengono da una singola tabella o vista | Se i dati di hello sono dispersi tra più tabelle, è possibile creare una singola visualizzazione dei dati di hello. Tuttavia, se si utilizza una vista, non sarà in grado di toouse integrato di SQL Server change rilevamento toorefresh un indice con le modifiche incrementali. Per altre informazioni, vedere [Acquisizione delle righe modificate ed eliminate](#CaptureChangedRows) di seguito. |
| Tipi di dati compatibili | La maggior parte ma non tutti i tipi SQL hello sono supportati in un indice di ricerca di Azure. Per un elenco, vedere [Elenco dei tipi di dati](#TypeMapping). |
| La sincronizzazione dei dati in tempo reale non è necessaria | Un indicizzatore può reindicizzare la tabella al massimo ogni 5 minuti. Se le modifiche dei dati e spesso hello cambia toobe necessità riflesse nell'indice hello entro pochi secondi o minuti singoli, è consigliabile utilizzare hello [API REST](https://docs.microsoft.com/rest/api/searchservice/AddUpdate-or-Delete-Documents) o [.NET SDK](search-import-data-dotnet.md) toopush direttamente le righe aggiornate. |
| L'indicizzazione incrementale è possibile | Se si dispone di un set di dati di grandi dimensioni e dell'indicizzatore di hello toorun piano in una pianificazione, ricerca di Azure deve essere in grado di tooefficiently identificare le righe nuove, modificate o eliminate. L'indicizzazione incrementale è consentito solo se si esegue l'indicizzazione su richiesta, non programmata, o se la si esegue per meno di 100.000 righe. Per altre informazioni, vedere [Acquisizione delle righe modificate ed eliminate](#CaptureChangedRows) di seguito. |

## <a name="create-an-azure-sql-indexer"></a>Creare un indicizzatore SQL di Azure

1. Creare l'origine dati hello:

   ```
    POST https://myservice.search.windows.net/datasources?api-version=2016-09-01
    Content-Type: application/json
    api-key: admin-key

    {
        "name" : "myazuresqldatasource",
        "type" : "azuresql",
        "credentials" : { "connectionString" : "Server=tcp:<your server>.database.windows.net,1433;Database=<your database>;User ID=<your user name>;Password=<your password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30;" },
        "container" : { "name" : "name of hello table or view that you want tooindex" }
    }
   ```

   È possibile ottenere la stringa di connessione hello da hello [portale di Azure](https://portal.azure.com); utilizzare hello `ADO.NET connection string` opzione.

2. Creare l'indice di ricerca di Azure di destinazione hello se non è già disponibile. È possibile creare un indice utilizzando hello [portale](https://portal.azure.com) o hello [creare API indice](https://docs.microsoft.com/rest/api/searchservice/Create-Index). Verificare che hello dello schema dell'indice di destinazione è compatibile con hello schema della tabella di origine hello [mapping di tipi di dati tra SQL e ricerca di Azure](#TypeMapping).

3. Creare un indicizzatore hello assegnarle un nome e facendo riferimento a indice di origine e destinazione dati hello:

    ```
    POST https://myservice.search.windows.net/indexers?api-version=2016-09-01
    Content-Type: application/json
    api-key: admin-key

    {
        "name" : "myindexer",
        "dataSourceName" : "myazuresqldatasource",
        "targetIndexName" : "target index name"
    }
    ```

Un indicizzatore creato in questo modo non dispone di una pianificazione. Viene eseguito non appena viene creato. È possibile rieseguirlo in qualsiasi momento mediante una richiesta di **esecuzione indicizzatore** :

    POST https://myservice.search.windows.net/indexers/myindexer/run?api-version=2016-09-01
    api-key: admin-key

È possibile personalizzare alcuni aspetti del comportamento dell'indicizzatore, ad esempio le dimensioni del batch e il numero di documenti che è possibile ignorare prima che un'esecuzione dell'indicizzatore abbia esito negativo. Per altre informazioni, vedere [Create Indexer API](https://docs.microsoft.com/rest/api/searchservice/Create-Indexer)(Creare un'API di indicizzatore).

Potrebbe essere necessario database tooyour tooconnect di tooallow servizi di Azure. Vedere [connessione da Azure](https://docs.microsoft.com/azure/sql-database/sql-database-firewall-configure) per istruzioni su come toodo che.

toomonitor hello lo stato dell'indicizzatore e la cronologia delle esecuzioni (numero di elementi indicizzati, errori e così via), utilizzare un **lo stato dell'indicizzatore** richiesta:

    GET https://myservice.search.windows.net/indexers/myindexer/status?api-version=2016-09-01
    api-key: admin-key

risposta Hello dovrebbe essere simile toohello seguenti:

    {
        "@odata.context":"https://myservice.search.windows.net/$metadata#Microsoft.Azure.Search.V2015_02_28.IndexerExecutionInfo",
        "status":"running",
        "lastResult": {
            "status":"success",
            "errorMessage":null,
            "startTime":"2015-02-21T00:23:24.957Z",
            "endTime":"2015-02-21T00:36:47.752Z",
            "errors":[],
            "itemsProcessed":1599501,
            "itemsFailed":0,
            "initialTrackingState":null,
            "finalTrackingState":null
        },
        "executionHistory":
        [
            {
                "status":"success",
                "errorMessage":null,
                "startTime":"2015-02-21T00:23:24.957Z",
                "endTime":"2015-02-21T00:36:47.752Z",
                "errors":[],
                "itemsProcessed":1599501,
                "itemsFailed":0,
                "initialTrackingState":null,
                "finalTrackingState":null
            },
            ... earlier history items
        ]
    }

Cronologia di esecuzione contiene backup too50 di esecuzioni di hello completata più di recente, che vengono ordinati in ordine cronologico inverso hello (in modo che l'esecuzione più recente di hello per primo in risposta hello).
Ulteriori informazioni sulla risposta hello sono reperibile [ottenere lo stato dell'indicizzatore](http://go.microsoft.com/fwlink/p/?LinkId=528198)

## <a name="run-indexers-on-a-schedule"></a>Eseguire gli indicizzatori in base a una pianificazione
È anche possibile disporre hello indicizzatore toorun periodicamente in base alla pianificazione. toodo, aggiungere hello **pianificazione** proprietà durante la creazione o l'aggiornamento dell'indicizzatore hello. esempio Hello riportato di seguito viene illustrato un indicizzatore di hello tooupdate richiesta PUT:

    PUT https://myservice.search.windows.net/indexers/myindexer?api-version=2016-09-01
    Content-Type: application/json
    api-key: admin-key

    {
        "dataSourceName" : "myazuresqldatasource",
        "targetIndexName" : "target index name",
        "schedule" : { "interval" : "PT10M", "startTime" : "2015-01-01T00:00:00Z" }
    }

Hello **intervallo** parametro è obbligatorio. intervallo "Hello" si riferisce tempo toohello tra inizio hello di due esecuzioni consecutive di indicizzatore. Hello più piccolo consentito intervallo è 5 minuti. Hello più lungo è un giorno. Il valore deve essere formattato come valore XSD "dayTimeDuration" (un subset limitato di un valore [duration ISO 8601](http://www.w3.org/TR/xmlschema11-2/#dayTimeDuration) ). modello Hello è: `P(nD)(T(nH)(nM))`. Esempi: `PT15M` ogni 15 minuti, `PT2H` ogni due ore.

Hello facoltativo **startTime** indica quando hello esecuzioni pianificate devono iniziare. Se viene omesso, viene utilizzata l'ora UTC corrente hello. Questa fase può essere hello oltre – in questo caso prima esecuzione hello viene pianificata come indicizzatore hello è in esecuzione continuamente dal hello startTime.  

È possibile effettuare solo l'esecuzione di un indicizzatore specificato per volta. Se un indicizzatore è in esecuzione quando è pianificata l'esecuzione, esecuzione hello viene rimandata fino al successivo orario pianificato hello.

Si consideri questo toomake un esempio più concreto. Si supponga che abbiamo hello seguenti pianificazione oraria configurato:

    "schedule" : { "interval" : "PT1H", "startTime" : "2015-03-01T00:00:00Z" }

Di seguito è illustrato ciò che accade:

1. prima esecuzione dell'indicizzatore di Hello inizia a o attorno al 1 marzo 2015 12:00 a.m. UTC più o meno.
2. Si supponga che l'esecuzione richieda 20 minuti (o un tempo qualsiasi inferiore a 1 ora).
3. avvio dell'esecuzione secondo Hello a o attorno al 1 marzo 2015 01:00.
4. Si supponga ora che l'esecuzione richieda più di un'ora, ad esempio 70 minuti, e che venga completata alle 02:10 circa.
5. È in corso 2:00:00, ora hello terza esecuzione toostart. Tuttavia, poiché hello seconda esecuzione da 01. è ancora in esecuzione, hello terzi è ignorata. avvio dell'esecuzione terzo Hello 03.00.

È possibile aggiungere, modificare o eliminare una pianificazione per un indicizzatore esistente utilizzando una richiesta di **indicizzatore PUT** .

<a name="CaptureChangedRows"></a>

## <a name="capture-new-changed-and-deleted-rows"></a>Acquisire righe nuove, modificate ed eliminate

Ricerca di Azure Usa **indicizzazione incrementale** tooavoid con toore indice hello intera tabella o vista ogni volta che viene eseguito un indicizzatore. Ricerca di Azure fornisce che due indicizzazione incrementale di rilevamento criteri toosupport di modifica. 

### <a name="sql-integrated-change-tracking-policy"></a>Criteri di rilevamento delle modifiche integrati di SQL
Se il database SQL supporta il [rilevamento delle modifiche](https://docs.microsoft.com/sql/relational-databases/track-changes/about-change-tracking-sql-server), è consigliabile usare i **criteri di rilevamento delle modifiche integrati di SQL**. Si tratta di criteri più efficienti hello. Inoltre, consente le righe eliminate tooidentify di ricerca di Azure senza dover tooadd una tabella di tooyour colonna esplicita "eliminazione temporanea".

#### <a name="requirements"></a>Requisiti 

+ Requisiti sulla versione del database:
  * SQL Server 2012 SP3 e versioni successive, se si usa SQL Server nelle macchine virtuali di Azure.
  * Database SQL di Azure V12, se si utilizza il database SQL di Azure SQL.
+ Solo tabelle, nessuna vista. 
+ Nel database di hello, [Abilita rilevamento](https://docs.microsoft.com/sql/relational-databases/track-changes/enable-and-disable-change-tracking-sql-server) per tabella hello. 
+ Nessuna chiave primaria composta (una chiave primaria che contiene più di una colonna) sulla tabella hello.  

#### <a name="usage"></a>Utilizzo

toouse questo criterio, creare o aggiornare l'origine dati simile al seguente:

    {
        "name" : "myazuresqldatasource",
        "type" : "azuresql",
        "credentials" : { "connectionString" : "connection string" },
        "container" : { "name" : "table or view name" },
        "dataChangeDetectionPolicy" : {
           "@odata.type" : "#Microsoft.Azure.Search.SqlIntegratedChangeTrackingPolicy"
      }
    }

Quando si usano i criteri di rilevamento delle modifiche integrati di SQL, non specificare criteri di rilevamento dell'eliminazione dei dati separati, perché questi ultimi includono il supporto predefinito per l'identificazione delle righe eliminate. Tuttavia, per operazioni"hello eliminazioni toobe rilevato", chiave di documento hello nell'indice di ricerca deve essere hello come chiave primaria hello hello tabella SQL. 

<a name="HighWaterMarkPolicy"></a>

### <a name="high-water-mark-change-detection-policy"></a>Criteri di rilevamento delle modifiche con limite massimo

Questi criteri di rilevamento modifiche si basano su una colonna "limite superiore" acquisizione versione hello o l'ora dell'ultimo aggiornamento di una riga. Se si usa una vista, è consigliabile usare i criteri di livello più alto. colonna limite massimo di Hello deve soddisfare i seguenti requisiti hello.

#### <a name="requirements"></a>Requisiti 

* Tutti gli inserimenti specificano un valore per la colonna hello.
* Elemento tooan di tutti gli aggiornamenti anche modificare il valore di hello della colonna hello.
* il valore di Hello di questa colonna aumenta con ogni inserimento o aggiornamento.
* Query con hello seguente WHERE e clausole ORDER BY possono essere eseguite in modo efficiente:`WHERE [High Water Mark Column] > [Current High Water Mark Value] ORDER BY [High Water Mark Column]`

> [!IMPORTANT] 
> È consigliabile utilizzare hello [rowversion](https://docs.microsoft.com/sql/t-sql/data-types/rowversion-transact-sql) tipo di dati colonna limite massimo di hello. Se si utilizza qualsiasi altro tipo di dati, il rilevamento delle modifiche non è garantito toocapture tutte le modifiche in presenza di hello delle transazioni eseguite contemporaneamente a una query di indicizzatore. Quando si utilizza **rowversion** in una configurazione con le repliche di sola lettura, deve puntare indicizzatore hello alla replica primaria hello. Per scenari di sincronizzazione dei dati, è possibile usare solo una replica primaria.

#### <a name="usage"></a>Utilizzo

toouse un limite massimo di criteri, creare o aggiornare l'origine dati simile al seguente:

    {
        "name" : "myazuresqldatasource",
        "type" : "azuresql",
        "credentials" : { "connectionString" : "connection string" },
        "container" : { "name" : "table or view name" },
        "dataChangeDetectionPolicy" : {
           "@odata.type" : "#Microsoft.Azure.Search.HighWaterMarkChangeDetectionPolicy",
           "highWaterMarkColumnName" : "[a rowversion or last_updated column name]"
      }
    }

> [!WARNING]
> Se la tabella di origine hello non dispone di un indice nella colonna limite massimo di hello, query utilizzate dall'indicizzatore SQL hello può verificarsi un timeout. In particolare, hello `ORDER BY [High Water Mark Column]` clausola richiede toorun un indice in modo efficiente quando hello tabella contiene molte righe.
>
>

Se si verificano errori di timeout, è possibile utilizzare hello `queryTimeout` indicizzatore configurazione impostazione tooset hello tooa valore di timeout query superiore al timeout di 5 minuti hello predefinito. Ad esempio, tooset hello timeout too10 in minuti, creare o aggiornare l'indicizzatore hello con hello seguente configurazione:

    {
      ... other indexer definition properties
     "parameters" : {
            "configuration" : { "queryTimeout" : "00:10:00" } }
    }

È anche possibile disabilitare hello `ORDER BY [High Water Mark Column]` clausola. Tuttavia, questa operazione è sconsigliata in quanto se l'esecuzione dell'indicizzatore hello è stato interrotto da un errore, indicizzatore hello ha toore processo tutte le righe se viene eseguito in un secondo momento, anche se l'indicizzatore hello è già elaborato quasi tutte le righe di hello tempo hello che è stata interrotta. hello toodisable `ORDER BY` clausola, utilizzo hello `disableOrderByHighWaterMarkColumn` impostazione nella definizione di indicizzatore hello:  

    {
     ... other indexer definition properties
     "parameters" : {
            "configuration" : { "disableOrderByHighWaterMarkColumn" : true } }
    }

### <a name="soft-delete-column-deletion-detection-policy"></a>Criteri di rilevamento eliminazione colonna di eliminazione temporanea
Quando le righe vengono eliminate dalla tabella di origine hello, si vorranno toodelete le righe dall'indice di ricerca hello anche. Se si utilizza SQL hello integrato criteri di rilevamento modifiche, questa viene preso in considerazione per l'utente. Tuttavia, criteri di rilevamento modifiche di limite massimo di hello non risultano utili con le righe eliminate. Quali toodo?

Se le righe di hello vengono fisicamente rimosse dalla tabella hello, ricerca di Azure è presente hello tooinfer modo di record che non esistono più.  Tuttavia, è possibile utilizzare eliminare righe di hello "soft-Elimina" tecnica toologically senza rimuoverli dalla tabella hello. Aggiungere una colonna tooyour tabella o vista e contrassegna le righe come eliminato utilizzando tale colonna.

Quando si utilizza una tecnica di soft-eliminazione hello, è possibile specificare i criteri di eliminazione temporanea hello come indicato di seguito durante la creazione o aggiornamento origine dati hello:

    {
        …,
        "dataDeletionDetectionPolicy" : {
           "@odata.type" : "#Microsoft.Azure.Search.SoftDeleteColumnDeletionDetectionPolicy",
           "softDeleteColumnName" : "[a column name]",
           "softDeleteMarkerValue" : "[hello value that indicates that a row is deleted]"
        }
    }

Hello **softDeleteMarkerValue** deve essere una stringa, utilizzare la rappresentazione di stringa hello tra il valore effettivo. Ad esempio, se si dispone di una colonna di tipo integer in cui le righe eliminate sono contrassegnate con il valore di hello 1, utilizzare `"1"`. Se si dispone di una colonna BIT in cui le righe eliminate sono contrassegnate con valore booleano true hello, utilizzare `"True"`.

<a name="TypeMapping"></a>

## <a name="mapping-between-sql-and-azure-search-data-types"></a>Mapping tra tipi di dati SQL e tipi di dati di Ricerca di Azure
| Tipo di dati SQL | Tipi di campi dell'indice di destinazione consentiti | Note |
| --- | --- | --- |
| bit |Edm.Boolean, Edm.String | |
| int, smallint, tinyint |Edm.Int32, Edm.Int64, Edm.String | |
| bigint |Edm.Int64, Edm.String | |
| real, float |Edm.Double, Edm.String | |
| smallmoney, money decimal numeric |Edm.String |Ricerca di Azure non supporta la conversione di tipi decimali in Edm.Double, perché in tal caso si perderebbe la precisione |
| char, nchar, varchar, nvarchar |Edm.String<br/>Collection(Edm.String) |Una stringa SQL può essere utilizzato toopopulate un campo Collection se la stringa hello rappresenta una matrice JSON di stringhe:`["red", "white", "blue"]` |
| smalldatetime, datetime, datetime2, date, datetimeoffset |Edm.DateTimeOffset, Edm.String | |
| uniqueidentifer |Edm.String | |
| geography |Edm.GeographyPoint |Sono supportate solo le istanze geografiche di tipo POINT con SRID 4326 (ovvero hello (impostazione predefinita) |
| rowversion |N/D |Colonne di versione di riga non possono essere archiviate nell'indice di ricerca hello, ma possono essere utilizzati per il rilevamento delle modifiche |
| time, timespan, binary, varbinary, image, xml, geometry, CLR types |N/D |Non supportate |

## <a name="configuration-settings"></a>Impostazioni di configurazione
L'indicizzatore SQL espone diverse impostazioni di configurazione:

| Impostazione | Tipo di dati | Scopo | Valore predefinito |
| --- | --- | --- | --- |
| queryTimeout |string |Set di hello timeout per l'esecuzione di query SQL |5 minuti ("00:05:00") |
| disableOrderByHighWaterMarkColumn |bool |Provoca hello della query SQL utilizzata da hello limite massimo criteri tooomit hello clausola ORDER BY. Vedere [Criteri di limite massimo](#HighWaterMarkPolicy) |false |

Queste impostazioni vengono utilizzate in hello `parameters.configuration` oggetto nella definizione di indicizzatore hello. Ad esempio, tooset hello query timeout too10 in minuti, creare o aggiornare l'indicizzatore hello con hello seguente configurazione:

    {
      ... other indexer definition properties
     "parameters" : {
            "configuration" : { "queryTimeout" : "00:10:00" } }
    }

## <a name="faq"></a>domande frequenti

**D: Posso usare l'indicizzatore di Azure SQL con i database SQL in esecuzione sulle macchine virtuali IaaS in Azure?**

Sì. Tuttavia, è necessario tooallow il database di ricerca servizio tooconnect tooyour. Per ulteriori informazioni, vedere [configurare una connessione da un tooSQL indicizzatore di ricerca di Azure Server in una macchina virtuale Azure](search-howto-connecting-azure-sql-iaas-to-azure-search-using-indexers.md).

**D: Posso usare l'indicizzatore di Azure SQL con i database SQL in esecuzione locale?**

Non direttamente. Non si consiglia o supportare una connessione diretta, tale operazione richiederebbe si tooopen il traffico tooInternet database. I clienti hanno avuto esito positivo in questo scenario grazie all'uso delle tecnologie bridge come Azure Data Factory. Per ulteriori informazioni, vedere [Push indice di ricerca di Azure tooan dati usando Azure Data Factory](https://docs.microsoft.com/azure/data-factory/data-factory-azure-search-connector).

**D: Posso usare l'indicizzatore di Azure SQL con database diversi da SQL Server in esecuzione in IaaS in Azure?**

No. Questo scenario, non è supportato perché non è stato verificato indicizzatore hello con alcun database diverso da SQL Server.  

**D: Posso creare più indicizzatori in esecuzione in una pianificazione?**

Sì. Tuttavia, è possibile eseguire un solo indicizzatore per volta in un nodo. Se è necessario più indicizzatori in esecuzione contemporaneamente, prendere in considerazione la scalabilità verticale del toomore servizio di ricerca di un'unità di ricerca.

**D: L’esecuzione di un indicizzatore influisce sul carico di lavoro della query?**

Sì. Esecuzioni dell'indicizzatore su uno dei nodi di hello nel servizio di ricerca e le risorse di tale nodo vengono condivise tra l'indicizzazione e serve il traffico di query e le altre richieste API. Se si eseguono un'indicizzazione e carichi di lavoro di query intensivi e si verifica una frequenza elevata di errori 503 o un aumento dei tempi di risposta, considerare il [ridimensionamento del servizio di ricerca](search-capacity-planning.md).

**D: Posso usare una replica secondaria in un [cluster di failover](https://docs.microsoft.com/azure/sql-database/sql-database-geo-replication-overview) come origine dati?**

Dipende. Per l'indicizzazione completa di una tabella o vista, è possibile usare una replica secondaria. 

Per l'indicizzazione incrementale, Ricerca di Azure supporta due criteri di rilevamento delle modifiche: il rilevamento delle modifiche integrato di SQL e il livello più alto.

Nelle repliche di sola lettura il database SQL non supporta il rilevamento delle modifiche integrato. Pertanto, è necessario usare il criterio del livello più alto. 

L'indicazione standard è tipo di dati rowversion hello toouse per la colonna di hello limite massimo. Tuttavia, l'uso di rowversion si basa sulla funzione `MIN_ACTIVE_ROWVERSION` del Database SQL, che non è supportata nelle repliche di sola lettura. Pertanto, deve puntare replica primaria di hello indicizzatore tooa se si utilizza rowversion.

Se si tenta di rowversion toouse su una replica di sola lettura, verrà visualizzato il seguente errore hello: 

    "Using a rowversion column for change tracking is not supported on secondary (read-only) availability replicas. Please update hello datasource and specify a connection toohello primary availability replica.Current database 'Updateability' property is 'READ_ONLY'".

**D: Posso usare una colonna diversa, non rowversion, per il rilevamento delle modifiche del livello più alto?**

Non è consigliabile. Solo **rowversion** consente una sincronizzazione dei dati affidabile. Tuttavia, a seconda della logica dell'applicazione, potrebbe essere sicuro:

+ È possibile assicurarsi che, durante l'esecuzione dell'indicizzatore hello, non sono presenti transazioni in sospeso nella tabella hello che si sta indicizzando (ad esempio, tutti gli aggiornamenti di tabella come un batch eseguito una pianificazione e pianificazione dell'indicizzatore di ricerca di Azure hello è impostato tooavoid sovrapposti con tabella hello pianificazione di aggiornamento).  

+ Eseguire periodicamente un toopick reindicizzazione completa di tutte le righe mancanti. 
