---
title: un database in SQL Data Warehouse aaaSecure | Documenti Microsoft
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
ms.openlocfilehash: 5ef4d760e00be46bfe7808bc95dbe1e4b3a51165
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="secure-a-database-in-sql-data-warehouse"></a>Proteggere un database in SQL Data Warehouse
> [!div class="op_single_selector"]
> * [Proteggere un database in SQL Data Warehouse](sql-data-warehouse-overview-manage-security.md)
> * [Autenticazione](sql-data-warehouse-authentication.md)
> * [Introduzione a Transparent Data Encryption (TDE) di SQL Data Warehouse](sql-data-warehouse-encryption-tde.md)
> * [Introduzione a Transparent Data Encryption (TDE)](sql-data-warehouse-encryption-tde-tsql.md)
> 
> 

In questo articolo vengono illustrati concetti di base di hello per proteggere il database di Azure SQL Data Warehouse. In particolare l'articolo spiega come iniziare a usare le risorse per limitare l'accesso, proteggere i dati e monitorare le attività in un database.

## <a name="connection-security"></a>Sicurezza delle connessioni
Sicurezza della connessione fa riferimento toohow limitare e proteggere le connessioni tooyour database utilizzando le regole del firewall e crittografia delle connessioni.

Le regole del firewall vengono utilizzate da entrambi hello server e hello database tooreject tentativi di connessione da indirizzi IP che non sono stato esplicitamente consentito. connessioni tooallow dall'applicazione o indirizzo IP pubblico del computer client, è innanzitutto necessario creare una regola firewall di livello server usando hello portale di Azure, API REST o PowerShell. Come procedura consigliata, è consigliabile limitare gli intervalli di indirizzi IP hello consentiti attraverso il firewall del server il più possibili.  tooaccess Azure SQL Data Warehouse dal computer locale, verificare che il firewall di hello in rete e nel computer locale consenta la comunicazione in uscita sulla porta TCP 1433.  Per altre informazioni, vedere il [firewall per il database SQL di Azure][Azure SQL Database firewall], [sp_set_firewall_rule][sp_set_firewall_rule] e [sp_set_database_firewall_rule][sp_set_database_firewall_rule].

Connessioni tooyour SQL Data Warehouse vengono crittografate per impostazione predefinita.  Modifica connessione impostazioni toodisable crittografia vengono ignorati.

## <a name="authentication"></a>Autenticazione
L'autenticazione si riferisce toohow dimostrare la propria identità durante la connessione di database toohello. SQL Data Warehouse attualmente supporta l'autenticazione di SQL Server con un nome utente e una password, nonché con Azure Active Directory. 

Durante la creazione di server logico hello per il database, è specificato un account di accesso "amministratore del server" con un nome utente e password. Utilizzando queste credenziali, è possibile autenticare tooany database su tale server come proprietario del database hello o "dbo" tramite l'autenticazione di SQL Server.

Tuttavia, come procedura consigliata, gli utenti dell'organizzazione devono utilizzare tooauthenticate un account diverso. In questo modo è possibile limitare le autorizzazioni di hello concesse toohello applicazione e ridurre i rischi di hello di attività dannose nel caso in cui il codice dell'applicazione attacco SQL injection di tooa vulnerabile. 

toocreate un utente con autenticazione di SQL Server, connettersi toohello **master** sul server con l'account di accesso di amministratore di server di database e creare un nuovo account di accesso server.  Inoltre, è toocreate una buona idea un utente nel database master di hello per gli utenti di Azure SQL Data Warehouse. Creazione di un utente nel database master consente a un utente toologin usando strumenti come SQL Server Management Studio senza specificare un nome di database.  Inoltre, consente loro toouse hello oggetto explorer tooview tutti i database in SQL server.

```sql
-- Connect toomaster database and create a login
CREATE LOGIN ApplicationLogin WITH PASSWORD = 'Str0ng_password';
CREATE USER ApplicationUser FOR LOGIN ApplicationLogin;
```

Quindi, connettersi tooyour **database SQL Data Warehouse** con l'account di accesso di amministratore di server e creare un utente di database basato su account di accesso server hello appena creato.

```sql
-- Connect tooSQL DW database and create a database user
CREATE USER ApplicationUser FOR LOGIN ApplicationLogin;
```

Se si prevede di effettuare operazioni aggiuntive, ad esempio creare account di accesso o la creazione di nuovi database, sarà anche necessario toobe assegnato toohello `Loginmanager` e `dbmanager` ruoli nel database master hello. Per ulteriori informazioni su questi ruoli aggiuntivi e autenticazione tooa Database SQL, vedere [gestione di database e account di accesso nel Database SQL di Azure][Managing databases and logins in Azure SQL Database].  Per ulteriori informazioni su Azure AD per SQL Data Warehouse, vedere [connessione tooSQL dati Warehouse da usando Azure Active Directory Authentication][Connecting tooSQL Data Warehouse By Using Azure Active Directory Authentication].

## <a name="authorization"></a>Authorization
L'autorizzazione fa riferimento toowhat è possibile eseguire all'interno di un database Azure SQL Data Warehouse e questa funzionalità è controllata dalle appartenenze al ruolo e dalle autorizzazioni dell'account utente. Come procedura consigliata, è necessario concedere privilegi minimi necessari hello gli utenti. Azure SQL Data Warehouse rende questo toomanage facilmente con i ruoli di T-SQL:

```sql
EXEC sp_addrolemember 'db_datareader', 'ApplicationUser'; -- allows ApplicationUser tooread data
EXEC sp_addrolemember 'db_datawriter', 'ApplicationUser'; -- allows ApplicationUser toowrite data
```

si è connessi con account amministratore del server Hello è un membro del ruolo db_owner, con le operazioni nel database di hello toodo autorità. Salvare questo account per la distribuzione degli aggiornamenti allo schema e altre operazioni di gestione. Utilizzare l'account "ApplicationUser" hello con tooconnect più limitato di autorizzazioni dal database dell'applicazione toohello con hello privilegi minimi necessari per l'applicazione.

Sono disponibili modi toofurther limite cosa si può fare con Database SQL di Azure:

* Livello di granularità [autorizzazioni] [ Permissions] consentono di controllo quali operazioni è possibile per le singole colonne, tabelle, viste, procedure e altri oggetti nel database di hello. Utilizzare autorizzazioni granulari toohave hello maggiore controllo e concedere le autorizzazioni minime a hello necessarie. sistema di un'autorizzazione di granularità Hello è abbastanza complesso e richiederà alcuni toouse Studio in modo efficace.
* [Ruoli del database] [ Database roles] diverso db_datareader e db_datawriter può essere utilizzato toocreate più potente applicazione gli account utente o account di gestione meno potenti. ruoli predefiniti del database incorporato Hello forniscono le autorizzazioni toogrant un modo semplice, ma possono comportare la concessione di ulteriori autorizzazioni rispetto al necessario.
* [Stored procedure] [ Stored procedures] può essere utilizzato toolimit azioni hello che possono essere eseguite sul database hello.

Gestione di database e server logici da hello portale classico di Azure o tramite API di gestione risorse di Azure hello è controllato dalle assegnazioni di ruolo dell'account utente del portale. Per altre informazioni su questo argomento, vedere [Controllo degli accessi in base al ruolo nel portale di Azure][Role-based access control in Azure Portal].

## <a name="encryption"></a>Crittografia
Azure SQL Data Warehouse Transparent Data Encryption (TDE) contribuisce alla protezione dalle minacce di hello di attività dannose eseguendo la crittografia in tempo reale e la decrittografia dei dati inattivi.  Quando si esegue la crittografia del database, senza richiedere modifiche tooyour applicazioni vengono crittografati i backup associati e i file di log delle transazioni. Transparent Data Encryption crittografa l'archivio di hello di un intero database utilizzando una chiave di crittografia simmetrica hello chiamata chiave database. Nel Database SQL di chiave di crittografia del database hello è protetto da un certificato server predefinito. certificato server predefinito Hello è univoco per ogni server di Database SQL. Microsoft ruota automaticamente questi certificati almeno ogni 90 giorni. algoritmo di crittografia Hello utilizzato da SQL Data Warehouse è AES-256. Per una descrizione generale della funzionalità TDE, vedere [Transparent Data Encryption][Transparent Data Encryption].

È possibile crittografare il database tramite hello [portale Azure] [ Encryption with Portal] o [T-SQL][Encryption with TSQL].

## <a name="next-steps"></a>Passaggi successivi
Per informazioni dettagliate ed esempi sulla connessione tooyour SQL Data Warehouse con protocolli diversi, vedere [connessione Data Warehouse tooSQL][Connect tooSQL Data Warehouse].

<!--Image references-->

<!--Article references-->
[Connect tooSQL Data Warehouse]: ./sql-data-warehouse-connect-overview.md
[Encryption with Portal]: ./sql-data-warehouse-encryption-tde.md
[Encryption with TSQL]: ./sql-data-warehouse-encryption-tde-tsql.md
[Connecting tooSQL Data Warehouse By Using Azure Active Directory Authentication]: ./sql-data-warehouse-authentication.md

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
