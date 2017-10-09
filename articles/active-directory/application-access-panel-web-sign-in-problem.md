---
title: la firma nel sito Web del Pannello di accesso toohello aaaProblem | Documenti Microsoft
description: Problemi di tootroubleshoot informazioni aggiuntive che possono verificarsi durante il tentativo di toosign in toouse hello Pannello di accesso
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.reviwer: japere
ms.openlocfilehash: 1037f7c5fbaa9425760ad5739b383c716d5fc3a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="problem-signing-in-toohello-access-panel-website"></a>Problema di accesso sito Web del Pannello di accesso toohello

Hello Pannello di accesso è un portale basato sul web che consente un utente che ha un lavoro o scuola account in Azure Active Directory (Azure AD) tooview e avviare basato su cloud applicazioni che amministratore hello Azure AD ha concesso l'accesso a. Un utente con le edizioni di Azure AD consente inoltre di gruppi self-service e funzionalità di gestione di app tramite hello Pannello di accesso. Hello Pannello di accesso è separato dal portale di Azure hello e non richiede agli utenti toohave una sottoscrizione di Azure.

Gli utenti possono accedere toohello Pannello di accesso se hanno un account aziendale o dell'istituto di istruzione in Azure AD.

-   Gli utenti possono essere autenticati direttamente tramite Azure AD.

-   Gli utenti possono essere autenticati tramite Active Directory Federation Services (AD FS).

-   Gli utenti possono essere autenticati tramite Windows Server Active Directory.

Se un utente dispone di una sottoscrizione per Azure o Office 365 e ha utilizzato hello portale di Azure o un'applicazione di Office 365, saranno in grado di toouse hello facilmente Pannello di accesso senza la necessità di toosign in nuovamente. Gli utenti non autenticati in toosign richiesta in utilizzando hello username e password per il proprio account in Azure AD. Se l'organizzazione hello è configurata la federazione, digitare il nome utente hello è sufficiente.

## <a name="general-issues-toocheck-first"></a>Generale problemi toocheck prima 

-   Verificare che l'utente hello accede toohello **correggere URL**: <https://myapps.microsoft.com>

-   Assicurarsi che il browser dell'utente hello sia aggiunto hello URL tooits **siti attendibili**

-   Verificare che l'account dell'utente hello è **abilitato** per accessi.

-   Verificare che l'account dell'utente hello è **non bloccato.**

-   Assicurarsi che utente hello **password non è scaduta o è stata dimenticata.**

-   Verificare che **Multi-Factor Authentication** non blocchi l'accesso utente.

-   Verificare che un criterio di **accesso condizionale** o di **protezione delle identità** non blocchi l'accesso utente.

-   Assicurarsi che un utente **informazioni di contatto autenticazione** è toodate tooallow multi-Factor Authentication o l'accesso condizionale criteri toobe applicata.

-   Verificare che tooalso try cancellare i cookie del browser e riprovare toosign in.

## <a name="meeting-browser-requirements-for-hello-access-panel"></a>Requisiti del browser per hello Pannello di accesso

Pannello di accesso Hello richiede un browser che supporta JavaScript e CSS sono state abilitate. toouse basato su password single sign-on (SSO nel Pannello di accesso, hello estensione del Pannello di accesso hello) deve essere installato nel browser dell'utente hello. Questa estensione viene scaricata automaticamente quando un utente seleziona un'applicazione configurata per il servizio Single Sign-On basato su password.

Per SSO basato su password, browser dell'utente finale di hello può essere:

-   Internet Explorer 8, 9, 10, 11 su Windows 7 o versioni successive

-   Edge su Windows 10 Anniversary Edition o versioni successive 

-   Chrome in Windows 7 o versione successiva e MacOS X o versione successiva

-   Firefox 26.0 o versione successiva in Windows XP SP2 o versione successiva e in Mac OS X 10.6 o versione successiva


## <a name="problems-with-hello-users-account"></a>Problemi con l'account dell'utente hello

Accesso toohello Pannello di accesso può essere bloccata a causa di problemi di tooa hello account utente. Di seguito sono riportate alcune soluzioni per i problemi relativi agli utenti e alle impostazioni degli account:

-   [Controllare se esiste un account utente in Azure Active Directory](#check-if-a-user-account-exists-in-azure-active-directory)

-   [Controllare lo stato dell'account di un utente](#check-a-users-account-status)

-   [Reimpostare la password di un utente](#reset-a-users-password)

-   [Abilitare la reimpostazione self-service delle password](#enable-self-service-password-reset)

-   [Controllare lo stato di autenticazione a più fattori di un utente](#check-a-users-multi-factor-authentication-status)

-   [Controllare le informazioni di contatto per l'autenticazione di un utente](#check-a-users-authentication-contact-info)

-   [Controllare le appartenenze ai gruppi di un utente ](#check-a-users-group-memberships)

-   [Controllare le licenze assegnate di un utente](#check-a-users-assigned-licenses)

-   [Assegnare una licenza a un utente](#assign-a-user-a-license)

### <a name="check-if-a-user-account-exists-in-azure-active-directory"></a>Controllare se esiste un account utente in Azure Active Directory

Se è presente, un account utente di toocheck procedura hello riportata di seguito:

1.  Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale.**

2.  Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.

3.  Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.

4.  Fare clic su **utenti e gruppi** nel menu di navigazione hello.

5.  Fare clic su **Tutti gli utenti**.

6.  **Ricerca** per utente hello si è interessati e **fare clic sulla riga hello** tooselect.

7.  Controllare la proprietà hello di hello utente oggetto toobe assicurarsi che vengano visualizzate come previsto e che nessun dato è manca.

### <a name="check-a-users-account-status"></a>Controllare lo stato dell'account di un utente

di toocheck un utente stato dell'account, attenersi alla procedura hello riportata di seguito:

1.  Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale.**

2.  Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.

3.  Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.

4.  Fare clic su **utenti e gruppi** nel menu di navigazione hello.

5.  Fare clic su **Tutti gli utenti**.

6.  **Ricerca** per utente hello si è interessati e **fare clic sulla riga hello** tooselect.

7.  Fare clic su **Profilo**.

8.  In **impostazioni** assicurarsi che **blocco Accedi** è troppo**n**.

### <a name="reset-a-users-password"></a>Reimpostare la password di un utente

tooreset una password, seguire hello passaggi riportati di seguito:

1.  Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale.**

2.  Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.

3.  Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.

4.  Fare clic su **utenti e gruppi** nel menu di navigazione hello.

5.  Fare clic su **Tutti gli utenti**.

6.  **Ricerca** per utente hello si è interessati e **fare clic sulla riga hello** tooselect.

7.  Fare clic su hello **reimpostazione password** pulsante nella parte superiore di hello del Pannello di utente hello.

8.  Fare clic su hello **reimpostazione password** pulsante hello **reimpostazione password** pannello visualizzato.

9.  Hello copia **password temporanea** o **immettere una nuova password** per utente hello.

10. Comunicare il nuovo utente toohello password, essere necessario toochange questa password durante il successivo accesso tooAzure Active Directory.

### <a name="enable-self-service-password-reset"></a>Abilitare la reimpostazione self-service delle password

password self-service tooenable reimpostare, attenersi alla procedura di distribuzione hello seguente:

-   [Abilitare gli utenti tooreset le password di Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started#enable-users-to-reset-their-azure-ad-passwords)

-   [Abilitare gli utenti tooreset o modificare le password di Active Directory locale](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started#enable-users-to-reset-or-change-their-ad-passwords)

### <a name="check-a-users-multi-factor-authentication-status"></a>Controllare lo stato di autenticazione a più fattori di un utente

toocheck un utente di multi-factor lo stato di autenticazione, seguire hello passaggi riportati di seguito:

1.  Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale.**

2.  Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.

3.  Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.

4.  Fare clic su **utenti e gruppi** nel menu di navigazione hello.

5.  Fare clic su **Tutti gli utenti**.

6.  Fare clic su hello **multi-Factor Authentication** pulsante nella parte superiore di hello del pannello hello.

7.  Una volta hello **portale di amministrazione di multi-Factor Authentication** carichi, verificare che trovano in hello **utenti** scheda.

8.  Trovare utente hello elenco hello degli utenti, la ricerca, filtro o l'ordinamento.

9.  Utente selezionare hello hello elenco di utenti e **abilitare**, **disabilitare**, o **Imponi** autenticazione a più fattori in base alle esigenze.

   >[!NOTE]
   >Se un utente si trova in un **applicato** stato, è possibile impostarle troppo**disabilitato** temporaneamente toolet li nuovamente nel proprio account. Una volta in, è possibile modificare il proprio stato troppo**abilitato** nuovamente toorequire li toore la registrazione di informazioni sul contatto durante il successivo accesso. In alternativa, è possibile seguire i passaggi hello hello [informazioni di contatto di autenticazione dell'utente di controllare](#check-a-users-authentication-contact-info) tooverify o set di dati per loro.
   >
   >

### <a name="check-a-users-authentication-contact-info"></a>Controllare le informazioni di contatto per l'autenticazione di un utente

informazioni utilizzate per multi-factor authentication, l'accesso condizionale, la protezione dell'identità e la reimpostazione della Password, contattare l'autenticazione dell'utente toocheck procedura hello riportata di seguito:

1.  Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale.**

2.  Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.

3.  Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.

4.  Fare clic su **utenti e gruppi** nel menu di navigazione hello.

5.  Fare clic su **Tutti gli utenti**.

6.  **Ricerca** per utente hello si è interessati e **fare clic sulla riga hello** tooselect.

7.  Fare clic su **Profilo**.

8.  Scorrere verso il basso troppo**informazioni di contatto autenticazione**.

9.  **Revisione** dati hello registrati per utente hello e aggiornare in base alle esigenze.

### <a name="check-a-users-group-memberships"></a>Controllare le appartenenze a gruppi dell'utente

di toocheck un utente appartenenza ai gruppi, attenersi alla procedura hello riportata di seguito:

1.  Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale.**

2.  Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.

3.  Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.

4.  Fare clic su **utenti e gruppi** nel menu di navigazione hello.

5.  Fare clic su **Tutti gli utenti**.

6.  **Ricerca** per utente hello si è interessati e **fare clic sulla riga hello** tooselect.

7.  Fare clic su **gruppi** toosee gruppi utente hello è membro.

### <a name="check-a-users-assigned-licenses"></a>Controllare le licenze assegnate di un utente

toocheck un utente assegnate le licenze, seguire hello passaggi riportati di seguito:

1.  Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale.**

2.  Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.

3.  Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.

4.  Fare clic su **utenti e gruppi** nel menu di navigazione hello.

5.  Fare clic su **Tutti gli utenti**.

6.  **Ricerca** per utente hello si è interessati e **fare clic sulla riga hello** tooselect.

7.  Fare clic su **licenze** toosee utente hello licenze è attualmente assegnato.

### <a name="assign-a-user-a-license"></a>Assegnare una licenza a un utente 

un utente, tooa licenza tooassign procedura hello riportata di seguito:

1.  Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale.**

2.  Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.

3.  Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.

4.  Fare clic su **utenti e gruppi** nel menu di navigazione hello.

5.  Fare clic su **Tutti gli utenti**.

6.  **Ricerca** per utente hello si è interessati e **fare clic sulla riga hello** tooselect.

7.  Fare clic su **licenze** toosee utente hello licenze è attualmente assegnato.

8.  Fare clic su hello **assegnare** pulsante.

9.  Selezionare **uno o più prodotti** dall'elenco di hello dei prodotti disponibili.

10. **Parametro facoltativo** fare clic su hello **opzioni assegnazione** toogranularly elemento assegnare i prodotti. Fare clic su **OK** al termine.

11. Fare clic su hello **assegnare** pulsante tooassign questi utente toothis licenze.

## <a name="if-these-troubleshooting-steps-do-not-resolve-hello-issue"></a>Se i passaggi di risoluzione dei problemi non risolvono il problema di hello

Aprire un ticket di supporto con hello se disponibili le seguenti informazioni:

-   ID errore di correlazione

-   UPN (indirizzo di posta elettronica dell'utente)

-   ID tenant

-   Tipo di browser

-   Fuso orario e ora o intervallo di tempo durante il quale si verifica l'errore

-   Tracce Fiddler

## <a name="next-steps"></a>Passaggi successivi
[Fornire le applicazioni single sign-on tooyour con Proxy dell'applicazione](active-directory-application-proxy-sso-using-kcd.md)
