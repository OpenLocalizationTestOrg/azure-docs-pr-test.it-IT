---
title: 'Introduzione al server Web ASP.NET per Azure AD v2: test | Microsoft Docs'
description: Implementazione di accessi Microsoft in una soluzione ASP.NET con un'applicazione tradizionale basata su Web browser tramite lo standard OpenID Connect
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: 00cb963e85111274c36c3a84489894811ad2dabd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
## <a name="test-your-code"></a><span data-ttu-id="7b2c1-103">Testare il codice</span><span class="sxs-lookup"><span data-stu-id="7b2c1-103">Test your code</span></span>

<span data-ttu-id="7b2c1-104">Premere `F5` per eseguire il progetto in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7b2c1-104">Press `F5` to run your project in Visual Studio.</span></span> <span data-ttu-id="7b2c1-105">Verrà aperto il browser e l'utente verrà indirizzato a *http://localhost:{porta}*, in cui verrà visualizzato il pulsante *Accedi con Microsoft*.</span><span class="sxs-lookup"><span data-stu-id="7b2c1-105">The browser will open and direct you to *http://localhost:{port}* where you’ll see the *Sign in with Microsoft* button.</span></span> <span data-ttu-id="7b2c1-106">Fare clic per eseguire l'accesso.</span><span class="sxs-lookup"><span data-stu-id="7b2c1-106">Go ahead and click it to sign in.</span></span>

<span data-ttu-id="7b2c1-107">Quando si è pronti per il test, usare un account aziendale o dell'istituto di istruzione (Azure Active Directory) oppure un account personale (live.com, outlook.com) per accedere.</span><span class="sxs-lookup"><span data-stu-id="7b2c1-107">When you're ready to test, use a work or school (Azure Active Directory), or a personal (live.com, outlook.com) account to sign in.</span></span> 

![Finestra del browser con accesso con Microsoft](media/active-directory-serversidewebapp-aspnetwebappowin-test/aspnetbrowsersignin.png)

![Finestra del browser con accesso con Microsoft](media/active-directory-serversidewebapp-aspnetwebappowin-test/aspnetbrowsersignin2.png)

#### <a name="expected-results"></a><span data-ttu-id="7b2c1-110">Risultati previsti</span><span class="sxs-lookup"><span data-stu-id="7b2c1-110">Expected results</span></span>
<span data-ttu-id="7b2c1-111">Dopo l'accesso, l'utente viene reindirizzato alla home page del sito Web, ossia all'URL HTTPS specificato nelle informazioni di registrazione dell'applicazione nel portale di registrazione delle applicazioni Microsoft.</span><span class="sxs-lookup"><span data-stu-id="7b2c1-111">After sign-in, the user is redirected to the home page of your web site which is the HTTPS URL specified in your application registration information in the Microsoft Application Registration Portal.</span></span> <span data-ttu-id="7b2c1-112">Nella pagina vengono ora visualizzati *Hello {utente}*, un collegamento per la disconnessione e uno per visualizzare le attestazioni dell'utente, ossia un collegamento al controller Authorize creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="7b2c1-112">This page now shows *Hello {User}* and a link to sign-out, and a link to see the user’s claims – which is a link to the Authorize controller created earlier.</span></span>

### <a name="see-users-claims"></a><span data-ttu-id="7b2c1-113">Visualizzare le attestazioni dell'utente</span><span class="sxs-lookup"><span data-stu-id="7b2c1-113">See user's claims</span></span>
<span data-ttu-id="7b2c1-114">Selezionare il collegamento ipertestuale per visualizzare le attestazioni dell'utente.</span><span class="sxs-lookup"><span data-stu-id="7b2c1-114">Select the hyperlink to see the user's claims.</span></span> <span data-ttu-id="7b2c1-115">Si accederà così al controller e alla visualizzazione disponibile solo per gli utenti autenticati.</span><span class="sxs-lookup"><span data-stu-id="7b2c1-115">This leads you to the controller and view that is only available to users that are authenticated.</span></span>

#### <a name="expected-results"></a><span data-ttu-id="7b2c1-116">Risultati previsti</span><span class="sxs-lookup"><span data-stu-id="7b2c1-116">Expected results</span></span>
 <span data-ttu-id="7b2c1-117">Verrà visualizzata una tabella contenente le proprietà di base dell'utente connesso:</span><span class="sxs-lookup"><span data-stu-id="7b2c1-117">You should see a table containing the basic properties of the logged user:</span></span>

| <span data-ttu-id="7b2c1-118">Proprietà</span><span class="sxs-lookup"><span data-stu-id="7b2c1-118">Property</span></span> | <span data-ttu-id="7b2c1-119">Valore</span><span class="sxs-lookup"><span data-stu-id="7b2c1-119">Value</span></span> | <span data-ttu-id="7b2c1-120">Descrizione</span><span class="sxs-lookup"><span data-stu-id="7b2c1-120">Description</span></span>|
|---|---|---|
| <span data-ttu-id="7b2c1-121">Nome</span><span class="sxs-lookup"><span data-stu-id="7b2c1-121">Name</span></span> | <span data-ttu-id="7b2c1-122">{Nome e cognome utente}</span><span class="sxs-lookup"><span data-stu-id="7b2c1-122">{User Full Name}</span></span> | <span data-ttu-id="7b2c1-123">Nome e cognome dell'utente</span><span class="sxs-lookup"><span data-stu-id="7b2c1-123">The user’s first and last name</span></span>
|<span data-ttu-id="7b2c1-124">Nome utente</span><span class="sxs-lookup"><span data-stu-id="7b2c1-124">Username</span></span> | <span>user@domain.com</span>| <span data-ttu-id="7b2c1-125">Nome utente usato per identificare l'utente connesso</span><span class="sxs-lookup"><span data-stu-id="7b2c1-125">The username used to identify the logged user</span></span>
| <span data-ttu-id="7b2c1-126">Subject</span><span class="sxs-lookup"><span data-stu-id="7b2c1-126">Subject</span></span>| <span data-ttu-id="7b2c1-127">{Soggetto}</span><span class="sxs-lookup"><span data-stu-id="7b2c1-127">{Subject}</span></span>|<span data-ttu-id="7b2c1-128">Stringa che identifica in modo univoco l'account di accesso dell'utente sul Web</span><span class="sxs-lookup"><span data-stu-id="7b2c1-128">A string to uniquely identify the user logon across the web</span></span>|
| <span data-ttu-id="7b2c1-129">ID tenant</span><span class="sxs-lookup"><span data-stu-id="7b2c1-129">Tenant ID</span></span>| <span data-ttu-id="7b2c1-130">{GUID}</span><span class="sxs-lookup"><span data-stu-id="7b2c1-130">{Guid}</span></span>| <span data-ttu-id="7b2c1-131">*GUID* che rappresenta in modo univoco l'organizzazione di Azure Active Directory dell'utente.</span><span class="sxs-lookup"><span data-stu-id="7b2c1-131">A *guid* to uniquely represent the user’s Azure Active Directory organization.</span></span>|

<span data-ttu-id="7b2c1-132">Verrà visualizzata anche una tabella contenente tutte le attestazioni utente incluse nella richiesta di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="7b2c1-132">In addition, you will see a table including all user claims included in authentication request.</span></span> <span data-ttu-id="7b2c1-133">Per un elenco e una spiegazione di tutte le attestazioni in un token ID, vedere questo [articolo](https://docs.microsoft.com/azure/active-directory/develop/active-directory-token-and-claims "Elenco delle attestazioni nei token ID").</span><span class="sxs-lookup"><span data-stu-id="7b2c1-133">For a list of all claims in an Id Token and explanation please see this [article](https://docs.microsoft.com/azure/active-directory/develop/active-directory-token-and-claims "List of Claims in Id Token").</span></span>


### <a name="test-accessing-a-method-that-has-an-authorize-attribute-optional"></a><span data-ttu-id="7b2c1-134">Testare l'accesso a un metodo con attributo *[Authorize]* (facoltativo)</span><span class="sxs-lookup"><span data-stu-id="7b2c1-134">Test accessing a method that has an *[Authorize]* attribute (Optional)</span></span>
<span data-ttu-id="7b2c1-135">In questo passaggio si testerà l'accesso al controller Authenticated come utente anonimo:</span><span class="sxs-lookup"><span data-stu-id="7b2c1-135">In this step, you will test accessing the Authenticated controller as an anonymous user:</span></span><br/>
<span data-ttu-id="7b2c1-136">Selezionare il collegamento per la disconnessione dell'utente e completare il processo di disconnessione.</span><span class="sxs-lookup"><span data-stu-id="7b2c1-136">Select the link to sign-out the user and complete the sign-out process.</span></span><br/>
<span data-ttu-id="7b2c1-137">Nel browser digitare http://localhost:{porta}/authenticated per accedere al controller protetto con l'attributo `[Authorize]`.</span><span class="sxs-lookup"><span data-stu-id="7b2c1-137">Now in your browser, type http://localhost:{port}/authenticated to access your controller that is protected with the `[Authorize]` attribute</span></span>

#### <a name="expected-results"></a><span data-ttu-id="7b2c1-138">Risultati previsti</span><span class="sxs-lookup"><span data-stu-id="7b2c1-138">Expected results</span></span>
<span data-ttu-id="7b2c1-139">Verrà visualizzata la richiesta di eseguire l'autenticazione per accedere alla visualizzazione.</span><span class="sxs-lookup"><span data-stu-id="7b2c1-139">You should receive the prompt requiring you to authenticate to see the view.</span></span>

## <a name="additional-information"></a><span data-ttu-id="7b2c1-140">Informazioni aggiuntive</span><span class="sxs-lookup"><span data-stu-id="7b2c1-140">Additional information</span></span>

<!--start-collapse-->
### <a name="protect-your-entire-web-site"></a><span data-ttu-id="7b2c1-141">Proteggere l'intero sito Web</span><span class="sxs-lookup"><span data-stu-id="7b2c1-141">Protect your entire web site</span></span>
<span data-ttu-id="7b2c1-142">Per proteggere l'intero sito Web, aggiungere `AuthorizeAttribute` a `GlobalFilters` nel metodo `Application_Start` di `Global.asax`:</span><span class="sxs-lookup"><span data-stu-id="7b2c1-142">To protect your entire web site, add the `AuthorizeAttribute` to `GlobalFilters` in `Global.asax` `Application_Start` method:</span></span>

```csharp
GlobalFilters.Filters.Add(new AuthorizeAttribute());
```
<!--end-collapse-->

<div></div>
<br/>

> [!NOTE]
> <span data-ttu-id="7b2c1-143">**Come limitare l'accesso all'applicazione agli utenti di una sola organizzazione**</span><span class="sxs-lookup"><span data-stu-id="7b2c1-143">**How to restrict users from only one organization to sign in to your application**</span></span>

> <span data-ttu-id="7b2c1-144">Per impostazione predefinita, all'applicazione possono accedere account personali (ad esempio outlook.com, live.com e altri) e account aziendali o di istituti di istruzione di qualsiasi organizzazione o azienda che abbia eseguito l'integrazione con Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7b2c1-144">By default, personal accounts (including outlook.com, live.com, and others) as well as work and school accounts from any company or organization that has integrated with Azure Active Directory can sign-in to your application.</span></span> 

> <span data-ttu-id="7b2c1-145">Se si vuole che l'applicazione accetti accessi da una sola organizzazione di Azure Active Directory, sostituire il parametro `Tenant` in *web.config* passando da `Common` al nome del tenant dell'organizzazione, ad esempio *contoso.onmicrosoft.com*.</span><span class="sxs-lookup"><span data-stu-id="7b2c1-145">If you want your application to accept sign-ins from only one Azure Active Directory organization, replace the `Tenant` parameter in *web.config* from `Common` to the tenant name of the organization – example, *contoso.onmicrosoft.com*.</span></span> <span data-ttu-id="7b2c1-146">Al termine, modificare l'argomento `ValidateIssuer` nella *classe di avvio OWIN* impostandolo su `true`.</span><span class="sxs-lookup"><span data-stu-id="7b2c1-146">After that, change the `ValidateIssuer` argument in your *OWIN Startup class* to `true`.</span></span>

> <span data-ttu-id="7b2c1-147">Per consentire l'accesso solo agli utenti di un elenco di organizzazioni specifiche, impostare `ValidateIssuer` su true e usare il parametro `ValidIssuers` per specificare un elenco di organizzazioni.</span><span class="sxs-lookup"><span data-stu-id="7b2c1-147">To allow users from only a list of specific organizations, set `ValidateIssuer` to true and use the `ValidIssuers` parameter to specify a list of organizations.</span></span>

> <span data-ttu-id="7b2c1-148">Un'altra opzione consiste nell'implementare un metodo personalizzato per convalidare le autorità di certificazione usando il parametro IssuerValidator.</span><span class="sxs-lookup"><span data-stu-id="7b2c1-148">Another option is to implement a custom method to validate the issuers using IssuerValidator parameter.</span></span> <span data-ttu-id="7b2c1-149">Per altre informazioni su `TokenValidationParameters`, vedere [questo](https://msdn.microsoft.com/library/system.identitymodel.tokens.tokenvalidationparameters.aspx "Articolo di MSDN su TokenValidationParameters") articolo di MSDN.</span><span class="sxs-lookup"><span data-stu-id="7b2c1-149">For more information about `TokenValidationParameters`, please see [this](https://msdn.microsoft.com/library/system.identitymodel.tokens.tokenvalidationparameters.aspx "TokenValidationParameters MSDN article") MSDN article.</span></span>

