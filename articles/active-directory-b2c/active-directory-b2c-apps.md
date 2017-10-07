---
title: Active Directory B2C aaaAzure | Documenti Microsoft
description: "tipi di Hello di applicazioni è possibile compilare in hello Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: bb9d4abe-0db7-4bd9-b0c4-2f43b2c9cf33
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 12/06/2016
ms.author: dastrock
ms.openlocfilehash: 7dd3dac781fb7e1553dd0f2d112b1956489a7dfd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-types-of-applications"></a>Azure Active Directory B2C: tipi di applicazioni
Azure Active Directory (Azure AD) B2C supporta l'autenticazione per un'ampia gamma di architetture di app moderne. Tutti gli elementi sono basati su protocolli standard del settore di hello [OAuth 2.0](active-directory-b2c-reference-protocols.md) o [OpenID Connect](active-directory-b2c-reference-protocols.md). Questo documento descrive brevemente i tipi di hello di App che è possibile compilare, indipendentemente dal linguaggio hello o piattaforma si preferisce. Consente inoltre di comprendere gli scenari di alto livello hello prima [avviare la creazione di applicazioni](active-directory-b2c-overview.md#get-started).

## <a name="hello-basics"></a>Nozioni di base Hello
Ogni applicazione che utilizza Azure Active Directory B2C deve essere registrata nel [directory B2C](active-directory-b2c-get-started.md) tramite hello [portale Azure](https://portal.azure.com/). processo di registrazione applicazione Hello raccoglie e assegna alcuni valori tooyour app:

* Un **ID applicazione** che identifica l'app in modo univoco.
* Oggetto **URI di reindirizzamento** che può essere utilizzato toodirect risposte tooyour indietro app.
* Altri valori specifici dello scenario. Per ulteriori dettagli, informazioni su come troppo[registrare un'app](active-directory-b2c-app-registration.md).

Dopo aver registrato l'applicazione hello, comunica con Azure AD mediante l'invio di richieste AD Azure toohello v 2.0 endpoint:

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize
https://login.microsoftonline.com/common/oauth2/v2.0/token
```

Ogni richiesta inviata tooAzure AD B2C specifica un **criteri**. Un criterio controlla il comportamento di hello di Azure Active Directory. È anche possibile utilizzare questi toocreate endpoint un set personalizzabile di esperienze utente. Tra i criteri comuni sono inclusi quelli per l'iscrizione, l'accesso e la modifica del profilo. Se non si ha familiarità con i criteri, è necessario essere a conoscenza hello Azure Active Directory B2C [framework criteri estendibile](active-directory-b2c-reference-policies.md) prima di continuare.

interazione di Hello di tutte le applicazioni con un endpoint v 2.0 segue uno schema analogo di alto livello:

1. app Hello indirizza hello utente toohello v 2.0 endpoint tooexecute un [criteri](active-directory-b2c-reference-policies.md).
2. utente Hello completa criteri hello in base a una definizione di criteri toohello.
3. app Hello riceve un tipo di token di sicurezza dall'endpoint di hello v 2.0.
4. app Hello utilizza informazioni di hello sicurezza tooaccess token protetto o una risorsa protetta.
5. server delle risorse Hello convalida hello sicurezza tooverify token che è possibile concedere l'accesso.
6. app Hello Aggiorna periodicamente il token di sicurezza hello.

<!-- TODO: Need a page for libraries toolink too-->
Questi passaggi possono differire leggermente in base al tipo di hello dell'app che si sta creando. Librerie open source possono indirizzare dettagli hello automaticamente.

## <a name="web-apps"></a>App Web
Per app Web (ad esempio .NET, PHP, Java, Ruby, Python e Node.js) ospitate in un server e accessibili tramite un browser, Azure AD B2C supporta [OpenID Connect](active-directory-b2c-reference-protocols.md) per tutte le esperienze utente, inclusa la gestione dell'iscrizione, dell'accesso e del profilo utente. Nell'implementazione di OpenID Connect hello Azure Active Directory B2C app web avvia queste esperienze utente inviando le richieste di autenticazione tooAzure Active Directory. Hello risultato della richiesta di hello è un `id_token`. Il token di sicurezza rappresenta l'identità dell'utente hello. Vengono inoltre fornite informazioni sull'utente hello in forma di hello di attestazioni:

```
// Partial raw id_token
eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6ImtyaU1QZG1Cd...

// Partial content of a decoded id_token
{
    "name": "John Smith",
    "email": "john.smith@gmail.com",
    "oid": "d9674823-dffc-4e3f-a6eb-62fe4bd48a58"
    ...
}
```

Ulteriori informazioni sui tipi di hello di token e attestazioni app tooan disponibile in hello [riferimento token B2C](active-directory-b2c-reference-tokens.md).

Nelle app Web, ogni esecuzione di [criteri](active-directory-b2c-reference-policies.md) include i passaggi generali seguenti:

![Immagine di corsie di app Web](./media/active-directory-b2c-apps/webapp.png)

Convalida di hello `id_token` utilizzando una chiave di firma pubblica che viene ricevuta da Azure AD è sufficiente identità di hello tooverify dell'utente hello. Consente anche di impostare un cookie di sessione che può essere utilizzato tooidentify hello utente nelle pagine successive richieste.

toosee questo scenario in azione, provare uno degli esempi di accesso di codice hello web app nel nostro [sezione Introduzione](active-directory-b2c-overview.md#get-started).

Aggiunta toofacilitating semplice sign-in, un'app di server web potrebbe essere necessario tooaccess un servizio back-end web. In questo caso, l'app web hello può eseguire leggermente diverso [OpenID Connect flusso](active-directory-b2c-reference-oidc.md) e acquisire i token con i codici di autorizzazione e token di aggiornamento. Questo scenario è illustrato nella seguente hello [sezione di Web API](#web-apis).

<!--, and in our [WebApp-WebAPI Getting started topic](active-directory-b2c-devquickstarts-web-api-dotnet.md).-->

## <a name="web-apis"></a>API Web
È possibile utilizzare servizi di Azure Active Directory B2C toosecure web, ad esempio API web RESTful dell'app. API Web può utilizzare toosecure OAuth 2.0 i propri dati, mediante l'autenticazione delle richieste HTTP in ingresso tramite i token. il chiamante di Hello di un'API web aggiunge un token nell'intestazione di autorizzazione hello di una richiesta HTTP:

```
GET /api/items HTTP/1.1
Host: www.mywebapi.com
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6...
Accept: application/json
...
```

API web Hello è quindi possibile utilizzare informazioni di identità e tooextract del chiamante di hello tooverify token hello API relative chiamante hello delle attestazioni che vengono codificate nel token hello. Ulteriori informazioni sui tipi di hello di token e attestazioni app tooan disponibile in hello [riferimento del token di Azure Active Directory B2C](active-directory-b2c-reference-tokens.md).

> [!NOTE]
> Azure AD B2C supporta attualmente solo API Web accessibili da propri client noti. Ad esempio, l'app completa può includere un'app per iOS, un'app per Android e un'API Web back-end. Questa architettura è completamente supportata. Consentendo ai client un partner, ad esempio un'altra app iOS, tooaccess hello stesso web che API non è attualmente supportato. Tutti i componenti di hello dell'applicazione completo devono condividere un ID applicazione singolo.
>
>

Un'API Web può ricevere token da molti tipi di client, tra cui app Web, app desktop e per dispositivi mobili, app a singola pagina, daemon sul lato server e altre API Web. Di seguito è riportato un esempio di flusso completo di hello per un'applicazione web che chiama un'API web:

![Immagine di corsie di API Web di app Web](./media/active-directory-b2c-apps/webapi.png)

toolearn ulteriori informazioni sui passaggi di hello per ottenere i token, i codici di autorizzazione e i token di aggiornamento a conoscenza hello [protocollo OAuth 2.0](active-directory-b2c-reference-oauth-code.md).

toolearn come toosecure un'API web con Azure Active Directory B2C, vedere hello web esercitazioni API nel nostro [sezione Introduzione](active-directory-b2c-overview.md#get-started).

## <a name="mobile-and-native-apps"></a>App per dispositivi mobili e native
Le app installate nei dispositivi, ad esempio le App per dispositivi mobili e desktop, è spesso necessario servizi back-end tooaccess o API web per conto degli utenti. È possibile aggiungere App native tooyour esperienze di gestione identità personalizzato e chiamare in modo sicuro i servizi back-end tramite Azure Active Directory B2C e hello [flusso di codice di autorizzazione OAuth 2.0](active-directory-b2c-reference-oauth-code.md).  

In questo flusso, viene eseguita l'applicazione hello [criteri](active-directory-b2c-reference-policies.md) e riceve un `authorization_code` da Azure Active Directory dopo il completamento di utente hello criteri hello. Hello `authorization_code` rappresenta hello servizi di back-end dell'app dell'autorizzazione toocall per conto di utenti hello è attualmente connesso. app Hello possono scambiare hello `authorization_code` in background hello per un `id_token` e `refresh_token`.  app Hello è possibile utilizzare hello `id_token` tooauthenticate tooa back-end API web nelle richieste HTTP. Inoltre possibile utilizzare hello `refresh_token` tooget un nuovo `id_token` dopo la scadenza di uno precedente.

> [!NOTE]
> Azure Active Directory B2C supporta attualmente solo i token che vengono utilizzati tooaccess un servizio web back-end dell'app. Ad esempio, l'app completa può includere un'app per iOS, un'app per Android e un'API Web back-end. Questa architettura è completamente supportata. Consentendo il tooaccess app iOS un'API web di partner con i token di accesso OAuth 2.0 non è attualmente supportato. Tutti i componenti di hello dell'applicazione completo devono condividere un ID applicazione singolo.
>
>

![Immagine di corsie di app native](./media/active-directory-b2c-apps/native.png)

## <a name="current-limitations"></a>Limitazioni correnti
Azure Active Directory B2C non supporta attualmente hello seguenti tipi di App, ma sono roadmap hello. 

### <a name="daemonsserver-side-apps"></a>App sul lato server o daemon
Le app che contengono i processi con esecuzione prolungata o che funzionano senza hello di un utente è inoltre necessario un modo tooaccess a risorse, ad esempio API web protette. Queste App possono eseguire l'autenticazione e di ottenere token utilizzando l'identità dell'applicazione hello (anziché l'identità dell'utente delegato) e tramite il flusso di credenziali client OAuth 2.0 hello.

Questo flusso non è attualmente supportato da Azure AD B2C. Le app possono ottenere i token solo dopo che si è verificato un flusso utente interattivo.

### <a name="web-api-chains-on-behalf-of-flow"></a>Catene di API Web (flusso On-Behalf-Of)
Molte architetture includono un'API che deve toocall web un'altra API web a valle, in cui entrambi sono protetti da Azure Active Directory B2C. Questo scenario è comune nei client nativi che hanno un back-end dell'API Web. Quindi chiama un servizio online Microsoft, ad esempio hello API Azure AD Graph.

Questo scenario di API web concatenate può essere supportato tramite la concessione di credenziali di hello JWT OAuth 2.0 connessione, noto anche come hello per conto di flusso.  Tuttavia, per conto di flusso di hello non è attualmente implementato in hello Azure Active Directory B2C.
