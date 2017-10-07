---
title: collaborazione aaaAzure attivo B2B Directory licenze indicazioni | Documenti Microsoft
description: "La Collaborazione B2B di Azure Active Directory non richiede le licenze di Azure AD a pagamento, ma è anche possibile ottenere le funzionalità a pagamento per gli utenti guest B2B"
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
ms.date: 08/09/2017
ms.author: curtand
ms.reviewer: sasubram
ms.custom: it-pro
ms.openlocfilehash: 8e15d66209b090bff210674ecdacc88cd642dcc0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2b-collaboration-licensing-guidance"></a>Linee guida sulla Collaborazione B2B di Azure Active Directory

È possibile utilizzare gli utenti guest di Azure AD B2B collaborazione funzionalità tooinvite nel tooallow tenant di Azure AD essi tooaccess servizi di Azure AD e altre risorse all'interno dell'organizzazione. Se si desidera tooprovide accedere alle funzionalità di Azure AD toopaid, B2B devono avere la licenza agli utenti guest di collaborazione con Azure AD le licenze appropriate. 

In particolare:
* Le funzionalità di Azure AD Free sono disponibili per gli utenti guest senza licenze aggiuntive.
* Se si desidera che gli utenti di tooB2B funzionalità Azure AD toopaid accesso tooprovide, è necessario sufficiente toosupport licenze agli utenti guest B2B.
* Un tenant di invitare con Azure Active Directory a pagamento di licenza con B2B collaborazione utilizzare diritti tooan aggiuntive cinque B2B guest utenti invitati toohello tenant.
* cliente di Hello proprietario hello si invitano tenant deve essere hello uno toodetermine quanti utenti di collaborazione B2B necessitano a pagamento di funzionalità di Azure AD. In base a pagamento di Azure AD hello funzionalità desiderate per gli utenti guest, è necessario disporre di sufficiente Azure AD a pagamento licenze agli utenti di collaborazione B2B toocover in hello stessa ratio 5:1.

Un utente guest di Collaborazione B2B viene aggiunto come utente da una società partner, non come dipendente dell'organizzazione o dipendente di un'azienda affiliata diversa. Un utente guest B2B può accedere con credenziali aggiuntive o con credenziali di proprietà dell'organizzazione, come illustrato in questo articolo. 

In altre parole, B2B licenze è impostata non dalla modalità di autenticazione dell'utente hello ma dalla relazione hello dell'organizzazione di tooyour utente hello. Se gli utenti non sono partner, vengono considerati in modo diverso a livello di licenza. Non sono considerati un utente di collaborazione B2B toobe per scopi di licenza, anche se i relativi UserType è contrassegnato come "Guest". È necessario assegnare a questi utenti licenze in base alla procedura normale, ovvero una licenza per utente. Questi utenti includono:
* Dipendenti
* Personale che accede con identità esterne
* Dipendenti di un'azienda affiliata diversa


## <a name="licensing-examples"></a>Esempi di licenza
- Un cliente vuole tooinvite 100 B2B collaborazione utenti tooits tenant di Azure AD. cliente Hello assegna la gestione degli accessi e il provisioning per tutti gli utenti, ma 50 utenti richiedono anche l'autenticazione a più fattori e l'accesso condizionale. Il cliente deve acquistare licenze di Azure AD Basic 10 e 10 toocover licenze di Azure AD Premium P1 questi utenti B2B correttamente. Se customer hello piani di funzionalità di protezione dell'identità toouse con utenti B2B, devono avere gli utenti di Azure AD Premium P2 licenze toocover hello invitato in hello stessa ratio 5:1.
- Un cliente dispone di 10 dipendenti, tutti coperti da una licenza Premium P1 di Azure AD, Sono ora desidera tooinvite 60 B2B che gli utenti che richiedono l'autenticazione a più fattori (MFA). In regole di gestione delle licenze 5:1 hello, hello cliente deve disporre di almeno 12 toocover licenze di Azure AD Premium P1 tutti gli utenti di collaborazione B2B 60. Perché hanno già 10 P1 Premium licenze per i 10 dipendenti, hanno diritti tooinvite 50 utenti B2B con funzionalità Premium P1 come autenticazione a più fattori. In questo esempio, quindi, si devono acquistare 2 P1 Premium licenze aggiuntive toocover hello rimanenti 10 B2B collaborazione agli utenti.

> [!NOTE]
> Non è ancora tooassign le licenze direttamente toohello B2B utenti tooenable questi diritti utente di collaborazione B2B.

cliente di Hello proprietario hello si invitano tenant deve essere hello uno toodetermine quanti utenti di collaborazione B2B necessitano a pagamento di funzionalità di Azure AD. A seconda che le funzionalità di Azure AD desiderato per gli utenti guest sono a pagamento, è necessario disporre di sufficiente Azure AD a pagamento agli utenti di collaborazione B2B di licenze toocover in rapporto di hello 5:1. 

## <a name="additional-licensing-details"></a>Altri dettagli sulle licenze
- Non è necessario tooactually gli account utente tooB2B di assegnare le licenze. Basato sul rapporto 5:1 hello, licenze viene automaticamente calcolata e segnalate.
- Se a pagamento licenza Azure AD non esiste alcuna nel tenant di hello ogni diritti hello Ottiene utenti invitati hello Azure AD gratuito offerte edition.
- Se un utente di collaborazione dispone già di un annuncio di Azure a pagamento di B2B licenza dalla propria organizzazione, non utilizzare una delle licenze di collaborazione B2B di hello del tenant invitando hello.

## <a name="advanced-discussion-what-are-hello-licensing-considerations-when-we-add-users-from-a-conglomerate-organization-as-members-using-your-apis"></a>Advanced discussione: che cosa sono alcune considerazioni sulle licenze di hello quando si aggiungono utenti da un'organizzazione conglomerata come "membri" utilizzando le API?
Un utente guest B2B è quello che è stato richiesto da un toowork di organizzazione del partner con organizzazione host hello. In genere, casi diversi da questo non vengono riconosciuti come B2B anche se usano funzionalità B2B. Prendiamo in esame due casi specifici:

1. Se un host invita un dipendente usando un indirizzo cliente
  * Questo scenario non è conforme ai criteri di licenza Microsoft e non è consigliato.

2. Se un'organizzazione host aggiunge un utente da un'altra organizzazione conglomerata
  1. In questo caso, l'utente hello è invitato a utilizzando le API B2B, ma in questo caso non è in genere B2B. In teoria, le organizzazioni dovremmo già invito ad altri utenti di organizzazioni di hello come membri (API consente che). In questo caso, le licenze hanno toobe assegnati membri toothese per tali risorse tooaccess hello si invitano dell'organizzazione.

  2. Alcune organizzazioni potrebbero essere tooadd hello toobe gli utenti dell'organizzazione altri aggiunti come "Guest" come criterio. Di seguito sono spiegati due casi:
      * Hello conglomerato organizzazione sta già utilizzando Azure AD e gli utenti invitato hello sono concessi in licenza in hello un'altra organizzazione: in questo caso, non è previsto un hello di toofollow tooneed utenti invitati formula 1:5 disposti in precedenza in questo documento. 

      * non utilizza Azure AD Hello conglomerato organizzazione o non dispone di licenze sufficiente: In questo caso, seguire hello formula 1:5 disposti in precedenza in questo documento.

## <a name="next-steps"></a>Passaggi successivi

Vedere gli altri articoli su Azure AD B2B Collaboration.

* [Che cos'è Azure AD B2B Collaboration?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [Procedura per aggiungere utenti di Collaborazione B2B ad Azure Active Directory da parte degli amministratori](active-directory-b2b-admin-add-users.md)
* [Procedura per aggiungere utenti di Collaborazione B2B da parte di Information Worker](active-directory-b2b-iw-add-users.md)
* [elementi Hello di posta elettronica di invito collaborazione B2B di hello](active-directory-b2b-invitation-email.md)
* [Riscatto dell'invito di Collaborazione B2B](active-directory-b2b-redemption-experience.md)
* [Risoluzione dei problemi di Collaborazione B2B di Azure Active Directory](active-directory-b2b-troubleshooting.md)
* [Domande frequenti su Collaborazione B2B di Azure Active Directory](active-directory-b2b-faq.md)
* [API e personalizzazione per Collaborazione B2B di Azure Active Directory](active-directory-b2b-api.md)
* [Autenticazione a più fattori per utenti di Collaborazione B2B](active-directory-b2b-mfa-instructions.md)
* [Aggiungere gli utenti per la Collaborazione B2B senza un invito](active-directory-b2b-add-user-without-invite.md)
* [Indice di articoli per la gestione di applicazioni in Azure Active Directory](active-directory-apps-index.md)
