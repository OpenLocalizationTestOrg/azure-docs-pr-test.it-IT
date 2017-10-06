---
title: aaaCompare B2B collaborazione e in Azure Active Directory B2C | Documenti Microsoft
description: "Qual è la differenza hello tra collaborazione B2B di Azure Active Directory e Azure Active Directory B2C?"
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
ms.date: 03/15/2017
ms.author: sasubram
ms.openlocfilehash: 34d88b9a7d023e077568e8df3d5e1610ae05b361
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="compare-b2b-collaboration-and-b2c-in-azure-active-directory"></a>Confrontare Collaborazione B2B e B2C di Azure Active Directory

Collaborazione B2B di Azure Active Directory (Azure AD) e Azure Active Directory B2C consentono entrambe toowork con utenti esterni di Azure AD. Di seguito è riportato un confronto tra le diverse caratteristiche.


Funzionalità di Collaborazione B2B |     Offerta autonoma di B2C di Azure AD
-------- | --------
Destinato: le organizzazioni che vogliono toobe tooauthenticate in grado di utenti da un'organizzazione partner, indipendentemente dal provider di identità. | Scopo: invitare i clienti di app Web e per dispositivi mobili, sia individui, clienti istituzionali oppure organizzazioni, in Azure AD.
Identità supportate: dipendenti con account aziendale o dell'istituto di istruzione, partner con account aziendale o dell'istituto di istruzione oppure qualsiasi indirizzo email. Non appena toosupport di federazione.  | Identità supportate: utenti consumer con account di applicazioni locali (qualsiasi indirizzo email o nome utente) o qualsiasi identità social supportata con federazione diretta.
Gli utenti partner hello di directory che: Partner vengono gestiti gli utenti dell'organizzazione esterna hello in hello stessa directory dei dipendenti, ma con annotazioni in modo speciale. Possono essere gestiti hello stesso modo come dipendenti, può essere aggiunto toohello stessi gruppi e così via  | Che sono entità di directory hello cliente utente: nella directory dell'applicazione hello. Gestito separatamente da hello directory dell'organizzazione dipendenti e partner (se presente.
Single sign-on (SSO) tooall Azure App connesse AD è supportato. Ad esempio, è possibile fornire accesso tooOffice 365 o applicazioni locali e le app SaaS tooother, ad esempio Salesforce o Workday.  |  SSO toocustomer proprietà App nei tenant di Azure Active Directory B2C hello è supportato. SSO tooOffice 365 o tooother app di Microsoft e SaaS non Microsoft non è supportato.
Ciclo di vita di partner: gestiti da hello host/si invitano dell'organizzazione.  | Ciclo di vita del cliente: modalità self-service o gestito da un'applicazione hello.
Criteri di sicurezza e conformità: gestiti da hello host/si invitano dell'organizzazione.  | Criteri di sicurezza e conformità: gestiti da un'applicazione hello.
Personalizzazione: viene usato il marchio dell'organizzazione host (o che manda l'invito).  |    Personalizzazione: gestita dall'applicazione. In genere tende prodotto toobe marchio, con dissolvenza organizzazione hello in background hello.
Per altre informazioni: [post di blog](https://blogs.technet.microsoft.com/enterprisemobility/2017/02/01/azure-ad-b2b-new-updates-make-cross-business-collab-easy/), [documentazione](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-b2b-what-is-azure-ad-b2b)  | Per altre informazioni: [pagina del prodotto](https://azure.microsoft.com/en-us/services/active-directory-b2c/), [documentazione](https://docs.microsoft.com/en-us/azure/active-directory-b2c/)


### <a name="next-steps"></a>Passaggi successivi

Vedere gli altri articoli su Azure AD B2B Collaboration.

* [Che cos'è Azure AD B2B Collaboration?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [Proprietà dell'utente di Collaborazione B2B](active-directory-b2b-user-properties.md)
* [Aggiunta di un ruolo di tooa utente collaborazione B2B](active-directory-b2b-add-guest-to-role.md)
* [Delegare gli inviti a Collaborazione B2B](active-directory-b2b-delegate-invitations.md)
* [Gruppi dinamici e Collaborazione B2B](active-directory-b2b-dynamic-groups.md)
* [Configurare app SaaS per Collaborazione B2B](active-directory-b2b-configure-saas-apps.md)
* [Token utente in Collaborazione B2B](active-directory-b2b-user-token.md)
* [Mapping delle attestazioni utente per Collaborazione B2B](active-directory-b2b-claims-mapping.md)
* [Condivisione esterna di Office 365](active-directory-b2b-o365-external-user.md)
* [Limitazioni correnti di Collaborazione B2B](active-directory-b2b-current-limitations.md)
* [Getting support for B2B collaboration](active-directory-b2b-support.md) (Ricevere supporto per Collaborazione B2B)
