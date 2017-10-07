---
title: aaaAuthentication e le autorizzazioni utente in Azure Analysis Services | Documenti Microsoft
description: Informazioni sull'autenticazione e le autorizzazioni utente in Azure Analysis Services.
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: dd49fd59eec1f68dfe8a0fe373fa612ac46de4e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="authentication-and-user-permissions"></a>Autenticazione e autorizzazioni utente
Azure Analysis Services usa Azure Active Directory (Azure AD) per la gestione delle identità e l'autenticazione degli utenti. Qualsiasi utente che crea, la gestione, o connessione tooan Azure Analysis Services server deve avere un'identità utente valida un [tenant di Azure AD](../active-directory/active-directory-administer.md) in hello stessa sottoscrizione.

Azure Analysis Services supporta la [collaborazione B2B di Azure AD](../active-directory/active-directory-b2b-what-is-azure-ad-b2b.md). Con B2B, gli utenti esterni all'organizzazione possono essere invitati come utenti guest in una directory di Azure AD. Gli utenti guest possono appartenere a un'altra directory di tenant di Azure AD o a qualsiasi indirizzo e-mail valido. Una volta invitati e utente hello accetta hello invito inviato tramite posta elettronica da Azure, hello identità utente viene aggiunto toohello directory del tenant. Le identità possono essere aggiunti gruppi toosecurity o come membri di un ruolo di amministratore o un database del server.

![Architettura dell'autenticazione di Azure Analysis Services](./media/analysis-services-manage-users/aas-manage-users-arch.png)

## <a name="authentication"></a>Autenticazione
Tutti gli strumenti e applicazioni client di utilizzano uno o più di Analysis Services hello [librerie client](analysis-services-data-providers.md) (AMO, MSOLAP, ADOMD) tooconnect tooa server. 

Queste tre librerie client supportano sia il flusso interattivo di Azure AD sia i metodi di autenticazione non interattivi. Hello due metodi non interattivo, la Password di Active Directory e l'autenticazione integrata di Active Directory possono essere utilizzati nelle applicazioni che utilizzano AMOMD e MSOLAP. Questi due metodi non aprono mai finestre di dialogo popup.

Le applicazioni client quali Excel e Power BI Desktop e strumenti come SQL Server Management Studio e SSDT installano versioni più recenti di hello delle librerie di hello quando aggiornata la versione più recente di toohello. Power BI Desktop, SQL Server Management Studio e SQL Server Data Tools vengono aggiornati ogni mese. Excel viene [aggiornato con Office 365](https://support.office.com/en-us/article/When-do-I-get-the-newest-features-in-Office-2016-for-Office-365-da36192c-58b9-4bc9-8d51-bb6eed468516). Gli aggiornamenti di Office 365 sono meno frequenti, alcune organizzazioni utilizzano channel posticipata hello e posticipati significato aggiornamenti dei mesi toothree.

 A seconda dell'applicazione client hello o strumento in uso, il tipo di hello di autenticazione e la modalità accesso potrebbe essere diverso. Ogni applicazione può supportano funzionalità diverse per la connessione a servizi toocloud come Azure Analysis Services.


### <a name="sql-server-management-studio-ssms"></a>SQL Server Management Studio (SSMS)
I server di Azure Analysis Services supportano connessioni da [SSMS V17.1](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) e versioni successive usando l'autenticazione di Windows, l'autenticazione della password di Active Directory e l'autenticazione universale di Active Directory. In generale, è consigliabile usare l'autenticazione universale di Active Directory per i motivi indicati di seguito:

*  Supporta i metodi autenticazione interattiva e non interattiva.

*  Supporta gli utenti guest di Azure B2B invitati nel tenant di Azure AS hello. Durante la connessione server tooa, gli utenti guest necessario selezionare l'autenticazione universale di Active Directory durante la connessione server toohello.

*  Supporta l'autenticazione a più fattori (Multi-Factor Authentication, MFA). Azure MFA consente di salvaguardare toodata di accesso e le applicazioni con una gamma di opzioni di verifica: telefonata, SMS, le smart card con pin, o la notifica dell'app mobile. La convalida di MFA interattiva con Azure AD può avvenire attraverso una finestra popup.

### <a name="sql-server-data-tools-ssdt"></a>SQL Server Data Tools (SSDT)
SSDT consente di connettersi utilizzando l'autenticazione universale di Active Directory con il supporto di MFA tooAzure Analysis Services. Gli utenti sono richieste toosign in tooAzure nella prima distribuzione hello utilizzando l'ID organizzativo (posta elettronica). Gli utenti devono accedere in tooAzure con un account con autorizzazioni di amministratore di server che esegue la distribuzione in server hello. Quando si accede in hello tooAzure prima volta, viene assegnato un token. SSDT memorizza nella cache di hello token in memoria per riconnessioni future.

### <a name="power-bi-desktop"></a>Power BI Desktop
Power BI Desktop si connette utilizzando l'autenticazione universale di Active Directory con il supporto di MFA tooAzure Analysis Services. Gli utenti sono richieste toosign in tooAzure sulla connessione prima di hello utilizzando l'ID organizzativo (posta elettronica). Gli utenti devono accedere tooAzure con un account che è incluso in un amministratore del server o ruolo del database.

### <a name="excel"></a>Excel
Gli utenti di Excel possono connettersi tooa server utilizzando un account di Windows, un ID organizzazione (indirizzo di posta elettronica) o un indirizzo di posta elettronica esterni. Identità di posta elettronica esterni devono esistere in hello Azure AD come utente guest.

## <a name="user-permissions"></a>Autorizzazioni utente

**Gli amministratori del server** sono tooan specifica istanza del server Azure Analysis Services. Si connettono con strumenti quali il portale di Azure, SQL Server Management Studio e SSDT tooperform attività quali l'aggiunta di database e la gestione dei ruoli utente. Per impostazione predefinita, utente hello che crea server hello viene automaticamente aggiunto come un amministratore del server Analysis Services. È possibile aggiungere altri amministratori tramite il portale di Azure o SSMS. Gli amministratori del server devono avere un account nel tenant di Azure AD hello in hello stessa sottoscrizione. vedere, più toolearn [gestire gli amministratori di server](analysis-services-server-admins.md). 


**Gli utenti del database** connessione database toomodel tramite applicazioni client quali Excel o Power BI. Gli utenti devono essere aggiunti toodatabase ruoli. I ruoli database definiscono l'amministratore, il processo o le autorizzazioni di lettura per un database. È importante toounderstand gli utenti del database in un ruolo con autorizzazioni di amministratore è diverso rispetto agli amministratori di server. Per impostazione predefinita, tuttavia, gli amministratori del server sono anche amministratori del database. vedere, più toolearn [gestire utenti e ruoli del database](analysis-services-database-users.md).

**Proprietari delle risorse di Azure**. I proprietari delle risorse gestiscono le risorse di una sottoscrizione di Azure. I proprietari di risorse possono aggiungere tooOwner identità utente di Azure AD o collaboratore ruoli all'interno di una sottoscrizione utilizzando **il controllo degli accessi** nel portale di Azure o con i modelli di gestione risorse di Azure. 

![Controllo di accesso nel portale di Azure](./media/analysis-services-manage-users/aas-manage-users-rbac.png)

Ruoli a questo livello si applicano toousers o gli account che richiedono attività tooperform che può essere completata nel portale di hello o utilizzando i modelli di gestione risorse di Azure. vedere, più toolearn [Role-Based Access Control](../active-directory/role-based-access-control-what-is.md). 


## <a name="database-roles"></a>Ruoli del database

 I ruoli definiti per un modello tabulare sono ruoli del database, Ovvero, i ruoli di hello contengono membri costituiti da utenti di Azure AD e i gruppi di sicurezza che dispongono di autorizzazioni specifiche che definiscono l'azione di hello tali membri possono richiedere su un database modello. Un ruolo del database viene creato come oggetto separato nel database di hello e si applica solo toohello database in cui è stato creato.   
  
 Per impostazione predefinita, quando si crea un nuovo progetto di modello tabulare, il progetto di modello hello non dispone di alcun ruolo. I ruoli possono essere definiti utilizzando la finestra di dialogo Gestione ruoli di hello in SSDT. Quando i ruoli vengono definiti durante la progettazione di modelli di progetto, vengono applicati toohello solo modello di database dell'area di lavoro. Quando viene distribuito il modello di hello, hello stessi ruoli vengono applicati toohello distribuito modello. Dopo la distribuzione di un modello, gli amministratori del server e del database possono gestire ruoli e membri tramite SSMS. vedere, più toolearn [gestire utenti e ruoli del database](analysis-services-database-users.md).
  


## <a name="next-steps"></a>Passaggi successivi

[Gestire accesso tooresources con gruppi di Azure Active Directory](../active-directory/active-directory-manage-groups.md)   
[Gestire ruoli e utenti del database](analysis-services-database-users.md)  
[Gestire gli amministratori di server](analysis-services-server-admins.md)  
[Controllo degli accessi in base al ruolo](../active-directory/role-based-access-control-what-is.md)  