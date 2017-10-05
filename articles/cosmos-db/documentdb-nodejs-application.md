---
title: Compilare un'app Web Node.js per Azure Cosmos DB | Microsoft Docs
description: Questa esercitazione di Node.js illustra come usare il servizio Microsoft Azure Cosmos DB per archiviare e accedere ai dati da un'applicazione Web Node.js Express ospitata in siti Web di Azure.
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
ms.openlocfilehash: 1a98509a98bcd2a5de593eb006f905766fe72966
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <span data-ttu-id="a249d-104"><a name="_Toc395783175"></a>Creare un'applicazione Web Node.js con Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="a249d-104"><a name="_Toc395783175"></a>Build a Node.js web application using Azure Cosmos DB</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a249d-105">.NET</span><span class="sxs-lookup"><span data-stu-id="a249d-105">.NET</span></span>](documentdb-dotnet-application.md)
> * [<span data-ttu-id="a249d-106">Node.JS</span><span class="sxs-lookup"><span data-stu-id="a249d-106">Node.js</span></span>](documentdb-nodejs-application.md)
> * [<span data-ttu-id="a249d-107">Java</span><span class="sxs-lookup"><span data-stu-id="a249d-107">Java</span></span>](documentdb-java-application.md)
> * [<span data-ttu-id="a249d-108">Python</span><span class="sxs-lookup"><span data-stu-id="a249d-108">Python</span></span>](documentdb-python-application.md)
> 
> 

<span data-ttu-id="a249d-109">Questa esercitazione relativa a Node.js illustra come usare Azure Cosmos DB e l'API di DocumentDB per archiviare e accedere ai dati da un'applicazione Node.js Express ospitata in Siti Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="a249d-109">This Node.js tutorial shows you how to use Azure Cosmos DB and the DocumentDB API to store and access data from a Node.js Express application hosted on Azure Websites.</span></span> <span data-ttu-id="a249d-110">Verrà creata una semplice applicazione di gestione delle attività basata su Web, un'app ToDo, che consente di creare, recuperare e completare le attività.</span><span class="sxs-lookup"><span data-stu-id="a249d-110">You build a simple web-based task-management application, a ToDo app, that allows creating, retrieving, and completing tasks.</span></span> <span data-ttu-id="a249d-111">Le attività vengono memorizzate come documenti JSON in Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="a249d-111">The tasks are stored as JSON documents in Azure Cosmos DB.</span></span> <span data-ttu-id="a249d-112">Questa esercitazione illustra la creazione e la distribuzione dell'app e fornisce informazioni dettagliate sulle operazioni in ogni frammento di codice.</span><span class="sxs-lookup"><span data-stu-id="a249d-112">This tutorial walks you through the creation and deployment of the app and explains what's happening in each snippet.</span></span>

![Schermata dell'applicazione My Todo List creata in questa esercitazione Node.js](./media/documentdb-nodejs-application/cosmos-db-node-js-mytodo.png)

<span data-ttu-id="a249d-114">Non si ha tempo di completare l'esercitazione e si preferisce ottenere semplicemente la soluzione completa.</span><span class="sxs-lookup"><span data-stu-id="a249d-114">Don't have time to complete the tutorial and just want to get the complete solution?</span></span> <span data-ttu-id="a249d-115">Non è un problema, è possibile ottenere la soluzione di esempio completa da [GitHub][GitHub].</span><span class="sxs-lookup"><span data-stu-id="a249d-115">Not a problem, you can get the complete sample solution from [GitHub][GitHub].</span></span> <span data-ttu-id="a249d-116">Per istruzioni su come eseguire l'app, vedere il file [Readme](https://github.com/Azure-Samples/documentdb-node-todo-app/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="a249d-116">Just read the [Readme](https://github.com/Azure-Samples/documentdb-node-todo-app/blob/master/README.md) file for instructions on how to run the app.</span></span>

## <span data-ttu-id="a249d-117"><a name="_Toc395783176"></a>Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="a249d-117"><a name="_Toc395783176"></a>Prerequisites</span></span>
> [!TIP]
> <span data-ttu-id="a249d-118">Questa esercitazione Node.js presuppone già una certa esperienza nell'uso di Node.js e di Siti Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="a249d-118">This Node.js tutorial assumes that you have some prior experience using Node.js and Azure Websites.</span></span>
> 
> 

<span data-ttu-id="a249d-119">Prima di seguire le istruzioni di questo articolo, verificare che siano disponibili gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="a249d-119">Before following the instructions in this article, you should ensure that you have the following:</span></span>

* <span data-ttu-id="a249d-120">Un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="a249d-120">An active Azure account.</span></span> <span data-ttu-id="a249d-121">Se non si dispone di un account, è possibile creare un account di valutazione gratuita in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="a249d-121">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="a249d-122">Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a249d-122">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

   <span data-ttu-id="a249d-123">OPPURE</span><span class="sxs-lookup"><span data-stu-id="a249d-123">OR</span></span>

   <span data-ttu-id="a249d-124">Un'installazione locale dell'[emulatore Azure Cosmos DB](local-emulator.md) (solo Windows).</span><span class="sxs-lookup"><span data-stu-id="a249d-124">A local installation of the [Azure Cosmos DB Emulator](local-emulator.md) (Windows only).</span></span>
* <span data-ttu-id="a249d-125">[Node.js][Node.js] 0.10.29 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="a249d-125">[Node.js][Node.js] version v0.10.29 or higher.</span></span>
* <span data-ttu-id="a249d-126">[Generatore di Express](http://www.expressjs.com/starter/generator.html), installabile tramite `npm install express-generator -g`</span><span class="sxs-lookup"><span data-stu-id="a249d-126">[Express generator](http://www.expressjs.com/starter/generator.html) (you can install this via `npm install express-generator -g`)</span></span>
* <span data-ttu-id="a249d-127">[Git][Git].</span><span class="sxs-lookup"><span data-stu-id="a249d-127">[Git][Git].</span></span>

## <span data-ttu-id="a249d-128"><a name="_Toc395637761"></a>Passaggio 1: Creare un account del database di Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="a249d-128"><a name="_Toc395637761"></a>Step 1: Create an Azure Cosmos DB database account</span></span>
<span data-ttu-id="a249d-129">Creare prima di tutto un account Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="a249d-129">Let's start by creating an Azure Cosmos DB account.</span></span> <span data-ttu-id="a249d-130">Se si ha già un account o si usa l'emulatore Azure Cosmos DB per questa esercitazione, è possibile andare al [Passaggio 2: Creare una nuova applicazione Node.js](#_Toc395783178).</span><span class="sxs-lookup"><span data-stu-id="a249d-130">If you already have an account or if you are using the Azure Cosmos DB Emulator for this tutorial, you can skip to [Step 2: Create a new Node.js application](#_Toc395783178).</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

[!INCLUDE [cosmos-db-keys](../../includes/cosmos-db-keys.md)]

## <span data-ttu-id="a249d-131"><a name="_Toc395783178"></a>Passaggio 2: Creare una nuova applicazione Node.js</span><span class="sxs-lookup"><span data-stu-id="a249d-131"><a name="_Toc395783178"></a>Step 2: Create a new Node.js application</span></span>
<span data-ttu-id="a249d-132">A questo punto si creerà un progetto base Node.js Hello World usando il framework [Express](http://expressjs.com/) .</span><span class="sxs-lookup"><span data-stu-id="a249d-132">Now let's learn to create a basic Hello World Node.js project using the [Express](http://expressjs.com/) framework.</span></span>

1. <span data-ttu-id="a249d-133">Aprire il terminale preferito, ad esempio il prompt dei comandi di Node.js.</span><span class="sxs-lookup"><span data-stu-id="a249d-133">Open your favorite terminal, such as the Node.js command prompt.</span></span>
2. <span data-ttu-id="a249d-134">Passare alla directory in cui si vuole archiviare la nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="a249d-134">Navigate to the directory in which you'd like to store the new application.</span></span>
3. <span data-ttu-id="a249d-135">Usare il generatore di Express per generare una nuova applicazione denominata **todo**.</span><span class="sxs-lookup"><span data-stu-id="a249d-135">Use the express generator to generate a new application called **todo**.</span></span>
   
        express todo
4. <span data-ttu-id="a249d-136">Aprire la nuova directory **todo** e installare le dipendenze.</span><span class="sxs-lookup"><span data-stu-id="a249d-136">Open your new **todo** directory and install dependencies.</span></span>
   
        cd todo
        npm install
5. <span data-ttu-id="a249d-137">Eseguire la nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="a249d-137">Run your new application.</span></span>
   
        npm start
6. <span data-ttu-id="a249d-138">È possibile visualizzare la nuova applicazione passando con il browser all'indirizzo [http://localhost:3000](http://localhost:3000).</span><span class="sxs-lookup"><span data-stu-id="a249d-138">You can view your new application by navigating your browser to [http://localhost:3000](http://localhost:3000).</span></span>
   
    ![Informazioni su Node.js - schermata dell'applicazione Hello World in una finestra del browser](./media/documentdb-nodejs-application/cosmos-db-node-js-express.png)

    <span data-ttu-id="a249d-140">Per arrestare l'applicazione, premere quindi CTRL+C nella finestra del terminale e fare clic su **y** per interrompere il processo batch.</span><span class="sxs-lookup"><span data-stu-id="a249d-140">Then, to stop the application, press CTRL+C in the terminal window and then click **y** to terminate the batch job.</span></span>

## <span data-ttu-id="a249d-141"><a name="_Toc395783179"></a>Passaggio 3: Installare moduli aggiuntivi</span><span class="sxs-lookup"><span data-stu-id="a249d-141"><a name="_Toc395783179"></a>Step 3: Install additional modules</span></span>
<span data-ttu-id="a249d-142">Il file **package.json** è uno di quelli creati nella radice del progetto.</span><span class="sxs-lookup"><span data-stu-id="a249d-142">The **package.json** file is one of the files created in the root of the project.</span></span> <span data-ttu-id="a249d-143">Questo file contiene un elenco di moduli aggiuntivi necessari per l'applicazione Node.js.</span><span class="sxs-lookup"><span data-stu-id="a249d-143">This file contains a list of additional modules that are required for your Node.js application.</span></span> <span data-ttu-id="a249d-144">In seguito, quando si distribuirà questa applicazione in un sito Web di Azure, il file verrà usato per determinare quali moduli devono essere installati in Azure per supportare l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="a249d-144">Later, when you deploy this application to Azure Websites, this file is used to determine which modules need to be installed on Azure to support your application.</span></span> <span data-ttu-id="a249d-145">Per l'esercitazione, è necessario installare altri due pacchetti.</span><span class="sxs-lookup"><span data-stu-id="a249d-145">We still need to install two more packages for this tutorial.</span></span>

1. <span data-ttu-id="a249d-146">Tornare al terminale e installare il modulo **async** tramite npm.</span><span class="sxs-lookup"><span data-stu-id="a249d-146">Back in the terminal, install the **async** module via npm.</span></span>
   
        npm install async --save
2. <span data-ttu-id="a249d-147">Installare il modulo **documentdb** tramite npm.</span><span class="sxs-lookup"><span data-stu-id="a249d-147">Install the **documentdb** module via npm.</span></span> <span data-ttu-id="a249d-148">Questo è il modulo in cui risiedono tutte le funzionalità avanzate di Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="a249d-148">This is the module where all the Azure Cosmos DB magic happens.</span></span>
   
        npm install documentdb --save
3. <span data-ttu-id="a249d-149">Con un rapido controllo del file **package.json** dell'applicazione si dovrebbero notare i moduli aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="a249d-149">A quick check of the **package.json** file of the application should show the additional modules.</span></span> <span data-ttu-id="a249d-150">Questo file indica ad Azure quali pacchetti scaricare e installare durante l'esecuzione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="a249d-150">This file will tell Azure which packages to download and install when running your application.</span></span> <span data-ttu-id="a249d-151">Dovrebbe essere simile all'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="a249d-151">It should resemble the example below.</span></span>
   
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
   
    <span data-ttu-id="a249d-152">Ciò indicherà a Node (e più avanti ad Azure) che l'applicazione dipende da questi moduli aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="a249d-152">This tells Node (and Azure later) that your application depends on these additional modules.</span></span>

## <span data-ttu-id="a249d-153"><a name="_Toc395783180"></a>Passaggio 4: Uso del servizio Azure Cosmos DB in un'applicazione Node</span><span class="sxs-lookup"><span data-stu-id="a249d-153"><a name="_Toc395783180"></a>Step 4: Using the Azure Cosmos DB service in a node application</span></span>
<span data-ttu-id="a249d-154">Al termine delle operazioni iniziali di installazione e configurazione, si può passare allo scopo effettivo di questa esercitazione, che consiste nello scrivere qualche riga di codice usando Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="a249d-154">That takes care of all the initial setup and configuration, now let’s get down to why we’re here, and that’s to write some code using Azure Cosmos DB.</span></span>

### <a name="create-the-model"></a><span data-ttu-id="a249d-155">Creare il modello</span><span class="sxs-lookup"><span data-stu-id="a249d-155">Create the model</span></span>
1. <span data-ttu-id="a249d-156">Nella directory del progetto creare una nuova directory denominata **models** nella stessa directory del file package.json.</span><span class="sxs-lookup"><span data-stu-id="a249d-156">In the project directory, create a new directory named **models** in the same directory as the package.json file.</span></span>
2. <span data-ttu-id="a249d-157">Nella directory **models** (modelli) creare un nuovo file denominato **taskDao.js**.</span><span class="sxs-lookup"><span data-stu-id="a249d-157">In the **models** directory, create a new file named **taskDao.js**.</span></span> <span data-ttu-id="a249d-158">Questo file conterrà il modello per le attività create dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="a249d-158">This file will contain the model for the tasks created by our application.</span></span>
3. <span data-ttu-id="a249d-159">Nella stessa directory **models** (modelli) creare un altro nuovo file denominato **docdbUtils.js**.</span><span class="sxs-lookup"><span data-stu-id="a249d-159">In the same **models** directory, create another new file named **docdbUtils.js**.</span></span> <span data-ttu-id="a249d-160">Questo file conterrà porzioni di codice utile e riutilizzabile, che verrà usato nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="a249d-160">This file will contain some useful, reusable, code that we will use throughout our application.</span></span> 
4. <span data-ttu-id="a249d-161">Copiare il codice seguente in **docdbUtils.js**</span><span class="sxs-lookup"><span data-stu-id="a249d-161">Copy the following code in to **docdbUtils.js**</span></span>
   
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
   
5. <span data-ttu-id="a249d-162">Salvare e chiudere il file **docdbUtils.js** .</span><span class="sxs-lookup"><span data-stu-id="a249d-162">Save and close the **docdbUtils.js** file.</span></span>
6. <span data-ttu-id="a249d-163">All'inizio del file **taskDao.js** aggiungere il codice seguente per fare riferimento a **DocumentDBClient** e **docdbUtils.js** creati in precedenza:</span><span class="sxs-lookup"><span data-stu-id="a249d-163">At the beginning of the **taskDao.js** file, add the following code to reference the **DocumentDBClient** and the **docdbUtils.js** we created above:</span></span>
   
        var DocumentDBClient = require('documentdb').DocumentClient;
        var docdbUtils = require('./docdbUtils');
7. <span data-ttu-id="a249d-164">Quindi, aggiungere il codice per definire ed esportare l'oggetto Task.</span><span class="sxs-lookup"><span data-stu-id="a249d-164">Next, you will add code to define and export the Task object.</span></span> <span data-ttu-id="a249d-165">Si occupa dell'inizializzazione dell'oggetto Task e della configurazione del database e della raccolta documenti che verranno usati.</span><span class="sxs-lookup"><span data-stu-id="a249d-165">This is responsible for initializing our Task object and setting up the Database and Document Collection we will use.</span></span>
   
        function TaskDao(documentDBClient, databaseId, collectionId) {
          this.client = documentDBClient;
          this.databaseId = databaseId;
          this.collectionId = collectionId;
   
          this.database = null;
          this.collection = null;
        }
   
        module.exports = TaskDao;
8. <span data-ttu-id="a249d-166">Aggiungere quindi il codice seguente per definire metodi aggiuntivi nell'oggetto Task che consentano l'interazione con i dati archiviati in Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="a249d-166">Next, add the following code to define additional methods on the Task object, which allow interactions with data stored in Azure Cosmos DB.</span></span>
   
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
9. <span data-ttu-id="a249d-167">Salvare e chiudere il file **taskDao.js** .</span><span class="sxs-lookup"><span data-stu-id="a249d-167">Save and close the **taskDao.js** file.</span></span> 

### <a name="create-the-controller"></a><span data-ttu-id="a249d-168">Creare il controller</span><span class="sxs-lookup"><span data-stu-id="a249d-168">Create the controller</span></span>
1. <span data-ttu-id="a249d-169">Nella directory **routes** (route) del progetto creare un nuovo file denominato **tasklist.js**.</span><span class="sxs-lookup"><span data-stu-id="a249d-169">In the **routes** directory of your project, create a new file named **tasklist.js**.</span></span> 
2. <span data-ttu-id="a249d-170">Aggiungere il seguente codice al file **tasklist.js**.</span><span class="sxs-lookup"><span data-stu-id="a249d-170">Add the following code to **tasklist.js**.</span></span> <span data-ttu-id="a249d-171">In questo modo vengono caricati i moduli DocumentDBClient e asincroni usati da **tasklist.js**.</span><span class="sxs-lookup"><span data-stu-id="a249d-171">This loads the DocumentDBClient and async modules, which are used by **tasklist.js**.</span></span> <span data-ttu-id="a249d-172">Viene anche definita la funzione **TaskList** a cui viene passata un'istanza dell'oggetto **Task** definito in precedenza:</span><span class="sxs-lookup"><span data-stu-id="a249d-172">This also defined the **TaskList** function, which is passed an instance of the **Task** object we defined earlier:</span></span>
   
        var DocumentDBClient = require('documentdb').DocumentClient;
        var async = require('async');
   
        function TaskList(taskDao) {
          this.taskDao = taskDao;
        }
   
        module.exports = TaskList;
3. <span data-ttu-id="a249d-173">Continuare ad aggiungere codice al file **tasklist.js** aggiungendo i metodi **showTasks, addTask** e **completeTasks**:</span><span class="sxs-lookup"><span data-stu-id="a249d-173">Continue adding to the **tasklist.js** file by adding the methods used to **showTasks, addTask**, and **completeTasks**:</span></span>
   
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
4. <span data-ttu-id="a249d-174">Salvare e chiudere il file **tasklist.js** .</span><span class="sxs-lookup"><span data-stu-id="a249d-174">Save and close the **tasklist.js** file.</span></span>

### <a name="add-configjs"></a><span data-ttu-id="a249d-175">Aggiungere config.json</span><span class="sxs-lookup"><span data-stu-id="a249d-175">Add config.js</span></span>
1. <span data-ttu-id="a249d-176">Nella directory del progetto creare un nuovo file denominato **config.js**.</span><span class="sxs-lookup"><span data-stu-id="a249d-176">In your project directory create a new file named **config.js**.</span></span>
2. <span data-ttu-id="a249d-177">Aggiungere quanto segue a **config.json**.</span><span class="sxs-lookup"><span data-stu-id="a249d-177">Add the following to **config.js**.</span></span> <span data-ttu-id="a249d-178">Definisce le impostazioni e i valori di configurazione necessari per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="a249d-178">This defines configuration settings and values needed for our application.</span></span>
   
        var config = {}
   
        config.host = process.env.HOST || "[the URI value from the Azure Cosmos DB Keys blade on http://portal.azure.com]";
        config.authKey = process.env.AUTH_KEY || "[the PRIMARY KEY value from the Azure Cosmos DB Keys blade on http://portal.azure.com]";
        config.databaseId = "ToDoList";
        config.collectionId = "Items";
   
        module.exports = config;
3. <span data-ttu-id="a249d-179">Nel file **config.js** aggiornare i valori HOST e AUTH_KEY usando i valori presenti nel pannello Chiavi dell'account Azure Cosmos DB nel [portale di Microsoft Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a249d-179">In the **config.js** file, update the values of HOST and AUTH_KEY using the values found in the Keys blade of your Azure Cosmos DB account on the [Microsoft Azure portal](https://portal.azure.com).</span></span>
4. <span data-ttu-id="a249d-180">Salvare e chiudere il file **config.js** .</span><span class="sxs-lookup"><span data-stu-id="a249d-180">Save and close the **config.js** file.</span></span>

### <a name="modify-appjs"></a><span data-ttu-id="a249d-181">Modificare il file app.js</span><span class="sxs-lookup"><span data-stu-id="a249d-181">Modify app.js</span></span>
1. <span data-ttu-id="a249d-182">Nella directory del progetto aprire il file **app.js** .</span><span class="sxs-lookup"><span data-stu-id="a249d-182">In the project directory, open the **app.js** file.</span></span> <span data-ttu-id="a249d-183">Questo file è stato creato in precedenza quando è stata creata l'applicazione Web Express.</span><span class="sxs-lookup"><span data-stu-id="a249d-183">This file was created earlier when the Express web application was created.</span></span>
2. <span data-ttu-id="a249d-184">Aggiungere il codice seguente all'inizio del file **app.js**</span><span class="sxs-lookup"><span data-stu-id="a249d-184">Add the following code to the top of **app.js**</span></span>
   
        var DocumentDBClient = require('documentdb').DocumentClient;
        var config = require('./config');
        var TaskList = require('./routes/tasklist');
        var TaskDao = require('./models/taskDao');
3. <span data-ttu-id="a249d-185">Questo codice definisce il file di configurazione da usare e procede con la lettura dei valori da questo file in alcune variabili che si useranno a breve.</span><span class="sxs-lookup"><span data-stu-id="a249d-185">This code defines the config file to be used, and proceeds to read values out of this file into some variables we will use soon.</span></span>
4. <span data-ttu-id="a249d-186">Sostituire le due righe seguenti nel file **app.js** :</span><span class="sxs-lookup"><span data-stu-id="a249d-186">Replace the following two lines in **app.js** file:</span></span>
   
        app.use('/', index);
        app.use('/users', users); 
   
      <span data-ttu-id="a249d-187">con il frammento seguente:</span><span class="sxs-lookup"><span data-stu-id="a249d-187">with the following snippet:</span></span>
   
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
5. <span data-ttu-id="a249d-188">Queste righe definiscono una nuova istanza dell'oggetto **TaskDao** con una nuova connessione a Azure Cosmos DB, usando i valori letti dal file **config.js**, inizializzano l'oggetto task e quindi associano le azioni modulo ai metodi nel controller **TaskList**.</span><span class="sxs-lookup"><span data-stu-id="a249d-188">These lines define a new instance of our **TaskDao** object, with a new connection to Azure Cosmos DB (using the values read from the **config.js**), initialize the task object and then bind form actions to methods on our **TaskList** controller.</span></span> 
6. <span data-ttu-id="a249d-189">Infine, salvare e chiudere il file **app.js**. La procedura è quasi terminata.</span><span class="sxs-lookup"><span data-stu-id="a249d-189">Finally, save and close the **app.js** file, we're just about done.</span></span>

## <span data-ttu-id="a249d-190"><a name="_Toc395783181"></a>Passaggio 5: Creare un'interfaccia utente</span><span class="sxs-lookup"><span data-stu-id="a249d-190"><a name="_Toc395783181"></a>Step 5: Build a user interface</span></span>
<span data-ttu-id="a249d-191">È ora possibile passare alla realizzazione di un'interfaccia utente che consenta a un utente di interagire con l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="a249d-191">Now let’s turn our attention to building the user interface so a user can actually interact with our application.</span></span> <span data-ttu-id="a249d-192">L'applicazione Express creata usa **Jade** come motore di visualizzazione.</span><span class="sxs-lookup"><span data-stu-id="a249d-192">The Express application we created uses **Jade** as the view engine.</span></span> <span data-ttu-id="a249d-193">Per altre informazioni su Jade, vedere [http://jade-lang.com/](http://jade-lang.com/).</span><span class="sxs-lookup"><span data-stu-id="a249d-193">For more information on Jade please refer to [http://jade-lang.com/](http://jade-lang.com/).</span></span>

1. <span data-ttu-id="a249d-194">Il file **layout.jade** della directory **views** viene usato come modello globale per altri file **.jade**.</span><span class="sxs-lookup"><span data-stu-id="a249d-194">The **layout.jade** file in the **views** directory is used as a global template for other **.jade** files.</span></span> <span data-ttu-id="a249d-195">In questo passaggio verrà modificato in modo da usare [Twitter Bootstrap](https://github.com/twbs/bootstrap), un toolkit che semplifica la progettazione di un sito Web di aspetto gradevole.</span><span class="sxs-lookup"><span data-stu-id="a249d-195">In this step you will modify it to use [Twitter Bootstrap](https://github.com/twbs/bootstrap), which is a toolkit that makes it easy to design a nice looking website.</span></span> 
2. <span data-ttu-id="a249d-196">Aprire il file **layout.jade** nella cartella **views** e sostituire il contenuto con quanto segue:</span><span class="sxs-lookup"><span data-stu-id="a249d-196">Open the **layout.jade** file found in the **views** folder and replace the contents with the following:</span></span>

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

    <span data-ttu-id="a249d-197">Ciò in effetti comunica al motore **Jade** di eseguire il rendering di una parte del codice HTML per l'applicazione e crea un **blocco** denominato **content** tramite cui è possibile fornire il layout per le pagine di contenuto.</span><span class="sxs-lookup"><span data-stu-id="a249d-197">This effectively tells the **Jade** engine to render some HTML for our application and creates a **block** called **content** where we can supply the layout for our content pages.</span></span>

    <span data-ttu-id="a249d-198">Salvare e chiudere il file **layout.jade** .</span><span class="sxs-lookup"><span data-stu-id="a249d-198">Save and close this **layout.jade** file.</span></span>

3. <span data-ttu-id="a249d-199">Aprire il file **index.jade** , la visualizzazione che sarà usata dall'applicazione, quindi sostituire il contenuto del file con quanto segue:</span><span class="sxs-lookup"><span data-stu-id="a249d-199">Now open the **index.jade** file, the view that will be used by our application, and replace the content of the file with the following:</span></span>
   
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
   

<span data-ttu-id="a249d-200">Questo estende il layout e fornisce contenuto per il segnaposto **content** già visto in precedenza nel file **layout.jade**.</span><span class="sxs-lookup"><span data-stu-id="a249d-200">This extends layout, and provides content for the **content** placeholder we saw in the **layout.jade** file earlier.</span></span>
   
<span data-ttu-id="a249d-201">In questo layout sono stati creati due moduli HTML.</span><span class="sxs-lookup"><span data-stu-id="a249d-201">In this layout we created two HTML forms.</span></span>

<span data-ttu-id="a249d-202">Il primo modulo contiene una tabella per i dati e un pulsante che consente di aggiornare gli elementi mediante la pubblicazione nel metodo **/completetask** del controller.</span><span class="sxs-lookup"><span data-stu-id="a249d-202">The first form contains a table for our data and a button that allows us to update items by posting to **/completetask** method of our controller.</span></span>
    
<span data-ttu-id="a249d-203">Il secondo modulo contiene due campi di input e un pulsante che consente di creare un nuovo elemento tramite la pubblicazione nel metodo **/addtask** del controller.</span><span class="sxs-lookup"><span data-stu-id="a249d-203">The second form contains two input fields and a button that allows us to create a new item by posting to **/addtask** method of our controller.</span></span>

<span data-ttu-id="a249d-204">Ciò è tutto quanto è necessario per il funzionamento dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="a249d-204">This should be all that we need for our application to work.</span></span>

## <span data-ttu-id="a249d-205"><a name="_Toc395783181"></a>Passaggio 6: Esecuzione dell'applicazione in locale</span><span class="sxs-lookup"><span data-stu-id="a249d-205"><a name="_Toc395783181"></a>Step 6: Run your application locally</span></span>
1. <span data-ttu-id="a249d-206">Per testare l'applicazione nel computer locale, eseguire `npm start` nel terminale per avviare l'applicazione, quindi aggiornare la pagina [http://localhost:3000](http://localhost:3000) del browser.</span><span class="sxs-lookup"><span data-stu-id="a249d-206">To test the application on your local machine, run `npm start` in the terminal to start your application, then refresh your [http://localhost:3000](http://localhost:3000) browser page.</span></span> <span data-ttu-id="a249d-207">L'aspetto della pagina dovrebbe essere simile all'immagine seguente:</span><span class="sxs-lookup"><span data-stu-id="a249d-207">The page should now look like the image below:</span></span>
   
    ![Schermata dell'applicazione MyTodo List in una finestra del browser](./media/documentdb-nodejs-application/cosmos-db-node-js-localhost.png)

    > [!TIP]
    > <span data-ttu-id="a249d-209">Se viene visualizzato un errore relativo al rientro nel file layout.jade o nel file index.jade, assicurarsi che le prime due righe in entrambi i file siano giustificate a sinistra, senza spazi.</span><span class="sxs-lookup"><span data-stu-id="a249d-209">If you receive an error about the indent in the layout.jade file or the index.jade file, ensure that the first two lines in both files is left justified, with no spaces.</span></span> <span data-ttu-id="a249d-210">Se sono presenti spazi davanti alle prime due righe, rimuoverli, salvare entrambi i file e quindi aggiornare la finestra del browser.</span><span class="sxs-lookup"><span data-stu-id="a249d-210">If there are spaces before the first two lines, remove them, save both files, then refresh your browser window.</span></span> 

2. <span data-ttu-id="a249d-211">Usare i campi Elemento, Nome elemento e Categoria per immettere una nuova attività e quindi fare clic su **Aggiungi elementi**.</span><span class="sxs-lookup"><span data-stu-id="a249d-211">Use the Item, Item Name and Category fields to enter a new task and then click **Add Item**.</span></span> <span data-ttu-id="a249d-212">Viene creato un documento in Azure Cosmos DB con queste proprietà.</span><span class="sxs-lookup"><span data-stu-id="a249d-212">This creates a document in Azure Cosmos DB with those properties.</span></span> 
3. <span data-ttu-id="a249d-213">La pagina verrà aggiornata e verrà visualizzato il nuovo elemento creato nell'elenco ToDo.</span><span class="sxs-lookup"><span data-stu-id="a249d-213">The page should update to display the newly created item in the ToDo list.</span></span>
   
    ![Schermata dell'applicazione con un nuovo elemento nell'elenco ToDo](./media/documentdb-nodejs-application/cosmos-db-node-js-added-task.png)
4. <span data-ttu-id="a249d-215">Per completare un'attività, è sufficiente selezionare la casella di controllo nella colonna Complete e quindi fare clic su **Update tasks**.</span><span class="sxs-lookup"><span data-stu-id="a249d-215">To complete a task, simply check the checkbox in the Complete column, and then click **Update tasks**.</span></span> <span data-ttu-id="a249d-216">Viene aggiornato il documento già creato.</span><span class="sxs-lookup"><span data-stu-id="a249d-216">This updates the document you already created.</span></span>

5. <span data-ttu-id="a249d-217">Per arrestare l'applicazione, premere CTRL+C nella finestra del terminale e quindi fare clic su **Y** per interrompere il processo batch.</span><span class="sxs-lookup"><span data-stu-id="a249d-217">To stop the application, press CTRL+C in the terminal window and then click **Y** to terminate the batch job.</span></span>

## <span data-ttu-id="a249d-218"><a name="_Toc395783182"></a>Passaggio 7: Distribuire il progetto di sviluppo dell'applicazione in Siti Web di Azure</span><span class="sxs-lookup"><span data-stu-id="a249d-218"><a name="_Toc395783182"></a>Step 7: Deploy your application development project to Azure Websites</span></span>
1. <span data-ttu-id="a249d-219">Se non è ancora stato fatto, abilitare un repository Git per il sito Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="a249d-219">If you haven't already, enable a git repository for your Azure Website.</span></span> <span data-ttu-id="a249d-220">Per istruzioni su come eseguire questa operazione, vedere l'argomento [Distribuzione dell'archivio Git locale nel servizio app di Azure](../app-service-web/app-service-deploy-local-git.md) .</span><span class="sxs-lookup"><span data-stu-id="a249d-220">You can find instructions on how to do this in the [Local Git Deployment to Azure App Service](../app-service-web/app-service-deploy-local-git.md) topic.</span></span>
2. <span data-ttu-id="a249d-221">Aggiungere il sito Web di Azure come Git remoto.</span><span class="sxs-lookup"><span data-stu-id="a249d-221">Add your Azure Website as a git remote.</span></span>
   
        git remote add azure https://username@your-azure-website.scm.azurewebsites.net:443/your-azure-website.git
3. <span data-ttu-id="a249d-222">Distribuire mediante push al sito remoto.</span><span class="sxs-lookup"><span data-stu-id="a249d-222">Deploy by pushing to the remote.</span></span>
   
        git push azure master
4. <span data-ttu-id="a249d-223">Dopo alcuni secondi, Git completerà la pubblicazione dell'applicazione Web e avvierà un browser in cui sarà possibile visualizzare quanto realizzato in esecuzione in Azure.</span><span class="sxs-lookup"><span data-stu-id="a249d-223">In a few seconds, git will finish publishing your web application and launch a browser where you can see your handiwork running in Azure!</span></span>

    <span data-ttu-id="a249d-224">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="a249d-224">Congratulations!</span></span> <span data-ttu-id="a249d-225">Si è creata la prima applicazione Web Express Node.js usando Azure Cosmos DB e la si è pubblicata in Siti Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="a249d-225">You have just built your first Node.js Express Web Application using Azure Cosmos DB and published it to Azure Websites.</span></span>

    <span data-ttu-id="a249d-226">Per scaricare o fare riferimento all'applicazione di riferimento completa per questa esercitazione, vedere [GitHub][GitHub].</span><span class="sxs-lookup"><span data-stu-id="a249d-226">If you want to download or refer to the complete reference application for this tutorial, it can be downloaded from [GitHub][GitHub].</span></span>

## <span data-ttu-id="a249d-227"><a name="_Toc395637775"></a>Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a249d-227"><a name="_Toc395637775"></a>Next steps</span></span>

* <span data-ttu-id="a249d-228">Per la scalabilità e i test delle prestazioni con Azure Cosmos DB,</span><span class="sxs-lookup"><span data-stu-id="a249d-228">Want to perform scale and performance testing with Azure Cosmos DB?</span></span> <span data-ttu-id="a249d-229">vedere [Test delle prestazioni e della scalabilità con Azure Cosmos DB](performance-testing.md).</span><span class="sxs-lookup"><span data-stu-id="a249d-229">See [Performance and Scale Testing with Azure Cosmos DB](performance-testing.md)</span></span>
* <span data-ttu-id="a249d-230">Informazioni su come [monitorare un account Azure Cosmos DB](monitor-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="a249d-230">Learn how to [monitor an Azure Cosmos DB account](monitor-accounts.md).</span></span>
* <span data-ttu-id="a249d-231">Eseguire query sul set di dati di esempio illustrato nella pagina [Query Playground](https://www.documentdb.com/sql/demo).</span><span class="sxs-lookup"><span data-stu-id="a249d-231">Run queries against our sample dataset in the [Query Playground](https://www.documentdb.com/sql/demo).</span></span>
* <span data-ttu-id="a249d-232">Esplorare la [Documentazione di Azure Cosmos DB](https://docs.microsoft.com/azure/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="a249d-232">Explore the [Azure Cosmos DB documentation](https://docs.microsoft.com/azure/documentdb/).</span></span>

[Node.js]: http://nodejs.org/
[Git]: http://git-scm.com/
[GitHub]: https://github.com/Azure-Samples/documentdb-node-todo-app

