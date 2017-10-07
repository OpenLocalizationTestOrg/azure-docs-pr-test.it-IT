---
title: portale di iscrizione aaaSelf-service per la collaborazione B2B di Azure Active Directory | Documenti Microsoft
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
ms.date: 05/24/2017
ms.author: sasubram
ms.openlocfilehash: c78920ecf812f7efc06a8b54b1fff834c32904f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="self-service-portal-for-azure-ad-b2b-collaboration-sign-up"></a>Portale self-service per l'iscrizione a Collaborazione B2B di Azure AD

I clienti possono eseguire molto con funzionalità incorporate di hello esposte tramite l'amministratore IT [portale di Azure](https://portal.azure.com) e nel [Pannello di accesso dell'applicazione](https://myapps.microsoft.com) per gli utenti finali. Tuttavia anche le aziende necessario flusso di lavoro caricamento hello toocustomize per toofit utenti B2B esigenze della propria organizzazione. È possibile farlo con la [nostra API](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation).

Nel corso delle conversazioni intrattenute con i clienti, un'esigenza comune risulta più evidente rispetto a tutte le altre. Hello si invitano organizzazione potrebbe non sapere anticipatamente che hello singoli collaboratori esterni sono che devono accedere alle risorse di tootheir. Volevano un modo per gli utenti dei partner commerciali troppo iscriversi autonomamente con un set di criteri che hello si invitano i controlli dell'organizzazione. Questo scenario è possibile tramite le API ed è quindi stato pubblicato un [progetto Github di esempio](https://github.com/Azure/active-directory-dotnet-graphapi-b2bportal-web) a tale scopo.

Il progetto Github viene illustrato come le organizzazioni possono usare le API e forniscono una funzionalità di sottoscrizione basata su criteri self-service per i relativi partner attendibili, con regole che determinano le app hello che possono accedere. Gli utenti partner è possono ottenere accesso tooresources quando sono necessari, in modo sicuro, senza richiedere hello si invitano caricare toomanually organizzazione li. È possibile distribuire facilmente progetto hello in una sottoscrizione di Azure di propria scelta.

## <a name="as-is-code"></a>Codice cosi com’è

Tenere presente che questo codice viene fornito come un esempio di utilizzo di invito hello B2B di Azure Active Directory API toodemonstrate. Deve essere preferibilmente personalizzato dal team di sviluppo o da un partner ed esaminato prima di essere distribuito in uno scenario di produzione.

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