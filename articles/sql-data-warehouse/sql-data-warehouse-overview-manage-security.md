---
title: Proteggere un database in SQL Data Warehouse | Documentazione Microsoft
description: Suggerimenti per proteggere un database in Azure SQL Data Warehouse per lo sviluppo di soluzioni.
services: sql-data-warehouse
documentationcenter: NA
author: ronortloff
manager: jhubbard
editor: 
ms.assetid: 8fa2f5ca-4cf5-4418-99a2-4dc745799850
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: security
ms.date: 10/31/2016
ms.author: rortloff;barbkess
ms.openlocfilehash: 6ea45c40bc428282faf24b4a08f8b0d345adb3fd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="secure-a-database-in-sql-data-warehouse"></a>Proteggere un database in SQL Data Warehouse
> [!div class="op_single_selector"]
> * [Proteggere un database in SQL Data Warehouse](sql-data-warehouse-overview-manage-security.md)
> * [Autenticazione](sql-data-warehouse-authentication.md)
> * [Introduzione a Transparent Data Encryption (TDE) di SQL Data Warehouse](sql-data-warehouse-encryption-tde.md)
> * [Introduzione a Transparent Data Encryption (TDE)](sql-data-warehouse-encryption-tde-tsql.md)
> 
> 

Questo articolo illustra i concetti di base relativi alla protezione del proprio database di Azure SQL Data Warehouse. In particolare l'articolo spiega come iniziare a usare le risorse per limitare l'accesso, proteggere i dati e monitorare le attività in un database.

## <a name="connection-security"></a>Sicurezza delle connessioni
La sicurezza delle connessioni fa riferimento al modo che si limitano e proteggono le connessioni al database mediante regole del firewall e crittografia di connessione.

Le regole del firewall vengono usate dal server e dal database per rifiutare i tentativi di connessione da indirizzi IP che non sono stati esplicitamente inclusi nell'elenco di IP consentiti. Prima di consentire le connessioni dall'applicazione o dall'indirizzo IP pubblico del computer client è necessario creare una regola firewall di livello server tramite il portale di Azure, l'API REST o PowerShell. Come procedura consigliata, si suggerisce di limitare gli intervalli di indirizzi IP consentiti attraverso il firewall del server quanto più possibile.  Per accedere ad Azure SQL Data Warehouse dal computer locale, verificare che il firewall in rete e nel computer locale consenta le comunicazioni in uscita sulla porta TCP 1433.  Per altre informazioni, vedere il [firewall per il database SQL di Azure][Azure SQL Database firewall], [sp_set_firewall_rule][sp_set_firewall_rule] e [sp_set_database_firewall_rule][sp_set_database_firewall_rule].

Le connessioni a SQL Data Warehouse vengono crittografate per impostazione predefinita.  La modifica delle impostazioni di connessione per disabilitare la crittografia viene ignorata.

## <a name="authentication"></a>Autenticazione
Per autenticazione si intende il modo in cui viene dimostrata la propria identità durante la connessione al database. SQL Data Warehouse attualmente supporta l'autenticazione di SQL Server con un nome utente e una password, nonché con Azure Active Directory. 

Durante la creazione del server logico per il database, è stato specificato un account di accesso "amministratore del server" con un nome utente e una password. Con queste credenziali è possibile eseguire l'autenticazione in qualsiasi database di tale server come proprietario del database, o "dbo", tramite l'autenticazione di SQL Server.

Tuttavia, come procedura consigliata, è opportuno che gli utenti dell'organizzazione usino un account diverso per l'autenticazione. Questo modo può possibile limitare le autorizzazioni concesse all'applicazione e ridurre i rischi di attività dannose nel caso in cui il codice dell'applicazione sia vulnerabile a un attacco SQL injection. 

Per creare un utente autenticato in SQL Server, connettersi al database **master** nel proprio server con l'account di accesso amministratore e creare un nuovo accesso al server.  Inoltre, è consigliabile creare un utente nel database master per gli utenti di SQL Data Warehouse di Azure. La creazione di un utente nel database master consente all'utente di accedere tramite strumenti come SSMS senza specificare un nome di database.  Consente inoltre di usare Esplora oggetti per visualizzare tutti i database in SQL server.

```sql
-- Connect to master database and create a login
CREATE LOGIN ApplicationLogin WITH PASSWORD = 'Str0ng_password';
CREATE USER ApplicationUser FOR LOGIN ApplicationLogin;
```

Quindi connettersi al **database di SQL Data Warehouse** con l'account di accesso amministratore server e creare un utente di database basato sull'account di accesso al server appena creato.

```sql
-- Connect to SQL DW database and create a database user
CREATE USER ApplicationUser FOR LOGIN ApplicationLogin;
```

Se un utente esegue altre operazioni, ad esempio crea accessi o nuovi database, avrà anche bisogno dell'assegnazione dei ruoli `Loginmanager` e `dbmanager` nel database master. Per altre informazioni sui questi ruoli aggiuntivi e sull'autenticazione a un database SQL, vedere [Gestione di database e account di accesso in database SQL di Azure][Managing databases and logins in Azure SQL Database].  Per altre informazioni su Azure AD per SQL Data Warehouse, vedere [Connessione a SQL Data Warehouse con l'autenticazione di Azure Active Directory][Connecting to SQL Data Warehouse By Using Azure Active Directory Authentication].

## <a name="authorization"></a>Authorization
Per autorizzazione si intendono le operazioni che è possibile effettuare all'interno di un database di Azure SQL Data Warehouse e questa funzionalità viene controllata mediante le autorizzazioni e le appartenenze ai ruoli dell'account utente. Come procedura consigliata, è opportuno concedere agli utenti i privilegi minimi necessari. Azure SQL Data Warehouse ne semplifica la gestione con i ruoli in T-SQL:

```sql
EXEC sp_addrolemember 'db_datareader', 'ApplicationUser'; -- allows ApplicationUser to read data
EXEC sp_addrolemember 'db_datawriter', 'ApplicationUser'; -- allows ApplicationUser to write data
```

L'account di amministrazione del server a cui ci si sta connettendo è un membro del ruolo db_owner, che è autorizzato a eseguire qualsiasi operazione all'interno del database. Salvare questo account per la distribuzione degli aggiornamenti allo schema e altre operazioni di gestione. Utilizzare l'account "ApplicationUser" con autorizzazioni più limitate per la connessione dall'applicazione al database con i privilegi minimi richiesti dall'applicazione.

Esistono modi per limitare ulteriormente le operazioni possibili con il database SQL di Azure:

* Le [autorizzazioni][Permissions] granulari consentono di controllare le operazioni possibili per le singole colonne, tabelle, viste, procedure e altri oggetti nel database. Usare le autorizzazioni granulari per avere il massimo controllo e concedere solo le autorizzazioni necessarie. Il sistema di autorizzazioni granulari è complesso; per usarlo in modo efficace è necessario un certo grado di preparazione.
* È possibile usare [ruoli del database][Database roles] diversi da db_datareader e db_datawriter per creare account utente dell'applicazione più potenti o account di gestione meno potenti. I ruoli del database predefiniti incorporati sono una soluzione semplice per la concessione di autorizzazioni, ma possono concedere più autorizzazioni di quelle necessarie.
* È possibile usare [stored procedure][Stored procedures] per limitare le operazioni che possono essere eseguite nel database.

La gestione di database e server logici dal portale di Azure classico o mediante l'API di gestione risorse di Azure viene controllata dalle assegnazioni di ruolo dell'account utente del portale. Per altre informazioni su questo argomento, vedere [Controllo degli accessi in base al ruolo nel portale di Azure][Role-based access control in Azure Portal].

## <a name="encryption"></a>Crittografia
La funzionalità Transparent Data Encryption (TDE) di Azure SQL Data Warehouse consente di proteggersi da attività dannose eseguendo in tempo reale la crittografia e la decrittografia dei dati inattivi.  Quando si crittografa il database, i file di log delle transazioni e i backup associati vengono crittografati senza bisogno di apportare modifiche alle applicazioni. TDE esegue la crittografia dell'archiviazione di un intero database usando una chiave simmetrica detta "chiave di crittografia del database". Nel database SQL la chiave di crittografia del database è protetta da un certificato server incorporato. Il certificato server incorporato è univoco per ogni server di database SQL. Microsoft ruota automaticamente questi certificati almeno ogni 90 giorni. L’algoritmo di crittografia utilizzato da SQL Data Warehouse è AES-256. Per una descrizione generale della funzionalità TDE, vedere [Transparent Data Encryption][Transparent Data Encryption].

È possibile crittografare il database usando il [portale di Azure][Encryption with Portal] o [T-SQL][Encryption with TSQL].

## <a name="next-steps"></a>Passaggi successivi
Per informazioni dettagliate ed esempi di connessione a SQL Data Warehouse con protocolli diversi, vedere [Connettersi ad Azure SQL Data Warehouse][Connect to SQL Data Warehouse].

<!--Image references-->

<!--Article references-->
[Connect to SQL Data Warehouse]: ./sql-data-warehouse-connect-overview.md
[Encryption with Portal]: ./sql-data-warehouse-encryption-tde.md
[Encryption with TSQL]: ./sql-data-warehouse-encryption-tde-tsql.md
[Connecting to SQL Data Warehouse By Using Azure Active Directory Authentication]: ./sql-data-warehouse-authentication.md

<!--MSDN references-->
[Azure SQL Database firewall]: https://msdn.microsoft.com/library/ee621782.aspx
[sp_set_firewall_rule]: https://msdn.microsoft.com/library/dn270017.aspx
[sp_set_database_firewall_rule]: https://msdn.microsoft.com/library/dn270010.aspx
[Database roles]: https://msdn.microsoft.com/library/ms189121.aspx
[Managing databases and logins in Azure SQL Database]: https://msdn.microsoft.com/library/ee336235.aspx
[Permissions]: https://msdn.microsoft.com/library/ms191291.aspx
[Stored procedures]: https://msdn.microsoft.com/library/ms190782.aspx
[Transparent Data Encryption]: https://msdn.microsoft.com/library/bb934049.aspx
[Azure portal]: https://portal.azure.com/

<!--Other Web references-->
[Role-based access control in Azure Portal]: https://azure.microsoft.com/documentation/articles/role-based-access-control-configure
