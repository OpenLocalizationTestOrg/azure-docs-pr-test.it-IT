---
title: aaaAzure AD v2 ASP.NET Web Server Getting Started - Test | Documenti Microsoft
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
ms.openlocfilehash: 99c7525b9146605142180962fc2a61b3c953c064
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
## <a name="test-your-code"></a><span data-ttu-id="e903d-103">Testare il codice</span><span class="sxs-lookup"><span data-stu-id="e903d-103">Test your code</span></span>

<span data-ttu-id="e903d-104">Premere `F5` toorun il progetto in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e903d-104">Press `F5` toorun your project in Visual Studio.</span></span> <span data-ttu-id="e903d-105">Hello browser verrà aperto e indirizzare è troppo*http://localhost: {porta}* dove verrà visualizzato hello *accedere con Microsoft* pulsante.</span><span class="sxs-lookup"><span data-stu-id="e903d-105">hello browser will open and direct you too*http://localhost:{port}* where you’ll see hello *Sign in with Microsoft* button.</span></span> <span data-ttu-id="e903d-106">Fare clic, toosign in.</span><span class="sxs-lookup"><span data-stu-id="e903d-106">Go ahead and click it toosign in.</span></span>

<span data-ttu-id="e903d-107">Quando si è pronti tootest, utilizzare una o dell'istituto di istruzione (Azure Active Directory), account aziendale o personale (live.com, outlook.com) toosign in.</span><span class="sxs-lookup"><span data-stu-id="e903d-107">When you're ready tootest, use a work or school (Azure Active Directory), or a personal (live.com, outlook.com) account toosign in.</span></span> 

![Finestra del browser con accesso con Microsoft](media/active-directory-serversidewebapp-aspnetwebappowin-test/aspnetbrowsersignin.png)

![Finestra del browser con accesso con Microsoft](media/active-directory-serversidewebapp-aspnetwebappowin-test/aspnetbrowsersignin2.png)

#### <a name="expected-results"></a><span data-ttu-id="e903d-110">Risultati previsti</span><span class="sxs-lookup"><span data-stu-id="e903d-110">Expected results</span></span>
<span data-ttu-id="e903d-111">Dopo l'accesso, utente hello è reindirizzato toohello home page del sito web che è l'URL HTTPS specificato nelle informazioni di registrazione dell'applicazione nel portale di registrazione dell'applicazione Microsoft hello hello.</span><span class="sxs-lookup"><span data-stu-id="e903d-111">After sign-in, hello user is redirected toohello home page of your web site which is hello HTTPS URL specified in your application registration information in hello Microsoft Application Registration Portal.</span></span> <span data-ttu-id="e903d-112">In questa pagina vengono ora *Hello {User}* e un collegamento toosign-out e le attestazioni dell'utente di hello toosee collegamento – che è un controller di Authorize toohello collegamento creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="e903d-112">This page now shows *Hello {User}* and a link toosign-out, and a link toosee hello user’s claims – which is a link toohello Authorize controller created earlier.</span></span>

### <a name="see-users-claims"></a><span data-ttu-id="e903d-113">Visualizzare le attestazioni dell'utente</span><span class="sxs-lookup"><span data-stu-id="e903d-113">See user's claims</span></span>
<span data-ttu-id="e903d-114">Selezionare le attestazioni dell'utente di hello collegamento ipertestuale toosee hello.</span><span class="sxs-lookup"><span data-stu-id="e903d-114">Select hello hyperlink toosee hello user's claims.</span></span> <span data-ttu-id="e903d-115">Ciò porta controller toohello e visualizzazione solo toousers disponibili che vengono autenticate.</span><span class="sxs-lookup"><span data-stu-id="e903d-115">This leads you toohello controller and view that is only available toousers that are authenticated.</span></span>

#### <a name="expected-results"></a><span data-ttu-id="e903d-116">Risultati previsti</span><span class="sxs-lookup"><span data-stu-id="e903d-116">Expected results</span></span>
 <span data-ttu-id="e903d-117">Verrà visualizzata una tabella contenente le proprietà di base hello dell'utente connesso hello:</span><span class="sxs-lookup"><span data-stu-id="e903d-117">You should see a table containing hello basic properties of hello logged user:</span></span>

| <span data-ttu-id="e903d-118">Proprietà</span><span class="sxs-lookup"><span data-stu-id="e903d-118">Property</span></span> | <span data-ttu-id="e903d-119">Valore</span><span class="sxs-lookup"><span data-stu-id="e903d-119">Value</span></span> | <span data-ttu-id="e903d-120">Descrizione</span><span class="sxs-lookup"><span data-stu-id="e903d-120">Description</span></span>|
|---|---|---|
| <span data-ttu-id="e903d-121">Nome</span><span class="sxs-lookup"><span data-stu-id="e903d-121">Name</span></span> | <span data-ttu-id="e903d-122">{Nome e cognome utente}</span><span class="sxs-lookup"><span data-stu-id="e903d-122">{User Full Name}</span></span> | <span data-ttu-id="e903d-123">utente Hello e del cognome</span><span class="sxs-lookup"><span data-stu-id="e903d-123">hello user’s first and last name</span></span>
|<span data-ttu-id="e903d-124">Username</span><span class="sxs-lookup"><span data-stu-id="e903d-124">Username</span></span> | <span>user@domain.com</span>| <span data-ttu-id="e903d-125">nome utente Hello utilizzato tooidentify hello registrato</span><span class="sxs-lookup"><span data-stu-id="e903d-125">hello username used tooidentify hello logged user</span></span>
| <span data-ttu-id="e903d-126">Oggetto</span><span class="sxs-lookup"><span data-stu-id="e903d-126">Subject</span></span>| <span data-ttu-id="e903d-127">{Soggetto}</span><span class="sxs-lookup"><span data-stu-id="e903d-127">{Subject}</span></span>|<span data-ttu-id="e903d-128">Una stringa di toouniquely identificare accesso utente hello Web hello</span><span class="sxs-lookup"><span data-stu-id="e903d-128">A string toouniquely identify hello user logon across hello web</span></span>|
| <span data-ttu-id="e903d-129">ID tenant</span><span class="sxs-lookup"><span data-stu-id="e903d-129">Tenant ID</span></span>| <span data-ttu-id="e903d-130">{GUID}</span><span class="sxs-lookup"><span data-stu-id="e903d-130">{Guid}</span></span>| <span data-ttu-id="e903d-131">Oggetto *guid* toouniquely rappresentano l'organizzazione di Azure Active Directory dell'utente di hello.</span><span class="sxs-lookup"><span data-stu-id="e903d-131">A *guid* toouniquely represent hello user’s Azure Active Directory organization.</span></span>|

<span data-ttu-id="e903d-132">Verrà visualizzata anche una tabella contenente tutte le attestazioni utente incluse nella richiesta di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="e903d-132">In addition, you will see a table including all user claims included in authentication request.</span></span> <span data-ttu-id="e903d-133">Per un elenco e una spiegazione di tutte le attestazioni in un token ID, vedere questo [articolo](https://docs.microsoft.com/azure/active-directory/develop/active-directory-token-and-claims "Elenco delle attestazioni nei token ID").</span><span class="sxs-lookup"><span data-stu-id="e903d-133">For a list of all claims in an Id Token and explanation please see this [article](https://docs.microsoft.com/azure/active-directory/develop/active-directory-token-and-claims "List of Claims in Id Token").</span></span>


### <a name="test-accessing-a-method-that-has-an-authorize-attribute-optional"></a><span data-ttu-id="e903d-134">Testare l'accesso a un metodo con attributo *[Authorize]* (facoltativo)</span><span class="sxs-lookup"><span data-stu-id="e903d-134">Test accessing a method that has an *[Authorize]* attribute (Optional)</span></span>
<span data-ttu-id="e903d-135">In questo passaggio, si verrà controller di test durante l'accesso ai hello autenticato come utente anonimo:</span><span class="sxs-lookup"><span data-stu-id="e903d-135">In this step, you will test accessing hello Authenticated controller as an anonymous user:</span></span><br/>
<span data-ttu-id="e903d-136">Selezionare utente hello toosign-out di collegamento hello e processo di disconnessione hello completo.</span><span class="sxs-lookup"><span data-stu-id="e903d-136">Select hello link toosign-out hello user and complete hello sign-out process.</span></span><br/>
<span data-ttu-id="e903d-137">A questo punto, nel browser, digitare http://localhost: {porta} / autenticato tooaccess il controller che è protetta con hello `[Authorize]` attributo</span><span class="sxs-lookup"><span data-stu-id="e903d-137">Now in your browser, type http://localhost:{port}/authenticated tooaccess your controller that is protected with hello `[Authorize]` attribute</span></span>

#### <a name="expected-results"></a><span data-ttu-id="e903d-138">Risultati previsti</span><span class="sxs-lookup"><span data-stu-id="e903d-138">Expected results</span></span>
<span data-ttu-id="e903d-139">Si dovrebbe ricevere la visualizzazione di hello toosee tooauthenticate di richiesta di hello.</span><span class="sxs-lookup"><span data-stu-id="e903d-139">You should receive hello prompt requiring you tooauthenticate toosee hello view.</span></span>

## <a name="additional-information"></a><span data-ttu-id="e903d-140">Informazioni aggiuntive</span><span class="sxs-lookup"><span data-stu-id="e903d-140">Additional information</span></span>

<!--start-collapse-->
### <a name="protect-your-entire-web-site"></a><span data-ttu-id="e903d-141">Proteggere l'intero sito Web</span><span class="sxs-lookup"><span data-stu-id="e903d-141">Protect your entire web site</span></span>
<span data-ttu-id="e903d-142">tooprotect l'intero sito web, aggiungere hello `AuthorizeAttribute` troppo`GlobalFilters` in `Global.asax` `Application_Start` metodo:</span><span class="sxs-lookup"><span data-stu-id="e903d-142">tooprotect your entire web site, add hello `AuthorizeAttribute` too`GlobalFilters` in `Global.asax` `Application_Start` method:</span></span>

```csharp
GlobalFilters.Filters.Add(new AuthorizeAttribute());
```
<!--end-collapse-->

<div></div>
<br/>

> [!NOTE]
> <span data-ttu-id="e903d-143">**Come gli utenti toorestrict da sola organizzazione toosign nell'applicazione tooyour**</span><span class="sxs-lookup"><span data-stu-id="e903d-143">**How toorestrict users from only one organization toosign in tooyour application**</span></span>

> <span data-ttu-id="e903d-144">Per impostazione predefinita, gli account personali (tra cui outlook.com, live.com e altri), nonché account aziendale e dell'istituto di istruzione da qualsiasi società o organizzazione che è integrato con Azure Active Directory può Accedi tooyour applicazione.</span><span class="sxs-lookup"><span data-stu-id="e903d-144">By default, personal accounts (including outlook.com, live.com, and others) as well as work and school accounts from any company or organization that has integrated with Azure Active Directory can sign-in tooyour application.</span></span> 

> <span data-ttu-id="e903d-145">Se si desidera che l'applicazione tooaccept accessi da sola organizzazione di Azure Active Directory, sostituire hello `Tenant` parametro *Web. config* da `Common` toohello nome del tenant dell'organizzazione hello-esempio *contoso.onmicrosoft.com*. Successivamente, modificare hello `ValidateIssuer` argomento in del *classe di avvio di OWIN* troppo`true`.</span><span class="sxs-lookup"><span data-stu-id="e903d-145">If you want your application tooaccept sign-ins from only one Azure Active Directory organization, replace hello `Tenant` parameter in *web.config* from `Common` toohello tenant name of hello organization – example, *contoso.onmicrosoft.com*. After that, change hello `ValidateIssuer` argument in your *OWIN Startup class* too`true`.</span></span>

> <span data-ttu-id="e903d-146">gli utenti tooallow da solo un elenco di aziende specifiche, impostare `ValidateIssuer` tootrue e utilizzare hello `ValidIssuers` toospecify parametro un elenco delle organizzazioni.</span><span class="sxs-lookup"><span data-stu-id="e903d-146">tooallow users from only a list of specific organizations, set `ValidateIssuer` tootrue and use hello `ValidIssuers` parameter toospecify a list of organizations.</span></span>

> <span data-ttu-id="e903d-147">Un'altra opzione è un metodo personalizzato tooimplement autorità emittenti di hello toovalidate utilizzando il parametro IssuerValidator.</span><span class="sxs-lookup"><span data-stu-id="e903d-147">Another option is tooimplement a custom method toovalidate hello issuers using IssuerValidator parameter.</span></span> <span data-ttu-id="e903d-148">Per altre informazioni su `TokenValidationParameters`, vedere [questo](https://msdn.microsoft.com/library/system.identitymodel.tokens.tokenvalidationparameters.aspx "Articolo di MSDN su TokenValidationParameters") articolo di MSDN.</span><span class="sxs-lookup"><span data-stu-id="e903d-148">For more information about `TokenValidationParameters`, please see [this](https://msdn.microsoft.com/library/system.identitymodel.tokens.tokenvalidationparameters.aspx "TokenValidationParameters MSDN article") MSDN article.</span></span>

