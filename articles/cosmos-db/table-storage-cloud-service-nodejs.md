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
# <a name="nodejs-web-application-using-storage"></a><span data-ttu-id="74387-103">Creazione di un'applicazione Web Node.js con Archiviazione</span><span class="sxs-lookup"><span data-stu-id="74387-103">Node.js Web Application using Storage</span></span>
## <a name="overview"></a><span data-ttu-id="74387-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="74387-104">Overview</span></span>
<span data-ttu-id="74387-105">In questa esercitazione, hello applicazione creata nel [applicazione Web Node.js mediante Express] esercitazione esteso mediante le librerie Client di hello Microsoft Azure per Node.js toowork con servizi di gestione dati.</span><span class="sxs-lookup"><span data-stu-id="74387-105">In this tutorial, hello application you created in the [Node.js Web Application using Express] tutorial is extended using hello Microsoft Azure Client Libraries for Node.js toowork with data management services.</span></span> <span data-ttu-id="74387-106">Estendere l'applicazione mediante la creazione di un'applicazione elenco attività basate sul web che è possibile distribuire tooAzure.</span><span class="sxs-lookup"><span data-stu-id="74387-106">You extend your application by creating a web-based task-list application that you can deploy tooAzure.</span></span> <span data-ttu-id="74387-107">elenco di attività Hello consente di recuperare le attività, aggiungere nuove attività e contrassegnare l'attività come completata.</span><span class="sxs-lookup"><span data-stu-id="74387-107">hello task list allows a user to retrieve tasks, add new tasks, and mark tasks as completed.</span></span>

<span data-ttu-id="74387-108">gli elementi di attività Hello vengono archiviati in archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="74387-108">hello task items are stored in Azure Storage.</span></span> <span data-ttu-id="74387-109">Archiviazione di Azure consente l'archiviazione di dati non strutturati, a tolleranza di errore e a disponibilità elevata.</span><span class="sxs-lookup"><span data-stu-id="74387-109">Azure Storage provides unstructured data storage that is fault-tolerant and highly available.</span></span> <span data-ttu-id="74387-110">Archiviazione di Azure include varie strutture di dati in cui è possibile archiviare i dati e da cui è possibile accedere ad essi.</span><span class="sxs-lookup"><span data-stu-id="74387-110">Azure Storage includes several data structures where you can store and access data.</span></span> <span data-ttu-id="74387-111">È possibile utilizzare servizi di archiviazione hello da hello API incluse in hello Azure SDK per Node.js o tramite le API REST.</span><span class="sxs-lookup"><span data-stu-id="74387-111">You can use hello storage services from hello APIs included in hello Azure SDK for Node.js or via REST APIs.</span></span> <span data-ttu-id="74387-112">Per ulteriori informazioni, vedere [Archiviazione e accesso ai dati in Azure].</span><span class="sxs-lookup"><span data-stu-id="74387-112">For more information, see [Storing and Accessing Data in Azure].</span></span>

<span data-ttu-id="74387-113">In questa esercitazione si presuppone che siano state completate hello [applicazione Web Node.js] e [Node.js con Express][applicazione Web Node.js mediante Express] esercitazioni.</span><span class="sxs-lookup"><span data-stu-id="74387-113">This tutorial assumes that you have completed hello [Node.js Web Application] and [Node.js with Express][Node.js Web Application using Express] tutorials.</span></span>

<span data-ttu-id="74387-114">Contiene hello le seguenti informazioni:</span><span class="sxs-lookup"><span data-stu-id="74387-114">It contains hello following information:</span></span>

* <span data-ttu-id="74387-115">Come toowork con hello motore del modello Jade</span><span class="sxs-lookup"><span data-stu-id="74387-115">How toowork with hello Jade template engine</span></span>
* <span data-ttu-id="74387-116">Come toowork con i servizi di gestione dati di Azure</span><span class="sxs-lookup"><span data-stu-id="74387-116">How toowork with Azure Data Management services</span></span>

<span data-ttu-id="74387-117">Hello seguente schermata mostra un'applicazione hello completata:</span><span class="sxs-lookup"><span data-stu-id="74387-117">hello following screenshot shows hello completed application:</span></span>

![Hello completata la pagina web in internet explorer](./media/table-storage-cloud-service-nodejs/getting-started-1.png)

## <a name="setting-storage-credentials-in-webconfig"></a><span data-ttu-id="74387-119">Impostazione delle credenziali di archiviazione in Web.Config</span><span class="sxs-lookup"><span data-stu-id="74387-119">Setting Storage Credentials in Web.Config</span></span>
<span data-ttu-id="74387-120">È necessario passare le credenziali di archiviazione tooaccess di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="74387-120">You must pass in storage credentials tooaccess Azure Storage.</span></span> <span data-ttu-id="74387-121">Questa operazione viene eseguita utilizzando le impostazioni dell'applicazione Web. config hello.</span><span class="sxs-lookup"><span data-stu-id="74387-121">This is done by utilizing hello web.config application settings.</span></span>
<span data-ttu-id="74387-122">le impostazioni di Web. config Hello vengono passate come tooNode variabili di ambiente, che vengono quindi letti da hello Azure SDK.</span><span class="sxs-lookup"><span data-stu-id="74387-122">hello web.config settings are passed as environment variables tooNode, which are then read by hello Azure SDK.</span></span>

> [!NOTE]
> <span data-ttu-id="74387-123">Le credenziali di archiviazione vengono utilizzate solo quando un'applicazione hello è tooAzure distribuito.</span><span class="sxs-lookup"><span data-stu-id="74387-123">Storage credentials are only used when hello application is deployed tooAzure.</span></span> <span data-ttu-id="74387-124">Quando in esecuzione nell'emulatore di hello, un'applicazione hello Usa emulatore di archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="74387-124">When running in hello emulator, hello application uses hello storage emulator.</span></span>
>
>

<span data-ttu-id="74387-125">Eseguire hello seguente credenziali dell'account di archiviazione di passaggi tooretrieve hello e aggiungerli toohello le impostazioni di Web. config:</span><span class="sxs-lookup"><span data-stu-id="74387-125">Perform hello following steps tooretrieve hello storage account credentials and add them toohello web.config settings:</span></span>

1. <span data-ttu-id="74387-126">Se non è già aperto, avviare hello Azure PowerShell da hello **avviare** menu espandendo **tutti i programmi, Azure**, fare doppio clic su **Azure PowerShell**, quindi selezionare  **Esegui come amministratore**.</span><span class="sxs-lookup"><span data-stu-id="74387-126">If it is not already open, start hello Azure PowerShell from hello **Start** menu by expanding **All Programs, Azure**, right-click **Azure PowerShell**, and then select **Run As Administrator**.</span></span>
2. <span data-ttu-id="74387-127">Cambia cartella toohello directory contenente l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="74387-127">Change directories toohello folder containing your application.</span></span> <span data-ttu-id="74387-128">Ad esempio, C:\\node\\tasklist\\WebRole1.</span><span class="sxs-lookup"><span data-stu-id="74387-128">For example, C:\\node\\tasklist\\WebRole1.</span></span>
3. <span data-ttu-id="74387-129">Dalla finestra di Powershell Azure hello, immettere hello seguenti informazioni sull'account di archiviazione di cmdlet tooretrieve hello:</span><span class="sxs-lookup"><span data-stu-id="74387-129">From hello Azure Powershell window, enter hello following cmdlet tooretrieve hello storage account information:</span></span>

    ```powershell
    PS C:\node\tasklist\WebRole1> Get-AzureStorageAccounts
    ```

   <span data-ttu-id="74387-130">Hello cmdlet precedente recupera hello elenco di account di archiviazione e le chiavi dell'account associate al servizio ospitato.</span><span class="sxs-lookup"><span data-stu-id="74387-130">hello preceding cmdlet retrieves hello list of storage accounts and account keys associated with your hosted service.</span></span>

   > [!NOTE]
   > <span data-ttu-id="74387-131">Poiché hello Azure SDK consente di creare un account di archiviazione quando si distribuisce un servizio, un account di archiviazione deve essere già esistente dalla distribuzione dell'applicazione nelle guide precedenti hello.</span><span class="sxs-lookup"><span data-stu-id="74387-131">Since hello Azure SDK creates a storage account when you deploy a service, a storage account should already exist from deploying your application in hello previous guides.</span></span>
   >
   >
4. <span data-ttu-id="74387-132">Aprire hello **Servicedefinition** file contenenti le impostazioni di ambiente hello che vengono utilizzate quando un'applicazione hello tooAzure distribuito:</span><span class="sxs-lookup"><span data-stu-id="74387-132">Open hello **ServiceDefinition.csdef** file containing hello environment settings that are used when hello application is deployed tooAzure:</span></span>

    ```powershell
    PS C:\node\tasklist> notepad ServiceDefinition.csdef
    ```

5. <span data-ttu-id="74387-133">Seguente hello Inserisci bloccare in **ambiente** elemento, sostituendo con i propri {ACCOUNT di archiviazione di} e {chiave di accesso di archiviazione} con il nome di account hello e chiave primaria di hello per account di archiviazione hello da toouse per la distribuzione:</span><span class="sxs-lookup"><span data-stu-id="74387-133">Insert hello following block under **Environment** element, substituting {STORAGE ACCOUNT} and {STORAGE ACCESS KEY} with hello account name and hello primary key for hello storage account you want toouse for deployment:</span></span>

  <Variable name="AZURE_STORAGE_ACCOUNT" value="{STORAGE ACCOUNT}" />
  <Variable name="AZURE_STORAGE_ACCESS_KEY" value="{STORAGE ACCESS KEY}" />

   ![contenuto del file Hello web.cloud.config](./media/table-storage-cloud-service-nodejs/node37.png)

6. <span data-ttu-id="74387-135">Salvare il file hello e chiudere il blocco note.</span><span class="sxs-lookup"><span data-stu-id="74387-135">Save hello file and close notepad.</span></span>

### <a name="install-additional-modules"></a><span data-ttu-id="74387-136">Installare moduli aggiuntivi</span><span class="sxs-lookup"><span data-stu-id="74387-136">Install additional modules</span></span>
1. <span data-ttu-id="74387-137">Hello utilizzo successivo comando tooinstall hello [azure], [nodo-uuid], [nconf] e [asincrona] moduli in locale, nonché a toosave una voce relativa toohello **package. JSON** file:</span><span class="sxs-lookup"><span data-stu-id="74387-137">Use hello following command tooinstall hello [azure], [node-uuid], [nconf] and [async] modules locally as well as toosave an entry for them toohello **package.json** file:</span></span>

  ```powershell
  PS C:\node\tasklist\WebRole1> npm install azure-storage node-uuid async nconf --save
  ```

  <span data-ttu-id="74387-138">output di Hello di questo comando risulterà simile toohello seguenti:</span><span class="sxs-lookup"><span data-stu-id="74387-138">hello output of this command should appear similar toohello following:</span></span>

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

## <a name="using-hello-table-service-in-a-node-application"></a><span data-ttu-id="74387-139">Utilizzo del servizio tabelle hello in un'applicazione di nodo</span><span class="sxs-lookup"><span data-stu-id="74387-139">Using hello Table service in a node application</span></span>
<span data-ttu-id="74387-140">In questa sezione, hello base dell'applicazione creato da hello **express** comando verrà esteso mediante l'aggiunta di un **task.js** file contenente il modello di hello per le attività.</span><span class="sxs-lookup"><span data-stu-id="74387-140">In this section, hello basic application created by hello **express** command is extended by adding a **task.js** file containing hello model for your tasks.</span></span> <span data-ttu-id="74387-141">Modificare hello esistente **app.js** file e creare un nuovo **tasklist.js** file che utilizza il modello di hello.</span><span class="sxs-lookup"><span data-stu-id="74387-141">Modify hello existing **app.js** file and create a new **tasklist.js** file that uses hello model.</span></span>

### <a name="create-hello-model"></a><span data-ttu-id="74387-142">Creare il modello di hello</span><span class="sxs-lookup"><span data-stu-id="74387-142">Create hello model</span></span>
1. <span data-ttu-id="74387-143">In hello **WebRole1** directory, creare una nuova directory denominata **modelli**.</span><span class="sxs-lookup"><span data-stu-id="74387-143">In hello **WebRole1** directory, create a new directory named **models**.</span></span>
2. <span data-ttu-id="74387-144">In hello **modelli** directory, creare un nuovo file denominato **task.js**.</span><span class="sxs-lookup"><span data-stu-id="74387-144">In hello **models** directory, create a new file named **task.js**.</span></span> <span data-ttu-id="74387-145">Questo file contiene il modello di hello per le operazioni di hello create dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="74387-145">This file contains hello model for hello tasks created by your application.</span></span>
3. <span data-ttu-id="74387-146">All'inizio di hello di hello **task.js** file, aggiungere hello tooreference richiesto dalle librerie di codice seguente:</span><span class="sxs-lookup"><span data-stu-id="74387-146">At hello beginning of hello **task.js** file, add hello following code tooreference required libraries:</span></span>

    ```nodejs
    var azure = require('azure-storage');
    var uuid = require('node-uuid');
    var entityGen = azure.TableUtilities.entityGenerator;
    ```

4. <span data-ttu-id="74387-147">Successivamente, aggiungere codice toodefine ed esportare l'oggetto attività hello.</span><span class="sxs-lookup"><span data-stu-id="74387-147">Next, add code toodefine and export hello Task object.</span></span> <span data-ttu-id="74387-148">oggetto attività Hello è responsabile per la connessione toohello tabella.</span><span class="sxs-lookup"><span data-stu-id="74387-148">hello Task object is responsible for connecting toohello table.</span></span>

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

5. <span data-ttu-id="74387-149">Successivamente, aggiungere hello seguito metodi aggiuntivi di codice toodefine nell'oggetto attività hello, che consentono le interazioni con i dati archiviati nella tabella hello:</span><span class="sxs-lookup"><span data-stu-id="74387-149">Next, add hello following code toodefine additional methods on hello Task object, which allow interactions with data stored in hello table:</span></span>

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

6. <span data-ttu-id="74387-150">Salvare e chiudere hello **task.js** file.</span><span class="sxs-lookup"><span data-stu-id="74387-150">Save and close hello **task.js** file.</span></span>

### <a name="create-hello-controller"></a><span data-ttu-id="74387-151">Creare controller hello</span><span class="sxs-lookup"><span data-stu-id="74387-151">Create hello controller</span></span>
1. <span data-ttu-id="74387-152">In hello **WebRole1/route** directory, creare un nuovo file denominato **tasklist.js** e aprirlo in un editor di testo.</span><span class="sxs-lookup"><span data-stu-id="74387-152">In hello **WebRole1/routes** directory, create a new file named **tasklist.js** and open it in a text editor.</span></span>
2. <span data-ttu-id="74387-153">Aggiungere hello seguente codice troppo**tasklist.js**.</span><span class="sxs-lookup"><span data-stu-id="74387-153">Add hello following code too**tasklist.js**.</span></span> <span data-ttu-id="74387-154">Questo codice carica hello azure e moduli asincrono, che vengono utilizzati da **tasklist.js** e definisce hello **TaskList** funzione, che viene passata un'istanza di hello **attività** è l'oggetto definito in precedenza:</span><span class="sxs-lookup"><span data-stu-id="74387-154">This code loads hello azure and async modules, which are used by **tasklist.js** and defines hello **TaskList** function, which is passed an instance of hello **Task** object we defined earlier:</span></span>

    ```nodejs
    var azure = require('azure-storage');
    var async = require('async');

    module.exports = TaskList;

    function TaskList(task) {
      this.task = task;
    }
    ```

3. <span data-ttu-id="74387-155">Continuare ad aggiungere toohello **tasklist.js** file mediante l'aggiunta di metodi hello troppo**showTasks**, **addTask**, e **completeTasks**:</span><span class="sxs-lookup"><span data-stu-id="74387-155">Continue adding toohello **tasklist.js** file by adding hello methods used too**showTasks**, **addTask**, and **completeTasks**:</span></span>

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

4. <span data-ttu-id="74387-156">Salvare hello **tasklist.js** file.</span><span class="sxs-lookup"><span data-stu-id="74387-156">Save hello **tasklist.js** file.</span></span>

### <a name="modify-appjs"></a><span data-ttu-id="74387-157">Modificare il file app.js</span><span class="sxs-lookup"><span data-stu-id="74387-157">Modify app.js</span></span>
1. <span data-ttu-id="74387-158">In hello **WebRole1** hello directory, aprire **app.js** file in un editor di testo.</span><span class="sxs-lookup"><span data-stu-id="74387-158">In hello **WebRole1** directory, open hello **app.js** file in a text editor.</span></span>
2. <span data-ttu-id="74387-159">Inizio hello del file hello, aggiungere hello seguente modulo hello azure tooload e impostare la chiave di nome e una partizione di tabella hello:</span><span class="sxs-lookup"><span data-stu-id="74387-159">At hello beginning of hello file, add hello following tooload hello azure module and set hello table name and partition key:</span></span>

    ```nodejs
    var azure = require('azure-storage');
    var tableName = 'tasks';
    var partitionKey = 'hometasks';
    ```

3. <span data-ttu-id="74387-160">Nel file app.js hello, scorrere verso il basso toowhere vedrai hello la seguente riga:</span><span class="sxs-lookup"><span data-stu-id="74387-160">In hello app.js file, scroll down toowhere you see hello following line:</span></span>

    ```nodejs
    app.use('/', routes);
    app.use('/users', users);
    ```

    <span data-ttu-id="74387-161">Sostituire hello precedenti righe con hello seguente codice.</span><span class="sxs-lookup"><span data-stu-id="74387-161">Replace hello preceding lines with hello following code.</span></span> <span data-ttu-id="74387-162">Questo codice Inizializza un'istanza di <strong>attività</strong> con un account di archiviazione tooyour di connessione.</span><span class="sxs-lookup"><span data-stu-id="74387-162">This code initializes an instance of <strong>Task</strong> with a connection tooyour storage account.</span></span> <span data-ttu-id="74387-163">Hello <strong>attività</strong> viene passato toohello <strong>TaskList</strong>, che utilizza toocommunicate con servizio tabella hello:</span><span class="sxs-lookup"><span data-stu-id="74387-163">hello <strong>Task</strong> is passed toohello <strong>TaskList</strong>, which uses it toocommunicate with hello Table service:</span></span>

    ```nodejs
    var TaskList = require('./routes/tasklist');
    var Task = require('./models/task');
    var task = new Task(azure.createTableService(), tableName, partitionKey);
    var taskList = new TaskList(task);

    app.get('/', taskList.showTasks.bind(taskList));
    app.post('/addtask', taskList.addTask.bind(taskList));
    app.post('/completetask', taskList.completeTask.bind(taskList));
    ```

4. <span data-ttu-id="74387-164">Salvare hello **app.js** file.</span><span class="sxs-lookup"><span data-stu-id="74387-164">Save hello **app.js** file.</span></span>

### <a name="modify-hello-index-view"></a><span data-ttu-id="74387-165">Modifica visualizzazione dell'indice hello</span><span class="sxs-lookup"><span data-stu-id="74387-165">Modify hello index view</span></span>
1. <span data-ttu-id="74387-166">Modificare le directory toohello **viste** hello directory e aprire **index.jade** file in un editor di testo.</span><span class="sxs-lookup"><span data-stu-id="74387-166">Change directories toohello **views** directory and open hello **index.jade** file in a text editor.</span></span>
2. <span data-ttu-id="74387-167">Sostituire il contenuto di hello di hello **index.jade** file con hello seguente codice.</span><span class="sxs-lookup"><span data-stu-id="74387-167">Replace hello contents of hello **index.jade** file with hello following code.</span></span> <span data-ttu-id="74387-168">Questo codice definisce la visualizzazione hello per le attività esistenti e un modulo per l'aggiunta di nuove attività e contrassegnare esistenti come completata.</span><span class="sxs-lookup"><span data-stu-id="74387-168">This code defines hello view for displaying existing tasks, and defines a form for adding new tasks and marking existing ones as completed.</span></span>

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

3. <span data-ttu-id="74387-169">Salvare e chiudere il file **index.jade** .</span><span class="sxs-lookup"><span data-stu-id="74387-169">Save and close **index.jade** file.</span></span>

### <a name="modify-hello-global-layout"></a><span data-ttu-id="74387-170">Modifica layout globale hello</span><span class="sxs-lookup"><span data-stu-id="74387-170">Modify hello global layout</span></span>
<span data-ttu-id="74387-171">Hello **layout.jade** file hello **viste** directory viene utilizzata come modello generale per altri **.jade** file.</span><span class="sxs-lookup"><span data-stu-id="74387-171">hello **layout.jade** file in hello **views** directory is used as a global template for other **.jade** files.</span></span> <span data-ttu-id="74387-172">In questo passaggio, modificare hello **layout.jade** file toouse [Twitter Bootstrap](https://github.com/twbs/bootstrap), che è un toolkit che rende facile toodesign un sito Web professionale nice.</span><span class="sxs-lookup"><span data-stu-id="74387-172">In this step, modify hello **layout.jade** file toouse [Twitter Bootstrap](https://github.com/twbs/bootstrap), which is a toolkit that makes it easy toodesign a nice looking website.</span></span>

1. <span data-ttu-id="74387-173">Scaricare ed estrarre file hello per [Twitter Bootstrap](http://getbootstrap.com/).</span><span class="sxs-lookup"><span data-stu-id="74387-173">Download and extract hello files for [Twitter Bootstrap](http://getbootstrap.com/).</span></span> <span data-ttu-id="74387-174">Hello copia **bootstrap.min.css** file hello **bootstrap\\dist\\css** cartella toohello **pubblica\\fogli di stile** directory dell'applicazione elenco attività.</span><span class="sxs-lookup"><span data-stu-id="74387-174">Copy hello **bootstrap.min.css** file from hello **bootstrap\\dist\\css** folder toohello **public\\stylesheets** directory of your tasklist application.</span></span>
2. <span data-ttu-id="74387-175">Da hello **viste** cartella, aprire hello **layout.jade** file nell'editor di testo e sostituire il contenuto di hello con hello seguente:</span><span class="sxs-lookup"><span data-stu-id="74387-175">From hello **views** folder, open hello **layout.jade** file in your text editor and replace hello contents with hello following:</span></span>

    <span data-ttu-id="74387-176">doctype html  html    head      title= title      link(rel='stylesheet', href='/stylesheets/bootstrap.min.css')      link(rel='stylesheet', href='/stylesheets/style.css')    body.app      nav.navbar.navbar-default        div.navbar-header          a.navbar-brand(href='/') My Tasks      block content</span><span class="sxs-lookup"><span data-stu-id="74387-176">doctype html  html    head      title= title      link(rel='stylesheet', href='/stylesheets/bootstrap.min.css')      link(rel='stylesheet', href='/stylesheets/style.css')    body.app      nav.navbar.navbar-default        div.navbar-header          a.navbar-brand(href='/') My Tasks      block content</span></span>

3. <span data-ttu-id="74387-177">Salvare hello **layout.jade** file.</span><span class="sxs-lookup"><span data-stu-id="74387-177">Save hello **layout.jade** file.</span></span>

### <a name="running-hello-application-in-hello-emulator"></a><span data-ttu-id="74387-178">Esecuzione dell'applicazione hello in hello emulatore</span><span class="sxs-lookup"><span data-stu-id="74387-178">Running hello Application in hello Emulator</span></span>
<span data-ttu-id="74387-179">Utilizzare hello seguito comando toostart hello applicazione nell'emulatore hello.</span><span class="sxs-lookup"><span data-stu-id="74387-179">Use hello following command toostart hello application in hello emulator.</span></span>

```powershell
PS C:\node\tasklist\WebRole1> start-azureemulator -launch
```

<span data-ttu-id="74387-180">browser Hello verrà visualizzato hello pagina seguente:</span><span class="sxs-lookup"><span data-stu-id="74387-180">hello browser opens and displays hello following page:</span></span>

![Un sito web di paging denominato elenco di attività personali con una tabella contenente le attività e i campi tooadd una nuova attività.](./media/table-storage-cloud-service-nodejs/node44.png)

<span data-ttu-id="74387-182">Utilizzare elementi del modulo di hello tooadd o rimuovere elementi esistenti, contrassegnandoli come completata.</span><span class="sxs-lookup"><span data-stu-id="74387-182">Use hello form tooadd items, or remove existing items by marking them as completed.</span></span>

## <a name="publishing-hello-application-tooazure"></a><span data-ttu-id="74387-183">Pubblicazione hello applicazione tooAzure</span><span class="sxs-lookup"><span data-stu-id="74387-183">Publishing hello Application tooAzure</span></span>
<span data-ttu-id="74387-184">Nella finestra di Windows PowerShell hello, chiamare hello seguente cmdlet tooredeploy tooAzure il servizio ospitato.</span><span class="sxs-lookup"><span data-stu-id="74387-184">In hello Windows PowerShell window, call hello following cmdlet tooredeploy your hosted service tooAzure.</span></span>

```powershell
PS C:\node\tasklist\WebRole1> Publish-AzureServiceProject -name myuniquename -location datacentername -launch
```

<span data-ttu-id="74387-185">Sostituire **myuniquename** con un nome univoco per questa applicazione.</span><span class="sxs-lookup"><span data-stu-id="74387-185">Replace **myuniquename** with a unique name for this application.</span></span> <span data-ttu-id="74387-186">Sostituire **datacentername** con nome hello del data center di Azure, ad esempio **Stati Uniti occidentali**.</span><span class="sxs-lookup"><span data-stu-id="74387-186">Replace **datacentername** with hello name of an Azure data center, such as **West US**.</span></span>

<span data-ttu-id="74387-187">Una volta completata la distribuzione di hello, vedrai un seguente toohello simile risposta:</span><span class="sxs-lookup"><span data-stu-id="74387-187">After hello deployment is complete, you should see a response similar toohello following:</span></span>

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

<span data-ttu-id="74387-188">Specificando hello **-avviare** opzione hello cmdlet precedente, il browser hello aprirà e visualizzerà l'applicazione in esecuzione in Azure quando viene completata la pubblicazione.</span><span class="sxs-lookup"><span data-stu-id="74387-188">By specifying hello **-launch** option in hello previous cmdlet, hello browser opens and displays your application running in Azure when publishing is completed.</span></span>

![Visualizzazione della pagina di elenco di attività personali hello una finestra del browser.](./media/table-storage-cloud-service-nodejs/getting-started-1.png)

## <a name="stopping-and-deleting-your-application"></a><span data-ttu-id="74387-191">Arresto ed eliminazione dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="74387-191">Stopping and Deleting Your Application</span></span>
<span data-ttu-id="74387-192">Dopo aver distribuito l'applicazione, è opportuno toodisable in modo da evitare i costi o compilare e distribuire applicazioni all'interno di hello gratuitamente periodo di tempo di valutazione.</span><span class="sxs-lookup"><span data-stu-id="74387-192">After deploying your application, you may want toodisable it so you can avoid costs or build and deploy other applications within hello free trial time period.</span></span>

<span data-ttu-id="74387-193">Azure addebita le istanze del ruolo Web al consumo, in base all'utilizzo di tempo del server su base oraria.</span><span class="sxs-lookup"><span data-stu-id="74387-193">Azure bills web role instances per hour of server time consumed.</span></span>
<span data-ttu-id="74387-194">Ora del server viene utilizzata una volta distribuita l'applicazione, anche se le istanze non sono in esecuzione e si trovano nello stato arrestato hello.</span><span class="sxs-lookup"><span data-stu-id="74387-194">Server time is consumed once your application is deployed, even if the instances are not running and are in hello stopped state.</span></span>

<span data-ttu-id="74387-195">Hello passaggi seguenti viene illustrato come toostop ed eliminare l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="74387-195">hello following steps show you how toostop and delete your application.</span></span>

1. <span data-ttu-id="74387-196">Nella finestra di Windows PowerShell hello, arrestare la distribuzione del servizio hello creata nella sezione precedente di hello con hello seguente cmdlet:</span><span class="sxs-lookup"><span data-stu-id="74387-196">In hello Windows PowerShell window, stop hello service deployment created in hello previous section with hello following cmdlet:</span></span>

    ```powershell
    PS C:\node\tasklist\WebRole1> Stop-AzureService
    ```

   <span data-ttu-id="74387-197">L'arresto del servizio hello potrebbe richiedere alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="74387-197">Stopping hello service may take several minutes.</span></span> <span data-ttu-id="74387-198">Quando il servizio hello viene arrestato, viene visualizzato un messaggio che indica che è stato arrestato.</span><span class="sxs-lookup"><span data-stu-id="74387-198">When hello service is stopped, you receive a message indicating that it has stopped.</span></span>

2. <span data-ttu-id="74387-199">servizio di hello toodelete, hello chiamata seguente cmdlet:</span><span class="sxs-lookup"><span data-stu-id="74387-199">toodelete hello service, call hello following cmdlet:</span></span>

    ```powershell
    PS C:\node\tasklist\WebRole1> Remove-AzureService contosotasklist
    ```

   <span data-ttu-id="74387-200">Quando richiesto, immettere **Y** servizio hello toodelete.</span><span class="sxs-lookup"><span data-stu-id="74387-200">When prompted, enter **Y** toodelete hello service.</span></span>

   <span data-ttu-id="74387-201">Eliminazione del servizio hello potrebbe richiedere alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="74387-201">Deleting hello service may take several minutes.</span></span> <span data-ttu-id="74387-202">Una volta eliminato il servizio di hello, si riceverà un messaggio che indica che il servizio di hello è stato eliminato.</span><span class="sxs-lookup"><span data-stu-id="74387-202">After hello service is deleted, you will receive a message indicating that hello service was deleted.</span></span>

[applicazione Web Node.js mediante Express]: http://azure.microsoft.com/develop/nodejs/tutorials/web-app-with-express/
[Archiviazione e accesso ai dati in Azure]: http://msdn.microsoft.com/library/azure/gg433040.aspx
[applicazione Web Node.js]: http://azure.microsoft.com/develop/nodejs/tutorials/getting-started/


