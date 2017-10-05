---
title: Gestione delle statistiche nelle tabelle in SQL Data Warehouse | Documentazione Microsoft
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
ms.openlocfilehash: 1d5ded69e394643ddfc3de0c6d30dbd30c8e848f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="managing-statistics-on-tables-in-sql-data-warehouse"></a><span data-ttu-id="4af63-103">Gestione delle statistiche nelle tabelle in SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="4af63-103">Managing statistics on tables in SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="4af63-104">[Panoramica][Overview]</span><span class="sxs-lookup"><span data-stu-id="4af63-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="4af63-105">[Tipi di dati][Data Types]</span><span class="sxs-lookup"><span data-stu-id="4af63-105">[Data Types][Data Types]</span></span>
> * <span data-ttu-id="4af63-106">[Distribuzione][Distribute]</span><span class="sxs-lookup"><span data-stu-id="4af63-106">[Distribute][Distribute]</span></span>
> * <span data-ttu-id="4af63-107">[Indice][Index]</span><span class="sxs-lookup"><span data-stu-id="4af63-107">[Index][Index]</span></span>
> * <span data-ttu-id="4af63-108">[Partizione][Partition]</span><span class="sxs-lookup"><span data-stu-id="4af63-108">[Partition][Partition]</span></span>
> * <span data-ttu-id="4af63-109">[Statistiche][Statistics]</span><span class="sxs-lookup"><span data-stu-id="4af63-109">[Statistics][Statistics]</span></span>
> * <span data-ttu-id="4af63-110">[Temporanee][Temporary]</span><span class="sxs-lookup"><span data-stu-id="4af63-110">[Temporary][Temporary]</span></span>
> 
> 

<span data-ttu-id="4af63-111">Più informazioni sui dati sono a disposizione di SQL Data Warehouse, più rapidamente può eseguire query.</span><span class="sxs-lookup"><span data-stu-id="4af63-111">The more SQL Data Warehouse knows about your data, the faster it can execute queries against your data.</span></span>  <span data-ttu-id="4af63-112">L'utente può comunicare i suoi dati a SQL Data Warehouse raccogliendone le statistiche.</span><span class="sxs-lookup"><span data-stu-id="4af63-112">The way that you tell SQL Data Warehouse about your data, is by collecting statistics about your data.</span></span>  <span data-ttu-id="4af63-113">Le statistiche sui dati sono fra gli aspetti più importanti per ottimizzare le query.</span><span class="sxs-lookup"><span data-stu-id="4af63-113">Having statistics on your data is one of the most important things you can do to optimize your queries.</span></span>  <span data-ttu-id="4af63-114">Le statistiche consentono a SQL Data Warehouse di creare il piano ottimale per le query.</span><span class="sxs-lookup"><span data-stu-id="4af63-114">Statistics help SQL Data Warehouse create the most optimal plan for your queries.</span></span>  <span data-ttu-id="4af63-115">Questo è dovuto al fatto che Query Optimizer di SQL Data Warehouse si basa sul costo.</span><span class="sxs-lookup"><span data-stu-id="4af63-115">This is because the SQL Data Warehouse query optimizer is a cost based optimizer.</span></span>  <span data-ttu-id="4af63-116">Ciò significa che esegue un confronto fra i costi di vari piani di query e poi sceglie quello che costa meno, che dovrebbe anche essere il piano eseguito più velocemente.</span><span class="sxs-lookup"><span data-stu-id="4af63-116">That is, it compares the cost of various query plans and then chooses the plan with the lowest cost, which should also be the plan that will execute the fastest.</span></span>

<span data-ttu-id="4af63-117">È possibile creare statistiche su una singola colonna, su più colonne o sull'indice di una tabella.</span><span class="sxs-lookup"><span data-stu-id="4af63-117">Statistics can be created on a single column, multiple columns or on an index of a table.</span></span>  <span data-ttu-id="4af63-118">Le statistiche vengono archiviate in un istogramma che acquisisce l'intervallo e la selettività dei valori.</span><span class="sxs-lookup"><span data-stu-id="4af63-118">Statistics are stored in a histogram which captures the range and selectivity of values.</span></span>  <span data-ttu-id="4af63-119">Questo aspetto riveste particolare interesse quando Query Optimizer deve valutare clausole JOIN, GROUP BY, HAVING e WHERE in una query.</span><span class="sxs-lookup"><span data-stu-id="4af63-119">This is of particular interest when the optimizer needs to evaluate JOINs, GROUP BY, HAVING and WHERE clauses in a query.</span></span>  <span data-ttu-id="4af63-120">Ad esempio, se Query Optimizer stima che la data da filtrare nella query restituirà 1 riga, potrebbe scegliere un piano molto diverso rispetto a quando stima che la data selezionata restituirà 1 milione di righe.</span><span class="sxs-lookup"><span data-stu-id="4af63-120">For example, if the optimizer estimates that the date you are filtering in your query will return 1 row, it may choose a very different plan than if it estimates that they date you have selected will return 1 million rows.</span></span>  <span data-ttu-id="4af63-121">Mentre è estremamente importante creare statistiche, è altrettanto importante che le statistiche riflettano *con precisione* lo stato corrente della tabella.</span><span class="sxs-lookup"><span data-stu-id="4af63-121">While creating statistics is extremely important, it is equally important that statistics *accurately* reflect the current state of the table.</span></span>  <span data-ttu-id="4af63-122">La presenza di statistiche aggiornate garantisce che Query Optimizer selezioni un buon piano.</span><span class="sxs-lookup"><span data-stu-id="4af63-122">Having up-to-date statistics ensures that a good plan is selected by the optimizer.</span></span>  <span data-ttu-id="4af63-123">La qualità dei piani creati dall'utilità di ottimizzazione dipende dalla qualità delle statistiche sui dati.</span><span class="sxs-lookup"><span data-stu-id="4af63-123">The plans created by the optimizer are only as good as the statistics on your data.</span></span>

<span data-ttu-id="4af63-124">Il processo di creazione e aggiornamento delle statistiche è attualmente manuale, ma è molto semplice.</span><span class="sxs-lookup"><span data-stu-id="4af63-124">The process of creating and updating statistics is currently a manual process, but is very simple to do.</span></span>  <span data-ttu-id="4af63-125">È diverso rispetto a SQL Server, che crea e aggiorna automaticamente le statistiche su singoli indici e colonne.</span><span class="sxs-lookup"><span data-stu-id="4af63-125">This is unlike SQL Server which automatically creates and updates statistics on single columns and indexes.</span></span>  <span data-ttu-id="4af63-126">Utilizzando le informazioni seguenti, è possibile automatizzare notevolmente la gestione delle statistiche sui dati.</span><span class="sxs-lookup"><span data-stu-id="4af63-126">By using the information below, you can greatly automate the management of the statistics on your data.</span></span> 

## <a name="getting-started-with-statistics"></a><span data-ttu-id="4af63-127">Introduzione alle statistiche</span><span class="sxs-lookup"><span data-stu-id="4af63-127">Getting started with statistics</span></span>
 <span data-ttu-id="4af63-128">La creazione di statistiche campionate su ogni colonna è un modo semplice per iniziare a usare le statistiche.</span><span class="sxs-lookup"><span data-stu-id="4af63-128">Creating sampled statistics on every column is an easy way to get started with statistics.</span></span>  <span data-ttu-id="4af63-129">Poiché è altrettanto importante tenere aggiornate le statistiche, un approccio conservativo potrebbe consistere nell'aggiornare le statistiche ogni giorno o dopo ogni caricamento.</span><span class="sxs-lookup"><span data-stu-id="4af63-129">Since it is equally important to keep statistics up-to-date, a conservative approach may be to update your statistics daily or after each load.</span></span> <span data-ttu-id="4af63-130">Sono sempre necessari compromessi tra le prestazioni e il costo di creazione e aggiornamento delle statistiche.</span><span class="sxs-lookup"><span data-stu-id="4af63-130">There are always trade-offs between performance and the cost to create and update statistics.</span></span>  <span data-ttu-id="4af63-131">Se si ritiene che la gestione di tutte le statistiche richieda troppo tempo, è consigliabile provare a scegliere in modo più selettivo le colonne con le statistiche o quelle che richiedono aggiornamenti frequenti.</span><span class="sxs-lookup"><span data-stu-id="4af63-131">If you find it is taking too long to maintain all of your statistics, you may want to try to be more selective about which columns have statistics or which columns need frequent updating.</span></span>  <span data-ttu-id="4af63-132">Potrebbe ad esempio essere consigliabile aggiornare le colonne di data ogni giorno piuttosto che dopo ogni caricamento, perché potrebbero essere aggiunti nuovi valori.</span><span class="sxs-lookup"><span data-stu-id="4af63-132">For example, you might want to update date columns daily, as new values may be added rather than after every load.</span></span> <span data-ttu-id="4af63-133">Anche in questo caso, il massimo vantaggio è offerto dalle statistiche su colonne usate nelle clausole JOIN, GROUP BY, HAVING e WHERE.</span><span class="sxs-lookup"><span data-stu-id="4af63-133">Again, you will gain the most benefit by having statistics on columns involved in JOINs, GROUP BY, HAVING and WHERE clauses.</span></span>  <span data-ttu-id="4af63-134">Se si dispone di una tabella con molte colonne che vengono usate solo nella clausola SELECT, le statistiche su queste colonne potrebbero non essere utili e dedicare un po' più di impegno a identificare solo le colonne in cui le statistiche saranno utili può ridurre il tempo per gestire le statistiche.</span><span class="sxs-lookup"><span data-stu-id="4af63-134">If you have a table with a lot of columns which are only used in the SELECT clause, statistics on these columns may not help, and spending a little more effort to identify only the columns where statistics will help, can reduce the time to maintain your statistics.</span></span>

## <a name="multi-column-statistics"></a><span data-ttu-id="4af63-135">Statistiche a più colonne</span><span class="sxs-lookup"><span data-stu-id="4af63-135">Multi-column statistics</span></span>
<span data-ttu-id="4af63-136">Oltre a creare le statistiche su singole colonne, ci si potrebbe rendere conto che le query possono trarre vantaggio da statistiche a più colonne.</span><span class="sxs-lookup"><span data-stu-id="4af63-136">In addition to creating statistics on single columns, you may find that your queries will benefit from multi-column statistics.</span></span>  <span data-ttu-id="4af63-137">Le statistiche a più colonne sono statistiche create su un elenco di colonne.</span><span class="sxs-lookup"><span data-stu-id="4af63-137">Multi-column statistics are statistics created on a list of columns.</span></span>  <span data-ttu-id="4af63-138">Includono statistiche a colonna singola nella prima colonna dell'elenco, oltre ad alcune informazioni di correlazione tra colonne definite densità.</span><span class="sxs-lookup"><span data-stu-id="4af63-138">They include single column statistics on the first column in the list, plus some cross-column correlation information called densities.</span></span>  <span data-ttu-id="4af63-139">Ad esempio, se si dispone di una tabella unita a un'altra in due colonne, ci si potrebbe rendere conto che SQL Data Warehouse può ottimizzare il piano nel caso in cui comprenda la relazione tra due colonne.</span><span class="sxs-lookup"><span data-stu-id="4af63-139">For example, if you have a table that joins to another on two columns, you may find that SQL Data Warehouse can better optimize the plan if it understands the relationship between two columns.</span></span>   <span data-ttu-id="4af63-140">Le statistiche a più colonne possono migliorare le prestazioni delle query per alcune operazioni, ad esempio nelle clausole JOIN composite e GROUP BY.</span><span class="sxs-lookup"><span data-stu-id="4af63-140">Multi-column statistics can improve query performance for some operations such as composite joins and group by.</span></span>

## <a name="updating-statistics"></a><span data-ttu-id="4af63-141">Aggiornamento delle statistiche</span><span class="sxs-lookup"><span data-stu-id="4af63-141">Updating statistics</span></span>
<span data-ttu-id="4af63-142">L'aggiornamento delle statistiche è una parte importante della routine gestione del database.</span><span class="sxs-lookup"><span data-stu-id="4af63-142">Updating statistics is an important part of your database management routine.</span></span>  <span data-ttu-id="4af63-143">Quando la distribuzione dei dati nel database subisce modifiche, è necessario aggiornare le statistiche.</span><span class="sxs-lookup"><span data-stu-id="4af63-143">When the distribution of data in the database changes, statistics need to be updated.</span></span>  <span data-ttu-id="4af63-144">La presenza di statistiche non aggiornate comporterà prestazioni di query non ottimali.</span><span class="sxs-lookup"><span data-stu-id="4af63-144">Out-of-date statistics will lead to sub-optimal query performance.</span></span>

<span data-ttu-id="4af63-145">Una procedura consigliata consiste nell'aggiornare le statistiche sulle colonne data ogni giorno quando vengono aggiunte nuove date.</span><span class="sxs-lookup"><span data-stu-id="4af63-145">One best practice is to update statistics on date columns each day as new dates are added.</span></span>  <span data-ttu-id="4af63-146">Ogni volta che vengono caricate nuove righe nel data warehouse, vengono aggiunte nuove date di caricamento o date di transazione.</span><span class="sxs-lookup"><span data-stu-id="4af63-146">Each time new rows are loaded into the data warehouse, new load dates or transaction dates are added.</span></span> <span data-ttu-id="4af63-147">Queste righe modificano la distribuzione dei dati e rendono non aggiornate le statistiche.</span><span class="sxs-lookup"><span data-stu-id="4af63-147">These change the data distribution and make the statistics out-of-date.</span></span> <span data-ttu-id="4af63-148">Al contrario, le statistiche su una colonna di paese in una tabella dei clienti possono non dover essere mai aggiornate, poiché la distribuzione dei valori in genere non cambia.</span><span class="sxs-lookup"><span data-stu-id="4af63-148">Conversely, statistics on a country column in a customer table might never need to be updated, as the distribution of values doesn’t generally change.</span></span> <span data-ttu-id="4af63-149">Supponendo che la distribuzione sia costante tra i clienti, l'aggiunta di nuove righe alla variazione di tabella non modificherà la distribuzione dei dati.</span><span class="sxs-lookup"><span data-stu-id="4af63-149">Assuming the distribution is constant between customers, adding new rows to the table variation isn't going to change the data distribution.</span></span> <span data-ttu-id="4af63-150">Tuttavia, se il data warehouse contiene solo un paese e si importano dati da un nuovo paese, facendo sì che vengano archiviati dati da più paesi, in quel caso si devono sicuramente aggiornare le statistiche sulla colonna del paese.</span><span class="sxs-lookup"><span data-stu-id="4af63-150">However, if your data warehouse only contains one country and you bring in data from a new country, resulting in data from multiple countries being stored, then you definitely need to update statistics on the country column.</span></span>

<span data-ttu-id="4af63-151">Quando si risolvono i problemi di una query è essenziale verificare prima di tutto se le statistiche sono aggiornate.</span><span class="sxs-lookup"><span data-stu-id="4af63-151">One of the first questions to ask when troubleshooting a query is, "Are the statistics up-to-date?"</span></span>

<span data-ttu-id="4af63-152">Questa verifica non può essere basata sulla data di creazione dei dati.</span><span class="sxs-lookup"><span data-stu-id="4af63-152">This question is not one that can be answered by the age of the data.</span></span> <span data-ttu-id="4af63-153">Un oggetto statistiche aggiornato può essere molto vecchio se non sono state apportate modifiche sostanziali ai dati sottostanti.</span><span class="sxs-lookup"><span data-stu-id="4af63-153">An up to date statistics object could be very old if there's been no material change to the underlying data.</span></span> <span data-ttu-id="4af63-154">È necessario aggiornare le statistiche *quando* vengono apportate modifiche sostanziali al numero di righe o modifiche materiali alla distribuzione dei valori per una colonna specifica.</span><span class="sxs-lookup"><span data-stu-id="4af63-154">When the number of rows has changed substantially or there is a material change in the distribution of values for a given column *then* it's time to update statistics.</span></span>  

<span data-ttu-id="4af63-155">Come riferimento, **SQL Server** (non SQL Data Warehouse) aggiorna automaticamente le statistiche nelle situazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="4af63-155">For reference, **SQL Server** (not SQL Data Warehouse) automatically updates statistics for these situations:</span></span>

* <span data-ttu-id="4af63-156">Se non si dispone di alcuna riga nella tabella, quando si aggiungono righe si ottiene un aggiornamento automatico delle statistiche</span><span class="sxs-lookup"><span data-stu-id="4af63-156">If you have zero rows in the table, when you add rows, you’ll get an automatic update of statistics</span></span>
* <span data-ttu-id="4af63-157">Quando si aggiungono più di 500 righe in una tabella che inizialmente ha meno di 500 righe (ad esempio, all'inizio ne ha 499 e poi si aggiungono 500 righe per un totale di 999 righe), si ottiene un aggiornamento automatico</span><span class="sxs-lookup"><span data-stu-id="4af63-157">When you add more than 500 rows to a table starting with less than 500 rows (e.g. at start you have 499 and then add 500 rows to a total of 999 rows), you’ll get an automatic update</span></span> 
* <span data-ttu-id="4af63-158">Una volta superate le 500 righe è necessario aggiungere altre 500 righe + il 20% delle dimensioni della tabella prima di ottenere un aggiornamento automatico delle statistiche</span><span class="sxs-lookup"><span data-stu-id="4af63-158">Once you’re over 500 rows you will have to add 500 additional rows + 20% of the size of the table before you’ll see an automatic update on the stats</span></span>

<span data-ttu-id="4af63-159">Poiché non esiste alcuna vista a gestione dinamica (DMV) per determinare se i dati all'interno della tabella sono cambiati dall'ultimo aggiornamento delle statistiche, sapere a quando risalgono le statistiche può fornire un quadro della situazione.</span><span class="sxs-lookup"><span data-stu-id="4af63-159">Since there is no DMV to determine if data within the table has changed since the last time statistics were updated, knowing the age of your statistics can provide you with part of the picture.</span></span>  <span data-ttu-id="4af63-160">È possibile usare la query seguente per determinare l'ultimo aggiornamento delle statistiche di ogni tabella.</span><span class="sxs-lookup"><span data-stu-id="4af63-160">You can use the following query to determine the last time your statistics where updated on each table.</span></span>  

> [!NOTE]
> <span data-ttu-id="4af63-161">Si tenga presente che se vi è una modifica sostanziale nella distribuzione dei valori per una determinata colonna, è necessario aggiornare le statistiche a prescindere da quando sono state aggiornate l'ultima volta.</span><span class="sxs-lookup"><span data-stu-id="4af63-161">Remember if there is a material change in the distribution of values for a given column, you should update statistics regardless of the last time they were updated.</span></span>  
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

<span data-ttu-id="4af63-162">Le colonne data in un data warehouse, ad esempio, necessitano solitamente di aggiornamenti frequenti delle statistiche.</span><span class="sxs-lookup"><span data-stu-id="4af63-162">Date columns in a data warehouse, for example, usually need frequent statistics updates.</span></span> <span data-ttu-id="4af63-163">Ogni volta che vengono caricate nuove righe nel data warehouse, vengono aggiunte nuove date di caricamento o date di transazione.</span><span class="sxs-lookup"><span data-stu-id="4af63-163">Each time new rows are loaded into the data warehouse, new load dates or transaction dates are added.</span></span> <span data-ttu-id="4af63-164">Queste righe modificano la distribuzione dei dati e rendono non aggiornate le statistiche.</span><span class="sxs-lookup"><span data-stu-id="4af63-164">These change the data distribution and make the statistics out-of-date.</span></span>  <span data-ttu-id="4af63-165">Al contrario, è possibile che non sia mai necessario aggiornare le statistiche relative alla colonna del sesso in una tabella clienti.</span><span class="sxs-lookup"><span data-stu-id="4af63-165">Conversely, statistics on a gender column on a customer table might never need to be updated.</span></span> <span data-ttu-id="4af63-166">Supponendo che la distribuzione sia costante tra i clienti, l'aggiunta di nuove righe alla variazione di tabella non modificherà la distribuzione dei dati.</span><span class="sxs-lookup"><span data-stu-id="4af63-166">Assuming the distribution is constant between customers, adding new rows to the table variation isn't going to change the data distribution.</span></span> <span data-ttu-id="4af63-167">Se tuttavia il data warehouse contiene solo un sesso e uno nuovo requisito ha come risultato più sessi, sarà decisamente necessario aggiornare le statistiche relative alla colonna del sesso.</span><span class="sxs-lookup"><span data-stu-id="4af63-167">However, if your data warehouse only contains one gender and a new requirement results in multiple genders then you definitely need to update statistics on the gender column.</span></span>

<span data-ttu-id="4af63-168">Per altre informazioni, vedere [Statistiche][Statistics] in MSDN.</span><span class="sxs-lookup"><span data-stu-id="4af63-168">For further explanation, see [Statistics][Statistics] on MSDN.</span></span>

## <a name="implementing-statistics-management"></a><span data-ttu-id="4af63-169">Implementazione della gestione delle statistiche</span><span class="sxs-lookup"><span data-stu-id="4af63-169">Implementing statistics management</span></span>
<span data-ttu-id="4af63-170">È spesso consigliabile estendere il processo di caricamento dei dati per assicurare che le statistiche vengano aggiornate al termine del caricamento.</span><span class="sxs-lookup"><span data-stu-id="4af63-170">It is often a good idea to extend your data loading process to ensure that statistics are updated at the end of the load.</span></span> <span data-ttu-id="4af63-171">Il caricamento dei dati è la fase in cui si verifica con maggiore frequenza una modifica delle dimensioni e/o della distribuzione dei valori delle tabelle.</span><span class="sxs-lookup"><span data-stu-id="4af63-171">The data load is when tables most frequently change their size and/or their distribution of values.</span></span> <span data-ttu-id="4af63-172">Questa è quindi una posizione logica per implementare alcuni processi di gestione.</span><span class="sxs-lookup"><span data-stu-id="4af63-172">Therefore, this is a logical place to implement some management processes.</span></span>

<span data-ttu-id="4af63-173">Di seguito sono disponibili alcuni principi guida per l'aggiornamento delle statistiche durante il processo di caricamento:</span><span class="sxs-lookup"><span data-stu-id="4af63-173">Some guiding principles are provided below for updating your statistics during the load process:</span></span>

* <span data-ttu-id="4af63-174">Assicurarsi che ogni tabella caricata includa almeno un oggetto statistiche aggiornato.</span><span class="sxs-lookup"><span data-stu-id="4af63-174">Ensure that each loaded table has at least one statistics object updated.</span></span> <span data-ttu-id="4af63-175">Ciò permette di aggiornare le informazioni sulle dimensioni delle tabelle (conteggio delle righe e conteggio delle pagine) come parte dell'aggiornamento delle statistiche.</span><span class="sxs-lookup"><span data-stu-id="4af63-175">This updates the tables size (row count and page count) information as part of the stats update.</span></span>
* <span data-ttu-id="4af63-176">Concentrarsi sulle colonne incluse nelle clausole JOIN, GROUP BY, ORDER BY e DISTINCT.</span><span class="sxs-lookup"><span data-stu-id="4af63-176">Focus on columns participating in JOIN, GROUP BY, ORDER BY and DISTINCT clauses</span></span>
* <span data-ttu-id="4af63-177">Prendere in considerazione una maggiore frequenza per l'aggiornamento delle colonne di tipo "parola chiave Ascending", ad esempio le date delle transazioni, poiché questi valori non verranno inclusi nell'istogramma delle statistiche.</span><span class="sxs-lookup"><span data-stu-id="4af63-177">Consider updating "ascending key" columns such as transaction dates more frequently as these values will not be included in the statistics histogram.</span></span>
* <span data-ttu-id="4af63-178">Prendere in considerazione una minore frequenza per l'aggiornamento delle colonne relative alla distribuzione statica.</span><span class="sxs-lookup"><span data-stu-id="4af63-178">Consider updating static distribution columns less frequently.</span></span>
* <span data-ttu-id="4af63-179">Occorre ricordare che ogni oggetto statistiche viene aggiornato in serie.</span><span class="sxs-lookup"><span data-stu-id="4af63-179">Remember each statistic object is updated in series.</span></span> <span data-ttu-id="4af63-180">La semplice implementazione di `UPDATE STATISTICS <TABLE_NAME>` potrebbe non essere ottimale, in particolare per tabelle di grandi dimensioni con molti oggetti statistici.</span><span class="sxs-lookup"><span data-stu-id="4af63-180">Simply implementing `UPDATE STATISTICS <TABLE_NAME>` may not be ideal - especially for wide tables with lots of statistics objects.</span></span>

> [!NOTE]
> <span data-ttu-id="4af63-181">Per altre informazioni sulla [parola chiave Ascending], vedere il white paper sul modello di stima della cardinalità di SQL Server 2014.</span><span class="sxs-lookup"><span data-stu-id="4af63-181">For more details on [ascending key] please refer to the SQL Server 2014 cardinality estimation model whitepaper.</span></span>
> 
> 

<span data-ttu-id="4af63-182">Per altre informazioni, vedere [Stima della cardinalità][Cardinality Estimation] in MSDN.</span><span class="sxs-lookup"><span data-stu-id="4af63-182">For further explanation, see  [Cardinality Estimation][Cardinality Estimation] on MSDN.</span></span>

## <a name="examples-create-statistics"></a><span data-ttu-id="4af63-183">Esempi: Creare le statistiche</span><span class="sxs-lookup"><span data-stu-id="4af63-183">Examples: Create statistics</span></span>
<span data-ttu-id="4af63-184">Questi esempi illustrano come usare diverse opzioni per la creazione delle statistiche.</span><span class="sxs-lookup"><span data-stu-id="4af63-184">These examples show how to use various options for creating statistics.</span></span> <span data-ttu-id="4af63-185">Le opzioni usate per ogni colonna dipendono dalle caratteristiche dei dati e dal modo in cui la colonna verrà usata nelle query.</span><span class="sxs-lookup"><span data-stu-id="4af63-185">The options that you use for each column depend on the characteristics of your data and how the column will be used in queries.</span></span>

### <a name="a-create-single-column-statistics-with-default-options"></a><span data-ttu-id="4af63-186">A.</span><span class="sxs-lookup"><span data-stu-id="4af63-186">A.</span></span> <span data-ttu-id="4af63-187">Creare statistiche a colonna singola con opzioni predefinite</span><span class="sxs-lookup"><span data-stu-id="4af63-187">Create single-column statistics with default options</span></span>
<span data-ttu-id="4af63-188">Per creare statistiche su una colonna, è sufficiente fornire un nome per l'oggetto statistiche e il nome della colonna.</span><span class="sxs-lookup"><span data-stu-id="4af63-188">To create statistics on a column, simply provide a name for the statistics object and the name of the column.</span></span>

<span data-ttu-id="4af63-189">Questa sintassi usa tutte le opzioni predefinite.</span><span class="sxs-lookup"><span data-stu-id="4af63-189">This syntax uses all of the default options.</span></span> <span data-ttu-id="4af63-190">Per impostazione predefinita, SQL Data Warehouse esegue il campionamento del 20% della tabella quando crea le statistiche.</span><span class="sxs-lookup"><span data-stu-id="4af63-190">By default, SQL Data Warehouse samples 20 percent of the table when it creates statistics.</span></span>

```sql
CREATE STATISTICS [statistics_name] ON [schema_name].[table_name]([column_name]);
```

<span data-ttu-id="4af63-191">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="4af63-191">For example:</span></span>

```sql
CREATE STATISTICS col1_stats ON dbo.table1 (col1);
```

### <a name="b-create-single-column-statistics-by-examining-every-row"></a><span data-ttu-id="4af63-192">B.</span><span class="sxs-lookup"><span data-stu-id="4af63-192">B.</span></span> <span data-ttu-id="4af63-193">Creare statistiche a colonna singola esaminando ogni riga</span><span class="sxs-lookup"><span data-stu-id="4af63-193">Create single-column statistics by examining every row</span></span>
<span data-ttu-id="4af63-194">La frequenza di campionamento del 20% è sufficiente per la maggior parte delle situazioni.</span><span class="sxs-lookup"><span data-stu-id="4af63-194">The default sampling rate of 20 percent is sufficient for most situations.</span></span> <span data-ttu-id="4af63-195">È tuttavia possibile modificare la frequenza di campionamento.</span><span class="sxs-lookup"><span data-stu-id="4af63-195">However, you can adjust the sampling rate.</span></span>

<span data-ttu-id="4af63-196">Per eseguire il campionamento dell'intera tabella, usare la sintassi seguente:</span><span class="sxs-lookup"><span data-stu-id="4af63-196">To sample the full table, use this syntax:</span></span>

```sql
CREATE STATISTICS [statistics_name] ON [schema_name].[table_name]([column_name]) WITH FULLSCAN;
```

<span data-ttu-id="4af63-197">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="4af63-197">For example:</span></span>

```sql
CREATE STATISTICS col1_stats ON dbo.table1 (col1) WITH FULLSCAN;
```

### <a name="c-create-single-column-statistics-by-specifying-the-sample-size"></a><span data-ttu-id="4af63-198">C.</span><span class="sxs-lookup"><span data-stu-id="4af63-198">C.</span></span> <span data-ttu-id="4af63-199">Creare statistiche a colonna singola specificando le dimensioni del campione</span><span class="sxs-lookup"><span data-stu-id="4af63-199">Create single-column statistics by specifying the sample size</span></span>
<span data-ttu-id="4af63-200">In alternativa, è possibile specificare le dimensioni del campione sotto forma di percentuale:</span><span class="sxs-lookup"><span data-stu-id="4af63-200">Alternatively, you can specify the sample size as a percent:</span></span>

```sql
CREATE STATISTICS col1_stats ON dbo.table1 (col1) WITH SAMPLE = 50 PERCENT;
```

### <a name="d-create-single-column-statistics-on-only-some-of-the-rows"></a><span data-ttu-id="4af63-201">D.</span><span class="sxs-lookup"><span data-stu-id="4af63-201">D.</span></span> <span data-ttu-id="4af63-202">Creare statistiche a colonna singola solo su alcune righe</span><span class="sxs-lookup"><span data-stu-id="4af63-202">Create single-column statistics on only some of the rows</span></span>
<span data-ttu-id="4af63-203">È anche possibile creare statistiche su una parte delle righe della tabella.</span><span class="sxs-lookup"><span data-stu-id="4af63-203">Another option, you can create statistics on a portion of the rows in your table.</span></span> <span data-ttu-id="4af63-204">Questa opzione è definita statistica filtrata.</span><span class="sxs-lookup"><span data-stu-id="4af63-204">This is called a filtered statistic.</span></span>

<span data-ttu-id="4af63-205">Ad esempio, è possibile usare le statistiche filtrate quando si prevede di eseguire una query in una partizione specifica di una tabella partizionata di grandi dimensioni.</span><span class="sxs-lookup"><span data-stu-id="4af63-205">For example, you could use filtered statistics when you plan to query a specific partition of a large partitioned table.</span></span> <span data-ttu-id="4af63-206">Se si creano statistiche solo sui valori della partizione, la precisione delle statistiche migliorerà e miglioreranno quindi le prestazioni delle query.</span><span class="sxs-lookup"><span data-stu-id="4af63-206">By creating statistics on only the partition values, the accuracy of the statistics will improve, and therefore improve query performance.</span></span>

<span data-ttu-id="4af63-207">Questo esempio crea statistiche su un intervallo di valori.</span><span class="sxs-lookup"><span data-stu-id="4af63-207">This example creates statistics on a range of values.</span></span> <span data-ttu-id="4af63-208">È possibile definire con facilità i valori in modo che corrispondano all'intervallo di valori in una partizione.</span><span class="sxs-lookup"><span data-stu-id="4af63-208">The values could easily be defined to match the range of values in a partition.</span></span>

```sql
CREATE STATISTICS stats_col1 ON table1(col1) WHERE col1 > '2000101' AND col1 < '20001231';
```

> [!NOTE]
> <span data-ttu-id="4af63-209">Per fare in modo che Query Optimizer prenda in considerazione l'uso delle statistiche filtrate quando sceglie il piano di query distribuite, è necessario che la query rientri nella definizione dell'oggetto statistiche.</span><span class="sxs-lookup"><span data-stu-id="4af63-209">For the query optimizer to consider using filtered statistics when it chooses the distributed query plan, the query must fit inside the definition of the statistics object.</span></span> <span data-ttu-id="4af63-210">Usando l'esempio precedente, la clausola where della query deve specificare valori col1 compresi tra 2000101 e 20001231.</span><span class="sxs-lookup"><span data-stu-id="4af63-210">Using the previous example, the query's where clause needs to specify col1 values between 2000101 and 20001231.</span></span>
> 
> 

### <a name="e-create-single-column-statistics-with-all-the-options"></a><span data-ttu-id="4af63-211">E.</span><span class="sxs-lookup"><span data-stu-id="4af63-211">E.</span></span> <span data-ttu-id="4af63-212">Creare statistiche a colonna singola con tutte le opzioni</span><span class="sxs-lookup"><span data-stu-id="4af63-212">Create single-column statistics with all the options</span></span>
<span data-ttu-id="4af63-213">È ovviamente possibile combinare tutte le opzioni.</span><span class="sxs-lookup"><span data-stu-id="4af63-213">You can, of course, combine the options together.</span></span> <span data-ttu-id="4af63-214">L'esempio seguente crea un oggetto statistiche filtrato con una dimensione di campionamento personalizzata:</span><span class="sxs-lookup"><span data-stu-id="4af63-214">The example below creates a filtered statistics object with a custom sample size:</span></span>

```sql
CREATE STATISTICS stats_col1 ON table1 (col1) WHERE col1 > '2000101' AND col1 < '20001231' WITH SAMPLE = 50 PERCENT;
```

<span data-ttu-id="4af63-215">Per i riferimenti completi, vedere [CREATE STATISTICS][CREATE STATISTICS] in MSDN.</span><span class="sxs-lookup"><span data-stu-id="4af63-215">For the full reference, see [CREATE STATISTICS][CREATE STATISTICS] on MSDN.</span></span>

### <a name="f-create-multi-column-statistics"></a><span data-ttu-id="4af63-216">F.</span><span class="sxs-lookup"><span data-stu-id="4af63-216">F.</span></span> <span data-ttu-id="4af63-217">Creare statistiche a più colonne</span><span class="sxs-lookup"><span data-stu-id="4af63-217">Create multi-column statistics</span></span>
<span data-ttu-id="4af63-218">Per creare statistiche a più colonne, è sufficiente usare gli esempi precedenti ma specificare più colonne.</span><span class="sxs-lookup"><span data-stu-id="4af63-218">To create a multi-column statistics, simply use the previous examples, but specify more columns.</span></span>

> [!NOTE]
> <span data-ttu-id="4af63-219">L'istogramma, che viene usato per stimare il numero di righe nei risultati delle query, sarà disponibile solo per la prima colonna elencata nella definizione dell'oggetto statistiche.</span><span class="sxs-lookup"><span data-stu-id="4af63-219">The histogram, which is used to estimate number of rows in the query result, is only available for the first column listed in the statistics object definition.</span></span>
> 
> 

<span data-ttu-id="4af63-220">In questo esempio l'istogramma è disponibile su *product\_category*.</span><span class="sxs-lookup"><span data-stu-id="4af63-220">In this example, the histogram is on *product\_category*.</span></span> <span data-ttu-id="4af63-221">Le statistiche tra le colonne vengono calcolate su *product\_category* e *product\_sub_c\ategory*:</span><span class="sxs-lookup"><span data-stu-id="4af63-221">Cross-column statistics are calculated on *product\_category* and *product\_sub_c\ategory*:</span></span>

```sql
CREATE STATISTICS stats_2cols ON table1 (product_category, product_sub_category) WHERE product_category > '2000101' AND product_category < '20001231' WITH SAMPLE = 50 PERCENT;
```

<span data-ttu-id="4af63-222">Poiché è presente una correlazione tra *product\_category* e *product\_sub\_category*, una statistica a più colonne può essere utile se si accede contemporaneamente a queste colonne.</span><span class="sxs-lookup"><span data-stu-id="4af63-222">Since there is a correlation between *product\_category* and *product\_sub\_category*, a multi-column stat can be useful if these columns are accessed at the same time.</span></span>

### <a name="g-create-statistics-on-all-the-columns-in-a-table"></a><span data-ttu-id="4af63-223">G.</span><span class="sxs-lookup"><span data-stu-id="4af63-223">G.</span></span> <span data-ttu-id="4af63-224">Creare statistiche su tutte le colonne in una tabella</span><span class="sxs-lookup"><span data-stu-id="4af63-224">Create statistics on all the columns in a table</span></span>
<span data-ttu-id="4af63-225">Un modo per creare le statistiche consiste nell'emettere comandi CREATE STATISTICS dopo la creazione della tabella.</span><span class="sxs-lookup"><span data-stu-id="4af63-225">One way to create statistics is to issues CREATE STATISTICS commands after creating the table.</span></span>

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

### <a name="h-use-a-stored-procedure-to-create-statistics-on-all-columns-in-a-database"></a><span data-ttu-id="4af63-226">H.</span><span class="sxs-lookup"><span data-stu-id="4af63-226">H.</span></span> <span data-ttu-id="4af63-227">Usare una stored procedure per creare statistiche su tutte le colonne in un database</span><span class="sxs-lookup"><span data-stu-id="4af63-227">Use a stored procedure to create statistics on all columns in a database</span></span>
<span data-ttu-id="4af63-228">SQL Data Warehouse non include una stored procedure di sistema equivalente a [sp_create_stats][] in SQL Server.</span><span class="sxs-lookup"><span data-stu-id="4af63-228">SQL Data Warehouse does not have a system stored procedure equivalent to [sp_create_stats][] in SQL Server.</span></span> <span data-ttu-id="4af63-229">Questa stored procedure crea un oggetto statistiche a colonna singola su ogni colonna del database che non include già statistiche.</span><span class="sxs-lookup"><span data-stu-id="4af63-229">This stored procedure creates a single column statistics object on every column of the database that doesn't already have statistics.</span></span>

<span data-ttu-id="4af63-230">Ciò permetterà di iniziare a progettare il database.</span><span class="sxs-lookup"><span data-stu-id="4af63-230">This will help you get started with your database design.</span></span> <span data-ttu-id="4af63-231">È possibile adattare l'operazione alle proprie esigenze.</span><span class="sxs-lookup"><span data-stu-id="4af63-231">Feel free to adapt it to your needs.</span></span>

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

<span data-ttu-id="4af63-232">Per creare statistiche su tutte le colonne della tabella con questa procedura, è sufficiente chiamarla.</span><span class="sxs-lookup"><span data-stu-id="4af63-232">To create statistics on all columns in the table with this procedure, simply call the procedure.</span></span>

```sql
prc_sqldw_create_stats;
```

## <a name="examples-update-statistics"></a><span data-ttu-id="4af63-233">Esempi: Aggiornare le statistiche</span><span class="sxs-lookup"><span data-stu-id="4af63-233">Examples: update statistics</span></span>
<span data-ttu-id="4af63-234">Per aggiornare le statistiche, è possibile eseguire le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="4af63-234">To update statistics, you can:</span></span>

1. <span data-ttu-id="4af63-235">Aggiornare un oggetto statistiche.</span><span class="sxs-lookup"><span data-stu-id="4af63-235">Update one statistics object.</span></span> <span data-ttu-id="4af63-236">Specificare il nome dell'oggetto statistiche da aggiornare.</span><span class="sxs-lookup"><span data-stu-id="4af63-236">Specify the name of the statistics object you wish to update.</span></span>
2. <span data-ttu-id="4af63-237">Aggiornare tutti gli oggetti statistiche in una tabella.</span><span class="sxs-lookup"><span data-stu-id="4af63-237">Update all statistics objects on a table.</span></span> <span data-ttu-id="4af63-238">Specificare il nome della tabella invece di un oggetto statistiche specifico.</span><span class="sxs-lookup"><span data-stu-id="4af63-238">Specify the name of the table instead of one specific statistics object.</span></span>

### <a name="a-update-one-specific-statistics-object"></a><span data-ttu-id="4af63-239">A.</span><span class="sxs-lookup"><span data-stu-id="4af63-239">A.</span></span> <span data-ttu-id="4af63-240">Aggiornare un oggetto statistiche specifico</span><span class="sxs-lookup"><span data-stu-id="4af63-240">Update one specific statistics object</span></span>
<span data-ttu-id="4af63-241">Usare la sintassi seguente per aggiornare un oggetto statistiche specifico:</span><span class="sxs-lookup"><span data-stu-id="4af63-241">Use the following syntax to update a specific statistics object:</span></span>

```sql
UPDATE STATISTICS [schema_name].[table_name]([stat_name]);
```

<span data-ttu-id="4af63-242">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="4af63-242">For example:</span></span>

```sql
UPDATE STATISTICS [dbo].[table1] ([stats_col1]);
```

<span data-ttu-id="4af63-243">L'aggiornamento di oggetti statistiche specifici permette di ridurre al minimo il tempo e le risorse necessari per gestire le statistiche.</span><span class="sxs-lookup"><span data-stu-id="4af63-243">By updating specific statistics objects, you can minimize the time and resources required to manage statistics.</span></span> <span data-ttu-id="4af63-244">È tuttavia necessario scegliere con attenzione gli oggetti statistiche migliori da aggiornare.</span><span class="sxs-lookup"><span data-stu-id="4af63-244">This requires some thought, though, to choose the best statistics objects to update.</span></span>

### <a name="b-update-all-statistics-on-a-table"></a><span data-ttu-id="4af63-245">B.</span><span class="sxs-lookup"><span data-stu-id="4af63-245">B.</span></span> <span data-ttu-id="4af63-246">Aggiornare tutte le statistiche in una tabella</span><span class="sxs-lookup"><span data-stu-id="4af63-246">Update all statistics on a table</span></span>
<span data-ttu-id="4af63-247">Illustra un semplice metodo di aggiornamento di tutti gli oggetti statistiche in una tabella.</span><span class="sxs-lookup"><span data-stu-id="4af63-247">This shows a simple method for updating all the statistics objects on a table.</span></span>

```sql
UPDATE STATISTICS [schema_name].[table_name];
```

<span data-ttu-id="4af63-248">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="4af63-248">For example:</span></span>

```sql
UPDATE STATISTICS dbo.table1;
```

<span data-ttu-id="4af63-249">Questa istruzione è facile da usare.</span><span class="sxs-lookup"><span data-stu-id="4af63-249">This statement is easy to use.</span></span> <span data-ttu-id="4af63-250">Occorre ricordare che aggiorna tutte le statistiche nella tabella e che quindi potrebbe eseguire più lavoro del necessario.</span><span class="sxs-lookup"><span data-stu-id="4af63-250">Just remember this updates all statistics on the table, and therefore might perform more work than is necessary.</span></span> <span data-ttu-id="4af63-251">Se le prestazioni non sono un problema, questo è decisamente il modo più semplice e più completo per assicurare che le statistiche siano aggiornate.</span><span class="sxs-lookup"><span data-stu-id="4af63-251">If the performance is not an issue, this is definitely the easiest and most complete way to guarantee statistics are up-to-date.</span></span>

> [!NOTE]
> <span data-ttu-id="4af63-252">Quando si aggiornano tutte le statistiche in una tabella, SQL Data Warehouse esegue un'analisi per campionare la tabella per ogni statistica.</span><span class="sxs-lookup"><span data-stu-id="4af63-252">When updating all statistics on a table, SQL Data Warehouse does a scan to sample the table for each statistics.</span></span> <span data-ttu-id="4af63-253">Se la tabella è grande, include molte colonne e molte statistiche, potrebbe risultare più efficiente aggiornare le singole statistiche in base alla necessità.</span><span class="sxs-lookup"><span data-stu-id="4af63-253">If the table is large, has many columns, and many statistics, it might be more efficient to update individual statistics based on need.</span></span>
> 
> 

<span data-ttu-id="4af63-254">Per l'implementazione di una procedura `UPDATE STATISTICS`, vedere l'articolo [Tabelle temporanee][Temporary].</span><span class="sxs-lookup"><span data-stu-id="4af63-254">For an implementation of an `UPDATE STATISTICS` procedure please see the [Temporary Tables][Temporary] article.</span></span> <span data-ttu-id="4af63-255">Il metodo di implementazione è leggermente diverso rispetto alla procedura `CREATE STATISTICS` precedente, ma il risultato finale è uguale.</span><span class="sxs-lookup"><span data-stu-id="4af63-255">The implementation method is slightly different to the `CREATE STATISTICS` procedure above but the end result is the same.</span></span>

<span data-ttu-id="4af63-256">Per la sintassi completa, vedere [UPDATE STATISTICS][Update Statistics] in MSDN.</span><span class="sxs-lookup"><span data-stu-id="4af63-256">For the full syntax, see [Update Statistics][Update Statistics] on MSDN.</span></span>

## <a name="statistics-metadata"></a><span data-ttu-id="4af63-257">Metadati delle statistiche</span><span class="sxs-lookup"><span data-stu-id="4af63-257">Statistics metadata</span></span>
<span data-ttu-id="4af63-258">Sono disponibili alcune visualizzazioni di sistema e funzioni che permettono di trovare informazioni sulle statistiche.</span><span class="sxs-lookup"><span data-stu-id="4af63-258">There are several system view and functions that you can use to find information about statistics.</span></span> <span data-ttu-id="4af63-259">Ad esempio, è possibile verificare se un oggetto statistiche non è aggiornato usando la funzione stats-date per vedere la data di creazione o dell'ultimo aggiornamento delle statistiche.</span><span class="sxs-lookup"><span data-stu-id="4af63-259">For example, you can see if a statistics object might be out-of-date by using the stats-date function to see when statistics were last created or updated.</span></span>

### <a name="catalog-views-for-statistics"></a><span data-ttu-id="4af63-260">Viste del catalogo per le statistiche</span><span class="sxs-lookup"><span data-stu-id="4af63-260">Catalog views for statistics</span></span>
<span data-ttu-id="4af63-261">Queste visualizzazioni di sistema forniscono informazioni sulle statistiche:</span><span class="sxs-lookup"><span data-stu-id="4af63-261">These system views provide information about statistics:</span></span>

| <span data-ttu-id="4af63-262">Vista del catalogo</span><span class="sxs-lookup"><span data-stu-id="4af63-262">Catalog View</span></span> | <span data-ttu-id="4af63-263">Descrizione</span><span class="sxs-lookup"><span data-stu-id="4af63-263">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="4af63-264">[sys.columns][sys.columns]</span><span class="sxs-lookup"><span data-stu-id="4af63-264">[sys.columns][sys.columns]</span></span> |<span data-ttu-id="4af63-265">Una riga per ogni colonna.</span><span class="sxs-lookup"><span data-stu-id="4af63-265">One row for each column.</span></span> |
| <span data-ttu-id="4af63-266">[sys.objects][sys.objects]</span><span class="sxs-lookup"><span data-stu-id="4af63-266">[sys.objects][sys.objects]</span></span> |<span data-ttu-id="4af63-267">Una riga per ogni oggetto del database.</span><span class="sxs-lookup"><span data-stu-id="4af63-267">One row for each object in the database.</span></span> |
| <span data-ttu-id="4af63-268">[sys.schemas][sys.schemas]</span><span class="sxs-lookup"><span data-stu-id="4af63-268">[sys.schemas][sys.schemas]</span></span> |<span data-ttu-id="4af63-269">Una riga per ogni schema del database.</span><span class="sxs-lookup"><span data-stu-id="4af63-269">One row for each schema in the database.</span></span> |
| <span data-ttu-id="4af63-270">[sys.stats][sys.stats]</span><span class="sxs-lookup"><span data-stu-id="4af63-270">[sys.stats][sys.stats]</span></span> |<span data-ttu-id="4af63-271">Una riga per ogni oggetto statistiche.</span><span class="sxs-lookup"><span data-stu-id="4af63-271">One row for each statistics object.</span></span> |
| <span data-ttu-id="4af63-272">[sys.stats_columns][sys.stats_columns]</span><span class="sxs-lookup"><span data-stu-id="4af63-272">[sys.stats_columns][sys.stats_columns]</span></span> |<span data-ttu-id="4af63-273">Una riga per ogni colonna nell'oggetto statistiche.</span><span class="sxs-lookup"><span data-stu-id="4af63-273">One row for each column in the statistics object.</span></span> <span data-ttu-id="4af63-274">Si collega a sys.columns.</span><span class="sxs-lookup"><span data-stu-id="4af63-274">Links back to sys.columns.</span></span> |
| <span data-ttu-id="4af63-275">[sys.tables][sys.tables]</span><span class="sxs-lookup"><span data-stu-id="4af63-275">[sys.tables][sys.tables]</span></span> |<span data-ttu-id="4af63-276">Una riga per ogni tabella (include le tabelle esterne).</span><span class="sxs-lookup"><span data-stu-id="4af63-276">One row for each table (includes external tables).</span></span> |
| <span data-ttu-id="4af63-277">[sys.table_types][sys.table_types]</span><span class="sxs-lookup"><span data-stu-id="4af63-277">[sys.table_types][sys.table_types]</span></span> |<span data-ttu-id="4af63-278">Una riga per ogni tipo di dati.</span><span class="sxs-lookup"><span data-stu-id="4af63-278">One row for each data type.</span></span> |

### <a name="system-functions-for-statistics"></a><span data-ttu-id="4af63-279">Funzioni di sistema per le statistiche</span><span class="sxs-lookup"><span data-stu-id="4af63-279">System functions for statistics</span></span>
<span data-ttu-id="4af63-280">Queste funzioni di sistema sono utili per usare le statistiche:</span><span class="sxs-lookup"><span data-stu-id="4af63-280">These system functions are useful for working with statistics:</span></span>

| <span data-ttu-id="4af63-281">Funzioni di sistema</span><span class="sxs-lookup"><span data-stu-id="4af63-281">System Function</span></span> | <span data-ttu-id="4af63-282">Descrizione</span><span class="sxs-lookup"><span data-stu-id="4af63-282">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="4af63-283">[STATS_DATE][STATS_DATE]</span><span class="sxs-lookup"><span data-stu-id="4af63-283">[STATS_DATE][STATS_DATE]</span></span> |<span data-ttu-id="4af63-284">Data dell'ultimo aggiornamento dell'oggetto statistiche.</span><span class="sxs-lookup"><span data-stu-id="4af63-284">Date the statistics object was last updated.</span></span> |
| <span data-ttu-id="4af63-285">[DBCC SHOW_STATISTICS][DBCC SHOW_STATISTICS]</span><span class="sxs-lookup"><span data-stu-id="4af63-285">[DBCC SHOW_STATISTICS][DBCC SHOW_STATISTICS]</span></span> |<span data-ttu-id="4af63-286">Fornisce informazioni a livello di riepilogo e dettagliate sulla distribuzione di valori riconosciute dall'oggetto statistiche.</span><span class="sxs-lookup"><span data-stu-id="4af63-286">Provides summary level and detailed information about the distribution of values as understood by the statistics object.</span></span> |

### <a name="combine-statistics-columns-and-functions-into-one-view"></a><span data-ttu-id="4af63-287">Combinare le colonne delle statistiche e le funzioni in un'unica visualizzazione</span><span class="sxs-lookup"><span data-stu-id="4af63-287">Combine statistics columns and functions into one view</span></span>
<span data-ttu-id="4af63-288">Questa visualizzazione riunisce le colonne relative alle statistiche e i risultati della funzione [STATS_DATE()][].</span><span class="sxs-lookup"><span data-stu-id="4af63-288">This view brings columns that relate to statistics, and results from the [STATS_DATE()][]function together.</span></span>

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

## <a name="dbcc-showstatistics-examples"></a><span data-ttu-id="4af63-289">Esempi di DBCC SHOW_STATISTICS()</span><span class="sxs-lookup"><span data-stu-id="4af63-289">DBCC SHOW_STATISTICS() examples</span></span>
<span data-ttu-id="4af63-290">DBCC SHOW_STATISTICS() mostra i dati inclusi in un oggetto statistiche.</span><span class="sxs-lookup"><span data-stu-id="4af63-290">DBCC SHOW_STATISTICS() shows the data held within a statistics object.</span></span> <span data-ttu-id="4af63-291">Questi dati sono costituiti da tre parti.</span><span class="sxs-lookup"><span data-stu-id="4af63-291">This data comes in three parts.</span></span>

1. <span data-ttu-id="4af63-292">Intestazione</span><span class="sxs-lookup"><span data-stu-id="4af63-292">Header</span></span>
2. <span data-ttu-id="4af63-293">Vettore di densità</span><span class="sxs-lookup"><span data-stu-id="4af63-293">Density Vector</span></span>
3. <span data-ttu-id="4af63-294">Istogramma</span><span class="sxs-lookup"><span data-stu-id="4af63-294">Histogram</span></span>

<span data-ttu-id="4af63-295">Metadati di intestazione sulle statistiche.</span><span class="sxs-lookup"><span data-stu-id="4af63-295">The header metadata about the statistics.</span></span> <span data-ttu-id="4af63-296">L'istogramma mostra la distribuzione dei valori nella prima colonna chiave dell'oggetto statistiche.</span><span class="sxs-lookup"><span data-stu-id="4af63-296">The histogram displays the distribution of values in the first key column of the statistics object.</span></span> <span data-ttu-id="4af63-297">Il vettore di densità misura la correlazione tra le colonne.</span><span class="sxs-lookup"><span data-stu-id="4af63-297">The density vector measures cross-column correlation.</span></span> <span data-ttu-id="4af63-298">SQL Data Warehouse calcola le stime di cardinalità con tutti i dati nell'oggetto statistiche.</span><span class="sxs-lookup"><span data-stu-id="4af63-298">SQLDW computes cardinality estimates with any of the data in the statistics object.</span></span>

### <a name="show-header-density-and-histogram"></a><span data-ttu-id="4af63-299">Mostrare l'intestazione, la densità e l'istogramma</span><span class="sxs-lookup"><span data-stu-id="4af63-299">Show header, density, and histogram</span></span>
<span data-ttu-id="4af63-300">Questo semplice esempio mostra tutte e tre le parti di un oggetto statistiche.</span><span class="sxs-lookup"><span data-stu-id="4af63-300">This simple example shows all three parts of a statistics object.</span></span>

```sql
DBCC SHOW_STATISTICS([<schema_name>.<table_name>],<stats_name>)
```

<span data-ttu-id="4af63-301">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="4af63-301">For example:</span></span>

```sql
DBCC SHOW_STATISTICS (dbo.table1, stats_col1);
```

### <a name="show-one-or-more-parts-of-dbcc-showstatistics"></a><span data-ttu-id="4af63-302">Mostrare una o più parti di DBCC SHOW_STATISTICS();</span><span class="sxs-lookup"><span data-stu-id="4af63-302">Show one or more parts of DBCC SHOW_STATISTICS();</span></span>
<span data-ttu-id="4af63-303">Se si è interessati a visualizzare solo parti specifiche, usare la clausola `WITH` e specificare le parti da visualizzare:</span><span class="sxs-lookup"><span data-stu-id="4af63-303">If you are only interested in viewing specific parts, use the `WITH` clause and specify which parts you want to see:</span></span>

```sql
DBCC SHOW_STATISTICS([<schema_name>.<table_name>],<stats_name>) WITH stat_header, histogram, density_vector
```

<span data-ttu-id="4af63-304">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="4af63-304">For example:</span></span>

```sql
DBCC SHOW_STATISTICS (dbo.table1, stats_col1) WITH histogram, density_vector
```

## <a name="dbcc-showstatistics-differences"></a><span data-ttu-id="4af63-305">Differenze di DBCC SHOW_STATISTICS()</span><span class="sxs-lookup"><span data-stu-id="4af63-305">DBCC SHOW_STATISTICS() differences</span></span>
<span data-ttu-id="4af63-306">DBCC SHOW_STATISTICS() viene implementato in modo più rigoroso in SQL Data Warehouse rispetto a SQL Server.</span><span class="sxs-lookup"><span data-stu-id="4af63-306">DBCC SHOW_STATISTICS() is more strictly implemented in SQL Data Warehouse compared to SQL Server.</span></span>

1. <span data-ttu-id="4af63-307">Le funzionalità non documentate non sono supportate</span><span class="sxs-lookup"><span data-stu-id="4af63-307">Undocumented features are not supported</span></span>
2. <span data-ttu-id="4af63-308">Non è possibile usare Stats_stream</span><span class="sxs-lookup"><span data-stu-id="4af63-308">Cannot use Stats_stream</span></span>
3. <span data-ttu-id="4af63-309">Non è possibile unire i risultati per sottoinsiemi specifici di dati statistici, ad esempio (STAT_HEADER JOIN DENSITY_VECTOR)</span><span class="sxs-lookup"><span data-stu-id="4af63-309">Cannot join results for specific subsets of statistics data e.g. (STAT_HEADER JOIN DENSITY_VECTOR)</span></span>
4. <span data-ttu-id="4af63-310">NO_INFOMSGS non può essere impostato per l'eliminazione del messaggio</span><span class="sxs-lookup"><span data-stu-id="4af63-310">NO_INFOMSGS cannot be set for message suppression</span></span>
5. <span data-ttu-id="4af63-311">Non è possibile usare le parentesi quadre per i nomi delle statistiche</span><span class="sxs-lookup"><span data-stu-id="4af63-311">Square brackets around statistics names cannot be used</span></span>
6. <span data-ttu-id="4af63-312">Non è possibile usare i nomi di colonna per identificare gli oggetti statistiche</span><span class="sxs-lookup"><span data-stu-id="4af63-312">Cannot use column names to identify statistics objects</span></span>
7. <span data-ttu-id="4af63-313">L'errore personalizzato 2767 non è supportato</span><span class="sxs-lookup"><span data-stu-id="4af63-313">Custom error 2767 is not supported</span></span>

## <a name="next-steps"></a><span data-ttu-id="4af63-314">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4af63-314">Next steps</span></span>
<span data-ttu-id="4af63-315">Per altri dettagli, vedere [DBCC SHOW_STATISTICS][DBCC SHOW_STATISTICS] in MSDN.</span><span class="sxs-lookup"><span data-stu-id="4af63-315">For more details, see [DBCC SHOW_STATISTICS][DBCC SHOW_STATISTICS] on MSDN.</span></span>  <span data-ttu-id="4af63-316">Per altre informazioni, vedere gli articoli su [panoramica delle tabelle][Overview], [tipi di dati delle tabelle][Data Types], [distribuzione di una tabella][Distribute], [indicizzazione di una tabella][Index], [partizionamento di una tabella][Partition] e [tabelle temporanee][Temporary].</span><span class="sxs-lookup"><span data-stu-id="4af63-316">To learn more, see the articles on [Table Overview][Overview], [Table Data Types][Data Types], [Distributing a Table][Distribute], [Indexing a Table][Index],  [Partitioning a Table][Partition] and [Temporary Tables][Temporary].</span></span>  <span data-ttu-id="4af63-317">Per altre informazioni sulle procedure consigliate, vedere [Procedure consigliate per SQL Data Warehouse][SQL Data Warehouse Best Practices].</span><span class="sxs-lookup"><span data-stu-id="4af63-317">For more about best practices, see [SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices].</span></span>  

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
