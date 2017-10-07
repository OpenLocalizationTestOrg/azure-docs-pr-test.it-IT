---
title: esercitazione aaaNode.js per hello API DocumentDB per Azure Cosmos DB | Documenti Microsoft
description: In questa esercitazione Node.js che crea un database Cosmos con hello API DocumentDB.
keywords: esercitazione su node.js, database nodo
services: cosmos-db
documentationcenter: node.js
author: AndrewHoh
manager: jhubbard
editor: monicar
ms.assetid: 14d52110-1dce-4ac0-9dd9-f936afccd550
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: node
ms.topic: article
ms.date: 08/14/2017
ms.author: anhoh
ms.openlocfilehash: fce244c6a5f321608e82ca51a2c987e84b98bffa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="nodejs-tutorial-use-hello-documentdb-api-in-azure-cosmos-db-toocreate-a-nodejs-console-application"></a><span data-ttu-id="a2e05-104">Esercitazione di Node.js: hello di utilizzare l'API DocumentDB in Azure Cosmos DB toocreate un'applicazione console Node.js</span><span class="sxs-lookup"><span data-stu-id="a2e05-104">Node.js tutorial: Use hello DocumentDB API in Azure Cosmos DB toocreate a Node.js console application</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a2e05-105">.NET</span><span class="sxs-lookup"><span data-stu-id="a2e05-105">.NET</span></span>](documentdb-get-started.md)
> * [<span data-ttu-id="a2e05-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="a2e05-106">.NET Core</span></span>](documentdb-dotnetcore-get-started.md)
> * [<span data-ttu-id="a2e05-107">Node.js per MongoDB</span><span class="sxs-lookup"><span data-stu-id="a2e05-107">Node.js for MongoDB</span></span>](mongodb-samples.md)
> * [<span data-ttu-id="a2e05-108">Node.js</span><span class="sxs-lookup"><span data-stu-id="a2e05-108">Node.js</span></span>](documentdb-nodejs-get-started.md)
> * [<span data-ttu-id="a2e05-109">Java</span><span class="sxs-lookup"><span data-stu-id="a2e05-109">Java</span></span>](documentdb-java-get-started.md)
> * [<span data-ttu-id="a2e05-110">C++</span><span class="sxs-lookup"><span data-stu-id="a2e05-110">C++</span></span>](documentdb-cpp-get-started.md)
>  
> 

<span data-ttu-id="a2e05-111">Benvenuti toohello Node.js esercitazione per hello Azure Cosmos DB Node.js SDK.</span><span class="sxs-lookup"><span data-stu-id="a2e05-111">Welcome toohello Node.js tutorial for hello Azure Cosmos DB Node.js SDK!</span></span> <span data-ttu-id="a2e05-112">Dopo aver seguito questa esercitazione, si otterrà un'applicazione console che consente di creare e ridefinire le query delle risorse Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="a2e05-112">After following this tutorial, you'll have a console application that creates and queries Azure Cosmos DB resources.</span></span>

<span data-ttu-id="a2e05-113">Tratteremo questo argomento:</span><span class="sxs-lookup"><span data-stu-id="a2e05-113">We'll cover:</span></span>

* <span data-ttu-id="a2e05-114">Creazione e connessione account Azure Cosmos DB tooan</span><span class="sxs-lookup"><span data-stu-id="a2e05-114">Creating and connecting tooan Azure Cosmos DB account</span></span>
* <span data-ttu-id="a2e05-115">Configurazione dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="a2e05-115">Setting up your application</span></span>
* <span data-ttu-id="a2e05-116">Creazione di un database nodo</span><span class="sxs-lookup"><span data-stu-id="a2e05-116">Creating a node database</span></span>
* <span data-ttu-id="a2e05-117">Creare una raccolta</span><span class="sxs-lookup"><span data-stu-id="a2e05-117">Creating a collection</span></span>
* <span data-ttu-id="a2e05-118">Creazione di documenti JSON</span><span class="sxs-lookup"><span data-stu-id="a2e05-118">Creating JSON documents</span></span>
* <span data-ttu-id="a2e05-119">Esecuzione di query hello raccolta</span><span class="sxs-lookup"><span data-stu-id="a2e05-119">Querying hello collection</span></span>
* <span data-ttu-id="a2e05-120">Sostituzione di un documento</span><span class="sxs-lookup"><span data-stu-id="a2e05-120">Replacing a document</span></span>
* <span data-ttu-id="a2e05-121">Eliminazione di un documento</span><span class="sxs-lookup"><span data-stu-id="a2e05-121">Deleting a document</span></span>
* <span data-ttu-id="a2e05-122">L'eliminazione di hello nodo database</span><span class="sxs-lookup"><span data-stu-id="a2e05-122">Deleting hello node database</span></span>

<span data-ttu-id="a2e05-123">Non si ha tempo?</span><span class="sxs-lookup"><span data-stu-id="a2e05-123">Don't have time?</span></span> <span data-ttu-id="a2e05-124">Nessun problema.</span><span class="sxs-lookup"><span data-stu-id="a2e05-124">Don't worry!</span></span> <span data-ttu-id="a2e05-125">la soluzione completa di Hello è disponibile in [GitHub](https://github.com/Azure-Samples/documentdb-node-getting-started).</span><span class="sxs-lookup"><span data-stu-id="a2e05-125">hello complete solution is available on [GitHub](https://github.com/Azure-Samples/documentdb-node-getting-started).</span></span> <span data-ttu-id="a2e05-126">Vedere [ottenere una soluzione completa hello](#GetSolution) per istruzioni rapide.</span><span class="sxs-lookup"><span data-stu-id="a2e05-126">See [Get hello complete solution](#GetSolution) for quick instructions.</span></span>

<span data-ttu-id="a2e05-127">Dopo aver completato l'esercitazione Node.js hello,. utilizzare hello pulsanti di voto in hello superiore e inferiore di questa pagina di toogive ci commenti e suggerimenti.</span><span class="sxs-lookup"><span data-stu-id="a2e05-127">After you've completed hello Node.js tutorial, please use hello voting buttons at hello top and bottom of this page toogive us feedback.</span></span> <span data-ttu-id="a2e05-128">Se desideri toocontact direttamente, ritieni libero tooinclude posta nei commenti.</span><span class="sxs-lookup"><span data-stu-id="a2e05-128">If you'd like us toocontact you directly, feel free tooinclude your email address in your comments.</span></span>

<span data-ttu-id="a2e05-129">Ecco come procedere.</span><span class="sxs-lookup"><span data-stu-id="a2e05-129">Now let's get started!</span></span>

## <a name="prerequisites-for-hello-nodejs-tutorial"></a><span data-ttu-id="a2e05-130">Prerequisiti per l'esercitazione Node.js hello</span><span class="sxs-lookup"><span data-stu-id="a2e05-130">Prerequisites for hello Node.js tutorial</span></span>
<span data-ttu-id="a2e05-131">Assicurarsi di avere hello segue:</span><span class="sxs-lookup"><span data-stu-id="a2e05-131">Please make sure you have hello following:</span></span>

* <span data-ttu-id="a2e05-132">Un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="a2e05-132">An active Azure account.</span></span> <span data-ttu-id="a2e05-133">Se non si ha un account, è possibile iscriversi per ottenere una [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a2e05-133">If you don't have one, you can sign up for a [Free Azure Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
    * <span data-ttu-id="a2e05-134">In alternativa, è possibile utilizzare hello [Azure Cosmos DB emulatore](local-emulator.md) per questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="a2e05-134">Alternatively, you can use hello [Azure Cosmos DB Emulator](local-emulator.md) for this tutorial.</span></span>
* <span data-ttu-id="a2e05-135">[Node.js](https://nodejs.org/) v0.10.29 o versioni successive.</span><span class="sxs-lookup"><span data-stu-id="a2e05-135">[Node.js](https://nodejs.org/) version v0.10.29 or higher.</span></span>

## <a name="step-1-create-an-azure-cosmos-db-account"></a><span data-ttu-id="a2e05-136">Passaggio 1: Creare un account di Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="a2e05-136">Step 1: Create an Azure Cosmos DB account</span></span>
<span data-ttu-id="a2e05-137">Creare prima di tutto un account Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="a2e05-137">Let's create an Azure Cosmos DB account.</span></span> <span data-ttu-id="a2e05-138">Se si dispone già di un account a cui si vuole toouse, è possibile andare troppo[impostare l'applicazione di Node.js](#SetupNode).</span><span class="sxs-lookup"><span data-stu-id="a2e05-138">If you already have an account you want toouse, you can skip ahead too[Set up your Node.js application](#SetupNode).</span></span> <span data-ttu-id="a2e05-139">Se si utilizza hello Azure Cosmos DB emulatore, eseguire le operazioni di hello in [emulatore di Azure Cosmos DB](local-emulator.md) toosetup hello emulatore e andare troppo[impostare l'applicazione di Node.js](#SetupNode).</span><span class="sxs-lookup"><span data-stu-id="a2e05-139">If you are using hello Azure Cosmos DB Emulator, please follow hello steps at [Azure Cosmos DB Emulator](local-emulator.md) toosetup hello emulator and skip ahead too[Set up your Node.js application](#SetupNode).</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <span data-ttu-id="a2e05-140"><a id="SetupNode"></a>Passaggio 2: Configurare l'applicazione Node.js</span><span class="sxs-lookup"><span data-stu-id="a2e05-140"><a id="SetupNode"></a>Step 2: Set up your Node.js application</span></span>
1. <span data-ttu-id="a2e05-141">Aprire il terminale preferito.</span><span class="sxs-lookup"><span data-stu-id="a2e05-141">Open your favorite terminal.</span></span>
2. <span data-ttu-id="a2e05-142">Individuare la cartella hello o la directory in cui si desidera toosave l'applicazione di Node.js.</span><span class="sxs-lookup"><span data-stu-id="a2e05-142">Locate hello folder or directory where you'd like toosave your Node.js application.</span></span>
3. <span data-ttu-id="a2e05-143">Creare due file JavaScript vuoti con hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="a2e05-143">Create two empty JavaScript files with hello following commands:</span></span>
   * <span data-ttu-id="a2e05-144">Windows:</span><span class="sxs-lookup"><span data-stu-id="a2e05-144">Windows:</span></span>
     * ```fsutil file createnew app.js 0```
     * ```fsutil file createnew config.js 0```
   * <span data-ttu-id="a2e05-145">Linux/OS X:</span><span class="sxs-lookup"><span data-stu-id="a2e05-145">Linux/OS X:</span></span>
     * ```touch app.js```
     * ```touch config.js```
4. <span data-ttu-id="a2e05-146">Installare il modulo documentdb hello tramite npm.</span><span class="sxs-lookup"><span data-stu-id="a2e05-146">Install hello documentdb module via npm.</span></span> <span data-ttu-id="a2e05-147">Utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="a2e05-147">Use hello following command:</span></span>
   * ```npm install documentdb --save```

<span data-ttu-id="a2e05-148">L'installazione è riuscita.</span><span class="sxs-lookup"><span data-stu-id="a2e05-148">Great!</span></span> <span data-ttu-id="a2e05-149">Dopo avere completato l'installazione, è possibile iniziare a scrivere il codice.</span><span class="sxs-lookup"><span data-stu-id="a2e05-149">Now that you've finished setting up, let's start writing some code.</span></span>

## <span data-ttu-id="a2e05-150"><a id="Config"></a>Passaggio 3: Impostare le configurazioni dell'app</span><span class="sxs-lookup"><span data-stu-id="a2e05-150"><a id="Config"></a>Step 3: Set your app's configurations</span></span>
<span data-ttu-id="a2e05-151">Aprire il file ```config.js``` in un editor di testo.</span><span class="sxs-lookup"><span data-stu-id="a2e05-151">Open ```config.js``` in your favorite text editor.</span></span>

<span data-ttu-id="a2e05-152">Quindi, copia e Incolla frammento di codice hello seguente e impostare le proprietà ```config.endpoint``` e ```config.primaryKey``` tooyour Azure Cosmos DB uri di endpoint e la chiave primaria.</span><span class="sxs-lookup"><span data-stu-id="a2e05-152">Then, copy and paste hello code snippet below and set properties ```config.endpoint``` and ```config.primaryKey``` tooyour Azure Cosmos DB endpoint uri and primary key.</span></span> <span data-ttu-id="a2e05-153">Entrambe queste configurazioni sono reperibili hello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a2e05-153">Both these configurations can be found in hello [Azure portal](https://portal.azure.com).</span></span>

![Esercitazione per Node.js - cattura di schermata del portale di Azure, con un account di Azure Cosmos DB, con l'hub attivo hello hello evidenziato, pulsante CHIAVI hello evidenziata nel Pannello di account Azure Cosmos DB hello hello URI, la chiave primaria e SECONDARIA i valori ed evidenziati nella hello Pannello di chiavi - database nodo][keys]

    // ADD THIS PART tooYOUR CODE
    var config = {}

    config.endpoint = "~your Azure Cosmos DB endpoint uri here~";
    config.primaryKey = "~your primary key here~";

<span data-ttu-id="a2e05-155">Copiare e incollare hello ```database id```, ```collection id```, e ```JSON documents``` tooyour ```config``` sottostante dell'oggetto in cui vengono impostati i ```config.endpoint``` e ```config.authKey``` proprietà.</span><span class="sxs-lookup"><span data-stu-id="a2e05-155">Copy and paste hello ```database id```, ```collection id```, and ```JSON documents``` tooyour ```config``` object below where you set your ```config.endpoint``` and ```config.authKey``` properties.</span></span> <span data-ttu-id="a2e05-156">Se si dispongono già di dati desiderato toostore nel database, è possibile utilizzare Azure Cosmos DB [dello strumento di migrazione dei dati](import-data.md) invece di aggiungere le definizioni di hello document.</span><span class="sxs-lookup"><span data-stu-id="a2e05-156">If you already have data you'd like toostore in your database, you can use Azure Cosmos DB's [Data Migration tool](import-data.md) rather than adding hello document definitions.</span></span>

    config.endpoint = "~your Azure Cosmos DB endpoint uri here~";
    config.primaryKey = "~your primary key here~";

    // ADD THIS PART tooYOUR CODE
    config.database = {
        "id": "FamilyDB"
    };

    config.collection = {
        "id": "FamilyColl"
    };

    config.documents = {
        "Andersen": {
            "id": "Anderson.1",
            "lastName": "Andersen",
            "parents": [{
                "firstName": "Thomas"
            }, {
                    "firstName": "Mary Kay"
                }],
            "children": [{
                "firstName": "Henriette Thaulow",
                "gender": "female",
                "grade": 5,
                "pets": [{
                    "givenName": "Fluffy"
                }]
            }],
            "address": {
                "state": "WA",
                "county": "King",
                "city": "Seattle"
            }
        },
        "Wakefield": {
            "id": "Wakefield.7",
            "parents": [{
                "familyName": "Wakefield",
                "firstName": "Robin"
            }, {
                    "familyName": "Miller",
                    "firstName": "Ben"
                }],
            "children": [{
                "familyName": "Merriam",
                "firstName": "Jesse",
                "gender": "female",
                "grade": 8,
                "pets": [{
                    "givenName": "Goofy"
                }, {
                        "givenName": "Shadow"
                    }]
            }, {
                    "familyName": "Miller",
                    "firstName": "Lisa",
                    "gender": "female",
                    "grade": 1
                }],
            "address": {
                "state": "NY",
                "county": "Manhattan",
                "city": "NY"
            },
            "isRegistered": false
        }
    };


<span data-ttu-id="a2e05-157">Hello database raccolta e definizioni del documento, che fungerà del database di Azure Cosmos ```database id```, ```collection id```e i dati dei documenti.</span><span class="sxs-lookup"><span data-stu-id="a2e05-157">hello database, collection, and document definitions will act as your Azure Cosmos DB ```database id```, ```collection id```, and documents' data.</span></span>

<span data-ttu-id="a2e05-158">Infine, esportare il ```config``` dell'oggetto, in modo che sia possibile farvi riferimento all'interno di hello ```app.js``` file.</span><span class="sxs-lookup"><span data-stu-id="a2e05-158">Finally, export your ```config``` object, so that you can reference it within hello ```app.js``` file.</span></span>

            },
            "isRegistered": false
        }
    };

    // ADD THIS PART tooYOUR CODE
    module.exports = config;

## <span data-ttu-id="a2e05-159"><a id="Connect"></a>Passaggio 4: Connettere l'account di Azure Cosmos DB tooan</span><span class="sxs-lookup"><span data-stu-id="a2e05-159"><a id="Connect"></a> Step 4: Connect tooan Azure Cosmos DB account</span></span>
<span data-ttu-id="a2e05-160">Aprire il vuoto ```app.js``` file nell'editor di testo hello.</span><span class="sxs-lookup"><span data-stu-id="a2e05-160">Open your empty ```app.js``` file in hello text editor.</span></span> <span data-ttu-id="a2e05-161">Copiare e incollare il codice hello seguito hello tooimport ```documentdb``` modulo e appena creata ```config``` modulo.</span><span class="sxs-lookup"><span data-stu-id="a2e05-161">Copy and paste hello code below tooimport hello ```documentdb``` module and your newly created ```config``` module.</span></span>

    // ADD THIS PART tooYOUR CODE
    "use strict";

    var documentClient = require("documentdb").DocumentClient;
    var config = require("./config");
    var url = require('url');

<span data-ttu-id="a2e05-162">Copiare e incollare hello toouse di codice hello salvato in precedenza ```config.endpoint``` e ```config.primaryKey``` toocreate DocumentClient una nuova.</span><span class="sxs-lookup"><span data-stu-id="a2e05-162">Copy and paste hello code toouse hello previously saved ```config.endpoint``` and ```config.primaryKey``` toocreate a new DocumentClient.</span></span>

    var config = require("./config");
    var url = require('url');

    // ADD THIS PART tooYOUR CODE
    var client = new documentClient(config.endpoint, { "masterKey": config.primaryKey });

<span data-ttu-id="a2e05-163">Ora che si dispone di client di hello codice tooinitialize hello DB Cosmos Azure, esaminiamo un utilizzo delle risorse di Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="a2e05-163">Now that you have hello code tooinitialize hello Azure Cosmos DB client, let's take a look at working with Azure Cosmos DB resources.</span></span>

## <a name="step-5-create-a-node-database"></a><span data-ttu-id="a2e05-164">Passaggio 5: Creare un database di Node</span><span class="sxs-lookup"><span data-stu-id="a2e05-164">Step 5: Create a Node database</span></span>
<span data-ttu-id="a2e05-165">Copiare e incollare il codice hello seguito hello tooset stato HTTP per non trovato, l'url di database hello e l'url della raccolta hello.</span><span class="sxs-lookup"><span data-stu-id="a2e05-165">Copy and paste hello code below tooset hello HTTP status for Not Found, hello database url, and hello collection url.</span></span> <span data-ttu-id="a2e05-166">Questi URL sono ricerca client DB Cosmos Azure hello insieme e il database corretto hello.</span><span class="sxs-lookup"><span data-stu-id="a2e05-166">These urls are how hello Azure Cosmos DB client will find hello right database and collection.</span></span>

    var client = new documentClient(config.endpoint, { "masterKey": config.primaryKey });

    // ADD THIS PART tooYOUR CODE
    var HttpStatusCodes = { NOTFOUND: 404 };
    var databaseUrl = `dbs/${config.database.id}`;
    var collectionUrl = `${databaseUrl}/colls/${config.collection.id}`;

<span data-ttu-id="a2e05-167">Oggetto [database](documentdb-resources.md#databases) possono essere create usando hello [createDatabase](https://azure.github.io/azure-documentdb-node/DocumentClient.html) funzione di hello **DocumentClient** classe.</span><span class="sxs-lookup"><span data-stu-id="a2e05-167">A [database](documentdb-resources.md#databases) can be created by using hello [createDatabase](https://azure.github.io/azure-documentdb-node/DocumentClient.html) function of hello **DocumentClient** class.</span></span> <span data-ttu-id="a2e05-168">Un database è contenitore logico di hello di archiviazione documenti partizionato nelle raccolte.</span><span class="sxs-lookup"><span data-stu-id="a2e05-168">A database is hello logical container of document storage partitioned across collections.</span></span>

<span data-ttu-id="a2e05-169">Copiare e incollare hello **getDatabase** funzione per la creazione del nuovo database nel file app.js hello con hello ```id``` specificato in hello ```config``` oggetto.</span><span class="sxs-lookup"><span data-stu-id="a2e05-169">Copy and paste hello **getDatabase** function for creating your new database in hello app.js file with hello ```id``` specified in hello ```config``` object.</span></span> <span data-ttu-id="a2e05-170">Hello funzione controllerà se hello del database con hello stesso ```FamilyRegistry``` id esiste già.</span><span class="sxs-lookup"><span data-stu-id="a2e05-170">hello function will check if hello database with hello same ```FamilyRegistry``` id does not already exist.</span></span> <span data-ttu-id="a2e05-171">Se esiste, verrà restituito il database esistente, invece di procedere con la creazione di un nuovo database.</span><span class="sxs-lookup"><span data-stu-id="a2e05-171">If it does exist, we'll return that database instead of creating a new one.</span></span>

    var collectionUrl = `${databaseUrl}/colls/${config.collection.id}`;

    // ADD THIS PART tooYOUR CODE
    function getDatabase() {
        console.log(`Getting database:\n${config.database.id}\n`);

        return new Promise((resolve, reject) => {
            client.readDatabase(databaseUrl, (err, result) => {
                if (err) {
                    if (err.code == HttpStatusCodes.NOTFOUND) {
                        client.createDatabase(config.database, (err, created) => {
                            if (err) reject(err)
                            else resolve(created);
                        });
                    } else {
                        reject(err);
                    }
                } else {
                    resolve(result);
                }
            });
        });
    }

<span data-ttu-id="a2e05-172">Copiare e incollare codice hello riportato di seguito in cui vengono impostate hello **getDatabase** funzione funzione di supporto hello tooadd **uscire** che verrà stampato il messaggio di uscita hello e chiamata hello troppo**getDatabase** (funzione).</span><span class="sxs-lookup"><span data-stu-id="a2e05-172">Copy and paste hello code below where you set hello **getDatabase** function tooadd hello helper function **exit** that will print hello exit message and hello call too**getDatabase** function.</span></span>

                } else {
                    resolve(result);
                }
            });
        });
    }

    // ADD THIS PART tooYOUR CODE
    function exit(message) {
        console.log(message);
        console.log('Press any key tooexit');
        process.stdin.setRawMode(true);
        process.stdin.resume();
        process.stdin.on('data', process.exit.bind(process, 0));
    }

    getDatabase()
    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

<span data-ttu-id="a2e05-173">Nella finestra del terminale, individuare il ```app.js``` file ed eseguire il comando di hello:```node app.js```</span><span class="sxs-lookup"><span data-stu-id="a2e05-173">In your terminal, locate your ```app.js``` file and run hello command: ```node app.js```</span></span>

<span data-ttu-id="a2e05-174">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="a2e05-174">Congratulations!</span></span> <span data-ttu-id="a2e05-175">La creazione di un database di Azure Cosmos DB è stata completata.</span><span class="sxs-lookup"><span data-stu-id="a2e05-175">You have successfully created an Azure Cosmos DB database.</span></span>

## <span data-ttu-id="a2e05-176"><a id="CreateColl"></a>Passaggio 6: Creare una raccolta</span><span class="sxs-lookup"><span data-stu-id="a2e05-176"><a id="CreateColl"></a>Step 6: Create a collection</span></span>
> [!WARNING]
> <span data-ttu-id="a2e05-177">**CreateDocumentCollectionAsync** crea una nuova raccolta, che ha implicazioni in termini di prezzi.</span><span class="sxs-lookup"><span data-stu-id="a2e05-177">**CreateDocumentCollectionAsync** will create a new collection, which has pricing implications.</span></span> <span data-ttu-id="a2e05-178">Per altre informazioni, visitare la [pagina relativa ai prezzi](https://azure.microsoft.com/pricing/details/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="a2e05-178">For more details, please visit our [pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/).</span></span>
> 
> 

<span data-ttu-id="a2e05-179">Oggetto [raccolta](documentdb-resources.md#collections) possono essere create usando hello [createCollection](https://azure.github.io/azure-documentdb-node/DocumentClient.html) funzione di hello **DocumentClient** classe.</span><span class="sxs-lookup"><span data-stu-id="a2e05-179">A [collection](documentdb-resources.md#collections) can be created by using hello [createCollection](https://azure.github.io/azure-documentdb-node/DocumentClient.html) function of hello **DocumentClient** class.</span></span> <span data-ttu-id="a2e05-180">Una raccolta è un contenitore di documenti JSON e di logica dell'applicazione JavaScript associata.</span><span class="sxs-lookup"><span data-stu-id="a2e05-180">A collection is a container of JSON documents and associated JavaScript application logic.</span></span>

<span data-ttu-id="a2e05-181">Copiare e incollare hello **getCollection** funzione sotto hello **getDatabase** funzionare in hello app.js file toocreate la nuova raccolta con hello ```id``` specificato in hello ```config```oggetto.</span><span class="sxs-lookup"><span data-stu-id="a2e05-181">Copy and paste hello **getCollection** function underneath hello **getDatabase** function in hello app.js file toocreate your new collection with hello ```id``` specified in hello ```config``` object.</span></span> <span data-ttu-id="a2e05-182">Nuovamente, verificheremo toomake assicurarsi che una raccolta con hello stesso ```FamilyCollection``` id esiste già.</span><span class="sxs-lookup"><span data-stu-id="a2e05-182">Again, we'll check toomake sure a collection with hello same ```FamilyCollection``` id does not already exist.</span></span> <span data-ttu-id="a2e05-183">Se esiste, verrà restituita la raccolta esistente, invece di procedere con la creazione di una nuova raccolta.</span><span class="sxs-lookup"><span data-stu-id="a2e05-183">If it does exist, we'll return that collection instead of creating a new one.</span></span>

                } else {
                    resolve(result);
                }
            });
        });
    }

    // ADD THIS PART tooYOUR CODE
    function getCollection() {
        console.log(`Getting collection:\n${config.collection.id}\n`);

        return new Promise((resolve, reject) => {
            client.readCollection(collectionUrl, (err, result) => {
                if (err) {
                    if (err.code == HttpStatusCodes.NOTFOUND) {
                        client.createCollection(databaseUrl, config.collection, { offerThroughput: 400 }, (err, created) => {
                            if (err) reject(err)
                            else resolve(created);
                        });
                    } else {
                        reject(err);
                    }
                } else {
                    resolve(result);
                }
            });
        });
    }

<span data-ttu-id="a2e05-184">Copiare e incollare il codice hello sotto la chiamata hello troppo**getDatabase** tooexecute hello **getCollection** (funzione).</span><span class="sxs-lookup"><span data-stu-id="a2e05-184">Copy and paste hello code below hello call too**getDatabase** tooexecute hello **getCollection** function.</span></span>

    getDatabase()

    // ADD THIS PART tooYOUR CODE
    .then(() => getCollection())
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

<span data-ttu-id="a2e05-185">Nella finestra del terminale, individuare il ```app.js``` file ed eseguire il comando di hello:```node app.js```</span><span class="sxs-lookup"><span data-stu-id="a2e05-185">In your terminal, locate your ```app.js``` file and run hello command: ```node app.js```</span></span>

<span data-ttu-id="a2e05-186">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="a2e05-186">Congratulations!</span></span> <span data-ttu-id="a2e05-187">La creazione di una raccolta di Azure Cosmos DB è stata completata.</span><span class="sxs-lookup"><span data-stu-id="a2e05-187">You have successfully created an Azure Cosmos DB collection.</span></span>

## <span data-ttu-id="a2e05-188"><a id="CreateDoc"></a>Passaggio 7: Creare un documento</span><span class="sxs-lookup"><span data-stu-id="a2e05-188"><a id="CreateDoc"></a>Step 7: Create a document</span></span>
<span data-ttu-id="a2e05-189">Oggetto [documento](documentdb-resources.md#documents) possono essere create usando hello [createDocument](https://azure.github.io/azure-documentdb-node/DocumentClient.html) funzione di hello **DocumentClient** classe.</span><span class="sxs-lookup"><span data-stu-id="a2e05-189">A [document](documentdb-resources.md#documents) can be created by using hello [createDocument](https://azure.github.io/azure-documentdb-node/DocumentClient.html) function of hello **DocumentClient** class.</span></span> <span data-ttu-id="a2e05-190">I documenti sono contenuto JSON definito dall'utente (arbitrario).</span><span class="sxs-lookup"><span data-stu-id="a2e05-190">Documents are user defined (arbitrary) JSON content.</span></span> <span data-ttu-id="a2e05-191">È ora possibile inserire un documento in Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="a2e05-191">You can now insert a document into Azure Cosmos DB.</span></span>

<span data-ttu-id="a2e05-192">Copiare e incollare hello **getFamilyDocument** funzione sotto hello **getCollection** funzione per la creazione di documenti di hello che contengono i dati JSON hello salvati in hello ```config``` oggetto.</span><span class="sxs-lookup"><span data-stu-id="a2e05-192">Copy and paste hello **getFamilyDocument** function underneath hello **getCollection** function for creating hello documents containing hello JSON data saved in hello ```config``` object.</span></span> <span data-ttu-id="a2e05-193">Nuovamente, verificheremo toomake assicurarsi che un documento con lo stesso id esiste già hello.</span><span class="sxs-lookup"><span data-stu-id="a2e05-193">Again, we'll check toomake sure a document with hello same id does not already exist.</span></span>

                } else {
                    resolve(result);
                }
            });
        });
    }

    // ADD THIS PART tooYOUR CODE
    function getFamilyDocument(document) {
        let documentUrl = `${collectionUrl}/docs/${document.id}`;
        console.log(`Getting document:\n${document.id}\n`);

        return new Promise((resolve, reject) => {
            client.readDocument(documentUrl, { partitionKey: document.district }, (err, result) => {
                if (err) {
                    if (err.code == HttpStatusCodes.NOTFOUND) {
                        client.createDocument(collectionUrl, document, (err, created) => {
                            if (err) reject(err)
                            else resolve(created);
                        });
                    } else {
                        reject(err);
                    }
                } else {
                    resolve(result);
                }
            });
        });
    };

<span data-ttu-id="a2e05-194">Copiare e incollare il codice hello sotto la chiamata hello troppo**getCollection** tooexecute hello **getFamilyDocument** (funzione).</span><span class="sxs-lookup"><span data-stu-id="a2e05-194">Copy and paste hello code below hello call too**getCollection** tooexecute hello **getFamilyDocument** function.</span></span>

    getDatabase()
    .then(() => getCollection())

    // ADD THIS PART tooYOUR CODE
    .then(() => getFamilyDocument(config.documents.Andersen))
    .then(() => getFamilyDocument(config.documents.Wakefield))
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

<span data-ttu-id="a2e05-195">Nella finestra del terminale, individuare il ```app.js``` file ed eseguire il comando di hello:```node app.js```</span><span class="sxs-lookup"><span data-stu-id="a2e05-195">In your terminal, locate your ```app.js``` file and run hello command: ```node app.js```</span></span>

<span data-ttu-id="a2e05-196">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="a2e05-196">Congratulations!</span></span> <span data-ttu-id="a2e05-197">La creazione di un documento di Azure Cosmos DB è stata completata.</span><span class="sxs-lookup"><span data-stu-id="a2e05-197">You have successfully created an Azure Cosmos DB document.</span></span>

![Database - diagramma che illustra relazione gerarchica di hello tra account hello, database hello, raccolta hello e documenti hello - nodo esercitazione Node.js](./media/documentdb-nodejs-get-started/node-js-tutorial-cosmos-db-account.png)

## <span data-ttu-id="a2e05-199"><a id="Query"></a>Passaggio 8: Eseguire query sulle risorse di Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="a2e05-199"><a id="Query"></a>Step 8: Query Azure Cosmos DB resources</span></span>
<span data-ttu-id="a2e05-200">Azure Cosmos DB supporta [query complesse](documentdb-sql-query.md) sui documenti JSON archiviati in ogni raccolta.</span><span class="sxs-lookup"><span data-stu-id="a2e05-200">Azure Cosmos DB supports [rich queries](documentdb-sql-query.md) against JSON documents stored in each collection.</span></span> <span data-ttu-id="a2e05-201">Hello codice di esempio seguente viene illustrata una query che è possibile eseguire sui documenti hello nella raccolta.</span><span class="sxs-lookup"><span data-stu-id="a2e05-201">hello following sample code shows a query that you can run against hello documents in your collection.</span></span>

<span data-ttu-id="a2e05-202">Copiare e incollare hello **queryCollection** funzione sotto hello **getFamilyDocument** funzione nel file app.js hello.</span><span class="sxs-lookup"><span data-stu-id="a2e05-202">Copy and paste hello **queryCollection** function underneath hello **getFamilyDocument** function in hello app.js file.</span></span> <span data-ttu-id="a2e05-203">Azure Cosmos DB supporta query simili a SQL, come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="a2e05-203">Azure Cosmos DB supports SQL-like queries as shown below.</span></span> <span data-ttu-id="a2e05-204">Per ulteriori informazioni sulla compilazione di query complesse, estrarre hello [Query Playground](https://www.documentdb.com/sql/demo) hello e [query documentazione](documentdb-sql-query.md).</span><span class="sxs-lookup"><span data-stu-id="a2e05-204">For more information on building complex queries, check out hello [Query Playground](https://www.documentdb.com/sql/demo) and hello [query documentation](documentdb-sql-query.md).</span></span>

                } else {
                    resolve(result);
                }
            });
        });
    }

    // ADD THIS PART tooYOUR CODE
    function queryCollection() {
        console.log(`Querying collection through index:\n${config.collection.id}`);

        return new Promise((resolve, reject) => {
            client.queryDocuments(
                collectionUrl,
                'SELECT VALUE r.children FROM root r WHERE r.lastName = "Andersen"'
            ).toArray((err, results) => {
                if (err) reject(err)
                else {
                    for (var queryResult of results) {
                        let resultString = JSON.stringify(queryResult);
                        console.log(`\tQuery returned ${resultString}`);
                    }
                    console.log();
                    resolve(results);
                }
            });
        });
    };


<span data-ttu-id="a2e05-205">Hello seguente diagramma viene illustrato come query di database SQL di Azure Cosmos hello sintassi viene chiamata insieme hello creata.</span><span class="sxs-lookup"><span data-stu-id="a2e05-205">hello following diagram illustrates how hello Azure Cosmos DB SQL query syntax is called against hello collection you created.</span></span>

![Database - diagramma che illustra ambito hello e il significato della query hello - nodo esercitazione Node.js](./media/documentdb-nodejs-get-started/node-js-tutorial-collection-documents.png)

<span data-ttu-id="a2e05-207">Hello [FROM](documentdb-sql-query.md#FromClause) parola chiave è facoltativa in query hello perché le query di database di Azure Cosmos sono già tooa con ambito singola raccolta.</span><span class="sxs-lookup"><span data-stu-id="a2e05-207">hello [FROM](documentdb-sql-query.md#FromClause) keyword is optional in hello query because Azure Cosmos DB queries are already scoped tooa single collection.</span></span> <span data-ttu-id="a2e05-208">Di conseguenza, "FROM Families f" può essere scambiata con "FROM root r" o con il nome di qualsiasi altra variabile scelta.</span><span class="sxs-lookup"><span data-stu-id="a2e05-208">Therefore, "FROM Families f" can be swapped with "FROM root r", or any other variable name you choose.</span></span> <span data-ttu-id="a2e05-209">Azure DB Cosmos dedurrà famiglie, alla radice o il nome di variabile hello scelto, raccolta corrente hello di riferimento per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="a2e05-209">Azure Cosmos DB will infer that Families, root, or hello variable name you chose, reference hello current collection by default.</span></span>

<span data-ttu-id="a2e05-210">Copiare e incollare il codice hello sotto la chiamata hello troppo**getFamilyDocument** tooexecute hello **queryCollection** (funzione).</span><span class="sxs-lookup"><span data-stu-id="a2e05-210">Copy and paste hello code below hello call too**getFamilyDocument** tooexecute hello **queryCollection** function.</span></span>

    .then(() => getFamilyDocument(config.documents.Andersen))
    .then(() => getFamilyDocument(config.documents.Wakefield))

    // ADD THIS PART tooYOUR CODE
    .then(() => queryCollection())
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

<span data-ttu-id="a2e05-211">Nella finestra del terminale, individuare il ```app.js``` file ed eseguire il comando di hello:```node app.js```</span><span class="sxs-lookup"><span data-stu-id="a2e05-211">In your terminal, locate your ```app.js``` file and run hello command: ```node app.js```</span></span>

<span data-ttu-id="a2e05-212">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="a2e05-212">Congratulations!</span></span> <span data-ttu-id="a2e05-213">L'esecuzione di query sui documenti di Azure Cosmos DB è stata completata.</span><span class="sxs-lookup"><span data-stu-id="a2e05-213">You have successfully queried Azure Cosmos DB documents.</span></span>

## <span data-ttu-id="a2e05-214"><a id="ReplaceDocument"></a>Passaggio 9: Sostituire un documento</span><span class="sxs-lookup"><span data-stu-id="a2e05-214"><a id="ReplaceDocument"></a>Step 9: Replace a document</span></span>
<span data-ttu-id="a2e05-215">Azure Cosmos DB supporta la sostituzione di documenti JSON.</span><span class="sxs-lookup"><span data-stu-id="a2e05-215">Azure Cosmos DB supports replacing JSON documents.</span></span>

<span data-ttu-id="a2e05-216">Copiare e incollare hello **replaceFamilyDocument** funzione sotto hello **queryCollection** funzione nel file app.js hello.</span><span class="sxs-lookup"><span data-stu-id="a2e05-216">Copy and paste hello **replaceFamilyDocument** function underneath hello **queryCollection** function in hello app.js file.</span></span>

                    }
                    console.log();
                    resolve(result);
                }
            });
        });
    }

    // ADD THIS PART tooYOUR CODE
    function replaceFamilyDocument(document) {
        let documentUrl = `${collectionUrl}/docs/${document.id}`;
        console.log(`Replacing document:\n${document.id}\n`);
        document.children[0].grade = 6;

        return new Promise((resolve, reject) => {
            client.replaceDocument(documentUrl, document, (err, result) => {
                if (err) reject(err);
                else {
                    resolve(result);
                }
            });
        });
    };

<span data-ttu-id="a2e05-217">Copiare e incollare il codice hello sotto la chiamata hello troppo**queryCollection** tooexecute hello **replaceDocument** (funzione).</span><span class="sxs-lookup"><span data-stu-id="a2e05-217">Copy and paste hello code below hello call too**queryCollection** tooexecute hello **replaceDocument** function.</span></span> <span data-ttu-id="a2e05-218">Inoltre, aggiungere toocall codice hello **queryCollection** nuovamente tooverify documento hello è stata modificata.</span><span class="sxs-lookup"><span data-stu-id="a2e05-218">Also, add hello code toocall **queryCollection** again tooverify that hello document had successfully changed.</span></span>

    .then(() => getFamilyDocument(config.documents.Andersen))
    .then(() => getFamilyDocument(config.documents.Wakefield))
    .then(() => queryCollection())

    // ADD THIS PART tooYOUR CODE
    .then(() => replaceFamilyDocument(config.documents.Andersen))
    .then(() => queryCollection())
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

<span data-ttu-id="a2e05-219">Nella finestra del terminale, individuare il ```app.js``` file ed eseguire il comando di hello:```node app.js```</span><span class="sxs-lookup"><span data-stu-id="a2e05-219">In your terminal, locate your ```app.js``` file and run hello command: ```node app.js```</span></span>

<span data-ttu-id="a2e05-220">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="a2e05-220">Congratulations!</span></span> <span data-ttu-id="a2e05-221">La sostituzione di un documento di Azure Cosmos DB è stata completata.</span><span class="sxs-lookup"><span data-stu-id="a2e05-221">You have successfully replaced an Azure Cosmos DB document.</span></span>

## <span data-ttu-id="a2e05-222"><a id="DeleteDocument"></a>Passaggio 10: Eliminare un documento</span><span class="sxs-lookup"><span data-stu-id="a2e05-222"><a id="DeleteDocument"></a>Step 10: Delete a document</span></span>
<span data-ttu-id="a2e05-223">Azure Cosmos DB supporta l'eliminazione di documenti JSON.</span><span class="sxs-lookup"><span data-stu-id="a2e05-223">Azure Cosmos DB supports deleting JSON documents.</span></span>

<span data-ttu-id="a2e05-224">Copiare e incollare hello **deleteFamilyDocument** funzione sotto hello **replaceFamilyDocument** (funzione).</span><span class="sxs-lookup"><span data-stu-id="a2e05-224">Copy and paste hello **deleteFamilyDocument** function underneath hello **replaceFamilyDocument** function.</span></span>

                else {
                    resolve(result);
                }
            });
        });
    };

    // ADD THIS PART tooYOUR CODE
    function deleteFamilyDocument(document) {
        let documentUrl = `${collectionUrl}/docs/${document.id}`;
        console.log(`Deleting document:\n${document.id}\n`);

        return new Promise((resolve, reject) => {
            client.deleteDocument(documentUrl, (err, result) => {
                if (err) reject(err);
                else {
                    resolve(result);
                }
            });
        });
    };

<span data-ttu-id="a2e05-225">Copiare e incollare il codice di hello seguito hello chiamata toohello secondo **queryCollection** tooexecute hello **deleteDocument** (funzione).</span><span class="sxs-lookup"><span data-stu-id="a2e05-225">Copy and paste hello code below hello call toohello second **queryCollection** tooexecute hello **deleteDocument** function.</span></span>

    .then(() => queryCollection())
    .then(() => replaceFamilyDocument(config.documents.Andersen))
    .then(() => queryCollection())

    // ADD THIS PART tooYOUR CODE
    .then(() => deleteFamilyDocument(config.documents.Andersen))
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

<span data-ttu-id="a2e05-226">Nella finestra del terminale, individuare il ```app.js``` file ed eseguire il comando di hello:```node app.js```</span><span class="sxs-lookup"><span data-stu-id="a2e05-226">In your terminal, locate your ```app.js``` file and run hello command: ```node app.js```</span></span>

<span data-ttu-id="a2e05-227">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="a2e05-227">Congratulations!</span></span> <span data-ttu-id="a2e05-228">L'eliminazione di un documento di Azure Cosmos DB è stata completata.</span><span class="sxs-lookup"><span data-stu-id="a2e05-228">You have successfully deleted an Azure Cosmos DB document.</span></span>

## <span data-ttu-id="a2e05-229"><a id="DeleteDatabase"></a>Passaggio 11: Eliminare database nodo hello</span><span class="sxs-lookup"><span data-stu-id="a2e05-229"><a id="DeleteDatabase"></a>Step 11: Delete hello Node database</span></span>
<span data-ttu-id="a2e05-230">L'eliminazione hello creata database rimuoverà database hello e tutte le risorse di elementi figlio (raccolte, documenti e così via).</span><span class="sxs-lookup"><span data-stu-id="a2e05-230">Deleting hello created database will remove hello database and all children resources (collections, documents, etc.).</span></span>

<span data-ttu-id="a2e05-231">Copiare e incollare hello **pulizia** funzione sotto hello **deleteFamilyDocument** database hello tooremove e tutte le risorse figlio di hello di funzione.</span><span class="sxs-lookup"><span data-stu-id="a2e05-231">Copy and paste hello **cleanup** function underneath hello **deleteFamilyDocument** function tooremove hello database and all hello children resources.</span></span>

                else {
                    resolve(result);
                }
            });
        });
    };

    // ADD THIS PART tooYOUR CODE
    function cleanup() {
        console.log(`Cleaning up by deleting database ${config.database.id}`);

        return new Promise((resolve, reject) => {
            client.deleteDatabase(databaseUrl, (err) => {
                if (err) reject(err)
                else resolve(null);
            });
        });
    }

<span data-ttu-id="a2e05-232">Copiare e incollare il codice hello sotto la chiamata hello troppo**deleteFamilyDocument** tooexecute hello **pulizia** (funzione).</span><span class="sxs-lookup"><span data-stu-id="a2e05-232">Copy and paste hello code below hello call too**deleteFamilyDocument** tooexecute hello **cleanup** function.</span></span>

    .then(() => deleteFamilyDocument(config.documents.Andersen))

    // ADD THIS PART tooYOUR CODE
    .then(() => cleanup())
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

## <span data-ttu-id="a2e05-233"><a id="Run"></a>Passaggio 12: Eseguire l'applicazione Node.js</span><span class="sxs-lookup"><span data-stu-id="a2e05-233"><a id="Run"></a>Step 12: Run your Node.js application all together!</span></span>
<span data-ttu-id="a2e05-234">Sequenza hello per chiamare le funzioni inconsistenze, dovrebbe essere simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="a2e05-234">Altogether, hello sequence for calling your functions should look like this:</span></span>

    getDatabase()
    .then(() => getCollection())
    .then(() => getFamilyDocument(config.documents.Andersen))
    .then(() => getFamilyDocument(config.documents.Wakefield))
    .then(() => queryCollection())
    .then(() => replaceFamilyDocument(config.documents.Andersen))
    .then(() => queryCollection())
    .then(() => deleteFamilyDocument(config.documents.Andersen))
    .then(() => cleanup())
    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

<span data-ttu-id="a2e05-235">Nella finestra del terminale, individuare il ```app.js``` file ed eseguire il comando di hello:```node app.js```</span><span class="sxs-lookup"><span data-stu-id="a2e05-235">In your terminal, locate your ```app.js``` file and run hello command: ```node app.js```</span></span>

<span data-ttu-id="a2e05-236">Si dovrebbe vedere l'output di hello dell'app avviata get.</span><span class="sxs-lookup"><span data-stu-id="a2e05-236">You should see hello output of your get started app.</span></span> <span data-ttu-id="a2e05-237">output di Hello devono corrispondere a testo di esempio hello riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="a2e05-237">hello output should match hello example text below.</span></span>

    Getting database:
    FamilyDB

    Getting collection:
    FamilyColl

    Getting document:
    Anderson.1

    Getting document:
    Wakefield.7

    Querying collection through index:
    FamilyColl
        Query returned [{"firstName":"Henriette Thaulow","gender":"female","grade":5,"pets":[{"givenName":"Fluffy"}]}]

    Replacing document:
    Anderson.1

    Querying collection through index:
    FamilyColl
        Query returned [{"firstName":"Henriette Thaulow","gender":"female","grade":6,"pets":[{"givenName":"Fluffy"}]}]

    Deleting document:
    Anderson.1

    Cleaning up by deleting database FamilyDB
    Completed successfully
    Press any key tooexit

<span data-ttu-id="a2e05-238">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="a2e05-238">Congratulations!</span></span> <span data-ttu-id="a2e05-239">È stato creato è stata completata l'esercitazione Node.js hello e avere la prima applicazione console Azure Cosmos DB!</span><span class="sxs-lookup"><span data-stu-id="a2e05-239">You've created you've completed hello Node.js tutorial and have your first Azure Cosmos DB console application!</span></span>

## <span data-ttu-id="a2e05-240"><a id="GetSolution"></a>Ottenere hello completo Node.js soluzione di esercitazione</span><span class="sxs-lookup"><span data-stu-id="a2e05-240"><a id="GetSolution"></a>Get hello complete Node.js tutorial solution</span></span>
<span data-ttu-id="a2e05-241">Se non hai tempo toocomplete hello passaggi in questa esercitazione, oppure solo da codice hello toodownload, è possibile ottenere dalla [GitHub](https://github.com/Azure-Samples/documentdb-node-getting-started).</span><span class="sxs-lookup"><span data-stu-id="a2e05-241">If you didn't have time toocomplete hello steps in this tutorial, or just want toodownload hello code, you can get it from [GitHub](https://github.com/Azure-Samples/documentdb-node-getting-started).</span></span>

<span data-ttu-id="a2e05-242">soluzione GetStarted hello toorun che contiene tutti gli esempi di hello in questo articolo, è necessario seguente hello:</span><span class="sxs-lookup"><span data-stu-id="a2e05-242">toorun hello GetStarted solution that contains all hello samples in this article, you will need hello following:</span></span>

* <span data-ttu-id="a2e05-243">[Account Azure Cosmos DB][create-account].</span><span class="sxs-lookup"><span data-stu-id="a2e05-243">[Azure Cosmos DB account][create-account].</span></span>
* <span data-ttu-id="a2e05-244">Hello [GetStarted](https://github.com/Azure-Samples/documentdb-node-getting-started) soluzione disponibile su GitHub.</span><span class="sxs-lookup"><span data-stu-id="a2e05-244">hello [GetStarted](https://github.com/Azure-Samples/documentdb-node-getting-started) solution available on GitHub.</span></span>

<span data-ttu-id="a2e05-245">Installare hello **documentdb** modulo tramite npm.</span><span class="sxs-lookup"><span data-stu-id="a2e05-245">Install hello **documentdb** module via npm.</span></span> <span data-ttu-id="a2e05-246">Utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="a2e05-246">Use hello following command:</span></span>

* ```npm install documentdb --save```

<span data-ttu-id="a2e05-247">Successivamente, nel hello ```config.js``` file, i valori di config.endpoint e config.authKey hello aggiornamento come descritto in [passaggio 3: impostare le configurazioni dell'applicazione](#Config).</span><span class="sxs-lookup"><span data-stu-id="a2e05-247">Next, in hello ```config.js``` file, update hello config.endpoint and config.authKey values as described in [Step 3: Set your app's configurations](#Config).</span></span> 

<span data-ttu-id="a2e05-248">Quindi nella finestra del terminale, individuare il ```app.js``` file ed eseguire il comando di hello: ```node app.js```.</span><span class="sxs-lookup"><span data-stu-id="a2e05-248">Then in your terminal, locate your ```app.js``` file and run hello command: ```node app.js```.</span></span>

<span data-ttu-id="a2e05-249">Per completare la procedura, è sufficiente procedere alla compilazione.</span><span class="sxs-lookup"><span data-stu-id="a2e05-249">That's it, build it and you're on your way!</span></span> 

## <a name="next-steps"></a><span data-ttu-id="a2e05-250">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a2e05-250">Next steps</span></span>
* <span data-ttu-id="a2e05-251">Per un esempio più complesso relativo a Node.js,</span><span class="sxs-lookup"><span data-stu-id="a2e05-251">Want a more complex Node.js sample?</span></span> <span data-ttu-id="a2e05-252">Vedere [Creare un'applicazione Web Node.js con Azure Cosmos DB](documentdb-nodejs-application.md).</span><span class="sxs-lookup"><span data-stu-id="a2e05-252">See [Build a Node.js web application using Azure Cosmos DB](documentdb-nodejs-application.md).</span></span>
* <span data-ttu-id="a2e05-253">Informazioni su come troppo[monitorare un account Azure Cosmos DB](monitor-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="a2e05-253">Learn how too[monitor an Azure Cosmos DB account](monitor-accounts.md).</span></span>
* <span data-ttu-id="a2e05-254">Eseguire query su questo set di dati di esempio in hello [Query Playground](https://www.documentdb.com/sql/demo).</span><span class="sxs-lookup"><span data-stu-id="a2e05-254">Run queries against our sample dataset in hello [Query Playground](https://www.documentdb.com/sql/demo).</span></span>
* <span data-ttu-id="a2e05-255">Ulteriori informazioni sul modello di programmazione hello nella sezione sviluppo di hello hello [pagina della documentazione di Azure Cosmos DB](https://azure.microsoft.com/documentation/services/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="a2e05-255">Learn more about hello programming model in hello Develop section of hello [Azure Cosmos DB documentation page](https://azure.microsoft.com/documentation/services/documentdb/).</span></span>

[create-account]: create-documentdb-dotnet.md#create-account
[keys]: media/documentdb-nodejs-get-started/node-js-tutorial-keys.png
