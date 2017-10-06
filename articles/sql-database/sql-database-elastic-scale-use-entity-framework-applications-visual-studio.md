---
title: libreria client di database elastico aaaUsing con Entity Framework | Documenti Microsoft
description: Usare la libreria client del database elastico e Entity Framework per la codifica di database
services: sql-database
documentationcenter: 
manager: jhubbard
author: torsteng
editor: 
ms.assetid: b9c3065b-cb92-41be-aa7f-deba23e7e159
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: torsteng
ms.openlocfilehash: 917f6d28d9855c0b42afe2c008613a9bbb3ec6b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="elastic-database-client-library-with-entity-framework"></a>Libreria client dei database elastici con Entity Framework
Questo documento illustra le modifiche di hello in un'applicazione Entity Framework che sono necessari toointegrate con hello [strumenti di Database elastico](sql-database-elastic-scale-introduction.md). Hello è attiva la composizione [gestione mappa partizioni](sql-database-elastic-scale-shard-map-management.md) e [routing dipendente dai dati](sql-database-elastic-scale-data-dependent-routing.md) con Entity Framework hello **Code First** approccio. Hello [codice innanzitutto - Nuovo Database](http://msdn.microsoft.com/data/jj193542.aspx) esercitazione per Entity Framework viene utilizzato come esempio in esecuzione in questo documento. codice di esempio Hello che accompagna questo documento fa parte degli strumenti di database elastico set di campioni in hello esempi di codice di Visual Studio.

## <a name="downloading-and-running-hello-sample-code"></a>Scaricare ed eseguire l'esempio di codice hello
codice di hello toodownload per questo articolo:

* È richiesto Visual Studio 2012 o versione successiva. 
* Scaricare hello [elastico strumenti DB per SQL Azure - esempio di integrazione di Entity Framework](https://code.msdn.microsoft.com/windowsapps/Elastic-Scale-with-Azure-bae904ba) da MSDN. Decomprimere percorso tooa di esempio hello di propria scelta.
* Avviare Visual Studio. 
* In Visual Studio selezionare File -> Apri progetto/soluzione. 
* In hello **Apri progetto** finestra di dialogo, passare toohello esempio scaricato e selezionare **EntityFrameworkCodeFirst.sln** tooopen: esempio hello. 

esempio hello toorun, è necessario toocreate tre database vuoto nel Database SQL di Azure:

* Database di gestione delle mappe partizioni
* Database partizione 1
* Database partizione 2

Dopo aver creato questi database, compilare segnaposto hello in **Program.cs** con il nome del server di database SQL di Azure, i nomi dei database hello e i database di toohello tooconnect le credenziali. Compilare la soluzione hello in Visual Studio. Visual Studio verranno scaricati i pacchetti NuGet hello necessario per la libreria client di database elastico hello, Entity Framework e la gestione come parte del processo di compilazione hello di errori temporanei. Verificare che per la soluzione sia abilitato il ripristino dei pacchetti NuGet. È possibile abilitare questa impostazione facendo clic sul file della soluzione in Esplora soluzioni di Visual Studio hello hello. 

## <a name="entity-framework-workflows"></a>Flussi di lavoro di Entity Framework
Gli sviluppatori di Entity Framework si basano su uno dei seguenti quattro applicazioni toobuild flussi di lavoro e la persistenza tooensure per gli oggetti dell'applicazione hello: 

* **Code First (Database nuovo)**: hello developer EF Crea modello hello nel codice dell'applicazione hello ed EF genera quindi il database di hello da esso. 
* **Code First (Database esistente)**: hello developer consente a Entity Framework di generare codice dell'applicazione hello per modello hello da un database esistente.
* **Prima del modello**: developer hello Crea modello hello nella finestra di progettazione EF hello e quindi EF database hello dal modello hello.
* **Database First**: developer hello utilizza EF tooling modello hello tooinfer da un database esistente. 

Tutti questi approcci si basano su hello DbContext classe tootransparently gestire connessioni al database e lo schema del database per un'applicazione. Come si parlerà in dettaglio più avanti nel documento hello, costruttori diversi nella classe di base di hello DbContext consentano per diversi livelli di controllo sulla creazione di connessione, la creazione di avvio automatico e dello schema del database. Difficoltà sorgono principalmente da tabelle dei fatti hello che Gestione connessione di database hello fornita da Entity Framework si interseca con funzionalità di gestione connessione hello hello dati dipendenti interfacce di routing fornite dalla libreria client di database elastico hello. 

## <a name="elastic-database-tools-assumptions"></a>Presupposti degli strumenti dei database elastici
Per le definizioni dei termini, vedere il [glossario degli strumenti del database elastico](sql-database-elastic-scale-glossary.md).

La libreria client dei database elastici consente di definire partizioni dei dati applicativi denominate shardlet. Gli Shardlet vengono identificati da una chiave di partizionamento orizzontale e sono mappate toospecific database. Un'applicazione può avere tutti i database in base alle esigenze e distribuire hello shardlet tooprovide sufficiente capacità o prestazioni ha requisiti di business corrente. mapping di Hello dei database toohello valori di chiave di partizionamento orizzontale vengono archiviati per una mappa partizioni fornita dal client di database elastico hello API. Questa funzionalità è denominata **Gestione mappe partizioni**. mappa partizioni Hello funge anche da Service broker hello di connessioni di database per le richieste che contengono una chiave di partizionamento orizzontale. Facciamo riferimento toothis funzionalità come **routing dipendente dai dati**. 

gestore mappe partizioni di Hello protegge gli utenti da visualizzazioni incoerenti nei dati di shardlet che possono verificarsi quando vengono eseguite operazioni di gestione di shardlet simultanee (ad esempio rilocazione dati da una partizione tooanother). toodo hello in tal caso, le mappe partizioni gestite da hello client libreria broker hello connessioni al database per un'applicazione. In questo modo, kill tooautomatically funzionalità di hello partizioni mappa una connessione al database quando le operazioni di gestione di partizioni potrebbe influire sulla hello shardlet che hello connessione è stata creata per. Questo approccio è necessario toointegrate con alcune delle funzionalità di Entity Framework, ad esempio la creazione di nuove connessioni da un uno toocheck esistente per l'esistenza del database. In generale, l'osservazione è stata che costruttori DbContext standard hello solo funzionano in maniera affidabile chiuse le connessioni ai database che possono essere clonate in modo sicuro per il lavoro di Entity Framework. il principio di progettazione Hello di database elastico è invece tooonly broker aperto connessioni. Si pensa di chiusura della connessione negoziata dalla libreria client hello passandolo tramite toohello EF DbContext potrebbe risolvere il problema. Chiusura della connessione hello e basarsi su apertura toore EF, tuttavia, uno foregoes controlli di convalida e la coerenza di hello eseguiti dalla libreria hello. funzionalità di migrazioni Hello in Entity Framework, tuttavia, utilizza queste hello toomanage connessioni dello schema di database in modo trasparente toohello applicazione sottostante. In teoria, si desideri tooretain e combinare tutte le funzionalità dalla libreria client di database elastico hello sia EF in hello stessa applicazione. Hello nella sezione seguente vengono illustrate queste proprietà e i requisiti in modo più dettagliato. 

## <a name="requirements"></a>Requisiti
Quando si utilizzano con libreria client di database elastico hello e le API di Entity Framework, è necessario hello tooretain le proprietà seguenti: 

* **Scalabilità orizzontale**: tooadd o Rimuovi database dal livello dati hello applicazione partizionati hello necessarie per le esigenze di capacità hello di un'applicazione hello. Ciò significa controllo sulla creazione di hello hello e l'eliminazione del database e l'utilizzo di hello elastico partizioni mappa gestione API toomanage del database e i mapping di shardlet. 
* **Coerenza**: partizionamento orizzontale si avvale di un'applicazione hello e utilizza hello funzionalità routing dipendente di dati della libreria client hello. danneggiamento tooavoid o risultati della query non corretto, le connessioni sono negoziate mediante gestore mappe partizioni di hello. In questo modo vengono mantenute anche la convalida e la coerenza.
* **Code First**: praticità hello tooretain del primo paradigma del EF codice. In Code First, le classi in un'applicazione hello vengono eseguito il mapping in modo trasparente toohello strutture di database sottostanti. il codice dell'applicazione Hello interagisce con DbSets che mascherare la maggior parte dei relativi aspetti hello sottostante l'elaborazione del database.
* **Schema**: Entity Framework gestisce la creazione iniziale dello schema del database e la successiva evoluzione dello schema mediante migrazioni. Con il mantenimento di queste funzionalità, è semplice come dati si evolve hello adattamento dell'app. 

indica a Hello materiale sussidiario seguente come toosatisfy questi requisiti per le applicazioni prima di codice utilizzando gli strumenti di database elastico. 

## <a name="data-dependent-routing-using-ef-dbcontext"></a>Routing dipendente dai dati con DbContext di Entity Framework
Le connessioni di database con Entity Framework vengono in genere gestite tramite sottoclassi di **DbContext**. Creare le sottoclassi derivandole da **DbContext**. In questo campo definire il **DbSets** che implementano le raccolte di database di backup di hello di oggetti CLR per l'applicazione. Nel contesto di hello di routing dipendente dai dati, è possibile identificare diverse proprietà utile che non contengono necessariamente per altri scenari di applicazioni Entity Framework prima di codice: 

* database Hello esiste già e registrata nella mappa partizioni di database elastico hello. 
* schema di Hello dell'applicazione hello è già stato distribuito toohello database (come illustrato di seguito). 
* Database toohello connessioni di routing dipendente dai dati sono negoziata da mappa partizioni hello. 

toointegrate **DbContexts** con il routing dipendente dai dati per la scalabilità orizzontale:

1. Creare connessioni fisica del database tramite le interfacce client di database elastico hello di gestore mappe partizioni di hello, 
2. Eseguire il wrapping connessione hello con hello **DbContext** sottoclasse
3. Passare la connessione hello verso il basso in hello **DbContext** tutta l'elaborazione sul lato EF hello hello accade anche tooensure di classi di base. 

Hello esempio di codice seguente viene illustrato questo approccio. (Questo codice è anche in hello che accompagna il progetto di Visual Studio)

    public class ElasticScaleContext<T> : DbContext
    {
    public DbSet<Blog> Blogs { get; set; }
    …

        // C'tor for data dependent routing. This call will open a validated connection 
        // routed toohello proper shard by hello shard map manager. 
        // Note that hello base class c'tor call will fail for an open connection
        // if migrations need toobe done and SQL credentials are used. This is hello reason for hello 
        // separation of c'tors into hello data-dependent routing case (this c'tor) and hello internal c'tor for new shards.
        public ElasticScaleContext(ShardMap shardMap, T shardingKey, string connectionStr)
            : base(CreateDDRConnection(shardMap, shardingKey, connectionStr), 
            true /* contextOwnsConnection */)
        {
        }

        // Only static methods are allowed in calls into base class c'tors.
        private static DbConnection CreateDDRConnection(
        ShardMap shardMap, 
        T shardingKey, 
        string connectionStr)
        {
            // No initialization
            Database.SetInitializer<ElasticScaleContext<T>>(null);

            // Ask shard map toobroker a validated connection for hello given key
            SqlConnection conn = shardMap.OpenConnectionForKey<T>
                                (shardingKey, connectionStr, ConnectionOptions.Validate);
            return conn;
        }    

## <a name="main-points"></a>Punti principali
* Un nuovo costruttore sostituisce il costruttore predefinito hello in sottoclasse DbContext hello 
* Hello nuovo costruttore accetta gli argomenti hello necessari per il routing dipendente dai dati tramite una libreria client di database elastico:
  
  * Hello partizioni mappa tooaccess hello interfacce di routing dipendente dai dati,
  * Hello shardlet hello tooidentify chiave di partizionamento orizzontale,
  * una stringa di connessione con le credenziali di hello per partizioni di toohello routing connessione di hello dipendente dai dati. 
* costruttore della classe base toohello Hello chiamata prende una deviazione in un metodo statico che esegue tutte le fasi hello necessarie per il routing dipendente dai dati. 
  
  * Usa chiamata OpenConnectionForKey hello delle interfacce di client di database elastico hello in hello partizioni mappa tooestablish una connessione aperta.
  * mappa partizioni Hello Crea partizioni di toohello connessione aperta hello che contiene shardlet hello per hello data chiave di partizionamento orizzontale.
  * Questa connessione aperta viene passata il costruttore della classe base toohello indietro di tooindicate DbContext che questa connessione è toobe utilizzato da Entity Framework anziché consentire a Entity Framework crea automaticamente una nuova connessione. Connessione di hello in questo modo è stata contrassegnata dal client di database elastico hello API in modo che sia possibile garantire la coerenza con le operazioni di gestione di partizioni della mappa.

Utilizzare il nuovo costruttore di hello per la sottoclasse DbContext anziché il costruttore predefinito hello nel codice. Di seguito è fornito un esempio: 

    // Create and save a new blog.

    Console.Write("Enter a name for a new blog: "); 
    var name = Console.ReadLine(); 

    using (var db = new ElasticScaleContext<int>( 
                            sharding.ShardMap,  
                            tenantId1,  
                            connStrBldr.ConnectionString)) 
    { 
        var blog = new Blog { Name = name }; 
        db.Blogs.Add(blog); 
        db.SaveChanges(); 

        // Display all Blogs for tenant 1 
        var query = from b in db.Blogs 
                    orderby b.Name 
                    select b; 
     … 
    }

nuovo costruttore Hello verrà visualizzata la partizione di toohello connessione hello contenente dati hello per shardlet hello identificato dal valore hello **tenantid1**. Hello codice hello **utilizzando** blocco rimane invariato tooaccess hello **DbSet** per i blog mediante EF in partizioni hello per **tenantid1**. In questo modo la semantica per una partizione toohello con ambito di codice hello in hello utilizzando blocco in modo che tutte le operazioni di database sono ora in cui **tenantid1** viene mantenuta. Ad esempio, una query LINQ sul blog di hello **DbSet** potrebbe restituire solo i blog archiviati nella partizione corrente hello, ma non hello quelli archiviati in altre partizioni.  

#### <a name="transient-faults-handling"></a>Gestione degli errori temporanei
Hello Microsoft Patterns & Practices team hello pubblicato [hello Transient Fault Handling Application Block](https://msdn.microsoft.com/library/dn440719.aspx). libreria di Hello viene utilizzata con una libreria client di scalabilità elastica in combinazione con Entity Framework. Tuttavia, assicurarsi che qualsiasi eccezione temporanea restituisce tooa luogo in cui è possibile assicurare che il nuovo costruttore hello utilizzato dopo un errore temporaneo in modo che qualsiasi nuovo tentativo di connessione utilizzando i costruttori di hello che sono stati modificati. In caso contrario, un toohello connessione corretto partizione non è garantito e non sono garanzie connessione hello viene mantenuta come mappa partizioni toohello si verificano modifiche. 

Hello nell'esempio di codice seguente illustra l'utilizzo un criterio di ripetizione SQL possibile intorno hello nuovo **DbContext** costruttori sottoclasse: 

    SqlDatabaseUtils.SqlRetryPolicy.ExecuteAction(() => 
    { 
        using (var db = new ElasticScaleContext<int>( 
                                sharding.ShardMap,  
                                tenantId1,  
                                connStrBldr.ConnectionString)) 
            { 
                    var blog = new Blog { Name = name }; 
                    db.Blogs.Add(blog); 
                    db.SaveChanges(); 
            … 
            } 
        }); 

**SqlDatabaseUtils.SqlRetryPolicy** in hello codice precedente viene definito come un **SqlDatabaseTransientErrorDetectionStrategy** con un numero di tentativi di 10 e 5 secondi di attesa tra i tentativi. Questo approccio è simile toohello indicazioni per Entity Framework e le transazioni avviate dall'utente (vedere [limitazioni con nuovo tentativo di strategie di esecuzione (a partire EF6)](http://msdn.microsoft.com/data/dn307226). Entrambe le situazioni richiedono tale applicazione hello controlla hello ambito toowhich hello eccezione temporanea restituisce: tooeither riaprire transazione hello o (come illustrato) ricreare contesto hello dal costruttore di hello corretto che utilizza hello database elastico libreria client.

Hello toocontrol necessità in eccezioni temporanee Iniziamo in ambito impedisce anche utilizzare hello incorporati hello **SqlAzureExecutionStrategy** fornito con Entity Framework. **SqlAzureExecutionStrategy** verrebbe riaprire una connessione, ma non utilizzare **OpenConnectionForKey** e pertanto Ignora tutte le convalide hello che viene eseguita come parte di hello **OpenConnectionForKey** chiamare. Nell'esempio di codice hello utilizza invece incorporato hello **DefaultExecutionStrategy** anche fornito con Entity Framework. Anziché troppo**SqlAzureExecutionStrategy**, funziona correttamente in combinazione con criteri di ripetizione hello dalla gestione degli errori temporanei. criteri di esecuzione Hello sono impostato in hello **ElasticScaleDbConfiguration** classe. Si noti che si è deciso di non toouse **DefaultSqlExecutionStrategy** poiché si consiglia di toouse **SqlAzureExecutionStrategy** se si verificano eccezioni temporanee - ciò provocherebbe toowrong comportamento come illustrato. Per ulteriori informazioni sui criteri di tentativi diverso hello ed Entity Framework, vedere [resilienza delle connessioni in EF](http://msdn.microsoft.com/data/dn456835.aspx).     

#### <a name="constructor-rewrites"></a>Riscritture dei costruttori
esempi di codice precedenti Hello illustrano predefinito hello costruttore riscrive richiesto per l'applicazione in ordine toouse dipendente dai dati di routing con hello Entity Framework. Hello nella tabella seguente consente di generalizzare costruttori di tooother questo approccio. 

| Costruttore corrente | Costruttore riscritto per i dati | Costruttore base | Note |
| --- | --- | --- | --- |
| MyContext() |ElasticScaleContext(ShardMap, TKey) |DbContext(DbConnection, bool) |connessione Hello deve toobe una funzione della mappa partizioni hello e la chiave di routing dipendente dai dati hello. Necessaria la creazione di connessione automatica tooby passata da Entity Framework e usare connessione hello toobroker di hello partizioni della mappa. |
| MyContext(string) |ElasticScaleContext(ShardMap, TKey) |DbContext(DbConnection, bool) |connessione Hello è una funzione della mappa partizioni hello e la chiave di routing dipendente dai dati hello. Una stringa di connessione o nome del database non funzionerà man mano che la convalida di elementi da ignorare dalla mappa partizioni hello. |
| MyContext(DbCompiledModel) |ElasticScaleContext(ShardMap, TKey, DbCompiledModel) |DbContext(DbConnection, DbCompiledModel, bool) |connessione Hello verrà vengono create per hello specificato chiave di partizionamento orizzontale e di mappa partizioni con il modello di hello forniti. modello compilato Hello verrà passata in toohello c'tor di base. |
| MyContext(DbConnection, bool) |ElasticScaleContext(ShardMap, TKey, bool) |DbContext(DbConnection, bool) |connessione Hello deve toobe dedotto dalla mappa partizioni hello e la chiave di hello. Ma non può essere fornita come input (a meno che tale input era già in uso mappa partizioni hello e la chiave di hello). Hello Boolean verrà passato. |
| MyContext(string, DbCompiledModel) |ElasticScaleContext(ShardMap, TKey, DbCompiledModel) |DbContext(DbConnection, DbCompiledModel, bool) |connessione Hello deve toobe dedotto dalla mappa partizioni hello e la chiave di hello. Ma non può essere fornita come input (a meno che tale input utilizzava mappa partizioni hello e la chiave di hello). modello compilato Hello verrà passato. |
| MyContext(ObjectContext, bool) |ElasticScaleContext(ShardMap, TKey, ObjectContext, bool) |DbContext(ObjectContext, bool) |nuovo costruttore Hello deve tooensure che qualsiasi connessione in hello che ObjectContext passato come input è nuovamente indirizzato tooa gestiti da scalabilità elastica. Una descrizione dettagliata dei ObjectContexts esula dall'ambito di hello di questo documento. |
| MyContext(DbConnection, DbCompiledModel,bool) |ElasticScaleContext(ShardMap, TKey, DbCompiledModel, bool) |DbContext(DbConnection, DbCompiledModel, bool); |connessione Hello deve toobe dedotto dalla mappa partizioni hello e la chiave di hello. connessione Hello non può essere fornito come input (a meno che tale input era già in uso mappa partizioni hello e la chiave di hello). Modello e un valore booleano vengono passati nel costruttore della classe base toohello. |

## <a name="shard-schema-deployment-through-ef-migrations"></a>Distribuzione dello schema partizione tramite migrazioni di Entity Framework
Gestione automatica dello schema è un'utile fornita da Entity Framework hello. Nel contesto di hello delle applicazioni che utilizzano gli strumenti di database elastici, si desidera tooretain questa funzionalità tooautomatically provisioning hello schema toonewly creato le partizioni quando i database vengono aggiunti toohello partizionati applicazione. Hello viene usata principalmente tooincrease capacità a livello di dati hello per le applicazioni partizionate mediante EF. Utilizzare la funzionalità di Entity Framework per la gestione dello schema di riduce l'attività di amministrazione di database hello con un'applicazione partizionata basata su Entity Framework. 

La distribuzione dello schema tramite migrazioni di Entity Framework funziona al meglio con le **connessioni non aperte**. Si tratta invece di scenario di toohello per routing dipendente dai dati che si basa su una connessione aperta hello fornita dall'API client di database elastico hello. Un'altra differenza è il requisito di coerenza hello: durante la verifica coerenza tooensure auspicabile per tutti i dati dipendenti dal routing connessioni tooprotect contro la manipolazione del mappa partizioni simultanee, non è un problema con nuovo database tooa distribuzione dello schema iniziale che non è ancora stato registrato nella mappa partizioni hello e non è ancora stato allocato toohold shardlet. È pertanto possibile basarsi su connessioni di database normale per questa scenari, come il routing dipendente dai toodata anziché.  

In tal modo in cui la distribuzione dello schema tramite le migrazioni di Entity Framework è strettamente con la registrazione di hello del nuovo database hello come una partizione nella mappa partizioni dell'applicazione hello tooan approccio. Questo comportamento si basa su hello seguenti prerequisiti: 

* database Hello è già stato creato. 
* database Hello è vuoto, contiene nessuno schema utente e nessun dato utente.
* database Hello non sono ancora accessibili attraverso le API client di database elastico hello per il routing dipendente dai dati. 

Con questi prerequisiti soddisfatti, è possibile creare una normale non aperto **SqlConnection** tookick off le migrazioni di Entity Framework per la distribuzione dello schema. Questo approccio viene illustrato nell'esempio di codice seguente Hello. 

        // Enter a new shard - i.e. an empty database - toohello shard map, allocate a first tenant tooit  
        // and kick off EF intialization of hello database toodeploy schema 

        public void RegisterNewShard(string server, string database, string connStr, int key) 
        { 

            Shard shard = this.ShardMap.CreateShard(new ShardLocation(server, database)); 

            SqlConnectionStringBuilder connStrBldr = new SqlConnectionStringBuilder(connStr); 
            connStrBldr.DataSource = server; 
            connStrBldr.InitialCatalog = database; 

            // Go into a DbContext tootrigger migrations and schema deployment for hello new shard. 
            // This requires an un-opened connection. 
            using (var db = new ElasticScaleContext<int>(connStrBldr.ConnectionString)) 
            { 
                // Run a query tooengage EF migrations 
                (from b in db.Blogs 
                    select b).Count(); 
            } 

            // Register hello mapping of hello tenant toohello shard in hello shard map. 
            // After this step, data-dependent routing on hello shard map can be used 

            this.ShardMap.CreatePointMapping(key, shard); 
        } 


Questo esempio viene illustrato il metodo hello **RegisterNewShard** che registri hello partizioni nella mappa partizioni hello, distribuisce lo schema di hello tramite migrazioni EF e archivia un mapping di una partizione toohello chiave di partizionamento orizzontale. Si basa su un costruttore di hello **DbContext** sottoclasse (**ElasticScaleContext** nell'esempio hello) che accetta come input una stringa di connessione SQL. codice Hello di questo costruttore è semplice, come hello esempio illustrato di seguito: 

        // C'tor toodeploy schema and migrations tooa new shard 
        protected internal ElasticScaleContext(string connectionString) 
            : base(SetInitializerForConnection(connectionString)) 
        { 
        } 

        // Only static methods are allowed in calls into base class c'tors 
        private static string SetInitializerForConnection(string connnectionString) 
        { 
            // We want existence checks so that hello schema can get deployed 
            Database.SetInitializer<ElasticScaleContext<T>>( 
        new CreateDatabaseIfNotExists<ElasticScaleContext<T>>()); 

            return connnectionString; 
        } 

Versione di hello del costruttore hello ereditati dalla classe base hello uno potrebbe avere usato. Ma hello codice esigenze tooensure che hello inizializzatore predefinito per Entity Framework viene usato durante la connessione. Di conseguenza hello deviazione breve in un metodo statico hello prima di chiamare il costruttore della classe base hello con la stringa di connessione hello. Si noti che la registrazione di hello di partizioni deve essere eseguito in un tooensure dominio o un processo app diverse impostazioni di inizializzatore hello per Entity Framework non sono in conflitto. 

## <a name="limitations"></a>Limitazioni
approcci Hello descritti nel presente documento comportano un paio di limitazioni: 

* Le applicazioni Entity Framework che utilizzano **LocalDb** prima di tutto necessario database di SQL Server toomigrate tooa normale prima di utilizzare una libreria client di database elastico. Con **LocalDb**non è possibile scalare orizzontalmente un'applicazione mediante il partizionamento orizzontale con la scalabilità elastica. Per lo sviluppo è comunque possibile usare **LocalDb**. 
* Qualsiasi applicazione toohello modifiche che implicano modifiche dello schema di database è necessario toogo tramite le migrazioni di EF su tutte le partizioni. codice di esempio Hello per questo documento viene illustrato come toodo questo. Considerare l'utilizzo di Update-Database con un tooiterate parametro ConnectionString su tutte le partizioni; estrazione hello T-SQL script o del hello in sospeso la migrazione tramite Update-Database con hello - opzione di Script e applicare le partizioni tooyour script hello T-SQL.  
* Data una richiesta, si presuppone che tutti i processi del database è contenuto all'interno di una singola partizione come identificato dalla chiave di partizionamento orizzontale hello fornita dalla richiesta hello. Questo presupposto, tuttavia, non è sempre valido, Ad esempio, quando non è possibile toomake una chiave di partizionamento orizzontale disponibile. tooaddress, hello libreria client fornisce hello **MultiShardQuery** classe che implementa un'astrazione di connessione per l'esecuzione di query su più partizioni. Apprendimento hello toouse **MultiShardQuery** in combinazione con Entity Framework è oltre l'ambito di hello di questo documento

## <a name="conclusion"></a>Conclusioni
Passaggi hello descritte nel presente documento, le applicazioni di EF possono utilizzare funzionalità della libreria di hello database elastico client per i dati dipendenti routing effettuando il refactoring di costruttori di hello **DbContext** sottoclassi utilizzate in hello EF applicazione. Toothose punti in cui è necessaria la modifica di hello limiti **DbContext** classi esistono già. Inoltre, le applicazioni Entity Framework è possono continuare toobenefit dalla distribuzione automatica dello schema combinando i passaggi di hello che richiamano hello necessarie EF migrazioni con la registrazione di hello di nuove partizioni e i mapping nella mappa partizioni hello. 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-scale-use-entity-framework-applications-visual-studio/sample.png
