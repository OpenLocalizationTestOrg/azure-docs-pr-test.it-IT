---
title: App aaaDevelop per Azure AD | Microsoft documenti
description: Scritto per professionisti IT di hello, questo articolo fornisce le linee guida per l'integrazione di applicazioni Azure con Active Directory.
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
editor: 
ms.assetid: dd69f2bc-37c5-457c-857d-27acb84267fb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/07/2017
ms.author: kgremban
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d2924be752af0be2843b1d9b74d9ec446d3fe1ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="develop-line-of-business-apps-for-azure-active-directory"></a>Sviluppare app line-of-business per Azure Active Directory
Questa guida fornisce una panoramica dello sviluppo di applicazioni di line-of-business (LoB) per Azure Active Directory (AD) .hello destinati destinatari sono gli amministratori globali di Active Directory o Office 365.

## <a name="overview"></a>Panoramica
La creazione di applicazioni integrate con Azure AD offre agli utenti dell'organizzazione servizi Single Sign-On per Office 365. Con un'applicazione hello in consente di Azure AD, che controllare i criteri di autenticazione hello per un'applicazione hello. altre informazioni sull'accesso condizionale e vedere App tooprotect con multi-factor authentication (MFA) toolearn [le regole di accesso di configurazione](active-directory-conditional-access-azuread-connected-apps.md).

Registrare il toouse applicazione Azure Active Directory. Registrazione di un'applicazione hello significa che gli sviluppatori possono utilizzare Azure AD tooauthenticate utenti e richiedere toouser di accedere alle risorse, ad esempio posta elettronica, calendario e documenti.

Qualsiasi membro della directory (non guest) può registrare un'applicazione, operazione nota anche come *creazione di un oggetto applicazione*.

Registrazione di un'applicazione consente qualsiasi esempio di hello toodo utente:

* Ottenere un'identità per l'applicazione riconosciuta da Azure AD
* Ottenere uno o più segreti/tasti hello applicazione può utilizzare tooauthenticate stesso tooAD
* Applicazione hello del marchio in hello portale di Azure con un nome personalizzato, logo, e così via.
* Applicare app tootheir funzionalità di Azure AD autorizzazioni, tra cui:

  * Controllo degli accessi in base al ruolo
  * Azure Active Directory come server di autorizzazione oAuth (un'API esposta da un'applicazione hello protetto)
* Dichiarare necessarie per toofunction applicazione hello delle autorizzazioni necessarie come previsto, tra cui:

      - Autorizzazioni per l'app (solo amministratori globali). Ad esempio: un altro Azure AD applicazione o un ruolo di appartenenza relativo tooan Azure, risorsa gruppo di risorse, l'appartenenza al ruolo o una sottoscrizione
      - Autorizzazioni delegate (qualsiasi utente). Ad esempio: Azure AD, Profilo di accesso e lettura

> [!NOTE]
> Per impostazione predefinita, qualsiasi membro può registrare un'applicazione. toolearn toorestrict le autorizzazioni per la registrazione di membri toospecific applicazioni, vedere [come le applicazioni vengono aggiunti AD tooAzure](develop/active-directory-how-applications-are-added.md#who-has-permission-to-add-applications-to-my-azure-ad-instance).
>
>

Ecco cosa ne, amministratore globale di hello, è necessario toodo toohelp gli sviluppatori effettuano le applicazioni di produzione:

* Configurare regole di accesso (criteri di accesso/autenticazione a più fattori)
* Configurare l'assegnazione di hello app toorequire utente e assegnare gli utenti
* Esclusione di esperienza di consenso utente hello predefinito

## <a name="configure-access-rules"></a>Configurare regole di accesso
Configurare App SaaS tooyour regole di accesso per applicazione. Ad esempio, è possibile richiedere l'autenticazione a più fattori o consentire solo l'accesso toousers su reti attendibili. Dettagli Hello per questo sono disponibili nel documento hello [le regole di accesso di configurazione](active-directory-conditional-access-azuread-connected-apps.md).

## <a name="configure-hello-app-toorequire-user-assignment-and-assign-users"></a>Configurare l'assegnazione di hello app toorequire utente e assegnare gli utenti
Per impostazione predefinita, gli utenti possono accedere alle applicazioni senza esservi assegnati. Tuttavia, se un'applicazione hello espone i ruoli o se si desidera tooappear applicazione hello nel Pannello di accesso dell'utente, è necessario che l'assegnazione utente.

[Richiedere l'assegnazione degli utenti](active-directory-applications-guiding-developers-requiring-user-assignment.md)

Per gli abbonati ad Azure AD Premium o Enterprise Mobility Suite (EMS), è consigliabile usare i gruppi. Assegnazione di gruppi di applicazioni toohello consente toodelegate accesso continuativo gestione toohello proprietario hello del gruppo di. È possibile creare il gruppo di hello o chiedere responsabile hello del gruppo di hello toocreate organizzazione utilizzando le funzionalità di gestione di gruppo.

[Assegnazione di utenti applicazione tooan](active-directory-applications-guiding-developers-assigning-users.md)  
[Assegnazione di gruppi di applicazioni tooan](active-directory-applications-guiding-developers-assigning-groups.md)

## <a name="suppress-user-consent"></a>Rimuovere l'esperienza di consenso dell'utente
Per impostazione predefinita, ogni utente passa attraverso un toosign esperienza di consenso in. esperienza di consenso Hello, che richiede agli utenti le autorizzazioni di toogrant tooan applicazione, può essere aggiunto agli utenti che hanno familiarità con tali decisioni.

Per le applicazioni attendibili, è possibile semplificare esperienza utente hello applicando toohello il consenso per conto dell'organizzazione.

Per ulteriori informazioni sul consenso dell'utente e consenso hello in Azure, vedere [integrazione di applicazioni con Azure Active Directory](active-directory-integrating-applications.md).

## <a name="related-articles"></a>Articoli correlati
* [Consentire alle applicazioni di accesso remoto sicuro tooon locale con Proxy dell'applicazione Azure AD](active-directory-application-proxy-get-started.md)
* [Anteprima dell'accesso condizionale di Azure per app SaaS](active-directory-conditional-access-azuread-connected-apps.md)
* [La gestione di accesso tooapps con Azure AD](active-directory-managing-access-to-apps.md)
* [Indice di articoli per la gestione di applicazioni in Azure Active Directory](active-directory-apps-index.md)
