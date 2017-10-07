---
title: prestazioni dell'indice columnstore aaaImprove in SQL Azure | Documenti Microsoft
description: Ridurre i requisiti di memoria o aumentare hello memoria disponibile toomaximize hello numero di righe di che un indice columnstore comprime in ogni gruppo di righe.
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: jhubbard
editor: 
ms.assetid: ef170f39-ae24-4b04-af76-53bb4c4d16d3
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: performance
ms.date: 6/2/2017
ms.author: shigu;barbkess
ms.openlocfilehash: 2c5a68435aa200236a2dc8538aa4638b52a59093
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="maximizing-rowgroup-quality-for-columnstore"></a>Ottimizzazione della qualità di un gruppo di righe per columnstore

Qualità del gruppo di righe è determinato dal numero di hello di righe in un gruppo di righe. Ridurre i requisiti di memoria o aumentare hello memoria disponibile toomaximize hello numero di righe di che un indice columnstore comprime in ogni gruppo di righe.  Utilizzare le frequenze di compressione tooimprove metodi e le prestazioni delle query per gli indici columnstore.

## <a name="why-hello-rowgroup-size-matters"></a>Importanza dimensioni rowgroup hello
Poiché un indice columnstore esegue l'analisi di una tabella eseguendo la scansione di segmenti di colonna del rowgroup singoli, aumenta il numero di hello di righe in ogni rowgroup migliora le prestazioni delle query. Quando rowgroup dispone di un numero elevato di righe, la compressione dei dati migliora ovvero sono meno tooread dati dal disco.

Per altre informazioni sui gruppi di righe, vedere [Descrizione degli indici columnstore](https://msdn.microsoft.com/library/gg492088.aspx).

## <a name="target-size-for-rowgroups"></a>Dimensioni di destinazione per i gruppi di righe
Per ottimizzare le prestazioni delle query, obiettivo di hello è numero hello toomaximize di righe per rowgroup in un indice columnstore. Un gruppo di righe può avere un massimo di 1.048.576 righe. È accettabile toonot sono hello massimo di righe per rowgroup. Gli indici columnstore ottengono buone prestazioni quando i gruppi di righe hanno almeno 100.000 righe.

## <a name="rowgroups-can-get-trimmed-during-compression"></a>I gruppi di righe possono essere tagliati durante la compressione

Durante una ricompilazione dell'indice columnstore o di caricamento bulk, in alcuni casi non è sufficiente toocompress di memoria disponibile che tutte hello righe designate per ogni rowgroup. Quando sono presenti richieste di memoria, gli indici columnstore trim dimensioni rowgroup hello in modo da poter eseguire correttamente la compressione ColumnStore hello. 

Quando sono presenti righe toocompress almeno 10.000 di memoria insufficiente in ogni gruppo di righe, SQL Data Warehouse genera un errore.

Per altre informazioni sul caricamento bulk, vedere [Caricamento bulk in un indice columnstore cluster](https://msdn.microsoft.com/en-us/library/dn935008.aspx#Bulk load into a clustered columnstore index).

## <a name="how-toomonitor-rowgroup-quality"></a>Come toomonitor rowgroup qualità

Non vi è una DMV (sys.dm_pdw_nodes_db_column_store_row_group_physical_stats) che espone informazioni utili, ad esempio numero di righe nel rowgroup e hello motivo per la rimozione se vi è stata l'eliminazione. È possibile creare queste informazioni tooget DMV hello seguente visualizza come un modo pratico di tooquery nel rowgroup taglio.

```sql
create view dbo.vCS_rg_physical_stats
as 
with cte
as
(
select   tb.[name]                    AS [logical_table_name]
,        rg.[row_group_id]            AS [row_group_id]
,        rg.[state]                   AS [state]
,        rg.[state_desc]              AS [state_desc]
,        rg.[total_rows]              AS [total_rows]
,        rg.[trim_reason_desc]        AS trim_reason_desc
,        mp.[physical_name]           AS physical_name
FROM    sys.[schemas] sm
JOIN    sys.[tables] tb               ON  sm.[schema_id]          = tb.[schema_id]                             
JOIN    sys.[pdw_table_mappings] mp   ON  tb.[object_id]          = mp.[object_id]
JOIN    sys.[pdw_nodes_tables] nt     ON  nt.[name]               = mp.[physical_name]
JOIN    sys.[dm_pdw_nodes_db_column_store_row_group_physical_stats] rg      ON  rg.[object_id]     = nt.[object_id]
                                                                            AND rg.[pdw_node_id]   = nt.[pdw_node_id]
                                        AND rg.[distribution_id]    = nt.[distribution_id]                                          
)
select *
from cte;
```

Hello trim_reason_desc indica se è stati tagliati hello rowgroup (trim_reason_desc = NO_TRIM implica non vi è alcuna operazione di taglio e gruppo di righe di qualità eccellente). Hello motivi trim seguenti indicano taglio prematura del gruppo di righe hello:
- BULKLOAD: Questo motivo trim viene utilizzato quando il batch in ingresso hello di righe per il carico hello era minore di 1 milione di righe. motore Hello crea gruppi di righe compresso se sono presenti più di 100.000 righe da inserire (come tooinserting anziché nell'archivio delta hello) ma set hello tooBULKLOAD motivo trim. In questo scenario, è consigliabile aumentare la tooaccumulate di finestra carico batch più righe. Inoltre, valutare di nuovo il partizionamento tooensure schema e non è troppo granulare come gruppi di righe non possono essere estesi dei limiti delle partizioni.
- MEMORY_LIMITATION: gruppi di righe toocreate con 1 milione di righe, una certa quantità di memoria di lavoro è richiesto dal motore di hello. Se la quantità di memoria disponibile durante il caricamento della sessione hello è inferiore al hello necessarie per l'utilizzo di memoria, gruppi di righe in modo anomalo ottengano rimosse. Hello le sezioni seguenti illustrano come tooestimate memoria necessari e allocare altra memoria.
- DICTIONARY_SIZE: questo motivo indica che il gruppo di righe è stato tagliato perché era presente almeno una colonna di stringhe con stringhe "wide" e/o a cardinalità elevata. dimensioni del dizionario Hello è limitato too16 MB in memoria e una volta raggiunto questo limite gruppo di righe hello è compresso. Se si esegue questa situazione, isolare colonna problematico hello in una tabella distinta.

## <a name="how-tooestimate-memory-requirements"></a>Come i requisiti di memoria tooestimate

<!--
tooview an estimate of hello memory requirements toocompress a rowgroup of maximum size into a columnstore index, download and run hello view [dbo.vCS_mon_mem_grant](). This view shows hello size of hello memory grant that a rowgroup requires for compression in toohello columnstore.
-->

un rowgroup toocompress massima di memoria necessaria Hello è circa

- 72 MB +
- \#righe \* \#colonne \* 8 byte +
- \#righe \*\#colonne stringa breve \* 32 byte +
- \#colonne stringa lunga \* 16 MB per il dizionario di compressione

dove le colonne stringa breve usano tipi di dati stringa < = 32 byte e le colonne stringa lunga usano tipi di dati stringa > 32 byte.

Le stringhe lunghe vengono compresse con un metodo di compressione progettato per la compressione del testo. Questo metodo di compressione Usa un *dizionario* toostore modelli di testo. dimensione massima di Hello di un oggetto dictionary è 16 MB. È presente un solo dizionario per ogni colonna stringa lunga hello rowgroup.

Per un'analisi approfondita dei requisiti di memoria columnstore, vedere il video [Azure SQL Data Warehouse scaling: configuration and guidance](https://myignite.microsoft.com/videos/14822) (Scalabilità di Azure SQL Data Warehouse: configurazione e linee guida).

## <a name="ways-tooreduce-memory-requirements"></a>Requisiti di memoria tooreduce modi

Utilizzare hello seguenti tecniche tooreduce hello i requisiti di memoria per la compressione di gruppi di righe in indici columnstore.

### <a name="use-fewer-columns"></a>Usare meno colonne
Se possibile, progettare la tabella hello con un numero di colonne. Quando un rowgroup viene compresso nel columnstore hello, indice columnstore hello comprime separatamente ogni segmento di colonna. Hello pertanto i requisiti di memoria aumenta toocompress un gruppo di righe come hello aumentare del numero di colonne.


### <a name="use-fewer-string-columns"></a>Usare meno colonne di stringhe
Le colonne di dati di tipo stringa richiedono una quantità di memoria maggiore rispetto ai tipi di dati numerici. requisiti di memoria tooreduce, prendere in considerazione la rimozione di colonne di tipo stringa dalle tabelle dei fatti e inserendole in tabelle di dimensioni più piccole.

Requisiti di memoria aggiuntivi per la compressione di stringhe:

- Tipi di dati stringa di caratteri too32 possono richiedere 32 byte aggiuntivi per ogni valore.
- I tipi di dati stringa con più di 32 caratteri vengono compressi mediante metodi di dizionario.  Ogni colonna nel gruppo di righe hello può richiedere di dizionario hello toobuild tooan aggiuntivo 16 MB.

### <a name="avoid-over-partitioning"></a>Evitare il partizionamento eccessivo

Gli indici columnstore creano uno o più gruppi di righe per partizione. In SQL Data Warehouse, hello partizioni aumentare del numero di rapidamente perché hello dati vengono distribuiti e viene partizionata in ogni distribuzione. Se nella tabella hello sono un numero eccessivo di partizioni, potrebbe non esserci sufficiente rowgroup hello toofill di righe. mancanza di Hello di righe non creano richieste di memoria durante la compressione, ma tale operazione comporta toorowgroups che non consentono di ottenere migliori prestazioni di query columnstore hello.

Un altro motivo tooavoid eccessiva partizionamento è presente un overhead di memoria per il caricamento delle righe in un indice columnstore in una tabella partizionata. Durante il caricamento, numero di partizioni può ricevere righe hello in arrivo, vengono mantenute in memoria fino a quando ogni partizione dispone di sufficiente toobe righe compressi. Con un numero eccessivo di partizioni vengono create richieste di memoria aggiuntive.

### <a name="simplify-hello-load-query"></a>Semplificare la query carico hello

database Hello condivide hello concessione di memoria per una query tra tutti gli operatori hello query hello. Quando una query di carico contiene tipi complessi e join, viene ridotto memoria hello disponibile per la compressione.

Progettare hello carico query toofocus solo sul caricamento query hello. Se è necessario toorun trasformazioni ai dati di hello, eseguirli separato dalla query carico hello. Ad esempio, organizzare i dati in una tabella heap, hello eseguire trasformazioni hello e quindi caricare hello tabella di gestione temporanea in indici columnstore hello. È possibile inoltre caricare innanzitutto i dati di hello e quindi utilizzare hello MPP sistema tootransform hello dati.

### <a name="adjust-maxdop"></a>Regolare MAXDOP

Ogni distribuzione comprime i rowgroup in columnstore hello in parallelo quando più di un core di CPU disponibile per ogni distribuzione. parallelismo Hello richiede risorse di memoria aggiuntiva, causando la pressione toomemory e la rimozione di rowgroup.

utilizzo della memoria tooreduce, è possibile utilizzare hello MAXDOP query hint tooforce hello carico operazione toorun in modalità seriale all'interno di ogni distribuzione.

```
CREATE TABLE MyFactSalesQuota
WITH (DISTRIBUTION = ROUND_ROBIN)
AS SELECT * FROM FactSalesQUota
OPTION (MAXDOP 1);
```

## <a name="ways-tooallocate-more-memory"></a>Modi tooallocate maggiore quantità di memoria

DWU hello dimensioni e la classe di risorse utente determinano la quantità di memoria è disponibile per una query dell'utente. concessione di memoria hello tooincrease per una query del carico, è possibile aumentare il numero di hello di Dwu o aumentare la classe di risorse hello.

- vedere hello tooincrease Dwu, [come scalare prestazioni?](sql-data-warehouse-manage-compute-overview.md#scale-compute)
- classe di risorse hello toochange per una query, vedere [un esempio di classe di risorse utente di modificare](sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).

Ad esempio, su 100 DWU un utente nella classe della risorsa smallrc hello può utilizzare 100 MB di memoria per ogni distribuzione. Per informazioni dettagliate di hello, vedere [concorrenza in SQL Data Warehouse](sql-data-warehouse-develop-concurrency.md).

Si supponga che si determina che è necessario 700 MB di dimensioni di memoria tooget rowgroup di alta qualità. In questi esempi viene illustrato come eseguire query carico hello con memoria sufficiente.

- Usando la DWU 1000 e mediumrc, la concessione di memoria è di 800 MB
- Usando la DWU 600 e largerc, la concessione di memoria è di 800 MB.


## <a name="next-steps"></a>Passaggi successivi

toofind prestazioni più elevate tooimprove modi in SQL Data Warehouse, vedere hello [Cenni preliminari sulle prestazioni](sql-data-warehouse-overview-manage-user-queries.md).

<!--Image references-->

<!--Article references-->


<!--MSDN references-->

<!--Other Web references-->
