---
title: prestazioni del database nel Database di SQL Azure aaaMonitoring | Documenti Microsoft
description: Informazioni sulle opzioni di hello per il monitoraggio del database con gli strumenti di Azure e viste a gestione dinamica.
keywords: monitoraggio database, prestazioni database cloud
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: a2e47475-c955-4a8d-a65c-cbef9a6d9b9f
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 01/10/2017
ms.author: carlrab
ms.openlocfilehash: b13771183d4ccf37f58e2fc518b9b14de38212dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-database-performance-in-azure-sql-database"></a>Monitoraggio delle prestazioni del database nel database SQL di Azure
Monitoraggio delle prestazioni di hello di un database SQL di Azure inizia con hello risorse utilizzo toohello relativo livello di prestazioni del database che si sceglie di monitoraggio. Il monitoraggio consente di determinare se il database dispone di capacità in eccesso o non riesce perché le risorse sono raggiunge il limite massimo e quindi decidere se è a livello di prestazioni di tempo tooadjust hello e [livello di servizio](sql-database-service-tiers.md) del database. È possibile monitorare il database utilizzando gli strumenti di grafici in hello [portale di Azure](https://portal.azure.com) o mediante SQL [viste a gestione dinamica](https://msdn.microsoft.com/library/ms188754.aspx).

## <a name="monitor-databases-using-hello-azure-portal"></a>Monitorare i database che utilizzano hello portale di Azure
In hello [portale di Azure](https://portal.azure.com/), è possibile monitorare l'utilizzo di un singolo database selezionandolo e facendo clic su hello **monitoraggio** grafico. Verrà visualizzata una **metrica** finestra che è possibile modificare, fare clic su hello **Modifica grafico** pulsante. Aggiungere hello seguenti metriche:

* Percentuale CPU
* Percentuale di DTU
* Percentuale di I/O di dati
* Percentuale di dimensioni del database

Dopo aver aggiunto queste metriche, è possibile continuare tooview nel hello **monitoraggio** grafico con ulteriori informazioni su hello **metrica** finestra. Tutte e quattro le metriche mostrano toohello relativa percentuale di utilizzo medio hello **DTU** del database. Vedere hello [livelli di servizio](sql-database-service-tiers.md) articolo per informazioni dettagliate su Dtu.

![Monitoraggio del livello di servizio delle prestazioni del database.](./media/sql-database-service-tiers/sqldb_service_tier_monitoring.png)

È anche possibile configurare avvisi sulle metriche delle prestazioni hello. Fare clic su hello **Aggiungi avviso** pulsante hello **metrica** finestra. Seguire hello guidata tooconfigure l'avviso. È possibile hello opzione tooalert se le metriche hello superano una determinata soglia o hello scende di sotto di una determinata soglia.

Ad esempio, se si prevede che il carico di lavoro hello in toogrow del database, è possibile scegliere tooconfigure di avvisi di posta elettronica ogni volta che il database raggiunge l'80% per una qualsiasi delle metriche delle prestazioni hello. È possibile utilizzare questo come un toofigure avviso anticipato out quando potrebbe essere tooswitch toohello livello di prestazioni superiore.

le metriche delle prestazioni di Hello consentono inoltre di stabilire se è in grado di toodowngrade tooa livello di prestazioni inferiore. Si supponga che si utilizza un database Standard S2 e mostrano le metriche delle prestazioni tutti che hello medio database non utilizza più di 10% in qualsiasi momento. È probabile che il database hello funzioni correttamente in S1 Standard. Tuttavia, essere consapevoli dei carichi di lavoro o in cui picchi fluttuare prima di apportare hello decisione toomove tooa livello di prestazioni inferiore.

## <a name="monitor-databases-using-dmvs"></a>Monitorare i database con le viste a gestione dinamica
Hello stesse metriche esposte nel portale di hello sono disponibili anche tramite viste di sistema: [resource_stats](https://msdn.microsoft.com/library/dn269979.aspx) in hello logico **master** database del server, e [sys.dm_db_ statistiche sulle risorse](https://msdn.microsoft.com/library/dn800981.aspx) nel database utente hello. Utilizzare **resource_stats** se è necessario toomonitor meno dati granulari in un periodo di tempo più lungo. Utilizzare **Sys.dm db_resource_stats** se è necessario toomonitor dati più granulari in un intervallo di tempo minore. Per ulteriori informazioni, vedere la [Guida alle prestazioni del database SQL di Azure](sql-database-single-database-monitor.md#monitor-resource-use).

> [!NOTE]
> **sys.dm_db_resource_stats** restituisce un set di risultati vuoto quando viene usato nei database Web e Business Edition, che sono stati ritirati.
>
>

### <a name="monitor-resource-use"></a>Monitorare l'uso delle risorse

È possibile monitorare l'utilizzo di risorse usando [Informazioni dettagliate prestazioni query del Database SQL](sql-database-query-performance.md) e [Archivio query](https://msdn.microsoft.com/library/dn817826.aspx).

È inoltre possibile monitorare l'utilizzo tramite queste due viste:

* [sys.dm_db_resource_stats](https://msdn.microsoft.com/library/dn800981.aspx)
* [sys.resource_stats](https://msdn.microsoft.com/library/dn269979.aspx)

#### <a name="sysdmdbresourcestats"></a>sys.dm_db_resource_stats
È possibile utilizzare hello [Sys.dm db_resource_stats](https://msdn.microsoft.com/library/dn800981.aspx) vista in ogni database SQL. Hello **Sys.dm db_resource_stats** visualizzazione Mostra recente livello di servizio relativo toohello risorse utilizzare dati. Informazioni relative a percentuali medie della CPU, dati I/O, scritture nei log e memoria vengono registrate ogni 15 secondi e vengono mantenute per un'ora.

Poiché questa vista fornisce una visione più granulare sull'uso delle risorse, usare prima **sys.dm_db_resource_stats** per eventuali analisi o risoluzioni di problemi allo stato corrente. Ad esempio, questa query Mostra Media hello e risorse massima utilizzo per il database corrente hello su hello ora precedente:

    SELECT  
        AVG(avg_cpu_percent) AS 'Average CPU use in percent',
        MAX(avg_cpu_percent) AS 'Maximum CPU use in percent',
        AVG(avg_data_io_percent) AS 'Average data I/O in percent',
        MAX(avg_data_io_percent) AS 'Maximum data I/O in percent',
        AVG(avg_log_write_percent) AS 'Average log write use in percent',
        MAX(avg_log_write_percent) AS 'Maximum log write use in percent',
        AVG(avg_memory_usage_percent) AS 'Average memory use in percent',
        MAX(avg_memory_usage_percent) AS 'Maximum memory use in percent'
    FROM sys.dm_db_resource_stats;  

Per altre query, vedere gli esempi di hello in [Sys.dm db_resource_stats](https://msdn.microsoft.com/library/dn800981.aspx).

#### <a name="sysresourcestats"></a>sys.resource_stats
Hello [resource_stats](https://msdn.microsoft.com/library/dn269979.aspx) visualizzazione hello **master** database dispone di informazioni che consentono di monitorare le prestazioni di hello del database SQL a livello di prestazioni e il servizio specifico . dati Hello vengono raccolti ogni 5 minuti e viene mantenuti per circa 35 giorni. Questa vista è utile per analisi cronologiche a lungo termine dell'uso delle risorse del database SQL.

Hello seguente grafico mostra utilizzo delle risorse della CPU hello per un database Premium con livello di prestazioni P2 hello per ogni ora in una settimana. Questo grafico inizia di lunedì, viene 5 giorni lavorativi e un fine settimana, quando si verifica molto meno in un'applicazione hello.

![Uso delle risorse del database SQL](./media/sql-database-performance-guidance/sql_db_resource_utilization.png)

Dai dati hello, questo database dispone attualmente di un carico massimo della CPU di poco il 50% della CPU utilizzare il livello di prestazioni relativa toohello P2 (a mezzogiorno di martedì). Se fattore più importante di hello nel profilo dell'applicazione hello delle risorse della CPU, è possibile decidere che P2 è hello destra adatta tooguarantee di livello delle prestazioni che hello sempre il carico di lavoro. Se si prevede un toogrow applicazione nel tempo, è toohave una buona idea un buffer di risorse aggiuntive in modo che un'applicazione hello non raggiunge mai il limite di livello di prestazioni hello. Se si aumenta il livello di prestazioni hello, è possibile evitare errori visibili clienti che potrebbero verificarsi quando un database non è sufficiente richieste tooprocess power in modo efficace, soprattutto in ambienti sensibili alla latenza. Un esempio è un database che supporta un'applicazione quale vengono disegnate pagine Web in base ai risultati di hello delle chiamate di database.

Altri tipi di applicazioni può essere interpretato hello stesso grafico in modo diverso. Ad esempio, se un'applicazione tenta di tooprocess dati del libro paga ogni giorno e ha hello stesso grafico, questo tipo di modello "processo batch" potrebbe essere eseguito correttamente con un livello di prestazioni P1. livello di prestazioni P1 Hello è 100 mentre quello too200 Dtu a livello di prestazioni P2 hello. livello di prestazioni P1 Hello fornisce prestazioni hello metà del livello di prestazioni P2 hello. Il 50% dell'uso della CPU nel livello P2 equivale quindi al 100% dell'uso della CPU in P1. Se i timeout non dispone di un'applicazione hello, non è rilevante se un processo richieda 2 o 2,5 ore toofinish, se però eseguito in giornata. Per un'applicazione che rientra in questa categoria è probabilmente sufficiente usare il livello di prestazioni P1. È possibile sfruttare il fatto di hello che vi sono periodi di tempo durante il giorno hello quando utilizzo delle risorse è inferiore, in modo che qualsiasi picco"grande" potrebbe trasformarsi in un unico di gestirle hello giornata hello. Hello a livello di prestazioni P1 potrebbe essere valido per questo tipo di applicazione e risparmiare denaro, purché i processi di hello possono terminare in orario ogni giorno.

Espone i Database di SQL Azure utilizzato informazioni sulle risorse per ogni database attivo nella hello **resource_stats** visualizzazione di hello **master** database in ogni server. dati Hello nella tabella hello vengono aggregati per intervalli di 5 minuti. Hello Basic, Standard e Premium livelli di servizio hello dati può richiedere più di 5 minuti tooappear nella tabella di hello, pertanto questi dati sono più utili per l'analisi cronologica anziché di analisi in tempo quasi reale. Hello query **resource_stats** vista toosee hello cronologia recente di un database e toovalidate prenotazione hello scelta recapitati prestazioni hello desiderato quando necessario.

> [!NOTE]
> È necessario essere connesso toohello **master** database la logica tooquery di server di database SQL **resource_stats** in hello seguono esempi.
> 
> 

Questo esempio viene illustrato come sono esposto dati hello in questa vista:

    SELECT TOP 10 *
    FROM sys.resource_stats
    WHERE database_name = 'resource1'
    ORDER BY start_time DESC

![vista del catalogo sys. resource_stats Hello](./media/sql-database-performance-guidance/sys_resource_stats.png)

Hello esempio successivo illustra diversi modi, che è possibile utilizzare hello **resource_stats** catalogo tooget informazioni sull'utilizzo delle risorse del database SQL:

1. toolook in hello oltre risorse della settimana utilizzare per hello userdb1 di database, è possibile eseguire questa query:
   
        SELECT *
        FROM sys.resource_stats
        WHERE database_name = 'userdb1' AND
              start_time > DATEADD(day, -7, GETDATE())
        ORDER BY start_time DESC;
2. tooevaluate come anche se il carico di lavoro si adatta a livello di prestazioni hello, occorre toodrill verso il basso in ogni aspetto hello la metrica delle risorse: CPU, letture, scritture, il numero di lavori e numero di sessioni. Ecco una rivista eseguire una query utilizzando **resource_stats** tooreport hello valori medi e massimi di queste metriche delle risorse:
   
        SELECT
            avg(avg_cpu_percent) AS 'Average CPU use in percent',
            max(avg_cpu_percent) AS 'Maximum CPU use in percent',
            avg(avg_data_io_percent) AS 'Average physical data I/O use in percent',
            max(avg_data_io_percent) AS 'Maximum physical data I/O use in percent',
            avg(avg_log_write_percent) AS 'Average log write use in percent',
            max(avg_log_write_percent) AS 'Maximum log write use in percent',
            avg(max_session_percent) AS 'Average % of sessions',
            max(max_session_percent) AS 'Maximum % of sessions',
            avg(max_worker_percent) AS 'Average % of workers',
            max(max_worker_percent) AS 'Maximum % of workers'
        FROM sys.resource_stats
        WHERE database_name = 'userdb1' AND start_time > DATEADD(day, -7, GETDATE());
3. Con queste informazioni sui valori medi e massimi di hello di ogni metrica della risorsa, è possibile valutare l'idoneità di rapporto al carico di lavoro nel livello di prestazioni hello che scelto. In genere, i valori medi di **resource_stats** consentono toouse una buona base di riferimento con dimensioni di destinazione hello. Deve trattarsi dello strumento di misurazione principale. Per un esempio, è possibile utilizzare il livello di servizio Standard hello con livello di prestazioni S2. Media Hello utilizzare le percentuali per le letture dei / o e CPU, operazioni di scrittura sono sotto il 40%, numero medio di hello dei thread di lavoro è minore di 50 e numero medio di hello delle sessioni è inferiore a 200. Il carico di lavoro può rientrare nel livello di prestazioni S1 hello. È facile toosee se il database rientra in lavoro hello e limiti di sessione. toosee se un database può rientrare nel livello di prestazioni inferiore con l'attributo tooCPU, letture e scritture, dividere il numero di DTU hello del livello di prestazioni inferiore hello per hello numero di DTU del livello di prestazioni corrente e moltiplicare il risultato di hello 100:
   
    **S1 DTU / S2 DTU * 100 = 20 / 50 * 100 = 40**
   
    il risultato di Hello è la differenza di prestazioni relativa hello tra hello due livelli di prestazioni in percentuale. Se l'utilizzo delle risorse non supera tale quantità, il carico di lavoro può rientrare nel livello di prestazioni inferiore hello. Tuttavia, è necessario toolook tutti gli intervalli di valori di utilizzo delle risorse e determinare, in percentuale, la frequenza con cui il carico di lavoro del database può rientrare nel livello di prestazioni inferiore hello. Hello nella query seguente restituisce hello adatta percentuale per ogni dimensione di risorsa, in base alla soglia di hello del 40% calcolata in questo esempio:
   
        SELECT
            (COUNT(database_name) - SUM(CASE WHEN avg_cpu_percent >= 40 THEN 1 ELSE 0 END) * 1.0) / COUNT(database_name) AS 'CPU Fit Percent'
            ,(COUNT(database_name) - SUM(CASE WHEN avg_log_write_percent >= 40 THEN 1 ELSE 0 END) * 1.0) / COUNT(database_name) AS 'Log Write Fit Percent'
            ,(COUNT(database_name) - SUM(CASE WHEN avg_data_io_percent >= 40 THEN 1 ELSE 0 END) * 1.0) / COUNT(database_name) AS 'Physical Data IO Fit Percent'
        FROM sys.resource_stats
        WHERE database_name = 'userdb1' AND start_time > DATEADD(day, -7, GETDATE());
   
    In base all'obiettivo del livello servizio del database (SLO), è possibile decidere se il carico di lavoro rientra nel livello di prestazioni inferiore hello. Se il carico di lavoro database SLO è pari al 99,9% e hello query precedente restituisce i valori maggiori di 99,9% per tutti i tre dimensioni della risorsa, il carico di lavoro che si adatta nel livello di prestazioni inferiore hello.
   
    Esaminando hello adatta percentuale offre inoltre comprendere se è necessario spostare livello toomeet prestazioni Avanti superiore toohello il SLO. Ad esempio, userdb1 hello dopo l'utilizzo della CPU per hello settimana precedente:
   
   | Percentuale CPU media | Percentuale CPU massima |
   | --- | --- |
   | 24,5 |100,00 |
   
    Hello utilizzo medio della CPU è circa un quarto del limite di hello del livello di prestazioni hello, che potrebbe rientrare perfettamente in hello livello delle prestazioni hello database. Tuttavia, valore massimo hello mostra che il database hello raggiunge il limite di hello del livello di prestazioni hello. È necessario toomove toohello livello di prestazioni superiore? Osservare come più volte i carico di lavoro raggiunge il 100% e confrontare il carico di lavoro database tooyour SLO.
   
        SELECT
        (COUNT(database_name) - SUM(CASE WHEN avg_cpu_percent >= 100 THEN 1 ELSE 0 END) * 1.0) / COUNT(database_name) AS 'CPU fit percent'
        ,(COUNT(database_name) - SUM(CASE WHEN avg_log_write_percent >= 100 THEN 1 ELSE 0 END) * 1.0) / COUNT(database_name) AS 'Log write fit percent'
        ,(COUNT(database_name) - SUM(CASE WHEN avg_data_io_percent >= 100 THEN 1 ELSE 0 END) * 1.0) / COUNT(database_name) AS 'Physical data I/O fit percent'
        FROM sys.resource_stats
        WHERE database_name = 'userdb1' AND start_time > DATEADD(day, -7, GETDATE());
   
    Se questa query restituisce un valore inferiore a 99,9% per le dimensioni di hello tre risorse, uno spostamento toohello successivo livello di prestazioni superiore oppure usare l'ottimizzazione di applicazioni tecniche tooreduce hello carico nel database SQL di hello.
4. In questo esercizio viene inoltre presa in considerazione l'aumento del carico di lavoro previsto di hello future.

Per il pool elastico, è possibile monitorare i singoli database nel pool di hello con le tecniche di hello descritti in questa sezione. Ma è anche possibile monitorare il pool di hello nel suo complesso. Per informazioni, vedere [Monitorare e gestire un elastico](sql-database-elastic-pool-manage-portal.md).


### <a name="maximum-concurrent-requests"></a>Numero massimo di richieste simultanee
numero di hello toosee di richieste simultanee, eseguire la query Transact-SQL nel database SQL di:

    SELECT COUNT(*) AS [Concurrent_Requests]
    FROM sys.dm_exec_requests R

carico di lavoro hello tooanalyze di un database di SQL Server locale, modificare toofilter questa query sul database specifico hello desiderato tooanalyze. Ad esempio, se si dispone di un database locale denominato MyDatabase, questa query Transact-SQL restituisce il conteggio di hello di richieste simultanee in tale database:

    SELECT COUNT(*) AS [Concurrent_Requests]
    FROM sys.dm_exec_requests R
    INNER JOIN sys.databases D ON D.database_id = R.database_id
    AND D.name = 'MyDatabase'

Questo è solo uno snapshot in un singolo punto nel tempo. tooget una migliore comprensione del carico di lavoro e requisiti di richieste simultanee, è necessario toocollect numero di campioni nel tempo.

### <a name="maximum-concurrent-logins"></a>Numero massimo di accessi simultanei
È possibile analizzare il tooget modelli un'idea della frequenza di hello degli account di accesso utente e dell'applicazione. È anche possibile eseguire caricamenti realistici in un ambiente test per toomake assicurarsi che non si riscontrano questo o altri limiti che vengono discussi in questo articolo. Non è disponibile alcuna vista di query singola o vista a gestione dinamica per la visualizzazione dei numeri o della cronologia degli accessi simultanei.

Se più client utilizzano hello stessa stringa di connessione, hello autentica il servizio ogni account di accesso. Se 10 utenti di connettersi contemporaneamente database tooa tramite hello stesso nome utente e password, non vi sarà 10 accessi simultanei. Questo limite si applica solo toohello durata dell'accesso hello e l'autenticazione. Se gli utenti di hello 10 stesso database toohello si connettono in sequenza, il numero di hello di accessi simultanei mai sarebbe maggiore di 1.

> [!NOTE]
> Attualmente, questo limite non si applica toodatabases nel pool elastico.
> 
> 

### <a name="maximum-sessions"></a>Numero massimo di sessioni
numero di hello toosee di sessioni attive correnti, eseguire la query Transact-SQL nel database SQL di:

    SELECT COUNT(*) AS [Sessions]
    FROM sys.dm_exec_connections

Se si sta analizzando un carico di lavoro di SQL Server locale, è possibile modificare hello toofocus di query su un database specifico. Questa query consente di determinare le esigenze di sessione possibili per il database di hello se si intende lo spostamento tooAzure Database SQL.

    SELECT COUNT(*)  AS [Sessions]
    FROM sys.dm_exec_connections C
    INNER JOIN sys.dm_exec_sessions S ON (S.session_id = C.session_id)
    INNER JOIN sys.databases D ON (D.database_id = S.database_id)
    WHERE D.name = 'MyDatabase'

Queste query restituiscono un conteggio temporizzato. Se si raccolgono più campioni nel tempo, è necessario migliore conoscenza di hello della sessione di utilizzare.

Per l'analisi di Database SQL, è possibile ottenere statistiche cronologiche sulle sessioni eseguendo una query hello [resource_stats](https://msdn.microsoft.com/library/dn269979.aspx) visualizzazione e la revisione hello **active_session_count** colonna. 
