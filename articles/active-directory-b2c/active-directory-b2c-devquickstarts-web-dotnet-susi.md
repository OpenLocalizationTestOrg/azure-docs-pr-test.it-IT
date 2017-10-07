---
title: Active Directory B2C aaaAzure | Documenti Microsoft
description: Come toobuild un'applicazione web con sign-configurazione/Accedi, profilare, modifica e la password reimpostato tramite Azure Active Directory B2C.
services: active-directory-b2c
documentationcenter: .net
author: parakhj
manager: krassk
editor: barbaraselden
ms.assetid: 30261336-d7a5-4a6d-8c1a-7943ad76ed25
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/17/2017
ms.author: parakhj
ms.openlocfilehash: 187f99a8dd50d212de4f0517f552cdbbe5a8edf4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-aspnet-web-app-with-azure-active-directory-b2c-sign-up-sign-in-profile-edit-and-password-reset"></a>Creare un'app Web ASP.NET con criteri di iscrizione, accesso, modifica del profilo e reimpostazione della password di Azure Active Directory B2C

Questa esercitazione illustra come:

> [!div class="checklist"]
> * Aggiungere app web di Azure Active Directory B2C identità funzionalità tooyour
> * Registrare l'app Web nella directory Azure AD B2C
> * Creare criteri di iscrizione/accesso, modifica del profilo e reimpostazione della password per l'app Web

## <a name="prerequisites"></a>Prerequisiti

- È necessario connettere l'account di Azure di tooan B2C Tenant. È possibile creare un account Azure gratuito [qui](https://azure.microsoft.com/en-us/).
- È necessario [Microsoft Visual Studio](https://www.visualstudio.com/) o programma tooview e modificare il codice di esempio hello simili.

## <a name="create-an-azure-ad-b2c-directory"></a>Creare una directory Azure AD B2C

Prima di poter usare Azure AD B2C, è necessario creare una directory, o tenant. Una directory è un contenitore per utenti, app, gruppi e altro ancora. Se non è già stato fatto, creare una directory B2C prima di continuare con questa guida.

[!INCLUDE [active-directory-b2c-create-tenant](../../includes/active-directory-b2c-create-tenant.md)]

> [!NOTE]
> 
> È necessario tooconnect hello B2C Tenant tooyour sottoscrizione di Azure. Dopo aver selezionato **crea**selezionare hello **toomy collegamento un esistente AD B2C Azure Tenant sottoscrizione di Azure** opzione e quindi in hello **Tenant di Azure Active Directory B2C** elenco a discesa, selezionare tenant Hello desiderato tooassociate.

## <a name="create-and-register-an-application"></a>Creare e registrare un'applicazione

Successivamente, è necessario toocreate e registrare app hello nella directory B2C. Fornisce informazioni che Azure Active Directory B2C deve toosecurely comunicare con l'app. 

[!INCLUDE [active-directory-b2c-register-web-api](../../includes/active-directory-b2c-register-web-api.md)]

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

Al termine, le impostazioni dell'applicazione includeranno un'API e un'applicazione nativa.

## <a name="create-policies-on-your-b2c-tenant"></a>Creare criteri nel tenant B2C

In Azure AD B2C ogni esperienza utente è definita da [criteri](active-directory-b2c-reference-policies.md)specifici. Questo esempio di codice contiene tre esperienze di identità: **iscrizione e accesso**, **modifica del profilo** e **reimpostazione della password**.  È necessario toocreate un criterio di ogni tipo, come descritto in hello [articolo di riferimento dei criteri](active-directory-b2c-reference-policies.md). Per ogni criterio, essere attributo del nome visualizzato hello tooselect o attestazioni e toocopy verso il basso nome hello dei criteri per un uso successivo.

### <a name="add-your-identity-providers"></a>Aggiungere i provider di identità

Dalle impostazioni selezionare **Provider di identità** e scegliere l'iscrizione tramite nome utente o posta elettronica.

### <a name="create-a-sign-up-and-sign-in-policy"></a>Creare criteri di iscrizione e di accesso

[!INCLUDE [active-directory-b2c-create-sign-in-sign-up-policy](../../includes/active-directory-b2c-create-sign-in-sign-up-policy.md)]

### <a name="create-a-profile-editing-policy"></a>Creare i criteri di modifica del profilo

[!INCLUDE [active-directory-b2c-create-profile-editing-policy](../../includes/active-directory-b2c-create-profile-editing-policy.md)]

### <a name="create-a-password-reset-policy"></a>Creare i criteri di reimpostazione delle password

[!INCLUDE [active-directory-b2c-create-password-reset-policy](../../includes/active-directory-b2c-create-password-reset-policy.md)]

Dopo aver creato i criteri, si è pronti toobuild l'app.

## <a name="download-hello-sample-code"></a>Scaricare il codice di esempio hello

codice Hello per questa esercitazione viene mantenuto nel [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi). È possibile clonare: esempio hello eseguendo:

```console
git clone https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi.git
```

Dopo aver scaricato il codice di esempio hello, verrà avviato tooget file con estensione sln di hello aprire Visual Studio. file di soluzione Hello contiene due progetti: `TaskWebApp` e `TaskService`. `TaskWebApp`è hello applicazione web MVC hello utente interagisce con. `TaskService`è l'API web back-end dell'applicazione hello che archivia l'elenco di attività di ogni utente. Questo articolo viene illustrato solo hello `TaskWebApp` dell'applicazione. toolearn come toobuild `TaskService` tramite Azure Active Directory B2C, vedere [l'esercitazione di api web .NET](active-directory-b2c-devquickstarts-api-dotnet.md).

## <a name="update-code-toouse-your-tenant-and-policies"></a>Aggiornare toouse codice i criteri e i tenant

L'esempio è configurato toouse hello criteri e i client ID dei nostri tenant dimostrativo. tooconnect è tooyour proprio tenant occorre tooopen `web.config` in hello `TaskWebApp` progetti e sostituire hello seguenti valori:

* `ida:Tenant` con il nome del tenant
* `ida:ClientId` con l'ID dell'applicazione di tipo app Web
* `ida:ClientSecret` con la chiave privata dell'app Web
* `ida:SignUpSignInPolicyId` con il nome del criterio "Iscrizione o accesso"
* `ida:EditProfilePolicyId` con il nome del criterio "Modifica profilo"
* `ida:ResetPasswordPolicyId` con il nome del criterio "Reimposta password"

## <a name="launch-hello-app"></a>Avviare l'applicazione hello
All'interno di Visual Studio, avviare app hello. Spostarsi sulla scheda elenco toohello e hello nota URl è: https://login.microsoftonline.com/*YourTenantName*/oauth2/v2.0/authorize?p=*YourSignUpPolicyName*& client_id = *YourclientID*...

Iscriversi per l'applicazione hello utilizzando il nome utente o indirizzo di posta elettronica. Disconnettersi, quindi accedere di nuovo e modificare il profilo di hello o reimpostare la password di hello. Disconnettersi ed eseguire l'accesso usando un account utente diverso. 

## <a name="add-social-idps"></a>Aggiungere i provider di identità per i social network

App hello supporta attualmente solo utente per l'abbonamento e Accedi con **gli account locali**; gli account archiviati nella directory B2C che utilizzano un nome utente e una password. Tramite Azure AD B2C è possibile aggiungere il supporto per altri **provider di identità** (IdP) senza modificare il codice.

tooadd social IDPs tooyour app, iniziare eseguendo hello dettagliate negli articoli seguenti. Per ogni provider di identità toosupport, è necessario tooregister un'applicazione in tale sistema e ottenere un ID client.

* [Configurare Facebook come provider di identità](active-directory-b2c-setup-fb-app.md)
* [Configurare Google come provider di identità](active-directory-b2c-setup-goog-app.md)
* [Configurare Amazon come provider di identità](active-directory-b2c-setup-amzn-app.md)
* [Configurare LinkedIn come provider di identità](active-directory-b2c-setup-li-app.md)

Dopo aver aggiunto hello identity provider tooyour directory B2C, modifica il tooinclude tre criteri hello IDPs nuovo, come descritto in hello [articolo di riferimento dei criteri](active-directory-b2c-reference-policies.md). Dopo aver salvato i criteri, eseguire l'applicazione hello nuovamente.  Dovrebbe essere hello che idps nuovo aggiunto come opzioni di accesso ed effettuare l'iscrizione in ognuna delle proprie esperienze di identità.

È possibile sperimentare i criteri e osservare l'effetto di hello nella tua app dell'esempio. Aggiungere o rimuovere provider di identità, manipolare le attestazioni dell'applicazione o modificare gli attributi per l'iscrizione. Fare delle prove fino a quando non è chiaro il modo in cui criteri, richieste di autenticazione e OWIN sono collegati tra loro.

## <a name="sample-code-walkthrough"></a>Procedura dettagliata per il codice di esempio
Hello le sezioni seguenti illustrano la configurazione del codice dell'applicazione di esempio hello. È possibile usare queste sezioni come guida per lo sviluppo dell'app.

### <a name="add-authentication-support"></a>Aggiungere il supporto per l'autenticazione

È ora possibile configurare il toouse app Azure Active Directory B2C. L'app comunica con Azure AD B2C inviando richieste di autenticazione OpenID Connect. le richieste di Hello prevedono esperienza utente hello app desidera tooexecute specificando criteri hello. È possibile utilizzare toosend libreria di Microsoft OWIN queste richieste, eseguire i criteri, gestire le sessioni utente e altro ancora.

#### <a name="install-owin"></a>Installare OWIN

toobegin, aggiungere il progetto toohello pacchetti NuGet di hello OWIN middleware utilizzando hello Console di gestione di pacchetti di Visual Studio.

```Console
PM> Install-Package Microsoft.Owin.Security.OpenIdConnect
PM> Install-Package Microsoft.Owin.Security.Cookies
PM> Install-Package Microsoft.Owin.Host.SystemWeb
```

#### <a name="add-an-owin-startup-class"></a>Aggiungere una classe di avvio OWIN

Aggiunge un toohello di classe di avvio OWIN API denominata `Startup.cs`.  Fare clic su progetto hello, selezionare **Aggiungi** e **nuovo elemento**e quindi cercare OWIN. middleware OWIN Hello richiamerà hello `Configuration(…)` metodo all'avvio dell'app.

In questo esempio, è stato modificato la dichiarazione di classe hello anche`public partial class Startup` e implementato hello altra parte della classe hello in `App_Start\Startup.Auth.cs`. Inside hello `Configuration` (metodo), è stata aggiunta una chiamata troppo`ConfigureAuth`, definito in `Startup.Auth.cs`. Dopo le modifiche di hello, `Startup.cs` sarà simile hello seguente:

```CSharp
// Startup.cs

public partial class Startup
{
    // hello OWIN middleware will invoke this method when hello app starts
    public void Configuration(IAppBuilder app)
    {
        // ConfigureAuth defined in other part of hello class
        ConfigureAuth(app);
    }
}
```

#### <a name="configure-hello-authentication-middleware"></a>Configurare il middleware di autenticazione hello

File aperti hello `App_Start\Startup.Auth.cs` e implementare hello `ConfigureAuth(...)` metodo. parametri che vengono forniti in Hello `OpenIdConnectAuthenticationOptions` fungono da coordinate per toocommunicate l'app con Azure Active Directory B2C. Se non si specifica determinati parametri, verrà utilizzato il valore di predefinito hello. Ad esempio, è stato specificato hello `ResponseType` nell'esempio hello hello così il valore predefinito `code id_token` verrà utilizzato in ogni tooAzure richiesta in uscita di Active Directory B2C.

È inoltre necessario tooset di autenticazione dei cookie. il middleware di OpenID Connect Hello utilizza le sessioni utente toomaintain i cookie, tra l'altro.

```CSharp
// App_Start\Startup.Auth.cs

public partial class Startup
{
    // Initialize variables ...

    // Configure hello OWIN middleware
    public void ConfigureAuth(IAppBuilder app)
    {
        app.UseCookieAuthentication(new CookieAuthenticationOptions());
        app.SetDefaultSignInAsAuthenticationType(CookieAuthenticationDefaults.AuthenticationType);

        app.UseOpenIdConnectAuthentication(
            new OpenIdConnectAuthenticationOptions
            {
                // Generate hello metadata address using hello tenant and policy information
                MetadataAddress = String.Format(AadInstance, Tenant, DefaultPolicy),

                // These are standard OpenID Connect parameters, with values pulled from web.config
                ClientId = ClientId,
                RedirectUri = RedirectUri,
                PostLogoutRedirectUri = RedirectUri,

                // Specify hello callbacks for each type of notifications
                Notifications = new OpenIdConnectAuthenticationNotifications
                {
                    RedirectToIdentityProvider = OnRedirectToIdentityProvider,
                    AuthorizationCodeReceived = OnAuthorizationCodeReceived,
                    AuthenticationFailed = OnAuthenticationFailed,
                },

                // Specify hello claims toovalidate
                TokenValidationParameters = new TokenValidationParameters
                {
                    NameClaimType = "name"
                },

                // Specify hello scope by appending all of hello scopes requested into one string (seperated by a blank space)
                Scope = $"{OpenIdConnectScopes.OpenId} {ReadTasksScope} {WriteTasksScope}"
            }
        );
    }

    // Implement hello "Notification" methods...
}
```

In `OpenIdConnectAuthenticationOptions` sopra, è possibile definire un set di funzioni di callback per determinate notifiche ricevute dal middleware di OpenID Connect hello. Questi comportamenti vengono definiti utilizzando un `OpenIdConnectAuthenticationNotifications` dell'oggetto e archiviati in hello `Notifications` variabile. In questo esempio, è possibile definire tre callback diversi a seconda evento hello.

### <a name="using-different-policies"></a>Uso di criteri diversi

Hello `RedirectToIdentityProvider` notifica viene attivata ogni volta che una richiesta tooAzure Active Directory B2C. Nella funzione di callback hello `OnRedirectToIdentityProvider`, controlliamo in hello in uscita chiamata se lo si desidera toouse criteri diversi. In ordine toodo reimpostare o modificare un profilo di una password, è necessario toouse criterio corrispondente di hello, ad esempio criteri anziché hello "Iscrizione o accesso" criterio di reimpostazione password hello.

In questo esempio, quando un utente richiede la password di hello tooreset o modificare il profilo di hello, aggiungiamo criteri hello preferiamo toouse nel contesto OWIN hello. Che può essere eseguita effettuando hello seguenti:

```CSharp
    // Let hello middleware know you are trying toouse hello edit profile policy
    HttpContext.GetOwinContext().Set("Policy", EditProfilePolicyId);
```

Ed è possibile implementare la funzione di callback hello `OnRedirectToIdentityProvider` eseguendo hello seguenti:

```CSharp
/*
*  On each call tooAzure AD B2C, check if a policy (e.g. hello profile edit or password reset policy) has been specified in hello OWIN context.
*  If so, use that policy when making hello call. Also, don't request a code (since it won't be needed).
*/
private Task OnRedirectToIdentityProvider(RedirectToIdentityProviderNotification<OpenIdConnectMessage, OpenIdConnectAuthenticationOptions> notification)
{
    var policy = notification.OwinContext.Get<string>("Policy");

    if (!string.IsNullOrEmpty(policy) && !policy.Equals(DefaultPolicy))
    {
        notification.ProtocolMessage.Scope = OpenIdConnectScopes.OpenId;
        notification.ProtocolMessage.ResponseType = OpenIdConnectResponseTypes.IdToken;
        notification.ProtocolMessage.IssuerAddress = notification.ProtocolMessage.IssuerAddress.Replace(DefaultPolicy, policy);
    }

    return Task.FromResult(0);
}
```

### <a name="handling-authorization-codes"></a>Gestione dei codici di autorizzazione

Hello `AuthorizationCodeReceived` notifica viene attivata quando viene ricevuto un codice di autorizzazione. il middleware di OpenID Connect Hello non supporta lo scambio di codici per i token di accesso. È possibile scambiare manualmente il codice hello per token hello in una funzione di callback. Per ulteriori informazioni, consultare hello [documentazione](active-directory-b2c-devquickstarts-web-api-dotnet.md) che spiega come.

### <a name="handling-errors"></a>Gestione degli errori

Hello `AuthenticationFailed` notifica viene attivata quando l'autenticazione non riesce. Nel relativo metodo di callback, è possibile gestire gli errori di hello nel modo desiderato. È tuttavia necessario aggiungere un controllo del codice di errore hello `AADB2C90118`. Durante l'esecuzione di hello del criterio "Iscrizione o accesso" hello, utente hello è hello opportunità tooselect un **password dimenticata?** collegamento. In questo caso, Azure Active Directory B2C invia l'app di tale codice di errore che indica che l'app deve effettuare una richiesta di usare i criteri di reimpostazione password hello.

```CSharp
/*
* Catch any failures received by hello authentication middleware and handle appropriately
*/
private Task OnAuthenticationFailed(AuthenticationFailedNotification<OpenIdConnectMessage, OpenIdConnectAuthenticationOptions> notification)
{
    notification.HandleResponse();

    // Handle hello error code that Azure AD B2C throws when trying tooreset a password from hello login page
    // because password reset is not supported by a "sign-up or sign-in policy"
    if (notification.ProtocolMessage.ErrorDescription != null && notification.ProtocolMessage.ErrorDescription.Contains("AADB2C90118"))
    {
        // If hello user clicked hello reset password link, redirect toohello reset password route
        notification.Response.Redirect("/Account/ResetPassword");
    }
    else if (notification.Exception.Message == "access_denied")
    {
        notification.Response.Redirect("/");
    }
    else
    {
        notification.Response.Redirect("/Home/Error?message=" + notification.Exception.Message);
    }

    return Task.FromResult(0);
}
```

### <a name="send-authentication-requests-tooazure-ad"></a>Inviare le richieste di autenticazione tooAzure AD

L'app è configurato correttamente toocommunicate con Azure Active Directory B2C tramite protocollo di autenticazione OpenID Connect hello. OWIN gestisce i dettagli di hello di creazione di messaggi di autenticazione, convalida dei token da Azure AD B2C e la gestione sessione utente. Che rimane è tooinitiate del flusso di ciascun utente.

Quando un utente seleziona **Sign up/Sign in**, **Modifica profilo**, o **reimpostazione password** hello web App, viene richiamata l'azione di hello associata `Controllers\AccountController.cs`:

```CSharp
// Controllers\AccountController.cs

/*
*  Called when requesting toosign up or sign in
*/
public void SignUpSignIn()
{
    // Use hello default policy tooprocess hello sign up / sign in flow
    if (!Request.IsAuthenticated)
    {
        HttpContext.GetOwinContext().Authentication.Challenge();
        return;
    }

    Response.Redirect("/");
}

/*
*  Called when requesting tooedit a profile
*/
public void EditProfile()
{
    if (Request.IsAuthenticated)
    {
        // Let hello middleware know you are trying toouse hello edit profile policy (see OnRedirectToIdentityProvider in Startup.Auth.cs)
        HttpContext.GetOwinContext().Set("Policy", Startup.EditProfilePolicyId);

        // Set hello page tooredirect tooafter editing hello profile
        var authenticationProperties = new AuthenticationProperties { RedirectUri = "/" };
        HttpContext.GetOwinContext().Authentication.Challenge(authenticationProperties);

        return;
    }

    Response.Redirect("/");

}

/*
*  Called when requesting tooreset a password
*/
public void ResetPassword()
{
    // Let hello middleware know you are trying toouse hello reset password policy (see OnRedirectToIdentityProvider in Startup.Auth.cs)
    HttpContext.GetOwinContext().Set("Policy", Startup.ResetPasswordPolicyId);

    // Set hello page tooredirect tooafter changing passwords
    var authenticationProperties = new AuthenticationProperties { RedirectUri = "/" };
    HttpContext.GetOwinContext().Authentication.Challenge(authenticationProperties);

    return;
}
```

È anche possibile utilizzare toosign OWIN utente hello dall'applicazione hello. In `Controllers\AccountController.cs` c'è:

```CSharp
// Controllers\AccountController.cs

/*
*  Called when requesting toosign out
*/
public void SignOut()
{
    // toosign out hello user, you should issue an OpenIDConnect sign out request.
    if (Request.IsAuthenticated)
    {
        IEnumerable<AuthenticationDescription> authTypes = HttpContext.GetOwinContext().Authentication.GetAuthenticationTypes();
        HttpContext.GetOwinContext().Authentication.SignOut(authTypes.Select(t => t.AuthenticationType).ToArray());
        Request.GetOwinContext().Authentication.GetAuthenticationTypes();
    }
}
```

In aggiunta tooexplicitly richiamare un criterio, è possibile utilizzare un `[Authorize]` tag nei controller di che viene eseguito un criterio se hello utente non è registrato. Aprire `Controllers\HomeController.cs` e aggiungere hello `[Authorize]` toohello tag attestazioni controller.  OWIN Seleziona ultimo criterio hello configurato quando hello `[Authorize]` tag viene raggiunto.

```CSharp
// Controllers\HomeController.cs

// You can use hello Authorize decorator tooexecute a certain policy if hello user is not already signed into hello app.
[Authorize]
public ActionResult Claims()
{
  ...
```

### <a name="display-user-information"></a>Visualizzare le informazioni utente

Quando si autenticano gli utenti tramite OpenID Connect, Azure AD B2C restituisce un'app toohello token ID contenente **attestazioni**. Questi sono asserzioni relative utente hello. È possibile utilizzare le attestazioni toopersonalize l'app.

Aprire hello `Controllers\HomeController.cs` file. È possibile accedere attestazioni utente nei controller di tramite hello `ClaimsPrincipal.Current` oggetto entità di sicurezza.

```CSharp
// Controllers\HomeController.cs

[Authorize]
public ActionResult Claims()
{
    Claim displayName = ClaimsPrincipal.Current.FindFirst(ClaimsPrincipal.Current.Identities.First().NameClaimType);
    ViewBag.DisplayName = displayName != null ? displayName.Value : string.Empty;
    return View();
}
```

È possibile accedere a tutte le attestazioni che l'applicazione riceve in hello stesso modo.  Un elenco di tutte le attestazioni hello riceve app hello è disponibile per l'utente in hello **attestazioni** pagina.
