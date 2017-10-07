---
title: 'Esercitazione su NoSQL: API di DocumentDB per Azure Cosmos DB Java SDK | Microsoft Docs'
description: "In questa esercitazione NoSQL che crea un database online e l'applicazione console Java utilizzando l'API DocumentDB hello per Azure Cosmos DB. Azure DocumentDB è un database NoSQL per JSON."
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
ms.openlocfilehash: 1a298a15ab911d140b9df30ad52cfe0fa07c55b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="nosql-tutorial-build-a-documentdb-api-java-console-application"></a><span data-ttu-id="2ce3b-105">Esercitazione su NoSQL: Compilare un'applicazione console Java con l'API di DocumentDB</span><span class="sxs-lookup"><span data-stu-id="2ce3b-105">NoSQL tutorial: Build a DocumentDB API Java console application</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="2ce3b-106">.NET</span><span class="sxs-lookup"><span data-stu-id="2ce3b-106">.NET</span></span>](documentdb-get-started.md)
> * [<span data-ttu-id="2ce3b-107">.NET Core</span><span class="sxs-lookup"><span data-stu-id="2ce3b-107">.NET Core</span></span>](documentdb-dotnetcore-get-started.md)
> * [<span data-ttu-id="2ce3b-108">Node.js per MongoDB</span><span class="sxs-lookup"><span data-stu-id="2ce3b-108">Node.js for MongoDB</span></span>](mongodb-samples.md)
> * [<span data-ttu-id="2ce3b-109">Node.js</span><span class="sxs-lookup"><span data-stu-id="2ce3b-109">Node.js</span></span>](documentdb-nodejs-get-started.md)
> * [<span data-ttu-id="2ce3b-110">Java</span><span class="sxs-lookup"><span data-stu-id="2ce3b-110">Java</span></span>](documentdb-java-get-started.md)
> * [<span data-ttu-id="2ce3b-111">C++</span><span class="sxs-lookup"><span data-stu-id="2ce3b-111">C++</span></span>](documentdb-cpp-get-started.md)
>  
> 

<span data-ttu-id="2ce3b-112">Introduzione toohello NoSQL esercitazione per l'API DocumentDB hello Azure SDK per Java DB Cosmos.</span><span class="sxs-lookup"><span data-stu-id="2ce3b-112">Welcome toohello NoSQL tutorial for hello DocumentDB API for Azure Cosmos DB Java SDK!</span></span> <span data-ttu-id="2ce3b-113">Dopo aver seguito questa esercitazione, si otterrà un'applicazione console che consente di creare e ridefinire le query delle risorse Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="2ce3b-113">After following this tutorial, you'll have a console application that creates and queries Azure Cosmos DB resources.</span></span>

<span data-ttu-id="2ce3b-114">Argomenti trattati:</span><span class="sxs-lookup"><span data-stu-id="2ce3b-114">We cover:</span></span>

* <span data-ttu-id="2ce3b-115">Creazione e connessione account Azure Cosmos DB tooan</span><span class="sxs-lookup"><span data-stu-id="2ce3b-115">Creating and connecting tooan Azure Cosmos DB account</span></span>
* <span data-ttu-id="2ce3b-116">Configurare una soluzione Visual Studio</span><span class="sxs-lookup"><span data-stu-id="2ce3b-116">Configuring your Visual Studio Solution</span></span>
* <span data-ttu-id="2ce3b-117">Creazione di un database online</span><span class="sxs-lookup"><span data-stu-id="2ce3b-117">Creating an online database</span></span>
* <span data-ttu-id="2ce3b-118">Creare una raccolta</span><span class="sxs-lookup"><span data-stu-id="2ce3b-118">Creating a collection</span></span>
* <span data-ttu-id="2ce3b-119">Creazione di documenti JSON</span><span class="sxs-lookup"><span data-stu-id="2ce3b-119">Creating JSON documents</span></span>
* <span data-ttu-id="2ce3b-120">Esecuzione di query hello raccolta</span><span class="sxs-lookup"><span data-stu-id="2ce3b-120">Querying hello collection</span></span>
* <span data-ttu-id="2ce3b-121">Creazione di documenti JSON</span><span class="sxs-lookup"><span data-stu-id="2ce3b-121">Creating JSON documents</span></span>
* <span data-ttu-id="2ce3b-122">Esecuzione di query hello raccolta</span><span class="sxs-lookup"><span data-stu-id="2ce3b-122">Querying hello collection</span></span>
* <span data-ttu-id="2ce3b-123">Sostituzione di un documento</span><span class="sxs-lookup"><span data-stu-id="2ce3b-123">Replacing a document</span></span>
* <span data-ttu-id="2ce3b-124">Eliminazione di un documento</span><span class="sxs-lookup"><span data-stu-id="2ce3b-124">Deleting a document</span></span>
* <span data-ttu-id="2ce3b-125">L'eliminazione di database hello</span><span class="sxs-lookup"><span data-stu-id="2ce3b-125">Deleting hello database</span></span>

<span data-ttu-id="2ce3b-126">Ecco come procedere.</span><span class="sxs-lookup"><span data-stu-id="2ce3b-126">Now let's get started!</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2ce3b-127">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="2ce3b-127">Prerequisites</span></span>
<span data-ttu-id="2ce3b-128">Verificare di che aver seguito hello:</span><span class="sxs-lookup"><span data-stu-id="2ce3b-128">Make sure you have hello following:</span></span>

* <span data-ttu-id="2ce3b-129">Un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="2ce3b-129">An active Azure account.</span></span> <span data-ttu-id="2ce3b-130">Se non si ha un account, è possibile iscriversi per ottenere un [account gratuito](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="2ce3b-130">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span> <span data-ttu-id="2ce3b-131">In alternativa, è possibile utilizzare hello [Azure Cosmos DB emulatore](local-emulator.md) per questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="2ce3b-131">Alternatively, you can use hello [Azure Cosmos DB Emulator](local-emulator.md) for this tutorial.</span></span>
* [<span data-ttu-id="2ce3b-132">Git</span><span class="sxs-lookup"><span data-stu-id="2ce3b-132">Git</span></span>](https://git-scm.com/downloads)
* <span data-ttu-id="2ce3b-133">[Java Development Kit (JDK) 7+](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span><span class="sxs-lookup"><span data-stu-id="2ce3b-133">[Java Development Kit (JDK) 7+](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span></span>
* <span data-ttu-id="2ce3b-134">[Maven](http://maven.apache.org/download.cgi).</span><span class="sxs-lookup"><span data-stu-id="2ce3b-134">[Maven](http://maven.apache.org/download.cgi).</span></span>

## <a name="step-1-create-an-azure-cosmos-db-account"></a><span data-ttu-id="2ce3b-135">Passaggio 1: Creare un account di Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="2ce3b-135">Step 1: Create an Azure Cosmos DB account</span></span>
<span data-ttu-id="2ce3b-136">Creare prima di tutto un account Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="2ce3b-136">Let's create an Azure Cosmos DB account.</span></span> <span data-ttu-id="2ce3b-137">Se si dispone già di un account a cui si vuole toouse, è possibile andare troppo[progetto GitHub di Clone hello](#GitClone).</span><span class="sxs-lookup"><span data-stu-id="2ce3b-137">If you already have an account you want toouse, you can skip ahead too[Clone hello GitHub project](#GitClone).</span></span> <span data-ttu-id="2ce3b-138">Se si utilizza l'emulatore di Azure Cosmos DB hello, seguire i passaggi di hello in [emulatore di Azure Cosmos DB](local-emulator.md) tooset backup emulatore hello e andare troppo[progetto GitHub di Clone hello](#GitClone).</span><span class="sxs-lookup"><span data-stu-id="2ce3b-138">If you are using hello Azure Cosmos DB Emulator, follow hello steps at [Azure Cosmos DB Emulator](local-emulator.md) tooset up hello emulator and skip ahead too[Clone hello GitHub project](#GitClone).</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <span data-ttu-id="2ce3b-139"><a id="GitClone"></a>Passaggio 2: Clonare progetto GitHub hello</span><span class="sxs-lookup"><span data-stu-id="2ce3b-139"><a id="GitClone"></a>Step 2: Clone hello GitHub project</span></span>
<span data-ttu-id="2ce3b-140">È possibile iniziare duplicando il repository GitHub hello per [Introduzione a Azure Cosmos DB e Java](https://github.com/Azure-Samples/documentdb-java-getting-started).</span><span class="sxs-lookup"><span data-stu-id="2ce3b-140">You can get started by cloning hello GitHub repository for [Get Started with Azure Cosmos DB and Java](https://github.com/Azure-Samples/documentdb-java-getting-started).</span></span> <span data-ttu-id="2ce3b-141">Ad esempio, eseguire hello seguente tooretrieve hello del progetto di esempio in locale da una directory locale.</span><span class="sxs-lookup"><span data-stu-id="2ce3b-141">For example, from a local directory run hello following tooretrieve hello sample project locally.</span></span>

    git clone git@github.com:Azure-Samples/azure-cosmos-db-documentdb-java-getting-started.git

    cd azure-cosmos-db-documentdb-java-getting-started

<span data-ttu-id="2ce3b-142">Hello directory contiene un `pom.xml` per progetto hello e una `src` cartella che contiene codice di origine Java inclusi `Program.java` che mostra come esegue semplici operazioni con Azure Cosmos DB come la creazione di documenti e query sui dati all'interno di un raccolta.</span><span class="sxs-lookup"><span data-stu-id="2ce3b-142">hello directory contains a `pom.xml` for hello project and a `src` folder containing Java source code including `Program.java` which shows how perform simple operations with Azure Cosmos DB like creating documents and querying data within a collection.</span></span> <span data-ttu-id="2ce3b-143">Hello `pom.xml` include una dipendenza hello [DocumentDB SDK per Java su Maven](https://mvnrepository.com/artifact/com.microsoft.azure/azure-documentdb).</span><span class="sxs-lookup"><span data-stu-id="2ce3b-143">hello `pom.xml` includes a dependency on hello [DocumentDB Java SDK on Maven](https://mvnrepository.com/artifact/com.microsoft.azure/azure-documentdb).</span></span>

    <dependency>
        <groupId>com.microsoft.azure</groupId>
        <artifactId>azure-documentdb</artifactId>
        <version>LATEST</version>
    </dependency>

## <span data-ttu-id="2ce3b-144"><a id="Connect"></a>Passaggio 3: Connettere l'account di Azure Cosmos DB tooan</span><span class="sxs-lookup"><span data-stu-id="2ce3b-144"><a id="Connect"></a>Step 3: Connect tooan Azure Cosmos DB account</span></span>
<span data-ttu-id="2ce3b-145">Successivamente, head nuovamente toohello [portale Azure](https://portal.azure.com) tooretrieve l'endpoint e la chiave master primaria.</span><span class="sxs-lookup"><span data-stu-id="2ce3b-145">Next, head back toohello [Azure Portal](https://portal.azure.com) tooretrieve your endpoint and primary master key.</span></span> <span data-ttu-id="2ce3b-146">Hello Azure Cosmos DB endpoint e la chiave primaria sono necessari per l'applicazione toounderstand in tooconnect e per Azure Cosmos DB tootrust connessione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="2ce3b-146">hello Azure Cosmos DB endpoint and primary key are necessary for your application toounderstand where tooconnect to, and for Azure Cosmos DB tootrust your application's connection.</span></span>

<span data-ttu-id="2ce3b-147">In hello portale di Azure, passare tooyour Azure Cosmos DB account e quindi fare clic su **chiavi**.</span><span class="sxs-lookup"><span data-stu-id="2ce3b-147">In hello Azure Portal, navigate tooyour Azure Cosmos DB account, and then click **Keys**.</span></span> <span data-ttu-id="2ce3b-148">Copiare hello URI dal portale di hello e incollarlo in `https://FILLME.documents.azure.com` nel file Program.java hello.</span><span class="sxs-lookup"><span data-stu-id="2ce3b-148">Copy hello URI from hello portal and paste it into `https://FILLME.documents.azure.com` in hello Program.java file.</span></span> <span data-ttu-id="2ce3b-149">Quindi copia hello chiave primaria dal portale hello e incollarlo in `FILLME`.</span><span class="sxs-lookup"><span data-stu-id="2ce3b-149">Then copy hello PRIMARY KEY from hello portal and paste it into `FILLME`.</span></span>

    this.client = new DocumentClient(
        "https://FILLME.documents.azure.com",
        "FILLME"
        , new ConnectionPolicy(),
        ConsistencyLevel.Session);

![Cattura di schermata del portale di Azure utilizzato da hello NoSQL esercitazione toocreate un'applicazione console Java hello.][keys]

## <a name="step-4-create-a-database"></a><span data-ttu-id="2ce3b-152">Passaggio 4: Creare un database</span><span class="sxs-lookup"><span data-stu-id="2ce3b-152">Step 4: Create a database</span></span>
<span data-ttu-id="2ce3b-153">Il database di Azure Cosmos [database](documentdb-resources.md#databases) possono essere create usando hello [createDatabase](/java/api/com.microsoft.azure.documentdb._document_client.createdatabase) metodo hello **DocumentClient** classe.</span><span class="sxs-lookup"><span data-stu-id="2ce3b-153">Your Azure Cosmos DB [database](documentdb-resources.md#databases) can be created by using hello [createDatabase](/java/api/com.microsoft.azure.documentdb._document_client.createdatabase) method of hello **DocumentClient** class.</span></span> <span data-ttu-id="2ce3b-154">Un database è contenitore logico di hello di archiviazione di documenti JSON partizionato nelle raccolte.</span><span class="sxs-lookup"><span data-stu-id="2ce3b-154">A database is hello logical container of JSON document storage partitioned across collections.</span></span>

    Database database = new Database();
    database.setId("familydb");
    this.client.createDatabase(database, null);

## <span data-ttu-id="2ce3b-155"><a id="CreateColl"></a>Passaggio 5: Creare una raccolta</span><span class="sxs-lookup"><span data-stu-id="2ce3b-155"><a id="CreateColl"></a>Step 5: Create a collection</span></span>
> [!WARNING]
> <span data-ttu-id="2ce3b-156">**createCollection** crea una nuova raccolta con velocità effettiva riservata, che presenta implicazioni in termini di prezzi.</span><span class="sxs-lookup"><span data-stu-id="2ce3b-156">**createCollection** creates a new collection with reserved throughput, which has pricing implications.</span></span> <span data-ttu-id="2ce3b-157">Per altre informazioni, visitare la [pagina relativa ai prezzi](https://azure.microsoft.com/pricing/details/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="2ce3b-157">For more details, visit our [pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/).</span></span>
> 
> 

<span data-ttu-id="2ce3b-158">Oggetto [raccolta](documentdb-resources.md#collections) possono essere create usando hello [createCollection](/java/api/com.microsoft.azure.documentdb._document_client.createcollection) metodo hello **DocumentClient** classe.</span><span class="sxs-lookup"><span data-stu-id="2ce3b-158">A [collection](documentdb-resources.md#collections) can be created by using hello [createCollection](/java/api/com.microsoft.azure.documentdb._document_client.createcollection) method of hello **DocumentClient** class.</span></span> <span data-ttu-id="2ce3b-159">Una raccolta è un contenitore di documenti JSON e di logica dell'applicazione JavaScript associata.</span><span class="sxs-lookup"><span data-stu-id="2ce3b-159">A collection is a container of JSON documents and associated JavaScript application logic.</span></span>


    DocumentCollection collectionInfo = new DocumentCollection();
    collectionInfo.setId("familycoll");

    // Azure Cosmos DB collections can be reserved with throughput specified in request units/second. 
    // Here we create a collection with 400 RU/s.
    RequestOptions requestOptions = new RequestOptions();
    requestOptions.setOfferThroughput(400);

    this.client.createCollection("/dbs/familydb", collectionInfo, requestOptions);

## <span data-ttu-id="2ce3b-160"><a id="CreateDoc"></a>Passaggio 6: Creare documenti JSON</span><span class="sxs-lookup"><span data-stu-id="2ce3b-160"><a id="CreateDoc"></a>Step 6: Create JSON documents</span></span>
<span data-ttu-id="2ce3b-161">Oggetto [documento](documentdb-resources.md#documents) possono essere create usando hello [createDocument](/java/api/com.microsoft.azure.documentdb._document_client.createdocument) metodo hello **DocumentClient** classe.</span><span class="sxs-lookup"><span data-stu-id="2ce3b-161">A [document](documentdb-resources.md#documents) can be created by using hello [createDocument](/java/api/com.microsoft.azure.documentdb._document_client.createdocument) method of hello **DocumentClient** class.</span></span> <span data-ttu-id="2ce3b-162">I documenti sono contenuto JSON definito dall'utente (arbitrario).</span><span class="sxs-lookup"><span data-stu-id="2ce3b-162">Documents are user-defined (arbitrary) JSON content.</span></span> <span data-ttu-id="2ce3b-163">Ora è possibile inserire uno o più documenti.</span><span class="sxs-lookup"><span data-stu-id="2ce3b-163">We can now insert one or more documents.</span></span> <span data-ttu-id="2ce3b-164">Se si dispongono già di dati desiderato toostore nel database, è possibile utilizzare Azure Cosmos DB [dello strumento di migrazione dei dati](import-data.md) dati hello tooimport in un database.</span><span class="sxs-lookup"><span data-stu-id="2ce3b-164">If you already have data you'd like toostore in your database, you can use Azure Cosmos DB's [Data Migration tool](import-data.md) tooimport hello data into a database.</span></span>

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

![Diagramma che illustra relazione gerarchica di hello tra account hello, database online hello, raccolta hello e documenti hello utilizzato dai hello NoSQL esercitazione toocreate un'applicazione console Java](./media/documentdb-get-started/nosql-tutorial-account-database.png)

## <span data-ttu-id="2ce3b-166"><a id="Query"></a>Passaggio 7: Eseguire query sulle risorse di Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="2ce3b-166"><a id="Query"></a>Step 7: Query Azure Cosmos DB resources</span></span>
<span data-ttu-id="2ce3b-167">Azure Cosmos DB supporta [query complesse](documentdb-sql-query.md) sui documenti JSON archiviati in ogni raccolta.</span><span class="sxs-lookup"><span data-stu-id="2ce3b-167">Azure Cosmos DB supports rich [queries](documentdb-sql-query.md) against JSON documents stored in each collection.</span></span>  <span data-ttu-id="2ce3b-168">Hello codice di esempio seguente viene illustrato come tooquery dei documenti in Azure Cosmos DB utilizzando la sintassi SQL con hello [queryDocuments](/java/api/com.microsoft.azure.documentdb._document_client.querydocuments) metodo.</span><span class="sxs-lookup"><span data-stu-id="2ce3b-168">hello following sample code shows how tooquery documents in Azure Cosmos DB using SQL syntax with hello [queryDocuments](/java/api/com.microsoft.azure.documentdb._document_client.querydocuments) method.</span></span>

    FeedResponse<Document> queryResults = this.client.queryDocuments(
        "/dbs/familydb/colls/familycoll",
        "SELECT * FROM Family WHERE Family.lastName = 'Andersen'", 
        null);

    System.out.println("Running SQL query...");
    for (Document family : queryResults.getQueryIterable()) {
        System.out.println(String.format("\tRead %s", family));
    }

## <span data-ttu-id="2ce3b-169"><a id="ReplaceDocument"></a>Passaggio 8: Sostituire un documento JSON</span><span class="sxs-lookup"><span data-stu-id="2ce3b-169"><a id="ReplaceDocument"></a>Step 8: Replace JSON document</span></span>
<span data-ttu-id="2ce3b-170">Azure Cosmos DB supporta l'aggiornamento di documenti JSON tramite hello [replaceDocument](/java/api/com.microsoft.azure.documentdb._document_client.replacedocument) metodo.</span><span class="sxs-lookup"><span data-stu-id="2ce3b-170">Azure Cosmos DB supports updating JSON documents using hello [replaceDocument](/java/api/com.microsoft.azure.documentdb._document_client.replacedocument) method.</span></span>

    // Update a property
    andersenFamily.Children[0].Grade = 6;

    this.client.replaceDocument(
        "/dbs/familydb/colls/familycoll/docs/Andersen.1", 
        andersenFamily,
        null);

## <span data-ttu-id="2ce3b-171"><a id="DeleteDocument"></a>Passaggio 9: Eliminare un documento JSON</span><span class="sxs-lookup"><span data-stu-id="2ce3b-171"><a id="DeleteDocument"></a>Step 9: Delete JSON document</span></span>
<span data-ttu-id="2ce3b-172">Analogamente, Azure Cosmos DB supporta l'eliminazione di documenti JSON tramite hello [deleteDocument](/java/api/com.microsoft.azure.documentdb._document_client.deletedocument) metodo.</span><span class="sxs-lookup"><span data-stu-id="2ce3b-172">Similarly, Azure Cosmos DB supports deleting JSON documents using hello [deleteDocument](/java/api/com.microsoft.azure.documentdb._document_client.deletedocument) method.</span></span>  

    this.client.delete("/dbs/familydb/colls/familycoll/docs/Andersen.1", null);

## <span data-ttu-id="2ce3b-173"><a id="DeleteDatabase"></a>Passaggio 10: Eliminare database hello</span><span class="sxs-lookup"><span data-stu-id="2ce3b-173"><a id="DeleteDatabase"></a>Step 10: Delete hello database</span></span>
<span data-ttu-id="2ce3b-174">L'eliminazione database hello creato rimuove database hello e tutte le risorse di elementi figlio (raccolte, documenti e così via).</span><span class="sxs-lookup"><span data-stu-id="2ce3b-174">Deleting hello created database removes hello database and all children resources (collections, documents, etc.).</span></span>

    this.client.deleteDatabase("/dbs/familydb", null);

## <span data-ttu-id="2ce3b-175"><a id="Run"></a>Passaggio 11: Eseguire l'intera applicazione console Java</span><span class="sxs-lookup"><span data-stu-id="2ce3b-175"><a id="Run"></a>Step 11: Run your Java console application all together!</span></span>
<span data-ttu-id="2ce3b-176">un'applicazione hello toorun dalla console di hello passare toohello cartella del progetto e compilazione Maven utilizzando:</span><span class="sxs-lookup"><span data-stu-id="2ce3b-176">toorun hello application from hello console, navigate toohello project folder and compile using Maven:</span></span>
    
    mvn package

<span data-ttu-id="2ce3b-177">Esecuzione `mvn package` Scarica libreria Azure Cosmos DB più recente di hello Maven e produce `GetStarted-0.0.1-SNAPSHOT.jar`.</span><span class="sxs-lookup"><span data-stu-id="2ce3b-177">Running `mvn package` downloads hello latest Azure Cosmos DB library from Maven and produces `GetStarted-0.0.1-SNAPSHOT.jar`.</span></span> <span data-ttu-id="2ce3b-178">Eseguire quindi l'applicazione hello eseguendo:</span><span class="sxs-lookup"><span data-stu-id="2ce3b-178">Then run hello app by running:</span></span>

    mvn exec:java -D exec.mainClass=GetStarted.Program

<span data-ttu-id="2ce3b-179">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="2ce3b-179">Congratulations!</span></span> <span data-ttu-id="2ce3b-180">L'esercitazione su NoSQL è stata completata ed è stata creata un'applicazione console Java funzionante.</span><span class="sxs-lookup"><span data-stu-id="2ce3b-180">You've completed this NoSQL tutorial and have a working Java console application!</span></span>

## <a name="next-steps"></a><span data-ttu-id="2ce3b-181">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2ce3b-181">Next steps</span></span>
* <span data-ttu-id="2ce3b-182">Per un'esercitazione su app Web Java,</span><span class="sxs-lookup"><span data-stu-id="2ce3b-182">Want a Java web app tutorial?</span></span> <span data-ttu-id="2ce3b-183">vedere [Creazione di un'applicazione Web Java con Azure Cosmos DB](documentdb-java-application.md).</span><span class="sxs-lookup"><span data-stu-id="2ce3b-183">See [Build a web application with Java using Azure Cosmos DB](documentdb-java-application.md).</span></span>
* <span data-ttu-id="2ce3b-184">Informazioni su come troppo[monitorare un account Azure Cosmos DB](monitor-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="2ce3b-184">Learn how too[monitor an Azure Cosmos DB account](monitor-accounts.md).</span></span>
* <span data-ttu-id="2ce3b-185">Eseguire query su questo set di dati di esempio in hello [Query Playground](https://www.documentdb.com/sql/demo).</span><span class="sxs-lookup"><span data-stu-id="2ce3b-185">Run queries against our sample dataset in hello [Query Playground](https://www.documentdb.com/sql/demo).</span></span>
* <span data-ttu-id="2ce3b-186">Ulteriori informazioni sul modello di programmazione hello nella sezione sviluppo di hello hello [pagina della documentazione di Azure Cosmos DB](https://azure.microsoft.com/documentation/services/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="2ce3b-186">Learn more about hello programming model in hello Develop section of hello [Azure Cosmos DB documentation page](https://azure.microsoft.com/documentation/services/documentdb/).</span></span>

[keys]: media/documentdb-get-started/nosql-tutorial-keys.png
