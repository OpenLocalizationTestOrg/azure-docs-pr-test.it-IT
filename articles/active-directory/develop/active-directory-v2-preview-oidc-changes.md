---
title: aaaChanges toohello AD Azure v 2.0 endpoint | Documenti Microsoft
description: Una descrizione delle modifiche che vengono effettuati i protocolli anteprima pubblica di toohello app modello v 2.0.
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: e6c5b891-0b5d-47dc-8184-5d0ef6a1a006
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/16/2016
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: d7b28a481e12d5dbbc4a10110193bdbd754f4929
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="important-updates-toohello-v20-authentication-protocols"></a>V 2.0 toohello aggiornamenti importanti protocolli di autenticazione
Nota per gli sviluppatori: Su hello due settimane successive, verrà rilasciato alcuni aggiornamenti i protocolli di autenticazione v 2.0 tooour che possono comportare modifiche per le applicazioni che è stato scritto durante il periodo di anteprima di rilievo.  

## <a name="who-does-this-affect"></a>Parti interessate
Qualsiasi App che sono stati scritti v 2.0 hello toouse convergente endpoint di autenticazione,

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize
```

Sono disponibili ulteriori informazioni sull'endpoint v 2.0 hello [qui](active-directory-appmodel-v2-overview.md).

Se creata un'app usando endpoint v 2.0 hello codificando toohello direttamente il protocollo v 2.0, utilizzando uno dei nostri middlewares di OpenID Connect o OAuth web o tramite altri 3 autenticazione tooperform librerie di terze parti, deve essere preparato tootest progetti e verificare eventuali modifiche necessarie.

## <a name="who-doesnt-this-affect"></a>Parti non interessate
Qualsiasi App che sono stati scritti su endpoint di autenticazione hello produzione AD Azure,

```
https://login.microsoftonline.com/common/oauth2/authorize
```

Questo protocollo è fisso e non subirà modifiche.

Inoltre, se l'app **solo** utilizza l'autenticazione tooperform la libreria ADAL, non sarà possibile toochange nulla.  ADAL è schermato app dalle modifiche hello.  

## <a name="what-are-hello-changes"></a>Quali sono le modifiche di hello?
### <a name="removing-hello-x5t-value-from-jwt-headers"></a>Rimozione di valore x5t hello dalle intestazioni JWT
Hello v 2.0 endpoint utilizza i token JWT, che contiene una sezione di intestazione parametri ai relativi metadati sul token hello.  Se si decodifica intestazione hello di uno dei nostri Jwt corrente, si otterrebbe simile al seguente:

```
{ 
    "type": "JWT",
    "alg": "RS256",
    "x5t": "MnC_VZcATfM5pOYiJHMba9goEKY",
    "kid": "MnC_VZcATfM5pOYiJHMba9goEKY"
}
```

In entrambe le proprietà "x5t" e "kid" hello identificano la chiave pubblica di hello che deve essere la firma del token di hello toovalidate utilizzati, così come viene recuperato dall'endpoint di metadati di OpenID Connect hello.

modifica di Hello che stiamo qui è proprietà hello "x5t" tooremove.  È possibile continuare hello toouse toovalidate meccanismi stesso token, ma è necessario basarsi solo sui hello "kid" proprietà tooretrieve hello chiave pubblica corretta, come specificato in hello protocollo OpenID Connect. 

> [!IMPORTANT]
> **Il processo: verificare che l'app non dipende dalla presenza hello del valore x5t hello.**
> 
> 

### <a name="removing-profileinfo"></a>Rimozione di profile_info
In precedenza, endpoint v 2.0 hello è stato restituendo un oggetto JSON con codificata base64 nelle risposte token chiamate `profile_info`.  Quando si richiede un token di accesso dall'endpoint v 2.0 hello inviando una richiesta per:

```
https://login.microsoftonline.com/common/oauth2/v2.0/token
```

risposta Hello sarebbe simile hello oggetto JSON seguente:

```
{ 
    "token_type": "Bearer",
    "expires_in": 3599,
    "scope": "https://outlook.office.com/mail.read",
    "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsI...",
    "refresh_token": "OAAABAAAAiL9Kn2Z27UubvWFPbm0gL...",
    "profile_info": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsI...",
}
```

Hello `profile_info` informazioni di valore contenuto utente hello che ha firmato in app hello: il nome visualizzato, nome, cognome, indirizzo di posta elettronica, identificatore e così via.  In primo luogo, hello `profile_info` usati per la memorizzazione nella cache di token e ai fini della visualizzazione.

Ora viene rimossa hello `profile_info` valore, ma niente paura, forniamo ancora questa toodevelopers informazioni in una posizione leggermente diversa.  Invece di `profile_info`, endpoint v 2.0 hello restituirà ora un `id_token` in ogni risposta token:

```
{ 
    "token_type": "Bearer",
    "expires_in": 3599,
    "scope": "https://outlook.office.com/mail.read",
    "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsI...",
    "refresh_token": "OAAABAAAAiL9Kn2Z27UubvWFPbm0gL...",
    "id_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsI...",
}
```

È possibile decodificare e analizzare hello id_token tooretrieve hello ricevuto da profile_info stesse informazioni.  Hello id_token è un JSON Web Token (JWT), con il contenuto come specificato da OpenID Connect.  Hello codice per questa operazione deve essere molto simile – è necessario semplicemente intermedio hello tooextract segmento (corpo hello) di id_token hello e base64 decodificarlo in oggetto JSON di hello tooaccess all'interno.

Su hello due settimane successive, è consigliabile codificare le informazioni sull'utente di app tooretrieve hello da entrambi hello `id_token` o `profile_info`; a seconda del valore è presente.  In questo modo, quando viene apportata la modifica hello, l'app è gestita senza transizione hello da `profile_info` troppo`id_token` senza interruzioni.

> [!IMPORTANT]
> **Il processo: verificare che l'app non dipende dalla presenza hello di hello `profile_info` valore.**
> 
> 

### <a name="removing-idtokenexpiresin"></a>Rimozione di id_token_expires_in
Simile troppo`profile_info`, viene anche rimossa hello `id_token_expires_in` parametro dalle risposte.  In precedenza, restituisce un valore per endpoint v 2.0 hello `id_token_expires_in` insieme a ogni risposta id_token, ad esempio in una risposta authorize:

```
https://myapp.com?id_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsI...&id_token_expires_in=3599...
```

O in una risposta del token:

```
{ 
    "token_type": "Bearer",
    "id_token_expires_in": 3599,
    "scope": "openid",
    "id_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsI...",
    "refresh_token": "OAAABAAAAiL9Kn2Z27UubvWFPbm0gL...",
    "profile_info": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsI...",
}
```

Hello `id_token_expires_in` valore indica il numero di hello di secondi hello id_token resta valido per.  A questo punto, viene rimossa hello `id_token_expires_in` valore completamente.  In alternativa, è possibile utilizzare standard di OpenID Connect hello `nbf` e `exp` validità hello tooexamine di un id_token di attestazioni.  Vedere hello [riferimento token v 2.0](active-directory-v2-tokens.md) per ulteriori informazioni su queste attestazioni.

> [!IMPORTANT]
> **Il processo: verificare che l'app non dipende dalla presenza hello di hello `id_token_expires_in` valore.**
> 
> 

### <a name="changing-hello-claims-returned-by-scopeopenid"></a>Modifica delle attestazioni hello restituita dall'ambito = openid
Questa modifica sarà hello più rilevante, infatti, influisce negativamente quasi tutte le applicazioni che utilizza hello v 2.0 endpoint.  Molte applicazioni invia richieste toohello v 2.0 endpoint utilizzando hello `openid` definire l'ambito, ad esempio:

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize?
client_id=...
&redirect_uri=...
&response_mode=form_post
&response_type=id_token
&scope=openid offline_access https://outlook.office.com/mail.read
```

Oggi, quando hello utente concede il consenso per hello `openid` ambito, l'app riceve una serie di informazioni sull'utente hello in hello id_token risultante.  Le attestazioni includono, ad esempio, il nome dell'utente, il nome utente preferito, l'indirizzo di posta elettronica, l'ID oggetto e altro ancora.

In questo aggiornamento, si sta modificando le informazioni di hello che hello `openid` ambito consente all'app l'accesso a comform toobetter con hello specifica OpenID Connect.  Hello `openid` ambito verrà solo consentire all'utente di hello app toosign in e ricevere un identificatore specifico dell'app per utente hello in hello `sub` attestazione di hello id_token.  Hello attestazioni in un id_token con solo hello `openid` ambito concessa sarà privo di informazioni personali.  Di seguito sono riportati alcuni esempi di attestazioni dell'id_token:

```
{ 
    "aud": "580e250c-8f26-49d0-bee8-1c078add1609",
    "iss": "https://login.microsoftonline.com/b9410318-09af-49c2-b0c3-653adc1f376e/v2.0 ",
    "iat": 1449520283,
    "nbf": 1449520283,
    "exp": 1449524183,
    "nonce": "12345",
    "sub": "MF4f-ggWMEji12KynJUNQZphaUTvLcQug5jdF2nl01Q",
    "tid": "b9410318-09af-49c2-b0c3-653adc1f376e",
    "ver": "2.0",
}
```

Se si desiderano tooobtain informazioni personali (PII) sull'utente hello nell'app, necessarie per l'app toorequest ulteriori autorizzazioni utente hello.  Microsoft sta introducendo il supporto per due nuovi ambiti dalla specifica di OpenID Connect hello: hello `email` e `profile` ambiti, che consentono di toodo così.

* Hello `email` ambito è molto semplice: consente l'indirizzo di posta elettronica principale dell'utente le app accesso toohello tramite hello `email` id_token hello di attestazione.  Si noti che hello `email` attestazione non sempre è presente in id_tokens: solo verrà incluso se è disponibile nel profilo dell'utente hello.
* Hello `profile` ambito mette a disposizione il tooall accesso app altre informazioni di base sull'utente hello-loro nome, nome utente preferito, ID di oggetto e così via.

In questo modo è toocode l'app in maniera minima riservatezza: è possibile richiedere utente hello solo i set di hello di informazioni che l'app richiede toodo relativo processo.  Se si desidera toocontinue recupero set completo di hello di informazioni sull'utente che sta ricevendo l'app, è necessario includere tutti e tre gli ambiti delle richieste di autorizzazione:

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize?
client_id=...
&redirect_uri=...
&response_mode=form_post
&response_type=id_token
&scope=openid profile email offline_access https://outlook.office.com/mail.read
```

L'app è possibile iniziare l'invio di hello `email` e `profile` immediatamente gli ambiti e hello v 2.0 endpoint verrà accettare questi due ambiti e iniziare la richiesta di autorizzazioni agli utenti in base alle esigenze.  Tuttavia, non modificare hello interpretazione hello di hello `openid` ambito verrà rese effettive per alcune settimane.

> [!IMPORTANT]
> **Il processo: Aggiungi hello `profile` e `email` ambiti se l'app richiede informazioni sull'utente hello.**  Si noti che ADAL includerà entrambe le autorizzazioni nelle richieste per impostazione predefinita. 
> 
> 

### <a name="removing-hello-issuer-trailing-slash"></a>Rimozione hello dell'autorità di certificazione con una barra finale.
In precedenza, hello dell'autorità di certificazione che viene visualizzato nel token dall'endpoint v 2.0 hello impiegato modulo hello

```
https://login.microsoftonline.com/{some-guid}/v2.0/
```

Guid hello in cui è tenantId hello del tenant hello Azure AD che ha rilasciato il token hello.  Con queste modifiche, il valore di autorità di certificazione hello diventa

```
https://login.microsoftonline.com/{some-guid}/v2.0 
```

in entrambi i token e nel documento di individuazione OpenID Connect hello.

> [!IMPORTANT]
> **Il processo: verificare che l'applicazione accetta un valore dell'autorità di certificazione hello con e senza una barra finale durante la convalida dell'autorità di certificazione.**
> 
> 

## <a name="why-change"></a>Perché cambiare
obiettivo principale di Hello per l'introduzione di queste modifiche è toobe conformi con hello OpenID Connect specifica standard.  Essendo OpenID Connect conforme, ci auguriamo che toominimize le differenze tra l'integrazione con servizi di identità Microsoft e con altri servizi di identità nel settore hello.  Vogliamo tooenable sviluppatori toouse le librerie di autenticazione open source preferita senza differenze di tooalter hello librerie tooaccommodate Microsoft.

## <a name="what-can-you-do"></a>Cosa fare
A partire da oggi, si può iniziare a creare tutte le modifiche di hello descritte in precedenza.  Nell'immediato:

1. **Rimuovere tutte le dipendenze da hello `x5t` parametro header.**
2. **Gestire correttamente la transizione hello da `profile_info` troppo`id_token` nelle risposte token.**
3. **Rimuovere tutte le dipendenze da hello `id_token_expires_in` parametro di risposta.**
4. **Aggiungere hello `profile` e `email` ambiti tooyour app se l'applicazione necessita di informazioni utente di base.**
5. **Accettare i valori dell'autorità di certificazione nei token con e senza una barra finale.**

Il nostro [documentazione relativa al protocollo v 2.0](active-directory-v2-protocols.md) è già stato aggiornato tooreflect queste modifiche, è possibile utilizzarlo come riferimento per consentire di aggiornare il codice.

Se si dispone di ulteriori domande sull'ambito hello delle modifiche di hello, è possibile tooreach libero out toous su Twitter in @AzureAD.

## <a name="how-often-will-protocol-changes-occur"></a>Frequenza delle modifiche ai protocolli
È non prevede altre importanti modifiche toohello i protocolli di autenticazione.  È intenzionalmente stiamo unendo le modifiche in una versione in modo che non sarà possibile toogo tramite questo tipo di processo di aggiornamento nuovamente nel prossimo futuro.  Naturalmente, continueremo tooadd funzionalità toohello convergente v 2.0 i servizio di autenticazione che è possibile trarre vantaggio da, ma tali modifiche devono essere additivo e non si interromperà il codice esistente.

Infine, desideriamo toosay grazie per provare operazioni durante il periodo di anteprima di hello.  esperienze dei nostri adottato e approfondimenti Hello sono state preziose finora e ci auguriamo che si continuerà a tooshare le opinioni e idee.

Buon lavoro.

Divisione di identità Microsoft Hello

