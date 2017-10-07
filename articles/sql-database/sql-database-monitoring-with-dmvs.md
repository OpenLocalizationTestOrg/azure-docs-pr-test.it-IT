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
# <a name="monitoring-azure-sql-database-using-dynamic-management-views"></a>Monitoraggio del database SQL di Azure tramite le visualizzazioni di gestione dinamica
Database SQL di Microsoft Azure consente un subset di gestione dinamica Visualizza toodiagnose problemi di prestazioni che potrebbero essere causati da query bloccate o con esecuzione prolungata, colli di bottiglia delle risorse, piani di query insufficienti e così via. In questo argomento vengono fornite informazioni su come toodetect problemi comuni di prestazioni utilizzando viste a gestione dinamica.

Il database SQL supporta parzialmente tre categorie di visualizzazioni a gestione dinamica:

* Visualizzazioni a gestione dinamica relative al database.
* Visualizzazioni a gestione dinamica relative all'esecuzione.
* Visualizzazioni a gestione dinamica relative alle transazioni.

Per informazioni dettagliate sulle visualizzazioni a gestione dinamica, vedere [Visualizzazioni a gestione dinamica e funzioni (Transact-SQL)](https://msdn.microsoft.com/library/ms188754.aspx) nella documentazione Online di SQL Server.

## <a name="permissions"></a>Autorizzazioni
Nel Database SQL, l'esecuzione di query in una visualizzazione a gestione dinamica richiede autorizzazioni **VIEW DATABASE STATE** . Hello **VIEW DATABASE STATE** autorizzazione restituisce informazioni su tutti gli oggetti nel database corrente hello.
hello toogrant **VIEW DATABASE STATE** autorizzazione tooa specifico utente del database, eseguire hello seguente query:

```GRANT VIEW DATABASE STATE toodatabase_user; ```

In un'istanza di SQL Server locale, le viste a gestione dinamica restituiscono informazioni sullo stato del server. Nel database SQL, restituiscono informazioni relative esclusivamente al database logico corrente.

## <a name="calculating-database-size"></a>Calcolo della dimensione del database
Hello query seguente restituisce hello delle dimensioni del database (in megabyte):

```
-- Calculates hello size of hello database.
SELECT SUM(reserved_page_count)*8.0/1024
FROM sys.dm_db_partition_stats;
GO
```

Hello nella query seguente restituisce hello dimensioni dei singoli oggetti (in megabyte) nel database:

```
-- Calculates hello size of individual database objects.
SELECT sys.objects.name, SUM(reserved_page_count) * 8.0 / 1024
FROM sys.dm_db_partition_stats, sys.objects
WHERE sys.dm_db_partition_stats.object_id = sys.objects.object_id
GROUP BY sys.objects.name;
GO
```

## <a name="monitoring-connections"></a>Monitoraggio delle connessioni
È possibile utilizzare hello [Sys.dm exec_connections](https://msdn.microsoft.com/library/ms181509.aspx) tooretrieve di informazioni sulle connessioni stabilite hello tooa specifici server Database SQL di Azure e i dettagli di hello di ogni connessione. Inoltre, hello [Sys.dm exec_sessions](https://msdn.microsoft.com/library/ms176013.aspx) Vista è utile durante il recupero di informazioni su tutte le connessioni utente attive e le attività interne.
Hello nella query seguente recupera le informazioni sulla connessione corrente hello:

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
> Durante l'esecuzione di hello **Sys.dm exec_requests** e **viste Sys.dm exec_sessions**, se sono presenti **VIEW DATABASE STATE** autorizzazioni sul database hello, vedere l'esecuzione di tutti sessioni nel database di hello; in caso contrario, vedrai hello solo la sessione corrente.
> 
> 

## <a name="monitoring-query-performance"></a>Monitoraggio delle prestazioni delle query
L’esecuzione della query rallentata o prolungata può consumare delle risorse di sistema importanti. In questa sezione viene illustrato come toouse viste a gestione dinamica toodetect alcuni problemi comuni di prestazioni query. Un riferimento precedente ma comunque utile per risolvere il problema, è hello [risoluzione dei problemi di prestazioni in SQL Server 2008](http://download.microsoft.com/download/D/B/D/DBDE7972-1EB9-470A-BA18-58849DB3EB3B/TShootPerfProbs2008.docx) articolo su Microsoft TechNet.

### <a name="finding-top-n-queries"></a>Ricerca delle prime n query
Hello esempio seguente vengono restituite informazioni su hello prime cinque query classificate in base al tempo medio della CPU. Nell'esempio le query hello in base a tootheir hash di query, in modo che le query logicamente equivalenti sono raggruppate per il consumo di risorse cumulativo.

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

### <a name="monitoring-blocked-queries"></a>Monitoraggio delle query bloccate
Le query lente o con esecuzione prolungata possono contribuiscono tooexcessive consumo delle risorse ed essere conseguenza hello di query bloccate. causa Hello di hello blocco può essere progettazione dell'applicazione, cattivi hello mancanza di indici utili, i piani di query e così via. È possibile utilizzare hello Sys.dm tran_locks tooget informazioni sull'attività di blocco corrente hello in Database SQL di Azure. Per un codice di esempio, vedere [sys.dm_tran_locks (Transact-SQL)](https://msdn.microsoft.com/library/ms190345.aspx) nella 	documentazione online di Microsoft SQL Server.

### <a name="monitoring-query-plans"></a>Monitoraggio dei piani di query
Un piano di query inefficiente può anche aumentare il consumo della CPU. esempio Hello utilizza hello [Sys.dm exec_query_stats](https://msdn.microsoft.com/library/ms189741.aspx) consente di visualizzare la query utilizza CPU cumulativa maggiore hello toodetermine.

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

## <a name="see-also"></a>Vedere anche
[Introduzione tooSQL Database](sql-database-technical-overview.md)

