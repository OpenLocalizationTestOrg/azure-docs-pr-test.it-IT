---
title: aaaAzure attivo B2B Directory API di collaborazione e la personalizzazione | Documenti Microsoft
description: "Collaborazione B2B di Active Directory di Azure supporta le relazioni tra società consentendo a partner commerciali tooselectively l'accesso alle applicazioni aziendali"
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 04/11/2017
ms.author: sasubram
ms.openlocfilehash: 2609971ffa5d2ebc9466c61f4e4af11f5b045ecb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2b-collaboration-api-and-customization"></a>API e personalizzazione per Collaborazione B2B di Azure Active Directory

Molti clienti abbiamo prodotto segnalare che desiderano toocustomize processo di invito hello in modo ottimale per le organizzazioni. Con l'API, è possibile farlo. [https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation)

## <a name="capabilities-of-hello-invitation-api"></a>Funzionalità di invito hello API
Hello API offre hello seguenti funzionalità:

1. Invitare un utente esterno con *qualsiasi* indirizzo di posta elettronica.

    ```
    "invitedUserDisplayName": "Sam"
    "invitedUserEmailAddress": "gsamoogle@gmail.com"
    ```

2. Personalizzare in cui si desidera il tooland utenti dopo che accettino le invito.

    ```
    "inviteRedirectUrl": "https://myapps.microsoft.com/"
    ```

3. Scegliere posta elettronica di invito standard hello toosend tramite us

    ```
    "sendInvitationMessage": true
    ```

  con un destinatario che è possibile personalizzare toohello

    ```
    "customizedMessageBody": "Hello Sam, let's collaborate!"
    ```

4. Scegliere toocc: i partecipanti tookeep in hello ciclo su questo collaboratore l'invito.

5. O personalizzare completamente l'invito e flusso di lavoro caricamento scegliendo non toosend notifiche tramite Azure AD.

    ```
    "sendInvitationMessage": false
    ```

  In questo caso, verrà restituito un URL di rimborso da hello API che è possibile incorporare in un modello di posta elettronica, messaggi immediati o altro metodo di distribuzione di propria scelta.

6. Infine, se si è un amministratore, è possibile scegliere utente hello tooinvite come membro.

    ```
    "invitedUserType": "Member"
    ```


## <a name="authorization-model"></a>Modello di autorizzazione
Hello API può essere eseguito in hello seguenti modalità di autorizzazione:

### <a name="app--user-mode"></a>Modalità app + utente
In questo modo, quando ci si accinge utilizza hello API esigenze toohave hello autorizzazioni toobe creare inviti B2B.

### <a name="app-only-mode"></a>Modalità solo app
Nel contesto solo app, app hello deve hello User.ReadWrite.All o Directory.ReadWrite.All ambiti per toosucceed invito hello.

Per altre informazioni, vedere https://graph.microsoft.io/docs/authorization/permission_scopes


## <a name="powershell"></a>PowerShell
È ora possibile toouse PowerShell tooadd e invita gli utenti esterni tooan organizzazione facilmente. Creare un invito tramite i cmdlet di hello:

```
New-AzureADMSInvitation
```

È possibile utilizzare hello le opzioni seguenti:

* -InvitedUserDisplayName
* -InvitedUserEmailAddress
* -SendInvitationMessage
* -InvitedUserMessageInfo

È inoltre possibile estrarre riferimento invito API hello in [https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation)

## <a name="next-steps"></a>Passaggi successivi

Vedere gli altri articoli su Azure AD B2B Collaboration.

* [Che cos'è Azure AD B2B Collaboration?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [Procedura per aggiungere utenti di Collaborazione B2B ad Azure Active Directory da parte degli amministratori](active-directory-b2b-admin-add-users.md)
* [Procedura per aggiungere utenti di Collaborazione B2B da parte di Information Worker](active-directory-b2b-iw-add-users.md)
* [elementi Hello di posta elettronica di invito collaborazione B2B di hello](active-directory-b2b-invitation-email.md)
* [Riscatto dell'invito di Collaborazione B2B](active-directory-b2b-redemption-experience.md)
* [Licenze per la Collaborazione B2B di Azure AD](active-directory-b2b-licensing.md)
* [Risoluzione dei problemi di Collaborazione B2B di Azure Active Directory](active-directory-b2b-troubleshooting.md)
* [Domande frequenti su Collaborazione B2B di Azure Active Directory](active-directory-b2b-faq.md)
* [Autenticazione a più fattori per utenti di Collaborazione B2B](active-directory-b2b-mfa-instructions.md)
* [Aggiungere gli utenti per la Collaborazione B2B senza un invito](active-directory-b2b-add-user-without-invite.md)
* [Indice di articoli per la gestione di applicazioni in Azure Active Directory](active-directory-apps-index.md)
