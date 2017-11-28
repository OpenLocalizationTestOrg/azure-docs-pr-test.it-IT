---
title: aaaIndexing nelle tabelle SQL Data Warehouse | Microsoft Azure
description: Introduzione all'indicizzazione delle tabelle in Azure SQL Data Warehouse.
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: barbkess
editor: 
ms.assetid: 3e617674-7b62-43ab-9ca2-3f40c41d5a88
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: tables
ms.date: 07/12/2016
ms.author: shigu;barbkess
ms.openlocfilehash: e614d63c8fb871f2ba388f14576cf9f282d4b818
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="indexing-tables-in-sql-data-warehouse"></a>Indicizzazione di tabelle in SQL Data Warehouse
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

SQL Data Warehouse offre diverse opzioni di indicizzazione, inclusi [indici columnstore cluster][clustered columnstore indexes], [indici cluster e indici non cluster][clustered indexes and nonclustered indexes].  Offre anche un'opzione senza indice nota come [heap][heap].  In questo articolo illustra i vantaggi di hello di ogni tipo di indice, nonché suggerimenti hello toogetting la maggior parte delle prestazioni degli indici. Vedere [tabella sintassi di create] [ create table syntax] per ulteriori informazioni su come toocreate una tabella in SQL Data Warehouse.

## <a name="clustered-columnstore-indexes"></a>Indici columnstore cluster
Per impostazione predefinita, SQL Data Warehouse crea un indice columnstore cluster quando non vengono specificate opzioni di indice in una tabella. Le tabelle columnstore cluster offrono entrambi hello massimo livello di compressione dei dati, nonché hello migliori prestazioni complessive delle query.  Le tabelle columnstore cluster verranno in genere che le tabelle heap o indice cluster e vengono in genere migliore hello per le tabelle di grandi dimensioni.  Per questi motivi, columnstore cluster è toostart sul posto migliore hello quando non si è certi di come tooindex la tabella.  

toocreate una tabella columnstore cluster, è sufficiente specificare l'indice COLUMNSTORE cluster nella clausola WITH hello oppure lasciare clausola WITH hello off:

```SQL
CREATE TABLE myTable   
  (  
    id int NOT NULL,  
    lastName varchar(20),  
    zipCode varchar(6)  
  )  
WITH ( CLUSTERED COLUMNSTORE INDEX );
```

In alcuni scenari l'indice columnstore cluster potrebbe non essere la scelta ideale:

* Le tabelle columnstore non supportano varchar(max), nvarchar(max) e varbinary(max).  È consigliabile usare tabelle heap o di indici cluster.
* Le tabelle columnstore potrebbero risultare meno efficiente per i dati temporanei.  È consigliabile usare tabelle heap oppure tabelle temporanee.
* Tabelle di piccole dimensioni con meno di 100 milioni di righe.  È consigliabile usare tabelle heap.

## <a name="heap-tables"></a>Tabelle heap
Quando si temporaneamente di destinazione dei dati in SQL Data Warehouse, è possibile che utilizza una tabella heap effettuerà hello processo complessivo più velocemente.  In questo modo tooheaps carichi sono più veloci rispetto alle tabelle tooindex e in alcuni hello casi successiva lettura può essere eseguita dalla cache.  Se si sta caricando toostage solo di dati prima di eseguire più trasformazioni, il caricamento della tabella di hello tabella tooheap sarà molto più rapido il caricamento di hello dati tooa cluster nella tabella columnstore. Inoltre, il caricamento di dati tooa [tabella temporanea] [ Temporary] caricherà inoltre molto più rapidamente il caricamento di un'archiviazione toopermanent tabella.  

Per le tabelle di ricerca di piccole dimensioni, inferiori a 100 milioni di righe, è spesso consigliabile scegliere le tabelle heap.  Le tabelle columnstore cluster iniziano tooachieve di compressione ottimale quando è presente più di 100 milioni di righe.

toocreate una tabella heap, specificare semplicemente l'HEAP nella clausola WITH hello:

```SQL
CREATE TABLE myTable   
  (  
    id int NOT NULL,  
    lastName varchar(20),  
    zipCode varchar(6)  
  )  
WITH ( HEAP );
```

## <a name="clustered-and-nonclustered-indexes"></a>Indici cluster e non cluster
Gli indici cluster potrebbero che le tabelle columnstore cluster quando una riga singola deve toobe rapidamente recuperati.  Per le query in cui una o poche ricerca riga è necessario tooperformance con estrema velocità, considerare un indice cluster o indici secondari.  Hello svantaggio toousing un indice cluster è che solo le query che utilizzano un filtro estremamente selettivo sulla colonna di indice cluster hello trarranno vantaggio.  filtro tooimprove su altre colonne di che un indice non cluster può essere aggiunte colonne di tooother.  Tuttavia, ogni indice che viene aggiunto tooa tabella aggiungerà sia lo spazio di elaborazione tooloads ora.

toocreate una tabella con indice cluster, è sufficiente specificare un indice cluster nella clausola WITH hello:

```SQL
CREATE TABLE myTable   
  (  
    id int NOT NULL,  
    lastName varchar(20),  
    zipCode varchar(6)  
  )  
WITH ( CLUSTERED INDEX (id) );
```

tooadd un indice non cluster in una tabella, è sufficiente utilizzare hello la seguente sintassi:

```SQL
CREATE INDEX zipCodeIndex ON t1 (zipCode);
```

## <a name="optimizing-clustered-columnstore-indexes"></a>Ottimizzazione degli indici columnstore cluster
I dati delle tabelle columnstore cluster sono organizzati in segmenti.  Disporre di qualità elevata segmento è critico tooachieving prestazioni ottimali delle query in una tabella columnstore.  Qualità segmento può essere misurata tramite un numero di righe in un gruppo di righe compresso hello.  Qualità di segmento è ottimale in cui sono presenti almeno 100 KB righe per ogni riga compresso gruppo e aumento delle prestazioni come numero hello di righe per ogni riga gruppo approccio 1.048.576 righe, ossia hello la maggior parte delle righe che può contenere un gruppo di righe.

Hello sotto visualizzazione può essere creato e usato nel hello toocompute sistema medie righe per ogni riga di gruppo e identificare tutti gli indici columnstore cluster ottimali.  ultima colonna di Hello in questa vista verrà generato come istruzione SQL che può essere utilizzato toorebuild degli indici.

```sql
CREATE VIEW dbo.vColumnstoreDensity
AS
SELECT
        GETDATE()                                                               AS [execution_date]
,       DB_Name()                                                               AS [database_name]
,       s.name                                                                  AS [schema_name]
,       t.name                                                                  AS [table_name]
,    COUNT(DISTINCT rg.[partition_number])                    AS [table_partition_count]
,       SUM(rg.[total_rows])                                                    AS [row_count_total]
,       SUM(rg.[total_rows])/COUNT(DISTINCT rg.[distribution_id])               AS [row_count_per_distribution_MAX]
,    CEILING    ((SUM(rg.[total_rows])*1.0/COUNT(DISTINCT rg.[distribution_id]))/1048576) AS [rowgroup_per_distribution_MAX]
,       SUM(CASE WHEN rg.[State] = 0 THEN 1                   ELSE 0    END)    AS [INVISIBLE_rowgroup_count]
,       SUM(CASE WHEN rg.[State] = 0 THEN rg.[total_rows]     ELSE 0    END)    AS [INVISIBLE_rowgroup_rows]
,       MIN(CASE WHEN rg.[State] = 0 THEN rg.[total_rows]     ELSE NULL END)    AS [INVISIBLE_rowgroup_rows_MIN]
,       MAX(CASE WHEN rg.[State] = 0 THEN rg.[total_rows]     ELSE NULL END)    AS [INVISIBLE_rowgroup_rows_MAX]
,       AVG(CASE WHEN rg.[State] = 0 THEN rg.[total_rows]     ELSE NULL END)    AS [INVISIBLE_rowgroup_rows_AVG]
,       SUM(CASE WHEN rg.[State] = 1 THEN 1                   ELSE 0    END)    AS [OPEN_rowgroup_count]
,       SUM(CASE WHEN rg.[State] = 1 THEN rg.[total_rows]     ELSE 0    END)    AS [OPEN_rowgroup_rows]
,       MIN(CASE WHEN rg.[State] = 1 THEN rg.[total_rows]     ELSE NULL END)    AS [OPEN_rowgroup_rows_MIN]
,       MAX(CASE WHEN rg.[State] = 1 THEN rg.[total_rows]     ELSE NULL END)    AS [OPEN_rowgroup_rows_MAX]
,       AVG(CASE WHEN rg.[State] = 1 THEN rg.[total_rows]     ELSE NULL END)    AS [OPEN_rowgroup_rows_AVG]
,       SUM(CASE WHEN rg.[State] = 2 THEN 1                   ELSE 0    END)    AS [CLOSED_rowgroup_count]
,       SUM(CASE WHEN rg.[State] = 2 THEN rg.[total_rows]     ELSE 0    END)    AS [CLOSED_rowgroup_rows]
,       MIN(CASE WHEN rg.[State] = 2 THEN rg.[total_rows]     ELSE NULL END)    AS [CLOSED_rowgroup_rows_MIN]
,       MAX(CASE WHEN rg.[State] = 2 THEN rg.[total_rows]     ELSE NULL END)    AS [CLOSED_rowgroup_rows_MAX]
,       AVG(CASE WHEN rg.[State] = 2 THEN rg.[total_rows]     ELSE NULL END)    AS [CLOSED_rowgroup_rows_AVG]
,       SUM(CASE WHEN rg.[State] = 3 THEN 1                   ELSE 0    END)    AS [COMPRESSED_rowgroup_count]
,       SUM(CASE WHEN rg.[State] = 3 THEN rg.[total_rows]     ELSE 0    END)    AS [COMPRESSED_rowgroup_rows]
,       SUM(CASE WHEN rg.[State] = 3 THEN rg.[deleted_rows]   ELSE 0    END)    AS [COMPRESSED_rowgroup_rows_DELETED]
,       MIN(CASE WHEN rg.[State] = 3 THEN rg.[total_rows]     ELSE NULL END)    AS [COMPRESSED_rowgroup_rows_MIN]
,       MAX(CASE WHEN rg.[State] = 3 THEN rg.[total_rows]     ELSE NULL END)    AS [COMPRESSED_rowgroup_rows_MAX]
,       AVG(CASE WHEN rg.[State] = 3 THEN rg.[total_rows]     ELSE NULL END)    AS [COMPRESSED_rowgroup_rows_AVG]
,       'ALTER INDEX ALL ON ' + s.name + '.' + t.NAME + ' REBUILD;'             AS [Rebuild_Index_SQL]
FROM    sys.[pdw_nodes_column_store_row_groups] rg
JOIN    sys.[pdw_nodes_tables] nt                   ON  rg.[object_id]          = nt.[object_id]
                                                    AND rg.[pdw_node_id]        = nt.[pdw_node_id]
                                                    AND rg.[distribution_id]    = nt.[distribution_id]
JOIN    sys.[pdw_table_mappings] mp                 ON  nt.[name]               = mp.[physical_name]
JOIN    sys.[tables] t                              ON  mp.[object_id]          = t.[object_id]
JOIN    sys.[schemas] s                             ON t.[schema_id]            = s.[schema_id]
GROUP BY
        s.[name]
,       t.[name]
;
```

Ora che è stato creato vista hello, eseguire la query tooidentify tabelle con gruppi di righe con meno di 100 KB righe.  Naturalmente, è opportuno soglia hello tooincrease di 100 KB se si sta cercando più qualità ottimale segmento. 

```sql
SELECT    *
FROM    [dbo].[vColumnstoreDensity]
WHERE    COMPRESSED_rowgroup_rows_AVG < 100000
        OR INVISIBLE_rowgroup_rows_AVG < 100000
```

Dopo aver eseguito la query hello è possibile iniziare toolook dati hello e analizzare i risultati. Questa tabella illustra quali toolook per l'analisi di gruppo di riga.

| Colonna | Come toouse dati |
| --- | --- |
| [table_partition_count] |Se hello tabella è partizionata, è possibile prevedere toosee superiore conteggi gruppo di righe aperto. Ogni partizione nella distribuzione hello potrebbe in teoria dispone di un gruppo di righe aperto è associato. Includere questo fattore nell'analisi. Una tabella di piccole dimensioni che è stata partizionata può essere ottimizzata rimuovendo hello partizionamento completamente come questo contribuisce a migliorare la compressione. |
| [row_count_total] |Numero totale di righe per tabella hello. Ad esempio, è possibile utilizzare questa percentuale del valore toocalculate di righe nello stato compresso hello. |
| [row_count_per_distribution_MAX] |Se tutte le righe sono distribuite uniformemente questo valore sarà il numero di destinazione hello di righe per ogni distribuzione. Confrontare questo valore con compressed_rowgroup_count hello. |
| [COMPRESSED_rowgroup_rows] |Numero totale di righe nel formato columnstore per tabella hello. |
| [COMPRESSED_rowgroup_rows_AVG] |Se il numero medio di hello di righe è significativamente minore di hello massimo numero delle righe per un gruppo di righe, è consigliabile utilizzare un'istruzione CTAS o ALTER INDEX REBUILD toorecompress hello dati |
| [COMPRESSED_rowgroup_count] |Numero di gruppi di righe nel formato columnstore. Se questo numero è molto alto nella tabella toohello relazione è un indicatore che densità columnstore hello è basso. |
| [COMPRESSED_rowgroup_rows_DELETED] |Le righe vengono eliminate in modo logico nel formato columnstore. Se il numero di hello è di dimensioni tootable relativa, provare a ricreare la partizione hello o la ricompilazione dell'indice hello quanto viene rimosso fisicamente. |
| [COMPRESSED_rowgroup_rows_MIN] |Utilizzare in combinazione con hello AVG e MAX colonne toounderstand hello intervallo di valori per i gruppi di righe hello del ColumnStore. Un numero basso oltre la soglia di carico hello (102.400 per ogni partizione allineata distribuzione) suggerisce che le ottimizzazioni sono disponibili in hello il caricamento dei dati |
| [COMPRESSED_rowgroup_rows_MAX] |Come sopra. |
| [OPEN_rowgroup_count] |I gruppi di righe aperti sono normali. È ragionevole prevedere un gruppo di righe aperto (OPEN) per ogni distribuzione di tabella (60). Un numero eccessivo suggerisce il caricamento di dati tra le partizioni. Verificare hello partizionamento toomake strategia che si tratti di audio |
| [OPEN_rowgroup_rows] |Ogni gruppo di righe può contenere al massimo 1.048.576 righe. Utilizzare questo valore toosee il livello di riempimento presenti gruppi di righe aperto hello |
| [OPEN_rowgroup_rows_MIN] |Aprire gruppi indicano che i dati sono trickle viene caricata nella tabella hello o che hello distribuita su righe rimanenti in questo gruppo di righe di carico precedente. Hello di utilizzare MIN, MAX, AVG colonne toosee la quantità di dati è rimasta in gruppi di righe aperto. Per le piccole tabelle è possibile 100% di tutti i dati di hello! In tal caso, ALTER INDEX REBUILD tooforce hello toocolumnstore di dati. |
| [OPEN_rowgroup_rows_MAX] |Come sopra. |
| [OPEN_rowgroup_rows_AVG] |Come sopra. |
| [CLOSED_rowgroup_rows] |Esaminare le righe del gruppo riga hello chiuso come controllo di integrità. |
| [CLOSED_rowgroup_count] |numero di Hello di gruppi di righe chiusi dovrebbe essere basso se qualsiasi sono visibili in tutti. Gruppi di righe chiusi possono essere convertito toocompressed rowg roups utilizzando hello ALTER INDEX... REORGANISE. In genere questa operazione non è tuttavia richiesta. Gruppi chiusi sono gruppi di righe toocolumnstore convertito automaticamente dal processo di "processo tuple-mover" hello in background. |
| [CLOSED_rowgroup_rows_MIN] |I gruppi di righe chiusi devono avere una velocità di riempimento molto elevata. Se la percentuale di riempimento hello per un gruppo di righe chiusi è bassa, quindi un'ulteriore analisi dei columnstore hello è obbligatoria. |
| [CLOSED_rowgroup_rows_MAX] |Come sopra. |
| [CLOSED_rowgroup_rows_AVG] |Come sopra. |
| [Rebuild_Index_SQL] |Indice columnstore di toorebuild SQL per una tabella |

## <a name="causes-of-poor-columnstore-index-quality"></a>Possibili cause di una qualità scadente dell'indice columnstore
Se è stato identificato le tabelle con una qualità segmento insufficienti, è possibile causa radice di hello tooidentify.  Di seguito sono riportate altre cause comuni della qualità scadente dei segmenti:

1. Utilizzo elevato di memoria durante la compilazione dell'indice
2. Volume elevato di operazioni DML
3. Operazioni di caricamento di piccole dimensioni o con un flusso irregolare 
4. Troppe partizioni

Questi fattori possono causare un toohave indice columnstore notevolmente inferiore hello ottimale 1 milione di righe per ogni gruppo di righe.  Inoltre, è possibile che le righe toogo toohello gruppo di righe delta anziché un gruppo di righe compresso. 

### <a name="memory-pressure-when-index-was-built"></a>Utilizzo elevato di memoria durante la compilazione dell'indice
numero di Hello di righe per ogni gruppo di righe compresso è direttamente correlati toohello larghezza della riga hello e hello quantità di memoria disponibile tooprocess hello gruppo di righe.  Quando le righe vengono scritti tabelle toocolumnstore eccessivo della memoria e qualità di segmento di columnstore potrebbe risentirne.  Pertanto, hello consiglia sessione hello toogive sta scrivendo le tabelle di indice columnstore tooyour accedono tooas minor quantità di memoria.  Poiché non esiste un compromesso tra memoria e concorrenza, indicazioni hello su hello destra memoria allocazione dipende dai dati hello in ogni riga della tabella, quantità hello di DWU avere allocato sistema tooyour e slot della quantità di hello di concorrenza è possono assegnare toohello sessione a cui viene scritto nella tabella dati tooyour.  Come procedura consigliata, è consigliabile iniziare con xlargerc se si utilizza DW300 o meno, largerc se si utilizza DW400 tooDW600 e mediumrc se si utilizza DW1000 e versioni successive.

### <a name="high-volume-of-dml-operations"></a>Volume elevato di operazioni DML
Un volume elevato di operazioni DML di aggiornamento ed eliminazione di righe può introdurre inefficienza hello ColumnStore. Ciò vale soprattutto quando vengono modificate maggioranza hello di righe hello in un gruppo di righe.

* Eliminazione di una riga da un gruppo di righe compresso solo logicamente contrassegna la riga hello come eliminato. la riga Hello rimane nel gruppo di righe compresso hello finché non viene ricompilata hello partizione o tabella.
* Inserimento di una riga aggiunge una tabella rowstore interno tootooan riga hello chiamata un gruppo di righe delta. la riga Hello inserito non è convertito toocolumnstore fino a quando il gruppo di righe delta hello è pieno e viene contrassegnato come chiuso. Gruppi di righe vengono chiusi dopo aver raggiunto la capacità massima di hello di 1.048.576 righe. 
* L'aggiornamento di una riga nel formato columnstore viene elaborato come un'eliminazione logica e poi come operazione di inserimento. la riga Hello inserito può essere archiviata nell'archivio delta hello.

Aggiornamento in batch e l'inserimento di operazioni che superano la soglia di blocco hello di 102.400 righe per partizione allineata distribuzione verrà scritti direttamente formattare toohello columnstore. Tuttavia, presupponendo una distribuzione uniforme, è necessario modificare 6.144 milioni di righe in un'unica operazione per questo toooccur toobe. Se il numero di hello di righe per una determinata partizione allineata distribuzione è meno di 102.400 righe hello entreranno archivio delta toohello e rimangono in fino a quando non sono state inserite righe sufficienti o modificato tooclose hello gruppo hello o un indice di riga è stato ricompilato.

### <a name="small-or-trickle-load-operations"></a>Operazioni di caricamento di piccole dimensioni o con un flusso irregolare 
I caricamenti di piccole dimensioni in SQL Data Warehouse sono anche definiti flussi irregolari. In genere rappresentano un flusso costante vicino di dati, il caricamento dal sistema hello. Tuttavia, come il flusso è quasi volume hello continua di righe non è particolarmente grandi. Molto spesso dati hello sono significativamente sotto la soglia di hello necessario per un formato toocolumnstore caricamento diretto.

In questi casi, è spesso dati di hello tooland migliori prima nell'archiviazione blob di Azure e lascia accumulare tooloading precedente. Questa tecnica viene spesso definita come *micro invio in batch*.

### <a name="too-many-partitions"></a>Troppe partizioni
Un altro aspetto tooconsider è impatto hello del partizionamento per le tabelle columnstore cluster.  Prima di eseguire il partizionamento, SQL Data Warehouse divide già i dati in 60 database.  Il partizionamento, quindi, suddivide ulteriormente i dati.  Se si partizionare i dati, quindi si desidererà tooconsider che **ogni** partizione sarà necessario toohave almeno 1 milione di righe toobenefit da un indice columnstore cluster.  Se si partizionare la tabella in 100 partizioni, quindi la tabella sarà necessario almeno 6 miliardi toohave toobenefit di righe da un indice columnstore cluster (60 distribuzioni * 100 partizioni * 1 milione di righe). Se la tabella di 100 partizione non dispone di 6 miliardi di righe, ridurre il numero di hello di partizioni o si consideri l'utilizzo di una tabella heap.

Dopo aver caricate le tabelle con alcuni dati, seguire hello sotto tooidentify passaggi e ricompilare le tabelle con indici columnstore cluster ottimali.

## <a name="rebuilding-indexes-tooimprove-segment-quality"></a>La ricompilazione di indici tooimprove segmento di qualità
### <a name="step-1-identify-or-create-user-which-uses-hello-right-resource-class"></a>Passaggio 1: Identificare o creare l'utente che utilizza una classe di risorse destra hello
Il più modo rapido tooimmediately migliorare la qualità del segmento è indice di hello toorebuild.  Hello SQL restituita da hello sopra vista restituirà un'istruzione ALTER INDEX REBUILD, che può essere utilizzato toorebuild degli indici.  Quando si ricompila gli indici, assicurarsi di allocare sufficiente memoria toohello sessione causerà la ricostruzione dell'indice.  toodo, questa classe di risorse hello aumento di un utente che dispone di autorizzazioni toorebuild hello indice su questo requisito minimo consigliato di toohello tabella.  Impossibile modificare la classe di risorse Hello hello proprietario dell'utente del database, pertanto se non è stato creato un utente nel sistema hello, sarà necessario pertanto innanzitutto toodo.  valore minimo di Hello che è consigliabile è xlargerc se si utilizza DW300 o meno, largerc se si utilizza DW400 tooDW600 e mediumrc se si utilizza DW1000 e versioni successive.

Di seguito è riportato un esempio di come tooallocate utente tooa di memoria più aumentando la relativa classe di risorse.  Per ulteriori informazioni sulle classi di risorse e come toocreate un nuovo utente è reperibile in hello [concorrenza e carico di lavoro gestione] [ Concurrency] articolo.

```sql
EXEC sp_addrolemember 'xlargerc', 'LoadUser'
```

### <a name="step-2-rebuild-clustered-columnstore-indexes-with-higher-resource-class-user"></a>Passaggio 2: Ricompilare gli indici columnstore cluster con un utente che usa una classe di risorse superiore
Accesso come hello utente ottenuto al passaggio 1 (ad esempio LoadUser), che ora utilizzando una classe di risorse superiore, eseguire le istruzioni ALTER INDEX hello.  Assicurarsi che l'utente disponga delle tabelle di toohello dell'autorizzazione ALTER in hello ricompilazione.  Questi esempi mostrano come toorebuild hello intero indice columnstore o come toorebuild una singola partizione. Tabelle di grandi dimensioni, è più pratici indici toorebuild una singola partizione alla volta.

In alternativa, invece di ricompilare l'indice di hello, è possibile copiare hello tabella tooa nuova tabella tramite [un'istruzione CTAS][CTAS].  Qual è il modo migliore? Per grandi volumi di dati [CTAS][CTAS] è in genere più veloce di [ALTER INDEX][ALTER INDEX]. Per i volumi di dati, più piccolo [ALTER INDEX] [ ALTER INDEX] è toouse più semplice e non richiedono tooswap tabella hello.  Vedere **la ricompilazione degli indici con un'istruzione CTAS e il cambio della partizione** seguito per ulteriori informazioni su come vengono indicizzati con un'istruzione CTAS toorebuild.

```sql
-- Rebuild hello entire clustered index
ALTER INDEX ALL ON [dbo].[DimProduct] REBUILD
```

```sql
-- Rebuild a single partition
ALTER INDEX ALL ON [dbo].[FactInternetSales] REBUILD Partition = 5
```

```sql
-- Rebuild a single partition with archival compression
ALTER INDEX ALL ON [dbo].[FactInternetSales] REBUILD Partition = 5 WITH (DATA_COMPRESSION = COLUMNSTORE_ARCHIVE)
```

```sql
-- Rebuild a single partition with columnstore compression
ALTER INDEX ALL ON [dbo].[FactInternetSales] REBUILD Partition = 5 WITH (DATA_COMPRESSION = COLUMNSTORE)
```

La ricompilazione di un indice in SQL Data Warehouse è un'operazione offline.  Per ulteriori informazioni sulla ricompilazione di indici, vedere ALTER INDEX REBUILD sezione hello [deframmentazione degli indici Columnstore] [ Columnstore Indexes Defragmentation] e hello sintassi argomento [ALTER INDEX] [ALTER INDEX].

### <a name="step-3-verify-clustered-columnstore-segment-quality-has-improved"></a>Passaggio 3: Verificare che la qualità dei segmenti columnstore cluster sia migliorata
Query hello Riesegui identificato nella tabella con una scarsa qualità di segmenti e verificare qualità di segmento sono migliorate.  Se non migliora la qualità segmento, è possibile che le righe della tabella hello sono molto grande.  È consigliabile usare una classe di risorse superiore o una DWU durante la ricompilazione degli indici.

## <a name="rebuilding-indexes-with-ctas-and-partition-switching"></a>Ricompilazione degli indici con CTAS e cambio della partizione
Questo esempio viene utilizzato [un'istruzione CTAS] [ CTAS] e toorebuild partizione della tabella del cambio di partizione. 

```sql
-- Step 1: Select hello partition of data and write it out tooa new table using CTAS
CREATE TABLE [dbo].[FactInternetSales_20000101_20010101]
    WITH    (   DISTRIBUTION = HASH([ProductKey])
            ,   CLUSTERED COLUMNSTORE INDEX
            ,   PARTITION   (   [OrderDateKey] RANGE RIGHT FOR VALUES
                                (20000101,20010101
                                )
                            )
            )
AS
SELECT  *
FROM    [dbo].[FactInternetSales]
WHERE   [OrderDateKey] >= 20000101
AND     [OrderDateKey] <  20010101
;

-- Step 2: Create a SWITCH out table
CREATE TABLE dbo.FactInternetSales_20000101
    WITH    (   DISTRIBUTION = HASH(ProductKey)
            ,   CLUSTERED COLUMNSTORE INDEX
            ,   PARTITION   (   [OrderDateKey] RANGE RIGHT FOR VALUES
                                (20000101
                                )
                            )
            )
AS
SELECT *
FROM    [dbo].[FactInternetSales]
WHERE   1=2 -- Note this table will be empty

-- Step 3: Switch OUT hello data 
ALTER TABLE [dbo].[FactInternetSales] SWITCH PARTITION 2 too [dbo].[FactInternetSales_20000101] PARTITION 2;

-- Step 4: Switch IN hello rebuilt data
ALTER TABLE [dbo].[FactInternetSales_20000101_20010101] SWITCH PARTITION 2 too [dbo].[FactInternetSales] PARTITION 2;
```

Per ulteriori informazioni sulla creazione di partizioni che usano `CTAS`, vedere hello [partizione] [ Partition] articolo.

## <a name="next-steps"></a>Passaggi successivi
toolearn, vedere gli articoli di hello in [Cenni preliminari su tabella][Overview], [tipi di dati tabella][Data Types], [la distribuzione di una tabella] [ Distribute], [Il partizionamento di una tabella][Partition], [gestione delle statistiche sulla tabella] [ Statistics] e [ Tabelle temporanee][Temporary].  toolearn più sulle procedure consigliate, vedere [procedure consigliate di SQL Data Warehouse][SQL Data Warehouse Best Practices].

<!--Image references-->

<!--Article references-->
[Overview]: ./sql-data-warehouse-tables-overview.md
[Data Types]: ./sql-data-warehouse-tables-data-types.md
[Distribute]: ./sql-data-warehouse-tables-distribute.md
[Index]: ./sql-data-warehouse-tables-index.md
[Partition]: ./sql-data-warehouse-tables-partition.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[Temporary]: ./sql-data-warehouse-tables-temporary.md
[Concurrency]: ./sql-data-warehouse-develop-concurrency.md
[CTAS]: ./sql-data-warehouse-develop-ctas.md
[SQL Data Warehouse Best Practices]: ./sql-data-warehouse-best-practices.md

<!--MSDN references-->
[ALTER INDEX]: https://msdn.microsoft.com/library/ms188388.aspx
[heap]: https://msdn.microsoft.com/library/hh213609.aspx
[clustered indexes and nonclustered indexes]: https://msdn.microsoft.com/library/ms190457.aspx
[create table syntax]: https://msdn.microsoft.com/library/mt203953.aspx
[Columnstore Indexes Defragmentation]: https://msdn.microsoft.com/library/dn935013.aspx#Anchor_1
[clustered columnstore indexes]: https://msdn.microsoft.com/library/gg492088.aspx

<!--Other Web references-->
