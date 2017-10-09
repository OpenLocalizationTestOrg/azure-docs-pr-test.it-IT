---
title: un'applicazione Azure Cosmos DB .NET utilizzando aaaBuild hello API Graph | Documenti Microsoft
description: "Visualizza un esempio di codice .NET è possibile utilizzare tooconnect tooand query Azure Cosmos DB"
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
ms.date: 07/28/2017
ms.author: denlee
ms.openlocfilehash: f28790fcb8c9f57c7bb3d844d8276fa04abcc39c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-net-application-using-hello-graph-api"></a><span data-ttu-id="bf037-103">Azure Cosmos DB: Compilare un'applicazione .NET usando hello API Graph</span><span class="sxs-lookup"><span data-stu-id="bf037-103">Azure Cosmos DB: Build a .NET application using hello Graph API</span></span>

<span data-ttu-id="bf037-104">Azure Cosmos DB è il servizio di database multimodello distribuito a livello globale di Microsoft.</span><span class="sxs-lookup"><span data-stu-id="bf037-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="bf037-105">Creare rapidamente e query chiave/valore, il documento e database grafico, ognuno dei quali trarre vantaggio dalla distribuzione globale hello e funzionalità di scalabilità orizzontale di base di Azure Cosmos DB hello.</span><span class="sxs-lookup"><span data-stu-id="bf037-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="bf037-106">Questa Guida introduttiva viene illustrato come un account Azure Cosmos DB toocreate, database e l'utilizzo di graph (contenitore) hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="bf037-106">This quick start demonstrates how toocreate an Azure Cosmos DB account, database, and graph (container) using hello Azure portal.</span></span> <span data-ttu-id="bf037-107">Quindi compilazione e l'esecuzione di un'applicazione console basata su hello [API Graph](graph-sdk-dotnet.md) (anteprima).</span><span class="sxs-lookup"><span data-stu-id="bf037-107">You then build and run a console app built on hello [Graph API](graph-sdk-dotnet.md) (preview).</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="bf037-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="bf037-108">Prerequisites</span></span>

<span data-ttu-id="bf037-109">Se si dispone già di Visual Studio 2017, che installata, è possibile scaricare e utilizzare hello **libero** [2017 di Visual Studio Community Edition](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="bf037-109">If you don’t already have Visual Studio 2017 installed, you can download and use hello **free** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="bf037-110">Assicurarsi di abilitare **lo sviluppo di Azure** durante l'installazione di Visual Studio hello.</span><span class="sxs-lookup"><span data-stu-id="bf037-110">Make sure that you enable **Azure development** during hello Visual Studio setup.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="bf037-111">Creare un account di database</span><span class="sxs-lookup"><span data-stu-id="bf037-111">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount-graph](../../includes/cosmos-db-create-dbaccount-graph.md)]

## <a name="add-a-graph"></a><span data-ttu-id="bf037-112">Aggiungere un grafo</span><span class="sxs-lookup"><span data-stu-id="bf037-112">Add a graph</span></span>

[!INCLUDE [cosmos-db-create-graph](../../includes/cosmos-db-create-graph.md)]

## <a name="clone-hello-sample-application"></a><span data-ttu-id="bf037-113">Applicazione di esempio hello clonare</span><span class="sxs-lookup"><span data-stu-id="bf037-113">Clone hello sample application</span></span>

<span data-ttu-id="bf037-114">Ora si app clone un'API Graph da github, impostare la stringa di connessione hello ed eseguirlo.</span><span class="sxs-lookup"><span data-stu-id="bf037-114">Now let's clone a Graph API app from github, set hello connection string, and run it.</span></span> <span data-ttu-id="bf037-115">Si noterà quanto sia facile toowork con i dati a livello di codice.</span><span class="sxs-lookup"><span data-stu-id="bf037-115">You'll see how easy it is toowork with data programmatically.</span></span> 

1. <span data-ttu-id="bf037-116">Aprire una finestra terminale git, ad esempio git bash, e `cd` tooa directory di lavoro.</span><span class="sxs-lookup"><span data-stu-id="bf037-116">Open a git terminal window, such as git bash, and `cd` tooa working directory.</span></span>  

2. <span data-ttu-id="bf037-117">Eseguire hello seguenti repository di esempio di comando tooclone hello.</span><span class="sxs-lookup"><span data-stu-id="bf037-117">Run hello following command tooclone hello sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-graph-dotnet-getting-started.git
    ```

3. <span data-ttu-id="bf037-118">Aprire Visual Studio e i file di soluzione hello aperto.</span><span class="sxs-lookup"><span data-stu-id="bf037-118">Then open Visual Studio and open hello solution file.</span></span> 

## <a name="review-hello-code"></a><span data-ttu-id="bf037-119">Esaminare il codice hello</span><span class="sxs-lookup"><span data-stu-id="bf037-119">Review hello code</span></span>

<span data-ttu-id="bf037-120">Questo punto, eseguire una rapida panoramica delle operazioni eseguite nell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="bf037-120">Let's make a quick review of what's happening in hello app.</span></span> <span data-ttu-id="bf037-121">File Program.cs aprire hello e trovare le righe di codice creano hello risorse Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="bf037-121">Open hello Program.cs file and you'll find that these lines of code create hello Azure Cosmos DB resources.</span></span> 

* <span data-ttu-id="bf037-122">Hello DocumentClient viene inizializzato.</span><span class="sxs-lookup"><span data-stu-id="bf037-122">hello DocumentClient is initialized.</span></span> <span data-ttu-id="bf037-123">Nell'anteprima hello, abbiamo aggiunto un'estensione di graph API client di Azure Cosmos DB hello.</span><span class="sxs-lookup"><span data-stu-id="bf037-123">In hello preview, we added a graph extension API on hello Azure Cosmos DB client.</span></span> <span data-ttu-id="bf037-124">Stiamo lavorando in un client di graph autonoma scollegato dal client di Azure Cosmos DB hello e risorse.</span><span class="sxs-lookup"><span data-stu-id="bf037-124">We are working on a standalone graph client decoupled from hello Azure Cosmos DB client and resources.</span></span>

    ```csharp
    using (DocumentClient client = new DocumentClient(
        new Uri(endpoint),
        authKey,
        new ConnectionPolicy { ConnectionMode = ConnectionMode.Direct, ConnectionProtocol = Protocol.Tcp }))
    ```

* <span data-ttu-id="bf037-125">Viene creato un nuovo database.</span><span class="sxs-lookup"><span data-stu-id="bf037-125">A new database is created.</span></span>

    ```csharp
    Database database = await client.CreateDatabaseIfNotExistsAsync(new Database { Id = "graphdb" });
    ```

* <span data-ttu-id="bf037-126">Viene creato un nuovo grafo.</span><span class="sxs-lookup"><span data-stu-id="bf037-126">A new graph is created.</span></span>

    ```csharp
    DocumentCollection graph = await client.CreateDocumentCollectionIfNotExistsAsync(
        UriFactory.CreateDatabaseUri("graphdb"),
        new DocumentCollection { Id = "graph" },
        new RequestOptions { OfferThroughput = 1000 });
    ```
* <span data-ttu-id="bf037-127">Una serie di passaggi Gremlin vengono eseguite utilizzando hello `CreateGremlinQuery` metodo.</span><span class="sxs-lookup"><span data-stu-id="bf037-127">A series of Gremlin steps are executed using hello `CreateGremlinQuery` method.</span></span>

    ```csharp
    // hello CreateGremlinQuery method extensions allow you tooexecute Gremlin queries and iterate
    // results asychronously
    IDocumentQuery<dynamic> query = client.CreateGremlinQuery<dynamic>(graph, "g.V().count()");
    while (query.HasMoreResults)
    {
        foreach (dynamic result in await query.ExecuteNextAsync())
        {
            Console.WriteLine($"\t {JsonConvert.SerializeObject(result)}");
        }
    }

    ```

## <a name="update-your-connection-string"></a><span data-ttu-id="bf037-128">Aggiornare la stringa di connessione</span><span class="sxs-lookup"><span data-stu-id="bf037-128">Update your connection string</span></span>

<span data-ttu-id="bf037-129">Tornare toohello tooget portale Azure le informazioni sulla stringa di connessione e copiarla in app hello.</span><span class="sxs-lookup"><span data-stu-id="bf037-129">Now go back toohello Azure portal tooget your connection string information and copy it into hello app.</span></span>

1. <span data-ttu-id="bf037-130">In Visual Studio 2017, aprire il file app. config hello.</span><span class="sxs-lookup"><span data-stu-id="bf037-130">In Visual Studio 2017, open hello App.config file.</span></span> 

2. <span data-ttu-id="bf037-131">Nel portale di Azure nell'account di Azure Cosmos DB, hello fare clic su **chiavi** nel riquadro di spostamento sinistro hello.</span><span class="sxs-lookup"><span data-stu-id="bf037-131">In hello Azure portal, in your Azure Cosmos DB account, click **Keys** in hello left navigation.</span></span> 

    ![Visualizzare e copiare una chiave primaria nel portale di Azure, nella pagina chiavi hello hello](./media/create-graph-dotnet/keys.png)

3. <span data-ttu-id="bf037-133">Copia il **URI** valore dal portale hello e renderlo hello valore della chiave di Endpoint hello in App. config. È possibile utilizzare il pulsante di copia hello come mostrato nella precedente schermata valore di hello toocopy hello.</span><span class="sxs-lookup"><span data-stu-id="bf037-133">Copy your **URI** value from hello portal and make it hello value of hello Endpoint key in App.config. You can use hello copy button as shown in hello preceding screenshot toocopy hello value.</span></span>

    `<add key="Endpoint" value="https://FILLME.documents.azure.com:443" />`

4. <span data-ttu-id="bf037-134">Copia il **chiave primaria** valore dal portale hello e renderlo hello valore della chiave AuthKey hello in App. config, quindi salvare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="bf037-134">Copy your **PRIMARY KEY** value from hello portal, and make it hello value of hello AuthKey key in App.config, then save your changes.</span></span> 

    `<add key="AuthKey" value="FILLME" />`

<span data-ttu-id="bf037-135">È stato aggiornato a questo punto l'app con tutte le informazioni di hello deve toocommunicate con Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="bf037-135">You've now updated your app with all hello info it needs toocommunicate with Azure Cosmos DB.</span></span> 

## <a name="run-hello-console-app"></a><span data-ttu-id="bf037-136">Eseguire app console hello</span><span class="sxs-lookup"><span data-stu-id="bf037-136">Run hello console app</span></span>

1. <span data-ttu-id="bf037-137">In Visual Studio, fare clic su hello **GraphGetStarted** nel progetto **Esplora** e quindi fare clic su **Gestisci pacchetti NuGet**.</span><span class="sxs-lookup"><span data-stu-id="bf037-137">In Visual Studio, right-click on hello **GraphGetStarted** project in **Solution Explorer** and then click **Manage NuGet Packages**.</span></span> 

2. <span data-ttu-id="bf037-138">In hello NuGet **Sfoglia** digitare *Microsoft.Azure.Graphs* e controllare hello **include una versione provvisoria** casella.</span><span class="sxs-lookup"><span data-stu-id="bf037-138">In hello NuGet **Browse** box, type *Microsoft.Azure.Graphs* and check hello **Includes prerelease** box.</span></span> 

3. <span data-ttu-id="bf037-139">Dai risultati di hello, installare hello **Microsoft.Azure.Graphs** libreria.</span><span class="sxs-lookup"><span data-stu-id="bf037-139">From hello results, install hello **Microsoft.Azure.Graphs** library.</span></span> <span data-ttu-id="bf037-140">Questo Installa pacchetto di hello Azure Cosmos DB grafico estensione della libreria e tutte le dipendenze.</span><span class="sxs-lookup"><span data-stu-id="bf037-140">This installs hello Azure Cosmos DB graph extension library package and all dependencies.</span></span>

    <span data-ttu-id="bf037-141">Se viene visualizzato un messaggio sull'esaminato soluzione toohello modifiche, fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="bf037-141">If you get a message about reviewing changes toohello solution, click **OK**.</span></span> <span data-ttu-id="bf037-142">Se viene visualizzato un messaggio sull'accettazione della licenza, fare clic su **Accetto**.</span><span class="sxs-lookup"><span data-stu-id="bf037-142">If you get a message about license acceptance, click **I accept**.</span></span>

4. <span data-ttu-id="bf037-143">Premere CTRL + F5 applicazione hello toorun.</span><span class="sxs-lookup"><span data-stu-id="bf037-143">Click CTRL + F5 toorun hello application.</span></span>

   <span data-ttu-id="bf037-144">finestra della console Hello Visualizza vertici hello e bordi aggiunti toohello grafico.</span><span class="sxs-lookup"><span data-stu-id="bf037-144">hello console window displays hello vertexes and edges being added toohello graph.</span></span> <span data-ttu-id="bf037-145">Quando hello completamento dello script, premere INVIO due volte finestra della console hello tooclose.</span><span class="sxs-lookup"><span data-stu-id="bf037-145">When hello script completes, press ENTER twice tooclose hello console window.</span></span> 

## <a name="browse-using-hello-data-explorer"></a><span data-ttu-id="bf037-146">Sfogliare il modello utilizzando hello Esplora dati</span><span class="sxs-lookup"><span data-stu-id="bf037-146">Browse using hello Data Explorer</span></span>

<span data-ttu-id="bf037-147">È possibile tornare indietro tooData Explorer nel portale di Azure hello e Sfoglia e query nei nuovi dati grafico.</span><span class="sxs-lookup"><span data-stu-id="bf037-147">You can now go back tooData Explorer in hello Azure portal and browse and query your new graph data.</span></span>

1. <span data-ttu-id="bf037-148">In Esplora dati hello nuovo database verrà visualizzato nel riquadro di grafici di hello.</span><span class="sxs-lookup"><span data-stu-id="bf037-148">In Data Explorer, hello new database appears in hello Graphs pane.</span></span> <span data-ttu-id="bf037-149">Espandere **graphdb** e **graphcollz** e quindi fare clic su **Grafico**.</span><span class="sxs-lookup"><span data-stu-id="bf037-149">Expand **graphdb**, **graphcollz**, and then click **Graph**.</span></span>

2. <span data-ttu-id="bf037-150">Fare clic su hello **Applica filtro** predefinito di hello toouse pulsante query tooview tutti i vertici hello nel grafico hello.</span><span class="sxs-lookup"><span data-stu-id="bf037-150">Click hello **Apply Filter** button toouse hello default query tooview all hello verticies in hello graph.</span></span> <span data-ttu-id="bf037-151">dati Hello generati dall'applicazione di esempio hello viene visualizzati nel riquadro di grafici di hello.</span><span class="sxs-lookup"><span data-stu-id="bf037-151">hello data generated by hello sample app is displayed in hello Graphs pane.</span></span>

    <span data-ttu-id="bf037-152">È possibile ingrandire o ridurre il grafico di hello, è possibile espandere lo spazio di visualizzazione grafico hello, aggiungere ulteriori vertici e spostare vertici su hello dell'area di visualizzazione.</span><span class="sxs-lookup"><span data-stu-id="bf037-152">You can zoom in and out of hello graph, you can expand hello graph display space, add additional verticies, and move verticies on hello display surface.</span></span>

    ![Visualizza un grafico di hello in Esplora dati nel portale di Azure hello](./media/create-graph-dotnet/graph-explorer.png)

## <a name="review-slas-in-hello-azure-portal"></a><span data-ttu-id="bf037-154">Esaminare i contratti di servizio nel portale di Azure hello</span><span class="sxs-lookup"><span data-stu-id="bf037-154">Review SLAs in hello Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="bf037-155">Pulire le risorse</span><span class="sxs-lookup"><span data-stu-id="bf037-155">Clean up resources</span></span>

<span data-ttu-id="bf037-156">Se non si ha intenzione toocontinue toouse questa app, eliminare tutte le risorse create da questa Guida rapida hello portale di Azure con hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="bf037-156">If you're not going toocontinue toouse this app, delete all resources created by this quickstart in hello Azure portal with hello following steps:</span></span> 

1. <span data-ttu-id="bf037-157">Dal menu a sinistra di hello in hello portale di Azure, fare clic su **gruppi di risorse** e quindi fare clic su nome hello della risorsa di hello è stato creato.</span><span class="sxs-lookup"><span data-stu-id="bf037-157">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span> 
2. <span data-ttu-id="bf037-158">Nella pagina di gruppo di risorse, fare clic su **eliminare**, digitare il nome di hello di hello risorsa toodelete nella casella di testo hello e quindi fare clic su **eliminare**.</span><span class="sxs-lookup"><span data-stu-id="bf037-158">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bf037-159">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="bf037-159">Next steps</span></span>

<span data-ttu-id="bf037-160">In questa Guida rapida, si è appreso come creare un grafico utilizzando Esplora dati hello toocreate un account Azure Cosmos DB ed eseguire un'app.</span><span class="sxs-lookup"><span data-stu-id="bf037-160">In this quickstart, you've learned how toocreate an Azure Cosmos DB account, create a graph using hello Data Explorer, and run an app.</span></span> <span data-ttu-id="bf037-161">È ora possibile creare query più complesse e implementare la potente logica di attraversamento dei grafi usando Gremlin.</span><span class="sxs-lookup"><span data-stu-id="bf037-161">You can now build more complex queries and implement powerful graph traversal logic using Gremlin.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="bf037-162">Eseguire query con Gremlin</span><span class="sxs-lookup"><span data-stu-id="bf037-162">Query using Gremlin</span></span>](tutorial-query-graph.md)

