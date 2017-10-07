---
title: autenticazione di Active Directory aaaAzure - SQL di Azure (panoramica) | Documenti Microsoft
description: Per ulteriori informazioni vedere toouse Azure Active Directory per l'autenticazione con il Database SQL e SQL Data Warehouse
services: sql-database
documentationcenter: 
author: BYHAM
manager: jhubbard
editor: 
tags: 
ms.assetid: 7e2508a1-347e-4f15-b060-d46602c5ce7e
ms.service: sql-database
ms.custom: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 08/11/2017
ms.author: rickbyh
ms.openlocfilehash: 7a63a162653b65294e11d3fa5bf39c320e742854
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-active-directory-authentication-for-authentication-with-sql-database-or-sql-data-warehouse"></a>Usare l'autenticazione di Azure Active Directory per l'autenticazione di un database SQL o di SQL Data Warehouse
L'autenticazione di Azure Active Directory è un meccanismo di connessione di Database SQL di Azure tooMicrosoft e [SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md) usando le identità in Azure Active Directory (Azure AD). Con l'autenticazione di Azure AD, è possibile gestire centralmente le identità hello di utenti del database e altri servizi Microsoft in un'unica posizione centrale. Gestione centrale di ID fornisce un'unica posizione toomanage gli utenti del database e semplifica la gestione delle autorizzazioni. Esempio hello vantaggi:

* Fornisce l'autenticazione Server tooSQL alternativo.
* Consente di arrestare la proliferazione di hello delle identità tra server di database.
* Consente la rotazione delle password in un'unica posizione.
* I clienti possono gestire le autorizzazioni del database tramite gruppi (AAD) esterni.
* Può eliminare l'archiviazione delle password abilitando l'autenticazione integrata di Windows e altre forme di autenticazione supportate da Azure Active Directory.
* Autenticazione di Azure AD Usa identità tooauthenticate utenti di database indipendente a livello di database hello.
* Azure AD supporta l'autenticazione basata su token per applicazioni che si connettono tooSQL Database.
* L'autenticazione di Azure AD supporta la federazione dei domini di AD FS o l'autenticazione utente/password nativa per un'istanza locale di Azure Active Directory senza la sincronizzazione del dominio.  
* Azure AD supporta le connessioni da SQL Server Management Studio che utilizzano l'autenticazione universale di Active Directory, che include l'MFA (Multi-Factor Authentication).  L'MFA include funzionalità avanzate di autenticazione con una serie di semplici opzioni di verifica, tra cui: chiamata telefonica, SMS, smart card con pin o notifica tramite app per dispositivi mobili. Per altre informazioni [Supporto di SQL Server Management Studio (SSMS) per l'autenticazione MFA di Azure AD con il database SQL e SQL Data Warehouse](sql-database-ssms-mfa-authentication.md).  

>  [!NOTE]  
>  Connessione tooSQL Server in esecuzione in una macchina virtuale di Azure non è supportato con un account Azure Active Directory. Usare un account Active Directory di dominio.  

passaggi di configurazione Hello includono hello seguendo procedure tooconfigure e utilizzano l'autenticazione di Azure Active Directory.

1. Creare e popolare un'istanza di Azure AD.
2. Facoltativo: Associare o modificare hello active directory a cui è attualmente associato alla sottoscrizione di Azure.
3. Creare un amministratore di Azure Active Directory per il server di Azure SQL o per [Azure SQL Data Warehouse](https://azure.microsoft.com/services/sql-data-warehouse/).
4. Configurare i computer client.
5. Creare utenti del database indipendente in tooAzure del database eseguito il mapping delle identità di Active Directory.
6. Connessione database tooyour usando le identità di Azure AD.

> [!NOTE]
> toolearn come toocreate e popolare Azure AD e quindi configurare Azure AD con Database SQL di Azure e SQL Data Warehouse, vedere [Configura Azure AD con Database SQL di Azure](sql-database-aad-authentication-configure.md).
>

## <a name="trust-architecture"></a>Architettura di attendibilità
Hello seguente diagramma di alto livello riepiloga l'architettura della soluzione hello di utilizzo dell'autenticazione di Azure AD con Database SQL di Azure. Hello stessi concetti si applicano tooSQL Data Warehouse. viene considerato toosupport password utente nativi di Azure AD, solo parte Cloud hello e Database SQL di Azure Active Directory o Azure. toosupport autenticazione federata (o un utente/password per le credenziali di Windows), è richiesta la comunicazione hello con blocco di ADFS. Hello indicano i percorsi di comunicazione.

![diagramma di autenticazione di aad][1]

Hello diagramma seguente indica la federazione hello trust e relazioni che consentono a un client tooconnect tooa database, presentando un token di hosting. token Hello è autenticato da Azure Active Directory ed è considerato attendibile dal database di hello. Il cliente 1 può rappresentare una Azure Active Directory con utenti nativi o una Azure AD con utenti federati. In questo esempio provengono da un'istanza federata di Azure Active Directory con AD FS sincronizzato con Azure Active Directory. È importante toounderstand che accedono a database tooa utilizzando l'autenticazione di Azure AD richiede che hello hosting sottoscrizione toohello associato AD Azure. stessa sottoscrizione Hello deve essere utilizzato toocreate hello SQL hosting messaggi hello del Server Database SQL di Azure o SQL Data Warehouse.

![relazione di sottoscrizione][2]

## <a name="administrator-structure"></a>Struttura dell'account amministratore
Quando si utilizza l'autenticazione di Azure AD, sono disponibili due account di amministratore per il server di Database SQL di hello; Hello amministratore originale di SQL Server e amministratore hello Azure AD. Hello stessi concetti si applicano tooSQL Data Warehouse. Solo amministratore di hello in base a un account Azure AD è possibile creare il primo utente di database contenuti di Azure AD di hello in un database utente. account di accesso amministratore Hello Azure AD può essere un utente di Azure Active Directory o un gruppo di Azure AD. Quando l'amministratore di hello è un account di gruppo, può essere utilizzato da qualsiasi membro del gruppo, consentendo agli amministratori di Azure AD più hello istanza di SQL Server. Utilizzando l'account di gruppo come amministratore migliora la gestibilità, consentendo toocentrally aggiungere e rimuovere membri dei gruppi in Azure AD senza modificare gli utenti di hello o autorizzazioni nel Database SQL. È possibile configurare un solo amministratore di Azure AD (utente o gruppo) alla volta.

![struttura di amministrazione][3]

## <a name="permissions"></a>Autorizzazioni
toocreate nuovi utenti, è necessario disporre hello `ALTER ANY USER` autorizzazione nel database di hello. Hello `ALTER ANY USER` autorizzazione può essere concessa tooany utente del database. Hello `ALTER ANY USER` autorizzazione viene inoltre assegnata hello account di amministratore server e gli utenti del database con hello `CONTROL ON DATABASE` o `ALTER ON DATABASE` disporre dell'autorizzazione per il database e dai membri di hello `db_owner` ruolo del database.

toocreate un utente del database indipendente in Database SQL di Azure o SQL Data Warehouse, è necessario connettersi toohello database utilizzando un'identità di Azure AD. toocreate hello primo utente del database indipendente, è necessario connettersi a database toohello tramite un amministratore di Azure AD (che è proprietario di hello del database hello). Questa operazione è illustrata nei passaggi 4 e 5 di seguito. Qualsiasi autenticazione di Azure AD è possibile solo se salve Azure AD è stato creato per il server di Database SQL di Azure o SQL Data Warehouse. Se è stata rimossa dal server hello salve Azure Active Directory, gli utenti di Azure Active Directory esistenti creati in precedenza all'interno di SQL Server non possono più connettersi toohello database utilizzando le proprie credenziali di Azure Active Directory.

## <a name="azure-ad-features-and-limitations"></a>Funzionalità e limitazioni di Azure AD
nel server SQL di Azure o SQL Data Warehouse, è possibile effettuare il provisioning Hello segue i membri di Azure Active Directory:

* I membri native: un membro creato in Azure Active Directory nel dominio gestito hello o in un dominio del cliente. Per ulteriori informazioni, vedere [aggiungere la propria tooAzure nome di dominio Active Directory](../active-directory/active-directory-add-domain.md).
* Membri del dominio federato: un membro creato in Azure AD con un dominio federato. Per altre informazioni, vedere il post di blog relativo al [nuovo supporto per la federazione in Microsoft Azure con Active Directory di Windows Server](https://azure.microsoft.com/blog/2012/11/28/windows-azure-now-supports-federation-with-windows-server-active-directory/).
* Membri importati da altre istanze di Azure AD che sono membri nativi o del dominio federato.
* Gruppi di Active Directory creati come gruppi di sicurezza.

Gli account Microsoft, ad esempio outlook.com, hotmail.com, live.com, oppure altri account guest, ad esempio gmail.com, yahoo.com, non sono supportati. Se non è possibile accedere troppo[https://login.live.com](https://login.live.com) utilizzando account hello e una password, quindi si utilizza un account Microsoft, che non è supportato per l'autenticazione di Azure AD per Database SQL di Azure o Azure SQL Data Warehouse.

## <a name="connecting-using-azure-ad-identities"></a>Connettersi usando le identità di Azure AD

L'autenticazione di Azure Active Directory supporta hello dei seguenti metodi di connessione database tooa mediante identità di Azure AD:

* Con l'autenticazione integrata di Windows
* Con un nome di entità e una password di Azure AD
* Con l'autenticazione del token dell'applicazione

### <a name="additional-considerations"></a>Considerazioni aggiuntive

* tooenhance gestibilità, si consiglia effettuare il provisioning di un annuncio di Azure dedicato gruppo come amministratore.   
* È possibile configurare un solo amministratore di Azure AD, utente o gruppo, per un server di Azure SQL o Azure SQL Data Warehouse in qualsiasi momento.   
* Solo un amministratore di Azure AD per SQL Server può connettersi inizialmente toohello Azure SQL server o Azure SQL Data Warehouse utilizzando un account Azure Active Directory. amministratore di Active Directory Hello è possibile configurare Azure AD successive agli utenti di database.   
* È consigliabile impostare hello connection timeout too30 (secondi).   
* SQL Server 2016 Management Studio e SQL Server Data Tools per Visual Studio 2015, versione 14.0.60311.1 di aprile 2016 o successiva, supportano l'autenticazione di Azure Active Directory. (Autenticazione di azure AD è supportato da hello **il Provider di dati .NET Framework per SqlServer**; almeno la versione .NET Framework 4.6). Pertanto hello versioni più recenti di questi strumenti e applicazioni livello dati (DAC e con estensione bacpac) possono utilizzare l'autenticazione di Azure AD.   
* [ODBC versione 13.1](https://www.microsoft.com/download/details.aspx?id=53339) supporta l'autenticazione di Azure Active Directory, tuttavia `bcp.exe` non può connettersi mediante l'autenticazione di Azure Active Directory perché usa un provider ODBC meno recente.   
* `sqlcmd`supporta inizio l'autenticazione di Azure Active Directory con versione 13.1 disponibili hello [area Download](http://go.microsoft.com/fwlink/?LinkID=825643).   
* SQL Server Data Tools per Visual Studio 2015 richiede almeno la versione di aprile 2016 hello di hello Data Tools (versione 14.0.60311.1). Gli utenti di Azure AD non sono attualmente visualizzati in Esplora oggetti di SSDT. In alternativa, consente di visualizzare gli utenti di hello [Sys. database_principals](https://msdn.microsoft.com/library/ms187328.aspx).   
* [Microsoft JDBC Driver 6.0 per server SQL](https://www.microsoft.com/download/details.aspx?id=11774) supporta l'autenticazione di Azure AD. Vedere anche [impostazione delle proprietà di connessione hello](https://msdn.microsoft.com/library/ms378988.aspx).   
* PolyBase non può eseguire l'autenticazione di Azure AD.   
* Autenticazione di Azure AD è supportato per il Database SQL dal portale di Azure hello **Database di importazione** e **Esporta Database** pannelli. Importazione ed esportazione utilizzando l'autenticazione di Azure AD è anche supportato da hello comando di PowerShell.   
* L'autenticazione di Azure AD è supportata per il database SQL e SQL Data Warehouse usando l'interfaccia della riga di comando di Azure. Per altre informazioni, vedere [Configurare e gestire l'autenticazione di Azure Active Directory con il database SQL oppure con SQL Data Warehouse](sql-database-aad-authentication-configure.md) e [SQL Server - az sql server](https://docs.microsoft.com/en-us/cli/azure/sql/server).

## <a name="next-steps"></a>Passaggi successivi
- toolearn come toocreate e popolare Azure AD e quindi configurare Azure AD con Database SQL di Azure o Azure SQL Data Warehouse, vedere [configurare e gestire l'autenticazione di Azure Active Directory con Database SQL o SQL Data Warehouse](sql-database-aad-authentication-configure.md).
- Per una panoramica dell'accesso e del controllo nel database SQL, vedere l'articolo relativo al [controllo dell'accesso al database SQL](sql-database-control-access.md).
- Per una panoramica degli account di accesso, degli utenti e dei ruoli del database nel database SQL, vedere l'articolo relativo ad [account di accesso, utenti e ruoli del database](sql-database-manage-logins.md).
- Per altre informazioni sulle entità di database, vedere [Entità](https://msdn.microsoft.com/library/ms181127.aspx).
- Per altre informazioni sui ruoli del database, vedere [Ruoli a livello di database](https://msdn.microsoft.com/library/ms189121.aspx).
- Per informazioni generali sulle regole del firewall, vedere l'articolo relativo alle [regole del firewall per il database SQL](sql-database-firewall-configure.md).

<!--Image references-->

[1]: ./media/sql-database-aad-authentication/1aad-auth-diagram.png
[2]: ./media/sql-database-aad-authentication/2subscription-relationship.png
[3]: ./media/sql-database-aad-authentication/3admin-structure.png
[4]: ./media/sql-database-aad-authentication/4select-subscription.png
[5]: ./media/sql-database-aad-authentication/5ad-settings-portal.png
[6]: ./media/sql-database-aad-authentication/6edit-directory-select.png
[7]: ./media/sql-database-aad-authentication/7edit-directory-confirm.png
[8]: ./media/sql-database-aad-authentication/8choose-ad.png
[9]: ./media/sql-database-aad-authentication/9ad-settings.png
[10]: ./media/sql-database-aad-authentication/10choose-admin.png
[11]: ./media/sql-database-aad-authentication/11connect-using-int-auth.png
[12]: ./media/sql-database-aad-authentication/12connect-using-pw-auth.png
[13]: ./media/sql-database-aad-authentication/13connect-to-db.png

