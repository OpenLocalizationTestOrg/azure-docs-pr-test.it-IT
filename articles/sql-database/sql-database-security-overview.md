---
title: Cenni preliminari sulla sicurezza di SQL Database aaaAzure | Documenti Microsoft
description: "Informazioni sulla sicurezza di Database SQL di Azure e SQL Server, tra cui hello le differenze tra SQL Server in locale e cloud hello per quanto riguarda tooauthentication, autorizzazione, la protezione della connessione, crittografia e la conformità."
services: sql-database
documentationcenter: 
author: tmullaney
manager: jhubbard
editor: 
ms.assetid: a012bb85-7fb4-4fde-a2fc-cf426c0a56bb
ms.service: sql-database
ms.custom: security
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-management
ms.date: 07/05/2017
ms.author: thmullan;jackr
ms.openlocfilehash: 7b0b0d1b59ec4018d9fb668bc8b6b56c9907e982
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="securing-your-sql-database"></a>Protezione del Database SQL

In questo articolo vengono illustrati concetti di base di hello di sicurezza di livello dati hello di un'applicazione utilizzando il Database SQL di Azure. In particolare, questo articolo consente di iniziare a usare le risorse per la protezione dei dati, il controllo dell'accesso e il monitoraggio proattivo. 

Per una panoramica completa delle funzionalità di sicurezza disponibili in tutte le versioni di SQL, vedere hello [centro di sicurezza per il motore di Database di SQL Server e Database SQL di Azure](https://msdn.microsoft.com/library/bb510589). Altre informazioni sono anche disponibili in hello [sicurezza e Database SQL di Azure white paper tecnico](https://download.microsoft.com/download/A/C/3/AC305059-2B3F-4B08-9952-34CDCA8115A9/Security_and_Azure_SQL_Database_White_paper.pdf) (PDF).

## <a name="protect-data"></a>Proteggere i dati
Il database SQL protegge i dati in movimento con la crittografia [Transport Layer Security](https://support.microsoft.com/kb/3135244), i dati inattivi con la crittografia [Transparent Data Encryption](http://go.microsoft.com/fwlink/?LinkId=526242) e i dati in uso con la crittografia [Always Encrypted](https://msdn.microsoft.com/library/mt163865.aspx). 

> [!IMPORTANT]
>Tutte le connessioni tooAzure Database di SQL richiedono una crittografia SSL/TLS () tutti gli orari mentre i dati sono "in transito" tooand dal database hello. Nella stringa di connessione dell'applicazione, è necessario specificare una connessione di parametri tooencrypt hello e *non* tootrust hello il certificato del server (questa operazione viene eseguita per se si copia la stringa di connessione di hello portale classico di Azure) in caso contrario connessione hello non eseguirà la verifica identità hello del server di hello e sarà soggetti attacchi troppo "man-in-the-middle". Per i driver di ADO.NET hello, ad esempio, questi parametri di stringa di connessione sono **Encrypt = True** e **TrustServerCertificate = False**. 

Per altri modi tooencrypt dei dati, prendere in considerazione:

* [Crittografia a livello di cella](https://msdn.microsoft.com/library/ms179331.aspx) tooencrypt colonne specifiche o anche le celle di dati con le chiavi di crittografia diversi.
* Se è necessario un modulo di sicurezza Hardware o la gestione centralizzata della gerarchia di chiavi di crittografia, è consigliabile utilizzare l' [insieme di credenziali chiave di Azure con SQL Server in una relativa macchina virtuale](http://blogs.technet.com/b/kv/archive/2015/01/12/using-the-key-vault-for-sql-server-encryption.aspx).

## <a name="control-access"></a>Controllare l'accesso
Database SQL protegge i dati tramite la limitazione di database di access tooyour utilizzando le regole firewall, richiedere agli utenti tooprove loro identità e autorizzazione toodata tramite appartenenza basata su ruoli e autorizzazioni, nonché tramite i meccanismi di autenticazione la sicurezza a livello di riga e la maschera dati dinamica. Per una discussione sull'utilizzo di hello della funzionalità di controllo di accesso nel Database SQL, vedere [controllare l'accesso](sql-database-control-access.md).

> [!IMPORTANT]
> La gestione dei database e dei server logici in Azure è controllata dalle assegnazioni di ruolo dell'account del portale utenti. Per ulteriori informazioni su questo argomento, vedere [Controllo di accesso basato sui ruoli nel portale di Azure](../active-directory/role-based-access-control-what-is.md).
>

### <a name="firewall-and-firewall-rules"></a>Firewall e regole del firewall
toohelp proteggere i dati, i firewall impediscono tutti i server di database di access tooyour finché non si specifica quali computer dispongono di autorizzazioni mediante [regole del firewall](sql-database-firewall-configure.md). firewall Hello concede accesso toodatabases in base a hello provenienti dall'indirizzo IP di ogni richiesta.

### <a name="authentication"></a>Autenticazione
L'autenticazione del database SQL si riferisce toohow dimostrare la propria identità durante la connessione di database toohello. Il database SQL supporta due tipi di autenticazione:

* **Autenticazione SQL**, che usa nome utente e password. Durante la creazione di server logico hello per il database, è specificato un account di accesso "amministratore del server" con un nome utente e password. Utilizzando queste credenziali, è possibile autenticare tooany database su tale server come proprietario del database hello o "dbo". 
* **Autenticazione di Azure Active Directory**, che usa identità gestite da Azure Active Directory ed è supportata per domini gestiti e integrati. [Quando possibile](https://msdn.microsoft.com/library/ms144284.aspx), usare l'autenticazione di Active Directory (sicurezza integrata). Se si desidera toouse autenticazione di Azure Active Directory, è necessario creare un altro amministratore del server denominato "Azure AD admin", che è consentito gruppi e utenti di Azure AD tooadminister hello. Questo amministratore può inoltre eseguire tutte le operazioni che un amministratore del server regolare può fare. Vedere [connessione tooSQL Database usando Azure Active Directory l'autenticazione](sql-database-aad-authentication.md) per una procedura dettagliata relativa toocreate un tooenable di amministrazione di Azure AD autenticazione di Azure Active Directory.

### <a name="authorization"></a>Authorization
Autorizzazione fa riferimento a un utente può eseguire all'interno di un Database di SQL Azure toowhat e questo è controllato da appartenenze al ruolo del database dell'account utente e a livello di oggetto autorizzazioni. Come procedura consigliata, è necessario concedere privilegi minimi necessari hello gli utenti. si è connessi con account amministratore del server Hello è un membro del ruolo db_owner, con le operazioni nel database di hello toodo autorità. Salvare questo account per la distribuzione degli aggiornamenti allo schema e altre operazioni di gestione. Utilizzare l'account "ApplicationUser" hello con tooconnect più limitato di autorizzazioni dal database dell'applicazione toohello con hello privilegi minimi necessari per l'applicazione.

### <a name="row-level-security"></a>Sicurezza a livello di riga
Sicurezza a livello di riga consente ai clienti toocontrol accesso toorows in una tabella di database in base alle caratteristiche di hello dell'utente hello esegue una query (ad esempio, gruppo appartenenza o l'esecuzione del contesto). Per altre informazioni, vedere [Sicurezza a livello di riga](https://msdn.microsoft.com/library/dn765131).

### <a name="data-masking"></a>Maschera dati 
La maschera dati dinamica del Database SQL limita l'esposizione dei dati sensibili nascondendoli agli utenti con privilegi toonon. Automaticamente la maschera dati dinamica consente di individuare dati potenzialmente sensibili nel Database SQL di Azure e fornisce suggerimenti pratici toomask questi campi, con un impatto minimo sul livello di applicazione hello. Alla vista dati sensibili hello nel set di risultati hello di una query su campi di database designati, senza modificare dati hello hello database funziona. Per ulteriori informazioni, vedere [iniziare con la maschera dati dinamica del Database SQL](sql-database-dynamic-data-masking-get-started.md) può essere utilizzato toolimit l'esposizione dei dati sensibili.

## <a name="proactive-monitoring"></a>Monitoraggio proattivo
Il database SQL protegge i dati fornendo funzionalità di controllo e di rilevamento delle minacce. 

### <a name="auditing"></a>Controllo
Controllo del Database SQL tiene traccia delle attività relative ai database e consente di conformità alle normative toomaintain, registrando i log di controllo tooan gli eventi di database nell'account di archiviazione di Azure. Il controllo consente attività di database in corso toounderstand, nonché analizzare e analizzare potenziali minacce di attività cronologica tooidentify o violazioni di sicurezza e di evitare eventuali abusi sospette. Per altre informazioni, vedere [Introduzione al controllo del database SQL](sql-database-auditing.md).  

### <a name="threat-detection"></a>Introduzione al rilevamento delle minacce
Rilevamento minacce si integra con il controllo, fornendo un ulteriore livello di business intelligence di sicurezza incorporata nel servizio di Database SQL di Azure hello che rileva i tentativi insoliti e potenzialmente dannoso tooaccess o exploit database. L'utente verrà avvisato di attività sospette, vulnerabilità potenziali e attacchi SQL injection, nonché di modelli di accesso al database anomali. È possibile visualizzare gli avvisi di rilevamento minacce dal [Centro sicurezza di Azure](https://azure.microsoft.com/services/security-center/) e fornire i dettagli dell'attività sospette e consigliabile azione sulla tooinvestigate e ridurre il rischio di hello. La funzionalità Rilevamento delle minacce ha un costo di $15/server/mese Sarà disponibile per hello 60 giorni prima. Per altre informazioni, vedere l' [Introduzione al rilevamento delle minacce nel database SQL](sql-database-threat-detection.md).
 
### <a name="data-masking"></a>Maschera dati 
La maschera dati dinamica del Database SQL limita l'esposizione dei dati sensibili nascondendoli agli utenti con privilegi toonon. Automaticamente la maschera dati dinamica consente di individuare dati potenzialmente sensibili nel Database SQL di Azure e fornisce suggerimenti pratici toomask questi campi, con un impatto minimo sul livello di applicazione hello. Alla vista dati sensibili hello nel set di risultati hello di una query su campi di database designati, senza modificare dati hello hello database funziona. Per altre informazioni, vedere [Introduzione alla maschera dati dinamica del database SQL](sql-database-dynamic-data-masking-get-started.md)
 
## <a name="compliance"></a>Conformità
Inoltre toohello sopra le funzionalità che consentono l'applicazione di soddisfare diversi requisiti di sicurezza, Database SQL di Azure anche partecipa ai controlli regolari e ha ottenuto la certificazione in base a una serie di standard di conformità. Per ulteriori informazioni, vedere hello [Microsoft Azure Trust Center](https://azure.microsoft.com/support/trust-center/), in cui è possibile trovare l'elenco più recente di hello di [certificazioni di conformità di Database SQL](https://azure.microsoft.com/support/trust-center/services/).

## <a name="next-steps"></a>Passaggi successivi

- Per una discussione sull'utilizzo di hello della funzionalità di controllo di accesso nel Database SQL, vedere [controllare l'accesso](sql-database-control-access.md).
- Per informazioni sul controllo del database, vedere [SQL Database auditing](sql-database-auditing.md) (Controllo del database SQL).
- Per informazioni sul rilevamento delle minacce, vedere [SQL Database threat detection](sql-database-threat-detection.md) (Rilevamento delle minacce nel database SQL).
