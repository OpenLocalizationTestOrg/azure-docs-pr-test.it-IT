---
title: Modifiche all'endpoint v2.0 di Azure AD | Documentazione Microsoft
description: Descrizione delle modifiche in corso ai protocolli del Modello app 2.0 disponibili in anteprima pubblica.
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
ms.openlocfilehash: ae73833a68db14804dc40eaf07ff7d3effaa9052
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="important-updates-to-the-v20-authentication-protocols"></a><span data-ttu-id="fba9a-103">Aggiornamenti importanti ai protocolli di autenticazione della versione 2.0</span><span class="sxs-lookup"><span data-stu-id="fba9a-103">Important Updates to the v2.0 Authentication Protocols</span></span>
<span data-ttu-id="fba9a-104">Nota per gli sviluppatori:</span><span class="sxs-lookup"><span data-stu-id="fba9a-104">Attention developers!</span></span> <span data-ttu-id="fba9a-105">nelle prossime due settimane verranno rilasciati alcuni aggiornamenti ai protocolli di autenticazione della versione 2.0 che potrebbero comportare modifiche di rilievo per le app scritte durante il periodo di anteprima.</span><span class="sxs-lookup"><span data-stu-id="fba9a-105">Over the next two weeks, we will be making a few updates to our v2.0 authentication protocols that may mean breaking changes for any apps you have written during our preview period.</span></span>  

## <a name="who-does-this-affect"></a><span data-ttu-id="fba9a-106">Parti interessate</span><span class="sxs-lookup"><span data-stu-id="fba9a-106">Who does this affect?</span></span>
<span data-ttu-id="fba9a-107">Le app scritte per l'uso dell'endpoint di autenticazione convergente della versione 2.0,</span><span class="sxs-lookup"><span data-stu-id="fba9a-107">Any apps that have been written to use the v2.0 converged authentication endpoint,</span></span>

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize
```

<span data-ttu-id="fba9a-108">Altre informazioni sull'endpoint della versione 2.0 sono disponibili [qui](active-directory-appmodel-v2-overview.md).</span><span class="sxs-lookup"><span data-stu-id="fba9a-108">More information on the v2.0 endpoint can be found [here](active-directory-appmodel-v2-overview.md).</span></span>

<span data-ttu-id="fba9a-109">Se è stata compilata un'app con l'endpoint della versione 2.0 creando il codice direttamente nel protocollo della versione 2.0 e usando il middleware Web OAuth o OpenID Connect oppure usando altre librerie di terze parti per eseguire l'autenticazione, è necessario testare i progetti e apportare le eventuali modifiche necessarie.</span><span class="sxs-lookup"><span data-stu-id="fba9a-109">If you have built an app using the v2.0 endpoint by coding directly to the v2.0 protocol, using any of our OpenID Connect or OAuth web middlewares, or using other 3rd party libraries to perform authentication, you should be prepared to test your projects and make changes if necessary.</span></span>

## <a name="who-doesnt-this-affect"></a><span data-ttu-id="fba9a-110">Parti non interessate</span><span class="sxs-lookup"><span data-stu-id="fba9a-110">Who doesn\`t this affect?</span></span>
<span data-ttu-id="fba9a-111">Le app scritte in base all'endpoint di autenticazione di Azure AD di produzione,</span><span class="sxs-lookup"><span data-stu-id="fba9a-111">Any apps that have been written against the production Azure AD authentication endpoint,</span></span>

```
https://login.microsoftonline.com/common/oauth2/authorize
```

<span data-ttu-id="fba9a-112">Questo protocollo è fisso e non subirà modifiche.</span><span class="sxs-lookup"><span data-stu-id="fba9a-112">This protocol is set in stone and will not be experiencing any changes.</span></span>

<span data-ttu-id="fba9a-113">Se l'app usa **solo** la libreria ADAL per eseguire l'autenticazione, non è necessario apportare alcuna modifica.</span><span class="sxs-lookup"><span data-stu-id="fba9a-113">Furthermore, if your app **only** uses our ADAL library to perform authentication, you won\`t have to change anything.</span></span>  <span data-ttu-id="fba9a-114">ADAL protegge l'app dalle modifiche.</span><span class="sxs-lookup"><span data-stu-id="fba9a-114">ADAL has shielded your app from the changes.</span></span>  

## <a name="what-are-the-changes"></a><span data-ttu-id="fba9a-115">Dettaglio delle modifiche</span><span class="sxs-lookup"><span data-stu-id="fba9a-115">What are the changes?</span></span>
### <a name="removing-the-x5t-value-from-jwt-headers"></a><span data-ttu-id="fba9a-116">Rimozione del valore x5t dalle intestazioni JWT</span><span class="sxs-lookup"><span data-stu-id="fba9a-116">Removing the x5t value from JWT headers</span></span>
<span data-ttu-id="fba9a-117">L'endpoint della versione 2.0 fa ampio uso dei token JWT, che contengono una sezione dei parametri di intestazione con i relativi metadati sul token.</span><span class="sxs-lookup"><span data-stu-id="fba9a-117">The v2.0 endpoint uses JWT tokens extensively, which contain a header parameters section with relevant metadata about the token.</span></span>  <span data-ttu-id="fba9a-118">Decodificando l'intestazione di uno dei JWT correnti, si otterrebbe un risultato simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="fba9a-118">If you decode the header of one of our current JWTs, you would find something like:</span></span>

```
{ 
    "type": "JWT",
    "alg": "RS256",
    "x5t": "MnC_VZcATfM5pOYiJHMba9goEKY",
    "kid": "MnC_VZcATfM5pOYiJHMba9goEKY"
}
```

<span data-ttu-id="fba9a-119">Dove entrambe le proprietà "x5t" e "kid" identificano la chiave pubblica da usare per convalidare la firma del token, recuperata dall'endpoint dei metadati di OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="fba9a-119">Where both the "x5t" and "kid" properties identify the public key that should be used to validate the token\`s signature, as retrieved from the OpenID Connect metadata endpoint.</span></span>

<span data-ttu-id="fba9a-120">La modifica consiste nella rimozione della proprietà "x5t".</span><span class="sxs-lookup"><span data-stu-id="fba9a-120">The change we are making here is to remove the "x5t" property.</span></span>  <span data-ttu-id="fba9a-121">È possibile continuare a usare gli stessi meccanismi per la convalida dei token, ma per il recupero della chiave pubblica corretta è possibile basarsi unicamente sulla proprietà "kid", come specificato nel protocollo OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="fba9a-121">You may continue to use the same mechanisms to validate tokens, but should rely only on the "kid" property to retrieve the correct public key, as specified in the OpenID Connect protocol.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="fba9a-122">**Assicurarsi che l'app non dipenda dall'esistenza del valore x5t.**</span><span class="sxs-lookup"><span data-stu-id="fba9a-122">**Your job: Make sure your app does not depend on the existence of the x5t value.**</span></span>
> 
> 

### <a name="removing-profileinfo"></a><span data-ttu-id="fba9a-123">Rimozione di profile_info</span><span class="sxs-lookup"><span data-stu-id="fba9a-123">Removing profile_info</span></span>
<span data-ttu-id="fba9a-124">In precedenza, l'endpoint della versione 2.0 restituiva un oggetto JSON con codifica Base64 denominato `profile_info` nelle risposte dei token.</span><span class="sxs-lookup"><span data-stu-id="fba9a-124">Previously, the v2.0 endpoint has been returning a base64 encoded JSON object in token responses called `profile_info`.</span></span>  <span data-ttu-id="fba9a-125">Quando si richiedeva un token di accesso dall'endpoint della versione 2.0 inviando una richiesta a:</span><span class="sxs-lookup"><span data-stu-id="fba9a-125">When requesting an access token from the v2.0 endpoint by sending a request to:</span></span>

```
https://login.microsoftonline.com/common/oauth2/v2.0/token
```

<span data-ttu-id="fba9a-126">La risposta era simile all'oggetto JSON seguente:</span><span class="sxs-lookup"><span data-stu-id="fba9a-126">The response would look like the following JSON object:</span></span>

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

<span data-ttu-id="fba9a-127">Il valore `profile_info` conteneva informazioni sull'utente che aveva eseguito l'accesso all'app, ad esempio il nome visualizzato, il nome, il cognome, l'indirizzo di posta elettronica, l'identificatore e così via.</span><span class="sxs-lookup"><span data-stu-id="fba9a-127">The `profile_info` value contained information about the user who signed into the app - their display name, first name, surname, email address, identifier, and so on.</span></span>  <span data-ttu-id="fba9a-128">`profile_info` veniva usato principalmente per la memorizzazione nella cache dei token e ai fini della visualizzazione.</span><span class="sxs-lookup"><span data-stu-id="fba9a-128">Primarily, the `profile_info` was used for token caching and display purposes.</span></span>

<span data-ttu-id="fba9a-129">Il valore `profile_info` è stato rimosso e le informazioni vengono ora fornite agli sviluppatori in una posizione leggermente diversa.</span><span class="sxs-lookup"><span data-stu-id="fba9a-129">We are now removing the `profile_info` value – but don't worry, we are still providing this information to developers in a slightly different place.</span></span>  <span data-ttu-id="fba9a-130">Invece di `profile_info`, l'endpoint della versione 2.0 restituisce ora un `id_token` in ogni risposta del token:</span><span class="sxs-lookup"><span data-stu-id="fba9a-130">Instead of `profile_info`, the v2.0 endpoint will now return an `id_token` in each token response:</span></span>

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

<span data-ttu-id="fba9a-131">È possibile decodificare e analizzare l'id_token per recuperare le stesse informazioni fornite da profile_info.</span><span class="sxs-lookup"><span data-stu-id="fba9a-131">You may decode and parse the id_token to retrieve the same information that you received from profile_info.</span></span>  <span data-ttu-id="fba9a-132">L'id_token è un token Web JSON (JWT) il cui contenuto è specificato da OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="fba9a-132">The id_token is a JSON Web Token (JWT), with contents as specified by OpenID Connect.</span></span>  <span data-ttu-id="fba9a-133">Il codice per eseguire questa operazione dovrebbe essere molto simile. È sufficiente estrarre il segmento intermedio (il corpo) dell'id_token e decodificarlo con Base64 per accedere all'oggetto JSON al suo interno.</span><span class="sxs-lookup"><span data-stu-id="fba9a-133">The code for doing so should be very similar – you simply need to extract the middle segment (the body) of the id_token and base64 decode it to access the JSON object within.</span></span>

<span data-ttu-id="fba9a-134">Nelle prossime due settimane è consigliabile scrivere il codice dell'app in modo che le informazioni sull'utente vengano recuperate da `id_token` o `profile_info`, a seconda del valore presente.</span><span class="sxs-lookup"><span data-stu-id="fba9a-134">Over the next two weeks, you should code your app to retrieve the user information from either the `id_token` or `profile_info`; whichever is present.</span></span>  <span data-ttu-id="fba9a-135">In questo modo, quando verrà apportata la modifica l'app potrà gestire senza problemi la transizione da `profile_info` a `id_token`, senza interruzioni.</span><span class="sxs-lookup"><span data-stu-id="fba9a-135">That way when the change is made, your app can seamlessly handle the transition from `profile_info` to `id_token` without interruption.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fba9a-136">**Assicurarsi che l'app non dipenda dall'esistenza del `profile_info` valore.**</span><span class="sxs-lookup"><span data-stu-id="fba9a-136">**Your job: Make sure your app does not depend on the existence of the `profile_info` value.**</span></span>
> 
> 

### <a name="removing-idtokenexpiresin"></a><span data-ttu-id="fba9a-137">Rimozione di id_token_expires_in</span><span class="sxs-lookup"><span data-stu-id="fba9a-137">Removing id_token_expires_in</span></span>
<span data-ttu-id="fba9a-138">Oltre a `profile_info` verrà rimosso anche il parametro `id_token_expires_in` dalle risposte.</span><span class="sxs-lookup"><span data-stu-id="fba9a-138">Similar to `profile_info`, we are also removing the `id_token_expires_in` parameter from responses.</span></span>  <span data-ttu-id="fba9a-139">In precedenza, l'endpoint della versione 2.0 restituiva un valore per `id_token_expires_in` insieme a ogni risposta dell'id_token, ad esempio in una risposta di autorizzazione:</span><span class="sxs-lookup"><span data-stu-id="fba9a-139">Previously, the v2.0 endpoint would return a value for `id_token_expires_in` along with each id_token response, for instance in an authorize response:</span></span>

```
https://myapp.com?id_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsI...&id_token_expires_in=3599...
```

<span data-ttu-id="fba9a-140">O in una risposta del token:</span><span class="sxs-lookup"><span data-stu-id="fba9a-140">Or in a token response:</span></span>

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

<span data-ttu-id="fba9a-141">Il valore `id_token_expires_in` indicava il numero di secondi di validità dell'id_token.</span><span class="sxs-lookup"><span data-stu-id="fba9a-141">The `id_token_expires_in` value would indicate the number of seconds the id_token would remain valid for.</span></span>  <span data-ttu-id="fba9a-142">Il valore `id_token_expires_in` viene ora completamente rimosso.</span><span class="sxs-lookup"><span data-stu-id="fba9a-142">Now, we are removing the `id_token_expires_in` value completely.</span></span>  <span data-ttu-id="fba9a-143">Al suo posto è possibile usare le attestazioni `nbf` e `exp` dello standard OpenID Connect per esaminare la validità di un id_token.</span><span class="sxs-lookup"><span data-stu-id="fba9a-143">Instead, you may use the OpenID Connect standard `nbf` and `exp` claims to examine the validity of an id_token.</span></span>  <span data-ttu-id="fba9a-144">Per altre informazioni su queste attestazioni, vedere il [riferimento al token della versione 2.0](active-directory-v2-tokens.md) .</span><span class="sxs-lookup"><span data-stu-id="fba9a-144">See the [v2.0 token reference](active-directory-v2-tokens.md) for more information on these claims.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fba9a-145">**Assicurarsi che l'app non dipenda dall'esistenza del `id_token_expires_in` valore.**</span><span class="sxs-lookup"><span data-stu-id="fba9a-145">**Your job: Make sure your app does not depend on the existence of the `id_token_expires_in` value.**</span></span>
> 
> 

### <a name="changing-the-claims-returned-by-scopeopenid"></a><span data-ttu-id="fba9a-146">Modifica delle attestazioni restituite da scope=openid</span><span class="sxs-lookup"><span data-stu-id="fba9a-146">Changing the claims returned by scope=openid</span></span>
<span data-ttu-id="fba9a-147">Questa sarà la modifica più significativa, che influirà su quasi tutte le app che usano l'endpoint della versione 2.0.</span><span class="sxs-lookup"><span data-stu-id="fba9a-147">This change will be the most significant – in fact, it will affect almost every app that uses the v2.0 endpoint.</span></span>  <span data-ttu-id="fba9a-148">Molte applicazioni inviano richieste all'endpoint della versione 2.0 usando l'ambito `openid`, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="fba9a-148">Many applications send requests to the v2.0 endpoint using the `openid` scope, like:</span></span>

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize?
client_id=...
&redirect_uri=...
&response_mode=form_post
&response_type=id_token
&scope=openid offline_access https://outlook.office.com/mail.read
```

<span data-ttu-id="fba9a-149">Attualmente, quando l'utente concede l'autorizzazione per l'ambito `openid`, l'applicazione riceve molte informazioni sull'utente nell'id_token risultante.</span><span class="sxs-lookup"><span data-stu-id="fba9a-149">Today, when the user grants consent for the `openid` scope, your app receives a wealth of information about the user in the resulting id_token.</span></span>  <span data-ttu-id="fba9a-150">Le attestazioni includono, ad esempio, il nome dell'utente, il nome utente preferito, l'indirizzo di posta elettronica, l'ID oggetto e altro ancora.</span><span class="sxs-lookup"><span data-stu-id="fba9a-150">These claims can include their name, preferred username, email address, object ID, and more.</span></span>

<span data-ttu-id="fba9a-151">In questo aggiornamento vengono modificate le informazioni a cui l'app ha accesso tramite l'ambito `openid` , per una maggiore conformità alle specifiche di OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="fba9a-151">In this update, we are changing the information that the `openid` scope affords your app access to, to better comform with the OpenID Connect specification.</span></span>  <span data-ttu-id="fba9a-152">L'ambito `openid` consente all'app di far accedere l'utente e di ricevere un identificatore specifico dell'app per l'utente nell'attestazione `sub` dell'id_token.</span><span class="sxs-lookup"><span data-stu-id="fba9a-152">The `openid` scope will only allow your app to sign the user in, and receive an app-specific identifier for the user in the `sub` claim of the id_token.</span></span>  <span data-ttu-id="fba9a-153">Le attestazioni in un id_token a cui è stato concesso solo l'ambito `openid` saranno prive di informazioni personali.</span><span class="sxs-lookup"><span data-stu-id="fba9a-153">The claims in an id_token with only the `openid` scope granted will be devoid of any personally identifiable information.</span></span>  <span data-ttu-id="fba9a-154">Di seguito sono riportati alcuni esempi di attestazioni dell'id_token:</span><span class="sxs-lookup"><span data-stu-id="fba9a-154">Example id_token claims are:</span></span>

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

<span data-ttu-id="fba9a-155">Per ottenere informazioni personali sull'utente nell'app, questa dovrà richiedere autorizzazioni aggiuntive all'utente.</span><span class="sxs-lookup"><span data-stu-id="fba9a-155">If you want to obtain personally identifiable information (PII) about the user in your app, your app will need to request additional permissions from the user.</span></span>  <span data-ttu-id="fba9a-156">Viene ora introdotto il supporto per due nuovi ambiti dalla specifica di OpenID Connect, `email` e `profile`, che consentono di eseguire questa operazione.</span><span class="sxs-lookup"><span data-stu-id="fba9a-156">We are introducing support for two new scopes from the OpenID Connect spec – the `email` and `profile` scopes – which allow you to do so.</span></span>

* <span data-ttu-id="fba9a-157">L'ambito `email` è molto semplice: consente all'app di accedere all'indirizzo di posta elettronica primario dell'utente tramite l'attestazione `email` nell'id_token.</span><span class="sxs-lookup"><span data-stu-id="fba9a-157">The `email` scope is very straightforward – it allows your app access to the user's primary email address via the `email` claim in the id_token.</span></span>  <span data-ttu-id="fba9a-158">Si noti che l'attestazione `email` non sarà sempre presente nell'id_token, ma verrà inclusa solo se disponibile nel profilo dell'utente.</span><span class="sxs-lookup"><span data-stu-id="fba9a-158">Note that the `email` claim will not always be present in id_tokens – it will only be included if available in the user's profile.</span></span>
* <span data-ttu-id="fba9a-159">L'ambito `profile` concede all'app l'accesso a tutte le altre informazioni di base sull'utente, vale a dire il nome, il nome utente preferito, l'ID oggetto e così via.</span><span class="sxs-lookup"><span data-stu-id="fba9a-159">The `profile` scope affords your app access to all other basic information about the user – their name, preferred username, object ID, and so on.</span></span>

<span data-ttu-id="fba9a-160">Questo permette di creare il codice dell'app in modo che la divulgazione delle informazioni sia minima, chiedendo all'utente solo il set di informazioni necessario per il funzionamento dell'app.</span><span class="sxs-lookup"><span data-stu-id="fba9a-160">This allows you to code your app in a minimal-disclosure fashion – you can ask the user for just the set of information that your app requires to do its job.</span></span>  <span data-ttu-id="fba9a-161">Se si vuole continuare a ottenere il set di informazioni utente completo attualmente ricevuto dall'app, è necessario includere tutti e tre gli ambiti nelle richieste di autorizzazione:</span><span class="sxs-lookup"><span data-stu-id="fba9a-161">If you want to continue getting the full set of user information that your app is currently receiving, you should include all three scopes in your authorization requests:</span></span>

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize?
client_id=...
&redirect_uri=...
&response_mode=form_post
&response_type=id_token
&scope=openid profile email offline_access https://outlook.office.com/mail.read
```

<span data-ttu-id="fba9a-162">L'applicazione può iniziare immediatamente a inviare gli ambiti `email` e `profile` e, dopo averli accettati, l'endpoint della versione 2.0 inizia a richiedere agli utenti le autorizzazioni necessarie.</span><span class="sxs-lookup"><span data-stu-id="fba9a-162">Your app can begin sending the `email` and `profile` scopes immediately, and the v2.0 endpoint will accept these two scopes and begin requesting permissions from users as necessary.</span></span>  <span data-ttu-id="fba9a-163">Tuttavia, la modifica all'interpretazione dell'ambito `openid` non sarà effettiva ancora per alcune settimane.</span><span class="sxs-lookup"><span data-stu-id="fba9a-163">However, the change in the interpretation of the `openid` scope will not take effect for a few weeks.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fba9a-164">**Aggiungere gli ambiti `profile` e `email` se l'app richiede informazioni sull'utente.**</span><span class="sxs-lookup"><span data-stu-id="fba9a-164">**Your job: Add the `profile` and `email` scopes if your app requires information about the user.**</span></span>  <span data-ttu-id="fba9a-165">Si noti che ADAL includerà entrambe le autorizzazioni nelle richieste per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="fba9a-165">Note that ADAL will include both of these permissions in requests by default.</span></span> 
> 
> 

### <a name="removing-the-issuer-trailing-slash"></a><span data-ttu-id="fba9a-166">Rimozione della barra finale dell'autorità di certificazione</span><span class="sxs-lookup"><span data-stu-id="fba9a-166">Removing the issuer trailing slash.</span></span>
<span data-ttu-id="fba9a-167">In precedenza, il valore dell'autorità di certificazione visualizzato nei token dall'endpoint della versione 2.0 aveva il formato</span><span class="sxs-lookup"><span data-stu-id="fba9a-167">Previously, the issuer value that appears in tokens from the v2.0 endpoint took the form</span></span>

```
https://login.microsoftonline.com/{some-guid}/v2.0/
```

<span data-ttu-id="fba9a-168">dove guid era l'ID tenant del tenant di Azure AD che aveva emesso il token.</span><span class="sxs-lookup"><span data-stu-id="fba9a-168">Where the guid was the tenantId of the Azure AD tenant which issued the token.</span></span>  <span data-ttu-id="fba9a-169">Con queste modifiche, il valore dell'autorità di certificazione diventa</span><span class="sxs-lookup"><span data-stu-id="fba9a-169">With these changes, the issuer value becomes</span></span>

```
https://login.microsoftonline.com/{some-guid}/v2.0 
```

<span data-ttu-id="fba9a-170">sia nei token che nel documento di individuazione di OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="fba9a-170">in both tokens and in the OpenID Connect discovery document.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fba9a-171">**Assicurarsi che l'app accetti il valore dell'autorità di certificazione con e senza una barra finale durante la convalida dell'autorità di certificazione.**</span><span class="sxs-lookup"><span data-stu-id="fba9a-171">**Your job: Make sure your app accepts the issuer value both with and without a trailing slash during issuer validation.**</span></span>
> 
> 

## <a name="why-change"></a><span data-ttu-id="fba9a-172">Perché cambiare</span><span class="sxs-lookup"><span data-stu-id="fba9a-172">Why change?</span></span>
<span data-ttu-id="fba9a-173">La motivazione principale per l'introduzione di queste modifiche è la conformità alle specifiche dello standard OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="fba9a-173">The primary motivation for introducing these changes is to be compliant with the OpenID Connect standard specification.</span></span>  <span data-ttu-id="fba9a-174">Con la conformità a OpenID Connect, Microsoft punta a ridurre al minimo le differenze tra l'integrazione con i servizi di identità Microsoft e con altri servizi di identità del settore.</span><span class="sxs-lookup"><span data-stu-id="fba9a-174">By being OpenID Connect compliant, we hope to minimize differences between integrating with Microsoft identity services and with other identity services in the industry.</span></span>  <span data-ttu-id="fba9a-175">Gli sviluppatori devono avere la possibilità di usare le librerie di autenticazione open source preferite, senza doverle adattare alle differenze di Microsoft.</span><span class="sxs-lookup"><span data-stu-id="fba9a-175">We want to enable developers to use their favorite open source authentication libraries without having to alter the libraries to accommodate Microsoft differences.</span></span>

## <a name="what-can-you-do"></a><span data-ttu-id="fba9a-176">Cosa fare</span><span class="sxs-lookup"><span data-stu-id="fba9a-176">What can you do?</span></span>
<span data-ttu-id="fba9a-177">A partire da oggi, è possibile iniziare ad apportare tutte le modifiche descritte sopra.</span><span class="sxs-lookup"><span data-stu-id="fba9a-177">As of today, you can begin making all of the changes described above.</span></span>  <span data-ttu-id="fba9a-178">Nell'immediato:</span><span class="sxs-lookup"><span data-stu-id="fba9a-178">You should immediately:</span></span>

1. <span data-ttu-id="fba9a-179">**Rimuovere tutte le dipendenze dal`x5t` parametro di intestazione.**</span><span class="sxs-lookup"><span data-stu-id="fba9a-179">**Remove any dependencies on the `x5t` header parameter.**</span></span>
2. <span data-ttu-id="fba9a-180">**Gestire correttamente la transizione da `profile_info` a `id_token` nelle risposte dei token**.</span><span class="sxs-lookup"><span data-stu-id="fba9a-180">**Gracefully handle the transition from `profile_info` to `id_token` in token responses.**</span></span>
3. <span data-ttu-id="fba9a-181">**Rimuovere tutte le dipendenze dal parametro di risposta `id_token_expires_in`.**</span><span class="sxs-lookup"><span data-stu-id="fba9a-181">**Remove any dependencies on the `id_token_expires_in` response parameter.**</span></span>
4. <span data-ttu-id="fba9a-182">**Aggiungere gli ambiti `profile` e `email` all'app se sono necessarie informazioni utente di base.**</span><span class="sxs-lookup"><span data-stu-id="fba9a-182">**Add the `profile` and `email` scopes to your app if your app needs basic user information.**</span></span>
5. <span data-ttu-id="fba9a-183">**Accettare i valori dell'autorità di certificazione nei token con e senza una barra finale.**</span><span class="sxs-lookup"><span data-stu-id="fba9a-183">**Accept issuer values in tokens both with and without a trailing slash.**</span></span>

<span data-ttu-id="fba9a-184">La [documentazione relativa al protocollo della versione 2.0](active-directory-v2-protocols.md) è già stata aggiornata in base a queste modifiche e può essere usata come riferimento nell'aggiornamento del codice.</span><span class="sxs-lookup"><span data-stu-id="fba9a-184">Our [v2.0 protocol documentation](active-directory-v2-protocols.md) has already been updated to reflect these changes, so you may use it as reference in helping update your code.</span></span>

<span data-ttu-id="fba9a-185">Per qualsiasi domanda sull'ambito delle modifiche, è possibile contattare @AzureAD su Twitter.</span><span class="sxs-lookup"><span data-stu-id="fba9a-185">If you have any further questions on the scope of the changes, please feel free to reach out to us on Twitter at @AzureAD.</span></span>

## <a name="how-often-will-protocol-changes-occur"></a><span data-ttu-id="fba9a-186">Frequenza delle modifiche ai protocolli</span><span class="sxs-lookup"><span data-stu-id="fba9a-186">How often will protocol changes occur?</span></span>
<span data-ttu-id="fba9a-187">Non sono previste altre modifiche di rilievo ai protocolli di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="fba9a-187">We do not foresee any further breaking changes to the authentication protocols.</span></span>  <span data-ttu-id="fba9a-188">Microsoft sta unendo intenzionalmente queste modifiche in un unico rilascio per evitare la necessità di eseguire questo tipo di processo di aggiornamento nel prossimo futuro.</span><span class="sxs-lookup"><span data-stu-id="fba9a-188">We are intentionally bundling these changes into one release so that you won\`t have to go through this type of update process again any time soon.</span></span>  <span data-ttu-id="fba9a-189">Verranno naturalmente aggiunte altre funzionalità al servizio di autenticazione convergente della versione 2.0, ma non comporteranno modifiche di rilievo al codice esistente.</span><span class="sxs-lookup"><span data-stu-id="fba9a-189">Of course, we will continue to add features to the converged v2.0 authentication service that you can take advantage of, but those changes should be additive and not break existing code.</span></span>

<span data-ttu-id="fba9a-190">Microsoft ringrazia gli utenti per la disponibilità nel periodo di anteprima.</span><span class="sxs-lookup"><span data-stu-id="fba9a-190">Lastly, we would like to say thank you for trying things out during the preview period.</span></span>  <span data-ttu-id="fba9a-191">Le informazioni e l'esperienza dei primi utenti sono state preziose e Microsoft si augura che continueranno a condividere idee e opinioni.</span><span class="sxs-lookup"><span data-stu-id="fba9a-191">The insights and experiences of our early adopters have been invaluable thus far, and we hope you\`ll continue to share your opinions and ideas.</span></span>

<span data-ttu-id="fba9a-192">Buon lavoro.</span><span class="sxs-lookup"><span data-stu-id="fba9a-192">Happy coding!</span></span>

<span data-ttu-id="fba9a-193">Microsoft Identity Division</span><span class="sxs-lookup"><span data-stu-id="fba9a-193">The Microsoft Identity Division</span></span>

