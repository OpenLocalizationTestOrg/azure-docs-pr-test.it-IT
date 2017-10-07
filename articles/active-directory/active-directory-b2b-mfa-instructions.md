---
title: l'accesso per gli utenti di collaborazione B2B di Azure Active Directory aaaConditional | Documenti Microsoft
description: Collaborazione B2B di Active Directory di Azure supporta multi-factor authentication (MFA) per applicazioni aziendali di accesso selettivo tooyour
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
ms.date: 05/24/2017
ms.author: sasubram
ms.openlocfilehash: 3a05be4393f74ff8e87f32432a222a5fbac9af62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="conditional-access-for-b2b-collaboration-users"></a>Accesso condizionale per gli utenti di Collaborazione B2B

## <a name="multi-factor-authentication-for-b2b-users"></a>Autenticazione a più fattori per gli utenti B2B
Con Collaborazione B2B di Azure AD, le organizzazioni possono applicare criteri di autenticazione a più fattori (MFA) per gli utenti B2B. Questi criteri possono essere applicati al tenant di hello, app o il livello di singolo utente, hello allo stesso modo che sono abilitate per i dipendenti a tempo pieno e i membri dell'organizzazione hello. Criteri di autenticazione a più fattori vengono applicati all'organizzazione risorse hello.

Esempio:
1. Lavoro informazioni o di amministrazione nella società invita l'utente dall'applicazione della società B tooan *Foo* nella società A.
2. Applicazione *Foo* società A è configurato toorequire MFA accesso.
3. Quando di tenta app tooaccess utente hello dalla società B *Foo* società hello un tenant, sono frequenti toocomplete una richiesta di autenticazione a più fattori.
4. Hello utente può impostare i relativi MFA con la società e sceglie l'opzione di autenticazione a più fattori.
5. Questo scenario funziona per qualsiasi identità, ad esempio di Azure AD o account del servizio gestito, se gli utenti della società B eseguono l'autenticazione usando un ID per social network.
6. La società A deve avere un numero sufficiente di licenze di Azure AD Premium che supportano l'autenticazione a più fattori. utente Hello dalla società B utilizza questa licenza dalla società A.

tenancy invitando Hello è sempre responsabile per l'autenticazione a più fattori per gli utenti dell'organizzazione partner hello, anche se l'organizzazione partner hello dispone di funzionalità di autenticazione a più fattori.

### <a name="setting-up-mfa-for-b2b-collaboration-users"></a>Configurazione dell'autenticazione a più fattori per gli utenti di Collaborazione B2B
toodiscover facilmente tooset di autenticazione a più fattori per gli utenti di collaborazione B2B, vedere vedere hello seguenti video:

>[!VIDEO https://channel9.msdn.com/Blogs/Azure/b2b-conditional-access-setup/Player]

### <a name="b2b-users-mfa-experience-for-offer-redemption"></a>Esperienza di autenticazione a più fattori per gli utenti di B2B per il riscatto dell'offerta
Estrarre hello esperienza riscatto di animazione toosee hello seguente:

>[!VIDEO https://channel9.msdn.com/Blogs/Azure/MFA-redemption/Player]

### <a name="mfa-reset-for-b2b-collaboration-users"></a>Reimpostazione dell'autenticazione a più fattori per gli utenti di Collaborazione B2B
Attualmente, salve può richiedere tooproof agli utenti di collaborazione B2B di nuovo solo usando hello i cmdlet di PowerShell seguente:

1. Connettersi AD tooAzure

  ```
  $cred = Get-Credential
  Connect-MsolService -Credential $cred
  ```
2. Ottenere tutti gli utenti con metodi di identificazione

  ```
  Get-MsolUser | where { $_.StrongAuthenticationMethods} | select UserPrincipalName, @{n="Methods";e={($_.StrongAuthenticationMethods).MethodType}}
  ```
  Di seguito è fornito un esempio:

  ```
  PS C:\Users\tjwasserGet-MsolUser | where { $_.StrongAuthenticationMethods} | select UserPrincipalName, @{n="Methods";e={($_.StrongAuthenticationMethods).MethodType}}
  ```

3. Ripristinare nuovamente il metodo di autenticazione a più fattori hello per un utente specifico toorequire hello B2B collaborazione utente tooset prova i metodi. Esempio:

  ```
  Reset-MsolStrongAuthenticationMethodByUpn -UserPrincipalName gsamoogle_gmail.com#EXT#@ WoodGroveAzureAD.onmicrosoft.com
  ```

### <a name="why-do-we-perform-mfa-at-hello-resource-tenancy"></a>Perché eseguire autenticazione a più fattori in tenancy risorse hello?

Nella versione corrente di hello, autenticazione a più fattori è sempre tenancy risorse hello, per motivi di prevedibilità. Si supponga, ad esempio, un utente di Contoso (Sally) è invitato tooFabrikam e Fabrikam è abilitata l'autenticazione a più fattori per gli utenti B2B.

Se Contoso dispone di criteri di autenticazione a più fattori abilitato per App1, ma non App2, quindi se si esamina hello attestazione Contoso MFA nel token hello, è possibile visualizzare hello problema seguente:

* Giorno 1: un utente con autenticazione a più fattori in Contoso accede ad App1 e non viene quindi visualizzata una richiesta MFA aggiuntiva in Fabrikam.

* Il giorno 2: utente hello ha avuto accesso alle App 2 in Contoso, a questo punto quando si accede a Fabrikam, deve registrare per l'autenticazione a più fattori non esiste.

Questo processo può generare confusione e provocare toodrop in completamenti di accesso.

Inoltre, anche se Contoso dispone di funzionalità di autenticazione a più fattori, non è sempre hello case hello Fabrikam sarebbe attendibili hello criteri Contoso MFA.

Infine, l'autenticazione a più fattori del tenant delle risorse funziona anche per account del servizio gestito, ID per social network e organizzazioni partner che non hanno configurato l'autenticazione a più fattori.

Pertanto, hello per l'autenticazione a più fattori per gli utenti B2B si consiglia di tooalways richiedono l'autenticazione a più fattori in hello si invitano tenant. Questo requisito può causare toodouble autenticazione a più fattori in alcuni casi, ma ogni volta che accedono tenant invitando hello, l'esperienza degli utenti finali di hello è stimabile: Sally deve registrare per l'autenticazione a più fattori con tenant invitando hello.

### <a name="device-based-location-based-and-risk-based-conditional-access-for-b2b-users"></a>Accesso condizionale basato sul dispositivo, sulla posizione e sui rischi per gli utenti B2B

Quando Contoso Abilita criteri di accesso condizionale basato su dispositivo per i dati aziendali, i dispositivi non gestiti da Contoso e non conformi ai criteri di dispositivi Contoso hello viene impedito l'accesso.

Se il dispositivo dell'utente hello B2B non è gestito da Contoso, accesso di utenti B2B da organizzazioni partner hello è bloccato in qualsiasi contesto di questi criteri vengono applicati. Tuttavia, Contoso è possibile creare elenchi contenenti tooexclude gli utenti partner specifico da hello criteri di accesso condizionale basato su dispositivi di esclusione.

#### <a name="location-based-conditional-access-for-b2b"></a>Accesso condizionale basato sulla posizione per B2B

Se l'organizzazione di invitare hello è in grado di toocreate un intervallo di indirizzi IP attendibile che definisce le organizzazioni partner, i criteri di accesso condizionale in base alla posizione possono essere applicati per gli utenti B2B.

#### <a name="risk-based-conditional-access-for-b2b"></a>Accesso condizionale basato sui rischi per B2B

Attualmente, criteri basati sul rischio di accesso non possono essere applicato tooB2B utenti perché viene eseguita la valutazione dei rischi hello organizzazione principale dell'utente hello B2B.

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
* [API e personalizzazione per Collaborazione B2B di Azure Active Directory](active-directory-b2b-api.md)
* [Aggiungere gli utenti per la Collaborazione B2B senza un invito](active-directory-b2b-add-user-without-invite.md)
* [Indice di articoli per la gestione di applicazioni in Azure Active Directory](active-directory-apps-index.md)
