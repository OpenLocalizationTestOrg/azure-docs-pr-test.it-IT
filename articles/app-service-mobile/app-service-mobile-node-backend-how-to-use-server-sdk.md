---
title: toowork aaaHow con i server back-end di hello Node.js SDK per App per dispositivi mobili | Documenti Microsoft
description: Informazioni su come toowork con hello server back-end di Node.js SDK per App Mobile di servizio App di Azure.
services: app-service\mobile
documentationcenter: 
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: e7d97d3b-356e-4fb3-ba88-38ecbda5ea50
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: node
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 2b1ea5fda6f6ca422b92fe29ff8d16bf035018d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-azure-mobile-apps-nodejs-sdk"></a>Come toouse hello Azure Mobile App Node.js SDK
[!INCLUDE [app-service-mobile-selector-server-sdk](../../includes/app-service-mobile-selector-server-sdk.md)]

In questo articolo fornisce informazioni dettagliate ed esempi che mostrano come toowork con un back-end di Node.js in Azure App Service App per dispositivi mobili.

## <a name="Introduction"></a>Introduzione
App per dispositivi mobili Azure App Service fornisce hello funzionalità tooadd ottimizzato mobile l'accesso ai dati dell'applicazione web di tooa API Web.  Hello Azure App Service Mobile App SDK è disponibile per applicazioni web ASP.NET e Node.js.  Hello SDK fornisce hello seguenti operazioni:

* Operazioni su tabella (read, insert, update, delete) per l'accesso ai dati
* Operazioni sulle API personalizzate

Entrambe le operazioni permettono l'autenticazione in tutti i provider di identità consentiti dal servizio app di Azure, inclusi i provider di identità basati su social network, ad esempio Facebook, Twitter, Google e Microsoft nonché Azure Active Directory per l'identità aziendale.

È possibile trovare esempi per ogni caso d'usano in hello [directory esempi su GitHub].

## <a name="supported-platforms"></a>Piattaforme supportate
Hello Azure Mobile App nodo SDK supporta hello che LTS corrente di rilascio del nodo e versioni successive.  A partire dalla scrittura, hello LTS più recente è v4.5.0 di nodo.  Altre versioni di Node potrebbero funzionare, ma non sono supportate.

Hello SDK nodo App Mobile di Azure supporta due driver di database - hello nodo mssql driver supporta SQL Azure e le istanze di SQL Server locale.  driver sqlite3 Hello supporta database SQLite in una singola istanza.

### <a name="howto-cmdline-basicapp"></a>Procedura: creare un back-end di base Node.js tramite hello riga di comando
Ogni back-end Node.js per le app per dispositivi mobili del servizio app di Azure viene avviato come applicazione ExpressJS.  ExpressJS è hello più popolari framework del servizio web disponibile per Node.js.  È possibile creare un'applicazione [Express] di base seguendo questa procedura:

1. Creare una directory per il progetto in una finestra di comando o di PowerShell.

        mkdir basicapp
2. Eseguire la struttura del pacchetto npm init tooinitialize hello.

        cd basicapp
        npm init

    comando di Hello npm init chiede un insieme di progetti di hello tooinitialize domande.  Vedere l'output di esempio hello:

    ![output di Hello npm init][0]
3. Installare le librerie di express e App mobili di azure hello dal repository npm hello.

        npm install --save express azure-mobile-apps
4. Creare un app.js file tooimplement hello mobili server di base.

        var express = require('express'),
            azureMobileApps = require('azure-mobile-apps');

        var app = express(),
            mobile = azureMobileApps();

        // Define a TodoItem table
        mobile.tables.add('TodoItem');

        // Add hello mobile API so it is accessible as a Web API
        app.use(mobile);

        // Start listening on HTTP
        app.listen(process.env.PORT || 3000);

Questa applicazione crea un WebAPI ottimizzata con un singolo endpoint (`/tables/TodoItem`) che fornisce l'accesso non autenticato tooan sottostante l'archivio dati SQL tramite uno schema dinamico.  È adatta per l'avvio rapido delle librerie client seguenti:

* [Avvio rapido di client Android]
* [Avvio rapido di client Apache Cordova]
* [Avvio rapido di client iOS]
* [Avvio rapido di client Windows Store]
* [Avvio rapido di client Xamarin.iOS]
* [Avvio rapido di client Xamarin.Android]
* [Avvio rapido di client Xamarin.Forms]

È possibile trovare codice hello per questa applicazione di base hello [esempio basicapp in GitHub].

### <a name="howto-vs2015-basicapp"></a>Procedura: Creare un back-end Node.js con Visual Studio 2015
Visual Studio 2015 richiede delle applicazioni Node.js toodevelop estensione all'interno di hello IDE.  toostart, installare hello [Node.js Tools 1.1 per Visual Studio].  Una volta installati hello Node.js Tools per Visual Studio, creare un'applicazione di 4. x Express:

1. Aprire hello **nuovo progetto** finestra di dialogo (da **File** > **New** > **progetto...** ).
2. Espandere **Modelli** > **JavaScript** > **Node.js**.
3. Seleziona hello **base Azure Node.js Express 4 applicazione**.
4. Inserire il nome di progetto hello.  Fare clic su *OK*.

    ![Nuovo progetto di Visual Studio 2015][1]
5. Pulsante destro del mouse hello **npm** nodo e selezionare **installare nuovi pacchetti npm...** .
6. Potrebbe essere necessario catalogo di npm toorefresh hello nella creazione di un'applicazione Node.js.  Fare clic su **Refresh** (Aggiorna), se necessario.
7. Immettere *App mobili di azure* nella casella di ricerca hello.  Fare clic su hello **-App mobili di azure-2.0.0** del pacchetto, quindi fare clic su **Installa pacchetto**.

    ![Installare nuovi pacchetti npm][2]
8. Fare clic su **Close**.
9. Aprire hello *app.js* tooadd supporto per applicazioni mobili di Azure SDK hello file.  Nella parte inferiore di riga 6 at hello della libreria hello richiedono istruzioni, aggiungere hello seguente codice:

        var bodyParser = require('body-parser');
        var azureMobileApps = require('azure-mobile-apps');

    Circa riga 27 dopo hello altre istruzioni app.use, aggiungere hello seguente codice:

        app.use('/users', users);

        // Azure Mobile Apps Initialization
        var mobile = azureMobileApps();
        mobile.tables.add('TodoItem');
        app.use(mobile);

    Salvare il file hello.
10. Eseguire un'applicazione hello in locale (Buongiorno API viene pubblicato su http://localhost:3000) oppure pubblicare tooAzure.

### <a name="create-node-backend-portal"></a>Procedura: creare un back-end di Node.js tramite hello portale di Azure
È possibile creare un diritto di back-end delle App per dispositivi mobili in hello [portale di Azure]. Eseguire hello seguenti passaggi oppure creare un client e server insieme seguente hello [creare un'app per dispositivi mobili](app-service-mobile-ios-get-started.md) esercitazione. esercitazione Hello contiene una versione semplificata di queste istruzioni ed è ottimale per la prova dei progetti concetto.

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service-classic](../../includes/app-service-mobile-dotnet-backend-create-new-service-classic.md)]

In hello *iniziare* pannello, in **creare una tabella API**, scegliere **Node.js** come il **language back-end**.
Casella hello per "**sono consapevole che verranno sovrascritti tutti i contenuti del sito.**", quindi fare clic su **tabella TodoItem creare**.

### <a name="download-quickstart"></a>Procedura: Download hello Node.js back-end delle Guide rapide progetto di codice tramite Git
Quando si crea un back-end dell'App Mobile Node.js tramite il portale di hello **introduttiva** pannello creato un progetto di Node.js per l'utente e del sito tooyour distribuito. È possibile aggiungere tabelle e le API e modificare i file di codice back-end Node.js hello nel portale di hello. È anche possibile utilizzare vari strumenti toodownload hello back-end progetto di distribuzione di in modo che è possibile aggiungere o modificare tabelle e le API, quindi pubblicare di nuovo il progetto hello. Per altre informazioni, vedere la [Guida alla distribuzione del servizio app di Azure]. Hello procedura seguente usa un codice del progetto Git repository toodownload hello Guida introduttiva.

1. Se non è già stato fatto, installare Git. Hello passaggi necessari tooinstall Git variano tra i sistemi operativi. Vedere la sezione [Installazione di Git](http://git-scm.com/book/en/Getting-Started-Installing-Git) per indicazioni specifiche del sistema operativo relative a distribuzioni e installazione.
2. Seguire i passaggi di hello in [Enable hello repository di applicazione di servizio App](../app-service-web/app-service-deploy-local-git.md#Step3) repository Git di hello tooenable per il sito di back-end, prendendo nota di hello distribuzione username e password.
3. Nel Pannello di hello per il back-end dell'App Mobile, prendere nota di hello **URL clone Git** impostazione.
4. Eseguire hello `git clone` comando utilizzando l'URL del clone Git hello, immettere la password quando richiesto, come nell'esempio seguente:

        $ git clone https://username@todolist.scm.azurewebsites.net:443/todolist.git
5. Si noti che i file di progetto e esplorazione toolocal directory, ovvero nel precedente esempio hello /todolist, sono stati scaricati. Individuare hello `todoitem.json` file hello `/tables` directory.  Questo file definisce le autorizzazioni sulla tabella.  Anche trovare hello `todoitem.js` file hello stessa directory, che definisce l'operazione CRUD di script per tabella hello.
6. Dopo avere apportato modifiche tooproject file, eseguire hello comandi tooadd, eseguire il commit, quindi caricare il sito toohello le modifiche seguenti:

        $ git commit -m "updated hello table script"
        $ git push origin master

    Quando si aggiungono nuovi file di progetto toohello, è necessario innanzitutto hello tooexecute `git add .` comando.

sito Hello viene ripubblicata senza modifiche ogni volta che un nuovo set di operazioni di commit viene inserito il sito toohello.

### <a name="howto-publish-to-azure"></a>Procedura: pubblicare il tooAzure back-end di Node.js
Microsoft Azure offre numerosi meccanismi per la pubblicazione di Azure App Service Mobile App Node.js back-end per hello servizio di Azure.  tra cui l'uso di strumenti di distribuzione integrati in Visual Studio, strumenti da riga di comando e opzioni di distribuzione continua basate sul controllo del codice sorgente.  Per altre informazioni su questo argomento, vedere la [Guida alla distribuzione del servizio app di Azure].

Il servizio app di Azure include suggerimenti specifici per l'applicazione Node.js che è consigliabile esaminare prima della distribuzione:

* Come troppo[specificare hello nodo versione]
* Come troppo[utilizzare i moduli del nodo]

### <a name="howto-enable-homepage"></a>Procedura: Abilitare una home page dell'applicazione
Molte applicazioni sono una combinazione di web e App per dispositivi mobili e framework ExpressJS hello consente toocombine due facet.  In alcuni casi, tuttavia, è preferibile tooonly implementare un'interfaccia per dispositivi mobili.  È utile tooprovide che un servizio app di hello tooensure di pagina di destinazione sia in esecuzione.  È possibile fornire la propria home page o abilitarne una temporanea.  tooenable una home page temporanea, utilizzare hello seguente tooinstantiate App mobili di Azure:

    var mobile = azureMobileApps({ homePage: true });

Se si desidera questa opzione è disponibile solo quando si sviluppa in locale, è possibile aggiungere questa impostazione tooyour `azureMobile.js` file.

## <a name="TableOperations"></a>Operazioni su tabella
Hello Server Node.js di App mobili di azure SDK fornisce meccanismi tooexpose dati archiviate nel Database di SQL Azure come un WebAPI tabelle.  Sono disponibili cinque operazioni.

| Operazione | Descrizione |
| --- | --- |
| GET /tables/*tablename* |Ottenere tutti i record nella tabella di hello |
| GET /tables/*tablename*/:id |Ottenere un record specifico nella tabella di hello |
| POST /tables/*tablename* |Creare un record nella tabella hello |
| PATCH /tables/*tablename*/:id |Aggiornare un record nella tabella hello |
| DELETE /tables/*tablename*/:id |Eliminare un record nella tabella hello |

Supporta questa WebAPI [OData] ed estende hello tabella dello schema toosupport [sincronizzazione dati offline].

### <a name="howto-dynamicschema"></a>Procedura: Definire le tabelle con uno schema dinamico
Perché sia possibile usare una tabella, è necessario prima definirla.  Le tabelle possono essere definite con uno schema statico (dove developer hello definisce colonne hello all'interno dello schema hello) o in modo dinamico (dove hello SDK controlli schema hello in base alle richieste in ingresso). Inoltre, sviluppatore hello è possibile controllare aspetti specifici di hello WebAPI aggiungendo definizione toohello del codice Javascript.

Come procedura consigliata, è necessario definire ogni tabella in un file Javascript nella directory di tabelle hello, quindi utilizzare le tabelle di hello tables.import() tooimport metodo.  Estensione basic-app hello, sarebbe possibile regolare file app.js hello:

    var express = require('express'),
        azureMobileApps = require('azure-mobile-apps');

    var app = express(),
        mobile = azureMobileApps();

    // Define hello database schema that is exposed
    mobile.tables.import('./tables');

    // Provide initialization of any tables that are statically defined
    mobile.tables.initialize().then(function () {
        // Add hello mobile API so it is accessible as a Web API
        app.use(mobile);

        // Start listening on HTTP
        app.listen(process.env.PORT || 3000);
    });

Definire la tabella hello. / tables/TodoItem.js:

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Additional configuration for hello table goes here

    module.exports = table;

Per impostazione predefinita, le tabelle usano lo schema dinamico.  tooturn disattivare lo schema dinamico impostato a livello globale, hello impostazione App **MS_DynamicSchema** toofalse all'interno di hello portale di Azure.

È possibile trovare un esempio completo in hello [esempio todo in GitHub].

### <a name="howto-staticschema"></a>Procedura: Definire le tabelle con uno schema statico
È possibile definire in modo esplicito hello colonne tooexpose tramite hello WebAPI.  Hello che App mobili di azure Node.js SDK aggiunge automaticamente eventuali colonne aggiuntive, necessarie per dati non in linea sincronizzazione toohello elenco fornito.  Ad esempio, le applicazioni client di avvio rapido richiedono una tabella con due colonne: text (una stringa) e complete (un valore booleano).  
tabella Hello può essere definita in hello tabella JavaScript file di definizione (che si trova nella directory di tabelle hello) come indicato di seguito:

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define hello columns within hello table
    table.columns = {
        "text": "string",
        "complete": "boolean"
    };

    // Turn off dynamic schema
    table.dynamicSchema = false;

    module.exports = table;

Se si definiscono le tabelle in modo statico, è necessario chiamare anche lo schema del database hello toocreate metodo tables.initialize() hello all'avvio.  metodo tables.initialize() Hello restituisce un [promessa] in modo che servizio web hello non soddisfare le richieste prima database hello da inizializzare.

### <a name="howto-sqlexpress-setup"></a>Procedura: Usare SQL Express come archivio dati di sviluppo nel computer locale
Hello App mobili di Azure hello AzureMobile App nodo SDK sono disponibili tre opzioni per la gestione di dati predefinito hello: SDK fornisce tre opzioni per la gestione di dati predefinito hello:

* Hello utilizzare **memoria** archivio di esempio tooprovide un non-persistent driver
* Hello utilizzare **mssql** tooprovide driver un archivio di dati SQL Express per lo sviluppo
* Hello utilizzare **mssql** tooprovide driver un archivio dati di Database SQL di Azure per la produzione

Hello Azure Mobile App Node.js SDK Usa hello [pacchetto Node.js mssql] tooestablish e utilizzare una connessione tooboth SQL Express e Database SQL.  Per questo pacchetto è necessario abilitare le connessioni TCP nell'istanza di SQL Express.

> [!TIP]
> driver di memoria Hello non fornisce un set completo di funzionalità per il test.  Se si desidera tootest back-end in locale, è consigliabile utilizzare hello di un archivio dati di SQL Express e hello driver mssql.
>
>

1. Scaricare e installare [Microsoft SQL Server 2014 Express].  Assicurarsi di che installare SQL Server 2014 Express hello con versione degli strumenti.  A meno che non è necessaria in modo esplicito il supporto a 64 bit, la versione a 32 bit hello utilizza minore quantità di memoria durante l'esecuzione.
2. Eseguire Gestione configurazione SQL Server 2014 hello.

   1. Espandere hello **configurazione di rete SQL Server** nodo nel menu di hello albero a sinistra.
   2. Fare clic su **Protocolli per SQLEXPRESS**.
   3. Fare clic con il pulsante destro del mouse su **TCP/IP** e scegliere **Abilita**.  Fare clic su **OK** nella finestra di dialogo popup hello.
   4. Fare clic con il pulsante destro del mouse su **TCP/IP** e scegliere **Proprietà**.
   5. Fare clic su hello **gli indirizzi IP** scheda.
   6. Trovare hello **IPAll** nodo.  In hello **la porta TCP** immettere **1433**.

          ![Configure SQL Express for TCP/IP][3]
   7. Fare clic su **OK**.  Fare clic su **OK** nella finestra di dialogo popup hello.
   8. Fare clic su **servizi di SQL Server** nel menu di hello albero a sinistra.
   9. Fare clic con il pulsante destro del mouse su **SQL Server (SQLEXPRESS)** e scegliere **Riavvia**
   10. Chiudere Gestione configurazione SQL Server 2014 hello.
3. Eseguire hello SQL Server 2014 Management Studio e connettersi tooyour istanza locale di SQL Express

   1. L'istanza in Esplora oggetti hello e scegliere **proprietà**
   2. Seleziona hello **sicurezza** pagina.
   3. Assicurarsi di hello **modalità di autenticazione di Windows e SQL Server** è selezionata
   4. Fare clic su **OK**

          ![Configure SQL Express Authentication][4]
   5. Espandere **sicurezza** > **gli account di accesso** in hello Esplora oggetti
   6. Fare clic con il pulsante destro del mouse su **Account di accesso** e scegliere **Nuovo account di accesso**
   7. Immettere un nome account di accesso.  Selezionare **Autenticazione di SQL Server**.  Immettere una Password, quindi immettere hello stessa password in **Conferma password**.  password di Hello deve soddisfare i requisiti di complessità di Windows.
   8. Fare clic su **OK**

          ![Add a new user tooSQL Express][5]
   9. Fare clic con il pulsante destro del mouse sul nuovo account di accesso e scegliere **Proprietà**
   10. Seleziona hello **i ruoli del Server** pagina
   11. Controllare hello casella Avanti toohello **dbcreator** ruolo del server
   12. Fare clic su **OK**
   13. Chiudere hello SQL Server 2015 Management Studio

Assicurarsi di hello record username e password che è stata selezionata.  A seconda dei requisiti di database specifico, potrebbe essere necessario tooassign altri ruoli del server o autorizzazioni.

applicazione Node.js Hello legge hello **SQLCONNSTR_MS_TableConnectionString** variabile di ambiente per la stringa di connessione hello per questo database.  Questa variabile può essere impostata all'interno dell'ambiente.  Ad esempio, è possibile utilizzare PowerShell tooset questa variabile di ambiente:

    $env:SQLCONNSTR_MS_TableConnectionString = "Server=127.0.0.1; Database=mytestdatabase; User Id=azuremobile; Password=T3stPa55word;"

Accedere a database hello tramite una connessione TCP/IP e fornire un nome utente e una password per la connessione hello.

### <a name="howto-config-localdev"></a>Procedura: Configurare il progetto per lo sviluppo locale
App per dispositivi mobili Azure legge un file JavaScript denominato *azureMobile.js* dal file System locale hello.  Non utilizzare hello di tooconfigure questo file app Mobile di Azure SDK nell'ambiente di produzione: utilizzare le impostazioni dell'App all'interno di hello [portale di Azure] invece.  Hello *azureMobile.js* file necessario esportare un oggetto di configurazione.  impostazioni di Hello più comuni sono:

* Impostazioni database
* Impostazioni di registrazione diagnostica
* Impostazioni CORS alternative

Un esempio *azureMobile.js* file implementa hello indicato di seguito le impostazioni del database precedente:

    module.exports = {
        cors: {
            origins: [ 'localhost' ]
        },
        data: {
            provider: 'mssql',
            server: '127.0.0.1',
            database: 'mytestdatabase',
            user: 'azuremobile',
            password: 'T3stPa55word'
        },
        logging: {
            level: 'verbose'
        }
    };

È consigliabile aggiungere *azureMobile.js* tooyour *con estensione gitignore* file (o altri ignorare i file di controllo del codice sorgente) tooprevent le password vengano archiviate nel cloud hello.  Configurare sempre le impostazioni di produzione nelle impostazioni dell'App all'interno di hello [portale di Azure].

### <a name="howto-appsettings"></a>Procedura: Configurare le impostazioni dell'app per dispositivi mobili
La maggior parte delle impostazioni in hello *azureMobile.js* file dispone di un'impostazione di App equivalente in hello [portale di Azure].  Uso dell'app di hello seguente elenco tooconfigure nelle impostazioni dell'App:

| Impostazione app | *azureMobile.js* | Descrizione | Valori validi |
|:--- |:--- |:--- |:--- |
| **MS_MobileAppName** |name |nome Hello dell'applicazione hello |string |
| **MS_MobileLoggingLevel** |logging.level |Livello di log minimo di messaggi toolog |error, warning, info, verbose, debug, silly |
| **MS_DebugMode** |debug |Abilitare o disabilitare la modalità di debug |true, false |
| **MS_TableSchema** |data.schema |Nome dello schema predefinito per le tabelle SQL |string (valore predefinito: dbo) |
| **MS_DynamicSchema** |data.dynamicSchema |Abilitare o disabilitare la modalità di debug |true, false |
| **MS_DisableVersionHeader** |versione (set tooundefined) |Disabilita l'intestazione X-ZUMO-Server-versione di hello |true, false |
| **MS_SkipVersionCheck** |skipversioncheck |Disabilita il controllo della versione API client hello |true, false |

tooset un'impostazione di App:

1. Accedi toohello [portale di Azure].
2. Selezionare **tutte le risorse** o **servizi App** quindi hello nome dell'App Mobile.
3. pannello impostazioni Hello viene aperto per impostazione predefinita. In caso contrario fare clic su **Impostazioni**.
4. Fare clic su **le impostazioni dell'applicazione** nel menu Generale hello.
5. Scorrere toohello sezione App impostazioni.
6. Se l'app impostazione già esiste, fare clic su hello valore hello app impostazione tooedit hello.
7. Se l'impostazione dell'app non esiste, immettere hello impostazione dell'App nella casella chiave hello e valore hello nella casella valore hello.
8. Al termine, fare clic su **Salva**.

Per modificare la maggior parte delle impostazioni dell'app, è necessario riavviare il servizio.

### <a name="howto-use-sqlazure"></a>Procedura: Usare il database SQL come archivio dati di produzione
<!--- ALTERNATE INCLUDE - we can't use ../includes/app-service-mobile-dotnet-backend-create-new-service.md - slightly different semantics -->

L'uso del database SQL di Azure come archivio dati è identico in tutti i tipi di applicazione del Servizio app di Azure. Se non è già stato fatto, seguire questi toocreate passaggi un back-end dell'App Mobile.

1. Accedi toohello [portale di Azure].
2. Hello in alto a sinistra della finestra hello, fare clic su hello **+ nuovo** pulsante > **Web e dispositivi mobili** > **App Mobile**, quindi specificare un nome per il back-end dell'App Mobile.
3. In hello **gruppo di risorse** immettere hello stesso nome dell'app.
4. piano di servizio App predefinito Hello è selezionato.  Se si desidera toochange piano di servizio App, è possibile farlo facendo clic sul piano di servizio App hello > **+ Crea nuovo**.  Specificare un nome del piano di servizio App nuovo hello e selezionare un percorso appropriato.  Selezionare un piano tariffario appropriato per il servizio hello tariffario hello. Selezionare **visualizzare tutti** tooview più prezzi opzioni, ad esempio **libero** e **Shared**.  Dopo aver selezionato il livello di prezzo, fare clic su hello **selezionare** pulsante.  In hello **piano di servizio App** pannello, fare clic su **OK**.
5. Fare clic su **Crea**. L'operazione di provisioning di un back-end dell'app per dispositivi mobili può richiedere alcuni minuti.  Una volta che viene eseguito il provisioning di back-end App Mobile hello, hello viene visualizzato il portale di hello **impostazioni** pannello back-end di hello App per dispositivi mobili.

Dopo la creazione di back-end di hello App per dispositivi mobili, è possibile scegliere tooeither connettere un SQL database tooyour App Mobile back-end esistente o creare un nuovo database SQL.  In questa sezione viene creato un database SQL.

> [!NOTE]
> Se si dispone già di un database in hello stessa posizione di back-end di hello app per dispositivi mobili, è invece possibile scegliere **utilizza un database esistente** e quindi selezionare il database. non è consigliabile utilizzare Hello di un database in una posizione diversa latenze più elevate.
>
>

1. In hello nuovo back-end App Mobile, fare clic su **impostazioni** > **App Mobile** > **dati** > **+ Aggiungi**.
2. In hello **aggiungere una connessione dati** pannello, fare clic su **Database di SQL - configurare le impostazioni necessarie** > **creare un nuovo database**.  Immettere il nome di hello del nuovo database hello in hello **nome** campo.
3. Fare clic su **Server**.  In hello **nuovo server** pannello, immettere un nome server univoci in hello **nome Server** campo e forniscono un adatto **account di accesso amministratore Server** e **Password**.  Verificare **server tooaccess di servizi di azure Consenti** è selezionata.  Fare clic su **OK**.

    ![Creare un database SQL di Azure][6]
4. In hello **nuovo database** pannello, fare clic su **OK**.
5. In hello **aggiungere una connessione dati** pannello seleziona **stringa di connessione**, immettere l'account di accesso hello e la password fornita durante la creazione di database hello.  Se si utilizza un database esistente, fornire le credenziali di account di accesso hello per quel database.  Dopo averli immessi fare clic su **OK**.
6. In hello **aggiungere una connessione dati** pannello fare nuovamente clic **OK** database hello toocreate.

<!--- END OF ALTERNATE INCLUDE -->

Creazione del database hello può richiedere alcuni minuti.  Hello utilizzare **notifiche** area toomonitor hello lo stato di avanzamento della distribuzione hello.  Avanza fino a quando il database di hello è stato distribuito correttamente.  Dopo aver distribuito correttamente, viene creata una stringa di connessione per istanza di Database SQL di hello nel back-end le impostazioni dell'App per dispositivi mobili.  È possibile visualizzare questa impostazione di app in hello **impostazioni** > **le impostazioni dell'applicazione** > **le stringhe di connessione**.

### <a name="howto-tables-auth"></a>Procedura: richiedere l'autenticazione per accesso tootables
Se si desidera toouse l'autenticazione del servizio App con endpoint tabelle hello, è necessario configurare l'autenticazione del servizio App in hello [portale di Azure] prima.  Per ulteriori informazioni sulla configurazione dell'autenticazione in un servizio App di Azure, esaminare hello Guida alla configurazione per il provider di identità hello intendi toouse:

* [Modalità autenticazione di Azure Active Directory tooconfigure]
* [Come tooconfigure l'autenticazione di Facebook]
* [Come tooconfigure l'autenticazione di Google]
* [Come tooconfigure Microsoft Authentication]
* [Come tooconfigure autenticazione Twitter]

Ogni tabella dispone di una proprietà di accesso che può essere utilizzato toocontrol accesso toohello tabella.  Hello seguente esempio mostra una tabella in modo statico definita necessaria autenticazione.

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define hello columns within hello table
    table.columns = {
        "text": "string",
        "complete": "boolean"
    };

    // Turn off dynamic schema
    table.dynamicSchema = false;

    // Require authentication tooaccess hello table
    table.access = 'authenticated';

    module.exports = table;

proprietà di accesso Hello può assumere uno dei tre valori

* *anonimo* indica che un'applicazione client hello è consentita tooread dati senza autenticazione
* *autenticazione* indica che un'applicazione hello client deve inviare un token di autenticazione valido con richiesta di hello
* *disabled* indica che la tabella è attualmente disabilitata.

Se la proprietà di accesso hello è definita, è consentito l'accesso non autenticato.

### <a name="howto-tables-getidentity"></a>Procedura: Usare le attestazioni di autenticazione con le tabelle
È possibile impostare diverse attestazioni richieste quando viene impostata l'autenticazione.  Queste attestazioni non sono in genere disponibili tramite hello `context.user` oggetto.  Tuttavia, possono essere recuperate utilizzando hello `context.user.getIdentity()` metodo.  Hello `getIdentity()` metodo restituisce una promessa che risolve l'oggetto tooan.  oggetto Hello è codificato dal metodo di autenticazione (facebook, google, twitter, microsoftaccount o aad).

Ad esempio, se si configura l'autenticazione di Account Microsoft e l'attestazione basata su indirizzi di posta elettronica hello richiesta, è possibile aggiungere record toohello indirizzo di posta elettronica hello con hello controller nella tabella seguente:

    var azureMobileApps = require('azure-mobile-apps');

    // Create a new table definition
    var table = azureMobileApps.table();

    table.columns = {
        "emailAddress": "string",
        "text": "string",
        "complete": "boolean"
    };
    table.dynamicSchema = false;
    table.access = 'authenticated';

    /**
    * Limit hello context query toothose records with hello authenticated user email address
    * @param {Context} context hello operation context
    * @returns {Promise} context execution Promise
    */
    function queryContextForEmail(context) {
        return context.user.getIdentity().then((data) => {
            context.query.where({ emailAddress: data.microsoftaccount.claims.emailaddress });
            return context.execute();
        });
    }

    /**
    * Adds hello email address from hello claims toohello context item - used for
    * insert operations
    * @param {Context} context hello operation context
    * @returns {Promise} context execution Promise
    */
    function addEmailToContext(context) {
        return context.user.getIdentity().then((data) => {
            context.item.emailAddress = data.microsoftaccount.claims.emailaddress;
            return context.execute();
        });
    }

    // Configure specific code when hello client does a request
    // READ - only return records belonging toohello authenticated user
    table.read(queryContextForEmail);

    // CREATE - add or overwrite hello userId based on hello authenticated user
    table.insert(addEmailToContext);

    // UPDATE - only allow updating of record belong toohello authenticated user
    table.update(queryContextForEmail);

    // DELETE - only allow deletion of records belong toohello authenticated uer
    table.delete(queryContextForEmail);

    module.exports = table;

toosee le attestazioni sono disponibili, utilizzare un hello tooview di web browser `/.auth/me` endpoint del sito.

### <a name="howto-tables-disabled"></a>Procedura: operazioni di tabella toospecific Disabilita accesso
In aggiunta tooappearing tabella hello, proprietà di accesso hello può essere utilizzato toocontrol singole operazioni.  Sono disponibili quattro operazioni:

* *lettura* hello ottenere RESTful operazione sulla tabella hello
* *Inserisci* hello POST RESTful operazione sulla tabella hello
* *aggiornare* hello PATCH RESTful operazione sulla tabella hello
* *eliminare* hello eliminare RESTful operazione sulla tabella hello

Ad esempio, è preferibile tooprovide una tabella non autenticata di sola lettura:

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Read-Only table - only allow READ operations
    table.read.access = 'anonymous';
    table.insert.access = 'disabled';
    table.update.access = 'disabled';
    table.delete.access = 'disabled';

    module.exports = table;

### <a name="howto-tables-query"></a>Procedura: modificare query hello utilizzato con operazioni di tabella
Un requisito comune per le operazioni di tabella è una vista limitata di dati hello tooprovide.  Ad esempio, è possibile fornire una tabella che è contrassegnata con hello autenticato ID utente in modo che è possibile leggere o aggiornare i propri record.  Hello definizione della tabella seguente fornisce questa funzionalità:

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define a static schema for hello table
    table.columns = {
        "userId": "string",
        "text": "string",
        "complete": "boolean"
    };
    table.dynamicSchema = false;

    // Require authentication for this table
    table.access = 'authenticated';

    // Ensure that only records for hello authenticated user are retrieved
    table.read(function (context) {
        context.query.where({ userId: context.user.id });
        return context.execute();
    });

    // When adding records, add or overwrite hello userId with hello authenticated user
    table.insert(function (context) {
        context.item.userId = context.user.id;
        return context.execute();
    });

    module.exports = table;

Le operazioni che in genere eseguono una query avranno una proprietà query modificabile con una clausola where. proprietà query Hello è un [QueryJS] oggetto che è in grado di elaborare tooconvert usato un toosomething di query OData che hello dati di back-end.  Per i casi di uguaglianza semplici (ad esempio hello uno precedente), è possibile utilizzare una mappa. È anche possibile aggiungere clausole SQL specifiche:

    context.query.where('myfield eq ?', 'value');

### <a name="howto-tables-softdelete"></a>Procedura: Configurare l'eliminazione temporanea in una tabella
L'eliminazione temporanea non elimina effettivamente i record.  Invece contrassegna come eliminati nel database di hello impostando tootrue colonna hello eliminato.  a meno che non hello Mobile Client SDK utilizza IncludeDeleted(), Hello App Mobile di Azure SDK rimuove automaticamente record eliminato dai risultati.  eliminare una tabella per soft, tooconfigure impostare hello `softDelete` proprietà nel file di definizione di tabella hello:

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define hello columns within hello table
    table.columns = {
        "text": "string",
        "complete": "boolean"
    };

    // Turn off dynamic schema
    table.dynamicSchema = false;

    // Turn on Soft Delete
    table.softDelete = true;

    // Require authentication tooaccess hello table
    table.access = 'authenticated';

    module.exports = table;

È necessario stabilire un meccanismo per l'eliminazione dei record, che sia da un'applicazione client, con un processo Web, tramite Funzioni di Azure o un'API personalizzata.

### <a name="howto-tables-seeding"></a>Procedura: Eseguire il seeding dei dati nel database
Quando si crea una nuova applicazione, è preferibile tooseed una tabella con dati.  Questa operazione può essere eseguita nel file di JavaScript definizione tabella hello come indicato di seguito:

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define hello columns within hello table
    table.columns = {
        "text": "string",
        "complete": "boolean"
    };
    table.seed = [
        { text: 'Example 1', complete: false },
        { text: 'Example 2', complete: true }
    ];

    // Turn off dynamic schema
    table.dynamicSchema = false;

    // Require authentication tooaccess hello table
    table.access = 'authenticated';

    module.exports = table;

Il seeding dei dati viene eseguito solo quando la tabella hello viene creata da hello App Mobile di Azure SDK.  Se la tabella hello esiste già nel database di hello, nessun dato viene inserito nella tabella hello.  Se lo schema dinamico è abilitato, lo schema viene dedotto dal dati hello seeding.

Si consiglia di chiamare in modo esplicito hello `tables.initialize()` tabella quando il servizio hello viene avviata l'esecuzione del metodo toocreate hello.

### <a name="Swagger"></a>Procedura: Abilitare il supporto di Swagger
Le app per dispositivi mobili del servizio app di Azure sono fornite con il supporto di [Swagger] incorporato.  tooenable supporto Swagger, installare innanzitutto swagger hello dell'interfaccia utente come dipendenza:

    npm install --save swagger-ui

Una volta installato, è possibile abilitare il supporto di Swagger nel costruttore di hello App mobili di Azure:

    var mobile = azureMobileApps({ swagger: true });

È probabilmente solo desidera tooenable Swagger supporto nelle edizioni di sviluppo.  È possibile farlo usando l'impostazione dell'app `NODE_ENV` :

    var mobile = azureMobileApps({ swagger: process.env.NODE_ENV !== 'production' });

Hello swagger endpoint si trova in http://*yoursite*.azurewebsites.net/swagger.  È possibile accedere hello Swagger dell'interfaccia utente tramite hello `/swagger/ui` endpoint.  Se si sceglie l'autenticazione toorequire dall'intera applicazione, Swagger genera un errore.  Per ottenere risultati ottimali, scegliere le richieste autenticate tooallow tramite in hello Azure l'autenticazione del servizio App / impostazioni di autorizzazione, quindi controllare l'autenticazione utilizzando hello `table.access` proprietà.

È inoltre possibile aggiungere hello Swagger opzione tooyour `azureMobile.js` file se si desidera solo Swagger supporto durante lo sviluppo in locale.

## <a name="a-namepushpush-notifications"></a><a name="push">Notifiche push
App per dispositivi mobili si integra con gli hub di notifica di Azure tooenable è toomillions di notifiche push toosend destinata dei dispositivi tra tutte le principali piattaforme. Tramite gli hub di notifica, è possibile inviare push tooiOS notifiche, i dispositivi Android e Windows. toolearn più sulle operazioni che è possibile eseguire con gli hub di notifica, vedere [Panoramica di hub di notifica](../notification-hubs/notification-hubs-push-notification-overview.md).

### </a><a name="send-push"></a>Procedura: Inviare notifiche push
Hello di codice seguente mostra i dispositivi iOS tooregistered notifica push toouse hello push oggetto toosend una trasmissione:

    // Create an APNS payload.
    var payload = '{"aps": {"alert": "This is an APNS payload."}}';

    // Only do hello push if configured
    if (context.push) {
        // Send a push notification using APNS.
        context.push.apns.send(null, payload, function (error) {
            if (error) {
                // Do something or log hello error.
            }
        });
    }

Per creare una registrazione di modello push client hello, è possibile inviare invece un toodevices di messaggio modello push su tutte le piattaforme supportate. Hello seguente codice mostra come toosend una notifica modello:

    // Define hello template payload.
    var payload = '{"messageParam": "This is a template payload."}';

    // Only do hello push if configured
    if (context.push) {
        // Send a template notification.
        context.push.send(null, payload, function (error) {
            if (error) {
                // Do something or log hello error.
            }
        });
    }


### <a name="push-user"></a>Procedura: tooan di notifiche push trasmissione autenticato l'utente con il tag
Quando un utente autenticato registrati per le notifiche push, un tag di ID utente viene aggiunto automaticamente toohello registrazione. Tramite questo tag, è possibile inviare push dispositivi tooall notifiche registrati da un utente specifico. Hello codice seguente ottiene hello SID dell'utente che effettua la richiesta hello e invia una registrazione di modello push notifica tooevery dispositivo per tale utente:

    // Only do hello push if configured
    if (context.push) {
        // Send a notification toohello current user.
        context.push.send(context.user.id, payload, function (error) {
            if (error) {
                // Do something or log hello error.
            }
        });
    }

Durante la registrazione per le notifiche push da un client autenticato, assicurarsi che l'autenticazione sia stata completata prima di tentare la registrazione.

## <a name="CustomAPI"></a> API personalizzate
### <a name="howto-customapi-basic"></a>Procedura: Definire un'API personalizzata
Inoltre toohello di accesso ai dati API tramite l'endpoint /tables hello, App mobili di Azure può fornire una copertura di API personalizzata.  Le API personalizzate sono definite in un simile definizioni di tabella toohello modo e possono accedere a tutti hello stessa funzionalità, tra cui l'autenticazione.

Se si desidera toouse l'autenticazione del servizio App con un'API personalizzata, è necessario configurare l'autenticazione del servizio App in hello [portale di Azure] prima.  Per ulteriori informazioni sulla configurazione dell'autenticazione in un servizio App di Azure, esaminare hello Guida alla configurazione per il provider di identità hello intendi toouse:

* [Modalità autenticazione di Azure Active Directory tooconfigure]
* [Come tooconfigure l'autenticazione di Facebook]
* [Come tooconfigure l'autenticazione di Google]
* [Come tooconfigure Microsoft Authentication]
* [Come tooconfigure autenticazione Twitter]

Le API personalizzate vengono definite in gran parte hello come hello tabelle API.

1. Creare una directory **api** .
2. Creare un file JavaScript definizione dell'API in hello **api** directory.
3. Utilizzare prova importazione metodo tooimport prova **api** directory.

Ecco di definizione dell'api prototipo hello in base a esempio di app basic hello che è utilizzate in precedenza.

    var express = require('express'),
        azureMobileApps = require('azure-mobile-apps');

    var app = express(),
        mobile = azureMobileApps();

    // Import hello Custom API
    mobile.api.import('./api');

    // Add hello mobile API so it is accessible as a Web API
    app.use(mobile);

    // Start listening on HTTP
    app.listen(process.env.PORT || 3000);

Esaminiamo un esempio di API che restituisce Data server hello utilizzando hello *Date.now()* metodo.  Di seguito è riportato il file di api/date.js hello:

    var api = {
        get: function (req, res, next) {
            var date = { currentTime: Date.now() };
            res.status(200).type('application/json').send(date);
        });
    };

    module.exports = api;

Ogni parametro è uno dei hello RESTful verbi standard - GET, POST, PATCH o DELETE.  metodo Hello è uno standard [ExpressJS Middleware] funzione che invia l'output di hello necessario.

### <a name="howto-customapi-auth"></a>Procedura: richiedere l'autenticazione per l'API di accesso tooa personalizzata
Implementa l'autenticazione in hello Azure Mobile App SDK allo stesso modo per endpoint di hello tabelle e le API personalizzate.  Per aggiungere l'autenticazione toohello API sviluppato nella sezione precedente di hello, aggiungere un **accesso** proprietà:

    var api = {
        get: function (req, res, next) {
            var date = { currentTime: Date.now() };
            res.status(200).type('application/json').send(date);
        });
    };
    // All methods must be authenticated.
    api.access = 'authenticated';

    module.exports = api;

È anche possibile specificare l'autenticazione su operazioni specifiche:

    var api = {
        get: function (req, res, next) {
            var date = { currentTime: Date.now() };
            res.status(200).type('application/json').send(date);
        }
    };
    // hello GET methods must be authenticated.
    api.get.access = 'authenticated';

    module.exports = api;

Hello stesso token utilizzato per l'endpoint di tabelle hello deve essere usato per le API personalizzate che richiede l'autenticazione.

### <a name="howto-customapi-auth"></a>Procedura: Gestire il caricamento di file di grandi dimensioni
Azure Mobile App SDK Usa hello [corpo parser middleware](https://github.com/expressjs/body-parser) tooaccept e decodificare il contenuto del corpo nell'elemento inviato.  È possibile preconfigurare caricamenti di file più grandi di corpo parser tooaccept:

    var express = require('express'),
        bodyParser = require('body-parser'),
        azureMobileApps = require('azure-mobile-apps');

    var app = express(),
        mobile = azureMobileApps();

    // Set up large body content handling
    app.use(bodyParser.json({ limit: '50mb' }));
    app.use(bodyParser.urlencoded({ limit: '50mb', extended: true }));

    // Import hello Custom API
    mobile.api.import('./api');

    // Add hello mobile API so it is accessible as a Web API
    app.use(mobile);

    // Start listening on HTTP
    app.listen(process.env.PORT || 3000);

file Hello è codificati prima della trasmissione in base 64.  Ciò aumenta la dimensione di hello del caricamento effettivo hello e pertanto hello dimensioni, che è necessario tener conto.

### <a name="howto-customapi-sql"></a>Procedura: Eseguire istruzioni SQL personalizzate
Hello App Mobile di Azure SDK consente l'accesso toohello intero contesto tramite l'oggetto richiesta hello, consentendo tooexecute i provider di dati definito toohello istruzioni SQL con parametri facilmente:

    var api = {
        get: function (request, response, next) {
            // Check for parameters - if not there, pass on tooa later API call
            if (typeof request.params.completed === 'undefined')
                return next();

            // Define hello query - anything that can be handled by hello mssql
            // driver is allowed.
            var query = {
                sql: 'UPDATE TodoItem SET complete=@completed',
                parameters: [{
                    completed: request.params.completed
                }]
            };

            // Execute hello query.  hello context for Azure Mobile Apps is available through
            // request.azureMobile - hello data object contains hello configured data provider.
            request.azureMobile.data.execute(query)
            .then(function (results) {
                response.json(results);
            });
        }
    };

    api.get.access = 'authenticated';
    module.exports = api;

## <a name="Debugging"></a>Debug, tabelle semplici e API semplici
### <a name="howto-diagnostic-logs"></a>Procedura: Eseguire il debug e diagnosticare e risolvere i problemi di App per dispositivi mobili di Azure
Hello Azure App Service fornisce diverse debug e risoluzione dei problemi di tecniche per applicazioni Node.js.
Fare riferimento toohello tooget articoli avviato nel back-end Node.js Mobile di risoluzione dei problemi seguenti:

* [Monitoraggio di un servizio app di Azure]
* [Abilitazione della registrazione diagnostica nel servizio app di Azure]
* [Risoluzione dei problemi di un Servizio app di Azure in Visual Studio]

Le applicazioni Node.js hanno accesso tooa ampia gamma di strumenti di log di diagnostica.  Internamente, hello Azure Mobile App Node.js SDK Usa [Winston] per la registrazione diagnostica.  La registrazione è abilitata automaticamente attivare la modalità di debug o dall'impostazione hello **MS_DebugMode** tootrue impostazione app in hello [portale di Azure]. Log generati vengono visualizzati nel log di diagnostica di hello in hello [portale di Azure].

### <a name="in-portal-editing"></a><a name="work-easy-tables"></a>Procedura: utilizzare tabelle semplice in hello portale di Azure
Tabelle di facile nel portale di hello consentono di creare e utilizzare direttamente le tabelle nel portale di hello. È anche possibile modificare le operazioni di tabella utilizzando l'Editor di servizio App hello.

Quando si fa clic su **Tabelle semplici** nelle impostazioni del sito di back-end, è possibile aggiungere, modificare o eliminare una tabella. È inoltre possibile visualizzare dati nella tabella hello.

![Utilizzare Easy Tables](./media/app-service-mobile-node-backend-how-to-use-server-sdk/mobile-apps-easy-tables.png)

Hello comandi riportati di seguito sono disponibili sulla barra dei comandi di hello per una tabella:

* **Modificare le autorizzazioni** : hello l'autorizzazione per la lettura di modifica, inserire, aggiornare ed eliminare operazioni sulla tabella hello.
  Le opzioni sono tooallow l'accesso anonimo, l'autenticazione toorequire o toodisable tutte toohello operazione di accesso.
* **Modificare lo script** -hello script per tabella hello viene aperto nell'Editor di servizio App hello.
* **Gestire schema** : aggiungere o eliminare le colonne o modificare l'indice di tabella hello.
* **Cancella tabella** -tronca una tabella esistente, eliminare tutte le righe di dati ma lasciando schema hello invariata.
* **Elimina righe** : è possibile eliminare singole righe di dati.
* **Visualizza i log di streaming** -consente di connettersi toohello streaming il servizio di registrazione per il sito.

### <a name="work-easy-apis"></a>Procedura: utilizzare le API semplice in hello portale di Azure
API semplice nel portale di hello consentono di creare e utilizzare con diritto di API personalizzata nel portale di hello. È possibile modificare gli script di API utilizzando l'Editor di servizio App hello.

Quando si fa clic su **API semplici** nelle impostazioni del sito di back-end, è possibile aggiungere, modificare o eliminare un endpoint API personalizzato.

![Utilizzare Easy APIs](./media/app-service-mobile-node-backend-how-to-use-server-sdk/mobile-apps-easy-apis.png)

Nel portale di hello, si può modificare le autorizzazioni di accesso hello per una determinata azione HTTP, file di script nell'Editor di servizio App di hello API, visualizzare o modificare i log di streaming hello.

### <a name="online-editor"></a>Procedura: modificare il codice nell'Editor di servizio App hello
Hello portale di Azure consente di modificare i file di script di back-end di Node. js in hello Editor di servizio App senza dover scaricare computer locale di hello progetto tooyour. file di script tooedit nell'editor online hello:

1. Nel pannello del back-end dell'app per dispositivi mobili fare clic su **Tutte le impostazioni** > **Easy tables** o **Easy APIs**, fare clic su una tabella o un'API e quindi su **Modifica script**. file di script Hello viene aperto in hello Editor di servizio App.

    ![Editor del servizio app](./media/app-service-mobile-node-backend-how-to-use-server-sdk/mobile-apps-visual-studio-editor.png)
2. Verificare il file del codice toohello le modifiche apportate nell'editor online hello. Le modifiche vengono salvate automaticamente durante la digitazione.

<!-- Images -->
[0]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/npm-init.png
[1]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/vs2015-new-project.png
[2]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/vs2015-install-npm.png
[3]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/sqlexpress-config.png
[4]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/sqlexpress-authconfig.png
[5]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/sqlexpress-newuser-1.png
[6]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/dotnet-backend-create-db.png

<!-- URLs -->
[Avvio rapido di client Android]: app-service-mobile-android-get-started.md
[Avvio rapido di client Apache Cordova]: app-service-mobile-cordova-get-started.md
[Avvio rapido di client iOS]: app-service-mobile-ios-get-started.md
[Avvio rapido di client Xamarin.iOS]: app-service-mobile-xamarin-ios-get-started.md
[Avvio rapido di client Xamarin.Android]: app-service-mobile-xamarin-android-get-started.md
[Avvio rapido di client Xamarin.Forms]: app-service-mobile-xamarin-forms-get-started.md
[Avvio rapido di client Windows Store]: app-service-mobile-windows-store-dotnet-get-started.md
[HTML/Javascript Client QuickStart]: app-service-html-get-started.md
[sincronizzazione dati offline]: app-service-mobile-offline-data-sync.md
[Modalità autenticazione di Azure Active Directory tooconfigure]: app-service-mobile-how-to-configure-active-directory-authentication.md
[Come tooconfigure l'autenticazione di Facebook]: app-service-mobile-how-to-configure-facebook-authentication.md
[Come tooconfigure l'autenticazione di Google]: app-service-mobile-how-to-configure-google-authentication.md
[Come tooconfigure Microsoft Authentication]: app-service-mobile-how-to-configure-microsoft-authentication.md
[Come tooconfigure autenticazione Twitter]: app-service-mobile-how-to-configure-twitter-authentication.md
[Guida alla distribuzione del servizio app di Azure]: ../app-service-web/web-sites-deploy.md
[Monitoraggio di un servizio app di Azure]: ../app-service-web/web-sites-monitor.md
[Abilitazione della registrazione diagnostica nel servizio app di Azure]: ../app-service-web/web-sites-enable-diagnostic-log.md
[Risoluzione dei problemi di un Servizio app di Azure in Visual Studio]: ../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md
[specificare hello nodo versione]: ../nodejs-specify-node-version-azure-apps.md
[utilizzare i moduli del nodo]: ../nodejs-use-node-modules-azure-apps.md
[Create a new Azure App Service]: ../app-service-web/
[azure-mobile-apps]: https://www.npmjs.com/package/azure-mobile-apps
[Express]: http://expressjs.com/
[Swagger]: http://swagger.io/

[portale di Azure]: https://portal.azure.com/
[OData]: http://www.odata.org
[promessa]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise
[esempio basicapp in GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/basic-app
[esempio todo in GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/todo
[directory esempi su GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples
[static-schema sample on GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/static-schema
[QueryJS]: https://github.com/Azure/queryjs
[Node.js Tools 1.1 per Visual Studio]: https://github.com/Microsoft/nodejstools/releases/tag/v1.1-RC.2.1
[pacchetto Node.js mssql]: https://www.npmjs.com/package/mssql
[Microsoft SQL Server 2014 Express]: http://www.microsoft.com/en-us/server-cloud/Products/sql-server-editions/sql-server-express.aspx
[ExpressJS Middleware]: http://expressjs.com/guide/using-middleware.html
[Winston]: https://github.com/winstonjs/winston
