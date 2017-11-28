---
title: "aaaLearn sui protocolli di autorizzazione hello è supportato dalla versione 2.0 di Azure AD | Documenti Microsoft"
description: Tooprotocols di Guida supportato dall'endpoint di hello Azure AD versione 2.0.
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 5fb4fa1b-8fc4-438e-b3b0-258d8c145f22
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: f90511b1880ff223f725c1f79df9f79bddccc7bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# Protocolli v2.0 - OAuth 2.0 e OpenID Connect
endpoint di Hello v 2.0 è possibile utilizzare Azure AD per identità-as-a-service con protocolli standard del settore, OpenID Connect e OAuth 2.0.  Servizio di hello è conforme agli standard, possono esistere sottili differenze tra le due implementazioni di questi protocolli.  informazioni di Hello qui sarà utile se si sceglie toowrite codice inviando direttamente & gestisce le richieste HTTP o utilizzare un 3rd party aprire raccolta di origine, anziché utilizzare uno dei nostri librerie open source.
<!-- TODO: Need link toolibraries above -->

> [!NOTE]
> Non tutte le caratteristiche e gli scenari di Azure Active Directory sono supportati dall'endpoint di hello v 2.0.  toodetermine se è necessario utilizzare endpoint v 2.0 hello, conoscenza [limitazioni v 2.0](active-directory-v2-limitations.md).
>
>

## Hello nozioni di base
In quasi tutti i flussi OAuth e OpenID Connect, sono disponibili quattro parti coinvolte nello scambio hello:

![Ruoli di OAuth 2.0](../../media/active-directory-v2-flows/protocols_roles.png)

* Hello **Server autorizzazione** hello v 2.0 endpoint.  È responsabile di garantire l'identità dell'utente hello, concessione e revoca accesso tooresources e rilascio di token.  È anche noto come provider di identità hello - gestisce in modo sicuro un valore toodo con dell'utente hello informazioni loro accesso e le relazioni di trust hello tra entità in un flusso.
* Hello **proprietario della risorsa** è in genere l'utente finale di hello.  È parte di hello che possiede i dati di hello e ha hello power tooallow terzi tooaccess dei dati o risorse.
* Hello **OAuth Client** è l'applicazione, identificato dall'ID applicazione.  È in genere parte hello che dell'utente finale hello interagisce con e richiede un token dal server di autorizzazione hello.  client Hello devono essere concesse autorizzazioni tooaccess hello risorsa da proprietario della risorsa hello.
* Hello **Server delle risorse** in cui risiede la risorsa hello o dati.  Considera attendibile il Server di autorizzazione toosecurely autenticare e autorizzare hello OAuth Client di hello e Usa connessione tooensure access_tokens che accedono a risorse tooa può essere concessa.

## Registrazione delle app
Ogni applicazione che utilizza hello v 2.0 endpoint dovrà essere toobe registrato presso [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) prima può interagire tramite OAuth o OpenID Connect.  processo di registrazione applicazione Hello raccogliere & assegnare alcuni valori tooyour app:

* Un **ID applicazione** che identifica l'app in modo univoco
* Oggetto **URI di reindirizzamento** o **identificatore pacchetto** che può essere utilizzato toodirect risposte tooyour back-app
* Altri valori specifici dello scenario

Per ulteriori dettagli, informazioni su come troppo[registrare un'app](active-directory-v2-app-registration.md).

## Endpoint
Una volta registrato, hello applicazione comunica con Azure AD mediante l'invio di richieste toohello v 2.0 endpoint:

```
https://login.microsoftonline.com/{tenant}/oauth2/v2.0/authorize
https://login.microsoftonline.com/{tenant}/oauth2/v2.0/token
```

In cui hello `{tenant}` può assumere uno dei quattro valori diversi:

| Valore | Descrizione |
| --- | --- |
| `common` |Consente agli utenti con account Microsoft personale e gli account di lavoro o dell'istituto di istruzione da Azure Active Directory toosign in un'applicazione hello. |
| `organizations` |Consente solo agli utenti con account di lavoro o dell'istituto di istruzione da Azure Active Directory toosign in un'applicazione hello. |
| `consumers` |Consente solo agli utenti con toosign di account Microsoft personale in un'applicazione hello. |
| `8eaef023-2b34-4da1-9baa-8bc8c9d6a490` oppure `contoso.onmicrosoft.com` |Consente solo agli utenti con account di lavoro o dell'istituto di istruzione da un particolare toosign tenant Azure Active Directory in un'applicazione hello.  Il nome descrittivo di dominio hello di hello tenant di Azure AD o identificatore guid del tenant hello può essere utilizzato. |

Per ulteriori informazioni su come toointeract con questi endpoint, scegliere un tipo particolare app riportata di seguito.

## Tokens
implementazione di v 2.0 Hello di OAuth 2.0 e OpenID Connect usano ampiamente i token di connessione, inclusi i token di connessione rappresentati come Jwt. Un token di connessione è una risorsa protetta un token di sicurezza leggero che concede hello tooa accesso "bearer". In questo senso, hello "bearer" è qualsiasi entità che possono presentare token hello. Se un'entità deve prima autenticarsi con token di connessione di Azure AD tooreceive hello, se necessario di hello token hello toosecure durante la trasmissione e di archiviazione non vengono eseguite operazioni, può essere intercettato e usato da parti non autorizzate. Molti token di sicurezza hanno meccanismi integrati per prevenire l'uso non autorizzato, ma i token di connessione ne sono sprovvisti e devono essere trasportati su un canale protetto, ad esempio Transport Layer Security (HTTPS). Se un token viene trasmesso in crittografato hello, un attacco man-in hello può essere utilizzato da un token di hello tooacquire malintenzionato e utilizzarlo per una risorsa tooa protetto da accessi non autorizzati. Hello stessi principi di sicurezza si applicano quando l'archiviazione o la memorizzazione nella cache i token di connessione per un uso successivo. Assicurarsi sempre che l'app trasmetta e archivi i token di connessione in modo sicuro. Per altre considerazioni sulla sicurezza dei token di connessione, vedere la [sezione 5 della specifica RFC 6750](http://tools.ietf.org/html/rfc6750).

Ulteriori dettagli sui diversi tipi di token utilizzati nell'endpoint di hello v 2.0 è disponibile in [hello riferimento dell'endpoint token v 2.0](active-directory-v2-tokens.md).

## Protocolli
Se si è pronti toosee richiede alcuni esempi, iniziare con uno di hello seguito esercitazioni.  Ognuno di essi corrisponde tooa uno scenario di autenticazione specifico.  Se è necessario determinare quale sia il flusso di destra hello per la Guida, consultare [hello tipi di App, è possibile compilare con v 2.0 hello](active-directory-v2-flows.md).

* [Creazione di un’applicazione Mobile e Nativa con OAuth 2.0](active-directory-v2-protocols-oauth-code.md)
* [Creazione di Web App con collegamento ID Open](active-directory-v2-protocols-oidc.md)
* [Creare app di pagina singola con hello flusso di OAuth 2.0 impliciti](active-directory-v2-protocols-implicit.md)
* [Daemon o processi sul lato Server di compilazione con hello flusso credenziali Client di OAuth 2.0](active-directory-v2-protocols-oauth-client-creds.md)
* [Ottenere i token in un'API Web con hello OAuth 2.0 per conto di flusso](active-directory-v2-protocols-oauth-on-behalf-of.md)
