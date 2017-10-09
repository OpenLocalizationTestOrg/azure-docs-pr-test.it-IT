---
title: app web .NET di aaaAzure AD introduzione | Documenti Microsoft
description: Compilare un'app Web .NET MVC che si integra con Azure AD per l'accesso.
services: active-directory
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: e15a41a4-dc5d-4c90-b3fe-5dc33b9a1e96
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 6d3098c9e3d7e1916ccb110c703f501ae52e788f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="aspnet-web-app-sign-in-and-sign-out-with-azure-ad"></a>Accesso e disconnessione all'app Web ASP.NET con Azure AD
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

Fornendo un singolo accesso e disconnessione con poche righe di codice, Azure Active Directory (Azure AD) rende più semplice è toooutsource app web gestione delle identità. È possibile firmare gli utenti da e verso le app web ASP.NET tramite l'implementazione Microsoft di hello dell'interfaccia Web aperta per il middleware .NET (OWIN). Il middleware OWIN gestito dalla community è incluso in .NET Framework 4.5. Questo articolo viene illustrato come toouse OWIN per:

* Accesso agli utenti in tooweb App usando Azure AD come provider di identità hello.
* Visualizzare alcune informazioni sugli utenti.
* Accesso agli utenti fuori hello app.

## <a name="before-you-get-started"></a>Prima di iniziare
* Scaricare hello [scheletro app](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/skeleton.zip) o scaricare hello [esempio completo](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/complete.zip).
* È inoltre necessario un tenant di Azure Active Directory nella quale app hello tooregister. Se si dispone già di un tenant di Azure AD, [informazioni su come tooget uno](active-directory-howto-tenant.md).

Quando si è pronti, seguire le procedure di hello in hello quattro sezioni.

## <a name="step-1-register-hello-new-app-with-azure-ad"></a>Passaggio 1: Registrare hello nuova app con Azure AD
tooset configurazione degli utenti di hello app tooauthenticate, innanzitutto effettuare la registrazione nel tenant di eseguendo hello seguenti:

1. Accedi toohello [portale di Azure](https://portal.azure.com).
2. Nella barra superiore hello, scegliere il nome dell'account. In hello **Directory** elenco, in cui si desidera tooregister hello app tenant di Active Directory selezionare hello.
3. Fare clic su **più servizi** in hello riquadro sinistro e quindi selezionare **Azure Active Directory**.
4. Fare clic su **Registrazioni per l'app** e scegliere **Aggiungi**.
5. Seguire hello richiede toocreate un nuovo **applicazione Web e/o WebAPI**.
  * **Nome** descrive toousers app hello.
  * **URL Sign-On** è l'URL di base dell'applicazione hello hello. URL predefinito dell'ossatura Hello è https://localhost:44320 /.
6. Dopo aver completato la registrazione di hello, Azure AD le assegna app hello un ID applicazione univoco. Copiare il valore di hello hello app pagina toouse nelle sezioni successive di hello.
7. Da hello **impostazioni** -> **proprietà** pagina per l'applicazione, aggiornare hello URI ID App. Hello **URI ID App** è un identificatore univoco per l'applicazione hello. Hello convenzione di denominazione è `https://<tenant-domain>/<app-name>` (ad esempio, `https://contoso.onmicrosoft.com/my-first-aad-app`).

## <a name="step-2-set-up-hello-app-toouse-hello-owin-authentication-pipeline"></a>Passaggio 2: Impostare la pipeline di autenticazione OWIN hello app toouse hello
In questo passaggio verranno configurati hello OWIN middleware toouse hello OpenID Connect protocollo di autenticazione. Utilizzare le richieste di accesso e disconnessione tooissue OWIN, gestire le sessioni utente, ottenere le informazioni utente e così via.

1. toobegin, aggiungere il progetto toohello pacchetti NuGet di hello OWIN middleware utilizzando la Console di gestione pacchetti hello.

     ```
     PM> Install-Package Microsoft.Owin.Security.OpenIdConnect
     PM> Install-Package Microsoft.Owin.Security.Cookies
     PM> Install-Package Microsoft.Owin.Host.SystemWeb
     ```

2. chiamata di un progetto di avvio di OWIN classe toohello tooadd `Startup.cs`, fare clic sul progetto hello, selezionare **Aggiungi**selezionare **nuovo elemento**e quindi cercare **OWIN**. middleware OWIN Hello richiama hello **Configuration(...)**  metodo hello app all'avvio.
3. Modificare la dichiarazione di classe hello troppo`public partial class Startup`. Parte di questa classe è stata già implementata in un altro file. In hello **Configuration(...)**  (metodo), effettuare una chiamata troppo**ConfgureAuth(...)**  tooset autenticazione per l'applicazione hello.  

     ```C#
     public partial class Startup
     {
         public void Configuration(IAppBuilder app)
         {
             ConfigureAuth(app);
         }
     }
     ```

4. Aprire il file App_Start\Startup.Auth.cs hello e quindi implementare hello **ConfigureAuth(...)**  metodo. parametri che vengono forniti in Hello *OpenIDConnectAuthenticationOptions* fungono da coordinate per hello app toocommunicate con Azure AD. È necessario anche tooset di autenticazione dei cookie, perché il middleware di OpenID Connect hello utilizza i cookie in background hello.

     ```C#
     public void ConfigureAuth(IAppBuilder app)
     {
         app.SetDefaultSignInAsAuthenticationType(CookieAuthenticationDefaults.AuthenticationType);

         app.UseCookieAuthentication(new CookieAuthenticationOptions());

         app.UseOpenIdConnectAuthentication(
             new OpenIdConnectAuthenticationOptions
             {
                 ClientId = clientId,
                 Authority = authority,
                 PostLogoutRedirectUri = postLogoutRedirectUri,
                 Notifications = new OpenIdConnectAuthenticationNotifications
                    {
                        AuthenticationFailed = context =>
                        {
                            context.HandleResponse();
                            context.Response.Redirect("/Error?message=" + context.Exception.Message);
                            return Task.FromResult(0);
                        }
                    }
             });
     }
     ```

5. Aprire hello. config nella directory radice del progetto hello hello e quindi immettere i valori di configurazione hello in hello `<appSettings>` sezione.
  * `ida:ClientId`: hello GUID copiato dalla hello portale di Azure in "passaggio 1: registrare hello nuova app con Azure AD."
  * `ida:Tenant`: nome hello del tenant di Azure AD (ad esempio, contoso.onmicrosoft.com).
  * `ida:PostLogoutRedirectUri`: indicatore di hello che indica AD Azure in cui un utente dovrebbe essere reindirizzato dopo una richiesta di disconnessione è stata completata.

## <a name="step-3-use-owin-tooissue-sign-in-and-sign-out-requests-tooazure-ad"></a>Passaggio 3: Usare OWIN tooissue accesso e disconnessione richiede tooAzure AD
applicazione Hello è ora toocommunicate configurato correttamente con Azure AD con protocollo di autenticazione OpenID Connect hello. OWIN gestita tutti hello dettagli di creazione di messaggi di autenticazione, convalida dei token da Azure AD e la gestione delle sessioni utente. Che rimane è toogive agli utenti un modo toosign in sia di disconnessione.

1. È possibile utilizzare autorizzare tag toosign di utenti toorequire il controller in prima dell'accesso a determinate pagine. toodo in tal caso, aprire controllers\homecontroller.cs. e quindi aggiungere hello `[Authorize]` tag toohello sul controller.

     ```C#
     [Authorize]
     public ActionResult About()
     {
       ...
     ```

2. È inoltre possibile utilizzare OWIN toodirectly problema delle richieste di autenticazione all'interno del codice. toodo scopo, aprire Controllers\AccountController.cs. In azioni hello SignIn() e SignOut () problema challenge OpenID Connect e richieste di disconnessione.

     ```C#
     public void SignIn()
     {
         // Send an OpenID Connect sign-in request.
         if (!Request.IsAuthenticated)
         {
             HttpContext.GetOwinContext().Authentication.Challenge(new AuthenticationProperties { RedirectUri = "/" }, OpenIdConnectAuthenticationDefaults.AuthenticationType);
         }
     }
     public void SignOut()
     {
         // Send an OpenID Connect sign-out request.
         HttpContext.GetOwinContext().Authentication.SignOut(
              OpenIdConnectAuthenticationDefaults.AuthenticationType, CookieAuthenticationDefaults.AuthenticationType);
     }
     ```

3. Aprire Views\Shared\_LoginPartial.cshtml tooshow hello utente hello app accesso e disconnessione dei collegamenti e tooprint il nome dell'utente hello in una vista.

    ```HTML
    @if (Request.IsAuthenticated)
    {
     <text>
         <ul class="nav navbar-nav navbar-right">
             <li class="navbar-text">
                 Hello, @User.Identity.Name!
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

## <a name="step-4-display-user-information"></a>Passaggio 4: visualizzare le informazioni utente
Quando autentica gli utenti con OpenID Connect, Azure AD restituisce un'app toohello id_token che contiene "attestazioni", o asserzioni sull'utente hello. È possibile usare queste app di hello toopersonalize basata su attestazioni eseguendo hello seguenti:

1. Aprire il file controllers\homecontroller.cs. hello. È possibile accedere attestazioni dell'utente hello nei controller di tramite hello `ClaimsPrincipal.Current` oggetto entità di sicurezza.

 ```C#
 public ActionResult About()
 {
     ViewBag.Name = ClaimsPrincipal.Current.FindFirst(ClaimTypes.Name).Value;
     ViewBag.ObjectId = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/objectidentifier").Value;
     ViewBag.GivenName = ClaimsPrincipal.Current.FindFirst(ClaimTypes.GivenName).Value;
     ViewBag.Surname = ClaimsPrincipal.Current.FindFirst(ClaimTypes.Surname).Value;
     ViewBag.UPN = ClaimsPrincipal.Current.FindFirst(ClaimTypes.Upn).Value;

     return View();
 }
 ```

2. Compilare ed eseguire l'applicazione hello. Se è già stato creato un nuovo utente nel tenant con un dominio onmicrosoft.com, è pertanto toodo ora hello. Ecco come:

  a. Accedere con tale utente e prendere nota come identità dell'utente hello si riflette nella barra superiore hello.

  b. Disconnettersi e accedere nuovamente come un altro utente nel tenant.

  c. Se lo si desidera, per vedere Single Sign-On in azione, registrare ed eseguire un'altra istanza di questa app (con il suo clientId).

## <a name="next-steps"></a>Passaggi successivi
Per riferimento, vedere [: esempio hello completato](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/complete.zip) (senza i valori di configurazione).

È possibile procedere con toomore argomenti avanzati. Provare ad esempio [Proteggere un'API Web con Azure AD](active-directory-devquickstarts-webapi-dotnet.md).

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
