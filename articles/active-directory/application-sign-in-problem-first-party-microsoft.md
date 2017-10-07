---
title: accesso tooa applicazione Microsoft aaaProblems | Documenti Microsoft
description: Risolvere i problemi comuni legati all'accesso toofirst parti Microsoft Applications mediante Azure AD (ad esempio Office 365)
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
ms.openlocfilehash: 35849ca8dbaa909d17b6d0da572f5c11041a8559
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
## <a name="problems-signing-in-tooa-microsoft-application"></a>Problemi durante l'accesso tooa applicazione Microsoft

Le applicazioni Microsoft (ad esempio Office 365 Exchange, SharePoint, Yammer e così via) vengono assegnate e gestite in modo leggermente diverso dalle applicazioni SaaS di terza parte o da altre applicazioni che si integrano con Azure AD per Single Sign On.

Esistono tre modi principali che un utente può ottenere accesso tooa applicazione Microsoft pubblicato.

-   Per le applicazioni di Office 365 hello o altri gruppi a pagamento, gli utenti hanno accesso tramite **assegnazione delle licenze** entrambi direttamente tootheir account utente o tramite un gruppo utilizzando la funzionalità di assegnazione in base al gruppo di licenze.

-   Per le applicazioni di Microsoft o una terza parte pubblica liberamente per chiunque toouse, gli utenti possono essere concesso l'accesso tramite **il consenso dell'utente**. This0 significa che toohello applicazione con il proprio account Azure Active Directory aziendale o dell'istituto di istruzione di accesso e che consentono di set di toohave accesso toosome limitata di dati al proprio account.

-   Per le applicazioni di Microsoft o un 3rd Party pubblica liberamente per chiunque toouse, gli utenti possono inoltre essere concesso l'accesso tramite **il consenso dell'amministratore**. Ciò significa che un amministratore ha determinato l'applicazione hello può essere utilizzata da tutti gli utenti nell'organizzazione di hello, in modo toohello applicazione con un account amministratore globale di accesso e concedere l'accesso tooeveryone organizzazione hello.

tootroubleshoot il problema, iniziare con hello [aree problematiche generali con accesso all'applicazione tooconsider](#general-problem-areas-with-application-access-to-consider) e quindi leggere hello [procedura dettagliata: passaggi tootroubleshoot accesso di Microsoft Application](#walkthrough-steps-to-troubleshoot-microsoft-application-access) tooget i dettagli di hello.

## <a name="general-problem-areas-with-application-access-tooconsider"></a>Aree problematiche generali con accesso all'applicazione tooconsider

Di seguito è riportato un elenco di hello aree di problemi generali che è possibile analizzare se si dispone di un'idea di dove toostart, ma è consigliabile leggere hello procedura dettagliata tooget passare rapidamente: [procedura dettagliata: passaggi tootroubleshoot accesso di Microsoft Application](#walkthrough-steps-to-troubleshoot-microsoft-application-access).

-   [Problemi con l'account dell'utente hello](#problems-with-the-users-account)

-   [Problemi relativi ai gruppi](#problems-with-groups)

-   [Problemi relativi ai criteri di accesso condizionale](#problems-with-conditional-access-policies)

-   [Problemi relativi al consenso dell'applicazione](#problems-with-application-consent)

## <a name="steps-tootroubleshoot-microsoft-application-access"></a>Passaggi tootroubleshoot accesso di Microsoft Application

Di seguito sono alcuni problemi comuni eseguire in quando gli utenti possono accedere tooa applicazione Microsoft.

-   Generale problemi toocheck prima

  * Verificare che l'utente hello accede toohello **correggere URL** e non è un URL dell'applicazione locale.

  * Verificare che l'account dell'utente hello è **non bloccato.**

  * Verificare che hello **account utente esista** in Azure Active Directory. [Controllare se esiste un account utente in Azure Active Directory](#problems-with-the-users-account)

  * Verificare che l'account dell'utente hello è **abilitato** per accessi. [Controllare lo stato dell'account di un utente](#problems-with-the-users-account)

  * Assicurarsi che utente hello **password non è scaduta o è stata dimenticata.** [Reimpostare la password di un utente](#reset-a-users-password) o [Abilitare la reimpostazione self-service delle password](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started)

   * Verificare che **Multi-Factor Authentication** non blocchi l'accesso utente. [Controllare lo stato di autenticazione a più fattori di un utente](#check-a-users-multi-factor-authentication-status) o [Controllare le informazioni di contatto per l'autenticazione di un utente](#check-a-users-authentication-contact-info)

   * Verificare che un criterio di **accesso condizionale** o di **protezione delle identità** non blocchi l'accesso utente. [Controllare un criterio specifico di accesso condizionale](#problems-with-conditional-access-policies), [Controllare i criteri di accesso condizionale di un'applicazione specifica](#check-a-specific-applications-conditional-access-policy) o [Disabilitare un criterio specifico di accesso condizionale](#disable-a-specific-conditional-access-policy)

   * Assicurarsi che un utente **informazioni di contatto autenticazione** è toodate tooallow multi-Factor Authentication o l'accesso condizionale criteri toobe applicata. [Controllare lo stato di autenticazione a più fattori di un utente](#check-a-users-multi-factor-authentication-status) o [Controllare le informazioni di contatto per l'autenticazione di un utente](#check-a-users-authentication-contact-info)

-   Per **Microsoft** **le applicazioni che richiedono una licenza** (ad esempio Office 365), ecco alcuni problemi specifici di toocheck dopo aver escluso problemi generali hello precedenti:

   * Garantire hello utente o ha un **assegnata una licenza.** [Controllare le licenze assegnate a un utente](#check-a-users-assigned-licenses) o [Controllare le licenze assegnate a un gruppo](#check-a-groups-assigned-licenses)

   * Se la licenza hello **assegnato tooa** **gruppo statico**, verificare che hello **utente è membro** di tale gruppo. [Controllare le appartenenze ai gruppi di un utente ](#check-a-users-group-memberships)

   * Se la licenza hello **assegnato tooa** **gruppo dinamico**, verificare che hello **regola gruppo dinamico è impostato correttamente**. [Controllare i criteri di appartenenza di un gruppo dinamico](#check-a-dynamic-groups-membership-criteria)

   * Se la licenza hello **assegnato tooa** **gruppo dinamico**, assicurarsi che il gruppo dinamico hello include **al termine dell'elaborazione** l'appartenenza e tale hello **utente è un membro** (può richiedere del tempo). [Controllare le appartenenze ai gruppi di un utente ](#check-a-users-group-memberships)

   *  Una volta che viene assegnata la licenza hello, assicurarsi che la licenza hello è **non scaduto**.

   *  Verificare che la licenza hello è **per un'applicazione hello** a cui accedono.

-   Per **Microsoft** **applicazioni che non richiedono una licenza**, ecco alcuni altri aspetti toocheck:

   * Se è richiesta l'applicazione hello **autorizzazioni a livello utente** (ad esempio "accedere a questa cassetta postale"), assicurarsi che l'utente hello ha effettuato l'accesso dell'applicazione toohello e ha eseguito un **operazione utente a livello di consenso**  toolet un'applicazione hello di accedere ai propri dati.

   * Se è richiesta l'applicazione hello **le autorizzazioni a livello di amministratore** (ad esempio "accedere a postali di utenti tutte le cassette"), assicurarsi che un amministratore globale ha eseguito un **operazione consenso a livello di amministratore in per conto di tutti gli utenti** organizzazione hello.

## <a name="problems-with-hello-users-account"></a>Problemi con l'account dell'utente hello

È possibile bloccare l'accesso all'applicazione a causa di problemi tooa a un utente assegnato toohello applicazione. Di seguito sono riportate alcune soluzioni per i problemi relativi agli utenti e alle impostazioni degli account:

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

  * **Nota**: se un utente si trova in un **applicato** stato, è possibile impostarle troppo**disabilitato** temporaneamente toolet li nuovamente nel proprio account. Una volta in, è possibile modificare il proprio stato troppo**abilitato** nuovamente toorequire li toore la registrazione di informazioni sul contatto durante il successivo accesso. In alternativa, è possibile seguire i passaggi hello hello [informazioni di contatto di autenticazione dell'utente di controllare](#check-a-users-authentication-contact-info) tooverify o set di dati per loro.

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

## <a name="problems-with-groups"></a>Problemi relativi ai gruppi

Accesso all'applicazione può essere bloccata a causa di problemi tooa con un gruppo a cui è assegnato toohello applicazione. Di seguito sono riportate alcune soluzioni per i problemi relativi a gruppi e ad appartenenze a gruppi:

-   [Controllare l'appartenenza di un gruppo](#check-a-groups-membership)

-   [Controllare i criteri di appartenenza di un gruppo dinamico](#check-a-dynamic-groups-membership-criteria)

-   [Controllare le licenze assegnate di un gruppo](#check-a-groups-assigned-licenses)

-   [Rielaborare le licenze di un gruppo](#reprocess-a-groups-licenses)

-   [Assegnare una licenza a un gruppo](#assign-a-group-a-license)

### <a name="check-a-groups-membership"></a>Controllare l'appartenenza di un gruppo

toocheck appartenenza a un gruppo, seguire hello passaggi riportati di seguito:

1.  Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale.**

2.  Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.

3.  Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.

4.  Fare clic su **utenti e gruppi** nel menu di navigazione hello.

5.  Fare clic su **Tutti i gruppi**.

6.  **Ricerca** per gruppo hello si è interessati e **fare clic sulla riga hello** tooselect.

7.  Fare clic su **membri** elenco hello tooreview di utenti assegnati toothis gruppo.

### <a name="check-a-dynamic-groups-membership-criteria"></a>Controllare i criteri di appartenenza di un gruppo dinamico 

toocheck criteri di appartenenza del gruppo dinamico, seguire i passaggi di hello seguenti:

1.  Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale.**

2.  Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.

3.  Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.

4.  Fare clic su **utenti e gruppi** nel menu di navigazione hello.

5.  Fare clic su **Tutti i gruppi**.

6.  **Ricerca** per gruppo hello si è interessati e **fare clic sulla riga hello** tooselect.

7.  Fare clic su **Regole di appartenenza dinamica**.

8.  Hello revisione **semplice** o **avanzate** regola definita per questo gruppo e verificare che tale utente hello da toobe un membro di questo gruppo soddisfa questi criteri.

### <a name="check-a-groups-assigned-licenses"></a>Controllare le licenze assegnate di un gruppo

toocheck un gruppo assegnate le licenze, seguire hello passaggi riportati di seguito:

1.  Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale.**

2.  Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.

3.  Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.

4.  Fare clic su **utenti e gruppi** nel menu di navigazione hello.

5.  Fare clic su **Tutti i gruppi**.

6.  **Ricerca** per gruppo hello si è interessati e **fare clic sulla riga hello** tooselect.

7.  Fare clic su **licenze** toosee quale gruppo di licenze hello è attualmente assegnato.

### <a name="reprocess-a-groups-licenses"></a>Rielaborare le licenze di un gruppo

tooreprocess un gruppo assegnate le licenze, seguire hello passaggi riportati di seguito:

1.  Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale.**

2.  Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.

3.  Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.

4.  Fare clic su **utenti e gruppi** nel menu di navigazione hello.

5.  Fare clic su **Tutti i gruppi**.

6.  **Ricerca** per gruppo hello si è interessati e **fare clic sulla riga hello** tooselect.

7.  Fare clic su **licenze** toosee quale gruppo di licenze hello è attualmente assegnato.

8.  Fare clic su hello **rielaborare** tooensure pulsante che i membri del gruppo di licenze assegnate toothis hello siano aggiornati. L'operazione potrebbe richiedere molto tempo, a seconda delle dimensioni di hello e la complessità del gruppo di hello.

   >[!NOTE]
   >toodo questo più velocemente, è consigliabile temporaneamente assegna una licenza toohello utente direttamente. [Assegnare una licenza a un utente](#problems-with-application-consent).
   >
   >

### <a name="assign-a-group-a-license"></a>Assegnare una licenza a un gruppo

un gruppo di licenze tooa tooassign procedura hello riportata di seguito:

1.  Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale.**

2.  Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.

3.  Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.

4.  Fare clic su **utenti e gruppi** nel menu di navigazione hello.

5.  Fare clic su **Tutti i gruppi**.

6.  **Ricerca** per gruppo hello si è interessati e **fare clic sulla riga hello** tooselect.

7.  Fare clic su **licenze** toosee quale gruppo di licenze hello è attualmente assegnato.

8.  Fare clic su hello **assegnare** pulsante.

9.  Selezionare **uno o più prodotti** dall'elenco di hello dei prodotti disponibili.

10. **Parametro facoltativo** fare clic su hello **opzioni assegnazione** toogranularly elemento assegnare i prodotti. Fare clic su **OK** al termine.

11. Fare clic su hello **assegnare** pulsante tooassign questi toothis di gruppo di licenze. L'operazione potrebbe richiedere molto tempo, a seconda delle dimensioni di hello e la complessità del gruppo di hello.

   >[!NOTE]
   >toodo questo più velocemente, è consigliabile temporaneamente assegna una licenza toohello utente direttamente. [Assegnare una licenza a un utente](#problems-with-application-consent).
   > 
   >

## <a name="problems-with-conditional-access-policies"></a>Problemi relativi ai criteri di accesso condizionale

### <a name="check-a-specific-conditional-access-policy"></a>Selezionare un criterio di accesso condizionale specifico

toocheck o convalidare i criteri di accesso condizionale singolo:

1.  Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale.**

2.  Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.

3.  Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.

4.  Fare clic su **applicazioni aziendali** nel menu di navigazione hello.

5.  Fare clic su hello **accesso condizionale** elemento di navigazione.

6.  Fare clic su criteri hello si è interessati nel controllo.

7.  Verificare che non vi siano condizioni specifiche, assegnazioni o altre impostazioni che possano bloccare l'accesso dell'utente.

   >[!NOTE]
   >È preferibile disabilitare tootemporarily tooensure questo criterio non influisce toodo aggiuntivi sign, hello set **abilitare i criteri di** attivare o disattivare troppo**n** e fare clic su hello **salvare** pulsante .
   >
   >

### <a name="check-a-specific-applications-conditional-access-policy"></a>Controllare i criteri di accesso condizionale di un'applicazione specifica

toocheck o convalidare i criteri di accesso condizionale configurati un'unica applicazione:

1.  Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale.**

2.  Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.

3.  Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.

4.  Fare clic su **applicazioni aziendali** nel menu di navigazione hello.

5.  Fare clic su **Tutte le applicazioni**.

6.  Ricerca per un'applicazione hello si è interessati o hello utente sta tentando di toosign nell'applicazione tooby visualizzare id nome o dell'applicazione.

     >[!NOTE]
     >Se un'applicazione hello si sta cercando non viene visualizzato, fare clic su hello **filtro** pulsante ed espandere ambito hello dell'elenco di hello troppo**tutte le applicazioni**. Se si desidera toosee più colonne, fare clic su hello **colonne** pulsante tooadd dettagli aggiuntivi per le applicazioni.
     >
     >

7.  Fare clic su hello **accesso condizionale** elemento di navigazione.

8.  Fare clic su criteri hello si è interessati nel controllo.

9.  Verificare che non vi siano condizioni specifiche, assegnazioni o altre impostazioni che possano bloccare l'accesso dell'utente.

     >[!NOTE]
     >È preferibile disabilitare tootemporarily tooensure questo criterio non influisce toodo aggiuntivi sign, hello set **abilitare i criteri di** attivare o disattivare troppo**n** e fare clic su hello **salvare** pulsante .
     >
     >

### <a name="disable-a-specific-conditional-access-policy"></a>Disabilitare un criterio di accesso condizionale specifico

toocheck o convalidare i criteri di accesso condizionale singolo:

1.  Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale.**

2.  Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.

3.  Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.

4.  Fare clic su **applicazioni aziendali** nel menu di navigazione hello.

5.  Fare clic su hello **accesso condizionale** elemento di navigazione.

6.  Fare clic su criteri hello si è interessati nel controllo.

7.  Disattivare il criterio di hello impostazione hello **abilitare i criteri di** attivare o disattivare troppo**n** e fare clic su hello **salvare** pulsante.

## <a name="problems-with-application-consent"></a>Problemi relativi al consenso dell'applicazione

È possibile bloccare l'accesso all'applicazione perché non si è verificata l'operazione di consenso hello delle autorizzazioni appropriate. Di seguito sono riportate alcune soluzioni per i problemi relativi al consenso dell'applicazione:

-   [Eseguire un'operazione di consenso a livello di utente](#perform-a-user-level-consent-operation)

-   [Eseguire un'operazione di consenso a livello di amministratore per qualsiasi applicazione](#perform-administrator-level-consent-operation-for-any-application)

-   [Eseguire un'operazione di consenso a livello di amministratore per un'applicazione a tenant singolo](#perform-administrator-level-consent-for-a-single-tenant-application)

-   [Eseguire un'operazione di consenso a livello di amministratore per un'applicazione multi-tenant](#perform-administrator-level-consent-for-a-multi-tenant-application)

### <a name="perform-a-user-level-consent-operation"></a>Eseguire un'operazione di consenso a livello di utente

-   Per qualsiasi applicazione abilitata Open ID connessione che richiede autorizzazioni di accesso dell'applicazione toohello nella schermata di esplorazione esegue un'applicazione di toohello livello di consenso dell'utente per l'utente connesso di hello.

-   Se si desidera toodo questo livello di codice, vedere [che richiede il consenso dell'utente singoli](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#requesting-individual-user-consent).

### <a name="perform-administrator-level-consent-operation-for-any-application"></a>Eseguire un'operazione di consenso a livello di amministratore per qualsiasi applicazione

-   Per **solo le applicazioni sviluppate utilizzando il modello di applicazione hello V1**, è possibile forzare questa toooccur di livello di consenso dell'utente amministratore aggiungendo "**? prompt = admin\_consenso**" toohello fine di un Nell'URL di accesso dell'applicazione.

-   Per **qualsiasi applicazione sviluppata utilizzando il modello di applicazione hello V2**, è possibile applicare questo toooccur amministratore a livello di consenso seguendo le istruzioni di hello in hello **richiedere le autorizzazioni di hello da una directory amministrazione** sezione [endpoint consenso dell'amministratore hello](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint).

### <a name="perform-administrator-level-consent-for-a-single-tenant-application"></a>Eseguire un'operazione di consenso a livello di amministratore per un'applicazione a tenant singolo

-   Per **applicazioni single-tenant** che non richiedono le autorizzazioni (ad esempio quelli di sviluppo o il proprietario dell'organizzazione), è possibile eseguire un **amministrative a livello di consenso** operazione per conto di tutti gli utenti di accedere come amministratore globale e facendo clic su hello **concedere le autorizzazioni** pulsante nella parte superiore di hello di hello **Registro di sistema -&gt; tutte le applicazioni -&gt; selezionare un'App: &gt; Autorizzazioni obbligatorie** blade.

-   Per **qualsiasi applicazione sviluppata utilizzando hello V1 o V2 applicazione**, è possibile applicare questo toooccur amministratore a livello di consenso seguendo le istruzioni di hello in hello **richiedere le autorizzazioni di hello da un l'amministratore di directory** sezione [endpoint consenso dell'amministratore hello](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint).

### <a name="perform-administrator-level-consent-for-a-multi-tenant-application"></a>Eseguire un'operazione di consenso a livello di amministratore per un'applicazione multi-tenant

-   Per le **applicazioni multi-tenant** che richiedono autorizzazioni (ad esempio un'applicazione sviluppata da terza parte o da Microsoft), è possibile eseguire un'operazione di **consenso a livello di amministratore**. Accedere come amministratore globale e facendo clic su hello **concedere le autorizzazioni** pulsante sotto hello **applicazioni aziendali -&gt; tutte le applicazioni -&gt; selezionare un'App -&gt; Autorizzazioni** blade (disponibile non appena).

-   È inoltre possibile applicare questo toooccur amministratore a livello di consenso seguendo le istruzioni di hello in hello **richiedere le autorizzazioni di hello da un amministratore di directory** sezione [endpoint consenso dell'amministratore hello](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint).

## <a name="next-steps"></a>Passaggi successivi
[Hello endpoint consenso dell'amministratore](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint)

