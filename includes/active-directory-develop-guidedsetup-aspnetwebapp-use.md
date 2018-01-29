
## <a name="add-a-controller-to-handle-sign-in-and-sign-out-requests"></a>Aggiungere un controller per gestire le richieste di accesso e disconnessione

Questo passaggio illustra come creare un nuovo controller per esporre i metodi di accesso e disconnessione.

1.  Fare clic con il pulsante destro del mouse sulla cartella `Controllers` e scegliere `Add` > `Controller`.
2.  Selezionare `MVC (.NET version) Controller – Empty`.
3.  Fare clic su *Aggiungi*.
4.  Assegnare il nome `HomeController` e fare clic su *Aggiungi*.
5.  Aggiungere i riferimenti *OWIN* alla classe:

```csharp
using Microsoft.Owin.Security;
using Microsoft.Owin.Security.Cookies;
using Microsoft.Owin.Security.OpenIdConnect;
```
<!-- Workaround for Docs conversion bug -->
<ol start="6">
<li>
Aggiungere al controller i due metodi seguenti per gestire l'accesso e la disconnessione avviando una richiesta di autenticazione tramite codice:
</li>
</ol>

```csharp
/// <summary>
/// Send an OpenID Connect sign-in request.
/// Alternatively, you can just decorate the SignIn method with the [Authorize] attribute
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

## <a name="create-the-apps-home-page-to-sign-in-users-via-a-sign-in-button"></a>Creare la home page dell'app per l'accesso degli utenti tramite un pulsante di accesso

In Visual Studio creare una nuova visualizzazione per aggiungere il pulsante di accesso e mostrare le informazioni relative all'utente dopo l'autenticazione:

1.  Fare clic con il pulsante destro del mouse sulla cartella `Views\Home` e scegliere `Add View`.
2.  Denominarlo `Index`.
3.  Aggiungere al file il codice HTML seguente, che include il pulsante di accesso:

```html
<html>
<head>
    <meta name="viewport" content="width=device-width" />
    <title>Sign-In with Microsoft Guide</title>
</head>
<body>
@if (!Request.IsAuthenticated)
{
    <!-- If the user is not authenticated, display the sign-in button -->
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
> Questa pagina aggiunge un pulsante di accesso in formato SVG con sfondo nero:<br/>![Pulsante "Accedi con Microsoft"](media/active-directory-develop-guidedsetup-aspnetwebapp-use/aspnetsigninbuttonsample.png)<br/> Per altri pulsanti di accesso, vedere [questa pagina](https://docs.microsoft.com/azure/active-directory/develop/active-directory-branding-guidelines "Linee guida sulla personalizzazione").
<!--end-collapse-->

## <a name="add-a-controller-to-display-users-claims"></a>Aggiungere un controller per visualizzare le attestazioni dell'utente
Questo controller illustra gli usi dell'attributo `[Authorize]` per la protezione di un controller. Questo attributo limita l'accesso al controller ai soli utenti autenticati. Il codice seguente usa l'attributo per visualizzare le attestazioni utente recuperate durante l'accesso.

1.  Fare clic con il pulsante destro del mouse sulla cartella `Controllers` e scegliere `Add` > `Controller`.
2.  Selezionare `MVC {version} Controller – Empty`.
3.  Fare clic su *Aggiungi*.
4.  Assegnare il nome `ClaimsController`.
5.  Sostituire il codice della classe controller con il codice seguente, che aggiunge l'attributo `[Authorize]` alla classe:

```csharp
[Authorize]
public class ClaimsController : Controller
{
    /// <summary>
    /// Add user's claims to viewbag
    /// </summary>
    /// <returns></returns>
    public ActionResult Index()
    {
        var claimsPrincipalCurrent = System.Security.Claims.ClaimsPrincipal.Current;
        //You get the user’s first and last name below:
        ViewBag.Name = claimsPrincipalCurrent.FindFirst("name").Value;

        // The 'preferred_username' claim can be used for showing the username
        ViewBag.Username = claimsPrincipalCurrent.FindFirst("preferred_username").Value;

        // The subject claim can be used to uniquely identify the user across the web
        ViewBag.Subject = claimsPrincipalCurrent.FindFirst(System.Security.Claims.ClaimTypes.NameIdentifier).Value;

        // TenantId is the unique Tenant Id - which represents an organization in Azure AD
        ViewBag.TenantId = claimsPrincipalCurrent.FindFirst("http://schemas.microsoft.com/identity/claims/tenantid").Value;

        return View();
    }
}
```

<!--start-collapse-->
### <a name="more-information"></a>Altre informazioni
> A causa dell'uso dell'attributo `[Authorize]`, tutti i metodi di questo controller possono essere eseguiti solo se l'utente è autenticato. Se un utente non autenticato prova ad accedere al controller, OWIN avvierà una richiesta di autenticazione e imporrà all'utente di autenticarsi. Il codice riportato sopra cerca nella raccolta di attestazioni dell'istanza `ClaimsPrincipal.Current` attributi utente specifici inclusi nel token dell'utente. Tali attributi includono nome e cognome, nome utente e soggetto ID utente globale dell'utente. Contengono anche l'*ID tenant*, che rappresenta l'ID dell'organizzazione dell'utente. 
<!--end-collapse-->

## <a name="create-a-view-to-display-the-users-claims"></a>Creare una visualizzazione per mostrare le attestazioni dell'utente

In Visual Studio creare una nuova visualizzazione per mostrare le attestazioni dell'utente in una pagina Web:

1.  Fare clic con il pulsante destro del mouse sulla cartella `Views\Claims` e scegliere `Add View`.
2.  Denominarlo `Index`.
3.  Aggiungere il codice HTML seguente al file:

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
