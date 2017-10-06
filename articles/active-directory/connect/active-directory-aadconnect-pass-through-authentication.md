---
title: 'Azure AD Connect: autenticazione pass-through | Documentazione Microsoft'
description: Questo articolo descrive l'autenticazione pass-through di Azure Active Directory (Azure AD) e come consenta gli accessi ad Azure AD tramite la convalida delle password degli utenti in Active Directory locale.
services: active-directory
keywords: "cos'è l'autenticazione pass-through di Azure AD Connect, installare Active Directory, componenti richiesti per Azure AD, SSO, Single Sign-On"
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
ms.openlocfilehash: 56cfb2c4f4afc7d46c926a392ae6ec01e96224d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="user-sign-in-with-azure-active-directory-pass-through-authentication"></a>Accesso utente con l'autenticazione pass-through di Azure Active Directory

## <a name="what-is-azure-active-directory-pass-through-authentication"></a>L'autenticazione pass-through di Azure Active Directory

L'autenticazione pass-through di Azure Active Directory (Azure AD) consente il toosign agli utenti di tooboth in locale e applicazioni basate su cloud usando hello stesse password. Questa funzionalità fornisce agli utenti un'esperienza migliore - una minore tooremember, password e riduce i costi di supporto tecnico IT, perché gli utenti sono meno probabile tooforget come toosign in. Quando gli utenti eseguono l'accesso usando Azure AD, la funzionalità convalida le loro password direttamente con Active Directory locale.

Questa funzionalità è un'alternativa troppo[la sincronizzazione dell'Hash Password di Azure AD](active-directory-aadconnectsync-implement-password-synchronization.md), che fornisce hello stessi vantaggi di tooorganizations autenticazione cloud. Tuttavia, i criteri di conformità e sicurezza in alcune organizzazioni non consentono di utilizzare queste organizzazioni le password degli utenti toosend, anche in un form con hash, di fuori i loro limiti interni. Autenticazione pass-through è una soluzione più adeguata per tali organizzazioni hello.

![Autenticazione pass-through di Azure AD](./media/active-directory-aadconnect-pass-through-authentication/pta1.png)

È possibile combinare l'autenticazione pass-through con hello [Single Sign-On trasparente](active-directory-aadconnect-sso.md) funzionalità. In questo modo, quando gli utenti accedono alle applicazioni sui computer aziendali all'interno della rete aziendale, non è necessario tootype in toosign le password in.

>[!IMPORTANT]
>L'autenticazione pass-through di Azure AD è attualmente in fase di anteprima.

## <a name="key-benefits-of-using-azure-ad-pass-through-authentication"></a>Vantaggi principali dell'uso dell'autenticazione pass-through di Azure AD

- *Miglioramento dell'esperienza utente*
  - Gli utenti utilizzano hello stesso toosign le password in locale e di applicazioni basate su cloud.
  - Gli utenti ridurre il tempo toohello per comunicare con il supporto tecnico IT la risoluzione dei problemi relativi alle password.
  - Gli utenti possono completare [la gestione delle password self-service](../active-directory-passwords-overview.md) attività nel cloud hello.
- *Facile toodeploy & amministrare*
  - Non sono necessarie distribuzioni locali o configurazioni di rete complesse.
  - È necessario solo un toobe lightweight agente installato on-premise.
  - Nessun sovraccarico di gestione. agente Hello riceve automaticamente miglioramenti e correzioni di bug.
- *Proteggere*
  - Non vengono mai archiviate password locali nel cloud hello in qualsiasi forma.
  - agente di Hello stabilisce solo connessioni in uscita all'interno della rete. Di conseguenza, vi sono requisito tooinstall hello agenti in una rete perimetrale, noto anche come una rete Perimetrale.
  - Consente di proteggere gli account utente operando senza problemi con [i criteri di accesso condizionale di Azure AD](../active-directory-conditional-access-azure-portal.md), tra cui l'autenticazione a più fattori (MFA, Multi-Factor Authentication) e [filtrando gli attacchi di forza bruta alle password](active-directory-aadconnect-pass-through-authentication-smart-lockout.md).
- *Disponibilità elevata*
  - Agenti aggiuntivi possono essere installati più locale server tooprovide la disponibilità elevata di richieste di accesso.

## <a name="feature-highlights"></a>Funzionalità in primo piano

- Supporta l'accesso utente in tutte le applicazioni basate su browser e nelle applicazioni client di Microsoft Office che usano l'[autenticazione moderna](https://aka.ms/modernauthga).
- Nomi utente di accesso possono essere un nome utente predefinito di hello locale (`userPrincipalName`) o un altro attributo configurata in Azure AD Connect (noto come `Alternate ID`).
- caratteristica Hello funziona perfettamente con [accesso condizionale](../active-directory-conditional-access.md) funzionalità, ad esempio multi-Factor Authentication (MFA) toohelp proteggere gli utenti.
- Gli ambienti a più foreste sono supportati se sono presenti relazioni di trust tra le foreste AD e se il routing del suffisso del nome è configurato correttamente.
- È una funzionalità disponibile gratuitamente e non è necessario qualsiasi edizione a pagamento di Azure AD toouse è.
- È possibile abilitarla tramite [Azure AD Connect](active-directory-aadconnect.md).
- Viene utilizzato un agente lightweight locale che è in ascolto per le risposte toopassword convalida richieste.
- L'installazione di più agenti garantisce la disponibilità elevata di richieste di accesso.
- Si [protegge](active-directory-aadconnect-pass-through-authentication-smart-lockout.md) gli account locali con bruta attacchi di forza password nel cloud hello.

## <a name="next-steps"></a>Passaggi successivi

- [**Quick Start**](active-directory-aadconnect-pass-through-authentication-quick-start.md) - Get up and running Azure AD Pass-through Authentication (Guida introduttiva: avvio ed esecuzione dell'autenticazione pass-through di Azure AD).
- [**Current limitations**](active-directory-aadconnect-pass-through-authentication-current-limitations.md) (Limitazioni correnti): questa funzionalità è attualmente in anteprima. Informazioni su quali scenari sono supportati e quali non lo sono.
- [**Approfondimento tecnico**](active-directory-aadconnect-pass-through-authentication-how-it-works.md): informazioni sul funzionamento di questa funzionalità.
- [**Domande frequenti su** ](active-directory-aadconnect-pass-through-authentication-faq.md) -risposte toofrequently domande frequenti.
- [**Risoluzione dei problemi** ](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) -informazioni su come le problematiche comuni tooresolve con funzionalità hello.
- [**Seamless Single Sign-On di Azure AD**](active-directory-aadconnect-sso.md): altre informazioni su questa funzionalità complementare.
- [**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect): per l'invio di richieste di nuove funzionalità.
