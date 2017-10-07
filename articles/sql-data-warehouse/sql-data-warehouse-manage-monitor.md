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
# <a name="monitor-your-workload-using-dmvs"></a>Monitoraggio del carico di lavoro mediante DMV
Questo articolo viene descritto come toouse viste a gestione dinamica (DMV) toomonitor il carico di lavoro e analizzare l'esecuzione di query in Azure SQL Data Warehouse.

## <a name="permissions"></a>Autorizzazioni
hello tooquery DMV in questo articolo, è richiesta l'autorizzazione VIEW DATABASE STATE o controllo. Concessione di VIEW DATABASE STATE in genere è autorizzazione hello preferito perché è molto più restrittiva.

```sql
GRANT VIEW DATABASE STATE toomyuser;
```

## <a name="monitor-connections"></a>Monitorare le connessioni
Tutti gli account di accesso tooSQL Data Warehouse vengono registrate troppo[sys.dm_pdw_exec_sessions][sys.dm_pdw_exec_sessions].  Questa DMV contiene hello ultimo 10.000 account di accesso.  session_id Hello è la chiave primaria di hello e viene assegnato in sequenza per ogni nuovo account di accesso.

```sql
-- Other Active Connections
SELECT * FROM sys.dm_pdw_exec_sessions where status <> 'Closed' and session_id <> session_id();
```

## <a name="monitor-query-execution"></a>Monitorare l'esecuzione di query
Tutte le query eseguite in SQL Data Warehouse vengono registrate troppo[sys.dm_pdw_exec_requests][sys.dm_pdw_exec_requests].  Questa DMV contiene hello ultimo 10.000 query eseguite.  request_id Hello in modo univoco identifica ogni query ed è hello chiave primaria per questa DMV.  request_id Hello viene assegnato in sequenza per ogni nuova query ed è preceduto con QID, che è l'acronimo di ID di query.  Se si esegue una query nella DMV per un dato session_id, vengono visualizzate tutte le query per un determinato accesso.

> [!NOTE]
> Le stored procedure usano più ID richiesta.  Gli ID richiesta vengono assegnati in ordine sequenziale. 
> 
> 

Di seguito sono piani di esecuzione delle query tooinvestigate toofollow passaggi e le ore per una determinata query.

### <a name="step-1-identify-hello-query-you-wish-tooinvestigate"></a>PASSAGGIO 1: Identificare query hello desiderato tooinvestigate
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

Da hello precedono i risultati della query, **hello nota ID richiesta** di cui si desidera tooinvestigate query di hello.

Le query in hello **Suspended** stato sono accodata a causa di limiti tooconcurrency. Queste query vengono visualizzati anche nella query di attese di hello sys.dm_pdw_waits con un tipo di UserConcurrencyResourceType. Per altre informazioni sui limiti di concorrenza, vedere [Gestione della concorrenza e del carico di lavoro][Concurrency and workload management]. L'attesa delle query può dipendere anche da altre motivazioni, come i blocchi degli oggetti.  Se la query è in attesa di una risorsa, vedere [Analisi delle query in attesa di risorse][Investigating queries waiting for resources] più avanti in questo articolo.

ricerca di hello toosimplify di una query nella tabella sys.dm_pdw_exec_requests hello, utilizzare [etichetta] [ LABEL] tooassign una query di tooyour di commento che può essere cercata in visualizzazione sys.dm_pdw_exec_requests hello.

```sql
-- Query with Label
SELECT *
FROM sys.tables
OPTION (LABEL = 'My Query')
;
```

### <a name="step-2-investigate-hello-query-plan"></a>PASSAGGIO 2: Esaminare il piano di query hello
Utilizza distribuite SQL (DSQL) piano hello ID richiesta tooretrieve hello query [sys.dm_pdw_request_steps][sys.dm_pdw_request_steps].

```sql
-- Find hello distributed query plan steps for a specific query.
-- Replace request_id with value from Step 1.

SELECT * FROM sys.dm_pdw_request_steps
WHERE request_id = 'QID####'
ORDER BY step_index;
```

Quando un piano DSQL sta richiedendo più tempo del previsto, causa hello può essere un piano complesso con il numero di passaggi DSQL o solo un passaggio richiede molto tempo.  Se il piano di hello numerosi passaggi con numerose operazioni di spostamento, prendere in considerazione lo spostamento dei dati tooreduce distribuzioni la tabella di ottimizzazione. Hello [tabella distribuzione] [ Table distribution] articolo spiega perché i dati devono essere spostato toosolve una query e vengono illustrati alcuni spostamento dei dati di toominimize strategie di distribuzione.

tooinvestigate ulteriori dettagli su un unico passaggio, hello *operation_type* colonna di hello di passaggio e prendere nota di query con esecuzione prolungata hello **passaggio indice**:

* Procedere al passaggio 3a per le **operazioni SQL**: OnOperation, RemoteOperation, ReturnOperation.
* Procedere al passaggio 3b per le **operazioni di spostamento dati**: ShuffleMoveOperation, BroadcastMoveOperation, TrimMoveOperation, PartitionMoveOperation, MoveOperation, CopyOperation.

### <a name="step-3a-investigate-sql-on-hello-distributed-databases"></a>PASSAGGIO 3a: provare a utilizzare SQL nei database hello distribuita
Utilizzare hello ID richiesta e i dettagli di hello passaggio indice tooretrieve da [sys.dm_pdw_sql_requests][sys.dm_pdw_sql_requests], che contiene informazioni sull'esecuzione del passaggio della query hello su tutti i hello distribuiti i database.

```sql
-- Find hello distribution run times for a SQL step.
-- Replace request_id and step_index with values from Step 1 and 3.

SELECT * FROM sys.dm_pdw_sql_requests
WHERE request_id = 'QID####' AND step_index = 2;
```

Durante l'esecuzione del passaggio della query hello [DBCC PDW_SHOWEXECUTIONPLAN] [ DBCC PDW_SHOWEXECUTIONPLAN] può essere utilizzato tooretrieve piano stimato hello SQL Server dalla cache dei piani di SQL Server in esecuzione in un particolare passaggio di hello hello distribuzione.

```sql
-- Find hello SQL Server execution plan for a query running on a specific SQL Data Warehouse Compute or Control node.
-- Replace distribution_id and spid with values from previous query.

DBCC PDW_SHOWEXECUTIONPLAN(1, 78);
```

### <a name="step-3b-investigate-data-movement-on-hello-distributed-databases"></a>PASSAGGIO 3b: esaminare lo spostamento di dati nei database hello distribuita
Utilizzare hello ID richiesta e informazioni di tooretrieve indice passaggio su un passaggio di spostamento dei dati in esecuzione in ogni distribuzione da hello [sys.dm_pdw_dms_workers][sys.dm_pdw_dms_workers].

```sql
-- Find hello information about all hello workers completing a Data Movement Step.
-- Replace request_id and step_index with values from Step 1 and 3.

SELECT * FROM sys.dm_pdw_dms_workers
WHERE request_id = 'QID####' AND step_index = 2;
```

* Controllare hello *total_elapsed_time* toosee colonna se una distribuzione particolare impiega molto più tempo per lo spostamento dei dati.
* Per la distribuzione con esecuzione prolungata hello, controllare hello *rows_processed* toosee colonna se il numero di hello di righe viene spostato da tale distribuzione è significativamente più grande rispetto ad altri. In caso affermativo, questo potrebbe indicare asimmetria dei dati sottostanti.

Se l'esecuzione di query hello [DBCC PDW_SHOWEXECUTIONPLAN] [ DBCC PDW_SHOWEXECUTIONPLAN] può essere utilizzato tooretrieve piano stimato hello SQL Server dalla cache dei piani SQL Server per hello attualmente in esecuzione SQL passaggio all'interno di un particolare hello distribuzione.

```sql
-- Find hello SQL Server estimated plan for a query running on a specific SQL Data Warehouse Compute or Control node.
-- Replace distribution_id and spid with values from previous query.

DBCC PDW_SHOWEXECUTIONPLAN(55, 238);
```

<a name="waiting"></a>

## <a name="monitor-waiting-queries"></a>Monitorare le query in attesa
Se si rileva che la query è bloccato perché è in attesa per una risorsa, ecco una query che visualizza tutte le risorse di hello è in attesa che una query.

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

Se la query hello è attivamente in attesa di risorse da un'altra query, quindi sarà stato hello **AcquireResources**.  Se query hello dispone di tutte le risorse necessarie hello, allora sarà stato hello **Granted**.

## <a name="monitor-tempdb"></a>Monitorare tempdb
Utilizzo di tempdb elevata può essere hello causa per un rallentamento delle prestazioni e problemi di memoria insufficiente. Verificare innanzitutto se si dispone di gruppi di righe di dati o inclinazione di scarsa qualità e intraprendere azioni appropriate hello. Se durante l'esecuzione di query tempdb raggiunge i limiti previsti, prendere in considerazione il ridimensionamento del data warehouse. Hello seguenti viene descritto come tooidentify utilizzo di tempdb per ogni query in ogni nodo. 

Creare hello seguente id di nodo appropriato vista tooassociate hello per sys.dm_pdw_sql_requests. Ciò consentirà si tooleverage altre DMV pass-through e unire in join le tabelle con sys.dm_pdw_sql_requests.

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
Eseguire hello tempdb toomonitor query seguenti:

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
## <a name="monitor-memory"></a>Monitorare la memoria

Memoria può essere hello causa per un rallentamento delle prestazioni e problemi di memoria insufficiente. Verificare innanzitutto se si dispone di gruppi di righe di dati o inclinazione di scarsa qualità e intraprendere azioni appropriate hello. Se durante l'esecuzione di query l'uso di memoria di SQL Server raggiunge i limiti previsti, prendere in considerazione il ridimensionamento del data warehouse.

Hello seguente query restituisce a SQL Server memoria e utilizzo della memoria per ogni nodo: 
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
## <a name="monitor-transaction-log-size"></a>Monitorare le dimensioni del log delle transazioni
Hello query seguente restituisce dimensioni del log delle transazioni hello in ogni distribuzione. Verificare se si dispone di gruppi di righe di dati o inclinazione di scarsa qualità e intraprendere azioni appropriate hello. Se uno dei file di log hello è prossimo da 160GB, considerare la scalabilità verticale l'istanza o limitando le dimensioni delle transazioni. 
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
## <a name="monitor-transaction-log-rollback"></a>Monitorare il ripristino dello stato precedente del log delle transazioni
Se le query hanno esito negativo o richiede un tooproceed molto tempo, è possibile controllare e monitorare nel caso di eventuali transazioni di cui eseguire il rollback.
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

## <a name="next-steps"></a>Passaggi successivi
Per altre informazioni sulle DMV, vedere [Viste di sistema][System views].
Per altre informazioni sulle procedure consigliate, vedere [Procedure consigliate per Azure SQL Data Warehouse][SQL Data Warehouse best practices]

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
