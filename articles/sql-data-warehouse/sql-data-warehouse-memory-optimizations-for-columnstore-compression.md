---
title: Migliorare le prestazioni dell'indice columnstore in Azure SQL | Documentazione Microsoft
description: Ridurre i requisiti di memoria o aumentare la memoria disponibile per accrescere al massimo il numero di righe che un indice columnstore comprime in ogni gruppo di righe.
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
ms.openlocfilehash: f0e0b839b4a0c216eee2eb5134d43b91d8f83289
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="maximizing-rowgroup-quality-for-columnstore"></a><span data-ttu-id="ccb43-103">Ottimizzazione della qualità di un gruppo di righe per columnstore</span><span class="sxs-lookup"><span data-stu-id="ccb43-103">Maximizing rowgroup quality for columnstore</span></span>

<span data-ttu-id="ccb43-104">La qualità di un gruppo di righe è determinata dal numero di righe nel gruppo.</span><span class="sxs-lookup"><span data-stu-id="ccb43-104">Rowgroup quality is determined by the number of rows in a rowgroup.</span></span> <span data-ttu-id="ccb43-105">Ridurre i requisiti di memoria o aumentare la memoria disponibile per accrescere al massimo il numero di righe che un indice columnstore comprime in ogni gruppo di righe.</span><span class="sxs-lookup"><span data-stu-id="ccb43-105">Reduce memory requirements or increase the available memory to maximize the number of rows a columnstore index compresses into each rowgroup.</span></span>  <span data-ttu-id="ccb43-106">Usare questi metodi per migliorare il tasso di compressione e le prestazioni delle query per gli indici columnstore.</span><span class="sxs-lookup"><span data-stu-id="ccb43-106">Use these methods to improve compression rates and query performance for columnstore indexes.</span></span>

## <a name="why-the-rowgroup-size-matters"></a><span data-ttu-id="ccb43-107">Perché sono importanti le dimensioni del gruppo di righe</span><span class="sxs-lookup"><span data-stu-id="ccb43-107">Why the rowgroup size matters</span></span>
<span data-ttu-id="ccb43-108">Poiché un indice columnstore analizza una tabella eseguendo la scansione di segmenti di colonna di singoli gruppi di righe, accrescendo al massimo il numero di righe in ogni gruppo di righe le prestazioni delle query migliorano.</span><span class="sxs-lookup"><span data-stu-id="ccb43-108">Since a columnstore index scans a table by scanning column segments of individual rowgroups, maximizing the number of rows in each rowgroup enhances query performance.</span></span> <span data-ttu-id="ccb43-109">Quando i gruppi di righe hanno un numero elevato di righe, la compressione dei dati migliora, il che significa meno dati da leggere dal disco.</span><span class="sxs-lookup"><span data-stu-id="ccb43-109">When rowgroups have a high number of rows, data compression improves which means there is less data to read from disk.</span></span>

<span data-ttu-id="ccb43-110">Per altre informazioni sui gruppi di righe, vedere [Descrizione degli indici columnstore](https://msdn.microsoft.com/library/gg492088.aspx).</span><span class="sxs-lookup"><span data-stu-id="ccb43-110">For more information about rowgroups, see [Columnstore Indexes Guide](https://msdn.microsoft.com/library/gg492088.aspx).</span></span>

## <a name="target-size-for-rowgroups"></a><span data-ttu-id="ccb43-111">Dimensioni di destinazione per i gruppi di righe</span><span class="sxs-lookup"><span data-stu-id="ccb43-111">Target size for rowgroups</span></span>
<span data-ttu-id="ccb43-112">Per ottimizzare le prestazioni delle query, l'obiettivo è accrescere al massimo il numero di righe per ogni gruppo di righe in un indice columnstore.</span><span class="sxs-lookup"><span data-stu-id="ccb43-112">For best query performance, the goal is to maximize the number of rows per rowgroup in a columnstore index.</span></span> <span data-ttu-id="ccb43-113">Un gruppo di righe può avere un massimo di 1.048.576 righe.</span><span class="sxs-lookup"><span data-stu-id="ccb43-113">A rowgroup can have a maximum of 1,048,576 rows.</span></span> <span data-ttu-id="ccb43-114">È accettabile non avere il numero massimo di righe per gruppo di righe.</span><span class="sxs-lookup"><span data-stu-id="ccb43-114">It's okay to not have the maximum number of rows per rowgroup.</span></span> <span data-ttu-id="ccb43-115">Gli indici columnstore ottengono buone prestazioni quando i gruppi di righe hanno almeno 100.000 righe.</span><span class="sxs-lookup"><span data-stu-id="ccb43-115">Columnstore indexes achieve good performance when rowgroups have at least 100,000 rows.</span></span>

## <a name="rowgroups-can-get-trimmed-during-compression"></a><span data-ttu-id="ccb43-116">I gruppi di righe possono essere tagliati durante la compressione</span><span class="sxs-lookup"><span data-stu-id="ccb43-116">Rowgroups can get trimmed during compression</span></span>

<span data-ttu-id="ccb43-117">Durante un caricamento bulk o la ricompilazione di un indice columnstore, talvolta non è disponibile memoria sufficiente per comprimere tutte le righe per ogni gruppo di righe.</span><span class="sxs-lookup"><span data-stu-id="ccb43-117">During a bulk load or columnstore index rebuild, sometimes there isn't enough memory available to compress all the rows designated for each rowgroup.</span></span> <span data-ttu-id="ccb43-118">Quando la memoria disponibile è scarsa, gli indici columnstore riducono le dimensioni del gruppo di righe in modo da consentire la compressione nel columnstore.</span><span class="sxs-lookup"><span data-stu-id="ccb43-118">When there is memory pressure, columnstore indexes trim the rowgroup sizes so compression into the columnstore can succeed.</span></span> 

<span data-ttu-id="ccb43-119">Quando la memoria è insufficiente per la compressione di almeno 10.000 righe in ogni gruppo di righe, SQL Data Warehouse genera un errore.</span><span class="sxs-lookup"><span data-stu-id="ccb43-119">When there is insufficient memory to compress at least 10,000 rows into each rowgroup, SQL Data Warehouse generates an error.</span></span>

<span data-ttu-id="ccb43-120">Per altre informazioni sul caricamento bulk, vedere [Caricamento bulk in un indice columnstore cluster](https://msdn.microsoft.com/en-us/library/dn935008.aspx#Bulk load into a clustered columnstore index).</span><span class="sxs-lookup"><span data-stu-id="ccb43-120">For more information on bulk loading, see [Bulk load into a clustered columnstore index](https://msdn.microsoft.com/en-us/library/dn935008.aspx#Bulk load into a clustered columnstore index).</span></span>

## <a name="how-to-monitor-rowgroup-quality"></a><span data-ttu-id="ccb43-121">Come monitorare la qualità di un gruppo di righe</span><span class="sxs-lookup"><span data-stu-id="ccb43-121">How to monitor rowgroup quality</span></span>

<span data-ttu-id="ccb43-122">È presente una DMV (sys.dm_pdw_nodes_db_column_store_row_group_physical_stats) che espone informazioni utili come il numero di righe presenti nei gruppi ed eventualmente il motivo per cui un gruppo di righe è stato tagliato.</span><span class="sxs-lookup"><span data-stu-id="ccb43-122">There is a DMV (sys.dm_pdw_nodes_db_column_store_row_group_physical_stats) that exposes useful information such as number of rows in rowgroups and the reason for trimming if there was trimming.</span></span> <span data-ttu-id="ccb43-123">Per effettuare una query su questa DMV allo scopo di ottenere informazioni sul trimming di un gruppo di righe, è possibile creare la vista seguente.</span><span class="sxs-lookup"><span data-stu-id="ccb43-123">You can create the following view as a handy way to query this DMV to get information on rowgroup trimming.</span></span>

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

<span data-ttu-id="ccb43-124">trim_reason_desc specifica se il gruppo di righe è stato tagliato (trim_reason_desc = NO_TRIM indica che il gruppo di righe è di qualità ottimale e non è stato tagliato).</span><span class="sxs-lookup"><span data-stu-id="ccb43-124">The trim_reason_desc tells whether the rowgroup was trimmed(trim_reason_desc = NO_TRIM implies there was no trimming and row group is of optimal quality).</span></span> <span data-ttu-id="ccb43-125">I motivi seguenti indicano che il gruppo di righe è stato tagliato prematuramente:</span><span class="sxs-lookup"><span data-stu-id="ccb43-125">The following trim reasons indicate premature trimming of the rowgroup:</span></span>
- <span data-ttu-id="ccb43-126">BULKLOAD: questo motivo viene usato se il batch di righe in ingresso per il caricamento è inferiore a 1 milione di righe.</span><span class="sxs-lookup"><span data-stu-id="ccb43-126">BULKLOAD: This trim reason is used when the incoming batch of rows for the load had less than 1 million rows.</span></span> <span data-ttu-id="ccb43-127">Il motore creerà gruppi di righe compressi se devono essere inserite più di 100.000 righe (a differenza dell'inserimento nell'archivio differenziale), ma imposta il motivo per cui il gruppo è stato tagliato su BULKLOAD.</span><span class="sxs-lookup"><span data-stu-id="ccb43-127">The engine will create compressed row groups if there are greater than 100,000 rows being inserted (as opposed to inserting into the delta store) but sets the trim reason to BULKLOAD.</span></span> <span data-ttu-id="ccb43-128">In questo scenario, valutare l'opportunità di ampliare la finestra di caricamento in batch in modo da accumulare più righe.</span><span class="sxs-lookup"><span data-stu-id="ccb43-128">In this scenario, consider increasing your batch load window to accumulate more rows.</span></span> <span data-ttu-id="ccb43-129">Rivalutare inoltre lo schema di partizionamento per verificare che non sia troppo granulare e che i gruppi di righe non possano quindi estendersi oltre i limiti della partizione.</span><span class="sxs-lookup"><span data-stu-id="ccb43-129">Also, reevaluate your partitioning scheme to ensure it is not too granular as row groups cannot span partition boundaries.</span></span>
- <span data-ttu-id="ccb43-130">MEMORY_LIMITATION: per creare gruppi di righe con 1 milione di righe, il motore richiede una certa quantità di memoria di lavoro.</span><span class="sxs-lookup"><span data-stu-id="ccb43-130">MEMORY_LIMITATION: To create row groups with 1 million rows, a certain amount of working memory is required by the engine.</span></span> <span data-ttu-id="ccb43-131">Se la memoria disponibile nella sessione di caricamento è inferiore alla memoria di lavoro necessaria, i gruppi di righe vengono tagliati in modo prematuro.</span><span class="sxs-lookup"><span data-stu-id="ccb43-131">When available memory of the loading session is less than the required working memory, row groups get prematurely trimmed.</span></span> <span data-ttu-id="ccb43-132">Le sezioni seguenti illustrano come stimare la memoria necessaria e allocare memoria aggiuntiva.</span><span class="sxs-lookup"><span data-stu-id="ccb43-132">The following sections explain how to estimate memory required and allocate more memory.</span></span>
- <span data-ttu-id="ccb43-133">DICTIONARY_SIZE: questo motivo indica che il gruppo di righe è stato tagliato perché era presente almeno una colonna di stringhe con stringhe "wide" e/o a cardinalità elevata.</span><span class="sxs-lookup"><span data-stu-id="ccb43-133">DICTIONARY_SIZE: This trim reason indicates that rowgroup trimming occurred because there was at least one string column with wide and/or high cardinality strings.</span></span> <span data-ttu-id="ccb43-134">Le dimensioni del dizionario sono limitate a 16 MB di memoria e, al raggiungimento di questo limite, il gruppo di righe viene compresso.</span><span class="sxs-lookup"><span data-stu-id="ccb43-134">The dictionary size is limited to 16 MB in memory and once this limit is reached the row group is compressed.</span></span> <span data-ttu-id="ccb43-135">Se si verifica questa situazione, valutare l'opportunità di isolare la colonna problematica in una tabella separata.</span><span class="sxs-lookup"><span data-stu-id="ccb43-135">If you do run into this situation, consider isolating the problematic column into a separate table.</span></span>

## <a name="how-to-estimate-memory-requirements"></a><span data-ttu-id="ccb43-136">Come stimare i requisiti di memoria</span><span class="sxs-lookup"><span data-stu-id="ccb43-136">How to estimate memory requirements</span></span>

<!--
To view an estimate of the memory requirements to compress a rowgroup of maximum size into a columnstore index, download and run the view [dbo.vCS_mon_mem_grant](). This view shows the size of the memory grant that a rowgroup requires for compression in to the columnstore.
-->

<span data-ttu-id="ccb43-137">La memoria massima necessaria per comprimere un gruppo di righe è circa</span><span class="sxs-lookup"><span data-stu-id="ccb43-137">The maximum required memory to compress one rowgroup is approximately</span></span>

- <span data-ttu-id="ccb43-138">72 MB +</span><span class="sxs-lookup"><span data-stu-id="ccb43-138">72 MB +</span></span>
- <span data-ttu-id="ccb43-139">\#righe \* \#colonne \* 8 byte +</span><span class="sxs-lookup"><span data-stu-id="ccb43-139">\#rows \* \#columns \* 8 bytes +</span></span>
- <span data-ttu-id="ccb43-140">\#righe \* \#colonne stringa breve \* 32 byte +</span><span class="sxs-lookup"><span data-stu-id="ccb43-140">\#rows \* \#short-string-columns \* 32 bytes +</span></span>
- <span data-ttu-id="ccb43-141">\#colonne stringa lunga \* 16 MB per il dizionario di compressione</span><span class="sxs-lookup"><span data-stu-id="ccb43-141">\#long-string-columns \* 16 MB for compression dictionary</span></span>

<span data-ttu-id="ccb43-142">dove le colonne stringa breve usano tipi di dati stringa < = 32 byte e le colonne stringa lunga usano tipi di dati stringa > 32 byte.</span><span class="sxs-lookup"><span data-stu-id="ccb43-142">where short-string-columns use string data types of <= 32 bytes and long-string-columns use string data types of > 32 bytes.</span></span>

<span data-ttu-id="ccb43-143">Le stringhe lunghe vengono compresse con un metodo di compressione progettato per la compressione del testo.</span><span class="sxs-lookup"><span data-stu-id="ccb43-143">Long strings are compressed with a compression method designed for compressing text.</span></span> <span data-ttu-id="ccb43-144">Questo metodo di compressione usa un *dizionario* per archiviare i modelli di testo.</span><span class="sxs-lookup"><span data-stu-id="ccb43-144">This compression method uses a *dictionary* to store text patterns.</span></span> <span data-ttu-id="ccb43-145">La dimensione massima di un oggetto dictionary è 16 MB.</span><span class="sxs-lookup"><span data-stu-id="ccb43-145">The maximum size of a dictionary is 16 MB.</span></span> <span data-ttu-id="ccb43-146">Esiste un solo dizionario per ogni colonna stringa lunga nel gruppo di righe.</span><span class="sxs-lookup"><span data-stu-id="ccb43-146">There is only one dictionary for each long string column in the rowgroup.</span></span>

<span data-ttu-id="ccb43-147">Per un'analisi approfondita dei requisiti di memoria columnstore, vedere il video [Azure SQL Data Warehouse scaling: configuration and guidance](https://myignite.microsoft.com/videos/14822) (Scalabilità di Azure SQL Data Warehouse: configurazione e linee guida).</span><span class="sxs-lookup"><span data-stu-id="ccb43-147">For an in-depth discussion of columnstore memory requirements, see the video [Azure SQL Data Warehouse scaling: configuration and guidance](https://myignite.microsoft.com/videos/14822).</span></span>

## <a name="ways-to-reduce-memory-requirements"></a><span data-ttu-id="ccb43-148">Modi per ridurre i requisiti di memoria</span><span class="sxs-lookup"><span data-stu-id="ccb43-148">Ways to reduce memory requirements</span></span>

<span data-ttu-id="ccb43-149">Usare le tecniche seguenti per ridurre i requisiti di memoria per la compressione dei gruppi di righe in indici columnstore.</span><span class="sxs-lookup"><span data-stu-id="ccb43-149">Use the following techniques to reduce the memory requirements for compressing rowgroups into columnstore indexes.</span></span>

### <a name="use-fewer-columns"></a><span data-ttu-id="ccb43-150">Usare meno colonne</span><span class="sxs-lookup"><span data-stu-id="ccb43-150">Use fewer columns</span></span>
<span data-ttu-id="ccb43-151">Se possibile, progettare la tabella con meno colonne.</span><span class="sxs-lookup"><span data-stu-id="ccb43-151">If possible, design the table with fewer columns.</span></span> <span data-ttu-id="ccb43-152">Quando un gruppo di righe viene compresso nel columnstore, l'indice columnstore comprime ogni segmento di colonna separatamente.</span><span class="sxs-lookup"><span data-stu-id="ccb43-152">When a rowgroup is compressed into the columnstore, the columnstore index compresses each column segment separately.</span></span> <span data-ttu-id="ccb43-153">Pertanto i requisiti di memoria per comprimere un gruppo di righe aumentano con l'aumentare del numero di colonne.</span><span class="sxs-lookup"><span data-stu-id="ccb43-153">Therefore the memory requirements to compress a rowgroup increase as the number of columns increases.</span></span>


### <a name="use-fewer-string-columns"></a><span data-ttu-id="ccb43-154">Usare meno colonne di stringhe</span><span class="sxs-lookup"><span data-stu-id="ccb43-154">Use fewer string columns</span></span>
<span data-ttu-id="ccb43-155">Le colonne di dati di tipo stringa richiedono una quantità di memoria maggiore rispetto ai tipi di dati numerici.</span><span class="sxs-lookup"><span data-stu-id="ccb43-155">Columns of string data types require more memory than numeric and date data types.</span></span> <span data-ttu-id="ccb43-156">Per ridurre i requisiti di memoria, prendere in considerazione la rimozione delle colonne di tipo stringa dalle tabelle di dati e il loro inserimento in tabelle di dimensioni minori.</span><span class="sxs-lookup"><span data-stu-id="ccb43-156">To reduce memory requirements, consider removing string columns from fact tables and putting them in smaller dimension tables.</span></span>

<span data-ttu-id="ccb43-157">Requisiti di memoria aggiuntivi per la compressione di stringhe:</span><span class="sxs-lookup"><span data-stu-id="ccb43-157">Additional memory requirements for string compression:</span></span>

- <span data-ttu-id="ccb43-158">I tipi di dati stringa fino a 32 caratteri possono richiedere 32 byte aggiuntivi per valore.</span><span class="sxs-lookup"><span data-stu-id="ccb43-158">String data types up to 32 characters can require 32 additional bytes per value.</span></span>
- <span data-ttu-id="ccb43-159">I tipi di dati stringa con più di 32 caratteri vengono compressi mediante metodi di dizionario.</span><span class="sxs-lookup"><span data-stu-id="ccb43-159">String data types with more than 32 characters are compressed using dictionary methods.</span></span>  <span data-ttu-id="ccb43-160">Ogni colonna del gruppo di righe può richiedere fino a 16 MB aggiuntivi per creare il dizionario.</span><span class="sxs-lookup"><span data-stu-id="ccb43-160">Each column in the rowgroup can require up to an additional 16 MB to build the dictionary.</span></span>

### <a name="avoid-over-partitioning"></a><span data-ttu-id="ccb43-161">Evitare il partizionamento eccessivo</span><span class="sxs-lookup"><span data-stu-id="ccb43-161">Avoid over-partitioning</span></span>

<span data-ttu-id="ccb43-162">Gli indici columnstore creano uno o più gruppi di righe per partizione.</span><span class="sxs-lookup"><span data-stu-id="ccb43-162">Columnstore indexes create one or more rowgroups per partition.</span></span> <span data-ttu-id="ccb43-163">In SQL Data Warehouse il numero di partizioni aumenta rapidamente perché i dati vengono distribuiti e ogni distribuzione è partizionata.</span><span class="sxs-lookup"><span data-stu-id="ccb43-163">In SQL Data Warehouse, the number of partitions grows quickly because the data is distributed and each distribution is partitioned.</span></span> <span data-ttu-id="ccb43-164">Se la tabella ha troppe partizioni, potrebbero esserci abbastanza righe per riempire i gruppi di righe.</span><span class="sxs-lookup"><span data-stu-id="ccb43-164">If the table has too many partitions, there might not be enough rows to fill the rowgroups.</span></span> <span data-ttu-id="ccb43-165">La mancanza di righe non crea richiesta di memoria durante la compressione, ma alcuni gruppi di righe soffriranno di scarse prestazioni delle query columnstore.</span><span class="sxs-lookup"><span data-stu-id="ccb43-165">The lack of rows does not create memory pressure during compression, but it leads to rowgroups that do not achieve the best columnstore query performance.</span></span>

<span data-ttu-id="ccb43-166">Un altro motivo per evitare l'eccessivo partizionamento è che il caricamento di righe in un indice columnstore in una tabella partizionata comporta un sovraccarico della memoria.</span><span class="sxs-lookup"><span data-stu-id="ccb43-166">Another reason to avoid over-partitioning is there is a memory overhead for loading rows into a columnstore index on a partitioned table.</span></span> <span data-ttu-id="ccb43-167">Durante il caricamento molte partizioni potrebbero ricevere le righe in ingresso, che vengono mantenute in memoria finché ogni partizione dispone di un numero di righe sufficiente da comprimere.</span><span class="sxs-lookup"><span data-stu-id="ccb43-167">During a load, many partitions could receive the incoming rows, which are held in memory until each partition has enough rows to be compressed.</span></span> <span data-ttu-id="ccb43-168">Con un numero eccessivo di partizioni vengono create richieste di memoria aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="ccb43-168">Having too many partitions creates additional memory pressure.</span></span>

### <a name="simplify-the-load-query"></a><span data-ttu-id="ccb43-169">Semplificare la query di caricamento</span><span class="sxs-lookup"><span data-stu-id="ccb43-169">Simplify the load query</span></span>

<span data-ttu-id="ccb43-170">Il database condivide la concessione di memoria per una query tra tutti gli operatori della query.</span><span class="sxs-lookup"><span data-stu-id="ccb43-170">The database shares the memory grant for a query among all the operators in the query.</span></span> <span data-ttu-id="ccb43-171">Quando una query di caricamento contiene ordinamenti complessi e join, la memoria disponibile per la compressione è ridotta.</span><span class="sxs-lookup"><span data-stu-id="ccb43-171">When a load query has complex sorts and joins, the memory available for compression is reduced.</span></span>

<span data-ttu-id="ccb43-172">Progettare la query di caricamento concentrandosi solo sul caricamento.</span><span class="sxs-lookup"><span data-stu-id="ccb43-172">Design the load query to focus only on loading the query.</span></span> <span data-ttu-id="ccb43-173">Se è necessario eseguire trasformazioni sui dati, eseguirle separatamente dalla query di caricamento.</span><span class="sxs-lookup"><span data-stu-id="ccb43-173">If you need to run transformations on the data, run them separate from the load query.</span></span> <span data-ttu-id="ccb43-174">Ad esempio, collocare temporaneamente i dati in una tabella heap, eseguire le trasformazioni e quindi caricare la tabella di gestione temporanea nell'indice columnstore.</span><span class="sxs-lookup"><span data-stu-id="ccb43-174">For example, stage the data in a heap table, run the transformations, and then load the staging table into the columnstore index.</span></span> <span data-ttu-id="ccb43-175">È possibile anche caricare prima i dati e poi usare il sistema MPP per trasformarli.</span><span class="sxs-lookup"><span data-stu-id="ccb43-175">You can also load the data first and then use the MPP system to transform the data.</span></span>

### <a name="adjust-maxdop"></a><span data-ttu-id="ccb43-176">Regolare MAXDOP</span><span class="sxs-lookup"><span data-stu-id="ccb43-176">Adjust MAXDOP</span></span>

<span data-ttu-id="ccb43-177">Ogni distribuzione comprime i gruppi di righe nel columnstore in parallelo quando c'è più di un core CPU disponibile per distribuzione.</span><span class="sxs-lookup"><span data-stu-id="ccb43-177">Each distribution compresses rowgroups into the columnstore in parallel when there is more than one CPU core available per distribution.</span></span> <span data-ttu-id="ccb43-178">Il parallelismo richiede risorse di memoria aggiuntive che possono portare a richieste di memoria pesanti e al taglio del gruppo di righe.</span><span class="sxs-lookup"><span data-stu-id="ccb43-178">The parallelism requires additional memory resources, which can lead to memory pressure and rowgroup trimming.</span></span>

<span data-ttu-id="ccb43-179">Per ridurre le richieste di memoria, è possibile usare l'hint di query MAXDOP per forzare l'esecuzione seriale dell'operazione di caricamento in ogni distribuzione.</span><span class="sxs-lookup"><span data-stu-id="ccb43-179">To reduce memory pressure, you can use the MAXDOP query hint to force the load operation to run in serial mode within each distribution.</span></span>

```
CREATE TABLE MyFactSalesQuota
WITH (DISTRIBUTION = ROUND_ROBIN)
AS SELECT * FROM FactSalesQUota
OPTION (MAXDOP 1);
```

## <a name="ways-to-allocate-more-memory"></a><span data-ttu-id="ccb43-180">Modi per allocare altra memoria</span><span class="sxs-lookup"><span data-stu-id="ccb43-180">Ways to allocate more memory</span></span>

<span data-ttu-id="ccb43-181">La dimensione delle DWU e la classe della risorsa utente insieme determinano la quantità di memoria disponibile per una query dell'utente.</span><span class="sxs-lookup"><span data-stu-id="ccb43-181">DWU size and the user resource class together determine how much memory is available for a user query.</span></span> <span data-ttu-id="ccb43-182">Per aumentare la concessione di memoria per una query di caricamento, è possibile aumentare il numero di DWU o aumentare la classe risorsa.</span><span class="sxs-lookup"><span data-stu-id="ccb43-182">To increase the memory grant for a load query, you can either increase the number of DWUs or increase the resource class.</span></span>

- <span data-ttu-id="ccb43-183">Per aumentare le DWU, vedere [Ridimensionare le prestazioni](sql-data-warehouse-manage-compute-overview.md#scale-compute)</span><span class="sxs-lookup"><span data-stu-id="ccb43-183">To increase the DWUs, see [How do I scale performance?](sql-data-warehouse-manage-compute-overview.md#scale-compute)</span></span>
- <span data-ttu-id="ccb43-184">Per cambiare la classe risorsa per una query, vedere [Esempio di modifica della classe di risorse di un utente](sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).</span><span class="sxs-lookup"><span data-stu-id="ccb43-184">To change the resource class for a query, see [Change a user resource class example](sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).</span></span>

<span data-ttu-id="ccb43-185">Ad esempio, sulla DWU 100 un utente nella classe risorsa smallrc può usare 100 MB di memoria per ogni distribuzione.</span><span class="sxs-lookup"><span data-stu-id="ccb43-185">For example, on DWU 100 a user in the smallrc resource class can use 100 MB of memory for each distribution.</span></span> <span data-ttu-id="ccb43-186">Per informazioni dettagliate, vedere [Gestione della concorrenza e del carico di lavoro in SQL Data Warehouse](sql-data-warehouse-develop-concurrency.md).</span><span class="sxs-lookup"><span data-stu-id="ccb43-186">For the details, see [Concurrency in SQL Data Warehouse](sql-data-warehouse-develop-concurrency.md).</span></span>

<span data-ttu-id="ccb43-187">Si supponga di determinare la necessità di 700 MB di memoria per ottenere le dimensioni di un gruppo di righe di alta qualità.</span><span class="sxs-lookup"><span data-stu-id="ccb43-187">Suppose you determine that you need 700 MB of memory to get high-quality rowgroup sizes.</span></span> <span data-ttu-id="ccb43-188">Questi esempi illustrano come eseguire la query di caricamento con memoria sufficiente.</span><span class="sxs-lookup"><span data-stu-id="ccb43-188">These examples show how you can run the load query with enough memory.</span></span>

- <span data-ttu-id="ccb43-189">Usando la DWU 1000 e mediumrc, la concessione di memoria è di 800 MB</span><span class="sxs-lookup"><span data-stu-id="ccb43-189">Using DWU 1000 and mediumrc, your memory grant is 800 MB</span></span>
- <span data-ttu-id="ccb43-190">Usando la DWU 600 e largerc, la concessione di memoria è di 800 MB.</span><span class="sxs-lookup"><span data-stu-id="ccb43-190">Using DWU 600 and largerc, your memory grant is 800 MB.</span></span>


## <a name="next-steps"></a><span data-ttu-id="ccb43-191">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ccb43-191">Next steps</span></span>

<span data-ttu-id="ccb43-192">Per trovare altri modi con cui migliorare le prestazioni in SQL Data Warehouse, vedere la sezione [Panoramica](sql-data-warehouse-overview-manage-user-queries.md) relativa alle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="ccb43-192">To find more ways to improve performance in SQL Data Warehouse, see the [Performance overview](sql-data-warehouse-overview-manage-user-queries.md).</span></span>

<!--Image references-->

<!--Article references-->


<!--MSDN references-->

<!--Other Web references-->
