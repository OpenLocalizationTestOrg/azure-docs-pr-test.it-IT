---
title: 'Azure AD Connect: Autenticazione pass-through - Limitazioni correnti | Microsoft Docs'
description: Questo articolo descrive le limitazioni correnti hello di autenticazione pass-through di Azure Active Directory (Azure AD).
services: active-directory
keywords: Autenticazione pass-through di Azure AD Connect, installare Active Directory, componenti necessari per Azure AD, SSO, Single Sign-On
documentationcenter: 
author: swkrish
manager: femila
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/03/2017
ms.author: billmath
ms.openlocfilehash: 2933745d071aae205c44659e6ea92697f390effb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-pass-through-authentication-current-limitations"></a>Autenticazione pass-through di Azure Active Directory - Limitazioni correnti

>[!IMPORTANT]
>L'autenticazione pass-through di Azure AD è attualmente in fase di anteprima. È una funzionalità disponibile gratuitamente e non è necessario qualsiasi edizione a pagamento di Azure AD toouse è. L'autenticazione pass-through è disponibile solo in hello world wide istanza Azure Active Directory e non su [Microsoft Cloud Germania](http://www.microsoft.de/cloud-deutschland) e [Cloud di Microsoft Azure per enti pubblici](https://azure.microsoft.com/features/gov/).

## <a name="supported-scenarios"></a>Scenari supportati

Hello seguenti scenari è completamente supportato durante l'anteprima:

- L'utente accede a tutte le applicazioni basate su Web browser.
- L'utente accede ad applicazioni client di Office 365 che supportano l'[autenticazione moderna](https://aka.ms/modernauthga).
- Aggiunta ad Azure AD per dispositivi Windows 10.
- Supporto di Exchange ActiveSync.

## <a name="unsupported-scenarios"></a>Scenari non supportati

Hello negli scenari seguenti vengono _non_ supportata durante l'anteprima:

- Accesso degli utenti ad applicazioni client legacy di Office (Office 2013 o versioni precedenti). Le organizzazioni sono invitati tooswitch toomodern autenticazione, se possibile. L'autenticazione moderna permette di supportare l'autenticazione pass-through e contribuisce anche a proteggere gli account utente tramite le funzionalità di [accesso condizionale](../active-directory-conditional-access.md), come l'autenticazione a più fattori.
- Accesso degli utenti ad applicazioni client Skype for Business, incluso Skype for Business 2016.
- L'utente accede a PowerShell v 1.0. È consigliabile tuttavia usare PowerShell 2.0.

>[!IMPORTANT]
>Come soluzione alternativa per scenari non supportati, attivare la sincronizzazione dell'Hash Password hello [funzionalità facoltative](active-directory-aadconnect-get-started-custom.md#optional-features) pagina nella procedura guidata Connetti hello Azure AD. Sincronizzazione dell'Hash password agisce come fallback per hello precedenti scenari _solo_ (e _non_ come un generico tooPass-tramite l'autenticazione di fallback). Se questi scenari non sono necessari, disabilitare la sincronizzazione dell'hash della password.

## <a name="next-steps"></a>Passaggi successivi
- [**Guida introduttiva**](active-directory-aadconnect-pass-through-authentication-quick-start.md): avvio ed esecuzione dell'autenticazione pass-through di Azure AD.
- [**Approfondimento tecnico**](active-directory-aadconnect-pass-through-authentication-how-it-works.md): informazioni sul funzionamento di questa funzionalità.
- [**Domande frequenti su** ](active-directory-aadconnect-pass-through-authentication-faq.md) -risposte toofrequently domande frequenti.
- [**Risoluzione dei problemi** ](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) -informazioni su come le problematiche comuni tooresolve con funzionalità hello.
- [**Seamless Single Sign-On di Azure AD**](active-directory-aadconnect-sso.md): altre informazioni su questa funzionalità complementare.
- [**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect): per l'invio di richieste di nuove funzionalità.
