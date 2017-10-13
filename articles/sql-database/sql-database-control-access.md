---
title: Concessione dell'accesso al database SQL di Azure | Documentazione Microsoft
description: Informazioni sulla concessione dell'accesso al database SQL di Microsoft Azure.
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
ms.openlocfilehash: 0ca1ccd273317d67537d31724d566625a4eb2c85
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="azure-sql-database-access-control"></a>Controllo dell'accesso al database SQL di Azure
Per garantire la sicurezza, il database SQL controlla l'accesso con regole del firewall che limitano la connettività in base all'indirizzo IP, meccanismi di autenticazione che richiedono agli utenti di dimostrare la propria identità e meccanismi di autorizzazione che consentono agli utenti di usufruire solo di azioni e dati specifici. 

> [!IMPORTANT]
> Per una panoramica delle funzionalità di sicurezza del database SQL, vedere la [panoramica della sicurezza in SQL](sql-database-security-overview.md). Per un'esercitazione, vedere [Proteggere il database SQL di Azure](sql-database-security-tutorial.md).

## <a name="firewall-and-firewall-rules"></a>Firewall e regole del firewall
Il database SQL di Microsoft Azure fornisce un servizio di database relazionale per Azure e altre applicazioni basate su Internet. Per proteggere i dati, il firewall impedisce qualsiasi accesso al server di database finché non vengono specificati i computer autorizzati. Il firewall concede l'accesso ai database in base all'indirizzo IP di origine di ogni richiesta. Per altre informazioni, vedere [Panoramica sulle regole del firewall per il database SQL di Azure](sql-database-firewall-configure.md).

Il servizio Database SQL di Azure è disponibile solo tramite la porta TCP 1433. Per accedere al database SQL dal computer, assicurarsi che il firewall del computer client consenta la comunicazione TCP in uscita sulla porta TCP 1433. Se non sono necessarie per altre applicazioni, bloccare le connessioni in ingresso sulla porta TCP 1433. 

Come parte del processo di connessione, le connessioni da macchine virtuali di Azure vengono reindirizzate a un indirizzo IP diverso e a una porta, univoca per ogni ruolo di lavoro. Il numero di porta è compreso nell'intervallo che va da 11000 a 11999. Per altre informazioni sulle porte TCP, vedere [Porte superiori a 1433 per ADO.NET 4.5 e il database SQL](sql-database-develop-direct-route-ports-adonet-v12.md).

## <a name="authentication"></a>Autenticazione

Il database SQL supporta due tipi di autenticazione:

* **Autenticazione SQL**, che usa nome utente e password. Durante la creazione del server logico per il database, è stato specificato un account di accesso "amministratore del server" con un nome utente e una password. Utilizzando queste credenziali, è possibile essere autenticati in qualsiasi database di tale server in qualità di proprietario del database o "dbo". 
* **Autenticazione di Azure Active Directory**, che usa identità gestite da Azure Active Directory ed è supportata per domini gestiti e integrati. [Quando possibile](https://docs.microsoft.com/sql/relational-databases/security/choose-an-authentication-mode), usare l'autenticazione di Active Directory (sicurezza integrata). Se si desidera utilizzare l'autenticazione di Azure Active Directory, è necessario creare un altro amministratore del server denominato "admin Azure AD," che è autorizzato ad amministrare utenti e gruppi di Azure AD. Questo amministratore può inoltre eseguire tutte le operazioni che un amministratore del server regolare può fare. Vedere [Connessione al Database SQL utilizzando l'autenticazione di Azure Active Directory](sql-database-aad-authentication.md) per una procedura dettagliata di come creare un amministratore di Azure AD per abilitare l'autenticazione di Azure Active Directory.

Il motore di Database chiude le connessioni che rimangono inattive per più di 30 minuti. La connessione deve accedere nuovamente prima di poter essere utilizzata. Per le connessioni al database SQL attive in modo continuo è necessaria la riautorizzazione (eseguita dal motore di database) almeno ogni 10 ore. Il motore di database tenta la riautorizzazione usando la password inviata originariamente e non è necessario alcun input dell'utente. Per motivi di prestazioni quando si reimposta una password nel Database SQL, la connessione non viene autenticata di nuovo, anche se viene reimpostata a causa del pool di connessioni. Ciò differisce dal comportamento del Server SQL locale. Se la password è stata modificata poichè la connessione è stata inizialmente autorizzata, è necessario terminare la connessione e effettuarne una nuova utilizzando la nuova password. Un utente con autorizzazione `KILL DATABASE CONNECTION` può terminare in modo esplicito una connessione al database SQL usando il comando [KILL](https://docs.microsoft.com/sql/t-sql/language-elements/kill-transact-sql).

È possibile creare gli account utente nel database master e concedere le relative autorizzazioni in tutti i database sul server oppure creare gli account nel database stesso (utenti indipendenti). Per informazioni sulla creazione e sulla gestione, vedere l'articolo su come [gestire gli account di accesso](sql-database-manage-logins.md). Per migliorare la portabilità e la scalabilità, usare utenti di database indipendente. Per altre informazioni sugli utenti indipendenti, vedere [Utenti di database indipendente: rendere portabile un database](https://docs.microsoft.com/sql/relational-databases/security/contained-database-users-making-your-database-portable), [CREATE USER (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/statements/create-user-transact-sql) e [Database indipendenti](https://docs.microsoft.com/sql/relational-databases/databases/contained-databases).

È consigliabile usare un account dedicato per l'autenticazione dell'applicazione. In questo modo è possibile limitare le autorizzazioni concesse all'applicazione e ridurre i rischi di attività dannose, nel caso in cui il codice dell'applicazione sia vulnerabile ad attacchi SQL injection. L'approccio consigliato consiste nel creare un [utente di database indipendente](https://docs.microsoft.com/sql/relational-databases/security/contained-database-users-making-your-database-portable), consentendo così l'autenticazione dell'app direttamente nel database. 

## <a name="authorization"></a>Authorization

Per autorizzazione si intendono le operazioni che l'utente può eseguire in un database SQL di Azure, che sono controllate dalle [appartenenze ai ruoli](https://docs.microsoft.com/sql/relational-databases/security/authentication-access/database-level-roles) del database e dalle [autorizzazioni a livello di oggetto](https://docs.microsoft.com/sql/relational-databases/security/permissions-database-engine) dell'account utente. Come procedura consigliata, è opportuno concedere agli utenti i privilegi minimi necessari. L'account di amministrazione del server a cui ci si sta connettendo è un membro del ruolo db_owner, che è autorizzato a eseguire qualsiasi operazione all'interno del database. Salvare questo account per la distribuzione degli aggiornamenti allo schema e altre operazioni di gestione. Utilizzare l'account "ApplicationUser" con autorizzazioni più limitate per la connessione dall'applicazione al database con i privilegi minimi richiesti dall'applicazione. Per altre informazioni, vedere l'articolo su come [gestire gli account di accesso](sql-database-manage-logins.md).

In genere, solo gli amministratori hanno necessità di accedere al database `master`. L'accesso di routine a ogni database utente deve avvenire tramite gli utenti non amministratori del database indipendente creati in ogni database. Quando si usano gli utenti del database indipendente non è necessario creare account di accesso nel database `master`. Per altre informazioni, vedere [Utenti di database indipendente: rendere portabile un database](https://docs.microsoft.com/sql/relational-databases/security/contained-database-users-making-your-database-portable).

È consigliabile acquisire familiarità con le funzionalità seguenti, utili per limitare o elevare le autorizzazioni:   
* È possibile usare la [rappresentazione](https://docs.microsoft.com/dotnet/framework/data/adonet/sql/customizing-permissions-with-impersonation-in-sql-server) e la [firma del modulo](https://docs.microsoft.com/dotnet/framework/data/adonet/sql/signing-stored-procedures-in-sql-server) per elevare temporaneamente le autorizzazioni in modo sicuro.
* [Sicurezza a livello di riga](https://docs.microsoft.com/sql/relational-databases/security/row-level-security) può essere utilizzato come limite alle cui righe un utente può accedere.
* [Mascheramento dei dati](sql-database-dynamic-data-masking-get-started.md) per limitare l'esposizione dei dati sensibili
* [Stored procedure](https://docs.microsoft.com/sql/relational-databases/stored-procedures/stored-procedures-database-engine) per limitare le operazioni che possono essere eseguite nel database.

## <a name="next-steps"></a>Passaggi successivi

- Per una panoramica delle funzionalità di sicurezza del database SQL, vedere la [panoramica della sicurezza in SQL](sql-database-security-overview.md).
- Per altre informazioni sulle regole del firewall, vedere [Regole del firewall](sql-database-firewall-configure.md).
- Per informazioni su utenti e account di accesso, vedere l'articolo su come [gestire gli account di accesso](sql-database-manage-logins.md). 
- Per informazioni sul monitoraggio proattivo, vedere [controllo del database ](sql-database-auditing.md) e [Rilevamento delle minacce nel database SQL](sql-database-threat-detection.md).
- Per un'esercitazione, vedere [Proteggere il database SQL di Azure](sql-database-security-tutorial.md).
