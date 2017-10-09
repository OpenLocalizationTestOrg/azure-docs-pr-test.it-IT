---
title: aaaAzure AD v2 ASP.NET Web Server Getting Started - il programma di installazione | Documenti Microsoft
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
ms.openlocfilehash: eadc59666557e9cd294e6e99391001120579144c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
## <a name="set-up-your-project"></a>Configurare il progetto

In questa sezione Mostra tooinstall passaggi hello e configurare pipeline autenticazione hello tramite il middleware OWIN in un progetto ASP.NET utilizzando OpenID Connect. 

> Se si preferisce toodownload il progetto di Visual Studio di questo esempio invece, [Scaricare un progetto](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-DotNet/archive/master.zip) e ignorare toohello [passaggio di configurazione](#create-an-application-express) tooconfigure nell'esempio di codice hello prima dell'esecuzione.

<!--start-collapse-->
> ### <a name="create-your-aspnet-project"></a>Creare un progetto ASP.NET

> 1. In Visual Studio: `File` > `New` > `Project`<br/>
> 2. In *Visual C#\Web* selezionare `ASP.NET Web Application (.NET Framework)`
> 3. Assegnare un nome all'applicazione e fare clic su *OK*
> 4. Selezionare `Empty` e hello selezionare la casella di controllo tooadd `MVC` riferimenti
<!--end-collapse-->

## <a name="add-authentication-components"></a>Aggiungere i componenti per l'autenticazione

1. In Visual Studio: `Tools` > `Nuget Package Manager` > `Package Manager Console`
2. Aggiungere *pacchetti NuGet di middleware OWIN* digitando hello segue nella finestra della Console di gestione pacchetti hello:

```powershell
Install-Package Microsoft.Owin.Security.OpenIdConnect
Install-Package Microsoft.Owin.Security.Cookies
Install-Package Microsoft.Owin.Host.SystemWeb
```

<!--start-collapse-->
> ### <a name="about-these-libraries"></a>Informazioni sulle librerie

>librerie di Hello precedente abilitare single sign-on (SSO) tramite OpenID Connect tramite l'autenticazione basata su cookie. Dopo l'autenticazione viene completata e token di hello che rappresenta utente hello viene inviato tooyour applicazione, il middleware OWIN crea un cookie di sessione. browser Hello utilizzerà questo cookie nelle richieste successive in modo non hello richiesto tooretype la propria password, ed non è necessaria alcuna verifica aggiuntiva.
<!--end-collapse-->

## <a name="configure-hello-authentication-pipeline"></a>Configurare una pipeline di autenticazione hello
passaggi Hello riportati di seguito sono utilizzati toocreate un middleware OWIN classe Startup tooconfigure OpenID Connect all'autenticazione. Questa classe verrà eseguita automaticamente all'avvio del processo di IIS.

> Se il progetto non dispone di un `Startup.cs` file nella cartella radice hello:<br/>
> 1. Fare clic con il pulsante destro sulla cartella radice del progetto hello: >`Add` > `New Item...` > `OWIN Startup class`<br/>
> 2. Assegnare il nome `Startup.cs`

> Verificare che nella classe hello selezionata è una classe di avvio di OWIN e non una standard classe c#. Verificarlo controllando se viene visualizzato `[assembly: OwinStartup(typeof({NameSpace}.Startup))]` sopra hello dello spazio dei nomi.


1. Aggiungere *OWIN* e *Microsoft. IdentityModel* fa riferimento a troppo`Startup.cs`:

```csharp
using Microsoft.Owin;
using Owin;
using Microsoft.IdentityModel.Protocols;
using Microsoft.Owin.Security;
using Microsoft.Owin.Security.Cookies;
using Microsoft.Owin.Security.OpenIdConnect;
using Microsoft.Owin.Security.Notifications;
```
<!-- Workaround for Docs conversion bug -->
<ol start="2">
<li>
Sostituire la classe di avvio con codice hello riportato di seguito:
</li>
</ol>

```csharp
public class Startup
{        
    // hello Client ID is used by hello application toouniquely identify itself tooAzure AD.
    string clientId = System.Configuration.ConfigurationManager.AppSettings["ClientId"];

    // RedirectUri is hello URL where hello user will be redirected tooafter they sign in.
    string redirectUri = System.Configuration.ConfigurationManager.AppSettings["RedirectUri"];

    // Tenant is hello tenant ID (e.g. contoso.onmicrosoft.com, or 'common' for multi-tenant)
    static string tenant = System.Configuration.ConfigurationManager.AppSettings["Tenant"];

    // Authority is hello URL for authority, composed by Azure Active Directory v2 endpoint and hello tenant name (e.g. https://login.microsoftonline.com/contoso.onmicrosoft.com/v2.0)
    string authority = String.Format(System.Globalization.CultureInfo.InvariantCulture, System.Configuration.ConfigurationManager.AppSettings["Authority"], tenant);

    /// <summary>
    /// Configure OWIN toouse OpenIdConnect 
    /// </summary>
    /// <param name="app"></param>
    public void Configuration(IAppBuilder app)
    {
        app.SetDefaultSignInAsAuthenticationType(CookieAuthenticationDefaults.AuthenticationType);

        app.UseCookieAuthentication(new CookieAuthenticationOptions());
            app.UseOpenIdConnectAuthentication(
            new OpenIdConnectAuthenticationOptions
            {
                // Sets hello ClientId, authority, RedirectUri as obtained from web.config
                ClientId = clientId,
                Authority = authority,
                RedirectUri = redirectUri,
                // PostLogoutRedirectUri is hello page that users will be redirected tooafter sign-out. In this case, it is using hello home page
                PostLogoutRedirectUri = redirectUri,
                Scope = OpenIdConnectScopes.OpenIdProfile,
                // ResponseType is set toorequest hello id_token - which contains basic information about hello signed-in user
                ResponseType = OpenIdConnectResponseTypes.IdToken,
                // ValidateIssuer set toofalse tooallow personal and work accounts from any organization toosign in tooyour application
                // tooonly allow users from a single organizations, set ValidateIssuer tootrue and 'tenant' setting in web.config toohello tenant name
                // tooallow users from only a list of specific organizations, set ValidateIssuer tootrue and use ValidIssuers parameter 
                TokenValidationParameters = new System.IdentityModel.Tokens.TokenValidationParameters() { ValidateIssuer = false },
                // OpenIdConnectAuthenticationNotifications configures OWIN toosend notification of failed authentications tooOnAuthenticationFailed method
                Notifications = new OpenIdConnectAuthenticationNotifications
                {
                    AuthenticationFailed = OnAuthenticationFailed
                }
            }
        );
    }

    /// <summary>
    /// Handle failed authentication requests by redirecting hello user toohello home page with an error in hello query string
    /// </summary>
    /// <param name="context"></param>
    /// <returns></returns>
    private Task OnAuthenticationFailed(AuthenticationFailedNotification<OpenIdConnectMessage, OpenIdConnectAuthenticationOptions> context)
    {
        context.HandleResponse();
        context.Response.Redirect("/?errormessage=" + context.Exception.Message);
        return Task.FromResult(0);
    }
}

```
<!--start-collapse-->
> ### <a name="more-information"></a>Altre informazioni

> parametri che vengono forniti in Hello *OpenIDConnectAuthenticationOptions* fungono da coordinate per toocommunicate applicazione hello con Azure AD. Poiché il middleware di OpenID Connect hello utilizza i cookie in background hello, è necessario anche tooset autenticazione cookie come codice hello precedente. Hello *ValidateIssuer* valore indica OpenIdConnect toonot limitare l'accesso tooone specifica organizzazione.
<!--end-collapse-->

