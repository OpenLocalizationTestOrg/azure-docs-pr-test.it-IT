---
title: 'Azure Cosmos DB: Creare un''app Web con .NET e l''API DocumentDB | Microsoft Docs'
description: Presenta un esempio di codice .NET che permette di connettersi all'API DocumentDB di Azure Cosmos DB e di eseguire query su di essa
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
ms.openlocfilehash: 9bb863261da64c97f99757d4a0cb3474a7755591
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="azure-cosmos-db-build-a-documentdb-api-web-app-with-net-and-the-azure-portal"></a><span data-ttu-id="3f14d-103">Azure Cosmos DB: Creare un'app Web per le API DocumentDB con .NET e il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="3f14d-103">Azure Cosmos DB: Build a DocumentDB API web app with .NET and the Azure portal</span></span>

<span data-ttu-id="3f14d-104">Azure Cosmos DB è il servizio di database multimodello distribuito a livello globale di Microsoft.</span><span class="sxs-lookup"><span data-stu-id="3f14d-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="3f14d-105">È possibile creare ed eseguire rapidamente query su database di documenti, coppie chiave/valore e grafi, sfruttando in ognuno dei casi i vantaggi offerti dalle funzionalità di scalabilità orizzontale e distribuzione globale alla base di Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="3f14d-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="3f14d-106">Questa guida di avvio rapido mostra come creare un account, un database di documenti e una raccolta di Azure Cosmos DB tramite il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="3f14d-106">This quick start demonstrates how to create an Azure Cosmos DB account, document database, and collection using the Azure portal.</span></span> <span data-ttu-id="3f14d-107">Si creerà e distribuirà quindi l'app Web elenco attività basata sull'[API .NET DocumentDB](documentdb-sdk-dotnet.md), come mostrato nello screenshot seguente.</span><span class="sxs-lookup"><span data-stu-id="3f14d-107">You'll then build and deploy a todo list web app built on the [DocumentDB .NET API](documentdb-sdk-dotnet.md), as shown in the following screenshot.</span></span> 

![App elenco attività con dati di esempio](./media/create-documentdb-dotnet/azure-comosdb-todo-app-list.png)

## <a name="prerequisites"></a><span data-ttu-id="3f14d-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="3f14d-109">Prerequisites</span></span>

<span data-ttu-id="3f14d-110">Se Visual Studio 2017 non è ancora installato, è possibile scaricare e usare la versione **gratuita** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="3f14d-110">If you don’t already have Visual Studio 2017 installed, you can download and use the **free** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="3f14d-111">Durante l'installazione di Visual Studio abilitare **Sviluppo di Azure**.</span><span class="sxs-lookup"><span data-stu-id="3f14d-111">Make sure that you enable **Azure development** during the Visual Studio setup.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

<a id="create-account"></a>
## <a name="create-a-database-account"></a><span data-ttu-id="3f14d-112">Creare un account di database</span><span class="sxs-lookup"><span data-stu-id="3f14d-112">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

<a id="create-collection"></a>
## <a name="add-a-collection"></a><span data-ttu-id="3f14d-113">Aggiungere una raccolta</span><span class="sxs-lookup"><span data-stu-id="3f14d-113">Add a collection</span></span>

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

<a id="add-sample-data"></a>
## <a name="add-sample-data"></a><span data-ttu-id="3f14d-114">Aggiungere dati di esempio</span><span class="sxs-lookup"><span data-stu-id="3f14d-114">Add sample data</span></span>

<span data-ttu-id="3f14d-115">È ora possibile aggiungere dati alla nuova raccolta usando Esplora dati.</span><span class="sxs-lookup"><span data-stu-id="3f14d-115">You can now add data to your new collection using Data Explorer.</span></span>

1. <span data-ttu-id="3f14d-116">In Esplora dati il nuovo database viene visualizzato nel riquadro Raccolte.</span><span class="sxs-lookup"><span data-stu-id="3f14d-116">In Data Explorer, the new database appears in the Collections pane.</span></span> <span data-ttu-id="3f14d-117">Espandere il database **Tasks**, espandere la raccolta **Items**, fare clic su **Documenti** e quindi su **Nuovo documento**.</span><span class="sxs-lookup"><span data-stu-id="3f14d-117">Expand the **Tasks** database, expand the **Items** collection, click **Documents**, and then click **New Documents**.</span></span> 

   ![Creare nuovi documenti in Esplora dati nel portale di Azure](./media/create-documentdb-dotnet/azure-cosmosdb-data-explorer-new-document.png)
  
2. <span data-ttu-id="3f14d-119">Aggiungere ora un documento alla raccolta con la struttura seguente.</span><span class="sxs-lookup"><span data-stu-id="3f14d-119">Now add a document to the collection with the following structure.</span></span>

     ```json
     {
         "id": "1",
         "category": "personal",
         "name": "groceries",
         "description": "Pick up apples and strawberries.",
         "isComplete": false
     }
     ```

3. <span data-ttu-id="3f14d-120">Dopo avere aggiunto il codice JSON alla scheda **Documenti**, fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="3f14d-120">Once you've added the json to the **Documents** tab, click **Save**.</span></span>

    ![Copiare i dati JSON e fare clic su Salva in Esplora dati nel portale di Azure](./media/create-documentdb-dotnet/azure-cosmosdb-data-explorer-save-document.png)

4.  <span data-ttu-id="3f14d-122">Creare e salvare un altro documento inserendo un valore univoco per la proprietà `id` e modificando le altre proprietà come si preferisce.</span><span class="sxs-lookup"><span data-stu-id="3f14d-122">Create and save one more document where you insert a unique value for the `id` property, and change the other properties as you see fit.</span></span> <span data-ttu-id="3f14d-123">I nuovi documenti possono avere la struttura desiderata, perché Azure Cosmos DB non impone alcuno schema per i dati.</span><span class="sxs-lookup"><span data-stu-id="3f14d-123">Your new documents can have any structure you want as Azure Cosmos DB doesn't impose any schema on your data.</span></span>

     <span data-ttu-id="3f14d-124">È ora possibile usare query in Esplora dati per recuperare i dati.</span><span class="sxs-lookup"><span data-stu-id="3f14d-124">You can now use queries in Data Explorer to retrieve your data.</span></span> <span data-ttu-id="3f14d-125">Per impostazione predefinita, Esplora dati usa `SELECT * FROM c` per recuperare tutti i documenti della raccolta, ma è possibile usare una [query SQL](documentdb-sql-query.md) diversa, ad esempio `SELECT * FROM c ORDER BY c._ts DESC`, per restituire tutti i documenti in ordine decrescente in base al timestamp.</span><span class="sxs-lookup"><span data-stu-id="3f14d-125">By default, Data Explorer uses `SELECT * FROM c` to retrieve all documents in the collection, but you can change that to a different [SQL query](documentdb-sql-query.md), such as `SELECT * FROM c ORDER BY c._ts DESC`, to return all the documents in descending order based on their timestamp.</span></span>
 
     <span data-ttu-id="3f14d-126">È anche possibile usare Esplora dati per creare stored procedure, funzioni definite dall'utente e trigger per eseguire la logica di business sul lato server e aumentare la velocità effettiva.</span><span class="sxs-lookup"><span data-stu-id="3f14d-126">You can also use Data Explorer to create stored procedures, UDFs, and triggers to perform server-side business logic as well as scale throughput.</span></span> <span data-ttu-id="3f14d-127">Esplora dati espone tutti i tipi di accesso ai dati a livello di codice predefiniti disponibili nelle API, ma consente anche di accedere facilmente ai dati nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="3f14d-127">Data Explorer exposes all of the built-in programmatic data access available in the APIs, but provides easy access to your data in the Azure portal.</span></span>

## <a name="clone-the-sample-application"></a><span data-ttu-id="3f14d-128">Clonare l'applicazione di esempio</span><span class="sxs-lookup"><span data-stu-id="3f14d-128">Clone the sample application</span></span>

<span data-ttu-id="3f14d-129">Si può ora passare a usare il codice.</span><span class="sxs-lookup"><span data-stu-id="3f14d-129">Now let's switch to working with code.</span></span> <span data-ttu-id="3f14d-130">Si clonerà un'app per le API DocumentDB da GitHub, si imposterà la stringa di connessione e si eseguirà l'app.</span><span class="sxs-lookup"><span data-stu-id="3f14d-130">Let's clone a DocumentDB API app from GitHub, set the connection string, and run it.</span></span> <span data-ttu-id="3f14d-131">Come si noterà, è facile usare i dati a livello di codice.</span><span class="sxs-lookup"><span data-stu-id="3f14d-131">You'll see how easy it is to work with data programmatically.</span></span> 

1. <span data-ttu-id="3f14d-132">Aprire una finestra del terminale Git, ad esempio Git Bash, ed eseguire il comando `CD` per passare a una directory di lavoro.</span><span class="sxs-lookup"><span data-stu-id="3f14d-132">Open a git terminal window, such as git bash, and `CD` to a working directory.</span></span>  

2. <span data-ttu-id="3f14d-133">Eseguire il comando seguente per clonare l'archivio di esempio.</span><span class="sxs-lookup"><span data-stu-id="3f14d-133">Run the following command to clone the sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/documentdb-dotnet-todo-app.git
    ```

3. <span data-ttu-id="3f14d-134">Aprire quindi il file della soluzione todo in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3f14d-134">Then open the todo solution file in Visual Studio.</span></span> 

## <a name="review-the-code"></a><span data-ttu-id="3f14d-135">Esaminare il codice</span><span class="sxs-lookup"><span data-stu-id="3f14d-135">Review the code</span></span>

<span data-ttu-id="3f14d-136">Ecco una breve analisi di ciò che accade nell'app.</span><span class="sxs-lookup"><span data-stu-id="3f14d-136">Let's make a quick review of what's happening in the app.</span></span> <span data-ttu-id="3f14d-137">Aprire il file DocumentDBRepository.cs. Come si noterà, queste righe di codice creano le risorse di Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="3f14d-137">Open the DocumentDBRepository.cs file and you'll find that these lines of code create the Azure Cosmos DB resources.</span></span> 

* <span data-ttu-id="3f14d-138">Viene inizializzato DocumentClient alla riga 73.</span><span class="sxs-lookup"><span data-stu-id="3f14d-138">The DocumentClient is initialized on line 73.</span></span>

    ```csharp
    client = new DocumentClient(new Uri(ConfigurationManager.AppSettings["endpoint"]), ConfigurationManager.AppSettings["authKey"]);`
    ```

* <span data-ttu-id="3f14d-139">Viene creato un nuovo database alla riga 88.</span><span class="sxs-lookup"><span data-stu-id="3f14d-139">A new database is created on line 88.</span></span>

    ```csharp
    await client.CreateDatabaseAsync(new Database { Id = DatabaseId });
    ```

* <span data-ttu-id="3f14d-140">Viene creata una nuova raccolta alla riga 107.</span><span class="sxs-lookup"><span data-stu-id="3f14d-140">A new collection is created on line 107.</span></span>

    ```csharp
    await client.CreateDocumentCollectionAsync(
        UriFactory.CreateDatabaseUri(DatabaseId),
        new DocumentCollection { Id = CollectionId },
        new RequestOptions { OfferThroughput = 1000 });
    ```

## <a name="update-your-connection-string"></a><span data-ttu-id="3f14d-141">Aggiornare la stringa di connessione</span><span class="sxs-lookup"><span data-stu-id="3f14d-141">Update your connection string</span></span>

<span data-ttu-id="3f14d-142">Tornare ora al portale di Azure per recuperare le informazioni sulla stringa di connessione e copiarle nell'app.</span><span class="sxs-lookup"><span data-stu-id="3f14d-142">Now go back to the Azure portal to get your connection string information and copy it into the app.</span></span>

1. <span data-ttu-id="3f14d-143">Nell'account Azure Cosmos DB nel [portale di Azure](http://portal.azure.com/) fare clic su **Chiavi** nel riquadro di spostamento a sinistra e quindi su **Chiavi di lettura/scrittura**.</span><span class="sxs-lookup"><span data-stu-id="3f14d-143">In the [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in the left navigation click **Keys**, and then click **Read-write Keys**.</span></span> <span data-ttu-id="3f14d-144">Usare i pulsanti di copia sul lato destro dello schermo per copiare l'URI e la chiave primaria nel file web.config nel passaggio seguente.</span><span class="sxs-lookup"><span data-stu-id="3f14d-144">You'll use the copy buttons on the right side of the screen to copy the URI and Primary Key into the web.config file in the next step.</span></span>

    ![Visualizzazione e copia di una chiave di accesso nel portale di Azure, pannello Chiavi](./media/create-documentdb-dotnet/keys.png)

2. <span data-ttu-id="3f14d-146">In Visual Studio 2017 aprire il file web.config.</span><span class="sxs-lookup"><span data-stu-id="3f14d-146">In Visual Studio 2017, open the web.config file.</span></span> 

3. <span data-ttu-id="3f14d-147">Copiare il valore di URI dal portale (usando il pulsante di copia) e impostarlo come valore della chiave di endpoint in web.config.</span><span class="sxs-lookup"><span data-stu-id="3f14d-147">Copy your URI value from the portal (using the copy button) and make it the value of the endpoint key in web.config.</span></span> 

    `<add key="endpoint" value="FILLME" />`

4. <span data-ttu-id="3f14d-148">Copiare quindi il valore di CHIAVE PRIMARIA dal portale e impostarlo come valore di authKey in web.config. L'app è stata aggiornata con tutte le informazioni necessarie per comunicare con Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="3f14d-148">Then copy your PRIMARY KEY value from the portal and make it the value of the authKey in web.config. You've now updated your app with all the info it needs to communicate with Azure Cosmos DB.</span></span> 

    `<add key="authKey" value="FILLME" />`
    
## <a name="run-the-web-app"></a><span data-ttu-id="3f14d-149">Eseguire l'app Web</span><span class="sxs-lookup"><span data-stu-id="3f14d-149">Run the web app</span></span>
1. <span data-ttu-id="3f14d-150">In Visual Studio fare clic con il pulsante destro del mouse sul progetto in **Esplora soluzioni** e quindi scegliere **Gestisci pacchetti NuGet**.</span><span class="sxs-lookup"><span data-stu-id="3f14d-150">In Visual Studio, right-click on the project in **Solution Explorer** and then click **Manage NuGet Packages**.</span></span> 

2. <span data-ttu-id="3f14d-151">Nella casella **Sfoglia** di NuGet digitare *DocumentDB*.</span><span class="sxs-lookup"><span data-stu-id="3f14d-151">In the NuGet **Browse** box, type *DocumentDB*.</span></span>

3. <span data-ttu-id="3f14d-152">Dai risultati installare la libreria **Microsoft.Azure.DocumentDB**.</span><span class="sxs-lookup"><span data-stu-id="3f14d-152">From the results, install the **Microsoft.Azure.DocumentDB** library.</span></span> <span data-ttu-id="3f14d-153">Viene installato il pacchetto Microsoft.Azure.DocumentDB, insieme a tutte le dipendenze.</span><span class="sxs-lookup"><span data-stu-id="3f14d-153">This installs the Microsoft.Azure.DocumentDB package as well as all dependencies.</span></span>

4. <span data-ttu-id="3f14d-154">Premere CTRL+F5 per eseguire l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="3f14d-154">Click CTRL + F5 to run the application.</span></span> <span data-ttu-id="3f14d-155">L'app viene visualizzata nel browser.</span><span class="sxs-lookup"><span data-stu-id="3f14d-155">Your app displays in your browser.</span></span> 

5. <span data-ttu-id="3f14d-156">Fare clic su **Crea nuovo** nel browser e creare alcune nuove attività nell'app elenco attività.</span><span class="sxs-lookup"><span data-stu-id="3f14d-156">Click **Create New** in the browser and create a few new tasks in your to-do app.</span></span>

   ![App elenco attività con dati di esempio](./media/create-documentdb-dotnet/azure-comosdb-todo-app-list.png)

<span data-ttu-id="3f14d-158">È ora possibile tornare a Esplora dati e visualizzare, modificare e usare questi nuovi dati, nonché eseguire query su di essi.</span><span class="sxs-lookup"><span data-stu-id="3f14d-158">You can now go back to Data Explorer and see query, modify, and work with this new data.</span></span> 

## <a name="review-slas-in-the-azure-portal"></a><span data-ttu-id="3f14d-159">Esaminare i contratti di servizio nel portale di Azure</span><span class="sxs-lookup"><span data-stu-id="3f14d-159">Review SLAs in the Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="3f14d-160">Pulire le risorse</span><span class="sxs-lookup"><span data-stu-id="3f14d-160">Clean up resources</span></span>

<span data-ttu-id="3f14d-161">Se non si intende continuare a usare l'app, eliminare tutte le risorse create tramite questa guida di avvio rapido nel portale di Azure eseguendo questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="3f14d-161">If you're not going to continue to use this app, delete all resources created by this quickstart in the Azure portal with the following steps:</span></span>

1. <span data-ttu-id="3f14d-162">Scegliere **Gruppi di risorse** dal menu a sinistra del portale di Azure e quindi fare clic sul nome della risorsa creata.</span><span class="sxs-lookup"><span data-stu-id="3f14d-162">From the left-hand menu in the Azure portal, click **Resource groups** and then click the name of the resource you created.</span></span> 
2. <span data-ttu-id="3f14d-163">Nella pagina del gruppo di risorse fare clic su **Elimina**, digitare il nome della risorsa da eliminare nella casella di testo e quindi fare clic su **Elimina**.</span><span class="sxs-lookup"><span data-stu-id="3f14d-163">On your resource group page, click **Delete**, type the name of the resource to delete in the text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3f14d-164">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3f14d-164">Next steps</span></span>

<span data-ttu-id="3f14d-165">In questa guida di avvio rapido si è appreso come creare un account Azure Cosmos DB, come creare una raccolta con Esplora dati e come eseguire un'app Web.</span><span class="sxs-lookup"><span data-stu-id="3f14d-165">In this quickstart, you've learned how to create an Azure Cosmos DB account, create a collection using the Data Explorer, and run a web app.</span></span> <span data-ttu-id="3f14d-166">È ora possibile importare dati aggiuntivi nell'account Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="3f14d-166">You can now import additional data to your Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="3f14d-167">Importare dati in Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="3f14d-167">Import data into Azure Cosmos DB</span></span>](import-data.md)


