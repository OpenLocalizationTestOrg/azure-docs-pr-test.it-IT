---
title: 'Azure AD Connect: funzionamento dell''autenticazione pass-through | Microsoft Docs'
description: Questo articolo descrive il funzionamento dell'autenticazione pass-through di Azure Active Directory.
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
ms.date: 07/27/2017
ms.author: billmath
ms.openlocfilehash: ffcebee572a9ba2840e81250651dea45599d65d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-pass-through-authentication-technical-deep-dive"></a>Autenticazione pass-through di Azure Active Directory: approfondimento tecnico

>[!IMPORTANT]
>L'autenticazione pass-through di Azure AD è attualmente in fase di anteprima. 

## <a name="how-does-azure-active-directory-pass-through-authentication-work"></a>Funzionamento dell'autenticazione pass-through di Azure Active Directory

Quando un utente tenta di toosign in un'applicazione protetta da Azure Active Directory (Azure AD) e se l'autenticazione pass-through è abilitato nel tenant di hello, hello si verificano i passaggi seguenti:

1. utente di Hello tenta tooaccess un'applicazione (ad esempio, hello Outlook Web App - https://outlook.office365.com/owa/).
2. Se l'utente hello non è già effettuato l'accesso, utente hello è reindirizzato toohello Azure AD nella pagina di accesso.
3. Hello immesso nome utente e password nella pagina di accesso AD Azure hello e fa clic sul pulsante "Accedi" hello.
4. Azure AD, alla ricezione di hello richiesta di accesso, posiziona hello username e password (crittografata utilizzando una chiave pubblica) in una coda.
5. Un agente autenticazione pass-through locali rende una coda toohello chiamata in uscita e recupera hello username e password crittografata.
6. agente Hello decrittografa password hello utilizzando la chiave privata.
7. agente Hello viene quindi convalidato hello username e password in Active Directory utilizzando le API Windows standard (un toowhat meccanismo simili è utilizzato da Active Directory Federation Services). Hello nome utente può essere un nome utente predefinito di hello locale (in genere `userPrincipalName`) o un altro attributo configurata in Azure AD Connect (noto come `Alternate ID`).
8. Controller di dominio Active Directory (DC) locale Hello quindi valuta hello richiesta e restituisce hello risposta appropriata (esito positivo, l'errore, password scaduta o utente bloccato) toohello agente.
9. agente Hello, a sua volta, restituisce questo tooAzure indietro risposta annuncio.
10. Azure AD restituisce una risposta hello e risponde toohello utente come appropriato: ad esempio, effettua l'accesso utente hello immediatamente o richieste per multi-Factor Authentication (MFA).
11. Se hello utente Accedi ha esito positivo, l'utente hello è tooaccess in grado di un'applicazione hello.

Hello diagramma seguente illustra tutti i componenti di hello e hello passaggi della procedura.

![Autenticazione pass-through](./media/active-directory-aadconnect-pass-through-authentication/pta2.png)

## <a name="next-steps"></a>Passaggi successivi
- [**Current limitations**](active-directory-aadconnect-pass-through-authentication-current-limitations.md) (Limitazioni correnti): questa funzionalità è attualmente in anteprima. Informazioni su quali scenari sono supportati e quali non lo sono.
- [**Guida introduttiva**](active-directory-aadconnect-pass-through-authentication-quick-start.md): avvio ed esecuzione dell'autenticazione pass-through di Azure AD.
- [**Domande frequenti su** ](active-directory-aadconnect-pass-through-authentication-faq.md) -risposte toofrequently domande frequenti.
- [**Risoluzione dei problemi** ](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) -informazioni su come le problematiche comuni tooresolve con funzionalità hello.
- [**Seamless Single Sign-On di Azure AD**](active-directory-aadconnect-sso.md): altre informazioni su questa funzionalità complementare.
- [**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect): per l'invio di richieste di nuove funzionalità.
