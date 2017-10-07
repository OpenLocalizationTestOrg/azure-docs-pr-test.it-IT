---
title: aaaMicrosoft stati utente di Azure multi-Factor Authentication
description: Informazioni sugli stati utente in Azure MFA.
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 0b9fde23-2d36-45b3-950d-f88624a68fbd
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: cf5b977b09d09330b7b3bc668abd79e602d62015
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toorequire-two-step-verification-for-a-user-or-group"></a>La verifica in due passaggi toorequire per un utente o gruppo

Sono disponibili due modi per richiedere la verifica in due passaggi. Hello prima opzione è tooenable ogni singolo utente per Azure multi-Factor Authentication (MFA). Quando gli utenti vengono abilitati singolarmente, eseguono sempre la verifica in due passaggi (con alcune eccezioni, ad esempio, quando effettuano l'accesso da indirizzi IP attendibili o se hello memorizzate dispositivi funzionalità è attivata). seconda opzione Hello è tooset un criterio di accesso condizionale che richiede la verifica in determinate condizioni.

>[!TIP] 
>Scegliere uno di questi metodi toorequire in due passaggi la verifica, non entrambi. L'abilitazione di un utente per Azure MFA sostituisce infatti eventuali criteri di accesso condizionale.

## <a name="which-option-is-right-for-you"></a>Scelta dell'opzione più adatta alle proprie esigenze

**L'abilitazione di autenticazione a più fattori di Azure, modificare stati utente** è hello approccio tradizionale per la richiesta di verifica in due passaggi. Funziona con entrambi Azure MFA nel cloud hello e Server di autenticazione a più fattori di Azure. Tutti gli utenti di hello che abiliti hanno hello stessa esperienza, si verifica in due passaggi tooperform ogni volta che effettuano l'accesso. L'abilitazione di un utente sostituisce eventuali criteri di accesso condizionale in vigore per l'utente. 

L'**abilitazione di Azure MFA con criteri di accesso condizionale** è un approccio più flessibile per richiedere la verifica in due passaggi. Funzionano solo per Azure MFA nel cloud hello, tuttavia, e l'accesso condizionale è un [a pagamento di funzionalità di Azure Active Directory](https://www.microsoft.com/cloud-platform/azure-active-directory-features). È possibile creare criteri di accesso condizionale che si applicano toogroups, nonché a singoli utenti. È possibile, ad esempio, assegnare ai gruppi ad alto rischio più restrizioni rispetto ai gruppi a basso rischio oppure richiedere la verifica in due passaggi solo per le app cloud ad alto rischio e non per quelle a basso rischio. 

Entrambe le opzioni richiesto tooregister gli utenti per hello Azure multi-Factor Authentication prima volta che accedono dopo requisiti hello è attivato. Entrambe le opzioni funzionano anche con hello configurabile [le impostazioni di Azure multi-Factor Authentication](multi-factor-authentication-whats-next.md)

## <a name="enable-azure-mfa-by-changing-user-status"></a>Abilitare Azure MFA modificando lo stato utente

Gli account utente in Azure multi-Factor Authentication hanno hello seguenti tre stati distinti:

| Stato | Descrizione | App interessate non basate su browser |
|:---:|:---:|:---:|
| Disabled |stato di Hello predefinito per un nuovo utente non registrato Azure multi-Factor Authentication (MFA). |No |
| Enabled |utente Hello è stato registrato in Azure MFA, ma non è registrato. Sarà richiesta tooregister hello successivo che accesso. |No.  Toowork continuerà fino a quando non viene completato il processo di registrazione hello. |
| Enforced |utente Hello è stato registrato e ha completato il processo di registrazione hello per Azure MFA. |Sì.  Le app richiedono password per le app. |

Stato di un utente riflette se un amministratore iscritti li in Azure MFA e se si è stato completato il processo di registrazione hello.

Tutti gli utenti iniziano con *disabilitato*. Quando si registrano gli utenti in Azure MFA, il relativo stato cambia in *abilitato*. Quando gli utenti abilitati l'accesso e completare il processo di registrazione hello, il relativo stato viene modificato troppo*applicati*.  

### <a name="view-hello-status-for-a-user"></a>Visualizzare lo stato di hello per un utente

Dopo la pagina in cui è possibile visualizzare e gestire gli stati utente di passaggi tooaccess hello hello di utilizzo:

1. Accedi toohello [portale di Azure](https://portal.azure.com) come amministratore.
2. Andare troppo**Azure Active Directory** > **utenti e gruppi** > **tutti gli utenti**.
3. Selezionare **Multi-Factor Authentication**.
   ![Selezionare Multi-Factor Authentication](./media/multi-factor-authentication-get-started-user-states/selectmfa.png)
4. Verrà visualizzata una nuova pagina che visualizza gli stati utente hello.
   ![Stati utente in Microsoft Azure Multi-Factor Authentication - screenshot](./media/multi-factor-authentication-get-started-user-states/userstate1.png)

### <a name="change-hello-status-for-a-user"></a>Modificare lo stato di hello per un utente

1. Utilizzare hello che precede la pagina utenti passaggi tooget toohello multi-factor authentication.
2. Trova hello utente che si desidera tooenable per Azure MFA. Potrebbe essere necessario toochange hello visualizzazione nella parte superiore di hello. 
   ![Trova utente - screenshot](./media/multi-factor-authentication-get-started-cloud/enable1.png)
3. Controllare nome tootheir successivo di hello casella.
4. Sulla destra, nella casella rapide hello, scegliere **abilitare** o **disabilitare**.
   ![Abilitare l'utente selezionato - screenshot](./media/multi-factor-authentication-get-started-cloud/user1.png)

   >[!TIP]
   >*Abilitato* automaticamente gli utenti passano troppo*applicati* quando si registra per Azure MFA. È non devono modificare manualmente hello utente stato tooenforced. 

5. Confermare la selezione nella finestra popup di hello visualizzata. 

È consigliabile inviare una notifica tramite posta elettronica agli utenti dopo averli abilitati. Segnalando che verranno richieste tooregister hello successivo che accesso. Inoltre, se l'organizzazione Usa le app non basate su browser che non supportano l'autenticazione moderna, sarà necessario toocreate le password dell'app. È inoltre possibile includere un collegamento di tooour [Guida dell'utente finale di Azure MFA](./end-user/multi-factor-authentication-end-user.md) toohelp loro introduzione.

### <a name="use-powershell"></a>Usare PowerShell
toochange hello utente lo stato dello stato utilizzando [Azure AD PowerShell](/powershell/azure/overview), modificare `$st.State`. Esistono tre possibili stati:

* Enabled
* Enforced
* Disabled  

Non spostare gli utenti direttamente toohello *applicato* stato. Applicazioni basate su browser non terminerà utente hello non ha effettuato la registrazione di autenticazione a più fattori e ottenuto una [password di app](multi-factor-authentication-whats-next.md#app-passwords). 

Utilizzo di PowerShell è una scelta ottimale quando è necessario toobulk consentendo agli utenti. Creare uno script di PowerShell che scorra un intero elenco di utenti e li abiliti:

        $st = New-Object -TypeName Microsoft.Online.Administration.StrongAuthenticationRequirement
        $st.RelyingParty = "*"
        $st.State = “Enabled”
        $sta = @($st)
        Set-MsolUser -UserPrincipalName bsimon@contoso.com -StrongAuthenticationRequirements $sta

Di seguito è fornito un esempio:

    $users = "bsimon@contoso.com","jsmith@contoso.com","ljacobson@contoso.com"
    foreach ($user in $users)
    {
        $st = New-Object -TypeName Microsoft.Online.Administration.StrongAuthenticationRequirement
        $st.RelyingParty = "*"
        $st.State = “Enabled”
        $sta = @($st)
        Set-MsolUser -UserPrincipalName $user -StrongAuthenticationRequirements $sta
    }

## <a name="enable-azure-mfa-with-a-conditional-access-policy"></a>Abilitare Azure MFA con criteri di accesso condizionale

L'accesso condizionale è una funzionalità a pagamento di Azure Active Directory caratterizzata da numerose opzioni di configurazione. Questa procedura illustra un modo toocreate un criterio. Per altre informazioni, vedere [Accesso condizionale in Azure Active Directory](../active-directory/active-directory-conditional-access-azure-portal.md).

1. Accedi toohello [portale di Azure](https://portal.azure.com) come amministratore.
2. Andare troppo**Azure Active Directory** > **accesso condizionale**.
3. Selezionare **Nuovi criteri**.
4. In **Assegnazioni** selezionare **Utenti e gruppi**. Hello utilizzare **Include** e **escludere** schede toospecify quali utenti e gruppi verranno gestiti da criteri hello.
5. In **Assegnazioni** selezionare **App cloud**. Scegliere tooinclude **tutte le app cloud**.
6. In **Controlli di accesso** selezionare **Concedi**. Selezionare **Richiedi autenticazione a più fattori**.
7. Attivare **abilitare i criteri di** troppo**su** e quindi selezionare **salvare**.

Hello altre opzioni di criteri di accesso condizionale hello consentono toospecify esattamente quando si verifica in due passaggi deve essere obbligatorio. Ad esempio, è possibile creare un criterio che specifichi: quando terzisti tentano tooaccess nostra app approvvigionamento da reti non attendibili nei dispositivi che non sono aggiunti a un dominio, richiedere la verifica in due passaggi. 

## <a name="next-steps"></a>Passaggi successivi

- Suggerimenti su hello [procedure consigliate per l'accesso condizionale](../active-directory/active-directory-conditional-access-best-practices.md)

- Gestire le impostazioni di Multi-Factor Authentication per [utenti e dispositivi](multi-factor-authentication-manage-users-and-devices.md)