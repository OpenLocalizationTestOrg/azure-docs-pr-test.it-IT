---
title: Programmazione JavaScript lato server per Azure Cosmos DB | Microsoft Docs
description: Informazioni su come usare Azure Cosmos DB per scrivere stored procedure, trigger del database e funzioni definite dall'utente in JavaScript. Ottenere suggerimenti sulla programmazione di database e altro ancora.
keywords: Trigger di database, stored procedure, programma di database, sproc, documentdb, azure, Microsoft Azure
services: cosmos-db
documentationcenter: 
author: aliuy
manager: jhubbard
editor: mimig
ms.assetid: 0fba7ebd-a4fc-4253-a786-97f1354fbf17
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2016
ms.author: andrl
ms.openlocfilehash: 8cddc7a8c9aa677b9c93bee3a7e05c226cc1f655
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="azure-cosmos-db-server-side-programming-stored-procedures-database-triggers-and-udfs"></a><span data-ttu-id="d4547-105">Programmazione lato server per Azure Cosmos DB: stored procedure, trigger del database e funzioni definite dall'utente</span><span class="sxs-lookup"><span data-stu-id="d4547-105">Azure Cosmos DB server-side programming: Stored procedures, database triggers, and UDFs</span></span>
<span data-ttu-id="d4547-106">L'esecuzione integrata e transazionale di JavaScript con il linguaggio di Azure Cosmos DB permette agli sviluppatori di scrivere **stored procedure**, **trigger** e **funzioni definite dall'utente** in modo nativo in [ECMAScript 2015](http://www.ecma-international.org/ecma-262/6.0/) JavaScript.</span><span class="sxs-lookup"><span data-stu-id="d4547-106">Learn how Azure Cosmos DB’s language integrated, transactional execution of JavaScript lets developers write **stored procedures**, **triggers** and **user defined functions (UDFs)** natively in an [ECMAScript 2015](http://www.ecma-international.org/ecma-262/6.0/) JavaScript.</span></span> <span data-ttu-id="d4547-107">Ciò consente di scrivere la logica dell'applicazione del programma del database che può essere inserita ed eseguita direttamente nelle partizioni di archiviazione del database.</span><span class="sxs-lookup"><span data-stu-id="d4547-107">This allows you to write database program application logic that can be shipped and executed directly on the database storage partitions.</span></span> 

<span data-ttu-id="d4547-108">Per iniziare, è consigliabile guardare il video seguente, in cui Andrew Liu introduce brevemente il modello di programmazione database lato server di Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d4547-108">We recommend getting started by watching the following video, where Andrew Liu provides a brief introduction to Cosmos DB's server-side database programming model.</span></span> 

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-Demo-A-Quick-Intro-to-Azure-DocumentDBs-Server-Side-Javascript/player]
> 
> 

<span data-ttu-id="d4547-109">Tornare quindi a questo articolo, che fornisce risposte alle domande seguenti:</span><span class="sxs-lookup"><span data-stu-id="d4547-109">Then, return to this article, where you'll learn the answers to the following questions:</span></span>  

* <span data-ttu-id="d4547-110">Come è possibile scrivere una stored procedure, un trigger o una funzione definita dall'utente usando JavaScript?</span><span class="sxs-lookup"><span data-stu-id="d4547-110">How do I write a a stored procedure, trigger, or UDF using JavaScript?</span></span>
* <span data-ttu-id="d4547-111">In che modo Cosmos DB garantisce proprietà ACID?</span><span class="sxs-lookup"><span data-stu-id="d4547-111">How does Cosmos DB guarantee ACID?</span></span>
* <span data-ttu-id="d4547-112">Come funzionano le transazioni in Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="d4547-112">How do transactions work in Cosmos DB?</span></span>
* <span data-ttu-id="d4547-113">Cosa sono i pre-trigger e i post-trigger e come si scrivono?</span><span class="sxs-lookup"><span data-stu-id="d4547-113">What are pre-triggers and post-triggers and how do I write one?</span></span>
* <span data-ttu-id="d4547-114">Come si registra e si esegue una stored procedure, un trigger o una funzione definita dall'utente in modalità RESTful usando HTTP?</span><span class="sxs-lookup"><span data-stu-id="d4547-114">How do I register and execute a stored procedure, trigger, or UDF in a RESTful manner by using HTTP?</span></span>
* <span data-ttu-id="d4547-115">Quali SDK di Cosmos DB sono disponibili per la creazione e l'esecuzione di stored procedure, trigger e funzioni definite dall'utente?</span><span class="sxs-lookup"><span data-stu-id="d4547-115">What Cosmos DB SDKs are available to create and execute stored procedures, triggers, and UDFs?</span></span>

## <a name="introduction-to-stored-procedure-and-udf-programming"></a><span data-ttu-id="d4547-116">Introduzione alle stored procedure e alla programmazione delle funzioni definite dall'utente</span><span class="sxs-lookup"><span data-stu-id="d4547-116">Introduction to Stored Procedure and UDF Programming</span></span>
<span data-ttu-id="d4547-117">Questo approccio di *"JavaScript come nuovo T-SQL"* libera gli sviluppatori di applicazioni dalle complessità delle mancate corrispondenze nel sistema dei tipi e delle tecnologie di mapping relazionale a oggetti.</span><span class="sxs-lookup"><span data-stu-id="d4547-117">This approach of *“JavaScript as a modern day T-SQL”* frees application developers from the complexities of type system mismatches and object-relational mapping technologies.</span></span> <span data-ttu-id="d4547-118">Comporta anche una serie di vantaggi intrinseci che possono essere utili per creare applicazioni avanzate:</span><span class="sxs-lookup"><span data-stu-id="d4547-118">It also has a number of intrinsic advantages that can be utilized to build rich applications:</span></span>  

* <span data-ttu-id="d4547-119">**Logica procedurale:** come linguaggio di programmazione di alto livello, JavaScript offre un'interfaccia completa e familiare per esprimere la logica di business.</span><span class="sxs-lookup"><span data-stu-id="d4547-119">**Procedural Logic:** JavaScript as a high level programming language, provides a rich and familiar interface to express business logic.</span></span> <span data-ttu-id="d4547-120">È possibile eseguire sequenze complesse di operazioni a ridosso dei dati.</span><span class="sxs-lookup"><span data-stu-id="d4547-120">You can perform complex sequences of operations closer to the data.</span></span>
* <span data-ttu-id="d4547-121">**Transazioni atomiche:** Cosmos DB garantisce che le operazioni di database all'interno di una singola stored procedure o un trigger siano atomiche.</span><span class="sxs-lookup"><span data-stu-id="d4547-121">**Atomic Transactions:** Cosmos DB guarantees that database operations performed inside a single stored procedure or trigger are atomic.</span></span> <span data-ttu-id="d4547-122">Di conseguenza, un'applicazione potrà combinare le operazioni correlate in un unico batch, in modo che o tutte o nessuna di esse avranno esito positivo.</span><span class="sxs-lookup"><span data-stu-id="d4547-122">This lets an application combine related operations in a single batch so that either all of them succeed or none of them succeed.</span></span> 
* <span data-ttu-id="d4547-123">**Prestazioni:** il mapping intrinseco di JSON al sistema di tipi del linguaggio JavaScript e il fatto che JSON rappresenta anche l'unità di base di archiviazione in Cosmos DB permette di eseguire una serie di ottimizzazioni, tra cui la materializzazione differita dei documenti JSON nel pool di buffer e la loro disponibilità su richiesta per il codice in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="d4547-123">**Performance:** The fact that JSON is intrinsically mapped to the Javascript language type system and is also the basic unit of storage in Cosmos DB allows for a number of optimizations like lazy materialization of JSON documents in the buffer pool and making them available on-demand to the executing code.</span></span> <span data-ttu-id="d4547-124">Vi sono altri vantaggi associati all'integrazione della logica di business nel database:</span><span class="sxs-lookup"><span data-stu-id="d4547-124">There are more performance benefits associated with shipping business logic to the database:</span></span>
  
  * <span data-ttu-id="d4547-125">Invio in batch: gli sviluppatori possono raggruppare le operazioni, come gli inserimenti, e inviarle in blocco.</span><span class="sxs-lookup"><span data-stu-id="d4547-125">Batching – Developers can group operations like inserts and submit them in bulk.</span></span> <span data-ttu-id="d4547-126">Ciò comporta una drastica riduzione del costo legato alla latenza del traffico di rete e dei costi generali di archiviazione per la creazione di transazioni separate.</span><span class="sxs-lookup"><span data-stu-id="d4547-126">The network traffic latency cost and the store overhead to create separate transactions are reduced significantly.</span></span> 
  * <span data-ttu-id="d4547-127">Precompilazione: Cosmos DB precompila stored procedure, trigger e funzioni definite dall'utente per evitare il costo della compilazione JavaScript per ogni chiamata.</span><span class="sxs-lookup"><span data-stu-id="d4547-127">Pre-compilation – Cosmos DB precompiles stored procedures, triggers and user defined functions (UDFs) to avoid JavaScript compilation cost for each invocation.</span></span> <span data-ttu-id="d4547-128">I costi generali di compilazione del codice byte per la logica procedurale vengono ammortizzati a un valore minimo.</span><span class="sxs-lookup"><span data-stu-id="d4547-128">The overhead of building the byte code for the procedural logic is amortized to a minimal value.</span></span>
  * <span data-ttu-id="d4547-129">Sequenziazione: molte operazioni necessitano di un effetto collaterale ("trigger") che implica potenzialmente l'esecuzione di una o più operazioni di archiviazione secondarie.</span><span class="sxs-lookup"><span data-stu-id="d4547-129">Sequencing – Many operations need a side-effect (“trigger”) that potentially involves doing one or many secondary store operations.</span></span> <span data-ttu-id="d4547-130">Atomicità a parte, offre prestazioni migliori quando viene passata al server.</span><span class="sxs-lookup"><span data-stu-id="d4547-130">Aside from atomicity, this is more performant when moved to the server.</span></span> 
* <span data-ttu-id="d4547-131">**Incapsulamento:** è possibile usare le stored procedure per raggruppare la logica di business in un solo posto.</span><span class="sxs-lookup"><span data-stu-id="d4547-131">**Encapsulation:** Stored procedures can be used to group business logic in one place.</span></span> <span data-ttu-id="d4547-132">Ciò comporta due vantaggi:</span><span class="sxs-lookup"><span data-stu-id="d4547-132">This has two advantages:</span></span>
  * <span data-ttu-id="d4547-133">Aggiunge un livello di astrazione al di sopra dei dati non elaborati, consentendo ai responsabili dell'architettura dati di far evolvere le proprie applicazioni indipendentemente dai dati.</span><span class="sxs-lookup"><span data-stu-id="d4547-133">It adds an abstraction layer on top of the raw data, which enables data architects to evolve their applications independently from the data.</span></span> <span data-ttu-id="d4547-134">Si tratta di una caratteristica particolarmente vantaggiosa quando i dati sono privi di schema, a causa dei presupposti transitori che potrebbe essere necessario integrare nell'applicazione qualora fosse necessario gestire i dati direttamente.</span><span class="sxs-lookup"><span data-stu-id="d4547-134">This is particularly advantageous when the data is schema-less, due to the brittle assumptions that may need to be baked into the application if they have to deal with data directly.</span></span>  
  * <span data-ttu-id="d4547-135">Questa astrazione consente alle grandi imprese di proteggere i propri dati semplificando l'accesso dagli script.</span><span class="sxs-lookup"><span data-stu-id="d4547-135">This abstraction lets enterprises keep their data secure by streamlining the access from the scripts.</span></span>  

<span data-ttu-id="d4547-136">La creazione e l'esecuzione di trigger del database, stored procedure e operatori di query personalizzati sono supportate tramite l'[API REST](/rest/api/documentdb/), [Azure DocumentDB Studio](https://github.com/mingaliu/DocumentDBStudio/releases) e gli [SDK client](documentdb-sdk-dotnet.md) in molte piattaforme, tra cui .NET, Node.js e JavaScript.</span><span class="sxs-lookup"><span data-stu-id="d4547-136">The creation and execution of database triggers, stored procedure and custom query operators is supported through the [REST API](/rest/api/documentdb/), [Azure DocumentDB Studio](https://github.com/mingaliu/DocumentDBStudio/releases), and [client SDKs](documentdb-sdk-dotnet.md) in many platforms including .NET, Node.js and JavaScript.</span></span>

<span data-ttu-id="d4547-137">Questa esercitazione usa [Node.js SDK con promesse Q](http://azure.github.io/azure-documentdb-node-q/) per illustrare la sintassi e l'uso di stored procedure, trigger e funzioni definite dall'utente.</span><span class="sxs-lookup"><span data-stu-id="d4547-137">This tutorial uses the [Node.js SDK with Q Promises](http://azure.github.io/azure-documentdb-node-q/) to illustrate syntax and usage of stored procedures, triggers, and UDFs.</span></span>   

## <a name="stored-procedures"></a><span data-ttu-id="d4547-138">Stored procedure</span><span class="sxs-lookup"><span data-stu-id="d4547-138">Stored procedures</span></span>
### <a name="example-write-a-simple-stored-procedure"></a><span data-ttu-id="d4547-139">Esempio: scrivere una stored procedure semplice</span><span class="sxs-lookup"><span data-stu-id="d4547-139">Example: Write a simple stored procedure</span></span>
<span data-ttu-id="d4547-140">Per cominciare, si analizzerà una semplice stored procedure che restituisce una risposta "Hello World".</span><span class="sxs-lookup"><span data-stu-id="d4547-140">Let’s start with a simple stored procedure that returns a “Hello World” response.</span></span>

    var helloWorldStoredProc = {
        id: "helloWorld",
        serverScript: function () {
            var context = getContext();
            var response = context.getResponse();

            response.setBody("Hello, World");
        }
    }


<span data-ttu-id="d4547-141">Le stored procedure vengono registrate per ogni raccolta e funzionano in qualsiasi documento e allegato presente nella raccolta.</span><span class="sxs-lookup"><span data-stu-id="d4547-141">Stored procedures are registered per collection, and can operate on any document and attachment present in that collection.</span></span> <span data-ttu-id="d4547-142">Nel frammento seguente viene spiegato come registrare la stored procedure helloWorld con una raccolta.</span><span class="sxs-lookup"><span data-stu-id="d4547-142">The following snippet shows how to register the helloWorld stored procedure with a collection.</span></span> 

    // register the stored procedure
    var createdStoredProcedure;
    client.createStoredProcedureAsync('dbs/testdb/colls/testColl', helloWorldStoredProc)
        .then(function (response) {
            createdStoredProcedure = response.resource;
            console.log("Successfully created stored procedure");
        }, function (error) {
            console.log("Error", error);
        });


<span data-ttu-id="d4547-143">Dopo aver registrato la stored procedure è possibile eseguirla a fronte della raccolta e leggere i risultati sul client.</span><span class="sxs-lookup"><span data-stu-id="d4547-143">Once the stored procedure is registered, we can execute it against the collection, and read the results back at the client.</span></span> 

    // execute the stored procedure
    client.executeStoredProcedureAsync('dbs/testdb/colls/testColl/sprocs/helloWorld')
        .then(function (response) {
            console.log(response.result); // "Hello, World"
        }, function (err) {
            console.log("Error", error);
        });


<span data-ttu-id="d4547-144">L'oggetto contesto offre accesso a tutte le operazioni che è possibile eseguire nelle risorse di archiviazione di Cosmos DB, oltre all'accesso agli oggetti richiesta e risposta.</span><span class="sxs-lookup"><span data-stu-id="d4547-144">The context object provides access to all operations that can be performed on Cosmos DB storage, as well as access to the request and response objects.</span></span> <span data-ttu-id="d4547-145">In questo caso, è stata usato l'oggetto risposta per impostare il corpo della risposta restituita al client.</span><span class="sxs-lookup"><span data-stu-id="d4547-145">In this case, we used the response object to set the body of the response that was sent back to the client.</span></span> <span data-ttu-id="d4547-146">Per altre informazioni, vedere la [documentazione relativa all'SDK del server JavaScript di Cosmos DB](http://azure.github.io/azure-documentdb-js-server/).</span><span class="sxs-lookup"><span data-stu-id="d4547-146">For more details, refer to the [Azure Cosmos DB JavaScript server SDK documentation](http://azure.github.io/azure-documentdb-js-server/).</span></span>  

<span data-ttu-id="d4547-147">Elaborando ulteriormente questo esempio, è possibile aggiungere alla stored procedure altre funzionalità relative al database.</span><span class="sxs-lookup"><span data-stu-id="d4547-147">Let us expand on this example and add more database related functionality to the stored procedure.</span></span> <span data-ttu-id="d4547-148">Le stored procedure possono creare, aggiornare, eseguire query ed eliminare documenti e allegati all'interno della raccolta.</span><span class="sxs-lookup"><span data-stu-id="d4547-148">Stored procedures can create, update, read, query and delete documents and attachments inside the collection.</span></span>    

### <a name="example-write-a-stored-procedure-to-create-a-document"></a><span data-ttu-id="d4547-149">Esempio: scrivere una stored procedure per creare un documento</span><span class="sxs-lookup"><span data-stu-id="d4547-149">Example: Write a stored procedure to create a document</span></span>
<span data-ttu-id="d4547-150">Il frammento successivo mostra come usare l'oggetto contesto per interagire con le risorse di Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d4547-150">The next snippet shows how to use the context object to interact with Cosmos DB resources.</span></span>

    var createDocumentStoredProc = {
        id: "createMyDocument",
        serverScript: function createMyDocument(documentToCreate) {
            var context = getContext();
            var collection = context.getCollection();

            var accepted = collection.createDocument(collection.getSelfLink(),
                  documentToCreate,
                  function (err, documentCreated) {
                      if (err) throw new Error('Error' + err.message);
                      context.getResponse().setBody(documentCreated.id)
                  });
            if (!accepted) return;
        }
    }


<span data-ttu-id="d4547-151">Questa stored procedure accetta come input documentToCreate, il corpo di un documento da creare nella raccolta corrente.</span><span class="sxs-lookup"><span data-stu-id="d4547-151">This stored procedure takes as input documentToCreate, the body of a document to be created in the current collection.</span></span> <span data-ttu-id="d4547-152">Tutte queste operazioni sono asincrone e dipendono dai callback della funzione JavaScript.</span><span class="sxs-lookup"><span data-stu-id="d4547-152">All such operations are asynchronous and depend on JavaScript function callbacks.</span></span> <span data-ttu-id="d4547-153">La funzione di callback ha due parametri: uno per l'oggetto errore in caso di errore dell'operazione e uno per l'oggetto creato.</span><span class="sxs-lookup"><span data-stu-id="d4547-153">The callback function has two parameters, one for the error object in case the operation fails, and one for the created object.</span></span> <span data-ttu-id="d4547-154">All'interno del callback, gli utenti possono gestire l'eccezione oppure generare un errore.</span><span class="sxs-lookup"><span data-stu-id="d4547-154">Inside the callback, users can either handle the exception or throw an error.</span></span> <span data-ttu-id="d4547-155">Nel caso in cui non sia disponibile un callback e si verifichi un errore, il runtime di Azure Cosmos DB genera un errore.</span><span class="sxs-lookup"><span data-stu-id="d4547-155">In case a callback is not provided and there is an error, the Azure Cosmos DB runtime throws an error.</span></span>   

<span data-ttu-id="d4547-156">Nell'esempio precedente il callback genera un errore se l'operazione non è riuscita.</span><span class="sxs-lookup"><span data-stu-id="d4547-156">In the example above, the callback throws an error if the operation failed.</span></span> <span data-ttu-id="d4547-157">In caso contrario, viene impostato l'ID del documento creato come corpo della risposta al client.</span><span class="sxs-lookup"><span data-stu-id="d4547-157">Otherwise, it sets the id of the created document as the body of the response to the client.</span></span> <span data-ttu-id="d4547-158">Ecco come viene eseguita questa stored procedure con i parametri di input.</span><span class="sxs-lookup"><span data-stu-id="d4547-158">Here is how this stored procedure is executed with input parameters.</span></span>

    // register the stored procedure
    client.createStoredProcedureAsync('dbs/testdb/colls/testColl', createDocumentStoredProc)
        .then(function (response) {
            var createdStoredProcedure = response.resource;

            // run stored procedure to create a document
            var docToCreate = {
                id: "DocFromSproc",
                book: "The Hitchhiker’s Guide to the Galaxy",
                author: "Douglas Adams"
            };

            return client.executeStoredProcedureAsync('dbs/testdb/colls/testColl/sprocs/createMyDocument',
                  docToCreate);
        }, function (error) {
            console.log("Error", error);
        })
    .then(function (response) {
        console.log(response); // "DocFromSproc"
    }, function (error) {
        console.log("Error", error);
    });


<span data-ttu-id="d4547-159">Notare che è possibile modificare questa stored procedure in modo che accetti una matrice di corpi di documenti come input e possa crearli tutti nell'esecuzione della stessa stored procedure, invece di inviare più richieste di rete per crearle individualmente.</span><span class="sxs-lookup"><span data-stu-id="d4547-159">Note that this stored procedure can be modified to take an array of document bodies as input and create them all in the same stored procedure execution instead of multiple network requests to create each of them individually.</span></span> <span data-ttu-id="d4547-160">Questo permette di implementare un'efficiente utilità di importazione in blocco per Cosmos DB, di cui si discuterà più avanti in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="d4547-160">This can be used to implement an efficient bulk importer for Cosmos DB (discussed later in this tutorial).</span></span>   

<span data-ttu-id="d4547-161">L'esempio descritto ha dimostrato come usare le stored procedure.</span><span class="sxs-lookup"><span data-stu-id="d4547-161">The example described demonstrated how to use stored procedures.</span></span> <span data-ttu-id="d4547-162">I trigger e le funzioni definite dall'utente (UDF) saranno trattati più avanti in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="d4547-162">We will cover triggers and user defined functions (UDFs) later in the tutorial.</span></span>

## <a name="database-program-transactions"></a><span data-ttu-id="d4547-163">Transazioni del programma del database</span><span class="sxs-lookup"><span data-stu-id="d4547-163">Database program transactions</span></span>
<span data-ttu-id="d4547-164">Una transazione in un tipico database può essere definita come una sequenza di operazioni eseguite come singola unità di lavoro logica.</span><span class="sxs-lookup"><span data-stu-id="d4547-164">Transaction in a typical database can be defined as a sequence of operations performed as a single logical unit of work.</span></span> <span data-ttu-id="d4547-165">Ogni transazione offre **garanzie ACID**.</span><span class="sxs-lookup"><span data-stu-id="d4547-165">Each transaction provides **ACID guarantees**.</span></span> <span data-ttu-id="d4547-166">ACID è un acronimo noto che riassume quattro proprietà: Atomicità, Coerenza, Isolamento e Durabilità.</span><span class="sxs-lookup"><span data-stu-id="d4547-166">ACID is a well-known acronym that stands for four properties -  Atomicity, Consistency, Isolation and Durability.</span></span>  

<span data-ttu-id="d4547-167">In breve, l'atomicità garantisce che tutte le operazioni eseguite nell'ambito di una transazione siano trattate come unità singola e che venga eseguito il commit di tutte le operazioni o di nessuna.</span><span class="sxs-lookup"><span data-stu-id="d4547-167">Briefly, atomicity guarantees that all the work done inside a transaction is treated as a single unit where either all of it is committed or none.</span></span> <span data-ttu-id="d4547-168">La coerenza garantisce che i dati siano sempre in ottimo stato interno in tutte le transazioni.</span><span class="sxs-lookup"><span data-stu-id="d4547-168">Consistency makes sure that the data is always in a good internal state across transactions.</span></span> <span data-ttu-id="d4547-169">L'isolamento garantisce che non vi siano transazioni conflittuali; in generale, la maggior parte dei sistemi commerciali offre più livelli di isolamento utilizzabili in base alle esigenze dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="d4547-169">Isolation guarantees that no two transactions interfere with each other – generally, most commercial systems provide multiple isolation levels that can be used based on the application needs.</span></span> <span data-ttu-id="d4547-170">La durabilità assicura che qualsiasi modifica di cui sia stato eseguito il commit nel database sia sempre presente.</span><span class="sxs-lookup"><span data-stu-id="d4547-170">Durability ensures that any change that’s committed in the database will always be present.</span></span>   

<span data-ttu-id="d4547-171">JavaScript in Cosmos DB è ospitato nello stesso spazio di memoria del database.</span><span class="sxs-lookup"><span data-stu-id="d4547-171">In Cosmos DB, JavaScript is hosted in the same memory space as the database.</span></span> <span data-ttu-id="d4547-172">Di conseguenza, le richieste effettuate nell'ambito delle stored procedure e dei trigger vengono eseguite nello stesso ambito di una sessione di database.</span><span class="sxs-lookup"><span data-stu-id="d4547-172">Hence, requests made within stored procedures and triggers execute in the same scope of a database session.</span></span> <span data-ttu-id="d4547-173">In questo modo Cosmos DB può garantire proprietà ACID per tutte le transazioni che fanno parte di una singola stored procedure o un unico trigger.</span><span class="sxs-lookup"><span data-stu-id="d4547-173">This enables Cosmos DB to guarantee ACID for all operations that are part of a single stored procedure/trigger.</span></span> <span data-ttu-id="d4547-174">Considerare la definizione della stored procedure seguente:</span><span class="sxs-lookup"><span data-stu-id="d4547-174">Consider the following stored procedure definition:</span></span>

    // JavaScript source code
    var exchangeItemsSproc = {
        id: "exchangeItems",
        serverScript: function (playerId1, playerId2) {
            var context = getContext();
            var collection = context.getCollection();
            var response = context.getResponse();

            var player1Document, player2Document;

            // query for players
            var filterQuery = 'SELECT * FROM Players p where p.id  = "' + playerId1 + '"';
            var accept = collection.queryDocuments(collection.getSelfLink(), filterQuery, {},
                function (err, documents, responseOptions) {
                    if (err) throw new Error("Error" + err.message);

                    if (documents.length != 1) throw "Unable to find both names";
                    player1Document = documents[0];

                    var filterQuery2 = 'SELECT * FROM Players p where p.id = "' + playerId2 + '"';
                    var accept2 = collection.queryDocuments(collection.getSelfLink(), filterQuery2, {},
                        function (err2, documents2, responseOptions2) {
                            if (err2) throw new Error("Error" + err2.message);
                            if (documents2.length != 1) throw "Unable to find both names";
                            player2Document = documents2[0];
                            swapItems(player1Document, player2Document);
                            return;
                        });
                    if (!accept2) throw "Unable to read player details, abort ";
                });

            if (!accept) throw "Unable to read player details, abort ";

            // swap the two players’ items
            function swapItems(player1, player2) {
                var player1ItemSave = player1.item;
                player1.item = player2.item;
                player2.item = player1ItemSave;

                var accept = collection.replaceDocument(player1._self, player1,
                    function (err, docReplaced) {
                        if (err) throw "Unable to update player 1, abort ";

                        var accept2 = collection.replaceDocument(player2._self, player2,
                            function (err2, docReplaced2) {
                                if (err) throw "Unable to update player 2, abort"
                            });

                        if (!accept2) throw "Unable to update player 2, abort";
                    });

                if (!accept) throw "Unable to update player 1, abort";
            }
        }
    }

    // register the stored procedure in Node.js client
    client.createStoredProcedureAsync(collection._self, exchangeItemsSproc)
        .then(function (response) {
            var createdStoredProcedure = response.resource;
        }
    );

<span data-ttu-id="d4547-175">Questa stored procedure usa le transazioni in un'applicazione di gioco per scambiare elementi tra due giocatori in un'unica operazione.</span><span class="sxs-lookup"><span data-stu-id="d4547-175">This stored procedure uses transactions within a gaming app to trade items between two players in a single operation.</span></span> <span data-ttu-id="d4547-176">La stored procedure prova a leggere due documenti, ciascuno corrispondente all'ID del giocatore passato come argomento.</span><span class="sxs-lookup"><span data-stu-id="d4547-176">The stored procedure attempts to read two documents each corresponding to the player IDs passed in as an argument.</span></span> <span data-ttu-id="d4547-177">Se vengono trovati i documenti di entrambi i giocatori, la stored procedure aggiorna i documenti scambiando gli elementi.</span><span class="sxs-lookup"><span data-stu-id="d4547-177">If both player documents are found, then the stored procedure updates the documents by swapping their items.</span></span> <span data-ttu-id="d4547-178">Se si verificano errori lungo il percorso, viene generata un'eccezione JavaScript che interrompe implicitamente la transazione.</span><span class="sxs-lookup"><span data-stu-id="d4547-178">If any errors are encountered along the way, it throws a JavaScript exception that implicitly aborts the transaction.</span></span>

<span data-ttu-id="d4547-179">Se la stored procedure della raccolta è registrata in una raccolta a partizione singola, la transazione ha come ambito tutti i documenti all'interno della raccolta.</span><span class="sxs-lookup"><span data-stu-id="d4547-179">If the collection the stored procedure is registered against is a single-partition collection, then the transaction is scoped to all the documents within the collection.</span></span> <span data-ttu-id="d4547-180">Se la raccolta è partizionata, le stored procedure vengono eseguite nell'ambito della transazione di una singola chiave di partizione.</span><span class="sxs-lookup"><span data-stu-id="d4547-180">If the collection is partitioned, then stored procedures are executed in the transaction scope of a single partition key.</span></span> <span data-ttu-id="d4547-181">Ogni esecuzione di stored procedure deve quindi includere un valore di chiave di partizione corrispondente all'ambito in cui la transazione deve essere eseguita.</span><span class="sxs-lookup"><span data-stu-id="d4547-181">Each stored procedure execution must then include a partition key value corresponding to the scope the transaction must run under.</span></span> <span data-ttu-id="d4547-182">Per altri dettagli, vedere l'articolo relativo al [partizionamento di Azure Cosmos DB](partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="d4547-182">For more details, see [Azure Cosmos DB Partitioning](partition-data.md).</span></span>

### <a name="commit-and-rollback"></a><span data-ttu-id="d4547-183">Commit e rollback</span><span class="sxs-lookup"><span data-stu-id="d4547-183">Commit and rollback</span></span>
<span data-ttu-id="d4547-184">Le transazioni sono integrate in maniera approfondita e nativa nel modello di programmazione JavaScript di Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d4547-184">Transactions are deeply and natively integrated into Cosmos DB’s JavaScript programming model.</span></span> <span data-ttu-id="d4547-185">All'interno di una funzione JavaScript, viene eseguito il wrapping di tutte le operazioni in un'unica transazione.</span><span class="sxs-lookup"><span data-stu-id="d4547-185">Inside a JavaScript function, all operations are automatically wrapped under a single transaction.</span></span> <span data-ttu-id="d4547-186">Se la funzione JavaScript viene completata senza eccezioni, viene eseguito il commit delle operazioni nel database.</span><span class="sxs-lookup"><span data-stu-id="d4547-186">If the JavaScript completes without any exception, the operations to the database are committed.</span></span> <span data-ttu-id="d4547-187">Le istruzioni "BEGIN TRANSACTION" e "COMMIT TRANSACTION" nei database relazionali sono implicite in Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d4547-187">In effect, the “BEGIN TRANSACTION” and “COMMIT TRANSACTION” statements in relational databases are implicit in Cosmos DB.</span></span>  

<span data-ttu-id="d4547-188">Se si verifica un'eccezione qualsiasi che viene propagata dallo script, il runtime JavaScript di Cosmos DB esegue il rollback dell'intera transazione.</span><span class="sxs-lookup"><span data-stu-id="d4547-188">If there is any exception that’s propagated from the script, Cosmos DB’s JavaScript runtime will roll back the whole transaction.</span></span> <span data-ttu-id="d4547-189">Come illustrato in un esempio precedente, la generazione di un'eccezione equivale effettivamente a un'istruzione "ROLLBACK TRANSACTION" in Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d4547-189">As shown in the earlier example, throwing an exception is effectively equivalent to a “ROLLBACK TRANSACTION” in Cosmos DB.</span></span>

### <a name="data-consistency"></a><span data-ttu-id="d4547-190">Coerenza dei dati</span><span class="sxs-lookup"><span data-stu-id="d4547-190">Data consistency</span></span>
<span data-ttu-id="d4547-191">Le stored procedure e i trigger vengono sempre eseguiti sulla cartella di replica principale del contenitore di Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d4547-191">Stored procedures and triggers are always executed on the primary replica of the Azure Cosmos DB container.</span></span> <span data-ttu-id="d4547-192">In tal modo si garantisce la coerenza assoluta delle letture all'interno delle stored procedure.</span><span class="sxs-lookup"><span data-stu-id="d4547-192">This ensures that reads from inside stored procedures offer strong consistency.</span></span> <span data-ttu-id="d4547-193">È possibile eseguire le query che usano funzioni definite dall'utente sulla replica principale o in qualsiasi replica secondaria, ma è necessario assicurarsi di soddisfare il livello di coerenza richiesto scegliendo la replica appropriata.</span><span class="sxs-lookup"><span data-stu-id="d4547-193">Queries using user defined functions can be executed on the primary or any secondary replica, but we ensure to meet the requested consistency level by choosing the appropriate replica.</span></span>

## <a name="bounded-execution"></a><span data-ttu-id="d4547-194">Esecuzione vincolata</span><span class="sxs-lookup"><span data-stu-id="d4547-194">Bounded execution</span></span>
<span data-ttu-id="d4547-195">Tutte le operazioni di Cosmos DB devono essere completate entro la scadenza specificata dal server.</span><span class="sxs-lookup"><span data-stu-id="d4547-195">All Cosmos DB operations must complete within the server specified request timeout duration.</span></span> <span data-ttu-id="d4547-196">Questo vincolo si applica anche alle funzioni JavaScript (stored procedure, trigger e funzioni definite dall'utente).</span><span class="sxs-lookup"><span data-stu-id="d4547-196">This constraint also applies to JavaScript functions (stored procedures, triggers and user-defined functions).</span></span> <span data-ttu-id="d4547-197">Se un'operazione non viene completata entro questo limite di tempo, viene eseguito il rollback della transazione.</span><span class="sxs-lookup"><span data-stu-id="d4547-197">If an operation does not complete with that time limit, the transaction is rolled back.</span></span> <span data-ttu-id="d4547-198">Le funzioni JavaScript devono terminare entro il tempo limite oppure implementare un modello basato sulla continuazione in modo da riprendere l'esecuzione o eseguirla in batch.</span><span class="sxs-lookup"><span data-stu-id="d4547-198">JavaScript functions must finish within the time limit or implement a continuation based model to batch/resume execution.</span></span>  

<span data-ttu-id="d4547-199">Per semplificare lo sviluppo delle stored procedure e dei trigger per la gestione dei limiti di tempo, tutte le funzioni nell'oggetto raccolta (per creare, leggere, sostituire ed eliminare i documenti e gli allegati) restituiscono un valore booleano che indica se l'operazione verrà completata.</span><span class="sxs-lookup"><span data-stu-id="d4547-199">In order to simplify development of stored procedures and triggers to handle time limits, all functions under the collection object (for create, read, replace, and delete of documents and attachments) return a Boolean value that represents whether that operation will complete.</span></span> <span data-ttu-id="d4547-200">Se questo valore è falso, sarà indice che il tempo limite sta per scadere e che è necessario concludere l'esecuzione della procedura.</span><span class="sxs-lookup"><span data-stu-id="d4547-200">If this value is false, it is an indication that the time limit is about to expire and that the procedure must wrap up execution.</span></span>  <span data-ttu-id="d4547-201">Il completamento delle operazioni inserite in coda precedentemente alla prima operazione di archiviazione non accettata è garantito se la stored procedure viene completata in tempo e non vengono inserite in coda altre richieste.</span><span class="sxs-lookup"><span data-stu-id="d4547-201">Operations queued prior to the first unaccepted store operation are guaranteed to complete if the stored procedure completes in time and does not queue any more requests.</span></span>  

<span data-ttu-id="d4547-202">Anche le funzioni JavaScript sono vincolate al consumo di risorse.</span><span class="sxs-lookup"><span data-stu-id="d4547-202">JavaScript functions are also bounded on resource consumption.</span></span> <span data-ttu-id="d4547-203">Cosmos DB riserva una velocità effettiva per ogni raccolta in base alle dimensioni dell'account di database di cui è stato effettuato il provisioning.</span><span class="sxs-lookup"><span data-stu-id="d4547-203">Cosmos DB reserves throughput per collection based on the provisioned size of a database account.</span></span> <span data-ttu-id="d4547-204">La velocità effettiva viene espressa in termini di un'unità normalizzata di consumo CPU, memoria e IO, denominata unità di richiesta, o RU.</span><span class="sxs-lookup"><span data-stu-id="d4547-204">Throughput is expressed in terms of a normalized unit of CPU, memory and IO consumption called request units or RUs.</span></span> <span data-ttu-id="d4547-205">Le funzioni JavaScript possono potenzialmente usare un numero elevato di RU in breve tempo; per tale motivo, è possibile che venga limitata la frequenza del traffico di rete quando si raggiunge il limite della raccolta.</span><span class="sxs-lookup"><span data-stu-id="d4547-205">JavaScript functions can potentially use up a large number of RUs within a short time, and might get rate-limited if the collection’s limit is reached.</span></span> <span data-ttu-id="d4547-206">È anche possibile che le stored procedure che richiedono un utilizzo elevato di risorse vengano messe in quarantena per assicurare la disponibilità delle operazioni di database primitive.</span><span class="sxs-lookup"><span data-stu-id="d4547-206">Resource intensive stored procedures might also be quarantined to ensure availability of primitive database operations.</span></span>  

### <a name="example-bulk-importing-data-into-a-database-program"></a><span data-ttu-id="d4547-207">Esempio: importazione in blocco dei dati in un programma di database</span><span class="sxs-lookup"><span data-stu-id="d4547-207">Example: Bulk importing data into a database program</span></span>
<span data-ttu-id="d4547-208">Di seguito è riportato un esempio di stored procedure scritta per importare in blocco i documenti in una raccolta.</span><span class="sxs-lookup"><span data-stu-id="d4547-208">Below is an example of a stored procedure that is written to bulk-import documents into a collection.</span></span> <span data-ttu-id="d4547-209">Da notare il modo in cui la stored procedure gestisce l'esecuzione vincolata verificando il valore booleano restituito da createDocument e quindi usa il numero di documenti inseriti in ogni chiamata della stored procedure per tracciare e riprendere l'avanzamento nei vari batch.</span><span class="sxs-lookup"><span data-stu-id="d4547-209">Note how the stored procedure handles bounded execution by checking the Boolean return value from createDocument, and then uses the count of documents inserted in each invocation of the stored procedure to track and resume progress across batches.</span></span>

    function bulkImport(docs) {
        var collection = getContext().getCollection();
        var collectionLink = collection.getSelfLink();

        // The count of imported docs, also used as current doc index.
        var count = 0;

        // Validate input.
        if (!docs) throw new Error("The array is undefined or null.");

        var docsLength = docs.length;
        if (docsLength == 0) {
            getContext().getResponse().setBody(0);
        }

        // Call the create API to create a document.
        tryCreate(docs[count], callback);

        // Note that there are 2 exit conditions:
        // 1) The createDocument request was not accepted. 
        //    In this case the callback will not be called, we just call setBody and we are done.
        // 2) The callback was called docs.length times.
        //    In this case all documents were created and we don’t need to call tryCreate anymore. Just call setBody and we are done.
        function tryCreate(doc, callback) {
            var isAccepted = collection.createDocument(collectionLink, doc, callback);

            // If the request was accepted, callback will be called.
            // Otherwise report current count back to the client, 
            // which will call the script again with remaining set of docs.
            if (!isAccepted) getContext().getResponse().setBody(count);
        }

        // This is called when collection.createDocument is done in order to process the result.
        function callback(err, doc, options) {
            if (err) throw err;

            // One more document has been inserted, increment the count.
            count++;

            if (count >= docsLength) {
                // If we created all documents, we are done. Just set the response.
                getContext().getResponse().setBody(count);
            } else {
                // Create next document.
                tryCreate(docs[count], callback);
            }
        }
    }

## <span data-ttu-id="d4547-210"><a id="trigger"></a> Trigger del database</span><span class="sxs-lookup"><span data-stu-id="d4547-210"><a id="trigger"></a> Database triggers</span></span>
### <a name="database-pre-triggers"></a><span data-ttu-id="d4547-211">Pre-trigger del database</span><span class="sxs-lookup"><span data-stu-id="d4547-211">Database pre-triggers</span></span>
<span data-ttu-id="d4547-212">Cosmos DB include trigger che vengono eseguiti o attivati da un'operazione su un documento.</span><span class="sxs-lookup"><span data-stu-id="d4547-212">Cosmos DB provides triggers that are executed or triggered by an operation on a document.</span></span> <span data-ttu-id="d4547-213">Ad esempio, quando si crea un documento è possibile specificare un pre-trigger, che verrà eseguito prima della creazione.</span><span class="sxs-lookup"><span data-stu-id="d4547-213">For example, you can specify a pre-trigger when you are creating a document – this pre-trigger will run before the document is created.</span></span> <span data-ttu-id="d4547-214">Di seguito è riportato un esempio di come è possibile usare i pre-trigger per convalidare le proprietà di un documento in corso di creazione:</span><span class="sxs-lookup"><span data-stu-id="d4547-214">The following is an example of how pre-triggers can be used to validate the properties of a document that is being created:</span></span>

    var validateDocumentContentsTrigger = {
        id: "validateDocumentContents",
        serverScript: function validate() {
            var context = getContext();
            var request = context.getRequest();

            // document to be created in the current operation
            var documentToCreate = request.getBody();

            // validate properties
            if (!("timestamp" in documentToCreate)) {
                var ts = new Date();
                documentToCreate["my timestamp"] = ts.getTime();
            }

            // update the document that will be created
            request.setBody(documentToCreate);
        },
        triggerType: TriggerType.Pre,
        triggerOperation: TriggerOperation.Create
    }


<span data-ttu-id="d4547-215">E il corrispondente codice di registrazione lato client di Node.js per il trigger:</span><span class="sxs-lookup"><span data-stu-id="d4547-215">And the corresponding Node.js client-side registration code for the trigger:</span></span>

    // register pre-trigger
    client.createTriggerAsync(collection.self, validateDocumentContentsTrigger)
        .then(function (response) {
            console.log("Created", response.resource);
            var docToCreate = {
                id: "DocWithTrigger",
                event: "Error",
                source: "Network outage"
            };

            // run trigger while creating above document 
            var options = { preTriggerInclude: "validateDocumentContents" };

            return client.createDocumentAsync(collection.self,
                  docToCreate, options);
        }, function (error) {
            console.log("Error", error);
        })
    .then(function (response) {
        console.log(response.resource); // document with timestamp property added
    }, function (error) {
        console.log("Error", error);
    });


<span data-ttu-id="d4547-216">I pre-trigger non possono avere parametri di input.</span><span class="sxs-lookup"><span data-stu-id="d4547-216">Pre-triggers cannot have any input parameters.</span></span> <span data-ttu-id="d4547-217">L'oggetto richiesta può essere usato per gestire il messaggio di richiesta associato all'operazione.</span><span class="sxs-lookup"><span data-stu-id="d4547-217">The request object can be used to manipulate the request message associated with the operation.</span></span> <span data-ttu-id="d4547-218">In questo caso, si esegue il pre-trigger preliminare contemporaneamente alla creazione di un documento e il corpo del messaggio di richiesta contiene il documento da creare in formato JSON.</span><span class="sxs-lookup"><span data-stu-id="d4547-218">Here, the pre-trigger is being run with the creation of a document, and the request message body contains the document to be created in JSON format.</span></span>   

<span data-ttu-id="d4547-219">Quando i trigger vengono registrati, gli utenti possono specificare le operazioni con le quali è possibile eseguirli.</span><span class="sxs-lookup"><span data-stu-id="d4547-219">When triggers are registered, users can specify the operations that it can run with.</span></span> <span data-ttu-id="d4547-220">Questo trigger è stato creato con TriggerOperation.Create, quindi quanto riportato di seguito non è consentito.</span><span class="sxs-lookup"><span data-stu-id="d4547-220">This trigger was created with TriggerOperation.Create, which means the following is not permitted.</span></span>

    var options = { preTriggerInclude: "validateDocumentContents" };

    client.replaceDocumentAsync(docToReplace.self,
                  newDocBody, options)
    .then(function (response) {
        console.log(response.resource);
    }, function (error) {
        console.log("Error", error);
    });

    // Fails, can’t use a create trigger in a replace operation

### <a name="database-post-triggers"></a><span data-ttu-id="d4547-221">Post-trigger del database</span><span class="sxs-lookup"><span data-stu-id="d4547-221">Database post-triggers</span></span>
<span data-ttu-id="d4547-222">I post-trigger, come i pre-trigger, sono associati a un'operazione su un documento e non accettano parametri di input.</span><span class="sxs-lookup"><span data-stu-id="d4547-222">Post-triggers, like pre-triggers, are associated with an operation on a document and don’t take any input parameters.</span></span> <span data-ttu-id="d4547-223">Vengono eseguiti **dopo** il completamento dell'operazione e hanno accesso al messaggio di risposta inviato al client.</span><span class="sxs-lookup"><span data-stu-id="d4547-223">They run **after** the operation has completed, and have access to the response message that is sent to the client.</span></span>   

<span data-ttu-id="d4547-224">Nell'esempio seguente vengono illustrati i post-trigger in azione:</span><span class="sxs-lookup"><span data-stu-id="d4547-224">The following example shows post-triggers in action:</span></span>

    var updateMetadataTrigger = {
        id: "updateMetadata",
        serverScript: function updateMetadata() {
            var context = getContext();
            var collection = context.getCollection();
            var response = context.getResponse();

            // document that was created
            var createdDocument = response.getBody();

            // query for metadata document
            var filterQuery = 'SELECT * FROM root r WHERE r.id = "_metadata"';
            var accept = collection.queryDocuments(collection.getSelfLink(), filterQuery,
                updateMetadataCallback);
            if(!accept) throw "Unable to update metadata, abort";

            function updateMetadataCallback(err, documents, responseOptions) {
                if(err) throw new Error("Error" + err.message);
                         if(documents.length != 1) throw 'Unable to find metadata document';

                         var metadataDocument = documents[0];

                         // update metadata
                         metadataDocument.createdDocuments += 1;
                         metadataDocument.createdNames += " " + createdDocument.id;
                         var accept = collection.replaceDocument(metadataDocument._self,
                               metadataDocument, function(err, docReplaced) {
                                      if(err) throw "Unable to update metadata, abort";
                               });
                         if(!accept) throw "Unable to update metadata, abort";
                         return;                    
            }                                                                                            
        },
        triggerType: TriggerType.Post,
        triggerOperation: TriggerOperation.All
    }


<span data-ttu-id="d4547-225">È possibile registrare un trigger come illustrato nell'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="d4547-225">The trigger can be registered as shown in the following sample.</span></span>

    // register post-trigger
    client.createTriggerAsync('dbs/testdb/colls/testColl', updateMetadataTrigger)
        .then(function(createdTrigger) { 
            var docToCreate = { 
                name: "artist_profile_1023",
                artist: "The Band",
                albums: ["Hellujah", "Rotators", "Spinning Top"]
            };

            // run trigger while creating above document 
            var options = { postTriggerInclude: "updateMetadata" };

            return client.createDocumentAsync(collection.self,
                  docToCreate, options);
        }, function(error) {
            console.log("Error" , error);
        })
    .then(function(response) {
        console.log(response.resource); 
    }, function(error) {
        console.log("Error" , error);
    });


<span data-ttu-id="d4547-226">Il trigger esegue query sul documento dei metadati, aggiornandolo con le informazioni relative al documento appena creato.</span><span class="sxs-lookup"><span data-stu-id="d4547-226">This trigger queries for the metadata document and updates it with details about the newly created document.</span></span>  

<span data-ttu-id="d4547-227">Un aspetto importante da tenere presente è l'esecuzione **transazionale** dei trigger in Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d4547-227">One thing that is important to note is the **transactional** execution of triggers in Cosmos DB.</span></span> <span data-ttu-id="d4547-228">Questo post-trigger viene eseguito come parte della stessa transazione relativa alla creazione del documento originale.</span><span class="sxs-lookup"><span data-stu-id="d4547-228">This post-trigger runs as part of the same transaction as the creation of the original document.</span></span> <span data-ttu-id="d4547-229">Pertanto, se si genera un'eccezione dal post-trigger (ad esempio se non è possibile aggiornare il documento dei metadati), l'intera transazione avrà esito negativo e verrà ripristinata allo stato precedente.</span><span class="sxs-lookup"><span data-stu-id="d4547-229">Therefore, if we throw an exception from the post-trigger (say if we are unable to update the metadata document), the whole transaction will fail and be rolled back.</span></span> <span data-ttu-id="d4547-230">Non verrà creato alcun documento e verrà restituita un'eccezione.</span><span class="sxs-lookup"><span data-stu-id="d4547-230">No document will be created, and an exception will be returned.</span></span>  

## <span data-ttu-id="d4547-231"><a id="udf"></a>Funzioni definite dall'utente</span><span class="sxs-lookup"><span data-stu-id="d4547-231"><a id="udf"></a>User-defined functions</span></span>
<span data-ttu-id="d4547-232">Le funzioni definite dall'utente permettono di estendere la grammatica del linguaggio di query SQL dell'API di DocumentDB e implementare la logica di business personalizzata.</span><span class="sxs-lookup"><span data-stu-id="d4547-232">User-defined functions (UDFs) are used to extend the DocumentDB API SQL query language grammar and implement custom business logic.</span></span> <span data-ttu-id="d4547-233">Possono essere richiamate solo dall'interno delle query.</span><span class="sxs-lookup"><span data-stu-id="d4547-233">They can only be called from inside queries.</span></span> <span data-ttu-id="d4547-234">Non hanno accesso all'oggetto contesto e vanno usate come JavaScript di solo calcolo.</span><span class="sxs-lookup"><span data-stu-id="d4547-234">They do not have access to the context object and are meant to be used as compute-only JavaScript.</span></span> <span data-ttu-id="d4547-235">È quindi possibile eseguire le funzioni definite dall'utente su repliche secondarie del servizio Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d4547-235">Therefore, UDFs can be run on secondary replicas of the Cosmos DB service.</span></span>  

<span data-ttu-id="d4547-236">L'esempio seguente consente di creare una funzione definita dall'utente per calcolare l'imposta sul reddito in base ai tassi relativi a varie fasce di reddito. La funzione viene quindi usata all'interno di una query per trovare tutte le persone che hanno pagato oltre 20.000 dollari di imposte.</span><span class="sxs-lookup"><span data-stu-id="d4547-236">The following sample creates a UDF to calculate income tax based on rates for various income brackets, and then uses it inside a query to find all people who paid more than $20,000 in taxes.</span></span>

    var taxUdf = {
        id: "tax",
        serverScript: function tax(income) {

            if(income == undefined) 
                throw 'no input';

            if (income < 1000) 
                return income * 0.1;
            else if (income < 10000) 
                return income * 0.2;
            else
                return income * 0.4;
        }
    }


<span data-ttu-id="d4547-237">La funzione UDF può in seguito essere usata in query come quella riportata nell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="d4547-237">The UDF can subsequently be used in queries like in the following sample:</span></span>

    // register UDF
    client.createUserDefinedFunctionAsync('dbs/testdb/colls/testColl', taxUdf)
        .then(function(response) { 
            console.log("Created", response.resource);

            var query = 'SELECT * FROM TaxPayers t WHERE udf.tax(t.income) > 20000'; 
            return client.queryDocuments('dbs/testdb/colls/testColl',
                   query).toArrayAsync();
        }, function(error) {
            console.log("Error" , error);
        })
    .then(function(response) {
        var documents = response.feed;
        console.log(response.resource); 
    }, function(error) {
        console.log("Error" , error);
    });

## <a name="javascript-language-integrated-query-api"></a><span data-ttu-id="d4547-238">API della Language-Integrated Query di JavaScript</span><span class="sxs-lookup"><span data-stu-id="d4547-238">JavaScript language-integrated query API</span></span>
<span data-ttu-id="d4547-239">Oltre a eseguire una query utilizzando la sintassi SQL del DocumentDB, il SDK sul lato server consente di eseguire query ottimizzate tramite un'interfaccia intuitiva JavaScript senza alcuna conoscenza di SQL.</span><span class="sxs-lookup"><span data-stu-id="d4547-239">In addition to issuing queries using DocumentDB’s SQL grammar, the server-side SDK allows you to perform optimized queries using a fluent JavaScript interface without any knowledge of SQL.</span></span> <span data-ttu-id="d4547-240">L'API della query JavaScript consente di creare query a livello di programmazione passando funzioni predicate in chiamate di funzione concatenabili, con una sintassi familiare alle librerie JavaScript predefinite e diffuse della matrice ECMAScript5 come lodash.</span><span class="sxs-lookup"><span data-stu-id="d4547-240">The JavaScript query API allows you to programmatically build queries by passing predicate functions into chainable function calls, with a syntax familiar to ECMAScript5's Array built-ins and popular JavaScript libraries like lodash.</span></span> <span data-ttu-id="d4547-241">Le query vengono analizzate dal runtime JavaScript per essere eseguite in modo efficiente usando gli indici di Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d4547-241">Queries are parsed by the JavaScript runtime to be executed efficiently using Azure Cosmos DB’s indices.</span></span>

> [!NOTE]
> <span data-ttu-id="d4547-242">`__` (doppio carattere di sottolineatura) è un alias per `getContext().getCollection()`.</span><span class="sxs-lookup"><span data-stu-id="d4547-242">`__` (double-underscore) is an alias to `getContext().getCollection()`.</span></span>
> <br/>
> <span data-ttu-id="d4547-243">Per accedere all'API della query JavaScript, in altre parole, è possibile utilizzare `__` o `getContext().getCollection()`.</span><span class="sxs-lookup"><span data-stu-id="d4547-243">In other words, you can use `__` or `getContext().getCollection()` to access the JavaScript query API.</span></span>
> 
> 

<span data-ttu-id="d4547-244">Tra le funzioni supportate:</span><span class="sxs-lookup"><span data-stu-id="d4547-244">Supported functions include:</span></span>

<ul>
<li><span data-ttu-id="d4547-245">
<b>chain() ... .value([callback] [, options])</b>
</span><span class="sxs-lookup"><span data-stu-id="d4547-245">
<b>chain() ... .value([callback] [, options])</b>
</span></span><ul>
<li>
<span data-ttu-id="d4547-246">Avvia una chiamata concatenata che deve terminare con value().</span><span class="sxs-lookup"><span data-stu-id="d4547-246">Starts a chained call which must be terminated with value().</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="d4547-247">
<b>filter(predicateFunction [, options] [, callback])</b>
</span><span class="sxs-lookup"><span data-stu-id="d4547-247">
<b>filter(predicateFunction [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="d4547-248">Filtra l'input usando una funzione predicato che restituisce true o false per includere o escludere i documenti di input dal set risultante.</span><span class="sxs-lookup"><span data-stu-id="d4547-248">Filters the input using a predicate function which returns true/false in order to filter in/out input documents into the resulting set.</span></span> <span data-ttu-id="d4547-249">Il comportamento è simile a quello di una clausola WHERE in SQL.</span><span class="sxs-lookup"><span data-stu-id="d4547-249">This behaves similar to a WHERE clause in SQL.</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="d4547-250">
<b>map(transformationFunction [, options] [, callback])</b>
</span><span class="sxs-lookup"><span data-stu-id="d4547-250">
<b>map(transformationFunction [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="d4547-251">Applica una proiezione a partire da una funzione di trasformazione che esegue il mapping di ogni elemento di input a un valore o oggetto JavaScript.</span><span class="sxs-lookup"><span data-stu-id="d4547-251">Applies a projection given a transformation function which maps each input item to a JavaScript object or value.</span></span> <span data-ttu-id="d4547-252">Il comportamento è simile a quello di una clausola SELECT in SQL.</span><span class="sxs-lookup"><span data-stu-id="d4547-252">This behaves similar to a SELECT clause in SQL.</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="d4547-253">
<b>pluck([propertyName] [, options] [, callback])</b>
</span><span class="sxs-lookup"><span data-stu-id="d4547-253">
<b>pluck([propertyName] [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="d4547-254">Collegamento a una mappa che consente di estrarre il valore di una singola proprietà da ogni elemento di input.</span><span class="sxs-lookup"><span data-stu-id="d4547-254">This is a shortcut for a map which extracts the value of a single property from each input item.</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="d4547-255">
<b>flatten([isShallow] [, options] [, callback])</b>
</span><span class="sxs-lookup"><span data-stu-id="d4547-255">
<b>flatten([isShallow] [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="d4547-256">Combina e appiattisce le matrici da ogni elemento di input in un'unica matrice.</span><span class="sxs-lookup"><span data-stu-id="d4547-256">Combines and flattens arrays from each input item in to a single array.</span></span> <span data-ttu-id="d4547-257">Il comportamento è simile a quello di SelectMany in LINQ.</span><span class="sxs-lookup"><span data-stu-id="d4547-257">This behaves similar to SelectMany in LINQ.</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="d4547-258">
<b>sortBy([predicate] [, options] [, callback])</b>
</span><span class="sxs-lookup"><span data-stu-id="d4547-258">
<b>sortBy([predicate] [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="d4547-259">Produce un nuovo set di documenti ordinandoli nel flusso di documenti di input in ordine crescente usando il predicato specificato.</span><span class="sxs-lookup"><span data-stu-id="d4547-259">Produce a new set of documents by sorting the documents in the input document stream in ascending order using the given predicate.</span></span> <span data-ttu-id="d4547-260">Il comportamento è simile a quello di una clausola ORDER BY in SQL.</span><span class="sxs-lookup"><span data-stu-id="d4547-260">This behaves similar to a ORDER BY clause in SQL.</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="d4547-261">
<b>sortByDescending([predicate] [, options] [, callback])</b>
</span><span class="sxs-lookup"><span data-stu-id="d4547-261">
<b>sortByDescending([predicate] [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="d4547-262">Produce un nuovo set di documenti ordinandoli nel flusso di documenti di input in ordine decrescente usando il predicato specificato.</span><span class="sxs-lookup"><span data-stu-id="d4547-262">Produce a new set of documents by sorting the documents in the input document stream in descending order using the given predicate.</span></span> <span data-ttu-id="d4547-263">Il comportamento è simile a quello di una clausola ORDER BY x DESC in SQL.</span><span class="sxs-lookup"><span data-stu-id="d4547-263">This behaves similar to a ORDER BY x DESC clause in SQL.</span></span>
</li>
</ul>
</li>
</ul>


<span data-ttu-id="d4547-264">Quando inclusi all'interno delle funzioni predicato e/o selettore, i seguenti costrutti JavaScript vengono automaticamente ottimizzati per l'esecuzione diretta sugli indici di Azure Cosmos DB:</span><span class="sxs-lookup"><span data-stu-id="d4547-264">When included inside predicate and/or selector functions, the following JavaScript constructs get automatically optimized to run directly on Azure Cosmos DB indices:</span></span>

* <span data-ttu-id="d4547-265">Operatori semplici: = + - * / % | ^ &amp; == != === !=== &lt; &gt; &lt;= &gt;= || &amp;&amp; &lt;&lt; &gt;&gt; &gt;&gt;&gt;!</span><span class="sxs-lookup"><span data-stu-id="d4547-265">Simple operators: = + - * / % | ^ &amp; == != === !=== &lt; &gt; &lt;= &gt;= || &amp;&amp; &lt;&lt; &gt;&gt; &gt;&gt;&gt;!</span></span> ~
* <span data-ttu-id="d4547-266">Valori letterali, incluso il valore letterale dell'oggetto: {}</span><span class="sxs-lookup"><span data-stu-id="d4547-266">Literals, including the object literal: {}</span></span>
* <span data-ttu-id="d4547-267">var, return</span><span class="sxs-lookup"><span data-stu-id="d4547-267">var, return</span></span>

<span data-ttu-id="d4547-268">I seguenti costrutti JavaScript non vengono ottimizzati per gli indici di Azure Cosmos DB:</span><span class="sxs-lookup"><span data-stu-id="d4547-268">The following JavaScript constructs do not get optimized for Azure Cosmos DB indices:</span></span>

* <span data-ttu-id="d4547-269">Flusso di controllo (ad esempio, se, per, mentre)</span><span class="sxs-lookup"><span data-stu-id="d4547-269">Control flow (e.g. if, for, while)</span></span>
* <span data-ttu-id="d4547-270">Chiamate di funzione</span><span class="sxs-lookup"><span data-stu-id="d4547-270">Function calls</span></span>

<span data-ttu-id="d4547-271">Per ulteriori informazioni, vedere [Server-Side JSDocs](http://azure.github.io/azure-documentdb-js-server/).</span><span class="sxs-lookup"><span data-stu-id="d4547-271">For more information, please see our [Server-Side JSDocs](http://azure.github.io/azure-documentdb-js-server/).</span></span>

### <a name="example-write-a-stored-procedure-using-the-javascript-query-api"></a><span data-ttu-id="d4547-272">Esempio: Scrivere una stored procedure usando l'API di query JavaScript</span><span class="sxs-lookup"><span data-stu-id="d4547-272">Example: Write a stored procedure using the JavaScript query API</span></span>
<span data-ttu-id="d4547-273">L'esempio di codice seguente illustra come usare l'API Query JavaScript nel contesto di una stored procedure.</span><span class="sxs-lookup"><span data-stu-id="d4547-273">The following code sample is an example of how the JavaScript Query API can be used in the context of a stored procedure.</span></span> <span data-ttu-id="d4547-274">La stored procedure inserisce un documento, fornito da un parametro di input, e aggiorna un documento di metadati, usando il metodo `__.filter()` , con minSize, maxSize e totalSize in base alla proprietà relativa alle dimensioni del documento di input.</span><span class="sxs-lookup"><span data-stu-id="d4547-274">The stored procedure inserts a document, given by an input parameter, and updates a metadata document, using the `__.filter()` method, with minSize, maxSize, and totalSize based upon the input document's size property.</span></span>

    /**
     * Insert actual doc and update metadata doc: minSize, maxSize, totalSize based on doc.size.
     */
    function insertDocumentAndUpdateMetadata(doc) {
      // HTTP error codes sent to our callback funciton by DocDB server.
      var ErrorCode = {
        RETRY_WITH: 449,
      }

      var isAccepted = __.createDocument(__.getSelfLink(), doc, {}, function(err, doc, options) {
        if (err) throw err;

        // Check the doc (ignore docs with invalid/zero size and metaDoc itself) and call updateMetadata.
        if (!doc.isMetadata && doc.size > 0) {
          // Get the meta document. We keep it in the same collection. it's the only doc that has .isMetadata = true.
          var result = __.filter(function(x) {
            return x.isMetadata === true
          }, function(err, feed, options) {
            if (err) throw err;

            // We assume that metadata doc was pre-created and must exist when this script is called.
            if (!feed || !feed.length) throw new Error("Failed to find the metadata document.");

            // The metadata document.
            var metaDoc = feed[0];

            // Update metaDoc.minSize:
            // for 1st document use doc.Size, for all the rest see if it's less than last min.
            if (metaDoc.minSize == 0) metaDoc.minSize = doc.size;
            else metaDoc.minSize = Math.min(metaDoc.minSize, doc.size);

            // Update metaDoc.maxSize.
            metaDoc.maxSize = Math.max(metaDoc.maxSize, doc.size);

            // Update metaDoc.totalSize.
            metaDoc.totalSize += doc.size;

            // Update/replace the metadata document in the store.
            var isAccepted = __.replaceDocument(metaDoc._self, metaDoc, function(err) {
              if (err) throw err;
              // Note: in case concurrent updates causes conflict with ErrorCode.RETRY_WITH, we can't read the meta again 
              //       and update again because due to Snapshot isolation we will read same exact version (we are in same transaction).
              //       We have to take care of that on the client side.
            });
            if (!isAccepted) throw new Error("replaceDocument(metaDoc) returned false.");
          });
          if (!result.isAccepted) throw new Error("filter for metaDoc returned false.");
        }
      });
      if (!isAccepted) throw new Error("createDocument(actual doc) returned false.");
    }

## <a name="sql-to-javascript-cheat-sheet"></a><span data-ttu-id="d4547-275">Foglio riassuntivo di SQL per JavaScript</span><span class="sxs-lookup"><span data-stu-id="d4547-275">SQL to Javascript cheat sheet</span></span>
<span data-ttu-id="d4547-276">Nella tabella seguente vengono presentate varie query SQL e le query JavaScript corrispondenti.</span><span class="sxs-lookup"><span data-stu-id="d4547-276">The following table presents various SQL queries and the corresponding JavaScript queries.</span></span>

<span data-ttu-id="d4547-277">Come le query SQL, le chiavi di proprietà del documento (ad esempio `doc.id`) fanno distinzione tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="d4547-277">As with SQL queries, document property keys (e.g. `doc.id`) are case-sensitive.</span></span>

|<span data-ttu-id="d4547-278">SQL</span><span class="sxs-lookup"><span data-stu-id="d4547-278">SQL</span></span>| <span data-ttu-id="d4547-279">API di query JavaScript</span><span class="sxs-lookup"><span data-stu-id="d4547-279">JavaScript Query API</span></span>|<span data-ttu-id="d4547-280">Descrizione sotto</span><span class="sxs-lookup"><span data-stu-id="d4547-280">Description below</span></span>|
|---|---|---|
|<span data-ttu-id="d4547-281">SELECT *</span><span class="sxs-lookup"><span data-stu-id="d4547-281">SELECT *</span></span><br><span data-ttu-id="d4547-282">FROM docs</span><span class="sxs-lookup"><span data-stu-id="d4547-282">FROM docs</span></span>| <span data-ttu-id="d4547-283">__.map(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="d4547-283">__.map(function(doc) {</span></span> <br><span data-ttu-id="d4547-284">&nbsp;&nbsp;&nbsp;&nbsp;return doc;</span><span class="sxs-lookup"><span data-stu-id="d4547-284">&nbsp;&nbsp;&nbsp;&nbsp;return doc;</span></span><br><span data-ttu-id="d4547-285">});</span><span class="sxs-lookup"><span data-stu-id="d4547-285">});</span></span>|<span data-ttu-id="d4547-286">1</span><span class="sxs-lookup"><span data-stu-id="d4547-286">1</span></span>|
|<span data-ttu-id="d4547-287">SELECT docs.id, docs.message AS msg, docs.actions</span><span class="sxs-lookup"><span data-stu-id="d4547-287">SELECT docs.id, docs.message AS msg, docs.actions</span></span> <br><span data-ttu-id="d4547-288">FROM docs</span><span class="sxs-lookup"><span data-stu-id="d4547-288">FROM docs</span></span>|<span data-ttu-id="d4547-289">__.map(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="d4547-289">__.map(function(doc) {</span></span><br><span data-ttu-id="d4547-290">&nbsp;&nbsp;&nbsp;&nbsp;return {</span><span class="sxs-lookup"><span data-stu-id="d4547-290">&nbsp;&nbsp;&nbsp;&nbsp;return {</span></span><br><span data-ttu-id="d4547-291">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;id: doc.id,</span><span class="sxs-lookup"><span data-stu-id="d4547-291">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;id: doc.id,</span></span><br><span data-ttu-id="d4547-292">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;msg: doc.message,</span><span class="sxs-lookup"><span data-stu-id="d4547-292">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;msg: doc.message,</span></span><br><span data-ttu-id="d4547-293">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;actions:doc.actions</span><span class="sxs-lookup"><span data-stu-id="d4547-293">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;actions:doc.actions</span></span><br><span data-ttu-id="d4547-294">&nbsp;&nbsp;&nbsp;&nbsp;};</span><span class="sxs-lookup"><span data-stu-id="d4547-294">&nbsp;&nbsp;&nbsp;&nbsp;};</span></span><br><span data-ttu-id="d4547-295">});</span><span class="sxs-lookup"><span data-stu-id="d4547-295">});</span></span>|<span data-ttu-id="d4547-296">2</span><span class="sxs-lookup"><span data-stu-id="d4547-296">2</span></span>|
|<span data-ttu-id="d4547-297">SELECT *</span><span class="sxs-lookup"><span data-stu-id="d4547-297">SELECT *</span></span><br><span data-ttu-id="d4547-298">FROM docs</span><span class="sxs-lookup"><span data-stu-id="d4547-298">FROM docs</span></span><br><span data-ttu-id="d4547-299">WHERE docs.id="X998_Y998"</span><span class="sxs-lookup"><span data-stu-id="d4547-299">WHERE docs.id="X998_Y998"</span></span>|<span data-ttu-id="d4547-300">__.filter(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="d4547-300">__.filter(function(doc) {</span></span><br><span data-ttu-id="d4547-301">&nbsp;&nbsp;&nbsp;&nbsp;return doc.id ==="X998_Y998";</span><span class="sxs-lookup"><span data-stu-id="d4547-301">&nbsp;&nbsp;&nbsp;&nbsp;return doc.id ==="X998_Y998";</span></span><br><span data-ttu-id="d4547-302">});</span><span class="sxs-lookup"><span data-stu-id="d4547-302">});</span></span>|<span data-ttu-id="d4547-303">3</span><span class="sxs-lookup"><span data-stu-id="d4547-303">3</span></span>|
|<span data-ttu-id="d4547-304">SELECT *</span><span class="sxs-lookup"><span data-stu-id="d4547-304">SELECT *</span></span><br><span data-ttu-id="d4547-305">FROM docs</span><span class="sxs-lookup"><span data-stu-id="d4547-305">FROM docs</span></span><br><span data-ttu-id="d4547-306">WHERE ARRAY_CONTAINS(docs.Tags, 123)</span><span class="sxs-lookup"><span data-stu-id="d4547-306">WHERE ARRAY_CONTAINS(docs.Tags, 123)</span></span>|<span data-ttu-id="d4547-307">__.filter(function(x) {</span><span class="sxs-lookup"><span data-stu-id="d4547-307">__.filter(function(x) {</span></span><br><span data-ttu-id="d4547-308">&nbsp;&nbsp;&nbsp;&nbsp;return x.Tags && x.Tags.indexOf(123) > -1;</span><span class="sxs-lookup"><span data-stu-id="d4547-308">&nbsp;&nbsp;&nbsp;&nbsp;return x.Tags && x.Tags.indexOf(123) > -1;</span></span><br><span data-ttu-id="d4547-309">});</span><span class="sxs-lookup"><span data-stu-id="d4547-309">});</span></span>|<span data-ttu-id="d4547-310">4</span><span class="sxs-lookup"><span data-stu-id="d4547-310">4</span></span>|
|<span data-ttu-id="d4547-311">SELECT docs.id, docs.message AS msg</span><span class="sxs-lookup"><span data-stu-id="d4547-311">SELECT docs.id, docs.message AS msg</span></span><br><span data-ttu-id="d4547-312">FROM docs</span><span class="sxs-lookup"><span data-stu-id="d4547-312">FROM docs</span></span><br><span data-ttu-id="d4547-313">WHERE docs.id="X998_Y998"</span><span class="sxs-lookup"><span data-stu-id="d4547-313">WHERE docs.id="X998_Y998"</span></span>|<span data-ttu-id="d4547-314">__.chain()</span><span class="sxs-lookup"><span data-stu-id="d4547-314">__.chain()</span></span><br><span data-ttu-id="d4547-315">&nbsp;&nbsp;&nbsp;&nbsp;.filter(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="d4547-315">&nbsp;&nbsp;&nbsp;&nbsp;.filter(function(doc) {</span></span><br><span data-ttu-id="d4547-316">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return doc.id ==="X998_Y998";</span><span class="sxs-lookup"><span data-stu-id="d4547-316">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return doc.id ==="X998_Y998";</span></span><br><span data-ttu-id="d4547-317">&nbsp;&nbsp;&nbsp;&nbsp;})</span><span class="sxs-lookup"><span data-stu-id="d4547-317">&nbsp;&nbsp;&nbsp;&nbsp;})</span></span><br><span data-ttu-id="d4547-318">&nbsp;&nbsp;&nbsp;&nbsp;.map(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="d4547-318">&nbsp;&nbsp;&nbsp;&nbsp;.map(function(doc) {</span></span><br><span data-ttu-id="d4547-319">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return {</span><span class="sxs-lookup"><span data-stu-id="d4547-319">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return {</span></span><br><span data-ttu-id="d4547-320">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;id: doc.id,</span><span class="sxs-lookup"><span data-stu-id="d4547-320">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;id: doc.id,</span></span><br><span data-ttu-id="d4547-321">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;msg: doc.message</span><span class="sxs-lookup"><span data-stu-id="d4547-321">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;msg: doc.message</span></span><br><span data-ttu-id="d4547-322">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;};</span><span class="sxs-lookup"><span data-stu-id="d4547-322">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;};</span></span><br><span data-ttu-id="d4547-323">&nbsp;&nbsp;&nbsp;&nbsp;})</span><span class="sxs-lookup"><span data-stu-id="d4547-323">&nbsp;&nbsp;&nbsp;&nbsp;})</span></span><br><span data-ttu-id="d4547-324">.value();</span><span class="sxs-lookup"><span data-stu-id="d4547-324">.value();</span></span>|<span data-ttu-id="d4547-325">5</span><span class="sxs-lookup"><span data-stu-id="d4547-325">5</span></span>|
|<span data-ttu-id="d4547-326">SELECT VALUE tag</span><span class="sxs-lookup"><span data-stu-id="d4547-326">SELECT VALUE tag</span></span><br><span data-ttu-id="d4547-327">FROM docs</span><span class="sxs-lookup"><span data-stu-id="d4547-327">FROM docs</span></span><br><span data-ttu-id="d4547-328">JOIN tag IN docs.Tags</span><span class="sxs-lookup"><span data-stu-id="d4547-328">JOIN tag IN docs.Tags</span></span><br><span data-ttu-id="d4547-329">ORDER BY docs._ts</span><span class="sxs-lookup"><span data-stu-id="d4547-329">ORDER BY docs._ts</span></span>|<span data-ttu-id="d4547-330">__.chain()</span><span class="sxs-lookup"><span data-stu-id="d4547-330">__.chain()</span></span><br><span data-ttu-id="d4547-331">&nbsp;&nbsp;&nbsp;&nbsp;.filter(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="d4547-331">&nbsp;&nbsp;&nbsp;&nbsp;.filter(function(doc) {</span></span><br><span data-ttu-id="d4547-332">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return doc.Tags && Array.isArray(doc.Tags);</span><span class="sxs-lookup"><span data-stu-id="d4547-332">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return doc.Tags && Array.isArray(doc.Tags);</span></span><br><span data-ttu-id="d4547-333">&nbsp;&nbsp;&nbsp;&nbsp;})</span><span class="sxs-lookup"><span data-stu-id="d4547-333">&nbsp;&nbsp;&nbsp;&nbsp;})</span></span><br><span data-ttu-id="d4547-334">&nbsp;&nbsp;&nbsp;&nbsp;.sortBy(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="d4547-334">&nbsp;&nbsp;&nbsp;&nbsp;.sortBy(function(doc) {</span></span><br><span data-ttu-id="d4547-335">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return doc._ts;</span><span class="sxs-lookup"><span data-stu-id="d4547-335">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return doc._ts;</span></span><br><span data-ttu-id="d4547-336">&nbsp;&nbsp;&nbsp;&nbsp;})</span><span class="sxs-lookup"><span data-stu-id="d4547-336">&nbsp;&nbsp;&nbsp;&nbsp;})</span></span><br><span data-ttu-id="d4547-337">&nbsp;&nbsp;&nbsp;&nbsp;.pluck("Tags")</span><span class="sxs-lookup"><span data-stu-id="d4547-337">&nbsp;&nbsp;&nbsp;&nbsp;.pluck("Tags")</span></span><br><span data-ttu-id="d4547-338">&nbsp;&nbsp;&nbsp;&nbsp;.flatten()</span><span class="sxs-lookup"><span data-stu-id="d4547-338">&nbsp;&nbsp;&nbsp;&nbsp;.flatten()</span></span><br><span data-ttu-id="d4547-339">&nbsp;&nbsp;&nbsp;&nbsp;.value()</span><span class="sxs-lookup"><span data-stu-id="d4547-339">&nbsp;&nbsp;&nbsp;&nbsp;.value()</span></span>|<span data-ttu-id="d4547-340">6</span><span class="sxs-lookup"><span data-stu-id="d4547-340">6</span></span>|

<span data-ttu-id="d4547-341">Le descrizioni seguenti illustrano ogni query nella tabella sopra.</span><span class="sxs-lookup"><span data-stu-id="d4547-341">The following descriptions explain each query in the table above.</span></span>
1. <span data-ttu-id="d4547-342">Viene restituita così com'è in tutti i documenti, impaginati con token di continuazione.</span><span class="sxs-lookup"><span data-stu-id="d4547-342">Results in all documents (paginated with continuation token) as is.</span></span>
2. <span data-ttu-id="d4547-343">Proietta l'ID, il messaggio (con aliasing effettuato a msg) e l'azione da tutti i documenti.</span><span class="sxs-lookup"><span data-stu-id="d4547-343">Projects the id, message (aliased to msg), and action from all documents.</span></span>
3. <span data-ttu-id="d4547-344">Esegue una query sui documenti con il predicato: id = "X998_Y998".</span><span class="sxs-lookup"><span data-stu-id="d4547-344">Queries for documents with the predicate: id = "X998_Y998".</span></span>
4. <span data-ttu-id="d4547-345">Esegue una query sui documenti che hanno una proprietà Tags e Tags è una matrice che contiene il valore 123.</span><span class="sxs-lookup"><span data-stu-id="d4547-345">Queries for documents that have a Tags property and Tags is an array containing the value 123.</span></span>
5. <span data-ttu-id="d4547-346">Esegue una query sui documenti con un predicato id = "X998_Y998" e quindi proietta l'ID e il messaggio (con aliasing effettuato a msg).</span><span class="sxs-lookup"><span data-stu-id="d4547-346">Queries for documents with a predicate, id = "X998_Y998", and then projects the id and message (aliased to msg).</span></span>
6. <span data-ttu-id="d4547-347">Filtra i documenti che hanno la proprietà di matrice Tags, ordina i documenti risultanti in base alla proprietà di sistema timestamp _ts e quindi proietta e appiattisce la matrice Tags.</span><span class="sxs-lookup"><span data-stu-id="d4547-347">Filters for documents which have an array property, Tags, and sorts the resulting documents by the _ts timestamp system property, and then projects + flattens the Tags array.</span></span>


## <a name="runtime-support"></a><span data-ttu-id="d4547-348">Supporto di runtime</span><span class="sxs-lookup"><span data-stu-id="d4547-348">Runtime support</span></span>
<span data-ttu-id="d4547-349">L'[API lato server JavaScript di DocumentDB](http://azure.github.io/azure-documentdb-js-server/) offre supporto per la maggior parte delle principali funzionalità del linguaggio JavaScript, secondo lo standard [ECMA-262](http://www.ecma-international.org/publications/standards/Ecma-262.htm).</span><span class="sxs-lookup"><span data-stu-id="d4547-349">[DocumentDB JavaScript server side API](http://azure.github.io/azure-documentdb-js-server/) provides support for the most of the mainstream JavaScript language features as standardized by [ECMA-262](http://www.ecma-international.org/publications/standards/Ecma-262.htm).</span></span>

### <a name="security"></a><span data-ttu-id="d4547-350">Sicurezza</span><span class="sxs-lookup"><span data-stu-id="d4547-350">Security</span></span>
<span data-ttu-id="d4547-351">Le stored procedure e i trigger di JavaScript vengono create in modalità sandbox in modo che gli effetti di un unico script non vengano trasferiti all'altro senza che siano stati prima sottoposti all'isolamento delle transazioni snapshot a livello di database.</span><span class="sxs-lookup"><span data-stu-id="d4547-351">JavaScript stored procedures and triggers are sandboxed so that the effects of one script do not leak to the other without going through the snapshot transaction isolation at the database level.</span></span> <span data-ttu-id="d4547-352">Gli ambienti di runtime vengono riuniti in pool, ma ripuliti dal contesto dopo ciascuna esecuzione.</span><span class="sxs-lookup"><span data-stu-id="d4547-352">The runtime environments are pooled but cleaned of the context after each run.</span></span> <span data-ttu-id="d4547-353">Di conseguenza è possibile garantirne la sicurezza rispetto a effetti collaterali imprevisti causati l'un l'altro.</span><span class="sxs-lookup"><span data-stu-id="d4547-353">Hence they are guaranteed to be safe of any unintended side effects from each other.</span></span>

### <a name="pre-compilation"></a><span data-ttu-id="d4547-354">Precompilazione</span><span class="sxs-lookup"><span data-stu-id="d4547-354">Pre-compilation</span></span>
<span data-ttu-id="d4547-355">Le stored procedure, i trigger e le UDF vengono precompilate implicitamente nel formato di codice byte per evitare i costi di compilazione ad ogni chiamata dello script.</span><span class="sxs-lookup"><span data-stu-id="d4547-355">Stored procedures, triggers and UDFs are implicitly precompiled to the byte code format in order to avoid compilation cost at the time of each script invocation.</span></span> <span data-ttu-id="d4547-356">Questo garantisce la velocità elevata e il footprint ridotto delle chiamate delle stored procedure.</span><span class="sxs-lookup"><span data-stu-id="d4547-356">This ensures invocations of stored procedures are fast and have a low footprint.</span></span>

## <a name="client-sdk-support"></a><span data-ttu-id="d4547-357">Supporto di client SDK</span><span class="sxs-lookup"><span data-stu-id="d4547-357">Client SDK support</span></span>
<span data-ttu-id="d4547-358">Oltre all'API DocumentDB per il client [Node.js](documentdb-sdk-node.md), Azure Cosmos DB include [.NET](documentdb-sdk-dotnet.md), [.NET Core](documentdb-sdk-dotnet-core.md), [Java](documentdb-sdk-java.md), [JavaScript](http://azure.github.io/azure-documentdb-js/) e [Python SDK](documentdb-sdk-python.md) per l'API DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="d4547-358">In addition to the DocumentDB API for [Node.js](documentdb-sdk-node.md) client, Azure Cosmos DB has [.NET](documentdb-sdk-dotnet.md), [.NET Core](documentdb-sdk-dotnet-core.md), [Java](documentdb-sdk-java.md), [JavaScript](http://azure.github.io/azure-documentdb-js/), and [Python SDKs](documentdb-sdk-python.md) for the DocumentDB API.</span></span> <span data-ttu-id="d4547-359">È possibile creare ed eseguire stored procedure, trigger e UDFs usando anche uno qualsiasi di questi SDK.</span><span class="sxs-lookup"><span data-stu-id="d4547-359">Stored procedures, triggers and UDFs can be created and executed using any of these SDKs as well.</span></span> <span data-ttu-id="d4547-360">Nell'esempio seguente viene illustrato come creare ed eseguire una stored procedure con il client .NET.</span><span class="sxs-lookup"><span data-stu-id="d4547-360">The following example shows how to create and execute a stored procedure using the .NET client.</span></span> <span data-ttu-id="d4547-361">Notare il modo in cui i tipi -NET vengono passati nella stored procedure come JSON e poi riletti.</span><span class="sxs-lookup"><span data-stu-id="d4547-361">Note how the .NET types are passed into the stored procedure as JSON and read back.</span></span>

    var markAntiquesSproc = new StoredProcedure
    {
        Id = "ValidateDocumentAge",
        Body = @"
                function(docToCreate, antiqueYear) {
                    var collection = getContext().getCollection();    
                    var response = getContext().getResponse();    

                    if(docToCreate.Year != undefined && docToCreate.Year < antiqueYear){
                        docToCreate.antique = true;
                    }

                    collection.createDocument(collection.getSelfLink(), docToCreate, {}, 
                        function(err, docCreated, options) { 
                            if(err) throw new Error('Error while creating document: ' + err.message);                              
                            if(options.maxCollectionSizeInMb == 0) throw 'max collection size not found'; 
                            response.setBody(docCreated);
                    });
             }"
    };

    // register stored procedure
    StoredProcedure createdStoredProcedure = await client.CreateStoredProcedureAsync(UriFactory.CreateDocumentCollectionUri("db", "coll"), markAntiquesSproc);
    dynamic document = new Document() { Id = "Borges_112" };
    document.Title = "Aleph";
    document.Year = 1949;

    // execute stored procedure
    Document createdDocument = await client.ExecuteStoredProcedureAsync<Document>(UriFactory.CreateStoredProcedureUri("db", "coll", "sproc"), document, 1920);


<span data-ttu-id="d4547-362">Questo esempio illustra come usare l'[API .NET di DocumentDB](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet) per creare un pre-trigger e quindi un documento con il trigger attivato.</span><span class="sxs-lookup"><span data-stu-id="d4547-362">This sample shows how to use the [DocumentDB .NET API](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet) to create a pre-trigger and create a document with the trigger enabled.</span></span> 

    Trigger preTrigger = new Trigger()
    {
        Id = "CapitalizeName",
        Body = @"function() {
            var item = getContext().getRequest().getBody();
            item.id = item.id.toUpperCase();
            getContext().getRequest().setBody(item);
        }",
        TriggerOperation = TriggerOperation.Create,
        TriggerType = TriggerType.Pre
    };

    Document createdItem = await client.CreateDocumentAsync(UriFactory.CreateDocumentCollectionUri("db", "coll"), new Document { Id = "documentdb" },
        new RequestOptions
        {
            PreTriggerInclude = new List<string> { "CapitalizeName" },
        });


<span data-ttu-id="d4547-363">L'esempio seguente illustra come creare una funzione definita dall'utente e usarla in una [query SQL dell'API di DocumentDB](documentdb-sql-query.md).</span><span class="sxs-lookup"><span data-stu-id="d4547-363">And the following example shows how to create a user defined function (UDF) and use it in a [DocumentDB API SQL query](documentdb-sql-query.md).</span></span>

    UserDefinedFunction function = new UserDefinedFunction()
    {
        Id = "LOWER",
        Body = @"function(input) 
        {
            return input.toLowerCase();
        }"
    };

    foreach (Book book in client.CreateDocumentQuery(UriFactory.CreateDocumentCollectionUri("db", "coll"),
        "SELECT * FROM Books b WHERE udf.LOWER(b.Title) = 'war and peace'"))
    {
        Console.WriteLine("Read {0} from query", book);
    }

## <a name="rest-api"></a><span data-ttu-id="d4547-364">API REST</span><span class="sxs-lookup"><span data-stu-id="d4547-364">REST API</span></span>
<span data-ttu-id="d4547-365">Tutte le operazioni di Azure Cosmos DB possono essere eseguite in modalità RESTful.</span><span class="sxs-lookup"><span data-stu-id="d4547-365">All Azure Cosmos DB operations can be performed in a RESTful manner.</span></span> <span data-ttu-id="d4547-366">È possibile registrare stored procedure, trigger e funzioni definite dall'utente in una raccolta usando il verbo HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="d4547-366">Stored procedures, triggers and user-defined functions can be registered under a collection by using HTTP POST.</span></span> <span data-ttu-id="d4547-367">Di seguito è riportato un esempio di come registrare una stored procedure:</span><span class="sxs-lookup"><span data-stu-id="d4547-367">The following is an example of how to register a stored procedure:</span></span>

    POST https://<url>/sprocs/ HTTP/1.1
    authorization: <<auth>>
    x-ms-date: Thu, 07 Aug 2014 03:43:10 GMT


    var x = {
      "name": "createAndAddProperty",
      "body": function (docToCreate, addedPropertyName, addedPropertyValue) {
                var collectionManager = getContext().getCollection();
                collectionManager.createDocument(
                    collectionManager.getSelfLink(),
                    docToCreate,
                    function(err, docCreated) {
                      if(err) throw new Error('Error:  ' + err.message);
                      docCreated[addedPropertyName] = addedPropertyValue;
                      getContext().getResponse().setBody(docCreated);
                    });
            }
    }


<span data-ttu-id="d4547-368">La stored procedure viene registrata eseguendo una richiesta POST nell'URI dbs/testdb/colls/testColl/sprocs con il corpo contenente la stored procedure da creare.</span><span class="sxs-lookup"><span data-stu-id="d4547-368">The stored procedure is registered by executing a POST request against the URI dbs/testdb/colls/testColl/sprocs with the body containing the stored procedure to create.</span></span> <span data-ttu-id="d4547-369">Trigger e funzioni definite dall'utente possono essere registrati in modo analogo eseguendo una richiesta POST rispettivamente su /triggers e /udfs.</span><span class="sxs-lookup"><span data-stu-id="d4547-369">Triggers and UDFs can be registered similarly by issuing a POST against /triggers and /udfs respectively.</span></span>
<span data-ttu-id="d4547-370">Questa stored procedure può quindi essere eseguita tramite una richiesta POST sul relativo collegamento alle risorse:</span><span class="sxs-lookup"><span data-stu-id="d4547-370">This stored procedure can then be executed by issuing a POST request against its resource link:</span></span>

    POST https://<url>/sprocs/<sproc> HTTP/1.1
    authorization: <<auth>>
    x-ms-date: Thu, 07 Aug 2014 03:43:20 GMT


    [ { "name": "TestDocument", "book": "Autumn of the Patriarch"}, "Price", 200 ]


<span data-ttu-id="d4547-371">In questo caso, l'input nella stored procedure viene passato al corpo della richiesta.</span><span class="sxs-lookup"><span data-stu-id="d4547-371">Here, the input to the stored procedure is passed in the request body.</span></span> <span data-ttu-id="d4547-372">Notare che l'input viene passato come matrice JSON dei parametri di input.</span><span class="sxs-lookup"><span data-stu-id="d4547-372">Note that the input is passed as a JSON array of input parameters.</span></span> <span data-ttu-id="d4547-373">La stored procedure accetta il primo input come documento che rappresenta il corpo della risposta.</span><span class="sxs-lookup"><span data-stu-id="d4547-373">The stored procedure takes the first input as a document that is a response body.</span></span> <span data-ttu-id="d4547-374">Il formato della risposta ricevuta è il seguente:</span><span class="sxs-lookup"><span data-stu-id="d4547-374">The response we receive is as follows:</span></span>

    HTTP/1.1 200 OK

    { 
      name: 'TestDocument',
      book: ‘Autumn of the Patriarch’,
      id: ‘V7tQANV3rAkDAAAAAAAAAA==‘,
      ts: 1407830727,
      self: ‘dbs/V7tQAA==/colls/V7tQANV3rAk=/docs/V7tQANV3rAkDAAAAAAAAAA==/’,
      etag: ‘6c006596-0000-0000-0000-53e9cac70000’,
      attachments: ‘attachments/’,
      Price: 200
    }


<span data-ttu-id="d4547-375">A differenza delle stored procedure, non è possibile eseguire direttamente i trigger,</span><span class="sxs-lookup"><span data-stu-id="d4547-375">Triggers, unlike stored procedures, cannot be executed directly.</span></span> <span data-ttu-id="d4547-376">che vengono però eseguiti come parte di un'operazione o di un documento.</span><span class="sxs-lookup"><span data-stu-id="d4547-376">Instead they are executed as part of an operation on a document.</span></span> <span data-ttu-id="d4547-377">È possibile specificare i trigger da eseguire con una richiesta usando le intestazioni HTTP.</span><span class="sxs-lookup"><span data-stu-id="d4547-377">We can specify the triggers to run with a request using HTTP headers.</span></span> <span data-ttu-id="d4547-378">Di seguito è riportata una richiesta per creare un documento.</span><span class="sxs-lookup"><span data-stu-id="d4547-378">The following is request to create a document.</span></span>

    POST https://<url>/docs/ HTTP/1.1
    authorization: <<auth>>
    x-ms-date: Thu, 07 Aug 2014 03:43:10 GMT
    x-ms-documentdb-pre-trigger-include: validateDocumentContents 
    x-ms-documentdb-post-trigger-include: bookCreationPostTrigger


    {
       "name": "newDocument",
       “title”: “The Wizard of Oz”,
       “author”: “Frank Baum”,
       “pages”: 92
    }


<span data-ttu-id="d4547-379">In questo caso, il pre-trigger da eseguire con la richiesta è specificato nell'intestazione x-ms-documentdb-pre-trigger-include.</span><span class="sxs-lookup"><span data-stu-id="d4547-379">Here the pre-trigger to be run with the request is specified in the x-ms-documentdb-pre-trigger-include header.</span></span> <span data-ttu-id="d4547-380">Di conseguenza, qualsiasi post-trigger viene indicato nell'intestazione x-ms-documentdb-post-trigger-include.</span><span class="sxs-lookup"><span data-stu-id="d4547-380">Correspondingly, any post-triggers are given in the x-ms-documentdb-post-trigger-include header.</span></span> <span data-ttu-id="d4547-381">Notare che è possibile specificare sia pre-trigger sia post-trigger per una determinata richiesta.</span><span class="sxs-lookup"><span data-stu-id="d4547-381">Note that both pre- and post-triggers can be specified for a given request.</span></span>

## <a name="sample-code"></a><span data-ttu-id="d4547-382">Codice di esempio</span><span class="sxs-lookup"><span data-stu-id="d4547-382">Sample code</span></span>
<span data-ttu-id="d4547-383">Per trovare altri esempi di codice sul lato server, inclusi esempi relativi all'[eliminazione in blocco](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples/stored-procedures/bulkDelete.js) e all'[aggiornamento](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples/stored-procedures/update.js), vedere l'[archivio GitHub](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples).</span><span class="sxs-lookup"><span data-stu-id="d4547-383">You can find more server-side code examples (including [bulk-delete](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples/stored-procedures/bulkDelete.js), and [update](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples/stored-procedures/update.js)) on our [GitHub repository](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples).</span></span>

<span data-ttu-id="d4547-384">Si desidera condividere la stored procedure awesome?</span><span class="sxs-lookup"><span data-stu-id="d4547-384">Want to share your awesome stored procedure?</span></span> <span data-ttu-id="d4547-385">Inviare una richiesta di pull!</span><span class="sxs-lookup"><span data-stu-id="d4547-385">Please, send us a pull-request!</span></span> 

## <a name="next-steps"></a><span data-ttu-id="d4547-386">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d4547-386">Next steps</span></span>
<span data-ttu-id="d4547-387">Quando sono presenti uno o più stored procedure, trigger e funzioni definite dall'utente create, è possibile caricarli e visualizzarli nel portale di Azure usando Esplora dati.</span><span class="sxs-lookup"><span data-stu-id="d4547-387">Once you have one or more stored procedures, triggers, and user-defined functions created, you can load them and view them in the Azure portal using Data Explorer.</span></span>

<span data-ttu-id="d4547-388">È inoltre possibile trovare i seguenti riferimenti e risorse utili per il percorso per altre informazioni sulla programmazione lato server Azure Cosmos DB:</span><span class="sxs-lookup"><span data-stu-id="d4547-388">You may also find the following references and resources useful in your path to learn more about Azure Cosmos dB server-side programming:</span></span>

* [<span data-ttu-id="d4547-389">Azure Cosmos DB SDK</span><span class="sxs-lookup"><span data-stu-id="d4547-389">Azure Cosmos DB SDKs</span></span>](documentdb-sdk-dotnet.md)
* [<span data-ttu-id="d4547-390">DocumentDB Studio</span><span class="sxs-lookup"><span data-stu-id="d4547-390">DocumentDB Studio</span></span>](https://github.com/mingaliu/DocumentDBStudio/releases)
* [<span data-ttu-id="d4547-391">JSON</span><span class="sxs-lookup"><span data-stu-id="d4547-391">JSON</span></span>](http://www.json.org/) 
* [<span data-ttu-id="d4547-392">JavaScript ECMA-262</span><span class="sxs-lookup"><span data-stu-id="d4547-392">JavaScript ECMA-262</span></span>](http://www.ecma-international.org/publications/standards/Ecma-262.htm)
* [<span data-ttu-id="d4547-393">Estensibilità di Database protette e portatile</span><span class="sxs-lookup"><span data-stu-id="d4547-393">Secure and Portable Database Extensibility</span></span>](http://dl.acm.org/citation.cfm?id=276339) 
* [<span data-ttu-id="d4547-394">Database architettura orientata ai servizi</span><span class="sxs-lookup"><span data-stu-id="d4547-394">Service Oriented Database Architecture</span></span>](http://dl.acm.org/citation.cfm?id=1066267&coll=Portal&dl=GUIDE) 
* [<span data-ttu-id="d4547-395">Hosting del Runtime .NET in Microsoft SQL server</span><span class="sxs-lookup"><span data-stu-id="d4547-395">Hosting the .NET Runtime in Microsoft SQL server</span></span>](http://dl.acm.org/citation.cfm?id=1007669)

