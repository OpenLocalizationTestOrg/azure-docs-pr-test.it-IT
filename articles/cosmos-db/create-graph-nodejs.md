---
title: Creare un'applicazione Node.js Azure Cosmos DB tramite l'API Graph | Microsoft Docs
description: Presenta un esempio di codice Node.js che permette di connettersi ad Azure Cosmos DB ed eseguire query sul servizio
services: cosmos-db
documentationcenter: 
author: dennyglee
manager: jhubbard
editor: 
ms.assetid: daacbabf-1bb5-497f-92db-079910703046
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 07/14/2017
ms.author: denlee
ms.openlocfilehash: 6d14719938af0ce825955389824441e111024869
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="azure-cosmos-db-build-a-nodejs-application-by-using-graph-api"></a><span data-ttu-id="5d414-103">Azure Cosmos DB: Creare un'applicazione Node.js tramite l'API Graph</span><span class="sxs-lookup"><span data-stu-id="5d414-103">Azure Cosmos DB: Build a Node.js application by using Graph API</span></span>

<span data-ttu-id="5d414-104">Azure Cosmos DB è il servizio di database multimodello distribuito a livello globale di Microsoft.</span><span class="sxs-lookup"><span data-stu-id="5d414-104">Azure Cosmos DB is the globally distributed multi-model database service from Microsoft.</span></span> <span data-ttu-id="5d414-105">È possibile creare ed eseguire rapidamente query su database di documenti, coppie chiave/valore e grafi, sfruttando in ognuno dei casi i vantaggi offerti dalle funzionalità di scalabilità orizzontale e distribuzione globale alla base di Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="5d414-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="5d414-106">Questa guida introduttiva mostra come creare un account Azure Cosmos DB per l'API Graph (anteprima), un database e un grafo tramite il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="5d414-106">This quick-start article demonstrates how to create an Azure Cosmos DB account for Graph API (preview), database, and graph by using the Azure portal.</span></span> <span data-ttu-id="5d414-107">Si creerà ed eseguirà quindi un'app console usando il driver open source [Gremlin Node.js](https://www.npmjs.com/package/gremlin-secure).</span><span class="sxs-lookup"><span data-stu-id="5d414-107">You then build and run a console app by using the open-source [Gremlin Node.js](https://www.npmjs.com/package/gremlin-secure) driver.</span></span>  

> [!NOTE]
> <span data-ttu-id="5d414-108">Il modulo npm `gremlin-secure` è una versione modificata del modulo `gremlin`, con il supporto per SSL e SASL necessario per la connessione con Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="5d414-108">The npm module `gremlin-secure` is a modified version of `gremlin` module, with support for SSL and SASL required for connecting with Azure Cosmos DB.</span></span> <span data-ttu-id="5d414-109">Il codice sorgente è disponibile su [Github](https://github.com/CosmosDB/gremlin-javascript).</span><span class="sxs-lookup"><span data-stu-id="5d414-109">Source code is available on [GitHub](https://github.com/CosmosDB/gremlin-javascript).</span></span>
>

## <a name="prerequisites"></a><span data-ttu-id="5d414-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="5d414-110">Prerequisites</span></span>

<span data-ttu-id="5d414-111">Prima di poter eseguire questo esempio, è necessario soddisfare i prerequisiti seguenti:</span><span class="sxs-lookup"><span data-stu-id="5d414-111">Before you can run this sample, you must have the following prerequisites:</span></span>
* <span data-ttu-id="5d414-112">[Node.js](https://nodejs.org/en/) versione v0.10.29 o versioni successive</span><span class="sxs-lookup"><span data-stu-id="5d414-112">[Node.js](https://nodejs.org/en/) version v0.10.29 or later</span></span>
* [<span data-ttu-id="5d414-113">Git</span><span class="sxs-lookup"><span data-stu-id="5d414-113">Git</span></span>](http://git-scm.com/)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="5d414-114">Creare un account di database</span><span class="sxs-lookup"><span data-stu-id="5d414-114">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount-graph](../../includes/cosmos-db-create-dbaccount-graph.md)]

## <a name="add-a-graph"></a><span data-ttu-id="5d414-115">Aggiungere un grafo</span><span class="sxs-lookup"><span data-stu-id="5d414-115">Add a graph</span></span>

[!INCLUDE [cosmos-db-create-graph](../../includes/cosmos-db-create-graph.md)]

## <a name="clone-the-sample-application"></a><span data-ttu-id="5d414-116">Clonare l'applicazione di esempio</span><span class="sxs-lookup"><span data-stu-id="5d414-116">Clone the sample application</span></span>

<span data-ttu-id="5d414-117">Clonare ora un'app per le API Graph da GitHub, impostare la stringa di connessione ed eseguirla.</span><span class="sxs-lookup"><span data-stu-id="5d414-117">Now let's clone a Graph API app from GitHub, set the connection string, and run it.</span></span> <span data-ttu-id="5d414-118">Come si noterà, è facile usare i dati a livello di codice.</span><span class="sxs-lookup"><span data-stu-id="5d414-118">You'll see how easy it is to work with data programmatically.</span></span> 

1. <span data-ttu-id="5d414-119">Aprire una finestra del terminale Git, ad esempio Git Bash, e usare il comando `cd` per passare a una directory di lavoro.</span><span class="sxs-lookup"><span data-stu-id="5d414-119">Open a Git terminal window, such as Git Bash, and change (via `cd` command) to a working directory.</span></span>  

2. <span data-ttu-id="5d414-120">Eseguire il comando seguente per clonare l'archivio di esempio.</span><span class="sxs-lookup"><span data-stu-id="5d414-120">Run the following command to clone the sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-graph-nodejs-getting-started.git
    ```

3. <span data-ttu-id="5d414-121">Aprire il file della soluzione in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5d414-121">Open the solution file in Visual Studio.</span></span> 

## <a name="review-the-code"></a><span data-ttu-id="5d414-122">Esaminare il codice</span><span class="sxs-lookup"><span data-stu-id="5d414-122">Review the code</span></span>

<span data-ttu-id="5d414-123">Ecco una breve analisi di ciò che accade nell'app.</span><span class="sxs-lookup"><span data-stu-id="5d414-123">Let's make a quick review of what's happening in the app.</span></span> <span data-ttu-id="5d414-124">Aprire il file `app.js`. Si vedranno le righe di codice seguenti.</span><span class="sxs-lookup"><span data-stu-id="5d414-124">Open the `app.js` file, and you'll find the following lines of code.</span></span> 

* <span data-ttu-id="5d414-125">Viene creato il client di Gremlin.</span><span class="sxs-lookup"><span data-stu-id="5d414-125">The Gremlin client is created.</span></span>

    ```nodejs
    const client = Gremlin.createClient(
        443, 
        config.endpoint, 
        { 
            "session": false, 
            "ssl": true, 
            "user": `/dbs/${config.database}/colls/${config.collection}`,
            "password": config.primaryKey
        });
    ```

  <span data-ttu-id="5d414-126">Le configurazioni sono tutte incluse in `config.js`, che verrà modificato nella sezione seguente.</span><span class="sxs-lookup"><span data-stu-id="5d414-126">The configurations are all in `config.js`, which we edit in the following section.</span></span>

* <span data-ttu-id="5d414-127">Viene eseguita una serie di passaggi di Gremlin con il metodo `client.execute`.</span><span class="sxs-lookup"><span data-stu-id="5d414-127">A series of Gremlin steps are executed with the `client.execute` method.</span></span>

    ```nodejs
    console.log('Running Count'); 
    client.execute("g.V().count()", { }, (err, results) => {
        if (err) return console.error(err);
        console.log(JSON.stringify(results));
        console.log();
    });
    ```

## <a name="update-your-connection-string"></a><span data-ttu-id="5d414-128">Aggiornare la stringa di connessione</span><span class="sxs-lookup"><span data-stu-id="5d414-128">Update your connection string</span></span>

1. <span data-ttu-id="5d414-129">Aprire il file config.js.</span><span class="sxs-lookup"><span data-stu-id="5d414-129">Open the config.js file.</span></span> 

2. <span data-ttu-id="5d414-130">In config.js compilare la chiave config.endpoint con il valore **URI Gremlin** disponibile nella pagina **Panoramica** del portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="5d414-130">In config.js, fill in the config.endpoint key with the **Gremlin URI** value from the **Overview** page of the Azure portal.</span></span> 

    `config.endpoint = "GRAPHENDPOINT";`

    ![Visualizzazione e copia di una chiave di accesso nel portale di Azure, pannello Chiavi](./media/create-graph-nodejs/gremlin-uri.png)

   <span data-ttu-id="5d414-132">Se il valore **URI Gremlin** è vuoto, è possibile generare il valore dalla pagina **Chiavi** del portale, usando il valore **URI**, rimuovendo https:// e sostituendo documents con graphs.</span><span class="sxs-lookup"><span data-stu-id="5d414-132">If the **Gremlin URI** value is blank, you can generate the value from the **Keys** page in the portal, using the **URI** value, removing https://, and changing documents to graphs.</span></span>

   <span data-ttu-id="5d414-133">L'endpoint Gremlin deve essere solo il nome host senza protocollo/numero di porta, ad esempio `mygraphdb.graphs.azure.com` (non `https://mygraphdb.graphs.azure.com` o `mygraphdb.graphs.azure.com:433`).</span><span class="sxs-lookup"><span data-stu-id="5d414-133">The Gremlin endpoint must be only the host name without the protocol/port number, like `mygraphdb.graphs.azure.com` (not `https://mygraphdb.graphs.azure.com` or `mygraphdb.graphs.azure.com:433`).</span></span>

3. <span data-ttu-id="5d414-134">In config.js compilare il valore di config.primaryKey con il valore **Chiave primaria** disponibile nella pagina **Chiavi** del portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="5d414-134">In config.js, fill in the config.primaryKey value in with the **Primary Key** value from the **Keys** page of the Azure portal.</span></span> 

    `config.primaryKey = "PRIMARYKEY";`

   ![Pannello Chiavi del portale di Azure](./media/create-graph-nodejs/keys.png)

4. <span data-ttu-id="5d414-136">Immettere il nome del database e il nome del grafo (contenitore) per il valore di config.database e config.collection.</span><span class="sxs-lookup"><span data-stu-id="5d414-136">Enter the database name, and graph (container) name for the value of config.database and config.collection.</span></span> 

<span data-ttu-id="5d414-137">Ecco un esempio dell'aspetto che dovrebbe avere il file config.js completato:</span><span class="sxs-lookup"><span data-stu-id="5d414-137">Here is an example of what your completed config.js file should look like:</span></span>

```nodejs
var config = {}

// Note that this must not have HTTPS or the port number
config.endpoint = "testgraphacct.graphs.azure.com";
config.primaryKey = "Pams6e7LEUS7LJ2Qk0fjZf3eGo65JdMWHmyn65i52w8ozPX2oxY3iP0yu05t9v1WymAHNcMwPIqNAEv3XDFsEg==";
config.database = "graphdb"
config.collection = "Persons"

module.exports = config;
```

## <a name="run-the-console-app"></a><span data-ttu-id="5d414-138">Eseguire l'app console</span><span class="sxs-lookup"><span data-stu-id="5d414-138">Run the console app</span></span>

1. <span data-ttu-id="5d414-139">Aprire una finestra del terminale e usare il comando `cd` per passare alla directory di installazione del file package.json incluso nel progetto.</span><span class="sxs-lookup"><span data-stu-id="5d414-139">Open a terminal window and change (via `cd` command) to the installation directory for the package.json file that's included in the project.</span></span>  

2. <span data-ttu-id="5d414-140">Eseguire `npm install` per installare i moduli npm necessari, tra cui `gremlin-secure`.</span><span class="sxs-lookup"><span data-stu-id="5d414-140">Run `npm install` to install the required npm modules, including `gremlin-secure`.</span></span>

3. <span data-ttu-id="5d414-141">Eseguire `node app.js` in un terminale per avviare l'applicazione Node.js.</span><span class="sxs-lookup"><span data-stu-id="5d414-141">Run `node app.js` in a terminal to start your node application.</span></span>

## <a name="browse-with-data-explorer"></a><span data-ttu-id="5d414-142">Esplorare con Esplora dati</span><span class="sxs-lookup"><span data-stu-id="5d414-142">Browse with Data Explorer</span></span>

<span data-ttu-id="5d414-143">È ora possibile tornare a Esplora dati nel portale di Azure per visualizzare, modificare e usare i nuovi dati del grafo ed eseguire query su di essi.</span><span class="sxs-lookup"><span data-stu-id="5d414-143">You can now go back to Data Explorer in the Azure portal to view, query, modify, and work with your new graph data.</span></span>

<span data-ttu-id="5d414-144">In Esplora dati il nuovo database viene visualizzato nel riquadro **Graph**.</span><span class="sxs-lookup"><span data-stu-id="5d414-144">In Data Explorer, the new database appears in the **Graphs** pane.</span></span> <span data-ttu-id="5d414-145">Espandere il database e la raccolta, quindi fare clic su **Grafico**.</span><span class="sxs-lookup"><span data-stu-id="5d414-145">Expand the database, followed by the collection, then click **Graph**.</span></span>

<span data-ttu-id="5d414-146">I dati generati dall'app di esempio vengono visualizzati nel riquadro successivo nella scheda **Grafico** quando si fa clic su **Applica filtro**.</span><span class="sxs-lookup"><span data-stu-id="5d414-146">The data generated by the sample app is displayed in the next pane within the **Graph** tab when you click **Apply Filter**.</span></span>

<span data-ttu-id="5d414-147">Provare a completare `g.V()` con `.has('firstName', 'Thomas')` per testare il filtro.</span><span class="sxs-lookup"><span data-stu-id="5d414-147">Try completing `g.V()` with `.has('firstName', 'Thomas')` to test the filter.</span></span> <span data-ttu-id="5d414-148">Si noti che il valore distingue tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="5d414-148">Do note that the value is case sensitive.</span></span>

## <a name="review-slas-in-the-azure-portal"></a><span data-ttu-id="5d414-149">Esaminare i contratti di servizio nel portale di Azure</span><span class="sxs-lookup"><span data-stu-id="5d414-149">Review SLAs in the Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-your-resources"></a><span data-ttu-id="5d414-150">Pulire le risorse</span><span class="sxs-lookup"><span data-stu-id="5d414-150">Clean up your resources</span></span>

<span data-ttu-id="5d414-151">Se non si prevede di continuare a usare questa app, eliminare tutte le risorse create in questo articolo eseguendo la procedura illustrata di seguito:</span><span class="sxs-lookup"><span data-stu-id="5d414-151">If you do not plan to continue using this app, delete all resources that you created in this article by doing the following:</span></span> 

1. <span data-ttu-id="5d414-152">Nel menu di spostamento a sinistra nel portale di Azure fare clic su **Gruppi di risorse** e quindi sul nome della risorsa creata.</span><span class="sxs-lookup"><span data-stu-id="5d414-152">In the Azure portal, on the left navigation menu, click **Resource groups**, and then click the name of the resource that you created.</span></span> 
2. <span data-ttu-id="5d414-153">Nella pagina del gruppo di risorse fare clic su **Elimina**, digitare il nome della risorsa da eliminare e quindi fare clic su **Elimina**.</span><span class="sxs-lookup"><span data-stu-id="5d414-153">On your resource group page, click **Delete**, type the name of the resource to be deleted, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5d414-154">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5d414-154">Next steps</span></span>

<span data-ttu-id="5d414-155">In questo articolo si è appreso come creare un account Azure Cosmos DB, come creare un grafo con Esplora dati e come eseguire un'app.</span><span class="sxs-lookup"><span data-stu-id="5d414-155">In this article, you've learned how to create an Azure Cosmos DB account, create a graph by using Data Explorer, and run an app.</span></span> <span data-ttu-id="5d414-156">È ora possibile creare query più complesse e implementare la potente logica di attraversamento dei grafi usando Gremlin.</span><span class="sxs-lookup"><span data-stu-id="5d414-156">You can now build more complex queries and implement powerful graph traversal logic by using Gremlin.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="5d414-157">Eseguire query con Gremlin</span><span class="sxs-lookup"><span data-stu-id="5d414-157">Query using Gremlin</span></span>](tutorial-query-graph.md)
