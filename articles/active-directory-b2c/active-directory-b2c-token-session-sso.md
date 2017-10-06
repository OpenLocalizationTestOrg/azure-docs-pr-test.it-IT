---
title: 'Azure Active Directory B2C: configurazione di token, sessione e accesso Single Sign-On | Documentazione Microsoft'
description: Configurazione di token, sessione e accesso Single Sign-On in Azure Active Directory B2C
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: e78e6344-0089-49bf-8c7b-5f634326f58c
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/26/2017
ms.author: swkrish
ms.openlocfilehash: 63325ed97a7363723c97ee3a992046ebb5592662
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-token-session-and-single-sign-on-configuration"></a>Azure Active Directory B2C: Configurazione di token, sessione e accesso Single Sign-On
Questa funzionalità offre un controllo dettagliato, in base ai [singoli criteri](active-directory-b2c-reference-policies.md), per gli elementi seguenti:

1. Durate dei token di sicurezza emessi da Azure Active Directory (Azure AD) B2C.
2. Durate delle sessioni delle applicazioni Web gestite da Azure AD B2C.
3. Formati di importanti attestazioni nei token di sicurezza hello generato da Azure Active Directory B2C.
4. Comportamento dell'accesso Single Sign-On (SSO) in più app e criteri nel tenant di B2C.

È possibile usare questa funzionalità nel tenant di B2C come indicato di seguito:

1. Seguire questi passaggi troppo[passare pannello funzionalità toohello B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) su hello portale di Azure.
2. Fare clic su **Criteri di accesso**. *Nota: è possibile usare questa funzionalità per qualsiasi tipo di criterio, non solo per i **criteri di accesso***.
3. Fare clic su un criterio per aprirlo. Ad esempio, fare clic su **B2C_1_SiIn**.
4. Fare clic su **modifica** nella parte superiore di hello del pannello hello.
5. Fare clic su **Token, session & single sign-on config** (Configurazione di token, sessione e accesso Single Sign-On).
6. Apportare le modifiche necessarie. Per informazioni sulle proprietà disponibili, vedere le sezioni successive.
7. Fare clic su **OK**.
8. Fare clic su **salvare** nella parte superiore di hello del pannello hello.

## <a name="token-lifetimes-configuration"></a>Configurazione delle durate dei token
Azure Active Directory B2C supporta hello [protocollo di autorizzazione OAuth 2.0](active-directory-b2c-reference-protocols.md) per l'abilitazione di proteggere l'accesso alle risorse tooprotected. tooimplement questo supporto, Azure AD B2C genera vari [i token di sicurezza](active-directory-b2c-reference-tokens.md). Si tratta di proprietà di hello che è possibile utilizzare toomanage durata dei token di sicurezza emesso da Azure Active Directory B2C:

* **Accedi al & ID token durate (minuti)**: durata hello di hello OAuth 2.0 connessione toogain utilizzati token accesso tooa la risorsa protetta. Azure AD B2C emette attualmente solo token ID. Questo valore verrà applicata tooaccess token, anche quando si aggiunge il supporto per loro.
  * Impostazione predefinita: 60 minuti.
  * Valore minimo (inclusivo): 5 minuti.
  * Valore massimo (inclusivo): 1440 minuti.
* **Durata del token di aggiornamento (giorni)**: hello periodo di tempo massimo prima che un token di aggiornamento può essere utilizzato tooacquire un nuovo accesso o un ID token (e, facoltativamente, un nuovo token di aggiornamento, se l'applicazione è state concesse hello `offline_access` ambito).
  * Impostazione predefinita: 14 giorni.
  * Valore minimo (inclusivo): 1 giorno.
  * Valore massimo (inclusivo): 90 giorni.
* **Aggiorna durata token di una finestra temporale scorrevole (giorni)**: dopo che l'utente di hello scadenza di questo intervallo di tempo è forzato toore-l'autenticazione, indipendentemente dal periodo di validità hello del token aggiornamento più recente di hello acquisito da un'applicazione hello. Possono essere fornita solo se il cambio di hello viene impostato troppo**associata**. È necessario toobe maggiore o uguale toohello **durata token di aggiornamento (giorni)** valore. Se il cambio di hello viene impostato troppo**Unbounded**, non è possibile fornire un valore specifico.
  * Impostazione predefinita: 90 giorni.
  * Valore minimo (inclusivo): 1 giorno.
  * Valore massimo (inclusivo): 365 giorni.

Ecco un paio di casi di utilizzo in cui è possibile abilitare l'uso di queste proprietà:

* Consente un toostay utente effettuato l'accesso a un'applicazione per dispositivi mobili in modo indefinito, purché sia continuamente attivo in un'applicazione hello. È possibile farlo dall'impostazione hello **durata finestra temporale scorrevole token di aggiornamento (giorni)** passare troppo**Unbounded** nei criteri di accesso.
* Soddisfare i requisiti di conformità e sicurezza del settore mediante l'impostazione di durata dei token hello accesso appropriato.

    > [!NOTE]
    > Queste impostazioni non sono disponibili per i criteri di reimpostazione della password.
    > 
    > 

## <a name="token-compatibility-settings"></a>Impostazioni di compatibilità dei token
Sono stati apportati formattazione modifiche tooimportant attestazioni nei token di sicurezza emesso da Azure Active Directory B2C. Questo è stato fatto tooimprove al supporto per il protocollo standard e per una migliore interoperabilità con le librerie di identità di terze parti. Tuttavia, App esistenti di rilievo tooavoid, creata hello seguente proprietà tooallow clienti tooopt-in base alle esigenze:

* **Attestazione autorità di certificazione (iss)**: identifica tenant di Azure Active Directory B2C hello che ha emesso il token hello.
  * `https://login.microsoftonline.com/{B2C tenant GUID}/v2.0/`: Questo è il valore di predefinito hello.
  * `https://login.microsoftonline.com/tfp/{B2C tenant GUID}/{Policy ID}/v2.0/`: Questo valore include gli ID dei tenant hello B2C sia criteri hello usato nella richiesta di token hello. Se l'app o la raccolta deve toobe Azure Active Directory B2C conformi con hello [OpenID Connect 1.0 individuazione spec](http://openid.net/specs/openid-connect-discovery-1_0.html), utilizzare questo valore.
* **Attestazione soggetto (sub)**: identifica entità hello, ad esempio, utente hello, per cui hello token rilascia informazioni.
  * **ObjectID**: questo è il valore di predefinito hello. Popola l'ID di oggetto hello di utente hello nella directory di hello in hello `sub` attestazione nel token hello.
  * **Non è supportato**: viene fornito solo per compatibilità con le versioni precedenti, si consiglia di passare troppo**ObjectID** non appena possibile.
* **Attestazioni che rappresentano ID criterio**: identifica il tipo di attestazione hello in cui hello ID criterio usato nella richiesta di token hello viene popolata.
  * **tfp**: questo è il valore di predefinito hello.
  * **ACR**: viene fornito solo per compatibilità con le versioni precedenti, si consiglia di passare troppo`tfp` non appena possibile.

## <a name="session-behavior"></a>Comportamento della sessione
Azure Active Directory B2C supporta hello [protocollo di autenticazione OpenID Connect](active-directory-b2c-reference-oidc.md) per consentire alle applicazioni protette tooweb Accedi. Proprietà di hello che è possibile utilizzare le sessioni dell'applicazione web di toomanage sono:

* **App Web durata della sessione (minuti)**: durata hello del cookie di sessione del Azure Active Directory B2C memorizzato nel browser dell'utente hello alla riuscita dell'autenticazione.
  * Impostazione predefinita: 1440 minuti.
  * Valore minimo (inclusivo): 15 minuti.
  * Valore massimo (inclusivo): 1440 minuti.
* **Timeout della sessione Web app**: se questa opzione è impostata troppo**assoluto**, hello è forzato toore-autenticazione dopo il periodo di tempo specificato da hello **app Web durata della sessione (minuti)** allo scadere dell'intervallo. Se questa opzione è impostata troppo**materiale** (hello impostazione predefinita), utente hello rimane connesso come utente hello è costantemente attivo nell'applicazione web.

Ecco un paio di casi di utilizzo in cui è possibile abilitare l'uso di queste proprietà:

* Soddisfare i requisiti di conformità e sicurezza del settore impostando sessione dell'applicazione web appropriato di hello durate.
* Imporre la ripetizione dell'autenticazione dopo un periodo di tempo specifico durante l'interazione di un utente con una parte a sicurezza elevata dell'applicazione Web. 

    > [!NOTE]
    > Queste impostazioni non sono disponibili per i criteri di reimpostazione della password.
    > 
    > 

## <a name="single-sign-on-sso-configuration"></a>Configurazione dell'accesso Single Sign-On
Se si dispone di più applicazioni e i criteri nel tenant di B2C, è possibile gestire le interazioni degli utenti tra loro utilizzando hello **configurazione Single sign-on** proprietà. È possibile impostare hello proprietà tooone di hello seguenti impostazioni:

* **Tenant**: impostazione predefinita hello. Con questa impostazione consente a più applicazioni e i criteri nel tenant di B2C tooshare hello stessa sessione utente. Ad esempio, quando un utente accede a un'applicazione, Contoso Shopping, può accedere contemporaneamente anche a un'altra applicazione, Contoso Pharmacy, senza alcun problema.
* **Applicazione**: in questo modo è toomaintain una sessione utente esclusivamente per un'applicazione indipendente da altre applicazioni. Ad esempio, se si desidera toosign utente hello in tooContoso. farmacia (con hello stesse credenziali), anche se è già connesso in Contoso market, un'altra applicazione nel hello egli stesso tenant B2C. 
* **Criteri**: in questo modo è toomaintain una sessione utente esclusivamente per un criterio, indipendente dalle applicazioni hello utilizzarlo. Ad esempio, se utente hello già effettuato l'accesso e completare un passaggio di multi factor authentication (MFA), egli possibile assegnargli parti toohigher sicurezza di accesso di più applicazioni, purché hello sessione collegata toohello criteri senza scadenza.
* **Disabilitato**: hello utente toorun tramite viaggio utente intera hello in questo modo a ogni esecuzione del criterio hello. Ad esempio, in questo modo sarà più utenti toosign tooyour applicazione (in un desktop scenario condiviso), anche mentre un singolo utente rimane connesso durante l'intero periodo di tempo hello.

    > [!NOTE]
    > Queste impostazioni non sono disponibili per i criteri di reimpostazione della password.
    > 
    > 

