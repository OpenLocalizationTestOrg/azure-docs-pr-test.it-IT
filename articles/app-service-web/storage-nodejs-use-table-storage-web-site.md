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
# <a name="nodejs-web-app-using-the-azure-table-service"></a><span data-ttu-id="213d1-103">App Web Node.js con il servizio tabelle di Azure</span><span class="sxs-lookup"><span data-stu-id="213d1-103">Node.js web app using the Azure Table Service</span></span>
## <a name="overview"></a><span data-ttu-id="213d1-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="213d1-104">Overview</span></span>
<span data-ttu-id="213d1-105">In questa esercitazione viene illustrato come usare il servizio tabelle fornito da Gestione dati di Azure per archiviare e accedere ai dati da un'applicazione [node] ospitata nel [servizio App di Azure](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="213d1-105">This tutorial shows you how to use Table service provided by Azure Data Management to store and access data from a [node] application hosted in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web Apps.</span></span> <span data-ttu-id="213d1-106">In questa esercitazione si presuppone che l'utente abbia già utilizzato l'applicazione Node e [Git].</span><span class="sxs-lookup"><span data-stu-id="213d1-106">This tutorial assumes that you have some prior experience using node and [Git].</span></span>

<span data-ttu-id="213d1-107">Si acquisiranno le nozioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="213d1-107">You will learn:</span></span>

* <span data-ttu-id="213d1-108">Usare npm (Node Package Manager) per installare i moduli di Node</span><span class="sxs-lookup"><span data-stu-id="213d1-108">How to use npm (node package manager) to install the node modules</span></span>
* <span data-ttu-id="213d1-109">Utilizzare il servizio tabelle di Azure</span><span class="sxs-lookup"><span data-stu-id="213d1-109">How to work with the Azure Table service</span></span>
* <span data-ttu-id="213d1-110">Come usare l'interfaccia della riga di comando di Azure per creare un'app Web.</span><span class="sxs-lookup"><span data-stu-id="213d1-110">How to use the Azure CLI to create a web app.</span></span>

<span data-ttu-id="213d1-111">In questa esercitazione verrà creata una semplice applicazione di "elenco attività" basata su Web che consente di creare, recuperare e completare le attività.</span><span class="sxs-lookup"><span data-stu-id="213d1-111">By following this tutorial, you will build a simple web-based "to-do list" application that allows creating, retrieving and completing tasks.</span></span> <span data-ttu-id="213d1-112">Le attività vengono archiviate nel servizio tabelle.</span><span class="sxs-lookup"><span data-stu-id="213d1-112">The tasks are stored in the Table service.</span></span>

<span data-ttu-id="213d1-113">Di seguito è riportata l'applicazione completata:</span><span class="sxs-lookup"><span data-stu-id="213d1-113">Here is the completed application:</span></span>

![Pagina Web con un elenco di attività vuoto][node-table-finished]

> [!NOTE]
> <span data-ttu-id="213d1-115">Per iniziare a usare Servizio app di Azure prima di registrarsi per ottenere un account Azure, andare a [Prova il servizio app](https://azure.microsoft.com/try/app-service/), dove è possibile creare un'app Web iniziale temporanea nel servizio app.</span><span class="sxs-lookup"><span data-stu-id="213d1-115">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="213d1-116">Non è necessario fornire una carta di credito né impegnarsi in alcun modo.</span><span class="sxs-lookup"><span data-stu-id="213d1-116">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="213d1-117">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="213d1-117">Prerequisites</span></span>
<span data-ttu-id="213d1-118">Prima di seguire le istruzioni di questo articolo, verificare che siano installati i seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="213d1-118">Before following the instructions in this article, ensure that you have the following installed:</span></span>

* <span data-ttu-id="213d1-119">[node] 0.10.24 o versione successiva</span><span class="sxs-lookup"><span data-stu-id="213d1-119">[node] version 0.10.24 or higher</span></span>
* <span data-ttu-id="213d1-120">[Git]</span><span class="sxs-lookup"><span data-stu-id="213d1-120">[Git]</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

## <a name="create-a-storage-account"></a><span data-ttu-id="213d1-121">Creare un account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="213d1-121">Create a storage account</span></span>
<span data-ttu-id="213d1-122">Creare un account di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="213d1-122">Create an Azure storage account.</span></span> <span data-ttu-id="213d1-123">L'app utilizzerà questo account per archiviare gli elementi dell'elenco attività.</span><span class="sxs-lookup"><span data-stu-id="213d1-123">The app will use this account to store the to-do items.</span></span>

1. <span data-ttu-id="213d1-124">Accedere al [Portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="213d1-124">Log into the [Azure Portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="213d1-125">Fare clic sull'icona **Nuovo** nella parte inferiore sinistra del portale, quindi fare clic su **Dati e archiviazione** > **Archiviazione**.</span><span class="sxs-lookup"><span data-stu-id="213d1-125">Click the **New** icon on the bottom left of the portal, then click **Data + Storage** > **Storage**.</span></span> <span data-ttu-id="213d1-126">Assegnare un nome univoco all'account di archiviazione e creare un nuovo [gruppo di risorse](../azure-resource-manager/resource-group-overview.md) correlato.</span><span class="sxs-lookup"><span data-stu-id="213d1-126">Give the storage account a unique name and create a new [resource group](../azure-resource-manager/resource-group-overview.md) for it.</span></span>
   
      ![Pulsante Nuovo](./media/storage-nodejs-use-table-storage-web-site/configure-storage.png)
   
    <span data-ttu-id="213d1-128">Quando l'account di archiviazione viene creato, nel pulsante **Notifiche** lampeggia in verde il testo **OPERAZIONE RIUSCITA** e il pannello dell'account di archiviazione si apre per visualizzare che appartiene al nuovo gruppo di risorse creato.</span><span class="sxs-lookup"><span data-stu-id="213d1-128">When the storage account has been created, the **Notifications** button will flash a green **SUCCESS** and the storage account's blade is open to show that it belongs to the new resource group you created.</span></span>
3. <span data-ttu-id="213d1-129">Nel pannello dell'account di archiviazione fare clic su **Impostazioni** > **Chiavi**.</span><span class="sxs-lookup"><span data-stu-id="213d1-129">In the storage account's blade, click **Settings** > **Keys**.</span></span> <span data-ttu-id="213d1-130">Copiare la chiave di accesso primaria negli Appunti.</span><span class="sxs-lookup"><span data-stu-id="213d1-130">Copy the primary access key to the clipboard.</span></span>
   
    ![Chiave di accesso][portal-storage-access-keys]

## <a name="install-modules-and-generate-scaffolding"></a><span data-ttu-id="213d1-132">Installazione dei moduli e generazione dello scaffolding</span><span class="sxs-lookup"><span data-stu-id="213d1-132">Install modules and generate scaffolding</span></span>
<span data-ttu-id="213d1-133">In questa sezione verrà creata una nuova applicazione Node e verrà utilizzato npm per aggiungere pacchetti di modulo.</span><span class="sxs-lookup"><span data-stu-id="213d1-133">In this section you will create a new Node application and use npm to add module packages.</span></span> <span data-ttu-id="213d1-134">Per questa applicazione verranno usati i moduli [Express] e [Azure].</span><span class="sxs-lookup"><span data-stu-id="213d1-134">For this application you will use the [Express] and [Azure] modules.</span></span> <span data-ttu-id="213d1-135">Il modulo Express fornisce un modello di framework View Controller per Node, mentre i moduli Azure forniscono la connettività al servizio tabelle.</span><span class="sxs-lookup"><span data-stu-id="213d1-135">The Express module provides a Model View Controller framework for node, while the Azure modules provides connectivity to the Table service.</span></span>

### <a name="install-express-and-generate-scaffolding"></a><span data-ttu-id="213d1-136">Installare Express e generare lo scaffolding</span><span class="sxs-lookup"><span data-stu-id="213d1-136">Install express and generate scaffolding</span></span>
1. <span data-ttu-id="213d1-137">Nella riga di comando creare una nuova directory denominata **elenco attività** e passare a tale directory.</span><span class="sxs-lookup"><span data-stu-id="213d1-137">From the command line, create a new directory named **tasklist** and switch to that directory.</span></span>  
2. <span data-ttu-id="213d1-138">Immettere il comando seguente per installare il modulo Express.</span><span class="sxs-lookup"><span data-stu-id="213d1-138">Enter the following command to install the Express module.</span></span>
   
        npm install express-generator@4.2.0 -g
   
    <span data-ttu-id="213d1-139">A seconda del sistema operativo, potrebbe essere necessario inserire l'elevazione "sudo" prima del comando:</span><span class="sxs-lookup"><span data-stu-id="213d1-139">Depending on the operating system, you may need to put 'sudo' before the command:</span></span>
   
        sudo npm install express-generator@4.2.0 -g
   
    <span data-ttu-id="213d1-140">L'output appare simile all'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="213d1-140">The output appears similar to the following example:</span></span>
   
        express-generator@4.2.0 /usr/local/lib/node_modules/express-generator
        ├── mkdirp@0.3.5
        └── commander@1.3.2 (keypress@0.1.0)
   
   > [!NOTE]
   > <span data-ttu-id="213d1-141">Il parametro "-g" consente di installare il modulo a livello globale.</span><span class="sxs-lookup"><span data-stu-id="213d1-141">The '-g' parameter installs the module globally.</span></span> <span data-ttu-id="213d1-142">In questo modo, è possibile usare **express** per generare lo scaffolding dell'app Web senza dover inserire informazioni aggiuntive sul percorso.</span><span class="sxs-lookup"><span data-stu-id="213d1-142">That way, we can use **express** to generate web app scaffolding without having to type in additional path information.</span></span>
   > 
   > 
3. <span data-ttu-id="213d1-143">Per creare lo scaffolding per l'applicazione, immettere il comando **express** :</span><span class="sxs-lookup"><span data-stu-id="213d1-143">To create the scaffolding for the application, enter the **express** command:</span></span>
   
        express
   
    <span data-ttu-id="213d1-144">L'output di questo comando appare simile al seguente esempio:</span><span class="sxs-lookup"><span data-stu-id="213d1-144">The output of this command appears similar to the following example:</span></span>
   
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
   
    <span data-ttu-id="213d1-145">Nella directory **tasklist** sono ora disponibili diverse nuove directory e file.</span><span class="sxs-lookup"><span data-stu-id="213d1-145">You now have several new directories and files in the **tasklist** directory.</span></span>

### <a name="install-additional-modules"></a><span data-ttu-id="213d1-146">Installare moduli aggiuntivi</span><span class="sxs-lookup"><span data-stu-id="213d1-146">Install additional modules</span></span>
<span data-ttu-id="213d1-147">Uno dei file creati da **express** è **package.json**.</span><span class="sxs-lookup"><span data-stu-id="213d1-147">One of the files that **express** creates is **package.json**.</span></span> <span data-ttu-id="213d1-148">Questo file contiene un elenco di dipendenze del modulo.</span><span class="sxs-lookup"><span data-stu-id="213d1-148">This file contains a list of module dependencies.</span></span> <span data-ttu-id="213d1-149">In seguito, quando si distribuirà l'applicazione nelle app Web del servizio app, questo file consentirà di determinare i moduli da installare in Azure.</span><span class="sxs-lookup"><span data-stu-id="213d1-149">Later, when you deploy the application to App Service Web Apps, this file determines which modules need to be installed on Azure.</span></span>

<span data-ttu-id="213d1-150">Nella riga di comando, per installare i moduli descritti nel file **package.json** , immettere il comando riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="213d1-150">From the command-line, enter the following command to install the modules described in the **package.json** file.</span></span> <span data-ttu-id="213d1-151">Potrebbe essere necessario utilizzare l'elevazione "sudo".</span><span class="sxs-lookup"><span data-stu-id="213d1-151">You may need to use 'sudo'.</span></span>

    npm install

<span data-ttu-id="213d1-152">L'output di questo comando appare simile al seguente esempio:</span><span class="sxs-lookup"><span data-stu-id="213d1-152">The output of this command appears similar to the following example:</span></span>

    debug@0.7.4 node_modules\debug

    cookie-parser@1.0.1 node_modules\cookie-parser
    ├── cookie-signature@1.0.3
    └── cookie@0.1.0

    [...]


<span data-ttu-id="213d1-153">Successivamente, immettere il comando riportato di seguito per installare i moduli [azure], [node-uuid], [nconf] e [async]:</span><span class="sxs-lookup"><span data-stu-id="213d1-153">Next, enter the following command to install the [azure], [node-uuid], [nconf] and [async] modules:</span></span>

    npm install azure-storage node-uuid async nconf --save

<span data-ttu-id="213d1-154">Il flag **--save** consente di aggiungere voci per questi moduli al file **package.json**.</span><span class="sxs-lookup"><span data-stu-id="213d1-154">The **--save** flag adds entries for these modules to the **package.json** file.</span></span>

<span data-ttu-id="213d1-155">L'output di questo comando appare simile al seguente esempio:</span><span class="sxs-lookup"><span data-stu-id="213d1-155">The output of this command appears similar to the following example:</span></span>

    async@0.9.0 node_modules\async

    node-uuid@1.4.1 node_modules\node-uuid

    nconf@0.6.9 node_modules\nconf
    ├── ini@1.2.1
    ├── async@0.2.9
    └── optimist@0.6.0 (wordwrap@0.0.2, minimist@0.0.10)

    [...]


## <a name="create-the-application"></a><span data-ttu-id="213d1-156">Creazione dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="213d1-156">Create the application</span></span>
<span data-ttu-id="213d1-157">A questo punto, è possibile compilare l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="213d1-157">Now we're ready to build the application.</span></span>

### <a name="create-a-model"></a><span data-ttu-id="213d1-158">Creare il modello</span><span class="sxs-lookup"><span data-stu-id="213d1-158">Create a model</span></span>
<span data-ttu-id="213d1-159">Un *modello* è un oggetto che rappresenta i dati nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="213d1-159">A *model* is an object that represents the data in your application.</span></span> <span data-ttu-id="213d1-160">Per l'applicazione, l'unico modello è l'oggetto attività, che rappresenta un elemento nell'elenco attività.</span><span class="sxs-lookup"><span data-stu-id="213d1-160">For the application, the only model is a task object, which represents an item in the to-do list.</span></span> <span data-ttu-id="213d1-161">Le attività saranno dotate dei campi seguenti:</span><span class="sxs-lookup"><span data-stu-id="213d1-161">Tasks will have the following fields:</span></span>

* <span data-ttu-id="213d1-162">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="213d1-162">PartitionKey</span></span>
* <span data-ttu-id="213d1-163">RowKey</span><span class="sxs-lookup"><span data-stu-id="213d1-163">RowKey</span></span>
* <span data-ttu-id="213d1-164">name (string)</span><span class="sxs-lookup"><span data-stu-id="213d1-164">name (string)</span></span>
* <span data-ttu-id="213d1-165">category (string)</span><span class="sxs-lookup"><span data-stu-id="213d1-165">category (string)</span></span>
* <span data-ttu-id="213d1-166">completed (Boolean)</span><span class="sxs-lookup"><span data-stu-id="213d1-166">completed (Boolean)</span></span>

<span data-ttu-id="213d1-167">Il servizio tabelle usa **PartitionKey** e **RowKey** come chiavi delle tabelle.</span><span class="sxs-lookup"><span data-stu-id="213d1-167">**PartitionKey** and **RowKey** are used by the Table Service as table keys.</span></span> <span data-ttu-id="213d1-168">Per altre informazioni, vedere [Informazioni sul modello di dati del servizio tabelle](https://msdn.microsoft.com/library/azure/dd179338.aspx).</span><span class="sxs-lookup"><span data-stu-id="213d1-168">For more information, see [Understanding the Table Service data model](https://msdn.microsoft.com/library/azure/dd179338.aspx).</span></span>

1. <span data-ttu-id="213d1-169">Nella directory **tasklist** creare una nuova directory denominata **models**.</span><span class="sxs-lookup"><span data-stu-id="213d1-169">In the **tasklist** directory, create a new directory named **models**.</span></span>
2. <span data-ttu-id="213d1-170">Nella directory **models** creare un nuovo file denominato **task.js**.</span><span class="sxs-lookup"><span data-stu-id="213d1-170">In the **models** directory, create a new file named **task.js**.</span></span> <span data-ttu-id="213d1-171">Questo file conterrà il modello per le attività create dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="213d1-171">This file will contain the model for the tasks created by your application.</span></span>
3. <span data-ttu-id="213d1-172">All'inizio del file **task.js** , aggiungere il codice seguente per fare riferimento alle librerie necessarie:</span><span class="sxs-lookup"><span data-stu-id="213d1-172">At the beginning of the **task.js** file, add the following code to reference required libraries:</span></span>
   
        var azure = require('azure-storage');
          var uuid = require('node-uuid');
        var entityGen = azure.TableUtilities.entityGenerator;
4. <span data-ttu-id="213d1-173">Aggiungere il codice seguente per definire ed esportare l'oggetto Task.</span><span class="sxs-lookup"><span data-stu-id="213d1-173">Add the following code to define and export the Task object.</span></span> <span data-ttu-id="213d1-174">Tale oggetto è responsabile per la connessione alla tabella.</span><span class="sxs-lookup"><span data-stu-id="213d1-174">This object is responsible for connecting to the table.</span></span>
   
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
5. <span data-ttu-id="213d1-175">Aggiungere il codice seguente per definire metodi aggiuntivi nell'oggetto Task che consentano le interazioni con i dati archiviati nella tabella:</span><span class="sxs-lookup"><span data-stu-id="213d1-175">Add the following code to define additional methods on the Task object, which allow interactions with data stored in the table:</span></span>
   
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
6. <span data-ttu-id="213d1-176">Salvare e chiudere il file **task.js** .</span><span class="sxs-lookup"><span data-stu-id="213d1-176">Save and close the **task.js** file.</span></span>

### <a name="create-a-controller"></a><span data-ttu-id="213d1-177">Creare un controller</span><span class="sxs-lookup"><span data-stu-id="213d1-177">Create a controller</span></span>
<span data-ttu-id="213d1-178">Un *controller* consente di gestire le richieste HTTP ed eseguire il rendering delle risposte HTML.</span><span class="sxs-lookup"><span data-stu-id="213d1-178">A *controller* handles HTTP requests and renders the HTML response.</span></span>

1. <span data-ttu-id="213d1-179">Nella directory **tasklist/routes** creare un nuovo file denominato **tasklist.js** e aprirlo in un editor di testo.</span><span class="sxs-lookup"><span data-stu-id="213d1-179">In the **tasklist/routes** directory, create a new file named **tasklist.js** and open it in a text editor.</span></span>
2. <span data-ttu-id="213d1-180">Aggiungere il seguente codice al file **tasklist.js**.</span><span class="sxs-lookup"><span data-stu-id="213d1-180">Add the following code to **tasklist.js**.</span></span> <span data-ttu-id="213d1-181">Ciò consente il caricamento dei moduli di Azure e di quelli asincroni, utilizzati da **tasklist.js**.</span><span class="sxs-lookup"><span data-stu-id="213d1-181">This loads the azure and async modules, which are used by **tasklist.js**.</span></span> <span data-ttu-id="213d1-182">Viene inoltre definita la funzione **TaskList**, che viene passata come un'istanza dell'oggetto **Task** definito in precedenza:</span><span class="sxs-lookup"><span data-stu-id="213d1-182">This also defines the **TaskList** function, which is passed an instance of the **Task** object we defined earlier:</span></span>
   
        var azure = require('azure-storage');
        var async = require('async');
   
        module.exports = TaskList;
3. <span data-ttu-id="213d1-183">Definire un oggetto **TaskList** .</span><span class="sxs-lookup"><span data-stu-id="213d1-183">Define a **TaskList** object.</span></span>
   
        function TaskList(task) {
          this.task = task;
        }
4. <span data-ttu-id="213d1-184">Aggiungere i metodi seguenti a **TaskList**:</span><span class="sxs-lookup"><span data-stu-id="213d1-184">Add the following methods to **TaskList**:</span></span>
   
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

### <a name="modify-appjs"></a><span data-ttu-id="213d1-185">Modificare il file app.js</span><span class="sxs-lookup"><span data-stu-id="213d1-185">Modify app.js</span></span>
1. <span data-ttu-id="213d1-186">Nella directory **tasklist** aprire il file **app.js**.</span><span class="sxs-lookup"><span data-stu-id="213d1-186">From the **tasklist** directory, open the **app.js** file.</span></span> <span data-ttu-id="213d1-187">Questo file è stato creato in precedenza eseguendo il comando **express** .</span><span class="sxs-lookup"><span data-stu-id="213d1-187">This file was created earlier by running the **express** command.</span></span>
2. <span data-ttu-id="213d1-188">Aggiungere quanto riportato di seguito all'inizio del file per caricare il modulo di Azure, impostare il nome della tabella, la chiave di partizione, e impostare le credenziali di archiviazione usate da questo esempio:</span><span class="sxs-lookup"><span data-stu-id="213d1-188">At the beginning of the file, add the following to load the azure module, set the table name, partition key, and set the storage credentials used by this example:</span></span>
   
        var azure = require('azure-storage');
        var nconf = require('nconf');
        nconf.env()
             .file({ file: 'config.json', search: true });
        var tableName = nconf.get("TABLE_NAME");
        var partitionKey = nconf.get("PARTITION_KEY");
        var accountName = nconf.get("STORAGE_NAME");
        var accountKey = nconf.get("STORAGE_KEY");
   
   > [!NOTE]
   > <span data-ttu-id="213d1-189">nconf caricherà i valori di configurazione dalle variabili di ambiente oppure dal file **config.json** , che verrà creato più avanti.</span><span class="sxs-lookup"><span data-stu-id="213d1-189">nconf will load the configuration values from either environment variables or the **config.json** file, which we will create later.</span></span>
   > 
   > 
3. <span data-ttu-id="213d1-190">Nel file app.js scorrere verso il basso fino a individuare la riga seguente:</span><span class="sxs-lookup"><span data-stu-id="213d1-190">In the app.js file, scroll down to where you see the following line:</span></span>
   
        app.use('/', routes);
        app.use('/users', users);
   
    <span data-ttu-id="213d1-191">Sostituire le righe sopra con il codice seguente.</span><span class="sxs-lookup"><span data-stu-id="213d1-191">Replace the above lines with the code shown below.</span></span> <span data-ttu-id="213d1-192">Verrà in tal modo inizializzata un'istanza di <strong>Task</strong> con una connessione all'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="213d1-192">This will initialize an instance of <strong>Task</strong> with a connection to your storage account.</span></span> <span data-ttu-id="213d1-193">Questa viene quindi passata a <strong>TaskList</strong>, che la userà per la comunicazione con il servizio tabelle:</span><span class="sxs-lookup"><span data-stu-id="213d1-193">This is passed to the <strong>TaskList</strong>, which will use it to communicate with the Table service:</span></span>
   
        var TaskList = require('./routes/tasklist');
        var Task = require('./models/task');
        var task = new Task(azure.createTableService(accountName, accountKey), tableName, partitionKey);
        var taskList = new TaskList(task);
   
        app.get('/', taskList.showTasks.bind(taskList));
        app.post('/addtask', taskList.addTask.bind(taskList));
        app.post('/completetask', taskList.completeTask.bind(taskList));
4. <span data-ttu-id="213d1-194">Salvare il file **app.js** .</span><span class="sxs-lookup"><span data-stu-id="213d1-194">Save the **app.js** file.</span></span>

### <a name="modify-the-index-view"></a><span data-ttu-id="213d1-195">Modificare la visualizzazione dell'indice</span><span class="sxs-lookup"><span data-stu-id="213d1-195">Modify the index view</span></span>
1. <span data-ttu-id="213d1-196">Aprire il file **tasklist/views/index.jade** in un editor di testo.</span><span class="sxs-lookup"><span data-stu-id="213d1-196">Open the **tasklist/views/index.jade** file in a text editor.</span></span>
2. <span data-ttu-id="213d1-197">Sostituire l'intero contenuto del file con il codice seguente.</span><span class="sxs-lookup"><span data-stu-id="213d1-197">Replace the entire contents of the file with the following code.</span></span> <span data-ttu-id="213d1-198">Ciò consente di definire una visualizzazione delle attività esistenti e includere un modulo per aggiungere nuove attività e contrassegnare quelle esistenti come completate.</span><span class="sxs-lookup"><span data-stu-id="213d1-198">This defines a view that displays existing tasks and includes a form for adding new tasks and marking existing ones as completed.</span></span>
   
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
3. <span data-ttu-id="213d1-199">Salvare e chiudere il file **index.jade** .</span><span class="sxs-lookup"><span data-stu-id="213d1-199">Save and close **index.jade** file.</span></span>

### <a name="modify-the-global-layout"></a><span data-ttu-id="213d1-200">Modificare il layout globale</span><span class="sxs-lookup"><span data-stu-id="213d1-200">Modify the global layout</span></span>
<span data-ttu-id="213d1-201">Il file **layout.jade** nella directory **views** è un modello globale per altri file **.jade**.</span><span class="sxs-lookup"><span data-stu-id="213d1-201">The **layout.jade** file in the **views** directory is a global template for other **.jade** files.</span></span> <span data-ttu-id="213d1-202">In questo passaggio verrà modificato in modo da utilizzare [Twitter Bootstrap](https://github.com/twbs/bootstrap), un toolkit che semplifica la progettazione di un'app Web di aspetto gradevole.</span><span class="sxs-lookup"><span data-stu-id="213d1-202">In this step you will modify it to use [Twitter Bootstrap](https://github.com/twbs/bootstrap), which is a toolkit that makes it easy to design a nice looking web app.</span></span>

<span data-ttu-id="213d1-203">Scaricare ed estrarre i file per [Twitter Bootstrap](http://getbootstrap.com/).</span><span class="sxs-lookup"><span data-stu-id="213d1-203">Download and extract the files for [Twitter Bootstrap](http://getbootstrap.com/).</span></span> <span data-ttu-id="213d1-204">Copiare il file **bootstrap.min.css** dalla cartella **css** di Bootstrap nella directory **public/stylesheets** dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="213d1-204">Copy the **bootstrap.min.css** file from the Bootstrap **css** folder into the **public/stylesheets** directory of your application.</span></span>

<span data-ttu-id="213d1-205">Dalla cartella **views** aprire **layout.jade** e sostituire l'intero contenuto con quello seguente:</span><span class="sxs-lookup"><span data-stu-id="213d1-205">From the **views** folder, open **layout.jade** and replace the entire contents with the following:</span></span>

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

### <a name="create-a-config-file"></a><span data-ttu-id="213d1-206">Creare un file config</span><span class="sxs-lookup"><span data-stu-id="213d1-206">Create a config file</span></span>
<span data-ttu-id="213d1-207">Per eseguire l'app a livello locale, verranno inserite le credenziali di Archiviazione di Azure in un file config.</span><span class="sxs-lookup"><span data-stu-id="213d1-207">To run the app locally, we'll put Azure Storage credentials into a config file.</span></span> <span data-ttu-id="213d1-208">Creare un file denominato **config.json** con il contenuto JSON seguente:</span><span class="sxs-lookup"><span data-stu-id="213d1-208">Create a file named **config.json* *with the following JSON:</span></span>

    {
        "STORAGE_NAME": "<storage account name>",
        "STORAGE_KEY": "<storage access key>",
        "PARTITION_KEY": "mytasks",
        "TABLE_NAME": "tasks"
    }

<span data-ttu-id="213d1-209">Sostituire **storage account name** con il nome dell'account di archiviazione creato in precedenza e sostituire **storage access key** con la chiave di accesso primaria per l'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="213d1-209">Replace **storage account name** with the name of the storage account you created earlier, and replace **storage access key** with the primary access key for your storage account.</span></span> <span data-ttu-id="213d1-210">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="213d1-210">For example:</span></span>

    {
        "STORAGE_NAME": "nodejsappstorage",
        "STORAGE_KEY": "KG0oDd..."
        "PARTITION_KEY": "mytasks",
        "TABLE_NAME": "tasks"
    }

<span data-ttu-id="213d1-211">Salvare il file *al livello di directory superiore* rispetto alla directory **tasklist** , come mostrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="213d1-211">Save this file *one directory level higher* than the **tasklist** directory, like this:</span></span>

    parent/
      |-- config.json
      |-- tasklist/

<span data-ttu-id="213d1-212">Tale operazione è necessaria per evitare di verificare il file config nel controllo del codice sorgente, in cui potrebbe diventare pubblico.</span><span class="sxs-lookup"><span data-stu-id="213d1-212">The reason for doing this is to avoid checking the config file into source control, where it might become public.</span></span> <span data-ttu-id="213d1-213">Quando si distribuisce l'app in Azure, si usano le variabili di ambiente invece di un file config.</span><span class="sxs-lookup"><span data-stu-id="213d1-213">When we deploy the app to Azure, we will use environment variables instead of a config file.</span></span>

## <a name="run-the-application-locally"></a><span data-ttu-id="213d1-214">Eseguire l'applicazione in locale</span><span class="sxs-lookup"><span data-stu-id="213d1-214">Run the application locally</span></span>
<span data-ttu-id="213d1-215">Per eseguire il test dell'applicazione nel computer locale, eseguire la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="213d1-215">To test the application on your local machine, perform the following steps:</span></span>

1. <span data-ttu-id="213d1-216">Dalla riga di comando passare alla directory **tasklist** .</span><span class="sxs-lookup"><span data-stu-id="213d1-216">From the command-line, change directories to the **tasklist** directory.</span></span>
2. <span data-ttu-id="213d1-217">Usare il comando seguente per avviare l'applicazione in locale:</span><span class="sxs-lookup"><span data-stu-id="213d1-217">Use the following command to launch the application locally:</span></span>
   
        npm start
3. <span data-ttu-id="213d1-218">Aprire un Web browser e passare all'indirizzo http://127.0.0.1:3000.</span><span class="sxs-lookup"><span data-stu-id="213d1-218">Open a web browser and navigate to http://127.0.0.1:3000.</span></span>
   
    <span data-ttu-id="213d1-219">Verrà visualizzata una pagina Web simile all'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="213d1-219">A web page similar to the following example appears.</span></span>
   
    ![Pagina Web con un elenco di attività vuoto][node-table-finished]
4. <span data-ttu-id="213d1-221">Per creare una nuova attività, immettere un nome e una categoria e fare clic su **Aggiungi elemento**.</span><span class="sxs-lookup"><span data-stu-id="213d1-221">To create a new to-do item, enter a name and category and click **Add Item**.</span></span> 
5. <span data-ttu-id="213d1-222">Per contrassegnare un'attività come completata, selezionare **Completa** e fare clic su **Aggiorna attività**.</span><span class="sxs-lookup"><span data-stu-id="213d1-222">To mark a task as complete, check **Complete** and click **Update Tasks**.</span></span>
   
    ![Immagine del nuovo elemento nell'elenco delle attività][node-table-list-items]

<span data-ttu-id="213d1-224">Anche se l'applicazione è in esecuzione in locale, i dati vengono archiviati nel servizio tabelle di Azure.</span><span class="sxs-lookup"><span data-stu-id="213d1-224">Even though the application is running locally, it is storing the data in the Azure Table service.</span></span>

## <a name="deploy-your-application-to-azure"></a><span data-ttu-id="213d1-225">Distribuire l'applicazione in Azure</span><span class="sxs-lookup"><span data-stu-id="213d1-225">Deploy your application to Azure</span></span>
<span data-ttu-id="213d1-226">Nei passaggi di questa sezione vengono usati gli strumenti da riga di comando di Azure per creare una nuova app Web nel servizio app e viene usato Git per distribuire l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="213d1-226">The steps in this section use the Azure command-line tools to create a new web app in App Service, and then use Git to deploy your application.</span></span> <span data-ttu-id="213d1-227">Per eseguire questi passaggi, è necessario disporre di una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="213d1-227">To perform these steps you must have an Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="213d1-228">È possibile eseguire queste procedure anche nel [Portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="213d1-228">These steps can also be performed by using the [Azure Portal](https://portal.azure.com/).</span></span> <span data-ttu-id="213d1-229">Vedere [Creazione e distribuzione di un'app Web Node.js nel Azure App Service].</span><span class="sxs-lookup"><span data-stu-id="213d1-229">See [Build and deploy a Node.js web app in Azure App Service].</span></span>
> 
> <span data-ttu-id="213d1-230">Se questa è la prima app Web di Azure che si crea, per distribuire l'applicazione è necessario utilizzare il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="213d1-230">If this is the first web app you have created, you must use the Azure Portal to deploy this application.</span></span>
> 
> 

<span data-ttu-id="213d1-231">Per iniziare, installare l' [Interfaccia della riga di comando di Azure] immettendo il seguente comando nella riga di comando:</span><span class="sxs-lookup"><span data-stu-id="213d1-231">To get started, install the [Azure CLI] by entering the following command from the command line:</span></span>

    npm install azure-cli -g

### <a name="import-publishing-settings"></a><span data-ttu-id="213d1-232">Importare le impostazioni di pubblicazione</span><span class="sxs-lookup"><span data-stu-id="213d1-232">Import publishing settings</span></span>
<span data-ttu-id="213d1-233">In questo passaggio verrà scaricato un file contenente informazioni sulla sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="213d1-233">In this step, you will download a file containing information about your subscription.</span></span>

1. <span data-ttu-id="213d1-234">Immettere il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="213d1-234">Enter the following command:</span></span>
   
        azure login
   
    <span data-ttu-id="213d1-235">Questo comando consente di avviare un browser e di passare alla pagina per il download.</span><span class="sxs-lookup"><span data-stu-id="213d1-235">This command launches a browser and navigates to the download page.</span></span> <span data-ttu-id="213d1-236">Se richiesto, accedere con l'account associato alla sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="213d1-236">If prompted, log in with the account associated with your Azure subscription.</span></span>
   
    <!-- ![The download page][download-publishing-settings] -->
   
    <span data-ttu-id="213d1-237">Il download del file inizia automaticamente. In caso contrario, è possibile fare clic sul collegamento all'inizio della pagina per scaricare manualmente il file.</span><span class="sxs-lookup"><span data-stu-id="213d1-237">The file download begins automatically; if it does not, you can click the link at the beginning of the page to manually download the file.</span></span> <span data-ttu-id="213d1-238">Salvare il file e prendere nota del percorso del file.</span><span class="sxs-lookup"><span data-stu-id="213d1-238">Save the file and note the file path.</span></span>
2. <span data-ttu-id="213d1-239">Immettere il seguente comando per importare le impostazioni:</span><span class="sxs-lookup"><span data-stu-id="213d1-239">Enter the following command to import the settings:</span></span>
   
        azure account import <path-to-file>
   
    <span data-ttu-id="213d1-240">Specificare il percorso e il nome del file delle impostazioni di pubblicazione scaricato nel passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="213d1-240">Specify the path and file name of the publishing settings file you downloaded in the previous step.</span></span>
3. <span data-ttu-id="213d1-241">Una volta importate le impostazioni, eliminare il file di impostazioni di pubblicazione.</span><span class="sxs-lookup"><span data-stu-id="213d1-241">After the settings are imported, delete the publish settings file.</span></span> <span data-ttu-id="213d1-242">Non è più necessario e contiene informazioni riservate relative alla sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="213d1-242">It is no longer needed, and contains sensitive information regarding your Azure subscription.</span></span>

### <a name="create-an-app-service-web-app"></a><span data-ttu-id="213d1-243">Creare un piano di servizio app</span><span class="sxs-lookup"><span data-stu-id="213d1-243">Create an App Service web app</span></span>
1. <span data-ttu-id="213d1-244">Dalla riga di comando passare alla directory **tasklist** .</span><span class="sxs-lookup"><span data-stu-id="213d1-244">From the command-line, change directories to the **tasklist** directory.</span></span>
2. <span data-ttu-id="213d1-245">Usare il comando seguente per creare una nuova app Web.</span><span class="sxs-lookup"><span data-stu-id="213d1-245">Use the following command to create a new web app.</span></span>
   
        azure site create --git
   
    <span data-ttu-id="213d1-246">Verrà richiesto il nome e il percorso dell'app Web.</span><span class="sxs-lookup"><span data-stu-id="213d1-246">You will be prompted for the web app name and location.</span></span> <span data-ttu-id="213d1-247">Fornire un nome univoco e selezionare la stessa area geografica dell'account di Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="213d1-247">Provide a unique name and select the same geographical location as your Azure Storage account.</span></span>
   
    <span data-ttu-id="213d1-248">Il parametro `--git` consente di creare un archivio GIT per l'app Web in Azure.</span><span class="sxs-lookup"><span data-stu-id="213d1-248">The `--git` parameter creates a Git repository on Azure for this web app.</span></span> <span data-ttu-id="213d1-249">Inoltre consente di inizializzare un archivio GIT nella directory corrente, se non ne esiste nessuno, e di aggiungere un [GIT remoto] denominato "azure", usato per pubblicare l'applicazione in Azure.</span><span class="sxs-lookup"><span data-stu-id="213d1-249">It also initializes a Git repository in the current directory if none exists, and adds a [Git remote] named 'azure', which is used to publish the application to Azure.</span></span> <span data-ttu-id="213d1-250">Infine, consente di creare un file **web.config** contenente le impostazioni usate da Azure per ospitare le applicazioni Node.</span><span class="sxs-lookup"><span data-stu-id="213d1-250">Finally, it creates a **web.config** file, which contains settings used by Azure to host node applications.</span></span> <span data-ttu-id="213d1-251">Se il parametro `--git` viene omesso ma la directory contiene un archivio GIT, il comando consente di creare comunque l'archivio "azure".</span><span class="sxs-lookup"><span data-stu-id="213d1-251">If you omit the `--git` parameter but the directory contains a Git repository, the command will still create the 'azure' remote.</span></span>
   
    <span data-ttu-id="213d1-252">Dopo il completamento di questo comando, verrà visualizzato un output simile al seguente.</span><span class="sxs-lookup"><span data-stu-id="213d1-252">Once this command has completed, you will see output similar to the following.</span></span> <span data-ttu-id="213d1-253">Si noti che la riga che inizia con **Website created at** contiene l'URL dell'app Web.</span><span class="sxs-lookup"><span data-stu-id="213d1-253">Note that the line beginning with **Website created at** contains the URL for the web app.</span></span>
   
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
   > <span data-ttu-id="213d1-254">Se si tratta della prima app Web del servizio app per la sottoscrizione, verrà indicato di usare il Portale di Azure per la creazione dell'app Web.</span><span class="sxs-lookup"><span data-stu-id="213d1-254">If this is the first App Service web app for your subscription, you will be instructed to use the Azure Portal to create the web app.</span></span> <span data-ttu-id="213d1-255">Per ulteriori informazioni, vedere [Creazione e distribuzione di un'app Web Node.js nel Azure App Service].</span><span class="sxs-lookup"><span data-stu-id="213d1-255">For more information, see [Build and deploy a Node.js web app in Azure App Service].</span></span>
   > 
   > 

### <a name="set-environment-variables"></a><span data-ttu-id="213d1-256">Impostare le variabili di ambiente</span><span class="sxs-lookup"><span data-stu-id="213d1-256">Set environment variables</span></span>
<span data-ttu-id="213d1-257">In questo passaggio verranno aggiunte le variabili di ambiente per la configurazione dell'app Web in Azure.</span><span class="sxs-lookup"><span data-stu-id="213d1-257">In this step, you will add environment variables to your web app configuration on Azure.</span></span>
<span data-ttu-id="213d1-258">Nella riga di comando immettere quanto segue:</span><span class="sxs-lookup"><span data-stu-id="213d1-258">From the command line, enter the following:</span></span>

    azure site appsetting add
        STORAGE_NAME=<storage account name>;STORAGE_KEY=<storage access key>;PARTITION_KEY=mytasks;TABLE_NAME=tasks


<span data-ttu-id="213d1-259">Sostituire **<storage account name>** con il nome dell'account di archiviazione creato in precedenza e sostituire **<storage access key>** con la chiave di accesso primaria per l'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="213d1-259">Replace **<storage account name>** with the name of the storage account you created earlier, and replace **<storage access key>** with the primary access key for your storage account.</span></span> <span data-ttu-id="213d1-260">Utilizzare gli stessi valori del file config.json creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="213d1-260">(Use the same values as the config.json file that you created earlier.)</span></span>

<span data-ttu-id="213d1-261">In alternativa, è possibile impostare le variabili di ambiente nel [Portale di Azure](https://portal.azure.com/):</span><span class="sxs-lookup"><span data-stu-id="213d1-261">Alternatively, you can set environment variables in the [Azure Portal](https://portal.azure.com/):</span></span>

1. <span data-ttu-id="213d1-262">Aprire il pannello dell'app Web facendo clic su **Sfoglia** > **App Web** > nome app Web.</span><span class="sxs-lookup"><span data-stu-id="213d1-262">Open the web app's blade by clicking **Browse** > **Web Apps** > your web app name.</span></span>
2. <span data-ttu-id="213d1-263">Nel pannello dell'app Web fare clic su **Tutte le impostazioni** > **Impostazioni dell'applicazione**.</span><span class="sxs-lookup"><span data-stu-id="213d1-263">In your web app's blade, click **All Settings** > **Application Settings**.</span></span>
   
     <!-- ![Top Menu](./media/storage-nodejs-use-table-storage-web-site/PollsCommonWebSiteTopMenu.png) -->
3. <span data-ttu-id="213d1-264">Scorrere verso il basso la sezione **Impostazioni app** e aggiungere le coppie chiave-valore.</span><span class="sxs-lookup"><span data-stu-id="213d1-264">Scroll down to the **App settings** section and add the key/value pairs.</span></span>
   
     ![Impostazioni app](./media/storage-nodejs-use-table-storage-web-site/storage-tasks-appsettings.png)
4. <span data-ttu-id="213d1-266">Fare clic su **SAVE**.</span><span class="sxs-lookup"><span data-stu-id="213d1-266">Click **SAVE**.</span></span>

### <a name="publish-the-application"></a><span data-ttu-id="213d1-267">Pubblicare l'applicazione</span><span class="sxs-lookup"><span data-stu-id="213d1-267">Publish the application</span></span>
<span data-ttu-id="213d1-268">Per pubblicare l'app, confermare i file di codice per GIT, quindi effettuare il push di azure/master.</span><span class="sxs-lookup"><span data-stu-id="213d1-268">To publish the app, commit the code files to Git and then push to azure/master.</span></span>

1. <span data-ttu-id="213d1-269">Impostare le credenziali di distribuzione</span><span class="sxs-lookup"><span data-stu-id="213d1-269">Set your deployment credentials.</span></span>
   
        azure site deployment user set <name> <password>
2. <span data-ttu-id="213d1-270">Aggiungere ed effettuare il commit dei file dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="213d1-270">Add and commit your application files.</span></span>
   
        git add .
        git commit -m "adding files"
3. <span data-ttu-id="213d1-271">Eseguire il push del commit per l'app Web del servizio app:</span><span class="sxs-lookup"><span data-stu-id="213d1-271">Push the commit to the App Service web app:</span></span>
   
        git push azure master
   
    <span data-ttu-id="213d1-272">Usare **master** come diramazione di destinazione.</span><span class="sxs-lookup"><span data-stu-id="213d1-272">Use **master** as the target branch.</span></span> <span data-ttu-id="213d1-273">Al termine della distribuzione, viene visualizzata un'istruzione simile al seguente esempio:</span><span class="sxs-lookup"><span data-stu-id="213d1-273">At the end of the deployment, you see a statement similar to the following example:</span></span>
   
        To https://username@tabletasklist.azurewebsites.net/TableTasklist.git
          * [new branch]      master -> master
4. <span data-ttu-id="213d1-274">Al termine dell'operazione di push, passare all'URL dell'app Web restituito in precedenza dal comando `azure create site` per visualizzare l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="213d1-274">Once the push operation has completed, browse to the web app URL returned previously by the `azure create site` command to view your application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="213d1-275">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="213d1-275">Next steps</span></span>
<span data-ttu-id="213d1-276">Nei passaggi di questo articolo viene descritto come archiviare informazioni tramite il servizio tabelle. Tuttavia per tale attività è anche possibile usare [MongoDB](https://mlab.com/azure/).</span><span class="sxs-lookup"><span data-stu-id="213d1-276">While the steps in this article describe using the Table Service to store information, you can also use [MongoDB](https://mlab.com/azure/).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="213d1-277">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="213d1-277">Additional resources</span></span>
<span data-ttu-id="213d1-278">[Interfaccia della riga di comando di Azure]</span><span class="sxs-lookup"><span data-stu-id="213d1-278">[Azure CLI]</span></span>

## <a name="whats-changed"></a><span data-ttu-id="213d1-279">Modifiche apportate</span><span class="sxs-lookup"><span data-stu-id="213d1-279">What's changed</span></span>
* <span data-ttu-id="213d1-280">Per una guida relativa al passaggio da Siti Web al servizio app, vedere [Servizio app di Azure e impatto sui servizi di Azure esistenti](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="213d1-280">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!-- URLs -->

<span data-ttu-id="213d1-281">[Creazione e distribuzione di un'app Web Node.js nel Azure App Service]: app-service-web-get-started-nodejs.md</span><span class="sxs-lookup"><span data-stu-id="213d1-281">[Build and deploy a Node.js web app in Azure App Service]: app-service-web-get-started-nodejs.md</span></span>
[Azure Developer Center]: /develop/nodejs/

<span data-ttu-id="213d1-282">[node]: http://nodejs.org</span><span class="sxs-lookup"><span data-stu-id="213d1-282">[node]: http://nodejs.org</span></span>
<span data-ttu-id="213d1-283">[Git]: http://git-scm.com</span><span class="sxs-lookup"><span data-stu-id="213d1-283">[Git]: http://git-scm.com</span></span>
<span data-ttu-id="213d1-284">[Express]: http://expressjs.com</span><span class="sxs-lookup"><span data-stu-id="213d1-284">[Express]: http://expressjs.com</span></span>
[for free]: http://windowsazure.com
<span data-ttu-id="213d1-285">[GIT remoto]: http://git-scm.com/docs/git-remote</span><span class="sxs-lookup"><span data-stu-id="213d1-285">[Git remote]: http://git-scm.com/docs/git-remote</span></span>

<span data-ttu-id="213d1-286">[Interfaccia della riga di comando di Azure]:../cli-install-nodejs.md</span><span class="sxs-lookup"><span data-stu-id="213d1-286">[Azure CLI]:../cli-install-nodejs.md</span></span>

<span data-ttu-id="213d1-287">[azure]: https://github.com/Azure/azure-sdk-for-node</span><span class="sxs-lookup"><span data-stu-id="213d1-287">[azure]: https://github.com/Azure/azure-sdk-for-node</span></span>
<span data-ttu-id="213d1-288">[node-uuid]: https://www.npmjs.com/package/node-uuid</span><span class="sxs-lookup"><span data-stu-id="213d1-288">[node-uuid]: https://www.npmjs.com/package/node-uuid</span></span>
<span data-ttu-id="213d1-289">[nconf]: https://www.npmjs.com/package/nconf</span><span class="sxs-lookup"><span data-stu-id="213d1-289">[nconf]: https://www.npmjs.com/package/nconf</span></span>
<span data-ttu-id="213d1-290">[async]: https://www.npmjs.com/package/async</span><span class="sxs-lookup"><span data-stu-id="213d1-290">[async]: https://www.npmjs.com/package/async</span></span>

[Azure Portal]: https://portal.azure.com

[Create and deploy a Node.js application to an Azure Web Site]: app-service-web-get-started-nodejs.md

<!-- Image References -->

[node-table-finished]: ./media/storage-nodejs-use-table-storage-web-site/table_todo_empty.png
[node-table-list-items]: ./media/storage-nodejs-use-table-storage-web-site/table_todo_list.png
[download-publishing-settings]: ./media/storage-nodejs-use-table-storage-web-site/azure-account-download-cli.png
[portal-storage-access-keys]: ./media/storage-nodejs-use-table-storage-web-site/manage-access-keys.png
[app-settings]: ./media/storage-nodejs-use-table-storage-web-site/storage-tasks-appsettings.png
