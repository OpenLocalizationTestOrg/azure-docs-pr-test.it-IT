---
title: Panoramica delle caratteristiche del Database SQL aaaAzure | Documenti Microsoft
description: "Questa pagina viene fornita una panoramica di database e server logici di Database SQL di Azure hello e include una matrice di supporto di funzionalità con collegamenti di ogni funzionalità elencate."
services: sql-database
documentationcenter: na
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: d1a46fa4-53d2-4d25-a0a7-92e8f9d70828
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 08/25/2017
ms.author: carlrab
ms.openlocfilehash: 463c88edcd38eabbc768cfb701bc74461836aa36
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sql-database-features"></a>Funzionalità di database SQL di Azure

Condivide una codebase comune con SQL Server di Database SQL di Azure e, a livello di database hello, supporta la maggior parte di hello stesse funzionalità. Hello principali differenze tra i Database di SQL Azure e SQL Server sono a livello di istanza hello. 

Continuiamo tooadd funzionalità tooAzure Database SQL. In modo che incoraggia la collaborazione è toovisit il nostro servizio Aggiorna pagina Web per Azure e toouse i relativi filtri:

* Filtrato toohello [servizio Database SQL](https://azure.microsoft.com/updates/?service=sql-database).
* Filtrati tooGeneral disponibilità [annunci (GA)](http://azure.microsoft.com/updates/?service=sql-database&update-type=general-availability) per le funzionalità di Database SQL.

## <a name="sql-server-and-sql-database-feature-support"></a>Supporto delle funzionalità di SQL Server e del database SQL

Hello nella tabella seguente sono elencate le funzionalità principali di hello di SQL Server e vengono fornite informazioni sul supporto di ogni particolare funzionalità e un collegamento toomore informazioni hello caratteristiche. Per le differenze di Transact-SQL tooconsider durante la migrazione di una soluzione di database esistente, vedere [differenze risoluzione Transact-SQL durante la migrazione tooSQL Database](sql-database-transact-sql-information.md).


| **Funzionalità SQL Server** | **Supportata nel database SQL di Azure** | 
| --- | --- |  
| [Always Encrypted](https://docs.microsoft.com/sql/relational-databases/security/encryption/always-encrypted-database-engine) | Sì. Vedere [Archivio certificati](sql-database-always-encrypted.md) e [Insieme di credenziali delle chiavi](sql-database-always-encrypted-azure-key-vault.md)|
| [Gruppi di disponibilità AlwaysOn](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/always-on-availability-groups-sql-server) | No. Vedere [Gruppi di failover e replica geografica attiva](sql-database-geo-replication-overview.md) |
| [Collegamento di un database](https://docs.microsoft.com/sql/relational-databases/databases/attach-a-database) | No |
| [Ruoli applicazione](https://docs.microsoft.com/sql/relational-databases/security/authentication-access/application-roles) | Sì |
| [File BACPAC (esportazione)](https://docs.microsoft.com/sql/relational-databases/data-tier-applications/export-a-data-tier-application) | Sì. Vedere [Esportazione di un database SQL](sql-database-export.md) |
| [File BACPAC (importazione)](https://docs.microsoft.com/sql/relational-databases/data-tier-applications/import-a-bacpac-file-to-create-a-new-user-database) | Sì. Vedere [Importazione di un database SQL](sql-database-import.md) |
| [Comando BACKUP](https://docs.microsoft.com/sql/t-sql/statements/backup-transact-sql) | No. Vedere [Backup automatizzati](sql-database-automated-backups.md) |
| [Funzioni predefinite](https://docs.microsoft.com/sql/t-sql/functions/functions) | Supportate per la maggior parte. Vedere le singole funzioni |
| [Change Data Capture](https://docs.microsoft.com/sql/relational-databases/track-changes/about-change-data-capture-sql-server) | No |
| [Rilevamento modifiche](https://docs.microsoft.com/sql/relational-databases/track-changes/about-change-tracking-sql-server) | Sì |
| [Istruzioni sulle regole di confronto](https://docs.microsoft.com/sql/t-sql/statements/collations) | Sì |
| [Indici columnstore](https://docs.microsoft.com/sql/relational-databases/indexes/columnstore-indexes-overview) | Sì. [Solo edizione Premium](https://docs.microsoft.com/sql/relational-databases/indexes/columnstore-indexes-overview) |
| [Common Language Runtime (CLR)](https://docs.microsoft.com/sql/relational-databases/clr-integration/common-language-runtime-clr-integration-programming-concepts) | No |
| [Database indipendenti](https://docs.microsoft.com/sql/relational-databases/databases/contained-databases) | Sì |
| [Utenti indipendenti](https://docs.microsoft.com/sql/relational-databases/security/contained-database-users-making-your-database-portable) | Sì |
| [Parole chiave degli elementi del linguaggio per il controllo di flusso](https://docs.microsoft.com/sql/t-sql/language-elements/control-of-flow) | Sì |
| [Query tra database](https://docs.microsoft.com/sql/relational-databases/in-memory-oltp/cross-database-queries) | Supportate parzialmente, vedere [Query elastiche](sql-database-elastic-query-overview.md) |
| [Cursori](https://docs.microsoft.com/sql/t-sql/language-elements/cursors-transact-sql) | Sì | 
| [Compressione dei dati](https://docs.microsoft.com/sql/relational-databases/data-compression/data-compression) | Sì |
| [Posta elettronica database](https://docs.microsoft.com/sql/relational-databases/database-mail/database-mail) | No |
| [Mirroring del database](https://docs.microsoft.com/sql/database-engine/database-mirroring/database-mirroring-sql-server) | No |
| [Impostazioni di configurazione del database](https://docs.microsoft.com/sql/t-sql/statements/alter-database-scoped-configuration-transact-sql) | Sì |
| [Data Quality Services (DQS)](https://docs.microsoft.com/sql/data-quality-services/data-quality-services) | No |
| [Snapshot del database](https://docs.microsoft.com/sql/relational-databases/databases/database-snapshots-sql-server) | No |
| [Tipi di dati](https://docs.microsoft.com/sql/t-sql/data-types/data-types-transact-sql) | Sì |  
| [Istruzioni DBCC](https://docs.microsoft.com/sql/t-sql/database-console-commands/dbcc-transact-sql) | Supportate per la maggior parte. Vedere le singole istruzioni |
| [Istruzioni DDL](https://docs.microsoft.com/sql/t-sql/statements/statements) | Supportate per la maggior parte. Vedere le singole istruzioni
| [Trigger DDL](https://docs.microsoft.com/sql/relational-databases/triggers/ddl-triggers) | Solo database |
| [Transazioni distribuite - MS DTC](https://docs.microsoft.com/sql/relational-databases/native-client-ole-db-transactions/supporting-distributed-transactions) | No. Vedere [Transazioni elastiche](sql-database-elastic-transactions-overview.md) |
| [Istruzioni DML](https://docs.microsoft.com/sql/t-sql/queries/queries) | Supportate per la maggior parte. Vedere le singole istruzioni |
| [Trigger DML](https://docs.microsoft.com/sql/relational-databases/triggers/dml-triggers) |
| [Viste a gestione dinamica](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/system-dynamic-management-views) | Supportate in alcuni casi. Vedere le singole DMV |
| [Notifiche degli eventi](https://docs.microsoft.com/sql/relational-databases/service-broker/event-notifications) | No. Vedere [Avvisi](sql-database-insights-alerts-portal.md) |
| [Espressioni](https://docs.microsoft.com/sql/t-sql/language-elements/expressions-transact-sql) |Sì |
| [Eventi estesi](https://docs.microsoft.com/sql/relational-databases/extended-events/extended-events) | Supportati in alcuni casi. Vedere i singoli eventi |
| [Stored procedure estese](https://docs.microsoft.com/sql/relational-databases/extended-stored-procedures-programming/creating-extended-stored-procedures) | No |
| [File e gruppi di file](https://docs.microsoft.com/sql/relational-databases/databases/database-files-and-filegroups) | Solo gruppi di file primari |
| [Filestream](https://docs.microsoft.com/sql/relational-databases/blob/filestream-sql-server) | No |
| [Ricerca full-text](https://docs.microsoft.com/sql/relational-databases/search/full-text-search) | I word breaker di terze parti non sono supportati |
| [Funzioni](https://docs.microsoft.com/sql/t-sql/functions/functions) | Supportate per la maggior parte. Vedere le singole funzioni |
| [Elaborazione del grafico](/sql/relational-databases/graphs/sql-graph-overview) | Sì |
| [Ottimizzazione in memoria](https://docs.microsoft.com/sql/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization) | Sì. [Solo edizione Premium](sql-database-in-memory.md) |
| [Supporto di dati JSON](https://docs.microsoft.com/sql/relational-databases/json/json-data-sql-server) | Sì |
| [Elementi del linguaggio](https://docs.microsoft.com/sql/t-sql/language-elements/language-elements-transact-sql) | Supportati per la maggior parte. Vedere i singoli elementi |  
| [Server collegati](https://docs.microsoft.com/sql/relational-databases/linked-servers/linked-servers-database-engine) | No. Vedere [Query elastica](sql-database-elastic-query-horizontal-partitioning.md) |
| [Log shipping](https://docs.microsoft.com/sql/database-engine/log-shipping/about-log-shipping-sql-server) | No. Vedere [Gruppi di failover e replica geografica attiva](sql-database-geo-replication-overview.md) |
| [Master Data Services (MDS)](https://docs.microsoft.com/sql/master-data-services/master-data-services-overview-mds) | No |
| [Registrazione minima nell'importazione bulk](https://docs.microsoft.com/sql/relational-databases/import-export/prerequisites-for-minimal-logging-in-bulk-import) | No |
| [Modifica dei dati di sistema](https://docs.microsoft.com/sql/relational-databases/databases/system-databases) | No |
| [Operazioni online sugli indici](https://docs.microsoft.com/sql/relational-databases/indexes/perform-index-operations-online) | Supportate. Dimensioni delle transazioni limitate dal livello di servizio |
| [Operatori](https://docs.microsoft.com/sql/t-sql/language-elements/operators-transact-sql) | Supportati per la maggior parte. Vedere i singoli operatori |
| [Ripristino temporizzato di un database](https://docs.microsoft.com/sql/relational-databases/backup-restore/restore-a-sql-server-database-to-a-point-in-time-full-recovery-model) | Sì. Vedere [Ripristino di un database SQL](sql-database-recovery-using-backups.md#point-in-time-restore) |
| [PolyBase](https://docs.microsoft.com/sql/relational-databases/polybase/polybase-guide) | No |
| [Gestione basata su criteri](https://docs.microsoft.com/sql/relational-databases/policy-based-management/administer-servers-by-using-policy-based-management) | No |
| [Predicati](https://docs.microsoft.com/sql/t-sql/queries/predicates) | Supportati per la maggior parte. Vedere i singoli predicati |
| [Servizi R](https://docs.microsoft.com/sql/advanced-analytics/r-services/sql-server-r-services) | No |
| [Resource Governor](https://docs.microsoft.com/sql/relational-databases/resource-governor/resource-governor) | No |
| [Istruzioni RESTORE](https://docs.microsoft.com/sql/t-sql/statements/restore-statements-for-restoring-recovering-and-managing-backups-transact-sql) | No | 
| [Ripristino del database da backup](https://docs.microsoft.com/sql/relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases#restore-data-backups) | Solo da backup predefiniti. Vedere [Ripristino di un database SQL](sql-database-recovery-using-backups.md) |
| [Sicurezza a livello di riga](https://docs.microsoft.com/sql/relational-databases/security/row-level-security) | Sì |
| [Ricerca semantica](https://docs.microsoft.com/sql/relational-databases/search/semantic-search-sql-server) | No |
| [Numeri di sequenza](https://docs.microsoft.com/sql/relational-databases/sequence-numbers/sequence-numbers) | Sì |
| [Service Broker](https://docs.microsoft.com/sql/database-engine/configure-windows/sql-server-service-broker) | No |
| [Impostazioni di configurazione del server](https://docs.microsoft.com/sql/database-engine/configure-windows/server-configuration-options-sql-server) | No |
| [Istruzioni SET](https://docs.microsoft.com/sql/t-sql/statements/set-statements-transact-sql) | Supportate per la maggior parte. Vedere le singole istruzioni 
| [Spatial](https://docs.microsoft.com/sql/relational-databases/spatial/spatial-data-sql-server) | Sì |
| [Agente SQL Server](https://docs.microsoft.com/sql/ssms/agent/sql-server-agent) | No. Vedere [Processi elastici](sql-database-elastic-jobs-getting-started.md) |
| [SQL Server Analysis Services (SSAS)](https://docs.microsoft.com/sql/analysis-services/analysis-services) | No. Vedere [Azure Analysis Services](https://azure.microsoft.com/services/analysis-services/) |
| [Controllo di SQL Server](https://docs.microsoft.com/sql/relational-databases/security/auditing/sql-server-audit-database-engine) | No. Vedere [Controllo del database SQL](sql-database-auditing.md) |
| [SQL Server Integration Services (SSIS)](https://docs.microsoft.com/sql/integration-services/sql-server-integration-services) | No. Vedere [Azure Data Factory](https://azure.microsoft.com/services/data-factory/) |
| [SQL Server PowerShell](https://docs.microsoft.com/sql/relational-databases/scripting/sql-server-powershell) | Sì |
| SQL Server Profiler | [Supportato](https://docs.microsoft.com/sql/tools/sql-server-profiler/sql-server-profiler) | No. Vedere [Eventi estesi](sql-database-xevent-db-diff-from-svr.md) |
| [Replica di SQL Server](https://docs.microsoft.com/sql/relational-databases/replication/sql-server-replication) | [Solo per iscritti alla replica transazionale e snapshot](sql-database-cloud-migrate.md) |
| [SQL Server Reporting Services (SSRS)](https://docs.microsoft.com/sql/reporting-services/create-deploy-and-manage-mobile-and-paginated-reports) | No |
| [Stored procedure](https://docs.microsoft.com/sql/relational-databases/stored-procedures/stored-procedures-database-engine) | Sì |
| [Funzioni archiviate nel sistema](https://docs.microsoft.com/sql/relational-databases/system-functions/system-functions-for-transact-sql) | Supportate in alcuni casi. Vedere le singole funzioni |
| [Stored procedure di sistema](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/system-stored-procedures-transact-sql) | Supportate in alcuni casi. Vedere le singole stored procedure |
| [Tabelle di sistema](https://docs.microsoft.com/sql/relational-databases/system-tables/system-tables-transact-sql) | Supportate in alcuni casi. Vedere le singole tabelle |
| [Viste del catalogo di sistema](https://docs.microsoft.com/sql/relational-databases/system-catalog-views/catalog-views-transact-sql) | Supportate in alcuni casi. Vedere le singole viste |
| [Partizionamento delle tabelle](https://docs.microsoft.com/sql/relational-databases/partitions/partitioned-tables-and-indexes) | Sì. Solo filegroup primari |
| [Tabelle temporanee](https://docs.microsoft.com/sql/t-sql/statements/create-table-transact-sql#temporary-tables) | Solo tabelle temporanee locali e globali con ambito database |
| [Tabelle temporali](https://docs.microsoft.com/sql/relational-databases/tables/temporal-tables) | Sì |
| [Transazioni](https://docs.microsoft.com/sql/t-sql/language-elements/transactions-transact-sql) | No |
| [Variabili](https://docs.microsoft.com/sql/t-sql/language-elements/variables-transact-sql) | Sì | 
| [Transparent Data Encryption (TDE)](https://docs.microsoft.com/sql/relational-databases/security/encryption/transparent-data-encryption-tde) | Sì |
| [Windows Server Failover Clustering](https://docs.microsoft.com/sql/sql-server/failover-clusters/windows/windows-server-failover-clustering-wsfc-with-sql-server) | No. Vedere [Gruppi di failover e replica geografica attiva](sql-database-geo-replication-overview.md) |
| [Indici XML](https://docs.microsoft.com/sql/t-sql/statements/create-xml-index-transact-sql) | Sì |

## <a name="next-steps"></a>Passaggi successivi

- Per informazioni su hello servizio Database SQL di Azure, vedere [che cos'è il Database SQL?](sql-database-technical-overview.md)
- Per informazioni sul supporto di Transact-SQL e le differenze, vedere [differenze risoluzione Transact-SQL durante la migrazione tooSQL Database](sql-database-transact-sql-information.md).
