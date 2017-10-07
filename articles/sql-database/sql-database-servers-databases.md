---
title: aaaCreate & gestire il server SQL Azure & database | Documenti Microsoft
description: Informazioni sui concetti di database e server di Database SQL di Azure e sulla creazione e la gestione di server e database che utilizzano hello portale di Azure PowerShell, hello CLI di Azure, Transact-SQL e hello API REST.
services: sql-database
documentationcenter: na
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/05/2017
ms.author: carlrab
ms.openlocfilehash: 0f526e388a5a620349f5a14e8d57a8355ac451ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-azure-sql-database-servers-and-databases"></a>Creare e gestire server e database del database SQL di Azure

Un database SQL di Azure è un database gestito in Microsoft Azure che viene creato in un [gruppo di risorse di Azure](../azure-resource-manager/resource-group-overview.md) con un set definito di [risorse di calcolo e archiviazione per carichi di lavoro diversi](sql-database-service-tiers.md). Un database SQL di Azure viene associato a un server logico di database SQL di Azure, creato all'interno di un'area specifica di Azure. 

## <a name="an-azure-sql-database-can-be-a-single-pooled-or-partitioned-database"></a>Un database SQL di Azure può essere un database singolo, in pool o partizionato

Un database SQL di Azure può essere:

- Un database singolo con relativo [set di risorse](sql-database-what-is-a-dtu.md#what-are-database-transaction-units-dtus) (DTU)
- Parte di un [pool elastico SQL](sql-database-elastic-pool.md) che [condivide un set di risorse](sql-database-what-is-a-dtu.md#what-are-elastic-database-transaction-units-edtus) (eDTU)
- Parte di un [set di scalabilità orizzontale di database partizionati](sql-database-elastic-scale-introduction.md#horizontal-and-vertical-scaling), che può essere singolo o in pool
- Parte di un set di database che fanno parte di uno [schema progettuale SaaS multi-tenant](sql-database-design-patterns-multi-tenancy-saas-applications.md), i cui database possono essere singoli o in pool (o entrambi) 

> [!TIP]
> Per i nomi di database validi, vedere [Database Identifiers](https://docs.microsoft.com/en-us/sql/relational-databases/databases/database-identifiers) (Identificatori di database). 
>
 
- Hello database regole di confronto predefinite utilizzate dal Database SQL di Microsoft Azure è **SQL_LATIN1_GENERAL_CP1_CI_AS**, dove **LATIN1_GENERAL** inglese (Stati Uniti), **CP1** è una tabella codici 1252, **CI** è tra maiuscole e minuscole, e **AS** accentati. Per ulteriori informazioni su come tooset hello regole di confronto, vedere [COLLATE (Transact-SQL)](https://msdn.microsoft.com/library/ms184391.aspx).
- Il database SQL di Microsoft Azure supporta la versione client 7.3 o successiva del protocollo TDS (Tabular Data Stream).
- Sono consentite solo connessioni TCP/IP.

## <a name="what-is-an-azure-sql-logical-server"></a>Che cos'è un server logico SQL di Azure?

Un server logico funge da punto amministrativo centrale per più database, inclusi [pool elastici SQL](sql-database-elastic-pool.md), [account di accesso](sql-database-manage-logins.md), [regole del firewall](sql-database-firewall-configure.md), [regole di controllo](sql-database-auditing.md), [criteri di rilevamento delle minacce](sql-database-threat-detection.md) e [gruppi di failover](sql-database-geo-replication-overview.md). Un server logico può trovarsi in un'area diversa rispetto al relativo gruppo di risorse. Hello del server logico deve esistere prima di poter creare database SQL di Azure hello. Tutti i database in un server vengono creati all'interno di hello stesso server logico hello area. 


> [!IMPORTANT]
> Nel Database SQL di un server è un costrutto logico che è diverso da quello di un'istanza di SQL Server che potrebbero avere familiarità con in HelloWorld locale. In particolare, hello servizio Database SQL offre alcuna garanzia sulla posizione del database hello in relazione server logici tootheir ed non espone alcun accesso a livello di istanza o le funzionalità.
> 

Quando si crea un server logico, immettere un server di account di accesso e una password che dispone di diritti amministrativi toohello il database master nel server e tutti i database creati in tale server. Questo account iniziale è un account di accesso SQL. Il database SQL di Azure supporta l'autenticazione SQL e l'autenticazione di Azure Active Directory. Per informazioni su account di accesso e autenticazione, vedere [Gestione di database e account di accesso nel database SQL di Azure](sql-database-manage-logins.md). L'autenticazione Windows non è supportata. 

> [!TIP]
> Per i nomi di gruppi di risorse e server validi, vedere [Regole di denominazione e restrizioni](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions).
>

Un server logico del database di Azure:

- Viene creato all'interno di una sottoscrizione di Azure, ma possono essere spostati con la sottoscrizione di risorse indipendente tooanother
- Risorsa padre hello per database, il pool elastico e data warehouse
- Fornisce uno spazio dei nomi per database, pool elastici e data warehouse
- È un contenitore logico con la semantica di durata sicuro - Elimina un server e Elimina hello database indipendenti, il pool elastico e data warehouse
- Partecipa [il controllo di accesso di Azure basata sui ruoli (RBAC)](/active-directory/role-based-access-control-what-is) -database, il pool elastico e data warehouse in un server ereditano i diritti di accesso dal server di hello
- È un elemento di ordine superiore dell'identità hello del database, il pool elastico e data warehouse per la risorsa di Azure a scopo di gestione (vedere URL hello schema per i database e i pool)
- Colloca risorse in un'area
- Fornisce un endpoint di connessione per l'accesso ai database (<serverName>.database.windows.net)
- Fornisce accesso toometadata riguardanti tramite DMV le risorse indipendenti dal database master di connessione tooa 
- Fornisce l'ambito di hello per criteri di gestione che si applicano tooits database - account di accesso, firewall, controllo, minaccia di rilevamento e così via. 
- È limitato da una quota nella sottoscrizione padre hello (sei server per ogni sottoscrizione per impostazione predefinita - [vedere sottoscrizione limita qui](../azure-subscription-service-limits.md))
- Fornisce l'ambito di hello per la quota di database e la quota DTU per le risorse di hello che contiene (ad esempio 45.000 DTU)
- Ambito di controllo delle versioni hello per funzionalità abilitate sulle risorse indipendenti 
- Gli account di accesso all'entità a livello di server possono gestire tutti i database in un server
- Può contenere gli account di accesso simile toothose nelle istanze di SQL Server on-premise che dispongono di accesso tooone o più database nel server di hello e possono essere concessi i diritti amministrativi limitati. Per altre informazioni, vedere [Autenticazione e autorizzazione per database SQL: concessione dell'accesso](sql-database-manage-logins.md).

## <a name="azure-sql-databases-protected-by-sql-database-firewall"></a>I database SQL di Azure sono protetti dal firewall del database SQL

toohelp proteggere i dati, un [firewall del Database SQL](sql-database-firewall-configure.md) impedisce a tutti i server di database di access tooyour o i relativi database di fuori del server di toohello connessione direttamente tramite la connessione di sottoscrizione di Azure. connettività aggiuntive tooenable, è necessario [creare uno o più regole firewall](sql-database-firewall-configure.md#creating-and-managing-firewall-rules). Per creare e gestire i pool elastici SQL, vedere [Pool elastici](sql-database-elastic-pool.md).

## <a name="manage-azure-sql-servers-databases-and-firewalls-using-hello-azure-portal"></a>Gestire i server SQL Azure, database e i firewall mediante hello portale di Azure

È possibile creare gruppo di risorse del database SQL di Azure hello anticipatamente o durante la creazione di server hello stesso. Sono disponibili più metodi per ottenere tooa nuovo modulo server SQL, creando un nuovo server SQL o come parte della creazione di un nuovo database. 

### <a name="create-a-blank-sql-server-logical-server"></a>Creare un server SQL Server vuoto (server logico)

un server (senza un database) di Database SQL di Azure utilizzando toocreate hello [portale di Azure](https://portal.azure.com), passare a un modulo vuoto SQL server (server logico) tooa. Hello schermata riportata di seguito viene illustrato un metodo per l'apertura di un modulo toocreate un server SQL logico vuoto. 

   ![modulo di creazione del server logico completato](./media/sql-database-migrate-your-sql-server-database/logical-server-create-completed.png)

Se viene visualizzato il modulo toothis utilizzando un altro metodo, informazioni hello in form di hello sono identiche.

### <a name="create-a-blank-or-sample-sql-database"></a>Creare un database SQL vuoto o di esempio

un database SQL di Azure utilizzando toocreate hello [portale di Azure](https://portal.azure.com), passare a un modulo del Database SQL vuoto tooa e fornire hello ha chiesto informazioni. È possibile creare il gruppo di risorse del database SQL di Azure hello e server logico anticipatamente o durante la creazione di database hello stesso. È possibile creare un database vuoto o creare un database di esempio basato su Adventure Works LT. 

  ![Creare il database 1](./media/sql-database-get-started-portal/create-database-1.png)

> [IMPORTANTE] Per informazioni sulla selezione di hello piano tariffario per il database, vedere [livelli di servizio](sql-database-service-tiers.md).
>

### <a name="manage-an-existing-sql-server"></a>Gestire un server SQL Server esistente

toomanage un server esistente, passare toohello server utilizzando un numero di metodi, ad esempio a causa di una pagina di database SQL specifico, hello **istanze di SQL Server** pagina o hello **tutte le risorse** pagina. Hello seguente schermata mostra come l'impostazione di un firewall a livello di server da hello toobegin **Panoramica** pagina per un server. 

   ![panoramica del server logico](./media/sql-database-migrate-your-sql-server-database/logical-server-overview.png)

toomanage un database esistente, passare toohello **database SQL** pagina e fare clic su database hello desiderato toomanage. Hello seguente schermata mostra come l'impostazione di un firewall di livello server per un database da hello toobegin **Panoramica** pagina di un database. 

   ![Regola del firewall del server](./media/sql-database-get-started-portal/server-firewall-rule.png) 

> [!IMPORTANT]
> proprietà tooconfigure delle prestazioni per un database, vedere [livelli di servizio](sql-database-service-tiers.md).
>

> [!TIP]
> Per un'esercitazione introduttiva del portale Azure, vedere [creare un database SQL di Azure nel portale di Azure hello](sql-database-get-started-portal.md).
>

## <a name="manage-azure-sql-servers-databases-and-firewalls-using-powershell"></a>Gestire server, database e firewall SQL di Azure con PowerShell

toocreate e gestire server SQL di Azure, database e i firewall con Azure PowerShell, usare i cmdlet di PowerShell seguente hello. Se è necessario tooinstall o l'aggiornamento di PowerShell, vedere [modulo installare Azure PowerShell](/powershell/azure/install-azurerm-ps). Per creare e gestire i pool elastici SQL, vedere [Pool elastici](sql-database-elastic-pool.md).

| Cmdlet | Descrizione |
| --- | --- |
|[New-AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase)|Crea un database |
|[Get-AzureRmSqlDatabase](/powershell/module/azurerm.sql/get-azurermsqldatabase)|Recupera uno o più database|
|[Set-AzureRmSqlDatabase](/powershell/module/azurerm.sql/set-azurermsqldatabase)|Imposta le proprietà per un database oppure sposta un database esistente in un pool elastico|
|[Remove-AzureRmSqlDatabase](/powershell/module/azurerm.sql/remove-azurermsqldatabase)|Rimuove un database|
|[New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup)|Crea un gruppo di risorse]
|[New-AzureRmSqlServer](/powershell/module/azurerm.sql/new-azurermsqlserver)|Crea un server|
|[Get-AzureRmSqlServer](/powershell/module/azurerm.sql/get-azurermsqlserver)|Restituisce informazioni sui server|
|[Set-AzureRmSqlServer](https://docs.microsoft.com/en-us/powershell/module/azurerm.sql/set-azurermsqlserver)|Modifica le proprietà di un server|
|[Remove-AzureRmSqlServer](/powershell/module/azurerm.sql/remove-azurermsqlserver)|Rimuove un server|
|[New-AzureRmSqlServerFirewallRule](/powershell/module/azurerm.sql/new-azurermsqlserverfirewallrule)|Crea una regola del firewall a livello di server |
|[Get-AzureRmSqlServerFirewallRule](/powershell/module/azurerm.sql/get-azurermsqlserverfirewallrule)|Ottiene le regole del firewall per un server|
|[Set-AzureRmSqlServerFirewallRule](/powershell/module/azurerm.sql/set-azurermsqlserverfirewallrule)|Modifica una regola del firewall in un server|
|[Remove-AzureRmSqlServerFirewallRule](/powershell/module/azurerm.sql/remove-azurermsqlserverfirewallrule)|Elimina una regola del firewall da un server|

> [!TIP]
> Per un'esercitazione introduttiva su PowerShell, vedere [Creare un singolo database SQL di Azure usando PowerShell](sql-database-get-started-portal.md). Per gli script di esempio di PowerShell, vedere [toocreate PowerShell di usare un singolo SQL Azure database e configurare una regola del firewall](scripts/sql-database-create-and-configure-database-powershell.md) e [monitoraggio e la scala di un singolo SQL del database tramite PowerShell](scripts/sql-database-monitor-and-scale-database-powershell.md).
>

## <a name="manage-azure-sql-servers-databases-and-firewalls-using-hello-azure-cli"></a>Gestire i server SQL Azure, database e i firewall mediante hello CLI di Azure

toocreate e gestire i server SQL Azure, database e i firewall con hello [CLI di Azure](/cli/azure/overview), utilizzare la seguente hello [Database SQL di Azure CLI](/cli/azure/sql/db) comandi. Hello utilizzare [Shell Cloud](/azure/cloud-shell/overview) toorun hello CLI nel browser o [installare](/cli/azure/install-azure-cli) sul macOS, Linux o Windows. Per creare e gestire i pool elastici SQL, vedere [Pool elastici](sql-database-elastic-pool.md).

| Cmdlet | Descrizione |
| --- | --- |
|[az sql db create](/cli/azure/sql/db#create) |Crea un database|
|[az sql db list](/cli/azure/sql/db#list)|Elenca tutti i database e i data warehouse in un server o tutti i database in un pool elastico|
|[az sql db list-editions](/cli/azure/sql/db#list-editions)|Elenca gli obiettivi di servizio e i limiti di archiviazione disponibili|
|[az sql db list-usages](/cli/azure/sql/db#list-usages)|Restituisce gli utilizzi del database|
|[az sql db show](/cli/azure/sql/db#show)|Recupera un database o un data warehouse|
|[az sql db update](/cli/azure/sql/db#update)|Aggiorna un database|
|[az sql db delete](/cli/azure/sql/db#delete)|Rimuove un database|
|[az group create](/cli/azure/group#create)|Crea un gruppo di risorse|
|[az sql server create](/cli/azure/sql/server#create)|Crea un server|
|[az sql server list](/cli/azure/sql/server#list)|Elenca i server|
|[az sql server list-usages](/cli/azure/sql/server#list-usages)|Restituisce gli utilizzi del server|
|[az sql server show](/cli/azure/sql/server#show)|Ottiene un server|
|[az sql server update](/cli/azure/sql/server#update)|Aggiorna un server|
|[az sql server delete](/cli/azure/sql/server#delete)|Consente di eliminare un server|
|[az sql server firewall-rule create](/cli/azure/sql/server/firewall-rule#create)|Crea una regola del firewall del server|
|[az sql server firewall-rule list](/cli/azure/sql/server/firewall-rule#list)|Elenca le regole firewall hello in un server|
|[az sql server firewall-rule show](/cli/azure/sql/server/firewall-rule#show)|Mostra il dettaglio hello di una regola del firewall|
|[az sql server firewall-rule update](/cli/azure/sql/server/firewall-rule#update)|Aggiorna una regola del firewall|
|[az sql server firewall-rule delete](/cli/azure/sql/server/firewall-rule#delete)|Elimina una regola del firewall|

> [!TIP]
> Per un'esercitazione introduttiva di Azure CLI, vedere [creare un singolo database di SQL Azure mediante Azure CLI hello](sql-database-get-started-cli.md). Per gli script di esempio CLI di Azure, vedere [toocreate CLI di utilizzare un singolo SQL Azure database e configurare una regola del firewall](scripts/sql-database-create-and-configure-database-cli.md) e [toomonitor CLI di utilizzo e la scala di un singolo database SQL](scripts/sql-database-monitor-and-scale-database-cli.md).
>

## <a name="manage-azure-sql-servers-databases-and-firewalls-using-transact-sql"></a>Gestire server, database e firewall SQL di Azure con Transact-SQL

toocreate e gestire server SQL di Azure, database e i firewall con Transact-SQL, utilizzare i comandi T-SQL seguente hello. È possibile eseguire questi comandi utilizzando il portale di Azure, hello [SQL Server Management Studio](/sql/ssms/use-sql-server-management-studio), [codice di Visual Studio](https://code.visualstudio.com/docs), o qualsiasi altro programma che è possibile connettere il server di Database SQL di Azure tooan e passare a Transact-SQL comandi. Per la gestione dei pool elastici SQL, vedere [Pool elastici](sql-database-elastic-pool.md).

> [!IMPORTANT]
> Non è possibile creare o eliminare un server con Transact-SQL.
>

| Comando | Descrizione |
| --- | --- |
|[CREATE DATABASE (database SQL di Azure)](/sql/t-sql/statements/create-database-azure-sql-database)|Crea un nuovo database. È necessario essere connessi toohello database master toocreate un nuovo database.|
| [ALTER DATABASE (database SQL di Azure)](/sql/t-sql/statements/alter-database-azure-sql-database) |Modifica un database SQL di Azure. |
|[ALTER DATABASE (Azure SQL Data Warehouse)](/sql/t-sql/statements/alter-database-azure-sql-data-warehouse)|Modifica un Azure SQL Data Warehouse.|
|[DROP DATABASE (Transact-SQL)](/sql/t-sql/statements/drop-database-transact-sql)|Questo comando elimina un database.|
|[sys.database_service_objectives (database SQL di Azure)](/sql/relational-databases/system-catalog-views/sys-database-service-objectives-azure-sql-database)|Restituisce hello edizione (livello di servizio), l'obiettivo di servizio (livello di prezzo) e nome del pool elastico, se presente, per un database SQL di Azure o un Data Warehouse di SQL Azure. Se connesso al database master di toohello in un server di Database SQL di Azure, restituisce informazioni su tutti i database. Per Azure SQL Data Warehouse, è necessario essere connessi toohello database master.|
|[sys.dm_db_resource_stats (database SQL di Azure)](/sql/relational-databases/system-dynamic-management-views/sys-dm-db-resource-stats-azure-sql-database)| Restituisce il consumo di CPU, I/O e memoria per un database SQL di Azure. È presente una riga per ogni 15 secondi, anche se è presente alcuna attività nel database di hello.|
|[sys.resource_stats (database SQL di Azure)](/sql/relational-databases/system-catalog-views/sys-resource-stats-azure-sql-database)|Restituisce i dati di archiviazione e di uso della CPU per un database SQL di Azure. dati Hello vengono raccolti e aggregati in intervalli di cinque minuti.|
|[sys.database_connection_stats (database SQL di Azure)](/sql/relational-databases/system-catalog-views/sys-database-connection-stats-azure-sql-database)|Contiene le statistiche per gli eventi di connettività di database del database SQL fornendo una panoramica delle connessioni di database riuscite e non riuscite. |
|[sys.event_log (database SQL di Azure)](/sql/relational-databases/system-catalog-views/sys-event-log-azure-sql-database)|Restituisce le connessioni del database SQL di Azure che hanno esito positivo, quelle che hanno esito negativo e i deadlock. È possibile utilizzare questo tootrack informazioni o risolvere i problemi dell'attività del database con il Database SQL.|
|[sp_set_firewall_rule (database SQL di Azure)](/sql/relational-databases/system-stored-procedures/sp-set-firewall-rule-azure-sql-database)|Crea o aggiorna le impostazioni firewall di livello server hello del server di Database SQL. Questa stored procedure è disponibile solo con account di accesso dell'entità a livello di server di hello toohello database master. Una regola del firewall a livello di server può essere creata solo tramite Transact-SQL dopo la prima regola del firewall di livello server hello è stato creato da un utente con autorizzazioni a livello di Azure|
|[sys.firewall_rules (database SQL di Azure)](/sql/relational-databases/system-catalog-views/sys-firewall-rules-azure-sql-database)|Restituisce informazioni sulle impostazioni del firewall a livello di server hello associata con il Database SQL di Microsoft Azure.|
|[sp_delete_firewall_rule (database SQL di Azure)](/sql/relational-databases/system-stored-procedures/sp-delete-firewall-rule-azure-sql-database)|Rimuove le impostazioni del firewall a livello di server dal server di database SQL. Questa stored procedure è disponibile solo con account di accesso dell'entità a livello di server di hello toohello database master.|
|[sp_set_database_firewall_rule (database SQL di Azure)](/sql/relational-databases/system-stored-procedures/sp-set-database-firewall-rule-azure-sql-database)|Crea o aggiorna regole firewall di livello database hello per il Database SQL di Azure o SQL Data Warehouse. Configurare le regole firewall del database per database master hello e per i database utente nel Database SQL. Le regole del firewall del database sono utili quando si usano utenti di database indipendenti. |
|[sys.database_firewall_rules (database SQL di Azure)](/sql/relational-databases/system-catalog-views/sys-database-firewall-rules-azure-sql-database)|Restituisce informazioni sulle impostazioni del firewall a livello di database hello associata con il Database SQL di Microsoft Azure. |
|[sp_delete_database_firewall_rule (database SQL di Azure)](/sql/relational-databases/system-stored-procedures/sp-delete-database-firewall-rule-azure-sql-database)|Rimuove l'impostazione del firewall a livello di database dal database SQL di Azure o da SQL Data Warehouse. |


> [!TIP]
> Per l'esercitazione introduttiva utilizzando SQL Server Management Studio per Microsoft Windows, vedere [Database SQL di Azure: dati tooconnect e query di utilizzare SQL Server Management Studio](sql-database-connect-query-ssms.md). Per un'esercitazione di avvio rapido con codice di Visual Studio in macOS hello, Linux o Windows, vedere [Database SQL di Azure: dati tooconnect e query di utilizzare Visual Studio Code](sql-database-connect-query-vscode.md).

## <a name="manage-azure-sql-servers-databases-and-firewalls-using-hello-rest-api"></a>Gestire i server SQL Azure, database e i firewall mediante l'API REST hello

toocreate e gestire i server SQL di Azure, database e i firewall mediante hello API REST, vedere [API REST di Azure SQL Database](/rest/api/sql/).

## <a name="next-steps"></a>Passaggi successivi

- toolearn sui pool di database con i pool elastici SQL, vedere [pool elastici](sql-database-elastic-pool.md).
- Per informazioni su hello servizio Database SQL di Azure, vedere [che cos'è il Database SQL?](sql-database-technical-overview.md).
- toolearn sulla migrazione tooAzure un database di SQL Server, vedere [eseguire la migrazione di Database SQL tooAzure](sql-database-cloud-migrate.md).
- Per informazioni sulle funzionalità supportate, vedere [Azure SQL Database features](sql-database-features.md) (Funzioni del database SQL di Azure).
