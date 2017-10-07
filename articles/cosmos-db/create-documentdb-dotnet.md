---
title: 'Azure Cosmos DB: Creare un''app web con .NET e hello API DocumentDB | Documenti Microsoft'
description: "Visualizza un esempio di codice .NET è possibile utilizzare query tooand tooconnect hello Azure Cosmos DB DocumentDB API"
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: 35517e35d80c48662a51a99814652ffa1121fc5d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-documentdb-api-web-app-with-net-and-hello-azure-portal"></a><span data-ttu-id="06bb9-103">DB Cosmos Azure: Creare un'app di web API DocumentDB con .NET e hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="06bb9-103">Azure Cosmos DB: Build a DocumentDB API web app with .NET and hello Azure portal</span></span>

<span data-ttu-id="06bb9-104">Azure Cosmos DB è il servizio di database multimodello distribuito a livello globale di Microsoft.</span><span class="sxs-lookup"><span data-stu-id="06bb9-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="06bb9-105">Creare rapidamente e query chiave/valore, il documento e database grafico, ognuno dei quali trarre vantaggio dalla distribuzione globale hello e funzionalità di scalabilità orizzontale di base di Azure Cosmos DB hello.</span><span class="sxs-lookup"><span data-stu-id="06bb9-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="06bb9-106">Questa Guida introduttiva viene illustrato come un account Azure Cosmos DB toocreate, database di documenti e l'utilizzo di raccolta hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="06bb9-106">This quick start demonstrates how toocreate an Azure Cosmos DB account, document database, and collection using hello Azure portal.</span></span> <span data-ttu-id="06bb9-107">Verrà quindi compilare e distribuire un'app web di elenco todo basata su hello [API .NET di DocumentDB](documentdb-sdk-dotnet.md), come illustrato nella seguente schermata hello.</span><span class="sxs-lookup"><span data-stu-id="06bb9-107">You'll then build and deploy a todo list web app built on hello [DocumentDB .NET API](documentdb-sdk-dotnet.md), as shown in hello following screenshot.</span></span> 

![App elenco attività con dati di esempio](./media/create-documentdb-dotnet/azure-comosdb-todo-app-list.png)

## <a name="prerequisites"></a><span data-ttu-id="06bb9-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="06bb9-109">Prerequisites</span></span>

<span data-ttu-id="06bb9-110">Se si dispone già di Visual Studio 2017, che installata, è possibile scaricare e utilizzare hello **libero** [2017 di Visual Studio Community Edition](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="06bb9-110">If you don’t already have Visual Studio 2017 installed, you can download and use hello **free** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="06bb9-111">Assicurarsi di abilitare **lo sviluppo di Azure** durante l'installazione di Visual Studio hello.</span><span class="sxs-lookup"><span data-stu-id="06bb9-111">Make sure that you enable **Azure development** during hello Visual Studio setup.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

<a id="create-account"></a>
## <a name="create-a-database-account"></a><span data-ttu-id="06bb9-112">Creare un account di database</span><span class="sxs-lookup"><span data-stu-id="06bb9-112">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

<a id="create-collection"></a>
## <a name="add-a-collection"></a><span data-ttu-id="06bb9-113">Aggiungere una raccolta</span><span class="sxs-lookup"><span data-stu-id="06bb9-113">Add a collection</span></span>

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

<a id="add-sample-data"></a>
## <a name="add-sample-data"></a><span data-ttu-id="06bb9-114">Aggiungere dati di esempio</span><span class="sxs-lookup"><span data-stu-id="06bb9-114">Add sample data</span></span>

<span data-ttu-id="06bb9-115">È ora possibile aggiungere una nuova raccolta utilizzando Esplora dati tooyour dati.</span><span class="sxs-lookup"><span data-stu-id="06bb9-115">You can now add data tooyour new collection using Data Explorer.</span></span>

1. <span data-ttu-id="06bb9-116">In Esplora dati hello nuovo database verrà visualizzato nel riquadro raccolte hello.</span><span class="sxs-lookup"><span data-stu-id="06bb9-116">In Data Explorer, hello new database appears in hello Collections pane.</span></span> <span data-ttu-id="06bb9-117">Espandere hello **attività** del database, espandere hello **elementi** raccolta, fare clic su **documenti**, quindi fare clic su **nuovi documenti**.</span><span class="sxs-lookup"><span data-stu-id="06bb9-117">Expand hello **Tasks** database, expand hello **Items** collection, click **Documents**, and then click **New Documents**.</span></span> 

   ![Creare nuovi documenti in Esplora dati nel portale di Azure hello](./media/create-documentdb-dotnet/azure-cosmosdb-data-explorer-new-document.png)
  
2. <span data-ttu-id="06bb9-119">Ora è possibile aggiungere una raccolta di documenti toohello con hello seguente struttura.</span><span class="sxs-lookup"><span data-stu-id="06bb9-119">Now add a document toohello collection with hello following structure.</span></span>

     ```json
     {
         "id": "1",
         "category": "personal",
         "name": "groceries",
         "description": "Pick up apples and strawberries.",
         "isComplete": false
     }
     ```

3. <span data-ttu-id="06bb9-120">Dopo aver aggiunto hello json toohello **documenti** scheda, fare clic su **salvare**.</span><span class="sxs-lookup"><span data-stu-id="06bb9-120">Once you've added hello json toohello **Documents** tab, click **Save**.</span></span>

    ![Copiare i dati json e fare clic su Salva in Esplora dati nel portale di Azure hello](./media/create-documentdb-dotnet/azure-cosmosdb-data-explorer-save-document.png)

4.  <span data-ttu-id="06bb9-122">Creare e salvare un documento più in cui si inserisce un valore univoco per hello `id` proprietà e modificare hello altre proprietà nel modo desiderato.</span><span class="sxs-lookup"><span data-stu-id="06bb9-122">Create and save one more document where you insert a unique value for hello `id` property, and change hello other properties as you see fit.</span></span> <span data-ttu-id="06bb9-123">I nuovi documenti possono avere la struttura desiderata, perché Azure Cosmos DB non impone alcuno schema per i dati.</span><span class="sxs-lookup"><span data-stu-id="06bb9-123">Your new documents can have any structure you want as Azure Cosmos DB doesn't impose any schema on your data.</span></span>

     <span data-ttu-id="06bb9-124">È ora possibile utilizzare le query in Esplora dati tooretrieve i dati.</span><span class="sxs-lookup"><span data-stu-id="06bb9-124">You can now use queries in Data Explorer tooretrieve your data.</span></span> <span data-ttu-id="06bb9-125">Per impostazione predefinita, si utilizza Esplora dati `SELECT * FROM c` tooretrieve tutti i documenti nella raccolta di hello, ma è possibile modificare tale tooa diversi [query SQL](documentdb-sql-query.md), ad esempio `SELECT * FROM c ORDER BY c._ts DESC`, tooreturn tutti i documenti hello in ordine decrescente in base a al relativo timestamp.</span><span class="sxs-lookup"><span data-stu-id="06bb9-125">By default, Data Explorer uses `SELECT * FROM c` tooretrieve all documents in hello collection, but you can change that tooa different [SQL query](documentdb-sql-query.md), such as `SELECT * FROM c ORDER BY c._ts DESC`, tooreturn all hello documents in descending order based on their timestamp.</span></span>
 
     <span data-ttu-id="06bb9-126">È inoltre possibile utilizzare Esplora dati toocreate stored procedure, funzioni definite dall'utente e anche logica di business sul lato server tooperform trigger come velocità effettiva di scala.</span><span class="sxs-lookup"><span data-stu-id="06bb9-126">You can also use Data Explorer toocreate stored procedures, UDFs, and triggers tooperform server-side business logic as well as scale throughput.</span></span> <span data-ttu-id="06bb9-127">Esplora dati espone tutti hello predefinite a livello di codice l'accesso ai dati disponibile in hello API, ma fornisce un accesso semplice tooyour dati hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="06bb9-127">Data Explorer exposes all of hello built-in programmatic data access available in hello APIs, but provides easy access tooyour data in hello Azure portal.</span></span>

## <a name="clone-hello-sample-application"></a><span data-ttu-id="06bb9-128">Applicazione di esempio hello clonare</span><span class="sxs-lookup"><span data-stu-id="06bb9-128">Clone hello sample application</span></span>

<span data-ttu-id="06bb9-129">Ora si passa tooworking con il codice.</span><span class="sxs-lookup"><span data-stu-id="06bb9-129">Now let's switch tooworking with code.</span></span> <span data-ttu-id="06bb9-130">Si clona una app per le API DocumentDB da GitHub, impostare la stringa di connessione hello ed eseguirlo.</span><span class="sxs-lookup"><span data-stu-id="06bb9-130">Let's clone a DocumentDB API app from GitHub, set hello connection string, and run it.</span></span> <span data-ttu-id="06bb9-131">Si noterà quanto sia facile toowork con i dati a livello di codice.</span><span class="sxs-lookup"><span data-stu-id="06bb9-131">You'll see how easy it is toowork with data programmatically.</span></span> 

1. <span data-ttu-id="06bb9-132">Aprire una finestra terminale git, ad esempio git bash, e `CD` tooa directory di lavoro.</span><span class="sxs-lookup"><span data-stu-id="06bb9-132">Open a git terminal window, such as git bash, and `CD` tooa working directory.</span></span>  

2. <span data-ttu-id="06bb9-133">Eseguire hello seguenti repository di esempio di comando tooclone hello.</span><span class="sxs-lookup"><span data-stu-id="06bb9-133">Run hello following command tooclone hello sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/documentdb-dotnet-todo-app.git
    ```

3. <span data-ttu-id="06bb9-134">Aprire file di soluzione todo hello in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="06bb9-134">Then open hello todo solution file in Visual Studio.</span></span> 

## <a name="review-hello-code"></a><span data-ttu-id="06bb9-135">Esaminare il codice hello</span><span class="sxs-lookup"><span data-stu-id="06bb9-135">Review hello code</span></span>

<span data-ttu-id="06bb9-136">Questo punto, eseguire una rapida panoramica delle operazioni eseguite nell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="06bb9-136">Let's make a quick review of what's happening in hello app.</span></span> <span data-ttu-id="06bb9-137">File DocumentDBRepository.cs aprire hello e trovare le righe di codice creano hello risorse Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="06bb9-137">Open hello DocumentDBRepository.cs file and you'll find that these lines of code create hello Azure Cosmos DB resources.</span></span> 

* <span data-ttu-id="06bb9-138">Hello DocumentClient viene inizializzato su riga 73.</span><span class="sxs-lookup"><span data-stu-id="06bb9-138">hello DocumentClient is initialized on line 73.</span></span>

    ```csharp
    client = new DocumentClient(new Uri(ConfigurationManager.AppSettings["endpoint"]), ConfigurationManager.AppSettings["authKey"]);`
    ```

* <span data-ttu-id="06bb9-139">Viene creato un nuovo database alla riga 88.</span><span class="sxs-lookup"><span data-stu-id="06bb9-139">A new database is created on line 88.</span></span>

    ```csharp
    await client.CreateDatabaseAsync(new Database { Id = DatabaseId });
    ```

* <span data-ttu-id="06bb9-140">Viene creata una nuova raccolta alla riga 107.</span><span class="sxs-lookup"><span data-stu-id="06bb9-140">A new collection is created on line 107.</span></span>

    ```csharp
    await client.CreateDocumentCollectionAsync(
        UriFactory.CreateDatabaseUri(DatabaseId),
        new DocumentCollection { Id = CollectionId },
        new RequestOptions { OfferThroughput = 1000 });
    ```

## <a name="update-your-connection-string"></a><span data-ttu-id="06bb9-141">Aggiornare la stringa di connessione</span><span class="sxs-lookup"><span data-stu-id="06bb9-141">Update your connection string</span></span>

<span data-ttu-id="06bb9-142">Tornare toohello tooget portale Azure le informazioni sulla stringa di connessione e copiarla in app hello.</span><span class="sxs-lookup"><span data-stu-id="06bb9-142">Now go back toohello Azure portal tooget your connection string information and copy it into hello app.</span></span>

1. <span data-ttu-id="06bb9-143">In hello [portale di Azure](http://portal.azure.com/)il Cosmos Azure DB account, nel riquadro di spostamento sinistro hello fare clic su **chiavi**, quindi fare clic su **le chiavi di lettura / scrittura**.</span><span class="sxs-lookup"><span data-stu-id="06bb9-143">In hello [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in hello left navigation click **Keys**, and then click **Read-write Keys**.</span></span> <span data-ttu-id="06bb9-144">Utilizzare i pulsanti di hello copia sul lato destro hello di hello toocopy di hello schermata URI e chiave primaria nel file Web. config hello nel passaggio successivo hello.</span><span class="sxs-lookup"><span data-stu-id="06bb9-144">You'll use hello copy buttons on hello right side of hello screen toocopy hello URI and Primary Key into hello web.config file in hello next step.</span></span>

    ![Visualizzare e copiare una chiave di accesso nel portale di Azure hello, pannello di chiavi](./media/create-documentdb-dotnet/keys.png)

2. <span data-ttu-id="06bb9-146">In Visual Studio 2017, aprire il file Web. config hello.</span><span class="sxs-lookup"><span data-stu-id="06bb9-146">In Visual Studio 2017, open hello web.config file.</span></span> 

3. <span data-ttu-id="06bb9-147">Copiare il valore dell'URI dal portale di hello (con il pulsante di copia hello) e renderlo hello valore della chiave di endpoint hello in Web. config.</span><span class="sxs-lookup"><span data-stu-id="06bb9-147">Copy your URI value from hello portal (using hello copy button) and make it hello value of hello endpoint key in web.config.</span></span> 

    `<add key="endpoint" value="FILLME" />`

4. <span data-ttu-id="06bb9-148">Quindi copiare il valore di chiave primaria dal portale di hello e renderlo hello valore authKey hello in Web. config. È stato aggiornato a questo punto l'app con tutte le informazioni di hello deve toocommunicate con Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="06bb9-148">Then copy your PRIMARY KEY value from hello portal and make it hello value of hello authKey in web.config. You've now updated your app with all hello info it needs toocommunicate with Azure Cosmos DB.</span></span> 

    `<add key="authKey" value="FILLME" />`
    
## <a name="run-hello-web-app"></a><span data-ttu-id="06bb9-149">Eseguire app web hello</span><span class="sxs-lookup"><span data-stu-id="06bb9-149">Run hello web app</span></span>
1. <span data-ttu-id="06bb9-150">In Visual Studio, fare clic su progetto hello in **Esplora** e quindi fare clic su **Gestisci pacchetti NuGet**.</span><span class="sxs-lookup"><span data-stu-id="06bb9-150">In Visual Studio, right-click on hello project in **Solution Explorer** and then click **Manage NuGet Packages**.</span></span> 

2. <span data-ttu-id="06bb9-151">In hello NuGet **Sfoglia** digitare *DocumentDB*.</span><span class="sxs-lookup"><span data-stu-id="06bb9-151">In hello NuGet **Browse** box, type *DocumentDB*.</span></span>

3. <span data-ttu-id="06bb9-152">Dai risultati di hello, installare hello **Microsoft.Azure.DocumentDB** libreria.</span><span class="sxs-lookup"><span data-stu-id="06bb9-152">From hello results, install hello **Microsoft.Azure.DocumentDB** library.</span></span> <span data-ttu-id="06bb9-153">Consente di installare il pacchetto di Microsoft.Azure.DocumentDB hello, nonché tutte le dipendenze.</span><span class="sxs-lookup"><span data-stu-id="06bb9-153">This installs hello Microsoft.Azure.DocumentDB package as well as all dependencies.</span></span>

4. <span data-ttu-id="06bb9-154">Premere CTRL + F5 applicazione hello toorun.</span><span class="sxs-lookup"><span data-stu-id="06bb9-154">Click CTRL + F5 toorun hello application.</span></span> <span data-ttu-id="06bb9-155">L'app viene visualizzata nel browser.</span><span class="sxs-lookup"><span data-stu-id="06bb9-155">Your app displays in your browser.</span></span> 

5. <span data-ttu-id="06bb9-156">Fare clic su **Crea nuovo** in hello browser e creare nuove attività alcuni nell'app attività da eseguire.</span><span class="sxs-lookup"><span data-stu-id="06bb9-156">Click **Create New** in hello browser and create a few new tasks in your to-do app.</span></span>

   ![App elenco attività con dati di esempio](./media/create-documentdb-dotnet/azure-comosdb-todo-app-list.png)

<span data-ttu-id="06bb9-158">È ora possibile tornare indietro tooData Esplora e vedere query, modificare e funzionare con questi nuovi dati.</span><span class="sxs-lookup"><span data-stu-id="06bb9-158">You can now go back tooData Explorer and see query, modify, and work with this new data.</span></span> 

## <a name="review-slas-in-hello-azure-portal"></a><span data-ttu-id="06bb9-159">Esaminare i contratti di servizio nel portale di Azure hello</span><span class="sxs-lookup"><span data-stu-id="06bb9-159">Review SLAs in hello Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="06bb9-160">Pulire le risorse</span><span class="sxs-lookup"><span data-stu-id="06bb9-160">Clean up resources</span></span>

<span data-ttu-id="06bb9-161">Se non si ha intenzione toocontinue toouse questa app, eliminare tutte le risorse create da questa Guida rapida hello portale di Azure con hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="06bb9-161">If you're not going toocontinue toouse this app, delete all resources created by this quickstart in hello Azure portal with hello following steps:</span></span>

1. <span data-ttu-id="06bb9-162">Dal menu a sinistra di hello in hello portale di Azure, fare clic su **gruppi di risorse** e quindi fare clic su nome hello della risorsa di hello è stato creato.</span><span class="sxs-lookup"><span data-stu-id="06bb9-162">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span> 
2. <span data-ttu-id="06bb9-163">Nella pagina di gruppo di risorse, fare clic su **eliminare**, digitare il nome di hello di hello risorsa toodelete nella casella di testo hello e quindi fare clic su **eliminare**.</span><span class="sxs-lookup"><span data-stu-id="06bb9-163">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="06bb9-164">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="06bb9-164">Next steps</span></span>

<span data-ttu-id="06bb9-165">In questa Guida rapida, si è appreso come creare una raccolta utilizzando Esplora dati hello toocreate un account Azure Cosmos DB ed eseguire un'app web.</span><span class="sxs-lookup"><span data-stu-id="06bb9-165">In this quickstart, you've learned how toocreate an Azure Cosmos DB account, create a collection using hello Data Explorer, and run a web app.</span></span> <span data-ttu-id="06bb9-166">È ora possibile importare account Cosmos DB tooyour di dati aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="06bb9-166">You can now import additional data tooyour Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="06bb9-167">Importare dati in Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="06bb9-167">Import data into Azure Cosmos DB</span></span>](import-data.md)


