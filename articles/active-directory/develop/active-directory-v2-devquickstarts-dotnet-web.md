---
title: v 2.0 aaaAzure AD .NET web app Accedi introduzione | Documenti Microsoft
description: Come toobuild un'App Web di MVC .NET che esegue l'accesso agli utenti con entrambi Account Microsoft personale e gli account aziendali o dell'istituto di istruzione.
services: active-directory
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: c8b97ac6-0a06-4367-81b6-7d1d98152b14
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 241e9c90bd752fbecc3696ce4f1bed3f9772189d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="add-sign-in-tooan-net-mvc-web-app"></a>Aggiungere app web di accesso tooan MVC .NET
Con l'endpoint di hello v 2.0, è possibile aggiungere rapidamente applicazioni web per l'autenticazione tooyour con supporto per entrambi gli account Microsoft personali e gli account aziendali o dell'istituto di istruzione.  Nelle app Web ASP.NET, a questo scopo si usa il middleware OWIN di Microsoft incluso in .NET Framework 4.5.

> [!NOTE]
> Non tutte le caratteristiche e gli scenari di Azure Active Directory sono supportati dall'endpoint di hello v 2.0.  toodetermine se è necessario utilizzare endpoint v 2.0 hello, conoscenza [limitazioni v 2.0](active-directory-v2-limitations.md).
>
>

 Qui creeremo un'app web che usa utente OWIN toosign hello in, visualizzare alcune informazioni sull'utente hello e sign hello utente all'esterno dell'app hello.

## <a name="download"></a>Scaricare
codice Hello per questa esercitazione viene mantenuto [su GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet).  toofollow lungo, è possibile [scheletro hello dell'app come un file ZIP di download](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet/archive/skeleton.zip) o scheletro hello clone:

```git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet.git```

app Hello completato è disponibile alla fine hello anche in questa esercitazione.

## <a name="register-an-app"></a>Registrare un'app
Creare una nuova app in [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) o seguire questa [procedura dettagliata](active-directory-v2-app-registration.md).  Verificare di:

* Copia verso il basso hello **Id applicazione** assegnato tooyour app, è necessario prima.
* Aggiungere hello **Web** piattaforma per l'app.
* Immettere hello corretto **URI di reindirizzamento**. uri di reindirizzamento Hello indica tooAzure Active Directory in cui devono essere indirizzate le risposte di autenticazione: hello valore predefinito per questa esercitazione è `https://localhost:44326/`.

## <a name="install--configure-owin-authentication"></a>Installare e configurare l'autenticazione OWIN
In questo caso, è possibile configurare hello OWIN middleware toouse hello OpenID Connect protocollo di autenticazione.  OWIN verrà essere tooissue utilizzato le richieste di accesso e disconnessione, gestire la sessione dell'utente hello e ottenere informazioni sull'utente hello, tra l'altro.

1. toobegin, aprire hello `web.config` file nella directory radice del progetto hello hello e immettere i valori di configurazione dell'applicazione in hello `<appSettings>` sezione.

  * Hello `ida:ClientId` è hello **Id applicazione** assegnato tooyour app nel portale di registrazione hello.
  * Hello `ida:RedirectUri` è hello **Uri di reindirizzamento** immesso nel portale di hello.

2. Successivamente, aggiungere hello OWIN middleware NuGet pacchetti toohello progetto utilizzando la Console di gestione pacchetti hello.

        ```
        PM> Install-Package Microsoft.Owin.Security.OpenIdConnect
        PM> Install-Package Microsoft.Owin.Security.Cookies
        PM> Install-Package Microsoft.Owin.Host.SystemWeb
        ```  

3. Aggiungi un progetto di toohello "Classe di avvio di OWIN" denominato `Startup.cs` destro fare clic sul progetto hello--> **Aggiungi** --> **nuovo elemento** --> ricerca per "OWIN".  middleware OWIN Hello richiamerà hello `Configuration(...)` metodo all'avvio dell'app.
4. Modificare anche la dichiarazione di classe hello`public partial class Startup` -è stato già parte di questa classe è implementato in un altro file.  In hello `Configuration(...)` (metodo), apportare una tooset tooConfigureAuth(...) chiamata di autenticazione per l'app web  

        ```C#
        [assembly: OwinStartup(typeof(Startup))]
        
        namespace TodoList_WebApp
        {
            public partial class Startup
            {
                public void Configuration(IAppBuilder app)
                {
                    ConfigureAuth(app);
                }
            }
        }
        ```

5. File aperti hello `App_Start\Startup.Auth.cs` e implementare hello `ConfigureAuth(...)` metodo.  parametri che vengono forniti in Hello `OpenIdConnectAuthenticationOptions` fungerà da coordinate per toocommunicate l'app con Azure AD.  È anche necessario tooset Cookie di autenticazione: hello middleware di OpenID Connect utilizza i cookie sotto copre hello.

        ```C#
        public void ConfigureAuth(IAppBuilder app)
                     {
                             app.SetDefaultSignInAsAuthenticationType(CookieAuthenticationDefaults.AuthenticationType);
        
                             app.UseCookieAuthentication(new CookieAuthenticationOptions());
        
                             app.UseOpenIdConnectAuthentication(
                                     new OpenIdConnectAuthenticationOptions
                                     {
                                             // hello `Authority` represents hello v2.0 endpoint - https://login.microsoftonline.com/common/v2.0
                                             // hello `Scope` describes hello permissions that your app will need.  See https://azure.microsoft.com/documentation/articles/active-directory-v2-scopes/
                                             // In a real application you could use issuer validation for additional checks, like making sure hello user's organization has signed up for your app, for instance.
        
                                             ClientId = clientId,
                                             Authority = String.Format(CultureInfo.InvariantCulture, aadInstance, "common", "/v2.0"),
                                             RedirectUri = redirectUri,
                                             Scope = "openid email profile",
                                             ResponseType = "id_token",
                                             PostLogoutRedirectUri = redirectUri,
                                             TokenValidationParameters = new TokenValidationParameters
                                             {
                                                     ValidateIssuer = false,
                                             },
                                             Notifications = new OpenIdConnectAuthenticationNotifications
                                             {
                                                     AuthenticationFailed = OnAuthenticationFailed,
                                             }
                                     });
                     }
        ```

## <a name="send-authentication-requests"></a>Invio di richieste di autenticazione
L'app è configurato correttamente toocommunicate con endpoint v 2.0 hello utilizzando hello protocollo di autenticazione OpenID Connect.  OWIN ha preso in considerazione tutti i dettagli di propriamente hello di creazione di messaggi di autenticazione, convalida dei token da Azure AD e la gestione sessione utente.  Che rimane è toogive agli utenti un modo toosign in sia di disconnessione.

- È possibile utilizzare autorizzare tag in toorequire il controller che l'utente accede prima di accedere a una determinata pagina.  Aprire `Controllers\HomeController.cs`e aggiungere hello `[Authorize]` tag toohello sul controller.
        
        ```C#
        [Authorize]
        public ActionResult About()
        {
          ...
        ```

- È inoltre possibile utilizzare OWIN toodirectly problema delle richieste di autenticazione all'interno del codice.  Aprire `Controllers\AccountController.cs`.  In hello SignIn() e azioni SignOut (), emettere challenge OpenID Connect e richieste di disconnessione, rispettivamente.

        ```C#
        public void SignIn()
        {
            // Send an OpenID Connect sign-in request.
            if (!Request.IsAuthenticated)
            {
                HttpContext.GetOwinContext().Authentication.Challenge(new AuthenticationProperties { RedirectUri = "/" }, OpenIdConnectAuthenticationDefaults.AuthenticationType);
            }
        }
        
        // BUGBUG: Ending a session with hello v2.0 endpoint is not yet supported.  Here, we just end hello session with hello web app.  
        public void SignOut()
        {
            // Send an OpenID Connect sign-out request.
            HttpContext.GetOwinContext().Authentication.SignOut(CookieAuthenticationDefaults.AuthenticationType);
            Response.Redirect("/");
        }
        ```

- Ora aprire `Views\Shared\_LoginPartial.cshtml`,  Si tratta in cui verranno Mostra utente hello collegamenti di accesso e disconnessione dell'app e stampare il nome dell'utente hello in una vista.

        ```HTML
        @if (Request.IsAuthenticated)
        {
            <text>
                <ul class="nav navbar-nav navbar-right">
                    <li class="navbar-text">
        
                        @*hello 'preferred_username' claim can be used for showing hello user's primary way of identifying themselves.*@
        
                        Hello, @(System.Security.Claims.ClaimsPrincipal.Current.FindFirst("preferred_username").Value)!
                    </li>
                    <li>
                        @Html.ActionLink("Sign out", "SignOut", "Account")
                    </li>
                </ul>
            </text>
        }
        else
        {
            <ul class="nav navbar-nav navbar-right">
                <li>@Html.ActionLink("Sign in", "SignIn", "Account", routeValues: null, htmlAttributes: new { id = "loginLink" })</li>
            </ul>
        }
        ```

## <a name="display-user-information"></a>Visualizzare le informazioni utente
Quando l'autenticazione degli utenti con OpenID Connect, l'endpoint v 2.0 hello restituisce un'app toohello id_token contenente attestazioni o asserzioni sull'utente hello.  È possibile utilizzare questi toopersonalize attestazioni app:

- Aprire hello `Controllers\HomeController.cs` file.  È possibile accedere attestazioni dell'utente hello nei controller di tramite hello `ClaimsPrincipal.Current` oggetto entità di sicurezza.

        ```C#
        [Authorize]
        public ActionResult About()
        {
            ViewBag.Name = ClaimsPrincipal.Current.FindFirst("name").Value;
        
            // hello object ID claim will only be emitted for work or school accounts at this time.
            Claim oid = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/objectidentifier");
            ViewBag.ObjectId = oid == null ? string.Empty : oid.Value;
        
            // hello 'preferred_username' claim can be used for showing hello user's primary way of identifying themselves
            ViewBag.Username = ClaimsPrincipal.Current.FindFirst("preferred_username").Value;
        
            // hello subject or nameidentifier claim can be used toouniquely identify hello user
            ViewBag.Subject = ClaimsPrincipal.Current.FindFirst("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier").Value;
        
            return View();
        }
        ```

## <a name="run"></a>Esegui
Infine compilare ed eseguire l'app.   Accedere con un Account Microsoft personale o un account aziendale o dell'istituto di istruzione e notare come identità dell'utente hello si riflette nella barra di spostamento superiore hello.  È ora disponibile un'app Web protetta usando protocolli standard del settore in grado di autenticare gli utenti con account personali, aziendali e dell'istituto di istruzione.

Per riferimento, hello completata esempio (senza i valori di configurazione) [viene fornito come un file ZIP qui](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet/archive/complete.zip), oppure duplicarlo da GitHub:

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet.git```

## <a name="next-steps"></a>Passaggi successivi
Ora è possibile passare ad argomenti più avanzati.  È opportuno tootry:

[Proteggere un'API Web con endpoint di hello hello v 2.0 >>](active-directory-devquickstarts-webapi-dotnet.md)

Per altre risorse, vedere:

* [Guida per sviluppatori v 2.0 Hello >>](active-directory-appmodel-v2-overview.md)
* [StackOverflow: tag "azure-active-directory" >>](http://stackoverflow.com/questions/tagged/azure-active-directory)

## <a name="get-security-updates-for-our-products"></a>Ottenere aggiornamenti della sicurezza per i prodotti
Si consiglia di generazione di eventi di sicurezza, visitare il sito di notifica tooget [questa pagina](https://technet.microsoft.com/security/dd252948) e la sottoscrizione di avvisi consultivo tooSecurity.
