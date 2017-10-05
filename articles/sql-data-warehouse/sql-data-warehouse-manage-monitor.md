---
title: Monitoraggio del carico di lavoro mediante DMV | Microsoft Docs
description: Informazioni sul monitoraggio del carico di lavoro mediante DMV.
services: sql-data-warehouse
documentationcenter: NA
author: sqlmojo
manager: jhubbard
editor: 
ms.assetid: 69ecd479-0941-48df-b3d0-cf54c79e6549
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: performance
ms.date: 10/31/2016
ms.author: joeyong;barbkess
ms.openlocfilehash: 7ce6c2cdf1e28852da536414533ccdcdaeb437e5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-your-workload-using-dmvs"></a><span data-ttu-id="e8481-103">Monitoraggio del carico di lavoro mediante DMV</span><span class="sxs-lookup"><span data-stu-id="e8481-103">Monitor your workload using DMVs</span></span>
<span data-ttu-id="e8481-104">In questo articolo viene descritto come utilizzare le viste a gestione dinamica (DMV) per monitorare il carico di lavoro ed esaminare l'esecuzione delle query SQL Data Warehouse di Azure.</span><span class="sxs-lookup"><span data-stu-id="e8481-104">This article describes how to use Dynamic Management Views (DMVs) to monitor your workload and investigate query execution in Azure SQL Data Warehouse.</span></span>

## <a name="permissions"></a><span data-ttu-id="e8481-105">Autorizzazioni</span><span class="sxs-lookup"><span data-stu-id="e8481-105">Permissions</span></span>
<span data-ttu-id="e8481-106">Per eseguire una query sulle DMV in questo articolo è necessaria l'autorizzazione VISUALIZZAZIONE STATO DEL DATABASE o CONTROLLO.</span><span class="sxs-lookup"><span data-stu-id="e8481-106">To query the DMVs in this article, you need either VIEW DATABASE STATE or CONTROL permission.</span></span> <span data-ttu-id="e8481-107">In genere si consiglia di concedere l'autorizzazione VISUALIZZAZIONE STATO DEL DATABASE poiché è molto più restrittiva.</span><span class="sxs-lookup"><span data-stu-id="e8481-107">Usually granting VIEW DATABASE STATE is the preferred permission as it is much more restrictive.</span></span>

```sql
GRANT VIEW DATABASE STATE TO myuser;
```

## <a name="monitor-connections"></a><span data-ttu-id="e8481-108">Monitorare le connessioni</span><span class="sxs-lookup"><span data-stu-id="e8481-108">Monitor connections</span></span>
<span data-ttu-id="e8481-109">Tutti gli accessi a SQL Data Warehouse vengono registrati in [sys.dm_pdw_exec_sessions][sys.dm_pdw_exec_sessions].</span><span class="sxs-lookup"><span data-stu-id="e8481-109">All logins to SQL Data Warehouse are logged to [sys.dm_pdw_exec_sessions][sys.dm_pdw_exec_sessions].</span></span>  <span data-ttu-id="e8481-110">Questa DMV contiene gli ultimi 10.000 accessi.</span><span class="sxs-lookup"><span data-stu-id="e8481-110">This DMV contains the last 10,000 logins.</span></span>  <span data-ttu-id="e8481-111">L'elemento session_id è la chiave primaria e viene assegnato in sequenza per ogni nuovo accesso.</span><span class="sxs-lookup"><span data-stu-id="e8481-111">The session_id is the primary key and is assigned sequentially for each new logon.</span></span>

```sql
-- Other Active Connections
SELECT * FROM sys.dm_pdw_exec_sessions where status <> 'Closed' and session_id <> session_id();
```

## <a name="monitor-query-execution"></a><span data-ttu-id="e8481-112">Monitorare l'esecuzione di query</span><span class="sxs-lookup"><span data-stu-id="e8481-112">Monitor query execution</span></span>
<span data-ttu-id="e8481-113">Tutte le query eseguite in SQL Data Warehouse vengono registrate in [sys.dm_pdw_exec_requests][sys.dm_pdw_exec_requests].</span><span class="sxs-lookup"><span data-stu-id="e8481-113">All queries executed on SQL Data Warehouse are logged to [sys.dm_pdw_exec_requests][sys.dm_pdw_exec_requests].</span></span>  <span data-ttu-id="e8481-114">Questa DMV contiene le ultime 10.000 query eseguite.</span><span class="sxs-lookup"><span data-stu-id="e8481-114">This DMV contains the last 10,000 queries executed.</span></span>  <span data-ttu-id="e8481-115">L'elemento request_id identifica in modo univoco ogni query ed è la chiave primaria per questa DMV.</span><span class="sxs-lookup"><span data-stu-id="e8481-115">The request_id uniquely identifies each query and is the primary key for this DMV.</span></span>  <span data-ttu-id="e8481-116">L'elemento request_id viene assegnato in sequenza per ogni nuova query ed è preceduto da un prefisso con QID, che indica l'ID query.</span><span class="sxs-lookup"><span data-stu-id="e8481-116">The request_id is assigned sequentially for each new query and is prefixed with QID, which stands for query ID.</span></span>  <span data-ttu-id="e8481-117">Se si esegue una query nella DMV per un dato session_id, vengono visualizzate tutte le query per un determinato accesso.</span><span class="sxs-lookup"><span data-stu-id="e8481-117">Querying this DMV for a given session_id shows all queries for a given logon.</span></span>

> [!NOTE]
> <span data-ttu-id="e8481-118">Le stored procedure usano più ID richiesta.</span><span class="sxs-lookup"><span data-stu-id="e8481-118">Stored procedures use multiple Request IDs.</span></span>  <span data-ttu-id="e8481-119">Gli ID richiesta vengono assegnati in ordine sequenziale.</span><span class="sxs-lookup"><span data-stu-id="e8481-119">Request IDs are assigned in sequential order.</span></span> 
> 
> 

<span data-ttu-id="e8481-120">Ecco i passaggi da seguire per analizzare i piani e i tempi di esecuzione delle query per una query specifica.</span><span class="sxs-lookup"><span data-stu-id="e8481-120">Here are steps to follow to investigate query execution plans and times for a particular query.</span></span>

### <a name="step-1-identify-the-query-you-wish-to-investigate"></a><span data-ttu-id="e8481-121">PASSAGGIO 1: individuare la query da analizzare</span><span class="sxs-lookup"><span data-stu-id="e8481-121">STEP 1: Identify the query you wish to investigate</span></span>
```sql
-- Monitor active queries
SELECT * 
FROM sys.dm_pdw_exec_requests 
WHERE status not in ('Completed','Failed','Cancelled')
  AND session_id <> session_id()
ORDER BY submit_time DESC;

-- Find top 10 queries longest running queries
SELECT TOP 10 * 
FROM sys.dm_pdw_exec_requests 
ORDER BY total_elapsed_time DESC;

-- Find a query with the Label 'My Query'
-- Use brackets when querying the label column, as it it a key word
SELECT  *
FROM    sys.dm_pdw_exec_requests
WHERE   [label] = 'My Query';
```

<span data-ttu-id="e8481-122">**Prendere nota dell'ID richiesta** della query che si desidera analizzare dai risultati della query precedente.</span><span class="sxs-lookup"><span data-stu-id="e8481-122">From the preceding query results, **note the Request ID** of the query that you would like to investigate.</span></span>

<span data-ttu-id="e8481-123">Le query con stato **Sospeso** vengono messe in coda a causa dei limiti di concorrenza.</span><span class="sxs-lookup"><span data-stu-id="e8481-123">Queries in the **Suspended** state are being queued due to concurrency limits.</span></span> <span data-ttu-id="e8481-124">Queste query vengono visualizzate anche nella query sys.dm_pdw_waits waits con un tipo UserConcurrencyResourceType.</span><span class="sxs-lookup"><span data-stu-id="e8481-124">These queries also appear in the sys.dm_pdw_waits waits query with a type of UserConcurrencyResourceType.</span></span> <span data-ttu-id="e8481-125">Per altre informazioni sui limiti di concorrenza, vedere [Gestione della concorrenza e del carico di lavoro][Concurrency and workload management].</span><span class="sxs-lookup"><span data-stu-id="e8481-125">See [Concurrency and workload management][Concurrency and workload management] for more details on concurrency limits.</span></span> <span data-ttu-id="e8481-126">L'attesa delle query può dipendere anche da altre motivazioni, come i blocchi degli oggetti.</span><span class="sxs-lookup"><span data-stu-id="e8481-126">Queries can also wait for other reasons such as for object locks.</span></span>  <span data-ttu-id="e8481-127">Se la query è in attesa di una risorsa, vedere [Analisi delle query in attesa di risorse][Investigating queries waiting for resources] più avanti in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="e8481-127">If your query is waiting for a resource, see [Investigating queries waiting for resources][Investigating queries waiting for resources] further down in this article.</span></span>

<span data-ttu-id="e8481-128">Per semplificare la ricerca di una query nella tabella sys.dm_pdw_exec_requests, usare [LABEL][LABEL] per assegnare alla query un commento che possa essere cercato nella visualizzazione sys.dm_pdw_exec_requests.</span><span class="sxs-lookup"><span data-stu-id="e8481-128">To simplify the lookup of a query in the sys.dm_pdw_exec_requests table, use [LABEL][LABEL] to assign a comment to your query that can be looked up in the sys.dm_pdw_exec_requests view.</span></span>

```sql
-- Query with Label
SELECT *
FROM sys.tables
OPTION (LABEL = 'My Query')
;
```

### <a name="step-2-investigate-the-query-plan"></a><span data-ttu-id="e8481-129">PASSAGGIO 2: Esaminare il piano di query</span><span class="sxs-lookup"><span data-stu-id="e8481-129">STEP 2: Investigate the query plan</span></span>
<span data-ttu-id="e8481-130">Usare l'ID richiesta per recuperare il piano Distributed SQL (DSQL) della query da [sys.dm_pdw_request_steps][sys.dm_pdw_request_steps].</span><span class="sxs-lookup"><span data-stu-id="e8481-130">Use the Request ID to retrieve the query's distributed SQL (DSQL) plan from [sys.dm_pdw_request_steps][sys.dm_pdw_request_steps].</span></span>

```sql
-- Find the distributed query plan steps for a specific query.
-- Replace request_id with value from Step 1.

SELECT * FROM sys.dm_pdw_request_steps
WHERE request_id = 'QID####'
ORDER BY step_index;
```

<span data-ttu-id="e8481-131">Quando un piano di DSQL impiega più tempo del previsto, la causa può essere un la complessità del piano, dovuta a molti passaggi di DSQL o a un solo passaggio che richiede molto tempo.</span><span class="sxs-lookup"><span data-stu-id="e8481-131">When a DSQL plan is taking longer than expected, the cause can be a complex plan with many DSQL steps or just one step taking a long time.</span></span>  <span data-ttu-id="e8481-132">Se il piano prevede molti passaggi con numerose operazioni di spostamento, prendere in considerazione di ottimizzare le distribuzioni di tabelle per ridurre lo spostamento dei dati.</span><span class="sxs-lookup"><span data-stu-id="e8481-132">If the plan is many steps with several move operations, consider optimizing your table distributions to reduce data movement.</span></span> <span data-ttu-id="e8481-133">L'articolo [Distribuzione di tabelle][Table distribution] spiega perché è necessario spostare i dati per risolvere una query e illustra alcune strategie di distribuzione per ridurre al minimo lo spostamento dei dati.</span><span class="sxs-lookup"><span data-stu-id="e8481-133">The [Table distribution][Table distribution] article explains why data must be moved to solve a query and explains some distribution strategies to minimize data movement.</span></span>

<span data-ttu-id="e8481-134">Per altre informazioni su un singolo passaggio, fare riferimento alla colonna *operation_type* del passaggio della query con esecuzione prolungata e all'**indice dei passaggi**:</span><span class="sxs-lookup"><span data-stu-id="e8481-134">To investigate further details about a single step, the *operation_type* column of the long-running query step and note the **Step Index**:</span></span>

* <span data-ttu-id="e8481-135">Procedere al passaggio 3a per le **operazioni SQL**: OnOperation, RemoteOperation, ReturnOperation.</span><span class="sxs-lookup"><span data-stu-id="e8481-135">Proceed with Step 3a for **SQL operations**: OnOperation, RemoteOperation, ReturnOperation.</span></span>
* <span data-ttu-id="e8481-136">Procedere al passaggio 3b per le **operazioni di spostamento dati**: ShuffleMoveOperation, BroadcastMoveOperation, TrimMoveOperation, PartitionMoveOperation, MoveOperation, CopyOperation.</span><span class="sxs-lookup"><span data-stu-id="e8481-136">Proceed with Step 3b for **Data Movement operations**: ShuffleMoveOperation, BroadcastMoveOperation, TrimMoveOperation, PartitionMoveOperation, MoveOperation, CopyOperation.</span></span>

### <a name="step-3a-investigate-sql-on-the-distributed-databases"></a><span data-ttu-id="e8481-137">PASSAGGIO 3a: Esaminare SQL nei database distribuiti</span><span class="sxs-lookup"><span data-stu-id="e8481-137">STEP 3a: Investigate SQL on the distributed databases</span></span>
<span data-ttu-id="e8481-138">Usare l'ID richiesta e l'indice dei passaggi per recuperare informazioni da [sys.dm_pdw_sql_requests][sys.dm_pdw_sql_requests], che contiene informazioni sull'esecuzione del passaggio della query in tutti i database distribuiti.</span><span class="sxs-lookup"><span data-stu-id="e8481-138">Use the Request ID and the Step Index to retrieve details from [sys.dm_pdw_sql_requests][sys.dm_pdw_sql_requests], which contains execution information of the query step on all of the distributed databases.</span></span>

```sql
-- Find the distribution run times for a SQL step.
-- Replace request_id and step_index with values from Step 1 and 3.

SELECT * FROM sys.dm_pdw_sql_requests
WHERE request_id = 'QID####' AND step_index = 2;
```

<span data-ttu-id="e8481-139">Quando è in esecuzione il passaggio della query, è possibile usare [DBCC PDW_SHOWEXECUTIONPLAN][DBCC PDW_SHOWEXECUTIONPLAN] per recuperare il piano stimato di SQL Server dalla cache dei piani di SQL Server per il passaggio di esecuzione in una distribuzione specifica.</span><span class="sxs-lookup"><span data-stu-id="e8481-139">When the query step is running, [DBCC PDW_SHOWEXECUTIONPLAN][DBCC PDW_SHOWEXECUTIONPLAN] can be used to retrieve the SQL Server estimated plan from the SQL Server plan cache for the step running on a particular distribution.</span></span>

```sql
-- Find the SQL Server execution plan for a query running on a specific SQL Data Warehouse Compute or Control node.
-- Replace distribution_id and spid with values from previous query.

DBCC PDW_SHOWEXECUTIONPLAN(1, 78);
```

### <a name="step-3b-investigate-data-movement-on-the-distributed-databases"></a><span data-ttu-id="e8481-140">PASSAGGIO 3b: Esaminare lo spostamento dei dati nei database distribuiti</span><span class="sxs-lookup"><span data-stu-id="e8481-140">STEP 3b: Investigate data movement on the distributed databases</span></span>
<span data-ttu-id="e8481-141">Usare l'ID richiesta e l'indice dei passaggi per recuperare informazioni sul passaggio di spostamento dei dati in esecuzione in ogni distribuzione da [sys.dm_pdw_dms_workers][sys.dm_pdw_dms_workers].</span><span class="sxs-lookup"><span data-stu-id="e8481-141">Use the Request ID and the Step Index to retrieve information about a data movement step running on each distribution from [sys.dm_pdw_dms_workers][sys.dm_pdw_dms_workers].</span></span>

```sql
-- Find the information about all the workers completing a Data Movement Step.
-- Replace request_id and step_index with values from Step 1 and 3.

SELECT * FROM sys.dm_pdw_dms_workers
WHERE request_id = 'QID####' AND step_index = 2;
```

* <span data-ttu-id="e8481-142">Controllare la colonna *total_elapsed_time* per verificare se una distribuzione particolare richiede più tempo per lo spostamento dei dati rispetto alle altre.</span><span class="sxs-lookup"><span data-stu-id="e8481-142">Check the *total_elapsed_time* column to see if a particular distribution is taking significantly longer than others for data movement.</span></span>
* <span data-ttu-id="e8481-143">Per la distribuzione con esecuzione prolungata, esaminare la colonna *rows_processed* e controllare se il numero di righe spostato da tale distribuzione è significativamente più grande rispetto alle altre.</span><span class="sxs-lookup"><span data-stu-id="e8481-143">For the long-running distribution, check the *rows_processed* column to see if the number of rows being moved from that distribution is significantly larger than others.</span></span> <span data-ttu-id="e8481-144">In caso affermativo, questo potrebbe indicare asimmetria dei dati sottostanti.</span><span class="sxs-lookup"><span data-stu-id="e8481-144">If so, this may indicate skew of your underlying data.</span></span>

<span data-ttu-id="e8481-145">Se la query è in esecuzione, è possibile usare [DBCC PDW_SHOWEXECUTIONPLAN][DBCC PDW_SHOWEXECUTIONPLAN] per recuperare il piano stimato di SQL Server dalla cache dei piani di SQL Server per il passaggio SQL in esecuzione per una distribuzione specifica.</span><span class="sxs-lookup"><span data-stu-id="e8481-145">If the query is running, [DBCC PDW_SHOWEXECUTIONPLAN][DBCC PDW_SHOWEXECUTIONPLAN] can be used to retrieve the SQL Server estimated plan from the SQL Server plan cache for the currently running SQL Step within a particular distribution.</span></span>

```sql
-- Find the SQL Server estimated plan for a query running on a specific SQL Data Warehouse Compute or Control node.
-- Replace distribution_id and spid with values from previous query.

DBCC PDW_SHOWEXECUTIONPLAN(55, 238);
```

<a name="waiting"></a>

## <a name="monitor-waiting-queries"></a><span data-ttu-id="e8481-146">Monitorare le query in attesa</span><span class="sxs-lookup"><span data-stu-id="e8481-146">Monitor waiting queries</span></span>
<span data-ttu-id="e8481-147">Se si rileva il mancato avanzamento di una query perché in attesa di una risorsa, ecco una query che mostra tutte le risorse attese da una query.</span><span class="sxs-lookup"><span data-stu-id="e8481-147">If you discover that your query is not making progress because it is waiting for a resource, here is a query that shows all the resources a query is waiting for.</span></span>

```sql
-- Find queries 
-- Replace request_id with value from Step 1.

SELECT waits.session_id,
      waits.request_id,  
      requests.command,
      requests.status,
      requests.start_time,  
      waits.type,
      waits.state,
      waits.object_type,
      waits.object_name
FROM   sys.dm_pdw_waits waits
   JOIN  sys.dm_pdw_exec_requests requests
   ON waits.request_id=requests.request_id
WHERE waits.request_id = 'QID####'
ORDER BY waits.object_name, waits.object_type, waits.state;
```

<span data-ttu-id="e8481-148">Se la query è attivamente in attesa di risorse da un'altra query, lo stato sarà **AcquireResources**.</span><span class="sxs-lookup"><span data-stu-id="e8481-148">If the query is actively waiting on resources from another query, then the state will be **AcquireResources**.</span></span>  <span data-ttu-id="e8481-149">Se la query dispone di tutte le risorse necessarie, lo stato sarà **Granted**.</span><span class="sxs-lookup"><span data-stu-id="e8481-149">If the query has all the required resources, then the state will be **Granted**.</span></span>

## <a name="monitor-tempdb"></a><span data-ttu-id="e8481-150">Monitorare tempdb</span><span class="sxs-lookup"><span data-stu-id="e8481-150">Monitor tempdb</span></span>
<span data-ttu-id="e8481-151">Un uso intensivo di tempdb può essere la causa principale del rallentamento delle prestazioni e dei problemi di memoria insufficiente.</span><span class="sxs-lookup"><span data-stu-id="e8481-151">High tempdb utilization can be the root cause for slow performance and out of memory issues.</span></span> <span data-ttu-id="e8481-152">In primo luogo verificare se sono presenti rowgroup di qualità insufficiente o asimmetria dei dati e adottare le misure appropriate.</span><span class="sxs-lookup"><span data-stu-id="e8481-152">Please first check if you have data skew or poor quality rowgroups and take the appropriate actions.</span></span> <span data-ttu-id="e8481-153">Se durante l'esecuzione di query tempdb raggiunge i limiti previsti, prendere in considerazione il ridimensionamento del data warehouse.</span><span class="sxs-lookup"><span data-stu-id="e8481-153">Consider scaling your data warehouse if you find tempdb reaching its limits during query execution.</span></span> <span data-ttu-id="e8481-154">Di seguito viene descritto come identificare l'uso di tempdb per ogni query in ogni nodo.</span><span class="sxs-lookup"><span data-stu-id="e8481-154">The following describes how to identify tempdb usage per query on each node.</span></span> 

<span data-ttu-id="e8481-155">Creare la vista seguente per associare l'ID nodo appropriato per sys.dm_pdw_sql_requests.</span><span class="sxs-lookup"><span data-stu-id="e8481-155">Create the following view to associate the appropriate node id for sys.dm_pdw_sql_requests.</span></span> <span data-ttu-id="e8481-156">In questo modo sarà possibile sfruttare altre DMV pass-through e unire le tabelle con sys.dm_pdw_sql_requests.</span><span class="sxs-lookup"><span data-stu-id="e8481-156">This will enable you to leverage other pass-through DMVs and join those tables with sys.dm_pdw_sql_requests.</span></span>

```sql
-- sys.dm_pdw_sql_requests with the correct node id
CREATE VIEW sql_requests AS
(SELECT
       sr.request_id,
       sr.step_index,
       (CASE 
              WHEN (sr.distribution_id = -1 ) THEN 
              (SELECT pdw_node_id FROM sys.dm_pdw_nodes WHERE type = 'CONTROL') 
              ELSE d.pdw_node_id END) AS pdw_node_id,
       sr.distribution_id,
       sr.status,
       sr.error_id,
       sr.start_time,
       sr.end_time,
       sr.total_elapsed_time,
       sr.row_count,
       sr.spid,
       sr.command
FROM sys.pdw_distributions AS d
RIGHT JOIN sys.dm_pdw_sql_requests AS sr ON d.distribution_id = sr.distribution_id)
```
<span data-ttu-id="e8481-157">Per monitorare tempdb eseguire la query seguente:</span><span class="sxs-lookup"><span data-stu-id="e8481-157">Run the following query to monitor tempdb:</span></span>

```sql
-- Monitor tempdb
SELECT
    sr.request_id,
    ssu.session_id,
    ssu.pdw_node_id,
    sr.command,
    sr.total_elapsed_time,
    es.login_name AS 'LoginName',
    DB_NAME(ssu.database_id) AS 'DatabaseName',
    (es.memory_usage * 8) AS 'MemoryUsage (in KB)',
    (ssu.user_objects_alloc_page_count * 8) AS 'Space Allocated For User Objects (in KB)',
    (ssu.user_objects_dealloc_page_count * 8) AS 'Space Deallocated For User Objects (in KB)',
    (ssu.internal_objects_alloc_page_count * 8) AS 'Space Allocated For Internal Objects (in KB)',
    (ssu.internal_objects_dealloc_page_count * 8) AS 'Space Deallocated For Internal Objects (in KB)',
    CASE es.is_user_process
    WHEN 1 THEN 'User Session'
    WHEN 0 THEN 'System Session'
    END AS 'SessionType',
    es.row_count AS 'RowCount'
FROM sys.dm_pdw_nodes_db_session_space_usage AS ssu
    INNER JOIN sys.dm_pdw_nodes_exec_sessions AS es ON ssu.session_id = es.session_id AND ssu.pdw_node_id = es.pdw_node_id
    INNER JOIN sys.dm_pdw_nodes_exec_connections AS er ON ssu.session_id = er.session_id AND ssu.pdw_node_id = er.pdw_node_id
    INNER JOIN sql_requests AS sr ON ssu.session_id = sr.spid AND ssu.pdw_node_id = sr.pdw_node_id
WHERE DB_NAME(ssu.database_id) = 'tempdb'
    AND es.session_id <> @@SPID
    AND es.login_name <> 'sa' 
ORDER BY sr.request_id;
```
## <a name="monitor-memory"></a><span data-ttu-id="e8481-158">Monitorare la memoria</span><span class="sxs-lookup"><span data-stu-id="e8481-158">Monitor memory</span></span>

<span data-ttu-id="e8481-159">La memoria può essere la causa principale del rallentamento delle prestazioni e dei problemi di memoria insufficiente.</span><span class="sxs-lookup"><span data-stu-id="e8481-159">Memory can be the root cause for slow performance and out of memory issues.</span></span> <span data-ttu-id="e8481-160">In primo luogo verificare se sono presenti rowgroup di qualità insufficiente o asimmetria dei dati e adottare le misure appropriate.</span><span class="sxs-lookup"><span data-stu-id="e8481-160">Please first check if you have data skew or poor quality rowgroups and take the appropriate actions.</span></span> <span data-ttu-id="e8481-161">Se durante l'esecuzione di query l'uso di memoria di SQL Server raggiunge i limiti previsti, prendere in considerazione il ridimensionamento del data warehouse.</span><span class="sxs-lookup"><span data-stu-id="e8481-161">Consider scaling your data warehouse if you find SQL Server memory usage reaching its limits during query execution.</span></span>

<span data-ttu-id="e8481-162">La query seguente restituisce l'uso di memoria di SQL Server e l'eventuale uso elevato in ogni nodo:</span><span class="sxs-lookup"><span data-stu-id="e8481-162">The following query returns SQL Server memory usage and memory pressure per node:</span></span>   
```sql
-- Memory consumption
SELECT
  pc1.cntr_value as Curr_Mem_KB, 
  pc1.cntr_value/1024.0 as Curr_Mem_MB,
  (pc1.cntr_value/1048576.0) as Curr_Mem_GB,
  pc2.cntr_value as Max_Mem_KB,
  pc2.cntr_value/1024.0 as Max_Mem_MB,
  (pc2.cntr_value/1048576.0) as Max_Mem_GB,
  pc1.cntr_value * 100.0/pc2.cntr_value AS Memory_Utilization_Percentage,
  pc1.pdw_node_id
FROM
-- pc1: current memory
sys.dm_pdw_nodes_os_performance_counters AS pc1
-- pc2: total memory allowed for this SQL instance
JOIN sys.dm_pdw_nodes_os_performance_counters AS pc2 
ON pc1.object_name = pc2.object_name AND pc1.pdw_node_id = pc2.pdw_node_id
WHERE
pc1.counter_name = 'Total Server Memory (KB)'
AND pc2.counter_name = 'Target Server Memory (KB)'
```
## <a name="monitor-transaction-log-size"></a><span data-ttu-id="e8481-163">Monitorare le dimensioni del log delle transazioni</span><span class="sxs-lookup"><span data-stu-id="e8481-163">Monitor transaction log size</span></span>
<span data-ttu-id="e8481-164">La query seguente restituisce le dimensioni del log delle transazioni per ogni distribuzione.</span><span class="sxs-lookup"><span data-stu-id="e8481-164">The following query returns the transaction log size on each distribution.</span></span> <span data-ttu-id="e8481-165">Verificare se sono presenti rowgroup di qualità insufficiente o asimmetria dei dati e adottare le misure appropriate.</span><span class="sxs-lookup"><span data-stu-id="e8481-165">Please check if you have data skew or poor quality rowgroups and take the appropriate actions.</span></span> <span data-ttu-id="e8481-166">Se uno dei file di log sta per raggiungere i 160 GB, considerare l'espansione dell'istanza del programma o la limitazione delle dimensioni delle transazioni.</span><span class="sxs-lookup"><span data-stu-id="e8481-166">If one of the log files is reaching 160GB, you should consider scaling up your instance or limiting your transaction size.</span></span> 
```sql
-- Transaction log size
SELECT
  instance_name as distribution_db,
  cntr_value*1.0/1048576 as log_file_size_used_GB,
  pdw_node_id 
FROM sys.dm_pdw_nodes_os_performance_counters 
WHERE 
instance_name like 'Distribution_%' 
AND counter_name = 'Log File(s) Used Size (KB)'
AND counter_name = 'Target Server Memory (KB)'
```
## <a name="monitor-transaction-log-rollback"></a><span data-ttu-id="e8481-167">Monitorare il ripristino dello stato precedente del log delle transazioni</span><span class="sxs-lookup"><span data-stu-id="e8481-167">Monitor transaction log rollback</span></span>
<span data-ttu-id="e8481-168">Se le query non vanno a buon fine o richiedono molto tempo, verificare se è in corso il ripristino dello stato precedente delle transazioni e monitorare questa operazione.</span><span class="sxs-lookup"><span data-stu-id="e8481-168">If your queries are failing or taking a long time to proceed, you can check and monitor if you have any transactions rolling back.</span></span>
```sql
-- Monitor rollback
SELECT 
    SUM(CASE WHEN t.database_transaction_next_undo_lsn IS NOT NULL THEN 1 ELSE 0 END),
    t.pdw_node_id,
    nod.[type]
FROM sys.dm_pdw_nodes_tran_database_transactions t
JOIN sys.dm_pdw_nodes nod ON t.pdw_node_id = nod.pdw_node_id
GROUP BY t.pdw_node_id, nod.[type]
```

## <a name="next-steps"></a><span data-ttu-id="e8481-169">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e8481-169">Next steps</span></span>
<span data-ttu-id="e8481-170">Per altre informazioni sulle DMV, vedere [Viste di sistema][System views].</span><span class="sxs-lookup"><span data-stu-id="e8481-170">See [System views][System views] for more information on DMVs.</span></span>
<span data-ttu-id="e8481-171">Per altre informazioni sulle procedure consigliate, vedere [Procedure consigliate per Azure SQL Data Warehouse][SQL Data Warehouse best practices]</span><span class="sxs-lookup"><span data-stu-id="e8481-171">See [SQL Data Warehouse best practices][SQL Data Warehouse best practices] for more information about best practices</span></span>

<!--Image references-->

<!--Article references-->
[Manage overview]: ./sql-data-warehouse-overview-manage.md
[SQL Data Warehouse best practices]: ./sql-data-warehouse-best-practices.md
[System views]: ./sql-data-warehouse-reference-tsql-system-views.md
[Table distribution]: ./sql-data-warehouse-tables-distribute.md
[Concurrency and workload management]: ./sql-data-warehouse-develop-concurrency.md
[Investigating queries waiting for resources]: ./sql-data-warehouse-manage-monitor.md#waiting

<!--MSDN references-->
[sys.dm_pdw_dms_workers]: http://msdn.microsoft.com/library/mt203878.aspx
[sys.dm_pdw_exec_requests]: http://msdn.microsoft.com/library/mt203887.aspx
[sys.dm_pdw_exec_sessions]: http://msdn.microsoft.com/library/mt203883.aspx
[sys.dm_pdw_request_steps]: http://msdn.microsoft.com/library/mt203913.aspx
[sys.dm_pdw_sql_requests]: http://msdn.microsoft.com/library/mt203889.aspx
[DBCC PDW_SHOWEXECUTIONPLAN]: http://msdn.microsoft.com/library/mt204017.aspx
[DBCC PDW_SHOWSPACEUSED]: http://msdn.microsoft.com/library/mt204028.aspx
[LABEL]: https://msdn.microsoft.com/library/ms190322.aspx
