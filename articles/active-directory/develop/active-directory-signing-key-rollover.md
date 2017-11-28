---
title: Rollover della chiave di firma in Azure AD | Microsoft Docs
description: Questo articolo illustra le procedure consigliate di rollover della chiave di firma per Azure Active Directory
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
ms.openlocfilehash: 228bb9058537af1e4eb38207c376c2eb86aee68c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="signing-key-rollover-in-azure-active-directory"></a><span data-ttu-id="bdfaf-103">Rollover della chiave di firma in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bdfaf-103">Signing key rollover in Azure Active Directory</span></span>
<span data-ttu-id="bdfaf-104">Questo argomento illustra che cosa è necessario sapere sulle chiavi pubbliche usate per la firma dei token di sicurezza in Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="bdfaf-104">This topic discusses what you need to know about the public keys that are used in Azure Active Directory (Azure AD) to sign security tokens.</span></span> <span data-ttu-id="bdfaf-105">È importante notare che il rollover di queste chiavi viene eseguito periodicamente e in caso di emergenza può essere eseguito immediatamente.</span><span class="sxs-lookup"><span data-stu-id="bdfaf-105">It is important to note that these keys rollover on a periodic basis and, in an emergency, could be rolled over immediately.</span></span> <span data-ttu-id="bdfaf-106">Tutte le applicazioni che usano Azure AD devono poter gestire a livello di codice il processo di rollover della chiave o stabilire un processo di rollover manuale periodico.</span><span class="sxs-lookup"><span data-stu-id="bdfaf-106">All applications that use Azure AD should be able to programmatically handle the key rollover process or establish a periodic manual rollover process.</span></span> <span data-ttu-id="bdfaf-107">Continuare la lettura per comprendere il funzionamento delle chiavi, come valutare l'impatto del rollover nell'applicazione e come aggiornare l'applicazione o stabilire un processo di rollover manuale periodico per gestire il rollover della chiave, se necessario.</span><span class="sxs-lookup"><span data-stu-id="bdfaf-107">Continue reading to understand how the keys work, how to assess the impact of the rollover to your application and how to update your application or establish a periodic manual rollover process to handle key rollover if necessary.</span></span>

## <a name="overview-of-signing-keys-in-azure-ad"></a><span data-ttu-id="bdfaf-108">Informazioni generali sulle chiavi di firma in Azure AD</span><span class="sxs-lookup"><span data-stu-id="bdfaf-108">Overview of signing keys in Azure AD</span></span>
<span data-ttu-id="bdfaf-109">Azure AD usa la crittografia a chiave pubblica basata su standard di settore per stabilire una relazione di trust tra se stesso e le applicazioni che usano Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bdfaf-109">Azure AD uses public-key cryptography built on industry standards to establish trust between itself and the applications that use it.</span></span> <span data-ttu-id="bdfaf-110">In termini pratici, Azure AD usa una chiave di firma costituita da una coppia di chiavi pubbliche e private.</span><span class="sxs-lookup"><span data-stu-id="bdfaf-110">In practical terms, this works in the following way: Azure AD uses a signing key that consists of a public and private key pair.</span></span> <span data-ttu-id="bdfaf-111">Quando un utente accede a un'applicazione che usa Azure AD per l'autenticazione, Azure AD crea un token di sicurezza contenente informazioni sull'utente.</span><span class="sxs-lookup"><span data-stu-id="bdfaf-111">When a user signs in to an application that uses Azure AD for authentication, Azure AD creates a security token that contains information about the user.</span></span> <span data-ttu-id="bdfaf-112">Questo token viene firmato da Azure AD con la chiave privata prima che venga inviato di nuovo all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="bdfaf-112">This token is signed by Azure AD using its private key before it is sent back to the application.</span></span> <span data-ttu-id="bdfaf-113">Per verificare che il token sia valido e sia stato realmente originato da Azure AD, l'applicazione deve convalidare la firma del token usando la chiave pubblica esposta da Azure AD contenuta nel [documento di individuazione di OpenID Connect](http://openid.net/specs/openid-connect-discovery-1_0.html) del tenant o nel [documento dei metadati della federazione](active-directory-federation-metadata.md) SAML/WS-Fed.</span><span class="sxs-lookup"><span data-stu-id="bdfaf-113">To verify that the token is valid and actually originated from Azure AD, the application must validate the token’s signature using the public key exposed by Azure AD that is contained in the tenant’s [OpenID Connect discovery document](http://openid.net/specs/openid-connect-discovery-1_0.html) or SAML/WS-Fed [federation metadata document](active-directory-federation-metadata.md).</span></span>

<span data-ttu-id="bdfaf-114">Per motivi di sicurezza, il rollover della chiave di firma di Azure AD viene eseguito periodicamente e può essere eseguito immediatamente in caso di emergenza.</span><span class="sxs-lookup"><span data-stu-id="bdfaf-114">For security purposes, Azure AD’s signing key rolls on a periodic basis and, in the case of an emergency, could be rolled over immediately.</span></span> <span data-ttu-id="bdfaf-115">Qualsiasi applicazione che si integra con Azure AD deve poter gestire un evento di rollover della chiave indipendentemente dalla frequenza con cui può verificarsi.</span><span class="sxs-lookup"><span data-stu-id="bdfaf-115">Any application that integrates with Azure AD should be prepared to handle a key rollover event no matter how frequently it may occur.</span></span> <span data-ttu-id="bdfaf-116">Se l'applicazione non ha la logica necessaria e prova a usare una chiave scaduta per verificare la firma su un token, la richiesta di accesso avrà esito negativo.</span><span class="sxs-lookup"><span data-stu-id="bdfaf-116">If it doesn’t, and your application attempts to use an expired key to verify the signature on a token, the sign-in request will fail.</span></span>

<span data-ttu-id="bdfaf-117">È sempre disponibile più di una chiave valida nel documento di individuazione di OpenID Connect e nel documento di metadati della federazione.</span><span class="sxs-lookup"><span data-stu-id="bdfaf-117">There is always more than one valid key available in the OpenID Connect discovery document and the federation metadata document.</span></span> <span data-ttu-id="bdfaf-118">L'applicazione deve poter usare qualsiasi chiave specificata nel documento perché di una chiave può essere eseguito il rollover a breve, un'altra può essere quella sostitutiva e così via.</span><span class="sxs-lookup"><span data-stu-id="bdfaf-118">Your application should be prepared to use any of the keys specified in the document, since one key may be rolled soon, another may be its replacement, and so forth.</span></span>

## <a name="how-to-assess-if-your-application-will-be-affected-and-what-to-do-about-it"></a><span data-ttu-id="bdfaf-119">Come valutare se l'applicazione sarà interessata e come intervenire</span><span class="sxs-lookup"><span data-stu-id="bdfaf-119">How to assess if your application will be affected and what to do about it</span></span>
<span data-ttu-id="bdfaf-120">Il modo in cui l'applicazione gestisce il rollover della chiave dipende da variabili come il tipo di applicazione o la libreria e il protocollo di identità usati.</span><span class="sxs-lookup"><span data-stu-id="bdfaf-120">How your application handles key rollover depends on variables such as the type of application or what identity protocol and library was used.</span></span> <span data-ttu-id="bdfaf-121">Le sezioni seguenti valutano se i tipi di applicazioni più comuni sono interessati dal rollover della chiave e offrono indicazioni su come aggiornare l'applicazione per supportare il rollover automatico o aggiornare la chiave manualmente.</span><span class="sxs-lookup"><span data-stu-id="bdfaf-121">The sections below assess whether the most common types of applications are impacted by the key rollover and provide guidance on how to update the application to support automatic rollover or manually update the key.</span></span>

* [<span data-ttu-id="bdfaf-122">Applicazioni client native che accedono alle risorse</span><span class="sxs-lookup"><span data-stu-id="bdfaf-122">Native client applications accessing resources</span></span>](#nativeclient)
* [<span data-ttu-id="bdfaf-123">API / applicazioni Web che accedono alle risorse</span><span class="sxs-lookup"><span data-stu-id="bdfaf-123">Web applications / APIs accessing resources</span></span>](#webclient)
* [<span data-ttu-id="bdfaf-124">API / applicazioni Web che proteggono le risorse e sono state compilate con i servizi app di Azure</span><span class="sxs-lookup"><span data-stu-id="bdfaf-124">Web applications / APIs protecting resources and built using Azure App Services</span></span>](#appservices)
* [<span data-ttu-id="bdfaf-125">API / applicazioni Web che proteggono le risorse usando middleware .NET OWIN OpenID Connect, WS-Fed o WindowsAzureActiveDirectoryBearerAuthentication</span><span class="sxs-lookup"><span data-stu-id="bdfaf-125">Web applications / APIs protecting resources using .NET OWIN OpenID Connect, WS-Fed or WindowsAzureActiveDirectoryBearerAuthentication middleware</span></span>](#owin)
* [<span data-ttu-id="bdfaf-126">API / applicazioni Web che proteggono le risorse usando middleware .NET Core OpenID Connect o JwtBearerAuthentication</span><span class="sxs-lookup"><span data-stu-id="bdfaf-126">Web applications / APIs protecting resources using .NET Core OpenID Connect or  JwtBearerAuthentication middleware</span></span>](#owincore)
* [<span data-ttu-id="bdfaf-127">API / applicazioni Web che proteggono le risorse usando il modulo Node.js passport-azure-ad</span><span class="sxs-lookup"><span data-stu-id="bdfaf-127">Web applications / APIs protecting resources using Node.js passport-azure-ad module</span></span>](#passport)
* [<span data-ttu-id="bdfaf-128">API/applicazioni Web che proteggono le risorse e sono state create con Visual Studio 2015 o Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="bdfaf-128">Web applications / APIs protecting resources and created with Visual Studio 2015 or Visual Studio 2017</span></span>](#vs2015)
* [<span data-ttu-id="bdfaf-129">Applicazioni Web che proteggono le risorse e sono state create con Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="bdfaf-129">Web applications protecting resources and created with Visual Studio 2013</span></span>](#vs2013)
* [<span data-ttu-id="bdfaf-130">API Web che proteggono le risorse e sono state create con Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="bdfaf-130">Web APIs protecting resources and created with Visual Studio 2013</span></span>](#vs2013_webapi)
* [<span data-ttu-id="bdfaf-131">Applicazioni Web che proteggono le risorse e sono state create con Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="bdfaf-131">Web applications protecting resources and created with Visual Studio 2012</span></span>](#vs2012)
* [<span data-ttu-id="bdfaf-132">Applicazioni Web che proteggono le risorse e sono state create con Visual Studio 2010 o 2008 o con Windows Identity Foundation</span><span class="sxs-lookup"><span data-stu-id="bdfaf-132">Web applications protecting resources and created with Visual Studio 2010, 2008 o using Windows Identity Foundation</span></span>](#vs2010)
* [<span data-ttu-id="bdfaf-133">API / applicazioni Web che proteggono le risorse usando qualsiasi altra libreria o con implementazione manuale di qualsiasi protocollo supportato</span><span class="sxs-lookup"><span data-stu-id="bdfaf-133">Web applications / APIs protecting resources using any other libraries or manually implementing any of the supported protocols</span></span>](#other)

<span data-ttu-id="bdfaf-134">Queste indicazioni **non** sono valide per:</span><span class="sxs-lookup"><span data-stu-id="bdfaf-134">This guidance is **not** applicable for:</span></span>

* <span data-ttu-id="bdfaf-135">Applicazioni aggiunte dalla raccolta di applicazioni di Azure AD (incluse quelle personalizzate), che hanno indicazioni separate per la chiave di firma.</span><span class="sxs-lookup"><span data-stu-id="bdfaf-135">Applications added from Azure AD Application Gallery (including Custom) have separate guidance with regards to signing keys.</span></span> [<span data-ttu-id="bdfaf-136">Altre informazioni.</span><span class="sxs-lookup"><span data-stu-id="bdfaf-136">More information.</span></span>](../active-directory-sso-certs.md)
* <span data-ttu-id="bdfaf-137">Applicazioni locali pubblicate tramite il proxy di applicazione, che non prevedono le chiavi di firma.</span><span class="sxs-lookup"><span data-stu-id="bdfaf-137">On-premises applications published via application proxy don't have to worry about signing keys.</span></span>

### <span data-ttu-id="bdfaf-138"><a name="nativeclient"></a>Applicazioni client native che accedono alle risorse</span><span class="sxs-lookup"><span data-stu-id="bdfaf-138"><a name="nativeclient"></a>Native client applications accessing resources</span></span>
<span data-ttu-id="bdfaf-139">Le applicazioni che si limitano ad accedere alle risorse, come</span><span class="sxs-lookup"><span data-stu-id="bdfaf-139">Applications that are only accessing resources (i.e</span></span> <span data-ttu-id="bdfaf-140">Microsoft Graph, l'insieme di credenziali, l'API Outlook e altre API Microsoft, in genere ottengono soltanto un token e lo passano al proprietario della risorsa.</span><span class="sxs-lookup"><span data-stu-id="bdfaf-140">Microsoft Graph, KeyVault, Outlook API and other Microsoft APIs) generally only obtain a token and pass it along to the resource owner.</span></span> <span data-ttu-id="bdfaf-141">Dato che tali applicazioni non proteggono risorse, il token non viene controllato e quindi non è necessario assicurarsi che sia firmato correttamente.</span><span class="sxs-lookup"><span data-stu-id="bdfaf-141">Given that they are not protecting any resources, they do not inspect the token and therefore do not need to ensure it is properly signed.</span></span>

<span data-ttu-id="bdfaf-142">Le applicazioni client native, sia per desktop che per dispositivi mobili, rientrano in questa categoria e quindi non sono interessate dal rollover.</span><span class="sxs-lookup"><span data-stu-id="bdfaf-142">Native client applications, whether desktop or mobile, fall into this category and are thus not impacted by the rollover.</span></span>

### <span data-ttu-id="bdfaf-143"><a name="webclient"></a>API / applicazioni Web che accedono alle risorse</span><span class="sxs-lookup"><span data-stu-id="bdfaf-143"><a name="webclient"></a>Web applications / APIs accessing resources</span></span>
<span data-ttu-id="bdfaf-144">Le applicazioni che si limitano ad accedere alle risorse, come</span><span class="sxs-lookup"><span data-stu-id="bdfaf-144">Applications that are only accessing resources (i.e</span></span> <span data-ttu-id="bdfaf-145">Microsoft Graph, l'insieme di credenziali, l'API Outlook e altre API Microsoft, in genere ottengono soltanto un token e lo passano al proprietario della risorsa.</span><span class="sxs-lookup"><span data-stu-id="bdfaf-145">Microsoft Graph, KeyVault, Outlook API and other Microsoft APIs) generally only obtain a token and pass it along to the resource owner.</span></span> <span data-ttu-id="bdfaf-146">Dato che tali applicazioni non proteggono risorse, il token non viene controllato e quindi non è necessario assicurarsi che sia firmato correttamente.</span><span class="sxs-lookup"><span data-stu-id="bdfaf-146">Given that they are not protecting any resources, they do not inspect the token and therefore do not need to ensure it is properly signed.</span></span>

<span data-ttu-id="bdfaf-147">Le applicazioni Web e le API Web che usano il flusso solo app (credenziali client / certificato client) rientrano in questa categoria e quindi non sono interessate dal rollover.</span><span class="sxs-lookup"><span data-stu-id="bdfaf-147">Web applications and web APIs that are using the app-only flow (client credentials / client certificate), fall into this category and are thus not impacted by the rollover.</span></span>

### <span data-ttu-id="bdfaf-148"><a name="appservices"></a>API / applicazioni Web che proteggono le risorse e sono state compilate con i servizi app di Azure</span><span class="sxs-lookup"><span data-stu-id="bdfaf-148"><a name="appservices"></a>Web applications / APIs protecting resources and built using Azure App Services</span></span>
<span data-ttu-id="bdfaf-149">La funzionalità di autenticazione / autorizzazione (EasyAuth) dei servizi app di Azure ha già la logica necessaria per gestire automaticamente il rollover della chiave.</span><span class="sxs-lookup"><span data-stu-id="bdfaf-149">Azure App Services' Authentication / Authorization (EasyAuth) functionality already has the necessary logic to handle key rollover automatically.</span></span>

### <span data-ttu-id="bdfaf-150"><a name="owin"></a>API / applicazioni Web che proteggono le risorse usando middleware .NET OWIN OpenID Connect, WS-Fed o WindowsAzureActiveDirectoryBearerAuthentication</span><span class="sxs-lookup"><span data-stu-id="bdfaf-150"><a name="owin"></a>Web applications / APIs protecting resources using .NET OWIN OpenID Connect, WS-Fed or WindowsAzureActiveDirectoryBearerAuthentication middleware</span></span>
<span data-ttu-id="bdfaf-151">Se l'applicazione usa middleware .NET OWIN OpenID Connect, WS-Fed o WindowsAzureActiveDirectoryBearerAuthentication, ha già la logica necessaria per gestire automaticamente il rollover della chiave.</span><span class="sxs-lookup"><span data-stu-id="bdfaf-151">If your application is using the .NET OWIN OpenID Connect, WS-Fed or WindowsAzureActiveDirectoryBearerAuthentication middleware, it already has the necessary logic to handle key rollover automatically.</span></span>

<span data-ttu-id="bdfaf-152">È possibile verificare che l'applicazione usi middleware di questo tipo cercando uno dei frammenti seguenti nei file Startup.cs o Startup.Auth.cs dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="bdfaf-152">You can confirm that your application is using any of these by looking for any of the following snippets in your application's Startup.cs or Startup.Auth.cs</span></span>

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

### <span data-ttu-id="bdfaf-153"><a name="owincore"></a>API / applicazioni Web che proteggono le risorse usando middleware .NET Core OpenID Connect o JwtBearerAuthentication</span><span class="sxs-lookup"><span data-stu-id="bdfaf-153"><a name="owincore"></a>Web applications / APIs protecting resources using .NET Core OpenID Connect or  JwtBearerAuthentication middleware</span></span>
<span data-ttu-id="bdfaf-154">Se l'applicazione usa middleware .NET Core OWIN OpenID Connect o JwtBearerAuthentication, ha già la logica necessaria per gestire automaticamente il rollover della chiave.</span><span class="sxs-lookup"><span data-stu-id="bdfaf-154">If your application is using the .NET Core OWIN OpenID Connect  or JwtBearerAuthentication middleware, it already has the necessary logic to handle key rollover automatically.</span></span>

<span data-ttu-id="bdfaf-155">È possibile verificare che l'applicazione usi middleware di questo tipo cercando uno dei frammenti seguenti nei file Startup.cs o Startup.Auth.cs dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="bdfaf-155">You can confirm that your application is using any of these by looking for any of the following snippets in your application's Startup.cs or Startup.Auth.cs</span></span>

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

### <span data-ttu-id="bdfaf-156"><a name="passport"></a>API / applicazioni Web che proteggono le risorse usando il modulo Node.js passport-azure-ad</span><span class="sxs-lookup"><span data-stu-id="bdfaf-156"><a name="passport"></a>Web applications / APIs protecting resources using Node.js passport-azure-ad module</span></span>
<span data-ttu-id="bdfaf-157">Se l'applicazione usa il modulo Node.js passport-ad, ha già la logica necessaria per gestire automaticamente il rollover della chiave.</span><span class="sxs-lookup"><span data-stu-id="bdfaf-157">If your application is using the Node.js passport-ad module, it already has the necessary logic to handle key rollover automatically.</span></span>

<span data-ttu-id="bdfaf-158">È possibile verificare che l'applicazione usi il modulo passport-ad cercando il frammento seguente nel file app.js dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="bdfaf-158">You can confirm that your application passport-ad by searching for the following snippet in your application's app.js</span></span>

```
var OIDCStrategy = require('passport-azure-ad').OIDCStrategy;

passport.use(new OIDCStrategy({
    //...
));
```

### <span data-ttu-id="bdfaf-159"><a name="vs2015"></a>API/applicazioni Web che proteggono le risorse e sono state create con Visual Studio 2015 o Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="bdfaf-159"><a name="vs2015"></a>Web applications / APIs protecting resources and created with Visual Studio 2015 or Visual Studio 2017</span></span>
<span data-ttu-id="bdfaf-160">Se l'applicazione è stata creata usando un modello di applicazione Web in Visual Studio 2015 o Visual Studio 2017 ed è stata selezionata l'opzione **Account aziendali o dell'istituto di istruzione** nel menu **Modifica autenticazione**, l'applicazione ha già la logica necessaria per gestire automaticamente il rollover della chiave.</span><span class="sxs-lookup"><span data-stu-id="bdfaf-160">If your application was built using a web application template in Visual Studio 2015 or Visual Studio 2017 and you selected **Work And School Accounts** from the **Change Authentication** menu, it already has the necessary logic to handle key rollover automatically.</span></span> <span data-ttu-id="bdfaf-161">Questa logica, incorporata nel middleware OWIN OpenID Connect, recupera e memorizza nella cache le chiavi dal documento di individuazione di OpenID Connect e le aggiorna periodicamente.</span><span class="sxs-lookup"><span data-stu-id="bdfaf-161">This logic, embedded in the OWIN OpenID Connect middleware, retrieves and caches the keys from the OpenID Connect discovery document and periodically refreshes them.</span></span>

<span data-ttu-id="bdfaf-162">Se l'autenticazione è stata aggiunta alla soluzione manualmente, l'applicazione potrebbe non avare la logica di rollover della chiave necessaria.</span><span class="sxs-lookup"><span data-stu-id="bdfaf-162">If you added authentication to your solution manually, your application might not have the necessary key rollover logic.</span></span> <span data-ttu-id="bdfaf-163">Sarà necessario scriverla oppure seguire i passaggi illustrati in [API/Applicazioni Web che proteggono le risorse usando qualsiasi altra libreria o con implementazione manuale di qualsiasi protocollo supportato](#other).</span><span class="sxs-lookup"><span data-stu-id="bdfaf-163">You will need to write it yourself, or follow the steps in [Web applications / APIs using any other libraries or manually implementing any of the supported protocols.](#other).</span></span>

### <span data-ttu-id="bdfaf-164"><a name="vs2013"></a>Applicazioni Web che proteggono le risorse e sono state create con Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="bdfaf-164"><a name="vs2013"></a>Web applications protecting resources and created with Visual Studio 2013</span></span>
<span data-ttu-id="bdfaf-165">Se l'applicazione è stata creata usando un modello di applicazione Web in Visual Studio 2013 e sono stati selezionati **account aziendali** dal menu **Modifica autenticazione**, l'applicazione ha già la logica necessaria per gestire automaticamente il rollover della chiave.</span><span class="sxs-lookup"><span data-stu-id="bdfaf-165">If your application was built using a web application template in Visual Studio 2013 and you selected **Organizational Accounts** from the **Change Authentication** menu, it already has the necessary logic to handle key rollover automatically.</span></span> <span data-ttu-id="bdfaf-166">Questa logica archivia l'identificatore univoco dell'organizzazione e informazioni sulla chiave di firma in due tabelle di database associate al progetto.</span><span class="sxs-lookup"><span data-stu-id="bdfaf-166">This logic stores your organization’s unique identifier and the signing key information in two database tables associated with the project.</span></span> <span data-ttu-id="bdfaf-167">La stringa di connessione per il database si trova nel file Web.config del progetto.</span><span class="sxs-lookup"><span data-stu-id="bdfaf-167">You can find the connection string for the database in the project’s Web.config file.</span></span>

<span data-ttu-id="bdfaf-168">Se l'autenticazione è stata aggiunta alla soluzione manualmente, l'applicazione potrebbe non avare la logica di rollover della chiave necessaria.</span><span class="sxs-lookup"><span data-stu-id="bdfaf-168">If you added authentication to your solution manually, your application might not have the necessary key rollover logic.</span></span> <span data-ttu-id="bdfaf-169">Sarà necessario scriverla oppure seguire i passaggi illustrati in [API/Applicazioni Web che proteggono le risorse usando qualsiasi altra libreria o con implementazione manuale di qualsiasi protocollo supportato](#other).</span><span class="sxs-lookup"><span data-stu-id="bdfaf-169">You will need to write it yourself, or follow the steps in [Web applications / APIs using any other libraries or manually implementing any of the supported protocols.](#other).</span></span>

<span data-ttu-id="bdfaf-170">I passaggi seguenti consentono di verificare il corretto funzionamento della logica dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="bdfaf-170">The following steps will help you verify that the logic is working properly in your application.</span></span>

1. <span data-ttu-id="bdfaf-171">In Visual Studio 2013 aprire la soluzione e quindi fare clic sulla scheda **Esplora Server** nella finestra di destra.</span><span class="sxs-lookup"><span data-stu-id="bdfaf-171">In Visual Studio 2013, open the solution, and then click on the **Server Explorer** tab on the right window.</span></span>
2. <span data-ttu-id="bdfaf-172">Espandere **Connessioni dati**, **DefaultConnection** e quindi **Tabelle**.</span><span class="sxs-lookup"><span data-stu-id="bdfaf-172">Expand **Data Connections**, **DefaultConnection**, and then **Tables**.</span></span> <span data-ttu-id="bdfaf-173">Trovare la tabella **IssuingAuthorityKeys**, fare clic con il pulsante destro del mouse e quindi scegliere **Mostra dati tabella**.</span><span class="sxs-lookup"><span data-stu-id="bdfaf-173">Locate the **IssuingAuthorityKeys** table, right-click it, and then click **Show Table Data**.</span></span>
3. <span data-ttu-id="bdfaf-174">Nella tabella **IssuingAuthorityKeys** sarà presente almeno una riga che corrisponde al valore di identificazione personale per la chiave.</span><span class="sxs-lookup"><span data-stu-id="bdfaf-174">In the **IssuingAuthorityKeys** table, there will be at least one row, which corresponds to the thumbprint value for the key.</span></span> <span data-ttu-id="bdfaf-175">Eliminare tutte le righe nella tabella.</span><span class="sxs-lookup"><span data-stu-id="bdfaf-175">Delete any rows in the table.</span></span>
4. <span data-ttu-id="bdfaf-176">Fare clic con il pulsante destro del mouse sulla tabella **Tenant** e quindi scegliere **Mostra dati tabella**.</span><span class="sxs-lookup"><span data-stu-id="bdfaf-176">Right-click the **Tenants** table, and then click **Show Table Data**.</span></span>
5. <span data-ttu-id="bdfaf-177">Nella tabella **Tenant** sarà presente almeno una riga che corrisponde a un identificatore di tenant directory univoco.</span><span class="sxs-lookup"><span data-stu-id="bdfaf-177">In the **Tenants** table, there will be at least one row, which corresponds to a unique directory tenant identifier.</span></span> <span data-ttu-id="bdfaf-178">Eliminare tutte le righe nella tabella.</span><span class="sxs-lookup"><span data-stu-id="bdfaf-178">Delete any rows in the table.</span></span> <span data-ttu-id="bdfaf-179">Se non si eliminano le righe nella tabella **Tenant** e nella tabella **IssuingAuthorityKeys**, si verificherà un errore in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="bdfaf-179">If you don't delete the rows in both the **Tenants** table and **IssuingAuthorityKeys** table, you will get an error at runtime.</span></span>
6. <span data-ttu-id="bdfaf-180">Compilare ed eseguire l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="bdfaf-180">Build and run the application.</span></span> <span data-ttu-id="bdfaf-181">Dopo aver effettuato l'accesso al proprio account sarà possibile arrestare l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="bdfaf-181">After you have logged in to your account, you can stop the application.</span></span>
7. <span data-ttu-id="bdfaf-182">Tornare a **Esplora Server** ed esaminare i valori nelle tabelle **IssuingAuthorityKeys** e **Tenant**.</span><span class="sxs-lookup"><span data-stu-id="bdfaf-182">Return to the **Server Explorer** and look at the values in the **IssuingAuthorityKeys** and **Tenants** table.</span></span> <span data-ttu-id="bdfaf-183">Si noterà che sono stati popolati automaticamente con le informazioni appropriate dal documento di metadati della federazione.</span><span class="sxs-lookup"><span data-stu-id="bdfaf-183">You’ll notice that they have been automatically repopulated with the appropriate information from the federation metadata document.</span></span>

### <span data-ttu-id="bdfaf-184"><a name="vs2013"></a>API Web che proteggono le risorse e sono state create con Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="bdfaf-184"><a name="vs2013"></a>Web APIs protecting resources and created with Visual Studio 2013</span></span>
<span data-ttu-id="bdfaf-185">Se è stata creata un'applicazione API Web in Visual Studio 2013 usando il modello API Web e sono stati selezionati **account aziendali** dal menu **Modifica autenticazione**, l'applicazione ha già la logica necessaria.</span><span class="sxs-lookup"><span data-stu-id="bdfaf-185">If you created a web API application in Visual Studio 2013 using the Web API template, and then selected **Organizational Accounts** from the **Change Authentication** menu, you already have the necessary logic in your application.</span></span>

<span data-ttu-id="bdfaf-186">Se l'autenticazione è stata configurata manualmente, seguire queste istruzioni per informazioni su come configurare l'API Web per aggiornare automaticamente le informazioni sulle chiavi.</span><span class="sxs-lookup"><span data-stu-id="bdfaf-186">If you manually configured authentication, follow the instructions below to learn how to configure your Web API to automatically update its key information.</span></span>

<span data-ttu-id="bdfaf-187">Il frammento di codice seguente illustra come ottenere le chiavi più recenti dal documento di metadati della federazione e quindi usare il [gestore dei token JWT](https://msdn.microsoft.com/library/dn205065.aspx) per convalidare il token.</span><span class="sxs-lookup"><span data-stu-id="bdfaf-187">The following code snippet demonstrates how to get the latest keys from the federation metadata document, and then use the [JWT Token Handler](https://msdn.microsoft.com/library/dn205065.aspx) to validate the token.</span></span> <span data-ttu-id="bdfaf-188">Il frammento di codice presuppone che si userà il proprio meccanismo di memorizzazione nella cache per mantenere la chiave per la convalida dei futuri token di Azure AD, che si trovino in un database, in un file di configurazione o altrove.</span><span class="sxs-lookup"><span data-stu-id="bdfaf-188">The code snippet assumes that you will use your own caching mechanism for persisting the key to validate future tokens from Azure AD, whether it be in a database, configuration file, or elsewhere.</span></span>

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

        // Validates the JWT Token that's part of the Authorization header in an HTTP request.
        public void ValidateJwtToken(string token)
        {
            JwtSecurityTokenHandler tokenHandler = new JwtSecurityTokenHandler()
            {
                // Do not disable for production code
                CertificateValidator = X509CertificateValidator.None
            };

            TokenValidationParameters validationParams = new TokenValidationParameters()
            {
                AllowedAudience = "[Your App ID URI goes here, as registered in the Azure Classic Portal]",
                ValidIssuer = "[The issuer for the token goes here, such as https://sts.windows.net/68b98905-130e-4d7c-b6e1-a158a9ed8449/]",
                SigningTokens = GetSigningCertificates(MetadataAddress)

                // Cache the signing tokens by your desired mechanism
            };

            Thread.CurrentPrincipal = tokenHandler.ValidateToken(token, validationParams);
        }

        // Returns a list of certificates from the specified metadata document.
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
                        throw new InvalidOperationException("There is no RoleDescriptor of type SecurityTokenServiceType in the metadata");
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

### <span data-ttu-id="bdfaf-189"><a name="vs2012"></a>Applicazioni Web che proteggono le risorse e sono state create con Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="bdfaf-189"><a name="vs2012"></a>Web applications protecting resources and created with Visual Studio 2012</span></span>
<span data-ttu-id="bdfaf-190">Se l'applicazione è stata creata in Visual Studio 2012 è stato probabilmente usato lo strumento Identità e accesso per configurare l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="bdfaf-190">If your application was built in Visual Studio 2012, you probably used the Identity and Access Tool to configure your application.</span></span> <span data-ttu-id="bdfaf-191">È anche probabile che si usi [Validating Issuer Name Registry (VINR)](https://msdn.microsoft.com/library/dn205067.aspx).</span><span class="sxs-lookup"><span data-stu-id="bdfaf-191">It’s also likely that you are using the [Validating Issuer Name Registry (VINR)](https://msdn.microsoft.com/library/dn205067.aspx).</span></span> <span data-ttu-id="bdfaf-192">VINR gestisce le informazioni sui provider di identità attendibili (Azure AD) e le chiavi usate per convalidare i token rilasciati dai provider.</span><span class="sxs-lookup"><span data-stu-id="bdfaf-192">The VINR is responsible for maintaining information about trusted identity providers (Azure AD) and the keys used to validate tokens issued by them.</span></span> <span data-ttu-id="bdfaf-193">VINR semplifica anche l'aggiornamento automatico delle informazioni sulla chiave archiviate in un file Web.config, scaricando il documento di metadati della federazione più recente associato alla directory, verificando se la configurazione è aggiornata con il documento più recente e aggiornando l'applicazione per l'uso della nuova chiave se necessario.</span><span class="sxs-lookup"><span data-stu-id="bdfaf-193">The VINR also makes it easy to automatically update the key information stored in a Web.config file by downloading the latest federation metadata document associated with your directory, checking if the configuration is out of date with the latest document, and updating the application to use the new key as necessary.</span></span>

<span data-ttu-id="bdfaf-194">Se l'applicazione è stata creata usando uno degli esempi di codice o le procedure dettagliate offerte da Microsoft, la logica di rollover della chiave è già inclusa nel progetto.</span><span class="sxs-lookup"><span data-stu-id="bdfaf-194">If you created your application using any of the code samples or walkthrough documentation provided by Microsoft, the key rollover logic is already included in your project.</span></span> <span data-ttu-id="bdfaf-195">Si noterà che il codice seguente esiste già nel progetto.</span><span class="sxs-lookup"><span data-stu-id="bdfaf-195">You will notice that the code below already exists in your project.</span></span> <span data-ttu-id="bdfaf-196">Se l'applicazione non ha questa logica, seguire questa procedura per aggiungerla e verificarne il corretto funzionamento.</span><span class="sxs-lookup"><span data-stu-id="bdfaf-196">If your application does not already have this logic, follow the steps below to add it and to verify that it’s working correctly.</span></span>

1. <span data-ttu-id="bdfaf-197">In **Esplora soluzioni** aggiungere un riferimento all'assembly **System.IdentityModel** per il progetto appropriato.</span><span class="sxs-lookup"><span data-stu-id="bdfaf-197">In **Solution Explorer**, add a reference to the **System.IdentityModel** assembly for the appropriate project.</span></span>
2. <span data-ttu-id="bdfaf-198">Aprire il file **Global.asax.cs** e aggiungere le direttive using seguenti:</span><span class="sxs-lookup"><span data-stu-id="bdfaf-198">Open the **Global.asax.cs** file and add the following using directives:</span></span>
   ```
   using System.Configuration;
   using System.IdentityModel.Tokens;
   ```
3. <span data-ttu-id="bdfaf-199">Aggiungere il metodo seguente al file **Global.asax.cs** :</span><span class="sxs-lookup"><span data-stu-id="bdfaf-199">Add the following method to the **Global.asax.cs** file:</span></span>
   ```
   protected void RefreshValidationSettings()
   {
    string configPath = AppDomain.CurrentDomain.BaseDirectory + "\\" + "Web.config";
    string metadataAddress =
                  ConfigurationManager.AppSettings["ida:FederationMetadataLocation"];
    ValidatingIssuerNameRegistry.WriteToConfig(metadataAddress, configPath);
   }
   ```
4. <span data-ttu-id="bdfaf-200">Richiamare il metodo **RefreshValidationSettings()** nel metodo **Application_Start()** in **Global.asax.cs** come illustrato:</span><span class="sxs-lookup"><span data-stu-id="bdfaf-200">Invoke the **RefreshValidationSettings()** method in the **Application_Start()** method in **Global.asax.cs** as shown:</span></span>
   ```
   protected void Application_Start()
   {
    AreaRegistration.RegisterAllAreas();
    ...
    RefreshValidationSettings();
   }
   ```

<span data-ttu-id="bdfaf-201">Dopo aver eseguito questi passaggi, il file Web.config dell'applicazione verrà aggiornato con le informazioni più recenti del documento di metadati della federazione, incluse le chiavi più recenti.</span><span class="sxs-lookup"><span data-stu-id="bdfaf-201">Once you have followed these steps, your application’s Web.config will be updated with the latest information from the federation metadata document, including the latest keys.</span></span> <span data-ttu-id="bdfaf-202">Questo aggiornamento verrà eseguito ogni volta che il pool di applicazioni viene riciclato in IIS. Per impostazione predefinita, IIS è impostato per il riciclo delle applicazioni ogni 29 ore.</span><span class="sxs-lookup"><span data-stu-id="bdfaf-202">This update will occur every time your application pool recycles in IIS; by default IIS is set to recycle applications every 29 hours.</span></span>

<span data-ttu-id="bdfaf-203">Seguire questa procedura per verificare che la logica di rollover della chiave funzioni.</span><span class="sxs-lookup"><span data-stu-id="bdfaf-203">Follow the steps below to verify that the key rollover logic is working.</span></span>

1. <span data-ttu-id="bdfaf-204">Dopo aver verificato che l'applicazione usi il codice indicato in precedenza, aprire il file **Web.config** e passare al blocco **<issuerNameRegistry>**, verificando in particolare le righe seguenti:</span><span class="sxs-lookup"><span data-stu-id="bdfaf-204">After you have verified that your application is using the code above, open the **Web.config** file and navigate to the **<issuerNameRegistry>** block, specifically looking for the following few lines:</span></span>
   ```
   <issuerNameRegistry type="System.IdentityModel.Tokens.ValidatingIssuerNameRegistry, System.IdentityModel.Tokens.ValidatingIssuerNameRegistry">
        <authority name="https://sts.windows.net/ec4187af-07da-4f01-b18f-64c2f5abecea/">
          <keys>
            <add thumbprint="3A38FA984E8560F19AADC9F86FE9594BB6AD049B" />
          </keys>
   ```
2. <span data-ttu-id="bdfaf-205">Nella tabella **<add thumbprint=””>** modificare il valore di identificazione personale sostituendo un carattere con uno diverso.</span><span class="sxs-lookup"><span data-stu-id="bdfaf-205">In the **<add thumbprint=””>** setting, change the thumbprint value by replacing any character with a different one.</span></span> <span data-ttu-id="bdfaf-206">Salvare il file **Web.config** .</span><span class="sxs-lookup"><span data-stu-id="bdfaf-206">Save the **Web.config** file.</span></span>
3. <span data-ttu-id="bdfaf-207">Compilare l'applicazione ed eseguirla.</span><span class="sxs-lookup"><span data-stu-id="bdfaf-207">Build the application, and then run it.</span></span> <span data-ttu-id="bdfaf-208">Se è possibile completare il processo di accesso, l'applicazione aggiorna in modo corretto la chiave scaricando le informazioni necessarie dal documento di metadati della federazione della directory.</span><span class="sxs-lookup"><span data-stu-id="bdfaf-208">If you can complete the sign-in process, your application is successfully updating the key by downloading the required information from your directory’s federation metadata document.</span></span> <span data-ttu-id="bdfaf-209">In caso di problemi di accesso verificare che le modifiche nell'applicazione siano corrette leggendo l'argomento [Adding Sign-On to Your Web Application Using Azure AD](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect) (Aggiunta del processo di accesso nell'applicazione Web tramite Azure AD) oppure scaricando ed esaminando l'esempio di codice seguente: [Multi-Tenant Cloud Application for Azure Active Directory](https://code.msdn.microsoft.com/multi-tenant-cloud-8015b84b) (Applicazione cloud multi-tenant per Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="bdfaf-209">If you are having issues signing in, ensure the changes in your application are correct by reading the [Adding Sign-On to Your Web Application Using Azure AD](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect) topic, or downloading and inspecting the following code sample: [Multi-Tenant Cloud Application for Azure Active Directory](https://code.msdn.microsoft.com/multi-tenant-cloud-8015b84b).</span></span>

### <span data-ttu-id="bdfaf-210"><a name="vs2010"></a>Applicazioni Web che proteggono le risorse e sono state create con Visual Studio 2008 o 2010 o con Windows Identity Foundation (WIF) v1.0 per .NET 3.5</span><span class="sxs-lookup"><span data-stu-id="bdfaf-210"><a name="vs2010"></a>Web applications protecting resources and created with Visual Studio 2008 or 2010 and Windows Identity Foundation (WIF) v1.0 for .NET 3.5</span></span>
<span data-ttu-id="bdfaf-211">Se è stata compilata un'applicazione in WIF v1.0 non esistono meccanismi per aggiornare automaticamente la configurazione dell'applicazione per l'uso di una nuova chiave.</span><span class="sxs-lookup"><span data-stu-id="bdfaf-211">If you built an application on WIF v1.0, there is no provided mechanism to automatically refresh your application’s configuration to use a new key.</span></span>

* <span data-ttu-id="bdfaf-212">*Modo più semplice* : usare lo strumento FedUtil incluso in WIF SDK, che può recuperare il documento di metadati più recente e aggiornare la configurazione.</span><span class="sxs-lookup"><span data-stu-id="bdfaf-212">*Easiest way* Use the FedUtil tooling included in the WIF SDK, which can retrieve the latest metadata document and update your configuration.</span></span>
* <span data-ttu-id="bdfaf-213">Aggiornare l'applicazione a .NET 4.5, che include la versione più recente di WIF nello spazio dei nomi System.</span><span class="sxs-lookup"><span data-stu-id="bdfaf-213">Update your application to .NET 4.5, which includes the newest version of WIF located in the System namespace.</span></span> <span data-ttu-id="bdfaf-214">Sarà quindi possibile usare [Validating Issuer Name Registry (VINR)](https://msdn.microsoft.com/library/dn205067.aspx) per eseguire gli aggiornamenti automatici della configurazione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="bdfaf-214">You can then use the [Validating Issuer Name Registry (VINR)](https://msdn.microsoft.com/library/dn205067.aspx) to perform automatic updates of the application’s configuration.</span></span>
* <span data-ttu-id="bdfaf-215">Eseguire un rollover manuale seguendo le istruzioni alla fine di questo documento.</span><span class="sxs-lookup"><span data-stu-id="bdfaf-215">Perform a manual rollover as per the instructions at the end of this guidance document.</span></span>

<span data-ttu-id="bdfaf-216">Istruzioni per usare FedUtil per aggiornare la configurazione:</span><span class="sxs-lookup"><span data-stu-id="bdfaf-216">Instructions to use the FedUtil to update your configuration:</span></span>

1. <span data-ttu-id="bdfaf-217">Verificare di avere l'SDK WIF v1.0 installato nel computer di sviluppo per Visual Studio 2008 o 2010.</span><span class="sxs-lookup"><span data-stu-id="bdfaf-217">Verify that you have the WIF v1.0 SDK installed on your development machine for Visual Studio 2008 or 2010.</span></span> <span data-ttu-id="bdfaf-218">È possibile [scaricarlo da qui](https://www.microsoft.com/en-us/download/details.aspx?id=4451) se non è ancora installato.</span><span class="sxs-lookup"><span data-stu-id="bdfaf-218">You can [download it from here](https://www.microsoft.com/en-us/download/details.aspx?id=4451) if you have not yet installed it.</span></span>
2. <span data-ttu-id="bdfaf-219">In Visual Studio aprire la soluzione, quindi fare clic con il pulsante destro del mouse sul progetto applicabile e scegliere **Update federation metadata**(Aggiorna metadati federazione).</span><span class="sxs-lookup"><span data-stu-id="bdfaf-219">In Visual Studio, open the solution, and then right-click the applicable project and select **Update federation metadata**.</span></span> <span data-ttu-id="bdfaf-220">Se questa opzione non è disponibile, FedUtil o l'SDK WIF v1.0 non è stato installato.</span><span class="sxs-lookup"><span data-stu-id="bdfaf-220">If this option is not available, FedUtil and/or the WIF v1.0 SDK has not been installed.</span></span>
3. <span data-ttu-id="bdfaf-221">Al prompt selezionare **Aggiorna** per iniziare l'aggiornamento dei metadati della federazione.</span><span class="sxs-lookup"><span data-stu-id="bdfaf-221">From the prompt, select **Update** to begin updating your federation metadata.</span></span> <span data-ttu-id="bdfaf-222">Se si ha accesso all'ambiente server in cui è ospitata l'applicazione, è possibile usare facoltativamente l' [utilità di pianificazione dell'aggiornamento automatico dei metadati](https://msdn.microsoft.com/library/ee517272.aspx)di FedUtil.</span><span class="sxs-lookup"><span data-stu-id="bdfaf-222">If you have access to the server environment where the application is hosted, you can optionally use FedUtil’s [automatic metadata update scheduler](https://msdn.microsoft.com/library/ee517272.aspx).</span></span>
4. <span data-ttu-id="bdfaf-223">Fare clic su **Fine** per completare il processo di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="bdfaf-223">Click **Finish** to complete the update process.</span></span>

### <span data-ttu-id="bdfaf-224"><a name="other"></a>API / applicazioni Web che proteggono le risorse usando qualsiasi altra libreria o con implementazione manuale di qualsiasi protocollo supportato</span><span class="sxs-lookup"><span data-stu-id="bdfaf-224"><a name="other"></a>Web applications / APIs protecting resources using any other libraries or manually implementing any of the supported protocols</span></span>
<span data-ttu-id="bdfaf-225">Se si usano altre librerie o si implementa manualmente qualsiasi protocollo supportato, sarà necessario esaminare la libreria o l'implementazione per verificare che la chiave venga recuperata dal documento di individuazione di OpenID Connect o dal documento di metadati della federazione.</span><span class="sxs-lookup"><span data-stu-id="bdfaf-225">If you are using some other library or manually implemented any of the supported protocols, you'll need to review the library or your implementation to ensure that the key is being retrieved from either the OpenID Connect discovery document or the federation metadata document.</span></span> <span data-ttu-id="bdfaf-226">Un modo per eseguire la verifica è cercare nel codice o nel codice della libreria chiamate al documento di individuazione di OpenID o al documento di metadati della federazione.</span><span class="sxs-lookup"><span data-stu-id="bdfaf-226">One way to check for this is to do a search in your code or the library's code for any calls out to either the OpenID discovery document or the federation metadata document.</span></span>

<span data-ttu-id="bdfaf-227">Se la chiave è archiviata in una posizione qualsiasi o è hardcoded nell'applicazione, è possibile recuperarla manualmente e aggiornarla di conseguenza eseguendo un rollover manuale in base alle istruzioni disponibili alla fine di questo documento.</span><span class="sxs-lookup"><span data-stu-id="bdfaf-227">If they key is being stored somewhere or hardcoded in your application, you can manually retrieve the key and update it accordingly by perform a manual rollover as per the instructions at the end of this guidance document.</span></span> <span data-ttu-id="bdfaf-228">**È vivamente consigliato ottimizzare l'applicazione per il supporto del rollover automatico** usando uno degli approcci descritti in questo articolo per evitare interruzioni future e sovraccarichi se Azure AD aumenta la cadenza di rollover o esegue un rollover di emergenza fuori programma.</span><span class="sxs-lookup"><span data-stu-id="bdfaf-228">**It is strongly encouraged that you enhance your application to support automatic rollover** using any of the approaches outline in this article to avoid future disruptions and overhead if Azure AD increases it's rollover cadence or has an emergency out-of-band rollover.</span></span>

## <a name="how-to-test-your-application-to-determine-if-it-will-be-affected"></a><span data-ttu-id="bdfaf-229">Come testare l'applicazione per stabilire se sarà interessata</span><span class="sxs-lookup"><span data-stu-id="bdfaf-229">How to test your application to determine if it will be affected</span></span>
<span data-ttu-id="bdfaf-230">È possibile verificare se l'applicazione supporta il rollover automatico della chiave scaricando gli script e seguendo le istruzioni contenute in [questo repository GitHub](https://github.com/AzureAD/azure-activedirectory-powershell-tokenkey)</span><span class="sxs-lookup"><span data-stu-id="bdfaf-230">You can validate whether your application supports automatic key rollover by downloading the scripts and following the instructions in [this GitHub repository.](https://github.com/AzureAD/azure-activedirectory-powershell-tokenkey)</span></span>

## <a name="how-to-perform-a-manual-rollover-if-you-application-does-not-support-automatic-rollover"></a><span data-ttu-id="bdfaf-231">Come eseguire un rollover manuale se l'applicazione non supporta il rollover automatico</span><span class="sxs-lookup"><span data-stu-id="bdfaf-231">How to perform a manual rollover if you application does not support automatic rollover</span></span>
<span data-ttu-id="bdfaf-232">Se l'applicazione **non** supporta il rollover automatico, sarà necessario stabilire un processo che monitori periodicamente le chiavi di firma di Azure AD ed esegua un rollover manuale di conseguenza.</span><span class="sxs-lookup"><span data-stu-id="bdfaf-232">If your application does **not** support automatic rollover, you will need to establish a process that periodically monitors Azure AD's signing keys and performs a manual rollover accordingly.</span></span> <span data-ttu-id="bdfaf-233">[Questo repository GitHub](https://github.com/AzureAD/azure-activedirectory-powershell-tokenkey) contiene gli script e le istruzioni necessarie.</span><span class="sxs-lookup"><span data-stu-id="bdfaf-233">[This GitHub repository](https://github.com/AzureAD/azure-activedirectory-powershell-tokenkey) contains scripts and instructions on how to do this.</span></span>

