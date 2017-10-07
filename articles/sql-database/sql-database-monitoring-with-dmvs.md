---
title: Azure SQL Database utilizzando viste a gestione dinamica aaaMonitoring | Documenti Microsoft
description: Informazioni su come toodetect e diagnosticare i problemi comuni di prestazioni tramite DMV viste toomonitor Database SQL di Microsoft Azure.
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
tags: 
ms.assetid: d08f505f-3c62-47d4-bab7-35c9a834b79b
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 01/10/2017
ms.author: carlrab
ms.openlocfilehash: 43d5fe2dd9a38d031e9334f6ad49fce5866e3bec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-azure-sql-database-using-dynamic-management-views"></a><span data-ttu-id="0a043-103">Monitoraggio del database SQL di Azure tramite le visualizzazioni di gestione dinamica</span><span class="sxs-lookup"><span data-stu-id="0a043-103">Monitoring Azure SQL Database using dynamic management views</span></span>
<span data-ttu-id="0a043-104">Database SQL di Microsoft Azure consente un subset di gestione dinamica Visualizza toodiagnose problemi di prestazioni che potrebbero essere causati da query bloccate o con esecuzione prolungata, colli di bottiglia delle risorse, piani di query insufficienti e così via.</span><span class="sxs-lookup"><span data-stu-id="0a043-104">Microsoft Azure SQL Database enables a subset of dynamic management views toodiagnose performance problems, which might be caused by blocked or long-running queries, resource bottlenecks, poor query plans, and so on.</span></span> <span data-ttu-id="0a043-105">In questo argomento vengono fornite informazioni su come toodetect problemi comuni di prestazioni utilizzando viste a gestione dinamica.</span><span class="sxs-lookup"><span data-stu-id="0a043-105">This topic provides information on how toodetect common performance problems by using dynamic management views.</span></span>

<span data-ttu-id="0a043-106">Il database SQL supporta parzialmente tre categorie di visualizzazioni a gestione dinamica:</span><span class="sxs-lookup"><span data-stu-id="0a043-106">SQL Database partially supports three categories of dynamic management views:</span></span>

* <span data-ttu-id="0a043-107">Visualizzazioni a gestione dinamica relative al database.</span><span class="sxs-lookup"><span data-stu-id="0a043-107">Database-related dynamic management views.</span></span>
* <span data-ttu-id="0a043-108">Visualizzazioni a gestione dinamica relative all'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="0a043-108">Execution-related dynamic management views.</span></span>
* <span data-ttu-id="0a043-109">Visualizzazioni a gestione dinamica relative alle transazioni.</span><span class="sxs-lookup"><span data-stu-id="0a043-109">Transaction-related dynamic management views.</span></span>

<span data-ttu-id="0a043-110">Per informazioni dettagliate sulle visualizzazioni a gestione dinamica, vedere [Visualizzazioni a gestione dinamica e funzioni (Transact-SQL)](https://msdn.microsoft.com/library/ms188754.aspx) nella documentazione Online di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="0a043-110">For detailed information on dynamic management views, see [Dynamic Management Views and Functions (Transact-SQL)](https://msdn.microsoft.com/library/ms188754.aspx) in SQL Server Books Online.</span></span>

## <a name="permissions"></a><span data-ttu-id="0a043-111">Autorizzazioni</span><span class="sxs-lookup"><span data-stu-id="0a043-111">Permissions</span></span>
<span data-ttu-id="0a043-112">Nel Database SQL, l'esecuzione di query in una visualizzazione a gestione dinamica richiede autorizzazioni **VIEW DATABASE STATE** .</span><span class="sxs-lookup"><span data-stu-id="0a043-112">In SQL Database, querying a dynamic management view requires **VIEW DATABASE STATE** permissions.</span></span> <span data-ttu-id="0a043-113">Hello **VIEW DATABASE STATE** autorizzazione restituisce informazioni su tutti gli oggetti nel database corrente hello.</span><span class="sxs-lookup"><span data-stu-id="0a043-113">hello **VIEW DATABASE STATE** permission returns information about all objects within hello current database.</span></span>
<span data-ttu-id="0a043-114">hello toogrant **VIEW DATABASE STATE** autorizzazione tooa specifico utente del database, eseguire hello seguente query:</span><span class="sxs-lookup"><span data-stu-id="0a043-114">toogrant hello **VIEW DATABASE STATE** permission tooa specific database user, run hello following query:</span></span>

```GRANT VIEW DATABASE STATE toodatabase_user; ```

<span data-ttu-id="0a043-115">In un'istanza di SQL Server locale, le viste a gestione dinamica restituiscono informazioni sullo stato del server.</span><span class="sxs-lookup"><span data-stu-id="0a043-115">In an instance of on-premises SQL Server, dynamic management views return server state information.</span></span> <span data-ttu-id="0a043-116">Nel database SQL, restituiscono informazioni relative esclusivamente al database logico corrente.</span><span class="sxs-lookup"><span data-stu-id="0a043-116">In SQL Database, they return information regarding your current logical database only.</span></span>

## <a name="calculating-database-size"></a><span data-ttu-id="0a043-117">Calcolo della dimensione del database</span><span class="sxs-lookup"><span data-stu-id="0a043-117">Calculating database size</span></span>
<span data-ttu-id="0a043-118">Hello query seguente restituisce hello delle dimensioni del database (in megabyte):</span><span class="sxs-lookup"><span data-stu-id="0a043-118">hello following query returns hello size of your database (in megabytes):</span></span>

```
-- Calculates hello size of hello database.
SELECT SUM(reserved_page_count)*8.0/1024
FROM sys.dm_db_partition_stats;
GO
```

<span data-ttu-id="0a043-119">Hello nella query seguente restituisce hello dimensioni dei singoli oggetti (in megabyte) nel database:</span><span class="sxs-lookup"><span data-stu-id="0a043-119">hello following query returns hello size of individual objects (in megabytes) in your database:</span></span>

```
-- Calculates hello size of individual database objects.
SELECT sys.objects.name, SUM(reserved_page_count) * 8.0 / 1024
FROM sys.dm_db_partition_stats, sys.objects
WHERE sys.dm_db_partition_stats.object_id = sys.objects.object_id
GROUP BY sys.objects.name;
GO
```

## <a name="monitoring-connections"></a><span data-ttu-id="0a043-120">Monitoraggio delle connessioni</span><span class="sxs-lookup"><span data-stu-id="0a043-120">Monitoring connections</span></span>
<span data-ttu-id="0a043-121">È possibile utilizzare hello [Sys.dm exec_connections](https://msdn.microsoft.com/library/ms181509.aspx) tooretrieve di informazioni sulle connessioni stabilite hello tooa specifici server Database SQL di Azure e i dettagli di hello di ogni connessione.</span><span class="sxs-lookup"><span data-stu-id="0a043-121">You can use hello [sys.dm_exec_connections](https://msdn.microsoft.com/library/ms181509.aspx) view tooretrieve information about hello connections established tooa specific Azure SQL Database server and hello details of each connection.</span></span> <span data-ttu-id="0a043-122">Inoltre, hello [Sys.dm exec_sessions](https://msdn.microsoft.com/library/ms176013.aspx) Vista è utile durante il recupero di informazioni su tutte le connessioni utente attive e le attività interne.</span><span class="sxs-lookup"><span data-stu-id="0a043-122">In addition, hello [sys.dm_exec_sessions](https://msdn.microsoft.com/library/ms176013.aspx) view is helpful when retrieving information about all active user connections and internal tasks.</span></span>
<span data-ttu-id="0a043-123">Hello nella query seguente recupera le informazioni sulla connessione corrente hello:</span><span class="sxs-lookup"><span data-stu-id="0a043-123">hello following query retrieves information on hello current connection:</span></span>

```
SELECT
    c.session_id, c.net_transport, c.encrypt_option,
    c.auth_scheme, s.host_name, s.program_name,
    s.client_interface_name, s.login_name, s.nt_domain,
    s.nt_user_name, s.original_login_name, c.connect_time,
    s.login_time
FROM sys.dm_exec_connections AS c
JOIN sys.dm_exec_sessions AS s
    ON c.session_id = s.session_id
WHERE c.session_id = @@SPID;
```

> [!NOTE]
> <span data-ttu-id="0a043-124">Durante l'esecuzione di hello **Sys.dm exec_requests** e **viste Sys.dm exec_sessions**, se sono presenti **VIEW DATABASE STATE** autorizzazioni sul database hello, vedere l'esecuzione di tutti sessioni nel database di hello; in caso contrario, vedrai hello solo la sessione corrente.</span><span class="sxs-lookup"><span data-stu-id="0a043-124">When executing hello **sys.dm_exec_requests** and **sys.dm_exec_sessions views**, if you have **VIEW DATABASE STATE** permission on hello database, you see all executing sessions on hello database; otherwise, you see only hello current session.</span></span>
> 
> 

## <a name="monitoring-query-performance"></a><span data-ttu-id="0a043-125">Monitoraggio delle prestazioni delle query</span><span class="sxs-lookup"><span data-stu-id="0a043-125">Monitoring query performance</span></span>
<span data-ttu-id="0a043-126">L’esecuzione della query rallentata o prolungata può consumare delle risorse di sistema importanti.</span><span class="sxs-lookup"><span data-stu-id="0a043-126">Slow or long running queries can consume significant system resources.</span></span> <span data-ttu-id="0a043-127">In questa sezione viene illustrato come toouse viste a gestione dinamica toodetect alcuni problemi comuni di prestazioni query.</span><span class="sxs-lookup"><span data-stu-id="0a043-127">This section demonstrates how toouse dynamic management views toodetect a few common query performance problems.</span></span> <span data-ttu-id="0a043-128">Un riferimento precedente ma comunque utile per risolvere il problema, è hello [risoluzione dei problemi di prestazioni in SQL Server 2008](http://download.microsoft.com/download/D/B/D/DBDE7972-1EB9-470A-BA18-58849DB3EB3B/TShootPerfProbs2008.docx) articolo su Microsoft TechNet.</span><span class="sxs-lookup"><span data-stu-id="0a043-128">An older but still helpful reference for troubleshooting, is hello [Troubleshooting Performance Problems in SQL Server 2008](http://download.microsoft.com/download/D/B/D/DBDE7972-1EB9-470A-BA18-58849DB3EB3B/TShootPerfProbs2008.docx) article on Microsoft TechNet.</span></span>

### <a name="finding-top-n-queries"></a><span data-ttu-id="0a043-129">Ricerca delle prime n query</span><span class="sxs-lookup"><span data-stu-id="0a043-129">Finding top N queries</span></span>
<span data-ttu-id="0a043-130">Hello esempio seguente vengono restituite informazioni su hello prime cinque query classificate in base al tempo medio della CPU.</span><span class="sxs-lookup"><span data-stu-id="0a043-130">hello following example returns information about hello top five queries ranked by average CPU time.</span></span> <span data-ttu-id="0a043-131">Nell'esempio le query hello in base a tootheir hash di query, in modo che le query logicamente equivalenti sono raggruppate per il consumo di risorse cumulativo.</span><span class="sxs-lookup"><span data-stu-id="0a043-131">This example aggregates hello queries according tootheir query hash, so that logically equivalent queries are grouped by their cumulative resource consumption.</span></span>

```
SELECT TOP 5 query_stats.query_hash AS "Query Hash",
    SUM(query_stats.total_worker_time) / SUM(query_stats.execution_count) AS "Avg CPU Time",
    MIN(query_stats.statement_text) AS "Statement Text"
FROM
    (SELECT QS.*,
    SUBSTRING(ST.text, (QS.statement_start_offset/2) + 1,
    ((CASE statement_end_offset
        WHEN -1 THEN DATALENGTH(ST.text)
        ELSE QS.statement_end_offset END
            - QS.statement_start_offset)/2) + 1) AS statement_text
     FROM sys.dm_exec_query_stats AS QS
     CROSS APPLY sys.dm_exec_sql_text(QS.sql_handle) as ST) as query_stats
GROUP BY query_stats.query_hash
ORDER BY 2 DESC;
```

### <a name="monitoring-blocked-queries"></a><span data-ttu-id="0a043-132">Monitoraggio delle query bloccate</span><span class="sxs-lookup"><span data-stu-id="0a043-132">Monitoring blocked queries</span></span>
<span data-ttu-id="0a043-133">Le query lente o con esecuzione prolungata possono contribuiscono tooexcessive consumo delle risorse ed essere conseguenza hello di query bloccate.</span><span class="sxs-lookup"><span data-stu-id="0a043-133">Slow or long-running queries can contribute tooexcessive resource consumption and be hello consequence of blocked queries.</span></span> <span data-ttu-id="0a043-134">causa Hello di hello blocco può essere progettazione dell'applicazione, cattivi hello mancanza di indici utili, i piani di query e così via.</span><span class="sxs-lookup"><span data-stu-id="0a043-134">hello cause of hello blocking can be poor application design, bad query plans, hello lack of useful indexes, and so on.</span></span> <span data-ttu-id="0a043-135">È possibile utilizzare hello Sys.dm tran_locks tooget informazioni sull'attività di blocco corrente hello in Database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="0a043-135">You can use hello sys.dm_tran_locks view tooget information about hello current locking activity in your Azure SQL Database.</span></span> <span data-ttu-id="0a043-136">Per un codice di esempio, vedere [sys.dm_tran_locks (Transact-SQL)](https://msdn.microsoft.com/library/ms190345.aspx) nella 	documentazione online di Microsoft SQL Server.</span><span class="sxs-lookup"><span data-stu-id="0a043-136">For example code, see [sys.dm_tran_locks (Transact-SQL)](https://msdn.microsoft.com/library/ms190345.aspx) in SQL Server Books Online.</span></span>

### <a name="monitoring-query-plans"></a><span data-ttu-id="0a043-137">Monitoraggio dei piani di query</span><span class="sxs-lookup"><span data-stu-id="0a043-137">Monitoring query plans</span></span>
<span data-ttu-id="0a043-138">Un piano di query inefficiente può anche aumentare il consumo della CPU.</span><span class="sxs-lookup"><span data-stu-id="0a043-138">An inefficient query plan also may increase CPU consumption.</span></span> <span data-ttu-id="0a043-139">esempio Hello utilizza hello [Sys.dm exec_query_stats](https://msdn.microsoft.com/library/ms189741.aspx) consente di visualizzare la query utilizza CPU cumulativa maggiore hello toodetermine.</span><span class="sxs-lookup"><span data-stu-id="0a043-139">hello following example uses hello [sys.dm_exec_query_stats](https://msdn.microsoft.com/library/ms189741.aspx) view toodetermine which query uses hello most cumulative CPU.</span></span>

```
SELECT
    highest_cpu_queries.plan_handle,
    highest_cpu_queries.total_worker_time,
    q.dbid,
    q.objectid,
    q.number,
    q.encrypted,
    q.[text]
FROM
    (SELECT TOP 50
        qs.plan_handle,
        qs.total_worker_time
    FROM
        sys.dm_exec_query_stats qs
    ORDER BY qs.total_worker_time desc) AS highest_cpu_queries
    CROSS APPLY sys.dm_exec_sql_text(plan_handle) AS q
ORDER BY highest_cpu_queries.total_worker_time DESC;
```

## <a name="see-also"></a><span data-ttu-id="0a043-140">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="0a043-140">See also</span></span>
[<span data-ttu-id="0a043-141">Introduzione tooSQL Database</span><span class="sxs-lookup"><span data-stu-id="0a043-141">Introduction tooSQL Database</span></span>](sql-database-technical-overview.md)

