---
title: Active Directory B2C aaaAzure | Documenti Microsoft
description: Come toobuild un'API Web .NET utilizzando Active B2C Directory di Azure, protette con token di accesso OAuth 2.0 per l'autenticazione.
services: active-directory-b2c
documentationcenter: .net
author: parakhj
manager: krassk
editor: 
ms.assetid: 7146ed7f-2eb5-49e9-8d8b-ea1a895e1966
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 03/17/2017
ms.author: parakhj
ms.openlocfilehash: d45364216deda38ef44b60dd11e86d9a089ad509
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-build-a-net-web-api"></a>Azure Active Directory B2C: compilare un'API Web .NET

Azure Active Directory (Azure AD) B2C permette di proteggere un'API Web usando i token di accesso OAuth 2.0. Questi token consentono al client App tooauthenticate toohello API. Questo articolo illustra come toocreate un'API di .NET MVC "elenco" che consente agli utenti del client attività tooCRUD dell'applicazione. API web Hello sia protetta con Azure Active Directory B2C e consente solo agli utenti autenticati toomanage proprio elenco di attività da eseguire.

## <a name="create-an-azure-ad-b2c-directory"></a>Creare una directory Azure AD B2C

Prima di poter usare Azure AD B2C, è necessario creare una directory, o tenant. Una directory è un contenitore per utenti, app, gruppi e così via. Se non è già stato fatto, [creare una directory B2C](active-directory-b2c-get-started.md) prima di proseguire con questa guida.

> [!NOTE]
> un'applicazione client Hello e API web devono utilizzare directory B2C hello stesso Azure Active Directory.
>

## <a name="create-a-web-api"></a>Creare un'API Web

Successivamente, è necessario toocreate un'app di API web nella directory B2C. In questo modo le informazioni di Azure AD che è necessario toosecurely a comunicare con l'app. toocreate un'app, seguire [queste istruzioni](active-directory-b2c-app-registration.md). Assicurarsi di:

* Includere un **app web** o **web API** in un'applicazione hello.
* Hello utilizzare **URI di reindirizzamento** `https://localhost:44332/` per l'app web hello. Questo è il percorso predefinito hello del client di app web hello per questo esempio di codice.
* Hello copia **ID applicazione** ovvero tooyour assegnato app. Sarà necessario più avanti.
* Immettere un identificatore app in **URI ID app**.
* Aggiungere le autorizzazioni tramite hello **pubblicati ambiti** menu.

  [!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a>Creare i criteri

In Azure AD B2C ogni esperienza utente è definita da [criteri](active-directory-b2c-reference-policies.md)specifici. Sarà necessario toocreate toocommunicate un criterio con Azure Active Directory B2C. È consigliabile utilizzare hello combinazione sign-configurazione/sign-in criteri, come descritto in hello [articolo di riferimento dei criteri](active-directory-b2c-reference-policies.md). Durante la creazione dei criteri, assicurarsi di:

* Scegliere **Nome visualizzato** e altri attributi di iscrizione nei criteri.
* Scegliere le attestazioni **Nome visualizzato** e **ID oggetto** come attestazioni dell'applicazione in tutti i criteri. È consentito scegliere anche altre attestazioni.
* Hello copia **nome** dei criteri dopo averlo creato. È necessario il nome di criterio hello in un secondo momento.

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

Dopo avere creato i criteri di hello, si è pronti toobuild l'app.

## <a name="download-hello-code"></a>Scaricare codice hello

codice Hello per questa esercitazione viene mantenuto nel [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi). È possibile clonare: esempio hello eseguendo:

```console
git clone https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi.git
```

Dopo aver scaricato il codice di esempio hello, verrà avviato tooget file con estensione sln di hello aprire Visual Studio. file di soluzione Hello contiene due progetti: `TaskWebApp` e `TaskService`. `TaskWebApp`è un'applicazione web MVC hello utente interagisce con. `TaskService`è l'API web back-end dell'applicazione hello che archivia l'elenco di attività di ogni utente. Questo articolo viene illustrato solo hello `TaskService` dell'applicazione. toolearn come toobuild `TaskWebApp` tramite Azure Active Directory B2C, vedere [l'esercitazione di app web .NET](active-directory-b2c-devquickstarts-web-dotnet-susi.md).

### <a name="update-hello-azure-ad-b2c-configuration"></a>Aggiornare la configurazione di hello Azure Active Directory B2C

L'esempio è configurato toouse hello criteri e i client ID dei nostri tenant dimostrativo. Se si desidera toouse il proprio tenant, sarà necessario hello toodo seguenti:

1. Aprire `web.config` in hello `TaskService` progetti e sostituire i valori hello per
    * `ida:Tenant` con il nome del tenant
    * `ida:ClientId` con l'ID dell'applicazione API Web
    * `ida:SignUpSignInPolicyId` con il nome del criterio "Iscrizione o accesso"

2. Aprire `web.config` in hello `TaskWebApp` progetti e sostituire i valori hello per
    * `ida:Tenant` con il nome del tenant
    * `ida:ClientId` con l'ID dell'applicazione di tipo app Web
    * `ida:ClientSecret` con la chiave privata dell'app Web
    * `ida:SignUpSignInPolicyId` con il nome del criterio "Iscrizione o accesso"
    * `ida:EditProfilePolicyId` con il nome del criterio "Modifica profilo"
    * `ida:ResetPasswordPolicyId` con il nome del criterio "Reimposta password"


## <a name="secure-hello-api"></a>Proteggi hello API

Quando è disponibile un client che chiama l'API, è possibile proteggere l'API, ad esempio `TaskService`, usando i token di connessione OAuth 2.0. In questo modo si garantisce che ogni API tooyour richiesta sarà valido solo se la richiesta hello dispone di un token di connessione. L'API può accettare e convalidare i token di connessione usando la libreria OWIN (Open Web Interface for .NET) di Microsoft.

### <a name="install-owin"></a>Installare OWIN

Iniziare con l'installazione della pipeline di autenticazione OAuth OWIN hello utilizzando hello Console di gestione di pacchetti di Visual Studio.

```Console
PM> Install-Package Microsoft.Owin.Security.OAuth -ProjectName TaskService
PM> Install-Package Microsoft.Owin.Security.Jwt -ProjectName TaskService
PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TaskService
```

Middleware OWIN hello che verrà accettati e convalidati i token di connessione verrà installato.

### <a name="add-an-owin-startup-class"></a>Aggiungere una classe di avvio OWIN

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

### <a name="configure-oauth-20-authentication"></a>Configurare l'autenticazione OAuth 2.0

File aperti hello `App_Start\Startup.Auth.cs`e implementare hello `ConfigureAuth(...)` metodo. Ad esempio, potrebbe avere questo aspetto hello seguente:

```CSharp
// App_Start\Startup.Auth.cs

 public partial class Startup
    {
        // These values are pulled from web.config
        public static string AadInstance = ConfigurationManager.AppSettings["ida:AadInstance"];
        public static string Tenant = ConfigurationManager.AppSettings["ida:Tenant"];
        public static string ClientId = ConfigurationManager.AppSettings["ida:ClientId"];
        public static string SignUpSignInPolicy = ConfigurationManager.AppSettings["ida:SignUpSignInPolicyId"];
        public static string DefaultPolicy = SignUpSignInPolicy;

        /*
         * Configure hello authorization OWIN middleware.
         */
        public void ConfigureAuth(IAppBuilder app)
        {
            TokenValidationParameters tvps = new TokenValidationParameters
            {
                // Accept only those tokens where hello audience of hello token is equal toohello client ID of this app
                ValidAudience = ClientId,
                AuthenticationType = Startup.DefaultPolicy
            };

            app.UseOAuthBearerAuthentication(new OAuthBearerAuthenticationOptions
            {
                // This SecurityTokenProvider fetches hello Azure AD B2C metadata & signing keys from hello OpenIDConnect metadata endpoint
                AccessTokenFormat = new JwtFormat(tvps, new OpenIdConnectCachingSecurityTokenProvider(String.Format(AadInstance, Tenant, DefaultPolicy)))
            });
        }
    }
```

### <a name="secure-hello-task-controller"></a>Proteggere i controller di attività hello

Dopo l'applicazione hello è autenticazione configurata toouse OAuth 2.0, è possibile proteggere l'API web mediante l'aggiunta di un `[Authorize]` controller attività toohello di tag. Questo è il controller hello in cui tutte le relative modifiche elenco attività viene eseguita, pertanto è consigliabile proteggere i controller di intero hello a livello di classe hello. È inoltre possibile aggiungere hello `[Authorize]` tag azioni tooindividual per un controllo più accurato.

```CSharp
// Controllers\TasksController.cs

[Authorize]
public class TasksController : ApiController
{
    ...
}
```

### <a name="get-user-information-from-hello-token"></a>Ottenere le informazioni utente da hello token

`TasksController`Archivia le attività in un database in cui ogni attività dispone di un utente associato "proprietario" attività hello. proprietario Hello è identificato da dell'utente hello **ID di oggetto**. (Questo è il motivo è necessario l'ID di oggetto hello tooadd come un'applicazione in tutti i criteri di attestazione.)

```CSharp
// Controllers\TasksController.cs

public IEnumerable<Models.Task> Get()
{
    string owner = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/objectidentifier").Value;
    IEnumerable<Models.Task> userTasks = db.Tasks.Where(t => t.owner == owner);
    return userTasks;
}
```

### <a name="validate-hello-permissions-in-hello-token"></a>Convalidare le autorizzazioni di hello nel token hello

Un requisito comune per l'API web è toovalidate hello "ambiti, presenti nel token hello. In questo modo si garantisce che l'utente hello ha accettato le condizioni del servizio di elenco attività toohello autorizzazioni tooaccess obbligatorio hello.

```CSharp
public IEnumerable<Models.Task> Get()
{
    if (ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/scope").Value != "read")
    {
        throw new HttpResponseException(new HttpResponseMessage {
            StatusCode = HttpStatusCode.Unauthorized,
            ReasonPhrase = "hello Scope claim does not contain 'read' or scope claim not found"
        });
    }
    ...
}
```

## <a name="run-hello-sample-app"></a>Eseguire app di esempio hello

Compilare ed eseguire infine `TaskWebApp` e `TaskService`. Creare alcune attività nell'elenco attività dell'utente hello e notare come vengono rese persistenti nell'API hello anche dopo l'arresto e riavvio di client hello.

## <a name="edit-your-policies"></a>Modificare i criteri

Dopo essersi assicurati un'API con Azure Active Directory B2C, è possibile utilizzare i criteri Sign-in/iscrizione e visualizzare gli effetti di hello (o assenza) su hello API. È possibile modificare le attestazioni applicazione hello nei criteri hello e modificare le informazioni utente hello disponibile nell'API web hello. Tutte le attestazioni che aggiungono sarà API web MVC .NET di tooyour disponibile in hello `ClaimsPrincipal` oggetto, come descritto in precedenza in questo articolo.
