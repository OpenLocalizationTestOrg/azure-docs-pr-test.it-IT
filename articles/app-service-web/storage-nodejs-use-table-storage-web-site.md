---
title: App Web Node.js con il servizio tabelle di Azure
description: Questa esercitazione illustra come usare il servizio tabelle di Azure per archiviare i dati da un'applicazione Node.js ospitata in app Web del servizio app di Azure.
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
ms.openlocfilehash: 3252914934c1084a165fa39ee983d3039e04d567
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="nodejs-web-app-using-the-azure-table-service"></a>App Web Node.js con il servizio tabelle di Azure
## <a name="overview"></a>Panoramica
In questa esercitazione viene illustrato come usare il servizio tabelle fornito da Gestione dati di Azure per archiviare e accedere ai dati da un'applicazione [node] ospitata nel [servizio App di Azure](http://go.microsoft.com/fwlink/?LinkId=529714). In questa esercitazione si presuppone che l'utente abbia già utilizzato l'applicazione Node e [Git].

Si acquisiranno le nozioni seguenti:

* Usare npm (Node Package Manager) per installare i moduli di Node
* Utilizzare il servizio tabelle di Azure
* Come usare l'interfaccia della riga di comando di Azure per creare un'app Web.

In questa esercitazione verrà creata una semplice applicazione di "elenco attività" basata su Web che consente di creare, recuperare e completare le attività. Le attività vengono archiviate nel servizio tabelle.

Di seguito è riportata l'applicazione completata:

![Pagina Web con un elenco di attività vuoto][node-table-finished]

> [!NOTE]
> Per iniziare a usare Servizio app di Azure prima di registrarsi per ottenere un account Azure, andare a [Prova il servizio app](https://azure.microsoft.com/try/app-service/), dove è possibile creare un'app Web iniziale temporanea nel servizio app. Non è necessario fornire una carta di credito né impegnarsi in alcun modo.
> 
> 

## <a name="prerequisites"></a>Prerequisiti
Prima di seguire le istruzioni di questo articolo, verificare che siano installati i seguenti elementi:

* [node] 0.10.24 o versione successiva
* [Git]

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

## <a name="create-a-storage-account"></a>Creare un account di archiviazione
Creare un account di archiviazione di Azure L'app utilizzerà questo account per archiviare gli elementi dell'elenco attività.

1. Accedere al [Portale di Azure](https://portal.azure.com/).
2. Fare clic sull'icona **Nuovo** nella parte inferiore sinistra del portale, quindi fare clic su **Dati e archiviazione** > **Archiviazione**. Assegnare un nome univoco all'account di archiviazione e creare un nuovo [gruppo di risorse](../azure-resource-manager/resource-group-overview.md) correlato.
   
      ![Pulsante Nuovo](./media/storage-nodejs-use-table-storage-web-site/configure-storage.png)
   
    Quando l'account di archiviazione viene creato, nel pulsante **Notifiche** lampeggia in verde il testo **OPERAZIONE RIUSCITA** e il pannello dell'account di archiviazione si apre per visualizzare che appartiene al nuovo gruppo di risorse creato.
3. Nel pannello dell'account di archiviazione fare clic su **Impostazioni** > **Chiavi**. Copiare la chiave di accesso primaria negli Appunti.
   
    ![Chiave di accesso][portal-storage-access-keys]

## <a name="install-modules-and-generate-scaffolding"></a>Installazione dei moduli e generazione dello scaffolding
In questa sezione verrà creata una nuova applicazione Node e verrà utilizzato npm per aggiungere pacchetti di modulo. Per questa applicazione verranno usati i moduli [Express] e [Azure]. Il modulo Express fornisce un modello di framework View Controller per Node, mentre i moduli Azure forniscono la connettività al servizio tabelle.

### <a name="install-express-and-generate-scaffolding"></a>Installare Express e generare lo scaffolding
1. Nella riga di comando creare una nuova directory denominata **elenco attività** e passare a tale directory.  
2. Immettere il comando seguente per installare il modulo Express.
   
        npm install express-generator@4.2.0 -g
   
    A seconda del sistema operativo, potrebbe essere necessario inserire l'elevazione "sudo" prima del comando:
   
        sudo npm install express-generator@4.2.0 -g
   
    L'output appare simile all'esempio seguente:
   
        express-generator@4.2.0 /usr/local/lib/node_modules/express-generator
        ├── mkdirp@0.3.5
        └── commander@1.3.2 (keypress@0.1.0)
   
   > [!NOTE]
   > Il parametro "-g" consente di installare il modulo a livello globale. In questo modo, è possibile usare **express** per generare lo scaffolding dell'app Web senza dover inserire informazioni aggiuntive sul percorso.
   > 
   > 
3. Per creare lo scaffolding per l'applicazione, immettere il comando **express** :
   
        express
   
    L'output di questo comando appare simile al seguente esempio:
   
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
   
           run the app:
             $ DEBUG=my-application ./bin/www
   
    Nella directory **tasklist** sono ora disponibili diverse nuove directory e file.

### <a name="install-additional-modules"></a>Installare moduli aggiuntivi
Uno dei file creati da **express** è **package.json**. Questo file contiene un elenco di dipendenze del modulo. In seguito, quando si distribuirà l'applicazione nelle app Web del servizio app, questo file consentirà di determinare i moduli da installare in Azure.

Nella riga di comando, per installare i moduli descritti nel file **package.json** , immettere il comando riportato di seguito. Potrebbe essere necessario utilizzare l'elevazione "sudo".

    npm install

L'output di questo comando appare simile al seguente esempio:

    debug@0.7.4 node_modules\debug

    cookie-parser@1.0.1 node_modules\cookie-parser
    ├── cookie-signature@1.0.3
    └── cookie@0.1.0

    [...]


Successivamente, immettere il comando riportato di seguito per installare i moduli [azure], [node-uuid], [nconf] e [async]:

    npm install azure-storage node-uuid async nconf --save

Il flag **--save** consente di aggiungere voci per questi moduli al file **package.json**.

L'output di questo comando appare simile al seguente esempio:

    async@0.9.0 node_modules\async

    node-uuid@1.4.1 node_modules\node-uuid

    nconf@0.6.9 node_modules\nconf
    ├── ini@1.2.1
    ├── async@0.2.9
    └── optimist@0.6.0 (wordwrap@0.0.2, minimist@0.0.10)

    [...]


## <a name="create-the-application"></a>Creazione dell'applicazione
A questo punto, è possibile compilare l'applicazione.

### <a name="create-a-model"></a>Creare il modello
Un *modello* è un oggetto che rappresenta i dati nell'applicazione. Per l'applicazione, l'unico modello è l'oggetto attività, che rappresenta un elemento nell'elenco attività. Le attività saranno dotate dei campi seguenti:

* PartitionKey
* RowKey
* name (string)
* category (string)
* completed (Boolean)

Il servizio tabelle usa **PartitionKey** e **RowKey** come chiavi delle tabelle. Per altre informazioni, vedere [Informazioni sul modello di dati del servizio tabelle](https://msdn.microsoft.com/library/azure/dd179338.aspx).

1. Nella directory **tasklist** creare una nuova directory denominata **models**.
2. Nella directory **models** creare un nuovo file denominato **task.js**. Questo file conterrà il modello per le attività create dall'applicazione.
3. All'inizio del file **task.js** , aggiungere il codice seguente per fare riferimento alle librerie necessarie:
   
        var azure = require('azure-storage');
          var uuid = require('node-uuid');
        var entityGen = azure.TableUtilities.entityGenerator;
4. Aggiungere il codice seguente per definire ed esportare l'oggetto Task. Tale oggetto è responsabile per la connessione alla tabella.
   
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
5. Aggiungere il codice seguente per definire metodi aggiuntivi nell'oggetto Task che consentano le interazioni con i dati archiviati nella tabella:
   
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
            // use entityGenerator to set types
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
6. Salvare e chiudere il file **task.js** .

### <a name="create-a-controller"></a>Creare un controller
Un *controller* consente di gestire le richieste HTTP ed eseguire il rendering delle risposte HTML.

1. Nella directory **tasklist/routes** creare un nuovo file denominato **tasklist.js** e aprirlo in un editor di testo.
2. Aggiungere il seguente codice al file **tasklist.js**. Ciò consente il caricamento dei moduli di Azure e di quelli asincroni, utilizzati da **tasklist.js**. Viene inoltre definita la funzione **TaskList**, che viene passata come un'istanza dell'oggetto **Task** definito in precedenza:
   
        var azure = require('azure-storage');
        var async = require('async');
   
        module.exports = TaskList;
3. Definire un oggetto **TaskList** .
   
        function TaskList(task) {
          this.task = task;
        }
4. Aggiungere i metodi seguenti a **TaskList**:
   
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
1. Nella directory **tasklist** aprire il file **app.js**. Questo file è stato creato in precedenza eseguendo il comando **express** .
2. Aggiungere quanto riportato di seguito all'inizio del file per caricare il modulo di Azure, impostare il nome della tabella, la chiave di partizione, e impostare le credenziali di archiviazione usate da questo esempio:
   
        var azure = require('azure-storage');
        var nconf = require('nconf');
        nconf.env()
             .file({ file: 'config.json', search: true });
        var tableName = nconf.get("TABLE_NAME");
        var partitionKey = nconf.get("PARTITION_KEY");
        var accountName = nconf.get("STORAGE_NAME");
        var accountKey = nconf.get("STORAGE_KEY");
   
   > [!NOTE]
   > nconf caricherà i valori di configurazione dalle variabili di ambiente oppure dal file **config.json** , che verrà creato più avanti.
   > 
   > 
3. Nel file app.js scorrere verso il basso fino a individuare la riga seguente:
   
        app.use('/', routes);
        app.use('/users', users);
   
    Sostituire le righe sopra con il codice seguente. Verrà in tal modo inizializzata un'istanza di <strong>Task</strong> con una connessione all'account di archiviazione. Questa viene quindi passata a <strong>TaskList</strong>, che la userà per la comunicazione con il servizio tabelle:
   
        var TaskList = require('./routes/tasklist');
        var Task = require('./models/task');
        var task = new Task(azure.createTableService(accountName, accountKey), tableName, partitionKey);
        var taskList = new TaskList(task);
   
        app.get('/', taskList.showTasks.bind(taskList));
        app.post('/addtask', taskList.addTask.bind(taskList));
        app.post('/completetask', taskList.completeTask.bind(taskList));
4. Salvare il file **app.js** .

### <a name="modify-the-index-view"></a>Modificare la visualizzazione dell'indice
1. Aprire il file **tasklist/views/index.jade** in un editor di testo.
2. Sostituire l'intero contenuto del file con il codice seguente. Ciò consente di definire una visualizzazione delle attività esistenti e includere un modulo per aggiungere nuove attività e contrassegnare quelle esistenti come completate.
   
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

### <a name="modify-the-global-layout"></a>Modificare il layout globale
Il file **layout.jade** nella directory **views** è un modello globale per altri file **.jade**. In questo passaggio verrà modificato in modo da utilizzare [Twitter Bootstrap](https://github.com/twbs/bootstrap), un toolkit che semplifica la progettazione di un'app Web di aspetto gradevole.

Scaricare ed estrarre i file per [Twitter Bootstrap](http://getbootstrap.com/). Copiare il file **bootstrap.min.css** dalla cartella **css** di Bootstrap nella directory **public/stylesheets** dell'applicazione.

Dalla cartella **views** aprire **layout.jade** e sostituire l'intero contenuto con quello seguente:

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
Per eseguire l'app a livello locale, verranno inserite le credenziali di Archiviazione di Azure in un file config. Creare un file denominato **config.json** con il contenuto JSON seguente:

    {
        "STORAGE_NAME": "<storage account name>",
        "STORAGE_KEY": "<storage access key>",
        "PARTITION_KEY": "mytasks",
        "TABLE_NAME": "tasks"
    }

Sostituire **storage account name** con il nome dell'account di archiviazione creato in precedenza e sostituire **storage access key** con la chiave di accesso primaria per l'account di archiviazione. Ad esempio:

    {
        "STORAGE_NAME": "nodejsappstorage",
        "STORAGE_KEY": "KG0oDd..."
        "PARTITION_KEY": "mytasks",
        "TABLE_NAME": "tasks"
    }

Salvare il file *al livello di directory superiore* rispetto alla directory **tasklist** , come mostrato di seguito:

    parent/
      |-- config.json
      |-- tasklist/

Tale operazione è necessaria per evitare di verificare il file config nel controllo del codice sorgente, in cui potrebbe diventare pubblico. Quando si distribuisce l'app in Azure, si usano le variabili di ambiente invece di un file config.

## <a name="run-the-application-locally"></a>Eseguire l'applicazione in locale
Per eseguire il test dell'applicazione nel computer locale, eseguire la procedura seguente:

1. Dalla riga di comando passare alla directory **tasklist** .
2. Usare il comando seguente per avviare l'applicazione in locale:
   
        npm start
3. Aprire un Web browser e passare all'indirizzo http://127.0.0.1:3000.
   
    Verrà visualizzata una pagina Web simile all'esempio seguente.
   
    ![Pagina Web con un elenco di attività vuoto][node-table-finished]
4. Per creare una nuova attività, immettere un nome e una categoria e fare clic su **Aggiungi elemento**. 
5. Per contrassegnare un'attività come completata, selezionare **Completa** e fare clic su **Aggiorna attività**.
   
    ![Immagine del nuovo elemento nell'elenco delle attività][node-table-list-items]

Anche se l'applicazione è in esecuzione in locale, i dati vengono archiviati nel servizio tabelle di Azure.

## <a name="deploy-your-application-to-azure"></a>Distribuire l'applicazione in Azure
Nei passaggi di questa sezione vengono usati gli strumenti da riga di comando di Azure per creare una nuova app Web nel servizio app e viene usato Git per distribuire l'applicazione. Per eseguire questi passaggi, è necessario disporre di una sottoscrizione di Azure.

> [!NOTE]
> È possibile eseguire queste procedure anche nel [Portale di Azure](https://portal.azure.com/). Vedere [Creazione e distribuzione di un'app Web Node.js nel Azure App Service].
> 
> Se questa è la prima app Web di Azure che si crea, per distribuire l'applicazione è necessario utilizzare il portale di Azure.
> 
> 

Per iniziare, installare l' [Interfaccia della riga di comando di Azure] immettendo il seguente comando nella riga di comando:

    npm install azure-cli -g

### <a name="import-publishing-settings"></a>Importare le impostazioni di pubblicazione
In questo passaggio verrà scaricato un file contenente informazioni sulla sottoscrizione.

1. Immettere il comando seguente:
   
        azure login
   
    Questo comando consente di avviare un browser e di passare alla pagina per il download. Se richiesto, accedere con l'account associato alla sottoscrizione di Azure.
   
    <!-- ![The download page][download-publishing-settings] -->
   
    Il download del file inizia automaticamente. In caso contrario, è possibile fare clic sul collegamento all'inizio della pagina per scaricare manualmente il file. Salvare il file e prendere nota del percorso del file.
2. Immettere il seguente comando per importare le impostazioni:
   
        azure account import <path-to-file>
   
    Specificare il percorso e il nome del file delle impostazioni di pubblicazione scaricato nel passaggio precedente.
3. Una volta importate le impostazioni, eliminare il file di impostazioni di pubblicazione. Non è più necessario e contiene informazioni riservate relative alla sottoscrizione di Azure.

### <a name="create-an-app-service-web-app"></a>Creare un piano di servizio app
1. Dalla riga di comando passare alla directory **tasklist** .
2. Usare il comando seguente per creare una nuova app Web.
   
        azure site create --git
   
    Verrà richiesto il nome e il percorso dell'app Web. Fornire un nome univoco e selezionare la stessa area geografica dell'account di Archiviazione di Azure.
   
    Il parametro `--git` consente di creare un archivio GIT per l'app Web in Azure. Inoltre consente di inizializzare un archivio GIT nella directory corrente, se non ne esiste nessuno, e di aggiungere un [GIT remoto] denominato "azure", usato per pubblicare l'applicazione in Azure. Infine, consente di creare un file **web.config** contenente le impostazioni usate da Azure per ospitare le applicazioni Node. Se il parametro `--git` viene omesso ma la directory contiene un archivio GIT, il comando consente di creare comunque l'archivio "azure".
   
    Dopo il completamento di questo comando, verrà visualizzato un output simile al seguente. Si noti che la riga che inizia con **Website created at** contiene l'URL dell'app Web.
   
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
   > Se si tratta della prima app Web del servizio app per la sottoscrizione, verrà indicato di usare il Portale di Azure per la creazione dell'app Web. Per ulteriori informazioni, vedere [Creazione e distribuzione di un'app Web Node.js nel Azure App Service].
   > 
   > 

### <a name="set-environment-variables"></a>Impostare le variabili di ambiente
In questo passaggio verranno aggiunte le variabili di ambiente per la configurazione dell'app Web in Azure.
Nella riga di comando immettere quanto segue:

    azure site appsetting add
        STORAGE_NAME=<storage account name>;STORAGE_KEY=<storage access key>;PARTITION_KEY=mytasks;TABLE_NAME=tasks


Sostituire **<storage account name>** con il nome dell'account di archiviazione creato in precedenza e sostituire **<storage access key>** con la chiave di accesso primaria per l'account di archiviazione. Utilizzare gli stessi valori del file config.json creato in precedenza.

In alternativa, è possibile impostare le variabili di ambiente nel [Portale di Azure](https://portal.azure.com/):

1. Aprire il pannello dell'app Web facendo clic su **Sfoglia** > **App Web** > nome app Web.
2. Nel pannello dell'app Web fare clic su **Tutte le impostazioni** > **Impostazioni dell'applicazione**.
   
     <!-- ![Top Menu](./media/storage-nodejs-use-table-storage-web-site/PollsCommonWebSiteTopMenu.png) -->
3. Scorrere verso il basso la sezione **Impostazioni app** e aggiungere le coppie chiave-valore.
   
     ![Impostazioni app](./media/storage-nodejs-use-table-storage-web-site/storage-tasks-appsettings.png)
4. Fare clic su **SAVE**.

### <a name="publish-the-application"></a>Pubblicare l'applicazione
Per pubblicare l'app, confermare i file di codice per GIT, quindi effettuare il push di azure/master.

1. Impostare le credenziali di distribuzione
   
        azure site deployment user set <name> <password>
2. Aggiungere ed effettuare il commit dei file dell'applicazione.
   
        git add .
        git commit -m "adding files"
3. Eseguire il push del commit per l'app Web del servizio app:
   
        git push azure master
   
    Usare **master** come diramazione di destinazione. Al termine della distribuzione, viene visualizzata un'istruzione simile al seguente esempio:
   
        To https://username@tabletasklist.azurewebsites.net/TableTasklist.git
          * [new branch]      master -> master
4. Al termine dell'operazione di push, passare all'URL dell'app Web restituito in precedenza dal comando `azure create site` per visualizzare l'applicazione.

## <a name="next-steps"></a>Passaggi successivi
Nei passaggi di questo articolo viene descritto come archiviare informazioni tramite il servizio tabelle. Tuttavia per tale attività è anche possibile usare [MongoDB](https://mlab.com/azure/). 

## <a name="additional-resources"></a>Risorse aggiuntive
[Interfaccia della riga di comando di Azure]

## <a name="whats-changed"></a>Modifiche apportate
* Per una guida relativa al passaggio da Siti Web al servizio app, vedere [Servizio app di Azure e impatto sui servizi di Azure esistenti](http://go.microsoft.com/fwlink/?LinkId=529714)

<!-- URLs -->

[Creazione e distribuzione di un'app Web Node.js nel Azure App Service]: app-service-web-get-started-nodejs.md
[Azure Developer Center]: /develop/nodejs/

[node]: http://nodejs.org
[Git]: http://git-scm.com
[Express]: http://expressjs.com
[for free]: http://windowsazure.com
[GIT remoto]: http://git-scm.com/docs/git-remote

[Interfaccia della riga di comando di Azure]:../cli-install-nodejs.md

[azure]: https://github.com/Azure/azure-sdk-for-node
[node-uuid]: https://www.npmjs.com/package/node-uuid
[nconf]: https://www.npmjs.com/package/nconf
[async]: https://www.npmjs.com/package/async

[Azure Portal]: https://portal.azure.com

[Create and deploy a Node.js application to an Azure Web Site]: app-service-web-get-started-nodejs.md

<!-- Image References -->

[node-table-finished]: ./media/storage-nodejs-use-table-storage-web-site/table_todo_empty.png
[node-table-list-items]: ./media/storage-nodejs-use-table-storage-web-site/table_todo_list.png
[download-publishing-settings]: ./media/storage-nodejs-use-table-storage-web-site/azure-account-download-cli.png
[portal-storage-access-keys]: ./media/storage-nodejs-use-table-storage-web-site/manage-access-keys.png
[app-settings]: ./media/storage-nodejs-use-table-storage-web-site/storage-tasks-appsettings.png
