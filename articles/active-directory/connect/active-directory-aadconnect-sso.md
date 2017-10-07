---
title: 'Azure AD Connect: Accesso Single Sign-On facile | Microsoft Docs'
description: "Questo argomento viene descritto come Azure Active Directory (Azure AD) trasparente Single Sign-On e la modalità consente di tooprovide true accesso single sign-on per gli utenti desktop aziendali all'interno della rete aziendale."
services: active-directory
keywords: "che cos'è Azure AD Connect, installare Active Directory, componenti richiesti per Azure AD, SSO, Single Sign-On"
documentationcenter: 
author: swkrish
manager: femila
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: billmath
ms.openlocfilehash: 11c778c37ee39866dcc3a14ab648cfcd8e322e47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-seamless-single-sign-on"></a>Accesso Single Sign-On facile di Azure Active Directory

## <a name="what-is-azure-active-directory-seamless-single-sign-on"></a>Che cos'è l'accesso Single Sign-On facile di Azure Active Directory?

Azure Active Directory trasparente Single Sign-On (SSO senza problemi per Azure AD) accede automaticamente gli utenti quando si trovano sulla rete aziendale dispositivi aziendali tooyour connesso. Quando abilitata, gli utenti non necessario tootype in toosign le password in Active Directory tooAzure e in genere, anche digitare i nomi utente. Questa funzionalità consente agli utenti l'accesso semplice applicazioni basate su cloud tooyour senza la necessità di tutti i componenti locali aggiuntive.

SSO senza problemi può essere combinato con entrambi hello [la sincronizzazione dell'Hash Password](active-directory-aadconnectsync-implement-password-synchronization.md) o [autenticazione pass-through](active-directory-aadconnect-pass-through-authentication.md) metodi di accesso.

![Accesso Single Sign-On facile](./media/active-directory-aadconnect-sso/sso1.png)

>[!IMPORTANT]
>L'accesso Single Sign-On facile è attualmente in fase di anteprima. Questa funzionalità è _non_ applicabile tooActive Directory Federation Services (ADFS).

## <a name="key-benefits"></a>Vantaggi principali

- *Miglioramento dell'esperienza utente*
  - Gli utenti vengono automaticamente connessi sia alle applicazioni locali che a quelle basate sul cloud.
  - Gli utenti non devono tooenter le password più volte.
- *Facile toodeploy & amministrare*
  - Non necessari componenti aggiuntivi locali toomake questo lavoro.
  - Funziona con qualsiasi metodo di autenticazione cloud: [sincronizzazione dell'hash delle password](active-directory-aadconnectsync-implement-password-synchronization.md) o [autenticazione pass-through](active-directory-aadconnect-pass-through-authentication.md).
  - Può essere implementata toosome o tutti gli utenti con criteri di gruppo.
  - Registrare i dispositivi non Windows 10 con Azure AD senza necessità di hello di qualsiasi infrastruttura ADFS. Questa funzionalità richiede che l'utente toouse versione 2.1 o versione successiva di hello [client all'area di lavoro](https://www.microsoft.com/download/details.aspx?id=53554).

## <a name="feature-highlights"></a>Funzionalità in primo piano

- Nome accesso utente può essere un nome utente predefinito di hello locale (`userPrincipalName`) o un altro attributo configurata in Azure AD Connect (`Alternate ID`). Entrambi utilizzano lavoro casi perché trasparente SSO utilizza hello `securityIdentifier` attestazione nel toolook ticket Kerberos di hello backup dell'oggetto utente corrispondente hello in Azure AD.
- L'accesso SSO facile è una funzionalità opportunistica. Se non riesce per qualsiasi motivo, l'esperienza di accesso utente hello torna comportamento normale tooits - ad esempio, hello utente deve tooenter la password nella pagina di accesso hello.
- Se un'applicazione inoltra un `domain_hint` (OpenID Connect) o `whr` parametro (SAML), che identifica il tenant, o `login_hint` parametro - identificazione utente hello, nel relativo AD Azure richiesta di accesso, gli utenti sono automaticamente l'accesso senza di essi Immettere i nomi utente o password.
- Può essere abilitata da Azure AD Connect.
- È una funzionalità disponibile gratuitamente e non è necessario qualsiasi edizione a pagamento di Azure AD toouse è.
- Può essere usata per i client basati su Web browser e i client di Office che supportano l'[autenticazione moderna](https://aka.ms/modernauthga) nelle piattaforme e nei browser idonei per l'autenticazione Kerberos:

| SO\Browser |Internet Explorer|Edge|Google Chrome|Mozilla Firefox|Safari|
| --- | --- |--- | --- | --- | -- 
|Windows 10|Sì|No|Sì|Sì\*|N/D 
|Windows 8.1|Sì|N/D|Sì|Sì\*|N/D 
|Windows 8|Sì|N/D|Sì|Sì\*|N/D 
|Windows 7|Sì|N/D|Sì|Sì\*|N/D
|Mac OS X|N/D |N/D |Sì\*|Sì\*|Sì\*

\*Richiede una [configurazione aggiuntiva](active-directory-aadconnect-sso-quick-start.md#browser-considerations)

>[!IMPORTANT]
>È recente eseguito il rollback il supporto per Edge tooinvestigate problemi segnalati.

>[!NOTE]
>Per Windows 10, hello consiglia toouse [aggiunta ad Azure AD](../active-directory-azureadjoin-overview.md) per hello ottimale esperienza single sign-on con Azure AD.

## <a name="next-steps"></a>Passaggi successivi

- [**Avvio rapido**](active-directory-aadconnect-sso-quick-start.md): avvio ed esecuzione di Accesso SSO facile di Azure AD.
- [**Approfondimento tecnico**](active-directory-aadconnect-sso-how-it-works.md): informazioni sul funzionamento di questa funzionalità.
- [**Domande frequenti su** ](active-directory-aadconnect-sso-faq.md) -risposte toofrequently domande frequenti.
- [**Risoluzione dei problemi** ](active-directory-aadconnect-troubleshoot-sso.md) -informazioni su come le problematiche comuni tooresolve con funzionalità hello.
- [**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect): per l'invio di richieste di nuove funzionalità.
