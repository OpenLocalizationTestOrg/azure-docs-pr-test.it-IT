---
title: "autenticazione a più fattori aaaConfigure - SQL di Azure | Documenti Microsoft"
description: Utilizzare Multi-Factored Authentication con SSMS per il database SQL e SQL Data Warehouse.
services: sql-database
documentationcenter: 
author: BYHAM
manager: jhubbard
editor: 
tags: 
ms.assetid: 
ms.service: sql-database
ms.custom: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/17/2017
ms.author: rickbyh
ms.openlocfilehash: acb275965f4199f7d5e1378d5077824a9bbc80e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-multi-factor-authentication-for-sql-server-management-studio-and-azure-ad"></a>Configurare Multi-Factor Authentication per SQL Server Management Studio e Azure AD

In questo argomento illustra come autenticazione a più fattori toouse Azure Active Directory (MFA) con SQL Server Management Studio. Quando ci si connette a SQL Server Management Studio o SqlPackage.exe tooAzure Database SQL e Azure SQL Data Warehouse, è possibile utilizzare Azure AD MFA.

Per una panoramica dell'autenticazione a più fattori per il database SQL di Azure, vedere [Autenticazione universale con database SQL e SQL Data Warehouse (supporto SSMS per MFA)](sql-database-ssms-mfa-authentication.md).

## <a name="configuration-steps"></a>Procedura di configurazione

1. **Configurare Azure Active Directory** : per ulteriori informazioni, vedere [amministrazione della directory di Azure AD](https://msdn.microsoft.com/library/azure/hh967611.aspx), [integrazione delle identità locali con Azure Active Directory](../active-directory/active-directory-aadconnect.md), [Aggiungere la propria tooAzure nome di dominio Active Directory](https://azure.microsoft.com/blog/2012/11/28/windows-azure-now-supports-federation-with-windows-server-active-directory/), [Microsoft Azure supporta ora la federazione con Windows Server Active Directory](https://azure.microsoft.com/blog/2012/11/28/windows-azure-now-supports-federation-with-windows-server-active-directory/), e [gestire Azure AD tramite Windows PowerShell ](https://msdn.microsoft.com/library/azure/jj151815.aspx).
2. **Configurare MFA**: per istruzioni dettagliate, vedere [Informazioni su Azure Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication.md) e [Accesso condizionale (MFA) con il database SQL di Azure e Azure SQL Data Warehouse](sql-database-conditional-access.md). Per l'accesso condizionale completo è necessaria l'edizione Premium di Azure Active Directory (Azure AD). Con l'edizione standard di Azure AD è disponibile l'autenticazione a più fattori limitata.
3. **Configurare il Database SQL o SQL Data Warehouse per l'autenticazione AD Azure** : per istruzioni dettagliate, vedere [tooSQL connessione Database o Data Warehouse da usando Azure Active Directory l'autenticazione di SQL](sql-database-aad-authentication.md).
4. **Download di SSMS** - computer client hello scaricare hello SSMS più recente, da [scaricare SQL Server Management Studio (SQL Server Management Studio)](https://msdn.microsoft.com/library/mt238290.aspx). Per tutte le funzionalità di hello in questo argomento, usare almeno luglio 2017, versione 17,2.  

## <a name="connecting-by-using-universal-authentication-with-ssms"></a>Connessione tramite l'autenticazione universale con SSMS

Hello alla procedura seguente viene illustrato come tooconnect tooSQL Database o SQL Data Warehouse utilizzando hello SSMS più recente.

1. utilizzo dell'autenticazione universale in hello tooconnect **connettersi tooServer** nella finestra di dialogo **Active Directory - Universal con il supporto di MFA**. (Se viene visualizzato **autenticazione universale di Active Directory** non sono nella versione più recente di hello di SSMS.)  
   ![1mfa-universal-connect][1]  
2. Hello completo **nome utente** casella con le credenziali di Azure Active Directory hello, in formato hello `user_name@domain.com`.  
   ![1mfa-universal-connect-user](./media/sql-database-ssms-mfa-auth/1mfa-universal-connect-user.png)   
3. Se si è connessi come utente guest, è necessario fare clic su **opzioni**e in hello **proprietà di connessione** della finestra di dialogo hello completo **ID tenant o nome di dominio Active Directory** casella. Per altre informazioni, vedere [Autenticazione universale con database SQL e SQL Data Warehouse (supporto SSMS per MFA)](sql-database-ssms-mfa-authentication.md).
   ![mfa-tenant-ssms](./media/sql-database-ssms-mfa-auth/mfa-tenant-ssms.png)   
4. Come di consueto per Database SQL e SQL Data Warehouse, è necessario fare clic su **opzioni** e specificare il database di hello in hello **opzioni** la finestra di dialogo. (Se hello connesso l'utente è un utente guest (ad esempio joe@outlook.com), è necessario hello casella di controllo e aggiungere l'ID tenant o nome di dominio hello AD corrente come parte delle opzioni. Vedere [Autenticazione universale con database SQL e SQL Data Warehouse (supporto SSMS per MFA)]()(sql-database-ssms-mfa-authentication.md. Fare clic su **Connetti**.  
5. Quando hello **Accedi tooyour account** viene visualizzata la finestra di dialogo, specificare account hello e una password dell'identità di Azure Active Directory. Se un utente fa parte di un dominio federato con Azure AD, non è necessario specificare la password.  
   ![2mfa-sign-in][2]  

   > [!NOTE]
   > L'utente viene connesso in questa fase nel caso dell'autenticazione universale con un account che non richiede l'MFA. Per gli utenti che richiedono autenticazione a più fattori, continuare con hello alla procedura seguente:
   >  
   
6. Potrebbero aprirsi due finestre di dialogo per la configurazione del metodo MFA. Questa volta operazione dipende impostazione dell'amministratore di autenticazione a più fattori hello e pertanto può essere facoltativa. Per un dominio di autenticazione a più fattori abilitata questo passaggio è a volte definito (ad esempio, hello dominio richiede agli utenti toouse una smart card e pin).  
   ![3mfa-setup][3]  
7. Hello secondo è possibile eseguire una sola volta la finestra di dialogo consente di dettagli hello tooselect del metodo di autenticazione. le opzioni possibili Hello vengono configurate dall'amministratore.  
   ![4mfa-verify-1][4]  
8. Hello Azure Active Directory invia hello tooyou informazioni di conferma. Quando si riceve il codice di verifica hello, immetterla nell'hello **immettere il codice di verifica** casella e fare clic su **Accedi**.  
   ![5mfa-verify-2][5]  

Al termine della procedura di verifica, di norma SSMS stabilisce la connessione se le credenziali sono valide e se il firewall lo consente.

## <a name="next-steps"></a>Passaggi successivi

* Per una panoramica dell'autenticazione a più fattori per il database SQL di Azure, vedere [Autenticazione universale con database SQL e SQL Data Warehouse (supporto SSMS per MFA)](sql-database-ssms-mfa-authentication.md).
* Concedere ad altri utenti di accesso database tooyour: [SQL Database autenticazione e autorizzazione: concessione dell'accesso](sql-database-manage-logins.md)  
Verificare che altri utenti possono connettersi tramite firewall hello: [regola firewall di configurare un server a livello di Database SQL di Azure utilizzando hello portale di Azure](sql-database-configure-firewall-settings.md)


[1]: ./media/sql-database-ssms-mfa-auth/1mfa-universal-connect.png
[2]: ./media/sql-database-ssms-mfa-auth/2mfa-sign-in.png
[3]: ./media/sql-database-ssms-mfa-auth/3mfa-setup.png
[4]: ./media/sql-database-ssms-mfa-auth/4mfa-verify-1.png
[5]: ./media/sql-database-ssms-mfa-auth/5mfa-verify-2.png

