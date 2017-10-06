---
title: tipi di aaaApp per endpoint v 2.0 di Azure Active Directory hello | Documenti Microsoft
description: tipi di Hello di App e gli scenari supportati dall'endpoint di v 2.0 hello Azure Active Directory.
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 494a06b8-0f9b-44e1-a7a2-d728cf2077ae
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/01/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: db95c88d6865abac8ce80378ccd6b63cb38e0a01
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="app-types-for-hello-azure-active-directory-v20-endpoint"></a>Tipi di App per l'endpoint di v 2.0 hello Azure Active Directory
Hello Azure Active Directory (Azure AD) v 2.0 endpoint supporta l'autenticazione per un'ampia gamma di architetture di applicazioni moderne, tutti gli elementi basati su protocolli standard del settore [2.0 OAuth o OpenID Connect](active-directory-v2-protocols.md). Questo articolo descrive i tipi di hello di App che è possibile compilare utilizzando la versione 2.0 di Azure AD, indipendentemente dal fatto la lingua preferita o una piattaforma. informazioni in questo articolo Hello sono progettato toohelp la conoscenza degli scenari di alto livello prima di [iniziare a utilizzarla con codice hello](active-directory-appmodel-v2-overview.md#getting-started).

> [!NOTE]
> endpoint di Hello v 2.0 non supporta tutti gli scenari di Azure Active Directory e le funzionalità. toodetermine se è necessario utilizzare endpoint v 2.0 hello, conoscenza [limitazioni v 2.0](active-directory-v2-limitations.md).
> 
> 

## <a name="hello-basics"></a>Nozioni di base Hello
È necessario registrare ogni applicazione che utilizza endpoint v 2.0 hello in hello [portale di registrazione dell'applicazione Microsoft](https://apps.dev.microsoft.com). processo di registrazione applicazione Hello raccoglie e assegna i valori per l'app:

* Un **ID applicazione** che identifica l'app in modo univoco
* Oggetto **URI di reindirizzamento** che è possibile utilizzare toodirect risposte tooyour back-app
* Altri valori specifici dello scenario

Per informazioni dettagliate, vedere come troppo[registrare un'app](active-directory-v2-app-registration.md).

Dopo aver registrato l'applicazione hello, hello applicazione comunica con Azure AD mediante l'invio di richieste AD Azure toohello v 2.0 endpoint. Offriamo Framework open source e le librerie che gestiscono hello dettagli di queste richieste. È anche la logica di autenticazione hello opzione tooimplement hello manualmente tramite la creazione di endpoint toothese richieste:

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize
https://login.microsoftonline.com/common/oauth2/v2.0/token
```
<!-- TODO: Need a page for libraries toolink too-->

## <a name="web-apps"></a>App Web
Per le app web (.NET, PHP, Java, Ruby, Python, nodo) che hello accessi utente tramite un browser, è possibile utilizzare [OpenID Connect](active-directory-v2-protocols.md) per l'accesso utente. In OpenID Connect, app web hello riceve un ID token. Un token ID è un token di sicurezza che verifica l'identità dell'utente hello e fornisce informazioni sull'utente hello in forma di hello di attestazioni:

```
// Partial raw ID token
eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6ImtyaU1QZG1Cd...

// Partial content of a decoded ID token
{
    "name": "John Smith",
    "email": "john.smith@gmail.com",
    "oid": "d9674823-dffc-4e3f-a6eb-62fe4bd48a58"
    ...
}
```

È possibile acquisire informazioni tutti i tipi di token e attestazioni che sono disponibili tooan app in hello hello [v 2.0 token riferimento](active-directory-v2-tokens.md).

Nelle applicazioni server web, il flusso di accesso autenticazione hello accetta questi passaggi:

![Flusso di autenticazione dell'app Web](../../media/active-directory-v2-flows/convergence_scenarios_webapp.png)

È possibile verificare l'identità dell'utente hello convalidando i token ID hello con una chiave di firma pubblica che viene ricevuta dall'endpoint di hello v 2.0. È impostato un cookie di sessione, che può essere utente hello tooidentify utilizzato nelle pagine successive richieste.

esempi di questo scenario in azione, provare una delle hello codice app web Accedi toosee nostri v 2.0 [Introduzione](active-directory-appmodel-v2-overview.md#getting-started) sezione.

Inoltre toosimple Accedi, un'app di server web potrebbe essere necessario tooaccess un altro servizio web, ad esempio un'API REST. In questo caso, hello web server app scatta in un flusso OAuth 2.0 e di OpenID Connect combinato usando hello [flusso di codice di autorizzazione OAuth 2.0](active-directory-v2-protocols.md). Per altre informazioni su questo scenario, vedere l'[introduzione alle app Web e alle API Web](active-directory-v2-devquickstarts-webapp-webapi-dotnet.md).

## <a name="web-apis"></a>API Web
È possibile utilizzare hello v 2.0 endpoint toosecure servizi web, ad esempio API Web RESTful dell'app. Invece di token ID e i cookie di sessione, un'API Web utilizza un toosecure token di accesso OAuth 2.0, dati e tooauthenticate le richieste in ingresso. il chiamante Hello di un'API Web aggiunge un token di accesso nell'intestazione di autorizzazione hello di una richiesta HTTP, simile al seguente:

```
GET /api/items HTTP/1.1
Host: www.mywebapi.com
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6...
Accept: application/json
...
```

Hello API Web utilizza le informazioni di identità e tooextract hello accesso token tooverify hello API del chiamante sul chiamante hello delle attestazioni che vengono codificate nel token di accesso hello. toolearn su tutti i tipi di token e attestazioni che sono disponibili tooan app, hello vedere hello [v 2.0 token riferimento](active-directory-v2-tokens.md).

Un'API Web è possibile concedere agli utenti hello power tooopt in o rifiutare esplicitamente una funzionalità specifica o dati che espongono le autorizzazioni, noto anche come [ambiti](active-directory-v2-scopes.md). Per un chiamata app tooacquire tooa ambito di autorizzazione, utente hello deve consentire toohello ambito durante un flusso. endpoint v 2.0 Hello chiede l'autorizzazione utente hello e tale hello che API Web riceve registra le autorizzazioni in tutti i token di accesso. Hello API Web convalida i token di accesso hello riceve in ogni chiamata e vengono eseguiti controlli di autorizzazione.

Un'API Web può ricevere token di accesso da tutti i tipi di app, tra cui app per server Web, desktop, per dispositivi mobili, a singola pagina, daemon sul lato server e anche altre API Web. flusso di alto livello Hello per un'API Web è simile al seguente:

![Flusso di autenticazione dell'API Web](../../media/active-directory-v2-flows/convergence_scenarios_webapi.png)

toolearn come toosecure un'API Web tramite i token di accesso OAuth2, hello codice API Web, vedere esempi in questo [Introduzione](active-directory-appmodel-v2-overview.md#getting-started) sezione.

In molti casi, le API web è inoltre necessario toomake richieste in uscita a valle tooother web API protette da Azure Active Directory.  toodo in tal caso, API web può sfruttare i vantaggi di Azure AD **sul conto di** flusso, che consente di hello web API tooexchange un token di accesso in ingresso per un altro toobe token di accesso utilizzati nelle richieste in uscita.  Hello v 2.0 dell'endpoint per conto di flusso è descritta in [dettaglio qui](active-directory-v2-protocols-oauth-on-behalf-of.md).

## <a name="mobile-and-native-apps"></a>App per dispositivi mobili e native
Dispositivo installato App, ad esempio le App per dispositivi mobili e desktop, è spesso necessario servizi back-end tooaccess o API Web che memorizzano i dati e funzioni per conto dell'utente. Queste applicazioni è possono aggiungere servizi tooback-end di accesso e autorizzazione tramite hello [flusso di codice di autorizzazione OAuth 2.0](active-directory-v2-protocols-oauth-code.md).

In questo flusso app hello riceve un codice di autorizzazione dall'endpoint v 2.0 hello quando hello utente accede. autorizzazione toocall servizi back-end dell'autorizzazione codice rappresenta hello app Hello per conto di utenti hello è connesso. app Hello può scambiare il codice di autorizzazione hello in background hello per un token di accesso OAuth 2.0 e un token di aggiornamento. app Hello può utilizzare hello accesso token tooauthenticate tooWeb API nelle richieste HTTP e hello aggiornamento tooget token nuovi token di accesso alla scadenza del token di accesso meno recenti.

![Flusso di autenticazione dell'app nativa](../../media/active-directory-v2-flows/convergence_scenarios_native.png)

## <a name="single-page-apps-javascript"></a>App a singola pagina (JavaScript)
Molte app moderne hanno un front-end dell'app a singola pagina scritto principalmente in JavaScript. Il front-end viene scritto spesso usando un framework come AngularJS, Ember.js o Durandal. endpoint v 2.0 Hello Azure AD supporta queste App tramite hello [flusso implicito OAuth 2.0](active-directory-v2-protocols-implicit.md).

In questo flusso app hello ricevuto token direttamente da hello v 2.0 autorizza un endpoint, senza gli scambi di qualsiasi server a server. Tutti la logica di autenticazione e accetta di gestione delle sessioni inserire interamente nel client JavaScript hello, senza i reindirizzamenti di pagina aggiuntiva.

![Flusso di autenticazione implicita](../../media/active-directory-v2-flows/convergence_scenarios_implicit.png)

toosee questo scenario in azione, provare uno degli esempi di codice hello applicazione a una pagina nel nostro [Introduzione](active-directory-appmodel-v2-overview.md#getting-started) sezione.

## <a name="daemons-and-server-side-apps"></a>App daemon e lato server
Le applicazioni che dispongono di processi a esecuzione prolungata o che funzionano senza l'interazione con un utente necessario anche un modo tooaccess protetto risorse, ad esempio API Web. Queste App possono eseguire l'autenticazione e di ottenere token utilizzando l'identità dell'applicazione hello, piuttosto che un utente delega di identità, con il flusso di credenziali client OAuth 2.0 hello.

In questo flusso app hello interagisce direttamente con hello `/token` endpoint tooobtain endpoint:

![Flusso di autenticazione dell'app daemon](../../media/active-directory-v2-flows/convergence_scenarios_daemon.png)

toobuild un'applicazione daemon, vedere la documentazione di credenziali client hello in nostro [Introduzione](active-directory-appmodel-v2-overview.md#getting-started) sezione o provare un [applicazione di esempio .NET](https://github.com/Azure-Samples/active-directory-dotnet-daemon-v2).
