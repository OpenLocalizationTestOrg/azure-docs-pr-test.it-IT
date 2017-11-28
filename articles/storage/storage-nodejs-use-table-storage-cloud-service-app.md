---
title: app aaaWeb con archiviazione tabella (Node.js) | Documenti Microsoft
description: Esercitazione si basa su hello App Web con l'esercitazione di Express e aggiunta di servizi di archiviazione di Azure e hello modulo Azure.
services: cloud-services, storage
documentationcenter: nodejs
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: e90959a2-4cb2-4b19-9bfb-aede15b18b1c
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: 4eba16f09f8b69cbc135d097e6ca71e08b33733c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="nodejs-web-application-using-storage"></a><span data-ttu-id="e07e4-103">Creazione di un'applicazione Web Node.js con Archiviazione</span><span class="sxs-lookup"><span data-stu-id="e07e4-103">Node.js Web Application using Storage</span></span>
## <a name="overview"></a><span data-ttu-id="e07e4-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="e07e4-104">Overview</span></span>
<span data-ttu-id="e07e4-105">In questa esercitazione verrà creata in un'applicazione hello esteso il [applicazione Web Node.js mediante Express] esercitazione tramite le librerie Client di hello Microsoft Azure per Node.js toowork con servizi di gestione dati.</span><span class="sxs-lookup"><span data-stu-id="e07e4-105">In this tutorial, you will extend hello application created in the [Node.js Web Application using Express] tutorial by using hello Microsoft Azure Client Libraries for Node.js toowork with data management services.</span></span> <span data-ttu-id="e07e4-106">Sarà possibile estendere l'applicazione toocreate un'applicazione elenco attività basate sul web che è possibile distribuire tooAzure.</span><span class="sxs-lookup"><span data-stu-id="e07e4-106">You will extend your application toocreate a web-based task-list application that you can deploy tooAzure.</span></span> <span data-ttu-id="e07e4-107">elenco di attività Hello consente di recuperare le attività, aggiungere nuove attività e contrassegnare l'attività come completata.</span><span class="sxs-lookup"><span data-stu-id="e07e4-107">hello task list allows a user to retrieve tasks, add new tasks, and mark tasks as completed.</span></span>

<span data-ttu-id="e07e4-108">gli elementi di attività Hello vengono archiviati in archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="e07e4-108">hello task items are stored in Azure Storage.</span></span> <span data-ttu-id="e07e4-109">Archiviazione di Azure consente l'archiviazione di dati non strutturati, a tolleranza di errore e a disponibilità elevata.</span><span class="sxs-lookup"><span data-stu-id="e07e4-109">Azure Storage provides unstructured data storage that is fault-tolerant and highly available.</span></span> <span data-ttu-id="e07e4-110">Archiviazione di Azure include diverse strutture di dati in cui è possibile archiviare e accedere ai dati e si possono utilizzare servizi di archiviazione hello da hello API incluse in hello Azure SDK per Node.js o tramite le API REST.</span><span class="sxs-lookup"><span data-stu-id="e07e4-110">Azure Storage includes several data structures where you can store and access data, and you can leverage hello storage services from hello APIs included in hello Azure SDK for Node.js or via REST APIs.</span></span> <span data-ttu-id="e07e4-111">Per ulteriori informazioni, vedere [Archiviazione e accesso ai dati in Azure].</span><span class="sxs-lookup"><span data-stu-id="e07e4-111">For more information, see [Storing and Accessing Data in Azure].</span></span>

<span data-ttu-id="e07e4-112">In questa esercitazione si presuppone che siano state completate hello [applicazione Web Node.js] e [Node.js con Express][applicazione Web Node.js mediante Express] esercitazioni.</span><span class="sxs-lookup"><span data-stu-id="e07e4-112">This tutorial assumes that you have completed hello [Node.js Web Application] and [Node.js with Express][Node.js Web Application using Express] tutorials.</span></span>

<span data-ttu-id="e07e4-113">Si acquisiranno le nozioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="e07e4-113">You will learn:</span></span>

* <span data-ttu-id="e07e4-114">Come toowork con hello motore del modello Jade</span><span class="sxs-lookup"><span data-stu-id="e07e4-114">How toowork with hello Jade template engine</span></span>
* <span data-ttu-id="e07e4-115">Come toowork con i servizi di gestione dati di Azure</span><span class="sxs-lookup"><span data-stu-id="e07e4-115">How toowork with Azure Data Management services</span></span>

<span data-ttu-id="e07e4-116">Di seguito viene riportata una schermata dell'applicazione hello completata:</span><span class="sxs-lookup"><span data-stu-id="e07e4-116">A screenshot of hello completed application is below:</span></span>

![Hello completata la pagina web in internet explorer](./media/storage-nodejs-use-table-storage-cloud-service-app/getting-started-1.png)

## <a name="setting-storage-credentials-in-webconfig"></a><span data-ttu-id="e07e4-118">Impostazione delle credenziali di archiviazione in Web.Config</span><span class="sxs-lookup"><span data-stu-id="e07e4-118">Setting Storage Credentials in Web.Config</span></span>
<span data-ttu-id="e07e4-119">tooaccess archiviazione di Azure, è necessario toopass in credenziali di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="e07e4-119">tooaccess Azure Storage, you need toopass in storage credentials.</span></span> <span data-ttu-id="e07e4-120">toodo, si utilizzano le impostazioni dell'applicazione Web. config.</span><span class="sxs-lookup"><span data-stu-id="e07e4-120">toodo this, you utilize web.config application settings.</span></span>
<span data-ttu-id="e07e4-121">Tali impostazioni verranno passate come tooNode variabili di ambiente, che vengono quindi letti da hello Azure SDK.</span><span class="sxs-lookup"><span data-stu-id="e07e4-121">Those settings will be passed as environment variables tooNode, which are then read by hello Azure SDK.</span></span>

> [!NOTE]
> <span data-ttu-id="e07e4-122">Le credenziali di archiviazione vengono utilizzate solo quando un'applicazione hello è tooAzure distribuito.</span><span class="sxs-lookup"><span data-stu-id="e07e4-122">Storage credentials are only used when hello application is deployed tooAzure.</span></span> <span data-ttu-id="e07e4-123">Quando in esecuzione nell'emulatore hello, un'applicazione hello utilizzerà l'emulatore di archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="e07e4-123">When running in hello emulator, hello application will use hello storage emulator.</span></span>
>
>

<span data-ttu-id="e07e4-124">Eseguire hello seguente credenziali dell'account di archiviazione di passaggi tooretrieve hello e aggiungerli toohello le impostazioni di Web. config:</span><span class="sxs-lookup"><span data-stu-id="e07e4-124">Perform hello following steps tooretrieve hello storage account credentials and add them toohello web.config settings:</span></span>

1. <span data-ttu-id="e07e4-125">Se non è già aperto, avviare hello Azure PowerShell da hello **avviare** menu espandendo **tutti i programmi, Azure**, fare doppio clic su **Azure PowerShell**, quindi selezionare  **Esegui come amministratore**.</span><span class="sxs-lookup"><span data-stu-id="e07e4-125">If it is not already open, start hello Azure PowerShell from hello **Start** menu by expanding **All Programs, Azure**, right-click **Azure PowerShell**, and then select **Run As Administrator**.</span></span>
2. <span data-ttu-id="e07e4-126">Cambia cartella toohello directory contenente l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="e07e4-126">Change directories toohello folder containing your application.</span></span> <span data-ttu-id="e07e4-127">Ad esempio, C:\\node\\tasklist\\WebRole1.</span><span class="sxs-lookup"><span data-stu-id="e07e4-127">For example, C:\\node\\tasklist\\WebRole1.</span></span>
3. <span data-ttu-id="e07e4-128">Dalla finestra di Powershell Azure hello immettere hello seguenti informazioni sull'account di archiviazione di cmdlet tooretrieve hello:</span><span class="sxs-lookup"><span data-stu-id="e07e4-128">From hello Azure Powershell window enter hello following cmdlet tooretrieve hello storage account information:</span></span>

    ```powershell
    PS C:\node\tasklist\WebRole1> Get-AzureStorageAccounts
    ```

   <span data-ttu-id="e07e4-129">Consente di recuperare elenco hello di account di archiviazione e l'account di chiavi associato al servizio ospitato.</span><span class="sxs-lookup"><span data-stu-id="e07e4-129">This retrieves hello list of storage accounts and account keys associated with your hosted service.</span></span>

   > [!NOTE]
   > <span data-ttu-id="e07e4-130">Poiché hello Azure SDK consente di creare un account di archiviazione quando si distribuisce un servizio, un account di archiviazione deve essere già esistente dalla distribuzione dell'applicazione nelle guide precedenti hello.</span><span class="sxs-lookup"><span data-stu-id="e07e4-130">Since hello Azure SDK creates a storage account when you deploy a service, a storage account should already exist from deploying your application in hello previous guides.</span></span>
   >
   >
4. <span data-ttu-id="e07e4-131">Aprire hello **Servicedefinition** file contenenti le impostazioni di ambiente hello che vengono utilizzate quando un'applicazione hello tooAzure distribuito:</span><span class="sxs-lookup"><span data-stu-id="e07e4-131">Open hello **ServiceDefinition.csdef** file containing hello environment settings that are used when hello application is deployed tooAzure:</span></span>

    ```powershell
    PS C:\node\tasklist> notepad ServiceDefinition.csdef
    ```

5. <span data-ttu-id="e07e4-132">Seguente hello Inserisci bloccare in **ambiente** elemento, sostituendo con i propri {ACCOUNT di archiviazione di} e {chiave di accesso di archiviazione} con il nome di account hello e chiave primaria di hello per account di archiviazione hello da toouse per la distribuzione:</span><span class="sxs-lookup"><span data-stu-id="e07e4-132">Insert hello following block under **Environment** element, substituting {STORAGE ACCOUNT} and {STORAGE ACCESS KEY} with hello account name and hello primary key for hello storage account you want toouse for deployment:</span></span>

  <Variable name="AZURE_STORAGE_ACCOUNT" value="{STORAGE ACCOUNT}" />
  <Variable name="AZURE_STORAGE_ACCESS_KEY" value="{STORAGE ACCESS KEY}" />

   ![contenuto del file Hello web.cloud.config](./media/storage-nodejs-use-table-storage-cloud-service-app/node37.png)

6. <span data-ttu-id="e07e4-134">Salvare il file hello e chiudere il blocco note.</span><span class="sxs-lookup"><span data-stu-id="e07e4-134">Save hello file and close notepad.</span></span>

### <a name="install-additional-modules"></a><span data-ttu-id="e07e4-135">Installare moduli aggiuntivi</span><span class="sxs-lookup"><span data-stu-id="e07e4-135">Install additional modules</span></span>
1. <span data-ttu-id="e07e4-136">Hello utilizzo successivo comando tooinstall hello [azure], [nodo-uuid], [nconf] e [asincrona] moduli in locale, nonché a toosave una voce relativa toohello **package. JSON** file:</span><span class="sxs-lookup"><span data-stu-id="e07e4-136">Use hello following command tooinstall hello [azure], [node-uuid], [nconf] and [async] modules locally as well as toosave an entry for them toohello **package.json** file:</span></span>

  ```powershell
  PS C:\node\tasklist\WebRole1> npm install azure-storage node-uuid async nconf --save
  ```

  <span data-ttu-id="e07e4-137">output di Hello di questo comando risulterà simile toohello seguenti:</span><span class="sxs-lookup"><span data-stu-id="e07e4-137">hello output of this command should appear similar toohello following:</span></span>

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

## <a name="using-hello-table-service-in-a-node-application"></a><span data-ttu-id="e07e4-138">Utilizzo del servizio tabelle hello in un'applicazione di nodo</span><span class="sxs-lookup"><span data-stu-id="e07e4-138">Using hello Table service in a node application</span></span>
<span data-ttu-id="e07e4-139">In questa sezione sarà possibile estendere un'applicazione hello base creata hello **express** comando aggiungendo un **task.js** file che contiene il modello di hello per le attività.</span><span class="sxs-lookup"><span data-stu-id="e07e4-139">In this section you will extend hello basic application created by hello **express** command by adding a **task.js** file which contains hello model for your tasks.</span></span> <span data-ttu-id="e07e4-140">È inoltre possibile modificare hello esistente **app.js** e creare un nuovo **tasklist.js** file che utilizza il modello di hello.</span><span class="sxs-lookup"><span data-stu-id="e07e4-140">You will also modify hello existing **app.js** and create a new **tasklist.js** file that uses hello model.</span></span>

### <a name="create-hello-model"></a><span data-ttu-id="e07e4-141">Creare il modello di hello</span><span class="sxs-lookup"><span data-stu-id="e07e4-141">Create hello model</span></span>
1. <span data-ttu-id="e07e4-142">In hello **WebRole1** directory, creare una nuova directory denominata **modelli**.</span><span class="sxs-lookup"><span data-stu-id="e07e4-142">In hello **WebRole1** directory, create a new directory named **models**.</span></span>
2. <span data-ttu-id="e07e4-143">In hello **modelli** directory, creare un nuovo file denominato **task.js**.</span><span class="sxs-lookup"><span data-stu-id="e07e4-143">In hello **models** directory, create a new file named **task.js**.</span></span> <span data-ttu-id="e07e4-144">Questo file contiene il modello di hello per le operazioni di hello create dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="e07e4-144">This file will contain hello model for hello tasks created by your application.</span></span>
3. <span data-ttu-id="e07e4-145">All'inizio di hello di hello **task.js** file, aggiungere hello tooreference richiesto dalle librerie di codice seguente:</span><span class="sxs-lookup"><span data-stu-id="e07e4-145">At hello beginning of hello **task.js** file, add hello following code tooreference required libraries:</span></span>

    ```nodejs
    var azure = require('azure-storage');
    var uuid = require('node-uuid');
    var entityGen = azure.TableUtilities.entityGenerator;
    ```

4. <span data-ttu-id="e07e4-146">Successivamente, aggiungere codice toodefine che esporta l'oggetto attività hello.</span><span class="sxs-lookup"><span data-stu-id="e07e4-146">Next, you will add code toodefine and export hello Task object.</span></span> <span data-ttu-id="e07e4-147">Questo oggetto è responsabile per la connessione toohello tabella.</span><span class="sxs-lookup"><span data-stu-id="e07e4-147">This object is responsible for connecting toohello table.</span></span>

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

5. <span data-ttu-id="e07e4-148">Successivamente, aggiungere hello seguito metodi aggiuntivi di codice toodefine nell'oggetto attività hello, che consentono le interazioni con i dati archiviati nella tabella hello:</span><span class="sxs-lookup"><span data-stu-id="e07e4-148">Next, add hello following code toodefine additional methods on hello Task object, which allow interactions with data stored in hello table:</span></span>

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

6. <span data-ttu-id="e07e4-149">Salvare e chiudere hello **task.js** file.</span><span class="sxs-lookup"><span data-stu-id="e07e4-149">Save and close hello **task.js** file.</span></span>

### <a name="create-hello-controller"></a><span data-ttu-id="e07e4-150">Creare controller hello</span><span class="sxs-lookup"><span data-stu-id="e07e4-150">Create hello controller</span></span>
1. <span data-ttu-id="e07e4-151">In hello **WebRole1/route** directory, creare un nuovo file denominato **tasklist.js** e aprirlo in un editor di testo.</span><span class="sxs-lookup"><span data-stu-id="e07e4-151">In hello **WebRole1/routes** directory, create a new file named **tasklist.js** and open it in a text editor.</span></span>
2. <span data-ttu-id="e07e4-152">Aggiungere hello seguente codice troppo**tasklist.js**.</span><span class="sxs-lookup"><span data-stu-id="e07e4-152">Add hello following code too**tasklist.js**.</span></span> <span data-ttu-id="e07e4-153">Viene caricato hello async moduli di azure e, che vengono usati da **tasklist.js**.</span><span class="sxs-lookup"><span data-stu-id="e07e4-153">This loads hello azure and async modules, which are used by **tasklist.js**.</span></span> <span data-ttu-id="e07e4-154">Definisce inoltre hello **TaskList** funzione, che viene passata un'istanza di hello **attività** dell'oggetto definita in precedenza:</span><span class="sxs-lookup"><span data-stu-id="e07e4-154">This also defines hello **TaskList** function, which is passed an instance of hello **Task** object we defined earlier:</span></span>

    ```nodejs
    var azure = require('azure-storage');
    var async = require('async');

    module.exports = TaskList;

    function TaskList(task) {
      this.task = task;
    }
    ```

3. <span data-ttu-id="e07e4-155">Continuare ad aggiungere toohello **tasklist.js** file mediante l'aggiunta di metodi hello troppo**showTasks**, **addTask**, e **completeTasks**:</span><span class="sxs-lookup"><span data-stu-id="e07e4-155">Continue adding toohello **tasklist.js** file by adding hello methods used too**showTasks**, **addTask**, and **completeTasks**:</span></span>

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

4. <span data-ttu-id="e07e4-156">Salvare hello **tasklist.js** file.</span><span class="sxs-lookup"><span data-stu-id="e07e4-156">Save hello **tasklist.js** file.</span></span>

### <a name="modify-appjs"></a><span data-ttu-id="e07e4-157">Modificare il file app.js</span><span class="sxs-lookup"><span data-stu-id="e07e4-157">Modify app.js</span></span>
1. <span data-ttu-id="e07e4-158">In hello **WebRole1** hello directory, aprire **app.js** file in un editor di testo.</span><span class="sxs-lookup"><span data-stu-id="e07e4-158">In hello **WebRole1** directory, open hello **app.js** file in a text editor.</span></span>
2. <span data-ttu-id="e07e4-159">Inizio hello del file hello, aggiungere hello seguente modulo hello azure tooload e impostare la chiave di nome e una partizione di tabella hello:</span><span class="sxs-lookup"><span data-stu-id="e07e4-159">At hello beginning of hello file, add hello following tooload hello azure module and set hello table name and partition key:</span></span>

    ```nodejs
    var azure = require('azure-storage');
    var tableName = 'tasks';
    var partitionKey = 'hometasks';
    ```

3. <span data-ttu-id="e07e4-160">Nel file app.js hello, scorrere verso il basso toowhere vedrai hello la seguente riga:</span><span class="sxs-lookup"><span data-stu-id="e07e4-160">In hello app.js file, scroll down toowhere you see hello following line:</span></span>

    ```nodejs
    app.use('/', routes);
    app.use('/users', users);
    ```

    <span data-ttu-id="e07e4-161">Sostituire hello sopra righe con codice hello riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="e07e4-161">Replace hello above lines with hello code shown below.</span></span> <span data-ttu-id="e07e4-162">Inizializza un'istanza di <strong>attività</strong> con un account di archiviazione tooyour di connessione.</span><span class="sxs-lookup"><span data-stu-id="e07e4-162">This will initialize an instance of <strong>Task</strong> with a connection tooyour storage account.</span></span> <span data-ttu-id="e07e4-163">Questo argomento viene passato toohello <strong>TaskList</strong>, che verrà utilizzato toocommunicate con hello del servizio tabelle:</span><span class="sxs-lookup"><span data-stu-id="e07e4-163">This is passed toohello <strong>TaskList</strong>, which will use it toocommunicate with hello Table service:</span></span>

    ```nodejs
    var TaskList = require('./routes/tasklist');
    var Task = require('./models/task');
    var task = new Task(azure.createTableService(), tableName, partitionKey);
    var taskList = new TaskList(task);

    app.get('/', taskList.showTasks.bind(taskList));
    app.post('/addtask', taskList.addTask.bind(taskList));
    app.post('/completetask', taskList.completeTask.bind(taskList));
    ```

4. <span data-ttu-id="e07e4-164">Salvare hello **app.js** file.</span><span class="sxs-lookup"><span data-stu-id="e07e4-164">Save hello **app.js** file.</span></span>

### <a name="modify-hello-index-view"></a><span data-ttu-id="e07e4-165">Modifica visualizzazione dell'indice hello</span><span class="sxs-lookup"><span data-stu-id="e07e4-165">Modify hello index view</span></span>
1. <span data-ttu-id="e07e4-166">Modificare le directory toohello **viste** hello directory e aprire **index.jade** file in un editor di testo.</span><span class="sxs-lookup"><span data-stu-id="e07e4-166">Change directories toohello **views** directory and open hello **index.jade** file in a text editor.</span></span>
2. <span data-ttu-id="e07e4-167">Sostituire il contenuto di hello di hello **index.jade** file con codice hello riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="e07e4-167">Replace hello contents of hello **index.jade** file with hello code below.</span></span> <span data-ttu-id="e07e4-168">Definisce la visualizzazione hello per le attività esistenti, nonché un form per l'aggiunta di nuove attività e contrassegnare esistenti come completata.</span><span class="sxs-lookup"><span data-stu-id="e07e4-168">This defines hello view for displaying existing tasks, as well as a form for adding new tasks and marking existing ones as completed.</span></span>

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

3. <span data-ttu-id="e07e4-169">Salvare e chiudere il file **index.jade** .</span><span class="sxs-lookup"><span data-stu-id="e07e4-169">Save and close **index.jade** file.</span></span>

### <a name="modify-hello-global-layout"></a><span data-ttu-id="e07e4-170">Modifica layout globale hello</span><span class="sxs-lookup"><span data-stu-id="e07e4-170">Modify hello global layout</span></span>
<span data-ttu-id="e07e4-171">Hello **layout.jade** file hello **viste** directory viene utilizzata come modello generale per altri **.jade** file.</span><span class="sxs-lookup"><span data-stu-id="e07e4-171">hello **layout.jade** file in hello **views** directory is used as a global template for other **.jade** files.</span></span> <span data-ttu-id="e07e4-172">In questo passaggio è necessario modificarlo toouse [Twitter Bootstrap](https://github.com/twbs/bootstrap), che è un toolkit che rende facile toodesign un sito Web professionale nice.</span><span class="sxs-lookup"><span data-stu-id="e07e4-172">In this step you will modify it toouse [Twitter Bootstrap](https://github.com/twbs/bootstrap), which is a toolkit that makes it easy toodesign a nice looking website.</span></span>

1. <span data-ttu-id="e07e4-173">Scaricare ed estrarre file hello per [Twitter Bootstrap](http://getbootstrap.com/).</span><span class="sxs-lookup"><span data-stu-id="e07e4-173">Download and extract hello files for [Twitter Bootstrap](http://getbootstrap.com/).</span></span> <span data-ttu-id="e07e4-174">Hello copia **bootstrap.min.css** file hello **bootstrap\\dist\\css** cartella toohello **pubblica\\fogli di stile** directory dell'applicazione elenco attività.</span><span class="sxs-lookup"><span data-stu-id="e07e4-174">Copy hello **bootstrap.min.css** file from hello **bootstrap\\dist\\css** folder toohello **public\\stylesheets** directory of your tasklist application.</span></span>
2. <span data-ttu-id="e07e4-175">Da hello **viste** cartella, aprire hello **layout.jade** il contenuto di hello editor e sostituire testo con il seguente hello:</span><span class="sxs-lookup"><span data-stu-id="e07e4-175">From hello **views** folder, open hello **layout.jade** in your text editor and replace hello contents with hello following:</span></span>

    <span data-ttu-id="e07e4-176">doctype html  html    head      title= title      link(rel='stylesheet', href='/stylesheets/bootstrap.min.css')      link(rel='stylesheet', href='/stylesheets/style.css')    body.app      nav.navbar.navbar-default        div.navbar-header          a.navbar-brand(href='/') My Tasks      block content</span><span class="sxs-lookup"><span data-stu-id="e07e4-176">doctype html  html    head      title= title      link(rel='stylesheet', href='/stylesheets/bootstrap.min.css')      link(rel='stylesheet', href='/stylesheets/style.css')    body.app      nav.navbar.navbar-default        div.navbar-header          a.navbar-brand(href='/') My Tasks      block content</span></span>

3. <span data-ttu-id="e07e4-177">Salvare hello **layout.jade** file.</span><span class="sxs-lookup"><span data-stu-id="e07e4-177">Save hello **layout.jade** file.</span></span>

### <a name="running-hello-application-in-hello-emulator"></a><span data-ttu-id="e07e4-178">Esecuzione dell'applicazione hello in hello emulatore</span><span class="sxs-lookup"><span data-stu-id="e07e4-178">Running hello Application in hello Emulator</span></span>
<span data-ttu-id="e07e4-179">Utilizzare hello seguito comando toostart hello applicazione nell'emulatore hello.</span><span class="sxs-lookup"><span data-stu-id="e07e4-179">Use hello following command toostart hello application in hello emulator.</span></span>

```powershell
PS C:\node\tasklist\WebRole1> start-azureemulator -launch
```

<span data-ttu-id="e07e4-180">browser Hello verrà aperto e Visualizza hello pagina seguente:</span><span class="sxs-lookup"><span data-stu-id="e07e4-180">hello browser will open and displays hello following page:</span></span>

![Un sito web di paging denominato elenco di attività personali con una tabella contenente le attività e i campi tooadd una nuova attività.](./media/storage-nodejs-use-table-storage-cloud-service-app/node44.png)

<span data-ttu-id="e07e4-182">Utilizzare elementi del modulo di hello tooadd o rimuovere elementi esistenti, contrassegnandoli come completata.</span><span class="sxs-lookup"><span data-stu-id="e07e4-182">Use hello form tooadd items, or remove existing items by marking them as completed.</span></span>

## <a name="publishing-hello-application-tooazure"></a><span data-ttu-id="e07e4-183">Pubblicazione hello applicazione tooAzure</span><span class="sxs-lookup"><span data-stu-id="e07e4-183">Publishing hello Application tooAzure</span></span>
<span data-ttu-id="e07e4-184">Nella finestra di Windows PowerShell hello, chiamare hello seguente cmdlet tooredeploy tooAzure il servizio ospitato.</span><span class="sxs-lookup"><span data-stu-id="e07e4-184">In hello Windows PowerShell window, call hello following cmdlet tooredeploy your hosted service tooAzure.</span></span>

```powershell
PS C:\node\tasklist\WebRole1> Publish-AzureServiceProject -name myuniquename -location datacentername -launch
```

<span data-ttu-id="e07e4-185">Sostituire **myuniquename** con un nome univoco per questa applicazione.</span><span class="sxs-lookup"><span data-stu-id="e07e4-185">Replace **myuniquename** with a unique name for this application.</span></span> <span data-ttu-id="e07e4-186">Sostituire **datacentername** con nome hello del data center di Azure, ad esempio **Stati Uniti occidentali**.</span><span class="sxs-lookup"><span data-stu-id="e07e4-186">Replace **datacentername** with hello name of an Azure data center, such as **West US**.</span></span>

<span data-ttu-id="e07e4-187">Una volta completata la distribuzione di hello, vedrai un seguente toohello simile risposta:</span><span class="sxs-lookup"><span data-stu-id="e07e4-187">After hello deployment is complete, you should see a response similar toohello following:</span></span>

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

<span data-ttu-id="e07e4-188">Come in precedenza, poiché è stato specificato hello **-avviare** opzione hello browser verrà aperto e visualizza l'applicazione in esecuzione in Azure quando viene completata la pubblicazione.</span><span class="sxs-lookup"><span data-stu-id="e07e4-188">As before, because you specified hello **-launch** option, hello browser opens and displays your application running in Azure when publishing is completed.</span></span>

![Visualizzazione della pagina di elenco di attività personali hello una finestra del browser.](./media/storage-nodejs-use-table-storage-cloud-service-app/getting-started-1.png)

## <a name="stopping-and-deleting-your-application"></a><span data-ttu-id="e07e4-191">Arresto ed eliminazione dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="e07e4-191">Stopping and Deleting Your Application</span></span>
<span data-ttu-id="e07e4-192">Dopo aver distribuito l'applicazione, è opportuno toodisable in modo da evitare i costi o compilare e distribuire applicazioni all'interno di hello gratuitamente periodo di tempo di valutazione.</span><span class="sxs-lookup"><span data-stu-id="e07e4-192">After deploying your application, you may want toodisable it so you can avoid costs or build and deploy other applications within hello free trial time period.</span></span>

<span data-ttu-id="e07e4-193">Azure addebita le istanze del ruolo Web al consumo, in base all'utilizzo di tempo del server su base oraria.</span><span class="sxs-lookup"><span data-stu-id="e07e4-193">Azure bills web role instances per hour of server time consumed.</span></span>
<span data-ttu-id="e07e4-194">Ora del server viene utilizzata una volta distribuita l'applicazione, anche se le istanze non sono in esecuzione e si trovano nello stato arrestato hello.</span><span class="sxs-lookup"><span data-stu-id="e07e4-194">Server time is consumed once your application is deployed, even if the instances are not running and are in hello stopped state.</span></span>

<span data-ttu-id="e07e4-195">Hello passaggi seguenti viene illustrato come toostop ed eliminare l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="e07e4-195">hello following steps show you how toostop and delete your application.</span></span>

1. <span data-ttu-id="e07e4-196">Nella finestra di Windows PowerShell hello, arrestare la distribuzione del servizio hello creata nella sezione precedente di hello con hello seguente cmdlet:</span><span class="sxs-lookup"><span data-stu-id="e07e4-196">In hello Windows PowerShell window, stop hello service deployment created in hello previous section with hello following cmdlet:</span></span>

    ```powershell
    PS C:\node\tasklist\WebRole1> Stop-AzureService
    ```

   <span data-ttu-id="e07e4-197">L'arresto del servizio hello potrebbe richiedere alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="e07e4-197">Stopping hello service may take several minutes.</span></span> <span data-ttu-id="e07e4-198">Quando il servizio hello viene arrestato, viene visualizzato un messaggio che indica che è stato arrestato.</span><span class="sxs-lookup"><span data-stu-id="e07e4-198">When hello service is stopped, you receive a message indicating that it has stopped.</span></span>

2. <span data-ttu-id="e07e4-199">servizio di hello toodelete, hello chiamata seguente cmdlet:</span><span class="sxs-lookup"><span data-stu-id="e07e4-199">toodelete hello service, call hello following cmdlet:</span></span>

    ```powershell
    PS C:\node\tasklist\WebRole1> Remove-AzureService contosotasklist
    ```

   <span data-ttu-id="e07e4-200">Quando richiesto, immettere **Y** servizio hello toodelete.</span><span class="sxs-lookup"><span data-stu-id="e07e4-200">When prompted, enter **Y** toodelete hello service.</span></span>

   <span data-ttu-id="e07e4-201">Eliminazione del servizio hello potrebbe richiedere alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="e07e4-201">Deleting hello service may take several minutes.</span></span> <span data-ttu-id="e07e4-202">Dopo aver eliminato il servizio hello viene visualizzato un messaggio che indica che il servizio di hello è stato eliminato.</span><span class="sxs-lookup"><span data-stu-id="e07e4-202">After hello service has been deleted you receive a message indicating that hello service was deleted.</span></span>

[applicazione Web Node.js mediante Express]: http://azure.microsoft.com/develop/nodejs/tutorials/web-app-with-express/
[Archiviazione e accesso ai dati in Azure]: http://msdn.microsoft.com/library/azure/gg433040.aspx
[applicazione Web Node.js]: http://azure.microsoft.com/develop/nodejs/tutorials/getting-started/


