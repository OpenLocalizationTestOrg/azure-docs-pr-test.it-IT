---
title: 'Azure Cosmos DB: Compilare un''applicazione console con Java e hello MongoDB API | Documenti Microsoft'
description: "Visualizza un esempio di codice Java è possibile utilizzare query tooand tooconnect hello Azure Cosmos DB MongoDB API"
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
ms.openlocfilehash: fbe416f6b20ed2bb83a1d41eb70ffc6e3cee2b61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-mongodb-api-console-app-with-java-and-hello-azure-portal"></a><span data-ttu-id="ffd5f-103">Azure DB Cosmos: Compilare un'applicazione console API MongoDB con Java e hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="ffd5f-103">Azure Cosmos DB: Build a MongoDB API console app with Java and hello Azure portal</span></span>

<span data-ttu-id="ffd5f-104">Azure Cosmos DB è il servizio di database multimodello distribuito a livello globale di Microsoft.</span><span class="sxs-lookup"><span data-stu-id="ffd5f-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="ffd5f-105">Creare rapidamente e query chiave/valore, il documento e database grafico, ognuno dei quali trarre vantaggio dalla distribuzione globale hello e funzionalità di scalabilità orizzontale di base di Azure Cosmos DB hello.</span><span class="sxs-lookup"><span data-stu-id="ffd5f-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="ffd5f-106">Questa Guida introduttiva viene illustrato come un account Azure Cosmos DB toocreate, database di documenti e l'utilizzo di raccolta hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="ffd5f-106">This quick start demonstrates how toocreate an Azure Cosmos DB account, document database, and collection using hello Azure portal.</span></span> <span data-ttu-id="ffd5f-107">Verrà quindi compilare e distribuire un'applicazione console basata su hello [driver MongoDB Java](https://docs.mongodb.com/ecosystem/drivers/java/).</span><span class="sxs-lookup"><span data-stu-id="ffd5f-107">You'll then build and deploy a console app built on hello [MongoDB Java driver](https://docs.mongodb.com/ecosystem/drivers/java/).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="ffd5f-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="ffd5f-108">Prerequisites</span></span>

* <span data-ttu-id="ffd5f-109">Prima di poter eseguire questo esempio, è necessario disporre di hello seguenti prerequisiti:</span><span class="sxs-lookup"><span data-stu-id="ffd5f-109">Before you can run this sample, you must have hello following prerequisites:</span></span>
   * <span data-ttu-id="ffd5f-110">JDK 1.7+ (eseguire `apt-get install default-jdk` se JDK non è disponibile)</span><span class="sxs-lookup"><span data-stu-id="ffd5f-110">JDK 1.7+ (Run `apt-get install default-jdk` if you don't have JDK)</span></span>
   * <span data-ttu-id="ffd5f-111">Maven (eseguire `apt-get install maven` se Maven non è disponibile)</span><span class="sxs-lookup"><span data-stu-id="ffd5f-111">Maven (Run `apt-get install maven` if you don't have Maven)</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="ffd5f-112">Creare un account di database</span><span class="sxs-lookup"><span data-stu-id="ffd5f-112">Create a database account</span></span>

[!INCLUDE [mongodb-create-dbaccount](../../includes/cosmos-db-create-dbaccount-mongodb.md)]

## <a name="add-a-collection"></a><span data-ttu-id="ffd5f-113">Aggiungere una raccolta</span><span class="sxs-lookup"><span data-stu-id="ffd5f-113">Add a collection</span></span>

<span data-ttu-id="ffd5f-114">Assegnare un nome al nuovo database, **db**, e alla nuova raccolta, **coll**.</span><span class="sxs-lookup"><span data-stu-id="ffd5f-114">Name your new database, **db**, and your new collection, **coll**.</span></span>

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

## <a name="clone-hello-sample-application"></a><span data-ttu-id="ffd5f-115">Applicazione di esempio hello clonare</span><span class="sxs-lookup"><span data-stu-id="ffd5f-115">Clone hello sample application</span></span>

<span data-ttu-id="ffd5f-116">Ora si app clone un'API di MongoDB da github, impostare la stringa di connessione hello ed eseguirlo.</span><span class="sxs-lookup"><span data-stu-id="ffd5f-116">Now let's clone a MongoDB API app from github, set hello connection string, and run it.</span></span> <span data-ttu-id="ffd5f-117">Si noterà quanto sia facile toowork con i dati a livello di codice.</span><span class="sxs-lookup"><span data-stu-id="ffd5f-117">You'll see how easy it is toowork with data programmatically.</span></span> 

1. <span data-ttu-id="ffd5f-118">Aprire una finestra terminale git, ad esempio git bash, e `cd` tooa directory di lavoro.</span><span class="sxs-lookup"><span data-stu-id="ffd5f-118">Open a git terminal window, such as git bash, and `cd` tooa working directory.</span></span>  

2. <span data-ttu-id="ffd5f-119">Eseguire hello seguenti repository di esempio di comando tooclone hello.</span><span class="sxs-lookup"><span data-stu-id="ffd5f-119">Run hello following command tooclone hello sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-mongodb-java-getting-started.git
    ```

3. <span data-ttu-id="ffd5f-120">Aprire quindi il file di soluzione hello in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ffd5f-120">Then open hello solution file in Visual Studio.</span></span> 

## <a name="review-hello-code"></a><span data-ttu-id="ffd5f-121">Esaminare il codice hello</span><span class="sxs-lookup"><span data-stu-id="ffd5f-121">Review hello code</span></span>

<span data-ttu-id="ffd5f-122">Questo punto, eseguire una rapida panoramica delle operazioni eseguite nell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="ffd5f-122">Let's make a quick review of what's happening in hello app.</span></span> <span data-ttu-id="ffd5f-123">Aprire hello `Program.cs` file e trovare le righe di codice creano hello risorse Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="ffd5f-123">Open hello `Program.cs` file and you'll find that these lines of code create hello Azure Cosmos DB resources.</span></span> 

* <span data-ttu-id="ffd5f-124">Hello DocumentClient viene inizializzato.</span><span class="sxs-lookup"><span data-stu-id="ffd5f-124">hello DocumentClient is initialized.</span></span>

    ```java
    MongoClientURI uri = new MongoClientURI("FILLME");`

    MongoClient mongoClient = new MongoClient(uri);            
    ```

* <span data-ttu-id="ffd5f-125">Vengono creati un nuovo database e una nuova raccolta.</span><span class="sxs-lookup"><span data-stu-id="ffd5f-125">A new database and collection are created.</span></span>

    ```java
    MongoDatabase database = mongoClient.getDatabase("db");

    MongoCollection<Document> collection = database.getCollection("coll");
    ```

* <span data-ttu-id="ffd5f-126">Vengono inseriti alcuni documenti usando `MongoCollection.insertOne`</span><span class="sxs-lookup"><span data-stu-id="ffd5f-126">Some documents are inserted using `MongoCollection.insertOne`</span></span>

    ```java
    Document document = new Document("fruit", "apple")
    collection.insertOne(document);
    ```

* <span data-ttu-id="ffd5f-127">Vengono eseguite alcune query usando `MongoCollection.find`</span><span class="sxs-lookup"><span data-stu-id="ffd5f-127">Some queries are performed using `MongoCollection.find`</span></span>

    ```java
    Document queryResult = collection.find(Filters.eq("fruit", "apple")).first();
    System.out.println(queryResult.toJson());       
    ```

## <a name="update-your-connection-string"></a><span data-ttu-id="ffd5f-128">Aggiornare la stringa di connessione</span><span class="sxs-lookup"><span data-stu-id="ffd5f-128">Update your connection string</span></span>

<span data-ttu-id="ffd5f-129">Tornare toohello tooget portale Azure le informazioni sulla stringa di connessione e copiarla in app hello.</span><span class="sxs-lookup"><span data-stu-id="ffd5f-129">Now go back toohello Azure portal tooget your connection string information and copy it into hello app.</span></span>

1. <span data-ttu-id="ffd5f-130">Hello Account, selezionare **avvio rapido**selezionare Java, quindi copiare negli Appunti tooyour stringa di connessione hello</span><span class="sxs-lookup"><span data-stu-id="ffd5f-130">From hello Account, select **Quick Start**, select Java, then copy hello connection string tooyour clipboard</span></span>

2. <span data-ttu-id="ffd5f-131">Aprire hello `Program.java` file, sostituire hello argomento toohello MongoClientURI costruttore con la stringa di connessione hello.</span><span class="sxs-lookup"><span data-stu-id="ffd5f-131">Open hello `Program.java` file, replace hello argument toohello MongoClientURI constructor with hello connection string.</span></span> <span data-ttu-id="ffd5f-132">È stato aggiornato a questo punto l'app con tutte le informazioni di hello deve toocommunicate con Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="ffd5f-132">You've now updated your app with all hello info it needs toocommunicate with Azure Cosmos DB.</span></span> 
    
## <a name="run-hello-console-app"></a><span data-ttu-id="ffd5f-133">Eseguire app console hello</span><span class="sxs-lookup"><span data-stu-id="ffd5f-133">Run hello console app</span></span>

1. <span data-ttu-id="ffd5f-134">Eseguire `mvn package` in un terminal tooinstall necessari moduli npm</span><span class="sxs-lookup"><span data-stu-id="ffd5f-134">Run `mvn package` in a terminal tooinstall required npm modules</span></span>

2. <span data-ttu-id="ffd5f-135">Eseguire `mvn exec:java -D exec.mainClass=GetStarted.Program` in un terminal toostart l'applicazione Java.</span><span class="sxs-lookup"><span data-stu-id="ffd5f-135">Run `mvn exec:java -D exec.mainClass=GetStarted.Program` in a terminal toostart your Java application.</span></span>

<span data-ttu-id="ffd5f-136">È ora possibile usare [Robomongo](mongodb-robomongo.md) / [Studio 3T](mongodb-mongochef.md) tooquery, modificare e utilizzare questi nuovi dati.</span><span class="sxs-lookup"><span data-stu-id="ffd5f-136">You can now use [Robomongo](mongodb-robomongo.md) / [Studio 3T](mongodb-mongochef.md) tooquery, modify, and work with this new data.</span></span>

## <a name="review-slas-in-hello-azure-portal"></a><span data-ttu-id="ffd5f-137">Esaminare i contratti di servizio nel portale di Azure hello</span><span class="sxs-lookup"><span data-stu-id="ffd5f-137">Review SLAs in hello Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="ffd5f-138">Pulire le risorse</span><span class="sxs-lookup"><span data-stu-id="ffd5f-138">Clean up resources</span></span>

<span data-ttu-id="ffd5f-139">Se non si ha intenzione toocontinue toouse questa app, eliminare tutte le risorse create da questa Guida rapida hello portale di Azure con hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="ffd5f-139">If you're not going toocontinue toouse this app, delete all resources created by this quickstart in hello Azure portal with hello following steps:</span></span>

1. <span data-ttu-id="ffd5f-140">Dal menu a sinistra di hello in hello portale di Azure, fare clic su **gruppi di risorse** e quindi fare clic su nome hello della risorsa di hello è stato creato.</span><span class="sxs-lookup"><span data-stu-id="ffd5f-140">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span> 
2. <span data-ttu-id="ffd5f-141">Nella pagina di gruppo di risorse, fare clic su **eliminare**, digitare il nome di hello di hello risorsa toodelete nella casella di testo hello e quindi fare clic su **eliminare**.</span><span class="sxs-lookup"><span data-stu-id="ffd5f-141">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ffd5f-142">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ffd5f-142">Next steps</span></span>

<span data-ttu-id="ffd5f-143">In questa Guida rapida, si è appreso come creare una raccolta utilizzando Esplora dati hello toocreate un account Azure Cosmos DB ed eseguire un'applicazione console.</span><span class="sxs-lookup"><span data-stu-id="ffd5f-143">In this quickstart, you've learned how toocreate an Azure Cosmos DB account, create a collection using hello Data Explorer, and run a console app.</span></span> <span data-ttu-id="ffd5f-144">È ora possibile importare account Cosmos DB tooyour di dati aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="ffd5f-144">You can now import additional data tooyour Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="ffd5f-145">Importare i dati di MongoDB in Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="ffd5f-145">Import MongoDB data into Azure Cosmos DB</span></span>](mongodb-migrate.md)


