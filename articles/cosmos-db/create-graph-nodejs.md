---
title: un'applicazione Azure Cosmos DB Node.js tramite l'API Graph aaaBuild | Documenti Microsoft
description: "Visualizza un esempio di codice Node.js è possibile utilizzare tooconnect tooand query Azure Cosmos DB"
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
ms.openlocfilehash: 1445755842bc4e4a84ca2b2f789aadde8467e190
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-nodejs-application-by-using-graph-api"></a><span data-ttu-id="fab32-103">Azure Cosmos DB: Creare un'applicazione Node.js tramite l'API Graph</span><span class="sxs-lookup"><span data-stu-id="fab32-103">Azure Cosmos DB: Build a Node.js application by using Graph API</span></span>

<span data-ttu-id="fab32-104">Azure DB Cosmos è servizio di database più modelli hello globale distribuito da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="fab32-104">Azure Cosmos DB is hello globally distributed multi-model database service from Microsoft.</span></span> <span data-ttu-id="fab32-105">Creare rapidamente e query chiave/valore, il documento e database grafico, ognuno dei quali trarre vantaggio dalla distribuzione globale hello e funzionalità di scalabilità orizzontale di base di Azure Cosmos DB hello.</span><span class="sxs-lookup"><span data-stu-id="fab32-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="fab32-106">In questo articolo Guida introduttiva viene illustrato come un database di Azure Cosmos toocreate account per l'API Graph (anteprima), database e grafico tramite hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="fab32-106">This quick-start article demonstrates how toocreate an Azure Cosmos DB account for Graph API (preview), database, and graph by using hello Azure portal.</span></span> <span data-ttu-id="fab32-107">Quindi compilazione e l'esecuzione di un'applicazione console tramite hello open source [Gremlin Node.js](https://www.npmjs.com/package/gremlin-secure) driver.</span><span class="sxs-lookup"><span data-stu-id="fab32-107">You then build and run a console app by using hello open-source [Gremlin Node.js](https://www.npmjs.com/package/gremlin-secure) driver.</span></span>  

> [!NOTE]
> <span data-ttu-id="fab32-108">modulo npm Hello `gremlin-secure` è una versione modificata di `gremlin` modulo, con supporto per SSL e SASL necessari per la connessione con Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="fab32-108">hello npm module `gremlin-secure` is a modified version of `gremlin` module, with support for SSL and SASL required for connecting with Azure Cosmos DB.</span></span> <span data-ttu-id="fab32-109">Il codice sorgente è disponibile su [Github](https://github.com/CosmosDB/gremlin-javascript).</span><span class="sxs-lookup"><span data-stu-id="fab32-109">Source code is available on [GitHub](https://github.com/CosmosDB/gremlin-javascript).</span></span>
>

## <a name="prerequisites"></a><span data-ttu-id="fab32-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="fab32-110">Prerequisites</span></span>

<span data-ttu-id="fab32-111">Prima di poter eseguire questo esempio, è necessario disporre di hello seguenti prerequisiti:</span><span class="sxs-lookup"><span data-stu-id="fab32-111">Before you can run this sample, you must have hello following prerequisites:</span></span>
* <span data-ttu-id="fab32-112">[Node.js](https://nodejs.org/en/) versione v0.10.29 o versioni successive</span><span class="sxs-lookup"><span data-stu-id="fab32-112">[Node.js](https://nodejs.org/en/) version v0.10.29 or later</span></span>
* [<span data-ttu-id="fab32-113">Git</span><span class="sxs-lookup"><span data-stu-id="fab32-113">Git</span></span>](http://git-scm.com/)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="fab32-114">Creare un account di database</span><span class="sxs-lookup"><span data-stu-id="fab32-114">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount-graph](../../includes/cosmos-db-create-dbaccount-graph.md)]

## <a name="add-a-graph"></a><span data-ttu-id="fab32-115">Aggiungere un grafo</span><span class="sxs-lookup"><span data-stu-id="fab32-115">Add a graph</span></span>

[!INCLUDE [cosmos-db-create-graph](../../includes/cosmos-db-create-graph.md)]

## <a name="clone-hello-sample-application"></a><span data-ttu-id="fab32-116">Applicazione di esempio hello clonare</span><span class="sxs-lookup"><span data-stu-id="fab32-116">Clone hello sample application</span></span>

<span data-ttu-id="fab32-117">Ora si app clone un'API Graph da GitHub, impostare la stringa di connessione hello ed eseguirlo.</span><span class="sxs-lookup"><span data-stu-id="fab32-117">Now let's clone a Graph API app from GitHub, set hello connection string, and run it.</span></span> <span data-ttu-id="fab32-118">Si noterà quanto sia facile toowork con i dati a livello di codice.</span><span class="sxs-lookup"><span data-stu-id="fab32-118">You'll see how easy it is toowork with data programmatically.</span></span> 

1. <span data-ttu-id="fab32-119">Aprire una finestra terminale Git, ad esempio Git Bash e modificare (tramite `cd` comando) tooa directory di lavoro.</span><span class="sxs-lookup"><span data-stu-id="fab32-119">Open a Git terminal window, such as Git Bash, and change (via `cd` command) tooa working directory.</span></span>  

2. <span data-ttu-id="fab32-120">Eseguire hello seguenti repository di esempio di comando tooclone hello.</span><span class="sxs-lookup"><span data-stu-id="fab32-120">Run hello following command tooclone hello sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-graph-nodejs-getting-started.git
    ```

3. <span data-ttu-id="fab32-121">Aprire il file di soluzione hello in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="fab32-121">Open hello solution file in Visual Studio.</span></span> 

## <a name="review-hello-code"></a><span data-ttu-id="fab32-122">Esaminare il codice hello</span><span class="sxs-lookup"><span data-stu-id="fab32-122">Review hello code</span></span>

<span data-ttu-id="fab32-123">Questo punto, eseguire una rapida panoramica delle operazioni eseguite nell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="fab32-123">Let's make a quick review of what's happening in hello app.</span></span> <span data-ttu-id="fab32-124">Aprire hello `app.js` file ed è possibile trovare hello righe di codice seguente.</span><span class="sxs-lookup"><span data-stu-id="fab32-124">Open hello `app.js` file, and you'll find hello following lines of code.</span></span> 

* <span data-ttu-id="fab32-125">Hello Gremlin client è stato creato.</span><span class="sxs-lookup"><span data-stu-id="fab32-125">hello Gremlin client is created.</span></span>

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

  <span data-ttu-id="fab32-126">salve le configurazioni sono tutti in `config.js`, che le modifiche apportate nella seguente sezione hello.</span><span class="sxs-lookup"><span data-stu-id="fab32-126">hello configurations are all in `config.js`, which we edit in hello following section.</span></span>

* <span data-ttu-id="fab32-127">Una serie di passaggi Gremlin vengono eseguiti con hello `client.execute` metodo.</span><span class="sxs-lookup"><span data-stu-id="fab32-127">A series of Gremlin steps are executed with hello `client.execute` method.</span></span>

    ```nodejs
    console.log('Running Count'); 
    client.execute("g.V().count()", { }, (err, results) => {
        if (err) return console.error(err);
        console.log(JSON.stringify(results));
        console.log();
    });
    ```

## <a name="update-your-connection-string"></a><span data-ttu-id="fab32-128">Aggiornare la stringa di connessione</span><span class="sxs-lookup"><span data-stu-id="fab32-128">Update your connection string</span></span>

1. <span data-ttu-id="fab32-129">File config.js hello aperto.</span><span class="sxs-lookup"><span data-stu-id="fab32-129">Open hello config.js file.</span></span> 

2. <span data-ttu-id="fab32-130">Nella config.js, inserire nella chiave config.endpoint hello con hello **Gremlin URI** valore hello **Panoramica** pagina del portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="fab32-130">In config.js, fill in hello config.endpoint key with hello **Gremlin URI** value from hello **Overview** page of hello Azure portal.</span></span> 

    `config.endpoint = "GRAPHENDPOINT";`

    ![Visualizzare e copiare una chiave di accesso nel portale di Azure hello, pannello di chiavi](./media/create-graph-nodejs/gremlin-uri.png)

   <span data-ttu-id="fab32-132">Se hello **Gremlin URI** valore è vuoto, è possibile generare il valore di hello da hello **chiavi** pagina nel portale di hello utilizzando hello **URI** valore, rimozione https:// e la modifica toographs documenti.</span><span class="sxs-lookup"><span data-stu-id="fab32-132">If hello **Gremlin URI** value is blank, you can generate hello value from hello **Keys** page in hello portal, using hello **URI** value, removing https://, and changing documents toographs.</span></span>

   <span data-ttu-id="fab32-133">endpoint Gremlin Hello deve essere solo nome host di hello senza un numero di porta o protocollo hello, ad esempio `mygraphdb.graphs.azure.com` (non `https://mygraphdb.graphs.azure.com` o `mygraphdb.graphs.azure.com:433`).</span><span class="sxs-lookup"><span data-stu-id="fab32-133">hello Gremlin endpoint must be only hello host name without hello protocol/port number, like `mygraphdb.graphs.azure.com` (not `https://mygraphdb.graphs.azure.com` or `mygraphdb.graphs.azure.com:433`).</span></span>

3. <span data-ttu-id="fab32-134">Nella config.js, inserire il valore config.primaryKey hello con hello **chiave primaria** valore hello **chiavi** pagina del portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="fab32-134">In config.js, fill in hello config.primaryKey value in with hello **Primary Key** value from hello **Keys** page of hello Azure portal.</span></span> 

    `config.primaryKey = "PRIMARYKEY";`

   ![Hello Azure-blade chiavi portale](./media/create-graph-nodejs/keys.png)

4. <span data-ttu-id="fab32-136">Immettere il nome di database hello e nome del grafico (contenitore) per il valore di hello di config.database e config.collection.</span><span class="sxs-lookup"><span data-stu-id="fab32-136">Enter hello database name, and graph (container) name for hello value of config.database and config.collection.</span></span> 

<span data-ttu-id="fab32-137">Ecco un esempio dell'aspetto che dovrebbe avere il file config.js completato:</span><span class="sxs-lookup"><span data-stu-id="fab32-137">Here is an example of what your completed config.js file should look like:</span></span>

```nodejs
var config = {}

// Note that this must not have HTTPS or hello port number
config.endpoint = "testgraphacct.graphs.azure.com";
config.primaryKey = "Pams6e7LEUS7LJ2Qk0fjZf3eGo65JdMWHmyn65i52w8ozPX2oxY3iP0yu05t9v1WymAHNcMwPIqNAEv3XDFsEg==";
config.database = "graphdb"
config.collection = "Persons"

module.exports = config;
```

## <a name="run-hello-console-app"></a><span data-ttu-id="fab32-138">Eseguire app console hello</span><span class="sxs-lookup"><span data-stu-id="fab32-138">Run hello console app</span></span>

1. <span data-ttu-id="fab32-139">Aprire una finestra terminale e modificare (tramite `cd` comando) toohello directory di installazione per il file package. JSON hello incluso nel progetto hello.</span><span class="sxs-lookup"><span data-stu-id="fab32-139">Open a terminal window and change (via `cd` command) toohello installation directory for hello package.json file that's included in hello project.</span></span>  

2. <span data-ttu-id="fab32-140">Eseguire `npm install` tooinstall hello necessari moduli npm, inclusi `gremlin-secure`.</span><span class="sxs-lookup"><span data-stu-id="fab32-140">Run `npm install` tooinstall hello required npm modules, including `gremlin-secure`.</span></span>

3. <span data-ttu-id="fab32-141">Eseguire `node app.js` in un terminal toostart l'applicazione del nodo.</span><span class="sxs-lookup"><span data-stu-id="fab32-141">Run `node app.js` in a terminal toostart your node application.</span></span>

## <a name="browse-with-data-explorer"></a><span data-ttu-id="fab32-142">Esplorare con Esplora dati</span><span class="sxs-lookup"><span data-stu-id="fab32-142">Browse with Data Explorer</span></span>

<span data-ttu-id="fab32-143">È ora possibile tornare tooData Esplora in hello tooview portale Azure, eseguire query, modificare e lavorare con i nuovi dati del grafico.</span><span class="sxs-lookup"><span data-stu-id="fab32-143">You can now go back tooData Explorer in hello Azure portal tooview, query, modify, and work with your new graph data.</span></span>

<span data-ttu-id="fab32-144">In Esplora dati hello nuovo database verrà visualizzato in hello **grafici** riquadro.</span><span class="sxs-lookup"><span data-stu-id="fab32-144">In Data Explorer, hello new database appears in hello **Graphs** pane.</span></span> <span data-ttu-id="fab32-145">Espandere database hello, seguito da una raccolta di hello, quindi fare clic su **grafico**.</span><span class="sxs-lookup"><span data-stu-id="fab32-145">Expand hello database, followed by hello collection, then click **Graph**.</span></span>

<span data-ttu-id="fab32-146">dati Hello generati dall'applicazione di esempio hello viene visualizzati nel riquadro successivo di hello all'interno di hello **grafico** scheda quando si fa clic **Applica filtro**.</span><span class="sxs-lookup"><span data-stu-id="fab32-146">hello data generated by hello sample app is displayed in hello next pane within hello **Graph** tab when you click **Apply Filter**.</span></span>

<span data-ttu-id="fab32-147">Provare a completare `g.V()` con `.has('firstName', 'Thomas')` filtro hello tootest.</span><span class="sxs-lookup"><span data-stu-id="fab32-147">Try completing `g.V()` with `.has('firstName', 'Thomas')` tootest hello filter.</span></span> <span data-ttu-id="fab32-148">Si noti che il valore di hello tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="fab32-148">Do note that hello value is case sensitive.</span></span>

## <a name="review-slas-in-hello-azure-portal"></a><span data-ttu-id="fab32-149">Esaminare i contratti di servizio nel portale di Azure hello</span><span class="sxs-lookup"><span data-stu-id="fab32-149">Review SLAs in hello Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-your-resources"></a><span data-ttu-id="fab32-150">Pulire le risorse</span><span class="sxs-lookup"><span data-stu-id="fab32-150">Clean up your resources</span></span>

<span data-ttu-id="fab32-151">Se non si prevede toocontinue utilizzando questa app, eliminare tutte le risorse che è stato creato in questo articolo eseguendo hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="fab32-151">If you do not plan toocontinue using this app, delete all resources that you created in this article by doing hello following:</span></span> 

1. <span data-ttu-id="fab32-152">Nel portale di Azure, nel menu di navigazione sinistro hello, hello fare clic su **gruppi di risorse**, quindi fare clic su nome hello della risorsa di hello creato.</span><span class="sxs-lookup"><span data-stu-id="fab32-152">In hello Azure portal, on hello left navigation menu, click **Resource groups**, and then click hello name of hello resource that you created.</span></span> 
2. <span data-ttu-id="fab32-153">Nella pagina di gruppo di risorse, fare clic su **eliminare**, digitare il nome di hello di hello risorsa toobe eliminato e quindi fare clic su **eliminare**.</span><span class="sxs-lookup"><span data-stu-id="fab32-153">On your resource group page, click **Delete**, type hello name of hello resource toobe deleted, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fab32-154">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="fab32-154">Next steps</span></span>

<span data-ttu-id="fab32-155">In questo articolo, si è appreso come creare un grafico utilizzando Esplora dati, un account Azure Cosmos DB, toocreate ed eseguire un'app.</span><span class="sxs-lookup"><span data-stu-id="fab32-155">In this article, you've learned how toocreate an Azure Cosmos DB account, create a graph by using Data Explorer, and run an app.</span></span> <span data-ttu-id="fab32-156">È ora possibile creare query più complesse e implementare la potente logica di attraversamento dei grafi usando Gremlin.</span><span class="sxs-lookup"><span data-stu-id="fab32-156">You can now build more complex queries and implement powerful graph traversal logic by using Gremlin.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="fab32-157">Eseguire query con Gremlin</span><span class="sxs-lookup"><span data-stu-id="fab32-157">Query using Gremlin</span></span>](tutorial-query-graph.md)
