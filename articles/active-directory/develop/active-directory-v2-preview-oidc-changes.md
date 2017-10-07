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
# <a name="important-updates-toohello-v20-authentication-protocols"></a><span data-ttu-id="becfa-103">V 2.0 toohello aggiornamenti importanti protocolli di autenticazione</span><span class="sxs-lookup"><span data-stu-id="becfa-103">Important Updates toohello v2.0 Authentication Protocols</span></span>
<span data-ttu-id="becfa-104">Nota per gli sviluppatori:</span><span class="sxs-lookup"><span data-stu-id="becfa-104">Attention developers!</span></span> <span data-ttu-id="becfa-105">Su hello due settimane successive, verrà rilasciato alcuni aggiornamenti i protocolli di autenticazione v 2.0 tooour che possono comportare modifiche per le applicazioni che è stato scritto durante il periodo di anteprima di rilievo.</span><span class="sxs-lookup"><span data-stu-id="becfa-105">Over hello next two weeks, we will be making a few updates tooour v2.0 authentication protocols that may mean breaking changes for any apps you have written during our preview period.</span></span>  

## <a name="who-does-this-affect"></a><span data-ttu-id="becfa-106">Parti interessate</span><span class="sxs-lookup"><span data-stu-id="becfa-106">Who does this affect?</span></span>
<span data-ttu-id="becfa-107">Qualsiasi App che sono stati scritti v 2.0 hello toouse convergente endpoint di autenticazione,</span><span class="sxs-lookup"><span data-stu-id="becfa-107">Any apps that have been written toouse hello v2.0 converged authentication endpoint,</span></span>

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize
```

<span data-ttu-id="becfa-108">Sono disponibili ulteriori informazioni sull'endpoint v 2.0 hello [qui](active-directory-appmodel-v2-overview.md).</span><span class="sxs-lookup"><span data-stu-id="becfa-108">More information on hello v2.0 endpoint can be found [here](active-directory-appmodel-v2-overview.md).</span></span>

<span data-ttu-id="becfa-109">Se creata un'app usando endpoint v 2.0 hello codificando toohello direttamente il protocollo v 2.0, utilizzando uno dei nostri middlewares di OpenID Connect o OAuth web o tramite altri 3 autenticazione tooperform librerie di terze parti, deve essere preparato tootest progetti e verificare eventuali modifiche necessarie.</span><span class="sxs-lookup"><span data-stu-id="becfa-109">If you have built an app using hello v2.0 endpoint by coding directly toohello v2.0 protocol, using any of our OpenID Connect or OAuth web middlewares, or using other 3rd party libraries tooperform authentication, you should be prepared tootest your projects and make changes if necessary.</span></span>

## <a name="who-doesnt-this-affect"></a><span data-ttu-id="becfa-110">Parti non interessate</span><span class="sxs-lookup"><span data-stu-id="becfa-110">Who doesn\`t this affect?</span></span>
<span data-ttu-id="becfa-111">Qualsiasi App che sono stati scritti su endpoint di autenticazione hello produzione AD Azure,</span><span class="sxs-lookup"><span data-stu-id="becfa-111">Any apps that have been written against hello production Azure AD authentication endpoint,</span></span>

```
https://login.microsoftonline.com/common/oauth2/authorize
```

<span data-ttu-id="becfa-112">Questo protocollo è fisso e non subirà modifiche.</span><span class="sxs-lookup"><span data-stu-id="becfa-112">This protocol is set in stone and will not be experiencing any changes.</span></span>

<span data-ttu-id="becfa-113">Inoltre, se l'app **solo** utilizza l'autenticazione tooperform la libreria ADAL, non sarà possibile toochange nulla.</span><span class="sxs-lookup"><span data-stu-id="becfa-113">Furthermore, if your app **only** uses our ADAL library tooperform authentication, you won\`t have toochange anything.</span></span>  <span data-ttu-id="becfa-114">ADAL è schermato app dalle modifiche hello.</span><span class="sxs-lookup"><span data-stu-id="becfa-114">ADAL has shielded your app from hello changes.</span></span>  

## <a name="what-are-hello-changes"></a><span data-ttu-id="becfa-115">Quali sono le modifiche di hello?</span><span class="sxs-lookup"><span data-stu-id="becfa-115">What are hello changes?</span></span>
### <a name="removing-hello-x5t-value-from-jwt-headers"></a><span data-ttu-id="becfa-116">Rimozione di valore x5t hello dalle intestazioni JWT</span><span class="sxs-lookup"><span data-stu-id="becfa-116">Removing hello x5t value from JWT headers</span></span>
<span data-ttu-id="becfa-117">Hello v 2.0 endpoint utilizza i token JWT, che contiene una sezione di intestazione parametri ai relativi metadati sul token hello.</span><span class="sxs-lookup"><span data-stu-id="becfa-117">hello v2.0 endpoint uses JWT tokens extensively, which contain a header parameters section with relevant metadata about hello token.</span></span>  <span data-ttu-id="becfa-118">Se si decodifica intestazione hello di uno dei nostri Jwt corrente, si otterrebbe simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="becfa-118">If you decode hello header of one of our current JWTs, you would find something like:</span></span>

```
{ 
    "type": "JWT",
    "alg": "RS256",
    "x5t": "MnC_VZcATfM5pOYiJHMba9goEKY",
    "kid": "MnC_VZcATfM5pOYiJHMba9goEKY"
}
```

<span data-ttu-id="becfa-119">In entrambe le proprietà "x5t" e "kid" hello identificano la chiave pubblica di hello che deve essere la firma del token di hello toovalidate utilizzati, così come viene recuperato dall'endpoint di metadati di OpenID Connect hello.</span><span class="sxs-lookup"><span data-stu-id="becfa-119">Where both hello "x5t" and "kid" properties identify hello public key that should be used toovalidate hello token\`s signature, as retrieved from hello OpenID Connect metadata endpoint.</span></span>

<span data-ttu-id="becfa-120">modifica di Hello che stiamo qui è proprietà hello "x5t" tooremove.</span><span class="sxs-lookup"><span data-stu-id="becfa-120">hello change we are making here is tooremove hello "x5t" property.</span></span>  <span data-ttu-id="becfa-121">È possibile continuare hello toouse toovalidate meccanismi stesso token, ma è necessario basarsi solo sui hello "kid" proprietà tooretrieve hello chiave pubblica corretta, come specificato in hello protocollo OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="becfa-121">You may continue toouse hello same mechanisms toovalidate tokens, but should rely only on hello "kid" property tooretrieve hello correct public key, as specified in hello OpenID Connect protocol.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="becfa-122">**Il processo: verificare che l'app non dipende dalla presenza hello del valore x5t hello.**</span><span class="sxs-lookup"><span data-stu-id="becfa-122">**Your job: Make sure your app does not depend on hello existence of hello x5t value.**</span></span>
> 
> 

### <a name="removing-profileinfo"></a><span data-ttu-id="becfa-123">Rimozione di profile_info</span><span class="sxs-lookup"><span data-stu-id="becfa-123">Removing profile_info</span></span>
<span data-ttu-id="becfa-124">In precedenza, endpoint v 2.0 hello è stato restituendo un oggetto JSON con codificata base64 nelle risposte token chiamate `profile_info`.</span><span class="sxs-lookup"><span data-stu-id="becfa-124">Previously, hello v2.0 endpoint has been returning a base64 encoded JSON object in token responses called `profile_info`.</span></span>  <span data-ttu-id="becfa-125">Quando si richiede un token di accesso dall'endpoint v 2.0 hello inviando una richiesta per:</span><span class="sxs-lookup"><span data-stu-id="becfa-125">When requesting an access token from hello v2.0 endpoint by sending a request to:</span></span>

```
https://login.microsoftonline.com/common/oauth2/v2.0/token
```

<span data-ttu-id="becfa-126">risposta Hello sarebbe simile hello oggetto JSON seguente:</span><span class="sxs-lookup"><span data-stu-id="becfa-126">hello response would look like hello following JSON object:</span></span>

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

<span data-ttu-id="becfa-127">Hello `profile_info` informazioni di valore contenuto utente hello che ha firmato in app hello: il nome visualizzato, nome, cognome, indirizzo di posta elettronica, identificatore e così via.</span><span class="sxs-lookup"><span data-stu-id="becfa-127">hello `profile_info` value contained information about hello user who signed into hello app - their display name, first name, surname, email address, identifier, and so on.</span></span>  <span data-ttu-id="becfa-128">In primo luogo, hello `profile_info` usati per la memorizzazione nella cache di token e ai fini della visualizzazione.</span><span class="sxs-lookup"><span data-stu-id="becfa-128">Primarily, hello `profile_info` was used for token caching and display purposes.</span></span>

<span data-ttu-id="becfa-129">Ora viene rimossa hello `profile_info` valore, ma niente paura, forniamo ancora questa toodevelopers informazioni in una posizione leggermente diversa.</span><span class="sxs-lookup"><span data-stu-id="becfa-129">We are now removing hello `profile_info` value – but don't worry, we are still providing this information toodevelopers in a slightly different place.</span></span>  <span data-ttu-id="becfa-130">Invece di `profile_info`, endpoint v 2.0 hello restituirà ora un `id_token` in ogni risposta token:</span><span class="sxs-lookup"><span data-stu-id="becfa-130">Instead of `profile_info`, hello v2.0 endpoint will now return an `id_token` in each token response:</span></span>

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

<span data-ttu-id="becfa-131">È possibile decodificare e analizzare hello id_token tooretrieve hello ricevuto da profile_info stesse informazioni.</span><span class="sxs-lookup"><span data-stu-id="becfa-131">You may decode and parse hello id_token tooretrieve hello same information that you received from profile_info.</span></span>  <span data-ttu-id="becfa-132">Hello id_token è un JSON Web Token (JWT), con il contenuto come specificato da OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="becfa-132">hello id_token is a JSON Web Token (JWT), with contents as specified by OpenID Connect.</span></span>  <span data-ttu-id="becfa-133">Hello codice per questa operazione deve essere molto simile – è necessario semplicemente intermedio hello tooextract segmento (corpo hello) di id_token hello e base64 decodificarlo in oggetto JSON di hello tooaccess all'interno.</span><span class="sxs-lookup"><span data-stu-id="becfa-133">hello code for doing so should be very similar – you simply need tooextract hello middle segment (hello body) of hello id_token and base64 decode it tooaccess hello JSON object within.</span></span>

<span data-ttu-id="becfa-134">Su hello due settimane successive, è consigliabile codificare le informazioni sull'utente di app tooretrieve hello da entrambi hello `id_token` o `profile_info`; a seconda del valore è presente.</span><span class="sxs-lookup"><span data-stu-id="becfa-134">Over hello next two weeks, you should code your app tooretrieve hello user information from either hello `id_token` or `profile_info`; whichever is present.</span></span>  <span data-ttu-id="becfa-135">In questo modo, quando viene apportata la modifica hello, l'app è gestita senza transizione hello da `profile_info` troppo`id_token` senza interruzioni.</span><span class="sxs-lookup"><span data-stu-id="becfa-135">That way when hello change is made, your app can seamlessly handle hello transition from `profile_info` too`id_token` without interruption.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="becfa-136">**Il processo: verificare che l'app non dipende dalla presenza hello di hello `profile_info` valore.**</span><span class="sxs-lookup"><span data-stu-id="becfa-136">**Your job: Make sure your app does not depend on hello existence of hello `profile_info` value.**</span></span>
> 
> 

### <a name="removing-idtokenexpiresin"></a><span data-ttu-id="becfa-137">Rimozione di id_token_expires_in</span><span class="sxs-lookup"><span data-stu-id="becfa-137">Removing id_token_expires_in</span></span>
<span data-ttu-id="becfa-138">Simile troppo`profile_info`, viene anche rimossa hello `id_token_expires_in` parametro dalle risposte.</span><span class="sxs-lookup"><span data-stu-id="becfa-138">Similar too`profile_info`, we are also removing hello `id_token_expires_in` parameter from responses.</span></span>  <span data-ttu-id="becfa-139">In precedenza, restituisce un valore per endpoint v 2.0 hello `id_token_expires_in` insieme a ogni risposta id_token, ad esempio in una risposta authorize:</span><span class="sxs-lookup"><span data-stu-id="becfa-139">Previously, hello v2.0 endpoint would return a value for `id_token_expires_in` along with each id_token response, for instance in an authorize response:</span></span>

```
https://myapp.com?id_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsI...&id_token_expires_in=3599...
```

<span data-ttu-id="becfa-140">O in una risposta del token:</span><span class="sxs-lookup"><span data-stu-id="becfa-140">Or in a token response:</span></span>

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

<span data-ttu-id="becfa-141">Hello `id_token_expires_in` valore indica il numero di hello di secondi hello id_token resta valido per.</span><span class="sxs-lookup"><span data-stu-id="becfa-141">hello `id_token_expires_in` value would indicate hello number of seconds hello id_token would remain valid for.</span></span>  <span data-ttu-id="becfa-142">A questo punto, viene rimossa hello `id_token_expires_in` valore completamente.</span><span class="sxs-lookup"><span data-stu-id="becfa-142">Now, we are removing hello `id_token_expires_in` value completely.</span></span>  <span data-ttu-id="becfa-143">In alternativa, è possibile utilizzare standard di OpenID Connect hello `nbf` e `exp` validità hello tooexamine di un id_token di attestazioni.</span><span class="sxs-lookup"><span data-stu-id="becfa-143">Instead, you may use hello OpenID Connect standard `nbf` and `exp` claims tooexamine hello validity of an id_token.</span></span>  <span data-ttu-id="becfa-144">Vedere hello [riferimento token v 2.0](active-directory-v2-tokens.md) per ulteriori informazioni su queste attestazioni.</span><span class="sxs-lookup"><span data-stu-id="becfa-144">See hello [v2.0 token reference](active-directory-v2-tokens.md) for more information on these claims.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="becfa-145">**Il processo: verificare che l'app non dipende dalla presenza hello di hello `id_token_expires_in` valore.**</span><span class="sxs-lookup"><span data-stu-id="becfa-145">**Your job: Make sure your app does not depend on hello existence of hello `id_token_expires_in` value.**</span></span>
> 
> 

### <a name="changing-hello-claims-returned-by-scopeopenid"></a><span data-ttu-id="becfa-146">Modifica delle attestazioni hello restituita dall'ambito = openid</span><span class="sxs-lookup"><span data-stu-id="becfa-146">Changing hello claims returned by scope=openid</span></span>
<span data-ttu-id="becfa-147">Questa modifica sarà hello più rilevante, infatti, influisce negativamente quasi tutte le applicazioni che utilizza hello v 2.0 endpoint.</span><span class="sxs-lookup"><span data-stu-id="becfa-147">This change will be hello most significant – in fact, it will affect almost every app that uses hello v2.0 endpoint.</span></span>  <span data-ttu-id="becfa-148">Molte applicazioni invia richieste toohello v 2.0 endpoint utilizzando hello `openid` definire l'ambito, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="becfa-148">Many applications send requests toohello v2.0 endpoint using hello `openid` scope, like:</span></span>

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize?
client_id=...
&redirect_uri=...
&response_mode=form_post
&response_type=id_token
&scope=openid offline_access https://outlook.office.com/mail.read
```

<span data-ttu-id="becfa-149">Oggi, quando hello utente concede il consenso per hello `openid` ambito, l'app riceve una serie di informazioni sull'utente hello in hello id_token risultante.</span><span class="sxs-lookup"><span data-stu-id="becfa-149">Today, when hello user grants consent for hello `openid` scope, your app receives a wealth of information about hello user in hello resulting id_token.</span></span>  <span data-ttu-id="becfa-150">Le attestazioni includono, ad esempio, il nome dell'utente, il nome utente preferito, l'indirizzo di posta elettronica, l'ID oggetto e altro ancora.</span><span class="sxs-lookup"><span data-stu-id="becfa-150">These claims can include their name, preferred username, email address, object ID, and more.</span></span>

<span data-ttu-id="becfa-151">In questo aggiornamento, si sta modificando le informazioni di hello che hello `openid` ambito consente all'app l'accesso a comform toobetter con hello specifica OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="becfa-151">In this update, we are changing hello information that hello `openid` scope affords your app access to, toobetter comform with hello OpenID Connect specification.</span></span>  <span data-ttu-id="becfa-152">Hello `openid` ambito verrà solo consentire all'utente di hello app toosign in e ricevere un identificatore specifico dell'app per utente hello in hello `sub` attestazione di hello id_token.</span><span class="sxs-lookup"><span data-stu-id="becfa-152">hello `openid` scope will only allow your app toosign hello user in, and receive an app-specific identifier for hello user in hello `sub` claim of hello id_token.</span></span>  <span data-ttu-id="becfa-153">Hello attestazioni in un id_token con solo hello `openid` ambito concessa sarà privo di informazioni personali.</span><span class="sxs-lookup"><span data-stu-id="becfa-153">hello claims in an id_token with only hello `openid` scope granted will be devoid of any personally identifiable information.</span></span>  <span data-ttu-id="becfa-154">Di seguito sono riportati alcuni esempi di attestazioni dell'id_token:</span><span class="sxs-lookup"><span data-stu-id="becfa-154">Example id_token claims are:</span></span>

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

<span data-ttu-id="becfa-155">Se si desiderano tooobtain informazioni personali (PII) sull'utente hello nell'app, necessarie per l'app toorequest ulteriori autorizzazioni utente hello.</span><span class="sxs-lookup"><span data-stu-id="becfa-155">If you want tooobtain personally identifiable information (PII) about hello user in your app, your app will need toorequest additional permissions from hello user.</span></span>  <span data-ttu-id="becfa-156">Microsoft sta introducendo il supporto per due nuovi ambiti dalla specifica di OpenID Connect hello: hello `email` e `profile` ambiti, che consentono di toodo così.</span><span class="sxs-lookup"><span data-stu-id="becfa-156">We are introducing support for two new scopes from hello OpenID Connect spec – hello `email` and `profile` scopes – which allow you toodo so.</span></span>

* <span data-ttu-id="becfa-157">Hello `email` ambito è molto semplice: consente l'indirizzo di posta elettronica principale dell'utente le app accesso toohello tramite hello `email` id_token hello di attestazione.</span><span class="sxs-lookup"><span data-stu-id="becfa-157">hello `email` scope is very straightforward – it allows your app access toohello user's primary email address via hello `email` claim in hello id_token.</span></span>  <span data-ttu-id="becfa-158">Si noti che hello `email` attestazione non sempre è presente in id_tokens: solo verrà incluso se è disponibile nel profilo dell'utente hello.</span><span class="sxs-lookup"><span data-stu-id="becfa-158">Note that hello `email` claim will not always be present in id_tokens – it will only be included if available in hello user's profile.</span></span>
* <span data-ttu-id="becfa-159">Hello `profile` ambito mette a disposizione il tooall accesso app altre informazioni di base sull'utente hello-loro nome, nome utente preferito, ID di oggetto e così via.</span><span class="sxs-lookup"><span data-stu-id="becfa-159">hello `profile` scope affords your app access tooall other basic information about hello user – their name, preferred username, object ID, and so on.</span></span>

<span data-ttu-id="becfa-160">In questo modo è toocode l'app in maniera minima riservatezza: è possibile richiedere utente hello solo i set di hello di informazioni che l'app richiede toodo relativo processo.</span><span class="sxs-lookup"><span data-stu-id="becfa-160">This allows you toocode your app in a minimal-disclosure fashion – you can ask hello user for just hello set of information that your app requires toodo its job.</span></span>  <span data-ttu-id="becfa-161">Se si desidera toocontinue recupero set completo di hello di informazioni sull'utente che sta ricevendo l'app, è necessario includere tutti e tre gli ambiti delle richieste di autorizzazione:</span><span class="sxs-lookup"><span data-stu-id="becfa-161">If you want toocontinue getting hello full set of user information that your app is currently receiving, you should include all three scopes in your authorization requests:</span></span>

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize?
client_id=...
&redirect_uri=...
&response_mode=form_post
&response_type=id_token
&scope=openid profile email offline_access https://outlook.office.com/mail.read
```

<span data-ttu-id="becfa-162">L'app è possibile iniziare l'invio di hello `email` e `profile` immediatamente gli ambiti e hello v 2.0 endpoint verrà accettare questi due ambiti e iniziare la richiesta di autorizzazioni agli utenti in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="becfa-162">Your app can begin sending hello `email` and `profile` scopes immediately, and hello v2.0 endpoint will accept these two scopes and begin requesting permissions from users as necessary.</span></span>  <span data-ttu-id="becfa-163">Tuttavia, non modificare hello interpretazione hello di hello `openid` ambito verrà rese effettive per alcune settimane.</span><span class="sxs-lookup"><span data-stu-id="becfa-163">However, hello change in hello interpretation of hello `openid` scope will not take effect for a few weeks.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="becfa-164">**Il processo: Aggiungi hello `profile` e `email` ambiti se l'app richiede informazioni sull'utente hello.**</span><span class="sxs-lookup"><span data-stu-id="becfa-164">**Your job: Add hello `profile` and `email` scopes if your app requires information about hello user.**</span></span>  <span data-ttu-id="becfa-165">Si noti che ADAL includerà entrambe le autorizzazioni nelle richieste per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="becfa-165">Note that ADAL will include both of these permissions in requests by default.</span></span> 
> 
> 

### <a name="removing-hello-issuer-trailing-slash"></a><span data-ttu-id="becfa-166">Rimozione hello dell'autorità di certificazione con una barra finale.</span><span class="sxs-lookup"><span data-stu-id="becfa-166">Removing hello issuer trailing slash.</span></span>
<span data-ttu-id="becfa-167">In precedenza, hello dell'autorità di certificazione che viene visualizzato nel token dall'endpoint v 2.0 hello impiegato modulo hello</span><span class="sxs-lookup"><span data-stu-id="becfa-167">Previously, hello issuer value that appears in tokens from hello v2.0 endpoint took hello form</span></span>

```
https://login.microsoftonline.com/{some-guid}/v2.0/
```

<span data-ttu-id="becfa-168">Guid hello in cui è tenantId hello del tenant hello Azure AD che ha rilasciato il token hello.</span><span class="sxs-lookup"><span data-stu-id="becfa-168">Where hello guid was hello tenantId of hello Azure AD tenant which issued hello token.</span></span>  <span data-ttu-id="becfa-169">Con queste modifiche, il valore di autorità di certificazione hello diventa</span><span class="sxs-lookup"><span data-stu-id="becfa-169">With these changes, hello issuer value becomes</span></span>

```
https://login.microsoftonline.com/{some-guid}/v2.0 
```

<span data-ttu-id="becfa-170">in entrambi i token e nel documento di individuazione OpenID Connect hello.</span><span class="sxs-lookup"><span data-stu-id="becfa-170">in both tokens and in hello OpenID Connect discovery document.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="becfa-171">**Il processo: verificare che l'applicazione accetta un valore dell'autorità di certificazione hello con e senza una barra finale durante la convalida dell'autorità di certificazione.**</span><span class="sxs-lookup"><span data-stu-id="becfa-171">**Your job: Make sure your app accepts hello issuer value both with and without a trailing slash during issuer validation.**</span></span>
> 
> 

## <a name="why-change"></a><span data-ttu-id="becfa-172">Perché cambiare</span><span class="sxs-lookup"><span data-stu-id="becfa-172">Why change?</span></span>
<span data-ttu-id="becfa-173">obiettivo principale di Hello per l'introduzione di queste modifiche è toobe conformi con hello OpenID Connect specifica standard.</span><span class="sxs-lookup"><span data-stu-id="becfa-173">hello primary motivation for introducing these changes is toobe compliant with hello OpenID Connect standard specification.</span></span>  <span data-ttu-id="becfa-174">Essendo OpenID Connect conforme, ci auguriamo che toominimize le differenze tra l'integrazione con servizi di identità Microsoft e con altri servizi di identità nel settore hello.</span><span class="sxs-lookup"><span data-stu-id="becfa-174">By being OpenID Connect compliant, we hope toominimize differences between integrating with Microsoft identity services and with other identity services in hello industry.</span></span>  <span data-ttu-id="becfa-175">Vogliamo tooenable sviluppatori toouse le librerie di autenticazione open source preferita senza differenze di tooalter hello librerie tooaccommodate Microsoft.</span><span class="sxs-lookup"><span data-stu-id="becfa-175">We want tooenable developers toouse their favorite open source authentication libraries without having tooalter hello libraries tooaccommodate Microsoft differences.</span></span>

## <a name="what-can-you-do"></a><span data-ttu-id="becfa-176">Cosa fare</span><span class="sxs-lookup"><span data-stu-id="becfa-176">What can you do?</span></span>
<span data-ttu-id="becfa-177">A partire da oggi, si può iniziare a creare tutte le modifiche di hello descritte in precedenza.</span><span class="sxs-lookup"><span data-stu-id="becfa-177">As of today, you can begin making all of hello changes described above.</span></span>  <span data-ttu-id="becfa-178">Nell'immediato:</span><span class="sxs-lookup"><span data-stu-id="becfa-178">You should immediately:</span></span>

1. <span data-ttu-id="becfa-179">**Rimuovere tutte le dipendenze da hello `x5t` parametro header.**</span><span class="sxs-lookup"><span data-stu-id="becfa-179">**Remove any dependencies on hello `x5t` header parameter.**</span></span>
2. <span data-ttu-id="becfa-180">**Gestire correttamente la transizione hello da `profile_info` troppo`id_token` nelle risposte token.**</span><span class="sxs-lookup"><span data-stu-id="becfa-180">**Gracefully handle hello transition from `profile_info` too`id_token` in token responses.**</span></span>
3. <span data-ttu-id="becfa-181">**Rimuovere tutte le dipendenze da hello `id_token_expires_in` parametro di risposta.**</span><span class="sxs-lookup"><span data-stu-id="becfa-181">**Remove any dependencies on hello `id_token_expires_in` response parameter.**</span></span>
4. <span data-ttu-id="becfa-182">**Aggiungere hello `profile` e `email` ambiti tooyour app se l'applicazione necessita di informazioni utente di base.**</span><span class="sxs-lookup"><span data-stu-id="becfa-182">**Add hello `profile` and `email` scopes tooyour app if your app needs basic user information.**</span></span>
5. <span data-ttu-id="becfa-183">**Accettare i valori dell'autorità di certificazione nei token con e senza una barra finale.**</span><span class="sxs-lookup"><span data-stu-id="becfa-183">**Accept issuer values in tokens both with and without a trailing slash.**</span></span>

<span data-ttu-id="becfa-184">Il nostro [documentazione relativa al protocollo v 2.0](active-directory-v2-protocols.md) è già stato aggiornato tooreflect queste modifiche, è possibile utilizzarlo come riferimento per consentire di aggiornare il codice.</span><span class="sxs-lookup"><span data-stu-id="becfa-184">Our [v2.0 protocol documentation](active-directory-v2-protocols.md) has already been updated tooreflect these changes, so you may use it as reference in helping update your code.</span></span>

<span data-ttu-id="becfa-185">Se si dispone di ulteriori domande sull'ambito hello delle modifiche di hello, è possibile tooreach libero out toous su Twitter in @AzureAD.</span><span class="sxs-lookup"><span data-stu-id="becfa-185">If you have any further questions on hello scope of hello changes, please feel free tooreach out toous on Twitter at @AzureAD.</span></span>

## <a name="how-often-will-protocol-changes-occur"></a><span data-ttu-id="becfa-186">Frequenza delle modifiche ai protocolli</span><span class="sxs-lookup"><span data-stu-id="becfa-186">How often will protocol changes occur?</span></span>
<span data-ttu-id="becfa-187">È non prevede altre importanti modifiche toohello i protocolli di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="becfa-187">We do not foresee any further breaking changes toohello authentication protocols.</span></span>  <span data-ttu-id="becfa-188">È intenzionalmente stiamo unendo le modifiche in una versione in modo che non sarà possibile toogo tramite questo tipo di processo di aggiornamento nuovamente nel prossimo futuro.</span><span class="sxs-lookup"><span data-stu-id="becfa-188">We are intentionally bundling these changes into one release so that you won\`t have toogo through this type of update process again any time soon.</span></span>  <span data-ttu-id="becfa-189">Naturalmente, continueremo tooadd funzionalità toohello convergente v 2.0 i servizio di autenticazione che è possibile trarre vantaggio da, ma tali modifiche devono essere additivo e non si interromperà il codice esistente.</span><span class="sxs-lookup"><span data-stu-id="becfa-189">Of course, we will continue tooadd features toohello converged v2.0 authentication service that you can take advantage of, but those changes should be additive and not break existing code.</span></span>

<span data-ttu-id="becfa-190">Infine, desideriamo toosay grazie per provare operazioni durante il periodo di anteprima di hello.</span><span class="sxs-lookup"><span data-stu-id="becfa-190">Lastly, we would like toosay thank you for trying things out during hello preview period.</span></span>  <span data-ttu-id="becfa-191">esperienze dei nostri adottato e approfondimenti Hello sono state preziose finora e ci auguriamo che si continuerà a tooshare le opinioni e idee.</span><span class="sxs-lookup"><span data-stu-id="becfa-191">hello insights and experiences of our early adopters have been invaluable thus far, and we hope you\`ll continue tooshare your opinions and ideas.</span></span>

<span data-ttu-id="becfa-192">Buon lavoro.</span><span class="sxs-lookup"><span data-stu-id="becfa-192">Happy coding!</span></span>

<span data-ttu-id="becfa-193">Divisione di identità Microsoft Hello</span><span class="sxs-lookup"><span data-stu-id="becfa-193">hello Microsoft Identity Division</span></span>

