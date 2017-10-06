---
title: aaaSQL le metriche di query per l'API DocumentDB DB Cosmos Azure | Documenti Microsoft
description: "Informazioni sulla modalità debug e tooinstrument hello le prestazioni delle query SQL di Azure Cosmos DB richieste."
keywords: sintassi sql, query sql, linguaggio di query json, concetti relativi ai database e query sql, funzioni di aggregazione
services: cosmos-db
documentationcenter: 
author: arramac
manager: jhubbard
editor: monicar
ms.assetid: b2fa8e8f-7291-45a3-9bd1-7284ed9077f8
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: arramac
ms.openlocfilehash: 2fee3786b7d48d254162699471943e316764b003
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tuning-query-performance-with-azure-cosmos-db"></a>Ottimizzazione delle prestazioni delle query con Azure Cosmos DB
Azure Cosmos DB fornisce un'[API SQL per le query sui dati](documentdb-sql-query.md), senza che siano necessari schemi o indici secondari. Questo articolo fornisce le seguenti informazioni per gli sviluppatori hello:

* Informazioni generali sull'esecuzione delle query SQL di Azure Cosmos DB
* Dettagli sulle intestazioni di richiesta e risposta delle query e le opzioni SDK client
* Suggerimenti e procedure consigliate per le prestazioni delle query
* Esempi di come tooutilize SQL esecuzione statistiche toodebug le prestazioni delle query

## <a name="about-sql-query-execution"></a>Informazioni sull'esecuzione di query SQL

In Azure Cosmos DB, vengono archiviati i dati in contenitori, che possono raggiungere dimensioni tooany [velocità effettiva di archiviazione dimensioni o richiesta](partition-data.md). Azure DB Cosmos scala facilmente dati tra partizioni fisiche in crescita dei dati toohandle copre hello o aumento della velocità effettiva di provisioning. È possibile emettere contenitore tooany di query SQL utilizzando hello API REST o uno dei hello supportato [SDK di DocumentDB](documentdb-sdk-dotnet.md).

Una breve panoramica del partizionamento: si definisce una chiave di partizione come "city", che determina il modo in cui vengono suddivisi i dati tra le partizioni fisiche. Chiave singola partizione di dati appartenente tooa (ad esempio, "city" = = "Seattle") vengono archiviati all'interno di una partizione fisica, ma in genere una singola partizione fisica dispone di più chiavi di partizione. Quando una partizione raggiunge la dimensione di archiviazione, hello servizio facilmente suddivide partizione hello in due nuove partizioni e divide la chiave di partizione hello in modo uniforme tra queste partizioni. Poiché le partizioni sono temporanee, hello API utilizzano un'astrazione di una "chiave intervallo di partizione", che indica gli intervalli hello degli hash di chiave di partizione. 

Quando si esegue un tooAzure query DB Cosmos, hello SDK consente di eseguire questi passaggi logici:

* Analizzare il piano di esecuzione di hello SQL query toodetermine hello query. 
* Se la query hello include un filtro con la chiave di partizione hello, ad esempio `SELECT * FROM c WHERE c.city = "Seattle"`, è indirizzato tooa singola partizione. Se query hello non dispone di un filtro sulla chiave di partizione, quindi viene eseguita in tutte le partizioni e risultati vengono uniti lato client.
* query Hello viene eseguito all'interno di ogni partizione in serie o parallela, in base alla configurazione di client. All'interno di ogni partizione, query hello potrebbe rendere uno o più round trip, a seconda della complessità della query hello, configurare dimensioni di pagina e il provisioning di velocità effettiva della raccolta hello. Ogni esecuzione restituisce il numero di hello di [unità richieste](request-units.md) utilizzati dall'esecuzione di query e, facoltativamente, le statistiche di esecuzione di query. 
* Hello SDK esegue un riepilogo dei risultati di query hello tra partizioni. Ad esempio, se tra partizioni, query di hello implica una clausola ORDER BY, risultati dalle singole partizioni sono ordinati merge tooreturn risultati in base all'ordinamento a livello globale. Se la query hello è un'aggregazione come `COUNT`, i conteggi di hello da singole partizioni vengono sommati tooproduce hello conteggio complessivo.

SDK di Hello offrono diverse opzioni per l'esecuzione di query. Ad esempio, in .NET queste opzioni sono disponibili in hello `FeedOptions` classe. Hello nella tabella seguente vengono descritte queste opzioni e l'impatto il tempo di esecuzione di query. 

| Opzione | Descrizione |
| ------ | ----------- |
| `EnableCrossPartitionQuery` | È necessario impostare tootrue per le query che richiede toobe eseguita per più di una partizione. Si tratta di un tooenable flag esplicita è compromessi tra prestazioni tenendo toomake durante la fase di sviluppo. |
| `EnableScanInQuery` | Deve essere impostato tootrue se è stata esplicitamente rifiutata l'indicizzazione, ma desidera comunque query hello toorun tramite un'analisi. Applicabile solo se l'indicizzazione per hello richieste solo percorso di filtro è disabilitato. | 
| `MaxItemCount` | numero massimo di Hello di tooreturn elementi per ogni server toohello di andata e ritorno. Tramite l'impostazione troppo-1, è possibile consentire server hello gestire hello numero di elementi. In alternativa, è possibile ridurre questo tooretrieve valore solo un piccolo numero di elementi per ogni round trip. 
| `MaxBufferedItemCount` | Questa è un'opzione sul lato client e utilizzata il consumo di memoria hello toolimit quando si esegue tra partizioni ORDER BY. Un valore più alto consente di ridurre la latenza di hello di ordinamento tra partizioni. |
| `MaxDegreeOfParallelism` | Ottiene o imposta il numero di hello di operazioni simultanee eseguite sul lato client durante l'esecuzione di query parallele nel servizio di database Azure DocumentDB hello. Un valore di proprietà positivo limita hello valore del numero di operazioni simultanee toohello set. Se è impostato tooless a 0, il sistema di hello decide automaticamente il numero di hello di toorun operazioni simultanee. |
| `PopulateQueryMetrics` | Consente la registrazione dettagliata delle statistiche sul tempo impiegato nelle varie fasi di esecuzione della query, come il tempo di compilazione, il tempo del ciclo di indice e il tempo di caricamento dei documenti. È possibile condividere l'output di statistiche sulle query con problemi di prestazioni delle query di supporto tecnico di Azure toodiagnose. |
| `RequestContinuation` | È possibile riprendere l'esecuzione di query passando il token di continuazione opaco hello restituito da una query. token di continuazione Hello incapsula tutti gli stati necessari per l'esecuzione di query. |
| `ResponseContinuationTokenLimitInKb` | È possibile limitare dimensioni massime di hello hello del token di continuazione restituito dal server hello. Potrebbe essere necessario tooset questo se l'applicazione disponga di limiti alle dimensioni dell'intestazione di risposta. Impostando questa opzione può aumentare hello RUs usato per le query hello e durata globali.  |

Prendiamo ad esempio, un esempio di query su richiesta in una raccolta con la chiave di partizione `/city` come partizione di hello chiave e viene eseguito il provisioning con 100.000 UR/sec velocità effettiva. Richiesta la query usando `CreateDocumentQuery<T>` in .NET hello seguente:

```cs
IDocumentQuery<dynamic> query = client.CreateDocumentQuery(
    UriFactory.CreateDocumentCollectionUri(DatabaseName, CollectionName), 
    "SELECT * FROM c WHERE c.city = 'Seattle'", 
    new FeedOptions 
    { 
        PopulateQueryMetrics = true, 
        MaxItemCount = -1, 
        MaxDegreeOfParallelism = -1, 
        EnableCrossPartitionQuery = true 
    }).AsDocumentQuery();

FeedResponse<dynamic> result = await query.ExecuteNextAsync();
```

Hello frammento SDK illustrato sopra, corrisponde a toohello seguente richiesta di API REST:

```
POST https://arramacquerymetrics-westus.documents.azure.com/dbs/db/colls/sample/docs HTTP/1.1
x-ms-continuation: 
x-ms-documentdb-isquery: True
x-ms-max-item-count: -1
x-ms-documentdb-query-enablecrosspartition: True
x-ms-documentdb-query-parallelizecrosspartitionquery: True
x-ms-documentdb-query-iscontinuationexpected: True
x-ms-documentdb-populatequerymetrics: True
x-ms-date: Tue, 27 Jun 2017 21:52:18 GMT
authorization: type%3dmaster%26ver%3d1.0%26sig%3drp1Hi83Y8aVV5V6LzZ6xhtQVXRAMz0WNMnUuvriUv%2b4%3d
x-ms-session-token: 7:8,6:2008,5:8,4:2008,3:8,2:2008,1:8,0:8,9:8,8:4008
Cache-Control: no-cache
x-ms-consistency-level: Session
User-Agent: documentdb-dotnet-sdk/1.14.1 Host/32-bit MicrosoftWindowsNT/6.2.9200.0
x-ms-version: 2017-02-22
Accept: application/json
Content-Type: application/query+json
Host: arramacquerymetrics-westus.documents.azure.com
Content-Length: 52
Expect: 100-continue

{"query":"SELECT * FROM c WHERE c.city = 'Seattle'"}
```

Ogni pagina di esecuzione della query corrisponde tooa API REST `POST` con hello `Accept: application/query+json` intestazione e query SQL hello nel corpo di hello. Ogni query rende uno o più server toohello trip con hello di arrotondamento `x-ms-continuation` token restituite tra l'esecuzione di tooresume hello client e server. opzioni di configurazione Hello FeedOptions vengono passate toohello server sotto forma di hello di intestazioni di richiesta. Ad esempio, `MaxItemCount` corrisponde troppo`x-ms-max-item-count`. 

richiesta Hello restituisce seguente hello (troncati per migliorare la leggibilità) risposta:

```
HTTP/1.1 200 Ok
Cache-Control: no-store, no-cache
Pragma: no-cache
Transfer-Encoding: chunked
Content-Type: application/json
Server: Microsoft-HTTPAPI/2.0
Strict-Transport-Security: max-age=31536000
x-ms-last-state-change-utc: Tue, 27 Jun 2017 21:01:57.561 GMT
x-ms-resource-quota: documentSize=10240;documentsSize=10485760;documentsCount=-1;collectionSize=10485760;
x-ms-resource-usage: documentSize=1;documentsSize=884;documentsCount=2000;collectionSize=1408;
x-ms-item-count: 2000
x-ms-schemaversion: 1.3
x-ms-alt-content-path: dbs/db/colls/sample
x-ms-content-path: +9kEANVq0wA=
x-ms-xp-role: 1
x-ms-documentdb-query-metrics: totalExecutionTimeInMs=33.67;queryCompileTimeInMs=0.06;queryLogicalPlanBuildTimeInMs=0.02;queryPhysicalPlanBuildTimeInMs=0.10;queryOptimizationTimeInMs=0.00;VMExecutionTimeInMs=32.56;indexLookupTimeInMs=0.36;documentLoadTimeInMs=9.58;systemFunctionExecuteTimeInMs=0.00;userFunctionExecuteTimeInMs=0.00;retrievedDocumentCount=2000;retrievedDocumentSize=1125600;outputDocumentCount=2000;writeOutputTimeInMs=18.10;indexUtilizationRatio=1.00
x-ms-request-charge: 604.42
x-ms-serviceversion: version=1.14.34.4
x-ms-activity-id: 0df8b5f6-83b9-4493-abda-cce6d0f91486
x-ms-session-token: 2:2008
x-ms-gatewayversion: version=1.14.33.2
Date: Tue, 27 Jun 2017 21:59:49 GMT
```

intestazioni di risposta chiave Hello restituite dalla query hello includono hello informazioni seguenti:

| Opzione | Descrizione |
| ------ | ----------- |
| `x-ms-item-count` | numero di Hello di elementi restituiti nella risposta hello. Questo dipende hello fornito `x-ms-max-item-count`, hello numero di elementi che è possibile adattare all'interno di hello dimensioni massime del payload della risposta, velocità effettiva di provisioning hello e il tempo di esecuzione di query. |  
| `x-ms-continuation:` | Hello continuazione token tooresume l'esecuzione di query hello, se sono disponibili altri risultati. | 
| `x-ms-documentdb-query-metrics` | statistiche sulle query Hello per l'esecuzione di hello. Si tratta di una stringa delimitata contenente le statistiche di tempo impiegato in hello diverse fasi di esecuzione di query. Restituito se `x-ms-documentdb-populatequerymetrics` è troppo`True`. | 
| `x-ms-request-charge` | numero di Hello [unità richieste](request-units.md) utilizzati da query hello. | 

Per informazioni dettagliate sulle opzioni e le intestazioni di richiesta di hello API REST, vedere [una query di risorse utilizzando l'API REST di DocumentDB hello](https://docs.microsoft.com/rest/api/documentdb/querying-documentdb-resources-using-the-rest-api).

## <a name="best-practices-for-query-performance"></a>Procedure consigliate per le prestazioni delle query
di seguito Hello sono fattori più comuni di hello che influiscono sulle prestazioni di query di database di Azure Cosmos. In questo articolo verrà esaminato in modo approfondito ognuno di questi argomenti.

| Fattore | Suggerimento | 
| ------ | -----| 
| Velocità effettiva con provisioning | Misurare RU per ogni query e assicurarsi di disporre di velocità effettiva di provisioning obbligatorio hello per le query. | 
| Partizionamento e chiavi di partizione | Ottimizza per le query con valore della chiave di partizione hello nella clausola di filtro hello per una latenza bassa. |
| Opzioni per SDK e query | Seguire le procedure consigliate dell'SDK come la connettività diretta e ottimizzare le opzioni di esecuzione delle query sul lato client. |
| Latenza di rete | Account per la rete overhead in misura e utilizzare multihosting tooread API da hello più vicino di area. |
| Criterio di indicizzazione | Assicurarsi di aver richiesto hello percorsi/criteri di indicizzazione per query hello. |
| Metriche di esecuzione delle query | Analizzare hello query esecuzione metriche tooidentify potenziale di riscrivere più volte le forme di dati e query.  |

### <a name="provisioned-throughput"></a>Velocità effettiva con provisioning
In Cosmos DB è possibile creare contenitori di dati, ognuno con una velocità effettiva riservata espressa in unità richiesta (UR) al secondo. Una lettura di un documento di 1 KB è 1 UR e ogni operazione (incluse le query) è normalizzato tooa numero fisso di destinatari in base a sua complessità. Se ad esempio è previsto un provisioning di 1000 UR/sec per il contenitore e si dispone di una query come `SELECT * FROM c WHERE c.city = 'Seattle'` che usa 5 UR, è possibile eseguire (1000 UR/sec) / (5 UR/query) = 200 query di questo tipo al secondo. 

Se si invia più di 200 query/sec, hello avviato limitazione di velocità di richieste in ingresso di sopra di 200/s. Hello SDK gestiscono automaticamente questo caso eseguendo un tentativi/backoff, pertanto è possibile riscontrare una latenza più elevata per le query. Aumento hello il provisioning della velocità effettiva toohello necessario valore migliora la velocità effettiva e la latenza delle query. 

toolearn più sulle unità di richiesta, vedere [unità richieste](request-units.md).

### <a name="partitioning-and-partition-keys"></a>Partizionamento e chiavi di partizione
Con Azure Cosmos DB, in genere le query eseguire in ordine da più veloce o più efficiente tooslower/meno efficiente hello. 

* GET su una singola chiave di partizione e chiave di elemento
* Query con una clausola di filtro su una singola chiave di partizione
* Query senza una clausola di filtro di uguaglianza o basato su intervallo su qualsiasi proprietà
* Query senza filtri

Esegue una query che tooconsult necessità tutte le partizioni è necessario una latenza maggiore e sarà possibile utilizzare RUs superiore. Poiché ogni partizione ha l'indicizzazione automatica in tutte le proprietà, query hello può essere fornita in modo efficiente tra l'indice di hello in questo caso. È possibile apportare le query che interessano più veloce di partizioni utilizzando le opzioni di parallelismo hello.

toolearn informazioni sulle partizioni e le chiavi di partizione, vedere [partizionamento nel database di Azure Cosmos](partition-data.md).

### <a name="sdk-and-query-options"></a>Opzioni per SDK e query
Vedere [suggerimenti sulle prestazioni](performance-tips.md) e [test delle prestazioni](performance-testing.md) per la modalità tooget hello migliori prestazioni lato client dal database di Azure Cosmos. Incluso l'utilizzo di hello SDK più recente, impostazione delle configurazioni specifiche della piattaforma come numero predefinito di connessioni, frequenza di garbage collection e come utilizzare opzioni di connettività semplice come Direct/TCP. 


#### <a name="max-item-count"></a>Numero massimo di elementi
Per le query, hello valore `MaxItemCount` può avere un impatto significativo sul tempo di query end-to-end. Ogni round trip toohello viene restituito non più di numero hello di elementi in `MaxItemCount` (valore predefinito è 100 elementi). Impostazione del valore maggiore di tooa (-1 è consigliato e massima) migliorerà la durata delle query complessiva, limitando il numero di hello di round trip tra server e client, in particolare per le query con il set di risultati di grandi dimensioni.

```cs
IDocumentQuery<dynamic> query = client.CreateDocumentQuery(
    UriFactory.CreateDocumentCollectionUri(DatabaseName, CollectionName), 
    "SELECT * FROM c WHERE c.city = 'Seattle'", 
    new FeedOptions 
    { 
        MaxItemCount = -1, 
    }).AsDocumentQuery();
```

#### <a name="max-degree-of-parallelism"></a>Massimo grado di parallelismo
Per le query, ottimizzare hello `MaxDegreeOfParallelism` le configurazioni hello tooidentify per l'applicazione, soprattutto se l'esecuzione di query tra partizioni (senza un filtro sul valore della chiave di partizione hello). `MaxDegreeOfParallelism`Controlla hello numero massimo di attività in parallelo, ad esempio, hello massimo toobe partizioni visitato in parallelo. 

```cs
IDocumentQuery<dynamic> query = client.CreateDocumentQuery(
    UriFactory.CreateDocumentCollectionUri(DatabaseName, CollectionName), 
    "SELECT * FROM c WHERE c.city = 'Seattle'", 
    new FeedOptions 
    { 
        MaxDegreeOfParallelism = -1, 
        EnableCrossPartitionQuery = true 
    }).AsDocumentQuery();
```

Presupponendo che
* D = numero massimo predefinito di attività in parallelo (= numero totale di processori nel computer client hello)
* P = Numero massimo di attività in parallelo specificato dall'utente
* N = numero di partizioni che deve toobe visitato per la risposta a una query

Di seguito sono le implicazioni di comportamento query parallele hello per diversi valori di P.
* (P == 0) => Modalità seriale
* (P == 1) => Massimo un'attività
* (P > 1) => Attività in parallelo minime (P, N) 
* (P < 1) => Attività in parallelo minime (N, D)

Per le note sulla versione degli SDK e altre informazioni sulle classi e i metodi implementati, vedere [SDK di DocumentDB](documentdb-sdk-dotnet.md)

### <a name="network-latency"></a>Latenza di rete
Vedere [distribuzione globale di Azure Cosmos DB](tutorial-global-distribution-documentdb.md) tooset distribuzione globale di backup, e collegare l'area più vicina toohello. Latenza di rete ha un impatto significativo sulle prestazioni delle query quando è necessario toomake più round trip o recuperare un grande set di risultati di query hello. 

Hello sezione sulle metriche di esecuzione di query viene illustrato come tooretrieve hello server tempo di esecuzione di query ( `totalExecutionTimeInMs`), in modo che è possibile distinguere tra tempo impiegato per l'esecuzione di query e il tempo impiegato per il trasferimento di rete.

### <a name="indexing-policy"></a>Criterio di indicizzazione
Per informazioni su percorsi, tipi e modalità di indicizzazione e sul relativo impatto sull'esecuzione delle query, vedere [Configurazione dei criteri di indicizzazione](indexing-policies.md). Per impostazione predefinita, hello criteri di indicizzazione utilizza Hash l'indicizzazione per le stringhe, che è efficace per le query di uguaglianza, ma non per le query di intervallo/ordine dalle query. Se è necessario le query di intervallo per le stringhe, è consigliabile specificare il tipo di indice di intervallo per tutte le stringhe di hello. 

## <a name="query-execution-metrics"></a>Metriche di esecuzione delle query
È possibile ottenere le metriche dettagliate sull'esecuzione di query passando hello facoltativo `x-ms-documentdb-populatequerymetrics` intestazione (`FeedOptions.PopulateQueryMetrics` in hello .NET SDK). valore restituito in Hello `x-ms-documentdb-query-metrics` ha hello seguenti coppie chiave-valore per risoluzione dell'esecuzione di query avanzata. 

```cs
IDocumentQuery<dynamic> query = client.CreateDocumentQuery(
    UriFactory.CreateDocumentCollectionUri(DatabaseName, CollectionName), 
    "SELECT * FROM c WHERE c.city = 'Seattle'", 
    new FeedOptions 
    { 
        PopulateQueryMetrics = true, 
    }).AsDocumentQuery();

FeedResponse<dynamic> result = await query.ExecuteNextAsync();

// Returns metrics by partition key range Id
IReadOnlyDictionary<string, QueryMetrics> metrics = result.QueryMetrics;

```

| Metrica | Unità | Descrizione | 
| ------ | -----| ----------- |
| `totalExecutionTimeInMs` | millisecondi | Tempo di esecuzione della query | 
| `queryCompileTimeInMs` | millisecondi | Tempo di compilazione della query  | 
| `queryLogicalPlanBuildTimeInMs` | millisecondi | Piano di query logica toobuild ora | 
| `queryPhysicalPlanBuildTimeInMs` | millisecondi | Piano di query fisiche toobuild ora | 
| `queryOptimizationTimeInMs` | millisecondi | Tempo impiegato per l'ottimizzazione della query | 
| `VMExecutionTimeInMs` | millisecondi | Tempo impiegato per l'esecuzione della query | 
| `indexLookupTimeInMs` | millisecondi | Tempo impiegato nel livello di indice fisico | 
| `documentLoadTimeInMs` | millisecondi | Tempo impiegato per il caricamento di documenti  | 
| `systemFunctionExecuteTimeInMs` | millisecondi | Tempo totale impiegato per l'esecuzione di funzioni di sistema (predefinite) in millisecondi  | 
| `userFunctionExecuteTimeInMs` | millisecondi | Tempo totale impiegato per l'esecuzione di funzioni definite dall'utente in millisecondi | 
| `retrievedDocumentCount` | millisecondi | Numero totale di documenti recuperati  | 
| `retrievedDocumentSize` | byte | Dimensione totale dei documenti recuperati in byte  | 
| `outputDocumentCount` | count | Numero di documenti di output | 
| `writeOutputTimeInMs` | millisecondi | Tempo di esecuzione della query in millisecondi | 
| `indexUtilizationRatio` | rapporto (<=1) | Percentuale del numero di documenti corrispondente al numero di toohello hello filtro dei documenti caricati  | 

Hello client SDK possono internamente rendere più query tooserve hello query operazioni all'interno di ogni partizione. client Hello rende più di una chiamata per ogni singola partizione se superano i risultati totali hello `x-ms-max-item-count`, se query hello maggiore velocità effettiva di provisioning hello per partizione hello, o se hello payload query raggiunge dimensioni massime di hello per pagina se hello query raggiunge hello sistema allocata limite di timeout. Ogni esecuzione parziale della query restituisce un `x-ms-documentdb-query-metrics` per la pagina. 

Ecco alcune query di esempio e in che modo toointerpret alcune metriche hello restituiti dall'esecuzione di query: 

| Query | Metrica di esempio | Descrizione | 
| ------ | -----| ----------- |
| `SELECT TOP 100 * FROM c` | `"RetrievedDocumentCount": 101` | Hello numero di documenti recuperati è 100 + la clausola TOP 1 toomatch hello. Il tempo della query viene impiegato per lo più in `WriteOutputTime` e `DocumentLoadTime` poiché si tratta di un'analisi. | 
| `SELECT TOP 500 * FROM c` | `"RetrievedDocumentCount": 501` | RetrievedDocumentCount è superiore (500 + 1 toomatch hello clausola TOP). | 
| `SELECT * FROM c WHERE c.N = 55` | `"IndexLookupTime": "00:00:00.0009500"` | Vengono impiegati circa 0,9 ms in IndexLookupTime per la ricerca della chiave, perché viene eseguita una ricerca nell'indice `/N/?`. | 
| `SELECT * FROM c WHERE c.N > 55` | `"IndexLookupTime": "00:00:00.0017700"` | Un tempo leggermente superiore (1,7 ms) viene impiegato per IndexLookupTime nel caso di un'analisi dell'intervallo, perché viene eseguita una ricerca nell'indice `/N/?`. | 
| `SELECT TOP 500 c.N FROM c` | `"IndexLookupTime": "00:00:00.0017700"` | Il tempo trascorso in `DocumentLoadTime` è lo stesso delle query precedenti, ma con un valore `WriteOutputTime` inferiore perché viene eseguita la proiezione di una sola proprietà. | 
| `SELECT TOP 500 udf.toPercent(c.N) FROM c` | `"UserDefinedFunctionExecutionTime": "00:00:00.2136500"` | Viene impiegato per circa 213 ms `UserDefinedFunctionExecutionTime` esecuzione hello funzione definita dall'utente su ogni valore di `c.N`. |
| `SELECT TOP 500 c.Name FROM c WHERE STARTSWITH(c.Name, 'Den')` | `"IndexLookupTime": "00:00:00.0006400", "SystemFunctionExecutionTime": "00:00:00.0074100"` | Vengono impiegati circa 0,6 ms in `IndexLookupTime` su `/Name/?`. La maggior parte delle hello query il tempo di esecuzione (ms ~ 7) in `SystemFunctionExecutionTime`. |
| `SELECT TOP 500 c.Name FROM c WHERE STARTSWITH(LOWER(c.Name), 'den')` | `"IndexLookupTime": "00:00:00", "RetrievedDocumentCount": 2491,  "OutputDocumentCount": 500` | La query viene eseguita come un'analisi perché usa `LOWER` e vengono restituiti 500 su 2491 documenti recuperati. |


## <a name="next-steps"></a>Passaggi successivi
* toolearn hello supportato gli operatori di query SQL sulle parole chiave, vedere [query SQL](documentdb-sql-query.md). 
* toolearn sulle unità di richiesta, vedere [unità richieste](request-units.md).
* toolearn sui criteri di indicizzazione, vedere [criteri di indicizzazione](indexing-policies.md) 


