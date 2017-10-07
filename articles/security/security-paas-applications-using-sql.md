---
title: aaaSecuring database PaaS in Azure | Documenti Microsoft
description: " Informazioni sulle procedure consigliate per la protezione delle applicazioni Web e per dispositivi mobili in PaaS tramite il database SQL di Azure e SQL Data Warehouse. "
services: security
documentationcenter: na
author: techlake
manager: MBaldwin
editor: 
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/11/2017
ms.author: terrylan
ms.openlocfilehash: a7f9a2846b59dcb05e82f2ad88b41c5213295603
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="securing-paas-databases-in-azure"></a>Protezione di database PaaS in Azure

In questo articolo vengono illustrate varie procedure consigliate per la protezione delle applicazioni Web e per dispositivi mobili in PaaS mediante il [database SQL di Azure](https://azure.microsoft.com/services/sql-database/) e [SQL Data Warehouse](https://azure.microsoft.com/services/sql-data-warehouse/). Queste procedure consigliate derivano dall'esperienza acquisita con Azure e l'esperienza dei clienti hello come manualmente.

## <a name="azure-sql-database-and-sql-data-warehouse"></a>Database SQL di Azure e SQL Data Warehouse
Il [database SQL di Azure](../sql-database/sql-database-technical-overview.md) e [SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md) forniscono un servizio di database relazionale per le applicazioni basate su Internet. Verranno ora illustrati i servizi che aiutano a proteggere applicazioni e dati quando si usano il database SQL di Azure e SQL Data Warehouse in una distribuzione PaaS:

- Autenticazione di Azure Active Directory (invece di autenticazione di SQL Server)
- Firewall SQL di Azure
- Transparent data encryption (TDE)

## <a name="best-practices"></a>Procedure consigliate

### <a name="use-a-centralized-identity-repository-for-authentication-and-authorization"></a>Usare un repository di identità centralizzato per autenticazione e autorizzazione

Database SQL di Azure possono essere configurato toouse uno dei due tipi di autenticazione:

- **Autenticazione SQL** usa nome utente e password. Durante la creazione di server logico hello per il database, è specificato un account di accesso "amministratore del server" con un nome utente e password. Utilizzando queste credenziali, è possibile autenticare tooany database su tale server come proprietario del database hello.

- **Autenticazione di Azure Active Directory** usa identità gestite da Azure Active Directory ed è supportata per domini gestiti e integrati. toouse autenticazione di Azure Active Directory, è necessario creare un altro amministratore del server denominato "Azure AD admin", che è consentito gruppi e utenti di Azure AD tooadminister hello. Questo amministratore può inoltre eseguire tutte le operazioni che un amministratore del server regolare può fare.

[L'autenticazione di Azure Active Directory](../active-directory/develop/active-directory-authentication-scenarios.md) è un meccanismo di connessione tooAzure Database SQL e SQL Data Warehouse usando le identità in Azure Active Directory (AD). Azure AD fornisce un'autenticazione Server tooSQL alternativo, pertanto è possibile arrestare la proliferazione di hello delle identità tra server di database. Consente di autenticazione AD Azure si toocentrally gestire le identità di hello di utenti di database e altri servizi Microsoft in un'unica posizione centrale. Gestione centrale di ID fornisce un'unica posizione toomanage gli utenti del database e semplifica la gestione delle autorizzazioni.  

Vantaggi dell'uso dell'autenticazione di Azure AD al posto dell'autenticazione SQL:

- Consente la rotazione delle password in un'unica posizione.
- Consente di gestire le autorizzazioni del database tramite gruppi Azure AD esterni.
- Consente di eliminare l'archiviazione delle password abilitando l'autenticazione integrata di Windows e altre forme di autenticazione supportate da Azure AD.
- Usa contenuti identità tooauthenticate utenti di database a livello di database hello.
- Supporta l'autenticazione basata su token per applicazioni che si connettono tooSQL Database.
- Supporta la federazione dei domini di AD FS o l'autenticazione utente/password nativa per un'istanza locale di Azure AD senza la sincronizzazione del dominio.
- Supporta le connessioni da SQL Server Management Studio che utilizzano l'autenticazione universale di Active Directory, che include l'autenticazione [MFA (Multi-Factor Authentication)](../multi-factor-authentication/multi-factor-authentication.md). L'MFA include funzionalità avanzate di autenticazione con una serie di semplici opzioni di verifica, tra cui: chiamata telefonica, SMS, smart card con pin o notifica tramite app per dispositivi mobili. Per altre informazioni [Supporto di SQL Server Management Studio (SSMS) per l'autenticazione MFA di Azure AD con il database SQL e SQL Data Warehouse](../sql-database/sql-database-ssms-mfa-authentication.md).

toolearn ulteriori informazioni sull'autenticazione di Azure AD, vedere:

- [Connessione tooSQL Database o Data Warehouse da usando Azure Active Directory l'autenticazione di SQL](../sql-database/sql-database-aad-authentication.md)
- [TooAzure l'autenticazione SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-authentication.md)
- [Supporto per l'autenticazione basata su token per il database di SQL Azure mediante l'autenticazione di Azure AD](https://blogs.msdn.microsoft.com/sqlsecurity/2016/02/09/token-based-authentication-support-for-azure-sql-db-using-azure-ad-auth/)

> [!NOTE]
> tooensure che Azure Active Directory è una scelta ottimale per l'ambiente, vedere [funzionalità Azure AD e limitazioni](../sql-database/sql-database-aad-authentication.md#azure-ad-features-and-limitations), in particolare hello considerazioni aggiuntive.
>
>

### <a name="restrict-access-based-on-ip-address"></a>Limitare l'accesso in base all'indirizzo IP
È possibile creare regole del firewall che specificano gli intervalli di indirizzi IP accettabili. Queste regole possono essere destinate sia server hello e livelli di database. Si consiglia di utilizzare le regole del firewall a livello di database ogni volta che sicurezza tooenhance possibili e toomake del database più portabile. Le regole del firewall a livello di server sono ideali per gli amministratori e quando si dispone di molti database che hanno hello stessi requisiti di accesso, ma si desidera ora toospend configurare singolarmente ogni database.

Le restrizioni predefinite agli indirizzi IP di origine del database SQL consentono l'accesso da qualsiasi indirizzo di Azure, inclusi altri tenant e sottoscrizioni. È possibile limitare questo tooonly consentire l'istanza di hello tooaccess gli indirizzi IP. Anche in presenza del firewall SQL e delle restrizioni per gli indirizzi IP, è comunque necessaria un'autenticazione avanzata. Visualizzare le raccomandazioni hello apportate in precedenza in questo articolo.

toolearn ulteriori informazioni sui Firewall di SQL Azure e le restrizioni IP, vedere:

- [Controllo dell'accesso al database SQL di Azure](../sql-database/sql-database-control-access.md)
- [Configurare le regole del firewall per il database SQL di Azure - Panoramica](../sql-database/sql-database-firewall-configure.md)
- [Configurare una regola firewall di livello server di Database SQL di Azure utilizzando hello portale di Azure](../sql-database/sql-database-configure-firewall-settings.md)

### <a name="encryption-of-data-at-rest"></a>Crittografia dei dati inattivi
La funzionalità [Transparent Data Encryption (TDE)](https://msdn.microsoft.com/library/azure/bb934049) è abilitata per impostazione predefinita. Crittografa in modo trasparente i file di log e dati di SQL Server, del database SQL di Azure e Microsoft Azure SQL Data Warehouse. Transparent Data Encryption consente di proteggere la violazione di file toohello accesso diretto o i backup. In questo modo si tooencrypt dati inattivi senza modificare applicazioni esistenti. Transparent Data Encryption sempre dovrebbe rimanere abilitata; Tuttavia, un utente malintenzionato che utilizza il percorso di accesso normale hello non verrà interrotta. Transparent Data Encryption fornisce hello possibilità toocomply con numerose leggi, normative e linee guida stabilite in vari settori.

Azure SQL gestisce i principali problemi correlati per TDE. Come con TDE, in locale è necessario prestare particolare attenzione tooensure recuperabilità e lo spostamento di database. In scenari più sofisticati, hello chiavi possono essere in modo esplicito gestite nell'insieme di credenziali chiave di Azure tramite EKM (vedere [abilitare TDE in SQL Server con EKM](/security/encryption/enable-tde-on-sql-server-using-ekm)). Ciò consente anche l'uso di Bring Your Own Key (BYOK) tramite la capacità BYOK di Azure Key Vault.

Azure SQL fornisce la crittografia per le colonne tramite [Always Encrypted](/sql/relational-databases/security/encryption/always-encrypted-database-engine). In questo modo l'accesso solo le applicazioni autorizzate toosensitive colonne. L'utilizzo di questo tipo di crittografia limita le query SQL per i valori tooequality basato su colonne crittografate.

La crittografia a livello di applicazione deve essere usata anche per dati selettivi. Problemi sovranità dati talvolta possono essere ridotto mediante la crittografia dei dati con una chiave che viene mantenuta in paese corretto hello. Ciò impedisce che il trasferimento di dati accidentali anche causa un problema perché è Impossibile toodecrypt hello dati senza chiave hello, presupponendo un algoritmo complesso viene utilizzati (ad esempio AES 256).

È possibile utilizzare i database di hello sicura toohelp precauzioni aggiuntive, ad esempio la progettazione di un sistema sicuro, la crittografia dei dati riservati e la creazione di un firewall attorno hello database server.

## <a name="next-steps"></a>Passaggi successivi
In questo articolo è stato introdotto è tooa raccolta di Database SQL e SQL Data Warehouse le procedure consigliate per proteggere il PaaS web e applicazioni per dispositivi mobili. toolearn più sulla protezione di distribuzioni PaaS, vedere:

- [Protezione delle distribuzioni PaaS](security-paas-deployments.md)
- [Protezione delle applicazioni Web e per dispositivi mobili in PaaS mediante i Servizi app di Azure](security-paas-applications-using-app-services.md)
