---
title: 'Azure Active Directory B2C: protocolli di autenticazione | Documentazione Microsoft'
description: "Modalità App toobuild direttamente tramite hello i protocolli supportati da Azure Active Directory B2C"
services: active-directory-b2c
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 5e407d0a-73a2-4d74-ac81-3aa6c31ddcee
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.openlocfilehash: 8fa4cbebe711841d410b3ae43b78f893c06d9b63
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# AD B2C Azure: protocolli di autenticazione
Azure Active Directory B2C (Azure AD B2C) fornisce l'identità come servizio per le app grazie al supporto di due protocolli standard del settore, OpenID Connect e OAuth 2.0. servizio Hello è conforme agli standard, ma le due implementazioni di questi protocolli possono presentare alcune differenze. 

informazioni di Hello in questa guida sono utile se si scrive codice per l'invio e la gestione delle richieste HTTP anziché tramite una libreria open source. È consigliabile leggere questa pagina prima di approfondire i dettagli di hello di ciascun protocollo specifico. Ma se si ha già familiarità con Azure Active Directory B2C, è possibile passare direttamente troppo[hello guide di riferimento di protocollo](#protocols).

<!-- TODO: Need link toolibraries above -->

## Nozioni di base Hello
Ogni applicazione che utilizza Azure Active Directory B2C deve toobe registrate nella directory di B2C in hello [portale di Azure](https://portal.azure.com). processo di registrazione applicazione Hello raccoglie e assegna alcuni valori tooyour app:

* Un **ID applicazione** che identifica l'app in modo univoco.
* Oggetto **URI di reindirizzamento** o **identificatore del pacchetto** che può essere utilizzato toodirect risposte tooyour indietro app.
* Altri valori specifici dello scenario Per ulteriori informazioni, vedere [come tooregister applicazione](active-directory-b2c-app-registration.md).

Dopo aver registrato l'app, comunica con Azure Active Directory (Azure AD) tramite l'invio di richieste toohello endpoint:

```
https://login.microsoftonline.com/{tenant}/oauth2/v2.0/authorize
https://login.microsoftonline.com/{tenant}/oauth2/v2.0/token
```

In quasi tutti i flussi OAuth e OpenID Connect, sono coinvolti nello scambio hello quattro parti:

![Ruoli di OAuth 2.0](./media/active-directory-b2c-reference-protocols/protocols_roles.png)

* Hello **server autorizzazione** endpoint hello Azure AD. Gestisce in modo sicuro informazioni toouser nulla correlati e l'accesso. Gestisce inoltre le relazioni di trust hello tra parti hello in un flusso. È responsabile della verifica hello dell'identità utente, la concessione e revoca accesso tooresources e rilascio di token. È anche noto come provider di identità hello.

* Hello **proprietario della risorsa** è in genere l'utente finale di hello. È parte di hello che possiede i dati di hello, e ha hello power tooallow terzi tooaccess dei dati o risorse.

* Hello **client OAuth** è l'app. ed è identificato dal relativo ID applicazione. È in genere parte hello che gli utenti finali interagiscono. Inoltre, le richieste token dal server di autorizzazione hello. proprietario della risorsa Hello deve concedere hello client autorizzazione tooaccess hello risorse.

* Hello **server delle risorse** in cui risiede la risorsa hello o dati. Considera attendibili autorizzazione hello server toosecurely autenticare e autorizzare i client di OAuth hello. Utilizza inoltre l'accesso connessione tooensure i token che accedono a risorse tooa può essere concessa.

## Criteri
I criteri di Azure Active Directory B2C sono senza dubbio, funzionalità più importanti di hello del servizio hello. Azure Active Directory B2C estende i protocolli di OAuth 2.0 e OpenID Connect standard hello introducendo i criteri. Questi consentono la Azure Active Directory B2C tooperform molto più semplice autenticazione e autorizzazione. 

I criteri descrivono in modo completo le esperienze di identità dell'utente, inclusi l'iscrizione, l'accesso e la modifica del profilo. I criteri possono essere definiti in un'interfaccia utente amministrativa ed eseguiti usando un parametro di query speciale nelle richieste di autenticazione HTTP. 

I criteri non sono funzionalità standard di OAuth 2.0 e OpenID Connect, pertanto è necessario intraprendere hello ora toounderstand li. Per ulteriori informazioni, vedere hello [Guida di riferimento dei criteri di Azure Active Directory B2C](active-directory-b2c-reference-policies.md).

## Tokens
implementazione di Hello Azure Active Directory B2C di OAuth 2.0 e OpenID Connect modo estensivo di token di connessione, inclusi i token di connessione che sono rappresentati come token web JSON (Jwt). Un token di connessione è una risorsa protetta un token di sicurezza leggero che concede hello tooa accesso "bearer".

connessione Hello è qualsiasi entità che possono presentare token hello. Per poter ricevere un token di connessione, Azure AD deve prima autenticare una parte. Tuttavia, se il token hello toosecure durante la trasmissione e di archiviazione non vengono eseguite operazioni hello necessario può essere intercettato e usato da parti non autorizzate.

Alcuni token di sicurezza hanno meccanismi predefiniti che ne impediscono l'uso da parti non autorizzate, ma i token di connessione non presentano questo meccanismo. Devono essere trasportati usando un canale protetto, ad esempio un protocollo Transport Layer Security (HTTPS). 

Se un token viene trasmesso all'esterno di un canale sicuro, un malintenzionato può usare un token di hello tooacquire attacco man-in-the-middle e usarlo risorsa tooa protetto di accesso toogain non autorizzato. Hello stessi principi di sicurezza si applicano quando i token di connessione vengono archiviati o memorizzate nella cache per un uso successivo. Assicurarsi sempre che l'app trasmetta e archivi i token di connessione in modo sicuro.

Per altre considerazioni sulla sicurezza dei token di connessione, vedere la [RFC 6750 Section 5](http://tools.ietf.org/html/rfc6750).

Sono disponibili in altre informazioni sui diversi tipi di token che vengono usati in Azure Active Directory B2C di hello [hello riferimento del token di Azure AD](active-directory-b2c-reference-tokens.md).

## Protocolli
Quando si è pronti richiede alcuni esempi di tooreview, è possibile iniziare con una delle seguenti esercitazioni hello. Ognuno corrisponde tooa uno scenario di autenticazione specifico. Se è necessario determinare il flusso è adatta alle proprie esigenze, consultare [hello tipi di App, è possibile compilare utilizzando Azure AD B2C](active-directory-b2c-apps.md).

* [Compilare applicazioni native e per dispositivi mobili con OAuth 2.0.](active-directory-b2c-reference-oauth-code.md)
* [Compilare app Web con OpenID Connect.](active-directory-b2c-reference-oidc.md)
* [Creazione di applicazioni a pagina singola tramite flusso implicito hello OAuth 2.0](active-directory-b2c-reference-spa.md)

