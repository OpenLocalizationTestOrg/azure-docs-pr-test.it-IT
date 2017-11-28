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
# <a name="managing-statistics-on-tables-in-sql-data-warehouse"></a><span data-ttu-id="c8cd5-103">Gestione delle statistiche nelle tabelle in SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="c8cd5-103">Managing statistics on tables in SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="c8cd5-104">[Panoramica][Overview]</span><span class="sxs-lookup"><span data-stu-id="c8cd5-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="c8cd5-105">[Tipi di dati][Data Types]</span><span class="sxs-lookup"><span data-stu-id="c8cd5-105">[Data Types][Data Types]</span></span>
> * <span data-ttu-id="c8cd5-106">[Distribuzione][Distribute]</span><span class="sxs-lookup"><span data-stu-id="c8cd5-106">[Distribute][Distribute]</span></span>
> * <span data-ttu-id="c8cd5-107">[Indice][Index]</span><span class="sxs-lookup"><span data-stu-id="c8cd5-107">[Index][Index]</span></span>
> * <span data-ttu-id="c8cd5-108">[Partizione][Partition]</span><span class="sxs-lookup"><span data-stu-id="c8cd5-108">[Partition][Partition]</span></span>
> * <span data-ttu-id="c8cd5-109">[Statistiche][Statistics]</span><span class="sxs-lookup"><span data-stu-id="c8cd5-109">[Statistics][Statistics]</span></span>
> * <span data-ttu-id="c8cd5-110">[Temporanee][Temporary]</span><span class="sxs-lookup"><span data-stu-id="c8cd5-110">[Temporary][Temporary]</span></span>
> 
> 

<span data-ttu-id="c8cd5-111">Hello ulteriori SQL Data Warehouse viene a conoscenza dei dati, hello più velocemente può eseguire query sui dati.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-111">hello more SQL Data Warehouse knows about your data, hello faster it can execute queries against your data.</span></span>  <span data-ttu-id="c8cd5-112">metodo Hello informare SQL Data Warehouse di dati, è la raccolta di statistiche sui dati.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-112">hello way that you tell SQL Data Warehouse about your data, is by collecting statistics about your data.</span></span>  <span data-ttu-id="c8cd5-113">Con le statistiche sui dati è una delle operazioni più importanti hello è possibile eseguire toooptimize le query.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-113">Having statistics on your data is one of hello most important things you can do toooptimize your queries.</span></span>  <span data-ttu-id="c8cd5-114">Statistiche consentono a SQL Data Warehouse di creare il piano ottimale di hello per le query.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-114">Statistics help SQL Data Warehouse create hello most optimal plan for your queries.</span></span>  <span data-ttu-id="c8cd5-115">Questo avviene perché query optimizer basati su query di SQL Data Warehouse di hello query optimizer è un costo.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-115">This is because hello SQL Data Warehouse query optimizer is a cost based optimizer.</span></span>  <span data-ttu-id="c8cd5-116">Vale a dire confronta il costo di hello dei diversi piani di query e quindi sceglie piano hello con costo più basso hello, che deve essere anche piano hello che eseguirà hello più veloce.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-116">That is, it compares hello cost of various query plans and then chooses hello plan with hello lowest cost, which should also be hello plan that will execute hello fastest.</span></span>

<span data-ttu-id="c8cd5-117">È possibile creare statistiche su una singola colonna, su più colonne o sull'indice di una tabella.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-117">Statistics can be created on a single column, multiple columns or on an index of a table.</span></span>  <span data-ttu-id="c8cd5-118">Le statistiche vengono archiviate in un istogramma che acquisisce intervallo hello e selettività dei valori.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-118">Statistics are stored in a histogram which captures hello range and selectivity of values.</span></span>  <span data-ttu-id="c8cd5-119">Si tratta di particolare interesse quando query optimizer hello deve tooevaluate join, GROUP BY, HAVING che clausole WHERE in una query.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-119">This is of particular interest when hello optimizer needs tooevaluate JOINs, GROUP BY, HAVING and WHERE clauses in a query.</span></span>  <span data-ttu-id="c8cd5-120">Ad esempio, se ottimizzatore di hello che data hello si filtrano nella query restituirà 1 riga, è possibile scegliere molto diversa rispetto a se in piano stime data è sono selezionata verrà restituito 1 milione di righe.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-120">For example, if hello optimizer estimates that hello date you are filtering in your query will return 1 row, it may choose a very different plan than if it estimates that they date you have selected will return 1 million rows.</span></span>  <span data-ttu-id="c8cd5-121">Durante la creazione di statistiche è estremamente importante, è ugualmente importante che le statistiche delle *accuratamente* rifletta hello lo stato corrente della tabella hello.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-121">While creating statistics is extremely important, it is equally important that statistics *accurately* reflect hello current state of hello table.</span></span>  <span data-ttu-id="c8cd5-122">Presenza di statistiche aggiornate assicura che un piano adeguato è selezionato da query optimizer hello.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-122">Having up-to-date statistics ensures that a good plan is selected by hello optimizer.</span></span>  <span data-ttu-id="c8cd5-123">i piani di Hello creati da query optimizer hello sono solo efficace delle statistiche di hello sui dati.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-123">hello plans created by hello optimizer are only as good as hello statistics on your data.</span></span>

<span data-ttu-id="c8cd5-124">il processo di Hello di creazione e aggiornamento delle statistiche è attualmente un processo manuale, ma è molto semplice toodo.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-124">hello process of creating and updating statistics is currently a manual process, but is very simple toodo.</span></span>  <span data-ttu-id="c8cd5-125">È diverso rispetto a SQL Server, che crea e aggiorna automaticamente le statistiche su singoli indici e colonne.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-125">This is unlike SQL Server which automatically creates and updates statistics on single columns and indexes.</span></span>  <span data-ttu-id="c8cd5-126">Utilizzando le informazioni di hello riportate di seguito, è possibile automatizzare notevolmente gestione hello delle statistiche di hello sui dati.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-126">By using hello information below, you can greatly automate hello management of hello statistics on your data.</span></span> 

## <a name="getting-started-with-statistics"></a><span data-ttu-id="c8cd5-127">Introduzione alle statistiche</span><span class="sxs-lookup"><span data-stu-id="c8cd5-127">Getting started with statistics</span></span>
 <span data-ttu-id="c8cd5-128">Creare le statistiche campionate ogni colonna viene avviato tooget un modo semplice con le statistiche.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-128">Creating sampled statistics on every column is an easy way tooget started with statistics.</span></span>  <span data-ttu-id="c8cd5-129">Poiché è ugualmente importante tookeep statistiche aggiornate, un approccio conservativo potrebbe essere tooupdate le statistiche di ogni giorno o dopo ogni carico.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-129">Since it is equally important tookeep statistics up-to-date, a conservative approach may be tooupdate your statistics daily or after each load.</span></span> <span data-ttu-id="c8cd5-130">Sono sempre presenti compromessi tra prestazioni e hello costo toocreate e aggiornare le statistiche.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-130">There are always trade-offs between performance and hello cost toocreate and update statistics.</span></span>  <span data-ttu-id="c8cd5-131">Se si ritiene che sta richiedendo troppo tempo toomaintain tutte le statistiche, è necessario frequenti toobe tootry più selettivo sulle statistiche dispongano quali colonne o le colonne di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-131">If you find it is taking too long toomaintain all of your statistics, you may want tootry toobe more selective about which columns have statistics or which columns need frequent updating.</span></span>  <span data-ttu-id="c8cd5-132">Ad esempio, potrebbe desiderato colonne data tooupdate ogni giorno, come è possibile aggiungere nuovi valori anziché dopo ogni carico.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-132">For example, you might want tooupdate date columns daily, as new values may be added rather than after every load.</span></span> <span data-ttu-id="c8cd5-133">Nuovamente, sarà possibile ottenere hello migliori con le statistiche su colonne coinvolte nel join, GROUP BY, HAVING che clausole WHERE.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-133">Again, you will gain hello most benefit by having statistics on columns involved in JOINs, GROUP BY, HAVING and WHERE clauses.</span></span>  <span data-ttu-id="c8cd5-134">Se si dispone di una tabella con molte clausola SELECT le colonne che vengono utilizzate solo in hello, statistiche su queste colonne potrebbero non aiutare e un po' più tooidentify di impegno di spesa solo le colonne hello consentono in cui le statistiche, può ridurre hello ora toomaintain le statistiche .</span><span class="sxs-lookup"><span data-stu-id="c8cd5-134">If you have a table with a lot of columns which are only used in hello SELECT clause, statistics on these columns may not help, and spending a little more effort tooidentify only hello columns where statistics will help, can reduce hello time toomaintain your statistics.</span></span>

## <a name="multi-column-statistics"></a><span data-ttu-id="c8cd5-135">Statistiche a più colonne</span><span class="sxs-lookup"><span data-stu-id="c8cd5-135">Multi-column statistics</span></span>
<span data-ttu-id="c8cd5-136">Inoltre toocreating le statistiche per colonne singole, è possibile che le query trarranno vantaggio dalle statistiche su più colonne.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-136">In addition toocreating statistics on single columns, you may find that your queries will benefit from multi-column statistics.</span></span>  <span data-ttu-id="c8cd5-137">Le statistiche a più colonne sono statistiche create su un elenco di colonne.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-137">Multi-column statistics are statistics created on a list of columns.</span></span>  <span data-ttu-id="c8cd5-138">Sono incluse le statistiche di colonna singola nella prima colonna hello nelle elenco hello e alcune informazioni di correlazione tra colonne chiamato densità.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-138">They include single column statistics on hello first column in hello list, plus some cross-column correlation information called densities.</span></span>  <span data-ttu-id="c8cd5-139">Ad esempio, se si dispone di una tabella che unisce in join tooanother su due colonne, è possibile che SQL Data Warehouse ottimizzare piano hello se riconosce relazione hello tra due colonne.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-139">For example, if you have a table that joins tooanother on two columns, you may find that SQL Data Warehouse can better optimize hello plan if it understands hello relationship between two columns.</span></span>   <span data-ttu-id="c8cd5-140">Le statistiche a più colonne possono migliorare le prestazioni delle query per alcune operazioni, ad esempio nelle clausole JOIN composite e GROUP BY.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-140">Multi-column statistics can improve query performance for some operations such as composite joins and group by.</span></span>

## <a name="updating-statistics"></a><span data-ttu-id="c8cd5-141">Aggiornamento delle statistiche</span><span class="sxs-lookup"><span data-stu-id="c8cd5-141">Updating statistics</span></span>
<span data-ttu-id="c8cd5-142">L'aggiornamento delle statistiche è una parte importante della routine gestione del database.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-142">Updating statistics is an important part of your database management routine.</span></span>  <span data-ttu-id="c8cd5-143">Quando viene modificato distribuzione hello dei dati nel database di hello, le statistiche devono toobe aggiornato.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-143">When hello distribution of data in hello database changes, statistics need toobe updated.</span></span>  <span data-ttu-id="c8cd5-144">Le statistiche non aggiornate determinerà le prestazioni delle query toosub ottimale.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-144">Out-of-date statistics will lead toosub-optimal query performance.</span></span>

<span data-ttu-id="c8cd5-145">Una procedura consigliata è tooupdate statistiche su colonne di data e ogni giorno vengono aggiunte nuove date.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-145">One best practice is tooupdate statistics on date columns each day as new dates are added.</span></span>  <span data-ttu-id="c8cd5-146">Le righe di nuovo ogni volta vengono caricati nel data warehouse di hello, vengono aggiunte nuove date di carico di transazione.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-146">Each time new rows are loaded into hello data warehouse, new load dates or transaction dates are added.</span></span> <span data-ttu-id="c8cd5-147">Questi modificano hello distribuzione dei dati e apportare le statistiche di hello non aggiornato.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-147">These change hello data distribution and make hello statistics out-of-date.</span></span> <span data-ttu-id="c8cd5-148">Al contrario, le statistiche su una colonna per il paese in una tabella clienti potrebbero non essere necessario toobe aggiornato, come la distribuzione di hello di valori in genere non viene modificato.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-148">Conversely, statistics on a country column in a customer table might never need toobe updated, as hello distribution of values doesn’t generally change.</span></span> <span data-ttu-id="c8cd5-149">Supponendo che la distribuzione di hello è costante tra i clienti, aggiunta di nuovi variazione della tabella toohello righe non sarà toochange distribuzione dei dati hello.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-149">Assuming hello distribution is constant between customers, adding new rows toohello table variation isn't going toochange hello data distribution.</span></span> <span data-ttu-id="c8cd5-150">Tuttavia, se il data warehouse contiene solo un paese e importare dati da un nuovo paese, risultante in dati di più paesi è stati archiviati, è assolutamente necessario statistiche tooupdate sulla colonna country hello.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-150">However, if your data warehouse only contains one country and you bring in data from a new country, resulting in data from multiple countries being stored, then you definitely need tooupdate statistics on hello country column.</span></span>

<span data-ttu-id="c8cd5-151">Uno dei hello prima domande tooask quando la risoluzione dei problemi di una query è "sono statistiche hello aggiornati?"</span><span class="sxs-lookup"><span data-stu-id="c8cd5-151">One of hello first questions tooask when troubleshooting a query is, "Are hello statistics up-to-date?"</span></span>

<span data-ttu-id="c8cd5-152">La domanda non è che è possibile rispondere in base all'età hello dei dati di hello.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-152">This question is not one that can be answered by hello age of hello data.</span></span> <span data-ttu-id="c8cd5-153">Un oggetto di statistiche aggiornato toodate potrebbe essere molto vecchio se non è stata eseguita alcuna toohello modifica sostanziale dati sottostanti.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-153">An up toodate statistics object could be very old if there's been no material change toohello underlying data.</span></span> <span data-ttu-id="c8cd5-154">Quando hello numero di righe è stato modificato sostanzialmente o viene apportata una modifica della distribuzione di valori per una determinata colonna hello materiale *quindi* è tooupdate delle statistiche.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-154">When hello number of rows has changed substantially or there is a material change in hello distribution of values for a given column *then* it's time tooupdate statistics.</span></span>  

<span data-ttu-id="c8cd5-155">Come riferimento, **SQL Server** (non SQL Data Warehouse) aggiorna automaticamente le statistiche nelle situazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="c8cd5-155">For reference, **SQL Server** (not SQL Data Warehouse) automatically updates statistics for these situations:</span></span>

* <span data-ttu-id="c8cd5-156">Se si dispone di zero righe nella tabella di hello, quando si aggiungono righe, si otterrà un aggiornamento automatico delle statistiche</span><span class="sxs-lookup"><span data-stu-id="c8cd5-156">If you have zero rows in hello table, when you add rows, you’ll get an automatic update of statistics</span></span>
* <span data-ttu-id="c8cd5-157">Quando si aggiunta più di 500 tabella tooa di righe a partire da meno di 500 righe (ad esempio all'inizio aver 499 e aggiungere quindi 500 righe tooa totale 999 righe), si otterrà un aggiornamento automatico</span><span class="sxs-lookup"><span data-stu-id="c8cd5-157">When you add more than 500 rows tooa table starting with less than 500 rows (e.g. at start you have 499 and then add 500 rows tooa total of 999 rows), you’ll get an automatic update</span></span> 
* <span data-ttu-id="c8cd5-158">Dopo aver oltre 500 righe è tooadd 500 righe aggiuntive + 20% delle dimensioni di hello della tabella hello prima sulla statistiche hello verrà visualizzato un aggiornamento automatico</span><span class="sxs-lookup"><span data-stu-id="c8cd5-158">Once you’re over 500 rows you will have tooadd 500 additional rows + 20% of hello size of hello table before you’ll see an automatic update on hello stats</span></span>

<span data-ttu-id="c8cd5-159">Poiché non esiste alcun toodetermine DMV dati all'interno di tabella hello sono stato modificato dopo l'aggiornamento delle statistiche ora ultimo hello, conoscere l'età di hello delle statistiche può fornire una parte di immagine hello.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-159">Since there is no DMV toodetermine if data within hello table has changed since hello last time statistics were updated, knowing hello age of your statistics can provide you with part of hello picture.</span></span>  <span data-ttu-id="c8cd5-160">È possibile utilizzare hello seguente toodetermine hello ultima le statistiche di query in cui l'aggiornamento in ogni tabella.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-160">You can use hello following query toodetermine hello last time your statistics where updated on each table.</span></span>  

> [!NOTE]
> <span data-ttu-id="c8cd5-161">Tenere presente che se è presente una modifica sostanziale nella distribuzione hello di valori per una determinata colonna, è necessario aggiornare le statistiche indipendentemente dal hello ultima volta che sono state aggiornate.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-161">Remember if there is a material change in hello distribution of values for a given column, you should update statistics regardless of hello last time they were updated.</span></span>  
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

<span data-ttu-id="c8cd5-162">Le colonne data in un data warehouse, ad esempio, necessitano solitamente di aggiornamenti frequenti delle statistiche.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-162">Date columns in a data warehouse, for example, usually need frequent statistics updates.</span></span> <span data-ttu-id="c8cd5-163">Le righe di nuovo ogni volta vengono caricati nel data warehouse di hello, vengono aggiunte nuove date di carico di transazione.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-163">Each time new rows are loaded into hello data warehouse, new load dates or transaction dates are added.</span></span> <span data-ttu-id="c8cd5-164">Questi modificano hello distribuzione dei dati e apportare le statistiche di hello non aggiornato.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-164">These change hello data distribution and make hello statistics out-of-date.</span></span>  <span data-ttu-id="c8cd5-165">Al contrario, le statistiche su una colonna relativa al sesso in una tabella clienti potrebbero non essere necessario toobe aggiornato.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-165">Conversely, statistics on a gender column on a customer table might never need toobe updated.</span></span> <span data-ttu-id="c8cd5-166">Supponendo che la distribuzione di hello è costante tra i clienti, aggiunta di nuovi variazione della tabella toohello righe non sarà toochange distribuzione dei dati hello.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-166">Assuming hello distribution is constant between customers, adding new rows toohello table variation isn't going toochange hello data distribution.</span></span> <span data-ttu-id="c8cd5-167">Tuttavia, se il data warehouse contiene solo un sesso e risultati di un nuovo requisito generano più i sessi è assolutamente necessario statistiche tooupdate nella colonna relativa al sesso hello.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-167">However, if your data warehouse only contains one gender and a new requirement results in multiple genders then you definitely need tooupdate statistics on hello gender column.</span></span>

<span data-ttu-id="c8cd5-168">Per altre informazioni, vedere [Statistiche][Statistics] in MSDN.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-168">For further explanation, see [Statistics][Statistics] on MSDN.</span></span>

## <a name="implementing-statistics-management"></a><span data-ttu-id="c8cd5-169">Implementazione della gestione delle statistiche</span><span class="sxs-lookup"><span data-stu-id="c8cd5-169">Implementing statistics management</span></span>
<span data-ttu-id="c8cd5-170">È spesso tooextend una buona idea dei dati durante il caricamento tooensure processo che le statistiche vengono aggiornate in hello fine del caricamento hello.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-170">It is often a good idea tooextend your data loading process tooensure that statistics are updated at hello end of hello load.</span></span> <span data-ttu-id="c8cd5-171">caricamento dei dati Hello è quando le tabelle cambiano più frequentemente alle dimensioni e/o la distribuzione di valori.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-171">hello data load is when tables most frequently change their size and/or their distribution of values.</span></span> <span data-ttu-id="c8cd5-172">Pertanto, si tratta di un punto logico di tooimplement alcuni processi di gestione.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-172">Therefore, this is a logical place tooimplement some management processes.</span></span>

<span data-ttu-id="c8cd5-173">Alcuni principi sono riportate di seguito per aggiornare le statistiche durante il processo di caricamento hello:</span><span class="sxs-lookup"><span data-stu-id="c8cd5-173">Some guiding principles are provided below for updating your statistics during hello load process:</span></span>

* <span data-ttu-id="c8cd5-174">Assicurarsi che ogni tabella caricata includa almeno un oggetto statistiche aggiornato.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-174">Ensure that each loaded table has at least one statistics object updated.</span></span> <span data-ttu-id="c8cd5-175">Questo hello aggiornamenti tabelle informazioni sulle dimensioni (numero di riga e conteggio delle pagine) come parte dell'aggiornamento di statistiche hello.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-175">This updates hello tables size (row count and page count) information as part of hello stats update.</span></span>
* <span data-ttu-id="c8cd5-176">Concentrarsi sulle colonne incluse nelle clausole JOIN, GROUP BY, ORDER BY e DISTINCT.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-176">Focus on columns participating in JOIN, GROUP BY, ORDER BY and DISTINCT clauses</span></span>
* <span data-ttu-id="c8cd5-177">È consigliabile aggiornare le colonne "chiave ascending", ad esempio transazioni più frequentemente di questi valori non verranno inclusi nell'istogramma delle statistiche hello date,</span><span class="sxs-lookup"><span data-stu-id="c8cd5-177">Consider updating "ascending key" columns such as transaction dates more frequently as these values will not be included in hello statistics histogram.</span></span>
* <span data-ttu-id="c8cd5-178">Prendere in considerazione una minore frequenza per l'aggiornamento delle colonne relative alla distribuzione statica.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-178">Consider updating static distribution columns less frequently.</span></span>
* <span data-ttu-id="c8cd5-179">Occorre ricordare che ogni oggetto statistiche viene aggiornato in serie.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-179">Remember each statistic object is updated in series.</span></span> <span data-ttu-id="c8cd5-180">La semplice implementazione di `UPDATE STATISTICS <TABLE_NAME>` potrebbe non essere ottimale, in particolare per tabelle di grandi dimensioni con molti oggetti statistici.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-180">Simply implementing `UPDATE STATISTICS <TABLE_NAME>` may not be ideal - especially for wide tables with lots of statistics objects.</span></span>

> [!NOTE]
> <span data-ttu-id="c8cd5-181">Per ulteriori informazioni su [crescente chiave] consultare il white paper del modello di stima della cardinalità toohello SQL Server 2014.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-181">For more details on [ascending key] please refer toohello SQL Server 2014 cardinality estimation model whitepaper.</span></span>
> 
> 

<span data-ttu-id="c8cd5-182">Per altre informazioni, vedere [Stima della cardinalità][Cardinality Estimation] in MSDN.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-182">For further explanation, see  [Cardinality Estimation][Cardinality Estimation] on MSDN.</span></span>

## <a name="examples-create-statistics"></a><span data-ttu-id="c8cd5-183">Esempi: Creare le statistiche</span><span class="sxs-lookup"><span data-stu-id="c8cd5-183">Examples: Create statistics</span></span>
<span data-ttu-id="c8cd5-184">Questi esempi mostrano come toouse varie opzioni per la creazione di statistiche.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-184">These examples show how toouse various options for creating statistics.</span></span> <span data-ttu-id="c8cd5-185">Opzioni Hello utilizzate per ogni colonna dipendono dalle caratteristiche hello dei dati e come colonna di hello verrà utilizzata nelle query.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-185">hello options that you use for each column depend on hello characteristics of your data and how hello column will be used in queries.</span></span>

### <a name="a-create-single-column-statistics-with-default-options"></a><span data-ttu-id="c8cd5-186">R.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-186">A.</span></span> <span data-ttu-id="c8cd5-187">Creare statistiche a colonna singola con opzioni predefinite</span><span class="sxs-lookup"><span data-stu-id="c8cd5-187">Create single-column statistics with default options</span></span>
<span data-ttu-id="c8cd5-188">toocreate statistiche su una colonna, è sufficiente fornire un nome di oggetto statistiche hello e hello della colonna hello.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-188">toocreate statistics on a column, simply provide a name for hello statistics object and hello name of hello column.</span></span>

<span data-ttu-id="c8cd5-189">Questa sintassi utilizza tutte le opzioni predefinite di hello.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-189">This syntax uses all of hello default options.</span></span> <span data-ttu-id="c8cd5-190">Per impostazione predefinita, SQL Data Warehouse esempi il 20% della tabella hello durante la creazione di statistiche.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-190">By default, SQL Data Warehouse samples 20 percent of hello table when it creates statistics.</span></span>

```sql
CREATE STATISTICS [statistics_name] ON [schema_name].[table_name]([column_name]);
```

<span data-ttu-id="c8cd5-191">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="c8cd5-191">For example:</span></span>

```sql
CREATE STATISTICS col1_stats ON dbo.table1 (col1);
```

### <a name="b-create-single-column-statistics-by-examining-every-row"></a><span data-ttu-id="c8cd5-192">B.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-192">B.</span></span> <span data-ttu-id="c8cd5-193">Creare statistiche a colonna singola esaminando ogni riga</span><span class="sxs-lookup"><span data-stu-id="c8cd5-193">Create single-column statistics by examining every row</span></span>
<span data-ttu-id="c8cd5-194">frequenza di campionamento predefinita Hello del 20% è sufficiente per la maggior parte delle situazioni.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-194">hello default sampling rate of 20 percent is sufficient for most situations.</span></span> <span data-ttu-id="c8cd5-195">Tuttavia, è possibile regolare la frequenza di campionamento hello.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-195">However, you can adjust hello sampling rate.</span></span>

<span data-ttu-id="c8cd5-196">hello toosample completo di tabella, utilizzare la seguente sintassi:</span><span class="sxs-lookup"><span data-stu-id="c8cd5-196">toosample hello full table, use this syntax:</span></span>

```sql
CREATE STATISTICS [statistics_name] ON [schema_name].[table_name]([column_name]) WITH FULLSCAN;
```

<span data-ttu-id="c8cd5-197">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="c8cd5-197">For example:</span></span>

```sql
CREATE STATISTICS col1_stats ON dbo.table1 (col1) WITH FULLSCAN;
```

### <a name="c-create-single-column-statistics-by-specifying-hello-sample-size"></a><span data-ttu-id="c8cd5-198">C.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-198">C.</span></span> <span data-ttu-id="c8cd5-199">Creare statistiche di colonna singola, specificando la dimensione del campione hello</span><span class="sxs-lookup"><span data-stu-id="c8cd5-199">Create single-column statistics by specifying hello sample size</span></span>
<span data-ttu-id="c8cd5-200">In alternativa, è possibile specificare la dimensione del campione hello sotto forma di percentuale:</span><span class="sxs-lookup"><span data-stu-id="c8cd5-200">Alternatively, you can specify hello sample size as a percent:</span></span>

```sql
CREATE STATISTICS col1_stats ON dbo.table1 (col1) WITH SAMPLE = 50 PERCENT;
```

### <a name="d-create-single-column-statistics-on-only-some-of-hello-rows"></a><span data-ttu-id="c8cd5-201">D.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-201">D.</span></span> <span data-ttu-id="c8cd5-202">Creare statistiche di colonna singola su tutte le righe di hello</span><span class="sxs-lookup"><span data-stu-id="c8cd5-202">Create single-column statistics on only some of hello rows</span></span>
<span data-ttu-id="c8cd5-203">Un'altra opzione, è possibile creare statistiche in una parte di hello righe nella tabella.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-203">Another option, you can create statistics on a portion of hello rows in your table.</span></span> <span data-ttu-id="c8cd5-204">Questa opzione è definita statistica filtrata.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-204">This is called a filtered statistic.</span></span>

<span data-ttu-id="c8cd5-205">Ad esempio, è possibile utilizzare le statistiche filtrate quando si pianifica una partizione specifica di una tabella partizionata grande tooquery.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-205">For example, you could use filtered statistics when you plan tooquery a specific partition of a large partitioned table.</span></span> <span data-ttu-id="c8cd5-206">Creando le statistiche su hello solo i valori della partizione, accuratezza hello di statistiche di hello migliorare e pertanto migliorare le prestazioni delle query.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-206">By creating statistics on only hello partition values, hello accuracy of hello statistics will improve, and therefore improve query performance.</span></span>

<span data-ttu-id="c8cd5-207">Questo esempio crea statistiche su un intervallo di valori.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-207">This example creates statistics on a range of values.</span></span> <span data-ttu-id="c8cd5-208">Hello valori potrebbero facilmente essere definita dall'intervallo di hello toomatch di valori in una partizione.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-208">hello values could easily be defined toomatch hello range of values in a partition.</span></span>

```sql
CREATE STATISTICS stats_col1 ON table1(col1) WHERE col1 > '2000101' AND col1 < '20001231';
```

> [!NOTE]
> <span data-ttu-id="c8cd5-209">Per hello query optimizer tooconsider le statistiche filtrate quando viene scelto il piano di query distribuite di hello, query hello deve adattarsi all'interno di hello definizione di oggetto statistiche hello.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-209">For hello query optimizer tooconsider using filtered statistics when it chooses hello distributed query plan, hello query must fit inside hello definition of hello statistics object.</span></span> <span data-ttu-id="c8cd5-210">Utilizzando l'esempio precedente di hello, hello della query in cui clausola deve toospecify col1 valori tra 2000101 e 20001231.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-210">Using hello previous example, hello query's where clause needs toospecify col1 values between 2000101 and 20001231.</span></span>
> 
> 

### <a name="e-create-single-column-statistics-with-all-hello-options"></a><span data-ttu-id="c8cd5-211">E.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-211">E.</span></span> <span data-ttu-id="c8cd5-212">Creare statistiche di colonna singola con tutte le opzioni di hello</span><span class="sxs-lookup"><span data-stu-id="c8cd5-212">Create single-column statistics with all hello options</span></span>
<span data-ttu-id="c8cd5-213">Naturalmente, è possibile, combinare insieme le opzioni di hello.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-213">You can, of course, combine hello options together.</span></span> <span data-ttu-id="c8cd5-214">esempio Hello seguente crea un oggetto statistiche filtrate con una dimensione di esempio personalizzati:</span><span class="sxs-lookup"><span data-stu-id="c8cd5-214">hello example below creates a filtered statistics object with a custom sample size:</span></span>

```sql
CREATE STATISTICS stats_col1 ON table1 (col1) WHERE col1 > '2000101' AND col1 < '20001231' WITH SAMPLE = 50 PERCENT;
```

<span data-ttu-id="c8cd5-215">Per informazioni di riferimento complete hello, vedere [CREATE STATISTICS] [ CREATE STATISTICS] su MSDN.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-215">For hello full reference, see [CREATE STATISTICS][CREATE STATISTICS] on MSDN.</span></span>

### <a name="f-create-multi-column-statistics"></a><span data-ttu-id="c8cd5-216">F.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-216">F.</span></span> <span data-ttu-id="c8cd5-217">Creare statistiche a più colonne</span><span class="sxs-lookup"><span data-stu-id="c8cd5-217">Create multi-column statistics</span></span>
<span data-ttu-id="c8cd5-218">semplicemente toocreate statistiche su più colonne, utilizzare hello precedenti esempi, ma specificare più colonne.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-218">toocreate a multi-column statistics, simply use hello previous examples, but specify more columns.</span></span>

> [!NOTE]
> <span data-ttu-id="c8cd5-219">Istogramma Hello, che viene utilizzato tooestimate numero di righe nel risultato della query hello, è disponibile solo per hello prima colonna nella definizione di oggetto statistiche hello.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-219">hello histogram, which is used tooestimate number of rows in hello query result, is only available for hello first column listed in hello statistics object definition.</span></span>
> 
> 

<span data-ttu-id="c8cd5-220">In questo esempio, istogramma hello è *prodotto\_categoria*.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-220">In this example, hello histogram is on *product\_category*.</span></span> <span data-ttu-id="c8cd5-221">Le statistiche tra le colonne vengono calcolate su *product\_category* e *product\_sub_c\ategory*:</span><span class="sxs-lookup"><span data-stu-id="c8cd5-221">Cross-column statistics are calculated on *product\_category* and *product\_sub_c\ategory*:</span></span>

```sql
CREATE STATISTICS stats_2cols ON table1 (product_category, product_sub_category) WHERE product_category > '2000101' AND product_category < '20001231' WITH SAMPLE = 50 PERCENT;
```

<span data-ttu-id="c8cd5-222">Poiché non esiste una correlazione tra *prodotto\_categoria* e *prodotto\_sub\_categoria*, un stat a più colonne possono essere utili se queste colonne sono accessibili in hello contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-222">Since there is a correlation between *product\_category* and *product\_sub\_category*, a multi-column stat can be useful if these columns are accessed at hello same time.</span></span>

### <a name="g-create-statistics-on-all-hello-columns-in-a-table"></a><span data-ttu-id="c8cd5-223">G.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-223">G.</span></span> <span data-ttu-id="c8cd5-224">Creare statistiche per tutte le colonne di hello in una tabella</span><span class="sxs-lookup"><span data-stu-id="c8cd5-224">Create statistics on all hello columns in a table</span></span>
<span data-ttu-id="c8cd5-225">Statistiche toocreate unidirezionale sono tooissues i comandi CREATE STATISTICS dopo la creazione tabella hello.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-225">One way toocreate statistics is tooissues CREATE STATISTICS commands after creating hello table.</span></span>

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

### <a name="h-use-a-stored-procedure-toocreate-statistics-on-all-columns-in-a-database"></a><span data-ttu-id="c8cd5-226">H.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-226">H.</span></span> <span data-ttu-id="c8cd5-227">Utilizzare le statistiche toocreate una stored procedure per tutte le colonne in un database</span><span class="sxs-lookup"><span data-stu-id="c8cd5-227">Use a stored procedure toocreate statistics on all columns in a database</span></span>
<span data-ttu-id="c8cd5-228">SQL Data Warehouse non dispone di un equivalente di stored procedure di sistema troppo [sp_create_stats] [] in SQL Server.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-228">SQL Data Warehouse does not have a system stored procedure equivalent too[sp_create_stats][] in SQL Server.</span></span> <span data-ttu-id="c8cd5-229">Questa stored procedure crea un oggetto statistiche di colonna singola per ogni colonna del database hello che non dispone già di statistiche.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-229">This stored procedure creates a single column statistics object on every column of hello database that doesn't already have statistics.</span></span>

<span data-ttu-id="c8cd5-230">Ciò permetterà di iniziare a progettare il database.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-230">This will help you get started with your database design.</span></span> <span data-ttu-id="c8cd5-231">È gratuito tooadapt è tooyour deve.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-231">Feel free tooadapt it tooyour needs.</span></span>

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

<span data-ttu-id="c8cd5-232">statistiche toocreate su tutte le colonne nella tabella hello con questa procedura, è sufficiente chiamare routine hello.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-232">toocreate statistics on all columns in hello table with this procedure, simply call hello procedure.</span></span>

```sql
prc_sqldw_create_stats;
```

## <a name="examples-update-statistics"></a><span data-ttu-id="c8cd5-233">Esempi: Aggiornare le statistiche</span><span class="sxs-lookup"><span data-stu-id="c8cd5-233">Examples: update statistics</span></span>
<span data-ttu-id="c8cd5-234">le statistiche tooupdate, è possibile:</span><span class="sxs-lookup"><span data-stu-id="c8cd5-234">tooupdate statistics, you can:</span></span>

1. <span data-ttu-id="c8cd5-235">Aggiornare un oggetto statistiche.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-235">Update one statistics object.</span></span> <span data-ttu-id="c8cd5-236">Specificare il nome di hello dell'oggetto statistiche desiderato tooupdate hello.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-236">Specify hello name of hello statistics object you wish tooupdate.</span></span>
2. <span data-ttu-id="c8cd5-237">Aggiornare tutti gli oggetti statistiche in una tabella.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-237">Update all statistics objects on a table.</span></span> <span data-ttu-id="c8cd5-238">Specificare il nome di hello della tabella di hello anziché un oggetto statistiche specifico.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-238">Specify hello name of hello table instead of one specific statistics object.</span></span>

### <a name="a-update-one-specific-statistics-object"></a><span data-ttu-id="c8cd5-239">R.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-239">A.</span></span> <span data-ttu-id="c8cd5-240">Aggiornare un oggetto statistiche specifico</span><span class="sxs-lookup"><span data-stu-id="c8cd5-240">Update one specific statistics object</span></span>
<span data-ttu-id="c8cd5-241">Utilizzare hello segue sintassi tooupdate un oggetto statistiche specifico:</span><span class="sxs-lookup"><span data-stu-id="c8cd5-241">Use hello following syntax tooupdate a specific statistics object:</span></span>

```sql
UPDATE STATISTICS [schema_name].[table_name]([stat_name]);
```

<span data-ttu-id="c8cd5-242">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="c8cd5-242">For example:</span></span>

```sql
UPDATE STATISTICS [dbo].[table1] ([stats_col1]);
```

<span data-ttu-id="c8cd5-243">Dall'aggiornamento di statistiche specifici oggetti, è possibile ridurre le statistiche di toomanage necessari tempo e risorse hello.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-243">By updating specific statistics objects, you can minimize hello time and resources required toomanage statistics.</span></span> <span data-ttu-id="c8cd5-244">Questa operazione richiede che alcuni considerato, tuttavia, toochoose hello migliore tooupdate oggetti statistiche.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-244">This requires some thought, though, toochoose hello best statistics objects tooupdate.</span></span>

### <a name="b-update-all-statistics-on-a-table"></a><span data-ttu-id="c8cd5-245">B.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-245">B.</span></span> <span data-ttu-id="c8cd5-246">Aggiornare tutte le statistiche in una tabella</span><span class="sxs-lookup"><span data-stu-id="c8cd5-246">Update all statistics on a table</span></span>
<span data-ttu-id="c8cd5-247">Mostra un metodo semplice per l'aggiornamento di tutti gli oggetti statistiche hello in una tabella.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-247">This shows a simple method for updating all hello statistics objects on a table.</span></span>

```sql
UPDATE STATISTICS [schema_name].[table_name];
```

<span data-ttu-id="c8cd5-248">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="c8cd5-248">For example:</span></span>

```sql
UPDATE STATISTICS dbo.table1;
```

<span data-ttu-id="c8cd5-249">Questa istruzione è facile toouse.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-249">This statement is easy toouse.</span></span> <span data-ttu-id="c8cd5-250">Ricorda però questo Aggiorna tutte le statistiche di tabella hello e pertanto potrebbe operare più del necessario.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-250">Just remember this updates all statistics on hello table, and therefore might perform more work than is necessary.</span></span> <span data-ttu-id="c8cd5-251">Se le prestazioni di hello non è un problema, questo è decisamente modo più semplice e completo hello tooguarantee statistiche siano aggiornate.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-251">If hello performance is not an issue, this is definitely hello easiest and most complete way tooguarantee statistics are up-to-date.</span></span>

> [!NOTE]
> <span data-ttu-id="c8cd5-252">Quando si aggiorna tutte le statistiche di una tabella, SQL Data Warehouse esegue una tabella di hello toosample analisi per ogni tipo di statistiche.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-252">When updating all statistics on a table, SQL Data Warehouse does a scan toosample hello table for each statistics.</span></span> <span data-ttu-id="c8cd5-253">Se la tabella hello è grande, dispone di un numero di colonne e molte statistiche, potrebbe essere più efficiente tooupdate singoli le statistiche in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-253">If hello table is large, has many columns, and many statistics, it might be more efficient tooupdate individual statistics based on need.</span></span>
> 
> 

<span data-ttu-id="c8cd5-254">Per un'implementazione di un `UPDATE STATISTICS` procedura vedere hello [tabelle temporanee] [ Temporary] articolo.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-254">For an implementation of an `UPDATE STATISTICS` procedure please see hello [Temporary Tables][Temporary] article.</span></span> <span data-ttu-id="c8cd5-255">il metodo di implementazione di Hello è leggermente diverso toohello `CREATE STATISTICS` procedura sopra indicata ma risultato finale hello è hello stesso.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-255">hello implementation method is slightly different toohello `CREATE STATISTICS` procedure above but hello end result is hello same.</span></span>

<span data-ttu-id="c8cd5-256">La sintassi completa di hello, vedere [Update Statistics] [ Update Statistics] su MSDN.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-256">For hello full syntax, see [Update Statistics][Update Statistics] on MSDN.</span></span>

## <a name="statistics-metadata"></a><span data-ttu-id="c8cd5-257">Metadati delle statistiche</span><span class="sxs-lookup"><span data-stu-id="c8cd5-257">Statistics metadata</span></span>
<span data-ttu-id="c8cd5-258">Esistono diverse vista di sistema e le funzioni che è possibile utilizzare toofind informazioni sulle statistiche.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-258">There are several system view and functions that you can use toofind information about statistics.</span></span> <span data-ttu-id="c8cd5-259">Ad esempio, è possibile visualizzare se un oggetto statistiche potrebbe essere obsolete utilizzando hello statistiche data funzione toosee quando le statistiche ultima create o aggiornate.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-259">For example, you can see if a statistics object might be out-of-date by using hello stats-date function toosee when statistics were last created or updated.</span></span>

### <a name="catalog-views-for-statistics"></a><span data-ttu-id="c8cd5-260">Viste del catalogo per le statistiche</span><span class="sxs-lookup"><span data-stu-id="c8cd5-260">Catalog views for statistics</span></span>
<span data-ttu-id="c8cd5-261">Queste visualizzazioni di sistema forniscono informazioni sulle statistiche:</span><span class="sxs-lookup"><span data-stu-id="c8cd5-261">These system views provide information about statistics:</span></span>

| <span data-ttu-id="c8cd5-262">Vista del catalogo</span><span class="sxs-lookup"><span data-stu-id="c8cd5-262">Catalog View</span></span> | <span data-ttu-id="c8cd5-263">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c8cd5-263">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="c8cd5-264">[sys.columns][sys.columns]</span><span class="sxs-lookup"><span data-stu-id="c8cd5-264">[sys.columns][sys.columns]</span></span> |<span data-ttu-id="c8cd5-265">Una riga per ogni colonna.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-265">One row for each column.</span></span> |
| <span data-ttu-id="c8cd5-266">[sys.objects][sys.objects]</span><span class="sxs-lookup"><span data-stu-id="c8cd5-266">[sys.objects][sys.objects]</span></span> |<span data-ttu-id="c8cd5-267">Una riga per ogni oggetto nel database di hello.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-267">One row for each object in hello database.</span></span> |
| <span data-ttu-id="c8cd5-268">[sys.schemas][sys.schemas]</span><span class="sxs-lookup"><span data-stu-id="c8cd5-268">[sys.schemas][sys.schemas]</span></span> |<span data-ttu-id="c8cd5-269">Una riga per ogni schema nel database di hello.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-269">One row for each schema in hello database.</span></span> |
| <span data-ttu-id="c8cd5-270">[sys.stats][sys.stats]</span><span class="sxs-lookup"><span data-stu-id="c8cd5-270">[sys.stats][sys.stats]</span></span> |<span data-ttu-id="c8cd5-271">Una riga per ogni oggetto statistiche.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-271">One row for each statistics object.</span></span> |
| <span data-ttu-id="c8cd5-272">[sys.stats_columns][sys.stats_columns]</span><span class="sxs-lookup"><span data-stu-id="c8cd5-272">[sys.stats_columns][sys.stats_columns]</span></span> |<span data-ttu-id="c8cd5-273">Una riga per ogni colonna nell'oggetto statistiche hello.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-273">One row for each column in hello statistics object.</span></span> <span data-ttu-id="c8cd5-274">Consente di tornare toosys.columns.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-274">Links back toosys.columns.</span></span> |
| <span data-ttu-id="c8cd5-275">[sys.tables][sys.tables]</span><span class="sxs-lookup"><span data-stu-id="c8cd5-275">[sys.tables][sys.tables]</span></span> |<span data-ttu-id="c8cd5-276">Una riga per ogni tabella (include le tabelle esterne).</span><span class="sxs-lookup"><span data-stu-id="c8cd5-276">One row for each table (includes external tables).</span></span> |
| <span data-ttu-id="c8cd5-277">[sys.table_types][sys.table_types]</span><span class="sxs-lookup"><span data-stu-id="c8cd5-277">[sys.table_types][sys.table_types]</span></span> |<span data-ttu-id="c8cd5-278">Una riga per ogni tipo di dati.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-278">One row for each data type.</span></span> |

### <a name="system-functions-for-statistics"></a><span data-ttu-id="c8cd5-279">Funzioni di sistema per le statistiche</span><span class="sxs-lookup"><span data-stu-id="c8cd5-279">System functions for statistics</span></span>
<span data-ttu-id="c8cd5-280">Queste funzioni di sistema sono utili per usare le statistiche:</span><span class="sxs-lookup"><span data-stu-id="c8cd5-280">These system functions are useful for working with statistics:</span></span>

| <span data-ttu-id="c8cd5-281">Funzioni di sistema</span><span class="sxs-lookup"><span data-stu-id="c8cd5-281">System Function</span></span> | <span data-ttu-id="c8cd5-282">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c8cd5-282">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="c8cd5-283">[STATS_DATE][STATS_DATE]</span><span class="sxs-lookup"><span data-stu-id="c8cd5-283">[STATS_DATE][STATS_DATE]</span></span> |<span data-ttu-id="c8cd5-284">Oggetto statistiche di hello data dell'ultimo aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-284">Date hello statistics object was last updated.</span></span> |
| <span data-ttu-id="c8cd5-285">[DBCC SHOW_STATISTICS][DBCC SHOW_STATISTICS]</span><span class="sxs-lookup"><span data-stu-id="c8cd5-285">[DBCC SHOW_STATISTICS][DBCC SHOW_STATISTICS]</span></span> |<span data-ttu-id="c8cd5-286">Fornisce informazioni di riepilogo livello e dettagliate sulla distribuzione dei valori di hello riconosciuto dall'oggetto statistiche hello.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-286">Provides summary level and detailed information about hello distribution of values as understood by hello statistics object.</span></span> |

### <a name="combine-statistics-columns-and-functions-into-one-view"></a><span data-ttu-id="c8cd5-287">Combinare le colonne delle statistiche e le funzioni in un'unica visualizzazione</span><span class="sxs-lookup"><span data-stu-id="c8cd5-287">Combine statistics columns and functions into one view</span></span>
<span data-ttu-id="c8cd5-288">Questa vista visualizza le colonne correlate tra loro toostatistics e risultati dalla funzione di hello [STATS_DATE()] [].</span><span class="sxs-lookup"><span data-stu-id="c8cd5-288">This view brings columns that relate toostatistics, and results from hello [STATS_DATE()][]function together.</span></span>

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

## <a name="dbcc-showstatistics-examples"></a><span data-ttu-id="c8cd5-289">Esempi di DBCC SHOW_STATISTICS()</span><span class="sxs-lookup"><span data-stu-id="c8cd5-289">DBCC SHOW_STATISTICS() examples</span></span>
<span data-ttu-id="c8cd5-290">DBCC SHOW_STATISTICS() Mostra i dati di hello contenuti all'interno di un oggetto statistiche.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-290">DBCC SHOW_STATISTICS() shows hello data held within a statistics object.</span></span> <span data-ttu-id="c8cd5-291">Questi dati sono costituiti da tre parti.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-291">This data comes in three parts.</span></span>

1. <span data-ttu-id="c8cd5-292">Intestazione</span><span class="sxs-lookup"><span data-stu-id="c8cd5-292">Header</span></span>
2. <span data-ttu-id="c8cd5-293">Vettore di densità</span><span class="sxs-lookup"><span data-stu-id="c8cd5-293">Density Vector</span></span>
3. <span data-ttu-id="c8cd5-294">Istogramma</span><span class="sxs-lookup"><span data-stu-id="c8cd5-294">Histogram</span></span>

<span data-ttu-id="c8cd5-295">metadati di intestazione Hello sulle statistiche di hello.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-295">hello header metadata about hello statistics.</span></span> <span data-ttu-id="c8cd5-296">Istogramma Hello Visualizza distribuzione hello dei valori nella prima colonna chiave di hello dell'oggetto statistiche hello.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-296">hello histogram displays hello distribution of values in hello first key column of hello statistics object.</span></span> <span data-ttu-id="c8cd5-297">vettore di densità Hello consente di misurare la correlazione tra colonne.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-297">hello density vector measures cross-column correlation.</span></span> <span data-ttu-id="c8cd5-298">SQLDW calcola le stime della cardinalità con i dati di hello nell'oggetto statistiche hello.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-298">SQLDW computes cardinality estimates with any of hello data in hello statistics object.</span></span>

### <a name="show-header-density-and-histogram"></a><span data-ttu-id="c8cd5-299">Mostrare l'intestazione, la densità e l'istogramma</span><span class="sxs-lookup"><span data-stu-id="c8cd5-299">Show header, density, and histogram</span></span>
<span data-ttu-id="c8cd5-300">Questo semplice esempio mostra tutte e tre le parti di un oggetto statistiche.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-300">This simple example shows all three parts of a statistics object.</span></span>

```sql
DBCC SHOW_STATISTICS([<schema_name>.<table_name>],<stats_name>)
```

<span data-ttu-id="c8cd5-301">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="c8cd5-301">For example:</span></span>

```sql
DBCC SHOW_STATISTICS (dbo.table1, stats_col1);
```

### <a name="show-one-or-more-parts-of-dbcc-showstatistics"></a><span data-ttu-id="c8cd5-302">Mostrare una o più parti di DBCC SHOW_STATISTICS();</span><span class="sxs-lookup"><span data-stu-id="c8cd5-302">Show one or more parts of DBCC SHOW_STATISTICS();</span></span>
<span data-ttu-id="c8cd5-303">Se si è solo interessati a visualizzare parti specifiche, utilizzare hello `WITH` clausola e specificare quali parti è desidera toosee:</span><span class="sxs-lookup"><span data-stu-id="c8cd5-303">If you are only interested in viewing specific parts, use hello `WITH` clause and specify which parts you want toosee:</span></span>

```sql
DBCC SHOW_STATISTICS([<schema_name>.<table_name>],<stats_name>) WITH stat_header, histogram, density_vector
```

<span data-ttu-id="c8cd5-304">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="c8cd5-304">For example:</span></span>

```sql
DBCC SHOW_STATISTICS (dbo.table1, stats_col1) WITH histogram, density_vector
```

## <a name="dbcc-showstatistics-differences"></a><span data-ttu-id="c8cd5-305">Differenze di DBCC SHOW_STATISTICS()</span><span class="sxs-lookup"><span data-stu-id="c8cd5-305">DBCC SHOW_STATISTICS() differences</span></span>
<span data-ttu-id="c8cd5-306">DBCC SHOW_STATISTICS() in modo più rigoroso viene implementato in SQL Data Warehouse confrontati tooSQL Server.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-306">DBCC SHOW_STATISTICS() is more strictly implemented in SQL Data Warehouse compared tooSQL Server.</span></span>

1. <span data-ttu-id="c8cd5-307">Le funzionalità non documentate non sono supportate</span><span class="sxs-lookup"><span data-stu-id="c8cd5-307">Undocumented features are not supported</span></span>
2. <span data-ttu-id="c8cd5-308">Non è possibile usare Stats_stream</span><span class="sxs-lookup"><span data-stu-id="c8cd5-308">Cannot use Stats_stream</span></span>
3. <span data-ttu-id="c8cd5-309">Non è possibile unire i risultati per sottoinsiemi specifici di dati statistici, ad esempio (STAT_HEADER JOIN DENSITY_VECTOR)</span><span class="sxs-lookup"><span data-stu-id="c8cd5-309">Cannot join results for specific subsets of statistics data e.g. (STAT_HEADER JOIN DENSITY_VECTOR)</span></span>
4. <span data-ttu-id="c8cd5-310">NO_INFOMSGS non può essere impostato per l'eliminazione del messaggio</span><span class="sxs-lookup"><span data-stu-id="c8cd5-310">NO_INFOMSGS cannot be set for message suppression</span></span>
5. <span data-ttu-id="c8cd5-311">Non è possibile usare le parentesi quadre per i nomi delle statistiche</span><span class="sxs-lookup"><span data-stu-id="c8cd5-311">Square brackets around statistics names cannot be used</span></span>
6. <span data-ttu-id="c8cd5-312">Impossibile utilizzare oggetti statistiche tooidentify i nomi di colonna</span><span class="sxs-lookup"><span data-stu-id="c8cd5-312">Cannot use column names tooidentify statistics objects</span></span>
7. <span data-ttu-id="c8cd5-313">L'errore personalizzato 2767 non è supportato</span><span class="sxs-lookup"><span data-stu-id="c8cd5-313">Custom error 2767 is not supported</span></span>

## <a name="next-steps"></a><span data-ttu-id="c8cd5-314">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c8cd5-314">Next steps</span></span>
<span data-ttu-id="c8cd5-315">Per altri dettagli, vedere [DBCC SHOW_STATISTICS][DBCC SHOW_STATISTICS] in MSDN.</span><span class="sxs-lookup"><span data-stu-id="c8cd5-315">For more details, see [DBCC SHOW_STATISTICS][DBCC SHOW_STATISTICS] on MSDN.</span></span>  <span data-ttu-id="c8cd5-316">toolearn, vedere gli articoli di hello in [Cenni preliminari su tabella][Overview], [tipi di dati tabella][Data Types], [la distribuzione di una tabella] [ Distribute], [L'indicizzazione di una tabella][Index], [il partizionamento di una tabella] [ Partition] e [ Tabelle temporanee][Temporary].</span><span class="sxs-lookup"><span data-stu-id="c8cd5-316">toolearn more, see hello articles on [Table Overview][Overview], [Table Data Types][Data Types], [Distributing a Table][Distribute], [Indexing a Table][Index],  [Partitioning a Table][Partition] and [Temporary Tables][Temporary].</span></span>  <span data-ttu-id="c8cd5-317">Per altre informazioni sulle procedure consigliate, vedere [Procedure consigliate per SQL Data Warehouse][SQL Data Warehouse Best Practices].</span><span class="sxs-lookup"><span data-stu-id="c8cd5-317">For more about best practices, see [SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices].</span></span>  

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
