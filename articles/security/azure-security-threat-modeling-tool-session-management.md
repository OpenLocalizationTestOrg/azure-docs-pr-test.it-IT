---
title: Gestione - di modellazione strumento Microsoft Threat - Azure aaaSession | Documenti Microsoft
description: misure di attenuazione esposte in hello strumento di modellazione del rischio di minacce per la
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
ms.openlocfilehash: 915ffae3f775ca6902fcfb93e7e1952ce85612f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="security-frame-session-management--articles"></a><span data-ttu-id="d2131-103">Infrastruttura di sicurezza: gestione della sessione - Articoli</span><span class="sxs-lookup"><span data-stu-id="d2131-103">Security Frame: Session Management | Articles</span></span> 
| <span data-ttu-id="d2131-104">Prodotto o servizio</span><span class="sxs-lookup"><span data-stu-id="d2131-104">Product/Service</span></span> | <span data-ttu-id="d2131-105">Articolo</span><span class="sxs-lookup"><span data-stu-id="d2131-105">Article</span></span> |
| --------------- | ------- |
| <span data-ttu-id="d2131-106">**Azure AD**</span><span class="sxs-lookup"><span data-stu-id="d2131-106">**Azure AD**</span></span>    | <ul><li>[<span data-ttu-id="d2131-107">Implementare la disconnessione appropriata con i metodi ADAL quando si usa Azure AD</span><span class="sxs-lookup"><span data-stu-id="d2131-107">Implement proper logout using ADAL methods when using Azure AD</span></span>](#logout-adal)</li></ul> |
| <span data-ttu-id="d2131-108">Dispositivo IoT</span><span class="sxs-lookup"><span data-stu-id="d2131-108">IoT Device</span></span> | <ul><li>[<span data-ttu-id="d2131-109">Usare durate limitate per i token di firma di accesso condiviso generati</span><span class="sxs-lookup"><span data-stu-id="d2131-109">Use finite lifetimes for generated SaS tokens</span></span>](#finite-tokens)</li></ul> |
| <span data-ttu-id="d2131-110">**Azure Document DB**</span><span class="sxs-lookup"><span data-stu-id="d2131-110">**Azure Document DB**</span></span> | <ul><li>[<span data-ttu-id="d2131-111">Usare durate minime per i token delle risorse generati</span><span class="sxs-lookup"><span data-stu-id="d2131-111">Use minimum token lifetimes for generated Resource tokens</span></span>](#resource-tokens)</li></ul> |
| <span data-ttu-id="d2131-112">**AD FS**</span><span class="sxs-lookup"><span data-stu-id="d2131-112">**ADFS**</span></span> | <ul><li>[<span data-ttu-id="d2131-113">Implementare la disconnessione appropriata con i metodi WsFederation quando si usa AD FS</span><span class="sxs-lookup"><span data-stu-id="d2131-113">Implement proper logout using WsFederation methods when using ADFS</span></span>](#wsfederation-logout)</li></ul> |
| <span data-ttu-id="d2131-114">**Identity Server**</span><span class="sxs-lookup"><span data-stu-id="d2131-114">**Identity Server**</span></span> | <ul><li>[<span data-ttu-id="d2131-115">Implementare la disconnessione appropriata quando si usa Identity Server</span><span class="sxs-lookup"><span data-stu-id="d2131-115">Implement proper logout when using Identity Server</span></span>](#proper-logout)</li></ul> |
| <span data-ttu-id="d2131-116">**Applicazione Web**</span><span class="sxs-lookup"><span data-stu-id="d2131-116">**Web Application**</span></span> | <ul><li>[<span data-ttu-id="d2131-117">Le applicazioni disponibili tramite HTTPS devono usare cookie sicuri</span><span class="sxs-lookup"><span data-stu-id="d2131-117">Applications available over HTTPS must use secure cookies</span></span>](#https-secure-cookies)</li><li>[<span data-ttu-id="d2131-118">Tutte le applicazioni basate su http devono specificare solo http per la definizione dei cookie</span><span class="sxs-lookup"><span data-stu-id="d2131-118">All http based application should specify http only for cookie definition</span></span>](#cookie-definition)</li><li>[<span data-ttu-id="d2131-119">Mitigare il rischio di attacchi basati su richieste intersito false nelle pagine Web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="d2131-119">Mitigate against Cross-Site Request Forgery (CSRF) attacks on ASP.NET web pages</span></span>](#csrf-asp)</li><li>[<span data-ttu-id="d2131-120">Configurare una sessione per la durata dell'inattività</span><span class="sxs-lookup"><span data-stu-id="d2131-120">Set up session for inactivity lifetime</span></span>](#inactivity-lifetime)</li><li>[<span data-ttu-id="d2131-121">Implementa la disconnessione appropriata da un'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="d2131-121">Implement proper logout from hello application</span></span>](#proper-app-logout)</li></ul> |
| <span data-ttu-id="d2131-122">**API Web**</span><span class="sxs-lookup"><span data-stu-id="d2131-122">**Web API**</span></span> | <ul><li>[<span data-ttu-id="d2131-123">Mitigare il rischio di attacchi basati su richieste intersito false nelle API Web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="d2131-123">Mitigate against Cross-Site Request Forgery (CSRF) attacks on ASP.NET Web APIs</span></span>](#csrf-api)</li></ul> |

## <span data-ttu-id="d2131-124"><a id="logout-adal"></a>Implementare la disconnessione appropriata con i metodi ADAL quando si usa Azure AD</span><span class="sxs-lookup"><span data-stu-id="d2131-124"><a id="logout-adal"></a>Implement proper logout using ADAL methods when using Azure AD</span></span>

| <span data-ttu-id="d2131-125">Titolo</span><span class="sxs-lookup"><span data-stu-id="d2131-125">Title</span></span>                   | <span data-ttu-id="d2131-126">Dettagli</span><span class="sxs-lookup"><span data-stu-id="d2131-126">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="d2131-127">**Componente**</span><span class="sxs-lookup"><span data-stu-id="d2131-127">**Component**</span></span>               | <span data-ttu-id="d2131-128">Azure AD</span><span class="sxs-lookup"><span data-stu-id="d2131-128">Azure AD</span></span> | 
| <span data-ttu-id="d2131-129">**Fase SDL**</span><span class="sxs-lookup"><span data-stu-id="d2131-129">**SDL Phase**</span></span>               | <span data-ttu-id="d2131-130">Compilare</span><span class="sxs-lookup"><span data-stu-id="d2131-130">Build</span></span> |  
| <span data-ttu-id="d2131-131">**Tecnologie applicabili**</span><span class="sxs-lookup"><span data-stu-id="d2131-131">**Applicable Technologies**</span></span> | <span data-ttu-id="d2131-132">Generico</span><span class="sxs-lookup"><span data-stu-id="d2131-132">Generic</span></span> |
| <span data-ttu-id="d2131-133">**Attributes (Attributi) (Attributi)**</span><span class="sxs-lookup"><span data-stu-id="d2131-133">**Attributes**</span></span>              | <span data-ttu-id="d2131-134">N/D</span><span class="sxs-lookup"><span data-stu-id="d2131-134">N/A</span></span>  |
| <span data-ttu-id="d2131-135">**Riferimenti**</span><span class="sxs-lookup"><span data-stu-id="d2131-135">**References**</span></span>              | <span data-ttu-id="d2131-136">N/D</span><span class="sxs-lookup"><span data-stu-id="d2131-136">N/A</span></span>  |
| <span data-ttu-id="d2131-137">**Passaggi**</span><span class="sxs-lookup"><span data-stu-id="d2131-137">**Steps**</span></span> | <span data-ttu-id="d2131-138">Se un'applicazione hello si basa sul token di accesso rilasciato da Azure AD, è necessario chiamare gestore eventi di disconnessione hello</span><span class="sxs-lookup"><span data-stu-id="d2131-138">If hello application relies on access token issued by Azure AD, hello logout event handler should call</span></span> |

### <a name="example"></a><span data-ttu-id="d2131-139">Esempio</span><span class="sxs-lookup"><span data-stu-id="d2131-139">Example</span></span>
```C#
HttpContext.GetOwinContext().Authentication.SignOut(OpenIdConnectAuthenticationDefaults.AuthenticationType, CookieAuthenticationDefaults.AuthenticationType)
```

### <a name="example"></a><span data-ttu-id="d2131-140">Esempio</span><span class="sxs-lookup"><span data-stu-id="d2131-140">Example</span></span>
<span data-ttu-id="d2131-141">Eliminerà anche definitivamente la sessione dell'utente chiamando il metodo Session.Abandon().</span><span class="sxs-lookup"><span data-stu-id="d2131-141">It should also destroy user's session by calling Session.Abandon() method.</span></span> <span data-ttu-id="d2131-142">Il metodo seguente illustra l'implementazione sicura della disconnessione utente:</span><span class="sxs-lookup"><span data-stu-id="d2131-142">Following method shows secure implementation of user logout:</span></span>
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

## <span data-ttu-id="d2131-143"><a id="finite-tokens"></a>Usare durate limitate per i token di firma di accesso condiviso generati</span><span class="sxs-lookup"><span data-stu-id="d2131-143"><a id="finite-tokens"></a>Use finite lifetimes for generated SaS tokens</span></span>

| <span data-ttu-id="d2131-144">Titolo</span><span class="sxs-lookup"><span data-stu-id="d2131-144">Title</span></span>                   | <span data-ttu-id="d2131-145">Dettagli</span><span class="sxs-lookup"><span data-stu-id="d2131-145">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="d2131-146">**Componente**</span><span class="sxs-lookup"><span data-stu-id="d2131-146">**Component**</span></span>               | <span data-ttu-id="d2131-147">Dispositivo IoT</span><span class="sxs-lookup"><span data-stu-id="d2131-147">IoT Device</span></span> | 
| <span data-ttu-id="d2131-148">**Fase SDL**</span><span class="sxs-lookup"><span data-stu-id="d2131-148">**SDL Phase**</span></span>               | <span data-ttu-id="d2131-149">Compilare</span><span class="sxs-lookup"><span data-stu-id="d2131-149">Build</span></span> |  
| <span data-ttu-id="d2131-150">**Tecnologie applicabili**</span><span class="sxs-lookup"><span data-stu-id="d2131-150">**Applicable Technologies**</span></span> | <span data-ttu-id="d2131-151">Generico</span><span class="sxs-lookup"><span data-stu-id="d2131-151">Generic</span></span> |
| <span data-ttu-id="d2131-152">**Attributes (Attributi) (Attributi)**</span><span class="sxs-lookup"><span data-stu-id="d2131-152">**Attributes**</span></span>              | <span data-ttu-id="d2131-153">N/D</span><span class="sxs-lookup"><span data-stu-id="d2131-153">N/A</span></span>  |
| <span data-ttu-id="d2131-154">**Riferimenti**</span><span class="sxs-lookup"><span data-stu-id="d2131-154">**References**</span></span>              | <span data-ttu-id="d2131-155">N/D</span><span class="sxs-lookup"><span data-stu-id="d2131-155">N/A</span></span>  |
| <span data-ttu-id="d2131-156">**Passaggi**</span><span class="sxs-lookup"><span data-stu-id="d2131-156">**Steps**</span></span> | <span data-ttu-id="d2131-157">I token di firma di accesso condiviso generati per l'autenticazione tooAzure IoT Hub dovrebbero avere un periodo di scadenza precisa.</span><span class="sxs-lookup"><span data-stu-id="d2131-157">SaS tokens generated for authenticating tooAzure IoT Hub should have a finite expiry period.</span></span> <span data-ttu-id="d2131-158">Mantenere hello SaS durata dei token tooa toolimit minimo hello tempo totale che possono essere riprodotte nel caso in cui i token hello risultano compromesse.</span><span class="sxs-lookup"><span data-stu-id="d2131-158">Keep hello SaS token lifetimes tooa minimum toolimit hello amount of time they can be replayed in case hello tokens are compromised.</span></span>|

## <span data-ttu-id="d2131-159"><a id="resource-tokens"></a>Usare durate minime per i token delle risorse generati</span><span class="sxs-lookup"><span data-stu-id="d2131-159"><a id="resource-tokens"></a>Use minimum token lifetimes for generated Resource tokens</span></span>

| <span data-ttu-id="d2131-160">Titolo</span><span class="sxs-lookup"><span data-stu-id="d2131-160">Title</span></span>                   | <span data-ttu-id="d2131-161">Dettagli</span><span class="sxs-lookup"><span data-stu-id="d2131-161">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="d2131-162">**Componente**</span><span class="sxs-lookup"><span data-stu-id="d2131-162">**Component**</span></span>               | <span data-ttu-id="d2131-163">Azure DocumentDB</span><span class="sxs-lookup"><span data-stu-id="d2131-163">Azure Document DB</span></span> | 
| <span data-ttu-id="d2131-164">**Fase SDL**</span><span class="sxs-lookup"><span data-stu-id="d2131-164">**SDL Phase**</span></span>               | <span data-ttu-id="d2131-165">Compilare</span><span class="sxs-lookup"><span data-stu-id="d2131-165">Build</span></span> |  
| <span data-ttu-id="d2131-166">**Tecnologie applicabili**</span><span class="sxs-lookup"><span data-stu-id="d2131-166">**Applicable Technologies**</span></span> | <span data-ttu-id="d2131-167">Generico</span><span class="sxs-lookup"><span data-stu-id="d2131-167">Generic</span></span> |
| <span data-ttu-id="d2131-168">**Attributes (Attributi) (Attributi)**</span><span class="sxs-lookup"><span data-stu-id="d2131-168">**Attributes**</span></span>              | <span data-ttu-id="d2131-169">N/D</span><span class="sxs-lookup"><span data-stu-id="d2131-169">N/A</span></span>  |
| <span data-ttu-id="d2131-170">**Riferimenti**</span><span class="sxs-lookup"><span data-stu-id="d2131-170">**References**</span></span>              | <span data-ttu-id="d2131-171">N/D</span><span class="sxs-lookup"><span data-stu-id="d2131-171">N/A</span></span>  |
| <span data-ttu-id="d2131-172">**Passaggi**</span><span class="sxs-lookup"><span data-stu-id="d2131-172">**Steps**</span></span> | <span data-ttu-id="d2131-173">Ridurre timespan hello del valore minimo tooa token risorsa richiesto.</span><span class="sxs-lookup"><span data-stu-id="d2131-173">Reduce hello timespan of resource token tooa minimum value required.</span></span> <span data-ttu-id="d2131-174">I token delle risorse hanno un intervallo di tempo valido predefinito di 1 ora.</span><span class="sxs-lookup"><span data-stu-id="d2131-174">Resource tokens have a default valid timespan of 1 hour.</span></span>|

## <span data-ttu-id="d2131-175"><a id="wsfederation-logout"></a>Implementare la disconnessione appropriata con i metodi WsFederation quando si usa AD FS</span><span class="sxs-lookup"><span data-stu-id="d2131-175"><a id="wsfederation-logout"></a>Implement proper logout using WsFederation methods when using ADFS</span></span>

| <span data-ttu-id="d2131-176">Titolo</span><span class="sxs-lookup"><span data-stu-id="d2131-176">Title</span></span>                   | <span data-ttu-id="d2131-177">Dettagli</span><span class="sxs-lookup"><span data-stu-id="d2131-177">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="d2131-178">**Componente**</span><span class="sxs-lookup"><span data-stu-id="d2131-178">**Component**</span></span>               | <span data-ttu-id="d2131-179">AD FS</span><span class="sxs-lookup"><span data-stu-id="d2131-179">ADFS</span></span> | 
| <span data-ttu-id="d2131-180">**Fase SDL**</span><span class="sxs-lookup"><span data-stu-id="d2131-180">**SDL Phase**</span></span>               | <span data-ttu-id="d2131-181">Compilare</span><span class="sxs-lookup"><span data-stu-id="d2131-181">Build</span></span> |  
| <span data-ttu-id="d2131-182">**Tecnologie applicabili**</span><span class="sxs-lookup"><span data-stu-id="d2131-182">**Applicable Technologies**</span></span> | <span data-ttu-id="d2131-183">Generico</span><span class="sxs-lookup"><span data-stu-id="d2131-183">Generic</span></span> |
| <span data-ttu-id="d2131-184">**Attributes (Attributi) (Attributi)**</span><span class="sxs-lookup"><span data-stu-id="d2131-184">**Attributes**</span></span>              | <span data-ttu-id="d2131-185">N/D</span><span class="sxs-lookup"><span data-stu-id="d2131-185">N/A</span></span>  |
| <span data-ttu-id="d2131-186">**Riferimenti**</span><span class="sxs-lookup"><span data-stu-id="d2131-186">**References**</span></span>              | <span data-ttu-id="d2131-187">N/D</span><span class="sxs-lookup"><span data-stu-id="d2131-187">N/A</span></span>  |
| <span data-ttu-id="d2131-188">**Passaggi**</span><span class="sxs-lookup"><span data-stu-id="d2131-188">**Steps**</span></span> | <span data-ttu-id="d2131-189">Se un'applicazione hello si basa sul token di servizio token di sicurezza emesso da ADFS, gestore eventi di disconnessione hello deve chiamare WSFederationAuthenticationModule.FederatedSignOut() metodo toolog utente hello.</span><span class="sxs-lookup"><span data-stu-id="d2131-189">If hello application relies on STS token issued by ADFS, hello logout event handler should call WSFederationAuthenticationModule.FederatedSignOut() method toolog out hello user.</span></span> <span data-ttu-id="d2131-190">Anche hello sessione corrente deve essere eliminato e valore del token di sessione hello deve essere reimpostato e considerati eliminati.</span><span class="sxs-lookup"><span data-stu-id="d2131-190">Also hello current session should be destroyed, and hello session token value should be reset and nullified.</span></span>|

### <a name="example"></a><span data-ttu-id="d2131-191">Esempio</span><span class="sxs-lookup"><span data-stu-id="d2131-191">Example</span></span>
```C#
        [HttpPost, ValidateAntiForgeryToken]
        [Authorization]
        public ActionResult SignOut(string redirectUrl)
        {
            if (!this.User.Identity.IsAuthenticated)
            {
                return this.View("LogOff", null);
            }

            // Removes hello user profile.
            this.Session.Clear();
            this.Session.Abandon();
            HttpContext.Current.Response.Cookies.Add(new System.Web.HttpCookie("ASP.NET_SessionId", string.Empty)
                {
                    Expires = DateTime.Now.AddDays(-1D),
                    Secure = true,
                    HttpOnly = true
                });

            // Signs out at hello specified security token service (STS) by using hello WS-Federation protocol.
            Uri signOutUrl = new Uri(FederatedAuthentication.WSFederationAuthenticationModule.Issuer);
            Uri replyUrl = new Uri(FederatedAuthentication.WSFederationAuthenticationModule.Realm);
            if (!string.IsNullOrEmpty(redirectUrl))
            {
                replyUrl = new Uri(FederatedAuthentication.WSFederationAuthenticationModule.Realm + redirectUrl);
            }
           //     Signs out of hello current session and raises hello appropriate events.
            var authModule = FederatedAuthentication.WSFederationAuthenticationModule;
            authModule.SignOut(false);
        //     Signs out at hello specified security token service (STS) by using hello WS-Federation
        //     protocol.            
            WSFederationAuthenticationModule.FederatedSignOut(signOutUrl, replyUrl);
            return new RedirectResult(redirectUrl);
        }
```

## <span data-ttu-id="d2131-192"><a id="proper-logout"></a>Implementare la disconnessione appropriata quando si usa Identity Server</span><span class="sxs-lookup"><span data-stu-id="d2131-192"><a id="proper-logout"></a>Implement proper logout when using Identity Server</span></span>

| <span data-ttu-id="d2131-193">Titolo</span><span class="sxs-lookup"><span data-stu-id="d2131-193">Title</span></span>                   | <span data-ttu-id="d2131-194">Dettagli</span><span class="sxs-lookup"><span data-stu-id="d2131-194">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="d2131-195">**Componente**</span><span class="sxs-lookup"><span data-stu-id="d2131-195">**Component**</span></span>               | <span data-ttu-id="d2131-196">Identity Server</span><span class="sxs-lookup"><span data-stu-id="d2131-196">Identity Server</span></span> | 
| <span data-ttu-id="d2131-197">**Fase SDL**</span><span class="sxs-lookup"><span data-stu-id="d2131-197">**SDL Phase**</span></span>               | <span data-ttu-id="d2131-198">Compilare</span><span class="sxs-lookup"><span data-stu-id="d2131-198">Build</span></span> |  
| <span data-ttu-id="d2131-199">**Tecnologie applicabili**</span><span class="sxs-lookup"><span data-stu-id="d2131-199">**Applicable Technologies**</span></span> | <span data-ttu-id="d2131-200">Generico</span><span class="sxs-lookup"><span data-stu-id="d2131-200">Generic</span></span> |
| <span data-ttu-id="d2131-201">**Attributes (Attributi) (Attributi)**</span><span class="sxs-lookup"><span data-stu-id="d2131-201">**Attributes**</span></span>              | <span data-ttu-id="d2131-202">N/D</span><span class="sxs-lookup"><span data-stu-id="d2131-202">N/A</span></span>  |
| <span data-ttu-id="d2131-203">**Riferimenti**</span><span class="sxs-lookup"><span data-stu-id="d2131-203">**References**</span></span>              | [<span data-ttu-id="d2131-204">IdentityServer3: disconnessione federata</span><span class="sxs-lookup"><span data-stu-id="d2131-204">IdentityServer3-Federated sign out</span></span>](https://identityserver.github.io/Documentation/docsv2/advanced/federated-signout.html) |
| <span data-ttu-id="d2131-205">**Passaggi**</span><span class="sxs-lookup"><span data-stu-id="d2131-205">**Steps**</span></span> | <span data-ttu-id="d2131-206">IdentityServer supporta hello possibilità toofederate con i provider di identità esterna.</span><span class="sxs-lookup"><span data-stu-id="d2131-206">IdentityServer supports hello ability toofederate with external identity providers.</span></span> <span data-ttu-id="d2131-207">Quando un utente esce da un provider di identità a monte, in base al protocollo hello utilizzato, potrebbe essere possibile tooreceive una notifica al momento della disconnessione utente hello. Consente di toonotify IdentityServer dei client in modo che possano accedere anche hello utente out. Controllare la documentazione di hello nella sezione dei riferimenti per i dettagli di implementazione hello hello.</span><span class="sxs-lookup"><span data-stu-id="d2131-207">When a user signs out of an upstream identity provider, depending upon hello protocol used, it might be possible tooreceive a notification when hello user signs out. It allows IdentityServer toonotify its clients so they can also sign hello user out. Check hello documentation in hello references section for hello implementation details.</span></span>|

## <span data-ttu-id="d2131-208"><a id="https-secure-cookies"></a>Le applicazioni disponibili tramite HTTPS devono usare cookie sicuri</span><span class="sxs-lookup"><span data-stu-id="d2131-208"><a id="https-secure-cookies"></a>Applications available over HTTPS must use secure cookies</span></span>

| <span data-ttu-id="d2131-209">Titolo</span><span class="sxs-lookup"><span data-stu-id="d2131-209">Title</span></span>                   | <span data-ttu-id="d2131-210">Dettagli</span><span class="sxs-lookup"><span data-stu-id="d2131-210">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="d2131-211">**Componente**</span><span class="sxs-lookup"><span data-stu-id="d2131-211">**Component**</span></span>               | <span data-ttu-id="d2131-212">Applicazione Web.</span><span class="sxs-lookup"><span data-stu-id="d2131-212">Web Application</span></span> | 
| <span data-ttu-id="d2131-213">**Fase SDL**</span><span class="sxs-lookup"><span data-stu-id="d2131-213">**SDL Phase**</span></span>               | <span data-ttu-id="d2131-214">Compilare</span><span class="sxs-lookup"><span data-stu-id="d2131-214">Build</span></span> |  
| <span data-ttu-id="d2131-215">**Tecnologie applicabili**</span><span class="sxs-lookup"><span data-stu-id="d2131-215">**Applicable Technologies**</span></span> | <span data-ttu-id="d2131-216">Generico</span><span class="sxs-lookup"><span data-stu-id="d2131-216">Generic</span></span> |
| <span data-ttu-id="d2131-217">**Attributes (Attributi) (Attributi)**</span><span class="sxs-lookup"><span data-stu-id="d2131-217">**Attributes**</span></span>              | <span data-ttu-id="d2131-218">Tipo di ambiente: locale</span><span class="sxs-lookup"><span data-stu-id="d2131-218">EnvironmentType - OnPrem</span></span> |
| <span data-ttu-id="d2131-219">**Riferimenti**</span><span class="sxs-lookup"><span data-stu-id="d2131-219">**References**</span></span>              | <span data-ttu-id="d2131-220">[Elemento httpCookies (schema delle impostazioni ASP.NET)](http://msdn.microsoft.com/library/ms228262(v=vs.100).aspx), [Proprietà HttpCookie.Secure](http://msdn.microsoft.com/library/system.web.httpcookie.secure.aspx)</span><span class="sxs-lookup"><span data-stu-id="d2131-220">[httpCookies Element (ASP.NET Settings Schema)](http://msdn.microsoft.com/library/ms228262(v=vs.100).aspx), [HttpCookie.Secure Property](http://msdn.microsoft.com/library/system.web.httpcookie.secure.aspx)</span></span> |
| <span data-ttu-id="d2131-221">**Passaggi**</span><span class="sxs-lookup"><span data-stu-id="d2131-221">**Steps**</span></span> | <span data-ttu-id="d2131-222">I cookie sono in genere solo per i quali vengono sono stati nell'ambito di dominio toohello accessibile.</span><span class="sxs-lookup"><span data-stu-id="d2131-222">Cookies are normally only accessible toohello domain for which they were scoped.</span></span> <span data-ttu-id="d2131-223">Purtroppo, definizione hello di "dominio" non include il protocollo di hello in modo che i cookie che vengono creati tramite HTTPS sono accessibili tramite HTTP.</span><span class="sxs-lookup"><span data-stu-id="d2131-223">Unfortunately, hello definition of "domain" does not include hello protocol so cookies that are created over HTTPS are accessible over HTTP.</span></span> <span data-ttu-id="d2131-224">attributo "sicuro" Hello indica browser toohello hello cookie devono solo essere resi disponibili tramite HTTPS.</span><span class="sxs-lookup"><span data-stu-id="d2131-224">hello "secure" attribute indicates toohello browser that hello cookie should only be made available over HTTPS.</span></span> <span data-ttu-id="d2131-225">Assicurarsi che tutti i cookie impostati su HTTPS utilizzino hello **sicura** attributo.</span><span class="sxs-lookup"><span data-stu-id="d2131-225">Ensure that all cookies set over HTTPS use hello **secure** attribute.</span></span> <span data-ttu-id="d2131-226">requisito di Hello può essere applicata nel file Web. config hello impostando tootrue attributo requireSSL di hello.</span><span class="sxs-lookup"><span data-stu-id="d2131-226">hello requirement can be enforced in hello web.config file by setting hello requireSSL attribute tootrue.</span></span> <span data-ttu-id="d2131-227">Si tratta di hello preferito approccio perché applicherà hello **sicura** attributo per tutti i cookie attuali e futuri senza hello necessità toomake eventuali ulteriori modifiche al codice.</span><span class="sxs-lookup"><span data-stu-id="d2131-227">It is hello preferred approach because it will enforce hello **secure** attribute for all current and future cookies without hello need toomake any additional code changes.</span></span>|

### <a name="example"></a><span data-ttu-id="d2131-228">Esempio</span><span class="sxs-lookup"><span data-stu-id="d2131-228">Example</span></span>
```C#
<configuration>
  <system.web>
    <httpCookies requireSSL="true"/>
  </system.web>
</configuration>
```
<span data-ttu-id="d2131-229">anche se quest'ultimo è un'applicazione hello tooaccess usato, viene applicata l'impostazione di Hello.</span><span class="sxs-lookup"><span data-stu-id="d2131-229">hello setting is enforced even if HTTP is used tooaccess hello application.</span></span> <span data-ttu-id="d2131-230">Se viene utilizzato HTTP tooaccess hello applicazione, le interruzioni di impostazione applicazione hello perché i cookie hello sono impostati con i browser di attributo e hello sicuro hello non invierà li hello riaggiungere toohello applicazione.</span><span class="sxs-lookup"><span data-stu-id="d2131-230">If HTTP is used tooaccess hello application, hello setting breaks hello application because hello cookies are set with hello secure attribute and hello browser will not send them back toohello application.</span></span>

| <span data-ttu-id="d2131-231">Titolo</span><span class="sxs-lookup"><span data-stu-id="d2131-231">Title</span></span>                   | <span data-ttu-id="d2131-232">Dettagli</span><span class="sxs-lookup"><span data-stu-id="d2131-232">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="d2131-233">**Componente**</span><span class="sxs-lookup"><span data-stu-id="d2131-233">**Component**</span></span>               | <span data-ttu-id="d2131-234">Applicazione Web.</span><span class="sxs-lookup"><span data-stu-id="d2131-234">Web Application</span></span> | 
| <span data-ttu-id="d2131-235">**Fase SDL**</span><span class="sxs-lookup"><span data-stu-id="d2131-235">**SDL Phase**</span></span>               | <span data-ttu-id="d2131-236">Compilare</span><span class="sxs-lookup"><span data-stu-id="d2131-236">Build</span></span> |  
| <span data-ttu-id="d2131-237">**Tecnologie applicabili**</span><span class="sxs-lookup"><span data-stu-id="d2131-237">**Applicable Technologies**</span></span> | <span data-ttu-id="d2131-238">Web Form, MVC 5</span><span class="sxs-lookup"><span data-stu-id="d2131-238">Web Forms, MVC5</span></span> |
| <span data-ttu-id="d2131-239">**Attributes (Attributi) (Attributi)**</span><span class="sxs-lookup"><span data-stu-id="d2131-239">**Attributes**</span></span>              | <span data-ttu-id="d2131-240">Tipo di ambiente: locale</span><span class="sxs-lookup"><span data-stu-id="d2131-240">EnvironmentType - OnPrem</span></span> |
| <span data-ttu-id="d2131-241">**Riferimenti**</span><span class="sxs-lookup"><span data-stu-id="d2131-241">**References**</span></span>              | <span data-ttu-id="d2131-242">N/D</span><span class="sxs-lookup"><span data-stu-id="d2131-242">N/A</span></span>  |
| <span data-ttu-id="d2131-243">**Passaggi**</span><span class="sxs-lookup"><span data-stu-id="d2131-243">**Steps**</span></span> | <span data-ttu-id="d2131-244">Quando un'applicazione web hello è hello Relying Party e hello IdP è server ADFS, attributo di protezione del token FedAuth hello può essere configurato dall'impostazione tooTrue requireSSL in `system.identityModel.services` sezione di Web. config:</span><span class="sxs-lookup"><span data-stu-id="d2131-244">When hello web application is hello Relying Party, and hello IdP is ADFS server, hello FedAuth token's secure attribute can be configured by setting requireSSL tooTrue in `system.identityModel.services` section of web.config:</span></span>|

### <a name="example"></a><span data-ttu-id="d2131-245">Esempio</span><span class="sxs-lookup"><span data-stu-id="d2131-245">Example</span></span>
```C#
  <system.identityModel.services>
    <federationConfiguration>
      <!-- Set requireSsl=true; domain=application domain name used by FedAuth cookies (Ex: .gdinfra.com); -->
      <cookieHandler requireSsl="true" persistentSessionLifetime="0.0:20:0" />
    ....  
    </federationConfiguration>
  </system.identityModel.services>
```

## <span data-ttu-id="d2131-246"><a id="cookie-definition"></a>Tutte le applicazioni basate su http devono specificare solo http per la definizione dei cookie</span><span class="sxs-lookup"><span data-stu-id="d2131-246"><a id="cookie-definition"></a>All http based application should specify http only for cookie definition</span></span>

| <span data-ttu-id="d2131-247">Titolo</span><span class="sxs-lookup"><span data-stu-id="d2131-247">Title</span></span>                   | <span data-ttu-id="d2131-248">Dettagli</span><span class="sxs-lookup"><span data-stu-id="d2131-248">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="d2131-249">**Componente**</span><span class="sxs-lookup"><span data-stu-id="d2131-249">**Component**</span></span>               | <span data-ttu-id="d2131-250">Applicazione Web.</span><span class="sxs-lookup"><span data-stu-id="d2131-250">Web Application</span></span> | 
| <span data-ttu-id="d2131-251">**Fase SDL**</span><span class="sxs-lookup"><span data-stu-id="d2131-251">**SDL Phase**</span></span>               | <span data-ttu-id="d2131-252">Compilare</span><span class="sxs-lookup"><span data-stu-id="d2131-252">Build</span></span> |  
| <span data-ttu-id="d2131-253">**Tecnologie applicabili**</span><span class="sxs-lookup"><span data-stu-id="d2131-253">**Applicable Technologies**</span></span> | <span data-ttu-id="d2131-254">Generico</span><span class="sxs-lookup"><span data-stu-id="d2131-254">Generic</span></span> |
| <span data-ttu-id="d2131-255">**Attributes (Attributi) (Attributi)**</span><span class="sxs-lookup"><span data-stu-id="d2131-255">**Attributes**</span></span>              | <span data-ttu-id="d2131-256">N/D</span><span class="sxs-lookup"><span data-stu-id="d2131-256">N/A</span></span>  |
| <span data-ttu-id="d2131-257">**Riferimenti**</span><span class="sxs-lookup"><span data-stu-id="d2131-257">**References**</span></span>              | <span data-ttu-id="d2131-258">[Secure Cookie Attribute](https://en.wikipedia.org/wiki/HTTP_cookie#Secure_cookie) (Attributo dei cookie Secure)</span><span class="sxs-lookup"><span data-stu-id="d2131-258">[Secure Cookie Attribute](https://en.wikipedia.org/wiki/HTTP_cookie#Secure_cookie)</span></span> |
| <span data-ttu-id="d2131-259">**Passaggi**</span><span class="sxs-lookup"><span data-stu-id="d2131-259">**Steps**</span></span> | <span data-ttu-id="d2131-260">rischio di hello toomitigate divulgazione di informazioni con un attacco di tipo cross-site scripting (XSS), un nuovo attributo - httpOnly - è stato introdotto toocookies ed è supportato da tutti i browser principali.</span><span class="sxs-lookup"><span data-stu-id="d2131-260">toomitigate hello risk of information disclosure with a cross-site scripting (XSS) attack, a new attribute - httpOnly - was introduced toocookies and is supported by all major browsers.</span></span> <span data-ttu-id="d2131-261">attributo di Hello specifica che un cookie non è accessibile tramite script.</span><span class="sxs-lookup"><span data-stu-id="d2131-261">hello attribute specifies that a cookie is not accessible through script.</span></span> <span data-ttu-id="d2131-262">Utilizzando cookie HttpOnly, un'applicazione web riduce le possibilità hello che informazioni riservate contenute nel cookie hello possono essere rubate tramite script e inviate tooan suo sito Web.</span><span class="sxs-lookup"><span data-stu-id="d2131-262">By using HttpOnly cookies, a web application reduces hello possibility that sensitive information contained in hello cookie can be stolen via script and sent tooan attacker's website.</span></span> |

### <a name="example"></a><span data-ttu-id="d2131-263">Esempio</span><span class="sxs-lookup"><span data-stu-id="d2131-263">Example</span></span>
<span data-ttu-id="d2131-264">Tutte le applicazioni basate su HTTP che usano cookie devono specificare HttpOnly nella definizione di cookie hello, mediante l'implementazione seguente configurazione in Web. config:</span><span class="sxs-lookup"><span data-stu-id="d2131-264">All HTTP-based applications that use cookies should specify HttpOnly in hello cookie definition, by implementing following configuration in web.config:</span></span>
```XML
<system.web>
.
.
   <httpCookies requireSSL="false" httpOnlyCookies="true"/>
.
.
</system.web>
```

| <span data-ttu-id="d2131-265">Titolo</span><span class="sxs-lookup"><span data-stu-id="d2131-265">Title</span></span>                   | <span data-ttu-id="d2131-266">Dettagli</span><span class="sxs-lookup"><span data-stu-id="d2131-266">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="d2131-267">**Componente**</span><span class="sxs-lookup"><span data-stu-id="d2131-267">**Component**</span></span>               | <span data-ttu-id="d2131-268">Applicazione Web.</span><span class="sxs-lookup"><span data-stu-id="d2131-268">Web Application</span></span> | 
| <span data-ttu-id="d2131-269">**Fase SDL**</span><span class="sxs-lookup"><span data-stu-id="d2131-269">**SDL Phase**</span></span>               | <span data-ttu-id="d2131-270">Compilare</span><span class="sxs-lookup"><span data-stu-id="d2131-270">Build</span></span> |  
| <span data-ttu-id="d2131-271">**Tecnologie applicabili**</span><span class="sxs-lookup"><span data-stu-id="d2131-271">**Applicable Technologies**</span></span> | <span data-ttu-id="d2131-272">Web Form</span><span class="sxs-lookup"><span data-stu-id="d2131-272">Web Forms</span></span> |
| <span data-ttu-id="d2131-273">**Attributes (Attributi) (Attributi)**</span><span class="sxs-lookup"><span data-stu-id="d2131-273">**Attributes**</span></span>              | <span data-ttu-id="d2131-274">N/D</span><span class="sxs-lookup"><span data-stu-id="d2131-274">N/A</span></span>  |
| <span data-ttu-id="d2131-275">**Riferimenti**</span><span class="sxs-lookup"><span data-stu-id="d2131-275">**References**</span></span>              | [<span data-ttu-id="d2131-276">Proprietà FormsAuthentication.RequireSSL</span><span class="sxs-lookup"><span data-stu-id="d2131-276">FormsAuthentication.RequireSSL Property</span></span>](https://msdn.microsoft.com/library/system.web.security.formsauthentication.requiressl.aspx) |
| <span data-ttu-id="d2131-277">**Passaggi**</span><span class="sxs-lookup"><span data-stu-id="d2131-277">**Steps**</span></span> | <span data-ttu-id="d2131-278">valore della proprietà RequireSSL Hello è impostato nel file di configurazione hello per un'applicazione ASP.NET tramite l'attributo requireSSL hello dell'elemento di configurazione hello.</span><span class="sxs-lookup"><span data-stu-id="d2131-278">hello RequireSSL property value is set in hello configuration file for an ASP.NET application by using hello requireSSL attribute of hello configuration element.</span></span> <span data-ttu-id="d2131-279">È possibile specificare nel file Web. config hello per l'applicazione ASP.NET se SSL (Secure Sockets Layer) è necessario tooreturn hello autenticazione basata su form cookie toohello dall'impostazione dell'attributo requireSSL hello.</span><span class="sxs-lookup"><span data-stu-id="d2131-279">You can specify in hello Web.config file for your ASP.NET application whether SSL (Secure Sockets Layer) is required tooreturn hello forms-authentication cookie toohello server by setting hello requireSSL attribute.</span></span>|

### <a name="example"></a><span data-ttu-id="d2131-280">Esempio</span><span class="sxs-lookup"><span data-stu-id="d2131-280">Example</span></span> 
<span data-ttu-id="d2131-281">Hello esempio di codice seguente imposta attributo requireSSL hello nel file Web. config hello.</span><span class="sxs-lookup"><span data-stu-id="d2131-281">hello following code example sets hello requireSSL attribute in hello Web.config file.</span></span>
```XML
<authentication mode="Forms">
  <forms loginUrl="member_login.aspx" cookieless="UseCookies" requireSSL="true"/>
</authentication>
```

| <span data-ttu-id="d2131-282">Titolo</span><span class="sxs-lookup"><span data-stu-id="d2131-282">Title</span></span>                   | <span data-ttu-id="d2131-283">Dettagli</span><span class="sxs-lookup"><span data-stu-id="d2131-283">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="d2131-284">**Componente**</span><span class="sxs-lookup"><span data-stu-id="d2131-284">**Component**</span></span>               | <span data-ttu-id="d2131-285">Applicazione Web.</span><span class="sxs-lookup"><span data-stu-id="d2131-285">Web Application</span></span> | 
| <span data-ttu-id="d2131-286">**Fase SDL**</span><span class="sxs-lookup"><span data-stu-id="d2131-286">**SDL Phase**</span></span>               | <span data-ttu-id="d2131-287">Compilare</span><span class="sxs-lookup"><span data-stu-id="d2131-287">Build</span></span> |  
| <span data-ttu-id="d2131-288">**Tecnologie applicabili**</span><span class="sxs-lookup"><span data-stu-id="d2131-288">**Applicable Technologies**</span></span> | <span data-ttu-id="d2131-289">MVC 5</span><span class="sxs-lookup"><span data-stu-id="d2131-289">MVC5</span></span> |
| <span data-ttu-id="d2131-290">**Attributes (Attributi) (Attributi)**</span><span class="sxs-lookup"><span data-stu-id="d2131-290">**Attributes**</span></span>              | <span data-ttu-id="d2131-291">Tipo di ambiente: locale</span><span class="sxs-lookup"><span data-stu-id="d2131-291">EnvironmentType - OnPrem</span></span> |
| <span data-ttu-id="d2131-292">**Riferimenti**</span><span class="sxs-lookup"><span data-stu-id="d2131-292">**References**</span></span>              | <span data-ttu-id="d2131-293">[Windows Identity Foundation (WIF) Configuration – Part II](https://blogs.msdn.microsoft.com/alikl/2011/02/01/windows-identity-foundation-wif-configuration-part-ii-cookiehandler-chunkedcookiehandler-customcookiehandler/) (Configurazione di Windows Identity Foundation (WIF): parte II)</span><span class="sxs-lookup"><span data-stu-id="d2131-293">[Windows Identity Foundation (WIF) Configuration – Part II](https://blogs.msdn.microsoft.com/alikl/2011/02/01/windows-identity-foundation-wif-configuration-part-ii-cookiehandler-chunkedcookiehandler-customcookiehandler/)</span></span> |
| <span data-ttu-id="d2131-294">**Passaggi**</span><span class="sxs-lookup"><span data-stu-id="d2131-294">**Steps**</span></span> | <span data-ttu-id="d2131-295">attributo httpOnly tooset dei cookie FedAuth hideFromCsript valore di attributo deve essere impostato tooTrue.</span><span class="sxs-lookup"><span data-stu-id="d2131-295">tooset httpOnly attribute for FedAuth cookies, hideFromCsript attribute value should be set tooTrue.</span></span> |

### <a name="example"></a><span data-ttu-id="d2131-296">Esempio</span><span class="sxs-lookup"><span data-stu-id="d2131-296">Example</span></span>
<span data-ttu-id="d2131-297">Configurazione seguente mostra la configurazione corretta di hello:</span><span class="sxs-lookup"><span data-stu-id="d2131-297">Following configuration shows hello correct configuration:</span></span>
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

## <span data-ttu-id="d2131-298"><a id="csrf-asp"></a>Mitigare il rischio di attacchi basati su richieste intersito false nelle pagine Web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="d2131-298"><a id="csrf-asp"></a>Mitigate against Cross-Site Request Forgery (CSRF) attacks on ASP.NET web pages</span></span>

| <span data-ttu-id="d2131-299">Titolo</span><span class="sxs-lookup"><span data-stu-id="d2131-299">Title</span></span>                   | <span data-ttu-id="d2131-300">Dettagli</span><span class="sxs-lookup"><span data-stu-id="d2131-300">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="d2131-301">**Componente**</span><span class="sxs-lookup"><span data-stu-id="d2131-301">**Component**</span></span>               | <span data-ttu-id="d2131-302">Applicazione Web.</span><span class="sxs-lookup"><span data-stu-id="d2131-302">Web Application</span></span> | 
| <span data-ttu-id="d2131-303">**Fase SDL**</span><span class="sxs-lookup"><span data-stu-id="d2131-303">**SDL Phase**</span></span>               | <span data-ttu-id="d2131-304">Compilare</span><span class="sxs-lookup"><span data-stu-id="d2131-304">Build</span></span> |  
| <span data-ttu-id="d2131-305">**Tecnologie applicabili**</span><span class="sxs-lookup"><span data-stu-id="d2131-305">**Applicable Technologies**</span></span> | <span data-ttu-id="d2131-306">Generico</span><span class="sxs-lookup"><span data-stu-id="d2131-306">Generic</span></span> |
| <span data-ttu-id="d2131-307">**Attributes (Attributi) (Attributi)**</span><span class="sxs-lookup"><span data-stu-id="d2131-307">**Attributes**</span></span>              | <span data-ttu-id="d2131-308">N/D</span><span class="sxs-lookup"><span data-stu-id="d2131-308">N/A</span></span>  |
| <span data-ttu-id="d2131-309">**Riferimenti**</span><span class="sxs-lookup"><span data-stu-id="d2131-309">**References**</span></span>              | <span data-ttu-id="d2131-310">N/D</span><span class="sxs-lookup"><span data-stu-id="d2131-310">N/A</span></span>  |
| <span data-ttu-id="d2131-311">**Passaggi**</span><span class="sxs-lookup"><span data-stu-id="d2131-311">**Steps**</span></span> | <span data-ttu-id="d2131-312">Falsificazione della richiesta tra siti tra (CSRF o XSRF) è un tipo di attacco in cui un utente malintenzionato può eseguire azioni nel contesto di sicurezza hello di sessione stabilita di un altro utente in un sito web.</span><span class="sxs-lookup"><span data-stu-id="d2131-312">Cross-site request forgery (CSRF or XSRF) is a type of attack in which an attacker can carry out actions in hello security context of a different user's established session on a web site.</span></span> <span data-ttu-id="d2131-313">obiettivo di Hello è toomodify o eliminare il contenuto del sito web di destinazione hello si basa esclusivamente su richiesta ricevuta tooauthenticate i cookie di sessione.</span><span class="sxs-lookup"><span data-stu-id="d2131-313">hello goal is toomodify or delete content, if hello targeted web site relies exclusively on session cookies tooauthenticate received request.</span></span> <span data-ttu-id="d2131-314">Un utente malintenzionato potrebbe sfruttare questa vulnerabilità tramite il recupero di un URL con un comando tooload browser di un utente diverso da un sito vulnerabile in cui hello utente è già connesso.</span><span class="sxs-lookup"><span data-stu-id="d2131-314">An attacker could exploit this vulnerability by getting a different user's browser tooload a URL with a command from a vulnerable site on which hello user is already logged in.</span></span> <span data-ttu-id="d2131-315">Esistono molti modi per toodo un utente malintenzionato che, ad esempio da un altro sito web di hosting che carica una risorsa dal server vulnerabile hello o recupero hello utente tooclick un collegamento.</span><span class="sxs-lookup"><span data-stu-id="d2131-315">There are many ways for an attacker toodo that, such as by hosting a different web site that loads a resource from hello vulnerable server, or getting hello user tooclick a link.</span></span> <span data-ttu-id="d2131-316">è possibile evitare l'attacco Hello se server hello invia un client toohello token aggiuntivi, è necessario hello client tooinclude token in tutte le richieste successive e verifica che tutte le richieste successive includono un token relativo toohello sessione corrente, ad esempio da utilizzo di ASP.NET AntiForgeryToken hello o ViewState.</span><span class="sxs-lookup"><span data-stu-id="d2131-316">hello attack can be prevented if hello server sends an additional token toohello client, requires hello client tooinclude that token in all future requests, and verifies that all future requests include a token that pertains toohello current session, such as by using hello ASP.NET AntiForgeryToken or ViewState.</span></span> |

| <span data-ttu-id="d2131-317">Titolo</span><span class="sxs-lookup"><span data-stu-id="d2131-317">Title</span></span>                   | <span data-ttu-id="d2131-318">Dettagli</span><span class="sxs-lookup"><span data-stu-id="d2131-318">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="d2131-319">**Componente**</span><span class="sxs-lookup"><span data-stu-id="d2131-319">**Component**</span></span>               | <span data-ttu-id="d2131-320">Applicazione Web.</span><span class="sxs-lookup"><span data-stu-id="d2131-320">Web Application</span></span> | 
| <span data-ttu-id="d2131-321">**Fase SDL**</span><span class="sxs-lookup"><span data-stu-id="d2131-321">**SDL Phase**</span></span>               | <span data-ttu-id="d2131-322">Compilare</span><span class="sxs-lookup"><span data-stu-id="d2131-322">Build</span></span> |  
| <span data-ttu-id="d2131-323">**Tecnologie applicabili**</span><span class="sxs-lookup"><span data-stu-id="d2131-323">**Applicable Technologies**</span></span> | <span data-ttu-id="d2131-324">MVC 5, MVC 6</span><span class="sxs-lookup"><span data-stu-id="d2131-324">MVC5, MVC6</span></span> |
| <span data-ttu-id="d2131-325">**Attributes (Attributi) (Attributi)**</span><span class="sxs-lookup"><span data-stu-id="d2131-325">**Attributes**</span></span>              | <span data-ttu-id="d2131-326">N/D</span><span class="sxs-lookup"><span data-stu-id="d2131-326">N/A</span></span>  |
| <span data-ttu-id="d2131-327">**Riferimenti**</span><span class="sxs-lookup"><span data-stu-id="d2131-327">**References**</span></span>              | <span data-ttu-id="d2131-328">[XSRF/CSRF Prevention in ASP.NET MVC and Web Pages](http://www.asp.net/mvc/overview/security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages) (Prevenzione delle richieste intersito false in ASP.NET MVC e nelle pagine Web ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="d2131-328">[XSRF/CSRF Prevention in ASP.NET MVC and Web Pages](http://www.asp.net/mvc/overview/security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages)</span></span> |
| <span data-ttu-id="d2131-329">**Passaggi**</span><span class="sxs-lookup"><span data-stu-id="d2131-329">**Steps**</span></span> | <span data-ttu-id="d2131-330">Form di anti-CSRF e ASP.NET MVC - hello utilizzare `AntiForgeryToken` il metodo di supporto per le viste; put un `Html.AntiForgeryToken()` in formato hello, ad esempio,</span><span class="sxs-lookup"><span data-stu-id="d2131-330">Anti-CSRF and ASP.NET MVC forms - Use hello `AntiForgeryToken` helper method on Views; put an `Html.AntiForgeryToken()` into hello form, for example,</span></span>|

### <a name="example"></a><span data-ttu-id="d2131-331">Esempio</span><span class="sxs-lookup"><span data-stu-id="d2131-331">Example</span></span>
```C#
@using (Html.BeginForm("UserProfile", "SubmitUpdate")) { 
    @Html.ValidationSummary(true) 
    @Html.AntiForgeryToken()
    <fieldset> 
```

### <a name="example"></a><span data-ttu-id="d2131-332">Esempio</span><span class="sxs-lookup"><span data-stu-id="d2131-332">Example</span></span>
```C#
<form action="/UserProfile/SubmitUpdate" method="post">
    <input name="__RequestVerificationToken" type="hidden" value="saTFWpkKN0BYazFtN6c4YbZAmsEwG0srqlUqqloi/fVgeV2ciIFVmelvzwRZpArs" />
    <!-- rest of form goes here -->
</form>
```

### <a name="example"></a><span data-ttu-id="d2131-333">Esempio</span><span class="sxs-lookup"><span data-stu-id="d2131-333">Example</span></span>
<span data-ttu-id="d2131-334">In hello stesso tempo visitatore di hello Html.AntiForgeryToken() offre un cookie denominato __RequestVerificationToken, con lo stesso valore hello casuale nascosto sopra specificato hello.</span><span class="sxs-lookup"><span data-stu-id="d2131-334">At hello same time, Html.AntiForgeryToken() gives hello visitor a cookie called __RequestVerificationToken, with hello same value as hello random hidden value shown above.</span></span> <span data-ttu-id="d2131-335">Toovalidate un post del form in ingresso, successivamente, aggiungere metodo di azione destinazione toohello filtro hello [ValidateAntiForgeryToken].</span><span class="sxs-lookup"><span data-stu-id="d2131-335">Next, toovalidate an incoming form post, add hello [ValidateAntiForgeryToken] filter toohello target action method.</span></span> <span data-ttu-id="d2131-336">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="d2131-336">For example:</span></span>
```
[ValidateAntiForgeryToken]
public ViewResult SubmitUpdate()
{
// ... etc.
}
```
<span data-ttu-id="d2131-337">Filtro di autorizzazione che controlla che:</span><span class="sxs-lookup"><span data-stu-id="d2131-337">Authorization filter that checks that:</span></span>
* <span data-ttu-id="d2131-338">richiesta in ingresso Hello dispone di un cookie denominato __RequestVerificationToken</span><span class="sxs-lookup"><span data-stu-id="d2131-338">hello incoming request has a cookie called __RequestVerificationToken</span></span>
* <span data-ttu-id="d2131-339">Hello richiesta in arrivo è un `Request.Form` voce denominata __RequestVerificationToken</span><span class="sxs-lookup"><span data-stu-id="d2131-339">hello incoming request has a `Request.Form` entry called __RequestVerificationToken</span></span>
* <span data-ttu-id="d2131-340">Questi cookie e `Request.Form` è ben corrispondono ai valori presupponendo che tutti, hello richiesta viene eseguita come di consueto.</span><span class="sxs-lookup"><span data-stu-id="d2131-340">These cookie and `Request.Form` values match Assuming all is well, hello request goes through as normal.</span></span> <span data-ttu-id="d2131-341">In caso contrario, si verifica un errore di autorizzazione e viene visualizzato il messaggio "Token antifalsificazione non specificato o non valido".</span><span class="sxs-lookup"><span data-stu-id="d2131-341">But if not, then an authorization failure with message “A required anti-forgery token was not supplied or was invalid”.</span></span> 

### <a name="example"></a><span data-ttu-id="d2131-342">Esempio</span><span class="sxs-lookup"><span data-stu-id="d2131-342">Example</span></span>
<span data-ttu-id="d2131-343">AJAX and anti-CSRF: token del form hello può costituire un problema per le richieste AJAX, perché una richiesta AJAX potrebbe inviare i dati JSON, non i dati di form HTML.</span><span class="sxs-lookup"><span data-stu-id="d2131-343">Anti-CSRF and AJAX: hello form token can be a problem for AJAX requests, because an AJAX request might send JSON data, not HTML form data.</span></span> <span data-ttu-id="d2131-344">Una soluzione è il token hello toosend in un'intestazione HTTP personalizzata.</span><span class="sxs-lookup"><span data-stu-id="d2131-344">One solution is toosend hello tokens in a custom HTTP header.</span></span> <span data-ttu-id="d2131-345">Hello codice seguente usa i token hello toogenerate di sintassi Razor e quindi aggiunge hello token tooan AJAX richiesta.</span><span class="sxs-lookup"><span data-stu-id="d2131-345">hello following code uses Razor syntax toogenerate hello tokens, and then adds hello tokens tooan AJAX request.</span></span> 
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

### <a name="example"></a><span data-ttu-id="d2131-346">Esempio</span><span class="sxs-lookup"><span data-stu-id="d2131-346">Example</span></span>
<span data-ttu-id="d2131-347">Quando si elabora una richiesta di hello, estrarre il token hello dall'intestazione della richiesta di hello.</span><span class="sxs-lookup"><span data-stu-id="d2131-347">When you process hello request, extract hello tokens from hello request header.</span></span> <span data-ttu-id="d2131-348">Quindi chiamare il metodo AntiForgery.Validate hello token hello toovalidate.</span><span class="sxs-lookup"><span data-stu-id="d2131-348">Then call hello AntiForgery.Validate method toovalidate hello tokens.</span></span> <span data-ttu-id="d2131-349">il metodo Validate Hello genera un'eccezione se i token hello non sono validi.</span><span class="sxs-lookup"><span data-stu-id="d2131-349">hello Validate method throws an exception if hello tokens are not valid.</span></span>
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

| <span data-ttu-id="d2131-350">Titolo</span><span class="sxs-lookup"><span data-stu-id="d2131-350">Title</span></span>                   | <span data-ttu-id="d2131-351">Dettagli</span><span class="sxs-lookup"><span data-stu-id="d2131-351">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="d2131-352">**Componente**</span><span class="sxs-lookup"><span data-stu-id="d2131-352">**Component**</span></span>               | <span data-ttu-id="d2131-353">Applicazione Web.</span><span class="sxs-lookup"><span data-stu-id="d2131-353">Web Application</span></span> | 
| <span data-ttu-id="d2131-354">**Fase SDL**</span><span class="sxs-lookup"><span data-stu-id="d2131-354">**SDL Phase**</span></span>               | <span data-ttu-id="d2131-355">Compilare</span><span class="sxs-lookup"><span data-stu-id="d2131-355">Build</span></span> |  
| <span data-ttu-id="d2131-356">**Tecnologie applicabili**</span><span class="sxs-lookup"><span data-stu-id="d2131-356">**Applicable Technologies**</span></span> | <span data-ttu-id="d2131-357">Web Form</span><span class="sxs-lookup"><span data-stu-id="d2131-357">Web Forms</span></span> |
| <span data-ttu-id="d2131-358">**Attributes (Attributi) (Attributi)**</span><span class="sxs-lookup"><span data-stu-id="d2131-358">**Attributes**</span></span>              | <span data-ttu-id="d2131-359">N/D</span><span class="sxs-lookup"><span data-stu-id="d2131-359">N/A</span></span>  |
| <span data-ttu-id="d2131-360">**Riferimenti**</span><span class="sxs-lookup"><span data-stu-id="d2131-360">**References**</span></span>              | [<span data-ttu-id="d2131-361">Take Advantage of ASP.NET predefinito Features tooFend Off Web attacchi</span><span class="sxs-lookup"><span data-stu-id="d2131-361">Take Advantage of ASP.NET Built-in Features tooFend Off Web Attacks</span></span>](https://msdn.microsoft.com/library/ms972969.aspx#securitybarriers_topic2) |
| <span data-ttu-id="d2131-362">**Passaggi**</span><span class="sxs-lookup"><span data-stu-id="d2131-362">**Steps**</span></span> | <span data-ttu-id="d2131-363">Attacchi CSRF nelle applicazioni Web Form di base possono essere contrastati impostando ViewStateUserKey tooa stringa casuale che varia per ogni utente - ID utente o, meglio ancora, ID di sessione.</span><span class="sxs-lookup"><span data-stu-id="d2131-363">CSRF attacks in WebForm based applications can be mitigated by setting ViewStateUserKey tooa random string that varies for each user - user ID or, better yet, session ID.</span></span> <span data-ttu-id="d2131-364">Per diversi motivi tecnici e legati ai social network, l'ID sessione è molto più appropriato perché non è prevedibile, scade ed è diverso per ogni utente.</span><span class="sxs-lookup"><span data-stu-id="d2131-364">For a number of technical and social reasons, session ID is a much better fit because a session ID is unpredictable, times out, and varies on a per-user basis.</span></span>|

### <a name="example"></a><span data-ttu-id="d2131-365">Esempio</span><span class="sxs-lookup"><span data-stu-id="d2131-365">Example</span></span>
<span data-ttu-id="d2131-366">Di seguito è riportato il codice di hello necessario toohave in tutte le pagine:</span><span class="sxs-lookup"><span data-stu-id="d2131-366">Here's hello code you need toohave in all of your pages:</span></span>
```C#
void Page_Init (object sender, EventArgs e) {
   ViewStateUserKey = Session.SessionID;
   :
}
```

## <span data-ttu-id="d2131-367"><a id="inactivity-lifetime"></a>Configurare una sessione per la durata dell'inattività</span><span class="sxs-lookup"><span data-stu-id="d2131-367"><a id="inactivity-lifetime"></a>Set up session for inactivity lifetime</span></span>

| <span data-ttu-id="d2131-368">Titolo</span><span class="sxs-lookup"><span data-stu-id="d2131-368">Title</span></span>                   | <span data-ttu-id="d2131-369">Dettagli</span><span class="sxs-lookup"><span data-stu-id="d2131-369">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="d2131-370">**Componente**</span><span class="sxs-lookup"><span data-stu-id="d2131-370">**Component**</span></span>               | <span data-ttu-id="d2131-371">Applicazione Web.</span><span class="sxs-lookup"><span data-stu-id="d2131-371">Web Application</span></span> | 
| <span data-ttu-id="d2131-372">**Fase SDL**</span><span class="sxs-lookup"><span data-stu-id="d2131-372">**SDL Phase**</span></span>               | <span data-ttu-id="d2131-373">Compilare</span><span class="sxs-lookup"><span data-stu-id="d2131-373">Build</span></span> |  
| <span data-ttu-id="d2131-374">**Tecnologie applicabili**</span><span class="sxs-lookup"><span data-stu-id="d2131-374">**Applicable Technologies**</span></span> | <span data-ttu-id="d2131-375">Generico</span><span class="sxs-lookup"><span data-stu-id="d2131-375">Generic</span></span> |
| <span data-ttu-id="d2131-376">**Attributes (Attributi) (Attributi)**</span><span class="sxs-lookup"><span data-stu-id="d2131-376">**Attributes**</span></span>              | <span data-ttu-id="d2131-377">N/D</span><span class="sxs-lookup"><span data-stu-id="d2131-377">N/A</span></span>  |
| <span data-ttu-id="d2131-378">**Riferimenti**</span><span class="sxs-lookup"><span data-stu-id="d2131-378">**References**</span></span>              | <span data-ttu-id="d2131-379">[Proprietà HttpSessionState.Timeout](https://msdn.microsoft.com/library/system.web.sessionstate.httpsessionstate.timeout(v=vs.110).aspx)</span><span class="sxs-lookup"><span data-stu-id="d2131-379">[HttpSessionState.Timeout Property](https://msdn.microsoft.com/library/system.web.sessionstate.httpsessionstate.timeout(v=vs.110).aspx)</span></span> |
| <span data-ttu-id="d2131-380">**Passaggi**</span><span class="sxs-lookup"><span data-stu-id="d2131-380">**Steps**</span></span> | <span data-ttu-id="d2131-381">Timeout della sessione rappresenta hello evento si verifica quando un utente non esegue nessuna azione in un sito web durante un intervallo (come definito dal server web).</span><span class="sxs-lookup"><span data-stu-id="d2131-381">Session timeout represents hello event occurring when a user does not perform any action on a web site during a interval (defined by web server).</span></span> <span data-ttu-id="d2131-382">Salve, evento sul lato server, modificare lo stato di hello di hello utente sessione too'invalid' (ad esempio "non è più utilizzata") e indicherà hello web server toodestroy (l'eliminazione di tutti i dati contenuti al suo interno).</span><span class="sxs-lookup"><span data-stu-id="d2131-382">hello event, on server side, change hello status of hello user session too'invalid' (for example  "not used anymore") and instruct hello web server toodestroy it (deleting all data contained into it).</span></span> <span data-ttu-id="d2131-383">Hello esempio di codice seguente imposta hello timeout sessione attributo too15 in minuti nel file Web. config hello.</span><span class="sxs-lookup"><span data-stu-id="d2131-383">hello following code example sets hello timeout session attribute too15 minutes in hello Web.config file.</span></span>|

### <a name="example"></a><span data-ttu-id="d2131-384">Esempio</span><span class="sxs-lookup"><span data-stu-id="d2131-384">Example</span></span>
<span data-ttu-id="d2131-385">``\`Codice XML <configuration> <system.web> <sessionState mode="InProc" cookieless="true" timeout="15" /> </system.web> </configuration></span><span class="sxs-lookup"><span data-stu-id="d2131-385">``\`XML code <configuration> <system.web> <sessionState mode="InProc" cookieless="true" timeout="15" /> </system.web> </configuration></span></span>
```

## <a id="threat-detection"></a>Enable Threat detection on Azure SQL
```

| <span data-ttu-id="d2131-386">Titolo</span><span class="sxs-lookup"><span data-stu-id="d2131-386">Title</span></span>                   | <span data-ttu-id="d2131-387">Dettagli</span><span class="sxs-lookup"><span data-stu-id="d2131-387">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="d2131-388">**Componente**</span><span class="sxs-lookup"><span data-stu-id="d2131-388">**Component**</span></span>               | <span data-ttu-id="d2131-389">Applicazione Web.</span><span class="sxs-lookup"><span data-stu-id="d2131-389">Web Application</span></span> | 
| <span data-ttu-id="d2131-390">**Fase SDL**</span><span class="sxs-lookup"><span data-stu-id="d2131-390">**SDL Phase**</span></span>               | <span data-ttu-id="d2131-391">Compilare</span><span class="sxs-lookup"><span data-stu-id="d2131-391">Build</span></span> |  
| <span data-ttu-id="d2131-392">**Tecnologie applicabili**</span><span class="sxs-lookup"><span data-stu-id="d2131-392">**Applicable Technologies**</span></span> | <span data-ttu-id="d2131-393">Web Form</span><span class="sxs-lookup"><span data-stu-id="d2131-393">Web Forms</span></span> |
| <span data-ttu-id="d2131-394">**Attributes (Attributi) (Attributi)**</span><span class="sxs-lookup"><span data-stu-id="d2131-394">**Attributes**</span></span>              | <span data-ttu-id="d2131-395">N/D</span><span class="sxs-lookup"><span data-stu-id="d2131-395">N/A</span></span>  |
| <span data-ttu-id="d2131-396">**Riferimenti**</span><span class="sxs-lookup"><span data-stu-id="d2131-396">**References**</span></span>              | <span data-ttu-id="d2131-397">[Elemento forms per authentication (schema delle impostazioni ASP.NET)](https://msdn.microsoft.com/library/1d3t3c61(v=vs.100).aspx)</span><span class="sxs-lookup"><span data-stu-id="d2131-397">[forms Element for authentication (ASP.NET Settings Schema)](https://msdn.microsoft.com/library/1d3t3c61(v=vs.100).aspx)</span></span> |
| <span data-ttu-id="d2131-398">**Passaggi**</span><span class="sxs-lookup"><span data-stu-id="d2131-398">**Steps**</span></span> | <span data-ttu-id="d2131-399">Impostare minuti hello too15 timeout di Ticket di autenticazione form cookie</span><span class="sxs-lookup"><span data-stu-id="d2131-399">Set hello Forms Authentication Ticket cookie timeout too15 minutes</span></span>|

### <a name="example"></a><span data-ttu-id="d2131-400">Esempio</span><span class="sxs-lookup"><span data-stu-id="d2131-400">Example</span></span>
<span data-ttu-id="d2131-401">``\`Codice XML <forms  name=".ASPXAUTH" loginUrl="login.aspx"  defaultUrl="default.aspx" protection="All" timeout="15" path="/" requireSSL="true" slidingExpiration="true"/>
</forms></span><span class="sxs-lookup"><span data-stu-id="d2131-401">``\`XML code <forms  name=".ASPXAUTH" loginUrl="login.aspx"  defaultUrl="default.aspx" protection="All" timeout="15" path="/" requireSSL="true" slidingExpiration="true"/>
</forms></span></span>
```

| Title                   | Details      |
| ----------------------- | ------------ |
| **Component**               | Web Application | 
| **SDL Phase**               | Build |  
| **Applicable Technologies** | Web Forms, MVC5 |
| **Attributes**              | EnvironmentType - OnPrem |
| **References**              | [asdeqa](https://skf.azurewebsites.net/Mitigations/Details/wefr) |
| **Steps** | When hello web application is Relying Party and ADFS is hello STS, hello lifetime of hello authentication cookies - FedAuth tokens - can be set by hello following configuration in web.config:|

### Example
```XML
  <system.identityModel.services>
    <federationConfiguration>
      <!-- Set requireSsl=true; domain=application domain name used by FedAuth cookies (Ex: .gdinfra.com); -->
      <cookieHandler requireSsl="true" persistentSessionLifetime="0.0:15:0" />
      <!-- Set requireHttps=true; -->
      <wsFederation passiveRedirectEnabled="true" issuer="http://localhost:39529/" realm="https://localhost:44302/" reply="https://localhost:44302/" requireHttps="true"/>
      <!--
      Use hello code below tooenable encryption-decryption of claims received from ADFS. Thumbprint value varies based on hello certificate being used.
      <serviceCertificate>
        <certificateReference findValue="4FBBBA33A1D11A9022A5BF3492FF83320007686A" storeLocation="LocalMachine" storeName="My" x509FindType="FindByThumbprint" />
      </serviceCertificate>
      -->
    </federationConfiguration>
  </system.identityModel.services>
```

### <a name="example"></a><span data-ttu-id="d2131-402">Esempio</span><span class="sxs-lookup"><span data-stu-id="d2131-402">Example</span></span>
<span data-ttu-id="d2131-403">Anche hello ADFS rilasciato la durata del token SAML attestazione deve essere impostato too15 minuti, eseguendo il comando di powershell nel server ADFS hello seguente hello:</span><span class="sxs-lookup"><span data-stu-id="d2131-403">Also hello ADFS issued SAML claim token's lifetime should be set too15 minutes, by executing hello following powershell command on hello ADFS server:</span></span>
```C#
Set-ADFSRelyingPartyTrust -TargetName “<RelyingPartyWebApp>” -ClaimsProviderName @(“Active Directory”) -TokenLifetime 15 -AlwaysRequireAuthentication $true
```

## <span data-ttu-id="d2131-404"><a id="proper-app-logout"></a>Implementa la disconnessione appropriata da un'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="d2131-404"><a id="proper-app-logout"></a>Implement proper logout from hello application</span></span>

| <span data-ttu-id="d2131-405">Titolo</span><span class="sxs-lookup"><span data-stu-id="d2131-405">Title</span></span>                   | <span data-ttu-id="d2131-406">Dettagli</span><span class="sxs-lookup"><span data-stu-id="d2131-406">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="d2131-407">**Componente**</span><span class="sxs-lookup"><span data-stu-id="d2131-407">**Component**</span></span>               | <span data-ttu-id="d2131-408">Applicazione Web.</span><span class="sxs-lookup"><span data-stu-id="d2131-408">Web Application</span></span> | 
| <span data-ttu-id="d2131-409">**Fase SDL**</span><span class="sxs-lookup"><span data-stu-id="d2131-409">**SDL Phase**</span></span>               | <span data-ttu-id="d2131-410">Compilare</span><span class="sxs-lookup"><span data-stu-id="d2131-410">Build</span></span> |  
| <span data-ttu-id="d2131-411">**Tecnologie applicabili**</span><span class="sxs-lookup"><span data-stu-id="d2131-411">**Applicable Technologies**</span></span> | <span data-ttu-id="d2131-412">Generico</span><span class="sxs-lookup"><span data-stu-id="d2131-412">Generic</span></span> |
| <span data-ttu-id="d2131-413">**Attributes (Attributi) (Attributi)**</span><span class="sxs-lookup"><span data-stu-id="d2131-413">**Attributes**</span></span>              | <span data-ttu-id="d2131-414">N/D</span><span class="sxs-lookup"><span data-stu-id="d2131-414">N/A</span></span>  |
| <span data-ttu-id="d2131-415">**Riferimenti**</span><span class="sxs-lookup"><span data-stu-id="d2131-415">**References**</span></span>              | <span data-ttu-id="d2131-416">N/D</span><span class="sxs-lookup"><span data-stu-id="d2131-416">N/A</span></span>  |
| <span data-ttu-id="d2131-417">**Passaggi**</span><span class="sxs-lookup"><span data-stu-id="d2131-417">**Steps**</span></span> | <span data-ttu-id="d2131-418">Eseguire Disconnetti appropriato da un'applicazione hello, quando l'utente preme disconnettersi dal pulsante.</span><span class="sxs-lookup"><span data-stu-id="d2131-418">Perform proper Sign Out from hello application, when user presses log out button.</span></span> <span data-ttu-id="d2131-419">Durante la disconnessione, l'applicazione deve eliminare definitivamente la sessione dell'utente e anche reimpostare e rendere null il valore del cookie della sessione, oltre a reimpostare e rendere null il valore del cookie di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="d2131-419">Upon logout, application should destroy user's session, and also reset and nullify session cookie value, along with resetting and nullifying authentication cookie value.</span></span> <span data-ttu-id="d2131-420">Inoltre, quando più sessioni tooa legati singola identità utente, si deve collettivamente terminare sul lato server hello timeout o disconnessione.</span><span class="sxs-lookup"><span data-stu-id="d2131-420">Also, when multiple sessions are tied tooa single user identity, they must be collectively terminated on hello server side at timeout or logout.</span></span> <span data-ttu-id="d2131-421">Assicurarsi infine che la funzionalità di disconnessione sia disponibile in ogni pagina.</span><span class="sxs-lookup"><span data-stu-id="d2131-421">Lastly, ensure that Logout functionality is available on every page.</span></span> |

## <span data-ttu-id="d2131-422"><a id="csrf-api"></a>Mitigare il rischio di attacchi basati su richieste intersito false nelle API Web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="d2131-422"><a id="csrf-api"></a>Mitigate against Cross-Site Request Forgery (CSRF) attacks on ASP.NET Web APIs</span></span>

| <span data-ttu-id="d2131-423">Titolo</span><span class="sxs-lookup"><span data-stu-id="d2131-423">Title</span></span>                   | <span data-ttu-id="d2131-424">Dettagli</span><span class="sxs-lookup"><span data-stu-id="d2131-424">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="d2131-425">**Componente**</span><span class="sxs-lookup"><span data-stu-id="d2131-425">**Component**</span></span>               | <span data-ttu-id="d2131-426">API Web</span><span class="sxs-lookup"><span data-stu-id="d2131-426">Web API</span></span> | 
| <span data-ttu-id="d2131-427">**Fase SDL**</span><span class="sxs-lookup"><span data-stu-id="d2131-427">**SDL Phase**</span></span>               | <span data-ttu-id="d2131-428">Compilare</span><span class="sxs-lookup"><span data-stu-id="d2131-428">Build</span></span> |  
| <span data-ttu-id="d2131-429">**Tecnologie applicabili**</span><span class="sxs-lookup"><span data-stu-id="d2131-429">**Applicable Technologies**</span></span> | <span data-ttu-id="d2131-430">Generico</span><span class="sxs-lookup"><span data-stu-id="d2131-430">Generic</span></span> |
| <span data-ttu-id="d2131-431">**Attributes (Attributi) (Attributi)**</span><span class="sxs-lookup"><span data-stu-id="d2131-431">**Attributes**</span></span>              | <span data-ttu-id="d2131-432">N/D</span><span class="sxs-lookup"><span data-stu-id="d2131-432">N/A</span></span>  |
| <span data-ttu-id="d2131-433">**Riferimenti**</span><span class="sxs-lookup"><span data-stu-id="d2131-433">**References**</span></span>              | <span data-ttu-id="d2131-434">N/D</span><span class="sxs-lookup"><span data-stu-id="d2131-434">N/A</span></span>  |
| <span data-ttu-id="d2131-435">**Passaggi**</span><span class="sxs-lookup"><span data-stu-id="d2131-435">**Steps**</span></span> | <span data-ttu-id="d2131-436">Falsificazione della richiesta tra siti tra (CSRF o XSRF) è un tipo di attacco in cui un utente malintenzionato può eseguire azioni nel contesto di sicurezza hello di sessione stabilita di un altro utente in un sito web.</span><span class="sxs-lookup"><span data-stu-id="d2131-436">Cross-site request forgery (CSRF or XSRF) is a type of attack in which an attacker can carry out actions in hello security context of a different user's established session on a web site.</span></span> <span data-ttu-id="d2131-437">obiettivo di Hello è toomodify o eliminare il contenuto del sito web di destinazione hello si basa esclusivamente su richiesta ricevuta tooauthenticate i cookie di sessione.</span><span class="sxs-lookup"><span data-stu-id="d2131-437">hello goal is toomodify or delete content, if hello targeted web site relies exclusively on session cookies tooauthenticate received request.</span></span> <span data-ttu-id="d2131-438">Un utente malintenzionato potrebbe sfruttare questa vulnerabilità tramite il recupero di un URL con un comando tooload browser di un utente diverso da un sito vulnerabile in cui hello utente è già connesso.</span><span class="sxs-lookup"><span data-stu-id="d2131-438">An attacker could exploit this vulnerability by getting a different user's browser tooload a URL with a command from a vulnerable site on which hello user is already logged in.</span></span> <span data-ttu-id="d2131-439">Esistono molti modi per toodo un utente malintenzionato che, ad esempio da un altro sito web di hosting che carica una risorsa dal server vulnerabile hello o recupero hello utente tooclick un collegamento.</span><span class="sxs-lookup"><span data-stu-id="d2131-439">There are many ways for an attacker toodo that, such as by hosting a different web site that loads a resource from hello vulnerable server, or getting hello user tooclick a link.</span></span> <span data-ttu-id="d2131-440">è possibile evitare l'attacco Hello se server hello invia un client toohello token aggiuntivi, è necessario hello client tooinclude token in tutte le richieste successive e verifica che tutte le richieste successive includono un token relativo toohello sessione corrente, ad esempio da utilizzo di ASP.NET AntiForgeryToken hello o ViewState.</span><span class="sxs-lookup"><span data-stu-id="d2131-440">hello attack can be prevented if hello server sends an additional token toohello client, requires hello client tooinclude that token in all future requests, and verifies that all future requests include a token that pertains toohello current session, such as by using hello ASP.NET AntiForgeryToken or ViewState.</span></span> |

| <span data-ttu-id="d2131-441">Titolo</span><span class="sxs-lookup"><span data-stu-id="d2131-441">Title</span></span>                   | <span data-ttu-id="d2131-442">Dettagli</span><span class="sxs-lookup"><span data-stu-id="d2131-442">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="d2131-443">**Componente**</span><span class="sxs-lookup"><span data-stu-id="d2131-443">**Component**</span></span>               | <span data-ttu-id="d2131-444">API Web</span><span class="sxs-lookup"><span data-stu-id="d2131-444">Web API</span></span> | 
| <span data-ttu-id="d2131-445">**Fase SDL**</span><span class="sxs-lookup"><span data-stu-id="d2131-445">**SDL Phase**</span></span>               | <span data-ttu-id="d2131-446">Compilare</span><span class="sxs-lookup"><span data-stu-id="d2131-446">Build</span></span> |  
| <span data-ttu-id="d2131-447">**Tecnologie applicabili**</span><span class="sxs-lookup"><span data-stu-id="d2131-447">**Applicable Technologies**</span></span> | <span data-ttu-id="d2131-448">MVC 5, MVC 6</span><span class="sxs-lookup"><span data-stu-id="d2131-448">MVC5, MVC6</span></span> |
| <span data-ttu-id="d2131-449">**Attributes (Attributi) (Attributi)**</span><span class="sxs-lookup"><span data-stu-id="d2131-449">**Attributes**</span></span>              | <span data-ttu-id="d2131-450">N/D</span><span class="sxs-lookup"><span data-stu-id="d2131-450">N/A</span></span>  |
| <span data-ttu-id="d2131-451">**Riferimenti**</span><span class="sxs-lookup"><span data-stu-id="d2131-451">**References**</span></span>              | <span data-ttu-id="d2131-452">[Preventing Cross-Site Request Forgery (CSRF) Attacks in ASP.NET Web API](http://www.asp.net/web-api/overview/security/preventing-cross-site-request-forgery-csrf-attacks) (Prevenzione di attacchi basati su richieste intersito false nelle API Web ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="d2131-452">[Preventing Cross-Site Request Forgery (CSRF) Attacks in ASP.NET Web API](http://www.asp.net/web-api/overview/security/preventing-cross-site-request-forgery-csrf-attacks)</span></span> |
| <span data-ttu-id="d2131-453">**Passaggi**</span><span class="sxs-lookup"><span data-stu-id="d2131-453">**Steps**</span></span> | <span data-ttu-id="d2131-454">AJAX and anti-CSRF: token del form hello può costituire un problema per le richieste AJAX, perché una richiesta AJAX potrebbe inviare i dati JSON, non i dati di form HTML.</span><span class="sxs-lookup"><span data-stu-id="d2131-454">Anti-CSRF and AJAX: hello form token can be a problem for AJAX requests, because an AJAX request might send JSON data, not HTML form data.</span></span> <span data-ttu-id="d2131-455">Una soluzione è il token hello toosend in un'intestazione HTTP personalizzata.</span><span class="sxs-lookup"><span data-stu-id="d2131-455">One solution is toosend hello tokens in a custom HTTP header.</span></span> <span data-ttu-id="d2131-456">Hello codice seguente usa i token hello toogenerate di sintassi Razor e quindi aggiunge hello token tooan AJAX richiesta.</span><span class="sxs-lookup"><span data-stu-id="d2131-456">hello following code uses Razor syntax toogenerate hello tokens, and then adds hello tokens tooan AJAX request.</span></span> |

### <a name="example"></a><span data-ttu-id="d2131-457">Esempio</span><span class="sxs-lookup"><span data-stu-id="d2131-457">Example</span></span>
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

### <a name="example"></a><span data-ttu-id="d2131-458">Esempio</span><span class="sxs-lookup"><span data-stu-id="d2131-458">Example</span></span>
<span data-ttu-id="d2131-459">Quando si elabora una richiesta di hello, estrarre il token hello dall'intestazione della richiesta di hello.</span><span class="sxs-lookup"><span data-stu-id="d2131-459">When you process hello request, extract hello tokens from hello request header.</span></span> <span data-ttu-id="d2131-460">Quindi chiamare il metodo AntiForgery.Validate hello token hello toovalidate.</span><span class="sxs-lookup"><span data-stu-id="d2131-460">Then call hello AntiForgery.Validate method toovalidate hello tokens.</span></span> <span data-ttu-id="d2131-461">il metodo Validate Hello genera un'eccezione se i token hello non sono validi.</span><span class="sxs-lookup"><span data-stu-id="d2131-461">hello Validate method throws an exception if hello tokens are not valid.</span></span>
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

### <a name="example"></a><span data-ttu-id="d2131-462">Esempio</span><span class="sxs-lookup"><span data-stu-id="d2131-462">Example</span></span>
<span data-ttu-id="d2131-463">Anti-CSRF e form di ASP.NET MVC - hello di utilizzare il metodo helper AntiForgeryToken sulle viste; Inserire un Html.AntiForgeryToken() modulo hello, ad esempio,</span><span class="sxs-lookup"><span data-stu-id="d2131-463">Anti-CSRF and ASP.NET MVC forms - Use hello AntiForgeryToken helper method on Views; put an Html.AntiForgeryToken() into hello form, for example,</span></span>
```C#
@using (Html.BeginForm("UserProfile", "SubmitUpdate")) { 
    @Html.ValidationSummary(true) 
    @Html.AntiForgeryToken()
    <fieldset> 
}
```

### <a name="example"></a><span data-ttu-id="d2131-464">Esempio</span><span class="sxs-lookup"><span data-stu-id="d2131-464">Example</span></span>
<span data-ttu-id="d2131-465">esempio Hello precedente verrà restituito simile alla seguente hello:</span><span class="sxs-lookup"><span data-stu-id="d2131-465">hello example above will output something like hello following:</span></span>
```C#
<form action="/UserProfile/SubmitUpdate" method="post">
    <input name="__RequestVerificationToken" type="hidden" value="saTFWpkKN0BYazFtN6c4YbZAmsEwG0srqlUqqloi/fVgeV2ciIFVmelvzwRZpArs" />
    <!-- rest of form goes here -->
</form>
```

### <a name="example"></a><span data-ttu-id="d2131-466">Esempio</span><span class="sxs-lookup"><span data-stu-id="d2131-466">Example</span></span>
<span data-ttu-id="d2131-467">In hello stesso tempo visitatore di hello Html.AntiForgeryToken() offre un cookie denominato __RequestVerificationToken, con lo stesso valore hello casuale nascosto sopra specificato hello.</span><span class="sxs-lookup"><span data-stu-id="d2131-467">At hello same time, Html.AntiForgeryToken() gives hello visitor a cookie called __RequestVerificationToken, with hello same value as hello random hidden value shown above.</span></span> <span data-ttu-id="d2131-468">Toovalidate un post del form in ingresso, successivamente, aggiungere metodo di azione destinazione toohello filtro hello [ValidateAntiForgeryToken].</span><span class="sxs-lookup"><span data-stu-id="d2131-468">Next, toovalidate an incoming form post, add hello [ValidateAntiForgeryToken] filter toohello target action method.</span></span> <span data-ttu-id="d2131-469">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="d2131-469">For example:</span></span>
```
[ValidateAntiForgeryToken]
public ViewResult SubmitUpdate()
{
// ... etc.
}
```
<span data-ttu-id="d2131-470">Filtro di autorizzazione che controlla che:</span><span class="sxs-lookup"><span data-stu-id="d2131-470">Authorization filter that checks that:</span></span>
* <span data-ttu-id="d2131-471">richiesta in ingresso Hello dispone di un cookie denominato __RequestVerificationToken</span><span class="sxs-lookup"><span data-stu-id="d2131-471">hello incoming request has a cookie called __RequestVerificationToken</span></span>
* <span data-ttu-id="d2131-472">Hello richiesta in arrivo è un `Request.Form` voce denominata __RequestVerificationToken</span><span class="sxs-lookup"><span data-stu-id="d2131-472">hello incoming request has a `Request.Form` entry called __RequestVerificationToken</span></span>
* <span data-ttu-id="d2131-473">Questi cookie e `Request.Form` è ben corrispondono ai valori presupponendo che tutti, hello richiesta viene eseguita come di consueto.</span><span class="sxs-lookup"><span data-stu-id="d2131-473">These cookie and `Request.Form` values match Assuming all is well, hello request goes through as normal.</span></span> <span data-ttu-id="d2131-474">In caso contrario, si verifica un errore di autorizzazione e viene visualizzato il messaggio "Token antifalsificazione non specificato o non valido".</span><span class="sxs-lookup"><span data-stu-id="d2131-474">But if not, then an authorization failure with message “A required anti-forgery token was not supplied or was invalid”.</span></span>

| <span data-ttu-id="d2131-475">Titolo</span><span class="sxs-lookup"><span data-stu-id="d2131-475">Title</span></span>                   | <span data-ttu-id="d2131-476">Dettagli</span><span class="sxs-lookup"><span data-stu-id="d2131-476">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="d2131-477">**Componente**</span><span class="sxs-lookup"><span data-stu-id="d2131-477">**Component**</span></span>               | <span data-ttu-id="d2131-478">API Web</span><span class="sxs-lookup"><span data-stu-id="d2131-478">Web API</span></span> | 
| <span data-ttu-id="d2131-479">**Fase SDL**</span><span class="sxs-lookup"><span data-stu-id="d2131-479">**SDL Phase**</span></span>               | <span data-ttu-id="d2131-480">Compilare</span><span class="sxs-lookup"><span data-stu-id="d2131-480">Build</span></span> |  
| <span data-ttu-id="d2131-481">**Tecnologie applicabili**</span><span class="sxs-lookup"><span data-stu-id="d2131-481">**Applicable Technologies**</span></span> | <span data-ttu-id="d2131-482">MVC 5, MVC 6</span><span class="sxs-lookup"><span data-stu-id="d2131-482">MVC5, MVC6</span></span> |
| <span data-ttu-id="d2131-483">**Attributes (Attributi) (Attributi)**</span><span class="sxs-lookup"><span data-stu-id="d2131-483">**Attributes**</span></span>              | <span data-ttu-id="d2131-484">Provider di identità: AD FS, provider di identità: Azure AD</span><span class="sxs-lookup"><span data-stu-id="d2131-484">Identity Provider - ADFS, Identity Provider - Azure AD</span></span> |
| <span data-ttu-id="d2131-485">**Riferimenti**</span><span class="sxs-lookup"><span data-stu-id="d2131-485">**References**</span></span>              | <span data-ttu-id="d2131-486">[Secure a Web API with Individual Accounts and Local Login in ASP.NET Web API 2.2](http://www.asp.net/web-api/overview/security/individual-accounts-in-web-api) (Proteggere un'API Web con account singoli e account di accesso locale in API Web ASP.NET 2.2)</span><span class="sxs-lookup"><span data-stu-id="d2131-486">[Secure a Web API with Individual Accounts and Local Login in ASP.NET Web API 2.2](http://www.asp.net/web-api/overview/security/individual-accounts-in-web-api)</span></span> |
| <span data-ttu-id="d2131-487">**Passaggi**</span><span class="sxs-lookup"><span data-stu-id="d2131-487">**Steps**</span></span> | <span data-ttu-id="d2131-488">Se hello API Web è protetto tramite OAuth 2.0, quindi è previsto che un token di connessione nella richiesta dell'intestazione e concede l'accesso toohello richiesta di autorizzazione solo se il token hello è valido.</span><span class="sxs-lookup"><span data-stu-id="d2131-488">If hello Web API is secured using OAuth 2.0, then it expects a bearer token in Authorization request header and grants access toohello request only if hello token is valid.</span></span> <span data-ttu-id="d2131-489">A differenza dell'autenticazione basata su cookie, i browser non collegare toorequests i token di connessione hello.</span><span class="sxs-lookup"><span data-stu-id="d2131-489">Unlike cookie based authentication, browsers do not attach hello bearer tokens toorequests.</span></span> <span data-ttu-id="d2131-490">richiesta di Hello client deve tooexplicitly collegare il token di connessione hello nell'intestazione della richiesta hello.</span><span class="sxs-lookup"><span data-stu-id="d2131-490">hello requesting client needs tooexplicitly attach hello bearer token in hello request header.</span></span> <span data-ttu-id="d2131-491">Per le API Web ASP.NET protette con OAuth 2.0, i token di connessione vengono quindi considerati una difesa contro gli attacchi basati su richieste intersito false.</span><span class="sxs-lookup"><span data-stu-id="d2131-491">Therefore, for ASP.NET Web APIs protected using OAuth 2.0, bearer tokens are considered as a defense against CSRF attacks.</span></span> <span data-ttu-id="d2131-492">Si noti che se un'applicazione hello parte MVC hello utilizza l'autenticazione basata su form (ad esempio, utilizza cookie), i token antifalsificazione toobe usato dall'app web MVC di hello.</span><span class="sxs-lookup"><span data-stu-id="d2131-492">Please note that if hello MVC portion of hello application uses forms authentication (i.e., uses cookies), anti-forgery tokens have toobe used by hello MVC web app.</span></span> |

### <a name="example"></a><span data-ttu-id="d2131-493">Esempio</span><span class="sxs-lookup"><span data-stu-id="d2131-493">Example</span></span>
<span data-ttu-id="d2131-494">API Web Hello è toobe informati toorely solo i token di connessione e non su cookie.</span><span class="sxs-lookup"><span data-stu-id="d2131-494">hello Web API has toobe informed toorely ONLY on bearer tokens and not on cookies.</span></span> <span data-ttu-id="d2131-495">Può essere eseguita da hello seguente configurazione in `WebApiConfig.Register` metodo: ' ' configurazione di codice C#. SuppressDefaultHostAuthentication(); configurazione. Filters. Add (nuovo HostAuthenticationFilter(OAuthDefaults.AuthenticationType));</span><span class="sxs-lookup"><span data-stu-id="d2131-495">It can be done by hello following configuration in `WebApiConfig.Register` method: ``\`C-Sharp code config.SuppressDefaultHostAuthentication(); config.Filters.Add(new HostAuthenticationFilter(OAuthDefaults.AuthenticationType));</span></span>
```
hello SuppressDefaultHostAuthentication method tells Web API tooignore any authentication that happens before hello request reaches hello Web API pipeline, either by IIS or by OWIN middleware. That way, we can restrict Web API tooauthenticate only using bearer tokens.
