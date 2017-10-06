---
title: aaaAzure SQL account di accesso e utenti | Documenti Microsoft
description: "Informazioni sulla gestione della sicurezza del Database SQL, in particolare come toomanage accesso e l'account di accesso di sicurezza del database tramite l'account dell'entità a livello di server di hello."
keywords: sicurezza del database sql, gestione della sicurezza del database, sicurezza degli account di accesso, sicurezza del database, accesso al database
services: sql-database
documentationcenter: 
author: BYHAM
manager: jhubbard
editor: 
tags: 
ms.assetid: 0a65a93f-d5dc-424b-a774-7ed62d996f8c
ms.service: sql-database
ms.custom: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 01/23/2017
ms.author: rickbyh
ms.openlocfilehash: dff889b9fed09146a10008c0d11ca9e71d91df5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="controlling-and-granting-database-access"></a>Controllo e concessione dell'accesso al database

Dopo aver configurate le regole del firewall, come uno degli account di amministratore di hello, come proprietario del database hello o come utente del database nel database di hello la connessione alle persone tooa Database SQL.  

>  [!NOTE]  
>  Questo argomento si applica tooAzure SQL server e database tooboth Database SQL e SQL Data Warehouse che vengono creati sul server SQL Azure hello. Per semplicità, Database SQL viene utilizzato quando si fa riferimento tooboth Database SQL e SQL Data Warehouse. 
>

> [!TIP]
> Per un'esercitazione, vedere [Proteggere il database SQL di Azure](sql-database-security-tutorial.md).
>


## <a name="unrestricted-administrative-accounts"></a>Account amministrativi senza restrizioni
Sono disponibili due account amministrativi, **Amministratore del server** e **Amministratore di Active Directory**, che agiscono come amministratori. tooidentify questi account di amministratore per SQL server, aprire hello portale di Azure e passare la proprietà toohello di SQL Server.

![Amministratori del server SQL](./media/sql-database-manage-logins/sql-admins.png)

- **Amministratore del server**   
Quando si crea un server SQL di Azure è necessario designare un **accesso amministratore server**. SQL server crea l'account come account di accesso nel database master hello. Tale account, che effettua la connessione con l'autenticazione di SQL Server (nome utente e password), Può esistere un solo account di questo tipo.   
- **Amministratore di Azure Active Directory**   
È possibile configurare come amministratore anche un account singolo o di gruppo di sicurezza di Azure Active Directory. È facoltativo tooconfigure amministratore AD Azure, ma un amministratore di Azure AD deve essere configurato se si desidera che gli account di Azure AD toouse, tooSQL tooconnect Database. Per ulteriori informazioni sulla configurazione di accesso di Azure Active Directory, vedere [tooSQL connessione Database o Data Warehouse da usando Azure Active Directory l'autenticazione di SQL](sql-database-aad-authentication.md) e [SSMS supporto per l'autenticazione a più fattori di Azure AD con SQL Database e SQL Data Warehouse](sql-database-ssms-mfa-authentication.md).
 

Hello **amministratore del Server** e **amministrazione di Azure AD** account ha hello seguenti caratteristiche:
- Si tratta di hello solo gli account in grado di connettersi automaticamente tooany Database di SQL Server hello. (tooconnect tooa i database utente, gli altri account deve essere proprietario di hello di hello del database o avere un account utente nel database utente hello.)
- Questi account immettere i database utente come hello `dbo` utente e disporre di tutte le autorizzazioni di hello nei database utente hello. (il proprietario di hello di un database utente immessi anche database hello come hello `dbo` utente.) 
- Questi account non si immette hello `master` database come hello `dbo` utente che dispone di autorizzazioni limitate nel database master. 
- Questi account non sono membri di hello SQL Server standard `sysadmin` ruolo predefinito del server, che non è disponibile nel database SQL.  
- Questi account possono creare, modificare ed eliminare database, account di accesso, utenti nel database master e regole firewall a livello di server.
- Questi account possono aggiungere e rimuovere membri toohello `dbmanager` e `loginmanager` ruoli.
- Questi account possono visualizzare hello `sys.sql_logins` tabella di sistema.

### <a name="configuring-hello-firewall"></a>Configurazione firewall hello
Quando il firewall di livello server hello è configurato per un singolo indirizzo IP o l'intervallo, hello **amministratore del server SQL** hello e **amministratore di Azure Active Directory** possono connettersi al database master toohello e hello tutti database utente. firewall di livello server Hello iniziale può essere configurato tramite hello [portale di Azure](sql-database-get-started-portal.md)tramite [PowerShell](sql-database-get-started-powershell.md) o tramite hello [API REST](https://msdn.microsoft.com/library/azure/dn505712.aspx). Dopo che è stata stabilita una connessione, è possibile configurare anche regole aggiuntive del firewall a livello di server con l'istruzione [Transact-SQL](sql-database-configure-firewall-settings.md).

### <a name="administrator-access-path"></a>Percorso di accesso degli amministratori
Quando il firewall di livello server hello sia configurato correttamente, hello **amministratore del server SQL** hello e **amministratore di Azure Active Directory** possono connettersi utilizzando gli strumenti client, ad esempio SQL Server Management Studio o SQL Server Data Tools. Strumenti più recenti di hello forniscono tutte le funzionalità di hello. Hello diagramma seguente mostra una configurazione tipica per hello due account di amministratore.

![Percorso di accesso degli amministratori](./media/sql-database-manage-logins/1sql-db-administrator-access.png)

Quando si utilizza una porta aperta nel firewall di livello server hello, gli amministratori possono connettersi tooany Database SQL.

### <a name="connecting-tooa-database-by-using-sql-server-management-studio"></a>Connessione di database tooa tramite SQL Server Management Studio
Per una procedura dettagliata Creazione di un server, un database, le regole del firewall a livello di server e si utilizza SQL Server Management Studio tooquery un database, vedere [iniziare con il server di Database SQL di Azure, database e le regole del firewall utilizzando hello portale di Azure SQL Server Management Studio e](sql-database-get-started-portal.md).

> [!IMPORTANT]
> È consigliabile utilizzare sempre hello versione più recente di Management Studio tooremain sincronizzati con gli aggiornamenti tooMicrosoft Azure e il Database SQL. [Aggiornare SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx).


## <a name="additional-server-level-administrative-roles"></a>Ruoli amministrativi aggiuntivi a livello di server
Inoltre toohello a livello di server ruoli amministrativi illustrato in precedenza, il Database SQL fornisce due ruoli amministrativi limitati gli account utente di hello database master toowhich possono essere aggiunti a cui concedere le autorizzazioni tooeither creare database o gestire account di accesso.

### <a name="database-creators"></a>Autori di database
Uno di questi ruoli amministrativi è hello **dbmanager** ruolo. I membri di questo ruolo possono creare nuovi database. toouse questo ruolo, si crea un utente in hello `master` database e quindi aggiungere hello utente toohello **dbmanager** ruolo del database. toocreate un database, l'utente hello deve essere un utente in base a un account di accesso di SQL Server nel database master hello o contenuto utente del database in base a un utente di Azure Active Directory.

1. Utilizzando un account amministratore, la connessione di database master toohello.
2. Passaggio facoltativo: creare un account di accesso autenticazione di SQL Server, tramite hello [CREATE LOGIN](https://msdn.microsoft.com/library/ms189751.aspx) istruzione. Istruzione di esempio:
   
   ```
   CREATE LOGIN Mary WITH PASSWORD = '<strong_password>';
   ```
   
   > [!NOTE]
   > Quando si crea un account di accesso o un utente di database indipendente, usare una password complessa. Per ulteriori informazioni, vedere [Password complesse](https://msdn.microsoft.com/library/ms161962.aspx).
    
   prestazioni tooimprove, gli account di accesso (entità a livello di server) sono temporaneamente nella cache a livello di database hello. cache di autenticazione hello toorefresh, vedere [DBCC FLUSHAUTHCACHE](https://msdn.microsoft.com/library/mt627793.aspx).

3. Nel database master hello, creare un utente tramite hello [CREATE USER](https://msdn.microsoft.com/library/ms173463.aspx) istruzione. Hello utente può essere un Azure Active Directory inclusa l'autenticazione utente del database (se è stato configurato l'ambiente per l'autenticazione di Azure AD), o un utente del database di SQL Server authentication contenuti o un utente di autenticazione di SQL Server in base a un database SQL Account di accesso di autenticazione server (creato nel passaggio precedente hello). Istruzioni di esempio:
   
   ```
   CREATE USER [mike@contoso.com] FROM EXTERNAL PROVIDER;
   CREATE USER Tran WITH PASSWORD = '<strong_password>';
   CREATE USER Mary FROM LOGIN Mary; 
   ```

4. Aggiungere il nuovo utente hello, toohello **dbmanager** ruolo del database tramite hello [ALTER ROLE](https://msdn.microsoft.com/library/ms189775.aspx) istruzione. Istruzioni di esempio:
   
   ```
   ALTER ROLE dbmanager ADD MEMBER Mary; 
   ALTER ROLE dbmanager ADD MEMBER [mike@contoso.com];
   ```
   
   > [!NOTE]
   > dbmanager Hello è un ruolo del database nel database master, pertanto è possibile aggiungere solo un ruolo del database utente toohello dbmanager. È possibile aggiungere un ruolo toodatabase a livello di accesso a livello di server.
    
5. Se necessario, configurare un firewall regola tooallow hello nuovo utente tooconnect. (nuovo utente hello potrebbe essere coperta da una regola firewall esistente).

Ora utente hello può connettersi a database master toohello e possa creare nuovi database. account Hello creazione hello database diventa il proprietario di hello del database di hello.

### <a name="login-managers"></a>Gestione degli account di accesso
Hello altri ruoli amministrativi sono ruolo di gestione di account di accesso hello. Membri di questo ruolo possono creare nuovi account di accesso nel database master hello. Se si desidera, è possibile completare hello stessi passaggi (creare un account di accesso e un utente e aggiungere un utente toohello **loginmanager** ruolo) tooenable un utente toocreate nuovi account di accesso nel database master hello. Gli account di accesso non sono in genere necessari come livello di database Microsoft consiglia di utilizzare gli utenti di database indipendente, che esegue l'autenticazione hello anziché gli utenti con account di accesso. Per altre informazioni, vedere [Utenti di database indipendente: rendere portabile un database](https://msdn.microsoft.com/library/ff929188.aspx).

## <a name="non-administrator-users"></a>Utenti non amministratori
In genere, gli account senza privilegi di amministratore non è necessario accedere toohello database master. Creare utenti del database indipendente a livello di database hello utilizzando hello [CREATE USER (Transact-SQL)](https://msdn.microsoft.com/library/ms173463.aspx) istruzione. Hello utente può essere un Azure Active Directory inclusa l'autenticazione utente del database (se è stato configurato l'ambiente per l'autenticazione di Azure AD), o un utente del database di SQL Server authentication contenuti o un utente di autenticazione di SQL Server in base a un database SQL Account di accesso di autenticazione server (creato nel passaggio precedente hello). Per altre informazioni, vedere [Utenti di database indipendente: rendere portabile un database](https://msdn.microsoft.com/library/ff929188.aspx). 

toocreate utenti, la connessione a database toohello ed eseguire istruzioni toohello simile seguono esempi:

```
CREATE USER Mary FROM LOGIN Mary; 
CREATE USER [mike@contoso.com] FROM EXTERNAL PROVIDER;
```

Inizialmente, solo uno di amministratori di hello o il proprietario di hello di hello database può creare utenti. tooauthorize utenti aggiuntivi toocreate nuovi utenti, concedere tale hello utente selezionato `ALTER ANY USER` autorizzazione, tramite un'istruzione, ad esempio:

```
GRANT ALTER ANY USER tooMary;
```

un membro di hello renderli toogive controllo completo di altri utenti del database di hello, **db_owner** ruolo predefinito del database utilizzando hello `ALTER ROLE` istruzione.

> [!NOTE]
> Hello più comuni motivo toocreate gli utenti del database con account di accesso, è quando sono presenti utenti di autenticazione di SQL Server che è necessitano accedere a database toomultiple. Gli utenti con account di accesso sono account di accesso collegati toohello e solo una password che viene mantenuta per l'accesso. Gli utenti di database indipendente in singoli database sono ognuno una singola entità che gestisce una propria password. Questo può creare confusione se gli utenti di database indipendente non usano password identiche.

### <a name="configuring-hello-database-level-firewall"></a>Configurazione dei firewall di livello database hello
Come procedura consigliata, gli utenti non amministratori dovrebbero possono accedere solo tramite i database di toohello firewall hello che usano. Invece di autorizzare i IP firewall gli indirizzi tramite hello a livello di server e concedere loro accesso tooall database, utilizzare hello [sp_set_database_firewall_rule](https://msdn.microsoft.com/library/dn270010.aspx) firewall di livello database hello tooconfigure di istruzione. firewall di livello database Hello non possono essere configurate utilizzando il portale di hello.

### <a name="non-administrator-access-path"></a>Percorso di accesso degli utenti non amministratori
Quando il firewall di livello database hello sia configurato correttamente, gli utenti del database hello possono connettersi utilizzando gli strumenti client, ad esempio SQL Server Management Studio o SQL Server Data Tools. Strumenti più recenti di hello forniscono tutte le funzionalità di hello. Hello seguente diagramma viene mostrato un percorso di accesso senza privilegi di amministratore tipico.

![Percorso di accesso degli utenti non amministratori](./media/sql-database-manage-logins/2sql-db-nonadmin-access.png)

## <a name="groups-and-roles"></a>Gruppi e ruoli
Gestione efficiente di accesso utilizza le autorizzazioni assegnate toogroups e ai ruoli anziché a singoli utenti. 

- Quando si usa l'autenticazione di Azure Active Directory, inserire gli utenti di Azure Active Directory in un gruppo di Azure Active Directory. Creare un utente di database indipendente per il gruppo di hello. Inserire uno o più utenti di database in un [ruolo del database](https://msdn.microsoft.com/library/ms189121) e quindi assegnare [autorizzazioni](https://msdn.microsoft.com/library/ms191291.aspx) toohello ruolo del database.

- Quando si utilizza l'autenticazione di SQL Server, è possibile creare utenti del database indipendente in database hello. Inserire uno o più utenti di database in un [ruolo del database](https://msdn.microsoft.com/library/ms189121) e quindi assegnare [autorizzazioni](https://msdn.microsoft.com/library/ms191291.aspx) toohello ruolo del database.

ruoli predefiniti del database Hello possono essere ad esempio i ruoli predefiniti hello **db_owner**, **db_ddladmin**, **db_datawriter**, **db_datareader**, **db_denydatawriter**, e **db_denydatareader**. **db_owner** è comunemente utilizzati toogrant autorizzazioni complete tooonly alcuni utenti. Hello altri ruoli predefiniti del database sono utili per ottenere rapidamente un database semplice in fase di sviluppo, ma non sono consigliati per la maggior parte dei database di produzione. Ad esempio, hello **db_datareader** ruolo predefinito del database concede l'accesso in lettura tooevery tabella nel database di hello, che è in genere è più strettamente necessaria. È preferibile hello toouse [CREATE ROLE](https://msdn.microsoft.com/library/ms187936.aspx) toocreate istruzione personalizzati definiti dall'utente i ruoli del database e concedere attentamente ogni hello ruolo almeno delle autorizzazioni necessarie per le esigenze di business hello. Quando un utente è un membro di più ruoli, aggregano le autorizzazioni di hello tutti.

## <a name="permissions"></a>Autorizzazioni
Nel database SQL possono essere concesse o negate singolarmente oltre 100 autorizzazioni. Molte di queste autorizzazioni sono annidate. Ad esempio, hello `UPDATE` l'autorizzazione per uno schema include hello `UPDATE` l'autorizzazione per ogni tabella all'interno di tale schema. Come la maggior parte dei sistemi di autorizzazione, hello un'autorizzazione negano un'istruzione grant. A causa di natura hello nidificata e il numero di hello di autorizzazioni, può richiedere attenzione Studio toodesign un tooproperly di sistema di autorizzazioni appropriate di proteggere il database. Iniziare con elenco hello di autorizzazioni [autorizzazioni (motore di Database)](https://msdn.microsoft.com/library/ms191291.aspx) ed esaminare hello [grafica del poster di dimensioni](http://go.microsoft.com/fwlink/?LinkId=229142) di autorizzazioni hello.


### <a name="considerations-and-restrictions"></a>Considerazioni e restrizioni
Quando si gestiscono gli account di accesso e gli utenti di Database SQL, considerare l'esempio hello:

* È necessario essere connesso toohello **master** del database durante l'esecuzione di hello `CREATE/ALTER/DROP DATABASE` istruzioni.   
* database utente corrispondente toohello Hello **amministratore del Server** account di accesso non può essere modificato o eliminato. 
* In lingua inglese Stati Uniti è lingua predefinita per hello di hello **amministratore del Server** account di accesso.
* Hello solo gli amministratori (**amministratore del Server** account di accesso o l'amministratore di Azure AD) e i membri di hello di hello **dbmanager** ruolo del database in hello **master** dispone di database hello tooexecute autorizzazione `CREATE DATABASE` e `DROP DATABASE` istruzioni.
* È necessario essere connessi toohello database master durante l'esecuzione di hello `CREATE/ALTER/DROP LOGIN` istruzioni. È tuttavia sconsigliato l'uso di account di accesso. Usare invece gli utenti del database indipendente.
* tooconnect tooa i database utente, è necessario fornire il nome di hello del database di hello nella stringa di connessione hello.
* Hello solo a livello di server principale hello e accesso membri di hello **loginmanager** ruolo del database in hello **master** database hanno hello tooexecute autorizzazione `CREATE LOGIN`, `ALTER LOGIN`, e `DROP LOGIN` istruzioni.
* Quando si esegue hello `CREATE/ALTER/DROP LOGIN` e `CREATE/ALTER/DROP DATABASE` istruzioni in un'applicazione ADO.NET, utilizzando i comandi con parametri non è consentito. Per ulteriori informazioni, vedere [Comandi e parametri](https://msdn.microsoft.com/library/ms254953.aspx).
* Quando si esegue hello `CREATE/ALTER/DROP DATABASE` e `CREATE/ALTER/DROP LOGIN` le istruzioni, ognuna di queste istruzioni deve essere hello solo l'istruzione in un batch Transact-SQL. In caso contrario, si verifica un errore. Ad esempio, hello che Transact-SQL seguente controlla l'esistenza del database hello. Se è presente, un `DROP DATABASE` database hello tooremove viene chiamata l'istruzione. Poiché hello `DROP DATABASE` istruzione non è di tipo hello unica istruzione nel batch di hello, eseguire hello seguente istruzione Transact-SQL genera un errore.

  ```
  IF EXISTS (SELECT [name]
           FROM   [sys].[databases]
           WHERE  [name] = N'database_name')
  DROP DATABASE [database_name];
  GO
  ```

* Quando si esegue hello `CREATE USER` istruzione con hello `FOR/FROM LOGIN` opzione, deve essere hello solo l'istruzione in un batch Transact-SQL.
* Quando si esegue hello `ALTER USER` istruzione con hello `WITH LOGIN` opzione, deve essere hello solo l'istruzione in un batch Transact-SQL.
* troppo`CREATE/ALTER/DROP` un utente richiede hello `ALTER ANY USER` autorizzazione sul database hello.
* Se il proprietario di hello di un ruolo del database tenta tooadd o rimuovere un altro tooor utente di database dal ruolo del database, può verificarsi il seguente errore hello: **utente o il ruolo 'Name' non esiste nel database.** Questo errore si verifica perché hello utente non è proprietario di toohello visibile. tooresolve questo problema, concedere hello ruolo proprietario hello `VIEW DEFINITION` autorizzazione utente hello. 


## <a name="next-steps"></a>Passaggi successivi

- toolearn più sulle regole del firewall, vedere [Firewall di Database SQL di Azure](sql-database-firewall-configure.md).
- Per una panoramica di tutte le funzionalità di sicurezza hello Database SQL, vedere [Cenni preliminari sulla sicurezza SQL](sql-database-security-overview.md).
- Per un'esercitazione, vedere [Proteggere il database SQL di Azure](sql-database-security-tutorial.md).
- Per informazioni sulle viste e sulle stored procedure, vedere [Creazione di viste e stored procedure](https://msdn.microsoft.com/library/ms365311.aspx)
- Per informazioni sulla concessione dell'oggetto di database di access tooa, vedere [tooa concessione dell'accesso oggetto di Database](https://msdn.microsoft.com/library/ms365327.aspx)
