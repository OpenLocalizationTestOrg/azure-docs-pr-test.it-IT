---
title: 'Esercitazione su NoSQL: API di DocumentDB per Azure Cosmos DB Java SDK | Microsoft Docs'
description: "Esercitazione su NoSQL che crea un database online e un'applicazione console Java con l'API di DocumentDB per Azure Cosmos DB. Azure DocumentDB è un database NoSQL per JSON."
keywords: esercitazione su nosql, database online, applicazione console java
services: cosmos-db
documentationcenter: Java
author: arramac
manager: jhubbard
editor: monicar
ms.assetid: 75a9efa1-7edd-4fed-9882-c0177274cbb2
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: article
ms.date: 05/22/2017
ms.author: arramac
ms.openlocfilehash: 5c4bcda308f001572e1c34e991616fc209250a02
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="nosql-tutorial-build-a-documentdb-api-java-console-application"></a><span data-ttu-id="b26ed-105">Esercitazione su NoSQL: Compilare un'applicazione console Java con l'API di DocumentDB</span><span class="sxs-lookup"><span data-stu-id="b26ed-105">NoSQL tutorial: Build a DocumentDB API Java console application</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b26ed-106">.NET</span><span class="sxs-lookup"><span data-stu-id="b26ed-106">.NET</span></span>](documentdb-get-started.md)
> * [<span data-ttu-id="b26ed-107">.NET Core</span><span class="sxs-lookup"><span data-stu-id="b26ed-107">.NET Core</span></span>](documentdb-dotnetcore-get-started.md)
> * [<span data-ttu-id="b26ed-108">Node.js per MongoDB</span><span class="sxs-lookup"><span data-stu-id="b26ed-108">Node.js for MongoDB</span></span>](mongodb-samples.md)
> * [<span data-ttu-id="b26ed-109">Node.js</span><span class="sxs-lookup"><span data-stu-id="b26ed-109">Node.js</span></span>](documentdb-nodejs-get-started.md)
> * [<span data-ttu-id="b26ed-110">Java</span><span class="sxs-lookup"><span data-stu-id="b26ed-110">Java</span></span>](documentdb-java-get-started.md)
> * [<span data-ttu-id="b26ed-111">C++</span><span class="sxs-lookup"><span data-stu-id="b26ed-111">C++</span></span>](documentdb-cpp-get-started.md)
>  
> 

<span data-ttu-id="b26ed-112">Esercitazione su NoSQL per l'API di DocumentDB per Azure Cosmos DB Java SDK.</span><span class="sxs-lookup"><span data-stu-id="b26ed-112">Welcome to the NoSQL tutorial for the DocumentDB API for Azure Cosmos DB Java SDK!</span></span> <span data-ttu-id="b26ed-113">Dopo aver seguito questa esercitazione, si otterrà un'applicazione console che consente di creare e ridefinire le query delle risorse Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="b26ed-113">After following this tutorial, you'll have a console application that creates and queries Azure Cosmos DB resources.</span></span>

<span data-ttu-id="b26ed-114">Argomenti trattati:</span><span class="sxs-lookup"><span data-stu-id="b26ed-114">We cover:</span></span>

* <span data-ttu-id="b26ed-115">Creazione e connessione a un account Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="b26ed-115">Creating and connecting to an Azure Cosmos DB account</span></span>
* <span data-ttu-id="b26ed-116">Configurare una soluzione Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b26ed-116">Configuring your Visual Studio Solution</span></span>
* <span data-ttu-id="b26ed-117">Creazione di un database online</span><span class="sxs-lookup"><span data-stu-id="b26ed-117">Creating an online database</span></span>
* <span data-ttu-id="b26ed-118">Creare una raccolta</span><span class="sxs-lookup"><span data-stu-id="b26ed-118">Creating a collection</span></span>
* <span data-ttu-id="b26ed-119">Creazione di documenti JSON</span><span class="sxs-lookup"><span data-stu-id="b26ed-119">Creating JSON documents</span></span>
* <span data-ttu-id="b26ed-120">Esecuzione di query sulla raccolta</span><span class="sxs-lookup"><span data-stu-id="b26ed-120">Querying the collection</span></span>
* <span data-ttu-id="b26ed-121">Creazione di documenti JSON</span><span class="sxs-lookup"><span data-stu-id="b26ed-121">Creating JSON documents</span></span>
* <span data-ttu-id="b26ed-122">Esecuzione di query sulla raccolta</span><span class="sxs-lookup"><span data-stu-id="b26ed-122">Querying the collection</span></span>
* <span data-ttu-id="b26ed-123">Sostituzione di un documento</span><span class="sxs-lookup"><span data-stu-id="b26ed-123">Replacing a document</span></span>
* <span data-ttu-id="b26ed-124">Eliminazione di un documento</span><span class="sxs-lookup"><span data-stu-id="b26ed-124">Deleting a document</span></span>
* <span data-ttu-id="b26ed-125">Eliminazione del database</span><span class="sxs-lookup"><span data-stu-id="b26ed-125">Deleting the database</span></span>

<span data-ttu-id="b26ed-126">Ecco come procedere.</span><span class="sxs-lookup"><span data-stu-id="b26ed-126">Now let's get started!</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b26ed-127">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="b26ed-127">Prerequisites</span></span>
<span data-ttu-id="b26ed-128">Assicurarsi che sia disponibile quanto segue:</span><span class="sxs-lookup"><span data-stu-id="b26ed-128">Make sure you have the following:</span></span>

* <span data-ttu-id="b26ed-129">Un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="b26ed-129">An active Azure account.</span></span> <span data-ttu-id="b26ed-130">Se non si ha un account, è possibile iscriversi per ottenere un [account gratuito](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="b26ed-130">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span> <span data-ttu-id="b26ed-131">In alternativa, per questa esercitazione è possibile usare l'[emulatore Azure Cosmos DB](local-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="b26ed-131">Alternatively, you can use the [Azure Cosmos DB Emulator](local-emulator.md) for this tutorial.</span></span>
* [<span data-ttu-id="b26ed-132">Git</span><span class="sxs-lookup"><span data-stu-id="b26ed-132">Git</span></span>](https://git-scm.com/downloads)
* <span data-ttu-id="b26ed-133">[Java Development Kit (JDK) 7+](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span><span class="sxs-lookup"><span data-stu-id="b26ed-133">[Java Development Kit (JDK) 7+](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span></span>
* <span data-ttu-id="b26ed-134">[Maven](http://maven.apache.org/download.cgi).</span><span class="sxs-lookup"><span data-stu-id="b26ed-134">[Maven](http://maven.apache.org/download.cgi).</span></span>

## <a name="step-1-create-an-azure-cosmos-db-account"></a><span data-ttu-id="b26ed-135">Passaggio 1: Creare un account di Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="b26ed-135">Step 1: Create an Azure Cosmos DB account</span></span>
<span data-ttu-id="b26ed-136">Creare prima di tutto un account Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="b26ed-136">Let's create an Azure Cosmos DB account.</span></span> <span data-ttu-id="b26ed-137">Se è già disponibile un account da usare, è possibile andare direttamente al passaggio [Clonare il progetto GitHub](#GitClone).</span><span class="sxs-lookup"><span data-stu-id="b26ed-137">If you already have an account you want to use, you can skip ahead to [Clone the GitHub project](#GitClone).</span></span> <span data-ttu-id="b26ed-138">Se si usa l'emulatore Azure Cosmos DB, seguire la procedura illustrata nell'articolo relativo all'[emulatore Azure Cosmos DB](local-emulator.md) per configurare l'emulatore e proseguire con il passaggio [Clonare il progetto GitHub](#GitClone).</span><span class="sxs-lookup"><span data-stu-id="b26ed-138">If you are using the Azure Cosmos DB Emulator, follow the steps at [Azure Cosmos DB Emulator](local-emulator.md) to set up the emulator and skip ahead to [Clone the GitHub project](#GitClone).</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <span data-ttu-id="b26ed-139"><a id="GitClone"></a>Passaggio 2: Clonare il progetto GitHub</span><span class="sxs-lookup"><span data-stu-id="b26ed-139"><a id="GitClone"></a>Step 2: Clone the GitHub project</span></span>
<span data-ttu-id="b26ed-140">Per iniziare, è possibile clonare il repository GitHub per l'[introduzione ad Azure Cosmos DB e Java](https://github.com/Azure-Samples/documentdb-java-getting-started).</span><span class="sxs-lookup"><span data-stu-id="b26ed-140">You can get started by cloning the GitHub repository for [Get Started with Azure Cosmos DB and Java](https://github.com/Azure-Samples/documentdb-java-getting-started).</span></span> <span data-ttu-id="b26ed-141">Eseguire questo comando da una directory locale per recuperare il progetto di esempio in locale.</span><span class="sxs-lookup"><span data-stu-id="b26ed-141">For example, from a local directory run the following to retrieve the sample project locally.</span></span>

    git clone git@github.com:Azure-Samples/azure-cosmos-db-documentdb-java-getting-started.git

    cd azure-cosmos-db-documentdb-java-getting-started

<span data-ttu-id="b26ed-142">La directory contiene un oggetto `pom.xml` per il progetto e una cartella `src` che contiene il codice sorgente Java incluso `Program.java`, che mostra come eseguire semplici operazioni con Azure Cosmos DB, come la creazione di documenti e l'esecuzione di query sui dati all'interno di una raccolta.</span><span class="sxs-lookup"><span data-stu-id="b26ed-142">The directory contains a `pom.xml` for the project and a `src` folder containing Java source code including `Program.java` which shows how perform simple operations with Azure Cosmos DB like creating documents and querying data within a collection.</span></span> <span data-ttu-id="b26ed-143">L'oggetto `pom.xml` include una dipendenza per [DocumentDB Java SDK su Maven](https://mvnrepository.com/artifact/com.microsoft.azure/azure-documentdb).</span><span class="sxs-lookup"><span data-stu-id="b26ed-143">The `pom.xml` includes a dependency on the [DocumentDB Java SDK on Maven](https://mvnrepository.com/artifact/com.microsoft.azure/azure-documentdb).</span></span>

    <dependency>
        <groupId>com.microsoft.azure</groupId>
        <artifactId>azure-documentdb</artifactId>
        <version>LATEST</version>
    </dependency>

## <span data-ttu-id="b26ed-144"><a id="Connect"></a>Passaggio 3: Connettersi a un account Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="b26ed-144"><a id="Connect"></a>Step 3: Connect to an Azure Cosmos DB account</span></span>
<span data-ttu-id="b26ed-145">Tornare al [portale di Azure](https://portal.azure.com) per recuperare l'endpoint e la chiave master primaria.</span><span class="sxs-lookup"><span data-stu-id="b26ed-145">Next, head back to the [Azure Portal](https://portal.azure.com) to retrieve your endpoint and primary master key.</span></span> <span data-ttu-id="b26ed-146">L'endpoint e la chiave primaria di Azure Cosmos DB sono necessari all'applicazione per conoscere la destinazione della connessione e ad Azure Cosmos DB per considerare attendibile la connessione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="b26ed-146">The Azure Cosmos DB endpoint and primary key are necessary for your application to understand where to connect to, and for Azure Cosmos DB to trust your application's connection.</span></span>

<span data-ttu-id="b26ed-147">Nel portale di Azure passare all'account Azure Cosmos DB e quindi fare clic su **Chiavi**.</span><span class="sxs-lookup"><span data-stu-id="b26ed-147">In the Azure Portal, navigate to your Azure Cosmos DB account, and then click **Keys**.</span></span> <span data-ttu-id="b26ed-148">Copiare l'URI dal portale e incollarlo in `https://FILLME.documents.azure.com` nel file Program.java.</span><span class="sxs-lookup"><span data-stu-id="b26ed-148">Copy the URI from the portal and paste it into `https://FILLME.documents.azure.com` in the Program.java file.</span></span> <span data-ttu-id="b26ed-149">Copiare quindi la CHIAVE PRIMARIA dal portale e incollarla in `FILLME`.</span><span class="sxs-lookup"><span data-stu-id="b26ed-149">Then copy the PRIMARY KEY from the portal and paste it into `FILLME`.</span></span>

    this.client = new DocumentClient(
        "https://FILLME.documents.azure.com",
        "FILLME"
        , new ConnectionPolicy(),
        ConsistencyLevel.Session);

![Screenshot del portale di Azure usato nell'esercitazione su NoSQL per creare un'applicazione console Java.][keys]

## <a name="step-4-create-a-database"></a><span data-ttu-id="b26ed-152">Passaggio 4: Creare un database</span><span class="sxs-lookup"><span data-stu-id="b26ed-152">Step 4: Create a database</span></span>
<span data-ttu-id="b26ed-153">È possibile creare un [database](documentdb-resources.md#databases) di Azure Cosmos DB usando il metodo [createDatabase](/java/api/com.microsoft.azure.documentdb._document_client.createdatabase) della classe **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="b26ed-153">Your Azure Cosmos DB [database](documentdb-resources.md#databases) can be created by using the [createDatabase](/java/api/com.microsoft.azure.documentdb._document_client.createdatabase) method of the **DocumentClient** class.</span></span> <span data-ttu-id="b26ed-154">Un database è il contenitore logico per l'archiviazione di documenti JSON partizionato nelle raccolte.</span><span class="sxs-lookup"><span data-stu-id="b26ed-154">A database is the logical container of JSON document storage partitioned across collections.</span></span>

    Database database = new Database();
    database.setId("familydb");
    this.client.createDatabase(database, null);

## <span data-ttu-id="b26ed-155"><a id="CreateColl"></a>Passaggio 5: Creare una raccolta</span><span class="sxs-lookup"><span data-stu-id="b26ed-155"><a id="CreateColl"></a>Step 5: Create a collection</span></span>
> [!WARNING]
> <span data-ttu-id="b26ed-156">**createCollection** crea una nuova raccolta con velocità effettiva riservata, che presenta implicazioni in termini di prezzi.</span><span class="sxs-lookup"><span data-stu-id="b26ed-156">**createCollection** creates a new collection with reserved throughput, which has pricing implications.</span></span> <span data-ttu-id="b26ed-157">Per altre informazioni, visitare la [pagina relativa ai prezzi](https://azure.microsoft.com/pricing/details/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="b26ed-157">For more details, visit our [pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/).</span></span>
> 
> 

<span data-ttu-id="b26ed-158">È possibile creare una [raccolta](documentdb-resources.md#collections) usando il metodo [createCollection](/java/api/com.microsoft.azure.documentdb._document_client.createcollection) della classe **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="b26ed-158">A [collection](documentdb-resources.md#collections) can be created by using the [createCollection](/java/api/com.microsoft.azure.documentdb._document_client.createcollection) method of the **DocumentClient** class.</span></span> <span data-ttu-id="b26ed-159">Una raccolta è un contenitore di documenti JSON e di logica dell'applicazione JavaScript associata.</span><span class="sxs-lookup"><span data-stu-id="b26ed-159">A collection is a container of JSON documents and associated JavaScript application logic.</span></span>


    DocumentCollection collectionInfo = new DocumentCollection();
    collectionInfo.setId("familycoll");

    // Azure Cosmos DB collections can be reserved with throughput specified in request units/second. 
    // Here we create a collection with 400 RU/s.
    RequestOptions requestOptions = new RequestOptions();
    requestOptions.setOfferThroughput(400);

    this.client.createCollection("/dbs/familydb", collectionInfo, requestOptions);

## <span data-ttu-id="b26ed-160"><a id="CreateDoc"></a>Passaggio 6: Creare documenti JSON</span><span class="sxs-lookup"><span data-stu-id="b26ed-160"><a id="CreateDoc"></a>Step 6: Create JSON documents</span></span>
<span data-ttu-id="b26ed-161">È possibile creare un [documento](documentdb-resources.md#documents) usando il metodo [createDocument](/java/api/com.microsoft.azure.documentdb._document_client.createdocument) della classe **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="b26ed-161">A [document](documentdb-resources.md#documents) can be created by using the [createDocument](/java/api/com.microsoft.azure.documentdb._document_client.createdocument) method of the **DocumentClient** class.</span></span> <span data-ttu-id="b26ed-162">I documenti sono contenuto JSON definito dall'utente (arbitrario).</span><span class="sxs-lookup"><span data-stu-id="b26ed-162">Documents are user-defined (arbitrary) JSON content.</span></span> <span data-ttu-id="b26ed-163">Ora è possibile inserire uno o più documenti.</span><span class="sxs-lookup"><span data-stu-id="b26ed-163">We can now insert one or more documents.</span></span> <span data-ttu-id="b26ed-164">Se sono già disponibili dati da archiviare nel database, è possibile usare lo [strumento di migrazione dei dati](import-data.md) di Azure Cosmos DB per importare i dati in un database.</span><span class="sxs-lookup"><span data-stu-id="b26ed-164">If you already have data you'd like to store in your database, you can use Azure Cosmos DB's [Data Migration tool](import-data.md) to import the data into a database.</span></span>

    // Insert your Java objects as documents 
    Family andersenFamily = new Family();
    andersenFamily.setId("Andersen.1");
    andersenFamily.setLastName("Andersen")

    // More initialization skipped for brevity. You can have nested references
    andersenFamily.setParents(new Parent[] { parent1, parent2 });
    andersenFamily.setDistrict("WA5");
    Address address = new Address();
    address.setCity("Seattle");
    address.setCounty("King");
    address.setState("WA");

    andersenFamily.setAddress(address);
    andersenFamily.setRegistered(true);

    this.client.createDocument("/dbs/familydb/colls/familycoll", family, new RequestOptions(), true);

![Diagramma che illustra la relazione gerarchica tra l'account, il database online, la raccolta e i documenti usati nell'esercitazione su NoSQL per creare un'applicazione console Java](./media/documentdb-get-started/nosql-tutorial-account-database.png)

## <span data-ttu-id="b26ed-166"><a id="Query"></a>Passaggio 7: Eseguire query sulle risorse di Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="b26ed-166"><a id="Query"></a>Step 7: Query Azure Cosmos DB resources</span></span>
<span data-ttu-id="b26ed-167">Azure Cosmos DB supporta [query complesse](documentdb-sql-query.md) sui documenti JSON archiviati in ogni raccolta.</span><span class="sxs-lookup"><span data-stu-id="b26ed-167">Azure Cosmos DB supports rich [queries](documentdb-sql-query.md) against JSON documents stored in each collection.</span></span>  <span data-ttu-id="b26ed-168">Il codice di esempio seguente mostra come eseguire query su documenti in Azure Cosmos DB usando la sintassi SQL con il metodo [queryDocuments](/java/api/com.microsoft.azure.documentdb._document_client.querydocuments).</span><span class="sxs-lookup"><span data-stu-id="b26ed-168">The following sample code shows how to query documents in Azure Cosmos DB using SQL syntax with the [queryDocuments](/java/api/com.microsoft.azure.documentdb._document_client.querydocuments) method.</span></span>

    FeedResponse<Document> queryResults = this.client.queryDocuments(
        "/dbs/familydb/colls/familycoll",
        "SELECT * FROM Family WHERE Family.lastName = 'Andersen'", 
        null);

    System.out.println("Running SQL query...");
    for (Document family : queryResults.getQueryIterable()) {
        System.out.println(String.format("\tRead %s", family));
    }

## <span data-ttu-id="b26ed-169"><a id="ReplaceDocument"></a>Passaggio 8: Sostituire un documento JSON</span><span class="sxs-lookup"><span data-stu-id="b26ed-169"><a id="ReplaceDocument"></a>Step 8: Replace JSON document</span></span>
<span data-ttu-id="b26ed-170">Azure Cosmos DB supporta l'aggiornamento di documenti JSON con il metodo [replaceDocument](/java/api/com.microsoft.azure.documentdb._document_client.replacedocument).</span><span class="sxs-lookup"><span data-stu-id="b26ed-170">Azure Cosmos DB supports updating JSON documents using the [replaceDocument](/java/api/com.microsoft.azure.documentdb._document_client.replacedocument) method.</span></span>

    // Update a property
    andersenFamily.Children[0].Grade = 6;

    this.client.replaceDocument(
        "/dbs/familydb/colls/familycoll/docs/Andersen.1", 
        andersenFamily,
        null);

## <span data-ttu-id="b26ed-171"><a id="DeleteDocument"></a>Passaggio 9: Eliminare un documento JSON</span><span class="sxs-lookup"><span data-stu-id="b26ed-171"><a id="DeleteDocument"></a>Step 9: Delete JSON document</span></span>
<span data-ttu-id="b26ed-172">Analogamente, Azure Cosmos DB supporta l'eliminazione di documenti JSON con il metodo [deleteDocument](/java/api/com.microsoft.azure.documentdb._document_client.deletedocument).</span><span class="sxs-lookup"><span data-stu-id="b26ed-172">Similarly, Azure Cosmos DB supports deleting JSON documents using the [deleteDocument](/java/api/com.microsoft.azure.documentdb._document_client.deletedocument) method.</span></span>  

    this.client.delete("/dbs/familydb/colls/familycoll/docs/Andersen.1", null);

## <span data-ttu-id="b26ed-173"><a id="DeleteDatabase"></a>Passaggio 10: Eliminare il database</span><span class="sxs-lookup"><span data-stu-id="b26ed-173"><a id="DeleteDatabase"></a>Step 10: Delete the database</span></span>
<span data-ttu-id="b26ed-174">Se si elimina il database creato, insieme al database vengono rimosse tutte le risorse figlio, come raccolte, documenti e così via.</span><span class="sxs-lookup"><span data-stu-id="b26ed-174">Deleting the created database removes the database and all children resources (collections, documents, etc.).</span></span>

    this.client.deleteDatabase("/dbs/familydb", null);

## <span data-ttu-id="b26ed-175"><a id="Run"></a>Passaggio 11: Eseguire l'intera applicazione console Java</span><span class="sxs-lookup"><span data-stu-id="b26ed-175"><a id="Run"></a>Step 11: Run your Java console application all together!</span></span>
<span data-ttu-id="b26ed-176">Per eseguire l'applicazione dalla console, passare alla cartella del progetto e compilare usando Maven:</span><span class="sxs-lookup"><span data-stu-id="b26ed-176">To run the application from the console, navigate to the project folder and compile using Maven:</span></span>
    
    mvn package

<span data-ttu-id="b26ed-177">L'esecuzione di `mvn package` scarica la libreria di Azure Cosmos DB più recente da Maven e produce `GetStarted-0.0.1-SNAPSHOT.jar`.</span><span class="sxs-lookup"><span data-stu-id="b26ed-177">Running `mvn package` downloads the latest Azure Cosmos DB library from Maven and produces `GetStarted-0.0.1-SNAPSHOT.jar`.</span></span> <span data-ttu-id="b26ed-178">Eseguire l'app usando quanto segue:</span><span class="sxs-lookup"><span data-stu-id="b26ed-178">Then run the app by running:</span></span>

    mvn exec:java -D exec.mainClass=GetStarted.Program

<span data-ttu-id="b26ed-179">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="b26ed-179">Congratulations!</span></span> <span data-ttu-id="b26ed-180">L'esercitazione su NoSQL è stata completata ed è stata creata un'applicazione console Java funzionante.</span><span class="sxs-lookup"><span data-stu-id="b26ed-180">You've completed this NoSQL tutorial and have a working Java console application!</span></span>

## <a name="next-steps"></a><span data-ttu-id="b26ed-181">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b26ed-181">Next steps</span></span>
* <span data-ttu-id="b26ed-182">Per un'esercitazione su app Web Java,</span><span class="sxs-lookup"><span data-stu-id="b26ed-182">Want a Java web app tutorial?</span></span> <span data-ttu-id="b26ed-183">vedere [Creazione di un'applicazione Web Java con Azure Cosmos DB](documentdb-java-application.md).</span><span class="sxs-lookup"><span data-stu-id="b26ed-183">See [Build a web application with Java using Azure Cosmos DB](documentdb-java-application.md).</span></span>
* <span data-ttu-id="b26ed-184">Informazioni su come [monitorare un account Azure Cosmos DB](monitor-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="b26ed-184">Learn how to [monitor an Azure Cosmos DB account](monitor-accounts.md).</span></span>
* <span data-ttu-id="b26ed-185">Eseguire query sul set di dati di esempio illustrato nella pagina [Query Playground](https://www.documentdb.com/sql/demo).</span><span class="sxs-lookup"><span data-stu-id="b26ed-185">Run queries against our sample dataset in the [Query Playground](https://www.documentdb.com/sql/demo).</span></span>
* <span data-ttu-id="b26ed-186">Per altre informazioni sul modello di programmazione, vedere la sezione relativa allo sviluppo nella pagina [Documentazione di Azure Cosmos DB](https://azure.microsoft.com/documentation/services/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="b26ed-186">Learn more about the programming model in the Develop section of the [Azure Cosmos DB documentation page](https://azure.microsoft.com/documentation/services/documentdb/).</span></span>

[keys]: media/documentdb-get-started/nosql-tutorial-keys.png
