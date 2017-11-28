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
# <span data-ttu-id="0d488-104"><a name="_Toc395783175"></a>Creare un'applicazione Web Node.js con Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="0d488-104"><a name="_Toc395783175"></a>Build a Node.js web application using Azure Cosmos DB</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0d488-105">.NET</span><span class="sxs-lookup"><span data-stu-id="0d488-105">.NET</span></span>](documentdb-dotnet-application.md)
> * [<span data-ttu-id="0d488-106">Node.JS</span><span class="sxs-lookup"><span data-stu-id="0d488-106">Node.js</span></span>](documentdb-nodejs-application.md)
> * [<span data-ttu-id="0d488-107">Java</span><span class="sxs-lookup"><span data-stu-id="0d488-107">Java</span></span>](documentdb-java-application.md)
> * [<span data-ttu-id="0d488-108">Python</span><span class="sxs-lookup"><span data-stu-id="0d488-108">Python</span></span>](documentdb-python-application.md)
> 
> 

<span data-ttu-id="0d488-109">Questa esercitazione Node.js illustra come toouse DB Cosmos Azure e l'API DocumentDB toostore e accedere ai dati da un'applicazione Node.js Express hello ospitato nei siti Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="0d488-109">This Node.js tutorial shows you how toouse Azure Cosmos DB and hello DocumentDB API toostore and access data from a Node.js Express application hosted on Azure Websites.</span></span> <span data-ttu-id="0d488-110">Verrà creata una semplice applicazione di gestione delle attività basata su Web, un'app ToDo, che consente di creare, recuperare e completare le attività.</span><span class="sxs-lookup"><span data-stu-id="0d488-110">You build a simple web-based task-management application, a ToDo app, that allows creating, retrieving, and completing tasks.</span></span> <span data-ttu-id="0d488-111">attività Hello vengono archiviate come documenti JSON in Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="0d488-111">hello tasks are stored as JSON documents in Azure Cosmos DB.</span></span> <span data-ttu-id="0d488-112">In questa esercitazione viene illustrata la creazione di hello e la distribuzione dell'applicazione hello e illustra ciò che avviene in ogni frammento di codice.</span><span class="sxs-lookup"><span data-stu-id="0d488-112">This tutorial walks you through hello creation and deployment of hello app and explains what's happening in each snippet.</span></span>

![Cattura di schermata di hello applicazione elenco attività personali creato in questa esercitazione Node.js](./media/documentdb-nodejs-application/cosmos-db-node-js-mytodo.png)

<span data-ttu-id="0d488-114">Non dispongono di esercitazione hello toocomplete di tempo e si desidera tooget soluzione completa di hello?</span><span class="sxs-lookup"><span data-stu-id="0d488-114">Don't have time toocomplete hello tutorial and just want tooget hello complete solution?</span></span> <span data-ttu-id="0d488-115">Non è un problema, è possibile ottenere soluzione di esempio completo di hello da [GitHub][GitHub].</span><span class="sxs-lookup"><span data-stu-id="0d488-115">Not a problem, you can get hello complete sample solution from [GitHub][GitHub].</span></span> <span data-ttu-id="0d488-116">Solo lettura hello [Leggimi](https://github.com/Azure-Samples/documentdb-node-todo-app/blob/master/README.md) file per istruzioni su come toorun hello app.</span><span class="sxs-lookup"><span data-stu-id="0d488-116">Just read hello [Readme](https://github.com/Azure-Samples/documentdb-node-todo-app/blob/master/README.md) file for instructions on how toorun hello app.</span></span>

## <span data-ttu-id="0d488-117"><a name="_Toc395783176"></a>Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="0d488-117"><a name="_Toc395783176"></a>Prerequisites</span></span>
> [!TIP]
> <span data-ttu-id="0d488-118">Questa esercitazione Node.js presuppone già una certa esperienza nell'uso di Node.js e di Siti Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="0d488-118">This Node.js tutorial assumes that you have some prior experience using Node.js and Azure Websites.</span></span>
> 
> 

<span data-ttu-id="0d488-119">Prima di seguire le istruzioni di hello in questo articolo, è necessario assicurarsi di aver seguito hello:</span><span class="sxs-lookup"><span data-stu-id="0d488-119">Before following hello instructions in this article, you should ensure that you have hello following:</span></span>

* <span data-ttu-id="0d488-120">Un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="0d488-120">An active Azure account.</span></span> <span data-ttu-id="0d488-121">Se non si dispone di un account, è possibile creare un account di valutazione gratuita in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="0d488-121">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="0d488-122">Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0d488-122">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

   <span data-ttu-id="0d488-123">OPPURE</span><span class="sxs-lookup"><span data-stu-id="0d488-123">OR</span></span>

   <span data-ttu-id="0d488-124">Un'installazione locale di hello [Azure Cosmos DB emulatore](local-emulator.md) (solo Windows).</span><span class="sxs-lookup"><span data-stu-id="0d488-124">A local installation of hello [Azure Cosmos DB Emulator](local-emulator.md) (Windows only).</span></span>
* <span data-ttu-id="0d488-125">[Node.js][Node.js] 0.10.29 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="0d488-125">[Node.js][Node.js] version v0.10.29 or higher.</span></span>
* <span data-ttu-id="0d488-126">[Generatore di Express](http://www.expressjs.com/starter/generator.html), installabile tramite `npm install express-generator -g`</span><span class="sxs-lookup"><span data-stu-id="0d488-126">[Express generator](http://www.expressjs.com/starter/generator.html) (you can install this via `npm install express-generator -g`)</span></span>
* <span data-ttu-id="0d488-127">[Git][Git].</span><span class="sxs-lookup"><span data-stu-id="0d488-127">[Git][Git].</span></span>

## <span data-ttu-id="0d488-128"><a name="_Toc395637761"></a>Passaggio 1: Creare un account del database di Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="0d488-128"><a name="_Toc395637761"></a>Step 1: Create an Azure Cosmos DB database account</span></span>
<span data-ttu-id="0d488-129">Creare prima di tutto un account Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="0d488-129">Let's start by creating an Azure Cosmos DB account.</span></span> <span data-ttu-id="0d488-130">Se è già un account o se si utilizza hello Azure Cosmos DB emulatore per questa esercitazione, è possibile ignorare troppo[passaggio 2: creare una nuova applicazione Node.js](#_Toc395783178).</span><span class="sxs-lookup"><span data-stu-id="0d488-130">If you already have an account or if you are using hello Azure Cosmos DB Emulator for this tutorial, you can skip too[Step 2: Create a new Node.js application](#_Toc395783178).</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

[!INCLUDE [cosmos-db-keys](../../includes/cosmos-db-keys.md)]

## <span data-ttu-id="0d488-131"><a name="_Toc395783178"></a>Passaggio 2: Creare una nuova applicazione Node.js</span><span class="sxs-lookup"><span data-stu-id="0d488-131"><a name="_Toc395783178"></a>Step 2: Create a new Node.js application</span></span>
<span data-ttu-id="0d488-132">Ora esaminiamo un progetto di base Hello World Node.js utilizzando hello toocreate [Express](http://expressjs.com/) framework.</span><span class="sxs-lookup"><span data-stu-id="0d488-132">Now let's learn toocreate a basic Hello World Node.js project using hello [Express](http://expressjs.com/) framework.</span></span>

1. <span data-ttu-id="0d488-133">Aprire il terminal preferito, ad esempio hello Node.js il prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="0d488-133">Open your favorite terminal, such as hello Node.js command prompt.</span></span>
2. <span data-ttu-id="0d488-134">Passare toohello directory in cui si desidera nuova applicazione di toostore hello.</span><span class="sxs-lookup"><span data-stu-id="0d488-134">Navigate toohello directory in which you'd like toostore hello new application.</span></span>
3. <span data-ttu-id="0d488-135">Utilizzare hello generatore express toogenerate una nuova applicazione denominata **todo**.</span><span class="sxs-lookup"><span data-stu-id="0d488-135">Use hello express generator toogenerate a new application called **todo**.</span></span>
   
        express todo
4. <span data-ttu-id="0d488-136">Aprire la nuova directory **todo** e installare le dipendenze.</span><span class="sxs-lookup"><span data-stu-id="0d488-136">Open your new **todo** directory and install dependencies.</span></span>
   
        cd todo
        npm install
5. <span data-ttu-id="0d488-137">Eseguire la nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="0d488-137">Run your new application.</span></span>
   
        npm start
6. <span data-ttu-id="0d488-138">È possibile visualizzare la nuova applicazione passando il browser troppo[http://localhost:3000](http://localhost:3000).</span><span class="sxs-lookup"><span data-stu-id="0d488-138">You can view your new application by navigating your browser too[http://localhost:3000](http://localhost:3000).</span></span>
   
    ![Informazioni su Node.js - schermata di hello applicazione Hello World in una finestra del browser](./media/documentdb-nodejs-application/cosmos-db-node-js-express.png)

    <span data-ttu-id="0d488-140">Quindi, toostop hello applicazione, premere CTRL + C nella finestra terminal hello e quindi fare clic su **y** processo batch di hello tooterminate.</span><span class="sxs-lookup"><span data-stu-id="0d488-140">Then, toostop hello application, press CTRL+C in hello terminal window and then click **y** tooterminate hello batch job.</span></span>

## <span data-ttu-id="0d488-141"><a name="_Toc395783179"></a>Passaggio 3: Installare moduli aggiuntivi</span><span class="sxs-lookup"><span data-stu-id="0d488-141"><a name="_Toc395783179"></a>Step 3: Install additional modules</span></span>
<span data-ttu-id="0d488-142">Hello **package. JSON** file è uno dei file hello creati nella directory radice del progetto hello hello.</span><span class="sxs-lookup"><span data-stu-id="0d488-142">hello **package.json** file is one of hello files created in hello root of hello project.</span></span> <span data-ttu-id="0d488-143">Questo file contiene un elenco di moduli aggiuntivi necessari per l'applicazione Node.js.</span><span class="sxs-lookup"><span data-stu-id="0d488-143">This file contains a list of additional modules that are required for your Node.js application.</span></span> <span data-ttu-id="0d488-144">In seguito, quando si distribuisce questo tooAzure applicazione siti Web, questo file viene utilizzato toodetermine quali toobe necessità di moduli in Azure toosupport l'applicazione installata.</span><span class="sxs-lookup"><span data-stu-id="0d488-144">Later, when you deploy this application tooAzure Websites, this file is used toodetermine which modules need toobe installed on Azure toosupport your application.</span></span> <span data-ttu-id="0d488-145">È comunque necessario tooinstall due altri pacchetti per questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="0d488-145">We still need tooinstall two more packages for this tutorial.</span></span>

1. <span data-ttu-id="0d488-146">In hello terminal, installare hello **async** modulo tramite npm.</span><span class="sxs-lookup"><span data-stu-id="0d488-146">Back in hello terminal, install hello **async** module via npm.</span></span>
   
        npm install async --save
2. <span data-ttu-id="0d488-147">Installare hello **documentdb** modulo tramite npm.</span><span class="sxs-lookup"><span data-stu-id="0d488-147">Install hello **documentdb** module via npm.</span></span> <span data-ttu-id="0d488-148">Questo è il modulo di hello in cui viene eseguita chiave di Azure Cosmos DB hello tutti.</span><span class="sxs-lookup"><span data-stu-id="0d488-148">This is hello module where all hello Azure Cosmos DB magic happens.</span></span>
   
        npm install documentdb --save
3. <span data-ttu-id="0d488-149">Un rapido controllo di hello **package. JSON** file dell'applicazione hello deve visualizzare hello moduli aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="0d488-149">A quick check of hello **package.json** file of hello application should show hello additional modules.</span></span> <span data-ttu-id="0d488-150">Questo file verrà indicare quali toodownload pacchetti ad Azure e installare durante l'esecuzione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="0d488-150">This file will tell Azure which packages toodownload and install when running your application.</span></span> <span data-ttu-id="0d488-151">Il risultato sarà simile esempio hello riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="0d488-151">It should resemble hello example below.</span></span>
   
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
   
    <span data-ttu-id="0d488-152">Ciò indicherà a Node (e più avanti ad Azure) che l'applicazione dipende da questi moduli aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="0d488-152">This tells Node (and Azure later) that your application depends on these additional modules.</span></span>

## <span data-ttu-id="0d488-153"><a name="_Toc395783180"></a>Passaggio 4: Utilizzo del servizio di Azure Cosmos DB hello in un'applicazione di nodo</span><span class="sxs-lookup"><span data-stu-id="0d488-153"><a name="_Toc395783180"></a>Step 4: Using hello Azure Cosmos DB service in a node application</span></span>
<span data-ttu-id="0d488-154">Che si occupa di tutto la configurazione iniziale di hello e la configurazione, ora si get verso il basso toowhy siamo qui, ovvero toowrite alcuni codice che usa Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="0d488-154">That takes care of all hello initial setup and configuration, now let’s get down toowhy we’re here, and that’s toowrite some code using Azure Cosmos DB.</span></span>

### <a name="create-hello-model"></a><span data-ttu-id="0d488-155">Creare il modello di hello</span><span class="sxs-lookup"><span data-stu-id="0d488-155">Create hello model</span></span>
1. <span data-ttu-id="0d488-156">Nella directory di progetto hello, creare una nuova directory denominata **modelli** in hello stessa directory del file package. JSON hello.</span><span class="sxs-lookup"><span data-stu-id="0d488-156">In hello project directory, create a new directory named **models** in hello same directory as hello package.json file.</span></span>
2. <span data-ttu-id="0d488-157">In hello **modelli** directory, creare un nuovo file denominato **taskDao.js**.</span><span class="sxs-lookup"><span data-stu-id="0d488-157">In hello **models** directory, create a new file named **taskDao.js**.</span></span> <span data-ttu-id="0d488-158">Questo file contiene il modello di hello per le operazioni di hello create tramite l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="0d488-158">This file will contain hello model for hello tasks created by our application.</span></span>
3. <span data-ttu-id="0d488-159">In hello stesso **modelli** directory, creare un nuovo file denominato **docdbUtils.js**.</span><span class="sxs-lookup"><span data-stu-id="0d488-159">In hello same **models** directory, create another new file named **docdbUtils.js**.</span></span> <span data-ttu-id="0d488-160">Questo file conterrà porzioni di codice utile e riutilizzabile, che verrà usato nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="0d488-160">This file will contain some useful, reusable, code that we will use throughout our application.</span></span> 
4. <span data-ttu-id="0d488-161">Copia hello di codice seguente troppo**docdbUtils.js**</span><span class="sxs-lookup"><span data-stu-id="0d488-161">Copy hello following code in too**docdbUtils.js**</span></span>
   
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
   
5. <span data-ttu-id="0d488-162">Salvare e chiudere hello **docdbUtils.js** file.</span><span class="sxs-lookup"><span data-stu-id="0d488-162">Save and close hello **docdbUtils.js** file.</span></span>
6. <span data-ttu-id="0d488-163">All'inizio di hello di hello **taskDao.js** file, aggiungere i seguenti hello tooreference codice hello **DocumentDBClient** hello e **docdbUtils.js** creato in precedenza:</span><span class="sxs-lookup"><span data-stu-id="0d488-163">At hello beginning of hello **taskDao.js** file, add hello following code tooreference hello **DocumentDBClient** and hello **docdbUtils.js** we created above:</span></span>
   
        var DocumentDBClient = require('documentdb').DocumentClient;
        var docdbUtils = require('./docdbUtils');
7. <span data-ttu-id="0d488-164">Successivamente, aggiungere codice toodefine che esporta l'oggetto attività hello.</span><span class="sxs-lookup"><span data-stu-id="0d488-164">Next, you will add code toodefine and export hello Task object.</span></span> <span data-ttu-id="0d488-165">Questo è responsabile per l'inizializzazione dell'oggetto di attività e configurando hello Database e la raccolta documenti verrà utilizzato.</span><span class="sxs-lookup"><span data-stu-id="0d488-165">This is responsible for initializing our Task object and setting up hello Database and Document Collection we will use.</span></span>
   
        function TaskDao(documentDBClient, databaseId, collectionId) {
          this.client = documentDBClient;
          this.databaseId = databaseId;
          this.collectionId = collectionId;
   
          this.database = null;
          this.collection = null;
        }
   
        module.exports = TaskDao;
8. <span data-ttu-id="0d488-166">Successivamente, aggiungere hello seguito metodi aggiuntivi di codice toodefine nell'oggetto attività hello, che consentono le interazioni con i dati archiviati nel database di Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="0d488-166">Next, add hello following code toodefine additional methods on hello Task object, which allow interactions with data stored in Azure Cosmos DB.</span></span>
   
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
9. <span data-ttu-id="0d488-167">Salvare e chiudere hello **taskDao.js** file.</span><span class="sxs-lookup"><span data-stu-id="0d488-167">Save and close hello **taskDao.js** file.</span></span> 

### <a name="create-hello-controller"></a><span data-ttu-id="0d488-168">Creare controller hello</span><span class="sxs-lookup"><span data-stu-id="0d488-168">Create hello controller</span></span>
1. <span data-ttu-id="0d488-169">In hello **route** directory del progetto, creare un nuovo file denominato **tasklist.js**.</span><span class="sxs-lookup"><span data-stu-id="0d488-169">In hello **routes** directory of your project, create a new file named **tasklist.js**.</span></span> 
2. <span data-ttu-id="0d488-170">Aggiungere hello seguente codice troppo**tasklist.js**.</span><span class="sxs-lookup"><span data-stu-id="0d488-170">Add hello following code too**tasklist.js**.</span></span> <span data-ttu-id="0d488-171">Viene caricato hello DocumentDBClient e async moduli, che vengono utilizzati da **tasklist.js**.</span><span class="sxs-lookup"><span data-stu-id="0d488-171">This loads hello DocumentDBClient and async modules, which are used by **tasklist.js**.</span></span> <span data-ttu-id="0d488-172">Questo elemento anche definito hello **TaskList** funzione, che viene passata un'istanza di hello **attività** dell'oggetto definita in precedenza:</span><span class="sxs-lookup"><span data-stu-id="0d488-172">This also defined hello **TaskList** function, which is passed an instance of hello **Task** object we defined earlier:</span></span>
   
        var DocumentDBClient = require('documentdb').DocumentClient;
        var async = require('async');
   
        function TaskList(taskDao) {
          this.taskDao = taskDao;
        }
   
        module.exports = TaskList;
3. <span data-ttu-id="0d488-173">Continuare ad aggiungere toohello **tasklist.js** file mediante l'aggiunta di metodi hello troppo**showTasks, addTask**, e **completeTasks**:</span><span class="sxs-lookup"><span data-stu-id="0d488-173">Continue adding toohello **tasklist.js** file by adding hello methods used too**showTasks, addTask**, and **completeTasks**:</span></span>
   
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
4. <span data-ttu-id="0d488-174">Salvare e chiudere hello **tasklist.js** file.</span><span class="sxs-lookup"><span data-stu-id="0d488-174">Save and close hello **tasklist.js** file.</span></span>

### <a name="add-configjs"></a><span data-ttu-id="0d488-175">Aggiungere config.json</span><span class="sxs-lookup"><span data-stu-id="0d488-175">Add config.js</span></span>
1. <span data-ttu-id="0d488-176">Nella directory del progetto creare un nuovo file denominato **config.js**.</span><span class="sxs-lookup"><span data-stu-id="0d488-176">In your project directory create a new file named **config.js**.</span></span>
2. <span data-ttu-id="0d488-177">Aggiungere il seguente troppo di hello**config.js**.</span><span class="sxs-lookup"><span data-stu-id="0d488-177">Add hello following too**config.js**.</span></span> <span data-ttu-id="0d488-178">Definisce le impostazioni e i valori di configurazione necessari per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="0d488-178">This defines configuration settings and values needed for our application.</span></span>
   
        var config = {}
   
        config.host = process.env.HOST || "[hello URI value from hello Azure Cosmos DB Keys blade on http://portal.azure.com]";
        config.authKey = process.env.AUTH_KEY || "[hello PRIMARY KEY value from hello Azure Cosmos DB Keys blade on http://portal.azure.com]";
        config.databaseId = "ToDoList";
        config.collectionId = "Items";
   
        module.exports = config;
3. <span data-ttu-id="0d488-179">In hello **config.js** file, i valori hello aggiornamento dell'HOST e utilizzando i valori hello trovati nel Pannello di hello chiavi dell'account di Azure Cosmos DB hello AUTH_KEY [portale Microsoft Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0d488-179">In hello **config.js** file, update hello values of HOST and AUTH_KEY using hello values found in hello Keys blade of your Azure Cosmos DB account on hello [Microsoft Azure portal](https://portal.azure.com).</span></span>
4. <span data-ttu-id="0d488-180">Salvare e chiudere hello **config.js** file.</span><span class="sxs-lookup"><span data-stu-id="0d488-180">Save and close hello **config.js** file.</span></span>

### <a name="modify-appjs"></a><span data-ttu-id="0d488-181">Modificare il file app.js</span><span class="sxs-lookup"><span data-stu-id="0d488-181">Modify app.js</span></span>
1. <span data-ttu-id="0d488-182">Nella directory di progetto hello, aprire hello **app.js** file.</span><span class="sxs-lookup"><span data-stu-id="0d488-182">In hello project directory, open hello **app.js** file.</span></span> <span data-ttu-id="0d488-183">Questo file è stato creato in precedenza, quando un'applicazione web hello Express è stata creata.</span><span class="sxs-lookup"><span data-stu-id="0d488-183">This file was created earlier when hello Express web application was created.</span></span>
2. <span data-ttu-id="0d488-184">Aggiungere hello seguente codice toohello cima a **app.js**</span><span class="sxs-lookup"><span data-stu-id="0d488-184">Add hello following code toohello top of **app.js**</span></span>
   
        var DocumentDBClient = require('documentdb').DocumentClient;
        var config = require('./config');
        var TaskList = require('./routes/tasklist');
        var TaskDao = require('./models/taskDao');
3. <span data-ttu-id="0d488-185">Questo codice definisce hello toobe di file di configurazione utilizzato e procede valori tooread da questo file in alcune variabili che non appena si utilizzerà.</span><span class="sxs-lookup"><span data-stu-id="0d488-185">This code defines hello config file toobe used, and proceeds tooread values out of this file into some variables we will use soon.</span></span>
4. <span data-ttu-id="0d488-186">Sostituire hello seguenti due righe in **app.js** file:</span><span class="sxs-lookup"><span data-stu-id="0d488-186">Replace hello following two lines in **app.js** file:</span></span>
   
        app.use('/', index);
        app.use('/users', users); 
   
      <span data-ttu-id="0d488-187">con hello frammento di codice seguente:</span><span class="sxs-lookup"><span data-stu-id="0d488-187">with hello following snippet:</span></span>
   
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
5. <span data-ttu-id="0d488-188">Queste righe definiscono una nuova istanza della nostri **TaskDao** oggetto, con un nuovo tooAzure connessione DB Cosmos (utilizzando i valori hello leggere hello **config.js**), inizializzare l'oggetto attività hello e quindi associare azioni modulo toomethods nel nostro **TaskList** controller.</span><span class="sxs-lookup"><span data-stu-id="0d488-188">These lines define a new instance of our **TaskDao** object, with a new connection tooAzure Cosmos DB (using hello values read from hello **config.js**), initialize hello task object and then bind form actions toomethods on our **TaskList** controller.</span></span> 
6. <span data-ttu-id="0d488-189">Infine, salvare e chiudere hello **app.js** file, è quasi completata.</span><span class="sxs-lookup"><span data-stu-id="0d488-189">Finally, save and close hello **app.js** file, we're just about done.</span></span>

## <span data-ttu-id="0d488-190"><a name="_Toc395783181"></a>Passaggio 5: Creare un'interfaccia utente</span><span class="sxs-lookup"><span data-stu-id="0d488-190"><a name="_Toc395783181"></a>Step 5: Build a user interface</span></span>
<span data-ttu-id="0d488-191">Ora in modo che un utente effettivamente possibile interagire con l'applicazione è possibile attivare l'interfaccia utente di attenzione toobuilding hello.</span><span class="sxs-lookup"><span data-stu-id="0d488-191">Now let’s turn our attention toobuilding hello user interface so a user can actually interact with our application.</span></span> <span data-ttu-id="0d488-192">Hello Express applicazione creata utilizza **Jade** come motore di visualizzazione hello.</span><span class="sxs-lookup"><span data-stu-id="0d488-192">hello Express application we created uses **Jade** as hello view engine.</span></span> <span data-ttu-id="0d488-193">Per ulteriori informazioni su Jade consultare troppo[http://jade-lang.com/](http://jade-lang.com/).</span><span class="sxs-lookup"><span data-stu-id="0d488-193">For more information on Jade please refer too[http://jade-lang.com/](http://jade-lang.com/).</span></span>

1. <span data-ttu-id="0d488-194">Hello **layout.jade** file hello **viste** directory viene utilizzata come modello generale per altri **.jade** file.</span><span class="sxs-lookup"><span data-stu-id="0d488-194">hello **layout.jade** file in hello **views** directory is used as a global template for other **.jade** files.</span></span> <span data-ttu-id="0d488-195">In questo passaggio è necessario modificarlo toouse [Twitter Bootstrap](https://github.com/twbs/bootstrap), che è un toolkit che rende facile toodesign un sito Web professionale nice.</span><span class="sxs-lookup"><span data-stu-id="0d488-195">In this step you will modify it toouse [Twitter Bootstrap](https://github.com/twbs/bootstrap), which is a toolkit that makes it easy toodesign a nice looking website.</span></span> 
2. <span data-ttu-id="0d488-196">Aprire hello **layout.jade** file trovato in hello **viste** cartella e sostituire il contenuto di hello con seguenti hello:</span><span class="sxs-lookup"><span data-stu-id="0d488-196">Open hello **layout.jade** file found in hello **views** folder and replace hello contents with hello following:</span></span>

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

    <span data-ttu-id="0d488-197">Ciò indica in modo efficace hello **Jade** toorender del motore del codice HTML per l'applicazione e crea un **blocco** chiamato **contenuto** in cui sia possibile fornire layout hello per il contenuto numero di pagine.</span><span class="sxs-lookup"><span data-stu-id="0d488-197">This effectively tells hello **Jade** engine toorender some HTML for our application and creates a **block** called **content** where we can supply hello layout for our content pages.</span></span>

    <span data-ttu-id="0d488-198">Salvare e chiudere il file **layout.jade** .</span><span class="sxs-lookup"><span data-stu-id="0d488-198">Save and close this **layout.jade** file.</span></span>

3. <span data-ttu-id="0d488-199">Aprire quindi hello **index.jade** file, la visualizzazione di hello che verrà utilizzato dall'applicazione e sostituirà il contenuto di hello del file hello con hello seguente:</span><span class="sxs-lookup"><span data-stu-id="0d488-199">Now open hello **index.jade** file, hello view that will be used by our application, and replace hello content of hello file with hello following:</span></span>
   
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
   

<span data-ttu-id="0d488-200">Questo layout estende e vengono forniti contenuti hello **contenuto** segnaposto è stato illustrato in hello **layout.jade** file in precedenza.</span><span class="sxs-lookup"><span data-stu-id="0d488-200">This extends layout, and provides content for hello **content** placeholder we saw in hello **layout.jade** file earlier.</span></span>
   
<span data-ttu-id="0d488-201">In questo layout sono stati creati due moduli HTML.</span><span class="sxs-lookup"><span data-stu-id="0d488-201">In this layout we created two HTML forms.</span></span>

<span data-ttu-id="0d488-202">primo form Hello contiene una tabella per i dati e un pulsante che consente di elaborare gli elementi tooupdate inviando troppo**/completetask** metodo per il controller.</span><span class="sxs-lookup"><span data-stu-id="0d488-202">hello first form contains a table for our data and a button that allows us tooupdate items by posting too**/completetask** method of our controller.</span></span>
    
<span data-ttu-id="0d488-203">seconda forma Hello contiene due campi di input e un pulsante che consente di elaborare un nuovo elemento toocreate inviando troppo**/addtask** metodo per il controller.</span><span class="sxs-lookup"><span data-stu-id="0d488-203">hello second form contains two input fields and a button that allows us toocreate a new item by posting too**/addtask** method of our controller.</span></span>

<span data-ttu-id="0d488-204">Deve trattarsi di tutto ciò che è necessario per il nostro toowork dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="0d488-204">This should be all that we need for our application toowork.</span></span>

## <span data-ttu-id="0d488-205"><a name="_Toc395783181"></a>Passaggio 6: Esecuzione dell'applicazione in locale</span><span class="sxs-lookup"><span data-stu-id="0d488-205"><a name="_Toc395783181"></a>Step 6: Run your application locally</span></span>
1. <span data-ttu-id="0d488-206">eseguire sul computer locale, un'applicazione hello tootest `npm start` in hello toostart terminal l'applicazione, quindi aggiornare il [http://localhost:3000](http://localhost:3000) pagina nel browser.</span><span class="sxs-lookup"><span data-stu-id="0d488-206">tootest hello application on your local machine, run `npm start` in hello terminal toostart your application, then refresh your [http://localhost:3000](http://localhost:3000) browser page.</span></span> <span data-ttu-id="0d488-207">pagina Hello dovrebbe apparire come hello immagine riportata di seguito:</span><span class="sxs-lookup"><span data-stu-id="0d488-207">hello page should now look like hello image below:</span></span>
   
    ![Schermata di hello applicazione MyTodo elenco in una finestra del browser](./media/documentdb-nodejs-application/cosmos-db-node-js-localhost.png)

    > [!TIP]
    > <span data-ttu-id="0d488-209">Se si riceve un errore relativo a hello rientro nel file di layout.jade hello o index.jade hello, verificare che hello prime due righe in entrambi i file è giustificato a sinistra, senza spazi.</span><span class="sxs-lookup"><span data-stu-id="0d488-209">If you receive an error about hello indent in hello layout.jade file or hello index.jade file, ensure that hello first two lines in both files is left justified, with no spaces.</span></span> <span data-ttu-id="0d488-210">Se sono presenti spazi prima delle prime due righe di hello, rimuoverli, salvare entrambi i file, quindi aggiornare la finestra del browser.</span><span class="sxs-lookup"><span data-stu-id="0d488-210">If there are spaces before hello first two lines, remove them, save both files, then refresh your browser window.</span></span> 

2. <span data-ttu-id="0d488-211">Utilizzare hello articolo, nome dell'elemento e categoria campi tooenter una nuova attività e quindi fare clic su **Aggiungi elemento**.</span><span class="sxs-lookup"><span data-stu-id="0d488-211">Use hello Item, Item Name and Category fields tooenter a new task and then click **Add Item**.</span></span> <span data-ttu-id="0d488-212">Viene creato un documento in Azure Cosmos DB con queste proprietà.</span><span class="sxs-lookup"><span data-stu-id="0d488-212">This creates a document in Azure Cosmos DB with those properties.</span></span> 
3. <span data-ttu-id="0d488-213">pagina Hello deve aggiornare hello toodisplay appena creato l'elemento nell'elenco attività hello.</span><span class="sxs-lookup"><span data-stu-id="0d488-213">hello page should update toodisplay hello newly created item in hello ToDo list.</span></span>
   
    ![Schermata dell'applicazione hello con un nuovo elemento nell'elenco attività hello](./media/documentdb-nodejs-application/cosmos-db-node-js-added-task.png)
4. <span data-ttu-id="0d488-215">semplicemente casella di controllo hello nella colonna completo hello toocomplete un'attività e quindi fare clic su **aggiornano le attività**.</span><span class="sxs-lookup"><span data-stu-id="0d488-215">toocomplete a task, simply check hello checkbox in hello Complete column, and then click **Update tasks**.</span></span> <span data-ttu-id="0d488-216">Questo documento aggiornamenti hello già stato creato.</span><span class="sxs-lookup"><span data-stu-id="0d488-216">This updates hello document you already created.</span></span>

5. <span data-ttu-id="0d488-217">un'applicazione hello toostop, premere CTRL + C nella finestra terminal hello e quindi fare clic su **Y** processo batch di hello tooterminate.</span><span class="sxs-lookup"><span data-stu-id="0d488-217">toostop hello application, press CTRL+C in hello terminal window and then click **Y** tooterminate hello batch job.</span></span>

## <span data-ttu-id="0d488-218"><a name="_Toc395783182"></a>Passaggio 7: Distribuire il tooAzure di progetto di sviluppo dell'applicazione siti Web</span><span class="sxs-lookup"><span data-stu-id="0d488-218"><a name="_Toc395783182"></a>Step 7: Deploy your application development project tooAzure Websites</span></span>
1. <span data-ttu-id="0d488-219">Se non è ancora stato fatto, abilitare un repository Git per il sito Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="0d488-219">If you haven't already, enable a git repository for your Azure Website.</span></span> <span data-ttu-id="0d488-220">È possibile trovare istruzioni su come toodo in hello [tooAzure distribuzione Git locale del servizio App](../app-service-web/app-service-deploy-local-git.md) argomento.</span><span class="sxs-lookup"><span data-stu-id="0d488-220">You can find instructions on how toodo this in hello [Local Git Deployment tooAzure App Service](../app-service-web/app-service-deploy-local-git.md) topic.</span></span>
2. <span data-ttu-id="0d488-221">Aggiungere il sito Web di Azure come Git remoto.</span><span class="sxs-lookup"><span data-stu-id="0d488-221">Add your Azure Website as a git remote.</span></span>
   
        git remote add azure https://username@your-azure-website.scm.azurewebsites.net:443/your-azure-website.git
3. <span data-ttu-id="0d488-222">Distribuire trasferendo toohello remoto.</span><span class="sxs-lookup"><span data-stu-id="0d488-222">Deploy by pushing toohello remote.</span></span>
   
        git push azure master
4. <span data-ttu-id="0d488-223">Dopo alcuni secondi, Git completerà la pubblicazione dell'applicazione Web e avvierà un browser in cui sarà possibile visualizzare quanto realizzato in esecuzione in Azure.</span><span class="sxs-lookup"><span data-stu-id="0d488-223">In a few seconds, git will finish publishing your web application and launch a browser where you can see your handiwork running in Azure!</span></span>

    <span data-ttu-id="0d488-224">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="0d488-224">Congratulations!</span></span> <span data-ttu-id="0d488-225">Appena creato prima Node.js Express applicazione Web tramite Azure Cosmos DB e pubblicarlo tooAzure siti Web.</span><span class="sxs-lookup"><span data-stu-id="0d488-225">You have just built your first Node.js Express Web Application using Azure Cosmos DB and published it tooAzure Websites.</span></span>

    <span data-ttu-id="0d488-226">Se si desidera toodownload o fare riferimento applicazione informazioni di riferimento complete toohello per questa esercitazione, può essere scaricato da [GitHub][GitHub].</span><span class="sxs-lookup"><span data-stu-id="0d488-226">If you want toodownload or refer toohello complete reference application for this tutorial, it can be downloaded from [GitHub][GitHub].</span></span>

## <span data-ttu-id="0d488-227"><a name="_Toc395637775"></a>Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0d488-227"><a name="_Toc395637775"></a>Next steps</span></span>

* <span data-ttu-id="0d488-228">Desidera tooperform scala e test delle prestazioni con Azure Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="0d488-228">Want tooperform scale and performance testing with Azure Cosmos DB?</span></span> <span data-ttu-id="0d488-229">vedere [Test delle prestazioni e della scalabilità con Azure Cosmos DB](performance-testing.md).</span><span class="sxs-lookup"><span data-stu-id="0d488-229">See [Performance and Scale Testing with Azure Cosmos DB](performance-testing.md)</span></span>
* <span data-ttu-id="0d488-230">Informazioni su come troppo[monitorare un account Azure Cosmos DB](monitor-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="0d488-230">Learn how too[monitor an Azure Cosmos DB account](monitor-accounts.md).</span></span>
* <span data-ttu-id="0d488-231">Eseguire query su questo set di dati di esempio in hello [Query Playground](https://www.documentdb.com/sql/demo).</span><span class="sxs-lookup"><span data-stu-id="0d488-231">Run queries against our sample dataset in hello [Query Playground](https://www.documentdb.com/sql/demo).</span></span>
* <span data-ttu-id="0d488-232">Esplorare hello [documentazione di Azure Cosmos DB](https://docs.microsoft.com/azure/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="0d488-232">Explore hello [Azure Cosmos DB documentation](https://docs.microsoft.com/azure/documentdb/).</span></span>

[Node.js]: http://nodejs.org/
[Git]: http://git-scm.com/
[GitHub]: https://github.com/Azure-Samples/documentdb-node-todo-app

