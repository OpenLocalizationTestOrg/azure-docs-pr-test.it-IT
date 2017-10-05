---
title: Creare un database di documenti di Azure Cosmos DB con Java | Microsoft Docs | Microsoft Docs
description: Presenta un esempio di codice Java che permette di connettersi all'API DocumentDB di Azure Cosmos DB ed eseguire query su di essa
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 89ea62bb-c620-46d5-baa0-eefd9888557c
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: hero-article
ms.date: 08/02/2017
ms.author: mimig
ms.openlocfilehash: df1a25d703a7b8082bdabb4f7d593cb005d416fe
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="azure-cosmos-db-create-a-document-database-using-java-and-the-azure-portal"></a><span data-ttu-id="60b48-103">Azure Cosmos DB: Creare un database di documenti con Java e il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="60b48-103">Azure Cosmos DB: Create a document database using Java and the Azure portal</span></span>

<span data-ttu-id="60b48-104">Azure Cosmos DB è il servizio di database multimodello distribuito a livello globale di Microsoft.</span><span class="sxs-lookup"><span data-stu-id="60b48-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="60b48-105">È possibile creare ed eseguire rapidamente query su database di documenti, coppie chiave/valore e grafi, sfruttando in ognuno dei casi i vantaggi offerti dalle funzionalità di scalabilità orizzontale e distribuzione globale alla base di Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="60b48-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="60b48-106">Questa guida introduttiva illustra come creare un database di documenti con gli strumenti del portale di Azure per Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="60b48-106">This quickstart creates a document database using the Azure portal tools for Azure Cosmos DB.</span></span> <span data-ttu-id="60b48-107">Illustra anche come creare rapidamente un'app console Java usando l'[API Java DocumentDB](documentdb-sdk-java.md).</span><span class="sxs-lookup"><span data-stu-id="60b48-107">This quickstart also shows you how to quickly create a Java console app using the [DocumentDB Java API](documentdb-sdk-java.md).</span></span> <span data-ttu-id="60b48-108">Le istruzioni di questa guida introduttiva possono essere eseguite in qualsiasi sistema operativo in grado di eseguire Java.</span><span class="sxs-lookup"><span data-stu-id="60b48-108">The instructions in this quickstart can be followed on any operating system that is capable of running Java.</span></span> <span data-ttu-id="60b48-109">Completando questa guida introduttiva si acquisirà familiarità con la creazione e la modifica di risorse database di documenti nell'interfaccia utente o a livello di codice, in base alle proprie preferenze.</span><span class="sxs-lookup"><span data-stu-id="60b48-109">By completing this quickstart you'll be familiar with creating and modifying document database resources in either the UI or programatically, whichever is your preference.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="60b48-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="60b48-110">Prerequisites</span></span>

* [<span data-ttu-id="60b48-111">Java Development Kit (JDK) 1.7+</span><span class="sxs-lookup"><span data-stu-id="60b48-111">Java Development Kit (JDK) 1.7+</span></span>](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
    * <span data-ttu-id="60b48-112">In Ubuntu eseguire `apt-get install default-jdk` per installare JDK.</span><span class="sxs-lookup"><span data-stu-id="60b48-112">On Ubuntu, run `apt-get install default-jdk` to install the JDK.</span></span>
    * <span data-ttu-id="60b48-113">Assicurarsi di impostare la variabile di ambiente JAVA_HOME in modo che faccia riferimento alla cartella di installazione di JDK.</span><span class="sxs-lookup"><span data-stu-id="60b48-113">Be sure to set the JAVA_HOME environment variable to point to the folder where the JDK is installed.</span></span>
* <span data-ttu-id="60b48-114">[Scaricare](http://maven.apache.org/download.cgi) e [installare](http://maven.apache.org/install.html) un archivio binario [Maven](http://maven.apache.org/)</span><span class="sxs-lookup"><span data-stu-id="60b48-114">[Download](http://maven.apache.org/download.cgi) and [install](http://maven.apache.org/install.html) a [Maven](http://maven.apache.org/) binary archive</span></span>
    * <span data-ttu-id="60b48-115">In Ubuntu è possibile eseguire `apt-get install maven` per installare Maven.</span><span class="sxs-lookup"><span data-stu-id="60b48-115">On Ubuntu, you can run `apt-get install maven` to install Maven.</span></span>
* [<span data-ttu-id="60b48-116">Git</span><span class="sxs-lookup"><span data-stu-id="60b48-116">Git</span></span>](https://www.git-scm.com/)
    * <span data-ttu-id="60b48-117">In Ubuntu è possibile eseguire `sudo apt-get install git` per installare Git.</span><span class="sxs-lookup"><span data-stu-id="60b48-117">On Ubuntu, you can run `sudo apt-get install git` to install Git.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="60b48-118">Creare un account di database</span><span class="sxs-lookup"><span data-stu-id="60b48-118">Create a database account</span></span>

<span data-ttu-id="60b48-119">Prima di poter creare un database di documenti, è necessario creare un account di database SQL (DocumentDB) con Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="60b48-119">Before you can create a document database, you need to create a SQL (DocumentDB) database account with Azure Cosmos DB.</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a><span data-ttu-id="60b48-120">Aggiungere una raccolta</span><span class="sxs-lookup"><span data-stu-id="60b48-120">Add a collection</span></span>

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

<a id="add-sample-data"></a>
## <a name="add-sample-data"></a><span data-ttu-id="60b48-121">Aggiungere dati di esempio</span><span class="sxs-lookup"><span data-stu-id="60b48-121">Add sample data</span></span>

<span data-ttu-id="60b48-122">È ora possibile aggiungere dati alla nuova raccolta usando Esplora dati.</span><span class="sxs-lookup"><span data-stu-id="60b48-122">You can now add data to your new collection using Data Explorer.</span></span>

1. <span data-ttu-id="60b48-123">In Esplora dati il nuovo database viene visualizzato nel riquadro Raccolte.</span><span class="sxs-lookup"><span data-stu-id="60b48-123">In Data Explorer, the new database appears in the Collections pane.</span></span> <span data-ttu-id="60b48-124">Espandere il database **Tasks**, espandere la raccolta **Items**, fare clic su **Documenti** e quindi su **Nuovo documento**.</span><span class="sxs-lookup"><span data-stu-id="60b48-124">Expand the **Tasks** database, expand the **Items** collection, click **Documents**, and then click **New Documents**.</span></span> 

   ![Creare nuovi documenti in Esplora dati nel portale di Azure](./media/create-documentdb-dotnet/azure-cosmosdb-data-explorer-new-document.png)
  
2. <span data-ttu-id="60b48-126">Aggiungere ora un documento alla raccolta con la struttura seguente.</span><span class="sxs-lookup"><span data-stu-id="60b48-126">Now add a document to the collection with the following structure.</span></span>

     ```json
     {
         "id": "1",
         "category": "personal",
         "name": "groceries",
         "description": "Pick up apples and strawberries.",
         "isComplete": false
     }
     ```

3. <span data-ttu-id="60b48-127">Dopo avere aggiunto il codice JSON alla scheda **Documenti**, fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="60b48-127">Once you've added the json to the **Documents** tab, click **Save**.</span></span>

    ![Copiare i dati JSON e fare clic su Salva in Esplora dati nel portale di Azure](./media/create-documentdb-dotnet/azure-cosmosdb-data-explorer-save-document.png)

4.  <span data-ttu-id="60b48-129">Creare e salvare un altro documento inserendo un valore univoco per la proprietà `id` e modificando le altre proprietà come si preferisce.</span><span class="sxs-lookup"><span data-stu-id="60b48-129">Create and save one more document where you insert a unique value for the `id` property, and change the other properties as you see fit.</span></span> <span data-ttu-id="60b48-130">I nuovi documenti possono avere la struttura desiderata, perché Azure Cosmos DB non impone alcuno schema per i dati.</span><span class="sxs-lookup"><span data-stu-id="60b48-130">Your new documents can have any structure you want as Azure Cosmos DB doesn't impose any schema on your data.</span></span>

     <span data-ttu-id="60b48-131">È ora possibile usare query in Esplora dati per recuperare i dati facendo clic sui pulsanti **Modifica filtro** e **Applica filtro**.</span><span class="sxs-lookup"><span data-stu-id="60b48-131">You can now use queries in Data Explorer to retrieve your data by clicking the **Edit Filter** and **Apply Filter** buttons.</span></span> <span data-ttu-id="60b48-132">Per impostazione predefinita, Esplora dati usa `SELECT * FROM c` per recuperare tutti i documenti della raccolta, ma è possibile usare una[query SQL](documentdb-sql-query.md) diversa, ad esempio `SELECT * FROM c ORDER BY c._ts DESC`, per restituire tutti i documenti in ordine decrescente in base al timestamp.</span><span class="sxs-lookup"><span data-stu-id="60b48-132">By default, Data Explorer uses `SELECT * FROM c` to retrieve all documents in the collection, but you can change that to a different [SQL query](documentdb-sql-query.md), such as `SELECT * FROM c ORDER BY c._ts DESC`, to return all the documents in descending order based on their timestamp.</span></span> 
 
     <span data-ttu-id="60b48-133">È anche possibile usare Esplora dati per creare stored procedure, funzioni definite dall'utente e trigger per eseguire la logica di business sul lato server e aumentare la velocità effettiva.</span><span class="sxs-lookup"><span data-stu-id="60b48-133">You can also use Data Explorer to create stored procedures, UDFs, and triggers to perform server-side business logic as well as scale throughput.</span></span> <span data-ttu-id="60b48-134">Esplora dati espone tutti i tipi di accesso ai dati a livello di codice predefiniti disponibili nelle API, ma consente anche di accedere facilmente ai dati nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="60b48-134">Data Explorer exposes all of the built-in programmatic data access available in the APIs, but provides easy access to your data in the Azure portal.</span></span>

## <a name="clone-the-sample-application"></a><span data-ttu-id="60b48-135">Clonare l'applicazione di esempio</span><span class="sxs-lookup"><span data-stu-id="60b48-135">Clone the sample application</span></span>

<span data-ttu-id="60b48-136">Si può ora passare a usare il codice.</span><span class="sxs-lookup"><span data-stu-id="60b48-136">Now let's switch to working with code.</span></span> <span data-ttu-id="60b48-137">Si clonerà un'app per le API DocumentDB da GitHub, si imposterà la stringa di connessione e la si eseguirà.</span><span class="sxs-lookup"><span data-stu-id="60b48-137">Let's clone a DocumentDB API app from GitHub, set the connection string, and run it.</span></span> <span data-ttu-id="60b48-138">Come si noterà, è facile usare i dati a livello di codice.</span><span class="sxs-lookup"><span data-stu-id="60b48-138">You see how easy it is to work with data programmatically.</span></span> 

1. <span data-ttu-id="60b48-139">Aprire una finestra del terminale Git, ad esempio Git Bash, ed eseguire il comando `CD` per passare a una directory di lavoro.</span><span class="sxs-lookup"><span data-stu-id="60b48-139">Open a git terminal window, such as git bash, and `CD` to a working directory.</span></span>  

2. <span data-ttu-id="60b48-140">Eseguire il comando seguente per clonare l'archivio di esempio.</span><span class="sxs-lookup"><span data-stu-id="60b48-140">Run the following command to clone the sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-documentdb-java-getting-started.git
    ```

## <a name="review-the-code"></a><span data-ttu-id="60b48-141">Esaminare il codice</span><span class="sxs-lookup"><span data-stu-id="60b48-141">Review the code</span></span>

<span data-ttu-id="60b48-142">Ecco una breve analisi di ciò che accade nell'app.</span><span class="sxs-lookup"><span data-stu-id="60b48-142">Let's make a quick review of what's happening in the app.</span></span> <span data-ttu-id="60b48-143">Aprire il file `Program.java` dalla cartella \src\GetStarted e trovare queste righe di codice che creano le risorse di Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="60b48-143">Open the `Program.java` file from the \src\GetStarted folder, and find these lines of code that create the Azure Cosmos DB resources.</span></span> 

* <span data-ttu-id="60b48-144">Viene inizializzato `DocumentClient`.</span><span class="sxs-lookup"><span data-stu-id="60b48-144">The `DocumentClient` is initialized.</span></span>

    ```java
    this.client = new DocumentClient("https://FILLME.documents.azure.com",
            "FILLME", 
            new ConnectionPolicy(),
            ConsistencyLevel.Session);
    ```

* <span data-ttu-id="60b48-145">Viene creato un nuovo database.</span><span class="sxs-lookup"><span data-stu-id="60b48-145">A new database is created.</span></span>

    ```java
    Database database = new Database();
    database.setId(databaseName);
    
    this.client.createDatabase(database, null);
    ```

* <span data-ttu-id="60b48-146">Viene creata una nuova raccolta.</span><span class="sxs-lookup"><span data-stu-id="60b48-146">A new collection is created.</span></span>

    ```java
    DocumentCollection collectionInfo = new DocumentCollection();
    collectionInfo.setId(collectionName);

    ...

    this.client.createCollection(databaseLink, collectionInfo, requestOptions);
    ```

* <span data-ttu-id="60b48-147">Vengono creati alcuni documenti.</span><span class="sxs-lookup"><span data-stu-id="60b48-147">Some documents are created.</span></span>

    ```java
    // Any Java object within your code can be serialized into JSON and written to Azure Cosmos DB
    Family andersenFamily = new Family();
    andersenFamily.setId("Andersen.1");
    andersenFamily.setLastName("Andersen");
    // More properties

    String collectionLink = String.format("/dbs/%s/colls/%s", databaseName, collectionName);
    this.client.createDocument(collectionLink, family, new RequestOptions(), true);
    ```

* <span data-ttu-id="60b48-148">Viene eseguita una query SQL su JSON.</span><span class="sxs-lookup"><span data-stu-id="60b48-148">A SQL query over JSON is performed.</span></span>

    ```java
    FeedOptions queryOptions = new FeedOptions();
    queryOptions.setPageSize(-1);
    queryOptions.setEnableCrossPartitionQuery(true);

    String collectionLink = String.format("/dbs/%s/colls/%s", databaseName, collectionName);
    FeedResponse<Document> queryResults = this.client.queryDocuments(
        collectionLink,
        "SELECT * FROM Family WHERE Family.lastName = 'Andersen'", queryOptions);

    System.out.println("Running SQL query...");
    for (Document family : queryResults.getQueryIterable()) {
        System.out.println(String.format("\tRead %s", family));
    }
    ```    

## <a name="update-your-connection-string"></a><span data-ttu-id="60b48-149">Aggiornare la stringa di connessione</span><span class="sxs-lookup"><span data-stu-id="60b48-149">Update your connection string</span></span>

<span data-ttu-id="60b48-150">Tornare ora al portale di Azure per recuperare le informazioni sulla stringa di connessione e copiarle nell'app.</span><span class="sxs-lookup"><span data-stu-id="60b48-150">Now go back to the Azure portal to get your connection string information and copy it into the app.</span></span> <span data-ttu-id="60b48-151">In questo modo l'app potrà comunicare con il database ospitato.</span><span class="sxs-lookup"><span data-stu-id="60b48-151">This will enable your app to communicate with your hosted database.</span></span>

1. <span data-ttu-id="60b48-152">Nell'account Azure Cosmos DB nel [portale di Azure](http://portal.azure.com/) fare clic su **Chiavi** nel riquadro di spostamento a sinistra e quindi su **Chiavi di lettura/scrittura**.</span><span class="sxs-lookup"><span data-stu-id="60b48-152">In the [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in the left navigation click **Keys**, and then click **Read-write Keys**.</span></span> <span data-ttu-id="60b48-153">Usare i pulsanti di copia sul lato destro dello schermo per copiare URI e CHIAVE PRIMARIA nel file `Program.java` nel passaggio seguente.</span><span class="sxs-lookup"><span data-stu-id="60b48-153">You'll use the copy buttons on the right side of the screen to copy the URI and PRIMARY KEY into the `Program.java` file in the next step.</span></span>

    ![Visualizzazione e copia di una chiave di accesso nel portale di Azure, pannello Chiavi](./media/create-documentdb-dotnet/keys.png)

2. <span data-ttu-id="60b48-155">Nel file `Program.java` aperto copiare il valore di URI dal portale (usando il pulsante di copia) e impostarlo come valore dell'endpoint del costruttore DocumentClient in `Program.java`.</span><span class="sxs-lookup"><span data-stu-id="60b48-155">In the open `Program.java` file, copy your URI value from the portal (using the copy button) and make it the value of the endpoint to the DocumentClient constructor in `Program.java`.</span></span> 

    `"https://FILLME.documents.azure.com"`

4. <span data-ttu-id="60b48-156">Copiare quindi il valore di CHIAVE PRIMARIA dal portale e incollarlo sopra "FILLME", come secondo parametro del costruttore DocumentClient.</span><span class="sxs-lookup"><span data-stu-id="60b48-156">Then copy your PRIMARY KEY value from the portal and paste it over “FILLME”, making it the second parameter in the DocumentClient constructor.</span></span> <span data-ttu-id="60b48-157">L'app è stata aggiornata con tutte le informazioni necessarie per comunicare con Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="60b48-157">You've now updated your app with all the info it needs to communicate with Azure Cosmos DB.</span></span> 
    
## <a name="run-the-app"></a><span data-ttu-id="60b48-158">Esecuzione dell'app</span><span class="sxs-lookup"><span data-stu-id="60b48-158">Run the app</span></span>

1. <span data-ttu-id="60b48-159">Nella finestra del terminale Git eseguire il comando `cd` per passare alla cartella azure-cosmos-db-documentdb-java-getting-started.</span><span class="sxs-lookup"><span data-stu-id="60b48-159">In the git terminal window, `cd` to the azure-cosmos-db-documentdb-java-getting-started folder.</span></span>

2. <span data-ttu-id="60b48-160">Nella finestra del terminale Git digitare `mvn package` per installare i pacchetti Java necessari.</span><span class="sxs-lookup"><span data-stu-id="60b48-160">In the git terminal window, type `mvn package` to install the required Java packages.</span></span>

3. <span data-ttu-id="60b48-161">Nella finestra del terminale Git eseguire `mvn exec:java -D exec.mainClass=GetStarted.Program` per avviare l'applicazione Java.</span><span class="sxs-lookup"><span data-stu-id="60b48-161">In the git terminal window, run `mvn exec:java -D exec.mainClass=GetStarted.Program` in the terminal window to start your Java application.</span></span>

    <span data-ttu-id="60b48-162">Nella finestra del terminale si riceverà la notifica che indica che il database FamilyDB è stato creato e in cui viene chiesto di premere un tasto per continuare.</span><span class="sxs-lookup"><span data-stu-id="60b48-162">In the terminal window, you'll receive notification that the FamilyDB database was created, and to press a key to continue.</span></span> <span data-ttu-id="60b48-163">Premere un tasto per creare il database, quindi passare a Esplora dati e osservare che ora contiene un database FamilyDB.</span><span class="sxs-lookup"><span data-stu-id="60b48-163">Press a key to create the database, then switch to the Data Explorer and you'll see that it now contains a FamilyDB database.</span></span> <span data-ttu-id="60b48-164">Continuare a premere i tasti per creare la raccolta e i documenti e quindi eseguire una query.</span><span class="sxs-lookup"><span data-stu-id="60b48-164">Continue to press keys to create the collection and the documents and then perform a query.</span></span> <span data-ttu-id="60b48-165">Quando viene completato il progetto, le risorse vengono eliminate dall'account.</span><span class="sxs-lookup"><span data-stu-id="60b48-165">When the project completes, the resources are deleted from your account.</span></span> 

    ![Visualizzazione e copia di una chiave di accesso nel portale di Azure, pannello Chiavi](./media/create-documentdb-java/console-output.png)


## <a name="review-slas-in-the-azure-portal"></a><span data-ttu-id="60b48-167">Esaminare i contratti di servizio nel portale di Azure</span><span class="sxs-lookup"><span data-stu-id="60b48-167">Review SLAs in the Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="60b48-168">Pulire le risorse</span><span class="sxs-lookup"><span data-stu-id="60b48-168">Clean up resources</span></span>

<span data-ttu-id="60b48-169">Se non si intende continuare a usare l'app, eliminare tutte le risorse create tramite questa guida di avvio rapido nel portale di Azure eseguendo questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="60b48-169">If you're not going to continue to use this app, delete all resources created by this quickstart in the Azure portal with the following steps:</span></span>

1. <span data-ttu-id="60b48-170">Scegliere **Gruppi di risorse** dal menu a sinistra del portale di Azure e quindi fare clic sul nome della risorsa creata.</span><span class="sxs-lookup"><span data-stu-id="60b48-170">From the left-hand menu in the Azure portal, click **Resource groups** and then click the name of the resource you created.</span></span> 
2. <span data-ttu-id="60b48-171">Nella pagina del gruppo di risorse fare clic su **Elimina**, digitare il nome della risorsa da eliminare nella casella di testo e quindi fare clic su **Elimina**.</span><span class="sxs-lookup"><span data-stu-id="60b48-171">On your resource group page, click **Delete**, type the name of the resource to delete in the text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="60b48-172">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="60b48-172">Next steps</span></span>

<span data-ttu-id="60b48-173">In questa guida di avvio rapido si è appreso come creare un account Azure Cosmos DB, un database di documenti e una raccolta usando Esplora dati e come creare eseguire un'app per ottenere lo stesso risultato a livello di codice.</span><span class="sxs-lookup"><span data-stu-id="60b48-173">In this quickstart, you've learned how to create an Azure Cosmos DB account, document database, and collection using the Data Explorer, and run an app to do the same thing programmatically.</span></span> <span data-ttu-id="60b48-174">È ora possibile importare dati aggiuntivi nell'account Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="60b48-174">You can now import additional data to your Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="60b48-175">Importare dati in Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="60b48-175">Import data into Azure Cosmos DB</span></span>](import-data.md)


