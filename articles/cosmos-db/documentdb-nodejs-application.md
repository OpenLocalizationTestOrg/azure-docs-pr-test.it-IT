---
title: un'app web Node. js per Azure Cosmos DB aaaBuild | Documenti Microsoft
description: In questa esercitazione Node.js Esplora come database di Microsoft Azure Cosmos toostore e l'accesso dei dati da un'applicazione web Node.js Express toouse ospitato nei siti Web di Azure.
keywords: Sviluppo di applicazioni, esercitazione sul database, informazioni su node.js, esercitazione su node.js
services: cosmos-db
documentationcenter: nodejs
author: mimig1
manager: jhubbard
editor: cgronlun
ms.assetid: 9da9e63b-e76a-434e-96dd-195ce2699ef3
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/14/2017
ms.author: mimig
ms.openlocfilehash: 31194dccf37eef69d2219b0d8328a88d434f79b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="_Toc395783175"></a>Creare un'applicazione Web Node.js con Azure Cosmos DB
> [!div class="op_single_selector"]
> * [.NET](documentdb-dotnet-application.md)
> * [Node.JS](documentdb-nodejs-application.md)
> * [Java](documentdb-java-application.md)
> * [Python](documentdb-python-application.md)
> 
> 

Questa esercitazione Node.js illustra come toouse DB Cosmos Azure e l'API DocumentDB toostore e accedere ai dati da un'applicazione Node.js Express hello ospitato nei siti Web di Azure. Verrà creata una semplice applicazione di gestione delle attività basata su Web, un'app ToDo, che consente di creare, recuperare e completare le attività. attività Hello vengono archiviate come documenti JSON in Azure Cosmos DB. In questa esercitazione viene illustrata la creazione di hello e la distribuzione dell'applicazione hello e illustra ciò che avviene in ogni frammento di codice.

![Cattura di schermata di hello applicazione elenco attività personali creato in questa esercitazione Node.js](./media/documentdb-nodejs-application/cosmos-db-node-js-mytodo.png)

Non dispongono di esercitazione hello toocomplete di tempo e si desidera tooget soluzione completa di hello? Non è un problema, è possibile ottenere soluzione di esempio completo di hello da [GitHub][GitHub]. Solo lettura hello [Leggimi](https://github.com/Azure-Samples/documentdb-node-todo-app/blob/master/README.md) file per istruzioni su come toorun hello app.

## <a name="_Toc395783176"></a>Prerequisiti
> [!TIP]
> Questa esercitazione Node.js presuppone già una certa esperienza nell'uso di Node.js e di Siti Web di Azure.
> 
> 

Prima di seguire le istruzioni di hello in questo articolo, è necessario assicurarsi di aver seguito hello:

* Un account Azure attivo. Se non si dispone di un account, è possibile creare un account di valutazione gratuita in pochi minuti. Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).

   OPPURE

   Un'installazione locale di hello [Azure Cosmos DB emulatore](local-emulator.md) (solo Windows).
* [Node.js][Node.js] 0.10.29 o versione successiva.
* [Generatore di Express](http://www.expressjs.com/starter/generator.html), installabile tramite `npm install express-generator -g`
* [Git][Git].

## <a name="_Toc395637761"></a>Passaggio 1: Creare un account del database di Azure Cosmos DB
Creare prima di tutto un account Azure Cosmos DB. Se è già un account o se si utilizza hello Azure Cosmos DB emulatore per questa esercitazione, è possibile ignorare troppo[passaggio 2: creare una nuova applicazione Node.js](#_Toc395783178).

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

[!INCLUDE [cosmos-db-keys](../../includes/cosmos-db-keys.md)]

## <a name="_Toc395783178"></a>Passaggio 2: Creare una nuova applicazione Node.js
Ora esaminiamo un progetto di base Hello World Node.js utilizzando hello toocreate [Express](http://expressjs.com/) framework.

1. Aprire il terminal preferito, ad esempio hello Node.js il prompt dei comandi.
2. Passare toohello directory in cui si desidera nuova applicazione di toostore hello.
3. Utilizzare hello generatore express toogenerate una nuova applicazione denominata **todo**.
   
        express todo
4. Aprire la nuova directory **todo** e installare le dipendenze.
   
        cd todo
        npm install
5. Eseguire la nuova applicazione.
   
        npm start
6. È possibile visualizzare la nuova applicazione passando il browser troppo[http://localhost:3000](http://localhost:3000).
   
    ![Informazioni su Node.js - schermata di hello applicazione Hello World in una finestra del browser](./media/documentdb-nodejs-application/cosmos-db-node-js-express.png)

    Quindi, toostop hello applicazione, premere CTRL + C nella finestra terminal hello e quindi fare clic su **y** processo batch di hello tooterminate.

## <a name="_Toc395783179"></a>Passaggio 3: Installare moduli aggiuntivi
Hello **package. JSON** file è uno dei file hello creati nella directory radice del progetto hello hello. Questo file contiene un elenco di moduli aggiuntivi necessari per l'applicazione Node.js. In seguito, quando si distribuisce questo tooAzure applicazione siti Web, questo file viene utilizzato toodetermine quali toobe necessità di moduli in Azure toosupport l'applicazione installata. È comunque necessario tooinstall due altri pacchetti per questa esercitazione.

1. In hello terminal, installare hello **async** modulo tramite npm.
   
        npm install async --save
2. Installare hello **documentdb** modulo tramite npm. Questo è il modulo di hello in cui viene eseguita chiave di Azure Cosmos DB hello tutti.
   
        npm install documentdb --save
3. Un rapido controllo di hello **package. JSON** file dell'applicazione hello deve visualizzare hello moduli aggiuntivi. Questo file verrà indicare quali toodownload pacchetti ad Azure e installare durante l'esecuzione dell'applicazione. Il risultato sarà simile esempio hello riportato di seguito.
   
        {
          "name": "todo",
          "version": "0.0.0",
          "private": true,
          "scripts": {
            "start": "node ./bin/www"
          },
          "dependencies": {
            "async": "^2.1.4",
            "body-parser": "~1.15.2",
            "cookie-parser": "~1.4.3",
            "debug": "~2.2.0",
            "documentdb": "^1.10.0",
            "express": "~4.14.0",
            "jade": "~1.11.0",
            "morgan": "~1.7.0",
            "serve-favicon": "~2.3.0"
          }
        }
   
    Ciò indicherà a Node (e più avanti ad Azure) che l'applicazione dipende da questi moduli aggiuntivi.

## <a name="_Toc395783180"></a>Passaggio 4: Utilizzo del servizio di Azure Cosmos DB hello in un'applicazione di nodo
Che si occupa di tutto la configurazione iniziale di hello e la configurazione, ora si get verso il basso toowhy siamo qui, ovvero toowrite alcuni codice che usa Azure Cosmos DB.

### <a name="create-hello-model"></a>Creare il modello di hello
1. Nella directory di progetto hello, creare una nuova directory denominata **modelli** in hello stessa directory del file package. JSON hello.
2. In hello **modelli** directory, creare un nuovo file denominato **taskDao.js**. Questo file contiene il modello di hello per le operazioni di hello create tramite l'applicazione.
3. In hello stesso **modelli** directory, creare un nuovo file denominato **docdbUtils.js**. Questo file conterrà porzioni di codice utile e riutilizzabile, che verrà usato nell'applicazione. 
4. Copia hello di codice seguente troppo**docdbUtils.js**
   
        var DocumentDBClient = require('documentdb').DocumentClient;
   
        var DocDBUtils = {
            getOrCreateDatabase: function (client, databaseId, callback) {
                var querySpec = {
                    query: 'SELECT * FROM root r WHERE r.id= @id',
                    parameters: [{
                        name: '@id',
                        value: databaseId
                    }]
                };
   
                client.queryDatabases(querySpec).toArray(function (err, results) {
                    if (err) {
                        callback(err);
   
                    } else {
                        if (results.length === 0) {
                            var databaseSpec = {
                                id: databaseId
                            };
   
                            client.createDatabase(databaseSpec, function (err, created) {
                                callback(null, created);
                            });
   
                        } else {
                            callback(null, results[0]);
                        }
                    }
                });
            },
   
            getOrCreateCollection: function (client, databaseLink, collectionId, callback) {
                var querySpec = {
                    query: 'SELECT * FROM root r WHERE r.id=@id',
                    parameters: [{
                        name: '@id',
                        value: collectionId
                    }]
                };               
   
                client.queryCollections(databaseLink, querySpec).toArray(function (err, results) {
                    if (err) {
                        callback(err);
   
                    } else {        
                        if (results.length === 0) {
                            var collectionSpec = {
                                id: collectionId
                            };
   
                            client.createCollection(databaseLink, collectionSpec, function (err, created) {
                                callback(null, created);
                            });
   
                        } else {
                            callback(null, results[0]);
                        }
                    }
                });
            }
        };
   
        module.exports = DocDBUtils;
   
5. Salvare e chiudere hello **docdbUtils.js** file.
6. All'inizio di hello di hello **taskDao.js** file, aggiungere i seguenti hello tooreference codice hello **DocumentDBClient** hello e **docdbUtils.js** creato in precedenza:
   
        var DocumentDBClient = require('documentdb').DocumentClient;
        var docdbUtils = require('./docdbUtils');
7. Successivamente, aggiungere codice toodefine che esporta l'oggetto attività hello. Questo è responsabile per l'inizializzazione dell'oggetto di attività e configurando hello Database e la raccolta documenti verrà utilizzato.
   
        function TaskDao(documentDBClient, databaseId, collectionId) {
          this.client = documentDBClient;
          this.databaseId = databaseId;
          this.collectionId = collectionId;
   
          this.database = null;
          this.collection = null;
        }
   
        module.exports = TaskDao;
8. Successivamente, aggiungere hello seguito metodi aggiuntivi di codice toodefine nell'oggetto attività hello, che consentono le interazioni con i dati archiviati nel database di Azure Cosmos.
   
        TaskDao.prototype = {
            init: function (callback) {
                var self = this;
   
                docdbUtils.getOrCreateDatabase(self.client, self.databaseId, function (err, db) {
                    if (err) {
                        callback(err);
                    } else {
                        self.database = db;
                        docdbUtils.getOrCreateCollection(self.client, self.database._self, self.collectionId, function (err, coll) {
                            if (err) {
                                callback(err);
   
                            } else {
                                self.collection = coll;
                            }
                        });
                    }
                });
            },
   
            find: function (querySpec, callback) {
                var self = this;
   
                self.client.queryDocuments(self.collection._self, querySpec).toArray(function (err, results) {
                    if (err) {
                        callback(err);
   
                    } else {
                        callback(null, results);
                    }
                });
            },
   
            addItem: function (item, callback) {
                var self = this;
   
                item.date = Date.now();
                item.completed = false;
   
                self.client.createDocument(self.collection._self, item, function (err, doc) {
                    if (err) {
                        callback(err);
   
                    } else {
                        callback(null, doc);
                    }
                });
            },
   
            updateItem: function (itemId, callback) {
                var self = this;
   
                self.getItem(itemId, function (err, doc) {
                    if (err) {
                        callback(err);
   
                    } else {
                        doc.completed = true;
   
                        self.client.replaceDocument(doc._self, doc, function (err, replaced) {
                            if (err) {
                                callback(err);
   
                            } else {
                                callback(null, replaced);
                            }
                        });
                    }
                });
            },
   
            getItem: function (itemId, callback) {
                var self = this;
   
                var querySpec = {
                    query: 'SELECT * FROM root r WHERE r.id = @id',
                    parameters: [{
                        name: '@id',
                        value: itemId
                    }]
                };
   
                self.client.queryDocuments(self.collection._self, querySpec).toArray(function (err, results) {
                    if (err) {
                        callback(err);
   
                    } else {
                        callback(null, results[0]);
                    }
                });
            }
        };
9. Salvare e chiudere hello **taskDao.js** file. 

### <a name="create-hello-controller"></a>Creare controller hello
1. In hello **route** directory del progetto, creare un nuovo file denominato **tasklist.js**. 
2. Aggiungere hello seguente codice troppo**tasklist.js**. Viene caricato hello DocumentDBClient e async moduli, che vengono utilizzati da **tasklist.js**. Questo elemento anche definito hello **TaskList** funzione, che viene passata un'istanza di hello **attività** dell'oggetto definita in precedenza:
   
        var DocumentDBClient = require('documentdb').DocumentClient;
        var async = require('async');
   
        function TaskList(taskDao) {
          this.taskDao = taskDao;
        }
   
        module.exports = TaskList;
3. Continuare ad aggiungere toohello **tasklist.js** file mediante l'aggiunta di metodi hello troppo**showTasks, addTask**, e **completeTasks**:
   
        TaskList.prototype = {
            showTasks: function (req, res) {
                var self = this;
   
                var querySpec = {
                    query: 'SELECT * FROM root r WHERE r.completed=@completed',
                    parameters: [{
                        name: '@completed',
                        value: false
                    }]
                };
   
                self.taskDao.find(querySpec, function (err, items) {
                    if (err) {
                        throw (err);
                    }
   
                    res.render('index', {
                        title: 'My ToDo List ',
                        tasks: items
                    });
                });
            },
   
            addTask: function (req, res) {
                var self = this;
                var item = req.body;
   
                self.taskDao.addItem(item, function (err) {
                    if (err) {
                        throw (err);
                    }
   
                    res.redirect('/');
                });
            },
   
            completeTask: function (req, res) {
                var self = this;
                var completedTasks = Object.keys(req.body);
   
                async.forEach(completedTasks, function taskIterator(completedTask, callback) {
                    self.taskDao.updateItem(completedTask, function (err) {
                        if (err) {
                            callback(err);
                        } else {
                            callback(null);
                        }
                    });
                }, function goHome(err) {
                    if (err) {
                        throw err;
                    } else {
                        res.redirect('/');
                    }
                });
            }
        };
4. Salvare e chiudere hello **tasklist.js** file.

### <a name="add-configjs"></a>Aggiungere config.json
1. Nella directory del progetto creare un nuovo file denominato **config.js**.
2. Aggiungere il seguente troppo di hello**config.js**. Definisce le impostazioni e i valori di configurazione necessari per l'applicazione.
   
        var config = {}
   
        config.host = process.env.HOST || "[hello URI value from hello Azure Cosmos DB Keys blade on http://portal.azure.com]";
        config.authKey = process.env.AUTH_KEY || "[hello PRIMARY KEY value from hello Azure Cosmos DB Keys blade on http://portal.azure.com]";
        config.databaseId = "ToDoList";
        config.collectionId = "Items";
   
        module.exports = config;
3. In hello **config.js** file, i valori hello aggiornamento dell'HOST e utilizzando i valori hello trovati nel Pannello di hello chiavi dell'account di Azure Cosmos DB hello AUTH_KEY [portale Microsoft Azure](https://portal.azure.com).
4. Salvare e chiudere hello **config.js** file.

### <a name="modify-appjs"></a>Modificare il file app.js
1. Nella directory di progetto hello, aprire hello **app.js** file. Questo file è stato creato in precedenza, quando un'applicazione web hello Express è stata creata.
2. Aggiungere hello seguente codice toohello cima a **app.js**
   
        var DocumentDBClient = require('documentdb').DocumentClient;
        var config = require('./config');
        var TaskList = require('./routes/tasklist');
        var TaskDao = require('./models/taskDao');
3. Questo codice definisce hello toobe di file di configurazione utilizzato e procede valori tooread da questo file in alcune variabili che non appena si utilizzerà.
4. Sostituire hello seguenti due righe in **app.js** file:
   
        app.use('/', index);
        app.use('/users', users); 
   
      con hello frammento di codice seguente:
   
        var docDbClient = new DocumentDBClient(config.host, {
            masterKey: config.authKey
        });
        var taskDao = new TaskDao(docDbClient, config.databaseId, config.collectionId);
        var taskList = new TaskList(taskDao);
        taskDao.init();
   
        app.get('/', taskList.showTasks.bind(taskList));
        app.post('/addtask', taskList.addTask.bind(taskList));
        app.post('/completetask', taskList.completeTask.bind(taskList));
        app.set('view engine', 'jade');
5. Queste righe definiscono una nuova istanza della nostri **TaskDao** oggetto, con un nuovo tooAzure connessione DB Cosmos (utilizzando i valori hello leggere hello **config.js**), inizializzare l'oggetto attività hello e quindi associare azioni modulo toomethods nel nostro **TaskList** controller. 
6. Infine, salvare e chiudere hello **app.js** file, è quasi completata.

## <a name="_Toc395783181"></a>Passaggio 5: Creare un'interfaccia utente
Ora in modo che un utente effettivamente possibile interagire con l'applicazione è possibile attivare l'interfaccia utente di attenzione toobuilding hello. Hello Express applicazione creata utilizza **Jade** come motore di visualizzazione hello. Per ulteriori informazioni su Jade consultare troppo[http://jade-lang.com/](http://jade-lang.com/).

1. Hello **layout.jade** file hello **viste** directory viene utilizzata come modello generale per altri **.jade** file. In questo passaggio è necessario modificarlo toouse [Twitter Bootstrap](https://github.com/twbs/bootstrap), che è un toolkit che rende facile toodesign un sito Web professionale nice. 
2. Aprire hello **layout.jade** file trovato in hello **viste** cartella e sostituire il contenuto di hello con seguenti hello:

    ```
    doctype html
    html
      head
        title= title
        link(rel='stylesheet', href='//ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap.min.css')
        link(rel='stylesheet', href='/stylesheets/style.css')
      body
        nav.navbar.navbar-inverse.navbar-fixed-top
          div.navbar-header
            a.navbar-brand(href='#') My Tasks
        block content
        script(src='//ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.2.min.js')
        script(src='//ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/bootstrap.min.js')
    ```

    Ciò indica in modo efficace hello **Jade** toorender del motore del codice HTML per l'applicazione e crea un **blocco** chiamato **contenuto** in cui sia possibile fornire layout hello per il contenuto numero di pagine.

    Salvare e chiudere il file **layout.jade** .

3. Aprire quindi hello **index.jade** file, la visualizzazione di hello che verrà utilizzato dall'applicazione e sostituirà il contenuto di hello del file hello con hello seguente:
   
        extends layout
        block content
           h1 #{title}
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
                     td #{task.name}
                     td #{task.category}
                     - var date  = new Date(task.date);
                     - var day   = date.getDate();
                     - var month = date.getMonth() + 1;
                     - var year  = date.getFullYear();
                     td #{month + "/" + day + "/" + year}
                     td
                       input(type="checkbox", name="#{task.id}", value="#{!task.completed}", checked=task.completed)
             button.btn.btn-primary(type="submit") Update tasks
           hr
           form.well(action="/addtask", method="post")
             .form-group
               label(for="name") Item Name:
               input.form-control(name="name", type="textbox")
             .form-group
               label(for="category") Item Category:
               input.form-control(name="category", type="textbox")
             br
             button.btn(type="submit") Add item
   

Questo layout estende e vengono forniti contenuti hello **contenuto** segnaposto è stato illustrato in hello **layout.jade** file in precedenza.
   
In questo layout sono stati creati due moduli HTML.

primo form Hello contiene una tabella per i dati e un pulsante che consente di elaborare gli elementi tooupdate inviando troppo**/completetask** metodo per il controller.
    
seconda forma Hello contiene due campi di input e un pulsante che consente di elaborare un nuovo elemento toocreate inviando troppo**/addtask** metodo per il controller.

Deve trattarsi di tutto ciò che è necessario per il nostro toowork dell'applicazione.

## <a name="_Toc395783181"></a>Passaggio 6: Esecuzione dell'applicazione in locale
1. eseguire sul computer locale, un'applicazione hello tootest `npm start` in hello toostart terminal l'applicazione, quindi aggiornare il [http://localhost:3000](http://localhost:3000) pagina nel browser. pagina Hello dovrebbe apparire come hello immagine riportata di seguito:
   
    ![Schermata di hello applicazione MyTodo elenco in una finestra del browser](./media/documentdb-nodejs-application/cosmos-db-node-js-localhost.png)

    > [!TIP]
    > Se si riceve un errore relativo a hello rientro nel file di layout.jade hello o index.jade hello, verificare che hello prime due righe in entrambi i file è giustificato a sinistra, senza spazi. Se sono presenti spazi prima delle prime due righe di hello, rimuoverli, salvare entrambi i file, quindi aggiornare la finestra del browser. 

2. Utilizzare hello articolo, nome dell'elemento e categoria campi tooenter una nuova attività e quindi fare clic su **Aggiungi elemento**. Viene creato un documento in Azure Cosmos DB con queste proprietà. 
3. pagina Hello deve aggiornare hello toodisplay appena creato l'elemento nell'elenco attività hello.
   
    ![Schermata dell'applicazione hello con un nuovo elemento nell'elenco attività hello](./media/documentdb-nodejs-application/cosmos-db-node-js-added-task.png)
4. semplicemente casella di controllo hello nella colonna completo hello toocomplete un'attività e quindi fare clic su **aggiornano le attività**. Questo documento aggiornamenti hello già stato creato.

5. un'applicazione hello toostop, premere CTRL + C nella finestra terminal hello e quindi fare clic su **Y** processo batch di hello tooterminate.

## <a name="_Toc395783182"></a>Passaggio 7: Distribuire il tooAzure di progetto di sviluppo dell'applicazione siti Web
1. Se non è ancora stato fatto, abilitare un repository Git per il sito Web di Azure. È possibile trovare istruzioni su come toodo in hello [tooAzure distribuzione Git locale del servizio App](../app-service-web/app-service-deploy-local-git.md) argomento.
2. Aggiungere il sito Web di Azure come Git remoto.
   
        git remote add azure https://username@your-azure-website.scm.azurewebsites.net:443/your-azure-website.git
3. Distribuire trasferendo toohello remoto.
   
        git push azure master
4. Dopo alcuni secondi, Git completerà la pubblicazione dell'applicazione Web e avvierà un browser in cui sarà possibile visualizzare quanto realizzato in esecuzione in Azure.

    Congratulazioni. Appena creato prima Node.js Express applicazione Web tramite Azure Cosmos DB e pubblicarlo tooAzure siti Web.

    Se si desidera toodownload o fare riferimento applicazione informazioni di riferimento complete toohello per questa esercitazione, può essere scaricato da [GitHub][GitHub].

## <a name="_Toc395637775"></a>Passaggi successivi

* Desidera tooperform scala e test delle prestazioni con Azure Cosmos DB? vedere [Test delle prestazioni e della scalabilità con Azure Cosmos DB](performance-testing.md).
* Informazioni su come troppo[monitorare un account Azure Cosmos DB](monitor-accounts.md).
* Eseguire query su questo set di dati di esempio in hello [Query Playground](https://www.documentdb.com/sql/demo).
* Esplorare hello [documentazione di Azure Cosmos DB](https://docs.microsoft.com/azure/documentdb/).

[Node.js]: http://nodejs.org/
[Git]: http://git-scm.com/
[GitHub]: https://github.com/Azure-Samples/documentdb-node-todo-app

