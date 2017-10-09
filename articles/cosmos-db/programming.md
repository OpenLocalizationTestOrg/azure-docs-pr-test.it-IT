---
title: programmazione JavaScript sul lato aaaServer per Azure Cosmos DB | Documenti Microsoft
description: Informazioni su come toouse Azure Cosmos DB toowrite stored procedure, trigger di database e funzioni definite dall'utente (UDF) in JavaScript. Ottenere suggerimenti sulla programmazione di database e altro ancora.
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
ms.openlocfilehash: 5a011d1c4b0b5908d5de73607a1bc328ed1711d0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-server-side-programming-stored-procedures-database-triggers-and-udfs"></a><span data-ttu-id="3ecd5-105">Programmazione lato server per Azure Cosmos DB: stored procedure, trigger del database e funzioni definite dall'utente</span><span class="sxs-lookup"><span data-stu-id="3ecd5-105">Azure Cosmos DB server-side programming: Stored procedures, database triggers, and UDFs</span></span>
<span data-ttu-id="3ecd5-106">L'esecuzione integrata e transazionale di JavaScript con il linguaggio di Azure Cosmos DB permette agli sviluppatori di scrivere **stored procedure**, **trigger** e **funzioni definite dall'utente** in modo nativo in [ECMAScript 2015](http://www.ecma-international.org/ecma-262/6.0/) JavaScript.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-106">Learn how Azure Cosmos DB’s language integrated, transactional execution of JavaScript lets developers write **stored procedures**, **triggers** and **user defined functions (UDFs)** natively in an [ECMAScript 2015](http://www.ecma-international.org/ecma-262/6.0/) JavaScript.</span></span> <span data-ttu-id="3ecd5-107">In questo modo toowrite database programma logica dell'applicazione che può essere inviata e può essere eseguita direttamente sulle partizioni di archiviazione di database hello.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-107">This allows you toowrite database program application logic that can be shipped and executed directly on hello database storage partitions.</span></span> 

<span data-ttu-id="3ecd5-108">È consigliabile ottenere avviata da hello guardando seguente video, in cui Andrew Liu fornisce tooCosmos una breve introduzione del database modello di programmazione sul lato server database.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-108">We recommend getting started by watching hello following video, where Andrew Liu provides a brief introduction tooCosmos DB's server-side database programming model.</span></span> 

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-Demo-A-Quick-Intro-to-Azure-DocumentDBs-Server-Side-Javascript/player]
> 
> 

<span data-ttu-id="3ecd5-109">Tornare quindi toothis articolo, in cui si apprenderà toohello risposte hello seguenti domande:</span><span class="sxs-lookup"><span data-stu-id="3ecd5-109">Then, return toothis article, where you'll learn hello answers toohello following questions:</span></span>  

* <span data-ttu-id="3ecd5-110">Come è possibile scrivere una stored procedure, un trigger o una funzione definita dall'utente usando JavaScript?</span><span class="sxs-lookup"><span data-stu-id="3ecd5-110">How do I write a a stored procedure, trigger, or UDF using JavaScript?</span></span>
* <span data-ttu-id="3ecd5-111">In che modo Cosmos DB garantisce proprietà ACID?</span><span class="sxs-lookup"><span data-stu-id="3ecd5-111">How does Cosmos DB guarantee ACID?</span></span>
* <span data-ttu-id="3ecd5-112">Come funzionano le transazioni in Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="3ecd5-112">How do transactions work in Cosmos DB?</span></span>
* <span data-ttu-id="3ecd5-113">Cosa sono i pre-trigger e i post-trigger e come si scrivono?</span><span class="sxs-lookup"><span data-stu-id="3ecd5-113">What are pre-triggers and post-triggers and how do I write one?</span></span>
* <span data-ttu-id="3ecd5-114">Come si registra e si esegue una stored procedure, un trigger o una funzione definita dall'utente in modalità RESTful usando HTTP?</span><span class="sxs-lookup"><span data-stu-id="3ecd5-114">How do I register and execute a stored procedure, trigger, or UDF in a RESTful manner by using HTTP?</span></span>
* <span data-ttu-id="3ecd5-115">Quali sono disponibili toocreate Cosmos DB SDK ed eseguire stored procedure, trigger e funzioni definite dall'utente?</span><span class="sxs-lookup"><span data-stu-id="3ecd5-115">What Cosmos DB SDKs are available toocreate and execute stored procedures, triggers, and UDFs?</span></span>

## <a name="introduction-toostored-procedure-and-udf-programming"></a><span data-ttu-id="3ecd5-116">Introduzione tooStored Procedure e funzioni definite dall'utente per la programmazione</span><span class="sxs-lookup"><span data-stu-id="3ecd5-116">Introduction tooStored Procedure and UDF Programming</span></span>
<span data-ttu-id="3ecd5-117">Questo approccio di *"JavaScript come una moderna T-SQL"* consente agli sviluppatori di applicazioni di complessità hello di sistema di tipi non corrispondenti e le tecnologie di mapping relazionale a oggetti.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-117">This approach of *“JavaScript as a modern day T-SQL”* frees application developers from hello complexities of type system mismatches and object-relational mapping technologies.</span></span> <span data-ttu-id="3ecd5-118">Include inoltre una serie di vantaggi intrinseci che possono essere utilizzati toobuild applicazioni:</span><span class="sxs-lookup"><span data-stu-id="3ecd5-118">It also has a number of intrinsic advantages that can be utilized toobuild rich applications:</span></span>  

* <span data-ttu-id="3ecd5-119">**Logica procedurale:** JavaScript come un linguaggio di programmazione di alto livello, fornisce un tooexpress un'interfaccia familiare e rich logica di business.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-119">**Procedural Logic:** JavaScript as a high level programming language, provides a rich and familiar interface tooexpress business logic.</span></span> <span data-ttu-id="3ecd5-120">È possibile eseguire complesse sequenze più vicino toohello dei dati delle operazioni.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-120">You can perform complex sequences of operations closer toohello data.</span></span>
* <span data-ttu-id="3ecd5-121">**Transazioni atomiche:** Cosmos DB garantisce che le operazioni di database all'interno di una singola stored procedure o un trigger siano atomiche.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-121">**Atomic Transactions:** Cosmos DB guarantees that database operations performed inside a single stored procedure or trigger are atomic.</span></span> <span data-ttu-id="3ecd5-122">Di conseguenza, un'applicazione potrà combinare le operazioni correlate in un unico batch, in modo che o tutte o nessuna di esse avranno esito positivo.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-122">This lets an application combine related operations in a single batch so that either all of them succeed or none of them succeed.</span></span> 
* <span data-ttu-id="3ecd5-123">**Prestazioni:** fatti hello che JSON è intrinsecamente mappato toohello Javascript language tipo sistema ed è anche unità di archiviazione nel database Cosmos base hello consente un numero di ottimizzazioni come lazy materializzazione di JSON documenti nel buffer hello pool e renderli disponibili su richiesta toohello, l'esecuzione del codice.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-123">**Performance:** hello fact that JSON is intrinsically mapped toohello Javascript language type system and is also hello basic unit of storage in Cosmos DB allows for a number of optimizations like lazy materialization of JSON documents in hello buffer pool and making them available on-demand toohello executing code.</span></span> <span data-ttu-id="3ecd5-124">Sono disponibili ulteriori vantaggi di prestazioni associati shipping database toohello logica di business:</span><span class="sxs-lookup"><span data-stu-id="3ecd5-124">There are more performance benefits associated with shipping business logic toohello database:</span></span>
  
  * <span data-ttu-id="3ecd5-125">Invio in batch: gli sviluppatori possono raggruppare le operazioni, come gli inserimenti, e inviarle in blocco.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-125">Batching – Developers can group operations like inserts and submit them in bulk.</span></span> <span data-ttu-id="3ecd5-126">costo di latenza di traffico di rete Hello e transazioni separate di hello archivio toocreate overhead vengono ridotti in modo significativo.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-126">hello network traffic latency cost and hello store overhead toocreate separate transactions are reduced significantly.</span></span> 
  * <span data-ttu-id="3ecd5-127">Pre-compilazione: consente di precompilare Cosmos DB stored procedure, trigger e definiti dall'utente le funzioni definite dal tooavoid JavaScript costo di compilazione per ogni chiamata.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-127">Pre-compilation – Cosmos DB precompiles stored procedures, triggers and user defined functions (UDFs) tooavoid JavaScript compilation cost for each invocation.</span></span> <span data-ttu-id="3ecd5-128">Hello overhead per la generazione di codice a un byte hello per logica procedurale hello è ammortizzato tooa di valore minimo.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-128">hello overhead of building hello byte code for hello procedural logic is amortized tooa minimal value.</span></span>
  * <span data-ttu-id="3ecd5-129">Sequenziazione: molte operazioni necessitano di un effetto collaterale ("trigger") che implica potenzialmente l'esecuzione di una o più operazioni di archiviazione secondarie.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-129">Sequencing – Many operations need a side-effect (“trigger”) that potentially involves doing one or many secondary store operations.</span></span> <span data-ttu-id="3ecd5-130">A parte l'atomicità, questo è più efficiente quando spostato toohello server.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-130">Aside from atomicity, this is more performant when moved toohello server.</span></span> 
* <span data-ttu-id="3ecd5-131">**Incapsulamento:** Stored procedure possono essere utilizzato toogroup logica di business in un'unica posizione.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-131">**Encapsulation:** Stored procedures can be used toogroup business logic in one place.</span></span> <span data-ttu-id="3ecd5-132">Ciò comporta due vantaggi:</span><span class="sxs-lookup"><span data-stu-id="3ecd5-132">This has two advantages:</span></span>
  * <span data-ttu-id="3ecd5-133">Aggiunge un livello di astrazione su dati non elaborati hello, che consente di applicazioni in modo indipendente da dati hello tooevolve architetti di dati.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-133">It adds an abstraction layer on top of hello raw data, which enables data architects tooevolve their applications independently from hello data.</span></span> <span data-ttu-id="3ecd5-134">Ciò è particolarmente utile quando i dati di hello sono senza schema, a causa di ipotesi fragile toohello che potrebbe essere necessario toobe baked in un'applicazione hello se hanno toodeal con i dati direttamente.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-134">This is particularly advantageous when hello data is schema-less, due toohello brittle assumptions that may need toobe baked into hello application if they have toodeal with data directly.</span></span>  
  * <span data-ttu-id="3ecd5-135">Questa astrazione consente alle aziende di proteggere i propri dati grazie alla semplificazione di accesso di hello dagli script hello.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-135">This abstraction lets enterprises keep their data secure by streamlining hello access from hello scripts.</span></span>  

<span data-ttu-id="3ecd5-136">Hello creazione ed esecuzione di trigger di database, stored procedure e gli operatori di query personalizzata è supportata tramite hello [API REST](/rest/api/documentdb/), [Azure DocumentDB Studio](https://github.com/mingaliu/DocumentDBStudio/releases), e [client SDK](documentdb-sdk-dotnet.md) in molte piattaforme, tra cui .NET, Node.js e JavaScript.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-136">hello creation and execution of database triggers, stored procedure and custom query operators is supported through hello [REST API](/rest/api/documentdb/), [Azure DocumentDB Studio](https://github.com/mingaliu/DocumentDBStudio/releases), and [client SDKs](documentdb-sdk-dotnet.md) in many platforms including .NET, Node.js and JavaScript.</span></span>

<span data-ttu-id="3ecd5-137">Questa esercitazione viene utilizzato hello [Node.js SDK con domande e](http://azure.github.io/azure-documentdb-node-q/) tooillustrate sintassi e l'utilizzo di stored procedure, trigger e funzioni definite dall'utente.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-137">This tutorial uses hello [Node.js SDK with Q Promises](http://azure.github.io/azure-documentdb-node-q/) tooillustrate syntax and usage of stored procedures, triggers, and UDFs.</span></span>   

## <a name="stored-procedures"></a><span data-ttu-id="3ecd5-138">Stored procedure</span><span class="sxs-lookup"><span data-stu-id="3ecd5-138">Stored procedures</span></span>
### <a name="example-write-a-simple-stored-procedure"></a><span data-ttu-id="3ecd5-139">Esempio: scrivere una stored procedure semplice</span><span class="sxs-lookup"><span data-stu-id="3ecd5-139">Example: Write a simple stored procedure</span></span>
<span data-ttu-id="3ecd5-140">Per cominciare, si analizzerà una semplice stored procedure che restituisce una risposta "Hello World".</span><span class="sxs-lookup"><span data-stu-id="3ecd5-140">Let’s start with a simple stored procedure that returns a “Hello World” response.</span></span>

    var helloWorldStoredProc = {
        id: "helloWorld",
        serverScript: function () {
            var context = getContext();
            var response = context.getResponse();

            response.setBody("Hello, World");
        }
    }


<span data-ttu-id="3ecd5-141">Le stored procedure vengono registrate per ogni raccolta e funzionano in qualsiasi documento e allegato presente nella raccolta.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-141">Stored procedures are registered per collection, and can operate on any document and attachment present in that collection.</span></span> <span data-ttu-id="3ecd5-142">Hello frammento di codice seguente viene illustrato come tooregister hello helloWorld stored procedure con una raccolta.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-142">hello following snippet shows how tooregister hello helloWorld stored procedure with a collection.</span></span> 

    // register hello stored procedure
    var createdStoredProcedure;
    client.createStoredProcedureAsync('dbs/testdb/colls/testColl', helloWorldStoredProc)
        .then(function (response) {
            createdStoredProcedure = response.resource;
            console.log("Successfully created stored procedure");
        }, function (error) {
            console.log("Error", error);
        });


<span data-ttu-id="3ecd5-143">Una volta registrata procedure hello archiviato, è possibile eseguirla insieme hello e leggere i risultati al client hello hello.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-143">Once hello stored procedure is registered, we can execute it against hello collection, and read hello results back at hello client.</span></span> 

    // execute hello stored procedure
    client.executeStoredProcedureAsync('dbs/testdb/colls/testColl/sprocs/helloWorld')
        .then(function (response) {
            console.log(response.result); // "Hello, World"
        }, function (err) {
            console.log("Error", error);
        });


<span data-ttu-id="3ecd5-144">oggetto di contesto Hello fornisce l'accesso tooall operazioni che possono essere eseguite su archiviazione Cosmos DB, nonché accedere agli oggetti di richiesta e risposta toohello.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-144">hello context object provides access tooall operations that can be performed on Cosmos DB storage, as well as access toohello request and response objects.</span></span> <span data-ttu-id="3ecd5-145">In questo caso, abbiamo utilizzato hello oggetto tooset hello corpo della risposta di risposta hello client toohello indietro è stato inviato.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-145">In this case, we used hello response object tooset hello body of hello response that was sent back toohello client.</span></span> <span data-ttu-id="3ecd5-146">Per ulteriori informazioni, vedere toohello [server Azure Cosmos DB JavaScript documentazione SDK](http://azure.github.io/azure-documentdb-js-server/).</span><span class="sxs-lookup"><span data-stu-id="3ecd5-146">For more details, refer toohello [Azure Cosmos DB JavaScript server SDK documentation](http://azure.github.io/azure-documentdb-js-server/).</span></span>  

<span data-ttu-id="3ecd5-147">Espandere questo esempio segnalare il problema e aggiungere altre funzionalità correlate del database toohello stored procedure.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-147">Let us expand on this example and add more database related functionality toohello stored procedure.</span></span> <span data-ttu-id="3ecd5-148">Stored procedure possono creare, aggiornare, leggere, eseguire una query ed eliminare documenti e gli allegati all'interno di hello.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-148">Stored procedures can create, update, read, query and delete documents and attachments inside hello collection.</span></span>    

### <a name="example-write-a-stored-procedure-toocreate-a-document"></a><span data-ttu-id="3ecd5-149">Esempio: Scrivere una stored procedure toocreate un documento</span><span class="sxs-lookup"><span data-stu-id="3ecd5-149">Example: Write a stored procedure toocreate a document</span></span>
<span data-ttu-id="3ecd5-150">frammento di codice Hello successivo mostra come toouse hello toointeract oggetto di contesto con risorse DB Cosmos.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-150">hello next snippet shows how toouse hello context object toointeract with Cosmos DB resources.</span></span>

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


<span data-ttu-id="3ecd5-151">Questa stored procedure accetta come input documentToCreate, corpo hello di toobe un documento creato nella raccolta corrente hello.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-151">This stored procedure takes as input documentToCreate, hello body of a document toobe created in hello current collection.</span></span> <span data-ttu-id="3ecd5-152">Tutte queste operazioni sono asincrone e dipendono dai callback della funzione JavaScript.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-152">All such operations are asynchronous and depend on JavaScript function callbacks.</span></span> <span data-ttu-id="3ecd5-153">funzione di callback Hello ha due parametri, uno per l'oggetto errore hello nel caso in cui hello operazione ha esito negativo e uno per hello creato l'oggetto.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-153">hello callback function has two parameters, one for hello error object in case hello operation fails, and one for hello created object.</span></span> <span data-ttu-id="3ecd5-154">All'interno di callback hello, gli utenti possono gestire hello eccezione o viene generato un errore.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-154">Inside hello callback, users can either handle hello exception or throw an error.</span></span> <span data-ttu-id="3ecd5-155">Nel caso in cui non è stato specificato un callback e si verifica un errore, hello Azure Cosmos DB runtime genera un errore.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-155">In case a callback is not provided and there is an error, hello Azure Cosmos DB runtime throws an error.</span></span>   

<span data-ttu-id="3ecd5-156">Nell'esempio hello sopra, il callback di hello genera un errore se hello operazione non riuscita.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-156">In hello example above, hello callback throws an error if hello operation failed.</span></span> <span data-ttu-id="3ecd5-157">In caso contrario, imposta id hello di hello creato documento come corpo hello del client di toohello risposta hello.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-157">Otherwise, it sets hello id of hello created document as hello body of hello response toohello client.</span></span> <span data-ttu-id="3ecd5-158">Ecco come viene eseguita questa stored procedure con i parametri di input.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-158">Here is how this stored procedure is executed with input parameters.</span></span>

    // register hello stored procedure
    client.createStoredProcedureAsync('dbs/testdb/colls/testColl', createDocumentStoredProc)
        .then(function (response) {
            var createdStoredProcedure = response.resource;

            // run stored procedure toocreate a document
            var docToCreate = {
                id: "DocFromSproc",
                book: "hello Hitchhiker’s Guide toohello Galaxy",
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


<span data-ttu-id="3ecd5-159">Si noti che questa stored procedure possono essere modificato tootake una matrice di corpi di documento come input e crearli in hello stesso archiviato esecuzione della procedura anziché una rete più richieste toocreate di essi singolarmente.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-159">Note that this stored procedure can be modified tootake an array of document bodies as input and create them all in hello same stored procedure execution instead of multiple network requests toocreate each of them individually.</span></span> <span data-ttu-id="3ecd5-160">Può essere utilizzato tooimplement un'unità di importazione bulk sia efficiente per DB Cosmos (descritto più avanti in questa esercitazione).</span><span class="sxs-lookup"><span data-stu-id="3ecd5-160">This can be used tooimplement an efficient bulk importer for Cosmos DB (discussed later in this tutorial).</span></span>   

<span data-ttu-id="3ecd5-161">esempio Hello descritto dimostrato come toouse stored procedure.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-161">hello example described demonstrated how toouse stored procedures.</span></span> <span data-ttu-id="3ecd5-162">I trigger e funzioni definite dall'utente (UDF) verranno illustrate più avanti nell'esercitazione di hello.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-162">We will cover triggers and user defined functions (UDFs) later in hello tutorial.</span></span>

## <a name="database-program-transactions"></a><span data-ttu-id="3ecd5-163">Transazioni del programma del database</span><span class="sxs-lookup"><span data-stu-id="3ecd5-163">Database program transactions</span></span>
<span data-ttu-id="3ecd5-164">Una transazione in un tipico database può essere definita come una sequenza di operazioni eseguite come singola unità di lavoro logica.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-164">Transaction in a typical database can be defined as a sequence of operations performed as a single logical unit of work.</span></span> <span data-ttu-id="3ecd5-165">Ogni transazione offre **garanzie ACID**.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-165">Each transaction provides **ACID guarantees**.</span></span> <span data-ttu-id="3ecd5-166">ACID è un acronimo noto che riassume quattro proprietà: Atomicità, Coerenza, Isolamento e Durabilità.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-166">ACID is a well-known acronym that stands for four properties -  Atomicity, Consistency, Isolation and Durability.</span></span>  

<span data-ttu-id="3ecd5-167">In breve, l'atomicità assicura che tutto il lavoro hello eseguito all'interno di una transazione viene considerato come una singola unità in cui entrambi tutti i relativi viene eseguito il commit o nessuno.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-167">Briefly, atomicity guarantees that all hello work done inside a transaction is treated as a single unit where either all of it is committed or none.</span></span> <span data-ttu-id="3ecd5-168">Coerenza assicura che i dati di hello sono sempre in buono stato interno tra le transazioni.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-168">Consistency makes sure that hello data is always in a good internal state across transactions.</span></span> <span data-ttu-id="3ecd5-169">Isolamento in modo che le due transazioni non interferiscono tra loro, in genere, la maggior parte dei sistemi forniscono più livelli di isolamento che possono essere utilizzati in base ai requisiti dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-169">Isolation guarantees that no two transactions interfere with each other – generally, most commercial systems provide multiple isolation levels that can be used based on hello application needs.</span></span> <span data-ttu-id="3ecd5-170">Durabilità assicura che qualsiasi modifica che viene eseguito il commit nel database di hello sarà sempre presenta.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-170">Durability ensures that any change that’s committed in hello database will always be present.</span></span>   

<span data-ttu-id="3ecd5-171">In DB Cosmos, JavaScript è ospitato in hello database hello stesso spazio di memoria.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-171">In Cosmos DB, JavaScript is hosted in hello same memory space as hello database.</span></span> <span data-ttu-id="3ecd5-172">Di conseguenza, le richieste effettuate all'interno di stored procedure e trigger è eseguite in hello stesso ambito di una sessione di database.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-172">Hence, requests made within stored procedures and triggers execute in hello same scope of a database session.</span></span> <span data-ttu-id="3ecd5-173">In questo modo Cosmos DB tooguarantee ACID per tutte le operazioni che fanno parte di un singolo stored procedure o trigger.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-173">This enables Cosmos DB tooguarantee ACID for all operations that are part of a single stored procedure/trigger.</span></span> <span data-ttu-id="3ecd5-174">Si consideri il seguente hello archiviati definizione della stored procedure:</span><span class="sxs-lookup"><span data-stu-id="3ecd5-174">Consider hello following stored procedure definition:</span></span>

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

                    if (documents.length != 1) throw "Unable toofind both names";
                    player1Document = documents[0];

                    var filterQuery2 = 'SELECT * FROM Players p where p.id = "' + playerId2 + '"';
                    var accept2 = collection.queryDocuments(collection.getSelfLink(), filterQuery2, {},
                        function (err2, documents2, responseOptions2) {
                            if (err2) throw new Error("Error" + err2.message);
                            if (documents2.length != 1) throw "Unable toofind both names";
                            player2Document = documents2[0];
                            swapItems(player1Document, player2Document);
                            return;
                        });
                    if (!accept2) throw "Unable tooread player details, abort ";
                });

            if (!accept) throw "Unable tooread player details, abort ";

            // swap hello two players’ items
            function swapItems(player1, player2) {
                var player1ItemSave = player1.item;
                player1.item = player2.item;
                player2.item = player1ItemSave;

                var accept = collection.replaceDocument(player1._self, player1,
                    function (err, docReplaced) {
                        if (err) throw "Unable tooupdate player 1, abort ";

                        var accept2 = collection.replaceDocument(player2._self, player2,
                            function (err2, docReplaced2) {
                                if (err) throw "Unable tooupdate player 2, abort"
                            });

                        if (!accept2) throw "Unable tooupdate player 2, abort";
                    });

                if (!accept) throw "Unable tooupdate player 1, abort";
            }
        }
    }

    // register hello stored procedure in Node.js client
    client.createStoredProcedureAsync(collection._self, exchangeItemsSproc)
        .then(function (response) {
            var createdStoredProcedure = response.resource;
        }
    );

<span data-ttu-id="3ecd5-175">Questa stored procedure utilizza transazioni all'interno di elementi di tootrade app un gioco tra due giocatori in un'unica operazione.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-175">This stored procedure uses transactions within a gaming app tootrade items between two players in a single operation.</span></span> <span data-ttu-id="3ecd5-176">Hello stored procedure tentativi tooread due documenti che ogni player toohello corrispondente di ID passato come argomento.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-176">hello stored procedure attempts tooread two documents each corresponding toohello player IDs passed in as an argument.</span></span> <span data-ttu-id="3ecd5-177">Se vengono trovati entrambi i documenti Windows Media player, quindi hello stored procedura consente di aggiornare documenti hello scambiando gli elementi.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-177">If both player documents are found, then hello stored procedure updates hello documents by swapping their items.</span></span> <span data-ttu-id="3ecd5-178">Se vengono rilevati errori durante il processo di hello, verrà generata un'eccezione JavaScript che la transazione hello si interrompe in modo implicito.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-178">If any errors are encountered along hello way, it throws a JavaScript exception that implicitly aborts hello transaction.</span></span>

<span data-ttu-id="3ecd5-179">Se hello procedure hello archiviato insieme è registrata in è una raccolta unica partizione, sarà hello transazione documenti hello tooall con ambito raccolta hello.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-179">If hello collection hello stored procedure is registered against is a single-partition collection, then hello transaction is scoped tooall hello documents within hello collection.</span></span> <span data-ttu-id="3ecd5-180">Se la raccolta hello è partizionata, stored procedure vengono eseguite nell'ambito di transazione hello di una chiave singola partizione.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-180">If hello collection is partitioned, then stored procedures are executed in hello transaction scope of a single partition key.</span></span> <span data-ttu-id="3ecd5-181">Ogni stored esecuzione di stored procedure deve quindi includere un valore di chiave di partizione della transazione hello ambito toohello corrispondente deve essere eseguito con.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-181">Each stored procedure execution must then include a partition key value corresponding toohello scope hello transaction must run under.</span></span> <span data-ttu-id="3ecd5-182">Per altri dettagli, vedere l'articolo relativo al [partizionamento di Azure Cosmos DB](partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="3ecd5-182">For more details, see [Azure Cosmos DB Partitioning](partition-data.md).</span></span>

### <a name="commit-and-rollback"></a><span data-ttu-id="3ecd5-183">Commit e rollback</span><span class="sxs-lookup"><span data-stu-id="3ecd5-183">Commit and rollback</span></span>
<span data-ttu-id="3ecd5-184">Le transazioni sono integrate in maniera approfondita e nativa nel modello di programmazione JavaScript di Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-184">Transactions are deeply and natively integrated into Cosmos DB’s JavaScript programming model.</span></span> <span data-ttu-id="3ecd5-185">All'interno di una funzione JavaScript, viene eseguito il wrapping di tutte le operazioni in un'unica transazione.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-185">Inside a JavaScript function, all operations are automatically wrapped under a single transaction.</span></span> <span data-ttu-id="3ecd5-186">Se hello JavaScript viene completata senza alcuna eccezione, il database toohello operations Manager hello viene eseguito il commit.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-186">If hello JavaScript completes without any exception, hello operations toohello database are committed.</span></span> <span data-ttu-id="3ecd5-187">In effetti, le istruzioni "BEGIN TRANSACTION" e "Eseguire il COMMIT della transazione" hello nei database relazionali sono implicite nel DB Cosmos.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-187">In effect, hello “BEGIN TRANSACTION” and “COMMIT TRANSACTION” statements in relational databases are implicit in Cosmos DB.</span></span>  

<span data-ttu-id="3ecd5-188">Se è presente qualsiasi eccezione che viene propagato da script hello, il runtime di JavaScript Cosmos DB eseguirà il rollback dell'intera transazione hello.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-188">If there is any exception that’s propagated from hello script, Cosmos DB’s JavaScript runtime will roll back hello whole transaction.</span></span> <span data-ttu-id="3ecd5-189">Come illustrato in precedenza in hello esempio, generare un'eccezione è tooa equivale "ROLLBACK TRANSACTION" DB Cosmos.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-189">As shown in hello earlier example, throwing an exception is effectively equivalent tooa “ROLLBACK TRANSACTION” in Cosmos DB.</span></span>

### <a name="data-consistency"></a><span data-ttu-id="3ecd5-190">Coerenza dei dati</span><span class="sxs-lookup"><span data-stu-id="3ecd5-190">Data consistency</span></span>
<span data-ttu-id="3ecd5-191">Stored procedure e trigger vengono sempre eseguiti sulla replica primaria di hello del contenitore di Azure Cosmos DB hello.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-191">Stored procedures and triggers are always executed on hello primary replica of hello Azure Cosmos DB container.</span></span> <span data-ttu-id="3ecd5-192">In tal modo si garantisce la coerenza assoluta delle letture all'interno delle stored procedure.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-192">This ensures that reads from inside stored procedures offer strong consistency.</span></span> <span data-ttu-id="3ecd5-193">Le query che utilizzano funzioni definite dall'utente possono essere eseguite su hello primaria o una qualsiasi replica secondaria, ma è garantire toomeet hello richiesto livello di coerenza scegliendo replica appropriata hello.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-193">Queries using user defined functions can be executed on hello primary or any secondary replica, but we ensure toomeet hello requested consistency level by choosing hello appropriate replica.</span></span>

## <a name="bounded-execution"></a><span data-ttu-id="3ecd5-194">Esecuzione vincolata</span><span class="sxs-lookup"><span data-stu-id="3ecd5-194">Bounded execution</span></span>
<span data-ttu-id="3ecd5-195">Tutte le operazioni DB Cosmos devono essere completata entro server hello specificato richiesta la durata del timeout.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-195">All Cosmos DB operations must complete within hello server specified request timeout duration.</span></span> <span data-ttu-id="3ecd5-196">Questo vincolo si applica anche funzioni tooJavaScript (stored procedure, trigger e funzioni definite dall'utente).</span><span class="sxs-lookup"><span data-stu-id="3ecd5-196">This constraint also applies tooJavaScript functions (stored procedures, triggers and user-defined functions).</span></span> <span data-ttu-id="3ecd5-197">Se un'operazione non viene completato con tale limite, viene eseguito il rollback delle transazioni hello.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-197">If an operation does not complete with that time limit, hello transaction is rolled back.</span></span> <span data-ttu-id="3ecd5-198">Le funzioni JavaScript devono terminare entro il limite di tempo hello o implementare una continuazione in base modellare toobatch o ripresa l'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-198">JavaScript functions must finish within hello time limit or implement a continuation based model toobatch/resume execution.</span></span>  

<span data-ttu-id="3ecd5-199">In ordine toosimplify lo sviluppo di stored procedure e trigger toohandle termini, tutte le funzioni nell'oggetto raccolta hello (per creare, leggere, sostituire e l'eliminazione di documenti e allegati) restituiscono un valore booleano che rappresenta se che verrà completata l'operazione.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-199">In order toosimplify development of stored procedures and triggers toohandle time limits, all functions under hello collection object (for create, read, replace, and delete of documents and attachments) return a Boolean value that represents whether that operation will complete.</span></span> <span data-ttu-id="3ecd5-200">Se questo valore è false, è un'indicazione che il limite di tempo hello sta tooexpire e tale procedura hello deve eseguire il wrapping di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-200">If this value is false, it is an indication that hello time limit is about tooexpire and that hello procedure must wrap up execution.</span></span>  <span data-ttu-id="3ecd5-201">Operazioni in coda toohello precedente prima archivio non accettato operazione sono consentite toocomplete se procedure hello archiviato viene completato in tempo e non mette in coda a tutte le altre richieste.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-201">Operations queued prior toohello first unaccepted store operation are guaranteed toocomplete if hello stored procedure completes in time and does not queue any more requests.</span></span>  

<span data-ttu-id="3ecd5-202">Anche le funzioni JavaScript sono vincolate al consumo di risorse.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-202">JavaScript functions are also bounded on resource consumption.</span></span> <span data-ttu-id="3ecd5-203">COSMOS DB riserva velocità effettiva per ogni raccolta in base alle dimensioni di hello il provisioning di un account di database.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-203">Cosmos DB reserves throughput per collection based on hello provisioned size of a database account.</span></span> <span data-ttu-id="3ecd5-204">La velocità effettiva viene espressa in termini di un'unità normalizzata di consumo CPU, memoria e IO, denominata unità di richiesta, o RU.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-204">Throughput is expressed in terms of a normalized unit of CPU, memory and IO consumption called request units or RUs.</span></span> <span data-ttu-id="3ecd5-205">Le funzioni JavaScript possono comportare l'utilizzo di un numero elevato di unità riservate all'interno di un breve periodo di tempo e potrebbero ottenere frequenza limitata se viene raggiunto il limite dell'insieme di hello.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-205">JavaScript functions can potentially use up a large number of RUs within a short time, and might get rate-limited if hello collection’s limit is reached.</span></span> <span data-ttu-id="3ecd5-206">Stored procedure con utilizzo intensivo risorsa potrebbero inoltre essere messi in quarantena tooensure disponibilità delle operazioni di database primitivo.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-206">Resource intensive stored procedures might also be quarantined tooensure availability of primitive database operations.</span></span>  

### <a name="example-bulk-importing-data-into-a-database-program"></a><span data-ttu-id="3ecd5-207">Esempio: importazione in blocco dei dati in un programma di database</span><span class="sxs-lookup"><span data-stu-id="3ecd5-207">Example: Bulk importing data into a database program</span></span>
<span data-ttu-id="3ecd5-208">Di seguito è riportato un esempio di una stored procedure che viene scritto toobulk-importazione di documenti in una raccolta.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-208">Below is an example of a stored procedure that is written toobulk-import documents into a collection.</span></span> <span data-ttu-id="3ecd5-209">Si noti come hello esecuzione di stored procedure handle delimitati controllando hello Boolean restituito da createDocument e quindi utilizza hello conteggio dei documenti inseriti in ogni chiamata di hello stored procedure tootrack e riprendere lo stato di avanzamento in batch.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-209">Note how hello stored procedure handles bounded execution by checking hello Boolean return value from createDocument, and then uses hello count of documents inserted in each invocation of hello stored procedure tootrack and resume progress across batches.</span></span>

    function bulkImport(docs) {
        var collection = getContext().getCollection();
        var collectionLink = collection.getSelfLink();

        // hello count of imported docs, also used as current doc index.
        var count = 0;

        // Validate input.
        if (!docs) throw new Error("hello array is undefined or null.");

        var docsLength = docs.length;
        if (docsLength == 0) {
            getContext().getResponse().setBody(0);
        }

        // Call hello create API toocreate a document.
        tryCreate(docs[count], callback);

        // Note that there are 2 exit conditions:
        // 1) hello createDocument request was not accepted. 
        //    In this case hello callback will not be called, we just call setBody and we are done.
        // 2) hello callback was called docs.length times.
        //    In this case all documents were created and we don’t need toocall tryCreate anymore. Just call setBody and we are done.
        function tryCreate(doc, callback) {
            var isAccepted = collection.createDocument(collectionLink, doc, callback);

            // If hello request was accepted, callback will be called.
            // Otherwise report current count back toohello client, 
            // which will call hello script again with remaining set of docs.
            if (!isAccepted) getContext().getResponse().setBody(count);
        }

        // This is called when collection.createDocument is done in order tooprocess hello result.
        function callback(err, doc, options) {
            if (err) throw err;

            // One more document has been inserted, increment hello count.
            count++;

            if (count >= docsLength) {
                // If we created all documents, we are done. Just set hello response.
                getContext().getResponse().setBody(count);
            } else {
                // Create next document.
                tryCreate(docs[count], callback);
            }
        }
    }

## <span data-ttu-id="3ecd5-210"><a id="trigger"></a> Trigger del database</span><span class="sxs-lookup"><span data-stu-id="3ecd5-210"><a id="trigger"></a> Database triggers</span></span>
### <a name="database-pre-triggers"></a><span data-ttu-id="3ecd5-211">Pre-trigger del database</span><span class="sxs-lookup"><span data-stu-id="3ecd5-211">Database pre-triggers</span></span>
<span data-ttu-id="3ecd5-212">Cosmos DB include trigger che vengono eseguiti o attivati da un'operazione su un documento.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-212">Cosmos DB provides triggers that are executed or triggered by an operation on a document.</span></span> <span data-ttu-id="3ecd5-213">Ad esempio, è possibile specificare un pre-trigger quando si crea un documento, pre-trigger verrà eseguito prima che venga creato il documento hello.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-213">For example, you can specify a pre-trigger when you are creating a document – this pre-trigger will run before hello document is created.</span></span> <span data-ttu-id="3ecd5-214">Hello Ecco un esempio di come pre-trigger può essere utilizzato toovalidate hello proprietà di un documento che viene creato:</span><span class="sxs-lookup"><span data-stu-id="3ecd5-214">hello following is an example of how pre-triggers can be used toovalidate hello properties of a document that is being created:</span></span>

    var validateDocumentContentsTrigger = {
        id: "validateDocumentContents",
        serverScript: function validate() {
            var context = getContext();
            var request = context.getRequest();

            // document toobe created in hello current operation
            var documentToCreate = request.getBody();

            // validate properties
            if (!("timestamp" in documentToCreate)) {
                var ts = new Date();
                documentToCreate["my timestamp"] = ts.getTime();
            }

            // update hello document that will be created
            request.setBody(documentToCreate);
        },
        triggerType: TriggerType.Pre,
        triggerOperation: TriggerOperation.Create
    }


<span data-ttu-id="3ecd5-215">E hello corrispondente codice di registrazione client-side Node.js per trigger hello:</span><span class="sxs-lookup"><span data-stu-id="3ecd5-215">And hello corresponding Node.js client-side registration code for hello trigger:</span></span>

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


<span data-ttu-id="3ecd5-216">I pre-trigger non possono avere parametri di input.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-216">Pre-triggers cannot have any input parameters.</span></span> <span data-ttu-id="3ecd5-217">oggetto richiesta Hello può essere utilizzato toomanipulate messaggio di richiesta di hello associato all'operazione hello.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-217">hello request object can be used toomanipulate hello request message associated with hello operation.</span></span> <span data-ttu-id="3ecd5-218">In questo caso, pre-trigger di hello è in esecuzione con creazione hello di un documento e corpo del messaggio di richiesta di hello contiene toobe documento hello creato in formato JSON.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-218">Here, hello pre-trigger is being run with hello creation of a document, and hello request message body contains hello document toobe created in JSON format.</span></span>   

<span data-ttu-id="3ecd5-219">Quando i trigger vengono registrati, gli utenti possono specificare le operazioni eseguibili con hello.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-219">When triggers are registered, users can specify hello operations that it can run with.</span></span> <span data-ttu-id="3ecd5-220">Questo trigger è stato creato con TriggerOperation.Create, ovvero seguente hello non è consentito.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-220">This trigger was created with TriggerOperation.Create, which means hello following is not permitted.</span></span>

    var options = { preTriggerInclude: "validateDocumentContents" };

    client.replaceDocumentAsync(docToReplace.self,
                  newDocBody, options)
    .then(function (response) {
        console.log(response.resource);
    }, function (error) {
        console.log("Error", error);
    });

    // Fails, can’t use a create trigger in a replace operation

### <a name="database-post-triggers"></a><span data-ttu-id="3ecd5-221">Post-trigger del database</span><span class="sxs-lookup"><span data-stu-id="3ecd5-221">Database post-triggers</span></span>
<span data-ttu-id="3ecd5-222">I post-trigger, come i pre-trigger, sono associati a un'operazione su un documento e non accettano parametri di input.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-222">Post-triggers, like pre-triggers, are associated with an operation on a document and don’t take any input parameters.</span></span> <span data-ttu-id="3ecd5-223">Vengono eseguiti **dopo** hello operazione è stata completata e hanno accesso toohello risposta messaggio che viene inviato toohello client.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-223">They run **after** hello operation has completed, and have access toohello response message that is sent toohello client.</span></span>   

<span data-ttu-id="3ecd5-224">Hello di esempio seguente mostra i post-trigger in azione:</span><span class="sxs-lookup"><span data-stu-id="3ecd5-224">hello following example shows post-triggers in action:</span></span>

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
            if(!accept) throw "Unable tooupdate metadata, abort";

            function updateMetadataCallback(err, documents, responseOptions) {
                if(err) throw new Error("Error" + err.message);
                         if(documents.length != 1) throw 'Unable toofind metadata document';

                         var metadataDocument = documents[0];

                         // update metadata
                         metadataDocument.createdDocuments += 1;
                         metadataDocument.createdNames += " " + createdDocument.id;
                         var accept = collection.replaceDocument(metadataDocument._self,
                               metadataDocument, function(err, docReplaced) {
                                      if(err) throw "Unable tooupdate metadata, abort";
                               });
                         if(!accept) throw "Unable tooupdate metadata, abort";
                         return;                    
            }                                                                                            
        },
        triggerType: TriggerType.Post,
        triggerOperation: TriggerOperation.All
    }


<span data-ttu-id="3ecd5-225">trigger Hello possono essere registrati come illustrato nel seguente esempio hello.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-225">hello trigger can be registered as shown in hello following sample.</span></span>

    // register post-trigger
    client.createTriggerAsync('dbs/testdb/colls/testColl', updateMetadataTrigger)
        .then(function(createdTrigger) { 
            var docToCreate = { 
                name: "artist_profile_1023",
                artist: "hello Band",
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


<span data-ttu-id="3ecd5-226">Trigger di una query per il documento di metadati hello e viene aggiornato con i dettagli sul documento hello appena creato.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-226">This trigger queries for hello metadata document and updates it with details about hello newly created document.</span></span>  

<span data-ttu-id="3ecd5-227">Un aspetto importante toonote hello **transazionale** esecuzione dei trigger nel database Cosmos.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-227">One thing that is important toonote is hello **transactional** execution of triggers in Cosmos DB.</span></span> <span data-ttu-id="3ecd5-228">Questo post-trigger viene eseguito come parte di hello creazione hello del documento originale hello stessa transazione.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-228">This post-trigger runs as part of hello same transaction as hello creation of hello original document.</span></span> <span data-ttu-id="3ecd5-229">Pertanto, se viene generata un'eccezione da un post-trigger di hello (ad esempio se il canale è documento di metadati non è possibile tooupdate hello), dell'intera transazione hello avrà esito negativo e il rollback.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-229">Therefore, if we throw an exception from hello post-trigger (say if we are unable tooupdate hello metadata document), hello whole transaction will fail and be rolled back.</span></span> <span data-ttu-id="3ecd5-230">Non verrà creato alcun documento e verrà restituita un'eccezione.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-230">No document will be created, and an exception will be returned.</span></span>  

## <span data-ttu-id="3ecd5-231"><a id="udf"></a>Funzioni definite dall'utente</span><span class="sxs-lookup"><span data-stu-id="3ecd5-231"><a id="udf"></a>User-defined functions</span></span>
<span data-ttu-id="3ecd5-232">Funzioni definite dall'utente (UDF) sono grammatica del linguaggio query SQL API DocumentDB hello tooextend utilizzata e implementano la logica di business personalizzata.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-232">User-defined functions (UDFs) are used tooextend hello DocumentDB API SQL query language grammar and implement custom business logic.</span></span> <span data-ttu-id="3ecd5-233">Possono essere richiamate solo dall'interno delle query.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-233">They can only be called from inside queries.</span></span> <span data-ttu-id="3ecd5-234">Non dispongono di oggetto di contesto di accesso toohello ma sono concepite toobe utilizzato come JavaScript di solo calcolo.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-234">They do not have access toohello context object and are meant toobe used as compute-only JavaScript.</span></span> <span data-ttu-id="3ecd5-235">Pertanto, è possibile eseguire funzioni definite dall'utente nelle repliche secondarie di hello servizio DB Cosmos.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-235">Therefore, UDFs can be run on secondary replicas of hello Cosmos DB service.</span></span>  

<span data-ttu-id="3ecd5-236">Hello esempio seguente viene creata una funzione definita dall'utente toocalculate reddito in base alle tariffe per parentesi quadre reddito diversi e viene utilizzata all'interno di una query toofind tutti gli utenti a pagamento di più di 20.000 $ imposte.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-236">hello following sample creates a UDF toocalculate income tax based on rates for various income brackets, and then uses it inside a query toofind all people who paid more than $20,000 in taxes.</span></span>

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


<span data-ttu-id="3ecd5-237">Hello funzione definita dall'utente può essere usato in seguito nelle query, come nel seguente esempio hello:</span><span class="sxs-lookup"><span data-stu-id="3ecd5-237">hello UDF can subsequently be used in queries like in hello following sample:</span></span>

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

## <a name="javascript-language-integrated-query-api"></a><span data-ttu-id="3ecd5-238">API della Language-Integrated Query di JavaScript</span><span class="sxs-lookup"><span data-stu-id="3ecd5-238">JavaScript language-integrated query API</span></span>
<span data-ttu-id="3ecd5-239">Query tooissuing utilizzando la grammatica SQL di DocumentDB, hello SDK lato server consente inoltre tooperform con ottimizzazione per la query utilizzando un'interfaccia intuitiva di JavaScript senza la conoscenza di SQL.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-239">In addition tooissuing queries using DocumentDB’s SQL grammar, hello server-side SDK allows you tooperform optimized queries using a fluent JavaScript interface without any knowledge of SQL.</span></span> <span data-ttu-id="3ecd5-240">query di JavaScript Hello che API consente query compilazione tooprogrammatically passando le funzioni di predicato in funzione concatenabile chiama, con un tooECMAScript5 familiare sintassi incorporati di matrice e librerie JavaScript più diffuse come lodash.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-240">hello JavaScript query API allows you tooprogrammatically build queries by passing predicate functions into chainable function calls, with a syntax familiar tooECMAScript5's Array built-ins and popular JavaScript libraries like lodash.</span></span> <span data-ttu-id="3ecd5-241">Le query vengono analizzate dal hello JavaScript runtime toobe eseguiti in modo efficiente con gli indici del database di Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-241">Queries are parsed by hello JavaScript runtime toobe executed efficiently using Azure Cosmos DB’s indices.</span></span>

> [!NOTE]
> <span data-ttu-id="3ecd5-242">`__`(doppio carattere di sottolineatura) è un alias troppo`getContext().getCollection()`.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-242">`__` (double-underscore) is an alias too`getContext().getCollection()`.</span></span>
> <br/>
> <span data-ttu-id="3ecd5-243">In altre parole, è possibile utilizzare `__` o `getContext().getCollection()` tooaccess hello API query JavaScript.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-243">In other words, you can use `__` or `getContext().getCollection()` tooaccess hello JavaScript query API.</span></span>
> 
> 

<span data-ttu-id="3ecd5-244">Tra le funzioni supportate:</span><span class="sxs-lookup"><span data-stu-id="3ecd5-244">Supported functions include:</span></span>

<ul>
<li><span data-ttu-id="3ecd5-245">
<b>chain() ... .value([callback] [, options])</b>
</span><span class="sxs-lookup"><span data-stu-id="3ecd5-245">
<b>chain() ... .value([callback] [, options])</b>
</span></span><ul>
<li>
<span data-ttu-id="3ecd5-246">Avvia una chiamata concatenata che deve terminare con value().</span><span class="sxs-lookup"><span data-stu-id="3ecd5-246">Starts a chained call which must be terminated with value().</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="3ecd5-247">
<b>filter(predicateFunction [, options] [, callback])</b>
</span><span class="sxs-lookup"><span data-stu-id="3ecd5-247">
<b>filter(predicateFunction [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="3ecd5-248">I filtri di input utilizzando una funzione di predicato restituisce true o false in ordine toofilter documenti di input in/out nel set risultante hello hello.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-248">Filters hello input using a predicate function which returns true/false in order toofilter in/out input documents into hello resulting set.</span></span> <span data-ttu-id="3ecd5-249">Questo comportamento è simile tooa clausola WHERE in SQL.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-249">This behaves similar tooa WHERE clause in SQL.</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="3ecd5-250">
<b>map(transformationFunction [, options] [, callback])</b>
</span><span class="sxs-lookup"><span data-stu-id="3ecd5-250">
<b>map(transformationFunction [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="3ecd5-251">Si applica una proiezione di una funzione di trasformazione che esegue il mapping di ogni oggetto JavaScript tooa di elemento di input o il valore specificata.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-251">Applies a projection given a transformation function which maps each input item tooa JavaScript object or value.</span></span> <span data-ttu-id="3ecd5-252">Questo comportamento è simile tooa di clausola SELECT in SQL.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-252">This behaves similar tooa SELECT clause in SQL.</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="3ecd5-253">
<b>pluck([propertyName] [, options] [, callback])</b>
</span><span class="sxs-lookup"><span data-stu-id="3ecd5-253">
<b>pluck([propertyName] [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="3ecd5-254">Si tratta di un collegamento per una mappa che estrae il valore di hello di una singola proprietà di ogni elemento di input.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-254">This is a shortcut for a map which extracts hello value of a single property from each input item.</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="3ecd5-255">
<b>flatten([isShallow] [, options] [, callback])</b>
</span><span class="sxs-lookup"><span data-stu-id="3ecd5-255">
<b>flatten([isShallow] [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="3ecd5-256">Combina e appiattisce matrici da ogni elemento di input in tooa singola matrice.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-256">Combines and flattens arrays from each input item in tooa single array.</span></span> <span data-ttu-id="3ecd5-257">Questo comportamento tooSelectMany simili nelle query LINQ.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-257">This behaves similar tooSelectMany in LINQ.</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="3ecd5-258">
<b>sortBy([predicate] [, options] [, callback])</b>
</span><span class="sxs-lookup"><span data-stu-id="3ecd5-258">
<b>sortBy([predicate] [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="3ecd5-259">Generare un nuovo set di documenti quando si ordinano i documenti hello nel flusso di input documento hello in ordine crescente utilizzando hello predicato specificato.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-259">Produce a new set of documents by sorting hello documents in hello input document stream in ascending order using hello given predicate.</span></span> <span data-ttu-id="3ecd5-260">Questo comportamento è simile tooa clausola ORDER BY in SQL.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-260">This behaves similar tooa ORDER BY clause in SQL.</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="3ecd5-261">
<b>sortByDescending([predicate] [, options] [, callback])</b>
</span><span class="sxs-lookup"><span data-stu-id="3ecd5-261">
<b>sortByDescending([predicate] [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="3ecd5-262">Generare un nuovo set di documenti quando si ordinano i documenti hello nel flusso di input documento hello in ordine decrescente utilizzando hello predicato specificato.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-262">Produce a new set of documents by sorting hello documents in hello input document stream in descending order using hello given predicate.</span></span> <span data-ttu-id="3ecd5-263">Il funzionamento è simile clausola ORDER BY x DESC tooa SQL.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-263">This behaves similar tooa ORDER BY x DESC clause in SQL.</span></span>
</li>
</ul>
</li>
</ul>


<span data-ttu-id="3ecd5-264">Quando incluso all'interno delle funzioni di predicato e/o selettore, hello seguenti costrutti JavaScript ottengono automaticamente ottimizzato toorun direttamente nel database di Azure Cosmos indici:</span><span class="sxs-lookup"><span data-stu-id="3ecd5-264">When included inside predicate and/or selector functions, hello following JavaScript constructs get automatically optimized toorun directly on Azure Cosmos DB indices:</span></span>

* <span data-ttu-id="3ecd5-265">Operatori semplici: = + - * / % | ^ &amp; == != === !=== &lt; &gt; &lt;= &gt;= || &amp;&amp; &lt;&lt; &gt;&gt; &gt;&gt;&gt;!</span><span class="sxs-lookup"><span data-stu-id="3ecd5-265">Simple operators: = + - * / % | ^ &amp; == != === !=== &lt; &gt; &lt;= &gt;= || &amp;&amp; &lt;&lt; &gt;&gt; &gt;&gt;&gt;!</span></span> ~
* <span data-ttu-id="3ecd5-266">Valori letterali, inclusi valore letterale di oggetto hello: {}</span><span class="sxs-lookup"><span data-stu-id="3ecd5-266">Literals, including hello object literal: {}</span></span>
* <span data-ttu-id="3ecd5-267">var, return</span><span class="sxs-lookup"><span data-stu-id="3ecd5-267">var, return</span></span>

<span data-ttu-id="3ecd5-268">Hello JavaScript seguente costruisce non ottenere ottimizzata per gli indici di database Cosmos Azure:</span><span class="sxs-lookup"><span data-stu-id="3ecd5-268">hello following JavaScript constructs do not get optimized for Azure Cosmos DB indices:</span></span>

* <span data-ttu-id="3ecd5-269">Flusso di controllo (ad esempio, se, per, mentre)</span><span class="sxs-lookup"><span data-stu-id="3ecd5-269">Control flow (e.g. if, for, while)</span></span>
* <span data-ttu-id="3ecd5-270">Chiamate di funzione</span><span class="sxs-lookup"><span data-stu-id="3ecd5-270">Function calls</span></span>

<span data-ttu-id="3ecd5-271">Per ulteriori informazioni, vedere [Server-Side JSDocs](http://azure.github.io/azure-documentdb-js-server/).</span><span class="sxs-lookup"><span data-stu-id="3ecd5-271">For more information, please see our [Server-Side JSDocs](http://azure.github.io/azure-documentdb-js-server/).</span></span>

### <a name="example-write-a-stored-procedure-using-hello-javascript-query-api"></a><span data-ttu-id="3ecd5-272">Esempio: Scrivere una stored procedure utilizzando l'API di query hello JavaScript</span><span class="sxs-lookup"><span data-stu-id="3ecd5-272">Example: Write a stored procedure using hello JavaScript query API</span></span>
<span data-ttu-id="3ecd5-273">Hello nell'esempio di codice seguente è riportato un esempio di come utilizzare JavaScript Query API hello nel contesto di hello di una stored procedure.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-273">hello following code sample is an example of how hello JavaScript Query API can be used in hello context of a stored procedure.</span></span> <span data-ttu-id="3ecd5-274">Inserisce un documento, fornito dal parametro di input, Hello stored procedure e aggiorna un documento di metadati utilizzando hello `__.filter()` metodo, con minSize, maxSize e totalSize in base alla proprietà di dimensioni del documento input hello.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-274">hello stored procedure inserts a document, given by an input parameter, and updates a metadata document, using hello `__.filter()` method, with minSize, maxSize, and totalSize based upon hello input document's size property.</span></span>

    /**
     * Insert actual doc and update metadata doc: minSize, maxSize, totalSize based on doc.size.
     */
    function insertDocumentAndUpdateMetadata(doc) {
      // HTTP error codes sent tooour callback funciton by DocDB server.
      var ErrorCode = {
        RETRY_WITH: 449,
      }

      var isAccepted = __.createDocument(__.getSelfLink(), doc, {}, function(err, doc, options) {
        if (err) throw err;

        // Check hello doc (ignore docs with invalid/zero size and metaDoc itself) and call updateMetadata.
        if (!doc.isMetadata && doc.size > 0) {
          // Get hello meta document. We keep it in hello same collection. it's hello only doc that has .isMetadata = true.
          var result = __.filter(function(x) {
            return x.isMetadata === true
          }, function(err, feed, options) {
            if (err) throw err;

            // We assume that metadata doc was pre-created and must exist when this script is called.
            if (!feed || !feed.length) throw new Error("Failed toofind hello metadata document.");

            // hello metadata document.
            var metaDoc = feed[0];

            // Update metaDoc.minSize:
            // for 1st document use doc.Size, for all hello rest see if it's less than last min.
            if (metaDoc.minSize == 0) metaDoc.minSize = doc.size;
            else metaDoc.minSize = Math.min(metaDoc.minSize, doc.size);

            // Update metaDoc.maxSize.
            metaDoc.maxSize = Math.max(metaDoc.maxSize, doc.size);

            // Update metaDoc.totalSize.
            metaDoc.totalSize += doc.size;

            // Update/replace hello metadata document in hello store.
            var isAccepted = __.replaceDocument(metaDoc._self, metaDoc, function(err) {
              if (err) throw err;
              // Note: in case concurrent updates causes conflict with ErrorCode.RETRY_WITH, we can't read hello meta again 
              //       and update again because due tooSnapshot isolation we will read same exact version (we are in same transaction).
              //       We have tootake care of that on hello client side.
            });
            if (!isAccepted) throw new Error("replaceDocument(metaDoc) returned false.");
          });
          if (!result.isAccepted) throw new Error("filter for metaDoc returned false.");
        }
      });
      if (!isAccepted) throw new Error("createDocument(actual doc) returned false.");
    }

## <a name="sql-toojavascript-cheat-sheet"></a><span data-ttu-id="3ecd5-275">Foglio informativo tooJavascript SQL</span><span class="sxs-lookup"><span data-stu-id="3ecd5-275">SQL tooJavascript cheat sheet</span></span>
<span data-ttu-id="3ecd5-276">Hello tabella seguente vengono illustrate diverse query JavaScript corrispondente hello e query SQL.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-276">hello following table presents various SQL queries and hello corresponding JavaScript queries.</span></span>

<span data-ttu-id="3ecd5-277">Come le query SQL, le chiavi di proprietà del documento (ad esempio `doc.id`) fanno distinzione tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-277">As with SQL queries, document property keys (e.g. `doc.id`) are case-sensitive.</span></span>

|<span data-ttu-id="3ecd5-278">SQL</span><span class="sxs-lookup"><span data-stu-id="3ecd5-278">SQL</span></span>| <span data-ttu-id="3ecd5-279">API di query JavaScript</span><span class="sxs-lookup"><span data-stu-id="3ecd5-279">JavaScript Query API</span></span>|<span data-ttu-id="3ecd5-280">Descrizione sotto</span><span class="sxs-lookup"><span data-stu-id="3ecd5-280">Description below</span></span>|
|---|---|---|
|<span data-ttu-id="3ecd5-281">SELECT *</span><span class="sxs-lookup"><span data-stu-id="3ecd5-281">SELECT *</span></span><br><span data-ttu-id="3ecd5-282">FROM docs</span><span class="sxs-lookup"><span data-stu-id="3ecd5-282">FROM docs</span></span>| <span data-ttu-id="3ecd5-283">__.map(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="3ecd5-283">__.map(function(doc) {</span></span> <br><span data-ttu-id="3ecd5-284">&nbsp;&nbsp;&nbsp;&nbsp;return doc;</span><span class="sxs-lookup"><span data-stu-id="3ecd5-284">&nbsp;&nbsp;&nbsp;&nbsp;return doc;</span></span><br><span data-ttu-id="3ecd5-285">});</span><span class="sxs-lookup"><span data-stu-id="3ecd5-285">});</span></span>|<span data-ttu-id="3ecd5-286">1</span><span class="sxs-lookup"><span data-stu-id="3ecd5-286">1</span></span>|
|<span data-ttu-id="3ecd5-287">SELECT docs.id, docs.message AS msg, docs.actions</span><span class="sxs-lookup"><span data-stu-id="3ecd5-287">SELECT docs.id, docs.message AS msg, docs.actions</span></span> <br><span data-ttu-id="3ecd5-288">FROM docs</span><span class="sxs-lookup"><span data-stu-id="3ecd5-288">FROM docs</span></span>|<span data-ttu-id="3ecd5-289">__.map(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="3ecd5-289">__.map(function(doc) {</span></span><br><span data-ttu-id="3ecd5-290">&nbsp;&nbsp;&nbsp;&nbsp;return {</span><span class="sxs-lookup"><span data-stu-id="3ecd5-290">&nbsp;&nbsp;&nbsp;&nbsp;return {</span></span><br><span data-ttu-id="3ecd5-291">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;id: doc.id,</span><span class="sxs-lookup"><span data-stu-id="3ecd5-291">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;id: doc.id,</span></span><br><span data-ttu-id="3ecd5-292">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;msg: doc.message,</span><span class="sxs-lookup"><span data-stu-id="3ecd5-292">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;msg: doc.message,</span></span><br><span data-ttu-id="3ecd5-293">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;actions:doc.actions</span><span class="sxs-lookup"><span data-stu-id="3ecd5-293">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;actions:doc.actions</span></span><br><span data-ttu-id="3ecd5-294">&nbsp;&nbsp;&nbsp;&nbsp;};</span><span class="sxs-lookup"><span data-stu-id="3ecd5-294">&nbsp;&nbsp;&nbsp;&nbsp;};</span></span><br><span data-ttu-id="3ecd5-295">});</span><span class="sxs-lookup"><span data-stu-id="3ecd5-295">});</span></span>|<span data-ttu-id="3ecd5-296">2</span><span class="sxs-lookup"><span data-stu-id="3ecd5-296">2</span></span>|
|<span data-ttu-id="3ecd5-297">SELECT *</span><span class="sxs-lookup"><span data-stu-id="3ecd5-297">SELECT *</span></span><br><span data-ttu-id="3ecd5-298">FROM docs</span><span class="sxs-lookup"><span data-stu-id="3ecd5-298">FROM docs</span></span><br><span data-ttu-id="3ecd5-299">WHERE docs.id="X998_Y998"</span><span class="sxs-lookup"><span data-stu-id="3ecd5-299">WHERE docs.id="X998_Y998"</span></span>|<span data-ttu-id="3ecd5-300">__.filter(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="3ecd5-300">__.filter(function(doc) {</span></span><br><span data-ttu-id="3ecd5-301">&nbsp;&nbsp;&nbsp;&nbsp;return doc.id ==="X998_Y998";</span><span class="sxs-lookup"><span data-stu-id="3ecd5-301">&nbsp;&nbsp;&nbsp;&nbsp;return doc.id ==="X998_Y998";</span></span><br><span data-ttu-id="3ecd5-302">});</span><span class="sxs-lookup"><span data-stu-id="3ecd5-302">});</span></span>|<span data-ttu-id="3ecd5-303">3</span><span class="sxs-lookup"><span data-stu-id="3ecd5-303">3</span></span>|
|<span data-ttu-id="3ecd5-304">SELECT *</span><span class="sxs-lookup"><span data-stu-id="3ecd5-304">SELECT *</span></span><br><span data-ttu-id="3ecd5-305">FROM docs</span><span class="sxs-lookup"><span data-stu-id="3ecd5-305">FROM docs</span></span><br><span data-ttu-id="3ecd5-306">WHERE ARRAY_CONTAINS(docs.Tags, 123)</span><span class="sxs-lookup"><span data-stu-id="3ecd5-306">WHERE ARRAY_CONTAINS(docs.Tags, 123)</span></span>|<span data-ttu-id="3ecd5-307">__.filter(function(x) {</span><span class="sxs-lookup"><span data-stu-id="3ecd5-307">__.filter(function(x) {</span></span><br><span data-ttu-id="3ecd5-308">&nbsp;&nbsp;&nbsp;&nbsp;return x.Tags && x.Tags.indexOf(123) > -1;</span><span class="sxs-lookup"><span data-stu-id="3ecd5-308">&nbsp;&nbsp;&nbsp;&nbsp;return x.Tags && x.Tags.indexOf(123) > -1;</span></span><br><span data-ttu-id="3ecd5-309">});</span><span class="sxs-lookup"><span data-stu-id="3ecd5-309">});</span></span>|<span data-ttu-id="3ecd5-310">4</span><span class="sxs-lookup"><span data-stu-id="3ecd5-310">4</span></span>|
|<span data-ttu-id="3ecd5-311">SELECT docs.id, docs.message AS msg</span><span class="sxs-lookup"><span data-stu-id="3ecd5-311">SELECT docs.id, docs.message AS msg</span></span><br><span data-ttu-id="3ecd5-312">FROM docs</span><span class="sxs-lookup"><span data-stu-id="3ecd5-312">FROM docs</span></span><br><span data-ttu-id="3ecd5-313">WHERE docs.id="X998_Y998"</span><span class="sxs-lookup"><span data-stu-id="3ecd5-313">WHERE docs.id="X998_Y998"</span></span>|<span data-ttu-id="3ecd5-314">__.chain()</span><span class="sxs-lookup"><span data-stu-id="3ecd5-314">__.chain()</span></span><br><span data-ttu-id="3ecd5-315">&nbsp;&nbsp;&nbsp;&nbsp;.filter(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="3ecd5-315">&nbsp;&nbsp;&nbsp;&nbsp;.filter(function(doc) {</span></span><br><span data-ttu-id="3ecd5-316">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return doc.id ==="X998_Y998";</span><span class="sxs-lookup"><span data-stu-id="3ecd5-316">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return doc.id ==="X998_Y998";</span></span><br><span data-ttu-id="3ecd5-317">&nbsp;&nbsp;&nbsp;&nbsp;})</span><span class="sxs-lookup"><span data-stu-id="3ecd5-317">&nbsp;&nbsp;&nbsp;&nbsp;})</span></span><br><span data-ttu-id="3ecd5-318">&nbsp;&nbsp;&nbsp;&nbsp;.map(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="3ecd5-318">&nbsp;&nbsp;&nbsp;&nbsp;.map(function(doc) {</span></span><br><span data-ttu-id="3ecd5-319">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return {</span><span class="sxs-lookup"><span data-stu-id="3ecd5-319">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return {</span></span><br><span data-ttu-id="3ecd5-320">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;id: doc.id,</span><span class="sxs-lookup"><span data-stu-id="3ecd5-320">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;id: doc.id,</span></span><br><span data-ttu-id="3ecd5-321">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;msg: doc.message</span><span class="sxs-lookup"><span data-stu-id="3ecd5-321">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;msg: doc.message</span></span><br><span data-ttu-id="3ecd5-322">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;};</span><span class="sxs-lookup"><span data-stu-id="3ecd5-322">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;};</span></span><br><span data-ttu-id="3ecd5-323">&nbsp;&nbsp;&nbsp;&nbsp;})</span><span class="sxs-lookup"><span data-stu-id="3ecd5-323">&nbsp;&nbsp;&nbsp;&nbsp;})</span></span><br><span data-ttu-id="3ecd5-324">.value();</span><span class="sxs-lookup"><span data-stu-id="3ecd5-324">.value();</span></span>|<span data-ttu-id="3ecd5-325">5</span><span class="sxs-lookup"><span data-stu-id="3ecd5-325">5</span></span>|
|<span data-ttu-id="3ecd5-326">SELECT VALUE tag</span><span class="sxs-lookup"><span data-stu-id="3ecd5-326">SELECT VALUE tag</span></span><br><span data-ttu-id="3ecd5-327">FROM docs</span><span class="sxs-lookup"><span data-stu-id="3ecd5-327">FROM docs</span></span><br><span data-ttu-id="3ecd5-328">JOIN tag IN docs.Tags</span><span class="sxs-lookup"><span data-stu-id="3ecd5-328">JOIN tag IN docs.Tags</span></span><br><span data-ttu-id="3ecd5-329">ORDER BY docs._ts</span><span class="sxs-lookup"><span data-stu-id="3ecd5-329">ORDER BY docs._ts</span></span>|<span data-ttu-id="3ecd5-330">__.chain()</span><span class="sxs-lookup"><span data-stu-id="3ecd5-330">__.chain()</span></span><br><span data-ttu-id="3ecd5-331">&nbsp;&nbsp;&nbsp;&nbsp;.filter(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="3ecd5-331">&nbsp;&nbsp;&nbsp;&nbsp;.filter(function(doc) {</span></span><br><span data-ttu-id="3ecd5-332">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;return doc.Tags &amp;&amp; Array.isArray(doc.Tags);</span><span class="sxs-lookup"><span data-stu-id="3ecd5-332">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return doc.Tags && Array.isArray(doc.Tags);</span></span><br><span data-ttu-id="3ecd5-333">&nbsp;&nbsp;&nbsp;&nbsp;})</span><span class="sxs-lookup"><span data-stu-id="3ecd5-333">&nbsp;&nbsp;&nbsp;&nbsp;})</span></span><br><span data-ttu-id="3ecd5-334">&nbsp;&nbsp;&nbsp;&nbsp;.sortBy(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="3ecd5-334">&nbsp;&nbsp;&nbsp;&nbsp;.sortBy(function(doc) {</span></span><br><span data-ttu-id="3ecd5-335">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return doc._ts;</span><span class="sxs-lookup"><span data-stu-id="3ecd5-335">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return doc._ts;</span></span><br><span data-ttu-id="3ecd5-336">&nbsp;&nbsp;&nbsp;&nbsp;})</span><span class="sxs-lookup"><span data-stu-id="3ecd5-336">&nbsp;&nbsp;&nbsp;&nbsp;})</span></span><br><span data-ttu-id="3ecd5-337">&nbsp;&nbsp;&nbsp;&nbsp;.pluck("Tags")</span><span class="sxs-lookup"><span data-stu-id="3ecd5-337">&nbsp;&nbsp;&nbsp;&nbsp;.pluck("Tags")</span></span><br><span data-ttu-id="3ecd5-338">&nbsp;&nbsp;&nbsp;&nbsp;.flatten()</span><span class="sxs-lookup"><span data-stu-id="3ecd5-338">&nbsp;&nbsp;&nbsp;&nbsp;.flatten()</span></span><br><span data-ttu-id="3ecd5-339">&nbsp;&nbsp;&nbsp;&nbsp;.value()</span><span class="sxs-lookup"><span data-stu-id="3ecd5-339">&nbsp;&nbsp;&nbsp;&nbsp;.value()</span></span>|<span data-ttu-id="3ecd5-340">6</span><span class="sxs-lookup"><span data-stu-id="3ecd5-340">6</span></span>|

<span data-ttu-id="3ecd5-341">Hello descrizioni riportate di seguito viene illustrato ogni query della tabella hello precedente.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-341">hello following descriptions explain each query in hello table above.</span></span>
1. <span data-ttu-id="3ecd5-342">Viene restituita così com'è in tutti i documenti, impaginati con token di continuazione.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-342">Results in all documents (paginated with continuation token) as is.</span></span>
2. <span data-ttu-id="3ecd5-343">Progetti hello id, il messaggio (alias toomsg) e azione da tutti i documenti.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-343">Projects hello id, message (aliased toomsg), and action from all documents.</span></span>
3. <span data-ttu-id="3ecd5-344">Le query per i documenti con un predicato hello: id = "X998_Y998".</span><span class="sxs-lookup"><span data-stu-id="3ecd5-344">Queries for documents with hello predicate: id = "X998_Y998".</span></span>
4. <span data-ttu-id="3ecd5-345">Le query per i documenti che presentano una proprietà di tag e tag è una matrice che contiene il valore di hello 123.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-345">Queries for documents that have a Tags property and Tags is an array containing hello value 123.</span></span>
5. <span data-ttu-id="3ecd5-346">Le query per i documenti con un predicato, id = "X998_Y998" e id di hello quindi progetti e dei messaggi (toomsg alias).</span><span class="sxs-lookup"><span data-stu-id="3ecd5-346">Queries for documents with a predicate, id = "X998_Y998", and then projects hello id and message (aliased toomsg).</span></span>
6. <span data-ttu-id="3ecd5-347">I filtri per i documenti che hanno una proprietà di matrice, tag, e documenti risultanti hello vengono ordinati in proprietà sistema del timestamp hello TS e quindi proiettato + appiattisce la matrice di tag hello.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-347">Filters for documents which have an array property, Tags, and sorts hello resulting documents by hello _ts timestamp system property, and then projects + flattens hello Tags array.</span></span>


## <a name="runtime-support"></a><span data-ttu-id="3ecd5-348">Supporto di runtime</span><span class="sxs-lookup"><span data-stu-id="3ecd5-348">Runtime support</span></span>
<span data-ttu-id="3ecd5-349">[API sul lato server di DocumentDB JavaScript](http://azure.github.io/azure-documentdb-js-server/) fornisce il supporto per hello la maggior parte delle hello mainstream funzionalità del linguaggio JavaScript come standard da [ECMA-262](http://www.ecma-international.org/publications/standards/Ecma-262.htm).</span><span class="sxs-lookup"><span data-stu-id="3ecd5-349">[DocumentDB JavaScript server side API](http://azure.github.io/azure-documentdb-js-server/) provides support for hello most of hello mainstream JavaScript language features as standardized by [ECMA-262](http://www.ecma-international.org/publications/standards/Ecma-262.htm).</span></span>

### <a name="security"></a><span data-ttu-id="3ecd5-350">Sicurezza</span><span class="sxs-lookup"><span data-stu-id="3ecd5-350">Security</span></span>
<span data-ttu-id="3ecd5-351">JavaScript stored procedure e trigger vengono create mediante sandbox in modo che gli effetti di hello di uno script non modificati non perdono toohello altri senza passare attraverso l'isolamento delle transazioni snapshot di hello a livello di database hello.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-351">JavaScript stored procedures and triggers are sandboxed so that hello effects of one script do not leak toohello other without going through hello snapshot transaction isolation at hello database level.</span></span> <span data-ttu-id="3ecd5-352">gli ambienti di runtime Hello sono in pool ma puliti del contesto di hello dopo ogni esecuzione.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-352">hello runtime environments are pooled but cleaned of hello context after each run.</span></span> <span data-ttu-id="3ecd5-353">Sono pertanto sono sicuramente toobe provvisoria di tutti gli effetti collaterali non intenzionali tra loro.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-353">Hence they are guaranteed toobe safe of any unintended side effects from each other.</span></span>

### <a name="pre-compilation"></a><span data-ttu-id="3ecd5-354">Precompilazione</span><span class="sxs-lookup"><span data-stu-id="3ecd5-354">Pre-compilation</span></span>
<span data-ttu-id="3ecd5-355">Stored procedure, trigger e funzioni definite dall'utente sono formato di codice in modo implicito precompilata toohello byte nel costo di compilazione tooavoid ordine in fase di hello di ogni chiamata dello script.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-355">Stored procedures, triggers and UDFs are implicitly precompiled toohello byte code format in order tooavoid compilation cost at hello time of each script invocation.</span></span> <span data-ttu-id="3ecd5-356">Questo garantisce la velocità elevata e il footprint ridotto delle chiamate delle stored procedure.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-356">This ensures invocations of stored procedures are fast and have a low footprint.</span></span>

## <a name="client-sdk-support"></a><span data-ttu-id="3ecd5-357">Supporto di client SDK</span><span class="sxs-lookup"><span data-stu-id="3ecd5-357">Client SDK support</span></span>
<span data-ttu-id="3ecd5-358">In aggiunta toohello API DocumentDB per [Node.js](documentdb-sdk-node.md) dispone di client, Azure Cosmos DB [.NET](documentdb-sdk-dotnet.md), [.NET Core](documentdb-sdk-dotnet-core.md), [Java](documentdb-sdk-java.md), [ JavaScript](http://azure.github.io/azure-documentdb-js/), e [Python SDK](documentdb-sdk-python.md) per hello API DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-358">In addition toohello DocumentDB API for [Node.js](documentdb-sdk-node.md) client, Azure Cosmos DB has [.NET](documentdb-sdk-dotnet.md), [.NET Core](documentdb-sdk-dotnet-core.md), [Java](documentdb-sdk-java.md), [JavaScript](http://azure.github.io/azure-documentdb-js/), and [Python SDKs](documentdb-sdk-python.md) for hello DocumentDB API.</span></span> <span data-ttu-id="3ecd5-359">È possibile creare ed eseguire stored procedure, trigger e UDFs usando anche uno qualsiasi di questi SDK.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-359">Stored procedures, triggers and UDFs can be created and executed using any of these SDKs as well.</span></span> <span data-ttu-id="3ecd5-360">Hello seguente esempio viene illustrato come toocreate ed eseguire una stored procedure utilizzando client .NET hello.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-360">hello following example shows how toocreate and execute a stored procedure using hello .NET client.</span></span> <span data-ttu-id="3ecd5-361">Si noti come tipi .NET hello vengono passati in hello stored procedure come JSON e leggere nuovamente.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-361">Note how hello .NET types are passed into hello stored procedure as JSON and read back.</span></span>

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


<span data-ttu-id="3ecd5-362">Questo esempio viene illustrato come hello toouse [API .NET di DocumentDB](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet) toocreate pre-trigger e creare un documento con trigger hello abilitato.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-362">This sample shows how toouse hello [DocumentDB .NET API](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet) toocreate a pre-trigger and create a document with hello trigger enabled.</span></span> 

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


<span data-ttu-id="3ecd5-363">E hello di esempio seguente viene illustrato come toocreate un utente definito (dall'utente UDF) (funzione) e utilizzarla in un [query SQL API DocumentDB](documentdb-sql-query.md).</span><span class="sxs-lookup"><span data-stu-id="3ecd5-363">And hello following example shows how toocreate a user defined function (UDF) and use it in a [DocumentDB API SQL query](documentdb-sql-query.md).</span></span>

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

## <a name="rest-api"></a><span data-ttu-id="3ecd5-364">API REST</span><span class="sxs-lookup"><span data-stu-id="3ecd5-364">REST API</span></span>
<span data-ttu-id="3ecd5-365">Tutte le operazioni di Azure Cosmos DB possono essere eseguite in modalità RESTful.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-365">All Azure Cosmos DB operations can be performed in a RESTful manner.</span></span> <span data-ttu-id="3ecd5-366">È possibile registrare stored procedure, trigger e funzioni definite dall'utente in una raccolta usando il verbo HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-366">Stored procedures, triggers and user-defined functions can be registered under a collection by using HTTP POST.</span></span> <span data-ttu-id="3ecd5-367">Hello seguito è riportato un esempio di come tooregister una stored procedure:</span><span class="sxs-lookup"><span data-stu-id="3ecd5-367">hello following is an example of how tooregister a stored procedure:</span></span>

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


<span data-ttu-id="3ecd5-368">Hello stored procedure è registrata tramite l'esecuzione di una richiesta POST hello URI dbs/testdb/colls/testColl/stored procedure con hello corpo contenente hello toocreate stored procedure.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-368">hello stored procedure is registered by executing a POST request against hello URI dbs/testdb/colls/testColl/sprocs with hello body containing hello stored procedure toocreate.</span></span> <span data-ttu-id="3ecd5-369">Trigger e funzioni definite dall'utente possono essere registrati in modo analogo eseguendo una richiesta POST rispettivamente su /triggers e /udfs.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-369">Triggers and UDFs can be registered similarly by issuing a POST against /triggers and /udfs respectively.</span></span>
<span data-ttu-id="3ecd5-370">Questa stored procedure può quindi essere eseguita tramite una richiesta POST sul relativo collegamento alle risorse:</span><span class="sxs-lookup"><span data-stu-id="3ecd5-370">This stored procedure can then be executed by issuing a POST request against its resource link:</span></span>

    POST https://<url>/sprocs/<sproc> HTTP/1.1
    authorization: <<auth>>
    x-ms-date: Thu, 07 Aug 2014 03:43:20 GMT


    [ { "name": "TestDocument", "book": "Autumn of hello Patriarch"}, "Price", 200 ]


<span data-ttu-id="3ecd5-371">In questo caso, procedure toohello input archiviato hello viene passata nel corpo della richiesta hello.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-371">Here, hello input toohello stored procedure is passed in hello request body.</span></span> <span data-ttu-id="3ecd5-372">Si noti che hello input viene passato come matrice JSON dei parametri di input.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-372">Note that hello input is passed as a JSON array of input parameters.</span></span> <span data-ttu-id="3ecd5-373">Hello stored procedure accetta hello primo input di un documento che è un corpo della risposta.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-373">hello stored procedure takes hello first input as a document that is a response body.</span></span> <span data-ttu-id="3ecd5-374">è stata ricevuta risposta di Hello è indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="3ecd5-374">hello response we receive is as follows:</span></span>

    HTTP/1.1 200 OK

    { 
      name: 'TestDocument',
      book: ‘Autumn of hello Patriarch’,
      id: ‘V7tQANV3rAkDAAAAAAAAAA==‘,
      ts: 1407830727,
      self: ‘dbs/V7tQAA==/colls/V7tQANV3rAk=/docs/V7tQANV3rAkDAAAAAAAAAA==/’,
      etag: ‘6c006596-0000-0000-0000-53e9cac70000’,
      attachments: ‘attachments/’,
      Price: 200
    }


<span data-ttu-id="3ecd5-375">A differenza delle stored procedure, non è possibile eseguire direttamente i trigger,</span><span class="sxs-lookup"><span data-stu-id="3ecd5-375">Triggers, unlike stored procedures, cannot be executed directly.</span></span> <span data-ttu-id="3ecd5-376">che vengono però eseguiti come parte di un'operazione o di un documento.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-376">Instead they are executed as part of an operation on a document.</span></span> <span data-ttu-id="3ecd5-377">È possibile specificare hello trigger toorun con una richiesta utilizzando le intestazioni HTTP.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-377">We can specify hello triggers toorun with a request using HTTP headers.</span></span> <span data-ttu-id="3ecd5-378">di seguito Hello è richiesta toocreate un documento.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-378">hello following is request toocreate a document.</span></span>

    POST https://<url>/docs/ HTTP/1.1
    authorization: <<auth>>
    x-ms-date: Thu, 07 Aug 2014 03:43:10 GMT
    x-ms-documentdb-pre-trigger-include: validateDocumentContents 
    x-ms-documentdb-post-trigger-include: bookCreationPostTrigger


    {
       "name": "newDocument",
       “title”: “hello Wizard of Oz”,
       “author”: “Frank Baum”,
       “pages”: 92
    }


<span data-ttu-id="3ecd5-379">Qui toobe pre-trigger hello eseguire con richiesta di hello viene specificato nell'intestazione x-ms-documentdb-pre-trigger-include hello.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-379">Here hello pre-trigger toobe run with hello request is specified in hello x-ms-documentdb-pre-trigger-include header.</span></span> <span data-ttu-id="3ecd5-380">Di conseguenza, qualsiasi post-trigger figurano nell'intestazione x-ms-documentdb-post-trigger-include hello.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-380">Correspondingly, any post-triggers are given in hello x-ms-documentdb-post-trigger-include header.</span></span> <span data-ttu-id="3ecd5-381">Notare che è possibile specificare sia pre-trigger sia post-trigger per una determinata richiesta.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-381">Note that both pre- and post-triggers can be specified for a given request.</span></span>

## <a name="sample-code"></a><span data-ttu-id="3ecd5-382">Codice di esempio</span><span class="sxs-lookup"><span data-stu-id="3ecd5-382">Sample code</span></span>
<span data-ttu-id="3ecd5-383">Per trovare altri esempi di codice sul lato server, inclusi esempi relativi all'[eliminazione in blocco](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples/stored-procedures/bulkDelete.js) e all'[aggiornamento](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples/stored-procedures/update.js), vedere l'[archivio GitHub](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples).</span><span class="sxs-lookup"><span data-stu-id="3ecd5-383">You can find more server-side code examples (including [bulk-delete](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples/stored-procedures/bulkDelete.js), and [update](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples/stored-procedures/update.js)) on our [GitHub repository](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples).</span></span>

<span data-ttu-id="3ecd5-384">Desidera tooshare straordinaria stored procedure?</span><span class="sxs-lookup"><span data-stu-id="3ecd5-384">Want tooshare your awesome stored procedure?</span></span> <span data-ttu-id="3ecd5-385">Inviare una richiesta di pull!</span><span class="sxs-lookup"><span data-stu-id="3ecd5-385">Please, send us a pull-request!</span></span> 

## <a name="next-steps"></a><span data-ttu-id="3ecd5-386">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3ecd5-386">Next steps</span></span>
<span data-ttu-id="3ecd5-387">Dopo aver creato uno o più stored procedure, trigger e funzioni definite dall'utente create, è possibile caricarli e visualizzarli nel portale di Azure utilizzando Esplora dati hello.</span><span class="sxs-lookup"><span data-stu-id="3ecd5-387">Once you have one or more stored procedures, triggers, and user-defined functions created, you can load them and view them in hello Azure portal using Data Explorer.</span></span>

<span data-ttu-id="3ecd5-388">È inoltre possibile trovare il seguente hello riferimenti e risorse utili per il percorso toolearn ulteriori informazioni sulla programmazione sul lato server dB Cosmos Azure:</span><span class="sxs-lookup"><span data-stu-id="3ecd5-388">You may also find hello following references and resources useful in your path toolearn more about Azure Cosmos dB server-side programming:</span></span>

* [<span data-ttu-id="3ecd5-389">Azure Cosmos DB SDK</span><span class="sxs-lookup"><span data-stu-id="3ecd5-389">Azure Cosmos DB SDKs</span></span>](documentdb-sdk-dotnet.md)
* [<span data-ttu-id="3ecd5-390">DocumentDB Studio</span><span class="sxs-lookup"><span data-stu-id="3ecd5-390">DocumentDB Studio</span></span>](https://github.com/mingaliu/DocumentDBStudio/releases)
* [<span data-ttu-id="3ecd5-391">JSON</span><span class="sxs-lookup"><span data-stu-id="3ecd5-391">JSON</span></span>](http://www.json.org/) 
* [<span data-ttu-id="3ecd5-392">JavaScript ECMA-262</span><span class="sxs-lookup"><span data-stu-id="3ecd5-392">JavaScript ECMA-262</span></span>](http://www.ecma-international.org/publications/standards/Ecma-262.htm)
* [<span data-ttu-id="3ecd5-393">Estensibilità di Database protette e portatile</span><span class="sxs-lookup"><span data-stu-id="3ecd5-393">Secure and Portable Database Extensibility</span></span>](http://dl.acm.org/citation.cfm?id=276339) 
* [<span data-ttu-id="3ecd5-394">Database architettura orientata ai servizi</span><span class="sxs-lookup"><span data-stu-id="3ecd5-394">Service Oriented Database Architecture</span></span>](http://dl.acm.org/citation.cfm?id=1066267&coll=Portal&dl=GUIDE) 
* [<span data-ttu-id="3ecd5-395">Hosting hello .NET Runtime in Microsoft SQL server</span><span class="sxs-lookup"><span data-stu-id="3ecd5-395">Hosting hello .NET Runtime in Microsoft SQL server</span></span>](http://dl.acm.org/citation.cfm?id=1007669)

