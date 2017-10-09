---
title: aaaAdd tooa accesso API web MVC .NET utilizzando hello endpoint v 2.0 di Azure AD | Documenti Microsoft
description: Come toobuild un'Api Web MVC di .NET che accetta i token da entrambi Account Microsoft personale e gli account aziendali o dell'istituto di istruzione.
services: active-directory
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: e77bc4e0-d0c9-4075-a3f6-769e2c810206
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 4e517145422bb6e9368e82a7eef4a5c57cce530a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="secure-an-mvc-web-api"></a>Proteggere un'API Web MVC
Con l'endpoint di Azure Active Directory hello v 2.0, è possibile proteggere un utilizzo di API Web [OAuth 2.0](active-directory-v2-protocols.md) i token di accesso, l'attivazione di utenti con entrambi account Microsoft personale e gli account aziendali o dell'istituto di istruzione toosecurely accedere l'API Web.

> [!NOTE]
> Non tutte le caratteristiche e gli scenari di Azure Active Directory sono supportati dall'endpoint di hello v 2.0.  toodetermine se è necessario utilizzare endpoint v 2.0 hello, conoscenza [limitazioni v 2.0](active-directory-v2-limitations.md).
>
>

Nelle API Web ASP.NET, a questo scopo si usa il middleware OWIN di Microsoft incluso in .NET Framework 4.5.  In questo caso si userà OWIN toobuild un'API Web MVC di "tooDo elenco" che consente ai client toocreate e leggere le attività dall'elenco di attività dell'utente.  API web Hello convalida che le richieste in ingresso contengono un token di accesso valido e rifiutare le richieste che non passano la convalida su una route protetta.  Questo esempio è stato creato con Visual Studio 2015.

## <a name="download"></a>Scaricare
codice Hello per questa esercitazione viene mantenuto [su GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet).  toofollow lungo, è possibile [scheletro hello dell'app come un file ZIP di download](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/skeleton.zip) o scheletro hello clone:

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet.git
```

app scheletro Hello include tutto il codice boilerplate hello per una semplice API, ma mancano le parti relative alle identità hello. Se non si desidera toofollow lungo, è possibile clonare o [scaricare l'esempio hello completato](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/complete.zip).

```
git clone https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet.git
```

## <a name="register-an-app"></a>Registrare un'app
Creare una nuova app in [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) o seguire questa [procedura dettagliata](active-directory-v2-app-registration.md).  Verificare di:

* Copia verso il basso hello **Id applicazione** assegnato tooyour app, è necessario prima.

Questa soluzione di visual studio contiene anche una "TodoListClient", che è una semplice applicazione WPF.  Hello TodoListClient è toodemonstrate utilizzato come un accesso dell'utente e la modalità con cui un client può inviare richieste tooyour API Web.  In questo caso, sia hello TodoListClient hello TodoListService sono rappresentati da e hello stessa app.  tooconfigure hello TodoListClient, è inoltre necessario:

* Aggiungere hello **Mobile** piattaforma per l'app.

## <a name="install-owin"></a>Installare OWIN
Una volta registrato un'app, è necessario tooset backup toocommunicate l'app con endpoint v 2.0 hello in richieste in ingresso di ordine toovalidate & token.

* toobegin, aprire la soluzione hello e aggiungere hello OWIN middleware NuGet pacchetti toohello progetto TodoListService utilizzando Console Gestione pacchetti hello.

```
PM> Install-Package Microsoft.Owin.Security.OAuth -ProjectName TodoListService
PM> Install-Package Microsoft.Owin.Security.Jwt -ProjectName TodoListService
PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TodoListService
PM> Install-Package Microsoft.IdentityModel.Protocol.Extensions -ProjectName TodoListService
```

## <a name="configure-oauth-authentication"></a>Configurare l'autenticazione OAuth
* Aggiungere un progetto TodoListService di avvio di OWIN classi toohello denominato `Startup.cs`.  --> Destro fare clic sul progetto hello **Aggiungi** --> **nuovo elemento** --> ricerca per "OWIN".  middleware OWIN Hello richiamerà hello `Configuration(…)` metodo all'avvio dell'app.
* Modificare anche la dichiarazione di classe hello`public partial class Startup` -è stato già parte di questa classe è implementato in un altro file.  In hello `Configuration(…)` (metodo), apportare una tooset tooConfgureAuth(...) chiamata di autenticazione per l'app web.

```C#
public partial class Startup
{
    public void Configuration(IAppBuilder app)
    {
        ConfigureAuth(app);
    }
}
```

* File aperti hello `App_Start\Startup.Auth.cs` e implementare hello `ConfigureAuth(…)` metodo, che verrà configurati i token di tooaccept hello Web API dall'endpoint di hello v 2.0.

```C#
public void ConfigureAuth(IAppBuilder app)
{
        var tvps = new TokenValidationParameters
        {
                // In this app, hello TodoListClient and TodoListService
                // are represented using hello same Application Id - we use
                // hello Application Id toorepresent hello audience, or the
                // intended recipient of tokens.

                ValidAudience = clientId,

                // In a real applicaiton, you might use issuer validation to
                // verify that hello user's organization (if applicable) has
                // signed up for hello app.  Here, we'll just turn it off.

                ValidateIssuer = false,
        };

        // Set up hello OWIN pipeline toouse OAuth 2.0 Bearer authentication.
        // hello options provided here tell hello middleware about hello type of tokens
        // that will be recieved, which are JWTs for hello v2.0 endpoint.

        // NOTE: hello usual WindowsAzureActiveDirectoryBearerAuthenticaitonMiddleware uses a
        // metadata endpoint which is not supported by hello v2.0 endpoint.  Instead, this
        // OpenIdConenctCachingSecurityTokenProvider can be used toofetch & use hello OpenIdConnect
        // metadata document.

        app.UseOAuthBearerAuthentication(new OAuthBearerAuthenticationOptions
        {
                AccessTokenFormat = new Microsoft.Owin.Security.Jwt.JwtFormat(tvps, new OpenIdConnectCachingSecurityTokenProvider("https://login.microsoftonline.com/common/v2.0/.well-known/openid-configuration")),
        });
}
```

* È ora possibile usare `[Authorize]` attributi tooprotect i controller e azioni con l'autenticazione della connessione OAuth 2.0.  Decorare hello `Controllers\TodoListController.cs` classe con un tag authorize.  Questa operazione forzerà toosign utente hello in prima di accedere a tale pagina.

```C#
[Authorize]
public class TodoListController : ApiController
{
```

* Quando un chiamante autorizzato correttamente richiama uno di hello `TodoListController` API, azione hello potrebbe essere necessario accedere tooinformation sul chiamante hello.  OWIN fornisce accesso toohello attestazioni in token di connessione hello tramite hello `ClaimsPrincpal` oggetto.  

```C#
public IEnumerable<TodoItem> Get()
{
    // You can use hello ClaimsPrincipal tooaccess information about the
    // user making hello call.  In this case, we use hello 'sub' or
    // NameIdentifier claim tooserve as a key for hello tasks in hello data store.

    Claim subject = ClaimsPrincipal.Current.FindFirst(ClaimTypes.NameIdentifier);

    return from todo in todoBag
           where todo.Owner == subject.Value
           select todo;
}
```

* Infine, aprire hello `web.config` file nella directory radice del progetto TodoListService hello hello e immettere i valori di configurazione in hello `<appSettings>` sezione.
  * Il `ida:Audience` è hello **Id applicazione** dell'app hello immesso nel portale di hello.

## <a name="configure-hello-client-app"></a>Configurare l'applicazione client hello
Prima di poter visualizzare hello servizio elenco attività nell'azione, è necessario tooconfigure hello Client elenco attività, affinché possa ottenere token dall'endpoint v 2.0 hello e rendere chiamate toohello servizio.

* Nel progetto TodoListClient hello aprire `App.config` e immettere i valori di configurazione in hello `<appSettings>` sezione.
  * Il `ida:ClientId` Id applicazione copiata dal portale hello.

Infine pulire, compilare ed eseguire ogni progetto.  È ora disponibile un'API Web .NET MVC che accetta token da account Microsoft personali, aziendali e dell'istituto di istruzione.  Accedere al hello TodoListClient e chiamare l'elenco di attività web api tooadd attività toohello dell'utente.

Per riferimento, hello completata esempio (senza i valori di configurazione) [viene fornito come un file ZIP qui](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/complete.zip), oppure duplicarlo da GitHub:

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet.git```

## <a name="next-steps"></a>Passaggi successivi
È ora possibile passare ad altri argomenti.  È opportuno tootry:

[Chiamare un'API Web da un'app Web &gt;&gt;](active-directory-v2-devquickstarts-webapp-webapi-dotnet.md)

Per altre risorse, vedere:

* [Guida per sviluppatori v 2.0 Hello >>](active-directory-appmodel-v2-overview.md)
* [StackOverflow: tag "azure-active-directory" >>](http://stackoverflow.com/questions/tagged/azure-active-directory)

## <a name="get-security-updates-for-our-products"></a>Ottenere aggiornamenti della sicurezza per i prodotti
Si consiglia di generazione di eventi di sicurezza, visitare il sito di notifica tooget [questa pagina](https://technet.microsoft.com/security/dd252948) e la sottoscrizione di avvisi consultivo tooSecurity.
