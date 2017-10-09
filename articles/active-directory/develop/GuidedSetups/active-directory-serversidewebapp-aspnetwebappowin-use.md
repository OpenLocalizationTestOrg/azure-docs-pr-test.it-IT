---
title: aaaAzure AD v2 ASP.NET Web Server Getting Started - utilizzo | Documenti Microsoft
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
ms.openlocfilehash: 03afce6fa6598215e8c4af841c00762c143a0cd4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
## <a name="add-a-controller-toohandle-sign-in-and-sign-out-requests"></a>Aggiungere richieste di accesso e disconnessione toohandle un controller

Questo passaggio viene illustrato come un nuovo tooexpose controller toocreate Accedi e i metodi di disconnessione.

1.  Fare clic con il pulsante destro hello `Controllers` cartella e scegliere`Add` > `Controller`
2.  Selezionare `MVC (.NET version) Controller – Empty`.
3.  Fare clic su *Aggiungi*.
4.  Assegnare il nome `HomeController` e fare clic su *Aggiungi*.
5.  Aggiungere *OWIN* fa riferimento la classe toohello:

```csharp
using Microsoft.Owin.Security;
using Microsoft.Owin.Security.Cookies;
using Microsoft.Owin.Security.OpenIdConnect;
```
<!-- Workaround for Docs conversion bug -->
<ol start="6">
<li>
Aggiungere due metodi di hello sotto toohandle accesso e disconnessione tooyour controller avviando una richiesta di autenticazione tramite codice:
</li>
</ol>

```csharp
/// <summary>
/// Send an OpenID Connect sign-in request.
/// Alternatively, you can just decorate hello SignIn method with hello [Authorize] attribute
/// </summary>
public void SignIn()
{
    if (!Request.IsAuthenticated)
    {
        HttpContext.GetOwinContext().Authentication.Challenge(
            new AuthenticationProperties{ RedirectUri = "/" },
            OpenIdConnectAuthenticationDefaults.AuthenticationType);
    }
}

/// <summary>
/// Send an OpenID Connect sign-out request.
/// </summary>
public void SignOut()
{
    HttpContext.GetOwinContext().Authentication.SignOut(
            OpenIdConnectAuthenticationDefaults.AuthenticationType,
            CookieAuthenticationDefaults.AuthenticationType);
}
```

## <a name="create-hello-apps-home-page-toosign-in-users-via-a-sign-in-button"></a>Creare toosign pagina iniziale dell'applicazione hello in utenti tramite un pulsante di accesso

In Visual Studio, creare un nuova visualizzazione tooadd hello-pulsante Accedi e visualizzare le informazioni utente dopo l'autenticazione:

1.  Fare clic con il pulsante destro hello `Views\Home` cartella e scegliere`Add View`
2.  Denominarlo `Index`.
3.  Aggiungere hello HTML, che include hello-pulsante Accedi, toohello file seguenti:

```html
<html>
<head>
    <meta name="viewport" content="width=device-width" />
    <title>Sign-In with Microsoft Guide</title>
</head>
<body>
@if (!Request.IsAuthenticated)
{
    <!-- If hello user is not authenticated, display hello sign-in button -->
    <a href="@Url.Action("SignIn", "Home")" style="text-decoration: none;">
        <svg xmlns="http://www.w3.org/2000/svg" xml:space="preserve" width="300px" height="50px" viewBox="0 0 3278 522" class="SignInButton">
        <style type="text/css">.fil0:hover {fill: #4B4B4B;} .fnt0 {font-size: 260px;font-family: 'Segoe UI Semibold', 'Segoe UI'; text-decoration: none;}</style>
        <rect class="fil0" x="2" y="2" width="3174" height="517" fill="black" />
        <rect x="150" y="129" width="122" height="122" fill="#F35325" />
        <rect x="284" y="129" width="122" height="122" fill="#81BC06" />
        <rect x="150" y="263" width="122" height="122" fill="#05A6F0" />
        <rect x="284" y="263" width="122" height="122" fill="#FFBA08" />
        <text x="470" y="357" fill="white" class="fnt0">Sign in with Microsoft</text>
        </svg>
    </a>
}
else
{
    <span><br/>Hello @System.Security.Claims.ClaimsPrincipal.Current.FindFirst("name").Value;</span>
    <br /><br />
    @Html.ActionLink("See Your Claims", "Index", "Claims")
    <br /><br />
    @Html.ActionLink("Sign out", "SignOut", "Home")
}
@if (!string.IsNullOrWhiteSpace(Request.QueryString["errormessage"]))
{
    <div style="background-color:red;color:white;font-weight: bold;">Error: @Request.QueryString["errormessage"]</div>
}
</body>
</html>
```
<!--start-collapse-->
### <a name="more-information"></a>Altre informazioni
> Questa pagina aggiunge un pulsante di accesso in formato SVG con sfondo nero:<br/>![Pulsante "Accedi con Microsoft"](media/active-directory-serversidewebapp-aspnetwebappowin-use/aspnetsigninbuttonsample.png)<br/> Per i pulsanti di segno più, visitare toohello [questa pagina](https://docs.microsoft.com/azure/active-directory/develop/active-directory-branding-guidelines "linee guida del marchio").
<!--end-collapse-->

## <a name="add-a-controller-toodisplay-users-claims"></a>Aggiungere le attestazioni dell'utente toodisplay controller
Questo controller illustra hello utilizza di hello `[Authorize]` attributo tooprotect un controller. Questo attributo limita controller toohello accesso consentendo solo utenti autenticati. Hello di codice riportato di seguito utilizza le attestazioni utente toodisplay degli attributi hello che sono state recuperate come parte di hello sign-in.

1.  Fare clic con il pulsante destro hello `Controllers` cartella:`Add` > `Controller`
2.  Selezionare `MVC {version} Controller – Empty`.
3.  Fare clic su *Aggiungi*.
4.  Assegnare il nome `ClaimsController`
5.  Sostituire il codice hello della classe controller con codice hello seguente - aggiunge hello `[Authorize]` toohello classe di attributo:

```csharp
[Authorize]
public class ClaimsController : Controller
{
    /// <summary>
    /// Add user's claims tooviewbag
    /// </summary>
    /// <returns></returns>
    public ActionResult Index()
    {
        var claimsPrincipalCurrent = System.Security.Claims.ClaimsPrincipal.Current;
        //You get hello user’s first and last name below:
        ViewBag.Name = claimsPrincipalCurrent.FindFirst("name").Value;

        // hello 'preferred_username' claim can be used for showing hello username
        ViewBag.Username = claimsPrincipalCurrent.FindFirst("preferred_username").Value;

        // hello subject claim can be used toouniquely identify hello user across hello web
        ViewBag.Subject = claimsPrincipalCurrent.FindFirst(System.Security.Claims.ClaimTypes.NameIdentifier).Value;

        // TenantId is hello unique Tenant Id - which represents an organization in Azure AD
        ViewBag.TenantId = claimsPrincipalCurrent.FindFirst("http://schemas.microsoft.com/identity/claims/tenantid").Value;

        return View();
    }
}
```

<!--start-collapse-->
### <a name="more-information"></a>Altre informazioni
> A causa di utilizzo di hello di hello `[Authorize]` attributo, tutti i metodi di questo controller può essere eseguita solo se hello utente è autenticato. Se l'utente hello non viene autenticato e tenta di controller hello tooaccess, OWIN verrà avviare una richiesta di autenticazione e forzare tooauthenticate utente hello. raccolta di hello delle attestazioni codice Hello sopra esamina hello `ClaimsPrincipal.Current` istanza per gli attributi utente specifico, incluse nel token dell'utente hello. Questi attributi includono nome completo dell'utente hello e nome utente, nonché soggetto di identificatore hello utente globale. Contiene inoltre hello *ID Tenant*, che rappresenta l'ID di hello per l'organizzazione dell'utente hello. 
<!--end-collapse-->

## <a name="create-a-view-toodisplay-hello-users-claims"></a>Creare una vista attestazioni dell'utente di hello toodisplay

In Visual Studio, creare una nuova vista attestazioni dell'utente di toodisplay hello in una pagina web:

1.  Fare clic con il pulsante destro hello `Views\Claims` cartella e:`Add View`
2.  Denominarlo `Index`.
3.  Aggiungere i seguenti file toohello HTML hello:

```html
<html>
<head>
    <meta name="viewport" content="width=device-width" />
    <title>Sign-In with Microsoft Sample</title>
    <link href="@Url.Content("~/Content/bootstrap.min.css")" rel="stylesheet" type="text/css" />
</head>
<body style="padding:50px">
    <h3>Main Claims:</h3>
    <table class="table table-striped table-bordered table-hover">
        <tr><td>Name</td><td>@ViewBag.Name</td></tr>
        <tr><td>Username</td><td>@ViewBag.Username</td></tr>
        <tr><td>Subject</td><td>@ViewBag.Subject</td></tr>
        <tr><td>TenantId</td><td>@ViewBag.TenantId</td></tr>
    </table>
    <br />
    <h3>All Claims:</h3>
    <table class="table table-striped table-bordered table-hover table-condensed">
    @foreach (var claim in System.Security.Claims.ClaimsPrincipal.Current.Claims)
    {
        <tr><td>@claim.Type</td><td>@claim.Value</td></tr>
    }
</table>
    <br />
    <br />
    @Html.ActionLink("Sign out", "SignOut", "Home", null, new { @class = "btn btn-primary" })
</body>
</html>
```
