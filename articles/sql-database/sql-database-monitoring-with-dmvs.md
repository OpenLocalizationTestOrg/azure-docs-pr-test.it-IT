---
title: Monitoraggio del database SQL di Azure tramite le visualizzazioni di gestione dinamica | Documentazione Microsoft
description: Informazioni su come rilevare e diagnosticare i problemi di prestazioni comuni utilizzando visualizzazioni a gestione dinamica per monitorare il Database SQL di Microsoft Azure.
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
ms.openlocfilehash: d9b007d29e06e672db71b4a8415673f258c3fd89
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="monitoring-azure-sql-database-using-dynamic-management-views"></a><span data-ttu-id="05d54-103">Monitoraggio del database SQL di Azure tramite le visualizzazioni di gestione dinamica</span><span class="sxs-lookup"><span data-stu-id="05d54-103">Monitoring Azure SQL Database using dynamic management views</span></span>
<span data-ttu-id="05d54-104">Il database SQL di Microsoft Azure consente a un sottoinsieme di visualizzazioni a gestione dinamica di diagnosticare i problemi delle prestazioni che potrebbero essere causati da query bloccate o con esecuzione prolungata, colli di bottiglia delle risorse, piani di query insufficienti e così via.</span><span class="sxs-lookup"><span data-stu-id="05d54-104">Microsoft Azure SQL Database enables a subset of dynamic management views to diagnose performance problems, which might be caused by blocked or long-running queries, resource bottlenecks, poor query plans, and so on.</span></span> <span data-ttu-id="05d54-105">Questo argomento fornisce informazioni su come rilevare problemi comuni relativi alle prestazioni tramite le DMV.</span><span class="sxs-lookup"><span data-stu-id="05d54-105">This topic provides information on how to detect common performance problems by using dynamic management views.</span></span>

<span data-ttu-id="05d54-106">Il database SQL supporta parzialmente tre categorie di visualizzazioni a gestione dinamica:</span><span class="sxs-lookup"><span data-stu-id="05d54-106">SQL Database partially supports three categories of dynamic management views:</span></span>

* <span data-ttu-id="05d54-107">Visualizzazioni a gestione dinamica relative al database.</span><span class="sxs-lookup"><span data-stu-id="05d54-107">Database-related dynamic management views.</span></span>
* <span data-ttu-id="05d54-108">Visualizzazioni a gestione dinamica relative all'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="05d54-108">Execution-related dynamic management views.</span></span>
* <span data-ttu-id="05d54-109">Visualizzazioni a gestione dinamica relative alle transazioni.</span><span class="sxs-lookup"><span data-stu-id="05d54-109">Transaction-related dynamic management views.</span></span>

<span data-ttu-id="05d54-110">Per informazioni dettagliate sulle visualizzazioni a gestione dinamica, vedere [Visualizzazioni a gestione dinamica e funzioni (Transact-SQL)](https://msdn.microsoft.com/library/ms188754.aspx) nella documentazione Online di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="05d54-110">For detailed information on dynamic management views, see [Dynamic Management Views and Functions (Transact-SQL)](https://msdn.microsoft.com/library/ms188754.aspx) in SQL Server Books Online.</span></span>

## <a name="permissions"></a><span data-ttu-id="05d54-111">Autorizzazioni</span><span class="sxs-lookup"><span data-stu-id="05d54-111">Permissions</span></span>
<span data-ttu-id="05d54-112">Nel Database SQL, l'esecuzione di query in una visualizzazione a gestione dinamica richiede autorizzazioni **VIEW DATABASE STATE** .</span><span class="sxs-lookup"><span data-stu-id="05d54-112">In SQL Database, querying a dynamic management view requires **VIEW DATABASE STATE** permissions.</span></span> <span data-ttu-id="05d54-113">Le autorizzazioni **VIEW DATABASE STATE** restituiscono informazioni su tutti gli oggetti all'interno del database corrente.</span><span class="sxs-lookup"><span data-stu-id="05d54-113">The **VIEW DATABASE STATE** permission returns information about all objects within the current database.</span></span>
<span data-ttu-id="05d54-114">Per concedere le autorizzazioni **VIEW DATABASE STATE** a un utente di database specifico, eseguire la query seguente:</span><span class="sxs-lookup"><span data-stu-id="05d54-114">To grant the **VIEW DATABASE STATE** permission to a specific database user, run the following query:</span></span>

```GRANT VIEW DATABASE STATE TO database_user; ```

<span data-ttu-id="05d54-115">In un'istanza di SQL Server locale, le viste a gestione dinamica restituiscono informazioni sullo stato del server.</span><span class="sxs-lookup"><span data-stu-id="05d54-115">In an instance of on-premises SQL Server, dynamic management views return server state information.</span></span> <span data-ttu-id="05d54-116">Nel database SQL, restituiscono informazioni relative esclusivamente al database logico corrente.</span><span class="sxs-lookup"><span data-stu-id="05d54-116">In SQL Database, they return information regarding your current logical database only.</span></span>

## <a name="calculating-database-size"></a><span data-ttu-id="05d54-117">Calcolo della dimensione del database</span><span class="sxs-lookup"><span data-stu-id="05d54-117">Calculating database size</span></span>
<span data-ttu-id="05d54-118">La seguente query restituisce la dimensione del database in megabyte:</span><span class="sxs-lookup"><span data-stu-id="05d54-118">The following query returns the size of your database (in megabytes):</span></span>

```
-- Calculates the size of the database.
SELECT SUM(reserved_page_count)*8.0/1024
FROM sys.dm_db_partition_stats;
GO
```

<span data-ttu-id="05d54-119">La query seguente restituisce le dimensioni dei singoli oggetti (in megabyte) nel database:</span><span class="sxs-lookup"><span data-stu-id="05d54-119">The following query returns the size of individual objects (in megabytes) in your database:</span></span>

```
-- Calculates the size of individual database objects.
SELECT sys.objects.name, SUM(reserved_page_count) * 8.0 / 1024
FROM sys.dm_db_partition_stats, sys.objects
WHERE sys.dm_db_partition_stats.object_id = sys.objects.object_id
GROUP BY sys.objects.name;
GO
```

## <a name="monitoring-connections"></a><span data-ttu-id="05d54-120">Monitoraggio delle connessioni</span><span class="sxs-lookup"><span data-stu-id="05d54-120">Monitoring connections</span></span>
<span data-ttu-id="05d54-121">È possibile usare la visualizzazione [sys.dm_exec_connections](https://msdn.microsoft.com/library/ms181509.aspx) per recuperare informazioni sulle connessioni stabilite con il server del database SQL specifico di Azure e i dettagli di ogni connessione.</span><span class="sxs-lookup"><span data-stu-id="05d54-121">You can use the [sys.dm_exec_connections](https://msdn.microsoft.com/library/ms181509.aspx) view to retrieve information about the connections established to a specific Azure SQL Database server and the details of each connection.</span></span> <span data-ttu-id="05d54-122">Inoltre, la visualizzazione [sys.dm_exec_sessions](https://msdn.microsoft.com/library/ms176013.aspx) è utile durante il recupero di informazioni su tutte le connessioni utente attive e le attività interne.</span><span class="sxs-lookup"><span data-stu-id="05d54-122">In addition, the [sys.dm_exec_sessions](https://msdn.microsoft.com/library/ms176013.aspx) view is helpful when retrieving information about all active user connections and internal tasks.</span></span>
<span data-ttu-id="05d54-123">La query seguente recupera le informazioni sulla connessione corrente.</span><span class="sxs-lookup"><span data-stu-id="05d54-123">The following query retrieves information on the current connection:</span></span>

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
> <span data-ttu-id="05d54-124">Quando si eseguono **sys.dm_exec_requests** e **sys.dm_exec_sessions**, se si dispone di un'autorizzazione **VIEW DATABASE STATE** sul database, saranno visibili tutte le sessioni in esecuzione sul database; in caso contrario, sarà visibile solo la sessione corrente.</span><span class="sxs-lookup"><span data-stu-id="05d54-124">When executing the **sys.dm_exec_requests** and **sys.dm_exec_sessions views**, if you have **VIEW DATABASE STATE** permission on the database, you see all executing sessions on the database; otherwise, you see only the current session.</span></span>
> 
> 

## <a name="monitoring-query-performance"></a><span data-ttu-id="05d54-125">Monitoraggio delle prestazioni delle query</span><span class="sxs-lookup"><span data-stu-id="05d54-125">Monitoring query performance</span></span>
<span data-ttu-id="05d54-126">L’esecuzione della query rallentata o prolungata può consumare delle risorse di sistema importanti.</span><span class="sxs-lookup"><span data-stu-id="05d54-126">Slow or long running queries can consume significant system resources.</span></span> <span data-ttu-id="05d54-127">In questa sezione viene illustrato come utilizzare le visualizzazioni a gestione dinamica per rilevare alcuni problemi di prestazione delle query comuni.</span><span class="sxs-lookup"><span data-stu-id="05d54-127">This section demonstrates how to use dynamic management views to detect a few common query performance problems.</span></span> <span data-ttu-id="05d54-128">Un riferimento precedente ma comunque utile per la risoluzione dei problemi, è l’articolo [Risoluzione dei problemi di prestazioni in SQL Server 2008](http://download.microsoft.com/download/D/B/D/DBDE7972-1EB9-470A-BA18-58849DB3EB3B/TShootPerfProbs2008.docx) su Microsoft TechNet.</span><span class="sxs-lookup"><span data-stu-id="05d54-128">An older but still helpful reference for troubleshooting, is the [Troubleshooting Performance Problems in SQL Server 2008](http://download.microsoft.com/download/D/B/D/DBDE7972-1EB9-470A-BA18-58849DB3EB3B/TShootPerfProbs2008.docx) article on Microsoft TechNet.</span></span>

### <a name="finding-top-n-queries"></a><span data-ttu-id="05d54-129">Ricerca delle prime n query</span><span class="sxs-lookup"><span data-stu-id="05d54-129">Finding top N queries</span></span>
<span data-ttu-id="05d54-130">Nell'esempio seguente vengono restituite informazioni sulle prime cinque query classificate in base al tempo medio della CPU.</span><span class="sxs-lookup"><span data-stu-id="05d54-130">The following example returns information about the top five queries ranked by average CPU time.</span></span> <span data-ttu-id="05d54-131">Nell'esempio le query vengono aggregate in base al relativo valore hash, in modo da raggruppare le query logicamente equivalenti in base all'utilizzo di risorse cumulativo.</span><span class="sxs-lookup"><span data-stu-id="05d54-131">This example aggregates the queries according to their query hash, so that logically equivalent queries are grouped by their cumulative resource consumption.</span></span>

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

### <a name="monitoring-blocked-queries"></a><span data-ttu-id="05d54-132">Monitoraggio delle query bloccate</span><span class="sxs-lookup"><span data-stu-id="05d54-132">Monitoring blocked queries</span></span>
<span data-ttu-id="05d54-133">Le query lente o con esecuzione prolungata possono contribuire al consumo eccessivo delle risorse ed essere la conseguenza di query bloccate.</span><span class="sxs-lookup"><span data-stu-id="05d54-133">Slow or long-running queries can contribute to excessive resource consumption and be the consequence of blocked queries.</span></span> <span data-ttu-id="05d54-134">Le cause del blocco possono essere una progettazione povera dell'applicazione, dei piani di query non validi, la mancanza di indici utili e così via.</span><span class="sxs-lookup"><span data-stu-id="05d54-134">The cause of the blocking can be poor application design, bad query plans, the lack of useful indexes, and so on.</span></span> <span data-ttu-id="05d54-135">È possibile utilizzare la visualizzazione in sys.dm_tran_locks per ottenere informazioni sulle attività di blocco corrente nel Database di SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="05d54-135">You can use the sys.dm_tran_locks view to get information about the current locking activity in your Azure SQL Database.</span></span> <span data-ttu-id="05d54-136">Per un codice di esempio, vedere [sys.dm_tran_locks (Transact-SQL)](https://msdn.microsoft.com/library/ms190345.aspx) nella 	documentazione online di Microsoft SQL Server.</span><span class="sxs-lookup"><span data-stu-id="05d54-136">For example code, see [sys.dm_tran_locks (Transact-SQL)](https://msdn.microsoft.com/library/ms190345.aspx) in SQL Server Books Online.</span></span>

### <a name="monitoring-query-plans"></a><span data-ttu-id="05d54-137">Monitoraggio dei piani di query</span><span class="sxs-lookup"><span data-stu-id="05d54-137">Monitoring query plans</span></span>
<span data-ttu-id="05d54-138">Un piano di query inefficiente può anche aumentare il consumo della CPU.</span><span class="sxs-lookup"><span data-stu-id="05d54-138">An inefficient query plan also may increase CPU consumption.</span></span> <span data-ttu-id="05d54-139">Nell'esempio seguente viene usata la visualizzazione [sys.dm_exec_query_stats](https://msdn.microsoft.com/library/ms189741.aspx) per determinare la query che usa la CPU cumulativa maggiore.</span><span class="sxs-lookup"><span data-stu-id="05d54-139">The following example uses the [sys.dm_exec_query_stats](https://msdn.microsoft.com/library/ms189741.aspx) view to determine which query uses the most cumulative CPU.</span></span>

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

## <a name="see-also"></a><span data-ttu-id="05d54-140">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="05d54-140">See also</span></span>
[<span data-ttu-id="05d54-141">Introduzione al Database SQL</span><span class="sxs-lookup"><span data-stu-id="05d54-141">Introduction to SQL Database</span></span>](sql-database-technical-overview.md)

