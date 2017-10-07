---
title: Database SQL di Azure di migrazione di differenze T-SQL aaaResolving | Documenti Microsoft
description: Istruzioni Transact-SQL non completamente supportate nel Database SQL di Azure
services: sql-database
documentationcenter: 
author: BYHAM
manager: jhubbard
editor: 
tags: 
ms.assetid: c05abd9e-28a7-4c97-9bdf-bc60d08fc92e
ms.service: sql-database
ms.custom: load & move data
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 03/17/2017
ms.author: rickbyh
ms.openlocfilehash: 3852013338bfdc6c7da9d1d879c54781682bc635
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="resolving-transact-sql-differences-during-migration-toosql-database"></a>Risoluzione di differenze di Transact-SQL durante la migrazione tooSQL Database   
Quando [la migrazione del database](sql-database-cloud-migrate.md) da tooAzure di SQL Server SQL Server, si potrebbe scoprire che il database richiede alcuni riprogettazione prima hello possibile eseguire la migrazione di SQL Server. In questo argomento fornisce indicazioni tooassist in esecuzione la riprogettazione sia comprensione hello sottostante motivi per cui hello riprogettazione è necessaria. incompatibilità toodetect, utilizzare hello [dati Migration Assistant (DMA)](https://www.microsoft.com/download/details.aspx?id=53595).

## <a name="overview"></a>Panoramica
La maggior parte delle funzionalità Transact-SQL usate dalle applicazioni è supportata in Microsoft SQL Server e nel database SQL di Azure. Ad esempio, hello componenti SQL di base, ad esempio tipi di dati, operatori, stringa, aritmetici, logici e funzioni per i cursori, funzionano in modo identico in SQL Server e Database SQL. T-SQL presenta, tuttavia, alcune differenze negli elementi DDL (data definition language) e DML (data manipulation language), di conseguenza alcune istruzioni e query T-SQL sono supportate solo in parte (questo verrà descritto più avanti in questo argomento).

Inoltre, alcune funzionalità e sintassi non supportata affatto perché il Database di SQL Azure è progettato tooisolate funzionalità dalle dipendenze nel database master hello e hello del sistema operativo. Di conseguenza, la maggior parte delle attività a livello di server non è appropriata al database SQL. Le istruzioni T-SQL non sono disponibili se configurano opzioni a livello di server e componenti del sistema operativo o se specificano una configurazione del file system. Quando sono necessarie tali funzionalità, spesso è disponibile un'alternativa appropriata dal database SQL o da un'altra funzionalità o un altro servizio di Azure. 

Ad esempio, la disponibilità elevata è incorporata in Azure, pertanto la configurazione di Always On non è necessaria (anche se è tooconfigure la replica geografica attiva per il ripristino più veloce nell'evento hello un'emergenza). In tal caso, le istruzioni T-SQL relative tooavailability gruppi non sono supportati dal Database SQL tooAlways correlati viste DMV di hello in anche non sono supportate.

Per un elenco delle funzionalità di hello che sono supportati e non supportati dal Database SQL, vedere [confronto delle funzionalità di Database SQL di Azure](sql-database-features.md). elenco di Hello in questa pagina integra tale argomento linee guida e le funzionalità e si concentra sulle istruzioni Transact-SQL.

## <a name="transact-sql-syntax-statements-with-partial-differences"></a>Istruzioni di sintassi Transact-SQL con differenze parziali
sono disponibili istruzioni DDL (data definition language) di Hello core, ma alcune istruzioni DDL sono funzionalità non supportate e posizionamento toodisk relative estensioni. 

- Le istruzioni CREATE e ALTER DATABASE offrono numerose opzioni. le istruzioni di Hello includono il posizionamento dei file FILESTREAM e opzioni di service broker che si applicano solo tooSQL Server. Questo potrebbe non è rilevante se si creano database prima di eseguire la migrazione, ma se si esegue la migrazione di codice T-SQL che crea i database è necessario confrontare [CREATE DATABASE (Database SQL di Azure)](https://msdn.microsoft.com/library/dn268335.aspx) con la sintassi di SQL Server hello in [crea DATABASE (SQL Server Transact-SQL)](https://msdn.microsoft.com/library/ms176061.aspx) toomake che sono supportate tutte le opzioni di hello è utilizzare. CREATE DATABASE per Database SQL di Azure dispone anche di obiettivo di servizio e le opzioni di scalabilità elastica che si applicano solo tooSQL Database.
- le istruzioni CREATE e ALTER TABLE di Hello sono disponibili opzioni di tabella FileTable che non possono essere utilizzate nel Database SQL poiché FILESTREAM non è supportato.
- Le istruzioni CREATE e ALTER login sono supportate, ma il Database SQL non offre tutte le opzioni di hello. toomake che portabilità, il database SQL Database incoraggia usando utenti del database anziché gli account di accesso ogni volta che è possibile indipendente. Per altre informazioni, vedere [CREATE/ALTER LOGIN](https://msdn.microsoft.com/library/ms189828.aspx) e [Controllo e concessione dell'accesso al database](https://docs.microsoft.com/azure/sql-database/sql-database-manage-logins).

## <a name="transact-sql-syntax-not-supported-in-sql-database"></a>Sintassi di Transact-SQL non supportata nel database SQL   
Inoltre tooTransact SQL istruzioni correlate toohello non supportate funzionalità descritte in [confronto delle funzionalità di Database SQL di Azure](sql-database-features.md), hello i gruppi di istruzioni e le istruzioni seguenti, che non sono supportati. Di conseguenza, se la migrazione del database toobe utilizza hello seguenti funzionalità, riprogettare il tooeliminate T-SQL queste funzionalità di T-SQL e istruzioni.

- Regole di confronto di oggetti di sistema
- Connessione correlata: istruzioni di Endpoint, `ORIGINAL_DB_NAME`. Database SQL non supporta l'autenticazione di Windows, ma supporta l'autenticazione di Azure Active Directory simile hello. Alcuni tipi di autenticazione richiedono hello l'ultima versione di SQL Server Management Studio. Per ulteriori informazioni, vedere [tooSQL connessione Database o Data Warehouse da usando Azure Active Directory l'autenticazione di SQL](sql-database-aad-authentication.md).
- Query tra database mediante nomi composti da tre o quattro parti. Le query tra database di sola lettura sono supportate mediante [query di database elastici](sql-database-elastic-query-overview.md).
- Concatenamento della proprietà tra database, impostazione `TRUSTWORTHY`
- `DATABASEPROPERTY` Usare invece `DATABASEPROPERTYEX`.
- `EXECUTE AS LOGIN` Usare invece 'EXECUTE AS USER'.
- La crittografia è supportata, ad eccezione della gestione delle chiavi estendibile
- Gestione degli eventi: notifiche degli eventi, notifiche di query
- Posizionamento dei file: sintassi relativa toodatabase il posizionamento dei file, dimensioni e i file di database gestiti automaticamente da Microsoft Azure.
- Disponibilità elevata: sintassi relativa disponibilità toohigh, che viene gestita tramite l'account di Microsoft Azure. Questa include la sintassi per backup, ripristino, AlwaysOn, mirroring del database, log shipping e modalità di ripristino.
- Lettore di log: la sintassi che si basa su hello agente di lettura log, che non è disponibile nel Database SQL: replica Push, Change Data Capture. Il database SQL può essere iscritto a un articolo di replica push.
- Funzioni: `fn_get_sql`, `fn_virtualfilestats`, `fn_virtualservernodes`
- Tabelle temporanee globali
- Hardware: Impostazioni di server correlati toohardware relative alla sintassi: ad esempio memoria, thread di lavoro, affinità di CPU, flag di traccia. In alternativa usare i livelli di servizio.
- `HAS_DBACCESS`
- `KILL STATS JOB`
- `OPENQUERY`, `OPENROWSET`, `OPENDATASOURCE` e nomi in quattro parti
- .NET framework: integrazione CLR con SQL Server
- Ricerca semantica
- Credenziali del server: usare le [credenziali con ambito database](https://msdn.microsoft.com/library/mt270260.aspx).
- Elementi a livello di server: ruoli del server, `IS_SRVROLEMEMBER`, `sys.login_token`. `GRANT`, `REVOKE` e `DENY` delle autorizzazioni a livello di server non sono disponibili anche se alcune vengono sostituite da autorizzazioni a livello di database. Alcune viste a gestione dinamica a livello di server dispongono di una vista a gestione dinamica equivalente a livello di database.
- `SET REMOTE_PROC_TRANSACTIONS`
- `SHUTDOWN`
- `sp_addmessage`
- Opzioni `sp_configure` e `RECONFIGURE`. Con [ALTER DATABASE SCOPED CONFIGURATION](https://msdn.microsoft.com/library/mt629158.aspx)sono disponibili alcune opzioni.
- `sp_helpuser`
- `sp_migrate_user_to_contained`
- SQL Server Agent: Sintassi che si basa su database MSDB di SQL Server Agent o hello hello: avvisi, operatori, server di gestione centrale. Usare invece gli script, ad esempio Azure PowerShell.
- SQL Server audit: usare il controllo del database SQL.
- Traccia SQL Server
- Flag di traccia: alcuni flag di traccia elementi siano stati spostati toocompatibility modalità.
- Debug di Transact-SQL
- Trigger: Con ambito Server o trigger di accesso
- `USE`istruzione: toochange hello database tooa diversi database di contesto, è necessario apportare un nuovo database nuovo toohello di connessione.

## <a name="full-transact-sql-reference"></a>Riferimento completo di Transact-SQL
Per ulteriori informazioni sulla grammatica Transact-SQL, uso ed esempi, vedere [riferimento a Transact-SQL (motore di Database)](https://msdn.microsoft.com/library/bb510741.aspx) nella documentazione Online di SQL Server. 

### <a name="about-hello-applies-to-tags"></a>Informazioni sui tag "Si applica a" hello
riferimento a Transact-SQL Hello include argomenti correlati tooSQL Server versioni 2008 toohello presenta. Sotto il titolo di argomento hello è una barra degli strumenti, piattaforme di elenco hello quattro SQL Server e che indica l'applicabilità. Ad esempio, i gruppi di disponibilità sono stati introdotti in SQL Server 2012. Il [CREATE AVAILABILTY GROUP](https://msdn.microsoft.com/library/ff878399.aspx) argomento indica che l'istruzione hello si applica a **SQL Server (a partire da 2012)**. non si applica l'istruzione Hello tooSQL Server 2008, SQL Server 2008 R2, Database SQL di Azure, Azure SQL Data Warehouse o Parallel Data Warehouse.

In alcuni casi, hello di tema generale di un argomento può essere usato in un prodotto, ma esistono differenze minime tra prodotti. differenze di Hello sono indicate in punti medi, hello vedere l'argomento appropriato. In alcuni casi, hello di tema generale di un argomento può essere usato in un prodotto, ma esistono differenze minime tra prodotti. differenze di Hello sono indicate in punti medi, hello vedere l'argomento appropriato. Ad esempio l'argomento CREATE TRIGGER hello è disponibile nel Database SQL. Ma hello **tutti i SERVER** opzione per i trigger a livello di server, indica che i trigger a livello di server possono essere utilizzati nel Database SQL. Usare i trigger a livello di database.

## <a name="next-steps"></a>Passaggi successivi

Per un elenco delle funzionalità di hello che sono supportati e non supportati dal Database SQL, vedere [confronto delle funzionalità di Database SQL di Azure](sql-database-features.md). elenco di Hello in questa pagina integra tale argomento linee guida e le funzionalità e si concentra sulle istruzioni Transact-SQL.

