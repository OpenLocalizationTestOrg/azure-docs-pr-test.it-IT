---
title: aaaAzure AD .NET web API introduzione | Documenti Microsoft
description: Come toobuild un'API web MVC .NET che si integra con Azure AD per l'autenticazione e autorizzazione.
services: active-directory
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 67e74774-1748-43ea-8130-55275a18320f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 91c93e1fe18855f5648076e59e2ccf081eec34bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="help-protect-a-web-api-by-using-bearer-tokens-from-azure-ad"></a>Proteggere un'API Web usando token di connessione di Azure AD
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

Se si sta creando un'applicazione che fornisce l'accesso alle risorse tooprotected, è necessario tooknow modalità di accesso alle risorse toothose tooprevent non autorizzata.
Azure Active Directory (Azure AD) rende più semplice e diretto toohelp proteggere un'API web tramite i token di accesso di connessione OAuth 2.0 con poche righe di codice.

Nelle App web ASP.NET, è possibile eseguire questa protezione tramite l'implementazione Microsoft di hello di hello basato sulla community middleware OWIN incluso in .NET Framework 4.5. In questo caso si userà OWIN toobuild un'API web "tooDo elenco" che:

* Designare le API protette.
* Convalida che le chiamate API web hello contengano un token di accesso valido.

toobuild hello tooDo API elenco, è innanzitutto necessario:

1. Registrare un'applicazione con Azure AD.
2. Impostare la pipeline di autenticazione OWIN hello app toouse hello.
3. Configurare un client applicazione toocall hello API web.

tooget avviato, [scaricare scheletro app hello](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/skeleton.zip) o [scaricare l'esempio hello completato](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/complete.zip). Ognuno è una soluzione di Visual Studio 2013. È inoltre necessario un tenant di Azure Active Directory in cui tooregister l'applicazione. Se non hai già fatto, [informazioni su come tooget uno](active-directory-howto-tenant.md).

## <a name="step-1-register-an-application-with-azure-ad"></a>Passaggio 1: Registrare un'applicazione con Azure AD
toohelp proteggere l'applicazione, è innanzitutto necessario toocreate un'applicazione nel tenant di fornire AD Azure con poche alcune informazioni fondamentali.

1. Accedi toohello [portale di Azure](https://portal.azure.com).

2. Nella barra superiore hello, fare clic sull'account. In hello **Directory** scegliere tenant hello Azure Active Directory in cui si desidera tooregister l'applicazione.

3. Fare clic su **più servizi** in hello riquadro sinistro e quindi selezionare **Azure Active Directory**.

4. Fare clic su **Registrazioni per l'app** e scegliere **Aggiungi**.

5. Seguire le istruzioni di hello e creare un nuovo **applicazione Web e/o API Web**.
  * **Nome** descrive toousers l'applicazione. Immettere **tooDo servizio elenco**.
  * **Uri di reindirizzamento** è una combinazione di schema e di stringa usato da Azure AD tooreturn qualsiasi token che è richiesta l'app. Immettere `https://localhost:44321/` per questo valore.

6. Da hello **impostazioni** -> **proprietà** pagina per l'applicazione, aggiornare hello URI ID App. Immettere un identificatore specifico del tenant. Ad esempio, immettere `https://contoso.onmicrosoft.com/TodoListService`.

7. Salvare la configurazione di hello. Lasciare aperta, portale hello perché è necessario anche tooregister l'applicazione client a breve.

## <a name="step-2-set-up-hello-app-toouse-hello-owin-authentication-pipeline"></a>Passaggio 2: Impostare la pipeline di autenticazione OWIN hello app toouse hello
le richieste in ingresso toovalidate e i token, è necessario tooset backup toocommunicate l'applicazione con Azure AD.

1. toobegin, aprire la soluzione hello e aggiungere progetto TodoListService hello OWIN middleware NuGet pacchetti toohello utilizzando la Console di gestione pacchetti hello.

    ```
    PM> Install-Package Microsoft.Owin.Security.ActiveDirectory -ProjectName TodoListService
    PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TodoListService
    ```

2. Aggiungere un progetto TodoListService di avvio di OWIN classi toohello denominato `Startup.cs`.  Progetto di hello pulsante destro del mouse, selezionare **Aggiungi** > **nuovo elemento**e quindi cercare **OWIN**. middleware OWIN Hello richiamerà hello `Configuration(…)` metodo all'avvio dell'app.

3. Modificare la dichiarazione di classe hello troppo`public partial class Startup`. Parte di questa classe è stata già implementata in un altro file. In hello `Configuration(…)` (metodo), effettuare una chiamata troppo`ConfgureAuth(…)` tooset autenticazione per l'app web.

    ```C#
    public partial class Startup
    {
        public void Configuration(IAppBuilder app)
        {
            ConfigureAuth(app);
        }
    }
    ```

4. File aperti hello `App_Start\Startup.Auth.cs` e implementare hello `ConfigureAuth(…)` metodo. Hello parametri forniti nella `WindowsAzureActiveDirectoryBearerAuthenticationOptions` fungerà da coordinate per toocommunicate l'app con Azure AD.

    ```C#
    public void ConfigureAuth(IAppBuilder app)
    {
        app.UseWindowsAzureActiveDirectoryBearerAuthentication(
            new WindowsAzureActiveDirectoryBearerAuthenticationOptions
            {
                Audience = ConfigurationManager.AppSettings["ida:Audience"],
                Tenant = ConfigurationManager.AppSettings["ida:Tenant"]
            });
    }
    ```

5. È ora possibile usare `[Authorize]` toohelp attributi proteggere i controller e azioni con l'autenticazione della connessione JSON Web Token (JWT). Decorare hello `Controllers\TodoListController.cs` classe con un tag authorize. Questa operazione forzerà toosign utente hello in prima di accedere a tale pagina.

    ```C#
    [Authorize]
    public class TodoListController : ApiController
    {
    ```

    Quando un chiamante autorizzato correttamente richiama uno di hello `TodoListController` API, azione hello potrebbe essere necessario accedere tooinformation sul chiamante hello. OWIN fornisce accesso toohello attestazioni in token di connessione hello tramite hello `ClaimsPrincpal` oggetto.  

6. Un requisito comune per l'API web è toovalidate hello "ambiti, presenti nel token hello. In questo modo si garantisce che l'utente hello ha accettato le condizioni toohello le autorizzazioni necessarie tooaccess hello tooDo servizio elenco.

    ```C#
    public IEnumerable<TodoItem> Get()
    {
        // user_impersonation is hello default permission exposed by applications in Azure AD
        if (ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/scope").Value != "user_impersonation")
        {
            throw new HttpResponseException(new HttpResponseMessage {
              StatusCode = HttpStatusCode.Unauthorized,
              ReasonPhrase = "hello Scope claim does not contain 'user_impersonation' or scope claim not found"
            });
        }
        ...
    }
    ```

7. Aprire hello `web.config` file nella directory radice del progetto TodoListService hello hello e immettere i valori di configurazione in hello `<appSettings>` sezione.
  * `ida:Tenant`è il nome di hello del tenant di Azure AD, ad esempio, contoso.onmicrosoft.com.
  * `ida:Audience`è hello URI ID App dell'applicazione hello immesso nel portale di Azure hello.

## <a name="step-3-configure-a-client-application-and-run-hello-service"></a>Passaggio 3: Configurare un'applicazione client ed eseguire il servizio di hello
Prima di poter visualizzare hello tooDo elenco servizio in azione, è necessario tooconfigure hello tooDo elenco client affinché possa ottenere i token da Azure AD e rendere chiamate toohello servizio.

1. Tornare indietro toohello [portale di Azure](https://portal.azure.com).

2. Creare una nuova applicazione nel tenant di Azure AD e selezionare **applicazione Client nativa** nel prompt di hello risultante.
  * **Nome** descrive toousers l'applicazione.
  * Immettere `http://TodoListClient/` per hello **Uri di reindirizzamento** valore.

3. Dopo aver completato la registrazione, Azure AD le assegna un'app di tooyour ID applicazione univoco. È necessario che questo valore in passaggi successivi hello, quindi copiarlo dalla pagina dell'applicazione hello.

4. Da hello **impostazioni** selezionare **autorizzazioni obbligatorie**e quindi selezionare **Aggiungi**. Individuare e selezionare hello tooDo servizio elenco, aggiungere hello **accesso TodoListService** autorizzazione in **autorizzazioni delegate**, quindi fare clic su **eseguita**.

5. In Visual Studio, aprire `App.config` in hello TodoListClient progetto e quindi immettere i valori di configurazione in hello `<appSettings>` sezione.

  * `ida:Tenant`è il nome di hello del tenant di Azure AD, ad esempio, contoso.onmicrosoft.com.
  * `ida:ClientId`è l'ID app hello copiata dal portale di Azure hello.
  * `todo:TodoListResourceId`è l'URI ID App hello tooDo applicazione di servizio elenco immesso nel portale di Azure hello hello.

## <a name="next-steps"></a>Passaggi successivi
Infine pulire, compilare ed eseguire ogni progetto. Se hai già fatto, è ora hello tempo toocreate un nuovo utente nel tenant con un *. dominio onmicrosoft.com. Eseguire l'accesso client di elenco tooDo toohello con tale utente e aggiungere l'elenco attività dell'utente toohello alcune attività.

Per riferimento, è disponibile in: esempio hello completata (senza i valori di configurazione) [GitHub](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/complete.zip). È possibile procedere in scenari con identità toomore.

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
