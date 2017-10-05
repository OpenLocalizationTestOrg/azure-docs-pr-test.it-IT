---
title: App Web con il servizio di archiviazione tabelle (Node.js) | Microsoft Docs
description: Esercitazione basata sull'esercitazione per la creazione di un'app Web con Express e in cui vengono aggiunti i servizi di archiviazione di Azure e il modulo di Azure.
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
ms.openlocfilehash: b802f880c1131abb7eb9ba00dd8f2e65017bc802
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="nodejs-web-application-using-storage"></a><span data-ttu-id="10787-103">Creazione di un'applicazione Web Node.js con Archiviazione</span><span class="sxs-lookup"><span data-stu-id="10787-103">Node.js Web Application using Storage</span></span>
## <a name="overview"></a><span data-ttu-id="10787-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="10787-104">Overview</span></span>
<span data-ttu-id="10787-105">In questa esercitazione, l'applicazione creata nell'esercitazione [Creazione di un'applicazione Web Node.js usando Express in un servizio cloud di Azure] viene estesa usando le librerie client di Microsoft Azure per Node.js in modo da poter lavorare con i servizi di gestione dati.</span><span class="sxs-lookup"><span data-stu-id="10787-105">In this tutorial, the application you created in the [Node.js Web Application using Express] tutorial is extended using the Microsoft Azure Client Libraries for Node.js to work with data management services.</span></span> <span data-ttu-id="10787-106">L'applicazione viene estesa creando un'applicazione elenco di attività basata sul Web che è possibile distribuire in Azure.</span><span class="sxs-lookup"><span data-stu-id="10787-106">You extend your application by creating a web-based task-list application that you can deploy to Azure.</span></span> <span data-ttu-id="10787-107">L'elenco di attività consente a un utente di recuperare le attività, aggiungerne di nuove e contrassegnarle come completate.</span><span class="sxs-lookup"><span data-stu-id="10787-107">The task list allows a user to retrieve tasks, add new tasks, and mark tasks as completed.</span></span>

<span data-ttu-id="10787-108">Gli elementi attività vengono archiviati in Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="10787-108">The task items are stored in Azure Storage.</span></span> <span data-ttu-id="10787-109">Archiviazione di Azure consente l'archiviazione di dati non strutturati, a tolleranza di errore e a disponibilità elevata.</span><span class="sxs-lookup"><span data-stu-id="10787-109">Azure Storage provides unstructured data storage that is fault-tolerant and highly available.</span></span> <span data-ttu-id="10787-110">Archiviazione di Azure include varie strutture di dati in cui è possibile archiviare i dati e da cui è possibile accedere ad essi.</span><span class="sxs-lookup"><span data-stu-id="10787-110">Azure Storage includes several data structures where you can store and access data.</span></span> <span data-ttu-id="10787-111">A questo scopo, è possibile usare i servizi di archiviazione delle API incluse in Azure SDK per Node.js o le API REST.</span><span class="sxs-lookup"><span data-stu-id="10787-111">You can use the storage services from the APIs included in the Azure SDK for Node.js or via REST APIs.</span></span> <span data-ttu-id="10787-112">Per ulteriori informazioni, vedere [Archiviazione e accesso ai dati in Azure].</span><span class="sxs-lookup"><span data-stu-id="10787-112">For more information, see [Storing and Accessing Data in Azure].</span></span>

<span data-ttu-id="10787-113">In questa esercitazione si presume che siano state completate le esercitazioni [Creazione e distribuzione di un'applicazione Node.js a un Servizio cloud di Azure] e [Creazione di un'applicazione Web Node.js usando Express in un servizio cloud di Azure][Creazione di un'applicazione Web Node.js usando Express in un servizio cloud di Azure].</span><span class="sxs-lookup"><span data-stu-id="10787-113">This tutorial assumes that you have completed the [Node.js Web Application] and [Node.js with Express][Node.js Web Application using Express] tutorials.</span></span>

<span data-ttu-id="10787-114">Contiene le informazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="10787-114">It contains the following information:</span></span>

* <span data-ttu-id="10787-115">Usare il motore dei modelli Jade</span><span class="sxs-lookup"><span data-stu-id="10787-115">How to work with the Jade template engine</span></span>
* <span data-ttu-id="10787-116">Usare i servizi di gestione dati di Azure</span><span class="sxs-lookup"><span data-stu-id="10787-116">How to work with Azure Data Management services</span></span>

<span data-ttu-id="10787-117">In questo screenshot viene visualizzata l'applicazione completata:</span><span class="sxs-lookup"><span data-stu-id="10787-117">The following screenshot shows the completed application:</span></span>

![Pagina Web completata in Internet Explorer](./media/table-storage-cloud-service-nodejs/getting-started-1.png)

## <a name="setting-storage-credentials-in-webconfig"></a><span data-ttu-id="10787-119">Impostazione delle credenziali di archiviazione in Web.Config</span><span class="sxs-lookup"><span data-stu-id="10787-119">Setting Storage Credentials in Web.Config</span></span>
<span data-ttu-id="10787-120">Per accedere ad Archiviazione di Azure, è necessario passare le credenziali di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="10787-120">You must pass in storage credentials to access Azure Storage.</span></span> <span data-ttu-id="10787-121">Per eseguire questa operazione, è possibile usare le impostazioni dell'applicazione web.config,</span><span class="sxs-lookup"><span data-stu-id="10787-121">This is done by utilizing the web.config application settings.</span></span>
<span data-ttu-id="10787-122">che vengono passate a Node come variabili di ambiente e che verranno lette da Azure SDK.</span><span class="sxs-lookup"><span data-stu-id="10787-122">The web.config settings are passed as environment variables to Node, which are then read by the Azure SDK.</span></span>

> [!NOTE]
> <span data-ttu-id="10787-123">Le credenziali di archiviazione vengono utilizzate solo quando l'applicazione viene distribuita in Azure.</span><span class="sxs-lookup"><span data-stu-id="10787-123">Storage credentials are only used when the application is deployed to Azure.</span></span> <span data-ttu-id="10787-124">Quando viene eseguita nell'emulatore, l'applicazione usa l'emulatore di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="10787-124">When running in the emulator, the application uses the storage emulator.</span></span>
>
>

<span data-ttu-id="10787-125">Eseguire i passaggi seguenti per recuperare le credenziali dell'account di archiviazione e aggiungerle alle impostazioni di web.config:</span><span class="sxs-lookup"><span data-stu-id="10787-125">Perform the following steps to retrieve the storage account credentials and add them to the web.config settings:</span></span>

1. <span data-ttu-id="10787-126">Se non è già aperto, avviare Azure PowerShell dal menu **Start** espandendo **Tutti i programmi, Azure**, fare clic con il pulsante destro del mouse su **Azure PowerShell** e quindi scegliere **Esegui come amministratore**.</span><span class="sxs-lookup"><span data-stu-id="10787-126">If it is not already open, start the Azure PowerShell from the **Start** menu by expanding **All Programs, Azure**, right-click **Azure PowerShell**, and then select **Run As Administrator**.</span></span>
2. <span data-ttu-id="10787-127">Sostituire le directory con la cartella contenente l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="10787-127">Change directories to the folder containing your application.</span></span> <span data-ttu-id="10787-128">Ad esempio, C:\\node\\tasklist\\WebRole1.</span><span class="sxs-lookup"><span data-stu-id="10787-128">For example, C:\\node\\tasklist\\WebRole1.</span></span>
3. <span data-ttu-id="10787-129">Nella finestra di Azure Powershell immettere il cmdlet seguente per recuperare le informazioni sull'account di archiviazione:</span><span class="sxs-lookup"><span data-stu-id="10787-129">From the Azure Powershell window, enter the following cmdlet to retrieve the storage account information:</span></span>

    ```powershell
    PS C:\node\tasklist\WebRole1> Get-AzureStorageAccounts
    ```

   <span data-ttu-id="10787-130">Con questo cmdlet viene recuperato l'elenco di account di archiviazione e di chiavi dell'account associati al servizio ospitato.</span><span class="sxs-lookup"><span data-stu-id="10787-130">The preceding cmdlet retrieves the list of storage accounts and account keys associated with your hosted service.</span></span>

   > [!NOTE]
   > <span data-ttu-id="10787-131">Dal momento che Azure SDK crea un account di archiviazione quando si distribuisce un servizio, esisterà già un account di archiviazione dalla distribuzione dell'applicazione nelle guide precedenti.</span><span class="sxs-lookup"><span data-stu-id="10787-131">Since the Azure SDK creates a storage account when you deploy a service, a storage account should already exist from deploying your application in the previous guides.</span></span>
   >
   >
4. <span data-ttu-id="10787-132">Aprire il file **ServiceDefinition.csdef** contenente le impostazioni dell'ambiente usate quando l'applicazione viene distribuita in Azure:</span><span class="sxs-lookup"><span data-stu-id="10787-132">Open the **ServiceDefinition.csdef** file containing the environment settings that are used when the application is deployed to Azure:</span></span>

    ```powershell
    PS C:\node\tasklist> notepad ServiceDefinition.csdef
    ```

5. <span data-ttu-id="10787-133">Inserire il blocco seguente sotto l'elemento **Environment**, sostituendo {STORAGE ACCOUNT} e {STORAGE ACCESS KEY} con il nome account e con la chiave primaria per l'account di archiviazione che si intende usare per la distribuzione:</span><span class="sxs-lookup"><span data-stu-id="10787-133">Insert the following block under **Environment** element, substituting {STORAGE ACCOUNT} and {STORAGE ACCESS KEY} with the account name and the primary key for the storage account you want to use for deployment:</span></span>

  <Variable name="AZURE_STORAGE_ACCOUNT" value="{STORAGE ACCOUNT}" />
  <Variable name="AZURE_STORAGE_ACCESS_KEY" value="{STORAGE ACCESS KEY}" />

   ![Contenuto file web.cloud.config](./media/table-storage-cloud-service-nodejs/node37.png)

6. <span data-ttu-id="10787-135">Salvare il file e chiudere Blocco note.</span><span class="sxs-lookup"><span data-stu-id="10787-135">Save the file and close notepad.</span></span>

### <a name="install-additional-modules"></a><span data-ttu-id="10787-136">Installare moduli aggiuntivi</span><span class="sxs-lookup"><span data-stu-id="10787-136">Install additional modules</span></span>
1. <span data-ttu-id="10787-137">Usare quindi il comando seguente per installare i moduli [azure], [node-uuid], [nconf] e [async] in locale e per salvare una voce per tali moduli nel file **package.json**:</span><span class="sxs-lookup"><span data-stu-id="10787-137">Use the following command to install the [azure], [node-uuid], [nconf] and [async] modules locally as well as to save an entry for them to the **package.json** file:</span></span>

  ```powershell
  PS C:\node\tasklist\WebRole1> npm install azure-storage node-uuid async nconf --save
  ```

  <span data-ttu-id="10787-138">L'output di questo comando dovrebbe apparire simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="10787-138">The output of this command should appear similar to the following:</span></span>

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

## <a name="using-the-table-service-in-a-node-application"></a><span data-ttu-id="10787-139">Utilizzo del servizio tabelle in un'applicazione Node</span><span class="sxs-lookup"><span data-stu-id="10787-139">Using the Table service in a node application</span></span>
<span data-ttu-id="10787-140">In questa sezione, l'applicazione di base creata con il comando **express** viene estesa aggiungendo un file **task.js** contenente il modello per le attività.</span><span class="sxs-lookup"><span data-stu-id="10787-140">In this section, the basic application created by the **express** command is extended by adding a **task.js** file containing the model for your tasks.</span></span> <span data-ttu-id="10787-141">Modificare il file **app.js** esistente e creare un nuovo file **tasklist.js** che usi il modello.</span><span class="sxs-lookup"><span data-stu-id="10787-141">Modify the existing **app.js** file and create a new **tasklist.js** file that uses the model.</span></span>

### <a name="create-the-model"></a><span data-ttu-id="10787-142">Creare il modello</span><span class="sxs-lookup"><span data-stu-id="10787-142">Create the model</span></span>
1. <span data-ttu-id="10787-143">Nella directory **WebRole1** creare una nuova directory denominata **models**.</span><span class="sxs-lookup"><span data-stu-id="10787-143">In the **WebRole1** directory, create a new directory named **models**.</span></span>
2. <span data-ttu-id="10787-144">Nella directory **models** creare un nuovo file denominato **task.js**.</span><span class="sxs-lookup"><span data-stu-id="10787-144">In the **models** directory, create a new file named **task.js**.</span></span> <span data-ttu-id="10787-145">Questo file contiene il modello per le attività create dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="10787-145">This file contains the model for the tasks created by your application.</span></span>
3. <span data-ttu-id="10787-146">All'inizio del file **task.js** , aggiungere il codice seguente per fare riferimento alle librerie necessarie:</span><span class="sxs-lookup"><span data-stu-id="10787-146">At the beginning of the **task.js** file, add the following code to reference required libraries:</span></span>

    ```nodejs
    var azure = require('azure-storage');
    var uuid = require('node-uuid');
    var entityGen = azure.TableUtilities.entityGenerator;
    ```

4. <span data-ttu-id="10787-147">Aggiungere quindi il codice per definire ed esportare l'oggetto Task,</span><span class="sxs-lookup"><span data-stu-id="10787-147">Next, add code to define and export the Task object.</span></span> <span data-ttu-id="10787-148">responsabile della connessione alla tabella.</span><span class="sxs-lookup"><span data-stu-id="10787-148">The Task object is responsible for connecting to the table.</span></span>

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

5. <span data-ttu-id="10787-149">Aggiungere quindi il codice seguente per definire metodi aggiuntivi nell'oggetto Task che consentano l'interazione con i dati archiviati nella tabella:</span><span class="sxs-lookup"><span data-stu-id="10787-149">Next, add the following code to define additional methods on the Task object, which allow interactions with data stored in the table:</span></span>

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
    ```

6. <span data-ttu-id="10787-150">Salvare e chiudere il file **task.js** .</span><span class="sxs-lookup"><span data-stu-id="10787-150">Save and close the **task.js** file.</span></span>

### <a name="create-the-controller"></a><span data-ttu-id="10787-151">Creare il controller</span><span class="sxs-lookup"><span data-stu-id="10787-151">Create the controller</span></span>
1. <span data-ttu-id="10787-152">Nella directory **WebRole1/routes** creare un nuovo file denominato **tasklist.js** e aprirlo in un editor di testo.</span><span class="sxs-lookup"><span data-stu-id="10787-152">In the **WebRole1/routes** directory, create a new file named **tasklist.js** and open it in a text editor.</span></span>
2. <span data-ttu-id="10787-153">Aggiungere il seguente codice al file **tasklist.js**.</span><span class="sxs-lookup"><span data-stu-id="10787-153">Add the following code to **tasklist.js**.</span></span> <span data-ttu-id="10787-154">Con questo codice vengono caricati i moduli di Azure e i moduli asincroni usati da **tasklist.js** e viene definita la funzione **TaskList**, che viene passata come istanza dell'oggetto **Task** definito in precedenza:</span><span class="sxs-lookup"><span data-stu-id="10787-154">This code loads the azure and async modules, which are used by **tasklist.js** and defines the **TaskList** function, which is passed an instance of the **Task** object we defined earlier:</span></span>

    ```nodejs
    var azure = require('azure-storage');
    var async = require('async');

    module.exports = TaskList;

    function TaskList(task) {
      this.task = task;
    }
    ```

3. <span data-ttu-id="10787-155">Continuare ad aggiungere codice al file **tasklist.js** aggiungendo i metodi **showTasks**, **addTask** e **completeTasks**:</span><span class="sxs-lookup"><span data-stu-id="10787-155">Continue adding to the **tasklist.js** file by adding the methods used to **showTasks**, **addTask**, and **completeTasks**:</span></span>

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

4. <span data-ttu-id="10787-156">Salvare il file **tasklist.js**.</span><span class="sxs-lookup"><span data-stu-id="10787-156">Save the **tasklist.js** file.</span></span>

### <a name="modify-appjs"></a><span data-ttu-id="10787-157">Modificare il file app.js</span><span class="sxs-lookup"><span data-stu-id="10787-157">Modify app.js</span></span>
1. <span data-ttu-id="10787-158">Nella directory **WebRole1** aprire il file **app.js** in un editor di testo.</span><span class="sxs-lookup"><span data-stu-id="10787-158">In the **WebRole1** directory, open the **app.js** file in a text editor.</span></span>
2. <span data-ttu-id="10787-159">Aggiungere quanto riportato di seguito all'inizio del file per caricare il modulo azure e impostare il nome della tabella e la chiave della partizione:</span><span class="sxs-lookup"><span data-stu-id="10787-159">At the beginning of the file, add the following to load the azure module and set the table name and partition key:</span></span>

    ```nodejs
    var azure = require('azure-storage');
    var tableName = 'tasks';
    var partitionKey = 'hometasks';
    ```

3. <span data-ttu-id="10787-160">Nel file app.js scorrere verso il basso fino a individuare la riga seguente:</span><span class="sxs-lookup"><span data-stu-id="10787-160">In the app.js file, scroll down to where you see the following line:</span></span>

    ```nodejs
    app.use('/', routes);
    app.use('/users', users);
    ```

    <span data-ttu-id="10787-161">Sostituire le righe sopra riportate con il codice seguente.</span><span class="sxs-lookup"><span data-stu-id="10787-161">Replace the preceding lines with the following code.</span></span> <span data-ttu-id="10787-162">Viene inizializzata un'istanza di <strong>Task</strong> con una connessione all'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="10787-162">This code initializes an instance of <strong>Task</strong> with a connection to your storage account.</span></span> <span data-ttu-id="10787-163">L'oggetto <strong>Task</strong> viene quindi passato a <strong>TaskList</strong>, che lo usa per comunicare con il servizio tabelle:</span><span class="sxs-lookup"><span data-stu-id="10787-163">The <strong>Task</strong> is passed to the <strong>TaskList</strong>, which uses it to communicate with the Table service:</span></span>

    ```nodejs
    var TaskList = require('./routes/tasklist');
    var Task = require('./models/task');
    var task = new Task(azure.createTableService(), tableName, partitionKey);
    var taskList = new TaskList(task);

    app.get('/', taskList.showTasks.bind(taskList));
    app.post('/addtask', taskList.addTask.bind(taskList));
    app.post('/completetask', taskList.completeTask.bind(taskList));
    ```

4. <span data-ttu-id="10787-164">Salvare il file **app.js** .</span><span class="sxs-lookup"><span data-stu-id="10787-164">Save the **app.js** file.</span></span>

### <a name="modify-the-index-view"></a><span data-ttu-id="10787-165">Modificare la visualizzazione dell'indice</span><span class="sxs-lookup"><span data-stu-id="10787-165">Modify the index view</span></span>
1. <span data-ttu-id="10787-166">Passare alla directory **views** e aprire il file **index.jade** in un editor di testo.</span><span class="sxs-lookup"><span data-stu-id="10787-166">Change directories to the **views** directory and open the **index.jade** file in a text editor.</span></span>
2. <span data-ttu-id="10787-167">Sostituire il contenuto del file **index.jade** con il codice seguente.</span><span class="sxs-lookup"><span data-stu-id="10787-167">Replace the contents of the **index.jade** file with the following code.</span></span> <span data-ttu-id="10787-168">Viene definita la visualizzazione delle attività esistenti, oltre a un formato per aggiungere nuove attività e contrassegnare quelle esistenti come completate.</span><span class="sxs-lookup"><span data-stu-id="10787-168">This code defines the view for displaying existing tasks, and defines a form for adding new tasks and marking existing ones as completed.</span></span>

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

3. <span data-ttu-id="10787-169">Salvare e chiudere il file **index.jade** .</span><span class="sxs-lookup"><span data-stu-id="10787-169">Save and close **index.jade** file.</span></span>

### <a name="modify-the-global-layout"></a><span data-ttu-id="10787-170">Modificare il layout globale</span><span class="sxs-lookup"><span data-stu-id="10787-170">Modify the global layout</span></span>
<span data-ttu-id="10787-171">Il file **layout.jade** della directory **views** viene usato come modello globale per altri file **.jade**.</span><span class="sxs-lookup"><span data-stu-id="10787-171">The **layout.jade** file in the **views** directory is used as a global template for other **.jade** files.</span></span> <span data-ttu-id="10787-172">In questo passaggio si modifica il file **layout.jade** in modo da usare [Twitter Bootstrap](https://github.com/twbs/bootstrap), un toolkit che semplifica la progettazione di un sito Web di aspetto gradevole.</span><span class="sxs-lookup"><span data-stu-id="10787-172">In this step, modify the **layout.jade** file to use [Twitter Bootstrap](https://github.com/twbs/bootstrap), which is a toolkit that makes it easy to design a nice looking website.</span></span>

1. <span data-ttu-id="10787-173">Scaricare ed estrarre i file per [Twitter Bootstrap](http://getbootstrap.com/).</span><span class="sxs-lookup"><span data-stu-id="10787-173">Download and extract the files for [Twitter Bootstrap](http://getbootstrap.com/).</span></span> <span data-ttu-id="10787-174">Copiare il file **bootstrap.min.css** dalla cartella **bootstrap\\dist\\css** alla directory **public\\stylesheets** dell'applicazione tasklist.</span><span class="sxs-lookup"><span data-stu-id="10787-174">Copy the **bootstrap.min.css** file from the **bootstrap\\dist\\css** folder to the **public\\stylesheets** directory of your tasklist application.</span></span>
2. <span data-ttu-id="10787-175">Dalla cartella **views** aprire il file **layout.jade** nell'editor di testo e sostituire il contenuto con quello seguente:</span><span class="sxs-lookup"><span data-stu-id="10787-175">From the **views** folder, open the **layout.jade** file in your text editor and replace the contents with the following:</span></span>

    <span data-ttu-id="10787-176">doctype html  html    head      title= title      link(rel='stylesheet', href='/stylesheets/bootstrap.min.css')      link(rel='stylesheet', href='/stylesheets/style.css')    body.app      nav.navbar.navbar-default        div.navbar-header          a.navbar-brand(href='/') My Tasks      block content</span><span class="sxs-lookup"><span data-stu-id="10787-176">doctype html  html    head      title= title      link(rel='stylesheet', href='/stylesheets/bootstrap.min.css')      link(rel='stylesheet', href='/stylesheets/style.css')    body.app      nav.navbar.navbar-default        div.navbar-header          a.navbar-brand(href='/') My Tasks      block content</span></span>

3. <span data-ttu-id="10787-177">Salvare il file **layout.jade**.</span><span class="sxs-lookup"><span data-stu-id="10787-177">Save the **layout.jade** file.</span></span>

### <a name="running-the-application-in-the-emulator"></a><span data-ttu-id="10787-178">Esecuzione dell'applicazione nell'emulatore</span><span class="sxs-lookup"><span data-stu-id="10787-178">Running the Application in the Emulator</span></span>
<span data-ttu-id="10787-179">Usare il comando seguente per avviare l'applicazione nell'emulatore.</span><span class="sxs-lookup"><span data-stu-id="10787-179">Use the following command to start the application in the emulator.</span></span>

```powershell
PS C:\node\tasklist\WebRole1> start-azureemulator -launch
```

<span data-ttu-id="10787-180">Nel browser viene visualizzata la pagina seguente:</span><span class="sxs-lookup"><span data-stu-id="10787-180">The browser opens and displays the following page:</span></span>

![Pagina Web intitolata My Task List con una tabella contenente le attività e i campi per aggiungere una nuova attività.](./media/table-storage-cloud-service-nodejs/node44.png)

<span data-ttu-id="10787-182">Usare il modulo per aggiungere elementi o rimuovere elementi esistenti contrassegnandoli come completati.</span><span class="sxs-lookup"><span data-stu-id="10787-182">Use the form to add items, or remove existing items by marking them as completed.</span></span>

## <a name="publishing-the-application-to-azure"></a><span data-ttu-id="10787-183">Pubblicazione dell'applicazione in Azure</span><span class="sxs-lookup"><span data-stu-id="10787-183">Publishing the Application to Azure</span></span>
<span data-ttu-id="10787-184">Nella finestra di Windows PowerShell chiamare il cmdlet seguente per ridistribuire il servizio ospitato in Azure.</span><span class="sxs-lookup"><span data-stu-id="10787-184">In the Windows PowerShell window, call the following cmdlet to redeploy your hosted service to Azure.</span></span>

```powershell
PS C:\node\tasklist\WebRole1> Publish-AzureServiceProject -name myuniquename -location datacentername -launch
```

<span data-ttu-id="10787-185">Sostituire **myuniquename** con un nome univoco per questa applicazione.</span><span class="sxs-lookup"><span data-stu-id="10787-185">Replace **myuniquename** with a unique name for this application.</span></span> <span data-ttu-id="10787-186">Sostituire **datacentername** con il nome di un data center di Azure, ad esempio **Stati Uniti occidentali**.</span><span class="sxs-lookup"><span data-stu-id="10787-186">Replace **datacentername** with the name of an Azure data center, such as **West US**.</span></span>

<span data-ttu-id="10787-187">Al termine della distribuzione, verrà visualizzata una risposta analoga alla seguente:</span><span class="sxs-lookup"><span data-stu-id="10787-187">After the deployment is complete, you should see a response similar to the following:</span></span>

```
  PS C:\node\tasklist> publish-azureserviceproject -servicename tasklist -location "West US"
  WARNING: Publishing tasklist to Microsoft Azure. This may take several minutes...
  WARNING: 2:18:42 PM - Preparing runtime deployment for service 'tasklist'
  WARNING: 2:18:42 PM - Verifying storage account 'tasklist'...
  WARNING: 2:18:43 PM - Preparing deployment for tasklist with Subscription ID: 65a1016d-0f67-45d2-b838-b8f373d6d52e...
  WARNING: 2:19:01 PM - Connecting...
  WARNING: 2:19:02 PM - Uploading Package to storage service larrystore...
  WARNING: 2:19:40 PM - Upgrading...
  WARNING: 2:22:48 PM - Created Deployment ID: b7134ab29b1249ff84ada2bd157f296a.
  WARNING: 2:22:48 PM - Initializing...
  WARNING: 2:22:49 PM - Instance WebRole1_IN_0 of role WebRole1 is ready.
  WARNING: 2:22:50 PM - Created Website URL: http://tasklist.cloudapp.net/.
```

<span data-ttu-id="10787-188">Avendo specificato l'opzione **-launch** nel cdmlet precedente, il browser si apre e visualizza l'applicazione in esecuzione in Azure al termine della pubblicazione.</span><span class="sxs-lookup"><span data-stu-id="10787-188">By specifying the **-launch** option in the previous cmdlet, the browser opens and displays your application running in Azure when publishing is completed.</span></span>

![Finestra del browser in cui è visualizzata la pagina My Task List.](./media/table-storage-cloud-service-nodejs/getting-started-1.png)

## <a name="stopping-and-deleting-your-application"></a><span data-ttu-id="10787-191">Arresto ed eliminazione dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="10787-191">Stopping and Deleting Your Application</span></span>
<span data-ttu-id="10787-192">Dopo aver distribuito l'applicazione, se necessario è possibile disabilitarla per evitare costi o creare e distribuire altre applicazioni entro il termine del periodo di valutazione gratuita.</span><span class="sxs-lookup"><span data-stu-id="10787-192">After deploying your application, you may want to disable it so you can avoid costs or build and deploy other applications within the free trial time period.</span></span>

<span data-ttu-id="10787-193">Azure addebita le istanze del ruolo Web al consumo, in base all'utilizzo di tempo del server su base oraria.</span><span class="sxs-lookup"><span data-stu-id="10787-193">Azure bills web role instances per hour of server time consumed.</span></span>
<span data-ttu-id="10787-194">Un'applicazione distribuita utilizza tempo del server anche se le istanze non sono in esecuzione e sono in stato arrestato.</span><span class="sxs-lookup"><span data-stu-id="10787-194">Server time is consumed once your application is deployed, even if the instances are not running and are in the stopped state.</span></span>

<span data-ttu-id="10787-195">Nella procedura seguente viene illustrato come arrestare ed eliminare l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="10787-195">The following steps show you how to stop and delete your application.</span></span>

1. <span data-ttu-id="10787-196">Nella finestra di Windows PowerShell arrestare la distribuzione del servizio creato nella sezione precedente con il cmdlet seguente:</span><span class="sxs-lookup"><span data-stu-id="10787-196">In the Windows PowerShell window, stop the service deployment created in the previous section with the following cmdlet:</span></span>

    ```powershell
    PS C:\node\tasklist\WebRole1> Stop-AzureService
    ```

   <span data-ttu-id="10787-197">L'arresto del servizio può richiedere diversi minuti.</span><span class="sxs-lookup"><span data-stu-id="10787-197">Stopping the service may take several minutes.</span></span> <span data-ttu-id="10787-198">Dopo l'arresto del servizio, viene visualizzato un messaggio di conferma dell'arresto.</span><span class="sxs-lookup"><span data-stu-id="10787-198">When the service is stopped, you receive a message indicating that it has stopped.</span></span>

2. <span data-ttu-id="10787-199">Per eliminare il servizio, chiamare il cmdlet seguente:</span><span class="sxs-lookup"><span data-stu-id="10787-199">To delete the service, call the following cmdlet:</span></span>

    ```powershell
    PS C:\node\tasklist\WebRole1> Remove-AzureService contosotasklist
    ```

   <span data-ttu-id="10787-200">Quando richiesto, immettere **Y** per eliminare il servizio.</span><span class="sxs-lookup"><span data-stu-id="10787-200">When prompted, enter **Y** to delete the service.</span></span>

   <span data-ttu-id="10787-201">L'eliminazione del servizio può richiedere diversi minuti.</span><span class="sxs-lookup"><span data-stu-id="10787-201">Deleting the service may take several minutes.</span></span> <span data-ttu-id="10787-202">Al termine della procedura di eliminazione del servizio, verrà visualizzato un messaggio di conferma dell'eliminazione.</span><span class="sxs-lookup"><span data-stu-id="10787-202">After the service is deleted, you will receive a message indicating that the service was deleted.</span></span>

[Creazione di un'applicazione Web Node.js usando Express in un servizio cloud di Azure]: http://azure.microsoft.com/develop/nodejs/tutorials/web-app-with-express/
[Archiviazione e accesso ai dati in Azure]: http://msdn.microsoft.com/library/azure/gg433040.aspx
[Creazione e distribuzione di un'applicazione Node.js a un Servizio cloud di Azure]: http://azure.microsoft.com/develop/nodejs/tutorials/getting-started/


