---
title: Tipi di app per l'endpoint v2.0 di Azure Active Directory | Documentazione Microsoft
description: Tipi di app e scenari supportati dall'endpoint v2.0 di Azure Active Directory.
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
ms.openlocfilehash: 9d59e7f0e8f326c40be86e199d7712f6c565cc13
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="app-types-for-the-azure-active-directory-v20-endpoint"></a><span data-ttu-id="441ec-103">Tipi di app per l'endpoint v2.0 di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="441ec-103">App types for the Azure Active Directory v2.0 endpoint</span></span>
<span data-ttu-id="441ec-104">L'endpoint v2.0 di Azure Active Directory supporta l'autenticazione di un'ampia gamma di architetture di app moderne, basate sui protocolli standard del settore [OAuth 2.0 o OpenID Connect](active-directory-v2-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="441ec-104">The Azure Active Directory (Azure AD) v2.0 endpoint supports authentication for a variety of modern app architectures, all of them based on industry-standard protocols [OAuth 2.0 or OpenID Connect](active-directory-v2-protocols.md).</span></span> <span data-ttu-id="441ec-105">Questo articolo descrive brevemente i tipi di app che è possibile compilare usando Azure AD v2.0, indipendentemente dal linguaggio o dalla piattaforma preferita.</span><span class="sxs-lookup"><span data-stu-id="441ec-105">This article describes the types of apps that you can build by using Azure AD v2.0, regardless of your preferred language or platform.</span></span> <span data-ttu-id="441ec-106">Le informazioni contenute in questo articolo consentono di comprendere gli scenari generali prima di [iniziare a usare il codice](active-directory-appmodel-v2-overview.md#getting-started).</span><span class="sxs-lookup"><span data-stu-id="441ec-106">The information in this article is designed to help you understand high-level scenarios before you [start working with the code](active-directory-appmodel-v2-overview.md#getting-started).</span></span>

> [!NOTE]
> <span data-ttu-id="441ec-107">Non tutti gli scenari e le funzionalità di Azure Active Directory sono supportati dall'endpoint v2.0.</span><span class="sxs-lookup"><span data-stu-id="441ec-107">The v2.0 endpoint doesn't support all Azure Active Directory scenarios and features.</span></span> <span data-ttu-id="441ec-108">Per determinare se è necessario usare l'endpoint 2.0, vedere l'articolo relativo alle [limitazioni della versione 2.0](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="441ec-108">To determine whether you should use the v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

## <a name="the-basics"></a><span data-ttu-id="441ec-109">Nozioni di base</span><span class="sxs-lookup"><span data-stu-id="441ec-109">The basics</span></span>
<span data-ttu-id="441ec-110">È necessario registrare ogni app che usa l'endpoint v 2.0 nel [portale di registrazione delle applicazioni Microsoft](https://apps.dev.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="441ec-110">You must register each app that uses the v2.0 endpoint in the [Microsoft Application Registration Portal](https://apps.dev.microsoft.com).</span></span> <span data-ttu-id="441ec-111">Il processo di registrazione delle app raccoglie e assegna all'app questi valori:</span><span class="sxs-lookup"><span data-stu-id="441ec-111">The app registration process collects and assigns these values for your app:</span></span>

* <span data-ttu-id="441ec-112">Un **ID applicazione** che identifica l'app in modo univoco</span><span class="sxs-lookup"><span data-stu-id="441ec-112">An **Application ID** that uniquely identifies your app</span></span>
* <span data-ttu-id="441ec-113">Un **URI di reindirizzamento** che può essere usato per reindirizzare le risposte all'app</span><span class="sxs-lookup"><span data-stu-id="441ec-113">A **Redirect URI** that you can use to direct responses back to your app</span></span>
* <span data-ttu-id="441ec-114">Altri valori specifici dello scenario</span><span class="sxs-lookup"><span data-stu-id="441ec-114">A few other scenario-specific values</span></span>

<span data-ttu-id="441ec-115">Per i dettagli, vedere come [registrare un'app](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="441ec-115">For details, learn how to [register an app](active-directory-v2-app-registration.md).</span></span>

<span data-ttu-id="441ec-116">Dopo la registrazione, l'app comunica con Azure AD inviando richieste all'endpoint di Azure AD 2.0.</span><span class="sxs-lookup"><span data-stu-id="441ec-116">After the app is registered, the app communicates with Azure AD by sending requests to the Azure AD v2.0 endpoint.</span></span> <span data-ttu-id="441ec-117">Microsoft offre framework e librerie open source che gestiscono i dettagli di queste richieste.</span><span class="sxs-lookup"><span data-stu-id="441ec-117">We provide open-source frameworks and libraries that handle the details of these requests.</span></span> <span data-ttu-id="441ec-118">È sempre possibile implementare personalmente la logica di autenticazione creando richieste a questi endpoint:</span><span class="sxs-lookup"><span data-stu-id="441ec-118">You also have the option to implement the authentication logic yourself by creating requests to these endpoints:</span></span>

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize
https://login.microsoftonline.com/common/oauth2/v2.0/token
```
<!-- TODO: Need a page for libraries to link to -->

## <a name="web-apps"></a><span data-ttu-id="441ec-119">App Web</span><span class="sxs-lookup"><span data-stu-id="441ec-119">Web apps</span></span>
<span data-ttu-id="441ec-120">Per le app Web (.NET, PHP, Java, Ruby, Python, Node) accessibili tramite un browser, è possibile eseguire l'accesso utente tramite [OpenID Connect](active-directory-v2-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="441ec-120">For web apps (.NET, PHP, Java, Ruby, Python, Node) that the user accesses through a browser, you can use [OpenID Connect](active-directory-v2-protocols.md) for user sign-in.</span></span> <span data-ttu-id="441ec-121">In OpenID Connect, l'app Web riceve un token ID.</span><span class="sxs-lookup"><span data-stu-id="441ec-121">In OpenID Connect, the web app receives an ID token.</span></span> <span data-ttu-id="441ec-122">Un token ID è un token di sicurezza che verifica l'identità dell'utente e fornisce informazioni sull'utente sotto forma di attestazioni:</span><span class="sxs-lookup"><span data-stu-id="441ec-122">An ID token is a security token that verifies the user's identity and provides information about the user in the form of claims:</span></span>

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

<span data-ttu-id="441ec-123">Per informazioni su tutti i tipi di token e attestazioni disponibili per un'app, vedere le [informazioni di riferimento sui token 2.0](active-directory-v2-tokens.md).</span><span class="sxs-lookup"><span data-stu-id="441ec-123">You can learn about all the types of tokens and claims that are available to an app in the [v2.0 tokens reference](active-directory-v2-tokens.md).</span></span>

<span data-ttu-id="441ec-124">Nelle app del server Web, il flusso di autenticazione dell'accesso esegue i passaggi generali seguenti:</span><span class="sxs-lookup"><span data-stu-id="441ec-124">In web server apps, the sign-in authentication flow takes these high-level steps:</span></span>

![Flusso di autenticazione dell'app Web](../../media/active-directory-v2-flows/convergence_scenarios_webapp.png)

<span data-ttu-id="441ec-126">È possibile verificare l'identità dell'utente convalidando il token ID con una chiave di firma pubblica ricevuta dall'endpoint 2.0.</span><span class="sxs-lookup"><span data-stu-id="441ec-126">You can ensure the user's identity by validating the ID token with a public signing key that is received from the v2.0 endpoint.</span></span> <span data-ttu-id="441ec-127">Viene anche impostato un cookie di sessione che può essere usato per identificare l'utente nelle richieste di pagina successive.</span><span class="sxs-lookup"><span data-stu-id="441ec-127">A session cookie is set, which can be used to identify the user on subsequent page requests.</span></span>

<span data-ttu-id="441ec-128">Per osservare il funzionamento di questo scenario, provare uno degli esempi di codice di accesso per app Web nella sezione [Introduzione](active-directory-appmodel-v2-overview.md#getting-started) per la versione 2.0.</span><span class="sxs-lookup"><span data-stu-id="441ec-128">To see this scenario in action, try one of the web app sign-in code samples in our v2.0 [Getting Started](active-directory-appmodel-v2-overview.md#getting-started) section.</span></span>

<span data-ttu-id="441ec-129">Oltre al semplice accesso, un'app per server Web potrebbe dover accedere ad altri servizi Web, ad esempio a un'API REST.</span><span class="sxs-lookup"><span data-stu-id="441ec-129">In addition to simple sign-in, a web server app might need to access another web service, such as a REST API.</span></span> <span data-ttu-id="441ec-130">In questo caso, l'app per server Web agisce in un flusso di OpenID Connect e OAuth 2.0 combinato, tramite il [flusso del codice di autorizzazione OAuth 2.0](active-directory-v2-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="441ec-130">In this case, the web server app engages in a combined OpenID Connect and OAuth 2.0 flow, by using the [OAuth 2.0 authorization code flow](active-directory-v2-protocols.md).</span></span> <span data-ttu-id="441ec-131">Per altre informazioni su questo scenario, vedere l'[introduzione alle app Web e alle API Web](active-directory-v2-devquickstarts-webapp-webapi-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="441ec-131">For more information about this scenario, read about [getting started with web apps and Web APIs](active-directory-v2-devquickstarts-webapp-webapi-dotnet.md).</span></span>

## <a name="web-apis"></a><span data-ttu-id="441ec-132">API Web</span><span class="sxs-lookup"><span data-stu-id="441ec-132">Web APIs</span></span>
<span data-ttu-id="441ec-133">È possibile usare l'endpoint v2.0 per proteggere i servizi Web, ad esempio l'API Web RESTful dell'app.</span><span class="sxs-lookup"><span data-stu-id="441ec-133">You can use the v2.0 endpoint to secure web services, such as your app's RESTful Web API.</span></span> <span data-ttu-id="441ec-134">Al posto dei token ID e dei cookie di sessione, un'API Web usa un token di accesso OAuth 2.0 per proteggere i dati e autenticare le richieste in ingresso.</span><span class="sxs-lookup"><span data-stu-id="441ec-134">Instead of ID tokens and session cookies, a Web API uses an OAuth 2.0 access token to secure its data and to authenticate incoming requests.</span></span> <span data-ttu-id="441ec-135">Il chiamante di un'API Web aggiunge un token di accesso nell'intestazione dell'autorizzazione di una richiesta HTTP come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="441ec-135">The caller of a Web API appends an access token in the authorization header of an HTTP request, like this:</span></span>

```
GET /api/items HTTP/1.1
Host: www.mywebapi.com
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6...
Accept: application/json
...
```

<span data-ttu-id="441ec-136">L'API Web usa il token di accesso per verificare l'identità del chiamante dell'API ed estrarre informazioni su quest'ultimo dalle attestazioni codificate nel token di accesso.</span><span class="sxs-lookup"><span data-stu-id="441ec-136">The Web API uses the access token to verify the API caller's identity and to extract information about the caller from claims that are encoded in the access token.</span></span> <span data-ttu-id="441ec-137">Per informazioni su tutti i tipi di token e attestazioni disponibili per un'app, vedere le [informazioni di riferimento sui token 2.0](active-directory-v2-tokens.md).</span><span class="sxs-lookup"><span data-stu-id="441ec-137">To learn about all the types of tokens and claims that are available to an app, see the [v2.0 tokens reference](active-directory-v2-tokens.md).</span></span>

<span data-ttu-id="441ec-138">Un'API Web può consentire agli utenti di fornire il consenso o rifiutare esplicitamente specifici dati o funzionalità esponendo le autorizzazioni, note anche come [ambiti](active-directory-v2-scopes.md).</span><span class="sxs-lookup"><span data-stu-id="441ec-138">A Web API can give users the power to opt in or opt out of specific functionality or data by exposing permissions, also known as [scopes](active-directory-v2-scopes.md).</span></span> <span data-ttu-id="441ec-139">Per far sì che un'app chiamante acquisisca l'autorizzazione ad accedere a un ambito, l'utente deve fornire il consenso all'ambito durante un flusso.</span><span class="sxs-lookup"><span data-stu-id="441ec-139">For a calling app to acquire permission to a scope, the user must consent to the scope during a flow.</span></span> <span data-ttu-id="441ec-140">L'endpoint 2.0 chiede l'autorizzazione all'utente e quindi registra le autorizzazioni nei token di accesso ricevuti dall'API Web.</span><span class="sxs-lookup"><span data-stu-id="441ec-140">The v2.0 endpoint asks the user for permission, and then records permissions in all access tokens that the Web API receives.</span></span> <span data-ttu-id="441ec-141">L'API Web convalida i token di accesso ricevuti ad ogni chiamata ed esegue i controlli di autorizzazione appropriati.</span><span class="sxs-lookup"><span data-stu-id="441ec-141">The Web API validates the access tokens it receives on each call and performs authorization checks.</span></span>

<span data-ttu-id="441ec-142">Un'API Web può ricevere token di accesso da tutti i tipi di app, tra cui app per server Web, desktop, per dispositivi mobili, a singola pagina, daemon sul lato server e anche altre API Web.</span><span class="sxs-lookup"><span data-stu-id="441ec-142">A Web API can receive access tokens from all types of apps, including web server apps, desktop and mobile apps, single-page apps, server-side daemons, and even other Web APIs.</span></span> <span data-ttu-id="441ec-143">Il flusso generale per un'API Web è simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="441ec-143">The high-level flow for a Web API looks like this:</span></span>

![Flusso di autenticazione dell'API Web](../../media/active-directory-v2-flows/convergence_scenarios_webapi.png)

<span data-ttu-id="441ec-145">Per informazioni su come proteggere un'API Web con i token di accesso OAuth2, vedere gli esempi di codice dell'API Web nella sezione [introduttiva](active-directory-appmodel-v2-overview.md#getting-started).</span><span class="sxs-lookup"><span data-stu-id="441ec-145">To learn how to secure a Web API by using OAuth2 access tokens, check out the Web API code samples in our [Getting Started](active-directory-appmodel-v2-overview.md#getting-started) section.</span></span>

<span data-ttu-id="441ec-146">In molti casi, le API Web devono anche effettuare richieste in uscita ad altre API Web downstream protette da Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="441ec-146">In many cases, web APIs also need to make outbound requests to other downstream web APIs secured by Azure Active Directory.</span></span>  <span data-ttu-id="441ec-147">A questo scopo, le API Web possono ricorrere al flusso **Per conto di** di Azure AD, che consente all'API Web di scambiare un token di accesso in ingresso con un altro token di accesso da usare in richieste in uscita.</span><span class="sxs-lookup"><span data-stu-id="441ec-147">To do so, web APIs can take advantage of Azure AD's **On Behalf Of** flow, which allows the web API to exchange an incoming access token for another access token to be used in outbound requests.</span></span>  <span data-ttu-id="441ec-148">Il flusso Per conto di dell'endpoint 2.0 è descritto nel [dettaglio qui](active-directory-v2-protocols-oauth-on-behalf-of.md).</span><span class="sxs-lookup"><span data-stu-id="441ec-148">The v2.0 endpoint's On Behalf Of flow is described in [detail here](active-directory-v2-protocols-oauth-on-behalf-of.md).</span></span>

## <a name="mobile-and-native-apps"></a><span data-ttu-id="441ec-149">App per dispositivi mobili e native</span><span class="sxs-lookup"><span data-stu-id="441ec-149">Mobile and native apps</span></span>
<span data-ttu-id="441ec-150">Le app installate in un dispositivo, ad esempio app desktop e per dispositivi mobili, devono spesso accedere a servizi back-end o ad API Web che archiviano i dati ed eseguono funzioni per conto dell'utente.</span><span class="sxs-lookup"><span data-stu-id="441ec-150">Device-installed apps, such as mobile and desktop apps, often need to access back-end services or Web APIs that store data and perform functions on behalf of a user.</span></span> <span data-ttu-id="441ec-151">Queste app possono aggiungere accesso e autorizzazioni ai servizi back-end tramite il [flusso del codice di autorizzazione OAuth 2.0](active-directory-v2-protocols-oauth-code.md).</span><span class="sxs-lookup"><span data-stu-id="441ec-151">These apps can add sign-in and authorization to back-end services by using the [OAuth 2.0 authorization code flow](active-directory-v2-protocols-oauth-code.md).</span></span>

<span data-ttu-id="441ec-152">In questo flusso, l'app riceve un codice di autorizzazione dall'endpoint 2.0 quando l'utente effettua l'accesso.</span><span class="sxs-lookup"><span data-stu-id="441ec-152">In this flow, the app receives an authorization code from the v2.0 endpoint when the user signs in.</span></span> <span data-ttu-id="441ec-153">Questo codice rappresenta l'autorizzazione dell'app a chiamare servizi back-end per conto dell'utente che ha eseguito l'accesso.</span><span class="sxs-lookup"><span data-stu-id="441ec-153">The authorization code represents the app's permission to call back-end services on behalf of the user who is signed in.</span></span> <span data-ttu-id="441ec-154">L'app può scambiare il codice di autorizzazione in background con un token di accesso OAuth 2.0 e un token di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="441ec-154">The app can exchange the authorization code in the background for an OAuth 2.0 access token and a refresh token.</span></span> <span data-ttu-id="441ec-155">L'app può usare il token di accesso per l'autenticazione all'API Web nelle richieste HTTP e il token di aggiornamento per ottenere nuovi token di accesso quando i precedenti scadono.</span><span class="sxs-lookup"><span data-stu-id="441ec-155">The app can use the access token to authenticate to Web APIs in HTTP requests, and use the refresh token to get new access tokens when older access tokens expire.</span></span>

![Flusso di autenticazione dell'app nativa](../../media/active-directory-v2-flows/convergence_scenarios_native.png)

## <a name="single-page-apps-javascript"></a><span data-ttu-id="441ec-157">App a singola pagina (JavaScript)</span><span class="sxs-lookup"><span data-stu-id="441ec-157">Single-page apps (JavaScript)</span></span>
<span data-ttu-id="441ec-158">Molte app moderne hanno un front-end dell'app a singola pagina scritto principalmente in JavaScript.</span><span class="sxs-lookup"><span data-stu-id="441ec-158">Many modern apps have a single-page app front end that primarily is written in JavaScript.</span></span> <span data-ttu-id="441ec-159">Il front-end viene scritto spesso usando un framework come AngularJS, Ember.js o Durandal.</span><span class="sxs-lookup"><span data-stu-id="441ec-159">Often, it's written by using a framework like AngularJS, Ember.js, or Durandal.js.</span></span> <span data-ttu-id="441ec-160">L'endpoint di Azure AD 2.0 supporta queste app tramite il [flusso implicito OAuth 2.0](active-directory-v2-protocols-implicit.md).</span><span class="sxs-lookup"><span data-stu-id="441ec-160">The Azure AD v2.0 endpoint supports these apps by using the [OAuth 2.0 implicit flow](active-directory-v2-protocols-implicit.md).</span></span>

<span data-ttu-id="441ec-161">In questo flusso, l'app riceve i token direttamente dall'endpoint di autorizzazione 2.0, senza eseguire scambi tra server.</span><span class="sxs-lookup"><span data-stu-id="441ec-161">In this flow, the app receives tokens directly from the v2.0 authorize endpoint, without any server-to-server exchanges.</span></span> <span data-ttu-id="441ec-162">In questo modo, tutta la logica di autenticazione e gestione della sessione avviene interamente nel client JavaScript, senza eseguire reindirizzamenti a pagine aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="441ec-162">All authentication logic and session handling takes place entirely in the JavaScript client, without extra page redirects.</span></span>

![Flusso di autenticazione implicita](../../media/active-directory-v2-flows/convergence_scenarios_implicit.png)

<span data-ttu-id="441ec-164">Per visualizzare questo scenario, provare uno degli esempi di codice di applicazione a singola pagina nella sezione [introduttiva](active-directory-appmodel-v2-overview.md#getting-started).</span><span class="sxs-lookup"><span data-stu-id="441ec-164">To see this scenario in action, try one of the single-page app code samples in our [Getting Started](active-directory-appmodel-v2-overview.md#getting-started) section.</span></span>

## <a name="daemons-and-server-side-apps"></a><span data-ttu-id="441ec-165">App daemon e lato server</span><span class="sxs-lookup"><span data-stu-id="441ec-165">Daemons and server-side apps</span></span>
<span data-ttu-id="441ec-166">Anche le app che contengono processi a esecuzione prolungata o che non prevedono l'interazione con l'utente necessitano di un modo per accedere alle risorse protette, ad esempio le API Web.</span><span class="sxs-lookup"><span data-stu-id="441ec-166">Apps that have long-running processes or that operate without interaction with a user also need a way to access secured resources, such as Web APIs.</span></span> <span data-ttu-id="441ec-167">Queste app possono autenticarsi e ottenere i token usando l'identità dell'app, anziché un'identità delegata dell'utente, con il flusso delle credenziali client di OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="441ec-167">These apps can authenticate and get tokens by using the app's identity, rather than a user's delegated identity, with the OAuth 2.0 client credentials flow.</span></span>

<span data-ttu-id="441ec-168">In questo flusso, l'app interagisce direttamente con l'endpoint `/token` per ottenere gli endpoint:</span><span class="sxs-lookup"><span data-stu-id="441ec-168">In this flow, the app interacts directly with the `/token` endpoint to obtain endpoints:</span></span>

![Flusso di autenticazione dell'app daemon](../../media/active-directory-v2-flows/convergence_scenarios_daemon.png)

<span data-ttu-id="441ec-170">Per compilare un'app daemon, vedere la documentazione sulle credenziali client nella sezione [Introduzione](active-directory-appmodel-v2-overview.md#getting-started) oppure provare un'[app di esempio .NET](https://github.com/Azure-Samples/active-directory-dotnet-daemon-v2).</span><span class="sxs-lookup"><span data-stu-id="441ec-170">To build a daemon app, see the client credentials documentation in our [Getting Started](active-directory-appmodel-v2-overview.md#getting-started) section, or try a [.NET sample app](https://github.com/Azure-Samples/active-directory-dotnet-daemon-v2).</span></span>
