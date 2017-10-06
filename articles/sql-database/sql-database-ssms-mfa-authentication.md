---
title: aaaMulti-Factor authentication - SQL di Azure | Documenti Microsoft
description: Utilizzare Multi-Factored Authentication con SSMS per il database SQL e SQL Data Warehouse.
services: sql-database
documentationcenter: 
author: BYHAM
manager: jhubbard
editor: 
tags: 
ms.assetid: fbd6e644-0520-439c-8304-2e4fb6d6eb91
ms.service: sql-database
ms.custom: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/19/2017
ms.author: rickbyh
ms.openlocfilehash: 57ef63b7c7f2c5cf64c3e1ee194d865ee5b14177
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="universal-authentication-with-sql-database-and-sql-data-warehouse-ssms-support-for-mfa"></a>Autenticazione universale con database SQL e SQL Data Warehouse (supporto SSMS per MFA)
Il database SQL e Azure SQL Data Warehouse supportano le connessioni da SQL Server Management Studio (SSMS) tramite l'*autenticazione universale di Active Directory*. 
**Scaricare hello SSMS più recente** - computer client hello scaricare hello la versione più recente di SSMS, da [scaricare SQL Server Management Studio (SQL Server Management Studio)](https://msdn.microsoft.com/library/mt238290.aspx). Per tutte le funzionalità di hello in questo argomento, usare almeno luglio 2017, versione 17,2.  Hello più recente connessione della finestra di dialogo simile al seguente: ![1mfa universal connessione](./media/sql-database-ssms-mfa-auth/1mfa-universal-connect.png "casella del nome utente hello viene completata.")  

## <a name="hello-five-authentication-options"></a>opzioni di autenticazione Hello cinque  
- Autenticazione universale di Active Directory supporta due metodi di autenticazione non interattivo hello (`Active Directory - Password` l'autenticazione e `Active Directory - Integrated` autenticazione). I metodi di autenticazione `Active Directory - Password` e `Active Directory - Integrated` non interattivi possono essere usati in svariate applicazioni (ADO.NET, JDBC, ODBC e così via). Questi due metodi non aprono mai finestre di dialogo popup.

- L'autenticazione `Active Directory - Universal with MFA` è un metodo interattivo che supporta anche *Azure Multi-Factor Authentication* (MFA). Azure MFA consente di salvaguardare accesso toodata e applicazioni rispettando richiesta dell'utente per un semplice processo. Fornisce l'autenticazione avanzata con una gamma di opzioni di verifica semplice (telefonata, SMS, le smart card con pin, o la notifica dell'app mobile), che consente agli utenti toochoose hello (metodo) preferiscono. La convalida di MFA interattiva con Azure AD può avvenire attraverso una finestra popup.

Per una descrizione di Multi-Factor Authentication (autenticazione a più fattori), consultare [Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication.md).
Per la procedura di configurazione, vedere [Configurare Multi-Factor Authentication con database SQL di Azure per SQL Server Management Studio](sql-database-ssms-mfa-authentication-configure.md).

### <a name="azure-ad-domain-name-or-tenant-id-parameter"></a>Parametro nome di dominio o ID tenant di Azure AD   

A partire da [SSMS versione 17](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms), gli utenti che vengono importati in hello corrente di Active Directory da altre directory di Azure Active Directory come utenti guest, possono fornire il nome di dominio hello Azure AD, o ID tenant al momento della connessione. Gli utenti guest includono quelli invitati da altre istanze di Azure AD, gli account Microsoft, ad esempio outlook.com, hotmail.com, live.com, o altri account come gmail.com. Queste informazioni consente **universali Active Directory con l'autenticazione MFA** tooidentify hello corretto l'autorità di autenticazione. Questa opzione è inoltre necessario toosupport account di Microsoft (MSA), ad esempio outlook.com, hotmail.com, live.com o account non MSA. Tutti questi utenti che desiderano toobe autenticato tramite l'autenticazione universale deve immettere il proprio nome di dominio Active Directory di Azure o di un tenant ID. Questo parametro rappresenta hello di hello Azure AD corrente dominio nome tenant ID che server Azure non è collegato. Ad esempio, se il Server di Azure è associato al dominio di Azure AD `contosotest.onmicrosoft.com` dove utente `joe@contosodev.onmicrosoft.com` è ospitato come un utente importato dal dominio di Azure AD `contosodev.onmicrosoft.com`, hello tooauthenticate necessario un nome di dominio è l'utente `contosotest.onmicrosoft.com`. Quando l'utente hello è un utente di hello Azure AD collegato tooAzure Server nativo e non è un account del servizio gestito, non è necessario alcun ID tenant o nome di dominio. parametro hello tooenter (a partire da SQL Server Management Studio versione 17,2), hello **connettersi tooDatabase** della finestra di dialogo hello completo della finestra di dialogo selezione **Active Directory - Universal con autenticazione a più fattori** l'autenticazione, Fare clic su **opzioni**, hello completo **nome utente** casella e quindi fare clic su hello **le proprietà di connessione** scheda. Controllare hello **ID tenant o nome di dominio Active Directory** e specificare l'autorità di autenticazione, ad esempio il nome di dominio hello (**contosotest.onmicrosoft.com**) o hello GUID dell'ID del tenant hello.  
   ![mfa-tenant-ssms](./media/sql-database-ssms-mfa-auth/mfa-tenant-ssms.png)   

### <a name="azure-ad-business-toobusiness-support"></a>Supporto di Azure AD business toobusiness   
Gli utenti di Azure AD è supportati negli scenari B2B di Azure Active Directory come utenti guest (vedere [cosa è collaborazione B2B di Azure](../active-directory/active-directory-b2b-what-is-azure-ad-b2b.md)) può connettersi tooSQL Database e SQL Data Warehouse solo come parte dei membri di un gruppo creato in Azure AD corrente e il mapping manualmente utilizzo di Transact-SQL hello `CREATE USER` istruzione in un database specifico. Ad esempio, se `steve@gmail.com` è tooAzure invitati AD `contosotest` (con il dominio di Active Directory di Azure hello `contosotest.onmicrosoft.com`), gruppo di Azure Active Directory, ad esempio `usergroup` deve essere creato in Azure Active Directory che contiene hello hello `steve@gmail.com` membro. Questo gruppo deve quindi essere creato per un database specifico, ad esempio MyDatabase, dall'amministratore del database SQL o dal DBO di Azure AD tramite un'istruzione Transact-SQL `CREATE USER [usergroup] FROM EXTERNAL PROVIDER`. Dopo aver creato l'utente del database hello, quindi hello utente `steve@gmail.com` può eseguire l'accesso troppo`MyDatabase` utilizzando l'opzione di autenticazione di SQL Server Management Studio hello `Active Directory – Universal with MFA support`. Hello usergroup, per impostazione predefinita, dispone solo di hello connettersi autorizzazione e qualsiasi ulteriore accesso ai dati che sarà necessario concedere in hello toobe modo normale. Si noti che l'utente `steve@gmail.com` come utente guest deve hello casella di controllo e aggiungere il nome di dominio Active Directory hello `contosotest.onmicrosoft.com` in SSMS hello **proprietà di connessione** la finestra di dialogo. Hello **ID tenant o nome di dominio Active Directory** opzione è supportata solo per hello Universal con le opzioni di connessione di autenticazione a più fattori, in caso contrario è disattivata.

## <a name="universal-authentication-limitations-for-sql-database-and-sql-data-warehouse"></a>Limitazioni dell'autenticazione universale per il database SQL e SQL Data Warehouse
* SQL Server Management Studio e SqlPackage.exe sono strumenti solo a hello attualmente abilitati per l'autenticazione a più fattori tramite l'autenticazione universale di Active Directory.
* La versione 17.2 di SSMS supporta l'accesso simultaneo di più utenti tramite l'autenticazione universale con supporto MFA. Versione 17,0 e 17.1, può essere un log in un'istanza di SQL Server Management Studio utilizzando l'account di Azure Active Directory singola autenticazione universale tooa. toolog in un altro account di Azure AD, è necessario utilizzare un'altra istanza di SQL Server Management Studio. (Questa restrizione è limitato tooActive autenticazione universale di Directory, è possibile registrare nei server di toodifferent utilizzando l'autenticazione di Password di Active Directory, l'autenticazione integrata di Active Directory o l'autenticazione di SQL Server).
* SSMS supporta l'autenticazione universale di Active Directory per la visualizzazione di Esplora oggetti, Editor di query e Archivio query.
* La versione 17.2 di SSMS fornisce il supporto di DacFx Wizard per le funzioni di esportazione, estrazione e distribuzione dei dati del database. Una volta autenticato un utente specifico tramite autenticazione universale dalla finestra di dialogo hello l'autenticazione iniziale, hello funzioni DacFx guidata hello stesso modo utilizzato per tutti gli altri metodi di autenticazione.
* Hello Progettazione tabelle SQL Server Management Studio non supporta l'autenticazione universale.
* Non ci sono requisiti software aggiuntivi per l'autenticazione universale di Active Directory ad eccezione del fatto che si utilizzi una versione supportata di SSMS.  
* versione di Hello Active Directory Authentication Library (ADAL) per l'autenticazione universale è stato aggiornato tooits versione ADAL.dll 3.13.9 disponibili rilasciato. Vedere [Active Directory Authentication Library 3.14.1](http://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/).


## <a name="next-steps"></a>Passaggi successivi

- Per la procedura di configurazione, vedere [Configurare Multi-Factor Authentication con database SQL di Azure per SQL Server Management Studio](sql-database-ssms-mfa-authentication-configure.md).
- Concedere ad altri utenti di accesso database tooyour: [SQL Database autenticazione e autorizzazione: concessione dell'accesso](sql-database-manage-logins.md)  
- Verificare che altri utenti possono connettersi tramite firewall hello: [regola firewall di configurare un server a livello di Database SQL di Azure utilizzando hello portale di Azure](sql-database-configure-firewall-settings.md)  
- [Configurare e gestire l'autenticazione di Azure Active Directory con il database SQL oppure con SQL Data Warehouse](sql-database-aad-authentication-configure.md)  
- [Microsoft SQL Server Data-Tier Application Framework (17.0.0 GA)](https://www.microsoft.com/download/details.aspx?id=55088)  
- [SQLPackage.exe](https://msdn.microsoft.com/library/hh550080.aspx)  
- [Importare un tooa file BACPAC Nuovo Database SQL di Azure](../sql-database/sql-database-import.md)  
- [Esportare un file BACPAC tooa database di SQL Azure](../sql-database/sql-database-export.md)  
- Interfaccia C# [IUniversalAuthProvider](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.iuniversalauthprovider.aspx)  
