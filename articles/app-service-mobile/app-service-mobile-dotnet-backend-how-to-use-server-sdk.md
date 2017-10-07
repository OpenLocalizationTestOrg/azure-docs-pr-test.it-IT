---
title: toowork aaaHow con server di back-end .NET hello SDK per App per dispositivi mobili | Documenti Microsoft
description: Informazioni su come toowork con hello server back-end .NET SDK per App Mobile di servizio App di Azure.
keywords: "servizio app, servizio app di Azure, app per dispositivi mobili, servizio mobile, scalabilità, scalabile, distribuzione app, distribuzione app di Azure"
services: app-service\mobile
documentationcenter: 
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 0620554f-9590-40a8-9f47-61c48c21076b
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 2946c5ba4424565ac764e2ce5597bf42362fcedf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="work-with-hello-net-backend-server-sdk-for-azure-mobile-apps"></a>Usare i server back-end di hello .NET SDK per App mobili di Azure
[!INCLUDE [app-service-mobile-selector-server-sdk](../../includes/app-service-mobile-selector-server-sdk.md)]

Questo argomento viene illustrato come toouse hello server back-end .NET SDK gli scenari principali di App Mobile di servizio App di Azure. Hello App Mobile di Azure SDK consente di lavorare con i client per dispositivi mobili da un'applicazione ASP.NET.

> [!TIP]
> Hello [server .NET SDK per App mobili di Azure] [ 2] è open source su GitHub. repository di Hello contiene tutto il codice sorgente tra gruppo di hello intero server SDK unit test e alcuni progetti di esempio.
>
>

## <a name="reference-documentation"></a>Documentazione di riferimento
documentazione di riferimento Hello per server hello SDK è disponibile in: [Azure Mobile app .NET Reference][1].

## <a name="create-app"></a>Procedura: Creare un back-end dell'app per dispositivi mobili .NET
Se si sta avviando un nuovo progetto, è possibile creare un'applicazione di servizio App utilizzando entrambi hello [portale di Azure] o Visual Studio. È possibile eseguire localmente hello applicazione di servizio App o pubblicare hello progetto tooyour basato su cloud App servizio app per dispositivi mobili.

Se si sta aggiungendo progetto esistente tooan di funzionalità per dispositivi mobili, vedere hello [scaricare e inizializzare hello SDK](#install-sdk) sezione.

### <a name="create-a-net-backend-using-hello-azure-portal"></a>Creare un back-end .NET utilizzando hello portale di Azure
toocreate un'App mobile back-end, di seguire hello [esercitazione rapida] [ 3] o eseguire la procedura seguente:

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service-classic](../../includes/app-service-mobile-dotnet-backend-create-new-service-classic.md)]

In hello *iniziare* pannello, in **creare una tabella API**, scegliere **c#** come il **language back-end**. Fare clic su **scaricare**, estrarre il progetto in formato compresso file tooyour locale computer e aprire la soluzione hello in Visual Studio.

### <a name="create-a-net-backend-using-visual-studio-2013-and-visual-studio-2015"></a>Creare un back-end .NET usando Visual Studio 2013 e Visual Studio 2015
Installare hello [Azure SDK per .NET] [ 4] (versione 2.9.0 o versione successiva) toocreate un progetto di App mobili di Azure in Visual Studio. Dopo aver installato hello SDK, è possibile creare un'applicazione ASP.NET tramite hello alla procedura seguente:

1. Aprire hello **nuovo progetto** finestra di dialogo (da *File* > **New** > **progetto...** ).
2. Espandere **Modelli** > **Visual C#** e selezionare **Web**.
3. Selezionare **Applicazione Web ASP.NET**.
4. Inserire il nome di progetto hello. Fare quindi clic su **OK**.
5. In *Modelli ASP.NET 4.5.2* selezionare **App mobile di Azure**. Controllare **Host nel cloud hello** toocreate un back-end mobile in hello cloud toowhich è possibile pubblicare il progetto.
6. Fare clic su **OK**.

## <a name="install-sdk"></a>Procedura: scaricare e inizializzare hello SDK
Hello SDK è disponibile in [NuGet.org]. Il pacchetto include tooget funzionalità di base necessarie hello avviato utilizzando hello SDK. tooinitialize hello SDK, è necessario tooperform azioni hello **HttpConfiguration** oggetto.

### <a name="install-hello-sdk"></a>Installare hello SDK
hello tooinstall SDK, destro del mouse sul progetto server hello in Visual Studio, selezionare **Gestisci pacchetti NuGet**, cercare hello [Microsoft.Azure.Mobile.Server] del pacchetto, quindi fare clic su  **Installare**.

### <a name="server-project-setup"></a>Inizializzare il progetto server hello
Un progetto server di back-end .NET è inizializzato tooother ASP.NET progetti simili, con l'inclusione di una classe di avvio OWIN. Verificare che si è fatto riferimento pacchetto NuGet hello `Microsoft.Owin.Host.SystemWeb`. Fare doppio clic su questa classe in Visual Studio, tooadd nel progetto server e selezionare **Aggiungi** >
**nuovo elemento**, quindi **Web**  >  ** Generale** > **classe di avvio di OWIN**.  Viene generata una classe con hello seguente attributo:

    [assembly: OwinStartup(typeof(YourServiceName.YourStartupClassName))]

In hello `Configuration()` metodo della classe di avvio OWIN, utilizzare un **HttpConfiguration** ambiente a oggetti tooconfigure hello App mobili di Azure.
Hello di esempio seguente consente di inizializzare il progetto server hello alcuna funzionalità aggiuntive:

    // in OWIN startup class
    public void Configuration(IAppBuilder app)
    {
        HttpConfiguration config = new HttpConfiguration();

        new MobileAppConfiguration()
            // no added features
            .ApplyTo(config);

        app.UseWebApi(config);
    }

tooenable singole funzionalità, è necessario chiamare metodi di estensione su hello **MobileAppConfiguration** oggetto prima di chiamare **ApplyTo**. Ad esempio, hello seguente di codice aggiunge predefinito hello instrada controller tooall API con attributo hello `[MobileAppController]` durante l'inizializzazione:

    new MobileAppConfiguration()
        .MapApiControllers()
        .ApplyTo(config);

avvio rapido server Hello da hello chiamate portale Azure **UseDefaultConfiguration()**. Questo toohello equivalente dopo l'installazione:

        new MobileAppConfiguration()
            .AddMobileAppHomeController()             // from hello Home package
            .MapApiControllers()
            .AddTables(                               // from hello Tables package
                new MobileAppTableConfiguration()
                    .MapTableControllers()
                    .AddEntityFramework()             // from hello Entity package
                )
            .AddPushNotifications()                   // from hello Notifications package
            .MapLegacyCrossDomainController()         // from hello CrossDomain package
            .ApplyTo(config);

metodi di estensione Hello utilizzati sono:

* `AddMobileAppHomeController()`fornisce una home page di hello predefinita App mobili di Azure.
* `MapApiControllers()`fornisce funzionalità dell'API personalizzata per i controller WebAPI decorati con hello `[MobileAppController]` attributo.
* `AddTables()`fornisce un mapping di hello `/tables` controller tootable endpoint.
* `AddTablesWithEntityFramework()`è una sintassi abbreviata per hello mapping `/tables` controller basati su endpoint che usa Entity Framework.
* `AddPushNotifications()` fornisce un semplice metodo di registrazione dei dispositivi per Hub di notifica.
* `MapLegacyCrossDomainController()` fornisce intestazioni CORS standard per lo sviluppo locale.

### <a name="sdk-extensions"></a>Estensioni SDK
Hello seguenti pacchetti di estensione basato su NuGet fornisce varie funzionalità mobile che può essere usata dall'applicazione. Abilitare le estensioni durante l'inizializzazione mediante hello **MobileAppConfiguration** oggetto.

* [Microsoft.Azure.Mobile.Server.Quickstart] supporta hello base programma di installazione di App per dispositivi mobili. Configurazione toohello aggiunto dal chiamante hello **UseDefaultConfiguration** il metodo di estensione durante l'inizializzazione. Questa estensione include le estensioni seguenti: pacchetti Notifications, Authentication, Entity, Tables, Crossdomain e Home. Questo pacchetto viene utilizzato da hello Guida introduttiva di App mobili disponibili nel portale di Azure hello.
* [Microsoft.Azure.Mobile.Server.Home](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Home/) implementa predefinito hello *questa app per dispositivi mobili sia in esecuzione pagina* per la radice del sito web di hello. Aggiungi configurazione toohello chiamando il **AddMobileAppHomeController** metodo di estensione.
* [Microsoft.Azure.Mobile.Server.Tables](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Tables/) include le classi per l'utilizzo di dati e set di backup della pipeline di dati hello. Aggiungi configurazione toohello dal chiamante hello **AddTables** metodo di estensione.
* [Microsoft.Azure.Mobile.Server.Entity](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Entity/) consente hello Entity Framework tooaccess dati hello Database SQL. Aggiungi configurazione toohello dal chiamante hello **AddTablesWithEntityFramework** metodo di estensione.
* [Microsoft.Azure.Mobile.Server.Authentication] Abilita middleware OWIN hello l'autenticazione e set di backup utilizzato toovalidate token. Aggiungi configurazione toohello dal chiamante hello **AddAppServiceAuthentication** e **IAppBuilder**. **UseAppServiceAuthentication** metodi di estensione.
* [Microsoft.Azure.Mobile.Server.Notifications] Consente le notifiche push e definisce un endpoint di registrazione push. Aggiungi configurazione toohello dal chiamante hello **AddPushNotifications** metodo di estensione.
* [Microsoft.Azure.Mobile.Server.CrossDomain](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.CrossDomain/) viene creato un controller che serve dati toolegacy browser dall'App Mobile. Aggiungi configurazione toohello chiamando il **MapLegacyCrossDomainController** metodo di estensione.
* [Microsoft.Azure.Mobile.Server.Login] fornisce il metodo AppServiceLoginHandler.CreateToken() hello, che è un metodo statico utilizzato durante gli scenari di autenticazione personalizzato.

## <a name="publish-server-project"></a>Procedura: pubblicare il progetto server di hello
In questa sezione viene illustrato come toopublish progetto back-end .NET da Visual Studio. È inoltre possibile distribuire il progetto back-end tramite Git o uno qualsiasi dei hello altri metodi descritti in hello [documentazione sulla distribuzione di servizio App di Azure](../app-service-web/web-sites-deploy.md).

1. In Visual Studio, ricompilare i pacchetti hello progetto toorestore NuGet.
2. In Esplora soluzioni, progetti hello pulsante destro del mouse, fare clic su **pubblica**. Hello prima volta che si pubblica, è necessario toodefine un profilo di pubblicazione. Se si ha già un profilo definito, è possibile selezionarlo e fare clic su **Pubblica**.
3. Se viene richiesto di tooselect una destinazione di pubblicazione, fare clic su **servizio App di Microsoft Azure** > **Avanti**, quindi, se necessario, accedi con le credenziali di Azure.
   Visual Studio scaricherà e memorizzerà le impostazioni di pubblicazione direttamente da Azure.

    ![](./media/app-service-mobile-dotnet-backend-how-to-use-server-sdk/publish-wizard-1.png)
4. Scegliere la **Sottoscrizione**, selezionare **Tipo di risorsa** da **Visualizza**, espandere **App per dispositivi mobili** e fare clic sul back-end di App per dispositivi mobili, quindi su **OK**.

    ![](./media/app-service-mobile-dotnet-backend-how-to-use-server-sdk/publish-wizard-2.png)
5. Verificare hello pubblicare informazioni sul profilo e fare clic su **pubblica**.

    ![](./media/app-service-mobile-dotnet-backend-how-to-use-server-sdk/publish-wizard-3.png)

    Quando il back-end dell'app per dispositivi mobili ha eseguito la pubblicazione, viene visualizzata una pagina di destinazione.

    ![](./media/app-service-mobile-dotnet-backend-how-to-use-server-sdk/publish-success.png)

## <a name="define-table-controller"></a> Procedura: Definire un controller tabelle
Definire un tooexpose Controller tabella un client di toomobile tabella SQL.  Per configurare un controller tabelle, sono necessari tre passaggi:

1. Creare una classe di oggetti di trasferimento dei dati.
2. Configurare un riferimento alla tabella nella classe DbContext Mobile hello.
3. Creare un controller tabelle.

Un oggetto di trasferimento dei dati è un oggetto C# normale che eredita `EntityData`.  ad esempio:

    public class TodoItem : EntityData
    {
        public string Text { get; set; }
        public bool Complete {get; set;}
    }

Hello DTO è tabella hello toodefine utilizzato nel database SQL di hello.  hello toocreate voce del database, aggiungere un `DbSet<>` proprietà hello DbContext in uso.  Nel modello di progetto predefinito hello per le applicazioni mobili di Azure, hello DbContext viene chiamato `Models\MobileServiceContext.cs`:

    public class MobileServiceContext : DbContext
    {
        private const string connectionStringName = "Name=MS_TableConnectionString";

        public MobileServiceContext() : base(connectionStringName)
        {

        }

        public DbSet<TodoItem> TodoItems { get; set; }

        protected override void OnModelCreating(DbModelBuilder modelBuilder)
        {
            modelBuilder.Conventions.Add(
                new AttributeToColumnAnnotationConvention<TableColumnAttribute, string>(
                    "ServiceColumnTable", (property, attributes) => attributes.Single().ColumnType.ToString()));
        }
    }

Se si dispone di hello che Azure SDK installato, è ora possibile creare un controller di tabella del modello come indicato di seguito:

1. Fare clic sulla cartella controller hello e selezionare **Aggiungi** > **Controller...** .
2. Seleziona hello **Controller tabelle di Azure Mobile app** opzione, quindi fare clic su **Aggiungi**.
3. In hello **Aggiungi Controller** finestra di dialogo:
   * In hello **classe modello** elenco a discesa selezionare il nuovo DTO.
   * In hello **DbContext** classe DbContext servizio Mobile hello selezionare elenco a discesa.
   * nome del Controller Hello viene creato automaticamente.
4. Fare clic su **Aggiungi**.

progetto server di avvio rapido Hello contiene un esempio di una semplice **TodoItemController**.

### <a name="adjust-pagesize"></a>Procedura: ridimensionare hello tabella paging
Per impostazione predefinita, App mobili di Azure restituisce 50 record per ogni richiesta.  Paging assicura che il client hello non utilizza i server dell'interfaccia utente di thread né hello troppo a lungo, garantire un'esperienza utente soddisfacente. toochange hello tabella dimensioni di paging sul lato server di aumento hello "consentito dimensioni della query" e hello sul lato server hello dimensioni pagina sul lato client "consentito dimensioni della query" viene regolato utilizzando hello `EnableQuery` attributo:

    [EnableQuery(PageSize = 500)]

Verificare che sia di hello PageSize hello uguale o maggiore di dimensione hello richiesta dal client hello.  Consultare la documentazione di HOWTO toohello client specifico per informazioni dettagliate sulla modifica delle dimensioni della pagina client hello.

## <a name="how-to-define-a-custom-api-controller"></a>Procedura: Definire un controller API personalizzato
controller API personalizzato Hello fornisce hello più semplice funzionalità tooyour App Mobile back-end esponendo un endpoint. È possibile registrare un controller di API specifici dispositivi mobili con attributo hello [MobileAppController]. Hello `MobileAppController` attributi Registra route hello, configura un serializzatore JSON di App mobili hello e attiva [il controllo della versione di client](app-service-mobile-client-and-server-versioning.md).

1. In Visual Studio, cartella Controllers di hello pulsante destro del mouse, quindi fare clic su **Aggiungi** > **Controller**selezionare **Web API 2 Controller&mdash;vuoto** e Fare clic su **Aggiungi**.
2. Specificare un nome in **Nome controller**, ad esempio `CustomController`, e fare clic su **Aggiungi**.
3. In file di classe controller nuovo hello, aggiungere hello seguente istruzione using:

        using Microsoft.Azure.Mobile.Server.Config;
4. Applicare hello **[MobileAppController]** attributo definizione della classe controller toohello API, come in hello di esempio seguente:

        [MobileAppController]
        public class CustomController : ApiController
        {
              //...
        }
5. Nel file di App_Start/Startup.MobileApp.cs, aggiungere una chiamata toohello **MapApiControllers** il metodo di estensione, come in hello di esempio seguente:

        new MobileAppConfiguration()
            .MapApiControllers()
            .ApplyTo(config);

È inoltre possibile utilizzare hello `UseDefaultConfiguration()` il metodo di estensione anziché `MapApiControllers()`. I controller a cui non è applicato **MobileAppControllerAttribute** continuano a essere accessibili da parte dei client, ma potrebbero non essere usati correttamente dai client con l'SDK client di App per dispositivi mobili.

## <a name="how-to-work-with-authentication"></a>Procedura: Usare l'autenticazione
App per dispositivi mobili Azure utilizza l'autenticazione del servizio App / autorizzazione toosecure mobile back-end.  In questa sezione illustra come hello tooperform seguenti attività correlate all'autenticazione in un progetto server di back-end .NET:

* [Procedura: aggiungere project server tooa di autenticazione](#add-auth)
* [Procedura: Usare l'autenticazione personalizzata per la propria applicazione](#custom-auth)
* [Procedura: Recuperare le informazioni sull'utente autenticato](#user-info)
* [Procedura: Limitare l'accesso ai dati per gli utenti autorizzati](#authorize)

### <a name="add-auth"></a>Procedura: aggiungere project server tooa di autenticazione
È possibile aggiungere un progetto server di autenticazione tooyour estendendo hello **MobileAppConfiguration** oggetto e la configurazione di middleware OWIN. Quando si installa hello [Microsoft.Azure.Mobile.Server.Quickstart] hello pacchetto e chiamare **UseDefaultConfiguration** metodo di estensione, è possibile ignorare toostep 3.

1. In Visual Studio, installare hello [Microsoft.Azure.Mobile.Server.Authentication] pacchetto.
2. Nel file di progetto Startup.cs hello, aggiungere hello successiva riga di codice all'inizio di hello di hello **configurazione** metodo:

        app.UseAppServiceAuthentication(config);

    Questo componente middleware OWIN convalida i token rilasciati da gateway di servizio App hello associata.
3. Aggiungere hello `[Authorize]` attributo tooany controller o al metodo che richiede l'autenticazione.

toolearn sulla tooauthenticate client tooyour back-end App per dispositivi mobili, vedere [Aggiungi autenticazione tooyour app](app-service-mobile-ios-get-started-users.md).

### <a name="custom-auth"></a>Procedura: Usare l'autenticazione personalizzata per la propria applicazione
Se non si desidera toouse uno dei provider di autenticazione/autorizzazione del servizio App hello, è possibile implementare il sistema di account di accesso. Installare hello [Microsoft.Azure.Mobile.Server.Login] tooassist con generazione di token di autenticazione del pacchetto.  Fornire il proprio codice per la convalida delle credenziali utente. È possibile, ad esempio, confrontare le password con salting e hashing in un database. Nel seguente esempio hello hello `isValidAssertion()` metodo (definito altrove) è responsabile di questi controlli.

autenticazione personalizzata Hello viene esposto tramite la creazione di un ApiController e l'esposizione di `register` e `login` azioni. client Hello deve utilizzare una personalizzata dell'interfaccia utente toocollect hello le informazioni utente hello.  informazioni di Hello sono chiamare inviato toohello API con un POST HTTP standard. Una volta server hello convalida asserzione hello, viene emesso un token utilizzando hello `AppServiceLoginHandler.CreateToken()` metodo.  Hello ApiController **non** utilizzare hello `[MobileAppController]` attributo.

Azione `login` di esempio:

        public IHttpActionResult Post([FromBody] JObject assertion)
        {
            if (isValidAssertion(assertion)) // user-defined function, checks against a database
            {
                JwtSecurityToken token = AppServiceLoginHandler.CreateToken(new Claim[] { new Claim(JwtRegisteredClaimNames.Sub, assertion["username"]) },
                    mySigningKey,
                    myAppURL,
                    myAppURL,
                    TimeSpan.FromHours(24) );
                return Ok(new LoginResult()
                {
                    AuthenticationToken = token.RawData,
                    User = new LoginResultUser() { UserId = userName.ToString() }
                });
            }
            else // user assertion was not valid
            {
                return this.Request.CreateUnauthorizedResponse();
            }
        }

In hello sopra riportato, LoginResult e LoginResultUser sono oggetti serializzabili che espone le proprietà necessarie. client Hello prevede l'account di accesso risposte toobe restituiti come oggetti JSON del modulo hello:

        {
            "authenticationToken": "<token>",
            "user": {
                "userId": "<userId>"
            }
        }

Hello `AppServiceLoginHandler.CreateToken()` metodo include un *destinatari* e *dell'autorità di certificazione* parametro. Entrambi questi parametri vengono impostate URL toohello della directory radice dell'applicazione utilizzando lo schema HTTPS hello. Analogamente è necessario impostare *secretKey* chiave di firma del valore di hello toobe dell'applicazione. Non distribuire hello chiave in un client per la firma come può essere utilizzato toomint chiavi e rappresentare gli utenti. È possibile ottenere hello firma chiave mentre ospitato nel servizio App facendo riferimento hello *sito Web\_AUTH\_firma\_chiave* variabile di ambiente. Se necessario in un contesto di debug locale, attenersi alle istruzioni hello hello [il debug locale con l'autenticazione](#local-debug) sezione chiave hello tooretrieve e archiviarle come un'impostazione dell'applicazione.

il token emesso Hello può includere anche altre attestazioni e una data di scadenza.  Come minimo, il token emesso hello deve includere un oggetto (**sub**) di attestazione.

È possibile supportare client standard hello `loginAsync()` metodo route autenticazione hello l'overload.  Se il client hello chiama `client.loginAsync('custom');` toolog in, il route deve essere `/.auth/login/custom`.  È possibile impostare route hello per l'utilizzo di controller di autenticazione personalizzata hello `MapHttpRoute()`:

    config.Routes.MapHttpRoute("custom", ".auth/login/custom", new { controller = "CustomAuth" });

> [!TIP]
> Utilizzando hello `loginAsync()` assicura è collegato il token di autenticazione hello tooevery chiamata successiva toohello servizio.
>
>

### <a name="user-info"></a>Procedura: Recuperare le informazioni sull'utente autenticato
Quando un utente viene autenticato dal servizio App, è possibile accedere hello assegnato ID utente e altre informazioni nel codice di back-end .NET. informazioni utente Hello è utilizzabile per prendere decisioni di autorizzazione nel back-end hello. Hello codice seguente ottiene l'ID utente hello associata a una richiesta:

    // Get hello SID of hello current user.
    var claimsPrincipal = this.User as ClaimsPrincipal;
    string sid = claimsPrincipal.FindFirst(ClaimTypes.NameIdentifier).Value;

Hello SID derivato dall'ID utente specifico del provider hello e static per un determinato utente e i provider di accesso.  Hello SID è null per i token di autenticazione non valido.

Il servizio app consente anche di richiedere le attestazioni specifiche dal provider di accesso. Ogni provider di identità può fornire altre informazioni usando l'SDK del provider di identità.  Ad esempio, è possibile utilizzare hello API Graph di Facebook per informazioni di amici.  Nel Pannello di provider hello in hello portale di Azure, è possibile specificare le attestazioni richieste. Alcune richieste richiedono un'ulteriore configurazione con il provider di identità hello.

esempio di codice seguente Hello hello chiamate **GetAppServiceIdentityAsync** estensione metodo tooget hello le credenziali di accesso, che includono le richieste di token toomake necessari accesso hello contro hello API Graph di Facebook:

    // Get hello credentials for hello logged-in user.
    var credentials =
        await this.User
        .GetAppServiceIdentityAsync<FacebookCredentials>(this.Request);

    if (credentials.Provider == "Facebook")
    {
        // Create a query string with hello Facebook access token.
        var fbRequestUrl = "https://graph.facebook.com/me/feed?access_token="
            + credentials.AccessToken;

        // Create an HttpClient request.
        var client = new System.Net.Http.HttpClient();

        // Request hello current user info from Facebook.
        var resp = await client.GetAsync(fbRequestUrl);
        resp.EnsureSuccessStatusCode();

        // Do something here with hello Facebook user information.
        var fbInfo = await resp.Content.ReadAsStringAsync();
    }

Aggiungere un tramite l'istruzione per `System.Security.Principal` tooprovide hello **GetAppServiceIdentityAsync** metodo di estensione.

### <a name="authorize"></a>Procedura: Limitare l’accesso ai dati per gli utenti autorizzati
Nella sezione precedente hello, abbiamo anche mostrato come tooretrieve hello ID utente di un utente autenticato. È possibile limitare l'accesso toodata e altre risorse in base a questo valore. Ad esempio, l'aggiunta di un tootables colonna ID utente e filtro dei risultati di query hello dall'ID utente hello è toolimit un modo semplice restituiti dati solo tooauthorized gli utenti. Hello codice seguente restituisce le righe di dati solo quando hello SID corrisponde al valore nella colonna di ID utente hello nella tabella TodoItem hello:

    // Get hello SID of hello current user.
    var claimsPrincipal = this.User as ClaimsPrincipal;
    string sid = claimsPrincipal.FindFirst(ClaimTypes.NameIdentifier).Value;

    // Only return data rows that belong toohello current user.
    return Query().Where(t => t.UserId == sid);

Hello `Query()` metodo restituisce un `IQueryable` che può essere modificato dal filtro toohandle LINQ.

## <a name="how-to-add-push-notifications-tooa-server-project"></a>Procedura: aggiungere project server tooa le notifiche di push
Aggiungi progetto server tooyour di notifiche push estendendo hello **MobileAppConfiguration** oggetto e la creazione di un client di hub di notifica.

1. In Visual Studio, fare clic sul progetto server hello e fare clic su **Gestisci pacchetti NuGet**, cercare `Microsoft.Azure.Mobile.Server.Notifications`, quindi fare clic su **installare**.
2. Ripetere questo hello tooinstall passaggio `Microsoft.Azure.NotificationHubs` pacchetto, che include una libreria client di hello hub di notifica.
3. In App_Start/Startup.MobileApp.cs e aggiungere una chiamata toohello **AddPushNotifications()** il metodo di estensione durante l'inizializzazione:

        new MobileAppConfiguration()
            // other features...
            .AddPushNotifications()
            .ApplyTo(config);
4. Aggiungere hello dopo il codice che crea un client di hub di notifica:

        // Get hello settings for hello server project.
        HttpConfiguration config = this.Configuration;
        MobileAppSettingsDictionary settings =
            config.GetMobileAppSettingsProvider().GetMobileAppSettings();

        // Get hello Notification Hubs credentials for hello Mobile App.
        string notificationHubName = settings.NotificationHubName;
        string notificationHubConnection = settings
            .Connections[MobileAppSettingsKeys.NotificationHubConnectionString].ConnectionString;

        // Create a new Notification Hub client.
        NotificationHubClient hub = NotificationHubClient
            .CreateClientFromConnectionString(notificationHubConnection, notificationHubName);

È ora possibile usare dispositivi tooregistered hello hub di notifica client toosend push delle notifiche. Per ulteriori informazioni, vedere [Aggiungi push notifiche tooyour app](app-service-mobile-ios-get-started-push.md). toolearn più sugli hub di notifica, vedere [Panoramica di hub di notifica](../notification-hubs/notification-hubs-push-notification-overview.md).

## <a name="tags"></a>Procedura: Abilitare le notifiche push mirate usando i tag
Gli hub di notifica consente di inviare notifiche destinazione toospecific registrazioni con tag. Diversi tag vengono creati automaticamente:

* ID di installazione Hello identifica un dispositivo specifico.
* Hello Id utente in base alle hello autenticato SID identifica un utente specifico.

Hello installazione ID è possibile accedere da hello **installationId** proprietà hello **MobileServiceClient**.  Hello esempio seguente viene illustrato come utilizzare un tooadd ID installazione un'installazione specifica di tag tooa nell'hub di notifica:

    hub.PatchInstallation("my-installation-id", new[]
    {
        new PartialUpdateOperation
        {
            Operation = UpdateOperationType.Add,
            Path = "/tags",
            Value = "{my-tag}"
        }
    });

Qualsiasi tag forniti dal client hello durante la registrazione della notifica push vengono ignorate dal back-end hello durante la creazione di installazione di hello. installazione toohello i tag tooenable tooadd un client, è necessario creare un'API personalizzata che consente di aggiungere tag usando hello modello precedente.

Vedere [tag di notifica push Client aggiunto] [ 5] nell'esempio di Guida introduttiva completato hello servizio App dell'App Mobile per un esempio.

## <a name="push-user"></a>Procedura: tooan di notifiche push trasmissione l'utente autenticato.
Quando un utente autenticato registrati per le notifiche push, un tag di ID utente viene aggiunto automaticamente toohello registrazione. Con questo tag, è possibile inviare registrati da questa persona dispositivi tooall di notifiche push. Hello codice seguente ottiene hello SID dell'utente che effettua la richiesta e invia una registrazione di modello push notifica tooevery dispositivo per tale persona:

    // Get hello current user SID and create a tag for hello current user.
    var claimsPrincipal = this.User as ClaimsPrincipal;
    string sid = claimsPrincipal.FindFirst(ClaimTypes.NameIdentifier).Value;
    string userTag = "_UserId:" + sid;

    // Build a dictionary for hello template with hello item message text.
    var notification = new Dictionary<string, string> { { "message", item.Text } };

    // Send a template notification toohello user ID.
    await hub.SendTemplateNotificationAsync(notification, userTag);

Durante la registrazione per le notifiche push da un client autenticato, assicurarsi che l'autenticazione sia stata completata prima di tentare la registrazione. Per ulteriori informazioni, vedere [Push toousers] [ 6] nell'esempio di Guida introduttiva completato hello App per dispositivi mobili del servizio App di back-end .NET.

## <a name="how-to-debug-and-troubleshoot-hello-net-server-sdk"></a>Procedura: eseguire il Debug e risoluzione dei problemi hello .NET Server SDK
Il servizio app di Azure offre diverse tecniche di debug e risoluzione dei problemi per le applicazioni ASP.NET:

* [Monitoraggio di un servizio app di Azure](../app-service-web/web-sites-monitor.md)
* [Abilitazione della registrazione diagnostica nel servizio app di Azure](../app-service-web/web-sites-enable-diagnostic-log.md)
* [Risoluzione dei problemi di un Servizio app di Azure in Visual Studio](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md)

### <a name="logging"></a>Registrazione
È possibile scrivere i log di diagnostica servizio tooApp mediante scrittura di traccia ASP.NET standard hello. Prima di scrivere log toohello, è necessario attivare la diagnostica di back-end App per dispositivi mobili.

tooenable di diagnostica e di scrittura toohello registri:

1. Seguire i passaggi di hello in [come diagnostica tooenable](../app-service-web/web-sites-enable-diagnostic-log.md#enablediag).
2. Aggiungere hello seguente istruzione using nel file di codice:

        using System.Web.Http.Tracing;
3. Creare un toowrite writer di traccia da hello .NET back-end toohello i log di diagnostica, come indicato di seguito:

        ITraceWriter traceWriter = this.Configuration.Services.GetTraceWriter();
        traceWriter.Info("Hello, World");
4. Pubblicare il progetto server e accedere hello App Mobile back-end tooexecute hello percorso del codice con la registrazione hello.
5. Scaricare e valutare i log di hello, come descritto in [procedura: scaricare i log](../app-service-web/web-sites-enable-diagnostic-log.md#download).

### <a name="local-debug"></a>Debug locale con autenticazione
È possibile eseguire l'applicazione localmente tootest modifiche prima di pubblicarli toohello cloud. Per la maggior parte dei back-end di App per dispositivi mobili di Azure, premere *F5* in Visual Studio. Esistono però alcune considerazioni aggiuntive quando si usa l'autenticazione.

È necessario disporre di un'app per dispositivi mobili basati su cloud con applicazione servizio di autenticazione/autorizzazione configurato e il client deve disporre di endpoint di cloud hello specificato come host di accesso alternativo hello. Vedere la documentazione di hello per la piattaforma del client per i passaggi specifici di hello necessari.

Verificare che nel back-end mobile sia installato [Microsoft.Azure.Mobile.Server.Authentication] . Quindi, nella classe di avvio dell'applicazione OWIN, aggiungere seguenti hello, dopo `MobileAppConfiguration` è stato applicato tooyour `HttpConfiguration`:

        app.UseAppServiceAuthentication(new AppServiceAuthenticationOptions()
        {
            SigningKey = ConfigurationManager.AppSettings["authSigningKey"],
            ValidAudiences = new[] { ConfigurationManager.AppSettings["authAudience"] },
            ValidIssuers = new[] { ConfigurationManager.AppSettings["authIssuer"] },
            TokenHandler = config.GetAppServiceTokenHandler()
        });

In hello sopra riportato, è necessario configurare hello *authAudience* e *authIssuer* le impostazioni dell'applicazione nel file Web. config file tooeach essere l'URL della directory radice dell'applicazione utilizzando hello HTTPS schema. Analogamente è necessario impostare *authSigningKey* chiave di firma del valore di hello toobe dell'applicazione.
chiave di firma hello tooobtain:

1. Esplorare app tooyour all'interno di hello [portale di Azure]
2. Fare clic su **Strumenti**, **Kudu**, **Vai**.
3. Nel sito di gestione di Kudu hello, fare clic su **ambiente**.
4. Trovare il valore di hello per *sito Web\_AUTH\_firma\_chiave*.

Hello utilizzare firma chiave per hello *authSigningKey* parametro nel file config dell'applicazione locale.  Il back-end per dispositivi mobili è ora token toovalidate forniti durante l'esecuzione in locale, quali client hello Ottiene token hello dall'endpoint basato su cloud hello.

[1]: https://msdn.microsoft.com/library/azure/dn961176.aspx
[2]: https://github.com/Azure/azure-mobile-apps-net-server
[3]: app-service-mobile-ios-get-started.md
[4]: https://azure.microsoft.com/downloads/
[5]: https://github.com/Azure-Samples/app-service-mobile-dotnet-backend-quickstart/blob/master/README.md#client-added-push-notification-tags
[6]: https://github.com/Azure-Samples/app-service-mobile-dotnet-backend-quickstart/blob/master/README.md#push-to-users
[portale di Azure]: https://portal.azure.com
[NuGet.org]: http://www.nuget.org/
[Microsoft.Azure.Mobile.Server]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server/
[Microsoft.Azure.Mobile.Server.Quickstart]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Quickstart/
[Microsoft.Azure.Mobile.Server.Authentication]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Authentication/
[Microsoft.Azure.Mobile.Server.Login]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Login/
[Microsoft.Azure.Mobile.Server.Notifications]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Notifications/
[MapHttpAttributeRoutes]: https://msdn.microsoft.com/library/dn479134(v=vs.118).aspx
