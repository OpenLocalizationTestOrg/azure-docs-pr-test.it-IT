---
title: un database di documenti DB Cosmos Azure con Java aaaCreate | Documenti Microsoft | Microsoft documenti
description: "Visualizza un esempio di codice Java è possibile utilizzare query tooand tooconnect hello Azure Cosmos DB DocumentDB API"
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
ms.openlocfilehash: 400c9e7780034d3e28d749e734786e950edad22f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-create-a-document-database-using-java-and-hello-azure-portal"></a><span data-ttu-id="28ed7-103">DB Cosmos Azure: Creare un database di documenti tramite Java e hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="28ed7-103">Azure Cosmos DB: Create a document database using Java and hello Azure portal</span></span>

<span data-ttu-id="28ed7-104">Azure Cosmos DB è il servizio di database multimodello distribuito a livello globale di Microsoft.</span><span class="sxs-lookup"><span data-stu-id="28ed7-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="28ed7-105">Creare rapidamente e query chiave/valore, il documento e database grafico, ognuno dei quali trarre vantaggio dalla distribuzione globale hello e funzionalità di scalabilità orizzontale di base di Azure Cosmos DB hello.</span><span class="sxs-lookup"><span data-stu-id="28ed7-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="28ed7-106">Questa Guida rapida viene creato un documento utilizzando database hello gli strumenti del portale di Azure per Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="28ed7-106">This quickstart creates a document database using hello Azure portal tools for Azure Cosmos DB.</span></span> <span data-ttu-id="28ed7-107">Questa Guida rapida illustra anche come tooquickly creare un'applicazione console Java utilizzando hello [API Java di DocumentDB](documentdb-sdk-java.md).</span><span class="sxs-lookup"><span data-stu-id="28ed7-107">This quickstart also shows you how tooquickly create a Java console app using hello [DocumentDB Java API](documentdb-sdk-java.md).</span></span> <span data-ttu-id="28ed7-108">istruzioni di Hello in questa Guida rapida possono essere seguite in qualsiasi sistema operativo che è in grado di eseguire Java.</span><span class="sxs-lookup"><span data-stu-id="28ed7-108">hello instructions in this quickstart can be followed on any operating system that is capable of running Java.</span></span> <span data-ttu-id="28ed7-109">Completando questa Guida rapida sarà familiarità con la creazione e la modifica delle risorse di database di documenti in hello dell'interfaccia utente o a livello di codice, a seconda del valore è la preferenza.</span><span class="sxs-lookup"><span data-stu-id="28ed7-109">By completing this quickstart you'll be familiar with creating and modifying document database resources in either hello UI or programatically, whichever is your preference.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="28ed7-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="28ed7-110">Prerequisites</span></span>

* [<span data-ttu-id="28ed7-111">Java Development Kit (JDK) 1.7+</span><span class="sxs-lookup"><span data-stu-id="28ed7-111">Java Development Kit (JDK) 1.7+</span></span>](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
    * <span data-ttu-id="28ed7-112">In Ubuntu, eseguire `apt-get install default-jdk` tooinstall hello JDK.</span><span class="sxs-lookup"><span data-stu-id="28ed7-112">On Ubuntu, run `apt-get install default-jdk` tooinstall hello JDK.</span></span>
    * <span data-ttu-id="28ed7-113">Essere tooset che hello JAVA_HOME ambiente variabile toopoint toohello cartella in cui è installato hello JDK.</span><span class="sxs-lookup"><span data-stu-id="28ed7-113">Be sure tooset hello JAVA_HOME environment variable toopoint toohello folder where hello JDK is installed.</span></span>
* <span data-ttu-id="28ed7-114">[Scaricare](http://maven.apache.org/download.cgi) e [installare](http://maven.apache.org/install.html) un archivio binario [Maven](http://maven.apache.org/)</span><span class="sxs-lookup"><span data-stu-id="28ed7-114">[Download](http://maven.apache.org/download.cgi) and [install](http://maven.apache.org/install.html) a [Maven](http://maven.apache.org/) binary archive</span></span>
    * <span data-ttu-id="28ed7-115">In Ubuntu, è possibile eseguire `apt-get install maven` tooinstall Maven.</span><span class="sxs-lookup"><span data-stu-id="28ed7-115">On Ubuntu, you can run `apt-get install maven` tooinstall Maven.</span></span>
* [<span data-ttu-id="28ed7-116">Git</span><span class="sxs-lookup"><span data-stu-id="28ed7-116">Git</span></span>](https://www.git-scm.com/)
    * <span data-ttu-id="28ed7-117">In Ubuntu, è possibile eseguire `sudo apt-get install git` tooinstall Git.</span><span class="sxs-lookup"><span data-stu-id="28ed7-117">On Ubuntu, you can run `sudo apt-get install git` tooinstall Git.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="28ed7-118">Creare un account di database</span><span class="sxs-lookup"><span data-stu-id="28ed7-118">Create a database account</span></span>

<span data-ttu-id="28ed7-119">Prima di creare un database di documenti, è necessario un account di database SQL (DocumentDB) con Azure Cosmos DB toocreate.</span><span class="sxs-lookup"><span data-stu-id="28ed7-119">Before you can create a document database, you need toocreate a SQL (DocumentDB) database account with Azure Cosmos DB.</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a><span data-ttu-id="28ed7-120">Aggiungere una raccolta</span><span class="sxs-lookup"><span data-stu-id="28ed7-120">Add a collection</span></span>

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

<a id="add-sample-data"></a>
## <a name="add-sample-data"></a><span data-ttu-id="28ed7-121">Aggiungere dati di esempio</span><span class="sxs-lookup"><span data-stu-id="28ed7-121">Add sample data</span></span>

<span data-ttu-id="28ed7-122">È ora possibile aggiungere una nuova raccolta utilizzando Esplora dati tooyour dati.</span><span class="sxs-lookup"><span data-stu-id="28ed7-122">You can now add data tooyour new collection using Data Explorer.</span></span>

1. <span data-ttu-id="28ed7-123">In Esplora dati hello nuovo database verrà visualizzato nel riquadro raccolte hello.</span><span class="sxs-lookup"><span data-stu-id="28ed7-123">In Data Explorer, hello new database appears in hello Collections pane.</span></span> <span data-ttu-id="28ed7-124">Espandere hello **attività** del database, espandere hello **elementi** raccolta, fare clic su **documenti**, quindi fare clic su **nuovi documenti**.</span><span class="sxs-lookup"><span data-stu-id="28ed7-124">Expand hello **Tasks** database, expand hello **Items** collection, click **Documents**, and then click **New Documents**.</span></span> 

   ![Creare nuovi documenti in Esplora dati nel portale di Azure hello](./media/create-documentdb-dotnet/azure-cosmosdb-data-explorer-new-document.png)
  
2. <span data-ttu-id="28ed7-126">Ora è possibile aggiungere una raccolta di documenti toohello con hello seguente struttura.</span><span class="sxs-lookup"><span data-stu-id="28ed7-126">Now add a document toohello collection with hello following structure.</span></span>

     ```json
     {
         "id": "1",
         "category": "personal",
         "name": "groceries",
         "description": "Pick up apples and strawberries.",
         "isComplete": false
     }
     ```

3. <span data-ttu-id="28ed7-127">Dopo aver aggiunto hello json toohello **documenti** scheda, fare clic su **salvare**.</span><span class="sxs-lookup"><span data-stu-id="28ed7-127">Once you've added hello json toohello **Documents** tab, click **Save**.</span></span>

    ![Copiare i dati json e fare clic su Salva in Esplora dati nel portale di Azure hello](./media/create-documentdb-dotnet/azure-cosmosdb-data-explorer-save-document.png)

4.  <span data-ttu-id="28ed7-129">Creare e salvare un documento più in cui si inserisce un valore univoco per hello `id` proprietà e modificare hello altre proprietà nel modo desiderato.</span><span class="sxs-lookup"><span data-stu-id="28ed7-129">Create and save one more document where you insert a unique value for hello `id` property, and change hello other properties as you see fit.</span></span> <span data-ttu-id="28ed7-130">I nuovi documenti possono avere la struttura desiderata, perché Azure Cosmos DB non impone alcuno schema per i dati.</span><span class="sxs-lookup"><span data-stu-id="28ed7-130">Your new documents can have any structure you want as Azure Cosmos DB doesn't impose any schema on your data.</span></span>

     <span data-ttu-id="28ed7-131">È possibile utilizzare le query in Esplora dati tooretrieve i dati facendo clic su hello **Modifica filtro** e **Applica filtro** pulsanti.</span><span class="sxs-lookup"><span data-stu-id="28ed7-131">You can now use queries in Data Explorer tooretrieve your data by clicking hello **Edit Filter** and **Apply Filter** buttons.</span></span> <span data-ttu-id="28ed7-132">Per impostazione predefinita, si utilizza Esplora dati `SELECT * FROM c` tooretrieve tutti i documenti nella raccolta di hello, ma è possibile modificare tale tooa diversi [query SQL](documentdb-sql-query.md), ad esempio `SELECT * FROM c ORDER BY c._ts DESC`, tooreturn tutti i documenti hello in ordine decrescente in base a al relativo timestamp.</span><span class="sxs-lookup"><span data-stu-id="28ed7-132">By default, Data Explorer uses `SELECT * FROM c` tooretrieve all documents in hello collection, but you can change that tooa different [SQL query](documentdb-sql-query.md), such as `SELECT * FROM c ORDER BY c._ts DESC`, tooreturn all hello documents in descending order based on their timestamp.</span></span> 
 
     <span data-ttu-id="28ed7-133">È inoltre possibile utilizzare Esplora dati toocreate stored procedure, funzioni definite dall'utente e anche logica di business sul lato server tooperform trigger come velocità effettiva di scala.</span><span class="sxs-lookup"><span data-stu-id="28ed7-133">You can also use Data Explorer toocreate stored procedures, UDFs, and triggers tooperform server-side business logic as well as scale throughput.</span></span> <span data-ttu-id="28ed7-134">Esplora dati espone tutti hello predefinite a livello di codice l'accesso ai dati disponibile in hello API, ma fornisce un accesso semplice tooyour dati hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="28ed7-134">Data Explorer exposes all of hello built-in programmatic data access available in hello APIs, but provides easy access tooyour data in hello Azure portal.</span></span>

## <a name="clone-hello-sample-application"></a><span data-ttu-id="28ed7-135">Applicazione di esempio hello clonare</span><span class="sxs-lookup"><span data-stu-id="28ed7-135">Clone hello sample application</span></span>

<span data-ttu-id="28ed7-136">Ora si passa tooworking con il codice.</span><span class="sxs-lookup"><span data-stu-id="28ed7-136">Now let's switch tooworking with code.</span></span> <span data-ttu-id="28ed7-137">Si clona una app per le API DocumentDB da GitHub, impostare la stringa di connessione hello ed eseguirlo.</span><span class="sxs-lookup"><span data-stu-id="28ed7-137">Let's clone a DocumentDB API app from GitHub, set hello connection string, and run it.</span></span> <span data-ttu-id="28ed7-138">Viene visualizzato quanto sia facile toowork con i dati a livello di codice.</span><span class="sxs-lookup"><span data-stu-id="28ed7-138">You see how easy it is toowork with data programmatically.</span></span> 

1. <span data-ttu-id="28ed7-139">Aprire una finestra terminale git, ad esempio git bash, e `CD` tooa directory di lavoro.</span><span class="sxs-lookup"><span data-stu-id="28ed7-139">Open a git terminal window, such as git bash, and `CD` tooa working directory.</span></span>  

2. <span data-ttu-id="28ed7-140">Eseguire hello seguenti repository di esempio di comando tooclone hello.</span><span class="sxs-lookup"><span data-stu-id="28ed7-140">Run hello following command tooclone hello sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-documentdb-java-getting-started.git
    ```

## <a name="review-hello-code"></a><span data-ttu-id="28ed7-141">Esaminare il codice hello</span><span class="sxs-lookup"><span data-stu-id="28ed7-141">Review hello code</span></span>

<span data-ttu-id="28ed7-142">Questo punto, eseguire una rapida panoramica delle operazioni eseguite nell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="28ed7-142">Let's make a quick review of what's happening in hello app.</span></span> <span data-ttu-id="28ed7-143">Aprire hello `Program.java` file dalla cartella \src\GetStarted hello e trovare le righe di codice che creano hello risorse Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="28ed7-143">Open hello `Program.java` file from hello \src\GetStarted folder, and find these lines of code that create hello Azure Cosmos DB resources.</span></span> 

* <span data-ttu-id="28ed7-144">Hello `DocumentClient` viene inizializzato.</span><span class="sxs-lookup"><span data-stu-id="28ed7-144">hello `DocumentClient` is initialized.</span></span>

    ```java
    this.client = new DocumentClient("https://FILLME.documents.azure.com",
            "FILLME", 
            new ConnectionPolicy(),
            ConsistencyLevel.Session);
    ```

* <span data-ttu-id="28ed7-145">Viene creato un nuovo database.</span><span class="sxs-lookup"><span data-stu-id="28ed7-145">A new database is created.</span></span>

    ```java
    Database database = new Database();
    database.setId(databaseName);
    
    this.client.createDatabase(database, null);
    ```

* <span data-ttu-id="28ed7-146">Viene creata una nuova raccolta.</span><span class="sxs-lookup"><span data-stu-id="28ed7-146">A new collection is created.</span></span>

    ```java
    DocumentCollection collectionInfo = new DocumentCollection();
    collectionInfo.setId(collectionName);

    ...

    this.client.createCollection(databaseLink, collectionInfo, requestOptions);
    ```

* <span data-ttu-id="28ed7-147">Vengono creati alcuni documenti.</span><span class="sxs-lookup"><span data-stu-id="28ed7-147">Some documents are created.</span></span>

    ```java
    // Any Java object within your code can be serialized into JSON and written tooAzure Cosmos DB
    Family andersenFamily = new Family();
    andersenFamily.setId("Andersen.1");
    andersenFamily.setLastName("Andersen");
    // More properties

    String collectionLink = String.format("/dbs/%s/colls/%s", databaseName, collectionName);
    this.client.createDocument(collectionLink, family, new RequestOptions(), true);
    ```

* <span data-ttu-id="28ed7-148">Viene eseguita una query SQL su JSON.</span><span class="sxs-lookup"><span data-stu-id="28ed7-148">A SQL query over JSON is performed.</span></span>

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

## <a name="update-your-connection-string"></a><span data-ttu-id="28ed7-149">Aggiornare la stringa di connessione</span><span class="sxs-lookup"><span data-stu-id="28ed7-149">Update your connection string</span></span>

<span data-ttu-id="28ed7-150">Tornare toohello tooget portale Azure le informazioni sulla stringa di connessione e copiarla in app hello.</span><span class="sxs-lookup"><span data-stu-id="28ed7-150">Now go back toohello Azure portal tooget your connection string information and copy it into hello app.</span></span> <span data-ttu-id="28ed7-151">In questo modo il toocommunicate app con il database di hosting.</span><span class="sxs-lookup"><span data-stu-id="28ed7-151">This will enable your app toocommunicate with your hosted database.</span></span>

1. <span data-ttu-id="28ed7-152">In hello [portale di Azure](http://portal.azure.com/)il Cosmos Azure DB account, nel riquadro di spostamento sinistro hello fare clic su **chiavi**, quindi fare clic su **le chiavi di lettura / scrittura**.</span><span class="sxs-lookup"><span data-stu-id="28ed7-152">In hello [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in hello left navigation click **Keys**, and then click **Read-write Keys**.</span></span> <span data-ttu-id="28ed7-153">È possibile usare i pulsanti copia hello per il lato destro hello di hello toocopy di hello schermata URI e chiave primaria in hello `Program.java` file nel passaggio successivo hello.</span><span class="sxs-lookup"><span data-stu-id="28ed7-153">You'll use hello copy buttons on hello right side of hello screen toocopy hello URI and PRIMARY KEY into hello `Program.java` file in hello next step.</span></span>

    ![Visualizzare e copiare una chiave di accesso nel portale di Azure hello, pannello di chiavi](./media/create-documentdb-dotnet/keys.png)

2. <span data-ttu-id="28ed7-155">In aprire hello `Program.java` file, copiare il valore dell'URI dal portale di hello (con il pulsante di copia hello) e renderla hello valore hello endpoint toohello DocumentClient costruttore `Program.java`.</span><span class="sxs-lookup"><span data-stu-id="28ed7-155">In hello open `Program.java` file, copy your URI value from hello portal (using hello copy button) and make it hello value of hello endpoint toohello DocumentClient constructor in `Program.java`.</span></span> 

    `"https://FILLME.documents.azure.com"`

4. <span data-ttu-id="28ed7-156">Quindi copiare il valore di chiave primaria dal portale di hello e incollarla su "FILLME", rendendo hello secondo parametro nel costruttore DocumentClient hello.</span><span class="sxs-lookup"><span data-stu-id="28ed7-156">Then copy your PRIMARY KEY value from hello portal and paste it over “FILLME”, making it hello second parameter in hello DocumentClient constructor.</span></span> <span data-ttu-id="28ed7-157">È stato aggiornato a questo punto l'app con tutte le informazioni di hello deve toocommunicate con Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="28ed7-157">You've now updated your app with all hello info it needs toocommunicate with Azure Cosmos DB.</span></span> 
    
## <a name="run-hello-app"></a><span data-ttu-id="28ed7-158">Eseguire app hello</span><span class="sxs-lookup"><span data-stu-id="28ed7-158">Run hello app</span></span>

1. <span data-ttu-id="28ed7-159">Nella finestra terminale git hello, `cd` toohello azure-cosmos-db-documentdb-java-getting-started cartella.</span><span class="sxs-lookup"><span data-stu-id="28ed7-159">In hello git terminal window, `cd` toohello azure-cosmos-db-documentdb-java-getting-started folder.</span></span>

2. <span data-ttu-id="28ed7-160">Nella finestra terminal git hello, digitare `mvn package` tooinstall hello necessari pacchetti Java.</span><span class="sxs-lookup"><span data-stu-id="28ed7-160">In hello git terminal window, type `mvn package` tooinstall hello required Java packages.</span></span>

3. <span data-ttu-id="28ed7-161">Nella finestra terminale di hello git, eseguire `mvn exec:java -D exec.mainClass=GetStarted.Program` hello finestra terminale toostart l'applicazione Java.</span><span class="sxs-lookup"><span data-stu-id="28ed7-161">In hello git terminal window, run `mvn exec:java -D exec.mainClass=GetStarted.Program` in hello terminal window toostart your Java application.</span></span>

    <span data-ttu-id="28ed7-162">Nella finestra terminal hello, si riceverà la notifica che hello FamilyDB database è stato creato e toopress toocontinue una chiave.</span><span class="sxs-lookup"><span data-stu-id="28ed7-162">In hello terminal window, you'll receive notification that hello FamilyDB database was created, and toopress a key toocontinue.</span></span> <span data-ttu-id="28ed7-163">Premere un database di hello toocreate chiave, quindi passare toohello Esplora dati e si noterà che ora contiene un database FamilyDB.</span><span class="sxs-lookup"><span data-stu-id="28ed7-163">Press a key toocreate hello database, then switch toohello Data Explorer and you'll see that it now contains a FamilyDB database.</span></span> <span data-ttu-id="28ed7-164">Continuare toopress chiavi toocreate hello hello e raccolta documenti e quindi eseguire una query.</span><span class="sxs-lookup"><span data-stu-id="28ed7-164">Continue toopress keys toocreate hello collection and hello documents and then perform a query.</span></span> <span data-ttu-id="28ed7-165">Al termine del progetto hello, vengono eliminate le risorse di hello dal tuo account.</span><span class="sxs-lookup"><span data-stu-id="28ed7-165">When hello project completes, hello resources are deleted from your account.</span></span> 

    ![Visualizzare e copiare una chiave di accesso nel portale di Azure hello, pannello di chiavi](./media/create-documentdb-java/console-output.png)


## <a name="review-slas-in-hello-azure-portal"></a><span data-ttu-id="28ed7-167">Esaminare i contratti di servizio nel portale di Azure hello</span><span class="sxs-lookup"><span data-stu-id="28ed7-167">Review SLAs in hello Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="28ed7-168">Pulire le risorse</span><span class="sxs-lookup"><span data-stu-id="28ed7-168">Clean up resources</span></span>

<span data-ttu-id="28ed7-169">Se non si ha intenzione toocontinue toouse questa app, eliminare tutte le risorse create da questa Guida rapida hello portale di Azure con hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="28ed7-169">If you're not going toocontinue toouse this app, delete all resources created by this quickstart in hello Azure portal with hello following steps:</span></span>

1. <span data-ttu-id="28ed7-170">Dal menu a sinistra di hello in hello portale di Azure, fare clic su **gruppi di risorse** e quindi fare clic su nome hello della risorsa di hello è stato creato.</span><span class="sxs-lookup"><span data-stu-id="28ed7-170">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span> 
2. <span data-ttu-id="28ed7-171">Nella pagina di gruppo di risorse, fare clic su **eliminare**, digitare il nome di hello di hello risorsa toodelete nella casella di testo hello e quindi fare clic su **eliminare**.</span><span class="sxs-lookup"><span data-stu-id="28ed7-171">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="28ed7-172">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="28ed7-172">Next steps</span></span>

<span data-ttu-id="28ed7-173">In questa Guida rapida, si è appreso come toocreate un account Azure Cosmos DB, database di documenti e raccolta utilizzando Esplora dati hello ed eseguire un toodo app hello stessa operazione a livello di codice.</span><span class="sxs-lookup"><span data-stu-id="28ed7-173">In this quickstart, you've learned how toocreate an Azure Cosmos DB account, document database, and collection using hello Data Explorer, and run an app toodo hello same thing programmatically.</span></span> <span data-ttu-id="28ed7-174">È ora possibile importare account Cosmos DB tooyour di dati aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="28ed7-174">You can now import additional data tooyour Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="28ed7-175">Importare dati in Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="28ed7-175">Import data into Azure Cosmos DB</span></span>](import-data.md)


