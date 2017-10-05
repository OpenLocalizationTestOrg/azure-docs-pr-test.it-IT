---
title: Esercitazione su Node.js per l'API DocumentDB per Azure Cosmos DB | Microsoft Docs
description: Esercitazione su Node.js che crea un'istanza di Cosmos DB con l'API DocumentDB.
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
ms.openlocfilehash: 6510e0270bb2efa252a2b2ad40014c5d26b74a81
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="nodejs-tutorial-use-the-documentdb-api-in-azure-cosmos-db-to-create-a-nodejs-console-application"></a><span data-ttu-id="f5c03-104">Esercitazione su Node.js: usare l'API DocumentDB in Azure Cosmos DB per creare un'applicazione console Node.js</span><span class="sxs-lookup"><span data-stu-id="f5c03-104">Node.js tutorial: Use the DocumentDB API in Azure Cosmos DB to create a Node.js console application</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f5c03-105">.NET</span><span class="sxs-lookup"><span data-stu-id="f5c03-105">.NET</span></span>](documentdb-get-started.md)
> * [<span data-ttu-id="f5c03-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="f5c03-106">.NET Core</span></span>](documentdb-dotnetcore-get-started.md)
> * [<span data-ttu-id="f5c03-107">Node.js per MongoDB</span><span class="sxs-lookup"><span data-stu-id="f5c03-107">Node.js for MongoDB</span></span>](mongodb-samples.md)
> * [<span data-ttu-id="f5c03-108">Node.js</span><span class="sxs-lookup"><span data-stu-id="f5c03-108">Node.js</span></span>](documentdb-nodejs-get-started.md)
> * [<span data-ttu-id="f5c03-109">Java</span><span class="sxs-lookup"><span data-stu-id="f5c03-109">Java</span></span>](documentdb-java-get-started.md)
> * [<span data-ttu-id="f5c03-110">C++</span><span class="sxs-lookup"><span data-stu-id="f5c03-110">C++</span></span>](documentdb-cpp-get-started.md)
>  
> 

<span data-ttu-id="f5c03-111">Esercitazione su Node.js per Azure Cosmos DB Node.js SDK.</span><span class="sxs-lookup"><span data-stu-id="f5c03-111">Welcome to the Node.js tutorial for the Azure Cosmos DB Node.js SDK!</span></span> <span data-ttu-id="f5c03-112">Dopo aver seguito questa esercitazione, si otterrà un'applicazione console che consente di creare e ridefinire le query delle risorse Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="f5c03-112">After following this tutorial, you'll have a console application that creates and queries Azure Cosmos DB resources.</span></span>

<span data-ttu-id="f5c03-113">Tratteremo questo argomento:</span><span class="sxs-lookup"><span data-stu-id="f5c03-113">We'll cover:</span></span>

* <span data-ttu-id="f5c03-114">Creazione e connessione a un account Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="f5c03-114">Creating and connecting to an Azure Cosmos DB account</span></span>
* <span data-ttu-id="f5c03-115">Configurazione dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="f5c03-115">Setting up your application</span></span>
* <span data-ttu-id="f5c03-116">Creazione di un database nodo</span><span class="sxs-lookup"><span data-stu-id="f5c03-116">Creating a node database</span></span>
* <span data-ttu-id="f5c03-117">Creare una raccolta</span><span class="sxs-lookup"><span data-stu-id="f5c03-117">Creating a collection</span></span>
* <span data-ttu-id="f5c03-118">Creazione di documenti JSON</span><span class="sxs-lookup"><span data-stu-id="f5c03-118">Creating JSON documents</span></span>
* <span data-ttu-id="f5c03-119">Esecuzione di query sulla raccolta</span><span class="sxs-lookup"><span data-stu-id="f5c03-119">Querying the collection</span></span>
* <span data-ttu-id="f5c03-120">Sostituzione di un documento</span><span class="sxs-lookup"><span data-stu-id="f5c03-120">Replacing a document</span></span>
* <span data-ttu-id="f5c03-121">Eliminazione di un documento</span><span class="sxs-lookup"><span data-stu-id="f5c03-121">Deleting a document</span></span>
* <span data-ttu-id="f5c03-122">Eliminazione del database nodo</span><span class="sxs-lookup"><span data-stu-id="f5c03-122">Deleting the node database</span></span>

<span data-ttu-id="f5c03-123">Non si ha tempo?</span><span class="sxs-lookup"><span data-stu-id="f5c03-123">Don't have time?</span></span> <span data-ttu-id="f5c03-124">Nessun problema.</span><span class="sxs-lookup"><span data-stu-id="f5c03-124">Don't worry!</span></span> <span data-ttu-id="f5c03-125">La soluzione completa è disponibile in [GitHub](https://github.com/Azure-Samples/documentdb-node-getting-started).</span><span class="sxs-lookup"><span data-stu-id="f5c03-125">The complete solution is available on [GitHub](https://github.com/Azure-Samples/documentdb-node-getting-started).</span></span> <span data-ttu-id="f5c03-126">Per istruzioni rapide, vedere [ottenere la soluzione completa](#GetSolution) .</span><span class="sxs-lookup"><span data-stu-id="f5c03-126">See [Get the complete solution](#GetSolution) for quick instructions.</span></span>

<span data-ttu-id="f5c03-127">Dopo aver completato l'esercitazione su Node.js, usare i pulsanti di voto all'inizio e alla fine di questa pagina per fornire commenti e suggerimenti.</span><span class="sxs-lookup"><span data-stu-id="f5c03-127">After you've completed the Node.js tutorial, please use the voting buttons at the top and bottom of this page to give us feedback.</span></span> <span data-ttu-id="f5c03-128">Se si desidera contattarci, è possibile includere l'indirizzo di posta elettronica nel commento per il follow-up.</span><span class="sxs-lookup"><span data-stu-id="f5c03-128">If you'd like us to contact you directly, feel free to include your email address in your comments.</span></span>

<span data-ttu-id="f5c03-129">Ecco come procedere.</span><span class="sxs-lookup"><span data-stu-id="f5c03-129">Now let's get started!</span></span>

## <a name="prerequisites-for-the-nodejs-tutorial"></a><span data-ttu-id="f5c03-130">Prerequisiti per l'esercitazione su Node.js</span><span class="sxs-lookup"><span data-stu-id="f5c03-130">Prerequisites for the Node.js tutorial</span></span>
<span data-ttu-id="f5c03-131">Assicurarsi di disporre di quanto segue:</span><span class="sxs-lookup"><span data-stu-id="f5c03-131">Please make sure you have the following:</span></span>

* <span data-ttu-id="f5c03-132">Un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="f5c03-132">An active Azure account.</span></span> <span data-ttu-id="f5c03-133">Se non si ha un account, è possibile iscriversi per ottenere una [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f5c03-133">If you don't have one, you can sign up for a [Free Azure Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
    * <span data-ttu-id="f5c03-134">In alternativa, per questa esercitazione è possibile usare l'[emulatore Azure Cosmos DB](local-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="f5c03-134">Alternatively, you can use the [Azure Cosmos DB Emulator](local-emulator.md) for this tutorial.</span></span>
* <span data-ttu-id="f5c03-135">[Node.js](https://nodejs.org/) v0.10.29 o versioni successive.</span><span class="sxs-lookup"><span data-stu-id="f5c03-135">[Node.js](https://nodejs.org/) version v0.10.29 or higher.</span></span>

## <a name="step-1-create-an-azure-cosmos-db-account"></a><span data-ttu-id="f5c03-136">Passaggio 1: Creare un account di Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="f5c03-136">Step 1: Create an Azure Cosmos DB account</span></span>
<span data-ttu-id="f5c03-137">Creare prima di tutto un account Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="f5c03-137">Let's create an Azure Cosmos DB account.</span></span> <span data-ttu-id="f5c03-138">Se è già disponibile un account da usare, è possibile passare a [Configurare l'applicazione Node.js](#SetupNode).</span><span class="sxs-lookup"><span data-stu-id="f5c03-138">If you already have an account you want to use, you can skip ahead to [Set up your Node.js application](#SetupNode).</span></span> <span data-ttu-id="f5c03-139">Se si usa l'emulatore Azure Cosmos DB, seguire la procedura descritta nell'articolo [Emulatore di Azure Cosmos DB](local-emulator.md) per configurare l'emulatore e proseguire con il passaggio [Configurare l'applicazione Node.js](#SetupNode).</span><span class="sxs-lookup"><span data-stu-id="f5c03-139">If you are using the Azure Cosmos DB Emulator, please follow the steps at [Azure Cosmos DB Emulator](local-emulator.md) to setup the emulator and skip ahead to [Set up your Node.js application](#SetupNode).</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <span data-ttu-id="f5c03-140"><a id="SetupNode"></a>Passaggio 2: Configurare l'applicazione Node.js</span><span class="sxs-lookup"><span data-stu-id="f5c03-140"><a id="SetupNode"></a>Step 2: Set up your Node.js application</span></span>
1. <span data-ttu-id="f5c03-141">Aprire il terminale preferito.</span><span class="sxs-lookup"><span data-stu-id="f5c03-141">Open your favorite terminal.</span></span>
2. <span data-ttu-id="f5c03-142">Individuare la cartella o la directory in cui si vuole salvare l'applicazione Node.js.</span><span class="sxs-lookup"><span data-stu-id="f5c03-142">Locate the folder or directory where you'd like to save your Node.js application.</span></span>
3. <span data-ttu-id="f5c03-143">Creare due file JavaScript vuoti con i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="f5c03-143">Create two empty JavaScript files with the following commands:</span></span>
   * <span data-ttu-id="f5c03-144">Windows:</span><span class="sxs-lookup"><span data-stu-id="f5c03-144">Windows:</span></span>
     * ```fsutil file createnew app.js 0```
     * ```fsutil file createnew config.js 0```
   * <span data-ttu-id="f5c03-145">Linux/OS X:</span><span class="sxs-lookup"><span data-stu-id="f5c03-145">Linux/OS X:</span></span>
     * ```touch app.js```
     * ```touch config.js```
4. <span data-ttu-id="f5c03-146">Installare il modulo documentdb tramite npm.</span><span class="sxs-lookup"><span data-stu-id="f5c03-146">Install the documentdb module via npm.</span></span> <span data-ttu-id="f5c03-147">Usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="f5c03-147">Use the following command:</span></span>
   * ```npm install documentdb --save```

<span data-ttu-id="f5c03-148">L'installazione è riuscita.</span><span class="sxs-lookup"><span data-stu-id="f5c03-148">Great!</span></span> <span data-ttu-id="f5c03-149">Dopo avere completato l'installazione, è possibile iniziare a scrivere il codice.</span><span class="sxs-lookup"><span data-stu-id="f5c03-149">Now that you've finished setting up, let's start writing some code.</span></span>

## <span data-ttu-id="f5c03-150"><a id="Config"></a>Passaggio 3: Impostare le configurazioni dell'app</span><span class="sxs-lookup"><span data-stu-id="f5c03-150"><a id="Config"></a>Step 3: Set your app's configurations</span></span>
<span data-ttu-id="f5c03-151">Aprire il file ```config.js``` in un editor di testo.</span><span class="sxs-lookup"><span data-stu-id="f5c03-151">Open ```config.js``` in your favorite text editor.</span></span>

<span data-ttu-id="f5c03-152">Quindi, copiare e incollare il frammento di codice riportato di seguito e impostare le proprietà ```config.endpoint``` e ```config.primaryKey``` sull'URI dell'endpoint Azure Cosmos DB e la chiave primaria.</span><span class="sxs-lookup"><span data-stu-id="f5c03-152">Then, copy and paste the code snippet below and set properties ```config.endpoint``` and ```config.primaryKey``` to your Azure Cosmos DB endpoint uri and primary key.</span></span> <span data-ttu-id="f5c03-153">Entrambe le configurazioni sono disponibili nel [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f5c03-153">Both these configurations can be found in the [Azure portal](https://portal.azure.com).</span></span>

![Esercitazione su Node.js: screenshot del portale di Azure che mostra un account Azure Cosmos DB con l'hub ATTIVO evidenziato, il pulsante CHIAVI evidenziato nel pannello dell'account Azure Cosmos DB e i valori di URI, CHIAVE PRIMARIA e CHIAVE SECONDARIA evidenziati nel pannello Chiavi, database nodo][keys]

    // ADD THIS PART TO YOUR CODE
    var config = {}

    config.endpoint = "~your Azure Cosmos DB endpoint uri here~";
    config.primaryKey = "~your primary key here~";

<span data-ttu-id="f5c03-155">Copiare e incollare ```database id```, ```collection id``` e ```JSON documents``` nell'oggetto ```config``` seguente in cui sono impostate le proprietà ```config.endpoint``` e ```config.authKey```.</span><span class="sxs-lookup"><span data-stu-id="f5c03-155">Copy and paste the ```database id```, ```collection id```, and ```JSON documents``` to your ```config``` object below where you set your ```config.endpoint``` and ```config.authKey``` properties.</span></span> <span data-ttu-id="f5c03-156">Se sono già disponibili dati da archiviare nel database, è possibile usare lo [strumento di migrazione dati](import-data.md) di Azure Cosmos DB invece di aggiungere le definizioni dei documenti.</span><span class="sxs-lookup"><span data-stu-id="f5c03-156">If you already have data you'd like to store in your database, you can use Azure Cosmos DB's [Data Migration tool](import-data.md) rather than adding the document definitions.</span></span>

    config.endpoint = "~your Azure Cosmos DB endpoint uri here~";
    config.primaryKey = "~your primary key here~";

    // ADD THIS PART TO YOUR CODE
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


<span data-ttu-id="f5c03-157">Le definizioni del database, della raccolta e del documento verranno usate come ```database id```, ```collection id``` e dati dei documenti di Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="f5c03-157">The database, collection, and document definitions will act as your Azure Cosmos DB ```database id```, ```collection id```, and documents' data.</span></span>

<span data-ttu-id="f5c03-158">Esportare infine l'oggetto ```config``` per farvi riferimento nel file ```app.js```.</span><span class="sxs-lookup"><span data-stu-id="f5c03-158">Finally, export your ```config``` object, so that you can reference it within the ```app.js``` file.</span></span>

            },
            "isRegistered": false
        }
    };

    // ADD THIS PART TO YOUR CODE
    module.exports = config;

## <span data-ttu-id="f5c03-159"><a id="Connect"></a> Passaggio 4: Connettersi a un account Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="f5c03-159"><a id="Connect"></a> Step 4: Connect to an Azure Cosmos DB account</span></span>
<span data-ttu-id="f5c03-160">Aprire il file ```app.js``` vuoto nell'editor di testo.</span><span class="sxs-lookup"><span data-stu-id="f5c03-160">Open your empty ```app.js``` file in the text editor.</span></span> <span data-ttu-id="f5c03-161">Copiare e incollare il codice seguente per importare il modulo ```documentdb``` e il modulo ```config``` appena creato.</span><span class="sxs-lookup"><span data-stu-id="f5c03-161">Copy and paste the code below to import the ```documentdb``` module and your newly created ```config``` module.</span></span>

    // ADD THIS PART TO YOUR CODE
    "use strict";

    var documentClient = require("documentdb").DocumentClient;
    var config = require("./config");
    var url = require('url');

<span data-ttu-id="f5c03-162">Copiare e incollare il codice per usare gli oggetti ```config.endpoint``` e ```config.primaryKey``` salvati in precedenza per creare un nuovo DocumentClient.</span><span class="sxs-lookup"><span data-stu-id="f5c03-162">Copy and paste the code to use the previously saved ```config.endpoint``` and ```config.primaryKey``` to create a new DocumentClient.</span></span>

    var config = require("./config");
    var url = require('url');

    // ADD THIS PART TO YOUR CODE
    var client = new documentClient(config.endpoint, { "masterKey": config.primaryKey });

<span data-ttu-id="f5c03-163">Ora che è disponibile il codice per inizializzare il client Azure Cosmos DB, è possibile esaminare l'uso delle risorse di Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="f5c03-163">Now that you have the code to initialize the Azure Cosmos DB client, let's take a look at working with Azure Cosmos DB resources.</span></span>

## <a name="step-5-create-a-node-database"></a><span data-ttu-id="f5c03-164">Passaggio 5: Creare un database di Node</span><span class="sxs-lookup"><span data-stu-id="f5c03-164">Step 5: Create a Node database</span></span>
<span data-ttu-id="f5c03-165">Copiare e incollare il codice seguente per impostare lo stato HTTP per l'URL della raccolta, l'URL di database e Non trovato.</span><span class="sxs-lookup"><span data-stu-id="f5c03-165">Copy and paste the code below to set the HTTP status for Not Found, the database url, and the collection url.</span></span> <span data-ttu-id="f5c03-166">Tali URL definiscono il modo in cui il client Azure Cosmos DB trova il database e la raccolta corretti.</span><span class="sxs-lookup"><span data-stu-id="f5c03-166">These urls are how the Azure Cosmos DB client will find the right database and collection.</span></span>

    var client = new documentClient(config.endpoint, { "masterKey": config.primaryKey });

    // ADD THIS PART TO YOUR CODE
    var HttpStatusCodes = { NOTFOUND: 404 };
    var databaseUrl = `dbs/${config.database.id}`;
    var collectionUrl = `${databaseUrl}/colls/${config.collection.id}`;

<span data-ttu-id="f5c03-167">È possibile creare un [database](documentdb-resources.md#databases) con la funzione [createDatabase](https://azure.github.io/azure-documentdb-node/DocumentClient.html) della classe **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="f5c03-167">A [database](documentdb-resources.md#databases) can be created by using the [createDatabase](https://azure.github.io/azure-documentdb-node/DocumentClient.html) function of the **DocumentClient** class.</span></span> <span data-ttu-id="f5c03-168">Un database è un contenitore logico di archiviazione documenti partizionato nelle raccolte.</span><span class="sxs-lookup"><span data-stu-id="f5c03-168">A database is the logical container of document storage partitioned across collections.</span></span>

<span data-ttu-id="f5c03-169">Copiare e incollare la funzione **getDatabase** per la creazione del nuovo database nel file app.js con l'```id``` specificato nell'oggetto ```config```.</span><span class="sxs-lookup"><span data-stu-id="f5c03-169">Copy and paste the **getDatabase** function for creating your new database in the app.js file with the ```id``` specified in the ```config``` object.</span></span> <span data-ttu-id="f5c03-170">La funzione controlla se esiste già un database con lo stesso ID ```FamilyRegistry``` .</span><span class="sxs-lookup"><span data-stu-id="f5c03-170">The function will check if the database with the same ```FamilyRegistry``` id does not already exist.</span></span> <span data-ttu-id="f5c03-171">Se esiste, verrà restituito il database esistente, invece di procedere con la creazione di un nuovo database.</span><span class="sxs-lookup"><span data-stu-id="f5c03-171">If it does exist, we'll return that database instead of creating a new one.</span></span>

    var collectionUrl = `${databaseUrl}/colls/${config.collection.id}`;

    // ADD THIS PART TO YOUR CODE
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

<span data-ttu-id="f5c03-172">Copiare e incollare il codice seguente in cui viene impostata la funzione **getDatabase** per aggiungere la funzione di supporto **exit**, che stampa il messaggio di uscita e la chiamata alla funzione **getDatabase**.</span><span class="sxs-lookup"><span data-stu-id="f5c03-172">Copy and paste the code below where you set the **getDatabase** function to add the helper function **exit** that will print the exit message and the call to **getDatabase** function.</span></span>

                } else {
                    resolve(result);
                }
            });
        });
    }

    // ADD THIS PART TO YOUR CODE
    function exit(message) {
        console.log(message);
        console.log('Press any key to exit');
        process.stdin.setRawMode(true);
        process.stdin.resume();
        process.stdin.on('data', process.exit.bind(process, 0));
    }

    getDatabase()
    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

<span data-ttu-id="f5c03-173">Nel terminale trovare il file ```app.js``` ed eseguire il comando ```node app.js```.</span><span class="sxs-lookup"><span data-stu-id="f5c03-173">In your terminal, locate your ```app.js``` file and run the command: ```node app.js```</span></span>

<span data-ttu-id="f5c03-174">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="f5c03-174">Congratulations!</span></span> <span data-ttu-id="f5c03-175">La creazione di un database di Azure Cosmos DB è stata completata.</span><span class="sxs-lookup"><span data-stu-id="f5c03-175">You have successfully created an Azure Cosmos DB database.</span></span>

## <span data-ttu-id="f5c03-176"><a id="CreateColl"></a>Passaggio 6: Creare una raccolta</span><span class="sxs-lookup"><span data-stu-id="f5c03-176"><a id="CreateColl"></a>Step 6: Create a collection</span></span>
> [!WARNING]
> <span data-ttu-id="f5c03-177">**CreateDocumentCollectionAsync** crea una nuova raccolta, che ha implicazioni in termini di prezzi.</span><span class="sxs-lookup"><span data-stu-id="f5c03-177">**CreateDocumentCollectionAsync** will create a new collection, which has pricing implications.</span></span> <span data-ttu-id="f5c03-178">Per altre informazioni, visitare la [pagina relativa ai prezzi](https://azure.microsoft.com/pricing/details/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="f5c03-178">For more details, please visit our [pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/).</span></span>
> 
> 

<span data-ttu-id="f5c03-179">È possibile creare una [raccolta](documentdb-resources.md#collections) con la funzione [createCollection](https://azure.github.io/azure-documentdb-node/DocumentClient.html) della classe **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="f5c03-179">A [collection](documentdb-resources.md#collections) can be created by using the [createCollection](https://azure.github.io/azure-documentdb-node/DocumentClient.html) function of the **DocumentClient** class.</span></span> <span data-ttu-id="f5c03-180">Una raccolta è un contenitore di documenti JSON e di logica dell'applicazione JavaScript associata.</span><span class="sxs-lookup"><span data-stu-id="f5c03-180">A collection is a container of JSON documents and associated JavaScript application logic.</span></span>

<span data-ttu-id="f5c03-181">Copiare e incollare la funzione **getCollection** sotto la funzione **getDatabase** nel file app.js per creare la nuova raccolta con il valore ```id``` specificato nell'oggetto ```config```.</span><span class="sxs-lookup"><span data-stu-id="f5c03-181">Copy and paste the **getCollection** function underneath the **getDatabase** function in the app.js file to create your new collection with the ```id``` specified in the ```config``` object.</span></span> <span data-ttu-id="f5c03-182">Anche in questo caso è necessario assicurarsi che non esista già una raccolta con lo stesso ID ```FamilyCollection``` .</span><span class="sxs-lookup"><span data-stu-id="f5c03-182">Again, we'll check to make sure a collection with the same ```FamilyCollection``` id does not already exist.</span></span> <span data-ttu-id="f5c03-183">Se esiste, verrà restituita la raccolta esistente, invece di procedere con la creazione di una nuova raccolta.</span><span class="sxs-lookup"><span data-stu-id="f5c03-183">If it does exist, we'll return that collection instead of creating a new one.</span></span>

                } else {
                    resolve(result);
                }
            });
        });
    }

    // ADD THIS PART TO YOUR CODE
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

<span data-ttu-id="f5c03-184">Copiare e incollare il codice sotto la chiamata a **getDatabase** per eseguire la funzione **getCollection**.</span><span class="sxs-lookup"><span data-stu-id="f5c03-184">Copy and paste the code below the call to **getDatabase** to execute the **getCollection** function.</span></span>

    getDatabase()

    // ADD THIS PART TO YOUR CODE
    .then(() => getCollection())
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

<span data-ttu-id="f5c03-185">Nel terminale trovare il file ```app.js``` ed eseguire il comando ```node app.js```.</span><span class="sxs-lookup"><span data-stu-id="f5c03-185">In your terminal, locate your ```app.js``` file and run the command: ```node app.js```</span></span>

<span data-ttu-id="f5c03-186">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="f5c03-186">Congratulations!</span></span> <span data-ttu-id="f5c03-187">La creazione di una raccolta di Azure Cosmos DB è stata completata.</span><span class="sxs-lookup"><span data-stu-id="f5c03-187">You have successfully created an Azure Cosmos DB collection.</span></span>

## <span data-ttu-id="f5c03-188"><a id="CreateDoc"></a>Passaggio 7: Creare un documento</span><span class="sxs-lookup"><span data-stu-id="f5c03-188"><a id="CreateDoc"></a>Step 7: Create a document</span></span>
<span data-ttu-id="f5c03-189">È possibile creare un [documento](documentdb-resources.md#documents) con la funzione [createDocument](https://azure.github.io/azure-documentdb-node/DocumentClient.html) della classe **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="f5c03-189">A [document](documentdb-resources.md#documents) can be created by using the [createDocument](https://azure.github.io/azure-documentdb-node/DocumentClient.html) function of the **DocumentClient** class.</span></span> <span data-ttu-id="f5c03-190">I documenti sono contenuto JSON definito dall'utente (arbitrario).</span><span class="sxs-lookup"><span data-stu-id="f5c03-190">Documents are user defined (arbitrary) JSON content.</span></span> <span data-ttu-id="f5c03-191">È ora possibile inserire un documento in Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="f5c03-191">You can now insert a document into Azure Cosmos DB.</span></span>

<span data-ttu-id="f5c03-192">Copiare e incollare la funzione **getFamilyDocument** sotto la funzione **getCollection** per la creazione di documenti che contengono i dati JSON salvati nell'oggetto ```config```.</span><span class="sxs-lookup"><span data-stu-id="f5c03-192">Copy and paste the **getFamilyDocument** function underneath the **getCollection** function for creating the documents containing the JSON data saved in the ```config``` object.</span></span> <span data-ttu-id="f5c03-193">Anche in questo caso è necessario assicurarsi che non esista già un documento con lo stesso ID.</span><span class="sxs-lookup"><span data-stu-id="f5c03-193">Again, we'll check to make sure a document with the same id does not already exist.</span></span>

                } else {
                    resolve(result);
                }
            });
        });
    }

    // ADD THIS PART TO YOUR CODE
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

<span data-ttu-id="f5c03-194">Copiare e incollare il codice sotto la chiamata a **getCollection** per eseguire la funzione **getFamilyDocument**.</span><span class="sxs-lookup"><span data-stu-id="f5c03-194">Copy and paste the code below the call to **getCollection** to execute the **getFamilyDocument** function.</span></span>

    getDatabase()
    .then(() => getCollection())

    // ADD THIS PART TO YOUR CODE
    .then(() => getFamilyDocument(config.documents.Andersen))
    .then(() => getFamilyDocument(config.documents.Wakefield))
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

<span data-ttu-id="f5c03-195">Nel terminale trovare il file ```app.js``` ed eseguire il comando ```node app.js```.</span><span class="sxs-lookup"><span data-stu-id="f5c03-195">In your terminal, locate your ```app.js``` file and run the command: ```node app.js```</span></span>

<span data-ttu-id="f5c03-196">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="f5c03-196">Congratulations!</span></span> <span data-ttu-id="f5c03-197">La creazione di un documento di Azure Cosmos DB è stata completata.</span><span class="sxs-lookup"><span data-stu-id="f5c03-197">You have successfully created an Azure Cosmos DB document.</span></span>

![Esercitazione su Node.js - Diagramma che illustra la relazione gerarchica tra l'account, il database, la raccolta e i documenti - Database nodo](./media/documentdb-nodejs-get-started/node-js-tutorial-cosmos-db-account.png)

## <span data-ttu-id="f5c03-199"><a id="Query"></a>Passaggio 8: Eseguire query sulle risorse di Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="f5c03-199"><a id="Query"></a>Step 8: Query Azure Cosmos DB resources</span></span>
<span data-ttu-id="f5c03-200">Azure Cosmos DB supporta [query complesse](documentdb-sql-query.md) sui documenti JSON archiviati in ogni raccolta.</span><span class="sxs-lookup"><span data-stu-id="f5c03-200">Azure Cosmos DB supports [rich queries](documentdb-sql-query.md) against JSON documents stored in each collection.</span></span> <span data-ttu-id="f5c03-201">L'esempio di codice seguente illustra una query eseguibile nei documenti della raccolta.</span><span class="sxs-lookup"><span data-stu-id="f5c03-201">The following sample code shows a query that you can run against the documents in your collection.</span></span>

<span data-ttu-id="f5c03-202">Copiare e incollare la funzione **queryCollection** sotto la funzione **getFamilyDocument** nel file app.js.</span><span class="sxs-lookup"><span data-stu-id="f5c03-202">Copy and paste the **queryCollection** function underneath the **getFamilyDocument** function in the app.js file.</span></span> <span data-ttu-id="f5c03-203">Azure Cosmos DB supporta query simili a SQL, come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="f5c03-203">Azure Cosmos DB supports SQL-like queries as shown below.</span></span> <span data-ttu-id="f5c03-204">Per altre informazioni sulla creazione di query complesse, vedere la pagina [Query Playground](https://www.documentdb.com/sql/demo) e la [documentazione sulle query](documentdb-sql-query.md).</span><span class="sxs-lookup"><span data-stu-id="f5c03-204">For more information on building complex queries, check out the [Query Playground](https://www.documentdb.com/sql/demo) and the [query documentation](documentdb-sql-query.md).</span></span>

                } else {
                    resolve(result);
                }
            });
        });
    }

    // ADD THIS PART TO YOUR CODE
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


<span data-ttu-id="f5c03-205">Il diagramma seguente illustra il modo in cui la sintassi di query SQL di Azure Cosmos DB viene chiamata nella raccolta creata.</span><span class="sxs-lookup"><span data-stu-id="f5c03-205">The following diagram illustrates how the Azure Cosmos DB SQL query syntax is called against the collection you created.</span></span>

![Esercitazione su Node.js - Diagramma che illustra l'ambito e il significato della query - Database nodo](./media/documentdb-nodejs-get-started/node-js-tutorial-collection-documents.png)

<span data-ttu-id="f5c03-207">La parola chiave [FROM](documentdb-sql-query.md#FromClause) è facoltativa nella query perché le query di Azure Cosmos DB sono già limitate a una singola raccolta.</span><span class="sxs-lookup"><span data-stu-id="f5c03-207">The [FROM](documentdb-sql-query.md#FromClause) keyword is optional in the query because Azure Cosmos DB queries are already scoped to a single collection.</span></span> <span data-ttu-id="f5c03-208">Di conseguenza, "FROM Families f" può essere scambiata con "FROM root r" o con il nome di qualsiasi altra variabile scelta.</span><span class="sxs-lookup"><span data-stu-id="f5c03-208">Therefore, "FROM Families f" can be swapped with "FROM root r", or any other variable name you choose.</span></span> <span data-ttu-id="f5c03-209">Azure Cosmos DB dedurrà che Families, root o il nome della variabile scelta, si riferisce per impostazione predefinita alla raccolta attuale.</span><span class="sxs-lookup"><span data-stu-id="f5c03-209">Azure Cosmos DB will infer that Families, root, or the variable name you chose, reference the current collection by default.</span></span>

<span data-ttu-id="f5c03-210">Copiare e incollare il codice sotto la chiamata a **getFamilyDocument** per eseguire la funzione **queryCollection**.</span><span class="sxs-lookup"><span data-stu-id="f5c03-210">Copy and paste the code below the call to **getFamilyDocument** to execute the **queryCollection** function.</span></span>

    .then(() => getFamilyDocument(config.documents.Andersen))
    .then(() => getFamilyDocument(config.documents.Wakefield))

    // ADD THIS PART TO YOUR CODE
    .then(() => queryCollection())
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

<span data-ttu-id="f5c03-211">Nel terminale trovare il file ```app.js``` ed eseguire il comando ```node app.js```.</span><span class="sxs-lookup"><span data-stu-id="f5c03-211">In your terminal, locate your ```app.js``` file and run the command: ```node app.js```</span></span>

<span data-ttu-id="f5c03-212">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="f5c03-212">Congratulations!</span></span> <span data-ttu-id="f5c03-213">L'esecuzione di query sui documenti di Azure Cosmos DB è stata completata.</span><span class="sxs-lookup"><span data-stu-id="f5c03-213">You have successfully queried Azure Cosmos DB documents.</span></span>

## <span data-ttu-id="f5c03-214"><a id="ReplaceDocument"></a>Passaggio 9: Sostituire un documento</span><span class="sxs-lookup"><span data-stu-id="f5c03-214"><a id="ReplaceDocument"></a>Step 9: Replace a document</span></span>
<span data-ttu-id="f5c03-215">Azure Cosmos DB supporta la sostituzione di documenti JSON.</span><span class="sxs-lookup"><span data-stu-id="f5c03-215">Azure Cosmos DB supports replacing JSON documents.</span></span>

<span data-ttu-id="f5c03-216">Copiare e incollare la funzione **replaceFamilyDocument** sotto la funzione **queryCollection** nel file app.js.</span><span class="sxs-lookup"><span data-stu-id="f5c03-216">Copy and paste the **replaceFamilyDocument** function underneath the **queryCollection** function in the app.js file.</span></span>

                    }
                    console.log();
                    resolve(result);
                }
            });
        });
    }

    // ADD THIS PART TO YOUR CODE
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

<span data-ttu-id="f5c03-217">Copiare e incollare il codice sotto la chiamata a **queryCollection** per eseguire la funzione **replaceDocument**.</span><span class="sxs-lookup"><span data-stu-id="f5c03-217">Copy and paste the code below the call to **queryCollection** to execute the **replaceDocument** function.</span></span> <span data-ttu-id="f5c03-218">Aggiungere anche il codice per chiamare nuovamente **queryCollection** e verificare che il documento sia stato modificato correttamente.</span><span class="sxs-lookup"><span data-stu-id="f5c03-218">Also, add the code to call **queryCollection** again to verify that the document had successfully changed.</span></span>

    .then(() => getFamilyDocument(config.documents.Andersen))
    .then(() => getFamilyDocument(config.documents.Wakefield))
    .then(() => queryCollection())

    // ADD THIS PART TO YOUR CODE
    .then(() => replaceFamilyDocument(config.documents.Andersen))
    .then(() => queryCollection())
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

<span data-ttu-id="f5c03-219">Nel terminale trovare il file ```app.js``` ed eseguire il comando ```node app.js```.</span><span class="sxs-lookup"><span data-stu-id="f5c03-219">In your terminal, locate your ```app.js``` file and run the command: ```node app.js```</span></span>

<span data-ttu-id="f5c03-220">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="f5c03-220">Congratulations!</span></span> <span data-ttu-id="f5c03-221">La sostituzione di un documento di Azure Cosmos DB è stata completata.</span><span class="sxs-lookup"><span data-stu-id="f5c03-221">You have successfully replaced an Azure Cosmos DB document.</span></span>

## <span data-ttu-id="f5c03-222"><a id="DeleteDocument"></a>Passaggio 10: Eliminare un documento</span><span class="sxs-lookup"><span data-stu-id="f5c03-222"><a id="DeleteDocument"></a>Step 10: Delete a document</span></span>
<span data-ttu-id="f5c03-223">Azure Cosmos DB supporta l'eliminazione di documenti JSON.</span><span class="sxs-lookup"><span data-stu-id="f5c03-223">Azure Cosmos DB supports deleting JSON documents.</span></span>

<span data-ttu-id="f5c03-224">Copiare e incollare la funzione **deleteFamilyDocument** sotto la funzione **replaceFamilyDocument**.</span><span class="sxs-lookup"><span data-stu-id="f5c03-224">Copy and paste the **deleteFamilyDocument** function underneath the **replaceFamilyDocument** function.</span></span>

                else {
                    resolve(result);
                }
            });
        });
    };

    // ADD THIS PART TO YOUR CODE
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

<span data-ttu-id="f5c03-225">Copiare e incollare il codice sotto la chiamata alla seconda funzione **queryCollection** per eseguire la funzione **deleteDocument**.</span><span class="sxs-lookup"><span data-stu-id="f5c03-225">Copy and paste the code below the call to the second **queryCollection** to execute the **deleteDocument** function.</span></span>

    .then(() => queryCollection())
    .then(() => replaceFamilyDocument(config.documents.Andersen))
    .then(() => queryCollection())

    // ADD THIS PART TO YOUR CODE
    .then(() => deleteFamilyDocument(config.documents.Andersen))
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

<span data-ttu-id="f5c03-226">Nel terminale trovare il file ```app.js``` ed eseguire il comando ```node app.js```.</span><span class="sxs-lookup"><span data-stu-id="f5c03-226">In your terminal, locate your ```app.js``` file and run the command: ```node app.js```</span></span>

<span data-ttu-id="f5c03-227">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="f5c03-227">Congratulations!</span></span> <span data-ttu-id="f5c03-228">L'eliminazione di un documento di Azure Cosmos DB è stata completata.</span><span class="sxs-lookup"><span data-stu-id="f5c03-228">You have successfully deleted an Azure Cosmos DB document.</span></span>

## <span data-ttu-id="f5c03-229"><a id="DeleteDatabase"></a>Passaggio 11: Eliminare il database Node</span><span class="sxs-lookup"><span data-stu-id="f5c03-229"><a id="DeleteDatabase"></a>Step 11: Delete the Node database</span></span>
<span data-ttu-id="f5c03-230">Se si elimina il database creato, verrà rimosso il database e tutte le risorse figlio (raccolte, documenti e così via).</span><span class="sxs-lookup"><span data-stu-id="f5c03-230">Deleting the created database will remove the database and all children resources (collections, documents, etc.).</span></span>

<span data-ttu-id="f5c03-231">Copiare e incollare la funzione **cleanup** sotto la funzione **deleteFamilyDocument** per rimuovere il database e tutte le risorse figlio.</span><span class="sxs-lookup"><span data-stu-id="f5c03-231">Copy and paste the **cleanup** function underneath the **deleteFamilyDocument** function to remove the database and all the children resources.</span></span>

                else {
                    resolve(result);
                }
            });
        });
    };

    // ADD THIS PART TO YOUR CODE
    function cleanup() {
        console.log(`Cleaning up by deleting database ${config.database.id}`);

        return new Promise((resolve, reject) => {
            client.deleteDatabase(databaseUrl, (err) => {
                if (err) reject(err)
                else resolve(null);
            });
        });
    }

<span data-ttu-id="f5c03-232">Copiare e incollare il codice sotto la chiamata a **deleteFamilyDocument** per eseguire la funzione **cleanup**.</span><span class="sxs-lookup"><span data-stu-id="f5c03-232">Copy and paste the code below the call to **deleteFamilyDocument** to execute the **cleanup** function.</span></span>

    .then(() => deleteFamilyDocument(config.documents.Andersen))

    // ADD THIS PART TO YOUR CODE
    .then(() => cleanup())
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

## <span data-ttu-id="f5c03-233"><a id="Run"></a>Passaggio 12: Eseguire l'applicazione Node.js</span><span class="sxs-lookup"><span data-stu-id="f5c03-233"><a id="Run"></a>Step 12: Run your Node.js application all together!</span></span>
<span data-ttu-id="f5c03-234">In generale, la sequenza per chiamare le funzioni dovrebbe avere un aspetto simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="f5c03-234">Altogether, the sequence for calling your functions should look like this:</span></span>

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

<span data-ttu-id="f5c03-235">Nel terminale trovare il file ```app.js``` ed eseguire il comando ```node app.js```.</span><span class="sxs-lookup"><span data-stu-id="f5c03-235">In your terminal, locate your ```app.js``` file and run the command: ```node app.js```</span></span>

<span data-ttu-id="f5c03-236">Verrà visualizzato l'output dell'app introduttiva.</span><span class="sxs-lookup"><span data-stu-id="f5c03-236">You should see the output of your get started app.</span></span> <span data-ttu-id="f5c03-237">L'output dovrebbe essere analogo al testo di esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="f5c03-237">The output should match the example text below.</span></span>

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
    Press any key to exit

<span data-ttu-id="f5c03-238">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="f5c03-238">Congratulations!</span></span> <span data-ttu-id="f5c03-239">È stata completata l'esercitazione su Node.js ed stata creata la prima applicazione console di Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="f5c03-239">You've created you've completed the Node.js tutorial and have your first Azure Cosmos DB console application!</span></span>

## <span data-ttu-id="f5c03-240"><a id="GetSolution"></a>Ottenere la soluzione completa per l'esercitazione su Node.js</span><span class="sxs-lookup"><span data-stu-id="f5c03-240"><a id="GetSolution"></a>Get the complete Node.js tutorial solution</span></span>
<span data-ttu-id="f5c03-241">Se non si ha tempo per completare le procedure dell'esercitazione o se si vogliono solo scaricare gli esempi di codice, è possibile ottenerli da [GitHub](https://github.com/Azure-Samples/documentdb-node-getting-started).</span><span class="sxs-lookup"><span data-stu-id="f5c03-241">If you didn't have time to complete the steps in this tutorial, or just want to download the code, you can get it from [GitHub](https://github.com/Azure-Samples/documentdb-node-getting-started).</span></span>

<span data-ttu-id="f5c03-242">Per eseguire la soluzione GetStarted completa contenente tutti gli esempi riportati in questo articolo, è necessario avere:</span><span class="sxs-lookup"><span data-stu-id="f5c03-242">To run the GetStarted solution that contains all the samples in this article, you will need the following:</span></span>

* <span data-ttu-id="f5c03-243">[Account Azure Cosmos DB][create-account].</span><span class="sxs-lookup"><span data-stu-id="f5c03-243">[Azure Cosmos DB account][create-account].</span></span>
* <span data-ttu-id="f5c03-244">La soluzione [GetStarted](https://github.com/Azure-Samples/documentdb-node-getting-started) disponibile su GitHub.</span><span class="sxs-lookup"><span data-stu-id="f5c03-244">The [GetStarted](https://github.com/Azure-Samples/documentdb-node-getting-started) solution available on GitHub.</span></span>

<span data-ttu-id="f5c03-245">Installare il modulo **documentdb** tramite npm.</span><span class="sxs-lookup"><span data-stu-id="f5c03-245">Install the **documentdb** module via npm.</span></span> <span data-ttu-id="f5c03-246">Usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="f5c03-246">Use the following command:</span></span>

* ```npm install documentdb --save```

<span data-ttu-id="f5c03-247">Nel file ```config.js``` aggiornare quindi i valori config.endpoint e config.authKey, come illustrato nel [Passaggio 3: Impostare le configurazioni dell'app](#Config).</span><span class="sxs-lookup"><span data-stu-id="f5c03-247">Next, in the ```config.js``` file, update the config.endpoint and config.authKey values as described in [Step 3: Set your app's configurations](#Config).</span></span> 

<span data-ttu-id="f5c03-248">Nel terminale trovare quindi il file ```app.js``` ed eseguire il comando: ```node app.js```.</span><span class="sxs-lookup"><span data-stu-id="f5c03-248">Then in your terminal, locate your ```app.js``` file and run the command: ```node app.js```.</span></span>

<span data-ttu-id="f5c03-249">Per completare la procedura, è sufficiente procedere alla compilazione.</span><span class="sxs-lookup"><span data-stu-id="f5c03-249">That's it, build it and you're on your way!</span></span> 

## <a name="next-steps"></a><span data-ttu-id="f5c03-250">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f5c03-250">Next steps</span></span>
* <span data-ttu-id="f5c03-251">Per un esempio più complesso relativo a Node.js,</span><span class="sxs-lookup"><span data-stu-id="f5c03-251">Want a more complex Node.js sample?</span></span> <span data-ttu-id="f5c03-252">Vedere [Creare un'applicazione Web Node.js con Azure Cosmos DB](documentdb-nodejs-application.md).</span><span class="sxs-lookup"><span data-stu-id="f5c03-252">See [Build a Node.js web application using Azure Cosmos DB](documentdb-nodejs-application.md).</span></span>
* <span data-ttu-id="f5c03-253">Informazioni su come [monitorare un account Azure Cosmos DB](monitor-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="f5c03-253">Learn how to [monitor an Azure Cosmos DB account](monitor-accounts.md).</span></span>
* <span data-ttu-id="f5c03-254">Eseguire query sul set di dati di esempio illustrato nella pagina [Query Playground](https://www.documentdb.com/sql/demo).</span><span class="sxs-lookup"><span data-stu-id="f5c03-254">Run queries against our sample dataset in the [Query Playground](https://www.documentdb.com/sql/demo).</span></span>
* <span data-ttu-id="f5c03-255">Per altre informazioni sul modello di programmazione, vedere la sezione relativa allo sviluppo nella pagina [Documentazione di Azure Cosmos DB](https://azure.microsoft.com/documentation/services/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="f5c03-255">Learn more about the programming model in the Develop section of the [Azure Cosmos DB documentation page](https://azure.microsoft.com/documentation/services/documentdb/).</span></span>

[create-account]: create-documentdb-dotnet.md#create-account
[keys]: media/documentdb-nodejs-get-started/node-js-tutorial-keys.png
