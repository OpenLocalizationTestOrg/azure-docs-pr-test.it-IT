---
title: app aaaWeb con archiviazione tabella (Node.js) | Documenti Microsoft
description: Esercitazione si basa su hello App Web con l'esercitazione di Express e aggiunta di servizi di archiviazione di Azure e hello modulo Azure.
services: cosmos-db
documentationcenter: nodejs
author: mimig1
manager: jhubbard
editor: tysonn
ms.assetid: e90959a2-4cb2-4b19-9bfb-aede15b18b1c
ms.service: cosmos-db
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 12/08/2016
ms.author: mimig
ms.openlocfilehash: 7eefc09baab61cf44c98183135abe572b11812e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="nodejs-web-application-using-storage"></a>Creazione di un'applicazione Web Node.js con Archiviazione
## <a name="overview"></a>Panoramica
In questa esercitazione, hello applicazione creata nel [applicazione Web Node.js mediante Express] esercitazione esteso mediante le librerie Client di hello Microsoft Azure per Node.js toowork con servizi di gestione dati. Estendere l'applicazione mediante la creazione di un'applicazione elenco attività basate sul web che è possibile distribuire tooAzure. elenco di attività Hello consente di recuperare le attività, aggiungere nuove attività e contrassegnare l'attività come completata.

gli elementi di attività Hello vengono archiviati in archiviazione di Azure. Archiviazione di Azure consente l'archiviazione di dati non strutturati, a tolleranza di errore e a disponibilità elevata. Archiviazione di Azure include varie strutture di dati in cui è possibile archiviare i dati e da cui è possibile accedere ad essi. È possibile utilizzare servizi di archiviazione hello da hello API incluse in hello Azure SDK per Node.js o tramite le API REST. Per ulteriori informazioni, vedere [Archiviazione e accesso ai dati in Azure].

In questa esercitazione si presuppone che siano state completate hello [applicazione Web Node.js] e [Node.js con Express][applicazione Web Node.js mediante Express] esercitazioni.

Contiene hello le seguenti informazioni:

* Come toowork con hello motore del modello Jade
* Come toowork con i servizi di gestione dati di Azure

Hello seguente schermata mostra un'applicazione hello completata:

![Hello completata la pagina web in internet explorer](./media/table-storage-cloud-service-nodejs/getting-started-1.png)

## <a name="setting-storage-credentials-in-webconfig"></a>Impostazione delle credenziali di archiviazione in Web.Config
È necessario passare le credenziali di archiviazione tooaccess di archiviazione di Azure. Questa operazione viene eseguita utilizzando le impostazioni dell'applicazione Web. config hello.
le impostazioni di Web. config Hello vengono passate come tooNode variabili di ambiente, che vengono quindi letti da hello Azure SDK.

> [!NOTE]
> Le credenziali di archiviazione vengono utilizzate solo quando un'applicazione hello è tooAzure distribuito. Quando in esecuzione nell'emulatore di hello, un'applicazione hello Usa emulatore di archiviazione hello.
>
>

Eseguire hello seguente credenziali dell'account di archiviazione di passaggi tooretrieve hello e aggiungerli toohello le impostazioni di Web. config:

1. Se non è già aperto, avviare hello Azure PowerShell da hello **avviare** menu espandendo **tutti i programmi, Azure**, fare doppio clic su **Azure PowerShell**, quindi selezionare  **Esegui come amministratore**.
2. Cambia cartella toohello directory contenente l'applicazione. Ad esempio, C:\\node\\tasklist\\WebRole1.
3. Dalla finestra di Powershell Azure hello, immettere hello seguenti informazioni sull'account di archiviazione di cmdlet tooretrieve hello:

    ```powershell
    PS C:\node\tasklist\WebRole1> Get-AzureStorageAccounts
    ```

   Hello cmdlet precedente recupera hello elenco di account di archiviazione e le chiavi dell'account associate al servizio ospitato.

   > [!NOTE]
   > Poiché hello Azure SDK consente di creare un account di archiviazione quando si distribuisce un servizio, un account di archiviazione deve essere già esistente dalla distribuzione dell'applicazione nelle guide precedenti hello.
   >
   >
4. Aprire hello **Servicedefinition** file contenenti le impostazioni di ambiente hello che vengono utilizzate quando un'applicazione hello tooAzure distribuito:

    ```powershell
    PS C:\node\tasklist> notepad ServiceDefinition.csdef
    ```

5. Seguente hello Inserisci bloccare in **ambiente** elemento, sostituendo con i propri {ACCOUNT di archiviazione di} e {chiave di accesso di archiviazione} con il nome di account hello e chiave primaria di hello per account di archiviazione hello da toouse per la distribuzione:

  <Variable name="AZURE_STORAGE_ACCOUNT" value="{STORAGE ACCOUNT}" />
  <Variable name="AZURE_STORAGE_ACCESS_KEY" value="{STORAGE ACCESS KEY}" />

   ![contenuto del file Hello web.cloud.config](./media/table-storage-cloud-service-nodejs/node37.png)

6. Salvare il file hello e chiudere il blocco note.

### <a name="install-additional-modules"></a>Installare moduli aggiuntivi
1. Hello utilizzo successivo comando tooinstall hello [azure], [nodo-uuid], [nconf] e [asincrona] moduli in locale, nonché a toosave una voce relativa toohello **package. JSON** file:

  ```powershell
  PS C:\node\tasklist\WebRole1> npm install azure-storage node-uuid async nconf --save
  ```

  output di Hello di questo comando risulterà simile toohello seguenti:

  ```
  node-uuid@1.4.1 node_modules\node-uuid

  nconf@0.6.9 node_modules\nconf
  ├── ini@1.1.0
  ├── async@0.2.9
  └── optimist@0.6.0 (wordwrap@0.0.2, minimist@0.0.8)

  azure-storage@0.1.0 node_modules\azure-storage
  ├── extend@1.2.1
  ├── xmlbuilder@0.4.3
  ├── mime@1.2.11
  ├── underscore@1.4.4
  ├── validator@3.1.0
  ├── node-uuid@1.4.1
  ├── xml2js@0.2.7 (sax@0.5.2)
  └── request@2.27.0 (json-stringify-safe@5.0.0, tunnel-agent@0.3.0, aws-sign@0.3.0, forever-agent@0.5.2, qs@0.6.6, oauth-sign@0.3.0, cookie-jar@0.3.0, hawk@1.0.0, form-data@0.1.3, http-signature@0.10.0)
  ```

## <a name="using-hello-table-service-in-a-node-application"></a>Utilizzo del servizio tabelle hello in un'applicazione di nodo
In questa sezione, hello base dell'applicazione creato da hello **express** comando verrà esteso mediante l'aggiunta di un **task.js** file contenente il modello di hello per le attività. Modificare hello esistente **app.js** file e creare un nuovo **tasklist.js** file che utilizza il modello di hello.

### <a name="create-hello-model"></a>Creare il modello di hello
1. In hello **WebRole1** directory, creare una nuova directory denominata **modelli**.
2. In hello **modelli** directory, creare un nuovo file denominato **task.js**. Questo file contiene il modello di hello per le operazioni di hello create dall'applicazione.
3. All'inizio di hello di hello **task.js** file, aggiungere hello tooreference richiesto dalle librerie di codice seguente:

    ```nodejs
    var azure = require('azure-storage');
    var uuid = require('node-uuid');
    var entityGen = azure.TableUtilities.entityGenerator;
    ```

4. Successivamente, aggiungere codice toodefine ed esportare l'oggetto attività hello. oggetto attività Hello è responsabile per la connessione toohello tabella.

    ```nodejs
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
    ```

5. Successivamente, aggiungere hello seguito metodi aggiuntivi di codice toodefine nell'oggetto attività hello, che consentono le interazioni con i dati archiviati nella tabella hello:

    ```nodejs
    Task.prototype = {
      find: function(query, callback) {
        self = this;
        self.storageClient.queryEntities(query, function entitiesQueried(error, result) {
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
    ```

6. Salvare e chiudere hello **task.js** file.

### <a name="create-hello-controller"></a>Creare controller hello
1. In hello **WebRole1/route** directory, creare un nuovo file denominato **tasklist.js** e aprirlo in un editor di testo.
2. Aggiungere hello seguente codice troppo**tasklist.js**. Questo codice carica hello azure e moduli asincrono, che vengono utilizzati da **tasklist.js** e definisce hello **TaskList** funzione, che viene passata un'istanza di hello **attività** è l'oggetto definito in precedenza:

    ```nodejs
    var azure = require('azure-storage');
    var async = require('async');

    module.exports = TaskList;

    function TaskList(task) {
      this.task = task;
    }
    ```

3. Continuare ad aggiungere toohello **tasklist.js** file mediante l'aggiunta di metodi hello troppo**showTasks**, **addTask**, e **completeTasks**:

    ```nodejs
    TaskList.prototype = {
      showTasks: function(req, res) {
        self = this;
        var query = azure.TableQuery()
          .where('completed eq ?', false);
        self.task.find(query, function itemsFound(error, items) {
          res.render('index',{title: 'My ToDo List ', tasks: items});
        });
      },

      addTask: function(req,res) {
        var self = this
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
    ```

4. Salvare hello **tasklist.js** file.

### <a name="modify-appjs"></a>Modificare il file app.js
1. In hello **WebRole1** hello directory, aprire **app.js** file in un editor di testo.
2. Inizio hello del file hello, aggiungere hello seguente modulo hello azure tooload e impostare la chiave di nome e una partizione di tabella hello:

    ```nodejs
    var azure = require('azure-storage');
    var tableName = 'tasks';
    var partitionKey = 'hometasks';
    ```

3. Nel file app.js hello, scorrere verso il basso toowhere vedrai hello la seguente riga:

    ```nodejs
    app.use('/', routes);
    app.use('/users', users);
    ```

    Sostituire hello precedenti righe con hello seguente codice. Questo codice Inizializza un'istanza di <strong>attività</strong> con un account di archiviazione tooyour di connessione. Hello <strong>attività</strong> viene passato toohello <strong>TaskList</strong>, che utilizza toocommunicate con servizio tabella hello:

    ```nodejs
    var TaskList = require('./routes/tasklist');
    var Task = require('./models/task');
    var task = new Task(azure.createTableService(), tableName, partitionKey);
    var taskList = new TaskList(task);

    app.get('/', taskList.showTasks.bind(taskList));
    app.post('/addtask', taskList.addTask.bind(taskList));
    app.post('/completetask', taskList.completeTask.bind(taskList));
    ```

4. Salvare hello **app.js** file.

### <a name="modify-hello-index-view"></a>Modifica visualizzazione dell'indice hello
1. Modificare le directory toohello **viste** hello directory e aprire **index.jade** file in un editor di testo.
2. Sostituire il contenuto di hello di hello **index.jade** file con hello seguente codice. Questo codice definisce la visualizzazione hello per le attività esistenti e un modulo per l'aggiunta di nuove attività e contrassegnare esistenti come completata.

    ```
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
          if tasks != []
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
    ```

3. Salvare e chiudere il file **index.jade** .

### <a name="modify-hello-global-layout"></a>Modifica layout globale hello
Hello **layout.jade** file hello **viste** directory viene utilizzata come modello generale per altri **.jade** file. In questo passaggio, modificare hello **layout.jade** file toouse [Twitter Bootstrap](https://github.com/twbs/bootstrap), che è un toolkit che rende facile toodesign un sito Web professionale nice.

1. Scaricare ed estrarre file hello per [Twitter Bootstrap](http://getbootstrap.com/). Hello copia **bootstrap.min.css** file hello **bootstrap\\dist\\css** cartella toohello **pubblica\\fogli di stile** directory dell'applicazione elenco attività.
2. Da hello **viste** cartella, aprire hello **layout.jade** file nell'editor di testo e sostituire il contenuto di hello con hello seguente:

    doctype html  html    head      title= title      link(rel='stylesheet', href='/stylesheets/bootstrap.min.css')      link(rel='stylesheet', href='/stylesheets/style.css')    body.app      nav.navbar.navbar-default        div.navbar-header          a.navbar-brand(href='/') My Tasks      block content

3. Salvare hello **layout.jade** file.

### <a name="running-hello-application-in-hello-emulator"></a>Esecuzione dell'applicazione hello in hello emulatore
Utilizzare hello seguito comando toostart hello applicazione nell'emulatore hello.

```powershell
PS C:\node\tasklist\WebRole1> start-azureemulator -launch
```

browser Hello verrà visualizzato hello pagina seguente:

![Un sito web di paging denominato elenco di attività personali con una tabella contenente le attività e i campi tooadd una nuova attività.](./media/table-storage-cloud-service-nodejs/node44.png)

Utilizzare elementi del modulo di hello tooadd o rimuovere elementi esistenti, contrassegnandoli come completata.

## <a name="publishing-hello-application-tooazure"></a>Pubblicazione hello applicazione tooAzure
Nella finestra di Windows PowerShell hello, chiamare hello seguente cmdlet tooredeploy tooAzure il servizio ospitato.

```powershell
PS C:\node\tasklist\WebRole1> Publish-AzureServiceProject -name myuniquename -location datacentername -launch
```

Sostituire **myuniquename** con un nome univoco per questa applicazione. Sostituire **datacentername** con nome hello del data center di Azure, ad esempio **Stati Uniti occidentali**.

Una volta completata la distribuzione di hello, vedrai un seguente toohello simile risposta:

```
  PS C:\node\tasklist> publish-azureserviceproject -servicename tasklist -location "West US"
  WARNING: Publishing tasklist tooMicrosoft Azure. This may take several minutes...
  WARNING: 2:18:42 PM - Preparing runtime deployment for service 'tasklist'
  WARNING: 2:18:42 PM - Verifying storage account 'tasklist'...
  WARNING: 2:18:43 PM - Preparing deployment for tasklist with Subscription ID: 65a1016d-0f67-45d2-b838-b8f373d6d52e...
  WARNING: 2:19:01 PM - Connecting...
  WARNING: 2:19:02 PM - Uploading Package toostorage service larrystore...
  WARNING: 2:19:40 PM - Upgrading...
  WARNING: 2:22:48 PM - Created Deployment ID: b7134ab29b1249ff84ada2bd157f296a.
  WARNING: 2:22:48 PM - Initializing...
  WARNING: 2:22:49 PM - Instance WebRole1_IN_0 of role WebRole1 is ready.
  WARNING: 2:22:50 PM - Created Website URL: http://tasklist.cloudapp.net/.
```

Specificando hello **-avviare** opzione hello cmdlet precedente, il browser hello aprirà e visualizzerà l'applicazione in esecuzione in Azure quando viene completata la pubblicazione.

![Visualizzazione della pagina di elenco di attività personali hello una finestra del browser. URL di Hello indica pagina hello ora sia ospitata in Azure.](./media/table-storage-cloud-service-nodejs/getting-started-1.png)

## <a name="stopping-and-deleting-your-application"></a>Arresto ed eliminazione dell'applicazione
Dopo aver distribuito l'applicazione, è opportuno toodisable in modo da evitare i costi o compilare e distribuire applicazioni all'interno di hello gratuitamente periodo di tempo di valutazione.

Azure addebita le istanze del ruolo Web al consumo, in base all'utilizzo di tempo del server su base oraria.
Ora del server viene utilizzata una volta distribuita l'applicazione, anche se le istanze non sono in esecuzione e si trovano nello stato arrestato hello.

Hello passaggi seguenti viene illustrato come toostop ed eliminare l'applicazione.

1. Nella finestra di Windows PowerShell hello, arrestare la distribuzione del servizio hello creata nella sezione precedente di hello con hello seguente cmdlet:

    ```powershell
    PS C:\node\tasklist\WebRole1> Stop-AzureService
    ```

   L'arresto del servizio hello potrebbe richiedere alcuni minuti. Quando il servizio hello viene arrestato, viene visualizzato un messaggio che indica che è stato arrestato.

2. servizio di hello toodelete, hello chiamata seguente cmdlet:

    ```powershell
    PS C:\node\tasklist\WebRole1> Remove-AzureService contosotasklist
    ```

   Quando richiesto, immettere **Y** servizio hello toodelete.

   Eliminazione del servizio hello potrebbe richiedere alcuni minuti. Una volta eliminato il servizio di hello, si riceverà un messaggio che indica che il servizio di hello è stato eliminato.

[applicazione Web Node.js mediante Express]: http://azure.microsoft.com/develop/nodejs/tutorials/web-app-with-express/
[Archiviazione e accesso ai dati in Azure]: http://msdn.microsoft.com/library/azure/gg433040.aspx
[applicazione Web Node.js]: http://azure.microsoft.com/develop/nodejs/tutorials/getting-started/


