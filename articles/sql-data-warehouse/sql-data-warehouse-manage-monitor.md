---
title: aaaMonitor il carico di lavoro mediante DMV | Documenti Microsoft
description: Informazioni su come toomonitor il carico di lavoro mediante DMV.
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
ms.openlocfilehash: acccf952d165ccec3de3b4b1c633b18bbbf78077
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-your-workload-using-dmvs"></a><span data-ttu-id="658b5-103">Monitoraggio del carico di lavoro mediante DMV</span><span class="sxs-lookup"><span data-stu-id="658b5-103">Monitor your workload using DMVs</span></span>
<span data-ttu-id="658b5-104">Questo articolo viene descritto come toouse viste a gestione dinamica (DMV) toomonitor il carico di lavoro e analizzare l'esecuzione di query in Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="658b5-104">This article describes how toouse Dynamic Management Views (DMVs) toomonitor your workload and investigate query execution in Azure SQL Data Warehouse.</span></span>

## <a name="permissions"></a><span data-ttu-id="658b5-105">Autorizzazioni</span><span class="sxs-lookup"><span data-stu-id="658b5-105">Permissions</span></span>
<span data-ttu-id="658b5-106">hello tooquery DMV in questo articolo, è richiesta l'autorizzazione VIEW DATABASE STATE o controllo.</span><span class="sxs-lookup"><span data-stu-id="658b5-106">tooquery hello DMVs in this article, you need either VIEW DATABASE STATE or CONTROL permission.</span></span> <span data-ttu-id="658b5-107">Concessione di VIEW DATABASE STATE in genere è autorizzazione hello preferito perché è molto più restrittiva.</span><span class="sxs-lookup"><span data-stu-id="658b5-107">Usually granting VIEW DATABASE STATE is hello preferred permission as it is much more restrictive.</span></span>

```sql
GRANT VIEW DATABASE STATE toomyuser;
```

## <a name="monitor-connections"></a><span data-ttu-id="658b5-108">Monitorare le connessioni</span><span class="sxs-lookup"><span data-stu-id="658b5-108">Monitor connections</span></span>
<span data-ttu-id="658b5-109">Tutti gli account di accesso tooSQL Data Warehouse vengono registrate troppo[sys.dm_pdw_exec_sessions][sys.dm_pdw_exec_sessions].</span><span class="sxs-lookup"><span data-stu-id="658b5-109">All logins tooSQL Data Warehouse are logged too[sys.dm_pdw_exec_sessions][sys.dm_pdw_exec_sessions].</span></span>  <span data-ttu-id="658b5-110">Questa DMV contiene hello ultimo 10.000 account di accesso.</span><span class="sxs-lookup"><span data-stu-id="658b5-110">This DMV contains hello last 10,000 logins.</span></span>  <span data-ttu-id="658b5-111">session_id Hello è la chiave primaria di hello e viene assegnato in sequenza per ogni nuovo account di accesso.</span><span class="sxs-lookup"><span data-stu-id="658b5-111">hello session_id is hello primary key and is assigned sequentially for each new logon.</span></span>

```sql
-- Other Active Connections
SELECT * FROM sys.dm_pdw_exec_sessions where status <> 'Closed' and session_id <> session_id();
```

## <a name="monitor-query-execution"></a><span data-ttu-id="658b5-112">Monitorare l'esecuzione di query</span><span class="sxs-lookup"><span data-stu-id="658b5-112">Monitor query execution</span></span>
<span data-ttu-id="658b5-113">Tutte le query eseguite in SQL Data Warehouse vengono registrate troppo[sys.dm_pdw_exec_requests][sys.dm_pdw_exec_requests].</span><span class="sxs-lookup"><span data-stu-id="658b5-113">All queries executed on SQL Data Warehouse are logged too[sys.dm_pdw_exec_requests][sys.dm_pdw_exec_requests].</span></span>  <span data-ttu-id="658b5-114">Questa DMV contiene hello ultimo 10.000 query eseguite.</span><span class="sxs-lookup"><span data-stu-id="658b5-114">This DMV contains hello last 10,000 queries executed.</span></span>  <span data-ttu-id="658b5-115">request_id Hello in modo univoco identifica ogni query ed è hello chiave primaria per questa DMV.</span><span class="sxs-lookup"><span data-stu-id="658b5-115">hello request_id uniquely identifies each query and is hello primary key for this DMV.</span></span>  <span data-ttu-id="658b5-116">request_id Hello viene assegnato in sequenza per ogni nuova query ed è preceduto con QID, che è l'acronimo di ID di query.</span><span class="sxs-lookup"><span data-stu-id="658b5-116">hello request_id is assigned sequentially for each new query and is prefixed with QID, which stands for query ID.</span></span>  <span data-ttu-id="658b5-117">Se si esegue una query nella DMV per un dato session_id, vengono visualizzate tutte le query per un determinato accesso.</span><span class="sxs-lookup"><span data-stu-id="658b5-117">Querying this DMV for a given session_id shows all queries for a given logon.</span></span>

> [!NOTE]
> <span data-ttu-id="658b5-118">Le stored procedure usano più ID richiesta.</span><span class="sxs-lookup"><span data-stu-id="658b5-118">Stored procedures use multiple Request IDs.</span></span>  <span data-ttu-id="658b5-119">Gli ID richiesta vengono assegnati in ordine sequenziale.</span><span class="sxs-lookup"><span data-stu-id="658b5-119">Request IDs are assigned in sequential order.</span></span> 
> 
> 

<span data-ttu-id="658b5-120">Di seguito sono piani di esecuzione delle query tooinvestigate toofollow passaggi e le ore per una determinata query.</span><span class="sxs-lookup"><span data-stu-id="658b5-120">Here are steps toofollow tooinvestigate query execution plans and times for a particular query.</span></span>

### <a name="step-1-identify-hello-query-you-wish-tooinvestigate"></a><span data-ttu-id="658b5-121">PASSAGGIO 1: Identificare query hello desiderato tooinvestigate</span><span class="sxs-lookup"><span data-stu-id="658b5-121">STEP 1: Identify hello query you wish tooinvestigate</span></span>
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

-- Find a query with hello Label 'My Query'
-- Use brackets when querying hello label column, as it it a key word
SELECT  *
FROM    sys.dm_pdw_exec_requests
WHERE   [label] = 'My Query';
```

<span data-ttu-id="658b5-122">Da hello precedono i risultati della query, **hello nota ID richiesta** di cui si desidera tooinvestigate query di hello.</span><span class="sxs-lookup"><span data-stu-id="658b5-122">From hello preceding query results, **note hello Request ID** of hello query that you would like tooinvestigate.</span></span>

<span data-ttu-id="658b5-123">Le query in hello **Suspended** stato sono accodata a causa di limiti tooconcurrency.</span><span class="sxs-lookup"><span data-stu-id="658b5-123">Queries in hello **Suspended** state are being queued due tooconcurrency limits.</span></span> <span data-ttu-id="658b5-124">Queste query vengono visualizzati anche nella query di attese di hello sys.dm_pdw_waits con un tipo di UserConcurrencyResourceType.</span><span class="sxs-lookup"><span data-stu-id="658b5-124">These queries also appear in hello sys.dm_pdw_waits waits query with a type of UserConcurrencyResourceType.</span></span> <span data-ttu-id="658b5-125">Per altre informazioni sui limiti di concorrenza, vedere [Gestione della concorrenza e del carico di lavoro][Concurrency and workload management].</span><span class="sxs-lookup"><span data-stu-id="658b5-125">See [Concurrency and workload management][Concurrency and workload management] for more details on concurrency limits.</span></span> <span data-ttu-id="658b5-126">L'attesa delle query può dipendere anche da altre motivazioni, come i blocchi degli oggetti.</span><span class="sxs-lookup"><span data-stu-id="658b5-126">Queries can also wait for other reasons such as for object locks.</span></span>  <span data-ttu-id="658b5-127">Se la query è in attesa di una risorsa, vedere [Analisi delle query in attesa di risorse][Investigating queries waiting for resources] più avanti in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="658b5-127">If your query is waiting for a resource, see [Investigating queries waiting for resources][Investigating queries waiting for resources] further down in this article.</span></span>

<span data-ttu-id="658b5-128">ricerca di hello toosimplify di una query nella tabella sys.dm_pdw_exec_requests hello, utilizzare [etichetta] [ LABEL] tooassign una query di tooyour di commento che può essere cercata in visualizzazione sys.dm_pdw_exec_requests hello.</span><span class="sxs-lookup"><span data-stu-id="658b5-128">toosimplify hello lookup of a query in hello sys.dm_pdw_exec_requests table, use [LABEL][LABEL] tooassign a comment tooyour query that can be looked up in hello sys.dm_pdw_exec_requests view.</span></span>

```sql
-- Query with Label
SELECT *
FROM sys.tables
OPTION (LABEL = 'My Query')
;
```

### <a name="step-2-investigate-hello-query-plan"></a><span data-ttu-id="658b5-129">PASSAGGIO 2: Esaminare il piano di query hello</span><span class="sxs-lookup"><span data-stu-id="658b5-129">STEP 2: Investigate hello query plan</span></span>
<span data-ttu-id="658b5-130">Utilizza distribuite SQL (DSQL) piano hello ID richiesta tooretrieve hello query [sys.dm_pdw_request_steps][sys.dm_pdw_request_steps].</span><span class="sxs-lookup"><span data-stu-id="658b5-130">Use hello Request ID tooretrieve hello query's distributed SQL (DSQL) plan from [sys.dm_pdw_request_steps][sys.dm_pdw_request_steps].</span></span>

```sql
-- Find hello distributed query plan steps for a specific query.
-- Replace request_id with value from Step 1.

SELECT * FROM sys.dm_pdw_request_steps
WHERE request_id = 'QID####'
ORDER BY step_index;
```

<span data-ttu-id="658b5-131">Quando un piano DSQL sta richiedendo più tempo del previsto, causa hello può essere un piano complesso con il numero di passaggi DSQL o solo un passaggio richiede molto tempo.</span><span class="sxs-lookup"><span data-stu-id="658b5-131">When a DSQL plan is taking longer than expected, hello cause can be a complex plan with many DSQL steps or just one step taking a long time.</span></span>  <span data-ttu-id="658b5-132">Se il piano di hello numerosi passaggi con numerose operazioni di spostamento, prendere in considerazione lo spostamento dei dati tooreduce distribuzioni la tabella di ottimizzazione.</span><span class="sxs-lookup"><span data-stu-id="658b5-132">If hello plan is many steps with several move operations, consider optimizing your table distributions tooreduce data movement.</span></span> <span data-ttu-id="658b5-133">Hello [tabella distribuzione] [ Table distribution] articolo spiega perché i dati devono essere spostato toosolve una query e vengono illustrati alcuni spostamento dei dati di toominimize strategie di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="658b5-133">hello [Table distribution][Table distribution] article explains why data must be moved toosolve a query and explains some distribution strategies toominimize data movement.</span></span>

<span data-ttu-id="658b5-134">tooinvestigate ulteriori dettagli su un unico passaggio, hello *operation_type* colonna di hello di passaggio e prendere nota di query con esecuzione prolungata hello **passaggio indice**:</span><span class="sxs-lookup"><span data-stu-id="658b5-134">tooinvestigate further details about a single step, hello *operation_type* column of hello long-running query step and note hello **Step Index**:</span></span>

* <span data-ttu-id="658b5-135">Procedere al passaggio 3a per le **operazioni SQL**: OnOperation, RemoteOperation, ReturnOperation.</span><span class="sxs-lookup"><span data-stu-id="658b5-135">Proceed with Step 3a for **SQL operations**: OnOperation, RemoteOperation, ReturnOperation.</span></span>
* <span data-ttu-id="658b5-136">Procedere al passaggio 3b per le **operazioni di spostamento dati**: ShuffleMoveOperation, BroadcastMoveOperation, TrimMoveOperation, PartitionMoveOperation, MoveOperation, CopyOperation.</span><span class="sxs-lookup"><span data-stu-id="658b5-136">Proceed with Step 3b for **Data Movement operations**: ShuffleMoveOperation, BroadcastMoveOperation, TrimMoveOperation, PartitionMoveOperation, MoveOperation, CopyOperation.</span></span>

### <a name="step-3a-investigate-sql-on-hello-distributed-databases"></a><span data-ttu-id="658b5-137">PASSAGGIO 3a: provare a utilizzare SQL nei database hello distribuita</span><span class="sxs-lookup"><span data-stu-id="658b5-137">STEP 3a: Investigate SQL on hello distributed databases</span></span>
<span data-ttu-id="658b5-138">Utilizzare hello ID richiesta e i dettagli di hello passaggio indice tooretrieve da [sys.dm_pdw_sql_requests][sys.dm_pdw_sql_requests], che contiene informazioni sull'esecuzione del passaggio della query hello su tutti i hello distribuiti i database.</span><span class="sxs-lookup"><span data-stu-id="658b5-138">Use hello Request ID and hello Step Index tooretrieve details from [sys.dm_pdw_sql_requests][sys.dm_pdw_sql_requests], which contains execution information of hello query step on all of hello distributed databases.</span></span>

```sql
-- Find hello distribution run times for a SQL step.
-- Replace request_id and step_index with values from Step 1 and 3.

SELECT * FROM sys.dm_pdw_sql_requests
WHERE request_id = 'QID####' AND step_index = 2;
```

<span data-ttu-id="658b5-139">Durante l'esecuzione del passaggio della query hello [DBCC PDW_SHOWEXECUTIONPLAN] [ DBCC PDW_SHOWEXECUTIONPLAN] può essere utilizzato tooretrieve piano stimato hello SQL Server dalla cache dei piani di SQL Server in esecuzione in un particolare passaggio di hello hello distribuzione.</span><span class="sxs-lookup"><span data-stu-id="658b5-139">When hello query step is running, [DBCC PDW_SHOWEXECUTIONPLAN][DBCC PDW_SHOWEXECUTIONPLAN] can be used tooretrieve hello SQL Server estimated plan from hello SQL Server plan cache for hello step running on a particular distribution.</span></span>

```sql
-- Find hello SQL Server execution plan for a query running on a specific SQL Data Warehouse Compute or Control node.
-- Replace distribution_id and spid with values from previous query.

DBCC PDW_SHOWEXECUTIONPLAN(1, 78);
```

### <a name="step-3b-investigate-data-movement-on-hello-distributed-databases"></a><span data-ttu-id="658b5-140">PASSAGGIO 3b: esaminare lo spostamento di dati nei database hello distribuita</span><span class="sxs-lookup"><span data-stu-id="658b5-140">STEP 3b: Investigate data movement on hello distributed databases</span></span>
<span data-ttu-id="658b5-141">Utilizzare hello ID richiesta e informazioni di tooretrieve indice passaggio su un passaggio di spostamento dei dati in esecuzione in ogni distribuzione da hello [sys.dm_pdw_dms_workers][sys.dm_pdw_dms_workers].</span><span class="sxs-lookup"><span data-stu-id="658b5-141">Use hello Request ID and hello Step Index tooretrieve information about a data movement step running on each distribution from [sys.dm_pdw_dms_workers][sys.dm_pdw_dms_workers].</span></span>

```sql
-- Find hello information about all hello workers completing a Data Movement Step.
-- Replace request_id and step_index with values from Step 1 and 3.

SELECT * FROM sys.dm_pdw_dms_workers
WHERE request_id = 'QID####' AND step_index = 2;
```

* <span data-ttu-id="658b5-142">Controllare hello *total_elapsed_time* toosee colonna se una distribuzione particolare impiega molto più tempo per lo spostamento dei dati.</span><span class="sxs-lookup"><span data-stu-id="658b5-142">Check hello *total_elapsed_time* column toosee if a particular distribution is taking significantly longer than others for data movement.</span></span>
* <span data-ttu-id="658b5-143">Per la distribuzione con esecuzione prolungata hello, controllare hello *rows_processed* toosee colonna se il numero di hello di righe viene spostato da tale distribuzione è significativamente più grande rispetto ad altri.</span><span class="sxs-lookup"><span data-stu-id="658b5-143">For hello long-running distribution, check hello *rows_processed* column toosee if hello number of rows being moved from that distribution is significantly larger than others.</span></span> <span data-ttu-id="658b5-144">In caso affermativo, questo potrebbe indicare asimmetria dei dati sottostanti.</span><span class="sxs-lookup"><span data-stu-id="658b5-144">If so, this may indicate skew of your underlying data.</span></span>

<span data-ttu-id="658b5-145">Se l'esecuzione di query hello [DBCC PDW_SHOWEXECUTIONPLAN] [ DBCC PDW_SHOWEXECUTIONPLAN] può essere utilizzato tooretrieve piano stimato hello SQL Server dalla cache dei piani SQL Server per hello attualmente in esecuzione SQL passaggio all'interno di un particolare hello distribuzione.</span><span class="sxs-lookup"><span data-stu-id="658b5-145">If hello query is running, [DBCC PDW_SHOWEXECUTIONPLAN][DBCC PDW_SHOWEXECUTIONPLAN] can be used tooretrieve hello SQL Server estimated plan from hello SQL Server plan cache for hello currently running SQL Step within a particular distribution.</span></span>

```sql
-- Find hello SQL Server estimated plan for a query running on a specific SQL Data Warehouse Compute or Control node.
-- Replace distribution_id and spid with values from previous query.

DBCC PDW_SHOWEXECUTIONPLAN(55, 238);
```

<a name="waiting"></a>

## <a name="monitor-waiting-queries"></a><span data-ttu-id="658b5-146">Monitorare le query in attesa</span><span class="sxs-lookup"><span data-stu-id="658b5-146">Monitor waiting queries</span></span>
<span data-ttu-id="658b5-147">Se si rileva che la query è bloccato perché è in attesa per una risorsa, ecco una query che visualizza tutte le risorse di hello è in attesa che una query.</span><span class="sxs-lookup"><span data-stu-id="658b5-147">If you discover that your query is not making progress because it is waiting for a resource, here is a query that shows all hello resources a query is waiting for.</span></span>

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

<span data-ttu-id="658b5-148">Se la query hello è attivamente in attesa di risorse da un'altra query, quindi sarà stato hello **AcquireResources**.</span><span class="sxs-lookup"><span data-stu-id="658b5-148">If hello query is actively waiting on resources from another query, then hello state will be **AcquireResources**.</span></span>  <span data-ttu-id="658b5-149">Se query hello dispone di tutte le risorse necessarie hello, allora sarà stato hello **Granted**.</span><span class="sxs-lookup"><span data-stu-id="658b5-149">If hello query has all hello required resources, then hello state will be **Granted**.</span></span>

## <a name="monitor-tempdb"></a><span data-ttu-id="658b5-150">Monitorare tempdb</span><span class="sxs-lookup"><span data-stu-id="658b5-150">Monitor tempdb</span></span>
<span data-ttu-id="658b5-151">Utilizzo di tempdb elevata può essere hello causa per un rallentamento delle prestazioni e problemi di memoria insufficiente.</span><span class="sxs-lookup"><span data-stu-id="658b5-151">High tempdb utilization can be hello root cause for slow performance and out of memory issues.</span></span> <span data-ttu-id="658b5-152">Verificare innanzitutto se si dispone di gruppi di righe di dati o inclinazione di scarsa qualità e intraprendere azioni appropriate hello.</span><span class="sxs-lookup"><span data-stu-id="658b5-152">Please first check if you have data skew or poor quality rowgroups and take hello appropriate actions.</span></span> <span data-ttu-id="658b5-153">Se durante l'esecuzione di query tempdb raggiunge i limiti previsti, prendere in considerazione il ridimensionamento del data warehouse.</span><span class="sxs-lookup"><span data-stu-id="658b5-153">Consider scaling your data warehouse if you find tempdb reaching its limits during query execution.</span></span> <span data-ttu-id="658b5-154">Hello seguenti viene descritto come tooidentify utilizzo di tempdb per ogni query in ogni nodo.</span><span class="sxs-lookup"><span data-stu-id="658b5-154">hello following describes how tooidentify tempdb usage per query on each node.</span></span> 

<span data-ttu-id="658b5-155">Creare hello seguente id di nodo appropriato vista tooassociate hello per sys.dm_pdw_sql_requests.</span><span class="sxs-lookup"><span data-stu-id="658b5-155">Create hello following view tooassociate hello appropriate node id for sys.dm_pdw_sql_requests.</span></span> <span data-ttu-id="658b5-156">Ciò consentirà si tooleverage altre DMV pass-through e unire in join le tabelle con sys.dm_pdw_sql_requests.</span><span class="sxs-lookup"><span data-stu-id="658b5-156">This will enable you tooleverage other pass-through DMVs and join those tables with sys.dm_pdw_sql_requests.</span></span>

```sql
-- sys.dm_pdw_sql_requests with hello correct node id
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
<span data-ttu-id="658b5-157">Eseguire hello tempdb toomonitor query seguenti:</span><span class="sxs-lookup"><span data-stu-id="658b5-157">Run hello following query toomonitor tempdb:</span></span>

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
## <a name="monitor-memory"></a><span data-ttu-id="658b5-158">Monitorare la memoria</span><span class="sxs-lookup"><span data-stu-id="658b5-158">Monitor memory</span></span>

<span data-ttu-id="658b5-159">Memoria può essere hello causa per un rallentamento delle prestazioni e problemi di memoria insufficiente.</span><span class="sxs-lookup"><span data-stu-id="658b5-159">Memory can be hello root cause for slow performance and out of memory issues.</span></span> <span data-ttu-id="658b5-160">Verificare innanzitutto se si dispone di gruppi di righe di dati o inclinazione di scarsa qualità e intraprendere azioni appropriate hello.</span><span class="sxs-lookup"><span data-stu-id="658b5-160">Please first check if you have data skew or poor quality rowgroups and take hello appropriate actions.</span></span> <span data-ttu-id="658b5-161">Se durante l'esecuzione di query l'uso di memoria di SQL Server raggiunge i limiti previsti, prendere in considerazione il ridimensionamento del data warehouse.</span><span class="sxs-lookup"><span data-stu-id="658b5-161">Consider scaling your data warehouse if you find SQL Server memory usage reaching its limits during query execution.</span></span>

<span data-ttu-id="658b5-162">Hello seguente query restituisce a SQL Server memoria e utilizzo della memoria per ogni nodo:</span><span class="sxs-lookup"><span data-stu-id="658b5-162">hello following query returns SQL Server memory usage and memory pressure per node:</span></span> 
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
## <a name="monitor-transaction-log-size"></a><span data-ttu-id="658b5-163">Monitorare le dimensioni del log delle transazioni</span><span class="sxs-lookup"><span data-stu-id="658b5-163">Monitor transaction log size</span></span>
<span data-ttu-id="658b5-164">Hello query seguente restituisce dimensioni del log delle transazioni hello in ogni distribuzione.</span><span class="sxs-lookup"><span data-stu-id="658b5-164">hello following query returns hello transaction log size on each distribution.</span></span> <span data-ttu-id="658b5-165">Verificare se si dispone di gruppi di righe di dati o inclinazione di scarsa qualità e intraprendere azioni appropriate hello.</span><span class="sxs-lookup"><span data-stu-id="658b5-165">Please check if you have data skew or poor quality rowgroups and take hello appropriate actions.</span></span> <span data-ttu-id="658b5-166">Se uno dei file di log hello è prossimo da 160GB, considerare la scalabilità verticale l'istanza o limitando le dimensioni delle transazioni.</span><span class="sxs-lookup"><span data-stu-id="658b5-166">If one of hello log files is reaching 160GB, you should consider scaling up your instance or limiting your transaction size.</span></span> 
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
## <a name="monitor-transaction-log-rollback"></a><span data-ttu-id="658b5-167">Monitorare il ripristino dello stato precedente del log delle transazioni</span><span class="sxs-lookup"><span data-stu-id="658b5-167">Monitor transaction log rollback</span></span>
<span data-ttu-id="658b5-168">Se le query hanno esito negativo o richiede un tooproceed molto tempo, è possibile controllare e monitorare nel caso di eventuali transazioni di cui eseguire il rollback.</span><span class="sxs-lookup"><span data-stu-id="658b5-168">If your queries are failing or taking a long time tooproceed, you can check and monitor if you have any transactions rolling back.</span></span>
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

## <a name="next-steps"></a><span data-ttu-id="658b5-169">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="658b5-169">Next steps</span></span>
<span data-ttu-id="658b5-170">Per altre informazioni sulle DMV, vedere [Viste di sistema][System views].</span><span class="sxs-lookup"><span data-stu-id="658b5-170">See [System views][System views] for more information on DMVs.</span></span>
<span data-ttu-id="658b5-171">Per altre informazioni sulle procedure consigliate, vedere [Procedure consigliate per Azure SQL Data Warehouse][SQL Data Warehouse best practices]</span><span class="sxs-lookup"><span data-stu-id="658b5-171">See [SQL Data Warehouse best practices][SQL Data Warehouse best practices] for more information about best practices</span></span>

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
