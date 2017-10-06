---
title: collaborazione B2B di Azure Active Directory aaaTroubleshooting | Documenti Microsoft
description: Informazioni su come risolvere i problemi comuni di Collaborazione B2B di Azure Active Directory
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
ms.date: 05/25/2017
ms.author: sasubram
ms.openlocfilehash: 6fcfd7e543cd7bb833225f8aa56e332e7a989faf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-azure-active-directory-b2b-collaboration"></a>Risoluzione dei problemi di Collaborazione B2B di Azure Active Directory

Questo articolo illustra come risolvere i problemi comuni di Collaborazione B2B di Azure Active Directory (Azure AD).


## <a name="ive-added-an-external-user-but-do-not-see-them-in-my-global-address-book-or-in-hello-people-picker"></a>È stato aggiunto un utente esterno, ma non vengano visualizzati nella Rubrica globale o in selezione utenti hello

In casi in cui gli utenti esterni non vengono popolati nell'elenco di hello, oggetto hello potrebbe richiedere alcuni minuti tooreplicate.

## <a name="a-b2b-guest-user-is-not-showing-up-in-sharepoint-onlineonedrive-people-picker"></a>Un utente guest B2B non compare nella selezione utenti di SharePoint Online/OneDrive 
 
Hello toosearch di possibilità per gli utenti guest esistenti nella selezione di utenti di SharePoint Online (Simulato) hello è disattivato per il comportamento legacy toomatch predefinito.

È possibile abilitare questa funzionalità tramite l'impostazione di 'ShowPeoplePickerSuggestionsForGuestUsers' in hello tenant e una raccolta siti livello hello. È possibile impostare funzionalità hello usano hello SPOTenant di Set e Set-SPOSite cmdlet, che consente ai membri toosearch tutti gli utenti guest esistenti nella directory hello. Le modifiche apportate nell'ambito del tenant hello non influiscono sui siti Simulato già sottoposto a provisioning.

## <a name="invitations-have-been-disabled-for-directory"></a>Gli inviti sono stati disabilitati per la directory

Se si riceve una notifica che non dispongono di autorizzazioni tooinvite utenti, verificare che l'account utente sia autorizzato tooinvite utenti esterni in impostazioni utente:

![](media/active-directory-b2b-troubleshooting/external-user-settings.png)

Se recentemente sono state modificate le impostazioni o assegnato hello mittente dell'invito Guest ruolo tooa utente, potrebbe essere presente un ritardo di 15-60 minuti affinché hello modifiche abbiano effetto.

## <a name="hello-user-that-i-invited-is-receiving-an-error-during-redemption"></a>utente Hello invitati, riceve un errore durante il riscatto

Di seguito sono riportati gli errori più comuni.

### <a name="invitees-admin-has-disallowed-emailverified-users-from-being-created-in-their-tenant"></a>L'amministratore dell'invitato non consente la creazione di utenti EmailVerified nel tenant

Quando si invitano gli utenti il cui organizzazione utilizza Azure Active Directory, ma in cui hello specifico account utente non esiste (ad esempio, hello utente non esiste in Azure Active Directory contoso.com). messaggio per l'amministratore di contoso.com può disporre di criteri sul posto impediscono agli utenti di creazione. utente di Hello deve controllare con loro toodetermine amministratore se gli utenti esterni sono consentiti. Hello amministratore dell'utente esterno potrebbe essere necessario tooallow verificato tramite posta elettronica agli utenti del proprio dominio (vedere questo [articolo](/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0) in modo che gli utenti verificati tramite posta elettronica).

![](media/active-directory-b2b-troubleshooting/allow-email-verified-users.png)

### <a name="external-user-does-not-exist-already-in-a-federated-domain"></a>L'utente esterno non esiste già in un dominio federato

Se si utilizza l'autenticazione di federazione e hello utente non esiste già in Azure Active Directory, non può essere invitati utente hello.

Questo problema, hello tooresolve amministratore dell'utente esterno deve sincronizzare tooAzure account dell'utente hello Active Directory.

## <a name="how-does--which-is-not-normally-a-valid-character-sync-with-azure-ad"></a>In che modo "\#", che in genere è un carattere non valido, viene sincronizzato con Azure AD?

"\#" è un carattere riservato in UPN per collaborazione B2B di Azure Active Directory o utenti esterni, perché hello invitato account user@contoso.com diventa user_contoso.com#EXT@fabrikam.onmicrosoft.com. Pertanto, \# in UPN provenienti da locali non sono consentiti toosign in toohello portale di Azure. 

## <a name="i-receive-an-error-when-adding-external-users-tooa-synchronized-group"></a>Viene visualizzato un errore durante l'aggiunta di utenti esterni tooa sincronizzazione gruppo

Gli utenti esterni possono essere aggiunte solo troppo "assegnato" o i gruppi "Sicurezza" e non toogroups che vengono controllati in locale.

## <a name="my-external-user-did-not-receive-an-email-tooredeem"></a>L'utente esterno non ha ricevuto un messaggio di posta elettronica tooredeem

l'invitato Hello deve verificare con i provider di servizi Internet o se è consentita tooensure filtro posta indesiderata che hello seguente indirizzo:Invites@microsoft.com

## <a name="i-notice-that-hello-custom-message-does-not-get-included-with-invitation-messages-at-times"></a>Si nota che messaggio hello personalizzati non vengono incluso con i messaggi di invito in alcuni casi

toocomply leggi in materia di privacy, le API non includono messaggi personalizzati nell'invito tramite posta elettronica hello quando:

- mittente dell'invito Hello non dispone di un indirizzo di posta elettronica in hello si invitano tenant
- Quando un'entità di servizio App Invia invito hello

Se questo scenario è tooyou importanti, è possibile eliminare l'account di posta elettronica di invito API e inviarlo tramite il meccanismo di posta elettronica hello di propria scelta. Consultare toomake legale dell'organizzazione che qualsiasi messaggio di posta elettronica inviati in questo modo inoltre conforme allo standard leggi sulla privacy.

## <a name="next-steps"></a>Passaggi successivi

Vedere gli altri articoli su Azure AD B2B Collaboration.

* [Che cos'è Azure AD B2B Collaboration?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [Procedura per aggiungere utenti di Collaborazione B2B ad Azure Active Directory da parte degli amministratori](active-directory-b2b-admin-add-users.md)
* [Procedura per aggiungere utenti di Collaborazione B2B da parte di Information Worker](active-directory-b2b-iw-add-users.md)
* [elementi Hello di posta elettronica di invito collaborazione B2B di hello](active-directory-b2b-invitation-email.md)
* [Riscatto dell'invito di Collaborazione B2B](active-directory-b2b-redemption-experience.md)
* [Licenze per la Collaborazione B2B di Azure AD](active-directory-b2b-licensing.md)
* [Domande frequenti su Collaborazione B2B di Azure Active Directory](active-directory-b2b-faq.md)
* [API e personalizzazione per Collaborazione B2B di Azure Active Directory](active-directory-b2b-api.md)
* [Autenticazione a più fattori per utenti di Collaborazione B2B](active-directory-b2b-mfa-instructions.md)
* [Aggiungere gli utenti per la Collaborazione B2B senza un invito](active-directory-b2b-add-user-without-invite.md)
* [Indice di articoli per la gestione di applicazioni in Azure Active Directory](active-directory-apps-index.md)
