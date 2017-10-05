---
title: 'Gestione della sessione: Microsoft Threat Modeling Tool - Azure | Microsoft Docs'
description: Procedure di mitigazione delle minacce esposte in Threat Modeling Tool
services: security
documentationcenter: na
author: RodSan
manager: RodSan
editor: RodSan
ms.assetid: na
ms.service: security
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: rodsan
ms.openlocfilehash: 56471d8ef68eacacb3ecebad5056d7e7a9f3ca40
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="security-frame-session-management--articles"></a><span data-ttu-id="9584b-103">Infrastruttura di sicurezza: gestione della sessione - Articoli</span><span class="sxs-lookup"><span data-stu-id="9584b-103">Security Frame: Session Management | Articles</span></span> 
| <span data-ttu-id="9584b-104">Prodotto o servizio</span><span class="sxs-lookup"><span data-stu-id="9584b-104">Product/Service</span></span> | <span data-ttu-id="9584b-105">Articolo</span><span class="sxs-lookup"><span data-stu-id="9584b-105">Article</span></span> |
| --------------- | ------- |
| <span data-ttu-id="9584b-106">**Azure AD**</span><span class="sxs-lookup"><span data-stu-id="9584b-106">**Azure AD**</span></span>    | <ul><li>[<span data-ttu-id="9584b-107">Implementare la disconnessione appropriata con i metodi ADAL quando si usa Azure AD</span><span class="sxs-lookup"><span data-stu-id="9584b-107">Implement proper logout using ADAL methods when using Azure AD</span></span>](#logout-adal)</li></ul> |
| <span data-ttu-id="9584b-108">Dispositivo IoT</span><span class="sxs-lookup"><span data-stu-id="9584b-108">IoT Device</span></span> | <ul><li>[<span data-ttu-id="9584b-109">Usare durate limitate per i token di firma di accesso condiviso generati</span><span class="sxs-lookup"><span data-stu-id="9584b-109">Use finite lifetimes for generated SaS tokens</span></span>](#finite-tokens)</li></ul> |
| <span data-ttu-id="9584b-110">**Azure Document DB**</span><span class="sxs-lookup"><span data-stu-id="9584b-110">**Azure Document DB**</span></span> | <ul><li>[<span data-ttu-id="9584b-111">Usare durate minime per i token delle risorse generati</span><span class="sxs-lookup"><span data-stu-id="9584b-111">Use minimum token lifetimes for generated Resource tokens</span></span>](#resource-tokens)</li></ul> |
| <span data-ttu-id="9584b-112">**AD FS**</span><span class="sxs-lookup"><span data-stu-id="9584b-112">**ADFS**</span></span> | <ul><li>[<span data-ttu-id="9584b-113">Implementare la disconnessione appropriata con i metodi WsFederation quando si usa AD FS</span><span class="sxs-lookup"><span data-stu-id="9584b-113">Implement proper logout using WsFederation methods when using ADFS</span></span>](#wsfederation-logout)</li></ul> |
| <span data-ttu-id="9584b-114">**Identity Server**</span><span class="sxs-lookup"><span data-stu-id="9584b-114">**Identity Server**</span></span> | <ul><li>[<span data-ttu-id="9584b-115">Implementare la disconnessione appropriata quando si usa Identity Server</span><span class="sxs-lookup"><span data-stu-id="9584b-115">Implement proper logout when using Identity Server</span></span>](#proper-logout)</li></ul> |
| <span data-ttu-id="9584b-116">**Applicazione Web**</span><span class="sxs-lookup"><span data-stu-id="9584b-116">**Web Application**</span></span> | <ul><li>[<span data-ttu-id="9584b-117">Le applicazioni disponibili tramite HTTPS devono usare cookie sicuri</span><span class="sxs-lookup"><span data-stu-id="9584b-117">Applications available over HTTPS must use secure cookies</span></span>](#https-secure-cookies)</li><li>[<span data-ttu-id="9584b-118">Tutte le applicazioni basate su http devono specificare solo http per la definizione dei cookie</span><span class="sxs-lookup"><span data-stu-id="9584b-118">All http based application should specify http only for cookie definition</span></span>](#cookie-definition)</li><li>[<span data-ttu-id="9584b-119">Mitigare il rischio di attacchi basati su richieste intersito false nelle pagine Web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="9584b-119">Mitigate against Cross-Site Request Forgery (CSRF) attacks on ASP.NET web pages</span></span>](#csrf-asp)</li><li>[<span data-ttu-id="9584b-120">Configurare una sessione per la durata dell'inattività</span><span class="sxs-lookup"><span data-stu-id="9584b-120">Set up session for inactivity lifetime</span></span>](#inactivity-lifetime)</li><li>[<span data-ttu-id="9584b-121">Implementare la disconnessione appropriata dall'applicazione</span><span class="sxs-lookup"><span data-stu-id="9584b-121">Implement proper logout from the application</span></span>](#proper-app-logout)</li></ul> |
| <span data-ttu-id="9584b-122">**API Web**</span><span class="sxs-lookup"><span data-stu-id="9584b-122">**Web API**</span></span> | <ul><li>[<span data-ttu-id="9584b-123">Mitigare il rischio di attacchi basati su richieste intersito false nelle API Web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="9584b-123">Mitigate against Cross-Site Request Forgery (CSRF) attacks on ASP.NET Web APIs</span></span>](#csrf-api)</li></ul> |

## <span data-ttu-id="9584b-124"><a id="logout-adal"></a>Implementare la disconnessione appropriata con i metodi ADAL quando si usa Azure AD</span><span class="sxs-lookup"><span data-stu-id="9584b-124"><a id="logout-adal"></a>Implement proper logout using ADAL methods when using Azure AD</span></span>

| <span data-ttu-id="9584b-125">Titolo</span><span class="sxs-lookup"><span data-stu-id="9584b-125">Title</span></span>                   | <span data-ttu-id="9584b-126">Dettagli</span><span class="sxs-lookup"><span data-stu-id="9584b-126">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="9584b-127">**Componente**</span><span class="sxs-lookup"><span data-stu-id="9584b-127">**Component**</span></span>               | <span data-ttu-id="9584b-128">Azure AD</span><span class="sxs-lookup"><span data-stu-id="9584b-128">Azure AD</span></span> | 
| <span data-ttu-id="9584b-129">**Fase SDL**</span><span class="sxs-lookup"><span data-stu-id="9584b-129">**SDL Phase**</span></span>               | <span data-ttu-id="9584b-130">Compilare</span><span class="sxs-lookup"><span data-stu-id="9584b-130">Build</span></span> |  
| <span data-ttu-id="9584b-131">**Tecnologie applicabili**</span><span class="sxs-lookup"><span data-stu-id="9584b-131">**Applicable Technologies**</span></span> | <span data-ttu-id="9584b-132">Generico</span><span class="sxs-lookup"><span data-stu-id="9584b-132">Generic</span></span> |
| <span data-ttu-id="9584b-133">**Attributes (Attributi) (Attributi)**</span><span class="sxs-lookup"><span data-stu-id="9584b-133">**Attributes**</span></span>              | <span data-ttu-id="9584b-134">N/D</span><span class="sxs-lookup"><span data-stu-id="9584b-134">N/A</span></span>  |
| <span data-ttu-id="9584b-135">**Riferimenti**</span><span class="sxs-lookup"><span data-stu-id="9584b-135">**References**</span></span>              | <span data-ttu-id="9584b-136">N/D</span><span class="sxs-lookup"><span data-stu-id="9584b-136">N/A</span></span>  |
| <span data-ttu-id="9584b-137">**Passaggi**</span><span class="sxs-lookup"><span data-stu-id="9584b-137">**Steps**</span></span> | <span data-ttu-id="9584b-138">Se l'applicazione si basa su un token di accesso rilasciato da Azure AD, il gestore eventi di disconnessione eseguirà la chiamata.</span><span class="sxs-lookup"><span data-stu-id="9584b-138">If the application relies on access token issued by Azure AD, the logout event handler should call</span></span> |

### <a name="example"></a><span data-ttu-id="9584b-139">Esempio</span><span class="sxs-lookup"><span data-stu-id="9584b-139">Example</span></span>
```C#
HttpContext.GetOwinContext().Authentication.SignOut(OpenIdConnectAuthenticationDefaults.AuthenticationType, CookieAuthenticationDefaults.AuthenticationType)
```

### <a name="example"></a><span data-ttu-id="9584b-140">Esempio</span><span class="sxs-lookup"><span data-stu-id="9584b-140">Example</span></span>
<span data-ttu-id="9584b-141">Eliminerà anche definitivamente la sessione dell'utente chiamando il metodo Session.Abandon().</span><span class="sxs-lookup"><span data-stu-id="9584b-141">It should also destroy user's session by calling Session.Abandon() method.</span></span> <span data-ttu-id="9584b-142">Il metodo seguente illustra l'implementazione sicura della disconnessione utente:</span><span class="sxs-lookup"><span data-stu-id="9584b-142">Following method shows secure implementation of user logout:</span></span>
```C#
    [HttpPost]
        [ValidateAntiForgeryToken]
        public void LogOff()
        {
            string userObjectID = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/objectidentifier").Value;
            AuthenticationContext authContext = new AuthenticationContext(Authority + TenantId, new NaiveSessionCache(userObjectID));
            authContext.TokenCache.Clear();
            Session.Clear();
            Session.Abandon();
            Response.SetCookie(new HttpCookie("ASP.NET_SessionId", string.Empty));
            HttpContext.GetOwinContext().Authentication.SignOut(
                OpenIdConnectAuthenticationDefaults.AuthenticationType,
                CookieAuthenticationDefaults.AuthenticationType);
        } 
```

## <span data-ttu-id="9584b-143"><a id="finite-tokens"></a>Usare durate limitate per i token di firma di accesso condiviso generati</span><span class="sxs-lookup"><span data-stu-id="9584b-143"><a id="finite-tokens"></a>Use finite lifetimes for generated SaS tokens</span></span>

| <span data-ttu-id="9584b-144">Titolo</span><span class="sxs-lookup"><span data-stu-id="9584b-144">Title</span></span>                   | <span data-ttu-id="9584b-145">Dettagli</span><span class="sxs-lookup"><span data-stu-id="9584b-145">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="9584b-146">**Componente**</span><span class="sxs-lookup"><span data-stu-id="9584b-146">**Component**</span></span>               | <span data-ttu-id="9584b-147">Dispositivo IoT</span><span class="sxs-lookup"><span data-stu-id="9584b-147">IoT Device</span></span> | 
| <span data-ttu-id="9584b-148">**Fase SDL**</span><span class="sxs-lookup"><span data-stu-id="9584b-148">**SDL Phase**</span></span>               | <span data-ttu-id="9584b-149">Compilare</span><span class="sxs-lookup"><span data-stu-id="9584b-149">Build</span></span> |  
| <span data-ttu-id="9584b-150">**Tecnologie applicabili**</span><span class="sxs-lookup"><span data-stu-id="9584b-150">**Applicable Technologies**</span></span> | <span data-ttu-id="9584b-151">Generico</span><span class="sxs-lookup"><span data-stu-id="9584b-151">Generic</span></span> |
| <span data-ttu-id="9584b-152">**Attributes (Attributi) (Attributi)**</span><span class="sxs-lookup"><span data-stu-id="9584b-152">**Attributes**</span></span>              | <span data-ttu-id="9584b-153">N/D</span><span class="sxs-lookup"><span data-stu-id="9584b-153">N/A</span></span>  |
| <span data-ttu-id="9584b-154">**Riferimenti**</span><span class="sxs-lookup"><span data-stu-id="9584b-154">**References**</span></span>              | <span data-ttu-id="9584b-155">N/D</span><span class="sxs-lookup"><span data-stu-id="9584b-155">N/A</span></span>  |
| <span data-ttu-id="9584b-156">**Passaggi**</span><span class="sxs-lookup"><span data-stu-id="9584b-156">**Steps**</span></span> | <span data-ttu-id="9584b-157">I token di firma di accesso condiviso generati per l'autenticazione all'hub IoT di Azure devono avere un periodo di validità limitato.</span><span class="sxs-lookup"><span data-stu-id="9584b-157">SaS tokens generated for authenticating to Azure IoT Hub should have a finite expiry period.</span></span> <span data-ttu-id="9584b-158">Impostare durate minime per i token di firma di accesso condiviso per limitare il periodo di tempo in cui i token possono essere riprodotti nel caso in cui vengano compromessi.</span><span class="sxs-lookup"><span data-stu-id="9584b-158">Keep the SaS token lifetimes to a minimum to limit the amount of time they can be replayed in case the tokens are compromised.</span></span>|

## <span data-ttu-id="9584b-159"><a id="resource-tokens"></a>Usare durate minime per i token delle risorse generati</span><span class="sxs-lookup"><span data-stu-id="9584b-159"><a id="resource-tokens"></a>Use minimum token lifetimes for generated Resource tokens</span></span>

| <span data-ttu-id="9584b-160">Titolo</span><span class="sxs-lookup"><span data-stu-id="9584b-160">Title</span></span>                   | <span data-ttu-id="9584b-161">Dettagli</span><span class="sxs-lookup"><span data-stu-id="9584b-161">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="9584b-162">**Componente**</span><span class="sxs-lookup"><span data-stu-id="9584b-162">**Component**</span></span>               | <span data-ttu-id="9584b-163">Azure DocumentDB</span><span class="sxs-lookup"><span data-stu-id="9584b-163">Azure Document DB</span></span> | 
| <span data-ttu-id="9584b-164">**Fase SDL**</span><span class="sxs-lookup"><span data-stu-id="9584b-164">**SDL Phase**</span></span>               | <span data-ttu-id="9584b-165">Compilare</span><span class="sxs-lookup"><span data-stu-id="9584b-165">Build</span></span> |  
| <span data-ttu-id="9584b-166">**Tecnologie applicabili**</span><span class="sxs-lookup"><span data-stu-id="9584b-166">**Applicable Technologies**</span></span> | <span data-ttu-id="9584b-167">Generico</span><span class="sxs-lookup"><span data-stu-id="9584b-167">Generic</span></span> |
| <span data-ttu-id="9584b-168">**Attributes (Attributi) (Attributi)**</span><span class="sxs-lookup"><span data-stu-id="9584b-168">**Attributes**</span></span>              | <span data-ttu-id="9584b-169">N/D</span><span class="sxs-lookup"><span data-stu-id="9584b-169">N/A</span></span>  |
| <span data-ttu-id="9584b-170">**Riferimenti**</span><span class="sxs-lookup"><span data-stu-id="9584b-170">**References**</span></span>              | <span data-ttu-id="9584b-171">N/D</span><span class="sxs-lookup"><span data-stu-id="9584b-171">N/A</span></span>  |
| <span data-ttu-id="9584b-172">**Passaggi**</span><span class="sxs-lookup"><span data-stu-id="9584b-172">**Steps**</span></span> | <span data-ttu-id="9584b-173">Ridurre l'intervallo di tempo del token della risorsa a un valore minimo necessario.</span><span class="sxs-lookup"><span data-stu-id="9584b-173">Reduce the timespan of resource token to a minimum value required.</span></span> <span data-ttu-id="9584b-174">I token delle risorse hanno un intervallo di tempo valido predefinito di 1 ora.</span><span class="sxs-lookup"><span data-stu-id="9584b-174">Resource tokens have a default valid timespan of 1 hour.</span></span>|

## <span data-ttu-id="9584b-175"><a id="wsfederation-logout"></a>Implementare la disconnessione appropriata con i metodi WsFederation quando si usa AD FS</span><span class="sxs-lookup"><span data-stu-id="9584b-175"><a id="wsfederation-logout"></a>Implement proper logout using WsFederation methods when using ADFS</span></span>

| <span data-ttu-id="9584b-176">Titolo</span><span class="sxs-lookup"><span data-stu-id="9584b-176">Title</span></span>                   | <span data-ttu-id="9584b-177">Dettagli</span><span class="sxs-lookup"><span data-stu-id="9584b-177">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="9584b-178">**Componente**</span><span class="sxs-lookup"><span data-stu-id="9584b-178">**Component**</span></span>               | <span data-ttu-id="9584b-179">AD FS</span><span class="sxs-lookup"><span data-stu-id="9584b-179">ADFS</span></span> | 
| <span data-ttu-id="9584b-180">**Fase SDL**</span><span class="sxs-lookup"><span data-stu-id="9584b-180">**SDL Phase**</span></span>               | <span data-ttu-id="9584b-181">Compilare</span><span class="sxs-lookup"><span data-stu-id="9584b-181">Build</span></span> |  
| <span data-ttu-id="9584b-182">**Tecnologie applicabili**</span><span class="sxs-lookup"><span data-stu-id="9584b-182">**Applicable Technologies**</span></span> | <span data-ttu-id="9584b-183">Generico</span><span class="sxs-lookup"><span data-stu-id="9584b-183">Generic</span></span> |
| <span data-ttu-id="9584b-184">**Attributes (Attributi) (Attributi)**</span><span class="sxs-lookup"><span data-stu-id="9584b-184">**Attributes**</span></span>              | <span data-ttu-id="9584b-185">N/D</span><span class="sxs-lookup"><span data-stu-id="9584b-185">N/A</span></span>  |
| <span data-ttu-id="9584b-186">**Riferimenti**</span><span class="sxs-lookup"><span data-stu-id="9584b-186">**References**</span></span>              | <span data-ttu-id="9584b-187">N/D</span><span class="sxs-lookup"><span data-stu-id="9584b-187">N/A</span></span>  |
| <span data-ttu-id="9584b-188">**Passaggi**</span><span class="sxs-lookup"><span data-stu-id="9584b-188">**Steps**</span></span> | <span data-ttu-id="9584b-189">Se l'applicazione si basa sul token del servizio token di sicurezza rilasciato da AD FS, il gestore eventi di disconnessione chiamerà il metodo WSFederationAuthenticationModule.FederatedSignOut() per disconnettere l'utente.</span><span class="sxs-lookup"><span data-stu-id="9584b-189">If the application relies on STS token issued by ADFS, the logout event handler should call WSFederationAuthenticationModule.FederatedSignOut() method to log out the user.</span></span> <span data-ttu-id="9584b-190">Verrà anche eliminata definitivamente la sessione corrente e il valore del token della sessione verrà reimpostato e reso null.</span><span class="sxs-lookup"><span data-stu-id="9584b-190">Also the current session should be destroyed, and the session token value should be reset and nullified.</span></span>|

### <a name="example"></a><span data-ttu-id="9584b-191">Esempio</span><span class="sxs-lookup"><span data-stu-id="9584b-191">Example</span></span>
```C#
        [HttpPost, ValidateAntiForgeryToken]
        [Authorization]
        public ActionResult SignOut(string redirectUrl)
        {
            if (!this.User.Identity.IsAuthenticated)
            {
                return this.View("LogOff", null);
            }

            // Removes the user profile.
            this.Session.Clear();
            this.Session.Abandon();
            HttpContext.Current.Response.Cookies.Add(new System.Web.HttpCookie("ASP.NET_SessionId", string.Empty)
                {
                    Expires = DateTime.Now.AddDays(-1D),
                    Secure = true,
                    HttpOnly = true
                });

            // Signs out at the specified security token service (STS) by using the WS-Federation protocol.
            Uri signOutUrl = new Uri(FederatedAuthentication.WSFederationAuthenticationModule.Issuer);
            Uri replyUrl = new Uri(FederatedAuthentication.WSFederationAuthenticationModule.Realm);
            if (!string.IsNullOrEmpty(redirectUrl))
            {
                replyUrl = new Uri(FederatedAuthentication.WSFederationAuthenticationModule.Realm + redirectUrl);
            }
           //     Signs out of the current session and raises the appropriate events.
            var authModule = FederatedAuthentication.WSFederationAuthenticationModule;
            authModule.SignOut(false);
        //     Signs out at the specified security token service (STS) by using the WS-Federation
        //     protocol.            
            WSFederationAuthenticationModule.FederatedSignOut(signOutUrl, replyUrl);
            return new RedirectResult(redirectUrl);
        }
```

## <span data-ttu-id="9584b-192"><a id="proper-logout"></a>Implementare la disconnessione appropriata quando si usa Identity Server</span><span class="sxs-lookup"><span data-stu-id="9584b-192"><a id="proper-logout"></a>Implement proper logout when using Identity Server</span></span>

| <span data-ttu-id="9584b-193">Titolo</span><span class="sxs-lookup"><span data-stu-id="9584b-193">Title</span></span>                   | <span data-ttu-id="9584b-194">Dettagli</span><span class="sxs-lookup"><span data-stu-id="9584b-194">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="9584b-195">**Componente**</span><span class="sxs-lookup"><span data-stu-id="9584b-195">**Component**</span></span>               | <span data-ttu-id="9584b-196">Identity Server</span><span class="sxs-lookup"><span data-stu-id="9584b-196">Identity Server</span></span> | 
| <span data-ttu-id="9584b-197">**Fase SDL**</span><span class="sxs-lookup"><span data-stu-id="9584b-197">**SDL Phase**</span></span>               | <span data-ttu-id="9584b-198">Compilare</span><span class="sxs-lookup"><span data-stu-id="9584b-198">Build</span></span> |  
| <span data-ttu-id="9584b-199">**Tecnologie applicabili**</span><span class="sxs-lookup"><span data-stu-id="9584b-199">**Applicable Technologies**</span></span> | <span data-ttu-id="9584b-200">Generico</span><span class="sxs-lookup"><span data-stu-id="9584b-200">Generic</span></span> |
| <span data-ttu-id="9584b-201">**Attributes (Attributi) (Attributi)**</span><span class="sxs-lookup"><span data-stu-id="9584b-201">**Attributes**</span></span>              | <span data-ttu-id="9584b-202">N/D</span><span class="sxs-lookup"><span data-stu-id="9584b-202">N/A</span></span>  |
| <span data-ttu-id="9584b-203">**Riferimenti**</span><span class="sxs-lookup"><span data-stu-id="9584b-203">**References**</span></span>              | [<span data-ttu-id="9584b-204">IdentityServer3: disconnessione federata</span><span class="sxs-lookup"><span data-stu-id="9584b-204">IdentityServer3-Federated sign out</span></span>](https://identityserver.github.io/Documentation/docsv2/advanced/federated-signout.html) |
| <span data-ttu-id="9584b-205">**Passaggi**</span><span class="sxs-lookup"><span data-stu-id="9584b-205">**Steps**</span></span> | <span data-ttu-id="9584b-206">Identity Server supporta la federazione con i provider di identità eterni.</span><span class="sxs-lookup"><span data-stu-id="9584b-206">IdentityServer supports the ability to federate with external identity providers.</span></span> <span data-ttu-id="9584b-207">Quando un utente si disconnette da un provider di identità upstream, a seconda del protocollo usato, si potrebbe ricevere una notifica quando l'utente si disconnette. Ciò consente quindi a Identity Server di inviare una notifica ai client che potranno disconnettere l'utente a loro volta. Controllare la documentazione nella sezione Riferimenti per i dettagli sull'implementazione.</span><span class="sxs-lookup"><span data-stu-id="9584b-207">When a user signs out of an upstream identity provider, depending upon the protocol used, it might be possible to receive a notification when the user signs out. It allows IdentityServer to notify its clients so they can also sign the user out. Check the documentation in the references section for the implementation details.</span></span>|

## <span data-ttu-id="9584b-208"><a id="https-secure-cookies"></a>Le applicazioni disponibili tramite HTTPS devono usare cookie sicuri</span><span class="sxs-lookup"><span data-stu-id="9584b-208"><a id="https-secure-cookies"></a>Applications available over HTTPS must use secure cookies</span></span>

| <span data-ttu-id="9584b-209">Titolo</span><span class="sxs-lookup"><span data-stu-id="9584b-209">Title</span></span>                   | <span data-ttu-id="9584b-210">Dettagli</span><span class="sxs-lookup"><span data-stu-id="9584b-210">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="9584b-211">**Componente**</span><span class="sxs-lookup"><span data-stu-id="9584b-211">**Component**</span></span>               | <span data-ttu-id="9584b-212">Applicazione Web.</span><span class="sxs-lookup"><span data-stu-id="9584b-212">Web Application</span></span> | 
| <span data-ttu-id="9584b-213">**Fase SDL**</span><span class="sxs-lookup"><span data-stu-id="9584b-213">**SDL Phase**</span></span>               | <span data-ttu-id="9584b-214">Compilare</span><span class="sxs-lookup"><span data-stu-id="9584b-214">Build</span></span> |  
| <span data-ttu-id="9584b-215">**Tecnologie applicabili**</span><span class="sxs-lookup"><span data-stu-id="9584b-215">**Applicable Technologies**</span></span> | <span data-ttu-id="9584b-216">Generico</span><span class="sxs-lookup"><span data-stu-id="9584b-216">Generic</span></span> |
| <span data-ttu-id="9584b-217">**Attributes (Attributi) (Attributi)**</span><span class="sxs-lookup"><span data-stu-id="9584b-217">**Attributes**</span></span>              | <span data-ttu-id="9584b-218">Tipo di ambiente: locale</span><span class="sxs-lookup"><span data-stu-id="9584b-218">EnvironmentType - OnPrem</span></span> |
| <span data-ttu-id="9584b-219">**Riferimenti**</span><span class="sxs-lookup"><span data-stu-id="9584b-219">**References**</span></span>              | <span data-ttu-id="9584b-220">[Elemento httpCookies (schema delle impostazioni ASP.NET)](http://msdn.microsoft.com/library/ms228262(v=vs.100).aspx), [Proprietà HttpCookie.Secure](http://msdn.microsoft.com/library/system.web.httpcookie.secure.aspx)</span><span class="sxs-lookup"><span data-stu-id="9584b-220">[httpCookies Element (ASP.NET Settings Schema)](http://msdn.microsoft.com/library/ms228262(v=vs.100).aspx), [HttpCookie.Secure Property](http://msdn.microsoft.com/library/system.web.httpcookie.secure.aspx)</span></span> |
| <span data-ttu-id="9584b-221">**Passaggi**</span><span class="sxs-lookup"><span data-stu-id="9584b-221">**Steps**</span></span> | <span data-ttu-id="9584b-222">I cookie in genere sono accessibili solo per il dominio per il cui ambito sono stati definiti.</span><span class="sxs-lookup"><span data-stu-id="9584b-222">Cookies are normally only accessible to the domain for which they were scoped.</span></span> <span data-ttu-id="9584b-223">La definizione di "dominio" purtroppo non include il protocollo, quindi i cookie creati tramite HTTPS sono accessibile tramite HTTP.</span><span class="sxs-lookup"><span data-stu-id="9584b-223">Unfortunately, the definition of "domain" does not include the protocol so cookies that are created over HTTPS are accessible over HTTP.</span></span> <span data-ttu-id="9584b-224">L'attributo "secure" indica al browser che il cookie deve essere disponibile solo tramite HTTPS.</span><span class="sxs-lookup"><span data-stu-id="9584b-224">The "secure" attribute indicates to the browser that the cookie should only be made available over HTTPS.</span></span> <span data-ttu-id="9584b-225">Assicurarsi che tutti i cookie impostati tramite HTTPS usino l'attributo **secure**.</span><span class="sxs-lookup"><span data-stu-id="9584b-225">Ensure that all cookies set over HTTPS use the **secure** attribute.</span></span> <span data-ttu-id="9584b-226">Il requisito può essere applicato nel file web.config impostando l'attributo requireSSL su true.</span><span class="sxs-lookup"><span data-stu-id="9584b-226">The requirement can be enforced in the web.config file by setting the requireSSL attribute to true.</span></span> <span data-ttu-id="9584b-227">Si tratta dell'approccio da preferire perché applicherà l'attributo **secure** per tutti i cookie correnti e futuri senza dover apportare altre modifiche al codice.</span><span class="sxs-lookup"><span data-stu-id="9584b-227">It is the preferred approach because it will enforce the **secure** attribute for all current and future cookies without the need to make any additional code changes.</span></span>|

### <a name="example"></a><span data-ttu-id="9584b-228">Esempio</span><span class="sxs-lookup"><span data-stu-id="9584b-228">Example</span></span>
```C#
<configuration>
  <system.web>
    <httpCookies requireSSL="true"/>
  </system.web>
</configuration>
```
<span data-ttu-id="9584b-229">L'impostazione viene applicata anche se viene usato HTTP per accedere all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="9584b-229">The setting is enforced even if HTTP is used to access the application.</span></span> <span data-ttu-id="9584b-230">Se viene usato HTTP per accedere all'applicazione, l'impostazione interrompe l'applicazione perché i cookie vengono impostati con l'attributo secure e il browser non li invierà di nuovo all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="9584b-230">If HTTP is used to access the application, the setting breaks the application because the cookies are set with the secure attribute and the browser will not send them back to the application.</span></span>

| <span data-ttu-id="9584b-231">Titolo</span><span class="sxs-lookup"><span data-stu-id="9584b-231">Title</span></span>                   | <span data-ttu-id="9584b-232">Dettagli</span><span class="sxs-lookup"><span data-stu-id="9584b-232">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="9584b-233">**Componente**</span><span class="sxs-lookup"><span data-stu-id="9584b-233">**Component**</span></span>               | <span data-ttu-id="9584b-234">Applicazione Web.</span><span class="sxs-lookup"><span data-stu-id="9584b-234">Web Application</span></span> | 
| <span data-ttu-id="9584b-235">**Fase SDL**</span><span class="sxs-lookup"><span data-stu-id="9584b-235">**SDL Phase**</span></span>               | <span data-ttu-id="9584b-236">Compilare</span><span class="sxs-lookup"><span data-stu-id="9584b-236">Build</span></span> |  
| <span data-ttu-id="9584b-237">**Tecnologie applicabili**</span><span class="sxs-lookup"><span data-stu-id="9584b-237">**Applicable Technologies**</span></span> | <span data-ttu-id="9584b-238">Web Form, MVC 5</span><span class="sxs-lookup"><span data-stu-id="9584b-238">Web Forms, MVC5</span></span> |
| <span data-ttu-id="9584b-239">**Attributes (Attributi) (Attributi)**</span><span class="sxs-lookup"><span data-stu-id="9584b-239">**Attributes**</span></span>              | <span data-ttu-id="9584b-240">Tipo di ambiente: locale</span><span class="sxs-lookup"><span data-stu-id="9584b-240">EnvironmentType - OnPrem</span></span> |
| <span data-ttu-id="9584b-241">**Riferimenti**</span><span class="sxs-lookup"><span data-stu-id="9584b-241">**References**</span></span>              | <span data-ttu-id="9584b-242">N/D</span><span class="sxs-lookup"><span data-stu-id="9584b-242">N/A</span></span>  |
| <span data-ttu-id="9584b-243">**Passaggi**</span><span class="sxs-lookup"><span data-stu-id="9584b-243">**Steps**</span></span> | <span data-ttu-id="9584b-244">Quando l'applicazione Web è la relying party e l'IdP è il server AD FS, l'attributo secure del token FedAuth può essere configurato impostando requireSSL su True nella sezione `system.identityModel.services` di web.config:</span><span class="sxs-lookup"><span data-stu-id="9584b-244">When the web application is the Relying Party, and the IdP is ADFS server, the FedAuth token's secure attribute can be configured by setting requireSSL to True in `system.identityModel.services` section of web.config:</span></span>|

### <a name="example"></a><span data-ttu-id="9584b-245">Esempio</span><span class="sxs-lookup"><span data-stu-id="9584b-245">Example</span></span>
```C#
  <system.identityModel.services>
    <federationConfiguration>
      <!-- Set requireSsl=true; domain=application domain name used by FedAuth cookies (Ex: .gdinfra.com); -->
      <cookieHandler requireSsl="true" persistentSessionLifetime="0.0:20:0" />
    ....  
    </federationConfiguration>
  </system.identityModel.services>
```

## <span data-ttu-id="9584b-246"><a id="cookie-definition"></a>Tutte le applicazioni basate su http devono specificare solo http per la definizione dei cookie</span><span class="sxs-lookup"><span data-stu-id="9584b-246"><a id="cookie-definition"></a>All http based application should specify http only for cookie definition</span></span>

| <span data-ttu-id="9584b-247">Titolo</span><span class="sxs-lookup"><span data-stu-id="9584b-247">Title</span></span>                   | <span data-ttu-id="9584b-248">Dettagli</span><span class="sxs-lookup"><span data-stu-id="9584b-248">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="9584b-249">**Componente**</span><span class="sxs-lookup"><span data-stu-id="9584b-249">**Component**</span></span>               | <span data-ttu-id="9584b-250">Applicazione Web.</span><span class="sxs-lookup"><span data-stu-id="9584b-250">Web Application</span></span> | 
| <span data-ttu-id="9584b-251">**Fase SDL**</span><span class="sxs-lookup"><span data-stu-id="9584b-251">**SDL Phase**</span></span>               | <span data-ttu-id="9584b-252">Compilare</span><span class="sxs-lookup"><span data-stu-id="9584b-252">Build</span></span> |  
| <span data-ttu-id="9584b-253">**Tecnologie applicabili**</span><span class="sxs-lookup"><span data-stu-id="9584b-253">**Applicable Technologies**</span></span> | <span data-ttu-id="9584b-254">Generico</span><span class="sxs-lookup"><span data-stu-id="9584b-254">Generic</span></span> |
| <span data-ttu-id="9584b-255">**Attributes (Attributi) (Attributi)**</span><span class="sxs-lookup"><span data-stu-id="9584b-255">**Attributes**</span></span>              | <span data-ttu-id="9584b-256">N/D</span><span class="sxs-lookup"><span data-stu-id="9584b-256">N/A</span></span>  |
| <span data-ttu-id="9584b-257">**Riferimenti**</span><span class="sxs-lookup"><span data-stu-id="9584b-257">**References**</span></span>              | <span data-ttu-id="9584b-258">[Secure Cookie Attribute](https://en.wikipedia.org/wiki/HTTP_cookie#Secure_cookie) (Attributo dei cookie Secure)</span><span class="sxs-lookup"><span data-stu-id="9584b-258">[Secure Cookie Attribute](https://en.wikipedia.org/wiki/HTTP_cookie#Secure_cookie)</span></span> |
| <span data-ttu-id="9584b-259">**Passaggi**</span><span class="sxs-lookup"><span data-stu-id="9584b-259">**Steps**</span></span> | <span data-ttu-id="9584b-260">Per mitigare il rischio di diffusione di informazioni con un attacco di tipo cross-site scripting (XSS), un nuovo attributo (httpOnly) è stato introdotto nei cookie ed è supportato da tutti i principali browser.</span><span class="sxs-lookup"><span data-stu-id="9584b-260">To mitigate the risk of information disclosure with a cross-site scripting (XSS) attack, a new attribute - httpOnly - was introduced to cookies and is supported by all major browsers.</span></span> <span data-ttu-id="9584b-261">L'attributo specifica che un cookie non è accessibile tramite script.</span><span class="sxs-lookup"><span data-stu-id="9584b-261">The attribute specifies that a cookie is not accessible through script.</span></span> <span data-ttu-id="9584b-262">Usando i cookie HttpOnly, un'applicazione Web riduce la possibilità che le informazioni sensibili contenute nel cookie possano essere sottratte tramite script e inviate al sito Web di un utente malintenzionato.</span><span class="sxs-lookup"><span data-stu-id="9584b-262">By using HttpOnly cookies, a web application reduces the possibility that sensitive information contained in the cookie can be stolen via script and sent to an attacker's website.</span></span> |

### <a name="example"></a><span data-ttu-id="9584b-263">Esempio</span><span class="sxs-lookup"><span data-stu-id="9584b-263">Example</span></span>
<span data-ttu-id="9584b-264">Tutte le applicazioni basate su HTTP che usano cookie devono specificare HttpOnly nella definizione del cookie, implementando la configurazione seguente in web.config:</span><span class="sxs-lookup"><span data-stu-id="9584b-264">All HTTP-based applications that use cookies should specify HttpOnly in the cookie definition, by implementing following configuration in web.config:</span></span>
```XML
<system.web>
.
.
   <httpCookies requireSSL="false" httpOnlyCookies="true"/>
.
.
</system.web>
```

| <span data-ttu-id="9584b-265">Titolo</span><span class="sxs-lookup"><span data-stu-id="9584b-265">Title</span></span>                   | <span data-ttu-id="9584b-266">Dettagli</span><span class="sxs-lookup"><span data-stu-id="9584b-266">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="9584b-267">**Componente**</span><span class="sxs-lookup"><span data-stu-id="9584b-267">**Component**</span></span>               | <span data-ttu-id="9584b-268">Applicazione Web.</span><span class="sxs-lookup"><span data-stu-id="9584b-268">Web Application</span></span> | 
| <span data-ttu-id="9584b-269">**Fase SDL**</span><span class="sxs-lookup"><span data-stu-id="9584b-269">**SDL Phase**</span></span>               | <span data-ttu-id="9584b-270">Compilare</span><span class="sxs-lookup"><span data-stu-id="9584b-270">Build</span></span> |  
| <span data-ttu-id="9584b-271">**Tecnologie applicabili**</span><span class="sxs-lookup"><span data-stu-id="9584b-271">**Applicable Technologies**</span></span> | <span data-ttu-id="9584b-272">Web Form</span><span class="sxs-lookup"><span data-stu-id="9584b-272">Web Forms</span></span> |
| <span data-ttu-id="9584b-273">**Attributes (Attributi) (Attributi)**</span><span class="sxs-lookup"><span data-stu-id="9584b-273">**Attributes**</span></span>              | <span data-ttu-id="9584b-274">N/D</span><span class="sxs-lookup"><span data-stu-id="9584b-274">N/A</span></span>  |
| <span data-ttu-id="9584b-275">**Riferimenti**</span><span class="sxs-lookup"><span data-stu-id="9584b-275">**References**</span></span>              | [<span data-ttu-id="9584b-276">Proprietà FormsAuthentication.RequireSSL</span><span class="sxs-lookup"><span data-stu-id="9584b-276">FormsAuthentication.RequireSSL Property</span></span>](https://msdn.microsoft.com/library/system.web.security.formsauthentication.requiressl.aspx) |
| <span data-ttu-id="9584b-277">**Passaggi**</span><span class="sxs-lookup"><span data-stu-id="9584b-277">**Steps**</span></span> | <span data-ttu-id="9584b-278">Il valore della proprietà RequireSSL viene impostato nel file di configurazione per un'applicazione ASP.NET usando l'attributo requireSSL dell'elemento di configurazione.</span><span class="sxs-lookup"><span data-stu-id="9584b-278">The RequireSSL property value is set in the configuration file for an ASP.NET application by using the requireSSL attribute of the configuration element.</span></span> <span data-ttu-id="9584b-279">È possibile specificare nel file Web.config per l'applicazione ASP.NET se SSL (Secure Sockets Layer) è necessario per restituire il cookie di autenticazione basata su form al server impostando l'attributo requireSSL.</span><span class="sxs-lookup"><span data-stu-id="9584b-279">You can specify in the Web.config file for your ASP.NET application whether SSL (Secure Sockets Layer) is required to return the forms-authentication cookie to the server by setting the requireSSL attribute.</span></span>|

### <a name="example"></a><span data-ttu-id="9584b-280">Esempio</span><span class="sxs-lookup"><span data-stu-id="9584b-280">Example</span></span> 
<span data-ttu-id="9584b-281">L'esempio di codice seguente imposta l'attributo requireSSL nel file Web.config.</span><span class="sxs-lookup"><span data-stu-id="9584b-281">The following code example sets the requireSSL attribute in the Web.config file.</span></span>
```XML
<authentication mode="Forms">
  <forms loginUrl="member_login.aspx" cookieless="UseCookies" requireSSL="true"/>
</authentication>
```

| <span data-ttu-id="9584b-282">Titolo</span><span class="sxs-lookup"><span data-stu-id="9584b-282">Title</span></span>                   | <span data-ttu-id="9584b-283">Dettagli</span><span class="sxs-lookup"><span data-stu-id="9584b-283">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="9584b-284">**Componente**</span><span class="sxs-lookup"><span data-stu-id="9584b-284">**Component**</span></span>               | <span data-ttu-id="9584b-285">Applicazione Web.</span><span class="sxs-lookup"><span data-stu-id="9584b-285">Web Application</span></span> | 
| <span data-ttu-id="9584b-286">**Fase SDL**</span><span class="sxs-lookup"><span data-stu-id="9584b-286">**SDL Phase**</span></span>               | <span data-ttu-id="9584b-287">Compilare</span><span class="sxs-lookup"><span data-stu-id="9584b-287">Build</span></span> |  
| <span data-ttu-id="9584b-288">**Tecnologie applicabili**</span><span class="sxs-lookup"><span data-stu-id="9584b-288">**Applicable Technologies**</span></span> | <span data-ttu-id="9584b-289">MVC 5</span><span class="sxs-lookup"><span data-stu-id="9584b-289">MVC5</span></span> |
| <span data-ttu-id="9584b-290">**Attributes (Attributi) (Attributi)**</span><span class="sxs-lookup"><span data-stu-id="9584b-290">**Attributes**</span></span>              | <span data-ttu-id="9584b-291">Tipo di ambiente: locale</span><span class="sxs-lookup"><span data-stu-id="9584b-291">EnvironmentType - OnPrem</span></span> |
| <span data-ttu-id="9584b-292">**Riferimenti**</span><span class="sxs-lookup"><span data-stu-id="9584b-292">**References**</span></span>              | <span data-ttu-id="9584b-293">[Windows Identity Foundation (WIF) Configuration – Part II](https://blogs.msdn.microsoft.com/alikl/2011/02/01/windows-identity-foundation-wif-configuration-part-ii-cookiehandler-chunkedcookiehandler-customcookiehandler/) (Configurazione di Windows Identity Foundation (WIF): parte II)</span><span class="sxs-lookup"><span data-stu-id="9584b-293">[Windows Identity Foundation (WIF) Configuration – Part II](https://blogs.msdn.microsoft.com/alikl/2011/02/01/windows-identity-foundation-wif-configuration-part-ii-cookiehandler-chunkedcookiehandler-customcookiehandler/)</span></span> |
| <span data-ttu-id="9584b-294">**Passaggi**</span><span class="sxs-lookup"><span data-stu-id="9584b-294">**Steps**</span></span> | <span data-ttu-id="9584b-295">Per impostare l'attributo httpOnly per i cookie FedAuth, il valore dell'attributo hideFromCsript deve essere impostato su True.</span><span class="sxs-lookup"><span data-stu-id="9584b-295">To set httpOnly attribute for FedAuth cookies, hideFromCsript attribute value should be set to True.</span></span> |

### <a name="example"></a><span data-ttu-id="9584b-296">Esempio</span><span class="sxs-lookup"><span data-stu-id="9584b-296">Example</span></span>
<span data-ttu-id="9584b-297">La configurazione seguente illustra la configurazione corretta:</span><span class="sxs-lookup"><span data-stu-id="9584b-297">Following configuration shows the correct configuration:</span></span>
```XML
<federatedAuthentication>
<cookieHandler mode="Custom"
                       hideFromScript="true"
                       name="FedAuth"
                       path="/"
                       requireSsl="true"
                       persistentSessionLifetime="25">
</cookieHandler>
</federatedAuthentication>
```

## <span data-ttu-id="9584b-298"><a id="csrf-asp"></a>Mitigare il rischio di attacchi basati su richieste intersito false nelle pagine Web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="9584b-298"><a id="csrf-asp"></a>Mitigate against Cross-Site Request Forgery (CSRF) attacks on ASP.NET web pages</span></span>

| <span data-ttu-id="9584b-299">Titolo</span><span class="sxs-lookup"><span data-stu-id="9584b-299">Title</span></span>                   | <span data-ttu-id="9584b-300">Dettagli</span><span class="sxs-lookup"><span data-stu-id="9584b-300">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="9584b-301">**Componente**</span><span class="sxs-lookup"><span data-stu-id="9584b-301">**Component**</span></span>               | <span data-ttu-id="9584b-302">Applicazione Web.</span><span class="sxs-lookup"><span data-stu-id="9584b-302">Web Application</span></span> | 
| <span data-ttu-id="9584b-303">**Fase SDL**</span><span class="sxs-lookup"><span data-stu-id="9584b-303">**SDL Phase**</span></span>               | <span data-ttu-id="9584b-304">Compilare</span><span class="sxs-lookup"><span data-stu-id="9584b-304">Build</span></span> |  
| <span data-ttu-id="9584b-305">**Tecnologie applicabili**</span><span class="sxs-lookup"><span data-stu-id="9584b-305">**Applicable Technologies**</span></span> | <span data-ttu-id="9584b-306">Generico</span><span class="sxs-lookup"><span data-stu-id="9584b-306">Generic</span></span> |
| <span data-ttu-id="9584b-307">**Attributes (Attributi) (Attributi)**</span><span class="sxs-lookup"><span data-stu-id="9584b-307">**Attributes**</span></span>              | <span data-ttu-id="9584b-308">N/D</span><span class="sxs-lookup"><span data-stu-id="9584b-308">N/A</span></span>  |
| <span data-ttu-id="9584b-309">**Riferimenti**</span><span class="sxs-lookup"><span data-stu-id="9584b-309">**References**</span></span>              | <span data-ttu-id="9584b-310">N/D</span><span class="sxs-lookup"><span data-stu-id="9584b-310">N/A</span></span>  |
| <span data-ttu-id="9584b-311">**Passaggi**</span><span class="sxs-lookup"><span data-stu-id="9584b-311">**Steps**</span></span> | <span data-ttu-id="9584b-312">Richiesta intersito falsa (CSRF o XSRF) è un tipo di attacco in cui un utente malintenzionato può eseguire azioni nel contesto di protezione della sessione stabilita di un utente diverso in un sito web.</span><span class="sxs-lookup"><span data-stu-id="9584b-312">Cross-site request forgery (CSRF or XSRF) is a type of attack in which an attacker can carry out actions in the security context of a different user's established session on a web site.</span></span> <span data-ttu-id="9584b-313">L'obiettivo è quello di modificare o eliminare il contenuto, se il sito web di destinazione si affida esclusivamente ai cookie di sessione per autenticare la richiesta ricevuta.</span><span class="sxs-lookup"><span data-stu-id="9584b-313">The goal is to modify or delete content, if the targeted web site relies exclusively on session cookies to authenticate received request.</span></span> <span data-ttu-id="9584b-314">Un utente malintenzionato potrebbe sfruttare questa vulnerabilità acquisendo il browser di un altro utente per caricare un URL con un comando da un sito vulnerabile a cui l'utente è già connesso.</span><span class="sxs-lookup"><span data-stu-id="9584b-314">An attacker could exploit this vulnerability by getting a different user's browser to load a URL with a command from a vulnerable site on which the user is already logged in.</span></span> <span data-ttu-id="9584b-315">Un utente malintenzionato può raggiungere questo scopo in diversi modi, ad esempio ospitando un sito Web diverso che carica una risorsa dal server vulnerabile o spingendo l'utente a fare clic su un collegamento.</span><span class="sxs-lookup"><span data-stu-id="9584b-315">There are many ways for an attacker to do that, such as by hosting a different web site that loads a resource from the vulnerable server, or getting the user to click a link.</span></span> <span data-ttu-id="9584b-316">L'attacco può essere evitato se il server invia un token aggiuntivo al client, richiede al client di includere tale token in tutte le richieste future e verifica che tutte le richieste future includano un token relativo alla sessione corrente, ad esempio usando AntiForgeryToken o ViewState di ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="9584b-316">The attack can be prevented if the server sends an additional token to the client, requires the client to include that token in all future requests, and verifies that all future requests include a token that pertains to the current session, such as by using the ASP.NET AntiForgeryToken or ViewState.</span></span> |

| <span data-ttu-id="9584b-317">Titolo</span><span class="sxs-lookup"><span data-stu-id="9584b-317">Title</span></span>                   | <span data-ttu-id="9584b-318">Dettagli</span><span class="sxs-lookup"><span data-stu-id="9584b-318">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="9584b-319">**Componente**</span><span class="sxs-lookup"><span data-stu-id="9584b-319">**Component**</span></span>               | <span data-ttu-id="9584b-320">Applicazione Web.</span><span class="sxs-lookup"><span data-stu-id="9584b-320">Web Application</span></span> | 
| <span data-ttu-id="9584b-321">**Fase SDL**</span><span class="sxs-lookup"><span data-stu-id="9584b-321">**SDL Phase**</span></span>               | <span data-ttu-id="9584b-322">Compilare</span><span class="sxs-lookup"><span data-stu-id="9584b-322">Build</span></span> |  
| <span data-ttu-id="9584b-323">**Tecnologie applicabili**</span><span class="sxs-lookup"><span data-stu-id="9584b-323">**Applicable Technologies**</span></span> | <span data-ttu-id="9584b-324">MVC 5, MVC 6</span><span class="sxs-lookup"><span data-stu-id="9584b-324">MVC5, MVC6</span></span> |
| <span data-ttu-id="9584b-325">**Attributes (Attributi) (Attributi)**</span><span class="sxs-lookup"><span data-stu-id="9584b-325">**Attributes**</span></span>              | <span data-ttu-id="9584b-326">N/D</span><span class="sxs-lookup"><span data-stu-id="9584b-326">N/A</span></span>  |
| <span data-ttu-id="9584b-327">**Riferimenti**</span><span class="sxs-lookup"><span data-stu-id="9584b-327">**References**</span></span>              | <span data-ttu-id="9584b-328">[XSRF/CSRF Prevention in ASP.NET MVC and Web Pages](http://www.asp.net/mvc/overview/security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages) (Prevenzione delle richieste intersito false in ASP.NET MVC e nelle pagine Web ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="9584b-328">[XSRF/CSRF Prevention in ASP.NET MVC and Web Pages](http://www.asp.net/mvc/overview/security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages)</span></span> |
| <span data-ttu-id="9584b-329">**Passaggi**</span><span class="sxs-lookup"><span data-stu-id="9584b-329">**Steps**</span></span> | <span data-ttu-id="9584b-330">Form ASP.NET MVC e contro le richieste intersito: usare il metodo helper `AntiForgeryToken` in Views. Inserire `Html.AntiForgeryToken()` nel form, ad esempio,</span><span class="sxs-lookup"><span data-stu-id="9584b-330">Anti-CSRF and ASP.NET MVC forms - Use the `AntiForgeryToken` helper method on Views; put an `Html.AntiForgeryToken()` into the form, for example,</span></span>|

### <a name="example"></a><span data-ttu-id="9584b-331">Esempio</span><span class="sxs-lookup"><span data-stu-id="9584b-331">Example</span></span>
```C#
@using (Html.BeginForm("UserProfile", "SubmitUpdate")) { 
    @Html.ValidationSummary(true) 
    @Html.AntiForgeryToken()
    <fieldset> 
```

### <a name="example"></a><span data-ttu-id="9584b-332">Esempio</span><span class="sxs-lookup"><span data-stu-id="9584b-332">Example</span></span>
```C#
<form action="/UserProfile/SubmitUpdate" method="post">
    <input name="__RequestVerificationToken" type="hidden" value="saTFWpkKN0BYazFtN6c4YbZAmsEwG0srqlUqqloi/fVgeV2ciIFVmelvzwRZpArs" />
    <!-- rest of form goes here -->
</form>
```

### <a name="example"></a><span data-ttu-id="9584b-333">Esempio</span><span class="sxs-lookup"><span data-stu-id="9584b-333">Example</span></span>
<span data-ttu-id="9584b-334">Html.AntiForgeryToken() assegna contemporaneamente al visitatore un cookie denominato __RequestVerificationToken, con lo stesso valore del valore nascosto casuale illustrato sopra.</span><span class="sxs-lookup"><span data-stu-id="9584b-334">At the same time, Html.AntiForgeryToken() gives the visitor a cookie called __RequestVerificationToken, with the same value as the random hidden value shown above.</span></span> <span data-ttu-id="9584b-335">Per convalidare un post del form in ingresso, aggiungere quindi il filtro [ValidateAntiForgeryToken] al metodo azione di destinazione.</span><span class="sxs-lookup"><span data-stu-id="9584b-335">Next, to validate an incoming form post, add the [ValidateAntiForgeryToken] filter to the target action method.</span></span> <span data-ttu-id="9584b-336">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="9584b-336">For example:</span></span>
```
[ValidateAntiForgeryToken]
public ViewResult SubmitUpdate()
{
// ... etc.
}
```
<span data-ttu-id="9584b-337">Filtro di autorizzazione che controlla che:</span><span class="sxs-lookup"><span data-stu-id="9584b-337">Authorization filter that checks that:</span></span>
* <span data-ttu-id="9584b-338">La richiesta in ingresso abbia un cookie denominato __RequestVerificationToken.</span><span class="sxs-lookup"><span data-stu-id="9584b-338">The incoming request has a cookie called __RequestVerificationToken</span></span>
* <span data-ttu-id="9584b-339">La richiesta in ingresso ha un cookie `Request.Form` denominato __RequestVerificationToken</span><span class="sxs-lookup"><span data-stu-id="9584b-339">The incoming request has a `Request.Form` entry called __RequestVerificationToken</span></span>
* <span data-ttu-id="9584b-340">Questi valori del cookie e di `Request.Form` corrispondono. Presumendo che sia tutto a posto, la richiesta viene completata normalmente.</span><span class="sxs-lookup"><span data-stu-id="9584b-340">These cookie and `Request.Form` values match Assuming all is well, the request goes through as normal.</span></span> <span data-ttu-id="9584b-341">In caso contrario, si verifica un errore di autorizzazione e viene visualizzato il messaggio "Token antifalsificazione non specificato o non valido".</span><span class="sxs-lookup"><span data-stu-id="9584b-341">But if not, then an authorization failure with message “A required anti-forgery token was not supplied or was invalid”.</span></span> 

### <a name="example"></a><span data-ttu-id="9584b-342">Esempio</span><span class="sxs-lookup"><span data-stu-id="9584b-342">Example</span></span>
<span data-ttu-id="9584b-343">Prevenzione di richieste intersito false e AJAX: il token del form può rappresentare un problema per le richieste AJAX, perché una richiesta AJAX potrebbe inviare dati JSON, non dati in formato HTML.</span><span class="sxs-lookup"><span data-stu-id="9584b-343">Anti-CSRF and AJAX: The form token can be a problem for AJAX requests, because an AJAX request might send JSON data, not HTML form data.</span></span> <span data-ttu-id="9584b-344">Una soluzione consiste nell'inviare i token in un'intestazione HTTP personalizzata.</span><span class="sxs-lookup"><span data-stu-id="9584b-344">One solution is to send the tokens in a custom HTTP header.</span></span> <span data-ttu-id="9584b-345">Il codice seguente usa la sintassi Razor per generare i token e quindi li aggiunge a una richiesta AJAX.</span><span class="sxs-lookup"><span data-stu-id="9584b-345">The following code uses Razor syntax to generate the tokens, and then adds the tokens to an AJAX request.</span></span> 
```C#
<script>
    @functions{
        public string TokenHeaderValue()
        {
            string cookieToken, formToken;
            AntiForgery.GetTokens(null, out cookieToken, out formToken);
            return cookieToken + ":" + formToken;                
        }
    }

    $.ajax("api/values", {
        type: "post",
        contentType: "application/json",
        data: {  }, // JSON data goes here
        dataType: "json",
        headers: {
            'RequestVerificationToken': '@TokenHeaderValue()'
        }
    });
</script>
```

### <a name="example"></a><span data-ttu-id="9584b-346">Esempio</span><span class="sxs-lookup"><span data-stu-id="9584b-346">Example</span></span>
<span data-ttu-id="9584b-347">Quando si elabora la richiesta, estrarre i token dall'intestazione della richiesta.</span><span class="sxs-lookup"><span data-stu-id="9584b-347">When you process the request, extract the tokens from the request header.</span></span> <span data-ttu-id="9584b-348">Chiamare quindi il metodo AntiForgery.Validate per convalidare i token.</span><span class="sxs-lookup"><span data-stu-id="9584b-348">Then call the AntiForgery.Validate method to validate the tokens.</span></span> <span data-ttu-id="9584b-349">Il metodo Validate genera un'eccezione se i token non sono validi.</span><span class="sxs-lookup"><span data-stu-id="9584b-349">The Validate method throws an exception if the tokens are not valid.</span></span>
```C#
void ValidateRequestHeader(HttpRequestMessage request)
{
    string cookieToken = "";
    string formToken = "";

    IEnumerable<string> tokenHeaders;
    if (request.Headers.TryGetValues("RequestVerificationToken", out tokenHeaders))
    {
        string[] tokens = tokenHeaders.First().Split(':');
        if (tokens.Length == 2)
        {
            cookieToken = tokens[0].Trim();
            formToken = tokens[1].Trim();
        }
    }
    AntiForgery.Validate(cookieToken, formToken);
}
```

| <span data-ttu-id="9584b-350">Titolo</span><span class="sxs-lookup"><span data-stu-id="9584b-350">Title</span></span>                   | <span data-ttu-id="9584b-351">Dettagli</span><span class="sxs-lookup"><span data-stu-id="9584b-351">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="9584b-352">**Componente**</span><span class="sxs-lookup"><span data-stu-id="9584b-352">**Component**</span></span>               | <span data-ttu-id="9584b-353">Applicazione Web.</span><span class="sxs-lookup"><span data-stu-id="9584b-353">Web Application</span></span> | 
| <span data-ttu-id="9584b-354">**Fase SDL**</span><span class="sxs-lookup"><span data-stu-id="9584b-354">**SDL Phase**</span></span>               | <span data-ttu-id="9584b-355">Compilare</span><span class="sxs-lookup"><span data-stu-id="9584b-355">Build</span></span> |  
| <span data-ttu-id="9584b-356">**Tecnologie applicabili**</span><span class="sxs-lookup"><span data-stu-id="9584b-356">**Applicable Technologies**</span></span> | <span data-ttu-id="9584b-357">Web Form</span><span class="sxs-lookup"><span data-stu-id="9584b-357">Web Forms</span></span> |
| <span data-ttu-id="9584b-358">**Attributes (Attributi) (Attributi)**</span><span class="sxs-lookup"><span data-stu-id="9584b-358">**Attributes**</span></span>              | <span data-ttu-id="9584b-359">N/D</span><span class="sxs-lookup"><span data-stu-id="9584b-359">N/A</span></span>  |
| <span data-ttu-id="9584b-360">**Riferimenti**</span><span class="sxs-lookup"><span data-stu-id="9584b-360">**References**</span></span>              | <span data-ttu-id="9584b-361">[Take Advantage of ASP.NET Built-in Features to Fend Off Web Attacks](https://msdn.microsoft.com/library/ms972969.aspx#securitybarriers_topic2) (Sfruttare le funzionalità predefinite di ASP.NET per respingere gli attacchi Web)</span><span class="sxs-lookup"><span data-stu-id="9584b-361">[Take Advantage of ASP.NET Built-in Features to Fend Off Web Attacks](https://msdn.microsoft.com/library/ms972969.aspx#securitybarriers_topic2)</span></span> |
| <span data-ttu-id="9584b-362">**Passaggi**</span><span class="sxs-lookup"><span data-stu-id="9584b-362">**Steps**</span></span> | <span data-ttu-id="9584b-363">Gli attacchi basati su richieste intersito false nelle applicazioni basate su Web Form possono essere mitigati impostando ViewStateUserKey su una stringa casuale diversa per ogni utente (ID utente o, meglio ancora, ID sessione).</span><span class="sxs-lookup"><span data-stu-id="9584b-363">CSRF attacks in WebForm based applications can be mitigated by setting ViewStateUserKey to a random string that varies for each user - user ID or, better yet, session ID.</span></span> <span data-ttu-id="9584b-364">Per diversi motivi tecnici e legati ai social network, l'ID sessione è molto più appropriato perché non è prevedibile, scade ed è diverso per ogni utente.</span><span class="sxs-lookup"><span data-stu-id="9584b-364">For a number of technical and social reasons, session ID is a much better fit because a session ID is unpredictable, times out, and varies on a per-user basis.</span></span>|

### <a name="example"></a><span data-ttu-id="9584b-365">Esempio</span><span class="sxs-lookup"><span data-stu-id="9584b-365">Example</span></span>
<span data-ttu-id="9584b-366">Ecco il codice che è necessario avere in tutte le pagine:</span><span class="sxs-lookup"><span data-stu-id="9584b-366">Here's the code you need to have in all of your pages:</span></span>
```C#
void Page_Init (object sender, EventArgs e) {
   ViewStateUserKey = Session.SessionID;
   :
}
```

## <span data-ttu-id="9584b-367"><a id="inactivity-lifetime"></a>Configurare una sessione per la durata dell'inattività</span><span class="sxs-lookup"><span data-stu-id="9584b-367"><a id="inactivity-lifetime"></a>Set up session for inactivity lifetime</span></span>

| <span data-ttu-id="9584b-368">Titolo</span><span class="sxs-lookup"><span data-stu-id="9584b-368">Title</span></span>                   | <span data-ttu-id="9584b-369">Dettagli</span><span class="sxs-lookup"><span data-stu-id="9584b-369">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="9584b-370">**Componente**</span><span class="sxs-lookup"><span data-stu-id="9584b-370">**Component**</span></span>               | <span data-ttu-id="9584b-371">Applicazione Web.</span><span class="sxs-lookup"><span data-stu-id="9584b-371">Web Application</span></span> | 
| <span data-ttu-id="9584b-372">**Fase SDL**</span><span class="sxs-lookup"><span data-stu-id="9584b-372">**SDL Phase**</span></span>               | <span data-ttu-id="9584b-373">Compilare</span><span class="sxs-lookup"><span data-stu-id="9584b-373">Build</span></span> |  
| <span data-ttu-id="9584b-374">**Tecnologie applicabili**</span><span class="sxs-lookup"><span data-stu-id="9584b-374">**Applicable Technologies**</span></span> | <span data-ttu-id="9584b-375">Generico</span><span class="sxs-lookup"><span data-stu-id="9584b-375">Generic</span></span> |
| <span data-ttu-id="9584b-376">**Attributes (Attributi) (Attributi)**</span><span class="sxs-lookup"><span data-stu-id="9584b-376">**Attributes**</span></span>              | <span data-ttu-id="9584b-377">N/D</span><span class="sxs-lookup"><span data-stu-id="9584b-377">N/A</span></span>  |
| <span data-ttu-id="9584b-378">**Riferimenti**</span><span class="sxs-lookup"><span data-stu-id="9584b-378">**References**</span></span>              | <span data-ttu-id="9584b-379">[Proprietà HttpSessionState.Timeout](https://msdn.microsoft.com/library/system.web.sessionstate.httpsessionstate.timeout(v=vs.110).aspx)</span><span class="sxs-lookup"><span data-stu-id="9584b-379">[HttpSessionState.Timeout Property](https://msdn.microsoft.com/library/system.web.sessionstate.httpsessionstate.timeout(v=vs.110).aspx)</span></span> |
| <span data-ttu-id="9584b-380">**Passaggi**</span><span class="sxs-lookup"><span data-stu-id="9584b-380">**Steps**</span></span> | <span data-ttu-id="9584b-381">Il timeout della sessione rappresenta l'evento che si verifica quando un utente non esegue alcuna azione in un sito Web durante un intervallo (definito dal server Web).</span><span class="sxs-lookup"><span data-stu-id="9584b-381">Session timeout represents the event occurring when a user does not perform any action on a web site during a interval (defined by web server).</span></span> <span data-ttu-id="9584b-382">L'evento sul lato server imposta lo stato della sessione utente come "non valida" (ad esempio, "non più usata") e indica al server Web di eliminarla definitivamente (eliminando tutti i dati contenuti).</span><span class="sxs-lookup"><span data-stu-id="9584b-382">The event, on server side, change the status of the user session to 'invalid' (for example  "not used anymore") and instruct the web server to destroy it (deleting all data contained into it).</span></span> <span data-ttu-id="9584b-383">L'esempio di codice seguente imposta l'attributo del timeout della sessione su 15 minuti nel file Web.config.</span><span class="sxs-lookup"><span data-stu-id="9584b-383">The following code example sets the timeout session attribute to 15 minutes in the Web.config file.</span></span>|

### <a name="example"></a><span data-ttu-id="9584b-384">Esempio</span><span class="sxs-lookup"><span data-stu-id="9584b-384">Example</span></span>
<span data-ttu-id="9584b-385">``\`Codice XML <configuration> <system.web> <sessionState mode="InProc" cookieless="true" timeout="15" /> </system.web> </configuration></span><span class="sxs-lookup"><span data-stu-id="9584b-385">``\`XML code <configuration> <system.web> <sessionState mode="InProc" cookieless="true" timeout="15" /> </system.web> </configuration></span></span>
```

## <a id="threat-detection"></a>Enable Threat detection on Azure SQL
```

| <span data-ttu-id="9584b-386">Titolo</span><span class="sxs-lookup"><span data-stu-id="9584b-386">Title</span></span>                   | <span data-ttu-id="9584b-387">Dettagli</span><span class="sxs-lookup"><span data-stu-id="9584b-387">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="9584b-388">**Componente**</span><span class="sxs-lookup"><span data-stu-id="9584b-388">**Component**</span></span>               | <span data-ttu-id="9584b-389">Applicazione Web.</span><span class="sxs-lookup"><span data-stu-id="9584b-389">Web Application</span></span> | 
| <span data-ttu-id="9584b-390">**Fase SDL**</span><span class="sxs-lookup"><span data-stu-id="9584b-390">**SDL Phase**</span></span>               | <span data-ttu-id="9584b-391">Compilare</span><span class="sxs-lookup"><span data-stu-id="9584b-391">Build</span></span> |  
| <span data-ttu-id="9584b-392">**Tecnologie applicabili**</span><span class="sxs-lookup"><span data-stu-id="9584b-392">**Applicable Technologies**</span></span> | <span data-ttu-id="9584b-393">Web Form</span><span class="sxs-lookup"><span data-stu-id="9584b-393">Web Forms</span></span> |
| <span data-ttu-id="9584b-394">**Attributes (Attributi) (Attributi)**</span><span class="sxs-lookup"><span data-stu-id="9584b-394">**Attributes**</span></span>              | <span data-ttu-id="9584b-395">N/D</span><span class="sxs-lookup"><span data-stu-id="9584b-395">N/A</span></span>  |
| <span data-ttu-id="9584b-396">**Riferimenti**</span><span class="sxs-lookup"><span data-stu-id="9584b-396">**References**</span></span>              | <span data-ttu-id="9584b-397">[Elemento forms per authentication (schema delle impostazioni ASP.NET)](https://msdn.microsoft.com/library/1d3t3c61(v=vs.100).aspx)</span><span class="sxs-lookup"><span data-stu-id="9584b-397">[forms Element for authentication (ASP.NET Settings Schema)](https://msdn.microsoft.com/library/1d3t3c61(v=vs.100).aspx)</span></span> |
| <span data-ttu-id="9584b-398">**Passaggi**</span><span class="sxs-lookup"><span data-stu-id="9584b-398">**Steps**</span></span> | <span data-ttu-id="9584b-399">Impostare il timeout del cookie del ticket di autenticazione basata su form su 15 minuti.</span><span class="sxs-lookup"><span data-stu-id="9584b-399">Set the Forms Authentication Ticket cookie timeout to 15 minutes</span></span>|

### <a name="example"></a><span data-ttu-id="9584b-400">Esempio</span><span class="sxs-lookup"><span data-stu-id="9584b-400">Example</span></span>
<span data-ttu-id="9584b-401">``\`Codice XML <forms  name=".ASPXAUTH" loginUrl="login.aspx"  defaultUrl="default.aspx" protection="All" timeout="15" path="/" requireSSL="true" slidingExpiration="true"/>
</forms></span><span class="sxs-lookup"><span data-stu-id="9584b-401">``\`XML code <forms  name=".ASPXAUTH" loginUrl="login.aspx"  defaultUrl="default.aspx" protection="All" timeout="15" path="/" requireSSL="true" slidingExpiration="true"/>
</forms></span></span>
```

| Title                   | Details      |
| ----------------------- | ------------ |
| **Component**               | Web Application | 
| **SDL Phase**               | Build |  
| **Applicable Technologies** | Web Forms, MVC5 |
| **Attributes**              | EnvironmentType - OnPrem |
| **References**              | [asdeqa](https://skf.azurewebsites.net/Mitigations/Details/wefr) |
| **Steps** | When the web application is Relying Party and ADFS is the STS, the lifetime of the authentication cookies - FedAuth tokens - can be set by the following configuration in web.config:|

### Example
```XML
  <system.identityModel.services>
    <federationConfiguration>
      <!-- Set requireSsl=true; domain=application domain name used by FedAuth cookies (Ex: .gdinfra.com); -->
      <cookieHandler requireSsl="true" persistentSessionLifetime="0.0:15:0" />
      <!-- Set requireHttps=true; -->
      <wsFederation passiveRedirectEnabled="true" issuer="http://localhost:39529/" realm="https://localhost:44302/" reply="https://localhost:44302/" requireHttps="true"/>
      <!--
      Use the code below to enable encryption-decryption of claims received from ADFS. Thumbprint value varies based on the certificate being used.
      <serviceCertificate>
        <certificateReference findValue="4FBBBA33A1D11A9022A5BF3492FF83320007686A" storeLocation="LocalMachine" storeName="My" x509FindType="FindByThumbprint" />
      </serviceCertificate>
      -->
    </federationConfiguration>
  </system.identityModel.services>
```

### <a name="example"></a><span data-ttu-id="9584b-402">Esempio</span><span class="sxs-lookup"><span data-stu-id="9584b-402">Example</span></span>
<span data-ttu-id="9584b-403">Anche la durata del token dell'attestazione SAML rilasciato da AD FS deve essere impostato su 15 minuti, eseguendo il comando di PowerShell seguente nel server AD FS:</span><span class="sxs-lookup"><span data-stu-id="9584b-403">Also the ADFS issued SAML claim token's lifetime should be set to 15 minutes, by executing the following powershell command on the ADFS server:</span></span>
```C#
Set-ADFSRelyingPartyTrust -TargetName “<RelyingPartyWebApp>” -ClaimsProviderName @(“Active Directory”) -TokenLifetime 15 -AlwaysRequireAuthentication $true
```

## <span data-ttu-id="9584b-404"><a id="proper-app-logout"></a>Implementare la disconnessione appropriata dall'applicazione</span><span class="sxs-lookup"><span data-stu-id="9584b-404"><a id="proper-app-logout"></a>Implement proper logout from the application</span></span>

| <span data-ttu-id="9584b-405">Titolo</span><span class="sxs-lookup"><span data-stu-id="9584b-405">Title</span></span>                   | <span data-ttu-id="9584b-406">Dettagli</span><span class="sxs-lookup"><span data-stu-id="9584b-406">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="9584b-407">**Componente**</span><span class="sxs-lookup"><span data-stu-id="9584b-407">**Component**</span></span>               | <span data-ttu-id="9584b-408">Applicazione Web.</span><span class="sxs-lookup"><span data-stu-id="9584b-408">Web Application</span></span> | 
| <span data-ttu-id="9584b-409">**Fase SDL**</span><span class="sxs-lookup"><span data-stu-id="9584b-409">**SDL Phase**</span></span>               | <span data-ttu-id="9584b-410">Compilare</span><span class="sxs-lookup"><span data-stu-id="9584b-410">Build</span></span> |  
| <span data-ttu-id="9584b-411">**Tecnologie applicabili**</span><span class="sxs-lookup"><span data-stu-id="9584b-411">**Applicable Technologies**</span></span> | <span data-ttu-id="9584b-412">Generico</span><span class="sxs-lookup"><span data-stu-id="9584b-412">Generic</span></span> |
| <span data-ttu-id="9584b-413">**Attributes (Attributi) (Attributi)**</span><span class="sxs-lookup"><span data-stu-id="9584b-413">**Attributes**</span></span>              | <span data-ttu-id="9584b-414">N/D</span><span class="sxs-lookup"><span data-stu-id="9584b-414">N/A</span></span>  |
| <span data-ttu-id="9584b-415">**Riferimenti**</span><span class="sxs-lookup"><span data-stu-id="9584b-415">**References**</span></span>              | <span data-ttu-id="9584b-416">N/D</span><span class="sxs-lookup"><span data-stu-id="9584b-416">N/A</span></span>  |
| <span data-ttu-id="9584b-417">**Passaggi**</span><span class="sxs-lookup"><span data-stu-id="9584b-417">**Steps**</span></span> | <span data-ttu-id="9584b-418">Eseguire la disconnessione appropriata dall'applicazione, quando l'utente fa clic sul pulsante di disconnessione.</span><span class="sxs-lookup"><span data-stu-id="9584b-418">Perform proper Sign Out from the application, when user presses log out button.</span></span> <span data-ttu-id="9584b-419">Durante la disconnessione, l'applicazione deve eliminare definitivamente la sessione dell'utente e anche reimpostare e rendere null il valore del cookie della sessione, oltre a reimpostare e rendere null il valore del cookie di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="9584b-419">Upon logout, application should destroy user's session, and also reset and nullify session cookie value, along with resetting and nullifying authentication cookie value.</span></span> <span data-ttu-id="9584b-420">Quando più sessioni sono collegate a una singola identità utente, è anche necessario terminarle collettivamente sul lato server al momento del timeout o della disconnessione.</span><span class="sxs-lookup"><span data-stu-id="9584b-420">Also, when multiple sessions are tied to a single user identity, they must be collectively terminated on the server side at timeout or logout.</span></span> <span data-ttu-id="9584b-421">Assicurarsi infine che la funzionalità di disconnessione sia disponibile in ogni pagina.</span><span class="sxs-lookup"><span data-stu-id="9584b-421">Lastly, ensure that Logout functionality is available on every page.</span></span> |

## <span data-ttu-id="9584b-422"><a id="csrf-api"></a>Mitigare il rischio di attacchi basati su richieste intersito false nelle API Web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="9584b-422"><a id="csrf-api"></a>Mitigate against Cross-Site Request Forgery (CSRF) attacks on ASP.NET Web APIs</span></span>

| <span data-ttu-id="9584b-423">Titolo</span><span class="sxs-lookup"><span data-stu-id="9584b-423">Title</span></span>                   | <span data-ttu-id="9584b-424">Dettagli</span><span class="sxs-lookup"><span data-stu-id="9584b-424">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="9584b-425">**Componente**</span><span class="sxs-lookup"><span data-stu-id="9584b-425">**Component**</span></span>               | <span data-ttu-id="9584b-426">API Web</span><span class="sxs-lookup"><span data-stu-id="9584b-426">Web API</span></span> | 
| <span data-ttu-id="9584b-427">**Fase SDL**</span><span class="sxs-lookup"><span data-stu-id="9584b-427">**SDL Phase**</span></span>               | <span data-ttu-id="9584b-428">Compilare</span><span class="sxs-lookup"><span data-stu-id="9584b-428">Build</span></span> |  
| <span data-ttu-id="9584b-429">**Tecnologie applicabili**</span><span class="sxs-lookup"><span data-stu-id="9584b-429">**Applicable Technologies**</span></span> | <span data-ttu-id="9584b-430">Generico</span><span class="sxs-lookup"><span data-stu-id="9584b-430">Generic</span></span> |
| <span data-ttu-id="9584b-431">**Attributes (Attributi) (Attributi)**</span><span class="sxs-lookup"><span data-stu-id="9584b-431">**Attributes**</span></span>              | <span data-ttu-id="9584b-432">N/D</span><span class="sxs-lookup"><span data-stu-id="9584b-432">N/A</span></span>  |
| <span data-ttu-id="9584b-433">**Riferimenti**</span><span class="sxs-lookup"><span data-stu-id="9584b-433">**References**</span></span>              | <span data-ttu-id="9584b-434">N/D</span><span class="sxs-lookup"><span data-stu-id="9584b-434">N/A</span></span>  |
| <span data-ttu-id="9584b-435">**Passaggi**</span><span class="sxs-lookup"><span data-stu-id="9584b-435">**Steps**</span></span> | <span data-ttu-id="9584b-436">Richiesta intersito falsa (CSRF o XSRF) è un tipo di attacco in cui un utente malintenzionato può eseguire azioni nel contesto di protezione della sessione stabilita di un utente diverso in un sito web.</span><span class="sxs-lookup"><span data-stu-id="9584b-436">Cross-site request forgery (CSRF or XSRF) is a type of attack in which an attacker can carry out actions in the security context of a different user's established session on a web site.</span></span> <span data-ttu-id="9584b-437">L'obiettivo è quello di modificare o eliminare il contenuto, se il sito web di destinazione si affida esclusivamente ai cookie di sessione per autenticare la richiesta ricevuta.</span><span class="sxs-lookup"><span data-stu-id="9584b-437">The goal is to modify or delete content, if the targeted web site relies exclusively on session cookies to authenticate received request.</span></span> <span data-ttu-id="9584b-438">Un utente malintenzionato potrebbe sfruttare questa vulnerabilità acquisendo il browser di un altro utente per caricare un URL con un comando da un sito vulnerabile a cui l'utente è già connesso.</span><span class="sxs-lookup"><span data-stu-id="9584b-438">An attacker could exploit this vulnerability by getting a different user's browser to load a URL with a command from a vulnerable site on which the user is already logged in.</span></span> <span data-ttu-id="9584b-439">Un utente malintenzionato può raggiungere questo scopo in diversi modi, ad esempio ospitando un sito Web diverso che carica una risorsa dal server vulnerabile o spingendo l'utente a fare clic su un collegamento.</span><span class="sxs-lookup"><span data-stu-id="9584b-439">There are many ways for an attacker to do that, such as by hosting a different web site that loads a resource from the vulnerable server, or getting the user to click a link.</span></span> <span data-ttu-id="9584b-440">L'attacco può essere evitato se il server invia un token aggiuntivo al client, richiede al client di includere tale token in tutte le richieste future e verifica che tutte le richieste future includano un token relativo alla sessione corrente, ad esempio usando AntiForgeryToken o ViewState di ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="9584b-440">The attack can be prevented if the server sends an additional token to the client, requires the client to include that token in all future requests, and verifies that all future requests include a token that pertains to the current session, such as by using the ASP.NET AntiForgeryToken or ViewState.</span></span> |

| <span data-ttu-id="9584b-441">Titolo</span><span class="sxs-lookup"><span data-stu-id="9584b-441">Title</span></span>                   | <span data-ttu-id="9584b-442">Dettagli</span><span class="sxs-lookup"><span data-stu-id="9584b-442">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="9584b-443">**Componente**</span><span class="sxs-lookup"><span data-stu-id="9584b-443">**Component**</span></span>               | <span data-ttu-id="9584b-444">API Web</span><span class="sxs-lookup"><span data-stu-id="9584b-444">Web API</span></span> | 
| <span data-ttu-id="9584b-445">**Fase SDL**</span><span class="sxs-lookup"><span data-stu-id="9584b-445">**SDL Phase**</span></span>               | <span data-ttu-id="9584b-446">Compilare</span><span class="sxs-lookup"><span data-stu-id="9584b-446">Build</span></span> |  
| <span data-ttu-id="9584b-447">**Tecnologie applicabili**</span><span class="sxs-lookup"><span data-stu-id="9584b-447">**Applicable Technologies**</span></span> | <span data-ttu-id="9584b-448">MVC 5, MVC 6</span><span class="sxs-lookup"><span data-stu-id="9584b-448">MVC5, MVC6</span></span> |
| <span data-ttu-id="9584b-449">**Attributes (Attributi) (Attributi)**</span><span class="sxs-lookup"><span data-stu-id="9584b-449">**Attributes**</span></span>              | <span data-ttu-id="9584b-450">N/D</span><span class="sxs-lookup"><span data-stu-id="9584b-450">N/A</span></span>  |
| <span data-ttu-id="9584b-451">**Riferimenti**</span><span class="sxs-lookup"><span data-stu-id="9584b-451">**References**</span></span>              | <span data-ttu-id="9584b-452">[Preventing Cross-Site Request Forgery (CSRF) Attacks in ASP.NET Web API](http://www.asp.net/web-api/overview/security/preventing-cross-site-request-forgery-csrf-attacks) (Prevenzione di attacchi basati su richieste intersito false nelle API Web ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="9584b-452">[Preventing Cross-Site Request Forgery (CSRF) Attacks in ASP.NET Web API](http://www.asp.net/web-api/overview/security/preventing-cross-site-request-forgery-csrf-attacks)</span></span> |
| <span data-ttu-id="9584b-453">**Passaggi**</span><span class="sxs-lookup"><span data-stu-id="9584b-453">**Steps**</span></span> | <span data-ttu-id="9584b-454">Prevenzione di richieste intersito false e AJAX: il token del form può rappresentare un problema per le richieste AJAX, perché una richiesta AJAX potrebbe inviare dati JSON, non dati in formato HTML.</span><span class="sxs-lookup"><span data-stu-id="9584b-454">Anti-CSRF and AJAX: The form token can be a problem for AJAX requests, because an AJAX request might send JSON data, not HTML form data.</span></span> <span data-ttu-id="9584b-455">Una soluzione consiste nell'inviare i token in un'intestazione HTTP personalizzata.</span><span class="sxs-lookup"><span data-stu-id="9584b-455">One solution is to send the tokens in a custom HTTP header.</span></span> <span data-ttu-id="9584b-456">Il codice seguente usa la sintassi Razor per generare i token e quindi li aggiunge a una richiesta AJAX.</span><span class="sxs-lookup"><span data-stu-id="9584b-456">The following code uses Razor syntax to generate the tokens, and then adds the tokens to an AJAX request.</span></span> |

### <a name="example"></a><span data-ttu-id="9584b-457">Esempio</span><span class="sxs-lookup"><span data-stu-id="9584b-457">Example</span></span>
```Javascript
<script>
    @functions{
        public string TokenHeaderValue()
        {
            string cookieToken, formToken;
            AntiForgery.GetTokens(null, out cookieToken, out formToken);
            return cookieToken + ":" + formToken;                
        }
    }
    $.ajax("api/values", {
        type: "post",
        contentType: "application/json",
        data: {  }, // JSON data goes here
        dataType: "json",
        headers: {
            'RequestVerificationToken': '@TokenHeaderValue()'
        }
    });
</script>
```

### <a name="example"></a><span data-ttu-id="9584b-458">Esempio</span><span class="sxs-lookup"><span data-stu-id="9584b-458">Example</span></span>
<span data-ttu-id="9584b-459">Quando si elabora la richiesta, estrarre i token dall'intestazione della richiesta.</span><span class="sxs-lookup"><span data-stu-id="9584b-459">When you process the request, extract the tokens from the request header.</span></span> <span data-ttu-id="9584b-460">Chiamare quindi il metodo AntiForgery.Validate per convalidare i token.</span><span class="sxs-lookup"><span data-stu-id="9584b-460">Then call the AntiForgery.Validate method to validate the tokens.</span></span> <span data-ttu-id="9584b-461">Il metodo Validate genera un'eccezione se i token non sono validi.</span><span class="sxs-lookup"><span data-stu-id="9584b-461">The Validate method throws an exception if the tokens are not valid.</span></span>
```C#
void ValidateRequestHeader(HttpRequestMessage request)
{
    string cookieToken = "";
    string formToken = "";

    IEnumerable<string> tokenHeaders;
    if (request.Headers.TryGetValues("RequestVerificationToken", out tokenHeaders))
    {
        string[] tokens = tokenHeaders.First().Split(':');
        if (tokens.Length == 2)
        {
            cookieToken = tokens[0].Trim();
            formToken = tokens[1].Trim();
        }
    }
    AntiForgery.Validate(cookieToken, formToken);
}
```

### <a name="example"></a><span data-ttu-id="9584b-462">Esempio</span><span class="sxs-lookup"><span data-stu-id="9584b-462">Example</span></span>
<span data-ttu-id="9584b-463">Form ASP.NET MVC e contro le richieste intersito: usare il metodo helper AntiForgeryToken in Views. Inserire Html.AntiForgeryToken() nel form, ad esempio,</span><span class="sxs-lookup"><span data-stu-id="9584b-463">Anti-CSRF and ASP.NET MVC forms - Use the AntiForgeryToken helper method on Views; put an Html.AntiForgeryToken() into the form, for example,</span></span>
```C#
@using (Html.BeginForm("UserProfile", "SubmitUpdate")) { 
    @Html.ValidationSummary(true) 
    @Html.AntiForgeryToken()
    <fieldset> 
}
```

### <a name="example"></a><span data-ttu-id="9584b-464">Esempio</span><span class="sxs-lookup"><span data-stu-id="9584b-464">Example</span></span>
<span data-ttu-id="9584b-465">Nell'esempio precedente verrà generato un output simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="9584b-465">The example above will output something like the following:</span></span>
```C#
<form action="/UserProfile/SubmitUpdate" method="post">
    <input name="__RequestVerificationToken" type="hidden" value="saTFWpkKN0BYazFtN6c4YbZAmsEwG0srqlUqqloi/fVgeV2ciIFVmelvzwRZpArs" />
    <!-- rest of form goes here -->
</form>
```

### <a name="example"></a><span data-ttu-id="9584b-466">Esempio</span><span class="sxs-lookup"><span data-stu-id="9584b-466">Example</span></span>
<span data-ttu-id="9584b-467">Html.AntiForgeryToken() assegna contemporaneamente al visitatore un cookie denominato __RequestVerificationToken, con lo stesso valore del valore nascosto casuale illustrato sopra.</span><span class="sxs-lookup"><span data-stu-id="9584b-467">At the same time, Html.AntiForgeryToken() gives the visitor a cookie called __RequestVerificationToken, with the same value as the random hidden value shown above.</span></span> <span data-ttu-id="9584b-468">Per convalidare un post del form in ingresso, aggiungere quindi il filtro [ValidateAntiForgeryToken] al metodo azione di destinazione.</span><span class="sxs-lookup"><span data-stu-id="9584b-468">Next, to validate an incoming form post, add the [ValidateAntiForgeryToken] filter to the target action method.</span></span> <span data-ttu-id="9584b-469">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="9584b-469">For example:</span></span>
```
[ValidateAntiForgeryToken]
public ViewResult SubmitUpdate()
{
// ... etc.
}
```
<span data-ttu-id="9584b-470">Filtro di autorizzazione che controlla che:</span><span class="sxs-lookup"><span data-stu-id="9584b-470">Authorization filter that checks that:</span></span>
* <span data-ttu-id="9584b-471">La richiesta in ingresso abbia un cookie denominato __RequestVerificationToken.</span><span class="sxs-lookup"><span data-stu-id="9584b-471">The incoming request has a cookie called __RequestVerificationToken</span></span>
* <span data-ttu-id="9584b-472">La richiesta in ingresso ha un cookie `Request.Form` denominato __RequestVerificationToken</span><span class="sxs-lookup"><span data-stu-id="9584b-472">The incoming request has a `Request.Form` entry called __RequestVerificationToken</span></span>
* <span data-ttu-id="9584b-473">Questi valori del cookie e di `Request.Form` corrispondono. Presumendo che sia tutto a posto, la richiesta viene completata normalmente.</span><span class="sxs-lookup"><span data-stu-id="9584b-473">These cookie and `Request.Form` values match Assuming all is well, the request goes through as normal.</span></span> <span data-ttu-id="9584b-474">In caso contrario, si verifica un errore di autorizzazione e viene visualizzato il messaggio "Token antifalsificazione non specificato o non valido".</span><span class="sxs-lookup"><span data-stu-id="9584b-474">But if not, then an authorization failure with message “A required anti-forgery token was not supplied or was invalid”.</span></span>

| <span data-ttu-id="9584b-475">Titolo</span><span class="sxs-lookup"><span data-stu-id="9584b-475">Title</span></span>                   | <span data-ttu-id="9584b-476">Dettagli</span><span class="sxs-lookup"><span data-stu-id="9584b-476">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="9584b-477">**Componente**</span><span class="sxs-lookup"><span data-stu-id="9584b-477">**Component**</span></span>               | <span data-ttu-id="9584b-478">API Web</span><span class="sxs-lookup"><span data-stu-id="9584b-478">Web API</span></span> | 
| <span data-ttu-id="9584b-479">**Fase SDL**</span><span class="sxs-lookup"><span data-stu-id="9584b-479">**SDL Phase**</span></span>               | <span data-ttu-id="9584b-480">Compilare</span><span class="sxs-lookup"><span data-stu-id="9584b-480">Build</span></span> |  
| <span data-ttu-id="9584b-481">**Tecnologie applicabili**</span><span class="sxs-lookup"><span data-stu-id="9584b-481">**Applicable Technologies**</span></span> | <span data-ttu-id="9584b-482">MVC 5, MVC 6</span><span class="sxs-lookup"><span data-stu-id="9584b-482">MVC5, MVC6</span></span> |
| <span data-ttu-id="9584b-483">**Attributes (Attributi) (Attributi)**</span><span class="sxs-lookup"><span data-stu-id="9584b-483">**Attributes**</span></span>              | <span data-ttu-id="9584b-484">Provider di identità: AD FS, provider di identità: Azure AD</span><span class="sxs-lookup"><span data-stu-id="9584b-484">Identity Provider - ADFS, Identity Provider - Azure AD</span></span> |
| <span data-ttu-id="9584b-485">**Riferimenti**</span><span class="sxs-lookup"><span data-stu-id="9584b-485">**References**</span></span>              | <span data-ttu-id="9584b-486">[Secure a Web API with Individual Accounts and Local Login in ASP.NET Web API 2.2](http://www.asp.net/web-api/overview/security/individual-accounts-in-web-api) (Proteggere un'API Web con account singoli e account di accesso locale in API Web ASP.NET 2.2)</span><span class="sxs-lookup"><span data-stu-id="9584b-486">[Secure a Web API with Individual Accounts and Local Login in ASP.NET Web API 2.2](http://www.asp.net/web-api/overview/security/individual-accounts-in-web-api)</span></span> |
| <span data-ttu-id="9584b-487">**Passaggi**</span><span class="sxs-lookup"><span data-stu-id="9584b-487">**Steps**</span></span> | <span data-ttu-id="9584b-488">Se l'API Web viene protetta con OAuth 2.0, è previsto un token di connessione nell'intestazione della richiesta di autorizzazione e l'accesso alla richiesta viene concesso solo se il token è valido.</span><span class="sxs-lookup"><span data-stu-id="9584b-488">If the Web API is secured using OAuth 2.0, then it expects a bearer token in Authorization request header and grants access to the request only if the token is valid.</span></span> <span data-ttu-id="9584b-489">Diversamente dall'autenticazione basata su cookie, i browser non allegano i token di connessione alle richieste.</span><span class="sxs-lookup"><span data-stu-id="9584b-489">Unlike cookie based authentication, browsers do not attach the bearer tokens to requests.</span></span> <span data-ttu-id="9584b-490">Il client richiedente deve allegare esplicitamente il token di connessione nell'intestazione della richiesta.</span><span class="sxs-lookup"><span data-stu-id="9584b-490">The requesting client needs to explicitly attach the bearer token in the request header.</span></span> <span data-ttu-id="9584b-491">Per le API Web ASP.NET protette con OAuth 2.0, i token di connessione vengono quindi considerati una difesa contro gli attacchi basati su richieste intersito false.</span><span class="sxs-lookup"><span data-stu-id="9584b-491">Therefore, for ASP.NET Web APIs protected using OAuth 2.0, bearer tokens are considered as a defense against CSRF attacks.</span></span> <span data-ttu-id="9584b-492">Tenere presente che, se la parte MVC dell'applicazione usa l'autenticazione basata su form (ad esempio, usa i cookie), dall'app Web MVC devono essere usati token antifalsificazione.</span><span class="sxs-lookup"><span data-stu-id="9584b-492">Please note that if the MVC portion of the application uses forms authentication (i.e., uses cookies), anti-forgery tokens have to be used by the MVC web app.</span></span> |

### <a name="example"></a><span data-ttu-id="9584b-493">Esempio</span><span class="sxs-lookup"><span data-stu-id="9584b-493">Example</span></span>
<span data-ttu-id="9584b-494">All'API Web deve essere comunicato di basarsi SOLO sui token di connessione e non sui cookie.</span><span class="sxs-lookup"><span data-stu-id="9584b-494">The Web API has to be informed to rely ONLY on bearer tokens and not on cookies.</span></span> <span data-ttu-id="9584b-495">È possibile seguire la configurazione nel metodo `WebApiConfig.Register`: ``\`C-Sharp code config.SuppressDefaultHostAuthentication(); config.Filters.Add(new HostAuthenticationFilter(OAuthDefaults.AuthenticationType));</span><span class="sxs-lookup"><span data-stu-id="9584b-495">It can be done by the following configuration in `WebApiConfig.Register` method: ``\`C-Sharp code config.SuppressDefaultHostAuthentication(); config.Filters.Add(new HostAuthenticationFilter(OAuthDefaults.AuthenticationType));</span></span>
```
The SuppressDefaultHostAuthentication method tells Web API to ignore any authentication that happens before the request reaches the Web API pipeline, either by IIS or by OWIN middleware. That way, we can restrict Web API to authenticate only using bearer tokens.