---
title: 'Azure Cosmos DB: Creare un''app console con Java e l''API MongoDB | Microsoft Docs'
description: Presenta un esempio di codice Java che permette di connettersi all'API MongoDB di Azure Cosmos DB ed eseguire query su di essa
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
ms.devlang: java
ms.topic: hero-article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: f84294d7d324f094d173f7a2ec89759266a74210
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cosmos-db-build-a-mongodb-api-console-app-with-java-and-the-azure-portal"></a><span data-ttu-id="216c7-103">Azure Cosmos DB: Creare un'app console API MongoDB con Java e il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="216c7-103">Azure Cosmos DB: Build a MongoDB API console app with Java and the Azure portal</span></span>

<span data-ttu-id="216c7-104">Azure Cosmos DB è il servizio di database multimodello distribuito a livello globale di Microsoft.</span><span class="sxs-lookup"><span data-stu-id="216c7-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="216c7-105">È possibile creare ed eseguire rapidamente query su database di documenti, coppie chiave/valore e grafi, sfruttando in ognuno dei casi i vantaggi offerti dalle funzionalità di scalabilità orizzontale e distribuzione globale alla base di Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="216c7-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="216c7-106">Questa guida di avvio rapido mostra come creare un account, un database di documenti e una raccolta di Azure Cosmos DB tramite il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="216c7-106">This quick start demonstrates how to create an Azure Cosmos DB account, document database, and collection using the Azure portal.</span></span> <span data-ttu-id="216c7-107">Si creerà e distribuirà quindi un'app console basata sul [driver Java MongoDB](https://docs.mongodb.com/ecosystem/drivers/java/).</span><span class="sxs-lookup"><span data-stu-id="216c7-107">You'll then build and deploy a console app built on the [MongoDB Java driver](https://docs.mongodb.com/ecosystem/drivers/java/).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="216c7-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="216c7-108">Prerequisites</span></span>

* <span data-ttu-id="216c7-109">Prima di poter eseguire questo esempio, è necessario soddisfare i prerequisiti seguenti:</span><span class="sxs-lookup"><span data-stu-id="216c7-109">Before you can run this sample, you must have the following prerequisites:</span></span>
   * <span data-ttu-id="216c7-110">JDK 1.7+ (eseguire `apt-get install default-jdk` se JDK non è disponibile)</span><span class="sxs-lookup"><span data-stu-id="216c7-110">JDK 1.7+ (Run `apt-get install default-jdk` if you don't have JDK)</span></span>
   * <span data-ttu-id="216c7-111">Maven (eseguire `apt-get install maven` se Maven non è disponibile)</span><span class="sxs-lookup"><span data-stu-id="216c7-111">Maven (Run `apt-get install maven` if you don't have Maven)</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="216c7-112">Creare un account di database</span><span class="sxs-lookup"><span data-stu-id="216c7-112">Create a database account</span></span>

[!INCLUDE [mongodb-create-dbaccount](../../includes/cosmos-db-create-dbaccount-mongodb.md)]

## <a name="add-a-collection"></a><span data-ttu-id="216c7-113">Aggiungere una raccolta</span><span class="sxs-lookup"><span data-stu-id="216c7-113">Add a collection</span></span>

<span data-ttu-id="216c7-114">Assegnare un nome al nuovo database, **db**, e alla nuova raccolta, **coll**.</span><span class="sxs-lookup"><span data-stu-id="216c7-114">Name your new database, **db**, and your new collection, **coll**.</span></span>

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

## <a name="clone-the-sample-application"></a><span data-ttu-id="216c7-115">Clonare l'applicazione di esempio</span><span class="sxs-lookup"><span data-stu-id="216c7-115">Clone the sample application</span></span>

<span data-ttu-id="216c7-116">Clonare ora un'app per le API MongoDB da GitHub, impostare la stringa di connessione ed eseguirla.</span><span class="sxs-lookup"><span data-stu-id="216c7-116">Now let's clone a MongoDB API app from github, set the connection string, and run it.</span></span> <span data-ttu-id="216c7-117">Come si noterà, è facile usare i dati a livello di codice.</span><span class="sxs-lookup"><span data-stu-id="216c7-117">You'll see how easy it is to work with data programmatically.</span></span> 

1. <span data-ttu-id="216c7-118">Aprire una finestra del terminale Git, ad esempio Git Bash, ed eseguire il comando `cd` per passare a una directory di lavoro.</span><span class="sxs-lookup"><span data-stu-id="216c7-118">Open a git terminal window, such as git bash, and `cd` to a working directory.</span></span>  

2. <span data-ttu-id="216c7-119">Eseguire il comando seguente per clonare l'archivio di esempio.</span><span class="sxs-lookup"><span data-stu-id="216c7-119">Run the following command to clone the sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-mongodb-java-getting-started.git
    ```

3. <span data-ttu-id="216c7-120">Aprire quindi il file della soluzione in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="216c7-120">Then open the solution file in Visual Studio.</span></span> 

## <a name="review-the-code"></a><span data-ttu-id="216c7-121">Esaminare il codice</span><span class="sxs-lookup"><span data-stu-id="216c7-121">Review the code</span></span>

<span data-ttu-id="216c7-122">Ecco una breve analisi di ciò che accade nell'app.</span><span class="sxs-lookup"><span data-stu-id="216c7-122">Let's make a quick review of what's happening in the app.</span></span> <span data-ttu-id="216c7-123">Aprire il file `Program.cs`. Come si noterà, queste righe di codice creano le risorse di Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="216c7-123">Open the `Program.cs` file and you'll find that these lines of code create the Azure Cosmos DB resources.</span></span> 

* <span data-ttu-id="216c7-124">Viene inizializzato DocumentClient.</span><span class="sxs-lookup"><span data-stu-id="216c7-124">The DocumentClient is initialized.</span></span>

    ```java
    MongoClientURI uri = new MongoClientURI("FILLME");`

    MongoClient mongoClient = new MongoClient(uri);            
    ```

* <span data-ttu-id="216c7-125">Vengono creati un nuovo database e una nuova raccolta.</span><span class="sxs-lookup"><span data-stu-id="216c7-125">A new database and collection are created.</span></span>

    ```java
    MongoDatabase database = mongoClient.getDatabase("db");

    MongoCollection<Document> collection = database.getCollection("coll");
    ```

* <span data-ttu-id="216c7-126">Vengono inseriti alcuni documenti usando `MongoCollection.insertOne`</span><span class="sxs-lookup"><span data-stu-id="216c7-126">Some documents are inserted using `MongoCollection.insertOne`</span></span>

    ```java
    Document document = new Document("fruit", "apple")
    collection.insertOne(document);
    ```

* <span data-ttu-id="216c7-127">Vengono eseguite alcune query usando `MongoCollection.find`</span><span class="sxs-lookup"><span data-stu-id="216c7-127">Some queries are performed using `MongoCollection.find`</span></span>

    ```java
    Document queryResult = collection.find(Filters.eq("fruit", "apple")).first();
    System.out.println(queryResult.toJson());       
    ```

## <a name="update-your-connection-string"></a><span data-ttu-id="216c7-128">Aggiornare la stringa di connessione</span><span class="sxs-lookup"><span data-stu-id="216c7-128">Update your connection string</span></span>

<span data-ttu-id="216c7-129">Tornare ora al portale di Azure per recuperare le informazioni sulla stringa di connessione e copiarle nell'app.</span><span class="sxs-lookup"><span data-stu-id="216c7-129">Now go back to the Azure portal to get your connection string information and copy it into the app.</span></span>

1. <span data-ttu-id="216c7-130">Dall'account, selezionare **Avvio rapido**, selezionare Java e quindi copiare la stringa di connessione negli Appunti</span><span class="sxs-lookup"><span data-stu-id="216c7-130">From the Account, select **Quick Start**, select Java, then copy the connection string to your clipboard</span></span>

2. <span data-ttu-id="216c7-131">Aprire il file `Program.java`, sostituire l'argomento del costruttore MongoClientURI con la stringa di connessione.</span><span class="sxs-lookup"><span data-stu-id="216c7-131">Open the `Program.java` file, replace the argument to the MongoClientURI constructor with the connection string.</span></span> <span data-ttu-id="216c7-132">L'app è stata aggiornata con tutte le informazioni necessarie per comunicare con Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="216c7-132">You've now updated your app with all the info it needs to communicate with Azure Cosmos DB.</span></span> 
    
## <a name="run-the-console-app"></a><span data-ttu-id="216c7-133">Eseguire l'app console</span><span class="sxs-lookup"><span data-stu-id="216c7-133">Run the console app</span></span>

1. <span data-ttu-id="216c7-134">Eseguire `mvn package` in un terminale per installare i moduli npm necessari</span><span class="sxs-lookup"><span data-stu-id="216c7-134">Run `mvn package` in a terminal to install required npm modules</span></span>

2. <span data-ttu-id="216c7-135">Eseguire `mvn exec:java -D exec.mainClass=GetStarted.Program` in un terminale per avviare l'applicazione Java.</span><span class="sxs-lookup"><span data-stu-id="216c7-135">Run `mvn exec:java -D exec.mainClass=GetStarted.Program` in a terminal to start your Java application.</span></span>

<span data-ttu-id="216c7-136">È ora possibile usare [Robomongo](mongodb-robomongo.md) / [Studio 3T](mongodb-mongochef.md) per modificare e usare i nuovi dati, nonché eseguire query su di essi.</span><span class="sxs-lookup"><span data-stu-id="216c7-136">You can now use [Robomongo](mongodb-robomongo.md) / [Studio 3T](mongodb-mongochef.md) to query, modify, and work with this new data.</span></span>

## <a name="review-slas-in-the-azure-portal"></a><span data-ttu-id="216c7-137">Esaminare i contratti di servizio nel portale di Azure</span><span class="sxs-lookup"><span data-stu-id="216c7-137">Review SLAs in the Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="216c7-138">Pulire le risorse</span><span class="sxs-lookup"><span data-stu-id="216c7-138">Clean up resources</span></span>

<span data-ttu-id="216c7-139">Se non si intende continuare a usare l'app, eliminare tutte le risorse create tramite questa guida di avvio rapido nel portale di Azure eseguendo questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="216c7-139">If you're not going to continue to use this app, delete all resources created by this quickstart in the Azure portal with the following steps:</span></span>

1. <span data-ttu-id="216c7-140">Scegliere **Gruppi di risorse** dal menu a sinistra del portale di Azure e quindi fare clic sul nome della risorsa creata.</span><span class="sxs-lookup"><span data-stu-id="216c7-140">From the left-hand menu in the Azure portal, click **Resource groups** and then click the name of the resource you created.</span></span> 
2. <span data-ttu-id="216c7-141">Nella pagina del gruppo di risorse fare clic su **Elimina**, digitare il nome della risorsa da eliminare nella casella di testo e quindi fare clic su **Elimina**.</span><span class="sxs-lookup"><span data-stu-id="216c7-141">On your resource group page, click **Delete**, type the name of the resource to delete in the text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="216c7-142">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="216c7-142">Next steps</span></span>

<span data-ttu-id="216c7-143">In questa guida di avvio rapido si è appreso come creare un account Azure Cosmos DB, come creare una raccolta con Esplora dati e come eseguire un'app console.</span><span class="sxs-lookup"><span data-stu-id="216c7-143">In this quickstart, you've learned how to create an Azure Cosmos DB account, create a collection using the Data Explorer, and run a console app.</span></span> <span data-ttu-id="216c7-144">È ora possibile importare dati aggiuntivi nell'account Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="216c7-144">You can now import additional data to your Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="216c7-145">Importare i dati di MongoDB in Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="216c7-145">Import MongoDB data into Azure Cosmos DB</span></span>](mongodb-migrate.md)


