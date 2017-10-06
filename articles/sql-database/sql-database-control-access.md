---
title: aaaGranting accesso tooAzure Database SQL | Documenti Microsoft
description: Informazioni sulla concessione dell'accesso tooMicrosoft Database SQL di Azure.
services: sql-database
documentationcenter: 
author: BYHAM
manager: jhubbard
editor: 
tags: 
ms.assetid: 8e71b04c-bc38-4153-8f83-f2b14faa31d9
ms.service: sql-database
ms.custom: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 02/06/2017
ms.author: rickbyh
ms.openlocfilehash: 4c32fafa7e98b731ff2f9bf4666da7e4a3145286
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sql-database-access-control"></a>Controllo dell'accesso al database SQL di Azure
sicurezza tooprovide, Database SQL controlla l'accesso con la limitazione di connettività utilizzando un indirizzo IP, i meccanismi di autenticazione che richiede agli utenti tooprove regole del firewall, identità e meccanismi di autorizzazione, limitando gli utenti toospecific azioni e i dati. 

> [!IMPORTANT]
> Per una panoramica delle funzionalità di sicurezza di hello Database SQL, vedere [Cenni preliminari sulla sicurezza SQL](sql-database-security-overview.md). Per un'esercitazione, vedere [Proteggere il database SQL di Azure](sql-database-security-tutorial.md).

## <a name="firewall-and-firewall-rules"></a>Firewall e regole del firewall
Il database SQL di Microsoft Azure fornisce un servizio di database relazionale per Azure e altre applicazioni basate su Internet. toohelp proteggere i dati, i firewall impediscono tutti i server di database di access tooyour finché non si specifica quali computer dispongono di autorizzazioni. firewall Hello concede accesso toodatabases in base a hello provenienti dall'indirizzo IP di ogni richiesta. Per altre informazioni, vedere [Panoramica sulle regole del firewall per il database SQL di Azure](sql-database-firewall-configure.md).

Hello servizio Database SQL di Azure è disponibile solo tramite la porta TCP 1433. tooaccess un Database SQL da questo computer, verificare che il firewall del computer client consenta la comunicazione TCP in uscita sulla porta TCP 1433. Se non sono necessarie per altre applicazioni, bloccare le connessioni in ingresso sulla porta TCP 1433. 

Come parte del processo di connessione hello, le connessioni da macchine virtuali di Azure vengono reindirizzate tooa diverso indirizzo IP e la porta, univoca per ogni ruolo di lavoro. numero di porta Hello è compreso nell'intervallo di hello da too11999 11000. Per altre informazioni sulle porte TCP, vedere [Porte superiori a 1433 per ADO.NET 4.5 e il database SQL](sql-database-develop-direct-route-ports-adonet-v12.md).

## <a name="authentication"></a>Autenticazione

Il database SQL supporta due tipi di autenticazione:

* **Autenticazione SQL**, che usa nome utente e password. Durante la creazione di server logico hello per il database, è specificato un account di accesso "amministratore del server" con un nome utente e password. Utilizzando queste credenziali, è possibile autenticare tooany database su tale server come proprietario del database hello o "dbo". 
* **Autenticazione di Azure Active Directory**, che usa identità gestite da Azure Active Directory ed è supportata per domini gestiti e integrati. [Quando possibile](https://docs.microsoft.com/sql/relational-databases/security/choose-an-authentication-mode), usare l'autenticazione di Active Directory (sicurezza integrata). Se si desidera toouse autenticazione di Azure Active Directory, è necessario creare un altro amministratore del server denominato "Azure AD admin", che è consentito gruppi e utenti di Azure AD tooadminister hello. Questo amministratore può inoltre eseguire tutte le operazioni che un amministratore del server regolare può fare. Vedere [connessione tooSQL Database usando Azure Active Directory l'autenticazione](sql-database-aad-authentication.md) per una procedura dettagliata relativa toocreate un tooenable di amministrazione di Azure AD autenticazione di Azure Active Directory.

Motore di Database Hello chiude le connessioni che rimangano inattive per più di 30 minuti. connessione Hello prima nuovo account di accesso può essere utilizzato. In modo continuo tooSQL connessioni attive del Database richiedono la riautorizzazione (eseguita dal motore di database hello) almeno ogni 10 ore. il motore di database Hello prova la nuova autorizzazione tramite password inviato hello e nessun input utente viene richiesto. Per motivi di prestazioni quando si reimposta una password nel Database SQL, hello connessione non è riautenticare, anche se hello connessione viene reimpostata a causa di limitazione delle richieste tooconnection. Ciò è diverso dal comportamento di hello del Server SQL locale. Se password hello è stata modificata dopo la connessione hello inizialmente è stata autorizzata, è necessario terminare la connessione hello e stabilire una nuova connessione utilizzando hello nuova password. Un utente con hello `KILL DATABASE CONNECTION` autorizzazione possa terminare in modo esplicito un tooSQL di connessione del Database tramite hello [KILL](https://docs.microsoft.com/sql/t-sql/language-elements/kill-transact-sql) comando.

Gli account utente possono essere creati nel database master hello e possono essere concesse le autorizzazioni in tutti i database nel server di hello o possono essere creati nel database di hello stesso (denominato utenti indipendenti). Per informazioni sulla creazione e sulla gestione, vedere l'articolo su come [gestire gli account di accesso](sql-database-manage-logins.md). portabilità tooenhance e scalabilty, utilizzare la scalabilità tooenhance agli utenti di database indipendente. Per altre informazioni sugli utenti indipendenti, vedere [Utenti di database indipendente: rendere portabile un database](https://docs.microsoft.com/sql/relational-databases/security/contained-database-users-making-your-database-portable), [CREATE USER (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/statements/create-user-transact-sql) e [Database indipendenti](https://docs.microsoft.com/sql/relational-databases/databases/contained-databases).

Come procedura consigliata l'applicazione deve utilizzare un account dedicato di tooauthenticate: in questo modo è possibile limitare le autorizzazioni di hello concesse toohello applicazione e ridurre i rischi di hello di attività dannose nel caso in cui il codice dell'applicazione è vulnerabile tooa SQL injection attacco. Hello approccio migliore consiste toocreate un [utente del database indipendente](https://docs.microsoft.com/sql/relational-databases/security/contained-database-users-making-your-database-portable), che consente il tooauthenticate app direttamente toohello database. 

## <a name="authorization"></a>Authorization

L'autorizzazione fa riferimento toowhat un utente può eseguire all'interno di un Database SQL di Azure e questa funzionalità è controllata dal database dell'account utente [le appartenenze ai ruoli](https://docs.microsoft.com/sql/relational-databases/security/authentication-access/database-level-roles) e [autorizzazioni a livello di oggetto](https://docs.microsoft.com/sql/relational-databases/security/permissions-database-engine). Come procedura consigliata, è necessario concedere privilegi minimi necessari hello gli utenti. si è connessi con account amministratore del server Hello è un membro del ruolo db_owner, con le operazioni nel database di hello toodo autorità. Salvare questo account per la distribuzione degli aggiornamenti allo schema e altre operazioni di gestione. Utilizzare l'account "ApplicationUser" hello con tooconnect più limitato di autorizzazioni dal database dell'applicazione toohello con hello privilegi minimi necessari per l'applicazione. Per altre informazioni, vedere l'articolo su come [gestire gli account di accesso](sql-database-manage-logins.md).

In genere, solo gli amministratori devono accedere toohello `master` database. Database di access di routine tooeach utente deve essere tramite gli utenti non amministratori di database indipendente in ogni database creati. Quando si usano utenti del database indipendente, non è necessario toocreate gli account di accesso in hello `master` database. Per altre informazioni, vedere [Utenti di database indipendente: rendere portabile un database](https://docs.microsoft.com/sql/relational-databases/security/contained-database-users-making-your-database-portable).

È opportuno acquisire familiarità con hello funzionalità che possono essere utilizzati toolimit o elevare le autorizzazioni seguenti:   
* [Rappresentazione](https://docs.microsoft.com/dotnet/framework/data/adonet/sql/customizing-permissions-with-impersonation-in-sql-server) e [firma modulo](https://docs.microsoft.com/dotnet/framework/data/adonet/sql/signing-stored-procedures-in-sql-server) possono essere utilizzati toosecurely elevare le autorizzazioni temporaneamente.
* [Sicurezza a livello di riga](https://docs.microsoft.com/sql/relational-databases/security/row-level-security) può essere utilizzato come limite alle cui righe un utente può accedere.
* [La maschera dati](sql-database-dynamic-data-masking-get-started.md) può essere utilizzato toolimit l'esposizione dei dati sensibili.
* [Stored procedure](https://docs.microsoft.com/sql/relational-databases/stored-procedures/stored-procedures-database-engine) può essere utilizzato toolimit azioni hello che possono essere eseguite sul database hello.

## <a name="next-steps"></a>Passaggi successivi

- Per una panoramica delle funzionalità di sicurezza di hello Database SQL, vedere [Cenni preliminari sulla sicurezza SQL](sql-database-security-overview.md).
- toolearn più sulle regole del firewall, vedere [regole del Firewall](sql-database-firewall-configure.md).
- toolearn sugli utenti e account di accesso, vedere [gestire gli account di accesso](sql-database-manage-logins.md). 
- Per informazioni sul monitoraggio proattivo, vedere [controllo del database ](sql-database-auditing.md) e [Rilevamento delle minacce nel database SQL](sql-database-threat-detection.md).
- Per un'esercitazione, vedere [Proteggere il database SQL di Azure](sql-database-security-tutorial.md).
