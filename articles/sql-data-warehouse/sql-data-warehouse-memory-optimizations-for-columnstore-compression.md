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
# <a name="maximizing-rowgroup-quality-for-columnstore"></a><span data-ttu-id="6e4b6-103">Ottimizzazione della qualità di un gruppo di righe per columnstore</span><span class="sxs-lookup"><span data-stu-id="6e4b6-103">Maximizing rowgroup quality for columnstore</span></span>

<span data-ttu-id="6e4b6-104">Qualità del gruppo di righe è determinato dal numero di hello di righe in un gruppo di righe.</span><span class="sxs-lookup"><span data-stu-id="6e4b6-104">Rowgroup quality is determined by hello number of rows in a rowgroup.</span></span> <span data-ttu-id="6e4b6-105">Ridurre i requisiti di memoria o aumentare hello memoria disponibile toomaximize hello numero di righe di che un indice columnstore comprime in ogni gruppo di righe.</span><span class="sxs-lookup"><span data-stu-id="6e4b6-105">Reduce memory requirements or increase hello available memory toomaximize hello number of rows a columnstore index compresses into each rowgroup.</span></span>  <span data-ttu-id="6e4b6-106">Utilizzare le frequenze di compressione tooimprove metodi e le prestazioni delle query per gli indici columnstore.</span><span class="sxs-lookup"><span data-stu-id="6e4b6-106">Use these methods tooimprove compression rates and query performance for columnstore indexes.</span></span>

## <a name="why-hello-rowgroup-size-matters"></a><span data-ttu-id="6e4b6-107">Importanza dimensioni rowgroup hello</span><span class="sxs-lookup"><span data-stu-id="6e4b6-107">Why hello rowgroup size matters</span></span>
<span data-ttu-id="6e4b6-108">Poiché un indice columnstore esegue l'analisi di una tabella eseguendo la scansione di segmenti di colonna del rowgroup singoli, aumenta il numero di hello di righe in ogni rowgroup migliora le prestazioni delle query.</span><span class="sxs-lookup"><span data-stu-id="6e4b6-108">Since a columnstore index scans a table by scanning column segments of individual rowgroups, maximizing hello number of rows in each rowgroup enhances query performance.</span></span> <span data-ttu-id="6e4b6-109">Quando rowgroup dispone di un numero elevato di righe, la compressione dei dati migliora ovvero sono meno tooread dati dal disco.</span><span class="sxs-lookup"><span data-stu-id="6e4b6-109">When rowgroups have a high number of rows, data compression improves which means there is less data tooread from disk.</span></span>

<span data-ttu-id="6e4b6-110">Per altre informazioni sui gruppi di righe, vedere [Descrizione degli indici columnstore](https://msdn.microsoft.com/library/gg492088.aspx).</span><span class="sxs-lookup"><span data-stu-id="6e4b6-110">For more information about rowgroups, see [Columnstore Indexes Guide](https://msdn.microsoft.com/library/gg492088.aspx).</span></span>

## <a name="target-size-for-rowgroups"></a><span data-ttu-id="6e4b6-111">Dimensioni di destinazione per i gruppi di righe</span><span class="sxs-lookup"><span data-stu-id="6e4b6-111">Target size for rowgroups</span></span>
<span data-ttu-id="6e4b6-112">Per ottimizzare le prestazioni delle query, obiettivo di hello è numero hello toomaximize di righe per rowgroup in un indice columnstore.</span><span class="sxs-lookup"><span data-stu-id="6e4b6-112">For best query performance, hello goal is toomaximize hello number of rows per rowgroup in a columnstore index.</span></span> <span data-ttu-id="6e4b6-113">Un gruppo di righe può avere un massimo di 1.048.576 righe.</span><span class="sxs-lookup"><span data-stu-id="6e4b6-113">A rowgroup can have a maximum of 1,048,576 rows.</span></span> <span data-ttu-id="6e4b6-114">È accettabile toonot sono hello massimo di righe per rowgroup.</span><span class="sxs-lookup"><span data-stu-id="6e4b6-114">It's okay toonot have hello maximum number of rows per rowgroup.</span></span> <span data-ttu-id="6e4b6-115">Gli indici columnstore ottengono buone prestazioni quando i gruppi di righe hanno almeno 100.000 righe.</span><span class="sxs-lookup"><span data-stu-id="6e4b6-115">Columnstore indexes achieve good performance when rowgroups have at least 100,000 rows.</span></span>

## <a name="rowgroups-can-get-trimmed-during-compression"></a><span data-ttu-id="6e4b6-116">I gruppi di righe possono essere tagliati durante la compressione</span><span class="sxs-lookup"><span data-stu-id="6e4b6-116">Rowgroups can get trimmed during compression</span></span>

<span data-ttu-id="6e4b6-117">Durante una ricompilazione dell'indice columnstore o di caricamento bulk, in alcuni casi non è sufficiente toocompress di memoria disponibile che tutte hello righe designate per ogni rowgroup.</span><span class="sxs-lookup"><span data-stu-id="6e4b6-117">During a bulk load or columnstore index rebuild, sometimes there isn't enough memory available toocompress all hello rows designated for each rowgroup.</span></span> <span data-ttu-id="6e4b6-118">Quando sono presenti richieste di memoria, gli indici columnstore trim dimensioni rowgroup hello in modo da poter eseguire correttamente la compressione ColumnStore hello.</span><span class="sxs-lookup"><span data-stu-id="6e4b6-118">When there is memory pressure, columnstore indexes trim hello rowgroup sizes so compression into hello columnstore can succeed.</span></span> 

<span data-ttu-id="6e4b6-119">Quando sono presenti righe toocompress almeno 10.000 di memoria insufficiente in ogni gruppo di righe, SQL Data Warehouse genera un errore.</span><span class="sxs-lookup"><span data-stu-id="6e4b6-119">When there is insufficient memory toocompress at least 10,000 rows into each rowgroup, SQL Data Warehouse generates an error.</span></span>

<span data-ttu-id="6e4b6-120">Per altre informazioni sul caricamento bulk, vedere [Caricamento bulk in un indice columnstore cluster](https://msdn.microsoft.com/en-us/library/dn935008.aspx#Bulk load into a clustered columnstore index).</span><span class="sxs-lookup"><span data-stu-id="6e4b6-120">For more information on bulk loading, see [Bulk load into a clustered columnstore index](https://msdn.microsoft.com/en-us/library/dn935008.aspx#Bulk load into a clustered columnstore index).</span></span>

## <a name="how-toomonitor-rowgroup-quality"></a><span data-ttu-id="6e4b6-121">Come toomonitor rowgroup qualità</span><span class="sxs-lookup"><span data-stu-id="6e4b6-121">How toomonitor rowgroup quality</span></span>

<span data-ttu-id="6e4b6-122">Non vi è una DMV (sys.dm_pdw_nodes_db_column_store_row_group_physical_stats) che espone informazioni utili, ad esempio numero di righe nel rowgroup e hello motivo per la rimozione se vi è stata l'eliminazione.</span><span class="sxs-lookup"><span data-stu-id="6e4b6-122">There is a DMV (sys.dm_pdw_nodes_db_column_store_row_group_physical_stats) that exposes useful information such as number of rows in rowgroups and hello reason for trimming if there was trimming.</span></span> <span data-ttu-id="6e4b6-123">È possibile creare queste informazioni tooget DMV hello seguente visualizza come un modo pratico di tooquery nel rowgroup taglio.</span><span class="sxs-lookup"><span data-stu-id="6e4b6-123">You can create hello following view as a handy way tooquery this DMV tooget information on rowgroup trimming.</span></span>

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

<span data-ttu-id="6e4b6-124">Hello trim_reason_desc indica se è stati tagliati hello rowgroup (trim_reason_desc = NO_TRIM implica non vi è alcuna operazione di taglio e gruppo di righe di qualità eccellente).</span><span class="sxs-lookup"><span data-stu-id="6e4b6-124">hello trim_reason_desc tells whether hello rowgroup was trimmed(trim_reason_desc = NO_TRIM implies there was no trimming and row group is of optimal quality).</span></span> <span data-ttu-id="6e4b6-125">Hello motivi trim seguenti indicano taglio prematura del gruppo di righe hello:</span><span class="sxs-lookup"><span data-stu-id="6e4b6-125">hello following trim reasons indicate premature trimming of hello rowgroup:</span></span>
- <span data-ttu-id="6e4b6-126">BULKLOAD: Questo motivo trim viene utilizzato quando il batch in ingresso hello di righe per il carico hello era minore di 1 milione di righe.</span><span class="sxs-lookup"><span data-stu-id="6e4b6-126">BULKLOAD: This trim reason is used when hello incoming batch of rows for hello load had less than 1 million rows.</span></span> <span data-ttu-id="6e4b6-127">motore Hello crea gruppi di righe compresso se sono presenti più di 100.000 righe da inserire (come tooinserting anziché nell'archivio delta hello) ma set hello tooBULKLOAD motivo trim.</span><span class="sxs-lookup"><span data-stu-id="6e4b6-127">hello engine will create compressed row groups if there are greater than 100,000 rows being inserted (as opposed tooinserting into hello delta store) but sets hello trim reason tooBULKLOAD.</span></span> <span data-ttu-id="6e4b6-128">In questo scenario, è consigliabile aumentare la tooaccumulate di finestra carico batch più righe.</span><span class="sxs-lookup"><span data-stu-id="6e4b6-128">In this scenario, consider increasing your batch load window tooaccumulate more rows.</span></span> <span data-ttu-id="6e4b6-129">Inoltre, valutare di nuovo il partizionamento tooensure schema e non è troppo granulare come gruppi di righe non possono essere estesi dei limiti delle partizioni.</span><span class="sxs-lookup"><span data-stu-id="6e4b6-129">Also, reevaluate your partitioning scheme tooensure it is not too granular as row groups cannot span partition boundaries.</span></span>
- <span data-ttu-id="6e4b6-130">MEMORY_LIMITATION: gruppi di righe toocreate con 1 milione di righe, una certa quantità di memoria di lavoro è richiesto dal motore di hello.</span><span class="sxs-lookup"><span data-stu-id="6e4b6-130">MEMORY_LIMITATION: toocreate row groups with 1 million rows, a certain amount of working memory is required by hello engine.</span></span> <span data-ttu-id="6e4b6-131">Se la quantità di memoria disponibile durante il caricamento della sessione hello è inferiore al hello necessarie per l'utilizzo di memoria, gruppi di righe in modo anomalo ottengano rimosse.</span><span class="sxs-lookup"><span data-stu-id="6e4b6-131">When available memory of hello loading session is less than hello required working memory, row groups get prematurely trimmed.</span></span> <span data-ttu-id="6e4b6-132">Hello le sezioni seguenti illustrano come tooestimate memoria necessari e allocare altra memoria.</span><span class="sxs-lookup"><span data-stu-id="6e4b6-132">hello following sections explain how tooestimate memory required and allocate more memory.</span></span>
- <span data-ttu-id="6e4b6-133">DICTIONARY_SIZE: questo motivo indica che il gruppo di righe è stato tagliato perché era presente almeno una colonna di stringhe con stringhe "wide" e/o a cardinalità elevata.</span><span class="sxs-lookup"><span data-stu-id="6e4b6-133">DICTIONARY_SIZE: This trim reason indicates that rowgroup trimming occurred because there was at least one string column with wide and/or high cardinality strings.</span></span> <span data-ttu-id="6e4b6-134">dimensioni del dizionario Hello è limitato too16 MB in memoria e una volta raggiunto questo limite gruppo di righe hello è compresso.</span><span class="sxs-lookup"><span data-stu-id="6e4b6-134">hello dictionary size is limited too16 MB in memory and once this limit is reached hello row group is compressed.</span></span> <span data-ttu-id="6e4b6-135">Se si esegue questa situazione, isolare colonna problematico hello in una tabella distinta.</span><span class="sxs-lookup"><span data-stu-id="6e4b6-135">If you do run into this situation, consider isolating hello problematic column into a separate table.</span></span>

## <a name="how-tooestimate-memory-requirements"></a><span data-ttu-id="6e4b6-136">Come i requisiti di memoria tooestimate</span><span class="sxs-lookup"><span data-stu-id="6e4b6-136">How tooestimate memory requirements</span></span>

<!--
tooview an estimate of hello memory requirements toocompress a rowgroup of maximum size into a columnstore index, download and run hello view [dbo.vCS_mon_mem_grant](). This view shows hello size of hello memory grant that a rowgroup requires for compression in toohello columnstore.
-->

<span data-ttu-id="6e4b6-137">un rowgroup toocompress massima di memoria necessaria Hello è circa</span><span class="sxs-lookup"><span data-stu-id="6e4b6-137">hello maximum required memory toocompress one rowgroup is approximately</span></span>

- <span data-ttu-id="6e4b6-138">72 MB +</span><span class="sxs-lookup"><span data-stu-id="6e4b6-138">72 MB +</span></span>
- <span data-ttu-id="6e4b6-139">\#righe \* \#colonne \* 8 byte +</span><span class="sxs-lookup"><span data-stu-id="6e4b6-139">\#rows \* \#columns \* 8 bytes +</span></span>
- <span data-ttu-id="6e4b6-140">\#righe \*\#colonne stringa breve \* 32 byte +</span><span class="sxs-lookup"><span data-stu-id="6e4b6-140">\#rows \* \#short-string-columns \* 32 bytes +</span></span>
- <span data-ttu-id="6e4b6-141">\#colonne stringa lunga \* 16 MB per il dizionario di compressione</span><span class="sxs-lookup"><span data-stu-id="6e4b6-141">\#long-string-columns \* 16 MB for compression dictionary</span></span>

<span data-ttu-id="6e4b6-142">dove le colonne stringa breve usano tipi di dati stringa < = 32 byte e le colonne stringa lunga usano tipi di dati stringa > 32 byte.</span><span class="sxs-lookup"><span data-stu-id="6e4b6-142">where short-string-columns use string data types of <= 32 bytes and long-string-columns use string data types of > 32 bytes.</span></span>

<span data-ttu-id="6e4b6-143">Le stringhe lunghe vengono compresse con un metodo di compressione progettato per la compressione del testo.</span><span class="sxs-lookup"><span data-stu-id="6e4b6-143">Long strings are compressed with a compression method designed for compressing text.</span></span> <span data-ttu-id="6e4b6-144">Questo metodo di compressione Usa un *dizionario* toostore modelli di testo.</span><span class="sxs-lookup"><span data-stu-id="6e4b6-144">This compression method uses a *dictionary* toostore text patterns.</span></span> <span data-ttu-id="6e4b6-145">dimensione massima di Hello di un oggetto dictionary è 16 MB.</span><span class="sxs-lookup"><span data-stu-id="6e4b6-145">hello maximum size of a dictionary is 16 MB.</span></span> <span data-ttu-id="6e4b6-146">È presente un solo dizionario per ogni colonna stringa lunga hello rowgroup.</span><span class="sxs-lookup"><span data-stu-id="6e4b6-146">There is only one dictionary for each long string column in hello rowgroup.</span></span>

<span data-ttu-id="6e4b6-147">Per un'analisi approfondita dei requisiti di memoria columnstore, vedere il video [Azure SQL Data Warehouse scaling: configuration and guidance](https://myignite.microsoft.com/videos/14822) (Scalabilità di Azure SQL Data Warehouse: configurazione e linee guida).</span><span class="sxs-lookup"><span data-stu-id="6e4b6-147">For an in-depth discussion of columnstore memory requirements, see the video [Azure SQL Data Warehouse scaling: configuration and guidance](https://myignite.microsoft.com/videos/14822).</span></span>

## <a name="ways-tooreduce-memory-requirements"></a><span data-ttu-id="6e4b6-148">Requisiti di memoria tooreduce modi</span><span class="sxs-lookup"><span data-stu-id="6e4b6-148">Ways tooreduce memory requirements</span></span>

<span data-ttu-id="6e4b6-149">Utilizzare hello seguenti tecniche tooreduce hello i requisiti di memoria per la compressione di gruppi di righe in indici columnstore.</span><span class="sxs-lookup"><span data-stu-id="6e4b6-149">Use hello following techniques tooreduce hello memory requirements for compressing rowgroups into columnstore indexes.</span></span>

### <a name="use-fewer-columns"></a><span data-ttu-id="6e4b6-150">Usare meno colonne</span><span class="sxs-lookup"><span data-stu-id="6e4b6-150">Use fewer columns</span></span>
<span data-ttu-id="6e4b6-151">Se possibile, progettare la tabella hello con un numero di colonne.</span><span class="sxs-lookup"><span data-stu-id="6e4b6-151">If possible, design hello table with fewer columns.</span></span> <span data-ttu-id="6e4b6-152">Quando un rowgroup viene compresso nel columnstore hello, indice columnstore hello comprime separatamente ogni segmento di colonna.</span><span class="sxs-lookup"><span data-stu-id="6e4b6-152">When a rowgroup is compressed into hello columnstore, hello columnstore index compresses each column segment separately.</span></span> <span data-ttu-id="6e4b6-153">Hello pertanto i requisiti di memoria aumenta toocompress un gruppo di righe come hello aumentare del numero di colonne.</span><span class="sxs-lookup"><span data-stu-id="6e4b6-153">Therefore hello memory requirements toocompress a rowgroup increase as hello number of columns increases.</span></span>


### <a name="use-fewer-string-columns"></a><span data-ttu-id="6e4b6-154">Usare meno colonne di stringhe</span><span class="sxs-lookup"><span data-stu-id="6e4b6-154">Use fewer string columns</span></span>
<span data-ttu-id="6e4b6-155">Le colonne di dati di tipo stringa richiedono una quantità di memoria maggiore rispetto ai tipi di dati numerici.</span><span class="sxs-lookup"><span data-stu-id="6e4b6-155">Columns of string data types require more memory than numeric and date data types.</span></span> <span data-ttu-id="6e4b6-156">requisiti di memoria tooreduce, prendere in considerazione la rimozione di colonne di tipo stringa dalle tabelle dei fatti e inserendole in tabelle di dimensioni più piccole.</span><span class="sxs-lookup"><span data-stu-id="6e4b6-156">tooreduce memory requirements, consider removing string columns from fact tables and putting them in smaller dimension tables.</span></span>

<span data-ttu-id="6e4b6-157">Requisiti di memoria aggiuntivi per la compressione di stringhe:</span><span class="sxs-lookup"><span data-stu-id="6e4b6-157">Additional memory requirements for string compression:</span></span>

- <span data-ttu-id="6e4b6-158">Tipi di dati stringa di caratteri too32 possono richiedere 32 byte aggiuntivi per ogni valore.</span><span class="sxs-lookup"><span data-stu-id="6e4b6-158">String data types up too32 characters can require 32 additional bytes per value.</span></span>
- <span data-ttu-id="6e4b6-159">I tipi di dati stringa con più di 32 caratteri vengono compressi mediante metodi di dizionario.</span><span class="sxs-lookup"><span data-stu-id="6e4b6-159">String data types with more than 32 characters are compressed using dictionary methods.</span></span>  <span data-ttu-id="6e4b6-160">Ogni colonna nel gruppo di righe hello può richiedere di dizionario hello toobuild tooan aggiuntivo 16 MB.</span><span class="sxs-lookup"><span data-stu-id="6e4b6-160">Each column in hello rowgroup can require up tooan additional 16 MB toobuild hello dictionary.</span></span>

### <a name="avoid-over-partitioning"></a><span data-ttu-id="6e4b6-161">Evitare il partizionamento eccessivo</span><span class="sxs-lookup"><span data-stu-id="6e4b6-161">Avoid over-partitioning</span></span>

<span data-ttu-id="6e4b6-162">Gli indici columnstore creano uno o più gruppi di righe per partizione.</span><span class="sxs-lookup"><span data-stu-id="6e4b6-162">Columnstore indexes create one or more rowgroups per partition.</span></span> <span data-ttu-id="6e4b6-163">In SQL Data Warehouse, hello partizioni aumentare del numero di rapidamente perché hello dati vengono distribuiti e viene partizionata in ogni distribuzione.</span><span class="sxs-lookup"><span data-stu-id="6e4b6-163">In SQL Data Warehouse, hello number of partitions grows quickly because hello data is distributed and each distribution is partitioned.</span></span> <span data-ttu-id="6e4b6-164">Se nella tabella hello sono un numero eccessivo di partizioni, potrebbe non esserci sufficiente rowgroup hello toofill di righe.</span><span class="sxs-lookup"><span data-stu-id="6e4b6-164">If hello table has too many partitions, there might not be enough rows toofill hello rowgroups.</span></span> <span data-ttu-id="6e4b6-165">mancanza di Hello di righe non creano richieste di memoria durante la compressione, ma tale operazione comporta toorowgroups che non consentono di ottenere migliori prestazioni di query columnstore hello.</span><span class="sxs-lookup"><span data-stu-id="6e4b6-165">hello lack of rows does not create memory pressure during compression, but it leads toorowgroups that do not achieve hello best columnstore query performance.</span></span>

<span data-ttu-id="6e4b6-166">Un altro motivo tooavoid eccessiva partizionamento è presente un overhead di memoria per il caricamento delle righe in un indice columnstore in una tabella partizionata.</span><span class="sxs-lookup"><span data-stu-id="6e4b6-166">Another reason tooavoid over-partitioning is there is a memory overhead for loading rows into a columnstore index on a partitioned table.</span></span> <span data-ttu-id="6e4b6-167">Durante il caricamento, numero di partizioni può ricevere righe hello in arrivo, vengono mantenute in memoria fino a quando ogni partizione dispone di sufficiente toobe righe compressi.</span><span class="sxs-lookup"><span data-stu-id="6e4b6-167">During a load, many partitions could receive hello incoming rows, which are held in memory until each partition has enough rows toobe compressed.</span></span> <span data-ttu-id="6e4b6-168">Con un numero eccessivo di partizioni vengono create richieste di memoria aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="6e4b6-168">Having too many partitions creates additional memory pressure.</span></span>

### <a name="simplify-hello-load-query"></a><span data-ttu-id="6e4b6-169">Semplificare la query carico hello</span><span class="sxs-lookup"><span data-stu-id="6e4b6-169">Simplify hello load query</span></span>

<span data-ttu-id="6e4b6-170">database Hello condivide hello concessione di memoria per una query tra tutti gli operatori hello query hello.</span><span class="sxs-lookup"><span data-stu-id="6e4b6-170">hello database shares hello memory grant for a query among all hello operators in hello query.</span></span> <span data-ttu-id="6e4b6-171">Quando una query di carico contiene tipi complessi e join, viene ridotto memoria hello disponibile per la compressione.</span><span class="sxs-lookup"><span data-stu-id="6e4b6-171">When a load query has complex sorts and joins, hello memory available for compression is reduced.</span></span>

<span data-ttu-id="6e4b6-172">Progettare hello carico query toofocus solo sul caricamento query hello.</span><span class="sxs-lookup"><span data-stu-id="6e4b6-172">Design hello load query toofocus only on loading hello query.</span></span> <span data-ttu-id="6e4b6-173">Se è necessario toorun trasformazioni ai dati di hello, eseguirli separato dalla query carico hello.</span><span class="sxs-lookup"><span data-stu-id="6e4b6-173">If you need toorun transformations on hello data, run them separate from hello load query.</span></span> <span data-ttu-id="6e4b6-174">Ad esempio, organizzare i dati in una tabella heap, hello eseguire trasformazioni hello e quindi caricare hello tabella di gestione temporanea in indici columnstore hello.</span><span class="sxs-lookup"><span data-stu-id="6e4b6-174">For example, stage hello data in a heap table, run hello transformations, and then load hello staging table into hello columnstore index.</span></span> <span data-ttu-id="6e4b6-175">È possibile inoltre caricare innanzitutto i dati di hello e quindi utilizzare hello MPP sistema tootransform hello dati.</span><span class="sxs-lookup"><span data-stu-id="6e4b6-175">You can also load hello data first and then use hello MPP system tootransform hello data.</span></span>

### <a name="adjust-maxdop"></a><span data-ttu-id="6e4b6-176">Regolare MAXDOP</span><span class="sxs-lookup"><span data-stu-id="6e4b6-176">Adjust MAXDOP</span></span>

<span data-ttu-id="6e4b6-177">Ogni distribuzione comprime i rowgroup in columnstore hello in parallelo quando più di un core di CPU disponibile per ogni distribuzione.</span><span class="sxs-lookup"><span data-stu-id="6e4b6-177">Each distribution compresses rowgroups into hello columnstore in parallel when there is more than one CPU core available per distribution.</span></span> <span data-ttu-id="6e4b6-178">parallelismo Hello richiede risorse di memoria aggiuntiva, causando la pressione toomemory e la rimozione di rowgroup.</span><span class="sxs-lookup"><span data-stu-id="6e4b6-178">hello parallelism requires additional memory resources, which can lead toomemory pressure and rowgroup trimming.</span></span>

<span data-ttu-id="6e4b6-179">utilizzo della memoria tooreduce, è possibile utilizzare hello MAXDOP query hint tooforce hello carico operazione toorun in modalità seriale all'interno di ogni distribuzione.</span><span class="sxs-lookup"><span data-stu-id="6e4b6-179">tooreduce memory pressure, you can use hello MAXDOP query hint tooforce hello load operation toorun in serial mode within each distribution.</span></span>

```
CREATE TABLE MyFactSalesQuota
WITH (DISTRIBUTION = ROUND_ROBIN)
AS SELECT * FROM FactSalesQUota
OPTION (MAXDOP 1);
```

## <a name="ways-tooallocate-more-memory"></a><span data-ttu-id="6e4b6-180">Modi tooallocate maggiore quantità di memoria</span><span class="sxs-lookup"><span data-stu-id="6e4b6-180">Ways tooallocate more memory</span></span>

<span data-ttu-id="6e4b6-181">DWU hello dimensioni e la classe di risorse utente determinano la quantità di memoria è disponibile per una query dell'utente.</span><span class="sxs-lookup"><span data-stu-id="6e4b6-181">DWU size and hello user resource class together determine how much memory is available for a user query.</span></span> <span data-ttu-id="6e4b6-182">concessione di memoria hello tooincrease per una query del carico, è possibile aumentare il numero di hello di Dwu o aumentare la classe di risorse hello.</span><span class="sxs-lookup"><span data-stu-id="6e4b6-182">tooincrease hello memory grant for a load query, you can either increase hello number of DWUs or increase hello resource class.</span></span>

- <span data-ttu-id="6e4b6-183">vedere hello tooincrease Dwu, [come scalare prestazioni?](sql-data-warehouse-manage-compute-overview.md#scale-compute)</span><span class="sxs-lookup"><span data-stu-id="6e4b6-183">tooincrease hello DWUs, see [How do I scale performance?](sql-data-warehouse-manage-compute-overview.md#scale-compute)</span></span>
- <span data-ttu-id="6e4b6-184">classe di risorse hello toochange per una query, vedere [un esempio di classe di risorse utente di modificare](sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).</span><span class="sxs-lookup"><span data-stu-id="6e4b6-184">toochange hello resource class for a query, see [Change a user resource class example](sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).</span></span>

<span data-ttu-id="6e4b6-185">Ad esempio, su 100 DWU un utente nella classe della risorsa smallrc hello può utilizzare 100 MB di memoria per ogni distribuzione.</span><span class="sxs-lookup"><span data-stu-id="6e4b6-185">For example, on DWU 100 a user in hello smallrc resource class can use 100 MB of memory for each distribution.</span></span> <span data-ttu-id="6e4b6-186">Per informazioni dettagliate di hello, vedere [concorrenza in SQL Data Warehouse](sql-data-warehouse-develop-concurrency.md).</span><span class="sxs-lookup"><span data-stu-id="6e4b6-186">For hello details, see [Concurrency in SQL Data Warehouse](sql-data-warehouse-develop-concurrency.md).</span></span>

<span data-ttu-id="6e4b6-187">Si supponga che si determina che è necessario 700 MB di dimensioni di memoria tooget rowgroup di alta qualità.</span><span class="sxs-lookup"><span data-stu-id="6e4b6-187">Suppose you determine that you need 700 MB of memory tooget high-quality rowgroup sizes.</span></span> <span data-ttu-id="6e4b6-188">In questi esempi viene illustrato come eseguire query carico hello con memoria sufficiente.</span><span class="sxs-lookup"><span data-stu-id="6e4b6-188">These examples show how you can run hello load query with enough memory.</span></span>

- <span data-ttu-id="6e4b6-189">Usando la DWU 1000 e mediumrc, la concessione di memoria è di 800 MB</span><span class="sxs-lookup"><span data-stu-id="6e4b6-189">Using DWU 1000 and mediumrc, your memory grant is 800 MB</span></span>
- <span data-ttu-id="6e4b6-190">Usando la DWU 600 e largerc, la concessione di memoria è di 800 MB.</span><span class="sxs-lookup"><span data-stu-id="6e4b6-190">Using DWU 600 and largerc, your memory grant is 800 MB.</span></span>


## <a name="next-steps"></a><span data-ttu-id="6e4b6-191">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6e4b6-191">Next steps</span></span>

<span data-ttu-id="6e4b6-192">toofind prestazioni più elevate tooimprove modi in SQL Data Warehouse, vedere hello [Cenni preliminari sulle prestazioni](sql-data-warehouse-overview-manage-user-queries.md).</span><span class="sxs-lookup"><span data-stu-id="6e4b6-192">toofind more ways tooimprove performance in SQL Data Warehouse, see hello [Performance overview](sql-data-warehouse-overview-manage-user-queries.md).</span></span>

<!--Image references-->

<!--Article references-->


<!--MSDN references-->

<!--Other Web references-->
