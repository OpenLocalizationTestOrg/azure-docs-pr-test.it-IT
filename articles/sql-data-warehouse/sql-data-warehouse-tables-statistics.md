---
title: aaaManaging sulle statistiche delle tabelle in SQL Data Warehouse | Documenti Microsoft
description: Introduzione alle statistiche nelle tabelle di SQL Data Warehouse di Azure.
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: jhubbard
editor: 
ms.assetid: faa1034d-314c-4f9d-af81-f5a9aedf33e4
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: tables
ms.date: 10/31/2016
ms.author: shigu;barbkess
ms.openlocfilehash: c9521dc47891f68d124e77a53e2e15d03275caaa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="managing-statistics-on-tables-in-sql-data-warehouse"></a>Gestione delle statistiche nelle tabelle in SQL Data Warehouse
> [!div class="op_single_selector"]
> * [Panoramica][Overview]
> * [Tipi di dati][Data Types]
> * [Distribuzione][Distribute]
> * [Indice][Index]
> * [Partizione][Partition]
> * [Statistiche][Statistics]
> * [Temporanee][Temporary]
> 
> 

Hello ulteriori SQL Data Warehouse viene a conoscenza dei dati, hello più velocemente può eseguire query sui dati.  metodo Hello informare SQL Data Warehouse di dati, è la raccolta di statistiche sui dati.  Con le statistiche sui dati è una delle operazioni più importanti hello è possibile eseguire toooptimize le query.  Statistiche consentono a SQL Data Warehouse di creare il piano ottimale di hello per le query.  Questo avviene perché query optimizer basati su query di SQL Data Warehouse di hello query optimizer è un costo.  Vale a dire confronta il costo di hello dei diversi piani di query e quindi sceglie piano hello con costo più basso hello, che deve essere anche piano hello che eseguirà hello più veloce.

È possibile creare statistiche su una singola colonna, su più colonne o sull'indice di una tabella.  Le statistiche vengono archiviate in un istogramma che acquisisce intervallo hello e selettività dei valori.  Si tratta di particolare interesse quando query optimizer hello deve tooevaluate join, GROUP BY, HAVING che clausole WHERE in una query.  Ad esempio, se ottimizzatore di hello che data hello si filtrano nella query restituirà 1 riga, è possibile scegliere molto diversa rispetto a se in piano stime data è sono selezionata verrà restituito 1 milione di righe.  Durante la creazione di statistiche è estremamente importante, è ugualmente importante che le statistiche delle *accuratamente* rifletta hello lo stato corrente della tabella hello.  Presenza di statistiche aggiornate assicura che un piano adeguato è selezionato da query optimizer hello.  i piani di Hello creati da query optimizer hello sono solo efficace delle statistiche di hello sui dati.

il processo di Hello di creazione e aggiornamento delle statistiche è attualmente un processo manuale, ma è molto semplice toodo.  È diverso rispetto a SQL Server, che crea e aggiorna automaticamente le statistiche su singoli indici e colonne.  Utilizzando le informazioni di hello riportate di seguito, è possibile automatizzare notevolmente gestione hello delle statistiche di hello sui dati. 

## <a name="getting-started-with-statistics"></a>Introduzione alle statistiche
 Creare le statistiche campionate ogni colonna viene avviato tooget un modo semplice con le statistiche.  Poiché è ugualmente importante tookeep statistiche aggiornate, un approccio conservativo potrebbe essere tooupdate le statistiche di ogni giorno o dopo ogni carico. Sono sempre presenti compromessi tra prestazioni e hello costo toocreate e aggiornare le statistiche.  Se si ritiene che sta richiedendo troppo tempo toomaintain tutte le statistiche, è necessario frequenti toobe tootry più selettivo sulle statistiche dispongano quali colonne o le colonne di aggiornamento.  Ad esempio, potrebbe desiderato colonne data tooupdate ogni giorno, come è possibile aggiungere nuovi valori anziché dopo ogni carico. Nuovamente, sarà possibile ottenere hello migliori con le statistiche su colonne coinvolte nel join, GROUP BY, HAVING che clausole WHERE.  Se si dispone di una tabella con molte clausola SELECT le colonne che vengono utilizzate solo in hello, statistiche su queste colonne potrebbero non aiutare e un po' più tooidentify di impegno di spesa solo le colonne hello consentono in cui le statistiche, può ridurre hello ora toomaintain le statistiche .

## <a name="multi-column-statistics"></a>Statistiche a più colonne
Inoltre toocreating le statistiche per colonne singole, è possibile che le query trarranno vantaggio dalle statistiche su più colonne.  Le statistiche a più colonne sono statistiche create su un elenco di colonne.  Sono incluse le statistiche di colonna singola nella prima colonna hello nelle elenco hello e alcune informazioni di correlazione tra colonne chiamato densità.  Ad esempio, se si dispone di una tabella che unisce in join tooanother su due colonne, è possibile che SQL Data Warehouse ottimizzare piano hello se riconosce relazione hello tra due colonne.   Le statistiche a più colonne possono migliorare le prestazioni delle query per alcune operazioni, ad esempio nelle clausole JOIN composite e GROUP BY.

## <a name="updating-statistics"></a>Aggiornamento delle statistiche
L'aggiornamento delle statistiche è una parte importante della routine gestione del database.  Quando viene modificato distribuzione hello dei dati nel database di hello, le statistiche devono toobe aggiornato.  Le statistiche non aggiornate determinerà le prestazioni delle query toosub ottimale.

Una procedura consigliata è tooupdate statistiche su colonne di data e ogni giorno vengono aggiunte nuove date.  Le righe di nuovo ogni volta vengono caricati nel data warehouse di hello, vengono aggiunte nuove date di carico di transazione. Questi modificano hello distribuzione dei dati e apportare le statistiche di hello non aggiornato. Al contrario, le statistiche su una colonna per il paese in una tabella clienti potrebbero non essere necessario toobe aggiornato, come la distribuzione di hello di valori in genere non viene modificato. Supponendo che la distribuzione di hello è costante tra i clienti, aggiunta di nuovi variazione della tabella toohello righe non sarà toochange distribuzione dei dati hello. Tuttavia, se il data warehouse contiene solo un paese e importare dati da un nuovo paese, risultante in dati di più paesi è stati archiviati, è assolutamente necessario statistiche tooupdate sulla colonna country hello.

Uno dei hello prima domande tooask quando la risoluzione dei problemi di una query è "sono statistiche hello aggiornati?"

La domanda non è che è possibile rispondere in base all'età hello dei dati di hello. Un oggetto di statistiche aggiornato toodate potrebbe essere molto vecchio se non è stata eseguita alcuna toohello modifica sostanziale dati sottostanti. Quando hello numero di righe è stato modificato sostanzialmente o viene apportata una modifica della distribuzione di valori per una determinata colonna hello materiale *quindi* è tooupdate delle statistiche.  

Come riferimento, **SQL Server** (non SQL Data Warehouse) aggiorna automaticamente le statistiche nelle situazioni seguenti:

* Se si dispone di zero righe nella tabella di hello, quando si aggiungono righe, si otterrà un aggiornamento automatico delle statistiche
* Quando si aggiunta più di 500 tabella tooa di righe a partire da meno di 500 righe (ad esempio all'inizio aver 499 e aggiungere quindi 500 righe tooa totale 999 righe), si otterrà un aggiornamento automatico 
* Dopo aver oltre 500 righe è tooadd 500 righe aggiuntive + 20% delle dimensioni di hello della tabella hello prima sulla statistiche hello verrà visualizzato un aggiornamento automatico

Poiché non esiste alcun toodetermine DMV dati all'interno di tabella hello sono stato modificato dopo l'aggiornamento delle statistiche ora ultimo hello, conoscere l'età di hello delle statistiche può fornire una parte di immagine hello.  È possibile utilizzare hello seguente toodetermine hello ultima le statistiche di query in cui l'aggiornamento in ogni tabella.  

> [!NOTE]
> Tenere presente che se è presente una modifica sostanziale nella distribuzione hello di valori per una determinata colonna, è necessario aggiornare le statistiche indipendentemente dal hello ultima volta che sono state aggiornate.  
> 
> 

```sql
SELECT
    sm.[name] AS [schema_name],
    tb.[name] AS [table_name],
    co.[name] AS [stats_column_name],
    st.[name] AS [stats_name],
    STATS_DATE(st.[object_id],st.[stats_id]) AS [stats_last_updated_date]
FROM
    sys.objects ob
    JOIN sys.stats st
        ON  ob.[object_id] = st.[object_id]
    JOIN sys.stats_columns sc    
        ON  st.[stats_id] = sc.[stats_id]
        AND st.[object_id] = sc.[object_id]
    JOIN sys.columns co    
        ON  sc.[column_id] = co.[column_id]
        AND sc.[object_id] = co.[object_id]
    JOIN sys.types  ty    
        ON  co.[user_type_id] = ty.[user_type_id]
    JOIN sys.tables tb    
        ON  co.[object_id] = tb.[object_id]
    JOIN sys.schemas sm    
        ON  tb.[schema_id] = sm.[schema_id]
WHERE
    st.[user_created] = 1;
```

Le colonne data in un data warehouse, ad esempio, necessitano solitamente di aggiornamenti frequenti delle statistiche. Le righe di nuovo ogni volta vengono caricati nel data warehouse di hello, vengono aggiunte nuove date di carico di transazione. Questi modificano hello distribuzione dei dati e apportare le statistiche di hello non aggiornato.  Al contrario, le statistiche su una colonna relativa al sesso in una tabella clienti potrebbero non essere necessario toobe aggiornato. Supponendo che la distribuzione di hello è costante tra i clienti, aggiunta di nuovi variazione della tabella toohello righe non sarà toochange distribuzione dei dati hello. Tuttavia, se il data warehouse contiene solo un sesso e risultati di un nuovo requisito generano più i sessi è assolutamente necessario statistiche tooupdate nella colonna relativa al sesso hello.

Per altre informazioni, vedere [Statistiche][Statistics] in MSDN.

## <a name="implementing-statistics-management"></a>Implementazione della gestione delle statistiche
È spesso tooextend una buona idea dei dati durante il caricamento tooensure processo che le statistiche vengono aggiornate in hello fine del caricamento hello. caricamento dei dati Hello è quando le tabelle cambiano più frequentemente alle dimensioni e/o la distribuzione di valori. Pertanto, si tratta di un punto logico di tooimplement alcuni processi di gestione.

Alcuni principi sono riportate di seguito per aggiornare le statistiche durante il processo di caricamento hello:

* Assicurarsi che ogni tabella caricata includa almeno un oggetto statistiche aggiornato. Questo hello aggiornamenti tabelle informazioni sulle dimensioni (numero di riga e conteggio delle pagine) come parte dell'aggiornamento di statistiche hello.
* Concentrarsi sulle colonne incluse nelle clausole JOIN, GROUP BY, ORDER BY e DISTINCT.
* È consigliabile aggiornare le colonne "chiave ascending", ad esempio transazioni più frequentemente di questi valori non verranno inclusi nell'istogramma delle statistiche hello date,
* Prendere in considerazione una minore frequenza per l'aggiornamento delle colonne relative alla distribuzione statica.
* Occorre ricordare che ogni oggetto statistiche viene aggiornato in serie. La semplice implementazione di `UPDATE STATISTICS <TABLE_NAME>` potrebbe non essere ottimale, in particolare per tabelle di grandi dimensioni con molti oggetti statistici.

> [!NOTE]
> Per ulteriori informazioni su [crescente chiave] consultare il white paper del modello di stima della cardinalità toohello SQL Server 2014.
> 
> 

Per altre informazioni, vedere [Stima della cardinalità][Cardinality Estimation] in MSDN.

## <a name="examples-create-statistics"></a>Esempi: Creare le statistiche
Questi esempi mostrano come toouse varie opzioni per la creazione di statistiche. Opzioni Hello utilizzate per ogni colonna dipendono dalle caratteristiche hello dei dati e come colonna di hello verrà utilizzata nelle query.

### <a name="a-create-single-column-statistics-with-default-options"></a>R. Creare statistiche a colonna singola con opzioni predefinite
toocreate statistiche su una colonna, è sufficiente fornire un nome di oggetto statistiche hello e hello della colonna hello.

Questa sintassi utilizza tutte le opzioni predefinite di hello. Per impostazione predefinita, SQL Data Warehouse esempi il 20% della tabella hello durante la creazione di statistiche.

```sql
CREATE STATISTICS [statistics_name] ON [schema_name].[table_name]([column_name]);
```

ad esempio:

```sql
CREATE STATISTICS col1_stats ON dbo.table1 (col1);
```

### <a name="b-create-single-column-statistics-by-examining-every-row"></a>B. Creare statistiche a colonna singola esaminando ogni riga
frequenza di campionamento predefinita Hello del 20% è sufficiente per la maggior parte delle situazioni. Tuttavia, è possibile regolare la frequenza di campionamento hello.

hello toosample completo di tabella, utilizzare la seguente sintassi:

```sql
CREATE STATISTICS [statistics_name] ON [schema_name].[table_name]([column_name]) WITH FULLSCAN;
```

ad esempio:

```sql
CREATE STATISTICS col1_stats ON dbo.table1 (col1) WITH FULLSCAN;
```

### <a name="c-create-single-column-statistics-by-specifying-hello-sample-size"></a>C. Creare statistiche di colonna singola, specificando la dimensione del campione hello
In alternativa, è possibile specificare la dimensione del campione hello sotto forma di percentuale:

```sql
CREATE STATISTICS col1_stats ON dbo.table1 (col1) WITH SAMPLE = 50 PERCENT;
```

### <a name="d-create-single-column-statistics-on-only-some-of-hello-rows"></a>D. Creare statistiche di colonna singola su tutte le righe di hello
Un'altra opzione, è possibile creare statistiche in una parte di hello righe nella tabella. Questa opzione è definita statistica filtrata.

Ad esempio, è possibile utilizzare le statistiche filtrate quando si pianifica una partizione specifica di una tabella partizionata grande tooquery. Creando le statistiche su hello solo i valori della partizione, accuratezza hello di statistiche di hello migliorare e pertanto migliorare le prestazioni delle query.

Questo esempio crea statistiche su un intervallo di valori. Hello valori potrebbero facilmente essere definita dall'intervallo di hello toomatch di valori in una partizione.

```sql
CREATE STATISTICS stats_col1 ON table1(col1) WHERE col1 > '2000101' AND col1 < '20001231';
```

> [!NOTE]
> Per hello query optimizer tooconsider le statistiche filtrate quando viene scelto il piano di query distribuite di hello, query hello deve adattarsi all'interno di hello definizione di oggetto statistiche hello. Utilizzando l'esempio precedente di hello, hello della query in cui clausola deve toospecify col1 valori tra 2000101 e 20001231.
> 
> 

### <a name="e-create-single-column-statistics-with-all-hello-options"></a>E. Creare statistiche di colonna singola con tutte le opzioni di hello
Naturalmente, è possibile, combinare insieme le opzioni di hello. esempio Hello seguente crea un oggetto statistiche filtrate con una dimensione di esempio personalizzati:

```sql
CREATE STATISTICS stats_col1 ON table1 (col1) WHERE col1 > '2000101' AND col1 < '20001231' WITH SAMPLE = 50 PERCENT;
```

Per informazioni di riferimento complete hello, vedere [CREATE STATISTICS] [ CREATE STATISTICS] su MSDN.

### <a name="f-create-multi-column-statistics"></a>F. Creare statistiche a più colonne
semplicemente toocreate statistiche su più colonne, utilizzare hello precedenti esempi, ma specificare più colonne.

> [!NOTE]
> Istogramma Hello, che viene utilizzato tooestimate numero di righe nel risultato della query hello, è disponibile solo per hello prima colonna nella definizione di oggetto statistiche hello.
> 
> 

In questo esempio, istogramma hello è *prodotto\_categoria*. Le statistiche tra le colonne vengono calcolate su *product\_category* e *product\_sub_c\ategory*:

```sql
CREATE STATISTICS stats_2cols ON table1 (product_category, product_sub_category) WHERE product_category > '2000101' AND product_category < '20001231' WITH SAMPLE = 50 PERCENT;
```

Poiché non esiste una correlazione tra *prodotto\_categoria* e *prodotto\_sub\_categoria*, un stat a più colonne possono essere utili se queste colonne sono accessibili in hello contemporaneamente.

### <a name="g-create-statistics-on-all-hello-columns-in-a-table"></a>G. Creare statistiche per tutte le colonne di hello in una tabella
Statistiche toocreate unidirezionale sono tooissues i comandi CREATE STATISTICS dopo la creazione tabella hello.

```sql
CREATE TABLE dbo.table1
(
   col1 int
,  col2 int
,  col3 int
)
WITH
  (
    CLUSTERED COLUMNSTORE INDEX
  )
;

CREATE STATISTICS stats_col1 on dbo.table1 (col1);
CREATE STATISTICS stats_col2 on dbo.table2 (col2);
CREATE STATISTICS stats_col3 on dbo.table3 (col3);
```

### <a name="h-use-a-stored-procedure-toocreate-statistics-on-all-columns-in-a-database"></a>H. Utilizzare le statistiche toocreate una stored procedure per tutte le colonne in un database
SQL Data Warehouse non dispone di un equivalente di stored procedure di sistema troppo [sp_create_stats] [] in SQL Server. Questa stored procedure crea un oggetto statistiche di colonna singola per ogni colonna del database hello che non dispone già di statistiche.

Ciò permetterà di iniziare a progettare il database. È gratuito tooadapt è tooyour deve.

```sql
CREATE PROCEDURE    [dbo].[prc_sqldw_create_stats]
(   @create_type    tinyint -- 1 default 2 Fullscan 3 Sample
,   @sample_pct     tinyint
)
AS

IF @create_type NOT IN (1,2,3)
BEGIN
    THROW 151000,'Invalid value for @stats_type parameter. Valid range 1 (default), 2 (fullscan) or 3 (sample).',1;
END;

IF @sample_pct IS NULL
BEGIN;
    SET @sample_pct = 20;
END;

IF OBJECT_ID('tempdb..#stats_ddl') IS NOT NULL
BEGIN;
    DROP TABLE #stats_ddl;
END;

CREATE TABLE #stats_ddl
WITH    (   DISTRIBUTION    = HASH([seq_nmbr])
        ,   LOCATION        = USER_DB
        )
AS
WITH T
AS
(
SELECT      t.[name]                        AS [table_name]
,           s.[name]                        AS [table_schema_name]
,           c.[name]                        AS [column_name]
,           c.[column_id]                   AS [column_id]
,           t.[object_id]                   AS [object_id]
,           ROW_NUMBER()
            OVER(ORDER BY (SELECT NULL))    AS [seq_nmbr]
FROM        sys.[tables] t
JOIN        sys.[schemas] s         ON  t.[schema_id]       = s.[schema_id]
JOIN        sys.[columns] c         ON  t.[object_id]       = c.[object_id]
LEFT JOIN   sys.[stats_columns] l   ON  l.[object_id]       = c.[object_id]
                                    AND l.[column_id]       = c.[column_id]
                                    AND l.[stats_column_id] = 1
LEFT JOIN    sys.[external_tables] e    ON    e.[object_id]        = t.[object_id]
WHERE       l.[object_id] IS NULL
AND            e.[object_id] IS NULL -- not an external table
)
SELECT  [table_schema_name]
,       [table_name]
,       [column_name]
,       [column_id]
,       [object_id]
,       [seq_nmbr]
,       CASE @create_type
        WHEN 1
        THEN    CAST('CREATE STATISTICS '+QUOTENAME('stat_'+table_schema_name+ '_' + table_name + '_'+column_name)+' ON '+QUOTENAME(table_schema_name)+'.'+QUOTENAME(table_name)+'('+QUOTENAME(column_name)+')' AS VARCHAR(8000))
        WHEN 2
        THEN    CAST('CREATE STATISTICS '+QUOTENAME('stat_'+table_schema_name+ '_' + table_name + '_'+column_name)+' ON '+QUOTENAME(table_schema_name)+'.'+QUOTENAME(table_name)+'('+QUOTENAME(column_name)+') WITH FULLSCAN' AS VARCHAR(8000))
        WHEN 3
        THEN    CAST('CREATE STATISTICS '+QUOTENAME('stat_'+table_schema_name+ '_' + table_name + '_'+column_name)+' ON '+QUOTENAME(table_schema_name)+'.'+QUOTENAME(table_name)+'('+QUOTENAME(column_name)+') WITH SAMPLE '+@sample_pct+'PERCENT' AS VARCHAR(8000))
        END AS create_stat_ddl
FROM T
;

DECLARE @i INT              = 1
,       @t INT              = (SELECT COUNT(*) FROM #stats_ddl)
,       @s NVARCHAR(4000)   = N''
;

WHILE @i <= @t
BEGIN
    SET @s=(SELECT create_stat_ddl FROM #stats_ddl WHERE seq_nmbr = @i);

    PRINT @s
    EXEC sp_executesql @s
    SET @i+=1;
END

DROP TABLE #stats_ddl;
```

statistiche toocreate su tutte le colonne nella tabella hello con questa procedura, è sufficiente chiamare routine hello.

```sql
prc_sqldw_create_stats;
```

## <a name="examples-update-statistics"></a>Esempi: Aggiornare le statistiche
le statistiche tooupdate, è possibile:

1. Aggiornare un oggetto statistiche. Specificare il nome di hello dell'oggetto statistiche desiderato tooupdate hello.
2. Aggiornare tutti gli oggetti statistiche in una tabella. Specificare il nome di hello della tabella di hello anziché un oggetto statistiche specifico.

### <a name="a-update-one-specific-statistics-object"></a>R. Aggiornare un oggetto statistiche specifico
Utilizzare hello segue sintassi tooupdate un oggetto statistiche specifico:

```sql
UPDATE STATISTICS [schema_name].[table_name]([stat_name]);
```

ad esempio:

```sql
UPDATE STATISTICS [dbo].[table1] ([stats_col1]);
```

Dall'aggiornamento di statistiche specifici oggetti, è possibile ridurre le statistiche di toomanage necessari tempo e risorse hello. Questa operazione richiede che alcuni considerato, tuttavia, toochoose hello migliore tooupdate oggetti statistiche.

### <a name="b-update-all-statistics-on-a-table"></a>B. Aggiornare tutte le statistiche in una tabella
Mostra un metodo semplice per l'aggiornamento di tutti gli oggetti statistiche hello in una tabella.

```sql
UPDATE STATISTICS [schema_name].[table_name];
```

ad esempio:

```sql
UPDATE STATISTICS dbo.table1;
```

Questa istruzione è facile toouse. Ricorda però questo Aggiorna tutte le statistiche di tabella hello e pertanto potrebbe operare più del necessario. Se le prestazioni di hello non è un problema, questo è decisamente modo più semplice e completo hello tooguarantee statistiche siano aggiornate.

> [!NOTE]
> Quando si aggiorna tutte le statistiche di una tabella, SQL Data Warehouse esegue una tabella di hello toosample analisi per ogni tipo di statistiche. Se la tabella hello è grande, dispone di un numero di colonne e molte statistiche, potrebbe essere più efficiente tooupdate singoli le statistiche in base alle esigenze.
> 
> 

Per un'implementazione di un `UPDATE STATISTICS` procedura vedere hello [tabelle temporanee] [ Temporary] articolo. il metodo di implementazione di Hello è leggermente diverso toohello `CREATE STATISTICS` procedura sopra indicata ma risultato finale hello è hello stesso.

La sintassi completa di hello, vedere [Update Statistics] [ Update Statistics] su MSDN.

## <a name="statistics-metadata"></a>Metadati delle statistiche
Esistono diverse vista di sistema e le funzioni che è possibile utilizzare toofind informazioni sulle statistiche. Ad esempio, è possibile visualizzare se un oggetto statistiche potrebbe essere obsolete utilizzando hello statistiche data funzione toosee quando le statistiche ultima create o aggiornate.

### <a name="catalog-views-for-statistics"></a>Viste del catalogo per le statistiche
Queste visualizzazioni di sistema forniscono informazioni sulle statistiche:

| Vista del catalogo | Descrizione |
|:--- |:--- |
| [sys.columns][sys.columns] |Una riga per ogni colonna. |
| [sys.objects][sys.objects] |Una riga per ogni oggetto nel database di hello. |
| [sys.schemas][sys.schemas] |Una riga per ogni schema nel database di hello. |
| [sys.stats][sys.stats] |Una riga per ogni oggetto statistiche. |
| [sys.stats_columns][sys.stats_columns] |Una riga per ogni colonna nell'oggetto statistiche hello. Consente di tornare toosys.columns. |
| [sys.tables][sys.tables] |Una riga per ogni tabella (include le tabelle esterne). |
| [sys.table_types][sys.table_types] |Una riga per ogni tipo di dati. |

### <a name="system-functions-for-statistics"></a>Funzioni di sistema per le statistiche
Queste funzioni di sistema sono utili per usare le statistiche:

| Funzioni di sistema | Descrizione |
|:--- |:--- |
| [STATS_DATE][STATS_DATE] |Oggetto statistiche di hello data dell'ultimo aggiornamento. |
| [DBCC SHOW_STATISTICS][DBCC SHOW_STATISTICS] |Fornisce informazioni di riepilogo livello e dettagliate sulla distribuzione dei valori di hello riconosciuto dall'oggetto statistiche hello. |

### <a name="combine-statistics-columns-and-functions-into-one-view"></a>Combinare le colonne delle statistiche e le funzioni in un'unica visualizzazione
Questa vista visualizza le colonne correlate tra loro toostatistics e risultati dalla funzione di hello [STATS_DATE()] [].

```sql
CREATE VIEW dbo.vstats_columns
AS
SELECT
        sm.[name]                           AS [schema_name]
,       tb.[name]                           AS [table_name]
,       st.[name]                           AS [stats_name]
,       st.[filter_definition]              AS [stats_filter_defiinition]
,       st.[has_filter]                     AS [stats_is_filtered]
,       STATS_DATE(st.[object_id],st.[stats_id])
                                            AS [stats_last_updated_date]
,       co.[name]                           AS [stats_column_name]
,       ty.[name]                           AS [column_type]
,       co.[max_length]                     AS [column_max_length]
,       co.[precision]                      AS [column_precision]
,       co.[scale]                          AS [column_scale]
,       co.[is_nullable]                    AS [column_is_nullable]
,       co.[collation_name]                 AS [column_collation_name]
,       QUOTENAME(sm.[name])+'.'+QUOTENAME(tb.[name])
                                            AS two_part_name
,       QUOTENAME(DB_NAME())+'.'+QUOTENAME(sm.[name])+'.'+QUOTENAME(tb.[name])
                                            AS three_part_name
FROM    sys.objects                         AS ob
JOIN    sys.stats           AS st ON    ob.[object_id]      = st.[object_id]
JOIN    sys.stats_columns   AS sc ON    st.[stats_id]       = sc.[stats_id]
                            AND         st.[object_id]      = sc.[object_id]
JOIN    sys.columns         AS co ON    sc.[column_id]      = co.[column_id]
                            AND         sc.[object_id]      = co.[object_id]
JOIN    sys.types           AS ty ON    co.[user_type_id]   = ty.[user_type_id]
JOIN    sys.tables          AS tb ON  co.[object_id]        = tb.[object_id]
JOIN    sys.schemas         AS sm ON  tb.[schema_id]        = sm.[schema_id]
WHERE   1=1
AND     st.[user_created] = 1
;
```

## <a name="dbcc-showstatistics-examples"></a>Esempi di DBCC SHOW_STATISTICS()
DBCC SHOW_STATISTICS() Mostra i dati di hello contenuti all'interno di un oggetto statistiche. Questi dati sono costituiti da tre parti.

1. Intestazione
2. Vettore di densità
3. Istogramma

metadati di intestazione Hello sulle statistiche di hello. Istogramma Hello Visualizza distribuzione hello dei valori nella prima colonna chiave di hello dell'oggetto statistiche hello. vettore di densità Hello consente di misurare la correlazione tra colonne. SQLDW calcola le stime della cardinalità con i dati di hello nell'oggetto statistiche hello.

### <a name="show-header-density-and-histogram"></a>Mostrare l'intestazione, la densità e l'istogramma
Questo semplice esempio mostra tutte e tre le parti di un oggetto statistiche.

```sql
DBCC SHOW_STATISTICS([<schema_name>.<table_name>],<stats_name>)
```

Ad esempio:

```sql
DBCC SHOW_STATISTICS (dbo.table1, stats_col1);
```

### <a name="show-one-or-more-parts-of-dbcc-showstatistics"></a>Mostrare una o più parti di DBCC SHOW_STATISTICS();
Se si è solo interessati a visualizzare parti specifiche, utilizzare hello `WITH` clausola e specificare quali parti è desidera toosee:

```sql
DBCC SHOW_STATISTICS([<schema_name>.<table_name>],<stats_name>) WITH stat_header, histogram, density_vector
```

ad esempio:

```sql
DBCC SHOW_STATISTICS (dbo.table1, stats_col1) WITH histogram, density_vector
```

## <a name="dbcc-showstatistics-differences"></a>Differenze di DBCC SHOW_STATISTICS()
DBCC SHOW_STATISTICS() in modo più rigoroso viene implementato in SQL Data Warehouse confrontati tooSQL Server.

1. Le funzionalità non documentate non sono supportate
2. Non è possibile usare Stats_stream
3. Non è possibile unire i risultati per sottoinsiemi specifici di dati statistici, ad esempio (STAT_HEADER JOIN DENSITY_VECTOR)
4. NO_INFOMSGS non può essere impostato per l'eliminazione del messaggio
5. Non è possibile usare le parentesi quadre per i nomi delle statistiche
6. Impossibile utilizzare oggetti statistiche tooidentify i nomi di colonna
7. L'errore personalizzato 2767 non è supportato

## <a name="next-steps"></a>Passaggi successivi
Per altri dettagli, vedere [DBCC SHOW_STATISTICS][DBCC SHOW_STATISTICS] in MSDN.  toolearn, vedere gli articoli di hello in [Cenni preliminari su tabella][Overview], [tipi di dati tabella][Data Types], [la distribuzione di una tabella] [ Distribute], [L'indicizzazione di una tabella][Index], [il partizionamento di una tabella] [ Partition] e [ Tabelle temporanee][Temporary].  Per altre informazioni sulle procedure consigliate, vedere [Procedure consigliate per SQL Data Warehouse][SQL Data Warehouse Best Practices].  

<!--Image references-->

<!--Article references-->
[Overview]: ./sql-data-warehouse-tables-overview.md
[Data Types]: ./sql-data-warehouse-tables-data-types.md
[Distribute]: ./sql-data-warehouse-tables-distribute.md
[Index]: ./sql-data-warehouse-tables-index.md
[Partition]: ./sql-data-warehouse-tables-partition.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[Temporary]: ./sql-data-warehouse-tables-temporary.md
[SQL Data Warehouse Best Practices]: ./sql-data-warehouse-best-practices.md

<!--MSDN references-->  
[Cardinality Estimation]: https://msdn.microsoft.com/library/dn600374.aspx
[CREATE STATISTICS]: https://msdn.microsoft.com/library/ms188038.aspx
[DBCC SHOW_STATISTICS]:https://msdn.microsoft.com/library/ms174384.aspx
[Statistics]: https://msdn.microsoft.com/library/ms190397.aspx
[STATS_DATE]: https://msdn.microsoft.com/library/ms190330.aspx
[sys.columns]: https://msdn.microsoft.com/library/ms176106.aspx
[sys.objects]: https://msdn.microsoft.com/library/ms190324.aspx
[sys.schemas]: https://msdn.microsoft.com/library/ms190324.aspx
[sys.stats]: https://msdn.microsoft.com/library/ms177623.aspx
[sys.stats_columns]: https://msdn.microsoft.com/library/ms187340.aspx
[sys.tables]: https://msdn.microsoft.com/library/ms187406.aspx
[sys.table_types]: https://msdn.microsoft.com/library/bb510623.aspx
[UPDATE STATISTICS]: https://msdn.microsoft.com/library/ms187348.aspx

<!--Other Web references-->  
