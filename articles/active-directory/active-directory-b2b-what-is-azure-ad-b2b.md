---
title: "aaaWhat è collaborazione B2B di Azure Active Directory? | Microsoft Docs"
description: "Collaborazione B2B di Active Directory di Azure supporta le relazioni tra società consentendo a partner commerciali tooselectively l'accesso alle applicazioni aziendali."
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 1464387b-ee8b-4c7c-94b3-2c5567224c27
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 06/27/2017
ms.author: curtand
ms.custom: aaddev
ms.reviewer: sasubram
ms.openlocfilehash: 359989b66f3d012c306e8748a607662fffacb919
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-ad-b2b-collaboration"></a>Informazioni su Collaborazione B2B di Azure AD

<iframe width="560" height="315" src="https://www.youtube.com/embed/AhwrweCBdsc" frameborder="0" allowfullscreen></iframe>

Funzionalità di Azure AD business-to-business (B2B) collaborazione abilitare un'organizzazione con Azure AD toowork in modo sicuro e protetto agli utenti di qualsiasi altra organizzazione, grande o piccola. che usi o meno Azure AD e che abbia o meno un'organizzazione IT. 

Le organizzazioni che usano Azure AD possono fornire accesso partner tootheir toodocuments, risorse e applicazioni, mantenendo il controllo completo sui propri dati aziendali. Gli sviluppatori possono utilizzare le applicazioni toowrite API di business-to-business hello Azure AD che riuniscono due organizzazioni in più in modo sicuro. Inoltre, è piuttosto semplice per gli utenti finali toonavigate.

97% dei clienti chiedevano di collaborazione B2B di Azure AD è molto importante toothem.

![Grafico a torta](media/active-directory-b2b-what-is-azure-ad-b2b/97-percent-support.png)

All'inizio di aprile 2017 erano già 3 milioni circa gli utenti che usavano le funzionalità di Collaborazione B2B di Azure AD. Oltre il 23% delle organizzazioni Azure AD con più di 10 utenti usano già queste funzionalità.

## <a name="hello-key-benefits-of-azure-ad-b2b-collaboration-tooyour-organization"></a>vantaggi principali di Hello dell'organizzazione tooyour di collaborazione B2B di Azure AD

### <a name="work-with-any-user-from-any-partner"></a>Lavorare con tutti gli utenti di qualsiasi partner

* I partner usano le proprie credenziali

* Nessun requisito per i partner toouse Azure AD

* Non sono necessarie directory esterne e non è richiesta un'installazione complessa

### <a name="simple-and-secure-collaboration"></a>Collaborazione sicura e semplice

* Fornire accesso tooany aziendale app o i dati durante l'applicazione sofisticati, Azure AD gestite i criteri di autorizzazione

* Semplice per gli utenti

* Sicurezza di livello aziendale per app e dati

### <a name="no-management-overhead"></a>Nessun sovraccarico di gestione

* Nessuna gestione di password o account esterno

* Nessuna gestione del ciclo di vita degli account sincronizzata o manuale

* Nessun sovraccarico amministrativo esterno

## <a name="you-can-easily-add-b2b-collaboration-users-tooyour-organization"></a>È possibile aggiungere facilmente organizzazione tooyour agli utenti di collaborazione B2B

Gli amministratori possono aggiungere utenti di collaborazione (guest) B2B hello [portale di Azure](https://portal.azure.com).

![Aggiungere utenti guest](media/active-directory-b2b-what-is-azure-ad-b2b/adding-b2b-users-admin.png)

### <a name="enable-your-collaborators-toobring-their-own-identity"></a>Abilitare il toobring collaboratori le proprie identità

Gli utenti di Collaborazione B2B possono accedere con un'identità a scelta. Se hello utente non dispone di un account Microsoft o un account Azure AD uno viene creato senza problemi per tali in fase di hello del riscatto di offerta.

![Scelta identità di accesso](media/active-directory-b2b-what-is-azure-ad-b2b/sign-in-identity-choice.png)

### <a name="delegate-tooapplication-and-group-owners"></a>Proprietari del delegato tooapplication e gruppo 
Applicazione e i proprietari del gruppo possono aggiungere utenti B2B tooany direttamente dell'applicazione che si è interessati, se si tratta di un'applicazione Microsoft o non. Gli amministratori possono delegare autorizzazioni tooadd B2B utenti toonon amministratori. Non amministratori possono utilizzare hello [Pannello di accesso di Azure AD applicazione](https://myapps.microsoft.com) tooadd B2B tooapplications di collaborazione agli utenti o gruppi.

![Pannello di accesso](media/active-directory-b2b-what-is-azure-ad-b2b/access-panel.png)

![Aggiungere un membro](media/active-directory-b2b-what-is-azure-ad-b2b/add-member.png)

### <a name="authorization-policies-protect-your-corporate-content"></a>Criteri di autorizzazione per proteggere i contenuti aziendali

Possono essere applicati criteri di accesso condizionale, ad esempio l'autenticazione a più fattori:
- A livello di tenant hello
- A livello di applicazione hello
- Per i dati e alle App aziendali tooprotect utenti specifici

![Aggiungere un membro](media/active-directory-b2b-what-is-azure-ad-b2b/add-member.png)

### <a name="use-our-apis-and-sample-code-tooeasily-build-applications-tooonboard"></a>Utilizzare le API e tooeasily codice di esempio compilare applicazioni tooonboard
Portare i partner esterni a bordo in modi personalizzati tooyour esigenze.

Utilizzo di hello [invito di collaborazione B2B API](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation), è possibile personalizzare le proprie esperienze di onboarding, inclusa la creazione di portali di iscrizione self-service. Viene presentato un codice di esempio per un portale self-service [su Github](https://github.com/Azure/active-directory-dotnet-graphapi-b2bportal-web).

![Portale di iscrizione](media/active-directory-b2b-what-is-azure-ad-b2b/sign-up-portal.png)

Con la collaborazione B2B di Azure Active Directory, è possibile ottenere potenzialità di Azure AD tooprotect hello le relazioni tra i partner in modo che gli utenti finali trovare semplice e intuitivo. Pertanto proseguire, hello join migliaia di organizzazioni che già utilizzano B2B di Azure Active Directory per la collaborazione esterna!

## <a name="next-steps"></a>Passaggi successivi

* Amministratore esperienze disponibili in hello [portale di Azure](https://portal.azure.com).

* Esperienze di lavoro di informazioni sono disponibili in hello [Pannello di accesso](https://myapps.microsoft.com).

* E, come sempre, la connessione con il team di prodotto hello per eventuali commenti e suggerimenti, discussioni e suggerimenti tramite il nostro [Microsoft Tech Community](https://techcommunity.microsoft.com/t5/Azure-Active-Directory-B2B/bd-p/AzureAD_B2b).

Vedere gli altri articoli su Azure AD B2B Collaboration.

* [Procedura per aggiungere utenti di Collaborazione B2B ad Azure Active Directory da parte degli amministratori](active-directory-b2b-admin-add-users.md)
* [Procedura per aggiungere utenti di Collaborazione B2B da parte di Information Worker](active-directory-b2b-iw-add-users.md)
* [elementi Hello di posta elettronica di invito collaborazione B2B di hello](active-directory-b2b-invitation-email.md)
* [Riscatto dell'invito di Collaborazione B2B](active-directory-b2b-redemption-experience.md)
* [Licenze per la Collaborazione B2B di Azure AD](active-directory-b2b-licensing.md)
* [Risoluzione dei problemi di Collaborazione B2B di Azure Active Directory](active-directory-b2b-troubleshooting.md)
* [Domande frequenti su Collaborazione B2B di Azure Active Directory](active-directory-b2b-faq.md)
* [API e personalizzazione per Collaborazione B2B di Azure Active Directory](active-directory-b2b-api.md)
* [Autenticazione a più fattori per utenti di Collaborazione B2B](active-directory-b2b-mfa-instructions.md)
* [Aggiungere gli utenti per la Collaborazione B2B senza un invito](active-directory-b2b-add-user-without-invite.md)
* [Controllo e creazione di report per un utente di Collaborazione B2B](active-directory-b2b-auditing-and-reporting.md)
* [Indice di articoli per la gestione di applicazioni in Azure Active Directory](active-directory-apps-index.md)
