---
title: regole del firewall di Database SQL aaaAzure | Documenti Microsoft
description: Informazioni su come tooconfigure un SQL database firewall con accesso toomanage di regole firewall a livello di server e a livello di database.
keywords: firewall del database
services: sql-database
documentationcenter: 
author: BYHAM
manager: jhubbard
editor: cgronlun
tags: 
ms.assetid: ac57f84c-35c3-4975-9903-241c8059011e
ms.service: sql-database
ms.custom: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 04/10/2017
ms.author: rickbyh
ms.openlocfilehash: 6a8cdf629d0d0e55421a5e9f9b894a21371be568
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sql-database-server-level-and-database-level-firewall-rules"></a>Regole firewall a livello di server e di database per il database SQL di Azure 

Il database SQL di Microsoft Azure fornisce un servizio di database relazionale per Azure e altre applicazioni basate su Internet. toohelp proteggere i dati, i firewall impediscono tutti i server di database di access tooyour finché non si specifica quali computer dispongono di autorizzazioni. firewall Hello concede accesso toodatabases in base a hello provenienti dall'indirizzo IP di ogni richiesta.

## <a name="overview"></a>Panoramica

Inizialmente, tutti i server di SQL Azure tooyour di accesso Transact-SQL è bloccato dal firewall hello. toobegin utilizzando il server SQL Azure, è necessario specificare uno o più regole firewall di livello server che consentono accesso tooyour Azure SQL server. Utilizzare toospecify di regole firewall hello quale indirizzo IP compreso tra hello Internet consentiti e indica se le applicazioni Azure possano tentare tooconnect tooyour Azure SQL server.

toojust accesso grant tooselectively uno dei database hello del server SQL Azure, è necessario creare una regola a livello di database per il database richiesto hello. Specificare un intervallo di indirizzi IP per la regola del firewall database hello che esula hello specificato nella regola del firewall a livello di server hello intervallo di indirizzi IP e verificare che l'indirizzo IP hello del client hello sia compreso nell'intervallo di hello specificato nella regola di hello a livello di database.

Hello di tentativi di connessione da Internet e Azure deve superare il firewall hello prima di poter raggiungere il server SQL di Azure o un Database SQL, come illustrato nel seguente diagramma hello:

   ![Diagramma che descrive la configurazione del firewall.][1]

* **Le regole del firewall a livello di server:** consentono tooaccess client l'intero server SQL Azure, vale a dire tutti i database all'interno di hello hello stesso server logico. Queste regole sono archiviate in hello **master** database. Regole del firewall a livello di server possono essere configurate tramite il portale di hello o utilizzando istruzioni Transact-SQL. le regole firewall di livello server toocreate con hello portale di Azure o PowerShell, è necessario essere proprietario della sottoscrizione hello o un collaboratore alla sottoscrizione. toocreate una regola del firewall a livello di server tramite Transact-SQL, è necessario connettere l'istanza del Database SQL toohello come account di accesso principale di hello a livello di server o amministratore di Azure Active Directory hello (il che significa che una regola del firewall a livello di server è necessario innanzitutto creare da un utente con autorizzazioni a livello di Azure).
* **Le regole del firewall a livello di database:** consentono client tooaccess determinati (sicuro) database all'interno di hello stesso server logico. È possibile creare queste regole per ogni database (inclusi hello **master** database0) e sono archiviate nei singoli database hello. Le regole del firewall a livello di database possono essere configurate solo tramite istruzioni Transact-SQL e solo dopo aver configurato hello primo firewall di livello server. Se si specifica un intervallo di indirizzi IP nella regola del firewall a livello di database hello è intervallo hello esterno specificato nella regola del firewall a livello di server hello, solo i client che dispongono di indirizzi IP nell'intervallo di hello a livello di database possono accedere a database hello. Per un database è possibile avere un massimo di 128 regole del firewall a livello di database. Le regole del firewall a livello di database per database master e utente possono essere create e gestite solo tramite Transact-SQL. Per ulteriori informazioni sulla configurazione delle regole del firewall a livello di database, vedere l'esempio hello più avanti in questo articolo e vedere [sp_set_database_firewall_rule (database SQL di Azure)](https://msdn.microsoft.com/library/dn270010.aspx).

**Consiglio:** Microsoft consiglia di utilizzare le regole del firewall a livello di database ogni volta che sicurezza tooenhance possibili e toomake del database più portabile. Utilizzare le regole del firewall a livello di server per gli amministratori e quando si dispone di molti database che hanno hello stessi requisiti di accesso e non si desidera ora toospend configurare singolarmente ogni database.

> [!Note]
> Per informazioni sui database portabile nel contesto di hello di continuità aziendale, vedere [requisiti di autenticazione per il ripristino di emergenza](sql-database-geo-replication-security-config.md).
>

### <a name="connecting-from-hello-internet"></a>Connessione da Internet hello

Quando un computer tenta di server di database tooyour tooconnect da hello Internet, firewall hello controlla innanzitutto hello provenienti dall'indirizzo IP della richiesta di hello rispetto alle regole firewall di livello database hello, per il database di hello che richiede la connessione hello:

* Se l'indirizzo IP hello della richiesta di hello è in uno degli intervalli di hello specificati nelle regole del firewall a livello di database hello, connessione hello viene concessa toohello Database SQL che contiene la regola di hello.
* Se l'indirizzo IP hello della richiesta di hello non è in uno degli intervalli di hello specificati nella regola del firewall a livello di database hello, vengono controllate le regole firewall di livello server hello. Se l'indirizzo IP hello della richiesta di hello è in uno degli intervalli di hello specificati nelle regole del firewall a livello di server hello, connessione hello viene concessa. Le regole del firewall a livello di server applicano tooall database SQL server SQL Azure hello.  
* Se l'indirizzo IP hello della richiesta di hello non è presente all'interno di intervalli hello specificata in una delle hello a livello di database o delle regole del firewall a livello di server, hello richiesta di connessione ha esito negativo.

> [!NOTE]
> tooaccess Database SQL di Azure dal computer locale, verificare che il firewall di hello in rete e nel computer locale consenta la comunicazione in uscita sulla porta TCP 1433.
> 

### <a name="connecting-from-azure"></a>Connessione da Azure
è necessario abilitare le applicazioni tooallow da Azure tooconnect tooyour server SQL di Azure, le connessioni di Azure. Quando un'applicazione da Azure tenta di server di database tooyour tooconnect, firewall hello verifica che le connessioni di Azure sono consentite. Un'impostazione con iniziale e finale uguale too0.0.0.0 di indirizzo del firewall indica che queste connessioni sono consentite. Se non è consentito il tentativo di connessione hello, hello richiesta non raggiungerà il server di Database SQL di Azure hello.

> [!IMPORTANT]
> Questa opzione Configura hello firewall tooallow tutte le connessioni dalle connessioni tra cui Azure dalle sottoscrizioni hello di altri clienti. Quando questa opzione, assicurarsi che l'account di accesso e autorizzazioni utente limitare tooonly accesso agli utenti autorizzati.
> 

## <a name="creating-and-managing-firewall-rules"></a>Creazione e gestione di regole del firewall
prima impostazione del firewall di livello server Hello può essere creata usando hello [portale di Azure](https://portal.azure.com/) o a livello di programmazione utilizzando [Azure PowerShell](https://msdn.microsoft.com/library/azure/dn546724.aspx), [CLI di Azure](/cli/azure/sql/server/firewall-rule#create), o hello [API REST](https://msdn.microsoft.com/library/azure/dn505712.aspx). Le regole del firewall a livello di server successive possono essere create e gestite utilizzando questi metodi e tramite Transact-SQL. 

> [!IMPORTANT]
> Le regole del firewall a livello di database possono essere create e gestite solo con Transact-SQL. 
>

prestazioni tooimprove, il firewall di livello server regole temporaneamente vengono memorizzati nella cache a livello di database hello. cache di hello toorefresh, vedere [DBCC FLUSHAUTHCACHE](https://msdn.microsoft.com/library/mt627793.aspx). 

> [!TIP]
> È possibile utilizzare [SQL Database Auditing](sql-database-auditing.md) tooaudit le modifiche alle firewall a livello di server e a livello di database.
>

### <a name="azure-portal"></a>Portale di Azure

una regola del firewall a livello di server nel portale di Azure hello tooset, è possibile proseguire toohello pagina di panoramica per la pagina di panoramica hello o database SQL di Azure per il server logico di Database di Azure.

> [!TIP]
> Per un'esercitazione, vedere [crea un database utilizzando il portale di Azure di hello](sql-database-get-started-portal.md).
>

**Dalla pagina di Panoramica del database**

1. Fare clic su una regola del firewall a livello di server dalla pagina di panoramica database hello, tooset **impostare firewall del server** sulla barra degli strumenti hello, come illustrato nella seguente immagine hello: hello **le impostazioni del Firewall** pagina per hello SQL Verrà visualizzata la finestra di server di database.

      ![Regola del firewall del server](./media/sql-database-get-started-portal/server-firewall-rule.png) 

2. Fare clic su **Aggiungi indirizzo IP del client** sull'indirizzo IP del computer hello hello barra degli strumenti tooadd hello attualmente in uso e quindi fare clic su **salvare**. Una regola del firewall a livello di server viene creata per l'indirizzo IP corrente.

      ![Impostare la regola del firewall del server](./media/sql-database-get-started-portal/server-firewall-rule-set.png) 

**Dalla pagina della panoramica del server**

pagina di panoramica per il server viene visualizzata, che mostra hello completamente Hello completo del server (ad esempio **mynewserver20170403.database.windows.net**) e offre opzioni per un'ulteriore configurazione.

1. Fare clic su una regola a livello di server dalla pagina di panoramica di server, tooset **Firewall** nel menu a sinistra di hello in impostazioni, come illustrato nella seguente immagine hello: 

     ![panoramica del server logico](./media/sql-database-migrate-your-sql-server-database/logical-server-overview.png)

2. Fare clic su **Aggiungi indirizzo IP del client** sull'indirizzo IP del computer hello hello barra degli strumenti tooadd hello attualmente in uso e quindi fare clic su **salvare**. Una regola del firewall a livello di server viene creata per l'indirizzo IP corrente.

     ![Impostare la regola del firewall del server](./media/sql-database-migrate-your-sql-server-database/server-firewall-rule-set.png)

### <a name="transact-sql"></a>Transact-SQL
| Vista del catalogo o una Stored Procedure | Level | Descrizione |
| --- | --- | --- |
| [sys.firewall_rules](https://msdn.microsoft.com/library/dn269980.aspx) |Server |Visualizza le regole firewall di livello server correnti hello |
| [sp_set_firewall_rule](https://msdn.microsoft.com/library/dn270017.aspx) |Server |Crea o aggiorna regole del firewall a livello di server |
| [sp_delete_firewall_rule](https://msdn.microsoft.com/library/dn270024.aspx) |Server |Rimuove regole del firewall a livello di server |
| [sys.database_firewall_rules](https://msdn.microsoft.com/library/dn269982.aspx) |Database |Visualizza le regole firewall di livello database correnti hello |
| [sp_set_database_firewall_rule](https://msdn.microsoft.com/library/dn270010.aspx) |Database |Crea o aggiorna regole firewall di livello database hello |
| [sp_delete_database_firewall_rule](https://msdn.microsoft.com/library/dn270030.aspx) |Database |Rimuove le regole del firewall a livello di database |


Hello negli esempi seguenti rivedere le regole esistenti hello, abilitare un intervallo di indirizzi IP nel server di hello Contoso e consente di eliminare una regola del firewall:
   
```sql
SELECT * FROM sys.firewall_rules ORDER BY name;
```
  
Successivamente, aggiungere una regola del firewall.
   
```sql
EXECUTE sp_set_firewall_rule @name = N'ContosoFirewallRule',
   @start_ip_address = '192.168.1.1', @end_ip_address = '192.168.1.10'
```

toodelete una regola del firewall a livello di server, eseguire la procedura di hello sp_delete_firewall_rule archiviati. Hello esempio Elimina regola hello denominata ContosoFirewallRule:
   
```sql
EXECUTE sp_delete_firewall_rule @name = N'ContosoFirewallRule'
```   

### <a name="azure-powershell"></a>Azure PowerShell
| Cmdlet | Level | Descrizione |
| --- | --- | --- |
| [Get-AzureSqlDatabaseServerFirewallRule](https://msdn.microsoft.com/library/azure/dn546731.aspx) |Server |Restituisce le regole firewall di livello server correnti hello |
| [New-AzureSqlDatabaseServerFirewallRule](https://msdn.microsoft.com/library/azure/dn546724.aspx) |Server |Crea una nuova regola del firewall a livello di server |
| [Set-AzureSqlDatabaseServerFirewallRule](https://msdn.microsoft.com/library/azure/dn546739.aspx) |Server |Aggiorna proprietà hello di una regola firewall di livello server esistente |
| [Remove-AzureSqlDatabaseServerFirewallRule](https://msdn.microsoft.com/library/azure/dn546727.aspx) |Server |Rimuove regole del firewall a livello di server |


Hello di esempio seguente imposta una regola del firewall a livello di server con PowerShell:

```powershell
New-AzureRmSqlServerFirewallRule -ResourceGroupName "myResourceGroup" `
    -ServerName $servername `
    -FirewallRuleName "AllowSome" -StartIpAddress "0.0.0.0" -EndIpAddress "0.0.0.0"
```

> [!TIP]
> Per esempi di PowerShell nel contesto di hello di una Guida introduttiva, vedere [creare DB - PowerShell](sql-database-get-started-powershell.md) e [creare un singolo database e configurare una regola del firewall tramite PowerShell](scripts/sql-database-create-and-configure-database-powershell.md)
>

### <a name="azure-cli"></a>Interfaccia della riga di comando di Azure
| Cmdlet | Level | Descrizione |
| --- | --- | --- |
| [az sql server firewall create](/cli/azure/sql/server/firewall-rule#create) | Crea un tooall di accesso tooallow regola firewall SQL database nel server di hello dall'intervallo di indirizzi IP hello immesso.|
| [az sql server firewall delete](/cli/azure/sql/server/firewall-rule#delete)| Elimina una regola del firewall.|
| [az sql server firewall list](/cli/azure/sql/server/firewall-rule#list)| Elenca le regole del firewall hello.|
| [az sql server firewall rule show](/cli/azure/sql/server/firewall-rule#show)| Mostra i dettagli di hello di una regola del firewall.|
| [ax sql server firewall rule update](/cli/azure/sql/server/firewall-rule#update)| Aggiorna una regola del firewall.

Hello di esempio seguente imposta una regola del firewall a livello di server utilizzando hello CLI di Azure: 

```azurecli-interactive
az sql server firewall-rule create --resource-group myResourceGroup --server $servername \
    -n AllowYourIp --start-ip-address 0.0.0.0 --end-ip-address 0.0.0.0
```

> [!TIP]
> Per un esempio di CLI di Azure nel contesto di hello di una Guida introduttiva, vedere [creare DDB - CLI di Azure](sql-database-get-started-cli.md) e [creare un singolo database e configurare una regola del firewall utilizzando hello CLI di Azure](scripts/sql-database-create-and-configure-database-cli.md)
>

### <a name="rest-api"></a>API REST
| API | Level | Descrizione |
| --- | --- | --- |
| [Elencare le regole del firewall](https://msdn.microsoft.com/library/azure/dn505715.aspx) |Server |Visualizza le regole firewall di livello server correnti hello |
| [Creare la regola del firewall](https://msdn.microsoft.com/library/azure/dn505712.aspx) |Server |Crea o aggiorna regole del firewall a livello di server |
| [Impostare la regola del firewall](https://msdn.microsoft.com/library/azure/dn505707.aspx) |Server |Aggiorna proprietà hello di una regola firewall di livello server esistente |
| [Eliminare la regola del firewall](https://msdn.microsoft.com/library/azure/dn505706.aspx) |Server |Rimuove regole del firewall a livello di server |

## <a name="server-level-firewall-rule-versus-a-database-level-firewall-rule"></a>Regola del firewall a livello di server contro una regola del firewall a livello di database
D: Gli utenti di un database devono essere completamente isolati da un altro database?   
  In caso affermativo, concedere l'accesso tramite le regole del firewall a livello di database. Questo evita utilizzando le regole firewall di livello server, che consente l'accesso attraverso il firewall hello tooall database, riducendo la profondità hello di difese.   
 
D: Gli utenti in corrispondenza dell'indirizzo IP hello necessario accedere tooall database?   
  Utilizzare firewall di livello server regole tooreduce hello numero di volte in cui che è necessario configurare le regole del firewall.   

D: Persona hello o configurazione di regole firewall hello solo team dispone di accesso tramite hello portale di Azure, PowerShell o API REST di hello?   
  È necessario usare le regole del firewall a livello di server. Le regole del firewall a livello di database possono essere configurate solo con Transact-SQL.  

D: Non è persona hello o configurazione di regole firewall hello team consentito dalla presenza di alto livello dell'autorizzazione a livello di database hello?   
  Usare le regole del firewall a livello di server. Per configurare regole del firewall a livello di database utilizzando Transact-SQL, è necessario almeno `CONTROL DATABASE` autorizzazione a livello di database hello.  

D: È la persona hello o team configurazione o il controllo delle regole del firewall hello, la gestione centralizzata delle regole del firewall per molti (ad esempio 100s) di database?   
  Questa selezione dipende dalle esigenze e degli ambienti. Le regole del firewall a livello di server potrebbero essere più facile tooconfigure, ma lo scripting è possibile configurare le regole in hello a livello di database. E anche se si utilizzano le regole del firewall a livello di server, potrebbe essere necessario regole firewall di database tooaudit hello toosee se gli utenti con `CONTROL` autorizzazione sul database hello hanno creato le regole del firewall a livello di database.   

D: È possibile usare un insieme di regole del firewall a livello di server e di database?   
  Sì. Alcuni utenti, ad esempio gli amministratori, potrebbero aver bisogno di regole del firewall a livello di server. Altri utenti, ad esempio gli utenti di un'applicazione di database, potrebbero aver bisogno di regole del firewall a livello di database.   

## <a name="troubleshooting-hello-database-firewall"></a>Risoluzione dei problemi di firewall del database hello
Considerare i seguenti punti di accesso toohello servizio Database SQL di Microsoft Azure non comportarsi come previsto hello:

* **Configurazione del firewall locale:** prima che il computer possa accedere a Database SQL di Azure, potrebbe essere necessario toocreate un'eccezione del firewall nel computer in uso per la porta TCP 1433. Se si apportano le connessioni all'interno dei confini di hello cloud di Azure, è possibile tooopen altre porte. Per ulteriori informazioni, vedere hello **Database SQL: all'esterno di Visual Studio all'interno di** sezione [porte 1433 per il Database di SQL e ADO.NET 4.5](sql-database-develop-direct-route-ports-adonet-v12.md).
* **La network address (NAT):** tooNAT scadenza, indirizzo IP di hello utilizzato per il tooAzure tooconnect computer Database SQL potrebbero essere diverso da indirizzo IP hello indicato nelle impostazioni di configurazione IP del computer. indirizzo IP di hello tooview è il computer utilizzando tooconnect tooAzure, accedi al portale toohello e passare toohello **configura** scheda server hello che ospita il database. In hello **indirizzi IP consentiti** sezione hello **indirizzo IP Client corrente** viene visualizzato. Fare clic su **Aggiungi** toohello **indirizzi IP consentiti** tooallow server hello tooaccess computer.
* **Elenco Consenti toohello le modifiche non sono state applicate ancora:** potrebbero essere presenti in quanto un ritardo di cinque minuti per la modifica di effetto di tootake configurazione di firewall di toohello Database SQL di Azure.
* **account di accesso Hello non è autorizzato o è stata utilizzata una password errata:** se un account di accesso non dispone di autorizzazioni nel server di Database SQL di Azure hello o password hello utilizzata è errata, server di Database SQL di Azure toohello connessione hello è negato. Creazione di un'impostazione del firewall fornisce solo i client con un'opportunità tooattempt connessione server tooyour; ogni client dovrà fornire le credenziali di sicurezza necessarie hello. Per ulteriori informazioni sulla preparazione degli account di accesso, vedere Gestione di database, account di accesso e utenti nel database SQL di Azure.
* **Indirizzo IP dinamico:** se si dispone di una connessione Internet con impostazione di indirizzi IP dinamici e si verificano problemi di comunicazione attraverso il firewall hello, è possibile provare una delle seguenti soluzioni hello:
  
  * Richiedere il Provider di servizi Internet (ISP) per l'intervallo di indirizzi IP hello assegnato tooyour i computer client che server di Database SQL di Azure hello di accesso e quindi aggiungere l'intervallo di indirizzi IP hello come una regola del firewall.
  * Ottenere indirizzi IP statici per i computer client e quindi aggiungere gli indirizzi IP hello come regole del firewall.

## <a name="next-steps"></a>Passaggi successivi

- Per una Guida introduttiva alla creazione di un database e di una regola del firewall a livello di server, vedere [Creare un database SQL di Azure nel portale di Azure](sql-database-get-started-portal.md).
- Per informazioni sulla connessione database di SQL Azure tooan da applicazioni di terze parti o open source di, vedere [tooSQL Database degli esempi di codice di avvio rapido Client](https://msdn.microsoft.com/library/azure/ee336282.aspx).
- Per informazioni su altre porte che potrebbe essere necessario tooopen, vedere hello **Database SQL: all'esterno di Visual Studio all'interno di** sezione [porte 1433 per il Database di SQL e ADO.NET 4.5](sql-database-develop-direct-route-ports-adonet-v12.md)
- Per una panoramica della sicurezza del Database SQL di Azure vedere [Protezione del Database SQL](sql-database-security-overview.md)

<!--Image references-->
[1]: ./media/sql-database-firewall-configure/sqldb-firewall-1.png
