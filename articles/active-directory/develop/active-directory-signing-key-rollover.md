---
title: Rollover della chiave di Azure AD aaaSigning | Documenti Microsoft
description: Questo articolo illustra hello consigliate rollover della chiave di firma per Azure Active Directory
services: active-directory
documentationcenter: .net
author: dstrockis
manager: krassk
editor: 
ms.assetid: ed964056-0723-42fe-bb69-e57323b9407f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2016
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: ac6ade7f3ba2fbd22ea6d447aa5d07a2d6bdd451
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="signing-key-rollover-in-azure-active-directory"></a><span data-ttu-id="9c300-103">Rollover della chiave di firma in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9c300-103">Signing key rollover in Azure Active Directory</span></span>
<span data-ttu-id="9c300-104">In questo argomento viene illustrato cosa occorre tooknow sulle chiavi pubbliche hello utilizzati nei token di sicurezza di Azure Active Directory (Azure AD) toosign.</span><span class="sxs-lookup"><span data-stu-id="9c300-104">This topic discusses what you need tooknow about hello public keys that are used in Azure Active Directory (Azure AD) toosign security tokens.</span></span> <span data-ttu-id="9c300-105">È importante toonote che questi rollover delle chiavi su base periodica e, in caso di emergenza, potrebbe essere eseguito il rollover immediatamente.</span><span class="sxs-lookup"><span data-stu-id="9c300-105">It is important toonote that these keys rollover on a periodic basis and, in an emergency, could be rolled over immediately.</span></span> <span data-ttu-id="9c300-106">Tutte le applicazioni che usano Azure AD devono essere in grado di tooprogrammatically handle hello rollover della chiave processo o stabilire un processo di rollover manuale periodico.</span><span class="sxs-lookup"><span data-stu-id="9c300-106">All applications that use Azure AD should be able tooprogrammatically handle hello key rollover process or establish a periodic manual rollover process.</span></span> <span data-ttu-id="9c300-107">Continuare la lettura toounderstand il funzionamento delle chiavi di hello, come tooassess hello impatto di un'applicazione hello rollover tooyour e come tooupdate l'applicazione o stabilire un rollover della chiave toohandle processo periodico di attivazione manuale, se necessario.</span><span class="sxs-lookup"><span data-stu-id="9c300-107">Continue reading toounderstand how hello keys work, how tooassess hello impact of hello rollover tooyour application and how tooupdate your application or establish a periodic manual rollover process toohandle key rollover if necessary.</span></span>

## <a name="overview-of-signing-keys-in-azure-ad"></a><span data-ttu-id="9c300-108">Informazioni generali sulle chiavi di firma in Azure AD</span><span class="sxs-lookup"><span data-stu-id="9c300-108">Overview of signing keys in Azure AD</span></span>
<span data-ttu-id="9c300-109">Azure AD Usa la crittografia a chiave pubblica basata su trust tooestablish standard di settore tra l'elemento e hello applicazioni che lo utilizzano.</span><span class="sxs-lookup"><span data-stu-id="9c300-109">Azure AD uses public-key cryptography built on industry standards tooestablish trust between itself and hello applications that use it.</span></span> <span data-ttu-id="9c300-110">In pratica, questo procedimento funziona nel seguente modo hello: Azure AD Usa una chiave di firma costituita da una coppia di chiavi pubblica e privata.</span><span class="sxs-lookup"><span data-stu-id="9c300-110">In practical terms, this works in hello following way: Azure AD uses a signing key that consists of a public and private key pair.</span></span> <span data-ttu-id="9c300-111">Quando un utente accede tooan applicazione che usa Azure AD per l'autenticazione, Azure AD crea un token di sicurezza che contiene informazioni sull'utente hello.</span><span class="sxs-lookup"><span data-stu-id="9c300-111">When a user signs in tooan application that uses Azure AD for authentication, Azure AD creates a security token that contains information about hello user.</span></span> <span data-ttu-id="9c300-112">Questo token viene firmato da Azure AD usando la relativa chiave privata prima di inviarlo applicazione toohello indietro.</span><span class="sxs-lookup"><span data-stu-id="9c300-112">This token is signed by Azure AD using its private key before it is sent back toohello application.</span></span> <span data-ttu-id="9c300-113">tooverify che hello token sia valido e provenga effettivamente da Azure AD, l'applicazione hello deve convalidare firma del token hello con la chiave pubblica di hello esposta da Azure Active Directory nel tenant di hello [documento di individuazione OpenID Connect](http://openid.net/specs/openid-connect-discovery-1_0.html) o SAML/WS-Fed [documento metadati federazione](active-directory-federation-metadata.md).</span><span class="sxs-lookup"><span data-stu-id="9c300-113">tooverify that hello token is valid and actually originated from Azure AD, hello application must validate hello token’s signature using hello public key exposed by Azure AD that is contained in hello tenant’s [OpenID Connect discovery document](http://openid.net/specs/openid-connect-discovery-1_0.html) or SAML/WS-Fed [federation metadata document](active-directory-federation-metadata.md).</span></span>

<span data-ttu-id="9c300-114">Per motivi di sicurezza, esegue il rollback chiave su base periodica e, nel caso di hello di un'emergenza, di firma di Azure AD può essere eseguito il rollover immediatamente.</span><span class="sxs-lookup"><span data-stu-id="9c300-114">For security purposes, Azure AD’s signing key rolls on a periodic basis and, in hello case of an emergency, could be rolled over immediately.</span></span> <span data-ttu-id="9c300-115">Qualsiasi applicazione che si integra con Azure AD deve essere preparata toohandle un evento di rollover della chiave non è rilevante la frequenza con cui può verificarsi.</span><span class="sxs-lookup"><span data-stu-id="9c300-115">Any application that integrates with Azure AD should be prepared toohandle a key rollover event no matter how frequently it may occur.</span></span> <span data-ttu-id="9c300-116">Ciò non accade, se l'applicazione tenta di toouse una firma di hello scaduti tooverify chiave su un token, richiesta di accesso hello avrà esito negativo.</span><span class="sxs-lookup"><span data-stu-id="9c300-116">If it doesn’t, and your application attempts toouse an expired key tooverify hello signature on a token, hello sign-in request will fail.</span></span>

<span data-ttu-id="9c300-117">Non esiste più di una chiave valida è sempre disponibile nel documento di individuazione OpenID Connect hello e documento di metadati di federazione hello.</span><span class="sxs-lookup"><span data-stu-id="9c300-117">There is always more than one valid key available in hello OpenID Connect discovery document and hello federation metadata document.</span></span> <span data-ttu-id="9c300-118">L'applicazione deve essere preparata toouse qualsiasi chiave hello specificato nel documento hello, poiché una chiave può essere implementata a breve, un altro può essere relativa sostituzione e così via.</span><span class="sxs-lookup"><span data-stu-id="9c300-118">Your application should be prepared toouse any of hello keys specified in hello document, since one key may be rolled soon, another may be its replacement, and so forth.</span></span>

## <a name="how-tooassess-if-your-application-will-be-affected-and-what-toodo-about-it"></a><span data-ttu-id="9c300-119">Come tooassess se l'applicazione sarà interessata e quale toodo su di esso</span><span class="sxs-lookup"><span data-stu-id="9c300-119">How tooassess if your application will be affected and what toodo about it</span></span>
<span data-ttu-id="9c300-120">Il modo in cui l'applicazione gestisce il rollover della chiave dipende da variabili quali il tipo di hello di applicazione o il protocollo di identità e la libreria è stata utilizzata.</span><span class="sxs-lookup"><span data-stu-id="9c300-120">How your application handles key rollover depends on variables such as hello type of application or what identity protocol and library was used.</span></span> <span data-ttu-id="9c300-121">Hello nelle sezioni seguenti vengono valutare se i tipi più comuni di hello delle applicazioni sono interessati da rollover della chiave hello e forniscono indicazioni su come tooupdate il rollover automatico toosupport applicazione hello o aggiornare manualmente la chiave di hello.</span><span class="sxs-lookup"><span data-stu-id="9c300-121">hello sections below assess whether hello most common types of applications are impacted by hello key rollover and provide guidance on how tooupdate hello application toosupport automatic rollover or manually update hello key.</span></span>

* [<span data-ttu-id="9c300-122">Applicazioni client native che accedono alle risorse</span><span class="sxs-lookup"><span data-stu-id="9c300-122">Native client applications accessing resources</span></span>](#nativeclient)
* [<span data-ttu-id="9c300-123">API / applicazioni Web che accedono alle risorse</span><span class="sxs-lookup"><span data-stu-id="9c300-123">Web applications / APIs accessing resources</span></span>](#webclient)
* [<span data-ttu-id="9c300-124">API / applicazioni Web che proteggono le risorse e sono state compilate con i servizi app di Azure</span><span class="sxs-lookup"><span data-stu-id="9c300-124">Web applications / APIs protecting resources and built using Azure App Services</span></span>](#appservices)
* [<span data-ttu-id="9c300-125">API / applicazioni Web che proteggono le risorse usando middleware .NET OWIN OpenID Connect, WS-Fed o WindowsAzureActiveDirectoryBearerAuthentication</span><span class="sxs-lookup"><span data-stu-id="9c300-125">Web applications / APIs protecting resources using .NET OWIN OpenID Connect, WS-Fed or WindowsAzureActiveDirectoryBearerAuthentication middleware</span></span>](#owin)
* [<span data-ttu-id="9c300-126">API / applicazioni Web che proteggono le risorse usando middleware .NET Core OpenID Connect o JwtBearerAuthentication</span><span class="sxs-lookup"><span data-stu-id="9c300-126">Web applications / APIs protecting resources using .NET Core OpenID Connect or  JwtBearerAuthentication middleware</span></span>](#owincore)
* [<span data-ttu-id="9c300-127">API / applicazioni Web che proteggono le risorse usando il modulo Node.js passport-azure-ad</span><span class="sxs-lookup"><span data-stu-id="9c300-127">Web applications / APIs protecting resources using Node.js passport-azure-ad module</span></span>](#passport)
* [<span data-ttu-id="9c300-128">API/applicazioni Web che proteggono le risorse e sono state create con Visual Studio 2015 o Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="9c300-128">Web applications / APIs protecting resources and created with Visual Studio 2015 or Visual Studio 2017</span></span>](#vs2015)
* [<span data-ttu-id="9c300-129">Applicazioni Web che proteggono le risorse e sono state create con Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="9c300-129">Web applications protecting resources and created with Visual Studio 2013</span></span>](#vs2013)
* [<span data-ttu-id="9c300-130">API Web che proteggono le risorse e sono state create con Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="9c300-130">Web APIs protecting resources and created with Visual Studio 2013</span></span>](#vs2013_webapi)
* [<span data-ttu-id="9c300-131">Applicazioni Web che proteggono le risorse e sono state create con Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="9c300-131">Web applications protecting resources and created with Visual Studio 2012</span></span>](#vs2012)
* [<span data-ttu-id="9c300-132">Applicazioni Web che proteggono le risorse e sono state create con Visual Studio 2010 o 2008 o con Windows Identity Foundation</span><span class="sxs-lookup"><span data-stu-id="9c300-132">Web applications protecting resources and created with Visual Studio 2010, 2008 o using Windows Identity Foundation</span></span>](#vs2010)
* [<span data-ttu-id="9c300-133">Applicazioni Web / API di protezione delle risorse utilizzando qualsiasi altre librerie o implementare manualmente uno di hello protocolli supportati</span><span class="sxs-lookup"><span data-stu-id="9c300-133">Web applications / APIs protecting resources using any other libraries or manually implementing any of hello supported protocols</span></span>](#other)

<span data-ttu-id="9c300-134">Queste indicazioni **non** sono valide per:</span><span class="sxs-lookup"><span data-stu-id="9c300-134">This guidance is **not** applicable for:</span></span>

* <span data-ttu-id="9c300-135">Applicazioni aggiunte dalla raccolta di applicazioni AD Azure (incluso personalizzato) hanno apposite istruzioni con relativamente toosigning chiavi.</span><span class="sxs-lookup"><span data-stu-id="9c300-135">Applications added from Azure AD Application Gallery (including Custom) have separate guidance with regards toosigning keys.</span></span> [<span data-ttu-id="9c300-136">Altre informazioni.</span><span class="sxs-lookup"><span data-stu-id="9c300-136">More information.</span></span>](../active-directory-sso-certs.md)
* <span data-ttu-id="9c300-137">Locale non dispone di applicazioni pubblicate tramite proxy applicazione tooworry sulle chiavi di firma.</span><span class="sxs-lookup"><span data-stu-id="9c300-137">On-premises applications published via application proxy don't have tooworry about signing keys.</span></span>

### <span data-ttu-id="9c300-138"><a name="nativeclient"></a>Applicazioni client native che accedono alle risorse</span><span class="sxs-lookup"><span data-stu-id="9c300-138"><a name="nativeclient"></a>Native client applications accessing resources</span></span>
<span data-ttu-id="9c300-139">Le applicazioni che si limitano ad accedere alle risorse, come</span><span class="sxs-lookup"><span data-stu-id="9c300-139">Applications that are only accessing resources (i.e</span></span> <span data-ttu-id="9c300-140">Microsoft Graph, KeyVault, API di Outlook e altre APIs Microsoft) in genere solo ottenere un token e passarlo lungo toohello proprietario della risorsa.</span><span class="sxs-lookup"><span data-stu-id="9c300-140">Microsoft Graph, KeyVault, Outlook API and other Microsoft APIs) generally only obtain a token and pass it along toohello resource owner.</span></span> <span data-ttu-id="9c300-141">Dato che non sono per proteggere le risorse, non controllano il token hello e pertanto non è necessario tooensure che è firmato correttamente.</span><span class="sxs-lookup"><span data-stu-id="9c300-141">Given that they are not protecting any resources, they do not inspect hello token and therefore do not need tooensure it is properly signed.</span></span>

<span data-ttu-id="9c300-142">Le applicazioni client native, se i computer desktop o portatile, in questa categoria rientrano e sono pertanto non è interessate da rollover hello.</span><span class="sxs-lookup"><span data-stu-id="9c300-142">Native client applications, whether desktop or mobile, fall into this category and are thus not impacted by hello rollover.</span></span>

### <span data-ttu-id="9c300-143"><a name="webclient"></a>API / applicazioni Web che accedono alle risorse</span><span class="sxs-lookup"><span data-stu-id="9c300-143"><a name="webclient"></a>Web applications / APIs accessing resources</span></span>
<span data-ttu-id="9c300-144">Le applicazioni che si limitano ad accedere alle risorse, come</span><span class="sxs-lookup"><span data-stu-id="9c300-144">Applications that are only accessing resources (i.e</span></span> <span data-ttu-id="9c300-145">Microsoft Graph, KeyVault, API di Outlook e altre APIs Microsoft) in genere solo ottenere un token e passarlo lungo toohello proprietario della risorsa.</span><span class="sxs-lookup"><span data-stu-id="9c300-145">Microsoft Graph, KeyVault, Outlook API and other Microsoft APIs) generally only obtain a token and pass it along toohello resource owner.</span></span> <span data-ttu-id="9c300-146">Dato che non sono per proteggere le risorse, non controllano il token hello e pertanto non è necessario tooensure che è firmato correttamente.</span><span class="sxs-lookup"><span data-stu-id="9c300-146">Given that they are not protecting any resources, they do not inspect hello token and therefore do not need tooensure it is properly signed.</span></span>

<span data-ttu-id="9c300-147">Le applicazioni Web e le API web che utilizzano il flusso solo app hello (credenziali client / certificato client), in questa categoria rientrano e sono pertanto non è interessato da rollover hello.</span><span class="sxs-lookup"><span data-stu-id="9c300-147">Web applications and web APIs that are using hello app-only flow (client credentials / client certificate), fall into this category and are thus not impacted by hello rollover.</span></span>

### <span data-ttu-id="9c300-148"><a name="appservices"></a>API / applicazioni Web che proteggono le risorse e sono state compilate con i servizi app di Azure</span><span class="sxs-lookup"><span data-stu-id="9c300-148"><a name="appservices"></a>Web applications / APIs protecting resources and built using Azure App Services</span></span>
<span data-ttu-id="9c300-149">L'autenticazione di Azure i servizi App / funzionalità di autorizzazione (EasyAuth) dispone già di rollover della chiave toohandle logica necessaria hello automaticamente.</span><span class="sxs-lookup"><span data-stu-id="9c300-149">Azure App Services' Authentication / Authorization (EasyAuth) functionality already has hello necessary logic toohandle key rollover automatically.</span></span>

### <span data-ttu-id="9c300-150"><a name="owin"></a>API / applicazioni Web che proteggono le risorse usando middleware .NET OWIN OpenID Connect, WS-Fed o WindowsAzureActiveDirectoryBearerAuthentication</span><span class="sxs-lookup"><span data-stu-id="9c300-150"><a name="owin"></a>Web applications / APIs protecting resources using .NET OWIN OpenID Connect, WS-Fed or WindowsAzureActiveDirectoryBearerAuthentication middleware</span></span>
<span data-ttu-id="9c300-151">Se l'applicazione utilizza hello .NET OWIN OpenID Connect, WS-Fed o middleware WindowsAzureActiveDirectoryBearerAuthentication, contiene già il rollover della chiave toohandle logica necessaria hello automaticamente.</span><span class="sxs-lookup"><span data-stu-id="9c300-151">If your application is using hello .NET OWIN OpenID Connect, WS-Fed or WindowsAzureActiveDirectoryBearerAuthentication middleware, it already has hello necessary logic toohandle key rollover automatically.</span></span>

<span data-ttu-id="9c300-152">È possibile verificare che l'applicazione utilizza uno di questi mediante la ricerca di uno qualsiasi dei seguenti frammenti di codice in Startup.cs o Startup.Auth.cs dell'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="9c300-152">You can confirm that your application is using any of these by looking for any of hello following snippets in your application's Startup.cs or Startup.Auth.cs</span></span>

```
app.UseOpenIdConnectAuthentication(
     new OpenIdConnectAuthenticationOptions
     {
         // ...
     });
```
```
app.UseWsFederationAuthentication(
    new WsFederationAuthenticationOptions
    {
     // ...
     });
```
```
 app.UseWindowsAzureActiveDirectoryBearerAuthentication(
     new WindowsAzureActiveDirectoryBearerAuthenticationOptions
     {
     // ...
     });
```

### <span data-ttu-id="9c300-153"><a name="owincore"></a>API / applicazioni Web che proteggono le risorse usando middleware .NET Core OpenID Connect o JwtBearerAuthentication</span><span class="sxs-lookup"><span data-stu-id="9c300-153"><a name="owincore"></a>Web applications / APIs protecting resources using .NET Core OpenID Connect or  JwtBearerAuthentication middleware</span></span>
<span data-ttu-id="9c300-154">Se l'applicazione utilizza hello .NET Core OWIN OpenID Connect o middleware JwtBearerAuthentication, contiene già il rollover della chiave toohandle logica necessaria hello automaticamente.</span><span class="sxs-lookup"><span data-stu-id="9c300-154">If your application is using hello .NET Core OWIN OpenID Connect  or JwtBearerAuthentication middleware, it already has hello necessary logic toohandle key rollover automatically.</span></span>

<span data-ttu-id="9c300-155">È possibile verificare che l'applicazione utilizza uno di questi mediante la ricerca di uno qualsiasi dei seguenti frammenti di codice in Startup.cs o Startup.Auth.cs dell'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="9c300-155">You can confirm that your application is using any of these by looking for any of hello following snippets in your application's Startup.cs or Startup.Auth.cs</span></span>

```
app.UseOpenIdConnectAuthentication(
     new OpenIdConnectAuthenticationOptions
     {
         // ...
     });
```
```
app.UseJwtBearerAuthentication(
    new JwtBearerAuthenticationOptions
    {
     // ...
     });
```

### <span data-ttu-id="9c300-156"><a name="passport"></a>API / applicazioni Web che proteggono le risorse usando il modulo Node.js passport-azure-ad</span><span class="sxs-lookup"><span data-stu-id="9c300-156"><a name="passport"></a>Web applications / APIs protecting resources using Node.js passport-azure-ad module</span></span>
<span data-ttu-id="9c300-157">Se l'applicazione utilizza hello Node.js passport ad modulo, contiene già il rollover della chiave toohandle logica necessaria hello automaticamente.</span><span class="sxs-lookup"><span data-stu-id="9c300-157">If your application is using hello Node.js passport-ad module, it already has hello necessary logic toohandle key rollover automatically.</span></span>

<span data-ttu-id="9c300-158">È possibile verificare che l'applicazione Active Directory a passport cercando hello seguente frammento di in app.js dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="9c300-158">You can confirm that your application passport-ad by searching for hello following snippet in your application's app.js</span></span>

```
var OIDCStrategy = require('passport-azure-ad').OIDCStrategy;

passport.use(new OIDCStrategy({
    //...
));
```

### <span data-ttu-id="9c300-159"><a name="vs2015"></a>API/applicazioni Web che proteggono le risorse e sono state create con Visual Studio 2015 o Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="9c300-159"><a name="vs2015"></a>Web applications / APIs protecting resources and created with Visual Studio 2015 or Visual Studio 2017</span></span>
<span data-ttu-id="9c300-160">Se l'applicazione è stato creato utilizzando un modello di applicazione web in Visual Studio 2015 o Visual Studio 2017 ed è stata selezionata **di lavoro e l'account dell'istituto di istruzione** da hello **Modifica autenticazione** menu, ha già dispone automaticamente di rollover della chiave toohandle hello logica necessaria.</span><span class="sxs-lookup"><span data-stu-id="9c300-160">If your application was built using a web application template in Visual Studio 2015 or Visual Studio 2017 and you selected **Work And School Accounts** from hello **Change Authentication** menu, it already has hello necessary logic toohandle key rollover automatically.</span></span> <span data-ttu-id="9c300-161">Questa logica incorporata nel middleware OWIN OpenID Connect hello, recupera e memorizza nella cache le chiavi di hello dal documento di individuazione OpenID Connect hello e vengono aggiornati periodicamente.</span><span class="sxs-lookup"><span data-stu-id="9c300-161">This logic, embedded in hello OWIN OpenID Connect middleware, retrieves and caches hello keys from hello OpenID Connect discovery document and periodically refreshes them.</span></span>

<span data-ttu-id="9c300-162">Se si aggiunta manualmente soluzione tooyour di autenticazione, l'applicazione non dispone della logica di rollover della chiave necessario hello.</span><span class="sxs-lookup"><span data-stu-id="9c300-162">If you added authentication tooyour solution manually, your application might not have hello necessary key rollover logic.</span></span> <span data-ttu-id="9c300-163">Sarà necessario toowrite, oppure hello seguire i passaggi [applicazioni Web API con tutte le altre librerie o implementare manualmente uno di hello supportati i protocolli.](#other).</span><span class="sxs-lookup"><span data-stu-id="9c300-163">You will need toowrite it yourself, or follow hello steps in [Web applications / APIs using any other libraries or manually implementing any of hello supported protocols.](#other).</span></span>

### <span data-ttu-id="9c300-164"><a name="vs2013"></a>Applicazioni Web che proteggono le risorse e sono state create con Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="9c300-164"><a name="vs2013"></a>Web applications protecting resources and created with Visual Studio 2013</span></span>
<span data-ttu-id="9c300-165">Se l'applicazione è stato creato utilizzando un modello di applicazione web in Visual Studio 2013 ed è stata selezionata **account aziendali** da hello **Modifica autenticazione** menu contiene già hello necessario rollover della chiave automaticamente toohandle logica.</span><span class="sxs-lookup"><span data-stu-id="9c300-165">If your application was built using a web application template in Visual Studio 2013 and you selected **Organizational Accounts** from hello **Change Authentication** menu, it already has hello necessary logic toohandle key rollover automatically.</span></span> <span data-ttu-id="9c300-166">Tale logica archivia l'identificatore univoco dell'organizzazione e la firma delle informazioni chiave in due tabelle di database associati al progetto hello hello.</span><span class="sxs-lookup"><span data-stu-id="9c300-166">This logic stores your organization’s unique identifier and hello signing key information in two database tables associated with hello project.</span></span> <span data-ttu-id="9c300-167">È possibile trovare la stringa di connessione hello per database hello nel file Web. config del progetto hello.</span><span class="sxs-lookup"><span data-stu-id="9c300-167">You can find hello connection string for hello database in hello project’s Web.config file.</span></span>

<span data-ttu-id="9c300-168">Se si aggiunta manualmente soluzione tooyour di autenticazione, l'applicazione non dispone della logica di rollover della chiave necessario hello.</span><span class="sxs-lookup"><span data-stu-id="9c300-168">If you added authentication tooyour solution manually, your application might not have hello necessary key rollover logic.</span></span> <span data-ttu-id="9c300-169">Sarà necessario toowrite, oppure hello seguire i passaggi [applicazioni Web API con tutte le altre librerie o implementare manualmente uno di hello supportati i protocolli.](#other).</span><span class="sxs-lookup"><span data-stu-id="9c300-169">You will need toowrite it yourself, or follow hello steps in [Web applications / APIs using any other libraries or manually implementing any of hello supported protocols.](#other).</span></span>

<span data-ttu-id="9c300-170">Hello alla procedura seguente consente di verificare il corretto funzionamento di logica di hello nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="9c300-170">hello following steps will help you verify that hello logic is working properly in your application.</span></span>

1. <span data-ttu-id="9c300-171">In Visual Studio 2013, aprire la soluzione hello e quindi fare clic su hello **Esplora Server** scheda nella finestra di destra hello.</span><span class="sxs-lookup"><span data-stu-id="9c300-171">In Visual Studio 2013, open hello solution, and then click on hello **Server Explorer** tab on hello right window.</span></span>
2. <span data-ttu-id="9c300-172">Espandere **Connessioni dati**, **DefaultConnection** e quindi **Tabelle**.</span><span class="sxs-lookup"><span data-stu-id="9c300-172">Expand **Data Connections**, **DefaultConnection**, and then **Tables**.</span></span> <span data-ttu-id="9c300-173">Individuare hello **tenant** tabella pulsante destro del mouse e quindi fare clic su **Mostra dati tabella**.</span><span class="sxs-lookup"><span data-stu-id="9c300-173">Locate hello **IssuingAuthorityKeys** table, right-click it, and then click **Show Table Data**.</span></span>
3. <span data-ttu-id="9c300-174">In hello **tenant** tabella, sarà presente almeno una riga, che corrisponde a toohello valore di identificazione personale per la chiave di hello.</span><span class="sxs-lookup"><span data-stu-id="9c300-174">In hello **IssuingAuthorityKeys** table, there will be at least one row, which corresponds toohello thumbprint value for hello key.</span></span> <span data-ttu-id="9c300-175">Eliminare tutte le righe nella tabella hello.</span><span class="sxs-lookup"><span data-stu-id="9c300-175">Delete any rows in hello table.</span></span>
4. <span data-ttu-id="9c300-176">Pulsante destro del mouse hello **tenant** tabella e quindi fare clic su **Mostra dati tabella**.</span><span class="sxs-lookup"><span data-stu-id="9c300-176">Right-click hello **Tenants** table, and then click **Show Table Data**.</span></span>
5. <span data-ttu-id="9c300-177">In hello **tenant** tabella, sarà presente almeno una riga, che corrisponde l'identificatore del tenant tooa directory univoco.</span><span class="sxs-lookup"><span data-stu-id="9c300-177">In hello **Tenants** table, there will be at least one row, which corresponds tooa unique directory tenant identifier.</span></span> <span data-ttu-id="9c300-178">Eliminare tutte le righe nella tabella hello.</span><span class="sxs-lookup"><span data-stu-id="9c300-178">Delete any rows in hello table.</span></span> <span data-ttu-id="9c300-179">Se non si elimina righe hello in entrambi hello **tenant** tabella e **tenant** tabella, si verificherà un errore in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="9c300-179">If you don't delete hello rows in both hello **Tenants** table and **IssuingAuthorityKeys** table, you will get an error at runtime.</span></span>
6. <span data-ttu-id="9c300-180">Compilare ed eseguire un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="9c300-180">Build and run hello application.</span></span> <span data-ttu-id="9c300-181">Dopo aver eseguito l'accesso in tooyour account, è possibile arrestare l'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="9c300-181">After you have logged in tooyour account, you can stop hello application.</span></span>
7. <span data-ttu-id="9c300-182">Restituire toohello **Esplora Server** ed esaminare i valori hello in hello **tenant** e **tenant** tabella.</span><span class="sxs-lookup"><span data-stu-id="9c300-182">Return toohello **Server Explorer** and look at hello values in hello **IssuingAuthorityKeys** and **Tenants** table.</span></span> <span data-ttu-id="9c300-183">Si noterà sono stati inseriti automaticamente con le informazioni appropriate hello dal documento di metadati di federazione hello.</span><span class="sxs-lookup"><span data-stu-id="9c300-183">You’ll notice that they have been automatically repopulated with hello appropriate information from hello federation metadata document.</span></span>

### <span data-ttu-id="9c300-184"><a name="vs2013"></a>API Web che proteggono le risorse e sono state create con Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="9c300-184"><a name="vs2013"></a>Web APIs protecting resources and created with Visual Studio 2013</span></span>
<span data-ttu-id="9c300-185">Se si creato un'applicazione API web in Visual Studio 2013 mediante il modello di API Web hello e quindi selezionato **account aziendali** da hello **Modifica autenticazione** menu già avere hello logica necessaria nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="9c300-185">If you created a web API application in Visual Studio 2013 using hello Web API template, and then selected **Organizational Accounts** from hello **Change Authentication** menu, you already have hello necessary logic in your application.</span></span>

<span data-ttu-id="9c300-186">Se è stato configurato manualmente authentication, attenersi alle istruzioni hello seguenti toolearn come tooconfigure tooautomatically l'API Web aggiornare le informazioni sulla chiave.</span><span class="sxs-lookup"><span data-stu-id="9c300-186">If you manually configured authentication, follow hello instructions below toolearn how tooconfigure your Web API tooautomatically update its key information.</span></span>

<span data-ttu-id="9c300-187">Hello frammento di codice seguente viene illustrato come tooget hello chiavi più recenti dal documento di metadati di federazione hello e quindi utilizzare hello [gestore dei Token JWT](https://msdn.microsoft.com/library/dn205065.aspx) token hello toovalidate.</span><span class="sxs-lookup"><span data-stu-id="9c300-187">hello following code snippet demonstrates how tooget hello latest keys from hello federation metadata document, and then use hello [JWT Token Handler](https://msdn.microsoft.com/library/dn205065.aspx) toovalidate hello token.</span></span> <span data-ttu-id="9c300-188">frammento di codice Hello si presuppone che si utilizzerà un meccanismo per la persistenza toovalidate chiave di hello futuri di memorizzazione nella cache dei token da Azure AD, che può essere in un database, file di configurazione o in un' posizione.</span><span class="sxs-lookup"><span data-stu-id="9c300-188">hello code snippet assumes that you will use your own caching mechanism for persisting hello key toovalidate future tokens from Azure AD, whether it be in a database, configuration file, or elsewhere.</span></span>

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.IdentityModel.Tokens;
using System.Configuration;
using System.Security.Cryptography.X509Certificates;
using System.Xml;
using System.IdentityModel.Metadata;
using System.ServiceModel.Security;
using System.Threading;

namespace JWTValidation
{
    public class JWTValidator
    {
        private string MetadataAddress = "[Your Federation Metadata document address goes here]";

        // Validates hello JWT Token that's part of hello Authorization header in an HTTP request.
        public void ValidateJwtToken(string token)
        {
            JwtSecurityTokenHandler tokenHandler = new JwtSecurityTokenHandler()
            {
                // Do not disable for production code
                CertificateValidator = X509CertificateValidator.None
            };

            TokenValidationParameters validationParams = new TokenValidationParameters()
            {
                AllowedAudience = "[Your App ID URI goes here, as registered in hello Azure Classic Portal]",
                ValidIssuer = "[hello issuer for hello token goes here, such as https://sts.windows.net/68b98905-130e-4d7c-b6e1-a158a9ed8449/]",
                SigningTokens = GetSigningCertificates(MetadataAddress)

                // Cache hello signing tokens by your desired mechanism
            };

            Thread.CurrentPrincipal = tokenHandler.ValidateToken(token, validationParams);
        }

        // Returns a list of certificates from hello specified metadata document.
        public List<X509SecurityToken> GetSigningCertificates(string metadataAddress)
        {
            List<X509SecurityToken> tokens = new List<X509SecurityToken>();

            if (metadataAddress == null)
            {
                throw new ArgumentNullException(metadataAddress);
            }

            using (XmlReader metadataReader = XmlReader.Create(metadataAddress))
            {
                MetadataSerializer serializer = new MetadataSerializer()
                {
                    // Do not disable for production code
                    CertificateValidationMode = X509CertificateValidationMode.None
                };

                EntityDescriptor metadata = serializer.ReadMetadata(metadataReader) as EntityDescriptor;

                if (metadata != null)
                {
                    SecurityTokenServiceDescriptor stsd = metadata.RoleDescriptors.OfType<SecurityTokenServiceDescriptor>().First();

                    if (stsd != null)
                    {
                        IEnumerable<X509RawDataKeyIdentifierClause> x509DataClauses = stsd.Keys.Where(key => key.KeyInfo != null && (key.Use == KeyType.Signing || key.Use == KeyType.Unspecified)).
                                                             Select(key => key.KeyInfo.OfType<X509RawDataKeyIdentifierClause>().First());

                        tokens.AddRange(x509DataClauses.Select(token => new X509SecurityToken(new X509Certificate2(token.GetX509RawData()))));
                    }
                    else
                    {
                        throw new InvalidOperationException("There is no RoleDescriptor of type SecurityTokenServiceType in hello metadata");
                    }
                }
                else
                {
                    throw new Exception("Invalid Federation Metadata document");
                }
            }
            return tokens;
        }
    }
}
```

### <span data-ttu-id="9c300-189"><a name="vs2012"></a>Applicazioni Web che proteggono le risorse e sono state create con Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="9c300-189"><a name="vs2012"></a>Web applications protecting resources and created with Visual Studio 2012</span></span>
<span data-ttu-id="9c300-190">Se l'applicazione è stata creata in Visual Studio 2012, è stato probabilmente usato hello identità e tooconfigure dello strumento di accesso dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="9c300-190">If your application was built in Visual Studio 2012, you probably used hello Identity and Access Tool tooconfigure your application.</span></span> <span data-ttu-id="9c300-191">È inoltre probabile che si sta utilizzando hello [convalida Issuer Name Registry (VINR)](https://msdn.microsoft.com/library/dn205067.aspx).</span><span class="sxs-lookup"><span data-stu-id="9c300-191">It’s also likely that you are using hello [Validating Issuer Name Registry (VINR)](https://msdn.microsoft.com/library/dn205067.aspx).</span></span> <span data-ttu-id="9c300-192">Hello VINR è responsabile della gestione delle informazioni sui provider di identità attendibili (Azure AD) e le chiavi di hello utilizzate toovalidate token emesso da essi.</span><span class="sxs-lookup"><span data-stu-id="9c300-192">hello VINR is responsible for maintaining information about trusted identity providers (Azure AD) and hello keys used toovalidate tokens issued by them.</span></span> <span data-ttu-id="9c300-193">Hello VINR rende facile tooautomatically aggiornamento hello informazioni sulle chiavi archiviate in un file Web. config scaricando hello più recente documento metadati federazione associato alla directory, controllando se hello non aggiornato con hello più recente documento e l'aggiornamento hello applicazione toouse hello nuova chiave in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="9c300-193">hello VINR also makes it easy tooautomatically update hello key information stored in a Web.config file by downloading hello latest federation metadata document associated with your directory, checking if hello configuration is out of date with hello latest document, and updating hello application toouse hello new key as necessary.</span></span>

<span data-ttu-id="9c300-194">Se è stato creato l'applicazione utilizzando uno degli esempi di codice hello o dettagliate fornite da Microsoft, la logica di rollover della chiave hello è già incluso nel progetto.</span><span class="sxs-lookup"><span data-stu-id="9c300-194">If you created your application using any of hello code samples or walkthrough documentation provided by Microsoft, hello key rollover logic is already included in your project.</span></span> <span data-ttu-id="9c300-195">Si noterà che codice hello seguente esiste già nel progetto.</span><span class="sxs-lookup"><span data-stu-id="9c300-195">You will notice that hello code below already exists in your project.</span></span> <span data-ttu-id="9c300-196">Se l'applicazione non dispone già di questa logica, seguire i passaggi di hello sotto tooadd e tooverify che funzioni correttamente.</span><span class="sxs-lookup"><span data-stu-id="9c300-196">If your application does not already have this logic, follow hello steps below tooadd it and tooverify that it’s working correctly.</span></span>

1. <span data-ttu-id="9c300-197">In **Esplora**, aggiungere un riferimento toohello **System. IdentityModel** assembly per il progetto appropriato hello.</span><span class="sxs-lookup"><span data-stu-id="9c300-197">In **Solution Explorer**, add a reference toohello **System.IdentityModel** assembly for hello appropriate project.</span></span>
2. <span data-ttu-id="9c300-198">Aprire hello **Global.asax.cs** file e aggiungere hello seguenti direttive using:</span><span class="sxs-lookup"><span data-stu-id="9c300-198">Open hello **Global.asax.cs** file and add hello following using directives:</span></span>
   ```
   using System.Configuration;
   using System.IdentityModel.Tokens;
   ```
3. <span data-ttu-id="9c300-199">Aggiungere hello seguente metodo toohello **Global.asax.cs** file:</span><span class="sxs-lookup"><span data-stu-id="9c300-199">Add hello following method toohello **Global.asax.cs** file:</span></span>
   ```
   protected void RefreshValidationSettings()
   {
    string configPath = AppDomain.CurrentDomain.BaseDirectory + "\\" + "Web.config";
    string metadataAddress =
                  ConfigurationManager.AppSettings["ida:FederationMetadataLocation"];
    ValidatingIssuerNameRegistry.WriteToConfig(metadataAddress, configPath);
   }
   ```
4. <span data-ttu-id="9c300-200">Richiamare hello **refreshvalidationsettings ()** metodo hello **Application_Start ()** metodo **Global.asax.cs** come illustrato:</span><span class="sxs-lookup"><span data-stu-id="9c300-200">Invoke hello **RefreshValidationSettings()** method in hello **Application_Start()** method in **Global.asax.cs** as shown:</span></span>
   ```
   protected void Application_Start()
   {
    AreaRegistration.RegisterAllAreas();
    ...
    RefreshValidationSettings();
   }
   ```

<span data-ttu-id="9c300-201">Dopo aver eseguito questi passaggi, Web. config dell'applicazione verrà aggiornato con informazioni più recenti di hello dal documento di metadati di federazione hello, incluse le chiavi più recenti di hello.</span><span class="sxs-lookup"><span data-stu-id="9c300-201">Once you have followed these steps, your application’s Web.config will be updated with hello latest information from hello federation metadata document, including hello latest keys.</span></span> <span data-ttu-id="9c300-202">Questo aggiornamento si verificherà ogni volta che il pool di applicazioni viene riciclato in IIS. Per impostazione predefinita IIS è toorecycle applicazioni 29 ore.</span><span class="sxs-lookup"><span data-stu-id="9c300-202">This update will occur every time your application pool recycles in IIS; by default IIS is set toorecycle applications every 29 hours.</span></span>

<span data-ttu-id="9c300-203">Eseguire operazioni di hello seguenti tooverify che la logica di rollover della chiave hello sia in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="9c300-203">Follow hello steps below tooverify that hello key rollover logic is working.</span></span>

1. <span data-ttu-id="9c300-204">Dopo aver verificato che l'applicazione utilizza codice hello sopra, aprire hello **Web. config** file e passare toohello  **<issuerNameRegistry>**  blocco, cercare in particolare hello alcune righe seguenti:</span><span class="sxs-lookup"><span data-stu-id="9c300-204">After you have verified that your application is using hello code above, open hello **Web.config** file and navigate toohello **<issuerNameRegistry>** block, specifically looking for hello following few lines:</span></span>
   ```
   <issuerNameRegistry type="System.IdentityModel.Tokens.ValidatingIssuerNameRegistry, System.IdentityModel.Tokens.ValidatingIssuerNameRegistry">
        <authority name="https://sts.windows.net/ec4187af-07da-4f01-b18f-64c2f5abecea/">
          <keys>
            <add thumbprint="3A38FA984E8560F19AADC9F86FE9594BB6AD049B" />
          </keys>
   ```
2. <span data-ttu-id="9c300-205">In hello  **<add thumbprint=””>**  impostazione, modificare il valore di identificazione personale hello sostituendo ogni carattere con uno diverso.</span><span class="sxs-lookup"><span data-stu-id="9c300-205">In hello **<add thumbprint=””>** setting, change hello thumbprint value by replacing any character with a different one.</span></span> <span data-ttu-id="9c300-206">Salvare hello **Web. config** file.</span><span class="sxs-lookup"><span data-stu-id="9c300-206">Save hello **Web.config** file.</span></span>
3. <span data-ttu-id="9c300-207">Compilare un'applicazione hello e quindi eseguirlo.</span><span class="sxs-lookup"><span data-stu-id="9c300-207">Build hello application, and then run it.</span></span> <span data-ttu-id="9c300-208">Se è possibile completare hello Accedi processo, l'applicazione aggiorna in modo corretto la chiave hello scaricando informazioni hello necessario dal documento di metadati di federazione della directory.</span><span class="sxs-lookup"><span data-stu-id="9c300-208">If you can complete hello sign-in process, your application is successfully updating hello key by downloading hello required information from your directory’s federation metadata document.</span></span> <span data-ttu-id="9c300-209">Se si sono verificati problemi di accesso, verificare le modifiche di hello nell'applicazione siano corrette leggendo hello [tooYour aggiunta Sign-On Web dell'applicazione tramite Azure Active Directory](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect) argomento oppure scaricare ed esaminare hello nell'esempio di codice seguente: [ Applicazione Cloud multi-Tenant per Azure Active Directory](https://code.msdn.microsoft.com/multi-tenant-cloud-8015b84b).</span><span class="sxs-lookup"><span data-stu-id="9c300-209">If you are having issues signing in, ensure hello changes in your application are correct by reading hello [Adding Sign-On tooYour Web Application Using Azure AD](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect) topic, or downloading and inspecting hello following code sample: [Multi-Tenant Cloud Application for Azure Active Directory](https://code.msdn.microsoft.com/multi-tenant-cloud-8015b84b).</span></span>

### <span data-ttu-id="9c300-210"><a name="vs2010"></a>Applicazioni Web che proteggono le risorse e sono state create con Visual Studio 2008 o 2010 o con Windows Identity Foundation (WIF) v1.0 per .NET 3.5</span><span class="sxs-lookup"><span data-stu-id="9c300-210"><a name="vs2010"></a>Web applications protecting resources and created with Visual Studio 2008 or 2010 and Windows Identity Foundation (WIF) v1.0 for .NET 3.5</span></span>
<span data-ttu-id="9c300-211">Se è stata compilata un'applicazione in WIF v 1.0, non vi è alcun aggiornamento tooautomatically meccanismo toouse di configurazione dell'applicazione una nuova chiave.</span><span class="sxs-lookup"><span data-stu-id="9c300-211">If you built an application on WIF v1.0, there is no provided mechanism tooautomatically refresh your application’s configuration toouse a new key.</span></span>

* <span data-ttu-id="9c300-212">*Il modo più semplice* utilizzare strumento di FedUtil hello incluso in WIF SDK, che può recuperare il documento di metadati più recente hello e aggiornare la configurazione di hello.</span><span class="sxs-lookup"><span data-stu-id="9c300-212">*Easiest way* Use hello FedUtil tooling included in hello WIF SDK, which can retrieve hello latest metadata document and update your configuration.</span></span>
* <span data-ttu-id="9c300-213">Aggiornare il too.NET applicazione 4.5, che include la versione più recente di hello di WIF nello spazio dei nomi System hello.</span><span class="sxs-lookup"><span data-stu-id="9c300-213">Update your application too.NET 4.5, which includes hello newest version of WIF located in hello System namespace.</span></span> <span data-ttu-id="9c300-214">È quindi possibile utilizzare hello [convalida Issuer Name Registry (VINR)](https://msdn.microsoft.com/library/dn205067.aspx) tooperform aggiornamenti automatici della configurazione dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="9c300-214">You can then use hello [Validating Issuer Name Registry (VINR)](https://msdn.microsoft.com/library/dn205067.aspx) tooperform automatic updates of hello application’s configuration.</span></span>
* <span data-ttu-id="9c300-215">Eseguire un rollover manuale in base alle istruzioni hello alla fine di hello di questo documento di istruzioni.</span><span class="sxs-lookup"><span data-stu-id="9c300-215">Perform a manual rollover as per hello instructions at hello end of this guidance document.</span></span>

<span data-ttu-id="9c300-216">Istruzioni toouse hello FedUtil tooupdate la configurazione:</span><span class="sxs-lookup"><span data-stu-id="9c300-216">Instructions toouse hello FedUtil tooupdate your configuration:</span></span>

1. <span data-ttu-id="9c300-217">Verificare di aver hello WIF v 1.0 SDK installato nel computer di sviluppo per Visual Studio 2008 o 2010.</span><span class="sxs-lookup"><span data-stu-id="9c300-217">Verify that you have hello WIF v1.0 SDK installed on your development machine for Visual Studio 2008 or 2010.</span></span> <span data-ttu-id="9c300-218">È possibile [scaricarlo da qui](https://www.microsoft.com/en-us/download/details.aspx?id=4451) se non è ancora installato.</span><span class="sxs-lookup"><span data-stu-id="9c300-218">You can [download it from here](https://www.microsoft.com/en-us/download/details.aspx?id=4451) if you have not yet installed it.</span></span>
2. <span data-ttu-id="9c300-219">In Visual Studio, aprire la soluzione hello, quindi fare clic sul progetto applicabile hello e selezionare **aggiornare i metadati di federazione**.</span><span class="sxs-lookup"><span data-stu-id="9c300-219">In Visual Studio, open hello solution, and then right-click hello applicable project and select **Update federation metadata**.</span></span> <span data-ttu-id="9c300-220">Se questa opzione non è disponibile, FedUtil o hello WIF v 1.0 SDK non è stato installato.</span><span class="sxs-lookup"><span data-stu-id="9c300-220">If this option is not available, FedUtil and/or hello WIF v1.0 SDK has not been installed.</span></span>
3. <span data-ttu-id="9c300-221">Dal prompt dei comandi hello, selezionare **aggiornamento** toobegin aggiornare i metadati di federazione.</span><span class="sxs-lookup"><span data-stu-id="9c300-221">From hello prompt, select **Update** toobegin updating your federation metadata.</span></span> <span data-ttu-id="9c300-222">Se si dispone di ambiente server di accesso toohello ospita un'applicazione hello, è possibile utilizzare facoltativamente FedUtil [dell'utilità di pianificazione aggiornamento automatico dei metadati](https://msdn.microsoft.com/library/ee517272.aspx).</span><span class="sxs-lookup"><span data-stu-id="9c300-222">If you have access toohello server environment where hello application is hosted, you can optionally use FedUtil’s [automatic metadata update scheduler](https://msdn.microsoft.com/library/ee517272.aspx).</span></span>
4. <span data-ttu-id="9c300-223">Fare clic su **fine** toocomplete processo di aggiornamento hello.</span><span class="sxs-lookup"><span data-stu-id="9c300-223">Click **Finish** toocomplete hello update process.</span></span>

### <span data-ttu-id="9c300-224"><a name="other"></a>Applicazioni Web / API di protezione delle risorse utilizzando qualsiasi altre librerie o implementare manualmente uno di hello protocolli supportati</span><span class="sxs-lookup"><span data-stu-id="9c300-224"><a name="other"></a>Web applications / APIs protecting resources using any other libraries or manually implementing any of hello supported protocols</span></span>
<span data-ttu-id="9c300-225">Se si utilizza qualche altra libreria o implementata manualmente i protocolli supportato hello, dovrai libreria hello tooreview o l'implementazione tooensure che hello chiave viene recuperato dal documento di individuazione OpenID Connect hello o hello documento di metadati di federazione.</span><span class="sxs-lookup"><span data-stu-id="9c300-225">If you are using some other library or manually implemented any of hello supported protocols, you'll need tooreview hello library or your implementation tooensure that hello key is being retrieved from either hello OpenID Connect discovery document or hello federation metadata document.</span></span> <span data-ttu-id="9c300-226">Un modo toocheck per questo è toodo una ricerca nel codice o nel codice della libreria hello per le chiamate di un documento di individuazione OpenID tooeither hello o documento di metadati di federazione hello.</span><span class="sxs-lookup"><span data-stu-id="9c300-226">One way toocheck for this is toodo a search in your code or hello library's code for any calls out tooeither hello OpenID discovery document or hello federation metadata document.</span></span>

<span data-ttu-id="9c300-227">Se la chiave viene archiviato in un punto o hardcoded nell'applicazione, è possibile eseguire manualmente recuperare chiave hello e l'aggiornamento pertanto di eseguire un rollover manuale in base alle istruzioni hello alla fine di hello di questo documento di istruzioni.</span><span class="sxs-lookup"><span data-stu-id="9c300-227">If they key is being stored somewhere or hardcoded in your application, you can manually retrieve hello key and update it accordingly by perform a manual rollover as per hello instructions at hello end of this guidance document.</span></span> <span data-ttu-id="9c300-228">**Migliorare il rollover automatico toosupport di applicazione è vivamente consigliato** utilizzando uno dei hello si avvicina struttura questo interruzioni future tooavoid di articolo e overhead se Azure Active Directory aumenta la frequenza di rollover o ha un emergenza rollover fuori banda.</span><span class="sxs-lookup"><span data-stu-id="9c300-228">**It is strongly encouraged that you enhance your application toosupport automatic rollover** using any of hello approaches outline in this article tooavoid future disruptions and overhead if Azure AD increases it's rollover cadence or has an emergency out-of-band rollover.</span></span>

## <a name="how-tootest-your-application-toodetermine-if-it-will-be-affected"></a><span data-ttu-id="9c300-229">Come tootest toodetermine l'applicazione, se ne risentirà</span><span class="sxs-lookup"><span data-stu-id="9c300-229">How tootest your application toodetermine if it will be affected</span></span>
<span data-ttu-id="9c300-230">È possibile verificare se l'applicazione supporta il rollover automatico della chiave download script hello e seguendo le istruzioni di hello in [questo repository GitHub.](https://github.com/AzureAD/azure-activedirectory-powershell-tokenkey)</span><span class="sxs-lookup"><span data-stu-id="9c300-230">You can validate whether your application supports automatic key rollover by downloading hello scripts and following hello instructions in [this GitHub repository.](https://github.com/AzureAD/azure-activedirectory-powershell-tokenkey)</span></span>

## <a name="how-tooperform-a-manual-rollover-if-you-application-does-not-support-automatic-rollover"></a><span data-ttu-id="9c300-231">Come tooperform un rollover manuale se l'applicazione non supporta il rollover automatico</span><span class="sxs-lookup"><span data-stu-id="9c300-231">How tooperform a manual rollover if you application does not support automatic rollover</span></span>
<span data-ttu-id="9c300-232">Se l'applicazione **non** supporta il rollover automatico, è necessario pertanto tooestablish un processo di firma del periodicamente monitoraggi Azure AD chiavi ed esegue un aggiornamento manuale.</span><span class="sxs-lookup"><span data-stu-id="9c300-232">If your application does **not** support automatic rollover, you will need tooestablish a process that periodically monitors Azure AD's signing keys and performs a manual rollover accordingly.</span></span> <span data-ttu-id="9c300-233">[Questo repository GitHub](https://github.com/AzureAD/azure-activedirectory-powershell-tokenkey) contiene script e istruzioni su come toodo questo.</span><span class="sxs-lookup"><span data-stu-id="9c300-233">[This GitHub repository](https://github.com/AzureAD/azure-activedirectory-powershell-tokenkey) contains scripts and instructions on how toodo this.</span></span>

