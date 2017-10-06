---
title: aaaHow toocreate un'App Web in Cache Redis | Documenti Microsoft
description: Informazioni su come toocreate un'App Web in Cache Redis
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 454e23d7-a99b-4e6e-8dd7-156451d2da7c
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: hero-article
ms.date: 05/09/2017
ms.author: sdanie
ms.openlocfilehash: d3e6df97b06fdf9032570dc360944be4bd7715de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-web-app-with-redis-cache"></a>Come toocreate un'App Web in Cache Redis
> [!div class="op_single_selector"]
> * [.NET](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [ASP.NET](cache-web-app-howto.md)
> * [Node.JS](cache-nodejs-get-started.md)
> * [Java](cache-java-get-started.md)
> * [Python](cache-python-get-started.md)
> 
> 

Questa esercitazione viene illustrato come toocreate e distribuire un'app web ASP.NET web applicazione tooa nel servizio App di Azure utilizzando Visual Studio 2017. applicazione di esempio Hello Visualizza un elenco delle statistiche team da un database e illustra i diversi modi toouse Cache Redis di Azure toostore e recuperare i dati dalla cache di hello. Dopo aver completato l'esercitazione hello avrai un'app web in esecuzione che legge e scrive tooa database, ottimizzata con Cache Redis di Azure e ospitati in Azure.

Si apprenderà come:

* Toocreate un MVC ASP.NET 5 web come applicazione in Visual Studio.
* Come tooaccess dati da un database tramite Entity Framework.
* La velocità effettiva dei dati tooimprove e ridurre il carico di database per l'archiviazione e recupero di dati tramite una Cache Redis di Azure.
* La modalità di ordinamento set tooretrieve hello top 5 team toouse un Redis.
* Tooprovision hello come risorse di Azure per un'applicazione hello utilizzando un modello di gestione risorse.
* Come toopublish hello tooAzure applicazione con Visual Studio.

## <a name="prerequisites"></a>Prerequisiti
esercitazione di hello toocomplete, è necessario disporre di hello seguenti prerequisiti.

* [Account di Azure](#azure-account)
* [Visual Studio 2017 con hello Azure SDK per .NET](#visual-studio-2017-with-the-azure-sdk-for-net)

### <a name="azure-account"></a>Account Azure
È necessario un'esercitazione di hello toocomplete account Azure. È possibile:

* [Aprire un account Azure gratuitamente](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=redis_cache_hero): È possibile ottenere crediti che possono essere utilizzati tootry out a pagamento di servizi di Azure. Anche dopo hello crediti, è possibile tenere conto di hello e utilizzare le funzionalità e servizi di Azure gratuiti.
* [Attivare i vantaggi della sottoscrizione Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=redis_cache_hero). con l'abbonamento MSDN ogni mese si accumulano crediti che è possibile usare per i servizi di Azure a pagamento.

### <a name="visual-studio-2017-with-hello-azure-sdk-for-net"></a>Visual Studio 2017 con hello Azure SDK per .NET
è stato scritto per Visual Studio 2017 esercitazione Hello con hello [Azure SDK per .NET](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes#azuretools). Azure SDK 2.9.5 Hello è incluso con il programma di installazione di hello Visual Studio.

Se si dispone di Visual Studio 2015, è possibile seguire l'esercitazione hello con hello [Azure SDK per .NET](../dotnet-sdk.md) 2.8.2 o versione successiva. [Download hello SDK più recente di Azure per Visual Studio 2015 qui](http://go.microsoft.com/fwlink/?linkid=518003). Visual Studio viene installato automaticamente con hello SDK se non si dispone già. Alcuni schermi potrebbero essere diverse dalle immagini raffigurate hello illustrate in questa esercitazione.

Se si dispone di Visual Studio 2013, è possibile [download hello SDK più recente di Azure per Visual Studio 2013](http://go.microsoft.com/fwlink/?LinkID=324322). Alcuni schermi potrebbero essere diverse dalle immagini raffigurate hello illustrate in questa esercitazione.

## <a name="create-hello-visual-studio-project"></a>Creare il progetto di Visual Studio hello
1. Aprire Visual Studio e fare clic su **File**, **Nuovo**, **Progetto**.
2. Espandere hello **Visual c#** nodo hello **modelli** elenco, selezionare **Cloud**, fare clic su **applicazione Web ASP.NET**. Assicurarsi che sia selezionata l'opzione **.NET Framework 4.5.2** o versione successiva.  Tipo **ContosoTeamStats** in hello **nome** casella di testo e fare clic su **OK**.
   
    ![Crea progetto][cache-create-project]
3. Selezionare **MVC** come tipo di progetto hello. 

    Verificare che **Nessuna autenticazione** specificato per hello **autenticazione** impostazioni. A seconda della versione di Visual Studio, predefinito hello è possibile impostare toosomething else. toochange, fare clic su **Modifica autenticazione** e selezionare **Nessuna autenticazione**.

    Se si segue insieme a Visual Studio 2015, deselezionare hello **Host nel cloud hello** casella di controllo. Sarà necessario [provisioning hello risorse di Azure](#provision-the-azure-resources) e [pubblicare tooAzure applicazione hello](#publish-the-application-to-azure) nei passaggi successivi dell'esercitazione hello. Per un esempio di provisioning di un'applicazione di servizio App web da Visual Studio lasciando **Host nel cloud hello** selezionata, vedere [iniziare con le app Web in Azure App Service, con ASP.NET e Visual Studio](../app-service-web/app-service-web-get-started-dotnet.md).
   
    ![Seleziona modello progetto][cache-select-template]
4. Fare clic su **OK** progetto hello toocreate.

## <a name="create-hello-aspnet-mvc-application"></a>Creare hello applicazione MVC ASP.NET
In questa sezione dell'esercitazione hello, si creerà un'applicazione hello base che legge e visualizza le statistiche team da un database.

* [Aggiungere il pacchetto NuGet di Entity Framework hello](#add-the-entity-framework-nuget-package)
* [Aggiungere modello hello](#add-the-model)
* [Aggiungi controller hello](#add-the-controller)
* [Configurare le visualizzazioni di hello](#configure-the-views)

### <a name="add-hello-entity-framework-nuget-package"></a>Aggiungere il pacchetto NuGet di Entity Framework hello

1. Fare clic su **Gestione pacchetti NuGet**, **Package Manager Console** da hello **strumenti** menu.
2. Esecuzione hello il seguente comando da hello **Package Manager Console** finestra.
    
    ```
    Install-Package EntityFramework
    ```

Per ulteriori informazioni sul pacchetto, vedere hello [EntityFramework](https://www.nuget.org/packages/EntityFramework/) pagina NuGet.

### <a name="add-hello-model"></a>Aggiungere modello hello
1. In **Esplora soluzioni** fare clic con il pulsante destro del mouse su **Modelli**, quindi scegliere **Aggiungi**, **Classe**. 
   
    ![Aggiungi modello][cache-model-add-class]
2. Immettere `Team` nome della classe hello e fare clic su **Aggiungi**.
   
    ![Aggiunta di una classe modello][cache-model-add-class-dialog]
3. Sostituire hello `using` le istruzioni nella parte superiore di hello di hello `Team.cs` file con il seguente hello `using` istruzioni.

    ```c#
    using System;
    using System.Collections.Generic;
    using System.Data.Entity;
    using System.Data.Entity.SqlServer;
    ```


1. Sostituire la definizione hello di hello `Team` classe con hello seguente frammento di codice che contiene una versione aggiornata `Team` classe definizione, nonché alcune altre classi di supporto di Entity Framework. Per ulteriori informazioni su hello codice primo approccio tooEntity Framework che viene utilizzato in questa esercitazione, vedere [codice prima tooa nuovo database](https://msdn.microsoft.com/data/jj193542).

    ```c#
    public class Team
    {
        public int ID { get; set; }
        public string Name { get; set; }
        public int Wins { get; set; }
        public int Losses { get; set; }
        public int Ties { get; set; }
    
        static public void PlayGames(IEnumerable<Team> teams)
        {
            // Simple random generation of statistics.
            Random r = new Random();
    
            foreach (var t in teams)
            {
                t.Wins = r.Next(33);
                t.Losses = r.Next(33);
                t.Ties = r.Next(0, 5);
            }
        }
    }
    
    public class TeamContext : DbContext
    {
        public TeamContext()
            : base("TeamContext")
        {
        }
    
        public DbSet<Team> Teams { get; set; }
    }
    
    public class TeamInitializer : CreateDatabaseIfNotExists<TeamContext>
    {
        protected override void Seed(TeamContext context)
        {
            var teams = new List<Team>
            {
                new Team{Name="Adventure Works Cycles"},
                new Team{Name="Alpine Ski House"},
                new Team{Name="Blue Yonder Airlines"},
                new Team{Name="Coho Vineyard"},
                new Team{Name="Contoso, Ltd."},
                new Team{Name="Fabrikam, Inc."},
                new Team{Name="Lucerne Publishing"},
                new Team{Name="Northwind Traders"},
                new Team{Name="Consolidated Messenger"},
                new Team{Name="Fourth Coffee"},
                new Team{Name="Graphic Design Institute"},
                new Team{Name="Nod Publishers"}
            };
    
            Team.PlayGames(teams);
    
            teams.ForEach(t => context.Teams.Add(t));
            context.SaveChanges();
        }
    }
    
    public class TeamConfiguration : DbConfiguration
    {
        public TeamConfiguration()
        {
            SetExecutionStrategy("System.Data.SqlClient", () => new SqlAzureExecutionStrategy());
        }
    }
    ```


1. In **Esplora**, fare doppio clic su **Web. config** tooopen è.
   
    ![Web.config][cache-web-config]
2. Aggiungere il seguente hello `connectionStrings` sezione. nome di Hello hello della stringa di connessione deve corrispondere hello nome di classe del contesto del database di Entity Framework che è hello `TeamContext`.

    ```xml
    <connectionStrings>
        <add name="TeamContext" connectionString="Data Source=(LocalDB)\MSSQLLocalDB;AttachDbFilename=|DataDirectory|\Teams.mdf;Integrated Security=True"     providerName="System.Data.SqlClient" />
    </connectionStrings>
    ```

    È possibile aggiungere nuovi hello `connectionStrings` sezione in modo che segua `configSections`, come illustrato nell'esempio seguente hello.

    ```xml
    <configuration>
      <configSections>
        <!-- For more information on Entity Framework configuration, visit http://go.microsoft.com/fwlink/?LinkID=237468 -->
        <section name="entityFramework" type="System.Data.Entity.Internal.ConfigFile.EntityFrameworkSection, EntityFramework, Version=6.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" requirePermission="false" />
      </configSections>
      <connectionStrings>
        <add name="TeamContext" connectionString="Data Source=(LocalDB)\MSSQLLocalDB;AttachDbFilename=|DataDirectory|\Teams.mdf;Integrated Security=True"     providerName="System.Data.SqlClient" />
      </connectionStrings>
      ...
      ```

    > [!NOTE]
    > La stringa di connessione potrebbe essere diversa a seconda della versione di hello di Visual Studio e SQL Server Express edition utilizzato esercitazione hello toocomplete. modello di Hello Web. config deve essere configurato toomatch l'installazione e può contenere `Data Source` come voci `(LocalDB)\v11.0` (da SQL Server Express 2012) o `Data Source=(LocalDB)\MSSQLLocalDB` (da SQL Server Express 2014 e versioni successive). Per altre informazioni sulle stringhe di connessione e le versioni di SQL Express, vedere [SQL Server 2016 Express LocalDB](https://docs.microsoft.com/sql/database-engine/configure-windows/sql-server-2016-express-localdb).

### <a name="add-hello-controller"></a>Aggiungi controller hello
1. Premere **F6** progetto hello toobuild. 
2. In **Esplora**, hello rapida **controller** cartella e scegliere **Aggiungi**, **Controller**.
   
    ![Aggiungi controller][cache-add-controller]
3. Scegliere **Controller MVC 5 con visualizzazioni, che usa Entity Framework** e quindi fare clic su **Aggiungi**. Se si verifica un errore dopo aver fatto clic **Aggiungi**, assicurarsi che siano compilati prima di tutto il progetto hello.
   
    ![Aggiunta di una classe controller][cache-add-controller-class]
4. Selezionare **Team (ContosoTeamStats.Models)** da hello **classe modello** elenco a discesa. Selezionare **TeamContext (ContosoTeamStats.Models)** da hello **classe contesto dati** elenco a discesa. Tipo `TeamsController` in hello **Controller** casella di testo Nome (se non è stato automaticamente popolata). Fare clic su **Aggiungi** toocreate hello classe controller e aggiungere visualizzazioni predefinite hello.
   
    ![Configura controller][cache-configure-controller]
5. In **Esplora**, espandere **Global. asax** fare doppio clic su **Global.asax.cs** tooopen è.
   
    ![Global.asax.cs][cache-global-asax]
6. Aggiungere i seguenti due hello `using` istruzioni all'inizio di hello del file hello in altri hello `using` istruzioni.

    ```c#
    using System.Data.Entity;
    using ContosoTeamStats.Models;
    ```


1. Aggiungere hello successiva riga di codice alla fine hello hello `Application_Start` metodo.

    ```c#
    Database.SetInitializer<TeamContext>(new TeamInitializer());
    ```


1. In **Esplora soluzioni** espandere `App_Start` e fare doppio clic su `RouteConfig.cs`.
   
    ![RouteConfig.cs][cache-RouteConfig-cs]
2. Sostituire `controller = "Home"` nel seguente codice hello hello `RegisterRoutes` metodo con `controller = "Teams"` come illustrato nell'esempio seguente hello.

    ```c#
    routes.MapRoute(
        name: "Default",
        url: "{controller}/{action}/{id}",
        defaults: new { controller = "Teams", action = "Index", id = UrlParameter.Optional }
    );
    ```


### <a name="configure-hello-views"></a>Configurare le visualizzazioni di hello
1. In **Esplora**, espandere hello **viste** cartella e quindi hello **Shared** cartella e fare doppio clic **layout. cshtml**. 
   
    ![file _Layout.cshtml][cache-layout-cshtml]
2. Modificare il contenuto di hello di hello `title` elemento e sostituire `My ASP.NET Application` con `Contoso Team Stats` come illustrato nell'esempio seguente hello.

    ```html
    <title>@ViewBag.Title - Contoso Team Stats</title>
    ```


1. In hello `body` sezione, aggiornare innanzitutto hello `Html.ActionLink` istruzione e sostituire `Application name` con `Contoso Team Stats` e sostituire `Home` con `Teams`.
   
   * Prima: `@Html.ActionLink("Application name", "Index", "Home", new { area = "" }, new { @class = "navbar-brand" })`
   * Dopo: `@Html.ActionLink("Contoso Team Stats", "Index", "Teams", new { area = "" }, new { @class = "navbar-brand" })`
     
     ![Modifiche al codice][cache-layout-cshtml-code]
2. Premere **Ctrl + F5** toobuild ed eseguire un'applicazione hello. Questa versione di un'applicazione hello legge risultati hello direttamente dal database di hello. Hello nota **Crea nuovo**, **modifica**, **dettagli**, e **eliminare** azioni che sono stati automaticamente aggiunti applicazione toohello da hello **Controller MVC 5 con visualizzazioni, mediante Entity Framework** lo scaffolding. Nella sezione successiva di hello di esercitazione hello aggiungerai accesso ai dati di Cache Redis toooptimize hello e forniscono funzionalità aggiuntive toohello applicazione.

![Applicazione iniziale][cache-starter-application]

## <a name="configure-hello-application-toouse-redis-cache"></a>Configurare toouse applicazione hello Cache Redis
In questa sezione dell'esercitazione hello sarà configurare toostore applicazione di esempio hello e recuperare statistiche squadra Contoso da un'istanza di Cache Redis di Azure tramite hello [stackexchange. Redis](https://github.com/StackExchange/StackExchange.Redis) client della cache.

* [Configurare toouse applicazione hello stackexchange. Redis](#configure-the-application-to-use-stackexchangeredis)
* [Aggiornare i risultati di hello TeamsController classe tooreturn dalla cache di hello o database hello](#update-the-teamscontroller-class-to-return-results-from-the-cache-or-the-database)
* [Hello crea, modifica, aggiornare ed eliminare toowork metodi con cache di hello](#update-the-create-edit-and-delete-methods-to-work-with-the-cache)
* [Aggiornare hello team indice vista toowork con cache di hello](#update-the-teams-index-view-to-work-with-the-cache)

### <a name="configure-hello-application-toouse-stackexchangeredis"></a>Configurare toouse applicazione hello stackexchange. Redis
1. Fare clic su un'applicazione client in Visual Studio usando il pacchetto NuGet stackexchange. Redis, hello tooconfigure **Gestione pacchetti NuGet**, **Package Manager Console** da hello **strumenti** menu.
2. Esecuzione hello il seguente comando da hello `Package Manager Console` finestra.
    
    ```
    Install-Package StackExchange.Redis
    ```
   
    Hello NuGet pacchetto Scarica e aggiunge hello necessari riferimenti ad assembly per il tooaccess di applicazione client Cache Redis di Azure con i client della cache di hello stackexchange. Redis. Se si preferisce una versione con nome sicuro di hello toouse `StackExchange.Redis` libreria client, installare hello `StackExchange.Redis.StrongName` pacchetto.
3. In **Esplora**, espandere hello **controller** cartella e fare doppio clic su **TeamsController.cs** tooopen è.
   
    ![Controller Teams][cache-teamscontroller]
4. Aggiungere i seguenti due hello `using` istruzioni troppo**TeamsController.cs**.

    ```c#   
    using System.Configuration;
    using StackExchange.Redis;
    ```

5. Aggiungere i seguenti due proprietà toohello hello `TeamsController` classe.

    ```c#   
    // Redis Connection string info
    private static Lazy<ConnectionMultiplexer> lazyConnection = new Lazy<ConnectionMultiplexer>(() =>
    {
        string cacheConnection = ConfigurationManager.AppSettings["CacheConnection"].ToString();
        return ConnectionMultiplexer.Connect(cacheConnection);
    });
    
    public static ConnectionMultiplexer Connection
    {
        get
        {
            return lazyConnection.Value;
        }
    }
    ```

6. Creare un file nel computer denominato `WebAppPlusCacheAppSecrets.config` e inserirle in un percorso che non è selezionata con il codice sorgente hello dell'applicazione di esempio, se si decide di toocheck in una posizione. In questo hello esempio `AppSettingsSecrets.config` file si trova in `C:\AppSecrets\WebAppPlusCacheAppSecrets.config`.
   
    Modifica hello `WebAppPlusCacheAppSecrets.config` aggiungere hello seguente contenuto e dei file. Se si esegue un'applicazione hello localmente queste informazioni sono l'istanza di Cache Redis di Azure di tooyour tooconnect utilizzato. Più avanti nell'esercitazione di hello consentiranno di eseguire il provisioning di un'istanza di Cache Redis di Azure di aggiornare password e nome della cache di hello. Se non si prevede di applicazione di esempio hello toorun locale è possibile ignorare la creazione di hello di questo file e i passaggi successivi hello che fanno riferimento a file hello, perché quando si distribuisce un'applicazione hello tooAzure recupera le informazioni di connessione della cache di hello da app hello l'impostazione per hello App Web e non da questo file. Poiché hello `WebAppPlusCacheAppSecrets.config` non è stato distribuito tooAzure con l'applicazione, non è necessario a meno che non si intende un'applicazione hello toorun localmente.

    ```xml
    <appSettings>
      <add key="CacheConnection" value="MyCache.redis.cache.windows.net,abortConnect=false,ssl=true,password=..."/>
    </appSettings>
    ```


1. In **Esplora**, fare doppio clic su **Web. config** tooopen è.
   
    ![Web.config][cache-web-config]
2. Aggiungere il seguente hello `file` attributo toohello `appSettings` elemento. Se si utilizza un altro nome di file o un percorso, sostituire i valori per hello quelli illustrati nell'esempio hello.
   
   * Prima: `<appSettings>`
   * Dopo: ` <appSettings file="C:\AppSecrets\WebAppPlusCacheAppSecrets.config">`
     
   il runtime ASP.NET Hello unisce il contenuto di hello del file esterno di hello con markup hello in hello `<appSettings>` elemento. Se non è possibile trovare il file specificato hello, Hello runtime ignora dell'attributo del file hello. I segreti (cache di tooyour stringhe di connessione di hello) non sono inclusi come parte del codice sorgente hello per un'applicazione hello. Quando si distribuisce il tooAzure app web, hello `WebAppPlusCacheAppSecrests.config` file non verrà distribuito (che è quello desiderato). Sono disponibili diversi modi toospecify questi segreti in Azure e in questa esercitazione vengono configurate automaticamente per l'utente quando si [provisioning hello risorse di Azure](#provision-the-azure-resources) in un passaggio successivo dell'esercitazione. Per ulteriori informazioni sull'utilizzo dei segreti in Azure, vedere [procedure consigliate per la distribuzione delle password e altri dati sensibili tooASP.NET e servizio App di Azure](http://www.asp.net/identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure).

### <a name="update-hello-teamscontroller-class-tooreturn-results-from-hello-cache-or-hello-database"></a>Aggiornare i risultati di hello TeamsController classe tooreturn dalla cache di hello o database hello
In questo esempio, le statistiche del team possono essere recuperate dal database hello o dalla cache di hello. Statistiche squadra vengono memorizzate nella cache di hello come serializzata `List<Team>`e anche come un set ordinato utilizzando tipi di dati Redis. Quando si recuperano elementi da un set ordinato, è possibile recuperare alcuni o tutti gli elementi o eseguire query per determinati elementi. In questo esempio query verranno eseguite su set hello ordinato per hello top 5 i team classificati in base al numero di wins.

> [!NOTE]
> Non è necessario toostore hello team statistiche in più formati nella cache di hello in ordine toouse Cache Redis di Azure. Questa esercitazione viene utilizzato più formati toodemonstrate alcuni modi diversi di hello e tipi di dati diversi è possibile utilizzare dati toocache.
> 
> 

1. Aggiungere il seguente hello `using` istruzioni toohello `TeamsController.cs` file nella parte superiore di hello con altri hello `using` istruzioni.

    ```c#   
    using System.Diagnostics;
    using Newtonsoft.Json;
    ```

2. Sostituire hello corrente `public ActionResult Index()` implementazione del metodo con hello seguito all'implementazione.

    ```c#
    // GET: Teams
    public ActionResult Index(string actionType, string resultType)
    {
        List<Team> teams = null;

        switch(actionType)
        {
            case "playGames": // Play a new season of games.
                PlayGames();
                break;

            case "clearCache": // Clear hello results from hello cache.
                ClearCachedTeams();
                break;

            case "rebuildDB": // Rebuild hello database with sample data.
                RebuildDB();
                break;
        }

        // Measure hello time it takes tooretrieve hello results.
        Stopwatch sw = Stopwatch.StartNew();

        switch(resultType)
        {
            case "teamsSortedSet": // Retrieve teams from sorted set.
                teams = GetFromSortedSet();
                break;

            case "teamsSortedSetTop5": // Retrieve hello top 5 teams from hello sorted set.
                teams = GetFromSortedSetTop5();
                break;

            case "teamsList": // Retrieve teams from hello cached List<Team>.
                teams = GetFromList();
                break;

            case "fromDB": // Retrieve results from hello database.
            default:
                teams = GetFromDB();
                break;
        }

        sw.Stop();
        double ms = sw.ElapsedTicks / (Stopwatch.Frequency / (1000.0));

        // Add hello elapsed time of hello operation toohello ViewBag.msg.
        ViewBag.msg += " MS: " + ms.ToString();

        return View(teams);
    }
    ```


1. Aggiungere i seguenti tre metodi toohello hello `TeamsController` hello tooimplement classe `playGames`, `clearCache`, e `rebuildDB` tipi di azione da hello passare istruzione aggiunta nel frammento di codice precedente hello.
   
    Hello `PlayGames` metodo Aggiorna statistiche squadra hello simulando una stagione dei giochi, Salva hello toohello database dei risultati e Cancella hello aggiornate dei dati dalla cache di hello.

    ```c#
    void PlayGames()
    {
        ViewBag.msg += "Updating team statistics. ";
        // Play a "season" of games.
        var teams = from t in db.Teams
                    select t;

        Team.PlayGames(teams);

        db.SaveChanges();

        // Clear any cached results
        ClearCachedTeams();
    }
    ```

    Hello `RebuildDB` metodo reinizializza hello database con il set predefinito di hello del team, genera le statistiche per essi, e Cancella hello aggiornate dei dati dalla cache di hello.

    ```c#
    void RebuildDB()
    {
        ViewBag.msg += "Rebuilding DB. ";
        // Delete and re-initialize hello database with sample data.
        db.Database.Delete();
        db.Database.Initialize(true);

        // Clear any cached results
        ClearCachedTeams();
    }
    ```

    Hello `ClearCachedTeams` metodo rimuove tutte le statistiche team memorizzati nella cache dalla cache di hello.

    ```c#
    void ClearCachedTeams()
    {
        IDatabase cache = Connection.GetDatabase();
        cache.KeyDelete("teamsList");
        cache.KeyDelete("teamsSortedSet");
        ViewBag.msg += "Team data removed from cache. ";
    } 
    ```


1. Aggiungere i seguenti quattro metodi toohello hello `TeamsController` hello tooimplement classe varie modalità di recupero di statistiche squadra hello dalla cache di hello e database hello. Ognuno di questi metodi restituisce un `List<Team>` che viene quindi visualizzato dalla visualizzazione hello.
   
    Hello `GetFromDB` metodo legge statistiche squadra hello dal database hello.
   
    ```c#
    List<Team> GetFromDB()
    {
        ViewBag.msg += "Results read from DB. ";
        var results = from t in db.Teams
            orderby t.Wins descending
            select t; 

        return results.ToList<Team>();
    }
    ```

    Hello `GetFromList` metodo legge statistiche squadra hello dalla cache come serializzata `List<Team>`. Se è presente un mancato riscontro nella cache, statistiche squadra hello sono lette dal database di hello e quindi memorizzate nella cache di hello per la volta successiva. In questo esempio si utilizza JSON.NET serializzazione tooserialize hello .NET oggetti tooand dalla cache di hello. Per ulteriori informazioni, vedere [come toowork con .NET gli oggetti nella Cache Redis di Azure](cache-dotnet-how-to-use-azure-redis-cache.md#work-with-net-objects-in-the-cache).

    ```c#
    List<Team> GetFromList()
    {
        List<Team> teams = null;

        IDatabase cache = Connection.GetDatabase();
        string serializedTeams = cache.StringGet("teamsList");
        if (!String.IsNullOrEmpty(serializedTeams))
        {
            teams = JsonConvert.DeserializeObject<List<Team>>(serializedTeams);

            ViewBag.msg += "List read from cache. ";
        }
        else
        {
            ViewBag.msg += "Teams list cache miss. ";
            // Get from database and store in cache
            teams = GetFromDB();

            ViewBag.msg += "Storing results toocache. ";
            cache.StringSet("teamsList", JsonConvert.SerializeObject(teams));
        }
        return teams;
    }
    ```

    Hello `GetFromSortedSet` metodo legge statistiche squadra hello da un set ordinato memorizzati nella cache. Se è presente un mancato riscontro nella cache, statistiche squadra hello sono lette dal database di hello e memorizzate nella cache di hello come un set ordinato.

    ```c#
    List<Team> GetFromSortedSet()
    {
        List<Team> teams = null;
        IDatabase cache = Connection.GetDatabase();
        // If hello key teamsSortedSet is not present, this method returns a 0 length collection.
        var teamsSortedSet = cache.SortedSetRangeByRankWithScores("teamsSortedSet", order: Order.Descending);
        if (teamsSortedSet.Count() > 0)
        {
            ViewBag.msg += "Reading sorted set from cache. ";
            teams = new List<Team>();
            foreach (var t in teamsSortedSet)
            {
                Team tt = JsonConvert.DeserializeObject<Team>(t.Element);
                teams.Add(tt);
            }
        }
        else
        {
            ViewBag.msg += "Teams sorted set cache miss. ";

            // Read from DB
            teams = GetFromDB();

            ViewBag.msg += "Storing results toocache. ";
            foreach (var t in teams)
            {
                Console.WriteLine("Adding toosorted set: {0} - {1}", t.Name, t.Wins);
                cache.SortedSetAdd("teamsSortedSet", JsonConvert.SerializeObject(t), t.Wins);
            }
        }
        return teams;
    }
    ```

    Hello `GetFromSortedSetTop5` metodo legge insieme 5 team dal memorizzati nella cache di hello ordinati superiore hello. Avvia il controllo della cache di hello esistenza hello di hello `teamsSortedSet` chiave. Se questa chiave non è presente, hello `GetFromSortedSet` metodo viene chiamato statistiche squadra di tooread hello e memorizzarli nella cache di hello. Successivamente, hello set ordinato memorizzati nella cache viene eseguita una query per hello top 5 i team che vengono restituiti.

    ```c#
    List<Team> GetFromSortedSetTop5()
    {
        List<Team> teams = null;
        IDatabase cache = Connection.GetDatabase();

        // If hello key teamsSortedSet is not present, this method returns a 0 length collection.
        var teamsSortedSet = cache.SortedSetRangeByRankWithScores("teamsSortedSet", stop: 4, order: Order.Descending);
        if(teamsSortedSet.Count() == 0)
        {
            // Load hello entire sorted set into hello cache.
            GetFromSortedSet();

            // Retrieve hello top 5 teams.
            teamsSortedSet = cache.SortedSetRangeByRankWithScores("teamsSortedSet", stop: 4, order: Order.Descending);
        }

        ViewBag.msg += "Retrieving top 5 teams from cache. ";
        // Get hello top 5 teams from hello sorted set
        teams = new List<Team>();
        foreach (var team in teamsSortedSet)
        {
            teams.Add(JsonConvert.DeserializeObject<Team>(team.Element));
        }
        return teams;
    }
    ```

### <a name="update-hello-create-edit-and-delete-methods-toowork-with-hello-cache"></a>Hello crea, modifica, aggiornare ed eliminare toowork metodi con cache di hello
codice di scaffolding Hello generato come parte di questo esempio include metodi tooadd, modificare ed eliminare i team. Ogni volta che un team viene aggiunto, modificato o rimosso, i dati di hello nella cache di hello diventano obsoleti. In questa sezione che si desidera modificare queste hello tooclear tre metodi memorizzati nella cache i team in modo che la cache di hello non verrà sincronizzata con il database di hello.

1. Sfoglia toohello `Create(Team team)` metodo hello `TeamsController` classe. Aggiungere una chiamata toohello `ClearCachedTeams` (metodo), come illustrato nell'esempio seguente hello.

    ```c#
    // POST: Teams/Create
    // tooprotect from overposting attacks, please enable hello specific properties you want toobind to, for 
    // more details see http://go.microsoft.com/fwlink/?LinkId=317598.
    [HttpPost]
    [ValidateAntiForgeryToken]
    public ActionResult Create([Bind(Include = "ID,Name,Wins,Losses,Ties")] Team team)
    {
        if (ModelState.IsValid)
        {
            db.Teams.Add(team);
            db.SaveChanges();
            // When a team is added, hello cache is out of date.
            // Clear hello cached teams.
            ClearCachedTeams();
            return RedirectToAction("Index");
        }

        return View(team);
    }
    ```


1. Sfoglia toohello `Edit(Team team)` metodo hello `TeamsController` classe. Aggiungere una chiamata toohello `ClearCachedTeams` (metodo), come illustrato nell'esempio seguente hello.

    ```c#
    // POST: Teams/Edit/5
    // tooprotect from overposting attacks, please enable hello specific properties you want toobind to, for 
    // more details see http://go.microsoft.com/fwlink/?LinkId=317598.
    [HttpPost]
    [ValidateAntiForgeryToken]
    public ActionResult Edit([Bind(Include = "ID,Name,Wins,Losses,Ties")] Team team)
    {
        if (ModelState.IsValid)
        {
            db.Entry(team).State = EntityState.Modified;
            db.SaveChanges();
            // When a team is edited, hello cache is out of date.
            // Clear hello cached teams.
            ClearCachedTeams();
            return RedirectToAction("Index");
        }
        return View(team);
    }
    ```


1. Sfoglia toohello `DeleteConfirmed(int id)` metodo hello `TeamsController` classe. Aggiungere una chiamata toohello `ClearCachedTeams` (metodo), come illustrato nell'esempio seguente hello.

    ```c#
    // POST: Teams/Delete/5
    [HttpPost, ActionName("Delete")]
    [ValidateAntiForgeryToken]
    public ActionResult DeleteConfirmed(int id)
    {
        Team team = db.Teams.Find(id);
        db.Teams.Remove(team);
        db.SaveChanges();
        // When a team is deleted, hello cache is out of date.
        // Clear hello cached teams.
        ClearCachedTeams();
        return RedirectToAction("Index");
    }
    ```


### <a name="update-hello-teams-index-view-toowork-with-hello-cache"></a>Aggiornare hello team indice vista toowork con cache di hello
1. In **Esplora**, espandere hello **viste** cartella, quindi hello **Team** cartella e fare doppio clic **cshtml**.
   
    ![Index.cshtml][cache-views-teams-index-cshtml]
2. Parte superiore di hello del file hello, cercare hello dopo l'elemento del paragrafo.
   
    ![Tabella delle azioni][cache-teams-index-table]
   
    Si tratta di hello collegamento toocreate un nuovo team. Sostituire l'elemento del paragrafo hello con hello nella tabella seguente. La tabella include collegamenti ad azioni per la creazione di un nuovo team, la riproduzione di una nuovo stagione dei giochi, la cancellazione della cache di hello, recupero team hello dalla cache di hello in diversi formati, il recupero dei team hello dal database hello e ricompilare hello database con dati di esempio aggiornato.

    ```html
    <table class="table">
        <tr>
            <td>
                @Html.ActionLink("Create New", "Create")
            </td>
            <td>
                @Html.ActionLink("Play Season", "Index", new { actionType = "playGames" })
            </td>
            <td>
                @Html.ActionLink("Clear Cache", "Index", new { actionType = "clearCache" })
            </td>
            <td>
                @Html.ActionLink("List from Cache", "Index", new { resultType = "teamsList" })
            </td>
            <td>
                @Html.ActionLink("Sorted Set from Cache", "Index", new { resultType = "teamsSortedSet" })
            </td>
            <td>
                @Html.ActionLink("Top 5 Teams from Cache", "Index", new { resultType = "teamsSortedSetTop5" })
            </td>
            <td>
                @Html.ActionLink("Load from DB", "Index", new { resultType = "fromDB" })
            </td>
            <td>
                @Html.ActionLink("Rebuild DB", "Index", new { actionType = "rebuildDB" })
            </td>
        </tr>    
    </table>
    ```


1. Scorri toohello alla fine di hello **cshtml** file e aggiungere il seguente hello `tr` elemento in modo che venga hello ultima riga hello ultima tabella nel file hello.
   
    ```html
    <tr><td colspan="5">@ViewBag.Msg</td></tr>
    ```
   
    Questa riga viene visualizzato il valore di hello di `ViewBag.Msg` che contiene un report di stato sull'operazione corrente hello. Hello `ViewBag.Msg` viene impostato quando si fa clic su uno dei collegamenti di azione hello dal passaggio precedente hello.   
   
    ![Messaggio di stato][cache-status-message]
2. Premere **F6** progetto hello toobuild.

## <a name="provision-hello-azure-resources"></a>Eseguire il provisioning hello risorse di Azure
toohost dell'applicazione in Azure, è necessario innanzitutto eseguire il provisioning di servizi di Azure che richiede l'applicazione hello. applicazione di esempio Hello in questa esercitazione Usa hello seguenti servizi di Azure.

* Cache Redis di Azure
* App Web del servizio app
* Database SQL

toodeploy gruppo di risorse nuove o esistenti tooa questi servizi di propria scelta, fare clic su hello seguente **distribuire tooAzure** pulsante.

[! [Deploy tooAzure] [deploybutton]](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-redis-cache-sql-database%2Fazuredeploy.json)

Questo **distribuire tooAzure** pulsante utilizza hello [creare un'App Web più Cache Redis di più Database SQL](https://github.com/Azure/azure-quickstart-templates/tree/master/201-web-app-redis-cache-sql-database) [Guida introduttiva di Azure](https://github.com/Azure/azure-quickstart-templates) modello tooprovision tali servizi e hello set stringa di connessione per l'impostazione di applicazione di Database SQL e hello hello per hello stringa di connessione della Cache Redis di Azure.

> [!NOTE]
> Se non si ha un account Azure, è possibile [creare un account Azure gratuito](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=redis_cache_hero) in pochi minuti.
> 
> 

Facendo clic su hello **distribuire tooAzure** pulsante accetta toohello portale di Azure e avvia hello processo di creazione di risorse hello descritte da modello hello.

![Distribuire tooAzure][cache-deploy-to-azure-step-1]

1. In hello **nozioni di base** sezione hello toouse di sottoscrizione di Azure, selezionare e selezionare un gruppo di risorse esistente o crearne uno nuovo e specificare il percorso del gruppo risorse hello.
2. In hello **impostazioni** sezione, specificare un **account di accesso amministratore** (non utilizzare **admin**), **Password dell'account di accesso amministratore**e  **Nome del database**. Hello altri parametri configurati per un servizio App gratuito piano e le opzioni di basso costo per Database SQL di hello e Cache Redis di Azure, che non provengono con un livello gratuito di hosting.

    ![Distribuire tooAzure][cache-deploy-to-azure-step-2]

3. Dopo aver configurato le impostazioni di hello desiderato, scorrere toohello fine pagina hello, hello leggere le condizioni e controllare hello **accetto le condizioni indicate in precedenza toohello** casella di controllo.
4. Fare clic su toobegin durante il provisioning delle risorse hello, **acquisto**.

stato di avanzamento hello tooview della distribuzione, fare clic sull'icona di notifica hello e fare clic su **distribuzione avviata**.

![La distribuzione è stata avviata][cache-deployment-started]

È possibile visualizzare lo stato di hello della distribuzione su hello **Microsoft.Template** blade.

![Distribuire tooAzure][cache-deploy-to-azure-step-3]

Al termine il provisioning, è possibile pubblicare tooAzure l'applicazione da Visual Studio.

> [!NOTE]
> Sono visualizzati eventuali errori che possono verificarsi durante il processo di provisioning hello in hello **Microsoft.Template** blade. Gli errori comuni sono relativi a un numero eccessivo di server SQL o di piani di hosting del Servizio app gratuito per ogni sottoscrizione. Risolvere gli eventuali errori e riavviare il processo di hello facendo **ridistribuire** su hello **Microsoft.Template** pannello o hello **distribuire tooAzure** pulsante in questa esercitazione.
> 
> 

## <a name="publish-hello-application-tooazure"></a>Pubblicare tooAzure applicazione hello
In questo passaggio dell'esercitazione hello, si sarà pubblicare tooAzure applicazione hello ed eseguirlo nel cloud hello.

1. Pulsante destro del mouse hello **ContosoTeamStats** sul progetto in Visual Studio e scegliere **pubblica**.
   
    ![Pubblica][cache-publish-app]
2. Fare clic su **Servizio app di Microsoft Azure**, scegliere **Seleziona esistente** e fare clic su **Pubblica**.
   
    ![Pubblica][cache-publish-to-app-service]
3. Selezionare la sottoscrizione di hello utilizzata quando la creazione di risorse di Azure, hello espandere il gruppo di risorse hello contenente risorse hello e seleziona hello desiderato App Web. Se è stato utilizzato hello **distribuire tooAzure** pulsante il nome dell'App Web inizia con **sito Web** seguita da alcuni caratteri aggiuntivi.
   
    ![Selezione dell'app Web][cache-select-web-app]
4. Fare clic su **OK** hello toobegin processo di pubblicazione. Dopo alcuni istanti completa hello processo di pubblicazione e un browser viene avviato con hello in esecuzione l'applicazione di esempio. Se è visualizzato un errore DNS durante la convalida o la pubblicazione e hello processo per il provisioning hello risorse Azure per un'applicazione hello ha appena completata di recente, attendere qualche istante e riprovare.
   
    ![Cache aggiunta][cache-added-to-application]

Hello nella tabella seguente descrive ciascun collegamento all'azione dall'applicazione di esempio hello.

| Azione | Descrizione |
| --- | --- |
| Creazione di un nuovo sito |Crea un nuovo team. |
| Play Season |Riprodurre una stagione dei giochi, statistiche team hello di aggiornamento, e cancella qualsiasi obsoleta dati dalla cache di hello del team. |
| Clear Cache |Statistiche del team crittografato hello dalla cache di hello. |
| List from Cache |Recuperare statistiche team hello dalla cache di hello. Se è presente un mancato riscontro nella cache, caricare statistiche hello dal database di hello e salvare toohello cache per la volta successiva. |
| Sorted Set from Cache |Recuperare statistiche team hello dalla cache di hello con un set ordinato. Se è presente un mancato riscontro nella cache, caricare statistiche hello dal database hello e salvare la cache toohello tramite un set ordinato. |
| Top 5 Teams from Cache |Recuperare i team di 5 superiore hello dalla cache di hello con un set ordinato. Se è presente un mancato riscontro nella cache, caricare statistiche hello dal database hello e salvare la cache toohello tramite un set ordinato. |
| Load from DB |Recuperare statistiche team hello dal database di hello. |
| Rebuild DB |Ricompilare database hello e caricarla con i dati di esempio team. |
| Edit / Details / Delete |Modifica un team, visualizza dettagli per un team, elimina un team. |

Fare clic su alcune delle azioni hello e sperimentare il recupero dei dati di hello provenienti da origini diverse hello. Non hello le differenze nel tempo hello che necessario hello toocomplete diverse modalità di recupero dei dati hello dal database di hello e cache di hello.

## <a name="delete-hello-resources-when-you-are-finished-with-hello-application"></a>Eliminare le risorse di hello dopo aver terminato con un'applicazione hello
Quando si è terminato con un'applicazione hello esempio dell'esercitazione, è possibile eliminare hello Azure le risorse utilizzate in ordine tooconserve costi e le risorse. Se si utilizza hello **distribuire tooAzure** pulsante hello [hello di effettuare il provisioning delle risorse di Azure](#provision-the-azure-resources) sezione e tutte le risorse sono contenute in hello stesso gruppo di risorse, è possibile eliminarle insieme in uno operazione eliminando il gruppo di risorse hello.

1. Accedi toohello [portale di Azure](https://portal.azure.com) e fare clic su **gruppi di risorse**.
2. Nome del gruppo di risorse in hello hello di tipo **filtrare gli elementi...**  casella di testo.
3. Fare clic su **...**  toohello a destra del gruppo di risorse.
4. Fare clic su **Elimina**.
   
    ![Elimina][cache-delete-resource-group]
5. Nome del gruppo di risorse e fare clic su di tipo hello **eliminare**.
   
    ![Conferma dell'eliminazione][cache-delete-confirm]

Dopo la risorsa di hello pochi istanti gruppo e tutte le risorse indipendenti vengono eliminate.

> [!IMPORTANT]
> Si noti che l'eliminazione di un gruppo di risorse è irreversibile e il gruppo di risorse di hello e tutte le risorse di hello in essa contenuti vengono eliminate definitivamente. Assicurarsi che non si accidentalmente Elimina il gruppo di risorse non corretto di hello o risorse. Se è stato creato risorse hello per l'hosting in questo esempio all'interno di un gruppo di risorse esistente, è possibile eliminare singolarmente ogni risorsa da loro rispettivi pannelli.
> 
> 

## <a name="run-hello-sample-application-on-your-local-machine"></a>Eseguire l'applicazione di esempio hello sul computer locale
un'applicazione hello toorun localmente nel computer, è necessario una Cache Redis di Azure dell'istanza in cui toocache i dati. 

* Se è stata pubblicata l'applicazione tooAzure come descritto nella sezione precedente di hello, è possibile utilizzare l'istanza di Cache Redis di Azure hello che è stato eseguito il provisioning durante questo passaggio.
* Se si dispone di un'altra istanza di Cache Redis di Azure esistente, è possibile utilizzare tale toorun in questo esempio in locale.
* Se è necessario toocreate un'istanza di Cache Redis di Azure, è possibile seguire i passaggi di hello in [creare una cache](cache-dotnet-how-to-use-azure-redis-cache.md#create-a-cache).

Dopo aver selezionato o creato toouse cache di hello, esplorare toohello cache nel portale di Azure hello e recuperare hello [nome host](cache-configure.md#properties) e [le chiavi di accesso](cache-configure.md#access-keys) per la cache. Per istruzioni, vedere [Configurare le impostazioni della cache Redis](cache-configure.md#configure-redis-cache-settings).

1. Aprire hello `WebAppPlusCacheAppSecrets.config` file creati durante hello [configurare toouse applicazione hello Cache Redis](#configure-the-application-to-use-redis-cache) passaggio di questa esercitazione utilizzando editor hello di propria scelta.
2. Modifica hello `value` attributo e sostituire `MyCache.redis.cache.windows.net` con hello [nome host](cache-configure.md#properties) della cache e specificare entrambi hello [chiave primaria o secondaria](cache-configure.md#access-keys) della cache come password hello.

    ```xml
    <appSettings>
      <add key="CacheConnection" value="MyCache.redis.cache.windows.net,abortConnect=false,ssl=true,password=..."/>
    </appSettings>
    ```


1. Premere **Ctrl + F5** toorun un'applicazione hello.

> [!NOTE]
> Si noti che cache di hello perché un'applicazione hello, tra cui database hello, viene eseguito localmente e hello Cache Redis è ospitata in Azure, ammesso toounder-hello dei database. Per prestazioni ottimali, hello applicazione client e l'istanza di Cache Redis di Azure deve essere in hello nello stesso percorso. 
> 
> 

## <a name="next-steps"></a>Passaggi successivi
* Altre informazioni, vedere [Introduzione a ASP.NET MVC 5](http://www.asp.net/mvc/overview/getting-started/introduction/getting-started) su hello [ASP.NET](http://asp.net/) sito.
* Per ulteriori esempi di creazione di un'App Web ASP.NET nel servizio App, vedere [creare e distribuire un'app web ASP.NET in Azure App Service](https://github.com/Microsoft/HealthClinic.biz/wiki/Create-and-deploy-an-ASP.NET-web-app-in-Azure-App-Service) da hello [HealthClinic.biz](https://github.com/Microsoft/HealthClinic.biz) 2015 Connetti [demo](https://blogs.msdn.microsoft.com/visualstudio/2015/12/08/connectdemos-2015-healthclinic-biz/).
  * Per altre guide rapide dalla demo HealthClinic.biz hello, vedere [strumenti Guida introduttiva per sviluppatori di Azure](https://github.com/Microsoft/HealthClinic.biz/wiki/Azure-Developer-Tools-Quickstarts).
* Altre informazioni su hello [codice prima tooa nuovo database](https://msdn.microsoft.com/data/jj193542) approccio tooEntity Framework che viene utilizzato in questa esercitazione.
* Altre informazioni sulle [app Web nel servizio app di Azure](../app-service-web/app-service-web-overview.md).
* Informazioni su come troppo[monitoraggio](cache-how-to-monitor.md) la cache di hello portale di Azure.
* Esplorare le funzionalità Premium della cache Redis di Azure
  
  * [Come la persistenza tooconfigure per una Cache Redis di Azure Premium](cache-how-to-premium-persistence.md)
  * [Come tooconfigure clustering per una Cache Redis di Azure Premium](cache-how-to-premium-clustering.md)
  * [La modalità di supporto tooconfigure rete virtuale per una Cache Redis di Azure Premium](cache-how-to-premium-vnet.md)
  * Vedere hello [Azure Redis Cache FAQ](cache-faq.md#what-redis-cache-offering-and-size-should-i-use) per ulteriori informazioni sulle dimensioni, velocità effettiva e la larghezza di banda con cache premium.

<!-- IMAGES -->
[cache-starter-application]: ./media/cache-web-app-howto/cache-starter-application.png
[cache-added-to-application]: ./media/cache-web-app-howto/cache-added-to-application.png
[cache-create-project]: ./media/cache-web-app-howto/cache-create-project.png
[cache-select-template]: ./media/cache-web-app-howto/cache-select-template.png
[cache-model-add-class]: ./media/cache-web-app-howto/cache-model-add-class.png
[cache-model-add-class-dialog]: ./media/cache-web-app-howto/cache-model-add-class-dialog.png
[cache-add-controller]: ./media/cache-web-app-howto/cache-add-controller.png
[cache-add-controller-class]: ./media/cache-web-app-howto/cache-add-controller-class.png
[cache-configure-controller]: ./media/cache-web-app-howto/cache-configure-controller.png
[cache-global-asax]: ./media/cache-web-app-howto/cache-global-asax.png
[cache-RouteConfig-cs]: ./media/cache-web-app-howto/cache-RouteConfig-cs.png
[cache-layout-cshtml]: ./media/cache-web-app-howto/cache-layout-cshtml.png
[cache-layout-cshtml-code]: ./media/cache-web-app-howto/cache-layout-cshtml-code.png
[redis-cache-manage-nuget-menu]: ./media/cache-web-app-howto/redis-cache-manage-nuget-menu.png
[redis-cache-stack-exchange-nuget]: ./media/cache-web-app-howto/redis-cache-stack-exchange-nuget.png
[cache-teamscontroller]: ./media/cache-web-app-howto/cache-teamscontroller.png
[cache-web-config]: ./media/cache-web-app-howto/cache-web-config.png
[cache-views-teams-index-cshtml]: ./media/cache-web-app-howto/cache-views-teams-index-cshtml.png
[cache-teams-index-table]: ./media/cache-web-app-howto/cache-teams-index-table.png
[cache-status-message]: ./media/cache-web-app-howto/cache-status-message.png
[deploybutton]: ./media/cache-web-app-howto/deploybutton.png
[cache-deploy-to-azure-step-1]: ./media/cache-web-app-howto/cache-deploy-to-azure-step-1.png
[cache-deploy-to-azure-step-2]: ./media/cache-web-app-howto/cache-deploy-to-azure-step-2.png
[cache-deploy-to-azure-step-3]: ./media/cache-web-app-howto/cache-deploy-to-azure-step-3.png
[cache-deployment-started]: ./media/cache-web-app-howto/cache-deployment-started.png
[cache-publish-app]: ./media/cache-web-app-howto/cache-publish-app.png
[cache-publish-to-app-service]: ./media/cache-web-app-howto/cache-publish-to-app-service.png
[cache-select-web-app]: ./media/cache-web-app-howto/cache-select-web-app.png
[cache-publish]: ./media/cache-web-app-howto/cache-publish.png
[cache-delete-resource-group]: ./media/cache-web-app-howto/cache-delete-resource-group.png
[cache-delete-confirm]: ./media/cache-web-app-howto/cache-delete-confirm.png

