---
title: app web aaaNode.js utilizzando hello del servizio tabelle di Azure
description: "Questa esercitazione viene illustrato come toouse hello Azure Table service toostore dati da un'applicazione Node.js che è ospitato in App Web di servizio App di Azure."
tags: azure-portal
services: app-service\web, storage
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: 029e6f46-f586-4309-adbf-71c7b8d537d4
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2016
ms.author: tarcher
ms.openlocfilehash: f6e08335b4c7f62f7b3994287edd586860cb7135
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="nodejs-web-app-using-hello-azure-table-service"></a>App web Node. js utilizzando hello del servizio tabelle di Azure
## <a name="overview"></a>Panoramica
Questa esercitazione viene illustrato come servizio tabelle toouse forniti da Gestione dati di Azure toostore e accedere ai dati da un [nodo] applicazione ospitata in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) App Web. In questa esercitazione si presuppone che l'utente abbia già utilizzato l'applicazione Node e [Git].

Si acquisiranno le nozioni seguenti:

* Come toouse npm (gestione di pacchetti di nodi) tooinstall hello i moduli del nodo
* Come toowork con hello servizio tabelle di Azure
* Come un'app web toouse hello toocreate CLI di Azure.

In questa esercitazione verrà creata una semplice applicazione di "elenco attività" basata su Web che consente di creare, recuperare e completare le attività. attività Hello vengono archiviate nel servizio tabelle hello.

Di seguito è riportata un'applicazione hello completata:

![Pagina Web con un elenco di attività vuoto][node-table-finished]

> [!NOTE]
> Se si desidera tooget avviato con il servizio App di Azure prima di effettuare l'iscrizione per un account Azure, andare troppo[tenta di servizio App](https://azure.microsoft.com/try/app-service/), in cui è possibile creare subito un'app web di breve durata starter nel servizio App. Non è necessario fornire una carta di credito né impegnarsi in alcun modo.
> 
> 

## <a name="prerequisites"></a>Prerequisiti
Prima di seguire le istruzioni di hello in questo articolo, assicurarsi di aver installato quanto segue hello:

* [nodo] 0.10.24 o versione successiva
* [Git]

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

## <a name="create-a-storage-account"></a>Creare un account di archiviazione
Creare un account di archiviazione di Azure app Hello utilizzerà questa attività da svolgere hello toostore di account.

1. Accedere al hello [portale Azure](https://portal.azure.com/).
2. Fare clic su hello **New** sull'icona nella parte inferiore di hello sinistra del portale hello, quindi fare clic su **dati e archiviazione** > **archiviazione**. Assegnare un nome univoco di account di archiviazione hello e creare un nuovo [gruppo di risorse](../azure-resource-manager/resource-group-overview.md) relativo.
   
      ![Pulsante Nuovo](./media/storage-nodejs-use-table-storage-web-site/configure-storage.png)
   
    Quando è stato creato l'account di archiviazione hello, hello **notifiche** pulsante farà lampeggiare una verde **esito positivo** ed è aperto il pannello dell'account di archiviazione hello gruppo tooshow appartiene toohello nuova risorsa creato.
3. Nel pannello hello account di archiviazione, fare clic su **impostazioni** > **chiavi**. Copiare negli Appunti toohello chiave di accesso primaria hello.
   
    ![Chiave di accesso][portal-storage-access-keys]

## <a name="install-modules-and-generate-scaffolding"></a>Installazione dei moduli e generazione dello scaffolding
In questa sezione verrà di creare una nuova applicazione di nodo e utilizzare i pacchetti di npm tooadd modulo. Per questa applicazione si utilizzerà hello [Express] e [Azure] moduli. modulo Express Hello fornisce un framework di Model View Controller per nodo, mentre hello moduli di Azure fornisce servizio di integrazione applicativa toohello tabella.

### <a name="install-express-and-generate-scaffolding"></a>Installare Express e generare lo scaffolding
1. Dalla riga di comando hello, creare una nuova directory denominata **tasklist** e commutatore toothat directory.  
2. Immettere hello seguente tooinstall hello Express il modulo.
   
        npm install express-generator@4.2.0 -g
   
    A seconda del sistema operativo hello, potrebbe essere necessario tooput 'sudo' prima del comando hello:
   
        sudo npm install express-generator@4.2.0 -g
   
    output di Hello visualizzato è simile toohello esempio seguente:
   
        express-generator@4.2.0 /usr/local/lib/node_modules/express-generator
        ├── mkdirp@0.3.5
        └── commander@1.3.2 (keypress@0.1.0)
   
   > [!NOTE]
   > Hello '-g' parametro Installa modulo hello a livello globale. In questo modo, è possibile utilizzare **express** lo scaffolding di app web toogenerate senza tootype in informazioni aggiuntive sul percorso.
   > 
   > 
3. lo scaffolding di hello toocreate per un'applicazione hello, immettere hello **express** comando:
   
        express
   
    output di Hello di questo comando viene visualizzato toohello simile esempio seguente:
   
           create : .
           create : ./package.json
           create : ./app.js
           create : ./public
           create : ./public/images
           create : ./routes
           create : ./routes/index.js
           create : ./routes/users.js
           create : ./public/stylesheets
           create : ./public/stylesheets/style.css
           create : ./views
           create : ./views/index.jade
           create : ./views/layout.jade
           create : ./views/error.jade
           create : ./public/javascripts
           create : ./bin
           create : ./bin/www
   
           install dependencies:
             $ cd . && npm install
   
           run hello app:
             $ DEBUG=my-application ./bin/www
   
    Sono disponibili diverse nuove directory e file hello **tasklist** directory.

### <a name="install-additional-modules"></a>Installare moduli aggiuntivi
Uno dei hello file che **express** crea è **package. JSON**. Questo file contiene un elenco di dipendenze del modulo. In un secondo momento, quando si distribuisce tooApp applicazione hello App Web del servizio, questo file determina i moduli necessari toobe installato in Azure.

Hello della riga di comando, digitare hello seguenti moduli di hello tooinstall comando descritti in hello **package. JSON** file. Potrebbe essere necessario toouse 'sudo'.

    npm install

output di Hello di questo comando viene visualizzato toohello simile esempio seguente:

    debug@0.7.4 node_modules\debug

    cookie-parser@1.0.1 node_modules\cookie-parser
    ├── cookie-signature@1.0.3
    └── cookie@0.1.0

    [...]


Quindi, immettere hello successivo comando tooinstall hello [azure], [nodo uuid], [nconf] e [async] moduli:

    npm install azure-storage node-uuid async nconf --save

Hello **-Salva** flag aggiunge voci per toohello questi moduli **package. JSON** file.

output di Hello di questo comando viene visualizzato toohello simile esempio seguente:

    async@0.9.0 node_modules\async

    node-uuid@1.4.1 node_modules\node-uuid

    nconf@0.6.9 node_modules\nconf
    ├── ini@1.2.1
    ├── async@0.2.9
    └── optimist@0.6.0 (wordwrap@0.0.2, minimist@0.0.10)

    [...]


## <a name="create-hello-application"></a>Creare un'applicazione hello
Si è un'applicazione hello toobuild pronto.

### <a name="create-a-model"></a>Creare il modello
Oggetto *modello* è un oggetto che rappresenta i dati di hello nell'applicazione. Per un'applicazione hello, modello solo hello è un oggetto attività, che rappresenta un elemento nell'elenco attività hello. Attività saranno necessario hello seguenti campi:

* PartitionKey
* RowKey
* name (string)
* category (string)
* completed (Boolean)

**PartitionKey** e **RowKey** vengono utilizzati dal servizio tabelle hello come chiavi della tabella. Per ulteriori informazioni, vedere [modello di dati del servizio tabelle hello comprensione](https://msdn.microsoft.com/library/azure/dd179338.aspx).

1. In hello **tasklist** directory, creare una nuova directory denominata **modelli**.
2. In hello **modelli** directory, creare un nuovo file denominato **task.js**. Questo file contiene il modello di hello per le operazioni di hello create dall'applicazione.
3. All'inizio di hello di hello **task.js** file, aggiungere hello tooreference richiesto dalle librerie di codice seguente:
   
        var azure = require('azure-storage');
          var uuid = require('node-uuid');
        var entityGen = azure.TableUtilities.entityGenerator;
4. Aggiungere seguente hello toodefine del codice e di esportare l'oggetto attività hello. Questo oggetto è responsabile per la connessione toohello tabella.
   
          module.exports = Task;
   
        function Task(storageClient, tableName, partitionKey) {
          this.storageClient = storageClient;
          this.tableName = tableName;
          this.partitionKey = partitionKey;
          this.storageClient.createTableIfNotExists(tableName, function tableCreated(error) {
            if(error) {
              throw error;
            }
          });
        };
5. Aggiungere hello seguito metodi aggiuntivi di codice toodefine nell'oggetto attività hello, che consentono le interazioni con i dati archiviati nella tabella hello:
   
        Task.prototype = {
          find: function(query, callback) {
            self = this;
            self.storageClient.queryEntities(this.tableName, query, null, function entitiesQueried(error, result) {
              if(error) {
                callback(error);
              } else {
                callback(null, result.entries);
              }
            });
          },
   
          addItem: function(item, callback) {
            self = this;
            // use entityGenerator tooset types
            // NOTE: RowKey must be a string type, even though
            // it contains a GUID in this example.
            var itemDescriptor = {
              PartitionKey: entityGen.String(self.partitionKey),
              RowKey: entityGen.String(uuid()),
              name: entityGen.String(item.name),
              category: entityGen.String(item.category),
              completed: entityGen.Boolean(false)
            };
            self.storageClient.insertEntity(self.tableName, itemDescriptor, function entityInserted(error) {
              if(error){  
                callback(error);
              }
              callback(null);
            });
          },
   
          updateItem: function(rKey, callback) {
            self = this;
            self.storageClient.retrieveEntity(self.tableName, self.partitionKey, rKey, function entityQueried(error, entity) {
              if(error) {
                callback(error);
              }
              entity.completed._ = true;
              self.storageClient.updateEntity(self.tableName, entity, function entityUpdated(error) {
                if(error) {
                  callback(error);
                }
                callback(null);
              });
            });
          }
        }
6. Salvare e chiudere hello **task.js** file.

### <a name="create-a-controller"></a>Creare un controller
Oggetto *controller* gestisce le richieste HTTP ed esegue il rendering di risposta hello HTML.

1. In hello **tasklist/route** directory, creare un nuovo file denominato **tasklist.js** e aprirlo in un editor di testo.
2. Aggiungere hello seguente codice troppo**tasklist.js**. Viene caricato hello async moduli di azure e, che vengono usati da **tasklist.js**. Definisce inoltre hello **TaskList** funzione, che viene passata un'istanza di hello **attività** dell'oggetto definita in precedenza:
   
        var azure = require('azure-storage');
        var async = require('async');
   
        module.exports = TaskList;
3. Definire un oggetto **TaskList** .
   
        function TaskList(task) {
          this.task = task;
        }
4. Aggiungere i seguenti metodi troppo hello**TaskList**:
   
        TaskList.prototype = {
          showTasks: function(req, res) {
            self = this;
            var query = new azure.TableQuery()
              .where('completed eq ?', false);
            self.task.find(query, function itemsFound(error, items) {
              res.render('index',{title: 'My ToDo List ', tasks: items});
            });
          },
   
          addTask: function(req,res) {
            var self = this;
            var item = req.body.item;
            self.task.addItem(item, function itemAdded(error) {
              if(error) {
                throw error;
              }
              res.redirect('/');
            });
          },
   
          completeTask: function(req,res) {
            var self = this;
            var completedTasks = Object.keys(req.body);
            async.forEach(completedTasks, function taskIterator(completedTask, callback) {
              self.task.updateItem(completedTask, function itemsUpdated(error) {
                if(error){
                  callback(error);
                } else {
                  callback(null);
                }
              });
            }, function goHome(error){
              if(error) {
                throw error;
              } else {
               res.redirect('/');
              }
            });
          }
        }

### <a name="modify-appjs"></a>Modificare il file app.js
1. Da hello **tasklist** hello directory, aprire **app.js** file. Questo file è stato creato in precedenza eseguendo hello **express** comando.
2. Inizio hello del file hello, aggiungere hello seguente modulo hello azure tooload, nome della tabella hello set, chiave di partizione e le credenziali di archiviazione hello set utilizzate in questo esempio:
   
        var azure = require('azure-storage');
        var nconf = require('nconf');
        nconf.env()
             .file({ file: 'config.json', search: true });
        var tableName = nconf.get("TABLE_NAME");
        var partitionKey = nconf.get("PARTITION_KEY");
        var accountName = nconf.get("STORAGE_NAME");
        var accountKey = nconf.get("STORAGE_KEY");
   
   > [!NOTE]
   > nconf caricherà i valori di configurazione hello da variabili di ambiente o hello **config. JSON** file, verrà creata in un secondo momento.
   > 
   > 
3. Nel file app.js hello, scorrere verso il basso toowhere vedrai hello la seguente riga:
   
        app.use('/', routes);
        app.use('/users', users);
   
    Sostituire hello sopra righe con codice hello riportato di seguito. Inizializza un'istanza di <strong>attività</strong> con un account di archiviazione tooyour di connessione. Questo argomento viene passato toohello <strong>TaskList</strong>, che verrà utilizzato toocommunicate con hello del servizio tabelle:
   
        var TaskList = require('./routes/tasklist');
        var Task = require('./models/task');
        var task = new Task(azure.createTableService(accountName, accountKey), tableName, partitionKey);
        var taskList = new TaskList(task);
   
        app.get('/', taskList.showTasks.bind(taskList));
        app.post('/addtask', taskList.addTask.bind(taskList));
        app.post('/completetask', taskList.completeTask.bind(taskList));
4. Salvare hello **app.js** file.

### <a name="modify-hello-index-view"></a>Modifica visualizzazione dell'indice hello
1. Aprire hello **tasklist/views/index.jade** file in un editor di testo.
2. Sostituire hello l'intero contenuto del file hello con hello seguente codice. Ciò consente di definire una visualizzazione delle attività esistenti e includere un modulo per aggiungere nuove attività e contrassegnare quelle esistenti come completate.
   
        extends layout
   
        block content
          h1= title
          br
   
          form(action="/completetask", method="post")
            table.table.table-striped.table-bordered
              tr
                td Name
                td Category
                td Date
                td Complete
              if (typeof tasks === "undefined")
                tr
                  td
              else
                each task in tasks
                  tr
                    td #{task.name._}
                    td #{task.category._}
                    - var day   = task.Timestamp._.getDate();
                    - var month = task.Timestamp._.getMonth() + 1;
                    - var year  = task.Timestamp._.getFullYear();
                    td #{month + "/" + day + "/" + year}
                    td
                      input(type="checkbox", name="#{task.RowKey._}", value="#{!task.completed._}", checked=task.completed._)
            button.btn(type="submit") Update tasks
          hr
          form.well(action="/addtask", method="post")
            label Item Name:
            input(name="item[name]", type="textbox")
            label Item Category:
            input(name="item[category]", type="textbox")
            br
            button.btn(type="submit") Add item
3. Salvare e chiudere il file **index.jade** .

### <a name="modify-hello-global-layout"></a>Modifica layout globale hello
Hello **layout.jade** file hello **viste** directory è un modello generale per altri **.jade** file. In questo passaggio è necessario modificarlo toouse [Twitter Bootstrap](https://github.com/twbs/bootstrap), che è un toolkit che rende facile toodesign un'app web di aspetto interessante.

Scaricare ed estrarre file hello per [Twitter Bootstrap](http://getbootstrap.com/). Hello copia **bootstrap.min.css** file hello Bootstrap **css** hello nella cartella **pubblico/fogli di stile** directory dell'applicazione.

Da hello **viste** cartella, aprire **layout.jade** e sostituire tutto il contenuto di hello con hello seguente:

    doctype html
    html
      head
        title= title
        link(rel='stylesheet', href='/stylesheets/bootstrap.min.css')
        link(rel='stylesheet', href='/stylesheets/style.css')
      body.app
        nav.navbar.navbar-default
          div.navbar-header
          a.navbar-brand(href='/') My Tasks
        block content

### <a name="create-a-config-file"></a>Creare un file config
toorun hello app localmente, si saranno inserire le credenziali di archiviazione di Azure in un file di configurazione. Creare un file denominato **config. JSON* * con hello JSON seguente:

    {
        "STORAGE_NAME": "<storage account name>",
        "STORAGE_KEY": "<storage access key>",
        "PARTITION_KEY": "mytasks",
        "TABLE_NAME": "tasks"
    }

Sostituire **nome account di archiviazione** con nome hello dell'archiviazione hello account creato in precedenza e sostituire **chiave di accesso di archiviazione** con la chiave di accesso primaria hello dell'account di archiviazione. ad esempio:

    {
        "STORAGE_NAME": "nodejsappstorage",
        "STORAGE_KEY": "KG0oDd..."
        "PARTITION_KEY": "mytasks",
        "TABLE_NAME": "tasks"
    }

Salvare il file *livello di una directory superiore* di hello **tasklist** directory, simile al seguente:

    parent/
      |-- config.json
      |-- tasklist/

motivo di Hello per eseguire questa operazione è tooavoid controllare il file di configurazione hello nel controllo del codice sorgente, in cui potrebbe non pubblico. Quando si distribuisce hello app tooAzure, si utilizzerà le variabili di ambiente invece di un file di configurazione.

## <a name="run-hello-application-locally"></a>Eseguire un'applicazione hello in locale
un'applicazione hello tootest sul computer locale, eseguire hello alla procedura seguente:

1. Hello della riga di comando, modificare le directory toohello **tasklist** directory.
2. Utilizzare hello successivo comando toolaunch un'applicazione hello in locale:
   
        npm start
3. Aprire un web browser e passare toohttp://127.0.0.1:3000.
   
    Viene visualizzato un toohello simile a pagina web seguente esempio.
   
    ![Pagina Web con un elenco di attività vuoto][node-table-finished]
4. toocreate un nuovo elemento di attività, immettere un nome e una categoria e fare clic su **Aggiungi elemento**. 
5. un'attività come il controllo completo, toomark **completa** e fare clic su **Aggiorna attività**.
   
    ![Un'immagine di hello nuovo elemento hello elenco di attività][node-table-list-items]

Anche se un'applicazione hello è in esecuzione in locale, l'archiviazione dati hello in hello del servizio tabelle di Azure.

## <a name="deploy-your-application-tooazure"></a>Distribuire l'applicazione tooAzure
passaggi Hello in questa sezione utilizzano gli strumenti da riga di comando di Azure di hello toocreate una nuova app web nel servizio App e quindi usare Git toodeploy l'applicazione. tooperform questi passaggi, è necessario disporre di una sottoscrizione di Azure.

> [!NOTE]
> Questi passaggi possono essere eseguiti anche utilizzando hello [portale Azure](https://portal.azure.com/). Vedere [Creazione e distribuzione di un'app Web Node.js nel Azure App Service].
> 
> Se si tratta di hello prima app web che è stato creato, è necessario utilizzare hello Azure Portal toodeploy questa applicazione.
> 
> 

tooget avviato, installare hello [CLI di Azure] immettendo hello comando seguente dalla riga di comando hello:

    npm install azure-cli -g

### <a name="import-publishing-settings"></a>Importare le impostazioni di pubblicazione
In questo passaggio verrà scaricato un file contenente informazioni sulla sottoscrizione.

1. Immettere hello comando seguente:
   
        azure login
   
    Questo comando viene avviato un browser e si sposta toohello pagina di download. Se richiesto, accedere con l'account hello associati alla sottoscrizione di Azure.
   
    <!-- ![hello download page][download-publishing-settings] -->
   
    download del file Hello inizia automaticamente. in caso contrario, è possibile fare clic su collegamento hello all'inizio di hello hello toomanually download hello del file della pagina. Salvare hello file e Nota hello percorso del file.
2. Immettere hello impostazioni hello tooimport del comando seguente:
   
        azure account import <path-to-file>
   
    Specificare hello percorso e il nome della pubblicazione di file di impostazioni che è stato scaricato nel passaggio precedente hello hello.
3. Dopo l'importano delle impostazioni di hello, hello di eliminare i file di impostazioni di pubblicazione. Non è più necessario e contiene informazioni riservate relative alla sottoscrizione di Azure.

### <a name="create-an-app-service-web-app"></a>Creare un piano di servizio app
1. Hello della riga di comando, modificare le directory toohello **tasklist** directory.
2. Utilizzare hello successivo comando toocreate una nuova app web.
   
        azure site create --git
   
    Verrà richiesto per la posizione e nome dell'applicazione web hello. Fornire un nome univoco e selezionare hello stessa località geografica dell'account di archiviazione di Azure.
   
    Hello `--git` parametro crea un repository Git in Azure per questa app web. Inizializza un repository Git nella directory corrente hello anche se non esiste e aggiunge un [Git remoto] denominato 'azure', che è usato toopublish hello applicazione tooAzure. Infine, viene creato un **Web. config** file che contiene le impostazioni utilizzate dalle applicazioni di Azure toohost nodo. Se si omette hello `--git` parametro ma hello directory contiene un repository Git, comando hello verrà comunque creati remoto hello 'azure'.
   
    Al termine di questo comando, verrà visualizzato il seguente toohello simili di output. Si noti che hello riga che inizia con **sito Web creato in** contiene hello URL per l'app web hello.
   
        info:   Executing command site create
        help:   Need a site name
        Name: TableTasklist
        info:   Using location southcentraluswebspace
        info:   Executing `git init`
        info:   Creating default .gitignore file
        info:   Creating a new web site
        info:   Created web site at  tabletasklist.azurewebsites.net
        info:   Initializing repository
        info:   Repository initialized
        info:   Executing `git remote add azure https://username@tabletasklist.azurewebsites.net/TableTasklist.git`
        info:   site create command OK
   
   > [!NOTE]
   > Se si tratta di hello prima applicazione del servizio web app per la sottoscrizione, sarà toouse istruzioni riportate hello Azure Portal toocreate hello web app. Per ulteriori informazioni, vedere [Creazione e distribuzione di un'app Web Node.js nel Azure App Service].
   > 
   > 

### <a name="set-environment-variables"></a>Impostare le variabili di ambiente
In questo passaggio si aggiungeranno configurazione dell'ambiente variabili tooyour web app in Azure.
Dalla riga di comando hello, immettere il seguente hello:

    azure site appsetting add
        STORAGE_NAME=<storage account name>;STORAGE_KEY=<storage access key>;PARTITION_KEY=mytasks;TABLE_NAME=tasks


Sostituire  **<storage account name>**  con nome hello dell'archiviazione hello account creato in precedenza e sostituire  **<storage access key>**  con la chiave di accesso primaria hello dell'account di archiviazione. (Utilizzare hello stesso valori come file config. JSON hello creato in precedenza).

In alternativa, è possibile impostare le variabili di ambiente in hello [portale Azure](https://portal.azure.com/):

1. Aprire il pannello dell'app web hello facendo **Sfoglia** > **App Web** > nome dell'app web.
2. Nel pannello dell'app Web fare clic su **Tutte le impostazioni** > **Impostazioni dell'applicazione**.
   
     <!-- ![Top Menu](./media/storage-nodejs-use-table-storage-web-site/PollsCommonWebSiteTopMenu.png) -->
3. Scorrere verso il basso toohello **impostazioni App** sezione e aggiungere coppie chiave/valore hello.
   
     ![Impostazioni app](./media/storage-nodejs-use-table-storage-web-site/storage-tasks-appsettings.png)
4. Fare clic su **SAVE**.

### <a name="publish-hello-application"></a>Pubblicare un'applicazione hello
app hello toopublish, eseguire il commit tooGit i file di codice hello e quindi push tooazure o master.

1. Impostare le credenziali di distribuzione
   
        azure site deployment user set <name> <password>
2. Aggiungere ed effettuare il commit dei file dell'applicazione.
   
        git add .
        git commit -m "adding files"
3. Push hello commit toohello App del servizio web app:
   
        git push azure master
   
    Utilizzare **master** come ramo di destinazione hello. Alla fine di hello della distribuzione di hello, viene visualizzato un toohello simile istruzione esempio seguente:
   
        toohttps://username@tabletasklist.azurewebsites.net/TableTasklist.git
          * [new branch]      master -> master
4. Una volta completata l'operazione di push hello, individuare l'URL dell'app web toohello restituito in precedenza da hello `azure create site` comando tooview l'applicazione.

## <a name="next-steps"></a>Passaggi successivi
Mentre hello in questo articolo viene descritta la utilizzando le informazioni di toostore di hello del servizio tabelle, è inoltre possibile utilizzare [MongoDB](https://mlab.com/azure/). 

## <a name="additional-resources"></a>Risorse aggiuntive
[CLI di Azure]

## <a name="whats-changed"></a>Modifiche apportate
* Per una Guida toohello modifica da siti Web tooApp servizio vedere: [relativo impatto sui servizi di Azure esistente e servizio App di Azure](http://go.microsoft.com/fwlink/?LinkId=529714)

<!-- URLs -->

[Creazione e distribuzione di un'app Web Node.js nel Azure App Service]: app-service-web-get-started-nodejs.md
[Azure Developer Center]: /develop/nodejs/

[nodo]: http://nodejs.org
[Git]: http://git-scm.com
[Express]: http://expressjs.com
[for free]: http://windowsazure.com
[Git remoto]: http://git-scm.com/docs/git-remote

[CLI di Azure]:../cli-install-nodejs.md

[azure]: https://github.com/Azure/azure-sdk-for-node
[nodo uuid]: https://www.npmjs.com/package/node-uuid
[nconf]: https://www.npmjs.com/package/nconf
[async]: https://www.npmjs.com/package/async

[Azure Portal]: https://portal.azure.com

[Create and deploy a Node.js application tooan Azure Web Site]: app-service-web-get-started-nodejs.md

<!-- Image References -->

[node-table-finished]: ./media/storage-nodejs-use-table-storage-web-site/table_todo_empty.png
[node-table-list-items]: ./media/storage-nodejs-use-table-storage-web-site/table_todo_list.png
[download-publishing-settings]: ./media/storage-nodejs-use-table-storage-web-site/azure-account-download-cli.png
[portal-storage-access-keys]: ./media/storage-nodejs-use-table-storage-web-site/manage-access-keys.png
[app-settings]: ./media/storage-nodejs-use-table-storage-web-site/storage-tasks-appsettings.png
