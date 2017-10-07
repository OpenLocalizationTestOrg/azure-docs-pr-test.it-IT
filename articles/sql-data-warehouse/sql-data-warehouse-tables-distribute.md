---
title: aaaDistributing nelle tabelle SQL Data Warehouse | Documenti Microsoft
description: Introduzione alla distribuzione di tabelle in SQL Data Warehouse di Azure.
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: barbkess
editor: 
ms.assetid: 5ed4337f-7262-4ef6-8fd6-1809ce9634fc
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: tables
ms.date: 10/31/2016
ms.author: shigu;barbkess
ms.openlocfilehash: 65093eeaeb00fef85aaa6070da2c976fed3f4bbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="distributing-tables-in-sql-data-warehouse"></a>Distribuzione di tabelle in SQL Data Warehouse
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

SQL Data Warehouse è un sistema di database distribuito a elaborazione parallela massiva.  Suddividendo i dati e le funzionalità di elaborazione tra più nodi, SQL Data Warehouse offre grande scalabilità, ben oltre qualsiasi sistema singolo.  Decidere come toodistribute i dati all'interno del Data Warehouse di SQL sono uno dei più importante hello fattori tooachieving ottenere prestazioni ottimali.   prestazioni di chiave toooptimal Hello sono ridurre al minimo lo spostamento dei dati e a sua volta lo spostamento dei dati di chiave toominimizing hello seleziona la strategia di distribuzione corretto hello.

## <a name="understanding-data-movement"></a>Comprendere lo spostamento dei dati
In un sistema MPP, dati hello da ogni tabella sono suddiviso tra diversi database sottostanti.  query Hello più ottimizzata su un sistema MPP possono semplicemente essere trasmessi tramite tooexecute hello singoli database distribuiti senza l'intervento dell'hello tra gli altri database.  Ad esempio, si supponga di avere un database con dati di vendita che contiene due tabelle, per vendite e clienti.  Se si dispone di una query che deve toojoin la tabella di clienti tooyour tabella sales e si divide sia le tabelle e sulle vendite clienti backup per il numero di clienti, l'inserimento di ogni cliente in un database separato, tutte le query che uniscono vendite e clienti possano essere risolti all'interno di ogni database con alcuna conoscenza di hello altri database.  Al contrario, se i dati di vendita diviso per il numero di ordine e i dati cliente numero cliente, quindi uno specifico database senza dati corrispondenti hello per ogni cliente e pertanto se si desidera toojoin i dati sui clienti tooyour i dati di vendita, è necessario tooget hello dati per ogni cliente dalla hello altri database.  Nel secondo esempio, lo spostamento di dati necessario toooccur toomove hello cliente dati toohello dati di vendita, in modo che hello due tabelle possono essere unite in join.  

Lo spostamento dei dati non è sempre un aspetto negativo, in alcuni casi è necessario toosolve una query.  Quando tuttavia è possibile evitare questo passaggio supplementare, la query verrà naturalmente eseguita più velocemente.  In genere lo spostamento dei dati si verifica quando le tabelle vengono unite in join o vengono eseguite aggregazioni.  Spesso è necessario toodo entrambi, in modo mentre è in grado di toooptimize per uno scenario, ad esempio un join, è comunque necessario toohelp lo spostamento dei dati per risolvere per hello altro scenario, ad esempio un'aggregazione.  stratagemma Hello è scoprire che è minore di lavoro.  Nella maggior parte dei casi, la distribuzione delle tabelle dei fatti di grandi dimensioni in una colonna normalmente unite in join è hello metodo più efficace per ridurre hello la maggior parte dello spostamento dei dati.  Distribuzione dei dati nelle colonne join è un molto più comune di metodo tooreduce lo spostamento dei dati rispetto alla distribuzione di dati nelle colonne coinvolte in un'aggregazione.

## <a name="select-distribution-method"></a>Selezionare il metodo di distribuzione
Dietro le quinte hello SQL Data Warehouse divide i dati in 60 database.  Ogni singolo database è tooas di cui si fa riferimento un **distribuzione**.  Quando i dati vengono caricati in ogni tabella, SQL Data Warehouse ha tooknow come toodivide i dati in queste 60 distribuzioni.  

metodo di distribuzione Hello è definito a livello di tabella hello e attualmente sono disponibili due opzioni:

1. **Round robin** , che distribuisce i dati in modo uniforme ma casuale.
2. **Distribuzione hash** , che distribuisce i dati in base ai valori hash di una singola colonna.

Per impostazione predefinita, quando si definisce un metodo di distribuzione di dati, la tabella verrà distribuita tramite hello **round robin** metodo di distribuzione.  Tuttavia, dopo aver acquisito più sofisticati nell'implementazione, è tooconsider utilizzando **hash distribuita** tabelle toominimize lo spostamento dei dati che a sua volta consente di ottimizzare le prestazioni delle query.

### <a name="round-robin-tables"></a>Tabelle round robin
Utilizzo di hello metodo Round Robin di distribuzione dei dati è molto come sembra.  I dati vengono caricati, ogni riga viene semplicemente inviato toohello successiva distribuzione.  Questo metodo di distribuzione dei dati hello distribuirà sempre in modo casuale dati hello molto in modo uniforme in tutte le distribuzioni di hello.  Non vi è alcun ordinamento eseguite durante hello round robin processo che inserisce i dati.  Per questo motivo, una distribuzione round robin viene a volte definita hash causale.  Con una tabella di round robin distribuita non contiene dati di hello toounderstand di necessità.  Per questo motivo le tabelle round robin sono spesso un'ottima scelta come destinazioni di caricamento.

Per impostazione predefinita, se nessun metodo di distribuzione scelto, hello metodo distribuzione round robin verrà utilizzato.  Tuttavia, mentre il round robin tabelle sono toouse facile, perché in modo casuale i dati vengono distribuiti attraverso il sistema hello che significa che il sistema di hello non può garantire quali distribuzione ogni riga è in.  Come un risultato di un sistema hello talvolta tooinvoke un toobetter di operazione di spostamento dati è necessario organizzare i dati prima che possa risolvere una query.  Questo passaggio aggiuntivo può rallentare le query.

Utilizzare la distribuzione Round Robin per la tabella in hello seguenti scenari:

* Quando si inizia come punto di partenza semplice.
* Se non è presente una chiave di join ovvia.
* Se non è presente la colonna buon candidato per la distribuzione di tabella hello hash
* Se hello tabella non condivide una chiave di join comune con altre tabelle
* Se il join hello è meno significativo di altri join nella query hello
* Quando la tabella hello è una tabella temporanea di gestione temporanea

Entrambi gli esempi seguenti creano una tabella round robin:

```SQL
-- Round Robin created by default
CREATE TABLE [dbo].[FactInternetSales]
(   [ProductKey]            int          NOT NULL
,   [OrderDateKey]          int          NOT NULL
,   [CustomerKey]           int          NOT NULL
,   [PromotionKey]          int          NOT NULL
,   [SalesOrderNumber]      nvarchar(20) NOT NULL
,   [OrderQuantity]         smallint     NOT NULL
,   [UnitPrice]             money        NOT NULL
,   [SalesAmount]           money        NOT NULL
)
;

-- Explicitly Created Round Robin Table
CREATE TABLE [dbo].[FactInternetSales]
(   [ProductKey]            int          NOT NULL
,   [OrderDateKey]          int          NOT NULL
,   [CustomerKey]           int          NOT NULL
,   [PromotionKey]          int          NOT NULL
,   [SalesOrderNumber]      nvarchar(20) NOT NULL
,   [OrderQuantity]         smallint     NOT NULL
,   [UnitPrice]             money        NOT NULL
,   [SalesAmount]           money        NOT NULL
)
WITH
(   CLUSTERED COLUMNSTORE INDEX
,   DISTRIBUTION = ROUND_ROBIN
)
;
```

> [!NOTE]
> Mentre il round robin è di tipo di tabella predefinito hello è esplicito nell'istruzione DDL è considerata buona norma in modo da deselezionare tooothers intenzioni hello del layout tabella.
>
>

### <a name="hash-distributed-tables"></a>Tabelle con distribuzione hash
Utilizzando un **Hash distribuita** toodistribute algoritmo delle tabelle è possono migliorare le prestazioni per molti scenari riducendo lo spostamento dei dati in fase di query.  Hash distribuite sono tabelle che sono divise tra hello distribuiti database utilizzando un algoritmo di hash su una singola colonna che può essere selezionato.  colonna di distribuzione Hello è determina la modalità di suddivisione dati hello tra i database distribuiti.  funzione hash Hello utilizza hello distribuzione colonna tooassign righe toodistributions.  algoritmo di hash Hello e distribuzione risulta è deterministica.  Vale a dire hello stesso valore con tipo di dati verrà sempre hello è toohello stessa distribuzione.    

Questo esempio permette di creare una tabella distribuita:

```SQL
CREATE TABLE [dbo].[FactInternetSales]
(   [ProductKey]            int          NOT NULL
,   [OrderDateKey]          int          NOT NULL
,   [CustomerKey]           int          NOT NULL
,   [PromotionKey]          int          NOT NULL
,   [SalesOrderNumber]      nvarchar(20) NOT NULL
,   [OrderQuantity]         smallint     NOT NULL
,   [UnitPrice]             money        NOT NULL
,   [SalesAmount]           money        NOT NULL
)
WITH
(   CLUSTERED COLUMNSTORE INDEX
,  DISTRIBUTION = HASH([ProductKey])
)
;
```

## <a name="select-distribution-column"></a>Selezionare la colonna di distribuzione
Quando si sceglie troppo**hash distribuire** una tabella, sarà necessario tooselect una colonna singola distribuzione.  Quando si seleziona una colonna di distribuzione, sono disponibili tre tooconsider alcuni dei fattori principali.  

Selezionare una singola colonna:

1. da non aggiornare,
2. per distribuire i dati in modo uniforme, evitando asimmetrie,
3. per ridurre al minimo lo spostamento dei dati.

### <a name="select-distribution-column-which-will-not-be-updated"></a>Selezionare una colonna di distribuzione da non aggiornare
Le colonne di distribuzione non sono aggiornabili. Occorre quindi selezionare una colonna con valori statici.  Se una colonna sarà necessario toobe aggiornato, non è in genere un candidato di distribuzione valide.  Se un caso in cui è necessario aggiornare una colonna di distribuzione, si possono eseguire innanzitutto l'eliminazione di riga hello e quindi inserendo una nuova riga.

### <a name="select-distribution-column-which-will-distribute-data-evenly"></a>Selezionare una colonna di distribuzione per distribuire i dati in modo uniforme
Dal momento che un sistema distribuito esegue solo il più rapidamente la distribuzione più lenta, è importante toodivide hello lavoro in modo uniforme tra distribuzioni hello in ordine tooachieve bilanciato esecuzione attraverso il sistema hello.  modo Hello lavoro hello è suddivisa in un sistema distribuito è basato su dove si trovano dati hello per ogni distribuzione.  Questo rende una colonna di destra distribuzione hello tooselect molto importante per la distribuzione dei dati di hello in modo che ogni distribuzione ha lavoro uguale e verrà take hello toocomplete tempo stesso la propria parte del lavoro hello.  Quando lavoro viene diviso e sistema hello, dati hello viene bilanciati tra le distribuzioni di hello.  Quando i dati non sono bilanciati in modo uniforme, si parla di **differenze di dati**.  

toodivide dati in modo uniforme ed evitare dati inclinazione, considerare i seguenti hello quando si seleziona la colonna di distribuzione:

1. Selezionare una colonna che contiene un numero significativo di valori distinct.
2. Evitare di distribuire dati in colonne con pochi valori distinti.
3. Evitare di distribuire dati in colonne con una frequenza elevata di valori Null.
4. Evitare di distribuire i dati in colonne data.

Poiché ogni valore con hash too1 delle distribuzioni di 60, la distribuzione uniforme tooachieve è tooselect una colonna che è altamente univoco e contiene più di 60 valori univoci.  tooillustrate, si consideri il caso in cui una colonna dispone solo valori univoci 40.  Se questa colonna è stata selezionata come chiave di distribuzione hello, dati hello per la tabella verrebbero reindirizzato 40 distribuzioni al massimo, lasciando 20 distribuzioni con alcun dato e non toodo l'elaborazione.  Al contrario, hello altre 40 distribuzioni sarebbe necessario più lavoro toodo, che se hello dati è stata distribuiti uniformemente le distribuzioni di più di 60.  Questo scenario è un esempio di differenza di dati.

Nel sistema MPP, ogni passaggio della query è in attesa per tutte le distribuzioni toocomplete della quota di lavoro hello.  Se una distribuzione è più operazioni rispetto ad altri utenti hello, hello risorse di hello altre distribuzioni sono essenzialmente sprecati in attesa solo su distribuzione occupato hello.  Quando si lavoro non viene distribuito uniformemente tra tutte le distribuzioni, si parla di **differenza di elaborazioni**.  Elaborazione inclinazione causerà toorun query inferiore se il carico di lavoro hello può essere distribuito uniformemente in distribuzioni hello.  Lo sfasamento dei segnali dati comporti tooprocessing inclinazione.

Evitare di distribuire nella colonna elevata ammette valori null come valori null hello verranno tutte inserite in hello stessa distribuzione. La distribuzione di una colonna della data può essere causato anche l'elaborazione di inclinazione perché tutti i dati per una data specificata verranno inserite in hello stessa distribuzione. Se più utenti eseguono query filtraggio tutti in hello stessa data, quindi solo 1 delle distribuzioni di 60 hello prevede di effettuare tutto il lavoro hello dopo una data specificata verranno solo su una distribuzione. In questo scenario, le query hello probabilmente eseguirà 60 volte inferiore se i dati di hello ugualmente sono stati distribuiti su tutte le distribuzioni di hello.

Quando non esiste alcuna colonna candidato ideale, quindi utilizzare round robin come metodo di distribuzione hello.

### <a name="select-distribution-column-which-will-minimize-data-movement"></a>Selezionare una colonna di distribuzione per ridurre al minimo lo spostamento dei dati
Ridurre al minimo lo spostamento di dati selezionando una colonna di destra distribuzione hello è una delle strategie più importanti di hello per ottimizzare le prestazioni del proprio SQL Data Warehouse.  In genere lo spostamento dei dati si verifica quando le tabelle vengono unite in join o vengono eseguite aggregazioni.  Le colonne usate nelle clausole `JOIN`, `GROUP BY`, `DISTINCT`, `OVER` e `HAVING` sono **ottimi** candidati per la distribuzione hash.

Hello d'altro canto, le colonne in hello `WHERE` eseguire clausola **non** effettuare per i candidati colonna hash valida perché limitano le distribuzioni partecipano a query hello, che causa l'elaborazione inclinazione.  Un buon esempio di una colonna che potrebbe essere tentati toodistribute, ma spesso può causare l'inclinazione di elaborazione è una colonna di date.

In generale, se si dispone di due tabelle dei fatti di grandi dimensioni interessate di frequente in un join, sarà possibile ottenere hello la maggior parte delle prestazioni tramite la distribuzione di entrambe le tabelle in una delle colonne di join hello.  Se si dispone di una tabella che non viene mai tooanother unita in join nella tabella dei fatti di grandi dimensioni, quindi cercare toocolumns che si trovano spesso in hello `GROUP BY` clausola.

Esistono alcuni criteri di chiave che devono essere soddisfatto tooavoid lo spostamento di dati durante un join:

1. Hello tabelle unite in join hello devono essere distribuito su hash **uno** di colonne hello che fanno parte di join hello.
2. i tipi di dati delle colonne di join hello Hello di entrambe le tabelle devono essere uguali.
3. colonne di Hello devono essere aggiunti con un operatore di uguaglianza.
4. Hello join tipo non può essere un `CROSS JOIN`.

## <a name="troubleshooting-data-skew"></a>Risoluzione dei problemi relativi alle asimmetrie dei dati
Quando i dati della tabella vengono distribuiti con metodo di distribuzione hash hello è possibile che alcune distribuzioni saranno sfasato toohave eccessivamente più dati rispetto ad altri. Eccessivi dati sfasamento del possono influire sulle prestazioni delle query, perché il risultato finale di hello di una query distribuita deve attendere toofinish distribuzione in esecuzione più lunga di hello. In base al grado hello di dati hello inclinazione che potrebbe essere necessario tooaddress.

### <a name="identifying-skew"></a>Identificazione dell'asimmetria dei dati
Tooidentify un modo semplice una tabella come asimmetrica è toouse `DBCC PDW_SHOWSPACEUSED`.  Si tratta di un modo molto rapido e semplice di toosee hello numero di righe della tabella che vengono archiviati in ognuna delle distribuzioni di hello 60 del database.  Tenere presente che per ottenere prestazioni più bilanciato hello, righe hello nella tabella distribuita devono essere suddivise in modo uniforme tra tutte le distribuzioni di hello.

```sql
-- Find data skew for a distributed table
DBCC PDW_SHOWSPACEUSED('dbo.FactInternetSales');
```

Tuttavia, se si esegue una query viste a gestione dinamica hello Azure SQL Data Warehouse (DMV) è possibile eseguire un'analisi più dettagliata.  toostart, creare la vista hello [dbo.vTableSizes] [ dbo.vTableSizes] visualizzare utilizzando hello SQL da [Cenni preliminari su tabella] [ Overview] articolo.  Una volta hello vista viene creata, eseguire questa query tooidentify quali tabelle presentano più di 10% dati inclinazione.

```sql
select *
from dbo.vTableSizes
where two_part_name in
    (
    select two_part_name
    from dbo.vTableSizes
    where row_count > 0
    group by two_part_name
    having min(row_count * 1.000)/max(row_count * 1.000) > .10
    )
order by two_part_name, row_count
;
```

### <a name="resolving-data-skew"></a>Risoluzione delle asimmetrie di distribuzione
Non tutti inclinazione è sufficiente toowarrant una correzione.  In alcuni casi, le prestazioni di hello di una tabella in alcune query possono annullare danni hello dei dati di inclinazione.  toodecide se è necessario risolvere i dati dello sfasamento dei segnali in una tabella, è necessario comprendere quanto possibile sui volumi di dati hello e query nel carico di lavoro.   Un modo toolook impatto hello di inclinazione è passaggi hello toouse hello [Query monitoraggio] [ Query Monitoring] articolo impatto hello toomonitor di inclinazione sulle prestazioni delle query e in particolare hello query lunghe toohow di impatto richiedere toocomplete in distribuzioni di singoli hello.

Distribuzione dei dati è una questione di ricerca hello giusto equilibrio riducendo al minimo lo sfasamento dei segnali dati e ridurre al minimo lo spostamento dei dati. Questi possono essere opposte obiettivi e talvolta potrebbe essere necessario tookeep dati inclinazione nello spostamento dei dati tooreduce di ordine. Ad esempio, quando la colonna di distribuzione hello è spesso hello condiviso colonna join e aggregazioni, si verrà essere riducendo al minimo lo spostamento dei dati. Hello c'è lo spostamento dei dati minimi hello superiore a quello previsto impatto hello di avere dati dello sfasamento dei segnali.

un tipico di Hello tooresolve dati inclinazione è toore-creare hello tabella con una colonna di distribuzione diverso. Poiché non esiste alcun modo toochange hello distribuzione colonna esistente, hello modo toochange hello distribuzione tabelle di una tabella è toorecreate con un [] [un'istruzione CTAS].  Di seguito sono riportati due esempi di risoluzione di distribuzioni asimmetriche dei dati:

### <a name="example-1-re-create-hello-table-with-a-new-distribution-column"></a>Esempio 1: Creare nuovamente la tabella hello con una nuova colonna di distribuzione
Questo esempio viene utilizzata [un'istruzione CTAS] [] toore-creare una tabella con una colonna di distribuzione hash diverso.

```sql
CREATE TABLE [dbo].[FactInternetSales_CustomerKey]
WITH (  CLUSTERED COLUMNSTORE INDEX
     ,  DISTRIBUTION =  HASH([CustomerKey])
     ,  PARTITION       ( [OrderDateKey] RANGE RIGHT FOR VALUES (   20000101, 20010101, 20020101, 20030101
                                                                ,   20040101, 20050101, 20060101, 20070101
                                                                ,   20080101, 20090101, 20100101, 20110101
                                                                ,   20120101, 20130101, 20140101, 20150101
                                                                ,   20160101, 20170101, 20180101, 20190101
                                                                ,   20200101, 20210101, 20220101, 20230101
                                                                ,   20240101, 20250101, 20260101, 20270101
                                                                ,   20280101, 20290101
                                                                )
                        )
    )
AS
SELECT  *
FROM    [dbo].[FactInternetSales]
OPTION  (LABEL  = 'CTAS : FactInternetSales_CustomerKey')
;

--Create statistics on new table
CREATE STATISTICS [ProductKey] ON [FactInternetSales_CustomerKey] ([ProductKey]);
CREATE STATISTICS [OrderDateKey] ON [FactInternetSales_CustomerKey] ([OrderDateKey]);
CREATE STATISTICS [CustomerKey] ON [FactInternetSales_CustomerKey] ([CustomerKey]);
CREATE STATISTICS [PromotionKey] ON [FactInternetSales_CustomerKey] ([PromotionKey]);
CREATE STATISTICS [SalesOrderNumber] ON [FactInternetSales_CustomerKey] ([SalesOrderNumber]);
CREATE STATISTICS [OrderQuantity] ON [FactInternetSales_CustomerKey] ([OrderQuantity]);
CREATE STATISTICS [UnitPrice] ON [FactInternetSales_CustomerKey] ([UnitPrice]);
CREATE STATISTICS [SalesAmount] ON [FactInternetSales_CustomerKey] ([SalesAmount]);

--Rename hello tables
RENAME OBJECT [dbo].[FactInternetSales] too[FactInternetSales_ProductKey];
RENAME OBJECT [dbo].[FactInternetSales_CustomerKey] too[FactInternetSales];
```

### <a name="example-2-re-create-hello-table-using-round-robin-distribution"></a>Esempio 2: Creare nuovamente tabella hello utilizzando la distribuzione round robin
Questo esempio viene utilizzata [un'istruzione CTAS] [] toore-creare una tabella con round robin anziché una distribuzione di hash. Questa modifica provocherà la distribuzione di dati anche a costo di hello spostamento dei dati maggiore.

```sql
CREATE TABLE [dbo].[FactInternetSales_ROUND_ROBIN]
WITH (  CLUSTERED COLUMNSTORE INDEX
     ,  DISTRIBUTION =  ROUND_ROBIN
     ,  PARTITION       ( [OrderDateKey] RANGE RIGHT FOR VALUES (   20000101, 20010101, 20020101, 20030101
                                                                ,   20040101, 20050101, 20060101, 20070101
                                                                ,   20080101, 20090101, 20100101, 20110101
                                                                ,   20120101, 20130101, 20140101, 20150101
                                                                ,   20160101, 20170101, 20180101, 20190101
                                                                ,   20200101, 20210101, 20220101, 20230101
                                                                ,   20240101, 20250101, 20260101, 20270101
                                                                ,   20280101, 20290101
                                                                )
                        )
    )
AS
SELECT  *
FROM    [dbo].[FactInternetSales]
OPTION  (LABEL  = 'CTAS : FactInternetSales_ROUND_ROBIN')
;

--Create statistics on new table
CREATE STATISTICS [ProductKey] ON [FactInternetSales_ROUND_ROBIN] ([ProductKey]);
CREATE STATISTICS [OrderDateKey] ON [FactInternetSales_ROUND_ROBIN] ([OrderDateKey]);
CREATE STATISTICS [CustomerKey] ON [FactInternetSales_ROUND_ROBIN] ([CustomerKey]);
CREATE STATISTICS [PromotionKey] ON [FactInternetSales_ROUND_ROBIN] ([PromotionKey]);
CREATE STATISTICS [SalesOrderNumber] ON [FactInternetSales_ROUND_ROBIN] ([SalesOrderNumber]);
CREATE STATISTICS [OrderQuantity] ON [FactInternetSales_ROUND_ROBIN] ([OrderQuantity]);
CREATE STATISTICS [UnitPrice] ON [FactInternetSales_ROUND_ROBIN] ([UnitPrice]);
CREATE STATISTICS [SalesAmount] ON [FactInternetSales_ROUND_ROBIN] ([SalesAmount]);

--Rename hello tables
RENAME OBJECT [dbo].[FactInternetSales] too[FactInternetSales_HASH];
RENAME OBJECT [dbo].[FactInternetSales_ROUND_ROBIN] too[FactInternetSales];
```

## <a name="next-steps"></a>Passaggi successivi
toolearn ulteriori informazioni su progettazione della tabella, vedere hello [Distribuisci][Distribute], [indice][Index], [partizione] [ Partition], [Tipi di dati][Data Types], [statistiche] [ Statistics] e [tabelle temporanee] [ Temporary] articoli.

Per una panoramica delle procedure consigliate, vedere [Procedure consigliate per SQL Data Warehouse][SQL Data Warehouse Best Practices].

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
[Query Monitoring]: ./sql-data-warehouse-manage-monitor.md
[dbo.vTableSizes]: ./sql-data-warehouse-tables-overview.md#table-size-queries

<!--MSDN references-->
[DBCC PDW_SHOWSPACEUSED()]: https://msdn.microsoft.com/library/mt204028.aspx

<!--Other Web references-->
